---
title: Adicionar o ContextHub às páginas e acessar armazenamentos
description: Adicionar o ContextHub às suas páginas para ativar os recursos do ContextHub e para vincular às bibliotecas JavaScript do ContextHub
exl-id: ae745af9-b49f-46b9-ab48-2fd256e9a681
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Adicionar o ContextHub às páginas e acessar armazenamentos {#adding-contexthub-to-pages-and-accessing-stores}

Adicione o ContextHub às suas páginas para ativar os recursos do ContextHub e vincular às bibliotecas JavaScript do ContextHub.

A API Javascript do ContextHub fornece acesso aos dados de contexto que o ContextHub gerencia. Esta página descreve resumidamente os principais recursos da API para acessar e manipular dados de contexto. Siga os links para a documentação de referência da API para ver informações detalhadas e exemplos de código.

## Adicionar o ContextHub a um componente de página {#adding-contexthub-to-a-page-component}

Para ativar os recursos do ContextHub e vincular às bibliotecas JavaScript do ContextHub, inclua o `contexthub` no `head` da sua página. O código HTL do componente de página deve ser semelhante ao seguinte exemplo:

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

Observe que também é necessário configurar se a barra de ferramentas do ContextHub aparece no modo de Visualização. Consulte [Exibir e ocultar a interface do usuário do ContextHub](ch-configuring.md#showing-and-hiding-the-contexthub-ui).

## Sobre armazenamentos do ContextHub {#about-contexthub-stores}

Use armazenamentos do ContextHub para persistir os dados de contexto. O ContextHub fornece os seguintes tipos de lojas que formam a base de todos os tipos de lojas:

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [JSONPStorePersisted](contexthub-api.md#contexthub-store-persistedstore)

Todos os tipos de armazenamento são extensões do [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) classe . Para obter informações sobre como criar um novo tipo de armazenamento, consulte [Criação de lojas personalizadas](ch-extend.md#creating-custom-store-candidates). Para obter informações sobre tipos de armazenamentos de amostra, consulte [Exemplos de candidatos à loja do ContextHub](ch-samplestores.md).

### Modos de persistência {#persistence-modes}

Os armazenamentos do Context Hub usam um dos seguintes modos de persistência:

* **Local:** Usa HTML5 localStorage para manter os dados. O armazenamento local é mantido no navegador em todas as sessões.
* **Sessão:** Usa HTML5 sessionStorage para manter os dados. O armazenamento de sessão é mantido pela duração da sessão do navegador e está disponível para todas as janelas do navegador.
* **Cookie:** Usa o suporte nativo de cookies do navegador para armazenamento de dados. Os dados do cookie são enviados para e do servidor em solicitações HTTP.
* **Window.name:** Usa a propriedade window.name para persistir os dados.
* **Memória:** Usa um objeto Javascript para persistir dados.

Por padrão, o Context Hub usa o modo de persistência Local. Se o navegador não suportar ou permitir o HTML5 localStorage, a persistência da sessão será usada. Se o navegador não suportar ou permitir o HTML5 sessionStorage, a persistência de Window.name será usada.

### Armazenamento de dados {#store-data}

Internamente, armazene formulários de dados em uma estrutura em árvore, permitindo que valores sejam adicionados como tipos primários ou objetos complexos. Quando objetos complexos são adicionados aos armazenamentos, as propriedades do objeto formam ramificações na árvore de dados. Por exemplo, o seguinte objeto complexo é adicionado a um armazenamento vazio chamado location:

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

A estrutura de árvore define itens de dados no armazenamento como pares de chave/valor. No exemplo acima, a chave `/number` corresponde ao valor `321`e a tecla `/data/country` corresponde ao valor `Switzerland`.

### Manipulação de Objetos {#manipulating-objects}

O ContextHub fornece a variável [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) classe para manipular objetos Javascript. Use as funções dessa classe para manipular objetos Javascript antes de adicioná-los a uma loja ou depois de obtê-los de uma loja.

Além disso, a variável [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) A classe fornece funções para serializar objetos para cadeia de caracteres e desserializar cadeias de caracteres para objetos. Use essa classe para manipular dados JSON para suportar navegadores que não incluem nativamente a variável `JSON.parse` e `JSON.stringify` funções.

## Interagir com armazenamentos do ContextHub {#interacting-with-contexthub-stores}

Use o [`ContextHub`](contexthub-api.md#ui-event-constants) Objeto Javascript para obter uma loja como um objeto Javascript. Depois de obter o objeto de armazenamento, você pode manipular os dados que ele contém. Use o [`getAllStores`](contexthub-api.md#getallstores) ou [`getStore`](contexthub-api.md#getstore-name) para obter a loja.

### Acesso aos dados do armazenamento {#accessing-store-data}

O [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) A classe Javascript define várias funções para interagir com dados de armazenamento. As seguintes funções armazenam e recuperam vários itens de dados contidos em objetos:

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

Os itens de dados individuais são armazenados como um conjunto de pares de chave/valor. Para armazenar e recuperar valores, especifique a chave correspondente:

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

Observe que os candidatos a armazenamento personalizado podem definir funções adicionais que fornecem acesso para armazenar dados.

>[!NOTE]
>
>Por padrão, o ContextHub não tem conhecimento do logon atualmente usado nos servidores de publicação e esses usuários são considerados pelo ContextHub como &quot;Anônimos&quot;.
>
>Você pode tornar o ContextHub ciente dos usuários conectados carregando o armazenamento de perfis. Consulte [exemplo de código no GitHub aqui](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### Eventos do ContextHub {#contexthub-eventing}

O ContextHub inclui uma estrutura de evento que permite reagir automaticamente para armazenar eventos. Cada objeto de armazenamento contém um [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) objeto que está disponível como [`eventing`](contexthub-api.md#eventing) propriedade. Use o [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) ou [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) para vincular uma função Javascript a um evento de loja.

## Uso do Context Hub para Manipular cookies {#using-context-hub-to-manipulate-cookies}

A API Javascript do Context Hub fornece suporte entre navegadores para manipular cookies do navegador. O [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) o namespace define várias funções para criar, manipular e excluir cookies.

## Determinar segmentos do ContextHub resolvidos {#determining-resolved-contexthub-segments}

O mecanismo de segmento do ContextHub permite determinar qual dos segmentos registrados é resolvido no contexto atual. Use a função getResolvedSegments do [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) classe para recuperar segmentos resolvidos. Em seguida, use o `getName` ou `getPath` da [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) classe para testar um segmento.

### Segmentos ContextHub {#contexthub-segments}

Os segmentos do ContextHub são instalados abaixo da variável `/conf/<site>/settings/wcm/segments` nó .

Os seguintes segmentos são instalados com a variável [Site tutorial WKND.](getting-started.md)

* verão
* inverno

As regras usadas para resolver esses segmentos são resumidas da seguinte maneira:

* Primeiro, o [geolocalização](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) é usada para determinar a latitude do usuário.
* Em seguida, o item de dados do mês da variável [loja de surferinfo](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) determina qual estação está nessa latitude.

>[!WARNING]
>
>Os segmentos instalados são fornecidos como configurações de referência para ajudar você a criar sua própria configuração dedicada para o seu projeto e, como tal, não devem ser usados diretamente.

## Depuração do ContextHub {#debugging-contexthub}

Há várias opções para depurar o ContextHub, incluindo a geração de logs. Consulte [Configuração do ContextHub para obter mais informações.](ch-configuring.md#logging-debug-messages-for-contexthub)

## Consulte a Visão geral da estrutura do ContextHub {#see-an-overview-of-the-contexthub-framework}

O ContextHub fornece uma [página de diagnósticos](ch-diagnostics.md) onde você pode ver uma visão geral da estrutura do ContextHub.
