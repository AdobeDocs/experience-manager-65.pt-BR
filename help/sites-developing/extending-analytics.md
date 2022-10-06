---
title: Extensão do rastreamento de eventos
seo-title: Extending Event Tracking
description: O AEM Analytics permite rastrear a interação do usuário no seu site
seo-description: AEM Analytics allows you to track user interaction on your website
uuid: 722798ac-4043-4918-a6df-9eda2c85020b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e0372f4a-fe7b-4526-8391-5bb345b51d70
exl-id: a71d20e6-0321-4afb-95fe-6de8b7b37245
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Extensão do rastreamento de eventos{#extending-event-tracking}

AEM Analytics permite que você acompanhe a interação do usuário em seu site. Como desenvolvedor, talvez seja necessário:

* Rastreie a forma como os visitantes interagem com seus componentes. Isso pode ser feito com [Eventos personalizados.](#custom-events)
* [Acessar valores no ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).
* [Adicionar retornos de chamada de registro](#adding-record-callbacks).

>[!NOTE]
>
>Essas informações são basicamente genéricas, mas usam [Adobe Analytics](/help/sites-administering/adobeanalytics.md) para exemplos específicos.
>
>Para obter informações gerais sobre o desenvolvimento de componentes e caixas de diálogo, consulte [Componentes de desenvolvimento](/help/sites-developing/components.md).

## Eventos personalizados {#custom-events}

Os eventos personalizados rastreiam qualquer coisa que dependa da disponibilidade de um componente específico na página. Isso também inclui eventos específicos do modelo, já que o componente da página é tratado como outro componente.

### Rastreamento De Eventos Personalizados No Carregamento Da Página {#tracking-custom-events-on-page-load}

Isso pode ser feito usando o pseudo-atributo `data-tracking` (o atributo de registro mais antigo ainda é compatível com versões anteriores). Você pode adicionar isso a qualquer tag HTML.

A sintaxe para `data-tracking` é

* `data-tracking="{'event': ['eventName'], 'values': {'key': 'value', 'nextKey': 'nextValue'}, componentPath: 'myapp/component/mycomponent'}"`

Você pode transmitir qualquer número de pares de valores chave como o segundo parâmetro, que é chamado de carga útil.

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

No carregamento da página, tudo `data-tracking` os atributos serão coletados e adicionados ao armazenamento de eventos do ContextHub, onde podem ser mapeados para eventos do Adobe Analytics. Eventos que não são mapeados não serão rastreados pelo Adobe Analytics. Consulte [Conexão com o Adobe Analytics](/help/sites-administering/adobeanalytics.md) para obter mais detalhes sobre eventos de mapeamento.

### Rastreamento de eventos personalizados após o carregamento da página {#tracking-custom-events-after-page-load}

Para rastrear eventos que ocorrem depois que uma página é carregada (como interações de usuário), use o `CQ_Analytics.record` Função do JavaScript:

* `CQ_Analytics.record({event: 'eventName', values: { valueName: 'VALUE' }, collect: false, options: { obj: this, defaultLinkType: 'X' }, componentPath: '<%=resource.getResourceType()%>'})`

Onde

* `events` é uma sequência de caracteres ou uma matriz de sequência (para vários eventos).

* `values` contém todos os valores a serem rastreados
* `collect` é opcional e retornará uma matriz contendo o evento e o objeto de dados.
* `options` é opcional e contém opções de rastreamento de link como o elemento HTML `obj` e ` [defaultLinkType](https://microsite.omniture.com/t2/help/en_US/sc/implement/index.html#linkType)`.

* `componentPath` é um atributo necessário e é recomendável defini-lo como `<%=resource.getResourceType()%>`

Por exemplo, com a seguinte definição, um usuário clica no botão **Ir para o início** causará os dois eventos, `jumptop` e `headlineclick`, a ser despedido:

```xml
<h1 data-tracking="{event: 'headline', values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'}">
  My Headline <a href="#" onclick="CQ_Analytics.record({event: ['jumptop','headlineclick'],  values: {level:'1'}, componentPath: '<%=resource.getResourceType()%>'})">Jump to top</a>
</h1>
```

## Acesso a valores no ContextHub {#accessing-values-in-the-contexthub}

A API do JavaScript do ContextHub tem um `getStore(name)` que retorna o armazenamento especificado, se disponível. A loja tem um `getItem(key)` que retorna o valor da chave especificada, se disponível. Usar o `getKeys()` é possível recuperar uma matriz de chaves definidas para a loja específica.

Você pode ser notificado sobre alterações de valor em uma loja vinculando uma função usando o `ContextHub.getStore(name).eventing.on(ContextHub.Constants.EVENT_STORE_UPDATED, handler, selector, triggerForPastEvents)` .

A melhor maneira de ser notificado da disponibilidade inicial do ContextHub é usar o `ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);` .

**Eventos adicionais para o ContextHub:**

Todas as lojas prontas:

`ContextHub.eventing.on(ContextHub.Constants.EVENT_ALL_STORES_READY, handler, selector, triggerForPastEvents);`

Específico da loja:

`ContextHub.getStore(store).eventing.on(ContextHub.Constants.EVENT_STORE_READY, handler, selector, triggerForPastEvents)`

>[!NOTE]
>
>Veja também a conclusão [Referência da API do ContextHub](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/contexthub-api.html#ContextHubJavascriptAPIReference)

## Adicionar Retornos de chamada de registro {#adding-record-callbacks}

Antes e depois dos retornos de chamada são registrados usando as funções `CQ_Analytics.registerBeforeCallback(callback,rank)` e `CQ_Analytics.registerAfterCallback(callback,rank)`.

Ambas as funções assumem uma função como o primeiro argumento e uma classificação como o segundo argumento, o que determina a ordem em que os retornos de chamada são executados.

Se o retorno de chamada retornar false, os retornos de chamada subsequentes na cadeia de execução não serão executados.
