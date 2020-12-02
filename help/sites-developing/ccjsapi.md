---
title: API JavaScript de contexto do cliente
seo-title: API JavaScript de contexto do cliente
description: A API do JavaScript para o contexto do cliente
seo-description: A API do JavaScript para o contexto do cliente
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '3163'
ht-degree: 4%

---


# API JavaScript de contexto do cliente{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

O objeto CQ_Analytics.ClientContextMgr é um singleton que contém um conjunto de armazenamentos de sessão autoregistrados e fornece métodos para registrar, persistir e gerenciar os armazenamentos de sessão.

Estende CQ_Analytics.PersistedSessionStore.

### Métodos {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

Retorna um armazenamento de sessão de um nome especificado. Consulte também [Acesso a um Repositório de Sessões](/help/sites-developing/client-context.md#accessing-session-stores).

**Parâmetros**

* name: String. O nome do armazenamento de sessão.

**Retorna**

Um objeto CQ_Analytics.SessionStore que representa o armazenamento de sessão do nome fornecido. Retorna `null` quando não existe nenhum armazenamento do nome fornecido.

#### register(sessionstore) {#register-sessionstore}

Registra um armazenamento de sessão com o Contexto do Cliente. Dispara os eventos de registro e atualização de armazenamento após a conclusão.

**Parâmetros**

* essionstore: CQ_Analytics.SessionStore. O objeto de repositório de sessão a ser registrado.

**Retorna**

Nenhum valor retornado.

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

Fornece métodos de acompanhamento para ativação e registro do armazenamento de sessão. Consulte também [Verificando se um Repositório de Sessões está Definido e Inicializado](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### Métodos {#methods-1}

#### onStoreInitialized(storeName, retorno de chamada, atraso) {#onstoreinitialized-storename-callback-delay}

Registra uma função de retorno de chamada que é chamada quando um armazenamento de sessão é inicializado. Para armazenamentos inicializados várias vezes, especifique um atraso de retorno de chamada para que a função de retorno de chamada seja chamada somente uma vez:

* Quando o armazenamento é inicializado durante o período de atraso de uma inicialização anterior, a chamada de função anterior é cancelada e a função é chamada novamente para a inicialização atual.
* Se o período de atraso expirar antes de ocorrer uma inicialização subsequente, a função de retorno de chamada será executada duas vezes.

Por exemplo, um armazenamento de sessão é baseado em um objeto JSON e recuperado por meio de uma solicitação JSON. Os seguintes cenários de inicialização são possíveis:

* A solicitação é concluída, os dados são recuperados e carregados no armazenamento. Nesse caso, a inicialização ocorre uma vez.
* Falha na solicitação (tempo limite). Nesse caso, a inicialização não ocorre e não há dados no armazenamento.
* O armazenamento é pré-preenchido com valores padrão (propriedades init), mas a solicitação falha (tempo limite). Há apenas uma inicialização com valores padrão.
* A loja está pré-preenchida.

Quando o atraso é definido como `true` ou um número de milissegundos, o método aguarda antes de chamar o método de retorno de chamada. Se outro evento de inicialização for acionado antes que o atraso seja passado, ele aguardará até que o tempo de atraso seja excedido sem nenhum evento de inicialização. Isso permite que a espera por um segundo evento de inicialização seja acionada e chama a função de retorno de chamada no caso mais ideal.

**Parâmetros**

* storeName: String. O nome do armazenamento de sessão para adicionar o ouvinte.
* retorno de chamada: Função. A função a ser chamada na inicialização do armazenamento.
* atraso: Booleano ou Número. A quantidade de tempo para atrasar a chamada para a função de retorno de chamada, em milissegundos. Um valor booliano de `true` usa o atraso padrão de `200 ms`. Um valor booliano de `false` ou um número negativo não faz com que nenhum atraso seja usado.

**Retorna**

Nenhum valor retornado.

#### onStoreRegistered(storeName, retorno de chamada) {#onstoreregistered-storename-callback}

Registra uma função de retorno de chamada que é chamada quando um armazenamento de sessão é registrado. O evento de registro ocorre quando uma loja está registrada em [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**Parâmetros**

* storeName: String. O nome do armazenamento de sessão para adicionar o ouvinte.
* retorno de chamada: Função. A função a ser chamada na inicialização do armazenamento.

**Retorna**

Nenhum valor retornado.

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

Um armazenamento de sessão não persistente que contém dados JSON. Os dados são recuperados de um serviço JSONP externo. Use o método `getInstance` ou `getRegisteredInstance` para criar uma instância dessa classe.

Estende CQ_Analytics.JSONStore.

### Propriedades {#properties}

Consulte CQ_Analytics.JSONStore e CQ_Analytics.SessionStore para obter as propriedades herdadas.

### Métodos {#methods-2}

Consulte também CQ_Analytics.JSONStore e CQ_Analytics.SessionStore para obter métodos herdados.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

Cria um objeto CQ_Analytics.JSONPStore.

**Parâmetros**

* storeName: String. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres de maiúsculas. Se nenhum storeName for fornecido, o método retornará null.
* serviceURL: String. O URL do serviço JSONP
* dynamicData: (Opcional) Objeto. Dados JSON a serem anexados aos dados de inicialização do armazenamento antes da função de retorno de chamada ser chamada.
* deferLoading: (Opcional) Booliano. Um valor true impede que o serviço JSONP seja chamado na criação de objetos. Um valor de false faz com que o serviço JSONP seja chamado.
* loadingCallback: (Opcional) String. O nome da função a ser chamada para o processamento do objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Retorna**

O novo objeto CQ_Analytics.JSONPStore, ou nulo se storeName for nulo.

#### getServiceURL() {#getserviceurl}

Recupera o URL do serviço JSONP que este objeto usa para recuperar dados JSON.

**Parâmetros**

Nenhum.

**Retorna**

Uma string que representa o URL do serviço, ou nulo se nenhum URL do serviço tiver sido configurado.

#### load(serviceURL, dynamicData, retorno de chamada) {#load-serviceurl-dynamicdata-callback}

Chama o serviço JSONP. O URL JSONP é o URL do serviço com um nome de função de retorno de chamada.

**Parâmetros**

* serviceURL: (Opcional) String. O serviço JSONP para ligar. Um valor nulo faz com que o URL de serviço já configurado seja usado. Um valor não nulo define o serviço JSONP a ser usado para esse objeto. (Consulte setServiceURL.)
* dynamicData: (Opcional) Objeto. Dados JSON a serem anexados aos dados de inicialização do armazenamento antes da função de retorno de chamada ser chamada.
* retorno de chamada: (Opcional) String. O nome da função a ser chamada para o processamento do objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Retorna**

Nenhum valor retornado.

#### registerNewInstance(storeName, serviceURL, dynamicData, retorno de chamada) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

Cria um objeto CQ_Analytics.JSONPStore e registra a loja com o Contexto do cliente.

**Parâmetros**

* storeName: String. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres de maiúsculas. Se nenhum storeName for fornecido, o método retornará null.
* serviceURL: (Opcional) String. O URL do serviço JSONP.
* dynamicData: (Opcional) Objeto. Dados JSON a serem anexados aos dados de inicialização do armazenamento antes da função de retorno de chamada ser chamada.
* retorno de chamada: (Opcional) String. O nome da função a ser chamada para o processamento do objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Retorna**

O objeto CQ_Analytics.JSONPStore registrado.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

Define o URL do serviço JSONP a ser usado para recuperar dados JSON.

**Parâmetros**

* serviceURL: String. O URL do serviço JSONP que fornece dados JSON

**Retorna**

Nenhum valor retornado.

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

Um container para um objeto JSON. Crie uma instância desta classe para criar um armazenamento de sessão não persistente que contenha dados JSON:

`myjsonstore = new CQ_Analytics.JSONStore`

É possível definir um conjunto de dados que preenche a loja na inicialização.

Estende CQ_Analytics.SessionStore.

### Propriedades {#properties-1}

#### STOREKEY {#storekey}

A chave que identifica a loja. Use o método `getInstance` para recuperar esse valor.

#### STORENAME {#storename}

O nome da loja. Use o método `getInstance` para recuperar esse valor.

### Métodos {#methods-3}

Consulte também CQ_Analytics.SessionStore para obter métodos herdados.

#### limpar() {#clear}

Remove os dados do armazenamento da sessão e remove todas as propriedades de inicialização.

**Parâmetros**

Nenhum.

**Retorna**

Nenhum valor retornado.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

Cria um objeto CQ_Analytics.JSONStore com um nome especificado e inicializado com os dados JSON fornecidos (chama o método initJSON).

**Parâmetros**

* storeName: String. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres de maiúsculas.
* jsonData: Objeto. Um objeto que contém dados JSON.

**Retorna**

O objeto CQ_Analytics.JSONStore.

#### getJSON() {#getjson}

Recupera os dados do armazenamento da sessão no formato JSON.

**Parâmetros**

Nenhum.

**Retorna**

Um objeto que representa os dados de armazenamento no formato JSON.

#### init() {#init}

Limpa o armazenamento da sessão e o inicializa com a propriedade initialization. Define o sinalizador de inicialização como `true` e dispara os eventos `initialize` e `update`.

**Parâmetros**

Nenhum.

**Retorna**

Nenhum dado retornado.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

Cria propriedades de inicialização a partir dos dados em um objeto JSON. Como opção, você pode remover todas as propriedades de inicialização existentes.

Os nomes das propriedades são derivados da hierarquia dos dados no objeto JSON. O código de exemplo a seguir representa um objeto JSON:

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

Neste exemplo, as seguintes propriedades são criadas na loja:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parâmetros**

* jsonData: Um objeto JSON que contém os dados a serem armazenados.
* doNotClear: Um valor de true preserva as propriedades de inicialização existentes e adiciona as derivadas do objeto JSON. Um valor de false remove as propriedades de inicialização existentes antes de adicionar as derivadas do objeto JSON.

**Retorna**

Nenhum valor retornado.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

Cria um objeto CQ_Analytics.JSONStore com um nome especificado e inicializado com os dados JSON fornecidos (chama o método initJSON). O novo objeto é registrado automaticamente no Gerenciador da Nuvem de sequência de cliques.

**Parâmetros**

* storeName: String. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres de maiúsculas.
* jsonData: Objeto. Um objeto que contém dados JSON.

**Retorna**

O objeto CQ_Analytics.JSONStore.

## CQ_Analytics.Observable {#cq-analytics-observable}

Dispara eventos e permite que outros objetos escutem esses eventos e reajam. As classes que estendem essa classe podem acionar eventos que fazem com que os ouvintes sejam chamados.

### Métodos {#methods-4}

#### addListener(evento, fct, escopo) {#addlistener-event-fct-scope}

Registra um ouvinte para um evento. Consulte também [Criar um ouvinte para reagir a uma atualização do armazenamento de sessão](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**Parâmetros**

* evento: String. O nome do evento para escutar.
* fct: Função. A função que é chamada quando o evento ocorre.
* escopo: (Opcional) Objeto. O escopo no qual executar a função handler. O contexto &quot;this&quot; da função do manipulador.

**Retorna**

Nenhum valor retornado.

#### removeListener(evento, fct) {#removelistener-event-fct}

Remove o manipulador de eventos fornecido para um evento.

**Parâmetros**

* evento: String. O nome do evento.
* fct: Função. O manipulador do evento.

**Retorna**

Nenhum valor retornado.

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

Um container persistente de um objeto JSON recuperado de um serviço JSONP remoto.

Estende CQ_Analytics.PersistedJSONStore.

### Métodos {#methods-5}

Consulte também CQ_Analytics.PersistedJSONStore para obter métodos herdados.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

Cria um objeto CQ_Analytics.PersistedJSONPStore.

**Parâmetros**

* storeName: String. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres de maiúsculas. Se nenhum storeName for fornecido, o método retornará null.
* serviceURL: String. O URL do serviço JSONP
* dynamicData: (Opcional) Objeto. Dados JSON a serem anexados aos dados de inicialização do armazenamento antes da função de retorno de chamada ser chamada.
* deferLoading: (Opcional) Booliano. Um valor true impede que o serviço JSONP seja chamado na criação de objetos. Um valor de false faz com que o serviço JSONP seja chamado.
* loadingCallback: (Opcional) String. O nome da função a ser chamada para o processamento do objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Retorna**

O novo objeto CQ_Analytics.PersistedJSONPStore, ou nulo se storeName for nulo.

#### getServiceURL() {#getserviceurl-1}

Recupera o URL do serviço JSONP que este objeto usa para recuperar dados JSON.

**Parâmetros**

Nenhum.

**Retorna**

Uma string que representa o URL do serviço, ou nulo se nenhum URL do serviço tiver sido configurado.

#### load(serviceURL, dynamicData, retorno de chamada) {#load-serviceurl-dynamicdata-callback-1}

Chama o serviço JSONP. O URL JSONP é o URL do serviço com um nome de função de retorno de chamada.

**Parâmetros**

* serviceURL: (Opcional) String. O serviço JSONP para ligar. Um valor nulo faz com que o URL de serviço já configurado seja usado. Um valor não nulo define o serviço JSONP a ser usado para esse objeto. (Consulte setServiceURL.)
* dynamicData: (Opcional) Objeto. Dados JSON a serem anexados aos dados de inicialização do armazenamento antes da função de retorno de chamada ser chamada.
* retorno de chamada: (Opcional) String. O nome da função a ser chamada para o processamento do objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Retorna**

Nenhum valor retornado.

#### registerNewInstance(storeName, serviceURL, dynamicData, retorno de chamada) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

Cria um objeto CQ_Analytics.PersistedJSONPStore e registra a loja com o Client Context.

**Parâmetros**

* storeName: String. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres de maiúsculas. Se nenhum storeName for fornecido, o método retornará null.
* serviceURL: (Opcional) String. O URL do serviço JSONP.
* dynamicData: (Opcional) Objeto. Dados JSON a serem anexados aos dados de inicialização do armazenamento antes da função de retorno de chamada ser chamada.
* retorno de chamada: (Opcional) String. O nome da função a ser chamada para o processamento do objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Retorna**

O objeto CQ_Analytics.PersistedJSONPStore registrado.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

Define o URL do serviço JSONP a ser usado para recuperar dados JSON.

**Parâmetros**

* serviceURL: String. O URL do serviço JSONP que fornece dados JSON

**Retorna**

Nenhum valor retornado.

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

Um container persistente de um objeto JSON.

Estende `CQ_Analytics.PersistedSessionStore`.

### Propriedades {#properties-2}

#### STOREKEY {#storekey-1}

A chave que identifica a loja. Use o método `getInstance` para recuperar esse valor.

#### STORENAME {#storename-1}

O nome da loja. Use o método `getInstance` para recuperar esse valor.

### Métodos {#methods-6}

Consulte também CQ_Analytics.PersistedSessionStore para obter métodos herdados.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

Cria um objeto CQ_Analytics.PersistedJSONStore com um nome especificado e inicializado com os dados JSON fornecidos (chama o método initJSON).

**Parâmetros**

* storeName: String. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres de maiúsculas.
* jsonData: Objeto. Um objeto que contém dados JSON.

**Retorna**

O objeto CQ_Analytics.PersistedJSONStore.

#### getJSON() {#getjson-1}

Recupera os dados do armazenamento da sessão no formato JSON.

**Parâmetros**

Nenhum.

**Retorna**

Um objeto que representa os dados de armazenamento no formato JSON.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

Cria propriedades de inicialização a partir dos dados em um objeto JSON. Como opção, você pode remover todas as propriedades de inicialização existentes.

Os nomes das propriedades são derivados da hierarquia dos dados no objeto JSON. O código de exemplo a seguir representa um objeto JSON:

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

Neste exemplo, as seguintes propriedades são criadas na loja:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parâmetros**

* jsonData: Um objeto JSON que contém os dados a serem armazenados.
* doNotClear: Um valor de true preserva as propriedades de inicialização existentes e adiciona as derivadas do objeto JSON. Um valor de false remove as propriedades de inicialização existentes antes de adicionar as derivadas do objeto JSON.

**Retorna**

Nenhum valor retornado.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

Cria um objeto CQ_Analytics.PersistedJSONStore com um nome especificado e inicializado com os dados JSON fornecidos (chama o método initJSON). O novo objeto é registrado automaticamente no Gerenciador de contexto do cliente.

**Parâmetros**

* storeName: String. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres de maiúsculas.
* jsonData: Objeto. Um objeto que contém dados JSON.

**Retorna**

O objeto CQ_Analytics.PersistedJSONStore.

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

Um container de propriedades e valores. Os dados são persistentes usando CQ_Analytics.SessionPersistence. Crie uma instância desta classe para criar um armazenamento de sessão persistente:

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

Estende CQ_Analytics.SessionStore.

### Propriedades {#properties-3}

#### STOREKEY {#storekey-2}

O valor padrão é `key`.

### Métodos {#methods-7}

Consulte CQ_Analytics.SessionStore para obter métodos herdados.

Quando os métodos herdados `clear`, `setProperty`, `setProperties`, `removeProperty` são usados para alterar os dados do armazenamento, as alterações são automaticamente persistentes, a menos que as propriedades alteradas sejam sinalizadas como notPersisted.

#### getStoreKey() {#getstorekey}

Recupera a propriedade `STOREKEY`.

**Parâmetros**

Nenhum

**Retorna**

O valor da propriedade `STOREKEY`.

#### isPersisted(name) {#ispersisted-name}

Determina se uma propriedade de dados é persistente.

**Parâmetros**

* name: String. O nome da propriedade.

**Retorna**

Um valor booliano de `true` se a propriedade for persistente e um valor de `false` se o valor não for uma propriedade persistente.

#### persist() {#persist}

Persiste no armazenamento da sessão. O modo de persistência padrão usa o navegador `localStorage` usando `ClientSidePersistence` como nome ( `window.localStorage.set("ClientSidePersistance", store);`)

Se localStorage não estiver disponível ou gravável, então a loja será mantida como uma propriedade da janela.

Dispara o evento `persist` após a conclusão.

**Parâmetros**

Nenhum

**Retorna**

Nenhum valor retornado.

#### reset(deferEvent) {#reset-deferevent}

Remove todas as propriedades de dados do repositório e persiste no armazenamento. Opcionalmente, não dispara o evento `udpate` após a conclusão.

**Parâmetros**

* deferEvent: Um valor true impede que o evento `update` seja acionado. Um valor de `false` faz com que o evento de atualização seja acionado.

**Retorna**

Nenhum valor retornado.

#### setNonPersisted(name) {#setnonpersisted-name}

Sinaliza uma propriedade de dados como não persistida.

**Parâmetros**

* name: String. O nome da propriedade que não deve ser persistente.

**Retorna**

Nenhum valor de retorno.

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore representa um armazenamento de sessão. Crie uma instância desta classe para criar um armazenamento de sessão:

`mystore = new CQ_Analytics.SessionStore`

Estende CQ_Analytics.Observable.

### Propriedades {#properties-4}

#### STORENAME {#storename-2}

O nome do armazenamento de sessão. Use getName para recuperar o valor dessa propriedade.

### Métodos {#methods-8}

#### addInitProperty(nome, valor) {#addinitproperty-name-value}

Adiciona uma propriedade e um valor aos dados de inicialização do armazenamento de sessão.

Use loadInitProperties para preencher os dados do armazenamento da sessão com os valores de inicialização.

**Parâmetros**

* name: String. O nome da propriedade a ser adicionada.
* valor: String. O valor da propriedade a ser adicionada.

**Retorna**

Nenhum valor retornado.

#### limpar() {#clear-1}

Remove todas as propriedades de dados do repositório.

**Parâmetros**

Nenhum.

**Retorna**

Nenhum valor de retorno.

#### getData(exclude) {#getdata-excluded}

Retorna os dados de armazenamento. Opcionalmente, exclui as propriedades de nome dos dados. Chama o método `init` se a propriedade data do armazenamento não existir.

**Parâmetros**

excluídos: (Opcional) Uma matriz de nomes de propriedade a serem excluídos dos dados retornados.

**Retorna**

Um objeto de propriedades e seus valores.

#### getInitProperty(name) {#getinitproperty-name}

Recupera o valor de uma propriedade de dados.

**Parâmetros**

* name: String. O nome da propriedade de dados a ser recuperada.

**Retorna**

O valor da propriedade data. Retorna `null` se o armazenamento de sessão não contiver nenhuma propriedade do nome fornecido.

#### getName() {#getname}

Retorna o nome do armazenamento da sessão.

**Parâmetros**

Nenhum.

**Retorna**

Um valor String que representa o nome da loja.

#### getProperty(name, raw) {#getproperty-name-raw}

Retorna o valor de uma propriedade. O valor é retornado como a propriedade bruta ou o valor filtrado por XSS. Chama o método `init` se a propriedade data do armazenamento não existir.

**Parâmetros**

* name: String. O nome da propriedade de dados a ser recuperada.
* bruto: Booleano. Um valor true faz com que o valor da propriedade bruta seja retornado. Um valor de false faz com que o valor retornado seja filtrado por XSS.

**Retorna**

O valor da propriedade data.

#### getPropertyNames(exclude) {#getpropertynames-excluded}

Retorna os nomes das propriedades que o armazenamento de sessão contém. Chama o método `init` se a propriedade data do armazenamento não existir.

**Parâmetros**

excluídos: (Opcional) Uma matriz de nomes de propriedade para omitir dos resultados.

**Retorna**

Uma matriz de valores String que representam os nomes das propriedades session.

#### getSessionStore() {#getsessionstore}

Retorna o armazenamento de sessão anexado ao objeto atual.

**Parâmetros**

Nenhum.

**Retorna**

this

#### init() {#init-1}

Marca a loja como inicializada e dispara o evento `initialize`.

**Parâmetros**

Nenhum.

**Retorna**

Nenhum valor retornado.

#### isInitialized() {#isinitialized}

Indica se o armazenamento de sessões foi inicializado.

**Parâmetros**

Nenhum.

**Retorna**

Um valor de `true` se o armazenamento for inicializado e um valor de `false` se o armazenamento não for inicializado.

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

Adiciona as propriedades de um determinado objeto aos dados de inicialização do armazenamento da sessão. Como opção, os dados do objeto também são adicionados aos dados do armazenamento.

**Parâmetros**

* obj: Um objeto que contém propriedades enumeráveis.
* setValues: Quando true, as propriedades obj são adicionadas aos dados do armazenamento da sessão se os dados do armazenamento ainda não incluírem uma propriedade com o mesmo nome. Quando falso, nenhum dado é adicionado aos dados do armazenamento da sessão.

**Retorna**

Nenhum valor retornado.

#### removeProperty(name) {#removeproperty-name}

Remove uma propriedade do armazenamento de sessão. Dispara o evento `update` após a conclusão. Chama o método `init` se a propriedade data do armazenamento não existir.

**Parâmetros**

* name: String. O nome da propriedade a ser removida.

**Retorna**

Nenhum valor retornado.

#### reset() {#reset}

Restaura os valores iniciais do armazenamento de dados. A implementação padrão simplesmente remove todos os dados. Dispara o evento `update` após a conclusão.

**Parâmetros**

Nenhum.

**Retorna**

Nenhum valor retornado.

#### setProperties(properties) {#setproperties-properties}

Define os valores de várias propriedades. Dispara o evento `update` após a conclusão. Chama o método `init` se a propriedade data do armazenamento não existir.

**Parâmetros**

* Propriedades: Objeto. Um objeto que contém propriedades enumeráveis. Cada nome e valor de propriedade é adicionado ao armazenamento.

**Retorna**

Nenhum valor retornado.

#### setProperty(name, value) {#setproperty-name-value}

Define o valor de uma propriedade. Dispara o evento `update` após a conclusão. Chama o método `init` se a propriedade data do armazenamento não existir.

**Parâmetros**

* name: String. O nome da propriedade.
* valor: String. Valor da propriedade.

**Retorna**

Nenhum valor retornado.
