---
title: Consultas persistentes de GraphQL
description: Saiba como criar consultas persistentes de GraphQL no Adobe Experience Manager para otimizar o desempenho. As consultas persistentes podem ser solicitadas por aplicativos clientes usando o método HTTP GET e a resposta pode ser armazenada em cache nas camadas Dispatcher e CDN, melhorando, em última análise, o desempenho dos aplicativos clientes.
source-git-commit: a717382fa4aaf637c5b1bf3ce4aca3f90a059458
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 72%

---

# Consultas persistentes de GraphQL  {#persisted-queries-caching}

As consultas persistentes são consultas de GraphQL criadas e armazenadas no servidor do Adobe Experience Manager (AEM) as a Cloud Service. Elas podem ser solicitadas com uma solicitação GET por aplicativos clientes. A resposta de uma solicitação do GET pode ser armazenada em cache nas camadas do Dispatcher e da Rede de entrega de conteúdo (CDN), melhorando, em última análise, o desempenho do aplicativo cliente que fez a solicitação. Isso é diferente das consultas de GraphQL padrão, que são executadas usando solicitações POST, onde a resposta não pode ser facilmente armazenada em cache.

<!--
>[!NOTE]
>
>Persisted Queries are recommended. See [GraphQL Query Best Practices (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) for details, and the related Dispatcher configuration.
-->

O [GraphiQL IDE](/help/assets/content-fragments/graphiql-ide.md) está disponível no AEM para que você desenvolva, teste e crie consultas GraphQL persistentes antes de [transferi-las para o ambiente de produção](#transfer-persisted-query-production). Para casos que precisam de personalização (por exemplo, quando [personalização do cache](/help/assets/content-fragments/graphiql-ide.md#caching-persisted-queries)) é possível usar a API; consulte o exemplo de cURL fornecido em [Como persistir uma consulta do GraphQL](#how-to-persist-query).

## Endpoints e consultas persistentes {#persisted-queries-and-endpoints}

Consultas persistentes devem sempre usar o endpoint relacionado à [configuração apropriada do Sites](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-aem-endpoint); para que possam usar um desses, ou ambos:

* A configuração global e o endpoint 
A consulta tem acesso a todos os modelos de fragmento de conteúdo.
* Configuração(ões) e endpoint(s) do Sites específicos 
A criação de uma consulta persistente para uma configuração do Sites específica requer um endpoint correspondente específico para a configuração do Sites (para fornecer acesso aos modelos de fragmento de conteúdo relacionados).
Por exemplo, para criar uma consulta persistente especificamente para a configuração do Sites WKND, uma configuração do Sites correspondente específica de WKND e um endpoint específico de WKND devem ser criados antecipadamente.

>[!NOTE]
>
>Consulte [Habilitar a funcionalidade de fragmentos de conteúdo no Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) para obter mais detalhes.
>
>As **Consultas GraphQL persistidas** precisam estar habilitadas para a configuração apropriada do Sites.

Por exemplo, se houver uma consulta específica chamada `my-query`, que usa um modelo `my-model` da configuração `my-conf` do Sites:

* É possível criar uma consulta usando o endpoint específico `my-conf` e, em seguida, a consulta será salva da seguinte maneira:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* É possível criar a mesma consulta usando o endpoint `global`, mas a consulta será salva da seguinte maneira:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Essas são duas consultas diferentes - salvas em caminhos diferentes.
>
>Por acaso, elas usam o mesmo modelo - mas por meio de diferentes endpoints.

## Como criar uma consulta persistente de GraphQL {#how-to-persist-query}

É recomendável criar consultas persistentes em um ambiente de criação do AEM inicialmente e, em seguida, [transferir a consulta](#transfer-persisted-query-production) para o ambiente de publicação da sua produção do AEM para ser usada pelos aplicativos.

Há vários métodos para criar consultas persistentes, incluindo:

* GraphiQL IDE - consulte [Salvar consultas persistentes](/help/assets/content-fragments/graphiql-ide.md#saving-persisted-queries) (método preferencial)
* cURL - consulte o exemplo a seguir
* Outras ferramentas, incluindo o [Postman](https://www.postman.com/)

O GraphiQL IDE é o método **preferencial** para consultas persistentes. Para persistir um determinado query usando o **cURL** ferramenta de linha de comando:

1. Prepare a consulta utilizando o método PUT no novo URL do endpoint `/graphql/persist.json/<config>/<persisted-label>`.

   Por exemplo, crie uma consulta persistente:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. Neste ponto, verifique a resposta.

   Por exemplo, verifique se há sucesso:

   ```json
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. É possível solicitar a consulta persistente utilizando o método GET com o URL `/graphql/execute.json/<shortPath>`.

   Por exemplo, use a consulta persistente:

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Atualize uma consulta persistente utilizando o método POST em um caminho de consulta já existente.

   Por exemplo, use a consulta persistente:

   ```shell
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Crie uma consulta agrupada simples.

   Por exemplo:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Crie uma consulta agrupada simples com controle de cache.

   Por exemplo:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Crie uma consulta persistente com parâmetros:

   Por exemplo:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```


## Como executar uma consulta persistente {#execute-persisted-query}

Para executar uma consulta persistente, um aplicativo cliente faz uma solicitação GET usando a seguinte sintaxe:

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

Onde `PERSISTENT_PATH` é um caminho encurtado no qual a consulta persistida é salva.

1. Por exemplo, `wknd` é o nome da configuração e `plain-article-query` é o nome da consulta persistida. Para executar a consulta:

   ```shell
   $ curl -X GET \
       https://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Execução de uma consulta com parâmetros.

   >[!NOTE]
   >
   > As variáveis e os valores de consulta devem ser corretamente [codificados](#encoding-query-url) ao executar uma consulta persistida.

   Por exemplo:

   ```bash
   $ curl -X GET \
       "https://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   Consulte o uso de [variáveis de consulta](#query-variables) para obter mais detalhes.

## Uso de variáveis de consulta {#query-variables}

As variáveis de consulta podem ser usadas com consultas persistentes. As variáveis de consulta são anexadas à solicitação e prefixadas por ponto e vírgula (`;`), usando o nome e o valor da variável. As variáveis são separadas por ponto e vírgula.

O padrão é semelhante ao seguinte:

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

Por exemplo, a consulta a seguir contém uma variável `activity` para filtrar uma lista com base em um valor de atividade:

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

Esta consulta pode ser persistida em um caminho `wknd/adventures-by-activity`. Para chamar a consulta persistente onde `activity=Camping`, a solicitação terá esta aparência:

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

Observe que `%3B` é a codificação UTF-8 para `;` e `%3D` é a codificação para `=`. As variáveis de consulta e quaisquer caracteres especiais devem ser [corretamente codificados](#encoding-query-url) para que a consulta persistente seja executada.

## Armazenamento em cache de consultas persistentes {#caching-persisted-queries}

As consultas persistentes são recomendadas, pois podem ser armazenadas em cache no [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=en) e camadas da Rede de entrega de conteúdo (CDN), melhorando o desempenho do aplicativo cliente que fez a solicitação.

Por padrão, o AEM invalidará o cache com base em uma definição de Time To Live (TTL). Esses TTLs podem ser definidos pelos seguintes parâmetros. Estes parâmetros podem ser acessados por vários meios, com variações nos nomes de acordo com o mecanismo usado:

| Tipo de cache | [Cabeçalho HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)  | cURL  | Configuração do OSGi  |
|--- |--- |--- |--- |--- |
| Navegador | `max-age` | `cache-control : max-age` | `cacheControlMaxAge` |
| CDN | `s-maxage` | `surrogate-control : max-age` | `surrogateControlMaxAge` |
| CDN | `stale-while-revalidate` | `surrogate-control : stale-while-revalidate ` | `surrogateControlStaleWhileRevalidate` |
| CDN | `stale-if-error` | `surrogate-control : stale-if-error` | `surrogateControlStaleIfError` |

### Instâncias do autor {#author-instances}

Para instâncias de autor, os valores padrão são:

* `max-age`  : 60
* `s-maxage` : 60
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

Estes:

* não pode ser substituído por uma configuração OSGi
* pode ser substituído por uma solicitação que define as configurações do cabeçalho HTTP usando cURL; deve incluir configurações adequadas para `cache-control` e/ou `surrogate-control`; para obter exemplos, consulte [Gerenciando o Cache no Nível de Consulta Persistente](#cache-persisted-query-level)

<!-- CQDOC-20186 -->
<!-- following entry is only when the GraphiQL IDE is ready; add cross-reference too -->
<!--
* can be overwritten if you specify values in the **Headers** dialog of the [GraphiQL IDE](#http-cache-headers-graphiql-ide)
-->

### Publicar instâncias {#publish-instances}

Para instâncias de publicação, os valores padrão são:

* `max-age`  : 60
* `s-maxage` : 7200
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

Eles podem ser substituídos:

<!-- CQDOC-20186 -->
<!-- following entry is only when the GraphiQL IDE is ready -->
<!--
* [from the GraphQL IDE](#http-cache-headers-graphiql-ide)
-->

* [no Nível de Consulta Persistente](#cache-persisted-query-level); isso envolve postar a consulta em AEM usando cURL na interface da linha de comando e publicar a consulta persistente.

* [com uma configuração OSGi](#cache-osgi-configration)

<!-- CQDOC-20186 -->
<!-- keep for future use; check link -->
<!--
### Managing HTTP Cache Headers in the GraphiQL IDE {#http-cache-headers-graphiql-ide}

The GraphiQL IDE - see [Saving Persisted Queries](/help/assets/content-fragments/graphiql-ide.md#managing-cache)
-->

### Gerenciando o Cache no Nível de Consulta Persistente {#cache-persisted-query-level}

Isso envolve postar a consulta em AEM usando cURL na interface da linha de comando.

Para obter um exemplo do método PUT (create):

```bash
curl -u admin:admin -X PUT \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

Para obter um exemplo do método POST (update):

```bash
curl -u admin:admin -X POST \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

O `cache-control` pode ser definido no momento da criação (PUT) ou posteriormente (por exemplo, por meio de uma solicitação POST por instância). O controle de cache é opcional ao criar a consulta persistente, pois o AEM pode fornecer o valor padrão. Consulte [Como persistir uma consulta do GraphQL](#how-to-persist-query), para obter um exemplo de persistência de um query usando cURL.

### Gerenciamento de cache com uma configuração OSGi {#cache-osgi-configration}

Para gerenciar o cache globalmente, você pode [definir as configurações do OSGi](/help/sites-deploying/configuring-osgi.md) para **Configuração do Serviço de Consulta Persistente**. Caso contrário, essa configuração do OSGi usará a variável [valores padrão para instâncias de publicação](#publish-instances).

>[!NOTE]
>
>A configuração do OSGi é adequada apenas para instâncias de publicação. A configuração existe nas instâncias do autor, mas é ignorada.

## Codificação do URL de consulta para uso por um aplicativo {#encoding-query-url}

Para uso por um aplicativo, quaisquer caracteres especiais usados ao criar variáveis de consulta (ou seja, ponto e vírgula (`;`), sinal de igual (`=`), barras `/`) devem ser convertidos para usar a codificação UTF-8 correspondente.

Por exemplo:

```bash
curl -X GET \ "https://localhost:4502/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

O URL pode ser dividido nas seguintes partes:

| Parte do URL | Descrição |
|----------| -------------|
| `/graphql/execute.json` | Endpoint de consulta persistida |
| `/wknd/adventure-by-path` | Caminho de consulta persistida |
| `%3B` | Codificação de `;` |
| `adventurePath` | Variável de consulta |
| `%3D` | Codificação de `=` |
| `%2F` | Codificação de `/` |
| `%2Fcontent%2Fdam...` | Caminho codificado para o fragmento de conteúdo |

Em textos sem formatação, o URI da solicitação tem a seguinte aparência:

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

Para usar uma consulta persistente em um aplicativo cliente, o SDK do cliente do AEM Headless deve ser usado para [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java) ou [NodeJS](https://github.com/adobe/aem-headless-client-nodejs). O SDK do cliente headless codificará automaticamente todas as variáveis de consulta apropriadamente na solicitação.

## Transferir uma consulta persistente para o ambiente de produção  {#transfer-persisted-query-production}

As consultas persistentes devem sempre ser criadas em um serviço de autor do AEM e publicadas (replicadas) em um serviço de publicação do AEM. Geralmente, as consultas persistentes são criadas e testadas em ambientes inferiores, como ambientes locais ou de desenvolvimento. Então, é necessário promover consultas persistentes a ambientes de nível superior, disponibilizando-as em um ambiente de publicação do AEM em produção para que os aplicativos clientes as consumam.

### Pacote de consultas persistidas

As consultas persistidas podem ser inseridas em [pacotes do AEM](/help/sites-administering/package-manager.md). Os pacotes do AEM podem ser baixados e instalados em diferentes ambientes. Os pacotes do AEM também podem ser replicados de um ambiente de autor do AEM para ambientes de publicação do AEM.

Para criar um pacote:

1. Navegue até **Ferramentas** > **Implantação** > **Pacotes**.
1. Crie um novo pacote tocando em **Criar pacote**. Isso abrirá uma caixa de diálogo para definir o pacote.
1. Em **Geral** na caixa de diálogo Definição do pacote, insira um **Nome** como “wknd-persistent-queries”.
1. Insira um número de versão como “1.0”.
1. Em **Filtros**, adicione um novo **Filtro**. Use o Localizador de caminhos para selecionar a pasta `persistentQueries`, abaixo da configuração. Por exemplo, para a configuração `wknd`, o caminho completo será `/conf/wknd/settings/graphql/persistentQueries`.
1. Toque em **Salvar** para salvar a nova definição de pacote e fechar a caixa de diálogo.
1. Toque no botão **Criar** na definição de pacote recém-criada.

Depois que o pacote tiver sido criado, você poderá:

* **Baixar** o pacote e fazer upload dele em um ambiente diferente.
* **Replicar** o pacote tocando em **Mais** > **Replicar**. Isso replicará o pacote no ambiente de publicação conectado do AEM.

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
