---
title: API Javascript do Client Context
seo-title: Client Context Javascript API
description: A API do Javascript para o Contexto do cliente
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
ht-degree: 2%

---

# API Javascript do Client Context{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

O objeto CQ_Analytics.ClientContextMgr é um singleton que contém um conjunto de armazenamentos de sessão registrados automaticamente e fornece métodos para registrar, persistir e gerenciar os armazenamentos de sessão.

Estende CQ_Analytics.PersistedSessionStore.

### Métodos {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

Retorna um armazenamento de sessão de um nome especificado. Consulte também [Acessar um armazenamento de sessão](/help/sites-developing/client-context.md#accessing-session-stores).

**Parâmetros**

* name: string. O nome do armazenamento de sessão.

**Devoluções**

Um objeto CQ_Analytics.SessionStore que representa o armazenamento de sessão do nome fornecido. Devoluções `null` quando não existe armazenamento com o nome fornecido.

#### register(sessionstore) {#register-sessionstore}

Registra um armazenamento de sessão com o Client Context. Aciona os eventos storeregister e storeupdate após a conclusão.

**Parâmetros**

* sessionstore: CQ_Analytics.SessionStore. O objeto de repositório de sessão a ser registrado.

**Devoluções**

Nenhum valor retornado.

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

Fornece métodos para escuta da ativação e registro do armazenamento de sessão. Consulte também [Verificando se um Armazenamento de Sessão está Definido e Inicializado](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### Métodos {#methods-1}

#### onStoreInitialized(storeName, retorno de chamada, atraso) {#onstoreinitialized-storename-callback-delay}

Registra uma função de retorno de chamada que é chamada quando um armazenamento de sessão é inicializado. Para lojas inicializadas várias vezes, especifique um atraso de retorno de chamada para que a função de retorno de chamada seja chamada apenas uma vez:

* Quando o armazenamento é inicializado durante o período de atraso de uma inicialização anterior, a chamada de função anterior é cancelada e a função é chamada novamente para a inicialização atual.
* Se o período de atraso ocorrer antes de uma inicialização subsequente, a função de retorno de chamada será executada duas vezes.

Por exemplo, um armazenamento de sessão é baseado em um objeto JSON e recuperado por uma solicitação JSON. Os seguintes cenários de inicialização são possíveis:

* A solicitação é concluída, os dados são recuperados e carregados no armazenamento. Nesse caso, a inicialização ocorre uma vez.
* A solicitação falha (tempo limite). Nesse caso, a inicialização não ocorre e não há dados no armazenamento.
* O armazenamento é pré-preenchido com valores padrão (propriedades init), mas a solicitação falha (tempo limite). Há apenas uma inicialização com valores padrão.
* O armazenamento é preenchido previamente

Quando o atraso estiver definido como `true` Para um número de milissegundos, o método aguarda antes de chamar o método de retorno de chamada. Se outro evento de inicialização for acionado antes que o atraso seja passado, ele aguardará até que o tempo de atraso seja excedido sem nenhum evento de inicialização. Isso permite aguardar um segundo evento de inicialização ser acionado e chama a função de retorno de chamada no caso ideal.

**Parâmetros**

* storeName: cadeia de caracteres. O nome do armazenamento de sessão para adicionar o listener.
* callback: Função. A função a ser chamada na inicialização de armazenamento.
* delay: Booleano ou número. O tempo de atraso da chamada para a função de retorno de chamada, em milissegundos. Um valor booleano de `true` usa o atraso padrão de `200 ms`. Um valor booleano de `false` ou um número negativo faz com que nenhum atraso seja usado.

**Devoluções**

Nenhum valor retornado.

#### onStoreRegistered(storeName, retorno de chamada) {#onstoreregistered-storename-callback}

Registra uma função de retorno de chamada que é chamada quando um armazenamento de sessão é registrado. O evento register ocorre quando um armazenamento é registrado para [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**Parâmetros**

* storeName: cadeia de caracteres. O nome do armazenamento de sessão para adicionar o listener.
* callback: Função. A função a ser chamada na inicialização de armazenamento.

**Devoluções**

Nenhum valor retornado.

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

Um armazenamento de sessão não persistente que contém dados JSON. Os dados são recuperados de um serviço JSONP externo. Use o `getInstance` ou `getRegisteredInstance` para criar uma ocorrência dessa classe.

Estende CQ_Analytics.JSONStore.

### Propriedades {#properties}

Consulte CQ_Analytics.JSONStore e CQ_Analytics.SessionStore para propriedades herdadas.

### Métodos {#methods-2}

Consulte também CQ_Analytics.JSONStore e CQ_Analytics.SessionStore para obter os métodos herdados.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

Cria um objeto CQ_Analytics.JSONPStore.

**Parâmetros**

* storeName: cadeia de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres em maiúsculas. Se nenhum storeName for fornecido, o método retornará null.
* serviceURL: string. O URL do serviço JSONP
* dynamicData: objeto (opcional). Dados JSON a serem anexados aos dados de inicialização do armazenamento antes que a função de retorno de chamada seja chamada.
* deferLoading: (opcional) booleano. Um valor true impede que o serviço JSONP seja chamado na criação do objeto. Um valor false faz com que o serviço JSONP seja chamado.
* loadingCallback: (opcional) cadeia de caracteres. O nome da função a ser chamada para processar o objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Devoluções**

O novo objeto CQ_Analytics.JSONPStore ou nulo se storeName for nulo.

#### getServiceURL() {#getserviceurl}

Recupera o URL do serviço JSONP que esse objeto usa para recuperar dados JSON.

**Parâmetros**

Nenhum.

**Devoluções**

Uma String que representa o URL de serviço ou nulo se nenhum URL de serviço tiver sido configurado.

#### load(serviceURL, dynamicData, retorno de chamada) {#load-serviceurl-dynamicdata-callback}

Chama o serviço JSONP. O URL JSONP é o URL de serviço sufixado com um determinado nome de função de retorno de chamada.

**Parâmetros**

* serviceURL: (opcional) string. O serviço JSONP a ser chamado. Um valor nulo faz com que a URL de serviço já configurada seja usada. Um valor não nulo define o serviço JSONP a ser usado para esse objeto. (Consulte setServiceURL.)
* dynamicData: objeto (opcional). Dados JSON a serem anexados aos dados de inicialização do armazenamento antes que a função de retorno de chamada seja chamada.
* callback: (Opcional) String. O nome da função a ser chamada para processar o objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Devoluções**

Nenhum valor retornado.

#### registerNewInstance(storeName, serviceURL, dynamicData, retorno de chamada) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

Cria um objeto CQ_Analytics.JSONPStore e registra o armazenamento com o Client Context.

**Parâmetros**

* storeName: cadeia de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres em maiúsculas. Se nenhum storeName for fornecido, o método retornará null.
* serviceURL: (opcional) string. O URL do serviço JSONP.
* dynamicData: objeto (opcional). Dados JSON a serem anexados aos dados de inicialização do armazenamento antes que a função de retorno de chamada seja chamada.
* callback: (Opcional) String. O nome da função a ser chamada para processar o objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Devoluções**

O objeto CQ_Analytics.JSONPStore registrado.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

Define o URL do serviço JSONP a ser usado para recuperar dados JSON.

**Parâmetros**

* serviceURL: string. O URL do serviço JSONP que fornece dados JSON

**Devoluções**

Nenhum valor retornado.

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

Um contêiner para um objeto JSON. Crie uma instância dessa classe para criar um armazenamento de sessão não persistente que contenha dados JSON:

`myjsonstore = new CQ_Analytics.JSONStore`

Você pode definir um conjunto de dados que preencha o armazenamento na inicialização.

Estende CQ_Analytics.SessionStore.

### Propriedades {#properties-1}

#### STOREKEY {#storekey}

A chave que identifica o armazenamento. Use o `getInstance` para recuperar esse valor.

#### STORENAME {#storename}

O nome do armazenamento. Use o `getInstance` para recuperar esse valor.

### Métodos {#methods-3}

Consulte também CQ_Analytics.SessionStore para ver os métodos herdados.

#### limpar() {#clear}

Remove os dados do repositório de sessão e remove todas as propriedades de inicialização.

**Parâmetros**

Nenhum.

**Devoluções**

Nenhum valor retornado.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

Cria um objeto CQ_Analytics.JSONStore com um determinado nome e inicializado com os dados JSON fornecidos (chama o método initJSON).

**Parâmetros**

* storeName: cadeia de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres em maiúsculas.
* jsonData: objeto. Um objeto que contém dados JSON.

**Devoluções**

O objeto CQ_Analytics.JSONStore.

#### getJSON() {#getjson}

Recupera os dados do armazenamento de sessão no formato JSON.

**Parâmetros**

Nenhum.

**Devoluções**

Um objeto que representa os dados do armazenamento no formato JSON.

#### init() {#init}

Limpa o armazenamento de sessão e o inicializa com a propriedade de inicialização. Define o sinalizador de inicialização como `true` e, em seguida, aciona o `initialize` e `update` eventos.

**Parâmetros**

Nenhum.

**Devoluções**

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

Neste exemplo, as seguintes propriedades são criadas no armazenamento:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parâmetros**

* jsonData: um objeto JSON que contém os dados a serem armazenados.
* doNotClear: um valor true preserva as propriedades de inicialização existentes e adiciona as derivadas do objeto JSON. Um valor false remove as propriedades de inicialização existentes antes de adicionar as derivadas do objeto JSON.

**Devoluções**

Nenhum valor retornado.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

Cria um objeto CQ_Analytics.JSONStore com um determinado nome e inicializado com os dados JSON fornecidos (chama o método initJSON). O novo objeto é registrado automaticamente com o Clickstream Cloud Manager.

**Parâmetros**

* storeName: cadeia de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres em maiúsculas.
* jsonData: objeto. Um objeto que contém dados JSON.

**Devoluções**

O objeto CQ_Analytics.JSONStore.

## CQ_Analytics.Observable {#cq-analytics-observable}

Aciona eventos e permite que outros objetos ouçam esses eventos e reajam. As classes que estendem essa classe podem acionar eventos que fazem com que os ouvintes sejam chamados.

### Métodos {#methods-4}

#### addListener(evento, fato, escopo) {#addlistener-event-fct-scope}

Registra um ouvinte para um evento. Consulte também [Criando um Listener para Reagir a uma Atualização de Repositório de Sessão](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**Parâmetros**

* event: String. O nome do evento a ser escutado.
* fato: função. A função chamada quando o evento ocorre.
* escopo: (opcional) objeto. O escopo no qual executar a função de manipulador. O contexto &quot;this&quot; da função do manipulador.

**Devoluções**

Nenhum valor retornado.

#### removeListener(evento, fato) {#removelistener-event-fct}

Remove o manipulador de eventos fornecido para um evento.

**Parâmetros**

* event: String. O nome do evento.
* fato: função. O manipulador de eventos.

**Devoluções**

Nenhum valor retornado.

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

Um contêiner persistente de um objeto JSON recuperado de um serviço JSONP remoto.

Estende CQ_Analytics.PersistedJSONStore.

### Métodos {#methods-5}

Consulte também CQ_Analytics.PersistedJSONStore para métodos herdados.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

Cria um objeto CQ_Analytics.PersistedJSONPStore.

**Parâmetros**

* storeName: cadeia de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres em maiúsculas. Se nenhum storeName for fornecido, o método retornará null.
* serviceURL: string. O URL do serviço JSONP
* dynamicData: objeto (opcional). Dados JSON a serem anexados aos dados de inicialização do armazenamento antes que a função de retorno de chamada seja chamada.
* deferLoading: (opcional) booleano. Um valor true impede que o serviço JSONP seja chamado na criação do objeto. Um valor false faz com que o serviço JSONP seja chamado.
* loadingCallback: (opcional) cadeia de caracteres. O nome da função a ser chamada para processar o objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Devoluções**

O novo objeto CQ_Analytics.PersistedJSONPStore ou nulo se storeName for nulo.

#### getServiceURL() {#getserviceurl-1}

Recupera o URL do serviço JSONP que esse objeto usa para recuperar dados JSON.

**Parâmetros**

Nenhum.

**Devoluções**

Uma String que representa o URL de serviço ou nulo se nenhum URL de serviço tiver sido configurado.

#### load(serviceURL, dynamicData, retorno de chamada) {#load-serviceurl-dynamicdata-callback-1}

Chama o serviço JSONP. O URL JSONP é o URL de serviço sufixado com um determinado nome de função de retorno de chamada.

**Parâmetros**

* serviceURL: (opcional) string. O serviço JSONP a ser chamado. Um valor nulo faz com que a URL de serviço já configurada seja usada. Um valor não nulo define o serviço JSONP a ser usado para esse objeto. (Consulte setServiceURL.)
* dynamicData: objeto (opcional). Dados JSON a serem anexados aos dados de inicialização do armazenamento antes que a função de retorno de chamada seja chamada.
* callback: (Opcional) String. O nome da função a ser chamada para processar o objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Devoluções**

Nenhum valor retornado.

#### registerNewInstance(storeName, serviceURL, dynamicData, retorno de chamada) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

Cria um objeto CQ_Analytics.PersistedJSONPStore e registra o armazenamento no Contexto do Cliente.

**Parâmetros**

* storeName: cadeia de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres em maiúsculas. Se nenhum storeName for fornecido, o método retornará null.
* serviceURL: (opcional) string. O URL do serviço JSONP.
* dynamicData: objeto (opcional). Dados JSON a serem anexados aos dados de inicialização do armazenamento antes que a função de retorno de chamada seja chamada.
* callback: (Opcional) String. O nome da função a ser chamada para processar o objeto JSONP retornado pelo serviço JSONP. A função de retorno de chamada deve definir um único parâmetro que seja um objeto CQ_Analytics.JSONPStore.

**Devoluções**

O objeto CQ_Analytics.PersistedJSONPStore registrado.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

Define o URL do serviço JSONP a ser usado para recuperar dados JSON.

**Parâmetros**

* serviceURL: string. O URL do serviço JSONP que fornece dados JSON

**Devoluções**

Nenhum valor retornado.

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

Um container persistente de um objeto JSON.

Estende `CQ_Analytics.PersistedSessionStore`.

### Propriedades {#properties-2}

#### STOREKEY {#storekey-1}

A chave que identifica o armazenamento. Use o `getInstance` para recuperar esse valor.

#### STORENAME {#storename-1}

O nome do armazenamento. Use o `getInstance` para recuperar esse valor.

### Métodos {#methods-6}

Consulte também CQ_Analytics.PersistedSessionStore para ver os métodos herdados.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

Cria um objeto CQ_Analytics.PersistedJSONStore com um determinado nome e inicializado com os dados JSON fornecidos (chama o método initJSON).

**Parâmetros**

* storeName: cadeia de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres em maiúsculas.
* jsonData: objeto. Um objeto que contém dados JSON.

**Devoluções**

O objeto CQ_Analytics.PersistedJSONStore.

#### getJSON() {#getjson-1}

Recupera os dados do armazenamento de sessão no formato JSON.

**Parâmetros**

Nenhum.

**Devoluções**

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

Neste exemplo, as seguintes propriedades são criadas no armazenamento:

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Parâmetros**

* jsonData: um objeto JSON que contém os dados a serem armazenados.
* doNotClear: um valor true preserva as propriedades de inicialização existentes e adiciona as derivadas do objeto JSON. Um valor false remove as propriedades de inicialização existentes antes de adicionar as derivadas do objeto JSON.

**Devoluções**

Nenhum valor retornado.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

Cria um objeto CQ_Analytics.PersistedJSONStore com um determinado nome e inicializado com os dados JSON fornecidos (chama o método initJSON). O novo objeto é registrado automaticamente com o Client Context Manager.

**Parâmetros**

* storeName: cadeia de caracteres. O nome a ser usado como a propriedade STORENAME. O valor da propriedade STOREKEY é definido como storeName com todos os caracteres em maiúsculas.
* jsonData: objeto. Um objeto que contém dados JSON.

**Devoluções**

O objeto CQ_Analytics.PersistedJSONStore.

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

Um container de propriedades e valores. Os dados são mantidos usando CQ_Analytics.SessionPersistence. Crie uma instância desta classe para criar um armazenamento de sessão persistente:

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

Estende CQ_Analytics.SessionStore.

### Propriedades {#properties-3}

#### STOREKEY {#storekey-2}

O valor padrão é `key`.

### Métodos {#methods-7}

Consulte CQ_Analytics.SessionStore para obter os métodos herdados.

Quando os métodos herdados `clear`, `setProperty`, `setProperties`, `removeProperty` são usados para alterar os dados de armazenamento, as alterações são automaticamente persistentes, a menos que as propriedades alteradas sejam sinalizadas como notPersisted.

#### getStoreKey() {#getstorekey}

Recupera o `STOREKEY` propriedade.

**Parâmetros**

Nenhum

**Devoluções**

O valor de `STOREKEY` propriedade.

#### isPersisted(name) {#ispersisted-name}

Determina se uma propriedade de dados é persistente.

**Parâmetros**

* name: string. O nome da propriedade.

**Devoluções**

Um valor booleano de `true` se a propriedade for persistente, e um valor de `false` se o valor não for uma propriedade persistente.

#### persist() {#persist}

Persiste no armazenamento de sessão. O modo de persistência padrão usa o navegador `localStorage` usar `ClientSidePersistence` como o nome ( `window.localStorage.set("ClientSidePersistance", store);`)

Se localStorage não estiver disponível ou não for gravável, o armazenamento será mantido como uma propriedade da janela.

Aciona o `persist` evento após a conclusão.

**Parâmetros**

Nenhum

**Devoluções**

Nenhum valor retornado.

#### redefinir(deferEvent) {#reset-deferevent}

Remove todas as propriedades de dados do armazenamento e mantém o armazenamento. Opcionalmente, o não aciona o `udpate` evento após a conclusão.

**Parâmetros**

* deferEvent: um valor de true impede que o `update` evento de ser disparado. Um valor de `false` faz com que o evento de atualização seja disparado.

**Devoluções**

Nenhum valor retornado.

#### setNonPersisted(nome) {#setnonpersisted-name}

Sinaliza uma propriedade de dados como não persistente.

**Parâmetros**

* name: string. O nome da propriedade que não deve ser persistida.

**Devoluções**

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

Use loadInitProperties para preencher os dados do armazenamento de sessão com os valores de inicialização.

**Parâmetros**

* name: string. O nome da propriedade a ser adicionada.
* value: String. O valor da propriedade a ser adicionada.

**Devoluções**

Nenhum valor retornado.

#### limpar() {#clear-1}

Remove todas as propriedades de dados do armazenamento.

**Parâmetros**

Nenhum.

**Devoluções**

Nenhum valor de retorno.

#### getData(excluded) {#getdata-excluded}

Retorna os dados da loja. Opcionalmente, exclui propriedades de nomes dos dados. Chama o `init` se a propriedade data do armazenamento não existir.

**Parâmetros**

excluded: (opcional) uma matriz de nomes de propriedade a serem excluídos dos dados retornados.

**Devoluções**

Um objeto de propriedades e seus valores.

#### getInitProperty(name) {#getinitproperty-name}

Recupera o valor de uma propriedade de dados.

**Parâmetros**

* name: string. O nome da propriedade de dados a ser recuperada.

**Devoluções**

O valor da propriedade data. Devoluções `null` se o armazenamento de sessão não contiver nenhuma propriedade do nome especificado.

#### getName() {#getname}

Retorna o nome do armazenamento de sessão.

**Parâmetros**

Nenhum.

**Devoluções**

Um valor String que representa o nome do armazenamento.

#### getProperty(name, raw) {#getproperty-name-raw}

Retorna o valor de uma propriedade. O valor é retornado como a propriedade bruta ou o valor filtrado por XSS. Chama o `init` se a propriedade data do armazenamento não existir.

**Parâmetros**

* name: string. O nome da propriedade de dados a ser recuperada.
* raw: Booleano. Um valor true faz com que o valor da propriedade raw seja retornado. Um valor false faz com que o valor retornado seja filtrado por XSS.

**Devoluções**

O valor da propriedade data.

#### getPropertyNames(excluída) {#getpropertynames-excluded}

Retorna os nomes das propriedades que o armazenamento de sessão contém. Chama o `init` se a propriedade data do armazenamento não existir.

**Parâmetros**

excluded: (opcional) uma matriz de nomes de propriedade a serem omitidos dos resultados.

**Devoluções**

Uma matriz de valores de String que representam os nomes de propriedade da sessão.

#### getSessionStore() {#getsessionstore}

Retorna o armazenamento de sessão anexado ao objeto atual.

**Parâmetros**

Nenhum.

**Devoluções**

este

#### init() {#init-1}

Marca o armazenamento como inicializado e aciona o `initialize` evento.

**Parâmetros**

Nenhum.

**Devoluções**

Nenhum valor retornado.

#### isInitialized() {#isinitialized}

Indica se o armazenamento de sessões foi inicializado.

**Parâmetros**

Nenhum.

**Devoluções**

Um valor de `true` se o armazenamento for inicializado e um valor de `false` se o armazenamento não for inicializado.

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

Adiciona as propriedades de um determinado objeto aos dados de inicialização do armazenamento da sessão. Opcionalmente, os dados do objeto também são adicionados aos dados de armazenamento.

**Parâmetros**

* obj: um objeto que contém propriedades enumeráveis.
* setValues: Quando verdadeiro, as propriedades obj são adicionadas aos dados do armazenamento da sessão se os dados do armazenamento ainda não incluírem uma propriedade com o mesmo nome. Quando false, nenhum dado é adicionado aos dados de armazenamento da sessão.

**Devoluções**

Nenhum valor retornado.

#### removeProperty(nome) {#removeproperty-name}

Remove uma propriedade do armazenamento de sessão. Aciona o `update` evento após a conclusão. Chama o `init` se a propriedade data do armazenamento não existir.

**Parâmetros**

* name: string. O nome da propriedade a ser removida.

**Devoluções**

Nenhum valor retornado.

#### redefinir() {#reset}

Restaura os valores iniciais do armazenamento de dados. A implementação padrão simplesmente remove todos os dados. Aciona o `update` evento após a conclusão.

**Parâmetros**

Nenhum.

**Devoluções**

Nenhum valor retornado.

#### setProperties(propriedades) {#setproperties-properties}

Define os valores de várias propriedades. Aciona o `update` evento após a conclusão. Chama o `init` se a propriedade data do armazenamento não existir.

**Parâmetros**

* Propriedades: Objeto. Um objeto que contém propriedades enumeráveis. Cada nome e valor de propriedade é adicionado ao armazenamento.

**Devoluções**

Nenhum valor retornado.

#### setProperty(nome, valor) {#setproperty-name-value}

Define o valor de uma propriedade. Aciona o `update` evento após a conclusão. Chama o `init` se a propriedade data do armazenamento não existir.

**Parâmetros**

* name: string. O nome da propriedade.
* value: String. Valor da propriedade.

**Devoluções**

Nenhum valor retornado.
