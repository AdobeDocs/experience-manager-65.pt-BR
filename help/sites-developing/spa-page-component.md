---
title: Componente da página SPA
seo-title: Componente da página SPA
description: Em um SPA, o componente de página não fornece os elementos HTML de seus componentes filho, mas delega isso na estrutura SPA. Esse documento explica como isso torna o componente de página de um SPA único.
seo-description: Em um SPA, o componente de página não fornece os elementos HTML de seus componentes filho, mas delega isso na estrutura SPA. Esse documento explica como isso torna o componente de página de um SPA único.
uuid: d444527a-e883-4873-a55b-c2bc140d8d7f
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6329301c-1a26-4a46-99ae-1b7cc15b08be
docset: aem65
translation-type: tm+mt
source-git-commit: 14cc66dfef7bc7781907bdd6093732912c064579
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---


# Componente da página SPA{#spa-page-component}

Em um SPA, o componente de página não fornece os elementos HTML de seus componentes filho, mas delega isso na estrutura SPA. Esse documento explica como isso torna o componente de página de um SPA único.

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização do cliente baseada em SPA estrutura (por exemplo, Reagir ou Angular).

## Introdução {#introduction}

O componente de página de um SPA não fornece os elementos HTML de seus componentes filho por meio de um arquivo JSP ou HTL e objetos de recurso. Esta operação é delegada no quadro SPA. A representação dos componentes filhos é buscada como uma estrutura de dados JSON (ou seja, o modelo). Os componentes SPA são adicionados à página de acordo com o modelo JSON fornecido. Dessa forma, a composição inicial do corpo do componente da página difere de seus equivalentes HTML pré-renderizados.

## Gerenciamento do modelo de página {#page-model-management}

A resolução e o gerenciamento do modelo de página são delegados em um módulo [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) fornecido. O SPA deve interagir com o módulo `PageModelManager` ao inicializar para buscar o modelo de página inicial e registrar-se para atualizações de modelo - produzido principalmente quando o autor está editando a página pelo Editor de páginas. O `PageModelManager` pode ser acessado por SPA projeto como um pacote npm. Sendo um intérprete entre o AEM e o SPA, o `PageModelManager` deve acompanhar o SPA.

Para permitir a criação da página, uma biblioteca de cliente chamada `cq.authoring.pagemodel.messaging` deve ser adicionada para fornecer um canal de comunicação entre o SPA e o editor de página. Se o componente de página SPA herdar do componente wcm/core da página, então há as seguintes opções para disponibilizar a categoria de biblioteca do cliente `cq.authoring.pagemodel.messaging`:

* Se o modelo for editável, adicione a categoria da biblioteca do cliente à política de página.
* Adicione a categoria da biblioteca do cliente usando `customfooterlibs.html` do componente da página.

Não se esqueça de limitar a inclusão da categoria `cq.authoring.pagemodel.messaging` ao contexto do editor de páginas.

## Tipo de dados de comunicação {#communication-data-type}

O tipo de dados de comunicação é definido como um elemento HTML dentro do componente Página AEM usando o atributo `data-cq-datatype`. Quando o tipo de dados de comunicação é definido como JSON, as solicitações de GET atingem os pontos finais do Modelo Sling de um componente. Depois que uma atualização ocorre no editor de página, a representação JSON do componente atualizado é enviada para a biblioteca do Modelo de página. A biblioteca do Modelo de página avisa o SPA de atualizações.

**Componente da página SPA -`body.html`**

```
<div id="page"></div>
```

Além de ser uma boa prática não atrasar a geração do DOM, a estrutura do SPA exige que os scripts sejam adicionados ao final do corpo.

**Componente da página SPA -`customfooterlibs.html`**

```
<sly data-sly-use.clientLib="${'/libs/granite/sightly/templates/clientlib.html'}"></sly>
<sly data-sly-test="${wcmmode.edit || wcmmode.preview}"
     data-sly-call="${clientLib.js @ categories='cq.authoring.pagemodel.messaging'}"></sly>
<sly data-sly-call="${clientLib.js @ categories='we-retail-journal-react'}"></sly>
```

As propriedades do recurso meta que descrevem o conteúdo SPA:

**Componente da página SPA -`customheaderlibs.html`**

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
>O seletor de modelo padrão é definido estaticamente ao solicitar a representação do Modelo Sling de um componente.

## Propriedades Meta {#meta-properties}

* `cq:wcmmode`: Modo WCM dos editores (por exemplo, página, modelo)
* `cq:pagemodel_root_url`: URL do modelo raiz do aplicativo. É fundamental ao acessar diretamente uma página secundária, pois o modelo de página filho é um fragmento do modelo raiz do aplicativo. Em seguida, ` [PageModelManager](/help/sites-developing/spa-page-component.md)` recompõe sistematicamente o modelo inicial do aplicativo ao inserir o aplicativo a partir do ponto de entrada raiz.

* `cq:pagemodel_router`: Ativar ou desativar o  ` [ModelRouter](/help/sites-developing/spa-routing.md)` da  `PageModelManager` biblioteca

* `cq:pagemodel_route_filters`: Lista separada por vírgulas ou expressões regulares para fornecer rotas que  ` [ModelRouter](/help/sites-developing/spa-routing.md)` devem ser ignoradas.

>[!CAUTION]
>
>Este documento usa o aplicativo do Journal We.Retail apenas para fins de demonstração. Não deve ser utilizado para qualquer trabalho de projeto.
>
>Qualquer projeto AEM deve aproveitar o [AEM Project Archetype](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/developing/archetype/overview.html), que suporta projetos SPA usando React ou Angular e aproveita o SPA SDK. Todos os projetos SPA no AEM devem ter por base o Maven Archetype para SPA Starter Kit.

## Sincronização de sobreposição do editor de páginas {#page-editor-overlay-synchronization}

A sincronização das sobreposições é garantida pelo mesmo Observador de mutações fornecido pela categoria `cq.authoring.page`.

## Configuração da Estrutura Exportada JSON do Modelo Sling {#sling-model-json-exported-structure-configuration}

Quando os recursos do roteamento estiverem ativados, a suposição é que a exportação JSON do SPA contenha as diferentes rotas do aplicativo graças à exportação JSON do componente de navegação AEM. A saída JSON do componente de navegação AEM pode ser configurada na política de conteúdo da página raiz SPA por meio das duas propriedades a seguir:

* `structureDepth`: Número correspondente à profundidade da árvore exportada
* `structurePatterns`: Regex de matriz de regex correspondente à página a ser exportada

Isso pode ser mostrado no conteúdo de amostra SPA em `/conf/we-retail-journal/react/settings/wcm/policies/we-retail-journal/react/components/structure/page/root`.
