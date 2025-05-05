---
title: Estender o rastreamento de eventos
description: O AEM Analytics permite rastrear a interação do usuário no seu site
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Developer
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Estender o rastreamento de eventos{#extending-event-tracking}

O AEM Analytics permite rastrear a interação do usuário no seu site. Como desenvolvedor, talvez seja necessário:

* Rastreie como os visitantes estão interagindo com seus componentes. Isso pode ser feito com [Eventos personalizados.](#custom-events)
* [Acesse valores no ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [Adicionar retornos de chamada de registro](#adding-record-callbacks).

>[!NOTE]
>
>Esta informação é basicamente genérica, mas usa [Adobe Analytics](/help/sites-administering/adobeanalytics.md) para exemplos específicos.
>
>Para obter informações gerais sobre o desenvolvimento de componentes e caixas de diálogo, consulte [Desenvolvimento de Componentes](/help/sites-developing/components.md).

## Eventos personalizados {#custom-events}

Os eventos personalizados rastreiam tudo o que depende da disponibilidade de um componente específico na página. Isso também inclui eventos específicos do modelo, pois o componente da página é tratado como outro componente.

### Rastreamento De Eventos Personalizados No Carregamento Da Página {#tracking-custom-events-on-page-load}

Isso pode ser feito usando o pseudoatributo `data-tracking` (o atributo de registro mais antigo ainda é compatível com versões anteriores). Você pode adicioná-lo a qualquer tag HTML.

A sintaxe para `data-tracking` é

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

Você pode passar qualquer número de pares de valor-chave como o segundo parâmetro, que é chamado de carga.

Um exemplo pode se parecer com:

```xml
<span data-tracking="{event:'blogEntryView',
                                values:{
                                   'blogEntryContentType': 'blog',
                                   'blogEntryUniqueID': '<%= xssAPI.encodeForJSString(entry.getId()) %>',
                                   'blogEntryTitle': '<%= xssAPI.encodeForJSString(entry.getTitle()) %>',
                                   'blogEntryAuthor':'<%= xssAPI.encodeForJSString(entry.getAuthor()) %>',
                                   'blogEntryPageLanguage':'<%= currentPage.getLanguage(true) %>'
                                },
                                componentPath:'myapp/component/mycomponent'}">
</span>
```

No carregamento da página, todos os atributos `data-tracking` serão coletados e adicionados ao armazenamento de eventos do ContextHub, onde podem ser mapeados para eventos do Adobe Analytics. Eventos que não estão mapeados não serão rastreados pelo Adobe Analytics. Consulte [Conectando-se ao Adobe Analytics](/help/sites-administering/adobeanalytics.md) para obter mais detalhes sobre como mapear eventos.

### Rastreamento de eventos personalizados após o carregamento da página {#tracking-custom-events-after-page-load}

Para rastrear eventos que ocorrem depois que uma página é carregada (como interações de usuário), use a função JavaScript `CQ_Analytics.record`:

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Onde

* `events` é uma cadeia ou uma matriz de cadeia de caracteres (para vários eventos).

* `values` contém todos os valores a serem rastreados
* `collect` é opcional e retornará uma matriz contendo o evento e o objeto de dados.
* `options` é opcional e contém opções de rastreamento de link como HTML elemento `obj` e ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` é um atributo necessário e é recomendável defini-lo como `<%=resource.getResourceType()%>`

Por exemplo, com a seguinte definição, um usuário que clicar no link **Ir para o início** fará com que os dois eventos, `jumptop` e `headlineclick`, sejam acionados:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Acesso a valores no ContextHub {#accessing-values-in-the-contexthub}

A API JavaScript do ContextHub tem uma função `getStore(name)` que retorna o armazenamento especificado, se disponível. O armazenamento tem uma função `getItem(key)` que retorna o valor da chave especificada, se disponível. Usando a função `getKeys()`, é possível recuperar uma matriz de chaves definidas para o armazenamento específico.

Você pode ser notificado sobre alterações de valor em um armazenamento associando uma função com a função `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`.

A melhor maneira de ser notificado da disponibilidade inicial do ContextHub é usar a função `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`.

**Eventos adicionais para ContextHub:**

Todas as lojas prontas:

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Específico da loja:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Consulte também a [Referência da API do ContextHub](https://helpx.adobe.com/br/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference) completa

## Adição de retornos de chamada de registro {#adding-record-callbacks}

Antes e depois dos retornos de chamada serem registrados usando as funções `CQ_Analytics.registerBeforeCallback(callback,rank)` e `CQ_Analytics.registerAfterCallback(callback,rank)`.

Ambas as funções assumem uma função como o primeiro argumento e uma classificação como o segundo argumento, que determina a ordem em que os retornos de chamada são executados.

Se o retorno de chamada retornar false, os retornos de chamada seguintes na cadeia de execução não serão executados.
