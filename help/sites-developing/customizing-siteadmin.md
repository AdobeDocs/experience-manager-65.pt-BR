---
title: Personalização do console Sites (interface clássica)
seo-title: Customizing the Websites Console (Classic UI)
description: O console Administração de Sites pode ser estendido para exibir colunas personalizadas
seo-description: The Websites Administration console can be extended to display custom columns
uuid: 9163fdff-5351-477d-b91c-8a74f8b41d34
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: aeb37103-541d-4235-8a78-980b78c8de66
docset: aem65
exl-id: 2b9b4857-821c-4f2f-9ed9-78a1c9f5ac67
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# Personalização do console Sites (interface clássica){#customizing-the-websites-console-classic-ui}

## Adicionar uma coluna personalizada ao console Sites (siteadmin) {#adding-a-custom-column-to-the-websites-siteadmin-console}

O console Administração de sites pode ser estendido para exibir colunas personalizadas. O console é criado com base em um objeto JSON que pode ser estendido pela criação de um serviço OSGI que implementa o `ListInfoProvider` interface. Esse serviço modifica o objeto JSON enviado ao cliente para criar o console.

Este tutorial passo a passo explica como exibir uma nova coluna no console Administração de sites, implementando o `ListInfoProvider` interface. Ele consiste nas seguintes etapas:

1. [Criação do serviço OSGI](#creating-the-osgi-service) e implantar o pacote que o contém no servidor AEM.
1. (opcional) [Teste do novo serviço](#testing-the-new-service) emitindo uma chamada JSON para solicitar o objeto JSON usado para criar o console.
1. [Exibição da nova coluna](#displaying-the-new-column) estendendo a estrutura dos nós do console no repositório.

>[!NOTE]
>
>Este tutorial também pode ser usado para estender os seguintes consoles de administração:
>
>* o console Ativos digitais
>* o console Comunidade
>


### Criação do serviço OSGI {#creating-the-osgi-service}

O `ListInfoProvider` a interface define dois métodos:

* `updateListGlobalInfo`, para atualizar as propriedades globais da lista,
* `updateListItemInfo`, para atualizar um item de lista única.

Os argumentos para ambos os métodos são:

* `request`, o objeto de solicitação Sling HTTP associado,
* `info`, o objeto JSON a ser atualizado, que é respectivamente a lista global ou o item de lista atual,
* `resource`, um recurso Sling.

O exemplo de implementação abaixo:

* Adiciona um *estrelado* propriedade de cada item, que é `true` se o nome da página começar com um *e* e `false` caso contrário.

* Adiciona um *starredCount* , que é global para a lista e contém o número de itens da lista.

Para criar o serviço OSGI:

1. Em CRXDE Lite, [criar um pacote](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. Adicione o código de amostra abaixo.
1. Crie o pacote.

O novo serviço está em execução.

```java
package com.test;

import com.day.cq.commons.ListInfoProvider;
import com.day.cq.i18n.I18n;
import com.day.cq.wcm.api.Page;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;

@Component(metatype = false)
@Service(value = ListInfoProvider.class)
public class StarredListInfoProvider implements ListInfoProvider {

    private int count = 0;

    public void updateListGlobalInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        info.put("starredCount", count);
        count = 0; // reset for next execution
    }

    public void updateListItemInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        Page page = resource.adaptTo(Page.class);
        if (page != null) {
            // Consider starred if page name starts with 'e'
            boolean starred = page.getName().startsWith("e");
            if (starred) {
                count++;
            }
            I18n i18n = new I18n(request);
            info.put("starred", starred ? i18n.get("Yes") : i18n.get("No"));
        }
    }

}
```

>[!CAUTION]
>
>* Sua implementação deve decidir, com base na solicitação e/ou no recurso fornecido, se ela deve ou não adicionar as informações ao objeto JSON.
>* Se o seu `ListInfoProvider` implementação define uma propriedade que já existe no objeto de resposta, seu valor será substituído pelo que você fornecer.
>
>  Você pode usar [classificação de serviço](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) para gerenciar a ordem de execução de vários `ListInfoProvider` implementações.

### Testando o novo serviço {#testing-the-new-service}

Ao abrir o console de administração de sites e navegar pelo site, o navegador emite uma chamada ajax para obter o objeto JSON usado para criar o console. Por exemplo, quando você navega para a variável `/content/geometrixx` , a seguinte solicitação é enviada ao servidor de AEM para criar o console:

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

Para garantir que o novo serviço esteja em execução após a implantação do pacote que o contém:

1. Aponte seu navegador para o seguinte URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. A resposta deve exibir as novas propriedades da seguinte maneira:

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### Exibição da nova coluna {#displaying-the-new-column}

A última etapa consiste em adaptar a estrutura dos nós do console de administração de sites para exibir a nova propriedade de todas as páginas do Geometrixx ao sobrepor `/libs/wcm/core/content/siteadmin`. Proceda do seguinte modo:

1. No CRXDE Lite, crie a estrutura dos nós `/apps/wcm/core/content` com nós do tipo `sling:Folder` para refletir a estrutura `/libs/wcm/core/content`.

1. Copie o nó `/libs/wcm/core/content/siteadmin` e cole-o abaixo `/apps/wcm/core/content`.

1. Copie o nó `/apps/wcm/core/content/siteadmin/grid/assets` para `/apps/wcm/core/content/siteadmin/grid/geometrixx` e altera suas propriedades:

   * Remover **pageText**

   * Definir **pathRegex** para `/content/geometrixx(/.*)?`
Isso tornará a configuração da grade ativa para todos os sites geometrixx.

   * Definir **storeProxySuffix** para `.pages.json`

   * Edite o **storeReaderFields** propriedade com vários valores e adicione o `starred` valor.

   * Para ativar a funcionalidade MSM, adicione os seguintes parâmetros MSM à propriedade multi-String **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. Adicione um `starred` nó (do tipo **nt:unstructured**) abaixo `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` com as seguintes propriedades:

   * **dataIndex**: `starred` do tipo String

   * **header**: `Starred` do tipo String

   * **xtype**: `gridcolumn` do tipo String

1. (opcional) Solte as colunas que você não deseja exibir em `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` é um caminho personalizado que, como padrão, aponta para `/libs/wcm/core/content/siteadmin`.
Para redirecionar isso para sua versão do siteadmin em `/apps/wcm/core/content/siteadmin` definir a propriedade `sling:vanityOrder` para ter um valor maior que o definido em `/libs/wcm/core/content/siteadmin`. O valor padrão é 300, portanto, qualquer valor maior é adequado.

1. Vá para o console de administração de sites e navegue até o site do Geometrixx:
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. A nova coluna chamada **Started** estiver disponível, exibindo informações personalizadas da seguinte maneira:

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>Se várias configurações de grade corresponderem ao caminho solicitado definido pela variável **pathRegex** , o primeiro será usado, e não o mais específico, o que significa que a ordem das configurações é importante.

### Pacote de exemplo {#sample-package}

O resultado deste tutorial está disponível na seção [Personalização do console de administração de sites](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) no Compartilhamento de pacotes.
