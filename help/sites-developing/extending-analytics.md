---
title: Extensão do rastreamento de Eventos
seo-title: Extensão do rastreamento de Eventos
description: O AEM Analytics permite rastrear a interação do usuário em seu site
seo-description: O AEM Analytics permite rastrear a interação do usuário em seu site
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---


# Extensão do rastreamento de Eventos{#extending-event-tracking}

O AEM Analytics permite que você rastreie a interação do usuário em seu site. Como desenvolvedor, talvez seja necessário:

* Acompanhe como os visitantes estão interagindo com seus componentes. Isso pode ser feito com [eventos personalizados.](#custom-events)
* [Acesse valores no ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [Adicionar retornos de chamada](#adding-record-callbacks) de registro.

>[!NOTE]
>
>Essas informações são basicamente genéricas, mas usam [Adobe Analytics](/help/sites-administering/adobeanalytics.md) para exemplos específicos.
>
>Para obter informações gerais sobre o desenvolvimento de componentes e caixas de diálogo, consulte [Desenvolvimento de componentes](/help/sites-developing/components.md).

## Eventos personalizados {#custom-events}

Os eventos personalizados rastreiam qualquer coisa que dependa da disponibilidade de um componente específico na página. Isso também inclui eventos específicos do modelo, já que o componente da página é tratado como outro componente.

### Rastreamento de Eventos personalizados no carregamento da página {#tracking-custom-events-on-page-load}

Isso pode ser feito usando o pseudo-atributo `data-tracking` (o atributo de registro mais antigo ainda é suportado para compatibilidade com versões anteriores). É possível adicionar isso a qualquer tag HTML.

A sintaxe para `data-tracking` é

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

Você pode passar qualquer número de pares de valores chave como o segundo parâmetro, que é chamado de carga.

Um exemplo pode ser semelhante a:

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

No carregamento da página, todos os atributos `data-tracking` serão coletados e adicionados ao armazenamento de eventos do ContextHub, onde podem ser mapeados para eventos Adobe Analytics. Eventos que não estão mapeados não serão rastreados pelo Adobe Analytics. Consulte [Ligar ao Adobe Analytics](/help/sites-administering/adobeanalytics.md) para obter mais detalhes sobre o mapeamento de eventos.

### Rastreamento de Eventos personalizados após o carregamento da página {#tracking-custom-events-after-page-load}

Para rastrear eventos que ocorrem depois que uma página é carregada (como interações de usuário), use a função `CQ_Analytics.record` JavaScript:

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Where

* `events` é uma string ou uma matriz de string (para vários eventos).

* `values` contém todos os valores a serem rastreados
* `collect` é opcional e retornará uma matriz contendo o evento e o objeto de dados.
* `options` é opcional e contém opções de rastreamento de link, como elemento HTML  `obj` e  ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` é um atributo necessário e é recomendável defini-lo como  `<%=resource.getResourceType()%>`

Por exemplo, com a seguinte definição, um usuário que clica no link **Ir para o início** fará com que os dois eventos, `jumptop` e `headlineclick`, sejam disparados:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Acessar valores no ContextHub {#accessing-values-in-the-contexthub}

A API JavaScript do ContextHub tem uma função `getStore(name)` que retorna o armazenamento especificado, se disponível. O armazenamento tem uma função `getItem(key)` que retorna o valor da chave especificada, se disponível. Usando a função `getKeys()` é possível recuperar uma matriz de chaves definidas para o armazenamento específico.

Você pode ser notificado sobre alterações de valor em uma loja vinculando uma função usando a função `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)`.

A melhor maneira de ser notificado sobre a disponibilidade inicial do ContextHub é usar a função `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`.

**Eventos adicionais para o ContextHub:**

Todas as lojas prontas:

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Específico da loja:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Consulte também a [Referência completa da API do ContextHub](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## Adicionando Retornos de chamada de registro {#adding-record-callbacks}

Antes e depois os retornos de chamada são registrados usando as funções `CQ_Analytics.registerBeforeCallback(callback,rank)` e `CQ_Analytics.registerAfterCallback(callback,rank)`.

Ambas as funções assumem uma função como o primeiro argumento e uma classificação como o segundo, o que determina a ordem em que os retornos de chamada são executados.

Se o retorno de chamada retornar false, os retornos de chamada que seguem na cadeia de execução não serão executados.
