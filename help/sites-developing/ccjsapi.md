---
title: API Javascript de contexto do cliente
seo-title: Client Context Javascript API
description: A API do Javascript para o contexto do cliente
seo-description: The Javascript API for Client Context
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
feature: Context Hub
exl-id: 24bdf9fc-71e6-4b99-9dad-0f41a5e36b98
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3153'
ht-degree: 4%

---

# API Javascript de contexto do cliente{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

O objeto CQ_Analytics.ClientContextMgr é um singleton que contém um conjunto de armazenamentos de sessão autoregistrados e fornece métodos para registrar, persistir e gerenciar os armazenamentos de sessão.

Estende CQ_Analytics.PersistedSessionStore.

### Métodos {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

Retorna um armazenamento de sessão com um nome especificado. Consulte também [Acessar um armazenamento de sessão](/help/sites-developing/client-context.md#accessing-session-stores).

**Parâmetros**

* name: Sequência de caracteres. O nome do armazenamento de sessão.

**Retorna**

Um objeto CQ_Analytics.SessionStore que representa o armazenamento de sessão do nome fornecido. Devoluções `null` quando não existe nenhum armazenamento do nome fornecido.

#### register(sessionstore) {#register-sessionstore}

Registra um armazenamento de sessão com o Contexto do Cliente. Aciona os eventos storeregister e storeupdate após a conclusão.

**Parâmetros**

* sessionstore: CQ_Analytics.SessionStore. O objeto do repositório de sessão a ser registrado.

**Retorna**

Nenhum valor retornado.

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

Fornece métodos de acompanhamento para ativação e registro da loja de sessões. Consulte também [Verificando se um armazenamento de sessão está definido e inicializado](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### Métodos {#methods-1}

#### onStoreInitialized(storeName, retorno de chamada, atraso) {#onstoreinitialized-storename-callback-delay}

Registra uma função de retorno de chamada que é chamada quando um armazenamento de sessão é inicializado. Para armazenamentos que são inicializados várias vezes, especifique um atraso de retorno de chamada para que a função de retorno de chamada seja chamada apenas uma vez:

* Quando o armazenamento é inicializado durante o período de atraso de uma inicialização anterior, a chamada de função anterior é cancelada e a função é chamada novamente para a inicialização atual.
* Se o período de atraso expirar antes de ocorrer uma inicialização subsequente, a função de retorno de chamada será executada duas vezes.

Por exemplo, um armazenamento de sessão é baseado em um objeto JSON e recuperado por meio de uma solicitação JSON. Os seguintes cenários de inicialização são possíveis:

* A solicitação é concluída, os dados recuperados e carregados no armazenamento. Nesse caso, a inicialização ocorre uma vez.
* A solicitação falha (tempo limite). Nesse caso, a inicialização não ocorre e não há dados no armazenamento.
* A loja é pré-preenchida com valores padrão (propriedades da inicialização), mas a solicitação falha (tempo limite). Há apenas uma inicialização com valores padrão.
* A loja é pré-preenchida.

Quando o atraso estiver definido como `true` Para um número de milissegundos, o método aguarda antes de chamar o método de retorno de chamada. Se outro evento de inicialização for acionado antes que o atraso seja passado, ele aguardará até que o tempo de atraso seja excedido sem nenhum evento de inicialização. Isso permite que a espera por que um segundo evento de inicialização seja acionado e chama a função de retorno de chamada no caso mais ideal.

**Parâmetros**

* storeName: Sequência de caracteres. O nome do armazenamento de sessão para adicionar o ouvinte.
* retorno de chamada: Função. A função a ser chamada na inicialização da loja.
* atraso: Booleano ou número. O tempo para atrasar a chamada para a função de retorno de chamada, em milissegundos. Um valor booleano de `true` usa o atraso padrão de `200 ms`. Um valor booleano de `false` ou um número negativo faz com que nenhum atraso seja usado.

**Retorna**

Nenhum valor retornado.

#### onStoreRegistered(storeName, retorno de chamada) {#onstoreregistered-storename-callback}

Registra uma função de retorno de chamada que é chamada quando um armazenamento de sessão é registrado. O evento de registro ocorre quando uma loja está registrada para [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**Parâmetros**

* storeName: Sequência de caracteres. O nome do armazenamento de sessão para adicionar o ouvinte.
* retorno de chamada: Função. A função a ser chamada na inicialização da loja.

**Retorna**

Nenhum valor retornado.

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

Um armazenamento de sessão não persistente que contém dados JSON. Os dados são recuperados de um serviço JSONP externo. Use o `getInstance` ou `getRegisteredInstance` para criar uma instância dessa classe.

Estende CQ_Analytics.JSONStore.

### Propriedades {#properties}

Consulte CQ_Analytics.JSONStore e CQ_Analytics.SessionStore para obter propriedades herdadas.

### Métodos {#methods-2}

Consulte também CQ_Analytics.JSONStore e CQ_Analytics.SessionStore para obter métodos herdados.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

Cria um objeto CQ_Analytics.JSONPStore.

**Parâmetros**

* storeName: Sequência de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido para storeName com todos os caracteres em maiúsculas. Se nenhum storeName for fornecido, o método retornará null.
* serviceURL: Sequência de caracteres. O URL do serviço JSONP
* dynamicData: (Opcional) Objeto. Dados JSON a serem anexados aos dados de inicialização do armazenamento antes da chamada da função de retorno de chamada.
* deferLoading: (Opcional) Booleano. Um valor true impede que o serviço JSONP seja chamado na criação do objeto. Um valor false faz com que o serviço JSONP seja chamado.
* loadingCallback: (Opcional) String. O nome da função a ser chamada para o processamento do objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Retorna**

O novo objeto CQ_Analytics.JSONPStore ou nulo se storeName for nulo.

#### getServiceURL() {#getserviceurl}

Recupera o URL do serviço JSONP que este objeto usa para recuperar dados JSON.

**Parâmetros**

Nenhum.

**Retorna**

Uma String que representa o URL do serviço ou nulo se nenhum URL de serviço tiver sido configurado.

#### load(serviceURL, dynamicData, retorno de chamada) {#load-serviceurl-dynamicdata-callback}

Chama o serviço JSONP. O URL JSONP é o sufixo do URL de serviço com um nome de função de retorno de chamada.

**Parâmetros**

* serviceURL: (Opcional) String. O serviço JSONP a ser chamado. Um valor nulo faz com que o URL de serviço já configurado seja usado. Um valor não nulo define o serviço JSONP a ser usado para esse objeto. (Consulte setServiceURL.)
* dynamicData: (Opcional) Objeto. Dados JSON a serem anexados aos dados de inicialização do armazenamento antes da chamada da função de retorno de chamada.
* retorno de chamada: (Opcional) String. O nome da função a ser chamada para o processamento do objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Retorna**

Nenhum valor retornado.

#### registerNewInstance(storeName, serviceURL, dynamicData, retorno de chamada) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

Cria um objeto CQ_Analytics.JSONPStore e registra a loja no Contexto do Cliente.

**Parâmetros**

* storeName: Sequência de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido para storeName com todos os caracteres em maiúsculas. Se nenhum storeName for fornecido, o método retornará null.
* serviceURL: (Opcional) String. O URL do serviço JSONP.
* dynamicData: (Opcional) Objeto. Dados JSON a serem anexados aos dados de inicialização do armazenamento antes da chamada da função de retorno de chamada.
* retorno de chamada: (Opcional) String. O nome da função a ser chamada para o processamento do objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Retorna**

O objeto CQ_Analytics.JSONPStore registrado.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

Define o URL do serviço JSONP a ser usado para recuperar dados JSON.

**Parâmetros**

* serviceURL: Sequência de caracteres. O URL do serviço JSONP que fornece dados JSON

**Retorna**

Nenhum valor retornado.

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

Um contêiner para um objeto JSON. Crie uma instância dessa classe para criar um armazenamento de sessão não persistente que contenha dados JSON:

`myjsonstore = new CQ_Analytics.JSONStore`

Você pode definir um conjunto de dados que preenche a loja na inicialização.

Estende CQ_Analytics.SessionStore.

### Propriedades {#properties-1}

#### STOREKEY {#storekey}

A chave que identifica a loja. Use o `getInstance` para recuperar esse valor.

#### STORENAME {#storename}

O nome da loja. Use o `getInstance` para recuperar esse valor.

### Métodos {#methods-3}

Consulte também CQ_Analytics.SessionStore para obter métodos herdados.

#### limpar() {#clear}

Remove os dados do armazenamento da sessão e remove todas as propriedades de inicialização.

**Parâmetros**

Nenhum.

**Retorna**

Nenhum valor retornado.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

Cria um objeto CQ_Analytics.JSONStore com um determinado nome e inicializado com os dados JSON fornecidos (chama o método initJSON).

**Parâmetros**

* storeName: Sequência de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido para storeName com todos os caracteres em maiúsculas.
* jsonData: Objeto. Um objeto que contém dados JSON.

**Retorna**

O objeto CQ_Analytics.JSONStore.

#### getJSON() {#getjson}

Recupera os dados do armazenamento da sessão no formato JSON.

**Parâmetros**

Nenhum.

**Retorna**

Um objeto que representa os dados do armazenamento no formato JSON.

#### init() {#init}

Apaga o armazenamento de sessão e o inicializa com a propriedade de inicialização. Define o sinalizador de inicialização como `true` e, em seguida, dispara o `initialize` e `update` eventos.

**Parâmetros**

Nenhum.

**Retorna**

Nenhum dado retornado.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

Cria propriedades de inicialização a partir dos dados em um objeto JSON. Opcionalmente, é possível remover todas as propriedades de inicialização existentes.

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
* doNotClear: Um valor true preserva as propriedades de inicialização existentes e adiciona as derivadas do objeto JSON. Um valor false remove as propriedades de inicialização existentes antes de adicionar aquelas derivadas do objeto JSON.

**Retorna**

Nenhum valor retornado.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

Cria um objeto CQ_Analytics.JSONStore com um determinado nome e inicializado com os dados JSON fornecidos (chama o método initJSON). O novo objeto é registrado automaticamente no Clickstream Cloud Manager.

**Parâmetros**

* storeName: Sequência de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido para storeName com todos os caracteres em maiúsculas.
* jsonData: Objeto. Um objeto que contém dados JSON.

**Retorna**

O objeto CQ_Analytics.JSONStore.

## CQ_Analytics.Observable {#cq-analytics-observable}

Aciona eventos e permite que outros objetos ouçam esses eventos e reajam. As classes que estendem essa classe podem disparar eventos que fazem com que os ouvintes sejam chamados.

### Métodos {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

Registra um ouvinte para um evento. Consulte também [Criando um ouvinte para reagir a uma atualização do armazenamento de sessão](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**Parâmetros**

* evento: Sequência de caracteres. O nome do evento que será escutado.
* fct: Função. A função que é chamada quando o evento ocorre.
* escopo: (Opcional) Objeto. O escopo no qual executar a função do manipulador. O contexto &quot;this&quot; da função de manipulador.

**Retorna**

Nenhum valor retornado.

#### removeListener(event, fct) {#removelistener-event-fct}

Remove o manipulador de eventos fornecido para um evento.

**Parâmetros**

* evento: Sequência de caracteres. O nome do evento.
* fct: Função. O manipulador de eventos.

**Retorna**

Nenhum valor retornado.

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

Um contêiner persistente de um objeto JSON recuperado de um serviço JSONP remoto.

Estende CQ_Analytics.PersistedJSONStore.

### Métodos {#methods-5}

Consulte também CQ_Analytics.PersistedJSONStore para obter métodos herdados.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

Cria um objeto CQ_Analytics.PersistedJSONPStore.

**Parâmetros**

* storeName: Sequência de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido para storeName com todos os caracteres em maiúsculas. Se nenhum storeName for fornecido, o método retornará null.
* serviceURL: Sequência de caracteres. O URL do serviço JSONP
* dynamicData: (Opcional) Objeto. Dados JSON a serem anexados aos dados de inicialização do armazenamento antes da chamada da função de retorno de chamada.
* deferLoading: (Opcional) Booleano. Um valor true impede que o serviço JSONP seja chamado na criação do objeto. Um valor false faz com que o serviço JSONP seja chamado.
* loadingCallback: (Opcional) String. O nome da função a ser chamada para o processamento do objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Retorna**

O novo objeto CQ_Analytics.PersistedJSONPStore ou nulo se storeName for nulo.

#### getServiceURL() {#getserviceurl-1}

Recupera o URL do serviço JSONP que este objeto usa para recuperar dados JSON.

**Parâmetros**

Nenhum.

**Retorna**

Uma String que representa o URL do serviço ou nulo se nenhum URL de serviço tiver sido configurado.

#### load(serviceURL, dynamicData, retorno de chamada) {#load-serviceurl-dynamicdata-callback-1}

Chama o serviço JSONP. O URL JSONP é o sufixo do URL de serviço com um nome de função de retorno de chamada.

**Parâmetros**

* serviceURL: (Opcional) String. O serviço JSONP a ser chamado. Um valor nulo faz com que o URL de serviço já configurado seja usado. Um valor não nulo define o serviço JSONP a ser usado para esse objeto. (Consulte setServiceURL.)
* dynamicData: (Opcional) Objeto. Dados JSON a serem anexados aos dados de inicialização do armazenamento antes da chamada da função de retorno de chamada.
* retorno de chamada: (Opcional) String. O nome da função a ser chamada para o processamento do objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Retorna**

Nenhum valor retornado.

#### registerNewInstance(storeName, serviceURL, dynamicData, retorno de chamada) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

Cria um objeto CQ_Analytics.PersistedJSONPStore e registra o armazenamento no Contexto do Cliente.

**Parâmetros**

* storeName: Sequência de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido para storeName com todos os caracteres em maiúsculas. Se nenhum storeName for fornecido, o método retornará null.
* serviceURL: (Opcional) String. O URL do serviço JSONP.
* dynamicData: (Opcional) Objeto. Dados JSON a serem anexados aos dados de inicialização do armazenamento antes da chamada da função de retorno de chamada.
* retorno de chamada: (Opcional) String. O nome da função a ser chamada para o processamento do objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Retorna**

O objeto CQ_Analytics.PersistedJSONPStore registrado.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

Define o URL do serviço JSONP a ser usado para recuperar dados JSON.

**Parâmetros**

* serviceURL: Sequência de caracteres. O URL do serviço JSONP que fornece dados JSON

**Retorna**

Nenhum valor retornado.

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

Um contêiner persistente de um objeto JSON.

Estende `CQ_Analytics.PersistedSessionStore`.

### Propriedades {#properties-2}

#### STOREKEY {#storekey-1}

A chave que identifica a loja. Use o `getInstance` para recuperar esse valor.

#### STORENAME {#storename-1}

O nome da loja. Use o `getInstance` para recuperar esse valor.

### Métodos {#methods-6}

Consulte também CQ_Analytics.PersistedSessionStore para obter métodos herdados.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

Cria um objeto CQ_Analytics.PersistedJSONStore com um determinado nome e inicializado com os dados JSON fornecidos (chama o método initJSON).

**Parâmetros**

* storeName: Sequência de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido para storeName com todos os caracteres em maiúsculas.
* jsonData: Objeto. Um objeto que contém dados JSON.

**Retorna**

O objeto CQ_Analytics.PersistedJSONStore .

#### getJSON() {#getjson-1}

Recupera os dados do armazenamento da sessão no formato JSON.

**Parâmetros**

Nenhum.

**Retorna**

Um objeto que representa os dados do armazenamento no formato JSON.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

Cria propriedades de inicialização a partir dos dados em um objeto JSON. Opcionalmente, é possível remover todas as propriedades de inicialização existentes.

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
* doNotClear: Um valor true preserva as propriedades de inicialização existentes e adiciona as derivadas do objeto JSON. Um valor false remove as propriedades de inicialização existentes antes de adicionar aquelas derivadas do objeto JSON.

**Retorna**

Nenhum valor retornado.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

Cria um objeto CQ_Analytics.PersistedJSONStore com um determinado nome e inicializado com os dados JSON fornecidos (chama o método initJSON). O novo objeto é registrado automaticamente no Gerenciador de Contexto do Cliente.

**Parâmetros**

* storeName: Sequência de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido para storeName com todos os caracteres em maiúsculas.
* jsonData: Objeto. Um objeto que contém dados JSON.

**Retorna**

O objeto CQ_Analytics.PersistedJSONStore .

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

Um contêiner de propriedades e valores. Os dados são mantidos usando CQ_Analytics.SessionPersistence. Crie uma instância dessa classe para criar um armazenamento de sessão persistente:

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

Estende CQ_Analytics.SessionStore.

### Propriedades {#properties-3}

#### STOREKEY {#storekey-2}

O valor padrão é `key`.

### Métodos {#methods-7}

Consulte CQ_Analytics.SessionStore para obter métodos herdados.

Quando os métodos herdados `clear`, `setProperty`, `setProperties`, `removeProperty` são usadas para alterar os dados do armazenamento, as alterações são automaticamente persistentes, a menos que as propriedades alteradas sejam sinalizadas como notPersisted.

#### getStoreKey() {#getstorekey}

Recupera o `STOREKEY` propriedade.

**Parâmetros**

Nenhum

**Retorna**

O valor da variável `STOREKEY` propriedade.

#### isPersisted(name) {#ispersisted-name}

Determina se uma propriedade de dados é persistente.

**Parâmetros**

* name: Sequência de caracteres. O nome da propriedade.

**Retorna**

Um valor booleano de `true` se a propriedade for persistente e um valor de `false` se o valor não for uma propriedade persistente.

#### persist() {#persist}

Persiste no armazenamento da sessão. O modo de persistência padrão usa o navegador `localStorage` usar `ClientSidePersistence` como o nome ( `window.localStorage.set("ClientSidePersistance", store);`)

Se localStorage não estiver disponível ou gravável, o armazenamento será mantido como uma propriedade da janela.

Aciona o `persist` após a conclusão.

**Parâmetros**

Nenhum

**Retorna**

Nenhum valor retornado.

#### reset(deferEvent) {#reset-deferevent}

Remove todas as propriedades de dados do armazenamento e mantém o armazenamento. Opcionalmente, não dispara a variável `udpate` após a conclusão.

**Parâmetros**

* deferEvent: Um valor de true impede que a variável `update` de ser acionado. Um valor de `false` O faz com que o evento de atualização seja acionado.

**Retorna**

Nenhum valor retornado.

#### setNonPersisted(name) {#setnonpersisted-name}

Sinaliza uma propriedade de dados como não persistente.

**Parâmetros**

* name: Sequência de caracteres. O nome da propriedade que não deve ser mantida.

**Retorna**

Nenhum valor de retorno.

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore representa um armazenamento de sessão. Crie uma instância dessa classe para criar um armazenamento de sessão:

`mystore = new CQ_Analytics.SessionStore`

Estende CQ_Analytics.Observable.

### Propriedades {#properties-4}

#### STORENAME {#storename-2}

O nome do armazenamento de sessão. Use getName para recuperar o valor dessa propriedade.

### Métodos {#methods-8}

#### addInitProperty(name, value) {#addinitproperty-name-value}

Adiciona uma propriedade e um valor aos dados de inicialização do repositório de sessão.

Use loadInitProperties para preencher os dados do repositório de sessão com os valores de inicialização.

**Parâmetros**

* name: Sequência de caracteres. O nome da propriedade a ser adicionada.
* valor: Sequência de caracteres. O valor da propriedade a ser adicionada.

**Retorna**

Nenhum valor retornado.

#### limpar() {#clear-1}

Remove todas as propriedades de dados do armazenamento.

**Parâmetros**

Nenhum.

**Retorna**

Nenhum valor de retorno.

#### getData(excluded) {#getdata-excluded}

Retorna os dados de armazenamento. Opcionalmente, exclui propriedades de nomes dos dados. Chama a `init` se a propriedade de dados do armazenamento não existir.

**Parâmetros**

excluídos: (Opcional) Uma matriz de nomes de propriedade a serem excluídos dos dados retornados.

**Retorna**

Um objeto de propriedades e seus valores.

#### getInitProperty(name) {#getinitproperty-name}

Recupera o valor de uma propriedade de dados.

**Parâmetros**

* name: Sequência de caracteres. O nome da propriedade de dados a ser recuperada.

**Retorna**

O valor da propriedade de dados. Devoluções `null` se o armazenamento de sessão não contiver nenhuma propriedade do nome fornecido.

#### getName() {#getname}

Retorna o nome do armazenamento da sessão.

**Parâmetros**

Nenhum.

**Retorna**

Um valor String que representa o nome do armazenamento.

#### getProperty(name, raw) {#getproperty-name-raw}

Retorna o valor de uma propriedade. O valor é retornado como a propriedade bruta ou o valor filtrado por XSS. Chama a `init` se a propriedade de dados do armazenamento não existir.

**Parâmetros**

* name: Sequência de caracteres. O nome da propriedade de dados a ser recuperada.
* bruto: Booleano. Um valor true faz com que o valor da propriedade bruta seja retornado. Um valor false faz com que o valor retornado seja filtrado por XSS.

**Retorna**

O valor da propriedade de dados.

#### getPropertyNames(excluded) {#getpropertynames-excluded}

Retorna os nomes das propriedades que o armazenamento de sessão contém. Chama a `init` se a propriedade de dados do armazenamento não existir.

**Parâmetros**

excluídos: (Opcional) Uma matriz de nomes de propriedade para omitir dos resultados.

**Retorna**

Uma matriz de valores de String que representam os nomes de propriedade da sessão.

#### getSessionStore() {#getsessionstore}

Retorna o armazenamento de sessão anexado ao objeto atual.

**Parâmetros**

Nenhum.

**Retorna**

this

#### init() {#init-1}

Marca o armazenamento como inicializado e dispara o `initialize` evento.

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

Adiciona as propriedades de um determinado objeto aos dados de inicialização do armazenamento de sessão. Opcionalmente, os dados do objeto também serão adicionados aos dados do armazenamento.

**Parâmetros**

* obj: Um objeto que contém propriedades enumeráveis.
* setValues: Quando verdadeiro, as propriedades do objeto são adicionadas aos dados do armazenamento da sessão se os dados do armazenamento ainda não incluírem uma propriedade do mesmo nome. Quando falso, nenhum dado é adicionado aos dados do armazenamento da sessão.

**Retorna**

Nenhum valor retornado.

#### removeProperty(name) {#removeproperty-name}

Remove uma propriedade do armazenamento de sessão. Aciona o `update` após a conclusão. Chama a `init` se a propriedade de dados do armazenamento não existir.

**Parâmetros**

* name: Sequência de caracteres. O nome da propriedade a ser removida.

**Retorna**

Nenhum valor retornado.

#### reset() {#reset}

Restaura os valores iniciais do armazenamento de dados. A implementação padrão simplesmente remove todos os dados. Aciona o `update` após a conclusão.

**Parâmetros**

Nenhum.

**Retorna**

Nenhum valor retornado.

#### setProperties(properties) {#setproperties-properties}

Define os valores de várias propriedades. Aciona o `update` após a conclusão. Chama a `init` se a propriedade de dados do armazenamento não existir.

**Parâmetros**

* Propriedades: Objeto. Um objeto que contém propriedades enumeráveis. Cada nome e valor de propriedade é adicionado ao armazenamento.

**Retorna**

Nenhum valor retornado.

#### setProperty(name, value) {#setproperty-name-value}

Define o valor de uma propriedade. Aciona o `update` após a conclusão. Chama a `init` se a propriedade de dados do armazenamento não existir.

**Parâmetros**

* name: Sequência de caracteres. O nome da propriedade.
* valor: Sequência de caracteres. Valor da propriedade.

**Retorna**

Nenhum valor retornado.
