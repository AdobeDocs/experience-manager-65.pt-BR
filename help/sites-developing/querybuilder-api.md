---
title: API do Construtor de Query
seo-title: API do Construtor de Query
description: A funcionalidade do Construtor de Query de compartilhamento de ativos é exposta por meio de uma API Java e REST.
seo-description: A funcionalidade do Construtor de Query de compartilhamento de ativos é exposta por meio de uma API Java e REST.
uuid: 6928c3e9-96a1-44ad-9785-350d95f1869a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7965b7ef-dec4-441a-a012-daf1d60df0fb
pagetitle: Query Builder API
tagskeywords: querybuilder
translation-type: tm+mt
source-git-commit: a491d4e9bd9ffc68c4ba7cac3149f48cf7576ee8

---


# API do Construtor de Query{#query-builder-api}

A funcionalidade do Construtor [de Query de compartilhamento de](/help/assets/assets-finder-editor.md) ativos é exposta por meio de uma API Java e uma API REST. Esta seção descreve essas APIs.

O construtor de query do lado do servidor ( [`QueryBuilder`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html)) aceitará uma descrição de query, criará e executará um query XPath, opcionalmente filtrará o conjunto de resultados e também extrairá aspectos, se desejado.

A descrição do query é simplesmente um conjunto de predicados ([`Predicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/Predicate.html)). Os exemplos incluem um predicado de texto completo, que corresponde à `jcr:contains()` função no XPath.

Para cada tipo de predicado, há um componente avaliador ([`PredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) que sabe como lidar com esse predicado específico para XPath, filtragem e extração de facetas. É muito fácil criar avaliadores personalizados, que são conectados por meio do tempo de execução do componente OSGi.

A REST API fornece acesso aos mesmos recursos por meio de HTTP, com respostas sendo enviadas em JSON.

>[!NOTE]
>
>A API do QueryBuilder é criada usando a API JCR. Você também pode query o JCR do Adobe Experience Manager usando a API JCR de um pacote OSGi. Para obter informações, consulte [Consultar dados do Adobe Experience Manager usando a API](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)JCR.

## Sessão Gem {#gem-session}

[O AEM Gems](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) é uma série de soluções técnicas oferecidas por especialistas da Adobe Experience Manager. Esta sessão dedicada ao construtor de query é muito útil para uma visão geral e uso da ferramenta.

>[!NOTE]
>
>Consulte os formulários de [pesquisa de sessão do AEM Gem facilitados com o AEM querybuilder](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html) para obter uma visão geral detalhada do construtor de query.

## Query de amostra {#sample-queries}

Essas amostras são fornecidas na notação de estilo de propriedades Java. Para usá-los com a API Java, use um Java `HashMap` como na amostra de API a seguir.

Para o Servlet `QueryBuilder` JSON, cada exemplo inclui um link para a instalação local do CQ (no local padrão, `http://localhost:4502`). Observe que é necessário fazer logon na instância do CQ antes de usar esses links.

>[!CAUTION]
>
>Por padrão, o servlet json do construtor de query exibe no máximo 10 ocorrências.
>
>A adição do seguinte parâmetro permite que o servlet exiba todos os resultados do query:
>
>**`p.limit=-1`**

>[!NOTE]
>
>Para visualização dos dados JSON retornados no seu navegador, você pode usar um plug-in como JSONView para Firefox.

### Retorno de todos os resultados {#returning-all-results}

O query a seguir **retornará dez resultados** (ou, para ser preciso, no máximo dez), mas informará o **Número de ocorrências:** que estão efetivamente disponíveis:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
orderby=path
```

O mesmo query (com o parâmetro `p.limit=-1`) **retornará todos os resultados** (pode ser um número alto, dependendo da sua instância):

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.limit=-1&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.limit=-1
orderby=path
```

### Uso de p.aginárioTotal para retornar os resultados {#using-p-guesstotal-to-return-the-results}

O objetivo do `p.guessTotal` parâmetro é retornar o número adequado de resultados que podem ser mostrados combinando os valores p.offset e p.limit mínimos viáveis. A vantagem de usar esse parâmetro é melhorar o desempenho com grandes conjuntos de resultados. Isso evita calcular o total completo (por exemplo, chamar result.getSize()) e ler todo o conjunto de resultados, otimizado até o mecanismo e índice OAK. Essa pode ser uma diferença significativa quando há 100 milhares de resultados, tanto no tempo de execução quanto no uso da memória.

A desvantagem do parâmetro é que os usuários não veem o total exato. Mas você pode definir um número mínimo como p.advindoTotal=1000 para que ele sempre leia até 1000, então você obtém totais exatos para conjuntos de resultados menores, mas se for mais que isso, você só pode mostrar &quot;e mais&quot;.

Adicione `p.guessTotal=true` ao query abaixo para ver como ele funciona:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=foundation/components/text
1_property.operation=like
p.guessTotal=true
orderby=path
```

O query retornará o `p.limit` padrão dos `10` resultados com um `0` deslocamento:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

A partir do AEM 6.0 SP2, você também pode usar um valor numérico para contar até um número personalizado de resultados máximos. Use o mesmo query como acima, mas altere o valor de `p.guessTotal` para `50`:

`http://localhost:4502/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=foundation/components/text&1_property.operation=like&p.guessTotal=50&orderby=path`

Ele retornará um número no mesmo limite padrão de 10 resultados com um deslocamento 0, mas exibirá apenas um máximo de 50 resultados:

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implementação da paginação {#implementing-pagination}

Por padrão, o Construtor de Query também fornece o número de ocorrências. Dependendo do tamanho do resultado, isso pode levar muito tempo, já que determinar a contagem precisa envolve verificar todos os resultados para o controle de acesso. A maior parte do total é usada para implementar a paginação para a interface do usuário final. Como determinar a contagem exata pode ser lenta, é recomendável usar o recurso de chuteTotal para implementar a paginação.

Por exemplo, a interface do usuário pode adaptar a seguinte abordagem:

* Obter e exibir a contagem precisa do número total de ocorrências ([SearchResult.getTotalMatches()](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/SearchResult.html#gettotalmatches) ou total na resposta querybuilder.json) são menores ou iguais a 100;
* Defina `guessTotal` como 100 ao fazer a chamada para o Construtor de Query.

* A resposta pode ter os seguintes resultados:

   * `total=43`, `more=false` - Indica que o número total de ocorrências é 43. A interface do usuário pode exibir até dez resultados como parte da primeira página e fornecer paginação para as próximas três páginas. Você também pode usar essa implementação para exibir um texto descritivo como **&quot;43 resultados encontrados&quot;**.
   * `total=100`, `more=true` - Indica que o número total de ocorrências é maior que 100 e que a contagem exata não é conhecida. A interface do usuário pode exibir até dez como parte da primeira página e fornecer paginação para as próximas dez páginas. Você também pode usar esse recurso para exibir um texto como **&quot;mais de 100 resultados encontrados&quot;**. À medida que o usuário vai para as próximas páginas, as chamadas feitas para o Construtor de Query aumentariam o limite de e também dos `guessTotal` e `offset` `limit` parâmetros.

`guessTotal` também deve ser usado nos casos em que a interface do usuário precisa usar a rolagem infinita, para evitar que o Construtor de Query determine a contagem exata de ocorrências.

### Encontre os arquivos jar e solicite-os, os mais recentes primeiro {#find-jar-files-and-order-them-newest-first}

`http://localhost:4502/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### Localizar todas as páginas e ordená-las pela última modificação {#find-all-pages-and-order-them-by-last-modified}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### Localizar todas as páginas e ordená-las pela última vez modificadas, mas decrescentes {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc]`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### Pesquisa de texto completo, ordenada por pontuação {#fulltext-search-ordered-by-score}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### Procurar páginas marcadas com uma determinada tag {#search-for-pages-tagged-with-a-certain-tag}

`http://localhost:4502/bin/querybuilder.json?type=cq:Page&amp;tagid=marketing:interest/product&amp;tagid.property=jcr:content/cq:tags&#39;

```xml
type=cq:Page
tagid=marketing:interest/product
tagid.property=jcr:content/cq:tags
```

Use o `tagid` predicado como no exemplo se você souber a ID explícita da tag.

Use o `tag` predicado para o caminho do título da tag (sem espaços).

Como, no exemplo anterior, você está procurando páginas ( `cq:Page` nós), é necessário usar o caminho relativo desse nó para o `tagid.property` predicado, que é `jcr:content/cq:tags`. Por padrão, o `tagid.property` seria simplesmente `cq:tags`.

### Pesquisar em vários caminhos (usando grupos) {#search-under-multiple-paths-using-groups}

`http://localhost:4502/bin/querybuilder.json?fulltext=Management&group.1_path=/content/geometrixx/en/company/management&group.2_path=/content/geometrixx/en/company/bod&group.p.or=true`

```xml
fulltext=Management
group.p.or=true
group.1_path=/content/geometrixx/en/company/management
group.2_path=/content/geometrixx/en/company/bod
```

Esse query usa um *grupo* (chamado &quot; `group`&quot;), que atua para delimitar subexpressões dentro de um query, assim como os parênteses fazem em classificações mais padrão. Por exemplo, o query anterior pode ser expresso em um estilo mais familiar como:

`"Management" and ("/content/geometrixx/en/company/management" or "/content/geometrixx/en/company/bod")`

Dentro do grupo no exemplo, o `path` predicado é usado várias vezes. Para diferenciar e ordenar as duas instâncias do predicado (a ordem é necessária para alguns predicados), você deve prefixar os predicados com *N* `_ where`*N *é o índice de ordenação. No exemplo anterior, os predicados resultantes são`1_path`e`2_path`.

O `p` in `p.or` é um delimitador especial indicando que o que segue (neste caso, um `or`) é um *parâmetro* do grupo, em oposição a um subpredicado do grupo, como `1_path`.

Se nenhum `p.or` for dado então todos os predicados são Eed juntos, ou seja, cada resultado deve satisfazer todos os predicados.

>[!NOTE]
>
>Não é possível usar o mesmo prefixo numérico em um único query, mesmo para predicados diferentes.

### Pesquisar propriedades {#search-for-properties}

Aqui você está procurando por todas as páginas de um determinado modelo, usando a `cq:template` propriedade:

`http://localhost:4502/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/apps/geometrixx/templates/homepage
```

Isso tem a desvantagem de que os `jcr:content` nós das páginas, não as próprias páginas, são retornados. Para resolver isso, você pode pesquisar por caminho relativo:

`http://localhost:4502/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/apps/geometrixx/templates/homepage
```

### Procurar várias propriedades {#search-for-multiple-properties}

Ao usar o predicado de propriedade várias vezes, é necessário adicionar os prefixos de número novamente:

`http://localhost:4502/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fapps%2fgeometrixx%2ftemplates%2fhomepage&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=English&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/apps/geometrixx/templates/homepage
2_property=jcr:content/jcr:title
2_property.value=English
```

### Procurar vários valores de propriedade {#search-for-multiple-property-values}

Para evitar grandes grupos quando você deseja pesquisar por vários valores de uma propriedade ( `"A" or "B" or "C"`), é possível fornecer vários valores ao `property` predicado:

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Products&property.2_value=Square&property.3_value=Events`

```xml
property=jcr:title
property.1_value=Products
property.2_value=Square
property.3_value=Events
```

Para propriedades de vários valores, também é possível exigir que vários valores correspondam ( `"A" and "B" and "C"`):

`http://localhost:4502/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=test&property.2_value=foo&property.3_value=bar`

```xml
property=jcr:title
property.and=true
property.1_value=test
property.2_value=foo
property.3_value=bar
```

## Refinando o que é retornado {#refining-what-is-returned}

Por padrão, o Servlet JSON do QueryBuilder retornará um conjunto padrão de propriedades para cada nó no resultado da pesquisa (por exemplo, caminho, nome, título, etc.). Para obter controle sobre quais propriedades são retornadas, é possível fazer o seguinte:

Especificar

```
p.hits=full
```

nesse caso, todas as propriedades serão incluídas para cada nó:

`http://localhost:4502/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
```

Uso

```
p.hits=selective
```

e especifique as propriedades que deseja obter

```
p.properties
```

separados por um espaço:

`http://localhost:4502/bin/querybuilder.json?p.hits=selective&property=jcr%3atitle&property.value=Triangle`

[ `http://localhost:4502/bin/querybuilder.json?`](http://localhost:4502/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Triangle) p.hits=select&amp; [](http://localhost:4502/bin/querybuilder.json?p.hits=selective&p.nodedepth=5&p.properties=sling%3aresourceType%20jcr%3apath&property=jcr%3atitle&property.value=Triangle)p.properties=sling%3aresourceType%20jcr%3primárioType&amp;property=jcr%3atitle&amp;property.value=Triangle

```xml
property=jcr:title
property.value=Triangle
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

Outra coisa que você pode fazer é incluir nós filhos na resposta do QueryBuilder. Para fazer isso, é necessário especificar

```
p.nodedepth=n
```

onde `n` é o número de níveis que você deseja que o query retorne. Observe que, para que um nó filho seja retornado, ele deve ser especificado pelo seletor de propriedades

```
p.hits=full
```

Exemplo:

`http://localhost:4502/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Triangle`

```xml
property=jcr:title
property.value=Triangle
p.hits=full
p.nodedepth=5
```

## Mais Predicados {#morepredicates}

Para obter mais predicados, consulte a página [Referência de previsão do Construtor de](/help/sites-developing/querybuilder-predicate-reference.md)Query.

Você também pode verificar o [Javadoc em busca das `PredicateEvaluator` classes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/PredicateEvaluator.html). O Javadoc para essas classes contém a lista de propriedades que você pode usar.

O prefixo do nome da classe (por exemplo, &quot; `similar`&quot; em [`SimilarityPredicateEvaluator`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) é a propriedade ** principal da classe. Essa propriedade também é o nome do predicado a ser usado no query (em minúsculas).

Para essas propriedades principais, você pode encurtar o query e usar &quot; `similar=/content/en`&quot; em vez da variante totalmente qualificada &quot; `similar.similar=/content/en`&quot;. O formulário totalmente qualificado deve ser usado para todas as propriedades não principais de uma classe.

## Exemplo de uso da API do Construtor de Query {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "Geometrixx";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory =     DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
    for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

>[!NOTE]
>
>Para saber como criar um pacote OSGi que usa a API do QueryBuilder e usar esse pacote OSGi em um aplicativo do Adobe Experience Manager, consulte [Criação de pacotes OSGi do Adobe CQ que usam a](https://helpx.adobe.com/experience-manager/using/using-query-builder-api.html)API do Query Builder.

O mesmo query executado por HTTP usando o servlet Query Builder (JSON):

`http://localhost:4502/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=Geometrixx&group.1_fulltext.relPath=jcr:content&group.2_fulltext=Geometrixx&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Armazenamento e carregamento de query {#storing-and-loading-queries}

Os Query podem ser armazenados no repositório para que você possa usá-los posteriormente. O `QueryBuilder` fornece o &quot; `storeQuery` método&quot; com a seguinte assinatura:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

Ao usar o [`QueryBuilder#storeQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#storequerycomdaycqsearchqueryjavalangstringbooleanjavaxjcrsession) método, o dado `Query` é armazenado no repositório como um arquivo ou como uma propriedade de acordo com o valor do `createFile` argumento. O exemplo a seguir mostra como salvar um caminho `Query` no caminho `/mypath/getfiles` como um arquivo:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Qualquer query armazenado anteriormente pode ser carregado do repositório usando o [`QueryBuilder#loadQuery`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html#loadqueryjavalangstringjavaxjcrsession) método:

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Por exemplo, um `Query` armazenado no caminho `/mypath/getfiles` pode ser carregado pelo seguinte snippet:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Teste e depuração {#testing-and-debugging}

Para reproduzir e depurar query do querybuilder, você pode usar o console do depurador do QueryBuilder em

`http://localhost:4502/libs/cq/search/content/querydebug.html`

ou, alternativamente, o servlet json querybuilder em

`http://localhost:4502/bin/querybuilder.json?path=/tmp`

( `path=/tmp` é apenas um exemplo).

### Recomendações gerais de depuração {#general-debugging-recommendations}

### Obter XPath explicável por meio de registro {#obtain-explain-able-xpath-via-logging}

Explique **todos** os query durante o ciclo de desenvolvimento em relação ao conjunto de índice do público alvo.

* Ative registros DEBUG para o QueryBuilder para obter o query XPath subjacente explicável

   * Navegue até https://&lt;nomedoservidor>:&lt;serverport>/system/console/slinglog. Crie um novo agente de log para `com.day.cq.search.impl.builder.QueryImpl` em **DEBUG**.

* Depois que DEBUG for ativado para a classe acima, os registros exibirão o XPath gerado pelo Construtor de Query.
* Copie o query XPath da entrada de registro do query QueryBuilder associado, por exemplo:

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* Cole o query XPath em [Explique o Query](/help/sites-administering/operations-dashboard.md#explain-query) como XPath para obter o plano do query

### Obtenha XPath explicável por meio do depurador do Construtor de Query {#obtain-explain-able-xpath-via-the-query-builder-debugger}

* Use o depurador do AEM QueryBuilder para gerar um query XPath explicável:

Explique **todos** os query durante o ciclo de desenvolvimento em relação ao conjunto de índice do público alvo.

**Obter XPath explicável por meio de registro**

* Ative registros DEBUG para o QueryBuilder para obter o query XPath subjacente explicável

   * Navegue até https://&lt;nomedoservidor>:&lt;serverport>/system/console/slinglog. Crie um novo agente de log para `com.day.cq.search.impl.builder.QueryImpl` em **DEBUG**.

* Depois que DEBUG for ativado para a classe acima, os registros exibirão o XPath gerado pelo Construtor de Query.
* Copie o query XPath da entrada de registro do query QueryBuilder associado, por exemplo:

   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]`

* Cole o query XPath em [Explique o Query](/help/sites-administering/operations-dashboard.md#explain-query) como XPath para obter o plano do query

**Obtenha XPath explicável por meio do depurador do Construtor de Query**

* Use o depurador do AEM QueryBuilder para gerar um query XPath explicável:

![chlimage_1-66](assets/chlimage_1-66a.png)

1. Forneça o query do Construtor de Query no depurador do Construtor de Query
1. Executar a pesquisa
1. Obter o XPath gerado
1. Cole o query XPath em Explique o Query como XPath para obter o plano do query

>[!NOTE]
>
>Os query que não são do querybuilder (XPath, JCR-SQL2) podem ser fornecidos diretamente para Explicar o Query.

Para obter um resumo sobre como depurar query com o QueryBuilder, consulte o vídeo abaixo.

>[!NOTE]
>
>[https://www.youtube.com/watch?v=BnyXjhRKYKc](https://www.youtube.com/watch?v=BnyXjhRKYKc)

## Depuração de Query com registro {#debugging-queries-with-logging}

>[!NOTE]
>
>A configuração dos registradores está descrita na seção [Creating Your Own Loggers and Writers (Criação de seus próprios registradores e escritores](/help/sites-deploying/configure-logging.md#creating-your-own-loggers-and-writers)).

A saída de log (nível INFO) da implementação do construtor de query ao executar o query descrito em Teste e Depuração:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=Geometrixx, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "Geometrixx") or jcr:contains(jcr:content/@cq:tags, "Geometrixx"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

Se você tiver um query usando avaliadores de predicado que filtram ou usam um pedido personalizado por comparador, isso também será observado no query:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Links Javadoc {#javadoc-links}

| **Javadoc** | **Descrição** |
|---|---|
| [com.day.cq.search](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/package-summary.html) | API básica do QueryBuilder e do Query |
| [com.day.cq.search.result](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/result/package-summary.html) | API de resultado |
| [com.day.cq.search.facets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/package-summary.html) | Aspectos |
| [com.day.cq.search.facets.buckets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Grupos (contidos em facetas) |
| [com.day.cq.search.eval](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) | Avaliadores Predicados |
| [com.day.cq.search.facets.extrators](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Extratores de Aspectos (para avaliadores) |
| [com.day.cq.search.writer](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/writer/package-summary.html) | Gravador de Ocorrência de Resultado JSON para o servlet Querybuilder (/bin/querybuilder.json) |

