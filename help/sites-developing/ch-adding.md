---
title: Adicionar o ContextHub a páginas e acessar lojas
description: Adicione o ContextHub às suas páginas para ativar os recursos do ContextHub e para vincular às bibliotecas de JavaScript do ContextHub
exl-id: ae745af9-b49f-46b9-ab48-2fd256e9a681
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Adicionar o ContextHub a páginas e acessar lojas {#adding-contexthub-to-pages-and-accessing-stores}

Adicione o ContextHub às suas páginas para ativar os recursos do ContextHub e para vincular às bibliotecas de JavaScript do ContextHub.

A API JavaScript do ContextHub fornece acesso aos dados de contexto que o ContextHub gerencia. Esta página descreve brevemente os principais recursos da API para acessar e manipular dados de contexto. Siga os links para a documentação de referência da API para ver informações detalhadas e exemplos de código.

## Adicionar o ContextHub a um componente de Página {#adding-contexthub-to-a-page-component}

Para ativar os recursos do ContextHub e vincular às bibliotecas JavaScript do ContextHub, inclua o `contexthub` componente no `head` seção da sua página. O código HTL do seu componente Página deve se parecer com o seguinte exemplo:

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

Observe que você também precisa configurar se a barra de ferramentas do ContextHub aparece no modo de Visualização. Consulte [Exibição e ocultação da interface do usuário do ContextHub](ch-configuring.md#showing-and-hiding-the-contexthub-ui).

## Sobre as lojas ContextHub {#about-contexthub-stores}

Use os armazenamentos do ContextHub para manter os dados de contexto. O ContextHub fornece os seguintes tipos de armazenamentos que formam a base de todos os tipos de armazenamentos:

* [ArmazenamentoPersistente](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [Armazenamento JSON](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [JSONPStorePersistente](contexthub-api.md#contexthub-store-persistedstore)

Todos os tipos de lojas são extensões da [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core) classe. Para obter informações sobre como criar um novo tipo de loja, consulte [Criar lojas personalizadas](ch-extend.md#creating-custom-store-candidates). Para obter informações sobre tipos de armazenamento de exemplo, consulte [Amostra de candidatos da loja do ContextHub](ch-samplestores.md).

### Modos de persistência {#persistence-modes}

Os armazenamentos do Context Hub usam um dos seguintes modos de persistência:

* **Local:** Usa o HTML5 localStorage para manter os dados. O armazenamento local é mantido no navegador em todas as sessões.
* **Sessão:** Usa HTML5 sessionStorage para manter os dados. O armazenamento de sessão é mantido pela duração da sessão do navegador e está disponível em todas as janelas do navegador.
* **Cookie:** Usa o suporte nativo do navegador a cookies para armazenamento de dados. Os dados de cookie são enviados de e para o servidor em solicitações HTTP.
* **Window.name:** Usa a propriedade window.name para manter os dados.
* **Memória:** Usa um objeto JavaScript para manter os dados.

Por padrão, o Context Hub usa o modo de persistência local. Se o navegador não suportar ou permitir HTML5 localStorage, a persistência de sessão será usada. Se o navegador não suportar ou permitir HTML5 sessionStorage, a persistência Window.name será usada.

### Armazenamento de dados {#store-data}

Internamente, os dados de armazenamento formam uma estrutura em árvore, permitindo que os valores sejam adicionados como tipos primários ou objetos complexos. Quando você adiciona objetos complexos a armazenamentos, as propriedades do objeto formam ramificações na árvore de dados. Por exemplo, o seguinte objeto complexo é adicionado a um armazenamento vazio chamado localização:

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

A estrutura de árvore dos dados de armazenamento pode ser conceitualizada da seguinte maneira:

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

A estrutura de árvore define itens de dados no armazenamento como pares de chave/valor. No exemplo acima, a chave `/number` corresponde ao valor `321`e a chave `/data/country` corresponde ao valor `Switzerland`.

### Manipulação de objetos {#manipulating-objects}

O ContextHub fornece o [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) para manipular objetos JavaScript. Use as funções dessa classe para manipular objetos JavaScript antes de adicioná-los a um armazenamento ou depois de obtê-los de um armazenamento.

Além disso, a [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) A classe fornece funções para serializar objetos para sequências e desserializar sequências para objetos. Use essa classe para manipular dados JSON para suportar navegadores que não incluem nativamente o `JSON.parse` e `JSON.stringify` funções.

## Interagir com lojas ContextHub {#interacting-with-contexthub-stores}

Use o [`ContextHub`](contexthub-api.md#ui-event-constants) JavaScript object para obter um armazenamento como um objeto JavaScript. Depois de obter o objeto de armazenamento, você pode manipular os dados que ele contém. Use o [`getAllStores`](contexthub-api.md#getallstores) ou o [`getStore`](contexthub-api.md#getstore-name) função para obter o armazenamento.

### Acessar dados da loja {#accessing-store-data}

A variável [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) A classe JavaScript define várias funções para interagir com os dados de armazenamento. As funções a seguir armazenam e recuperam vários itens de dados contidos em objetos:

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

Os itens de dados individuais são armazenados como um conjunto de pares de chave-valor. Para armazenar e recuperar valores, especifique a chave correspondente:

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

Observe que os candidatos de armazenamento personalizado podem definir funções adicionais que forneçam acesso aos dados de armazenamento.

>[!NOTE]
>
>Por padrão, o ContextHub não reconhece o logon atual usado em servidores de publicação e esses usuários são considerados pelo ContextHub como &quot;Anônimos&quot;.
>
>Você pode tornar o ContextHub ciente dos usuários conectados ao carregar o armazenamento de perfil. Consulte [exemplo de código no GitHub aqui](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### Eventos do ContextHub {#contexthub-eventing}

O ContextHub inclui uma estrutura de eventos que permite que você reaja automaticamente aos eventos de armazenamento. Cada objeto de armazenamento contém um [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) objeto que está disponível como o [`eventing`](contexthub-api.md#eventing) propriedade. Use o [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) ou [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) para vincular uma função JavaScript a um evento de armazenamento.

## Utilização do Context Hub para manipular cookies {#using-context-hub-to-manipulate-cookies}

A API JavaScript do Context Hub oferece suporte entre navegadores para manipular cookies do navegador. A variável [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) O namespace define várias funções para criar, manipular e excluir cookies.

## Determinar segmentos resolvidos do ContextHub {#determining-resolved-contexthub-segments}

O mecanismo de segmento do ContextHub permite determinar quais dos segmentos registrados são resolvidos no contexto atual. Use a função getResolvedSegments do [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) classe para recuperar segmentos resolvidos. Em seguida, use o `getName` ou `getPath` função da [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) classe a ser testada para um segmento.

### Segmentos ContextHub {#contexthub-segments}

Os segmentos do ContextHub são instalados abaixo do `/conf/<site>/settings/wcm/segments` nó.

Os seguintes segmentos são instalados com o [Site do tutorial do WKND.](getting-started.md)

* verão
* inverno

As regras usadas para resolver esses segmentos são resumidas da seguinte maneira:

* Primeiro, o [localização geográfica](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) armazenamento é usado para determinar a latitude do usuário.
* Em seguida, o item de dados mensal do [loja surferinfo](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) determina a estação nessa latitude.

>[!WARNING]
>
>Os segmentos instalados são fornecidos como configurações de referência para ajudar você a criar sua própria configuração dedicada para o projeto e, como tal, não devem ser usados diretamente.

## Depuração do ContextHub {#debugging-contexthub}

Há várias opções para depurar o ContextHub, incluindo a geração de logs. Consulte [Configuração do ContextHub para obter mais informações.](ch-configuring.md#logging-debug-messages-for-contexthub)

## Consulte uma visão geral da estrutura do ContextHub {#see-an-overview-of-the-contexthub-framework}

O ContextHub fornece uma [página de diagnósticos](ch-diagnostics.md) onde você pode ter uma visão geral da estrutura do ContextHub.
