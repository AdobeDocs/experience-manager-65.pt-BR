---
title: Personalização dos consoles
seo-title: Personalização dos consoles
description: AEM fornece vários mecanismos para permitir que você personalize os consoles da sua instância de criação
seo-description: AEM fornece vários mecanismos para permitir que você personalize os consoles da sua instância de criação
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---


# Personalização dos consoles {#customizing-the-consoles}

>[!CAUTION]
>
>Este documento descreve como personalizar consoles na interface moderna e habilitada para toque e não se aplica à interface clássica.

AEM fornece vários mecanismos para permitir que você personalize os consoles (e a [funcionalidade de criação de página](/help/sites-developing/customizing-page-authoring-touch.md)) da sua instância de criação.

* Clientlibs
Clientlibs permitem estender a implementação padrão para obter novas funcionalidades, reutilizando funções, objetos e métodos padrão. Ao personalizar, você pode criar sua própria clientlib em `/apps.` Por exemplo, ela pode conter o código necessário para seu componente personalizado.

* Sobreposições
As sobreposições são baseadas em definições de nó e permitem que você sobreponha a funcionalidade padrão (em `/libs`) com sua própria funcionalidade personalizada (em `/apps`). Ao criar uma sobreposição, uma cópia 1:1 do original não é necessária, já que a fusão de recursos sling permite herança.

Eles podem ser usados de várias maneiras para estender seus consoles de AEM. Uma pequena seleção é abordada abaixo (em um nível alto).

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* Usar e criar [clientlibs](/help/sites-developing/clientlibs.md).
>* Usar e criar [sobreposições](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>
>
Este tópico também é abordado na sessão [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html) - [Personalização da interface do usuário para AEM 6.0](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html).

>[!CAUTION]
>
>Você ***deve*** não alterar nada no caminho `/libs`.
>
>Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode muito bem ser substituído quando você aplicar uma correção ou um pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recrie o item necessário (isto é, como ele existe em `/libs`) em `/apps`
   >
   >
1. Faça quaisquer alterações em `/apps`

>



Por exemplo, o seguinte local na estrutura `/libs` pode ser sobreposto:

* consoles (quaisquer consoles com base nas páginas da interface do usuário do Granite); por exemplo:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Consulte o artigo da Base de conhecimento, [Resolução de problemas AEM problemas da interface do usuário do toque](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html), para obter mais dicas e ferramentas.

## Personalização da Visualização padrão para um console {#customizing-the-default-view-for-a-console}

Você pode personalizar a visualização padrão (coluna, cartão, lista) para um console:

1. É possível reordenar as visualizações sobrepondo a entrada necessária de abaixo:

   `/libs/wcm/core/content/sites/jcr:content/views`

   A primeira entrada será o padrão.

   Os nós disponíveis correlacionam-se às opções de visualização disponíveis:

   * `column`
   * `card`
   * `list`

1. Por exemplo, em uma sobreposição para lista:

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   Defina a seguinte propriedade:

   * **Nome**: `sling:orderBefore`
   * **Tipo**: `String`
   * **Valor**:  `column`

### Adicionar nova ação à barra de ferramentas {#add-new-action-to-the-toolbar}

1. Você pode criar seus próprios componentes e incluir as bibliotecas do cliente correspondentes para ações personalizadas. Por exemplo, uma ação **Promover ao Twitter** em:

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   Isso pode ser conectado a um item da barra de ferramentas no console:

   `/apps/<yourProject>/admin/ext/launches`

   Por exemplo, no modo de seleção:

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Restringir uma ação da barra de ferramentas a um grupo específico {#restrict-a-toolbar-action-to-a-specific-group}

1. É possível usar uma condição de renderização personalizada para sobrepor a ação padrão e impor condições específicas que devem ser cumpridas antes de ser renderizada.

   Por exemplo, crie um componente para controlar as condições de renderização de acordo com o grupo:

   `/apps/myapp/components/renderconditions/group`

1. Para aplicá-los à ação Criar site no console Sites:

   `/libs/wcm/core/content/sites`

   Crie a sobreposição:

   `/apps/wcm/core/content/sites`

1. Em seguida, adicione a condição de renderização para a ação:

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   Usando as propriedades neste nó, é possível definir `groups` permitido para executar a ação específica; por exemplo, `administrators`

### Personalização de colunas na Visualização da Lista {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Esse recurso é otimizado para colunas de campos de texto; para outros tipos de dados, é possível sobrepor `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` em `/apps`.

Para personalizar as colunas na visualização da lista:

1. Sobreponha a lista das colunas disponíveis.

   * No nó:

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * Adicione suas novas colunas ou remova as existentes.
   Consulte [Usando Sobreposições (e a Fusão de Recursos Sling)](/help/sites-developing/overlays.md) para obter mais informações.

1. Opcionalmente:

   * Se desejar conectar dados adicionais, você precisa gravar um [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) com um
      `pageInfoProviderType` propriedade.

   Por exemplo, consulte a classe/grupo anexado (do GitHub) abaixo.

1. Agora é possível selecionar a coluna no configurador de coluna da visualização de lista.

### Filtrar recursos {#filtering-resources}

Ao usar um console, um caso de uso comum é quando o usuário deve selecionar entre os recursos (por exemplo, páginas, componentes, ativos etc.). Isso pode assumir a forma de uma lista, por exemplo, a partir da qual o autor deve escolher um item.

Para manter a lista em um tamanho razoável e também relevante para o caso de uso, um filtro pode ser implementado na forma de um predicado personalizado. Consulte [este artigo](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) para obter detalhes.
