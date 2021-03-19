---
title: Referência de API do Javascript do ContextHub
seo-title: Referência de API do Javascript do ContextHub
description: A API Javascript do ContextHub está disponível para seus scripts quando o componente ContextHub foi adicionado à página
seo-description: A API Javascript do ContextHub está disponível para seus scripts quando o componente ContextHub foi adicionado à página
uuid: 296d6c8e-517f-4837-9e86-ae571ea8aa17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 90605f41-1861-4891-a7c8-b8b5918cd5c6
feature: Context Hub
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '5031'
ht-degree: 3%

---


# Referência de API do Javascript do ContextHub{#contexthub-javascript-api-reference}

A API Javascript do ContextHub está disponível para seus scripts quando o componente [ContextHub foi adicionado à página](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component).

## Constantes do ContextHub {#contexthub-constants}

Valores constantes que a API Javascript do ContextHub define.

### Constantes do evento {#event-constants}

A tabela a seguir lista os nomes dos eventos que ocorrem para as lojas do ContextHub. Consulte também [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing).

| Constante | Descrição | Valor |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | Namespace do evento do ContextHub | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | Indica que todas as lojas necessárias estão registradas, inicializadas e prontas para serem consumidas | pronto para todas as lojas |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | Indica que nem todos os armazenamentos foram inicializados dentro de um determinado tempo limite | armazenamentos parcialmente prontos |
| ContextHub.Constants.EVENT_STORE_REGISTERED | Disparado quando uma loja é registrada | registrado na loja |
| ContextHub.Constants.EVENT_STORE_READY | Indica que as lojas estão prontas para funcionar. É acionado imediatamente após o registro, exceto armazenamentos JSONP, onde é acionado quando os dados são buscados). | pronto para armazenamento |
| ContextHub.Constants.EVENT_STORE_UPDATED | Disparado quando um armazenamento atualiza sua persistência | armazenado atualizado |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | Nome do contêiner de persistência | ContextHubPersistence |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | Armazena o nome da chave de persistência específica onde o resultado JSON bruto é armazenado | /_/raw-response |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | Armazena um carimbo de data e hora específico que indica quando os dados JSON foram obtidos | /_/tempo de resposta |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | Armazena url específico do serviço JSON usado durante a última chamada | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | Indica se a interface do usuário do ContextHub foi expandida | /_/contêiner expandido |

### Constantes de evento da interface do usuário {#ui-event-constants}

A tabela a seguir lista os nomes dos eventos que ocorrem para a interface do usuário do ContextHub.

| **Constante** | **Descrição** | **Valor** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | Disparado quando um modo é registrado | ui-mode-register |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | Acionado quando um modo não está registrado | ui-mode-unregister |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | Acionado quando um renderizador de modo é registrado | ui-mode-renderer-register |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | Acionado quando um renderizador de modo não está registrado | ui-mode-renderer-unregister |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | Acionado quando um novo modo é adicionado | ui-mode-added |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | Acionado quando um modo é removido | ui-mode-remove |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | Acionado quando um modo é selecionado pelo usuário | ui-mode-seleted |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | Acionado quando um novo módulo é registrado | ui-module-registrado |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | Acionado quando um módulo não está registrado | ui-module-unregister |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | Acionado quando um renderizador de módulo é registrado | ui-module-renderer-register |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | Acionado quando um renderizador de módulo não está registrado | ui-module-renderer-unregister |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | Acionado quando um novo módulo é adicionado | ui-module adicionado |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | Acionado quando um módulo é removido | ui-module-removido |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | Acionado quando o contêiner da interface do usuário é adicionado à página | ui-container-added |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | Acionado quando a interface do usuário do ContextHub é aberta | ui-container-opened |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | Acionada quando a interface do usuário do ContextHub é recolhida | ui-container-closed |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | Acionado quando uma propriedade é modificada | ui-property-modified |
| ContextHub.Constants.EVENT_UI_RENDERED | Disparado sempre que a interface do usuário do ContextHub é renderizada (por exemplo, após uma alteração de propriedade) | ui-renderizado |
| ContextHub.Constants.EVENT_UI_INITIALIZED | Disparado quando o contêiner da interface do usuário é inicializado | ui-initialized |
| ContextHub.Constants.ACTIVE_UI_MODE | Indica o modo de interface do usuário ativo | /_/ative-ui-mode |

## Referência de API do Javascript do ContextHub {#contexthub-javascript-api-reference-2}

O objeto ContextHub fornece acesso a todos os armazenamentos.

### Funções (ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

Retorna todos os armazenamentos registrados do ContextHub.

Essa função não tem parâmetros.

**Retorna**

Um objeto que contém todos os armazenamentos do ContextHub. Cada loja é um objeto que usa o mesmo nome da loja.

**Exemplo**

O exemplo a seguir recupera todos os armazenamentos e recupera o armazenamento de geolocalização:

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

Recupera uma loja como um objeto Javascript.

**Parâmetros**

* **name:** o nome com o qual a loja foi registrada.

**Retorna**

Um objeto que representa o armazenamento.

**Exemplo**

O exemplo a seguir recupera o armazenamento de geolocalização:

```
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

Representa um segmento do ContextHub. Use o ContextHub.SegmentEngine.SegmentManager para obter segmentos.

### Funções (ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

Retorna o nome do segmento como um valor de String.

#### getPath() {#getpath}

Retorna o caminho do repositório da definição do segmento como um valor de String.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Fornece acesso aos segmentos do ContextHub.

### Funções (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

Retorna os segmentos que são resolvidos no contexto atual. Essa função não tem parâmetros.

**Retorna**

Uma matriz de objetos ContextHub.SegmentEngine.Segment.

## ContextHub.Store.Core {#contexthub-store-core}

A classe base dos armazenamentos do ContextHub.

### Propriedades (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### evento {#eventing}

Um objeto [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing). Use esse objeto para vincular funções a fim de armazenar eventos. Para obter informações sobre o valor padrão e a inicialização, consulte [init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).

#### name {#name}

O nome da loja.

#### persistência {#persistence}

Um objeto ContextHub.Utils.Persistence. Para obter informações sobre o valor padrão e a inicialização, consulte `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### Funções (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

Une um objeto de dados ou uma matriz aos dados da loja. Cada par de chave/valor no objeto ou matriz é adicionado ao armazenamento (por meio da função `setItem` ):

* **Objeto:** Chaves são os nomes das propriedades.
* **Matriz:** as chaves são os índices da matriz.

Observe que os valores podem ser objetos.

**Parâmetros**

* **tree:**  (objeto ou matriz) os dados a serem adicionados ao armazenamento.
* **opções:**  (Object) um objeto opcional de opções passado para a função setItem. Para obter informações, consulte o parâmetro `options` de [setItem(key,value,options)](/help/sites-developing/contexthub-api.md#setitem-key-value-options).

**Retorna**

Um valor `boolean`:

* Um valor `true` indica que o objeto de dados foi armazenado.
* Um valor `false` indica que o armazenamento de dados permanece inalterado.

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

Cria uma referência de uma chave para outra chave. Uma chave não pode fazer referência a si mesma.

**Parâmetros**

* **chave:** a chave que faz referência  `anotherKey`.

* **outra chave:** a chave referenciada por  `key`.

**Retorna**

Um valor `boolean`:

* Um valor `true` indica que a referência foi adicionada.
* Um valor `false` indica que nenhuma referência foi adicionada.

#### advertisingReadiness() {#announcereadiness}

Aciona o evento `ready` para esta loja. Essa função não tem parâmetros e não retorna valor.

#### clean() {#clean}

Remove todos os dados do armazenamento. A função não tem parâmetros e nenhum valor de retorno.

#### getItem(key) {#getitem-key}

Retorna o valor associado a uma chave.

**Parâmetros**

* **key:**  (String) a chave para a qual retornar o valor.

**Retorna**

Um Objeto que representa o valor da chave.

#### getKeys(includeInternals) {#getkeys-includeinternals}

Recupera as chaves da loja. Opcionalmente, é possível recuperar as chaves usadas internamente pela estrutura do ContextHub.

**Parâmetros**

* **includeInternals:** um valor de  `true` inclui chaves usadas internamente nos resultados. Essas chaves começam com o caractere sublinhado (&quot;_&quot;). O valor padrão é `false`.

**Retorna**

Uma matriz de nomes de chaves (valores `string`).

#### getReferences() {#getreferences}

Recupera as referências da loja.

**Retorna**

Uma matriz que usa chaves de referência como índices para as chaves referenciadas:

* As chaves de referência correspondem ao parâmetro `key` da função `addReference`.

* As chaves referenciadas correspondem ao parâmetro `anotherKey` da função `addReference`.

#### getTree(includeInternals) {#gettree-includeinternals}

Recupera a árvore de dados do armazenamento. Opcionalmente, é possível incluir os pares chave/valor usados internamente pela estrutura do ContextHub.

**Parâmetros**

* `includeInternals:` Um valor de  `true` inclui pares de chave/valor usados internamente nos resultados. As chaves desses dados começam com o caractere sublinhado (&quot;_&quot;). O valor padrão é `false`.

**Retorna**

Um objeto que representa a árvore de dados. As chaves são os nomes de propriedade do objeto.

#### init(name, config) {#init-name-config}

Inicializa o armazenamento.

* Define os dados do armazenamento para um objeto vazio.
* Define as referências de armazenamento para um objeto vazio.
* O eventChannel é data:*name*, onde *name* é o nome da loja.

* O storeDataKey é /store/*name*, onde *name* é o nome do armazenamento.

**Parâmetros**

* **name:** o nome do armazenamento.
* **config:** um objeto que contém propriedades de configuração:

   * eventDeferring: O valor padrão é 32.
   * evento: O objeto [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) para esta loja. O valor padrão é o que o objeto ContextHub.eventing usa.
   * persistência: O objeto ContextHub.Utils.Persistence para esta loja. O valor padrão é o objeto ContextHub.persistence.

#### isEventingPaused() {#iseventingpaused}

Determina se o evento está pausado para esta loja.

**Retorna**

Um valor booleano:

* `true`: O evento é pausado para que nenhum evento seja acionado para esta loja.
* `false`: Os eventos não são pausados para que sejam acionados para esta loja.

#### pauseEventing() {#pauseeventing}

Pausa o evento para a loja para que nenhum evento seja acionado. Essa função não requer parâmetros e não retorna valor.

#### removeItem(key, options) {#removeitem-key-options}

Remove um par de chave/valor do armazenamento.

Quando uma chave é removida, a função aciona o evento `data` . Os dados do evento incluem o nome do armazenamento, o nome da chave que foi removida, o valor que foi removido, o novo valor para a chave (nulo) e o tipo de ação &quot;remover&quot;.

Como opção, você pode impedir o acionamento do evento `data` .

**Parâmetros**

* **key:**  (String) o nome da chave a ser removida.
* **opções:**  (Objeto) Um objeto de opções. As seguintes propriedades de objeto são válidas:

   * silencioso: Um valor `true` impede o acionamento do evento `data`. O valor padrão é `false`.

**Retorna**

Um valor `boolean`:

* Um valor `true` indica que o par chave/valor foi removido.
* Um valor `false` indica que o armazenamento de dados permanece inalterado porque a chave não foi encontrada no armazenamento.

#### removeReference(key) {#removereference-key}

Remove uma referência da loja.

**Parâmetros**

* **chave:** a referência principal a ser removida. Esse parâmetro corresponde ao parâmetro `key` da função `addReference`.

**Retorna**

Um valor `boolean`:

* Um valor de `true` indica que a referência foi removida.
* Um valor `false` indica que a chave não era válida e que o armazenamento não foi alterado.

#### reset(keepRemainingData) {#reset-keepremainingdata}

Redefine os valores iniciais dos dados persistentes do armazenamento. Como opção, você pode remover todos os outros dados do armazenamento. O evento é pausado para esta loja enquanto ela é redefinida. Essa função não retorna valor.

Os valores iniciais são fornecidos na propriedade initialValues do objeto de configuração que é usado para instanciar o objeto de armazenamento.

**Parâmetros**

* **keepRemainingData:**  (Booleano) Um valor true faz com que os dados não iniciais sejam mantidos. Um valor false faz com que todos os dados sejam removidos, exceto os valores iniciais.

Redefine os valores iniciais dos dados persistentes do armazenamento. Como opção, você pode remover todos os outros dados do armazenamento. O evento é pausado para esta loja enquanto ela é redefinida. Essa função não retorna valor.

Os valores iniciais são fornecidos na propriedade initialValues do objeto de configuração que é usado para instanciar o objeto de armazenamento.

**Parâmetros**

* keepRemainingData: (Booleano) Um valor true faz com que os dados não iniciais sejam persistentes. Um valor false faz com que todos os dados sejam removidos, exceto os valores iniciais.

#### resolveReference(key, retry) {#resolvereference-key-retry}

Recupera uma chave referenciada. Como opção, você pode especificar o número de iterações a serem usadas para resolver a melhor correspondência.

**Parâmetros**

* **key:**  (String) a chave para a qual resolver a referência. Esse parâmetro `key` corresponde ao parâmetro `key` da função `addReference`.

* **nova tentativa:**  (Número) o número de iterações a serem usadas.

**Retorna**

Um valor `string` que representa a chave referenciada. Se nenhuma referência for resolvida, o valor do parâmetro `key` será retornado.

#### resumeEventing() {#resumeeventing}

Retoma o evento para esta loja para que os eventos sejam acionados. Essa função não define parâmetros e não retorna valor.

#### setItem(key, value, options) {#setitem-key-value-options}

Adiciona um par de chave/valor à loja.

Aciona o evento `data` somente se o valor da chave for diferente do valor armazenado atualmente para a chave. Opcionalmente, você pode impedir o acionamento do evento `data`.

Os dados do evento incluem o nome do armazenamento, a chave, o valor anterior, o novo valor e o tipo de ação `set`.

**Parâmetros**

* **key:**  (String) o nome da chave.
* **opções:**  (Objeto) Um objeto de opções. As seguintes propriedades de objeto são válidas:

   * silencioso: Um valor `true` impede o acionamento do evento `data`. O valor padrão é `false`.

* **value:**  (Object) o valor a ser associado à chave.

**Retorna**

Um valor `boolean`:

* Um valor `true` indica que o objeto de dados foi armazenado.
* Um valor `false` indica que o armazenamento de dados permanece inalterado.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Um armazenamento que contém dados JSON. Os dados são recuperados de um serviço JSONP externo ou, opcionalmente, de um serviço que retorna dados JSON. Especifique os detalhes do serviço usando a função [ `init`](/help/sites-developing/contexthub-api.md#init-name-config) ao criar uma instância dessa classe.

O armazenamento usa persistência na memória (variável Javascript). Os dados de armazenamento estão disponíveis somente durante a vida útil da página.

ContextHub.Store.JSONPStore estende [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) e herda as funções dessa classe.

### Funções (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Configura os detalhes para conexão com o serviço JSONP que este objeto usa. Você pode atualizar ou substituir a configuração existente. A função não retorna valor.

**Parâmetros**

* **serviceConfig:** um objeto que contém as seguintes propriedades:

   * host: (String) O nome do servidor ou endereço IP.
   * jsonp: (Booleano) Um valor true indica que o serviço é um serviço JSONP; caso contrário, é false. Quando verdadeiro, o {retorno de chamada: &quot;ContextHub.Callbacks.*O objeto Object.name*} é adicionado ao objeto service.params.
   * params: (Objeto) Parâmetros de URL representados como propriedades de objetos. Os nomes de parâmetros são nomes de propriedades e os valores de parâmetros são valores de propriedades.
   * caminho: (String) O caminho para o serviço.
   * porta: (Número) O número da porta do serviço.
   * seguro: (String ou Boolean) Determina o protocolo a ser usado para o URL do serviço:

      * auto: //
      * true: https://
      * falso: https://

* **override:**  (Boolean). Um valor `true` faz com que a configuração de serviço existente seja substituída pelas propriedades de `serviceConfig`. Um valor `false` faz com que as propriedades de configuração do serviço existentes sejam mescladas com as propriedades de `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Retorna a resposta bruta armazenada em cache desde a última chamada para o serviço JSONP. A função não requer parâmetros.

**Retorna**

Um objeto que representa a resposta bruta.

#### getServiceDetails() {#getservicedetails}

Recupera o objeto de serviço para este objeto ContextHub.Store.JSONPStore. O objeto de serviço contém todas as informações necessárias para criar o URL de serviço.

**Retorna**

Um objeto com as seguintes propriedades:

* **host:**  (String) o nome do servidor ou endereço IP.
* **jsonp:** (Boolean) Um valor true indica que o serviço é um serviço JSONP; caso contrário, é false. Quando verdadeiro, o {retorno de chamada: &quot;ContextHub.Callbacks.*O objeto Object.name*} é adicionado ao objeto service.params.

* **params:**  (Object) Parâmetros de URL representados como propriedades do objeto. Os nomes de parâmetros são nomes de propriedades e os valores de parâmetros são valores de propriedades.
* **path:**  (String) o caminho para o serviço.
* **porta:**  (Número) o número da porta do serviço.
* **secure:**  (String ou Boolean) determina o protocolo a ser usado para o URL de serviço:

   * auto: //
   * true: https://
   * falso: https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

Recupera o URL do serviço JSONP.

**Parâmetros**

* **resolver:**  (Booleano) Determina se os parâmetros resolvidos devem ser incluídos no URL. Um valor de `true` resolve parâmetros, e `false` não resolve.

**Retorna**

Um valor `string` que representa o URL do serviço.

#### init(name, config) {#init-name-config-1}

inicializa o objeto ContextHub.Store.JSONPStore .

**Parâmetros**

* **name:**  (String) o nome do armazenamento.
* **config:**  (Object) um objeto que contém a propriedade de serviço. O objeto JSONPStore usa as propriedades do objeto `service` para construir o URL do serviço JSONP:

   * eventDeferring: 32.
   * evento: O objeto ContextHub.Utils.Eventing para esta loja. O valor padrão é o objeto `ContextHub.eventing`.
   * persistência: O objeto ContextHub.Utils.Persistence para esta loja. Por padrão, a persistência de memória é usada (objeto Javascript).
   * serviço: (Objeto)

      * host: (String) O nome do servidor ou endereço IP.
      * jsonp: (Booleano) Um valor true indica que o serviço é um serviço JSONP; caso contrário, é false. Quando verdadeiro, o objeto `{callback: "ContextHub.Callbacks.*Object.name*}`é adicionado a `service.params`.
      * params: (Objeto) Parâmetros de URL representados como propriedades de objetos. Nomes e valores de parâmetros são os nomes e valores da propriedade de objeto, respectivamente.
      * caminho: (String) O caminho para o serviço.
      * porta: (Número) O número da porta do serviço.
      * seguro: (String ou Boolean) Determina o protocolo a ser usado para o URL do serviço:

         * auto: //
         * true: https://
         * falso: https://
      * tempo limite: (Número) A quantidade de tempo para aguardar a resposta do serviço JSONP antes de atingir o tempo limite, em milissegundos.
      * ttl: O tempo mínimo, em milissegundos, que passa entre as chamadas para o serviço JSONP. (Consulte a função [queryService](/help/sites-developing/contexthub-api.md#queryservice-reload)).


#### queryService(reload) {#queryservice-reload}

Consulta o serviço JSONP remoto e armazena em cache a resposta. Se a quantidade de tempo desde a chamada anterior para essa função for menor que o valor de `config.service.ttl`, o serviço não é chamado e a resposta em cache não é alterada. Como opção, você pode forçar a chamada do serviço. A propriedade `config.service.ttl`é definida ao chamar a função [init](/help/sites-developing/contexthub-api.md#init-name-config) para inicializar o armazenamento.

Aciona o evento ready quando o query for concluído. Se o URL do serviço JSONP não estiver definido, a função não fará nada.

**Parâmetros**

* **reload:** (Boolean) um valor true remove a resposta em cache e força o serviço JSONP a ser chamado.

#### reset {#reset}

Redefine os valores iniciais dos dados persistentes do armazenamento e, em seguida, chama o serviço JSONP. Como opção, você pode remover todos os outros dados do armazenamento. O evento é pausado para esta loja enquanto os valores iniciais são redefinidos. Essa função não retorna valor.

Os valores iniciais são fornecidos na propriedade initialValues do objeto de configuração que é usado para instanciar o objeto de armazenamento.

**Parâmetros**

* **keepRemainingData:**  (Booleano) Um valor true faz com que os dados não iniciais sejam mantidos. Um valor false faz com que todos os dados sejam removidos, exceto os valores iniciais.

#### resolveParameter(f) {#resolveparameter-f}

Resolve o parâmetro especificado.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PersistedJSONPStore estende [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) para herdar todas as funções dessa classe. No entanto, os dados recuperados do serviço JSONP são mantidos de acordo com a configuração de persistência do ContextHub. (Consulte [Modos de Persistência](/help/sites-developing/ch-adding.md#persistence-modes).)

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

O ContextHub.Store.PersistedStore estende [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) para herdar todas as funções dessa classe. Os dados nesse armazenamento são mantidos de acordo com a configuração da persistência do ContextHub.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

O ContextHub.Store.SessionStore estende [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) para que ele herde todas as funções dessa classe. Os dados nesse armazenamento são mantidos com persistência na memória (objeto Javascript).

## ContextHub.UI {#contexthub-ui}

Gerencia módulos de interface e renderizadores de módulo de interface do usuário.

### Funções (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

Registra um renderizador de módulo de interface do usuário com o ContextHub. Depois que o renderizador é registrado, ele pode ser usado para [criar módulos de interface do usuário](ch-configuring.md#adding-a-ui-module). Use essa função quando estiver [estendendo ContextHub.UI.BaseModuleRenderer](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types) para criar um renderizador de Módulo de interface do usuário personalizado.

**Parâmetros**

* **moduleType:**  (String) o identificador do renderizador do módulo da interface do usuário. Se um renderizador já estiver registrado usando o valor especificado, o renderizador existente não será registrado antes que esse renderizador seja registrado.
* **renderizador:**  (String) o nome da classe que renderiza o módulo da interface do usuário.
* **dontRender:** (Booleano) defina como  `true` para impedir que a interface do usuário do ContextHub seja renderizada depois que o renderizador for registrado. O valor padrão é `false`.

**Exemplo**

O exemplo a seguir registra um renderizador como o tipo de módulo contexthub.browserinfo .

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

Uma classe de utilitário para interagir com cookies.

### Funções (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

Determina se um cookie existe.

**Parâmetros**

* **chave:** Uma  `String` que contém a chave do cookie para o qual você está testando.

**Retorna**

Um valor `boolean` de true indica que o cookie existe.

**Exemplo**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

Retorna todos os cookies que têm chaves que correspondem a um filtro.

**Parâmetros**

* (Opcional) **filtro:** Critérios para as chaves de cookie correspondentes. Para retornar todos os cookies, não especifique nenhum valor. Os seguintes tipos são suportados:

   * Sequência de caracteres: A string é comparada à chave do cookie.
   * Matriz: Cada item na matriz é um filtro.
   * Um objeto RegExp: A função de teste do objeto é usada para corresponder às chaves do cookie.
   * Uma função: Uma função que testa uma chave de cookie para obter uma correspondência. A função deve assumir a chave do cookie como parâmetro e retornar true se o teste confirmar uma correspondência.

**Retorna**

Um objeto de cookies. As propriedades do objeto são chaves de cookie e os valores-chave são valores de cookie.

**Exemplo**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Retorna um valor de cookie.

**Parâmetros**

* **chave:** a chave do cookie para o qual você deseja obter o valor.

**Retorna**

O valor do cookie ou `null` se nenhum cookie foi encontrado para a chave.

**Exemplo**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

Retorna uma matriz das chaves dos cookies existentes que correspondem a um filtro.

**Parâmetros**

* **filtro:** Critérios para corresponder a chaves de cookie. Os seguintes tipos são suportados:

   * Sequência de caracteres: A string é comparada à chave do cookie.
   * Matriz: Cada item na matriz é um filtro.
   * Um objeto RegExp: A função de teste do objeto é usada para corresponder às chaves do cookie.
   * Uma função: Uma função que testa uma chave de cookie para obter uma correspondência. A função deve assumir a chave do cookie como parâmetro e retornar `true` se o teste confirmar uma correspondência.

**Retorna**

Uma matriz de strings na qual cada string é a chave de um cookie que corresponde ao filtro.

**Exemplo**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Remove um cookie. Para remover o cookie, o valor é definido como uma string vazia e a data de expiração é definida como o dia antes da data atual.

**Parâmetros**

* **chave:** um  `String` valor que representa a chave do cookie a ser removido.

* **opções:** um objeto que contém valores de propriedade para configurar os atributos do cookie. Consulte a função ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` para obter informações. A propriedade `expires` não tem efeito.

**Retorna**

Essa função não retorna um valor.

**Exemplo**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

Cria um cookie da chave e valor fornecidos e adiciona o cookie ao documento atual. Como opção, você pode especificar opções que configuram os atributos do cookie.

**Parâmetros**

* **chave:** uma string que contém a chave do cookie.
* **value:** uma string que contém o valor do cookie.
* **opções:**  (opcional) um objeto que contém qualquer uma das seguintes propriedades que configuram os atributos do cookie:

   * expira: Um valor `date` ou `number` que especifica quando o cookie expira. Um valor de data especifica o tempo absoluto de expiração. Um número (em dias) define o tempo de expiração para a hora atual mais o número. O valor padrão é `undefined`.
   * seguro: Um valor `boolean` que especifica o atributo `Secure` do cookie. O valor padrão é `false`.
   * caminho: Um valor `String` a ser usado como o atributo `Path` do cookie. O valor padrão é `undefined`.

**Retorna**

O cookie com o valor definido.

**Exemplo**

```
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### vanish(filter, options) {#vanish-filter-options}

Remove todos os cookies que correspondem a um determinado filtro. Os cookies são combinados usando a função getKeys e removidos usando a função removeItem .

**Parâmetros**

* **filter:** o  `filter` argumento a ser usado na chamada para a  `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)` função .

* **opções:** o  `options` argumento a ser usado na chamada para a  `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)` função .

**Retorna**

Essa função não retorna um valor.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

Permite vincular e desvincular funções a eventos de armazenamento do ContextHub. Acesse os objetos ContextHub.Utils.Eventing de um armazenamento usando a propriedade [eventing](/help/sites-developing/contexthub-api.md#eventing) do armazenamento.

### Funções (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, seletor) {#off-name-selector}

Desvincula uma função de um evento.

**Parâmetros**

* **name:** o  [nome do ](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) evento para o qual você está desvinculando a função.

* **seletor:** o seletor que identifica o vínculo. (Consulte o parâmetro `selector` para as funções [on](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) e [once](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents)).

**Retorna**

Essa função não retorna valor.

#### on(name, handler, seletor, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Vincula uma função a um evento. A função é chamada sempre que o evento ocorre. Como opção, a função pode ser chamada para eventos que ocorreram no passado, antes que o vínculo seja estabelecido.

**Parâmetros**

* **name:**  (String) o  [nome do ](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) evento ao qual você está vinculando a função.

* **manipulador:**  (função) a função a ser vinculada ao evento.
* **seletor:**  (cadeia de caracteres) um identificador exclusivo para a associação. Você precisa do seletor para identificar o vínculo se quiser usar a função `off` para remover o vínculo.

* **triggerForPastEvents:**  (Booleano) Indica se o manipulador deve ser executado para eventos que ocorreram no passado. Um valor `true` chama o manipulador para eventos anteriores. Um valor `false` chama o âncora para eventos futuros. O valor padrão é `true`.

**Retorna**

Quando o argumento `triggerForPastEvents` é `true`, essa função retorna um valor `boolean` que indica se o evento ocorreu no passado:

* `true`: O evento ocorreu no passado e o manipulador será chamado.
* `false`: O evento não ocorreu no passado.

Se `triggerForPastEvents` for `false`, essa função não retornará nenhum valor.

**Exemplo**

O exemplo a seguir vincula uma função ao evento de dados do armazenamento de geolocalização. A função preenche um elemento na página com o valor do item de dados de latitude da loja.

```
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(name, handler, seletor, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

Vincula uma função a um evento. A função é chamada somente uma vez, para a primeira ocorrência do evento. Como opção, a função pode ser chamada para o evento que ocorreu no passado, antes que o vínculo seja estabelecido.

**Parâmetros**

* **name:**  (String) o  [nome do ](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) evento ao qual você está vinculando a função.

* **manipulador:**  (função) a função a ser vinculada ao evento.
* **seletor:**  (cadeia de caracteres) um identificador exclusivo para a associação. Você precisa do seletor para identificar o vínculo se quiser usar a função `off` para remover o vínculo.

* **triggerForPastEvents:**  (Booleano) Indica se o manipulador deve ser executado para eventos que ocorreram no passado. Um valor `true` chama o manipulador para eventos anteriores. Um valor `false` chama o âncora para eventos futuros. O valor padrão é `true`.

**Retorna**

Quando o argumento `triggerForPastEvents` é `true`, essa função retorna um valor `boolean` que indica se o evento ocorreu no passado:

* `true`: O evento ocorreu no passado e o manipulador será chamado.
* `false`: O evento não ocorreu no passado.

Se `triggerForPastEvents` for `false`, essa função não retornará nenhum valor.

## ContextHub.Utils.herança {#contexthub-utils-inheritance}

Uma classe de utilitário que permite a um objeto herdar as propriedades e os métodos de outro objeto.

### Funções (ContextHub.Utils.hereditance) {#functions-contexthub-utils-inheritance}

#### herdar(filho, pai) {#inherit-child-parent}

Faz com que um objeto herde as propriedades e os métodos de outro objeto.

**Parâmetros**

* **child:**  (Object) o objeto que herda.
* **parent:**  (objeto) o objeto que define as propriedades e os métodos herdados.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Fornece funções para serializar objetos no formato JSON e desserializar cadeias JSON em objetos.

### Funções (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

Analisa um valor de string como JSON e o converte em um objeto javascript.

**Parâmetros**

* **dados:** um valor de string no formato JSON.

**Retorna**

Um objeto Javascript.

**Exemplo**

O código `ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");` retorna o seguinte objeto:

```
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

Serializa valores e objetos Javascript em valores de string de formato JSON.

**Parâmetros**

* **dados:** o valor ou objeto a ser serializado. Essa função suporta valores booleanos, de matriz, de número, de string e de data.

**Retorna**

O valor da string serializada. Quando `data` é um valor R `egExp`, essa função retorna um objeto vazio. Quando `data` é uma função, retorna `undefined`.

**Exemplo**

O código a seguir retorna `"{'city':'Basel','country':'Switzerland','population':'173330'}":`

```
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

Essa classe facilita a manipulação de objetos de dados que serão armazenados ou recuperados de armazenamentos do ContextHub.

### Funções (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

Cria uma cópia de um objeto de dados e adiciona a ele a árvore de dados de um segundo objeto. A função retorna a cópia e não modifica nenhum dos objetos originais. Quando as árvores de dados dos dois objetos contêm chaves idênticas, o valor do segundo objeto substitui o valor do primeiro objeto.

**Parâmetros**

* **tree:** o objeto que é copiado.
* **SecondTree:** o objeto que é unido com a cópia do  `tree` objeto.

**Retorna**

Um objeto que contém os dados unidos.

#### cleanup() {#cleanup}

Cria uma cópia de um objeto, localiza e remove itens na árvore de dados que não contêm valores, valores nulos ou valores indefinidos e retorna a cópia.

**Parâmetros**

* **árvore:** o objeto a ser limpo.

**Retorna**

Uma cópia da árvore que é limpa.

#### getItem() {#getitem}

Recupera o valor de um objeto para a chave a.

**Parâmetros**

* **árvore:** o objeto de dados.
* **key:** a chave do valor que você deseja recuperar.

**Retorna**

O valor que corresponde à chave. Quando a chave tem chaves secundárias, essa função retorna um objeto complexo. Quando o tipo do valor da chave é `undefined`, `null` é retornado.

**Exemplo**

Considere o seguinte objeto Javascript:

```
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

O código de exemplo a seguir retorna o valor `260`:

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

O código de exemplo a seguir recupera o valor de uma chave que tenha chaves secundárias:

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

A função retorna o seguinte objeto:

```
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

Recupera todas as chaves da árvore de dados de um objeto. Como opção, você pode recuperar apenas as chaves dos filhos de uma chave específica. Opcionalmente, também é possível especificar uma ordem de classificação das chaves recuperadas.

**Parâmetros**

* **árvore:** o objeto a partir do qual recuperar as chaves da árvore de dados.
* **principal:**  (opcional) a chave de um item na árvore de dados para a qual você deseja recuperar as chaves dos itens filhos.
* **order:**  (Opcional) Uma função que determina a ordem de classificação das chaves retornadas. (Consulte [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) no Mozilla Developer Network.)

**Retorna**

Uma matriz de chaves.

**Exemplo**

Considere o seguinte objeto:

```
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

O script `ContextHub.Utils.JSON.tree.getKeys(myObject);` retorna a seguinte matriz:

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Cria uma cópia de um determinado objeto, remove a ramificação especificada da árvore de dados e retorna a cópia modificada.

**Parâmetros**

* árvore: Um objeto de dados.
* chave: A chave a ser removida.

**Retorna**

Uma cópia do objeto de dados original com a chave removida.

**Exemplo**

Considere o seguinte objeto:

```
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

O script de exemplo a seguir remove a ramificação /um/dois/três/quatro da árvore de dados:

```
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

A função retorna o seguinte objeto:

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

Limpa os valores da sequência de caracteres para torná-los utilizáveis como chaves. Para limpar uma string, essa função executa as seguintes ações:

* Reduz várias barras consecutivas para a frente em uma única barra.
* Remove o espaço em branco do início e do fim da cadeia de caracteres.
* Divide o resultado em uma matriz de strings demarcadas por barras.

Use a matriz resultante para criar uma chave utilizável.  **Parâmetros**

* **chave:** o  `string` para limpar.

**Retorna**

Uma matriz de valores `string` onde cada string é a parte do `key` que foi demarcada por barras. representa a chave sanitizada. Se a matriz sanitizada tiver um comprimento de zero, essa função retornará `null`.

**Exemplo**

O código a seguir limpa uma string para produzir a matriz `["this", "is", "a", "path"]` e então gera a chave `"/this/is/a/path"` a partir da matriz:

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

Adiciona um par chave/valor à árvore de dados de uma cópia de um objeto. Para obter informações sobre árvores de dados, consulte [Persistência](/help/sites-developing/contexthub.md#persistence).

**Parâmetros**

* árvore: Um objeto de dados.
* chave: A chave para associar ao valor que você está adicionando. A chave é o caminho para o item na árvore de dados. Essa função chama `ContextHub.Utils.JSON.tree.sanitize` para limpar a chave antes de adicioná-la.
* valor: O valor a ser adicionado à árvore de dados.

**Retorna**

Uma cópia do objeto `tree` que inclui o par `key`/ `value`.

**Exemplo**

Considere o seguinte código Javascript:

```
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

O objeto myObject tem o seguinte valor:

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

Permite registrar candidatos a lojas e obter candidatos a lojas registradas.

### Funções (ContextHub.Utils.storeCandidates) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

Retorna os tipos de loja que são registrados como candidatos de loja. Recupere os predicados registrados de um tipo de armazenamento específico ou de todos os tipos de armazenamento.

**Parâmetros**

* **storeType:**  (String) o nome do tipo de armazenamento. Consulte o parâmetro `storeType` da função [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates).

**Retorna**

Um objeto de tipos de armazenamento. As propriedades do objeto são os nomes do tipo de armazenamento e os valores da propriedade são uma matriz de candidatos a armazenamento registrado.

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

Retorna um tipo de armazenamento dos candidatos registrados. Se mais de um tipo de armazenamento do mesmo nome for registrado, a função retornará o tipo de armazenamento com a prioridade mais alta.

**Parâmetros**

* storeType: (String) O nome do candidato da loja. Consulte o parâmetro `storeType` da função [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies).

**Retorna**

Um objeto que representa o candidato de armazenamento registrado. Se o Tipo de armazenamento solicitado não estiver registrado, um erro será lançado.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Retorna os nomes dos tipos de loja que estão registrados como candidatos de loja. Essa função não requer parâmetros.

**Retorna**

Uma matriz de valores da string, em que cada string é o tipo de armazenamento com o qual um candidato a loja foi registrado. Consulte o parâmetro `storeType` da função [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates).

#### registerStoreCandidate(store, storeType, priority, apply) {#registerstorecandidate-store-storetype-priority-applies}

Registra um objeto de loja como candidato de loja usando um nome e uma prioridade.

A prioridade é um número que indica a importância das lojas com mesmo nome. Quando um candidato de loja é registrado usando o mesmo nome de um candidato de loja já registrado, o candidato com prioridade mais alta é usado. Ao registrar um candidato a loja, a loja é registrada somente se a prioridade for maior que os candidatos a loja registrada com o mesmo nome.

**Parâmetros**

* **store:**  (Object) o objeto store a ser registrado como candidato de loja.
* **storeType:**  (String) o nome do candidato da loja. Esse valor é necessário ao criar uma instância do candidato de loja.
* **priority:**  (Number) A prioridade do candidato a loja.
* **se aplica:**  (Função) a função a ser chamada que avalia a aplicabilidade da loja no ambiente atual. A função deve retornar `true` se a loja for aplicável, caso contrário, `false`. O valor padrão é uma função que retorna true: `function() {return true;}`

**Exemplo**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

