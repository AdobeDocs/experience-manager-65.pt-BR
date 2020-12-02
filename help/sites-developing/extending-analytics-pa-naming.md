---
title: Implementação de nomenclatura de página do lado do servidor para o Analytics
seo-title: Implementação de nomenclatura de página do lado do servidor para o Analytics
description: A Adobe Analytics usa a propriedade s.pageName para identificar exclusivamente páginas e associar os dados coletados para as páginas
seo-description: A Adobe Analytics usa a propriedade s.pageName para identificar exclusivamente páginas e associar os dados coletados para as páginas
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---


# Implementação de nomenclatura de página do lado do servidor para o Analytics{#implementing-server-side-page-naming-for-analytics}

A Adobe Analytics usa a propriedade `s.pageName` para identificar exclusivamente as páginas e associar os dados coletados para elas. Normalmente, você executa as seguintes tarefas em AEM para atribuir um valor a essa propriedade que AEM envia para o Analytics:

* Use a estrutura de serviço em nuvem do Analytics para mapear uma variável CQ para a propriedade `s.pageName` do Analytics. (Consulte [Mapeamento de dados de componente com propriedades do Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md).)

* Projete o componente da página para que ele inclua a variável CQ que você mapeia para a propriedade `s.pageName`. (Consulte [Implementação do rastreamento Adobe Analytics para componentes personalizados](/help/sites-developing/extending-analytics-components.md).)

Para expor os dados do relatório do Analytics no console Sites e no Content Insight, AEM requer o valor da propriedade `s.pageName` para cada página. A API Java do AEM Analytics define a interface `AnalyticsPageNameProvider` que você implementa para fornecer o console Sites e o Content Insights com o valor da propriedade `s.pageName`. Seu serviço `AnaltyicsPageNameProvider` resolve a propriedade pageName no servidor para fins de relatórios, pois pode ser definido dinamicamente usando o Javascript no cliente para fins de rastreamento.

## O serviço de provedor de nome de página padrão do Analytics {#the-default-analytics-page-name-provider-service}

O serviço `DefaultPageNameProvider` é o serviço padrão que determina o valor da propriedade `s.pageName` a ser usada para recuperar dados do Analytics de uma página. O serviço funciona em conjunto com o componente de página de base AEM ( `/libs/foundation/components/page`). Este componente de página define as seguintes variáveis CQ que devem ser mapeadas para a propriedade `s.pageName`:

* `pagedata.path`: O valor é definido como o caminho da página.
* `pagedata.title`: O valor é definido para o título da página.
* `pagedata.navTitle`: O valor é definido para o título de navegação da página.

O serviço `DefaultPageNameProvider` determina qual dessas variáveis CQ está mapeada para a propriedade `s.pageName` na estrutura do serviço em nuvem do Analytics. O serviço então determina a propriedade de página apropriada a ser usada para recuperar os dados do relatório de análise:

* `pagedata.path`: O serviço usa  `page.getPath()`

* `pagedata.title`: O serviço usa  `page.getTitle()`

* `pagedata.navTitle`: O serviço usa  `page.getNavigationTitle()`

O objeto `page` é o objeto Java [ `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) da página.

Se você não mapear uma variável CQ para a propriedade `s.pageName` na estrutura, o valor de `s.pageName` será gerado a partir do caminho da página. Por exemplo, a página com o caminho `/content/geometrixx/en` usa o valor `content:geometrixx:en` para `s.pageName`.

>[!NOTE]
>
>O serviço DefaultPageNameProvider usa uma classificação de serviço de 100.

## Manutenção da continuidade no Relatórios do Analytics {#maintaining-continuity-in-analytics-reporting}

A manutenção de um histórico completo de dados analíticos para uma página exige que o valor da propriedade s.pageName usada para uma página nunca seja alterado. No entanto, as propriedades de análise que o componente da página de base define podem ser facilmente alteradas. Por exemplo, mover uma página altera o valor de `pagedata.path` e quebra a continuidade do histórico de relatórios:

* Os dados coletados para o caminho anterior não estão mais associados à página.
* Se uma página diferente usar o caminho que outra página uma vez usou, a página diferente herdará os dados desse caminho.

Para garantir a continuidade do relatórios, o valor de `s.pageName` deve ter as seguintes características:

* Único.
* Estável.
* Leitura humana.

Por exemplo, um componente de página personalizado pode incluir uma propriedade de página que os autores usam para especificar uma ID exclusiva para a página que é usada como valor para a propriedade `s.pageProperties`:

* A página inclui uma variável do Analytics definida como o valor da ID exclusiva armazenada na propriedade da página.
* A variável analytics é mapeada para a propriedade `s.pageProperties` na estrutura do Analytics.
* Sua implementação da interface AnalyticsPageNameProvider recupera o valor da propriedade da página a ser usada para consultar os dados do Analytics da página.

>[!NOTE]
>
>Peça ajuda ao seu consultor do Analytics para desenvolver uma estratégia eficaz para seu `s.pageName` valor.

### Implementação de um serviço de provedor de nomes de página do Analytics {#implementing-an-analytics-page-name-provider-service}

Implemente a interface `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` como um serviço OSGi para personalizar a lógica que recupera o valor da propriedade `s.pageName`. A análise da página Sites e o Content Insight usam o serviço para recuperar dados de relatório do Analytics.

A interface AnalyticsPageNameProvider define dois métodos que devem ser implementados:

* `getPageName`: Retorna um  `String` valor que representa o valor a ser usado como a  `s.pageName` propriedade.

* `getResource`: Retorna um  `org.apache.sling.api.resource.Resource` objeto que representa a página associada à  `s.pageName` propriedade.

Ambos os métodos tomam um objeto `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` como parâmetro. A classe `AnalyticsPageNameContext` fornece informações sobre o contexto das chamadas de análise:

* O caminho base do recurso de página.
* O objeto `Framework` para a configuração do serviço de nuvem do Analytics.
* O objeto `Resource` da página.
* O objeto `ResourceResolver` da página.

A classe também fornece um setter para o nome da página.

### Exemplo de Implementação do AnalyticsPageNameProvider {#example-analyticspagenameprovider-implementation}

O exemplo a seguir `AnalyticsPageNameProvider` implementação suporta um componente de página personalizado:

* O componente estende o componente da página de base.
* A caixa de diálogo inclui um campo que os autores usam para especificar o valor da propriedade `s.pageName`.
* O valor da propriedade é armazenado na propriedade pageName do nó `jcr:content`das instâncias de página.
* A propriedade analytics que armazena a propriedade `s.pageName` é chamada `pagedata.pagename`. Essa propriedade é mapeada para a propriedade `s.pageName` na estrutura do Analytics.

A seguinte implementação do método `getPageName` retornará o valor da propriedade do nó pageName se o mapeamento da estrutura estiver configurado corretamente:

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

A seguinte implementação do método getResource retorna o objeto Resource para a página:

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

