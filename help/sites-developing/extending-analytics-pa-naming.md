---
title: Implementação da nomenclatura de página do lado do servidor para o Analytics
seo-title: Implementing Server-Side Page Naming for Analytics
description: O Adobe Analytics usa a propriedade s.pageName para identificar páginas de maneira exclusiva e associar os dados coletados para as páginas
seo-description: Adobe Analytics uses the s.pageName property to uniquely identify pages and to associate the data that is collected for the pages
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 0%

---

# Implementação da nomenclatura de página do lado do servidor para o Analytics{#implementing-server-side-page-naming-for-analytics}

O Adobe Analytics usa o `s.pageName` para identificar de forma exclusiva as páginas e associar os dados coletados para elas. Normalmente, você executa as seguintes tarefas no AEM para atribuir um valor a essa propriedade que o AEM envia para o Analytics:

* Usar a estrutura do Analytics Cloud Service para mapear uma variável do CQ para o Analytics `s.pageName` propriedade. (Consulte [Mapeamento de dados do componente com propriedades do Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md).)

* Crie o componente de página para que ele inclua a variável CQ que você mapeia para a `s.pageName` propriedade. (Consulte [Implementação do Adobe Analytics Tracking para componentes personalizados](/help/sites-developing/extending-analytics-components.md).)

Para expor os dados de relatório do Analytics no console Sites e no Content Insight, o AEM requer o valor de `s.pageName` para cada página. A API Java do AEM Analytics define o `AnalyticsPageNameProvider` que você implementa para fornecer ao console Sites e aos Insights de conteúdo o valor da variável `s.pageName` propriedade. Seu `AnaltyicsPageNameProvider` O serviço resolve a propriedade pageName no servidor para fins de relatório, pois ela pode ser definida dinamicamente usando JavaScript no cliente para fins de rastreamento.

## O Serviço do provedor de nome de página padrão do Analytics {#the-default-analytics-page-name-provider-service}

A variável `DefaultPageNameProvider` serviço é o serviço padrão que determina o valor da variável `s.pageName` propriedade a ser usada para recuperar dados do Analytics de uma página. O serviço funciona em conjunto com o componente de página de base AEM ( `/libs/foundation/components/page`). Esse componente de página define as seguintes variáveis do CQ que devem ser mapeadas para o `s.pageName` propriedade:

* `pagedata.path`: O valor é definido para o caminho da página.
* `pagedata.title`: o valor é definido como o título da página.
* `pagedata.navTitle`: O valor é definido como o título da navegação da página.

A variável `DefaultPageNameProvider` serviço determina qual dessas variáveis do CQ é mapeada para a variável `s.pageName` propriedade na estrutura do Analytics Cloud Service. O serviço determina a propriedade de página apropriada a ser usada para recuperar dados de relatório de análise:

* `pagedata.path`: O serviço usa `page.getPath()`

* `pagedata.title`: O serviço usa `page.getTitle()`

* `pagedata.navTitle`: O serviço usa `page.getNavigationTitle()`

A variável `page` objeto é o é o [`com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Objeto Java da página.

Se você não mapear uma variável do CQ para o `s.pageName` no framework, o valor para `s.pageName` é gerado pelo caminho da página. Por exemplo, a página com o caminho `/content/geometrixx/en` usa o valor `content:geometrixx:en` para `s.pageName`.

>[!NOTE]
>
>O serviço DefaultPageNameProvider usa 100 classificações de serviço.

## Manutenção da continuidade nos relatórios do Analytics {#maintaining-continuity-in-analytics-reporting}

Para manter um histórico completo dos dados de análise de uma página, é necessário que o valor da propriedade s.pageName usada para uma página nunca seja alterado. No entanto, as propriedades de análise que o componente de página de base define podem ser facilmente alteradas. Por exemplo, mover uma página altera o valor de `pagedata.path` e interrompe a continuidade do histórico de relatórios:

* Os dados coletados para o caminho anterior não estão mais associados à página.
* Se uma página diferente usar o caminho que outra página usou uma vez, a página diferente herdará os dados desse caminho.

Para garantir a continuidade dos relatórios, o valor `s.pageName` deve ter as seguintes características:

* Único.
* Estável.
* Legível.

Por exemplo, um componente de página personalizado pode incluir uma propriedade de página que os autores usam para especificar uma ID exclusiva para a página, usada como o valor da `s.pageProperties` propriedade:

* A página inclui uma variável de análise definida como o valor da ID exclusiva armazenada na propriedade da página.
* A variável do Analytics é mapeada para a variável `s.pageProperties` propriedade no framework do Analytics.
* A implementação da interface AnalyticsPageNameProvider recupera o valor da propriedade de página a ser usada para consultar os dados de análise da página.

>[!NOTE]
>
>Peça ajuda ao seu consultor do Analytics para desenvolver uma estratégia eficaz para o seu `s.pageName` valor.

### Implementação de um serviço de provedor de nome de página do Analytics {#implementing-an-analytics-page-name-provider-service}

Implementar o `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` como um serviço OSGi para personalizar a lógica que recupera a variável `s.pageName` valor da propriedade. A análise de página do Sites e o Content Insight usam o serviço para recuperar dados de relatório do Analytics.

A interface do AnalyticsPageNameProvider define dois métodos que devem ser implementados:

* `getPageName`: retorna um `String` que representa o valor a ser usado como `s.pageName` propriedade.

* `getResource`: retorna um `org.apache.sling.api.resource.Resource` objeto que representa a página associada à `s.pageName` propriedade.

Ambos os métodos têm um `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` objeto como parâmetro. A variável `AnalyticsPageNameContext` A classe fornece informações sobre o contexto das chamadas de análise:

* O caminho base do recurso de página.
* A variável `Framework` para a configuração do Analytics Cloud Service.
* A variável `Resource` para a página.
* A variável `ResourceResolver` para a página.

A classe também fornece um setter para o nome da página.

### Exemplo de implementação de AnalyticsPageNameProvider {#example-analyticspagenameprovider-implementation}

O exemplo a seguir `AnalyticsPageNameProvider` A implementação do é compatível com um componente de página personalizado:

* O componente estende o componente de página de base.
* A caixa de diálogo inclui um campo que os autores usam para especificar o valor do `s.pageName` propriedade.
* O valor da propriedade é armazenado na propriedade pageName do `jcr:content`nó das instâncias de página.
* A propriedade do Analytics que armazena a variável `s.pageName` a propriedade é chamada `pagedata.pagename`. Essa propriedade é mapeada para o `s.pageName` propriedade no framework do Analytics.

A seguinte aplicação do `getPageName` O método retornará o valor da propriedade do nó pageName se o mapeamento da estrutura estiver configurado corretamente:

```java
public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.pagename")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }
```

A seguinte implementação do método getResource retorna o objeto Resource da página:

```java
     public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
             Iterator<Resource>
             hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
             if (hits.hasNext()) {
              res = hits.next();
              res = res.getParent();
             }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
```

O código a seguir representa a classe inteira, incluindo anotações SCR que configuram o serviço. Observe que a classificação de serviço é 200, o que substitui o serviço padrão.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2019 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.day.cq.analytics.sitecatalyst;

import java.util.Iterator;

import javax.jcr.query.Query;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;

import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext;
import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider;
import com.day.cq.analytics.sitecatalyst.Framework;
import com.day.cq.wcm.api.Page;

import static com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext.S_PAGE_NAME;

/**
 * Default implementation of {@link AnalyticsPageNameProvider} that resolves
 * page title, path or navTitle if mapped in {@link Framework}.
 */
@Component(
    service = { AnalyticsPageNameProvider.class },
    property = {
        Constants.SERVICE_DESCRIPTION + "=Example Page Name Resolver implementation",
        Constants.SERVICE_RANKING + ":Integer=200"
    }
)
public class ExamplePageNameProvider implements AnalyticsPageNameProvider {
    public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.path")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }

    public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
                Iterator<Resource>
                hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
                if (hits.hasNext()) {
                    res = hits.next();
                    res = res.getParent();
                }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
}
```
