---
title: Adicionando o ContextHub a páginas e acessando lojas
description: Adicione o ContextHub às suas páginas para ativar os recursos do ContextHub e para vincular às bibliotecas do ContextHub Javascript
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---


# Adicionando o ContextHub a páginas e acessando lojas {#adding-contexthub-to-pages-and-accessing-stores}

Adicione o ContextHub às suas páginas para ativar os recursos do ContextHub e para vincular às bibliotecas do ContextHub Javascript.

A API Javascript do ContextHub fornece acesso aos dados de contexto que o ContextHub gerencia. Esta página descreve resumidamente os principais recursos da API para acessar e manipular dados de contexto. Siga os links para a documentação de referência da API para ver informações detalhadas e exemplos de código.

## Adicionar o ContextHub a um componente de página {#adding-contexthub-to-a-page-component}

Para ativar os recursos do ContextHub e vincular às bibliotecas do ContextHub Javascript, inclua o `contexthub` componente na seção da `head` página. O código HTL do componente de sua página deve se assemelhar ao exemplo a seguir:

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

Observe que também é necessário configurar se a barra de ferramentas do ContextHub aparece no modo de Pré-visualização. Consulte [Mostrar e ocultar a interface do usuário](ch-configuring.md#showing-and-hiding-the-contexthub-ui)do ContextHub.

## Sobre as Lojas do ContextHub {#about-contexthub-stores}

Use os armazenamentos do ContextHub para persistir nos dados de contexto. O ContextHub fornece os seguintes tipos de lojas que formam a base de todos os tipos de lojas:

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

Todos os tipos de armazenamento são extensões da [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) classe. Para obter informações sobre como criar um novo tipo de armazenamento, consulte [Criação de armazenamentos](ch-extend.md#creating-custom-store-candidates)personalizados. Para obter informações sobre tipos de armazenamento de amostra, consulte [Amostra de candidatos](ch-samplestores.md)à loja do ContextHub.

### Modos de persistência {#persistence-modes}

Os armazenamentos do Context Hub usam um dos seguintes modos de persistência:

* **Local:** Usa HTML5 localStorage para persistir os dados. O armazenamento local é persistente no navegador entre sessões.
* **Sessão:** Usa HTML5 sessionStorage para persistir os dados. O armazenamento de sessão é persistente durante a sessão do navegador e está disponível para todas as janelas do navegador.
* **Cookie:** Usa o suporte nativo do navegador a cookies para armazenamento de dados. Os dados do cookie são enviados para e do servidor em solicitações HTTP.
* **Window.name:** Usa a propriedade window.name para persistir nos dados.
* **Memória:** Usa um objeto Javascript para persistir os dados.

Por padrão, o Context Hub usa o modo de persistência Local. Se o navegador não suportar ou permitir HTML5 localStorage, a persistência da sessão será usada. Se o navegador não oferecer suporte ou permitir o HTML5 sessionStorage, a persistência de Window.name será usada.

### Armazenamento de dados {#store-data}

Internamente, armazene formulários de dados em uma estrutura em árvore, permitindo que valores sejam adicionados como tipos primários ou objetos complexos. Quando objetos complexos são adicionados a armazenamentos, as propriedades de objetos formam ramificações na árvore de dados. Por exemplo, o seguinte objeto complexo é adicionado a uma loja vazia com o nome de local:

```javascript
Object {
   number: 321,
   data: {
      city: "Basel",
      country: "Switzerland",
      details: {
         population: 173330,
         elevation: 260
      }
   }
}
```

A estrutura em árvore dos dados de armazenamento pode ser conceitualizada da seguinte maneira:

```text
/
|- number
|- data
      |- city
      |- country
      |- details
            |- population
            |- elevation
```

A estrutura em árvore define itens de dados no armazenamento como pares de chave/valor. No exemplo acima, a chave `/number` corresponde ao valor `321`, e a chave `/data/country` corresponde ao valor `Switzerland`.

### Manipulação de objetos {#manipulating-objects}

O ContextHub fornece a [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) classe para manipular objetos Javascript. Use as funções dessa classe para manipular objetos Javascript antes de adicioná-los a uma loja ou depois de obtê-los de uma loja.

Além disso, a [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) classe fornece funções para serialização de objetos em strings e desserialização de strings em objetos. Use essa classe para manipular dados JSON para suportar navegadores que não incluem nativamente as funções `JSON.parse` e `JSON.stringify` .

## Interação com as armazenamentos do ContextHub {#interacting-with-contexthub-stores}

Use o objeto [`ContextHub`](contexthub-api.md#ui-event-constants) Javascript para obter uma loja como um objeto Javascript. Depois de obter o objeto store, é possível manipular os dados que ele contém. Use a função [`getAllStores`](contexthub-api.md#getallstores) ou a [`getStore`](contexthub-api.md#getstore-name) função para obter a loja.

### Acessar dados da loja {#accessing-store-data}

A classe [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) Javascript define várias funções para interagir com dados de armazenamento. As seguintes funções armazenam e recuperam vários itens de dados contidos em objetos:

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

Os itens de dados individuais são armazenados como um conjunto de pares de chave/valor. Para armazenar e recuperar valores, especifique a chave correspondente:

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

Observe que os candidatos a armazenamento personalizado podem definir funções adicionais que fornecem acesso aos dados de armazenamento.

>[!NOTE]
>
>Por padrão, o ContextHub não está ciente do logon atualmente usado em servidores de publicação e esses usuários são considerados pelo ContextHub como &quot;Anônimos&quot;.
>
>Você pode tornar o ContextHub ciente dos usuários conectados carregando a loja de perfis. Consulte o código de [amostra no GitHub aqui](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### Eventos do ContextHub {#contexthub-eventing}

O ContextHub inclui uma estrutura de evento que permite que você reaja automaticamente para armazenar eventos. Cada objeto store contém um [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) objeto que está disponível como [`eventing`](contexthub-api.md#eventing) propriedade do armazenamento. Use a função [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) ou [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) para vincular uma função Javascript a um evento de loja.

## Uso do Context Hub para Manipular Cookies {#using-context-hub-to-manipulate-cookies}

A API Javascript do Context Hub fornece suporte entre navegadores para lidar com cookies de navegadores. A [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) namespace define várias funções para criar, manipular e excluir cookies.

## Determinando segmentos resolvidos do ContextHub {#determining-resolved-contexthub-segments}

O mecanismo de segmento ContextHub permite que você determine quais segmentos registrados são resolvidos no contexto atual. Use a função getResolvedSegments da [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) classe para recuperar segmentos resolvidos. Em seguida, use a função `getName` ou `getPath` da [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) classe para testar um segmento.

### Segmentos ContextHub {#contexthub-segments}

Os segmentos do ContextHub são instalados abaixo do `/conf/<site>/settings/wcm/segments` nó.

Os seguintes segmentos são instalados com o site de tutorial [WKND.](getting-started.md)

* verão
* inverno

As regras usadas para resolver esses segmentos são resumidas da seguinte forma:

* Primeiro, a loja de [geolocalização](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) é usada para determinar a latitude do usuário.
* Em seguida, o item de dados do mês da loja [](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) surferinfo determina qual estação está nessa latitude.

>[!WARNING]
>
>Os segmentos instalados são fornecidos como configurações de referência para ajudá-lo a criar sua própria configuração dedicada ao seu projeto e, como tal, não devem ser usados diretamente.

## Depuração do ContextHub {#debugging-contexthub}

Há várias opções para depurar o ContextHub, incluindo a geração de logs. Consulte [Configuração do ContextHub para obter mais informações.](ch-configuring.md#logging-debug-messages-for-contexthub)

## Consulte uma visão geral da estrutura do ContextHub {#see-an-overview-of-the-contexthub-framework}

O ContextHub fornece uma página [de](ch-diagnostics.md) diagnósticos onde você pode ver uma visão geral da estrutura do ContextHub.
