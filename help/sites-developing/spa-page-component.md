---
title: Componente de página SPA
description: Em um SPA, o componente de página não fornece os elementos de HTML de seus componentes filhos, mas delega isso à estrutura do SPA. Este documento explica como isso torna o componente de página de um SPA exclusivo.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: 0e9e2350-67ef-45c3-991f-6c1cd98fe93d
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 6d961456e0e1f7a26121da9be493308a62c53e04
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 6%

---


# Componente de página SPA{#spa-page-component}

Em um SPA, o componente de página não fornece os elementos de HTML de seus componentes filhos, mas delega isso à estrutura do SPA. Este documento explica como isso torna o componente de página de um SPA exclusivo.

{{ue-over-spa}}

## Introdução {#introduction}

O componente de página de um SPA não fornece os elementos de HTML de seus componentes filhos por meio de um arquivo JSP ou HTL e objetos de recurso. Esta operação é delegada na estrutura de SPA. A representação de componentes secundários é buscada como uma estrutura de dados JSON (ou seja, o modelo). Os componentes do SPA são adicionados à página de acordo com o modelo JSON fornecido. Dessa forma, a composição do corpo inicial do componente de página difere de suas contrapartes de HTML pré-renderizadas.

## Gerenciamento do modelo de página {#page-model-management}

A resolução e o gerenciamento do modelo de página são delegados a um módulo [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) fornecido. O SPA deve interagir com o módulo `PageModelManager` quando ele é inicializado para buscar o modelo de página inicial e se registrar para atualizações de modelo - produzido principalmente quando o autor está editando a página por meio do Editor de páginas. O `PageModelManager` pode ser acessado pelo projeto SPA como um pacote npm. Por ser um intérprete entre AEM e SPA, o `PageModelManager` deve acompanhar o SPA.

Para permitir que a página seja criada, uma biblioteca do cliente chamada `cq.authoring.pagemodel.messaging` deve ser adicionada para fornecer um canal de comunicação entre o SPA e o editor de páginas. Se o componente da página SPA herdar do componente wcm/core da página, as seguintes opções estarão disponíveis para tornar a categoria da biblioteca cliente `cq.authoring.pagemodel.messaging`:

* Se o modelo for editável, adicione a categoria da biblioteca do cliente à política da página.
* Adicione a categoria da biblioteca do cliente usando o `customfooterlibs.html` do componente de página.

Não se esqueça de limitar a inclusão da categoria `cq.authoring.pagemodel.messaging` ao contexto do editor de páginas.

## Tipo de dados da comunicação {#communication-data-type}

O tipo de dados de comunicação é definido como um elemento HTML dentro do componente Página AEM usando o atributo `data-cq-datatype`. Quando o tipo de dados de comunicação é definido como JSON, as solicitações do GET atingem os pontos de extremidade do Modelo Sling de um componente. Depois que uma atualização ocorre no editor de páginas, a representação JSON do componente atualizado é enviada para a biblioteca do Modelo de página. A biblioteca Modelo de página avisa o SPA sobre atualizações.

Componente de página do **SPA -`body.html`**

```
<div id="page"></div>
```

Além de ser uma boa prática para não atrasar a geração de DOM, a estrutura SPA requer que os scripts sejam adicionados ao final do corpo.

**Componente de página do SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

As propriedades do meta recursos que descrevem o conteúdo SPA:

Componente de página do **SPA -`customheaderlibs.html`**

```
<meta property="cq:datatype" data-sly-test="${wcmmode.edit || wcmmode.preview}" content="JSON"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.edit}" content="edit"/>
<meta property="cq:wcmmode" data-sly-test="${wcmmode.preview}" content="preview"/>
<meta property="cq:pagemodel_root_url" data-sly-use.page="com.adobe.cq.sample.spa.journal.models.AppPage" content="${page.rootUrl}"/>
<sly data-sly-use.clientlib="/libs/granite/sightly/templates/clientlib.html">
    <sly data-sly-call="${clientlib.css @ categories='we-retail-journal-react'}"/>
</sly>
```

>[!NOTE]
>
>O seletor de modelo padrão é definido estaticamente ao solicitar a representação do Modelo do Sling de um componente.

## Propriedades Meta {#meta-properties}

* `cq:wcmmode`: Modo WCM dos editores (por exemplo, página, modelo)
* `cq:pagemodel_root_url`: URL do modelo raiz do Aplicativo. Fundamental ao acessar diretamente uma página secundária, pois o modelo de página secundária é um fragmento do modelo raiz do aplicativo. O ` [PageModelManager](/help/sites-developing/spa-page-component.md)` então recompõe sistematicamente o modelo inicial do aplicativo como entrada no aplicativo a partir de seu ponto de entrada raiz.

* `cq:pagemodel_router`: Habilitar ou desabilitar o ` [ModelRouter](/help/sites-developing/spa-routing.md)` da biblioteca `PageModelManager`

* `cq:pagemodel_route_filters`: lista separada por vírgulas ou expressões regulares para fornecer rotas que ` [ModelRouter](/help/sites-developing/spa-routing.md)` deve ignorar.

>[!CAUTION]
>
>Este documento usa o aplicativo We.Retail Journal somente para fins de demonstração. Não use para nenhum trabalho de projeto.
>
>Qualquer projeto AEM deve usar o [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR), que oferece suporte a projetos SPA usando o React ou o Angular SPA SDK SPA AEM SPA e usa o.Todos os projetos no devem ser baseados no Arquétipo Maven para o Kit Inicial.

## Sincronização de sobreposição do editor de páginas {#page-editor-overlay-synchronization}

A sincronização das sobreposições é garantida pelo mesmo Mutation Observer fornecido pela categoria `cq.authoring.page`.

## Configuração da estrutura exportada JSON do modelo Sling {#sling-model-json-exported-structure-configuration}

Quando os recursos de roteamento estão ativados, presume-se que a exportação em JSON do SPA contenha as diferentes rotas do aplicativo graças à exportação em JSON do componente de navegação AEM. A saída JSON do componente de navegação do AEM pode ser configurada na política de conteúdo da página raiz do SPA por meio das duas propriedades a seguir:

* `structureDepth`: Número correspondente à profundidade da árvore exportada
* `structurePatterns`: Regex da matriz de regexes correspondentes à página a ser exportada

Isso pode ser mostrado no conteúdo da amostra do SPA em `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
