---
title: Solução de problemas de Query lentos
seo-title: Solução de problemas de Query lentos
description: 'null'
seo-description: 'null'
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
translation-type: tm+mt
source-git-commit: 6d8680bcfb03197ac33bc7efb0e40796e38fef20
workflow-type: tm+mt
source-wordcount: '2267'
ht-degree: 0%

---


# Solução de problemas de Query lentos{#troubleshooting-slow-queries}

## Classificações de Query lento {#slow-query-classifications}

Há 3 classificações principais de query lentos em AEM, listadas por gravidade:

1. **query sem índice**

   * Query que **não** são resolvidos para um índice e percorrem o conteúdo do JCR para coletar resultados

1. **query com pouca restrição (ou com escopo)**

   * Query que são resolvidos para um índice, mas devem atravessar todas as entradas de índice para coletar resultados

1. **Grandes query de conjunto de resultados**

   * Query que retornam números muito grandes de resultados

As primeiras 2 classificações de query (sem índice e com pouca restrição) são lentas, pois forçam o mecanismo de query Oak a inspecionar cada resultado **potencial** (nó de conteúdo ou entrada de índice) para identificar qual pertence ao conjunto de resultados **real** .

O ato de inspecionar cada resultado potencial é o que se chama de Navegação.

Uma vez que cada resultado potencial deve ser inspecionado, o custo para determinar o conjunto de resultados real cresce linearmente com o número de resultados potenciais.

A adição de restrições de query e índices de ajuste permite que os dados de índice sejam armazenados em um formato otimizado, permitindo uma recuperação rápida de resultados e reduz ou elimina a necessidade de inspeção linear de conjuntos de resultados potenciais.

No AEM 6.3, por padrão, quando uma passagem de 100.000 é atingida, o query falha e lança uma exceção. Esse limite não existe por padrão em versões AEM anteriores à AEM 6.3, mas pode ser definido por meio das Configurações do mecanismo de Query Apache Jackrabbit Configuração OSGi e do bean QueryEngineSettings JMX (propriedade LimitReads).

### Detecção de Query sem índice {#detecting-index-less-queries}

#### Durante o desenvolvimento {#during-development}

Explicar **todos** os query e garantir que seus planos de query não contenham o **/&amp;ast; uma explicação transversal** . Exemplo de plano de query de percurso:

* **PLANO:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Pós-implantação {#post-deployment}

* Monitore os query transversais `error.log` sem índice:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Essa mensagem será registrada somente se nenhum índice estiver disponível e se o query potencialmente atravessar muitos nós. As mensagens não são registradas se um índice estiver disponível, mas o valor de passagem é pequeno e, portanto, rápido.

* Visit the AEM [Query Performance](/help/sites-administering/operations-dashboard.md#query-performance) operations console and [Explain](/help/sites-administering/operations-dashboard.md#explain-query) slow queries looking for traversal or no index query explanations.

### Detecção de Query com restrições erradas {#detecting-poorly-restricted-queries}

#### Durante o desenvolvimento {#during-development-1}

Explique todos os query e verifique se eles foram resolvidos para um índice ajustado para corresponder às restrições de propriedade do query.

* A cobertura do plano de query ideal tem como objetivo todas as restrições de propriedade e, no mínimo, as restrições de propriedade mais rigorosas do query. `indexRules`
* Query que classificam os resultados devem ser resolvidos para um Índice de propriedades Lucene com regras de índice para as propriedades classificadas por `orderable=true.`

#### Por exemplo, o padrão `cqPageLucene` não tem uma regra de índice para `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Antes de adicionar a regra de índice cq:tags

* **cq:regras de índice de tags**

   * Não existe fora da caixa

* **query Construtor de Query**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **plano de Query**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Esse query é resolvido para o `cqPageLucene` índice, mas como não existe uma regra de índice de propriedade para `jcr:content` ou `cq:tags`, quando essa restrição é avaliada, todos os registros no `cqPageLucene` índice são verificados para determinar uma correspondência. Isso significa que, se o índice contiver 1 milhão de `cq:Page` nós, 1 milhão de registros serão verificados para determinar o conjunto de resultados.

Após adicionar a regra de índice cq:tags

* **cq:regras de índice de tags**

   ```js
   /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
   @name=jcr:content/cq:tags
   @propertyIndex=true
   ```

* **query Construtor de Query**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=myTagNamespace:myTag
   ```

* **plano de Query**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

A adição de indexRule para `jcr:content/cq:tags` no `cqPageLucene` índice permite que `cq:tags` os dados sejam armazenados de forma otimizada.

Quando um query com a restrição é executado, o índice pode procurar os resultados por valor. `jcr:content/cq:tags` Isso significa que se 100 `cq:Page` nós tiverem `myTagNamespace:myTag` como valor, apenas esses 100 resultados serão retornados, e os outros 999.000 serão excluídos das verificações de restrições, melhorando o desempenho em um fator de 10.000.

É claro que novas restrições ao query reduzem os conjuntos de resultados elegíveis e otimizam ainda mais a otimização do query.

Da mesma forma, sem uma regra de índice adicional para a `cq:tags` propriedade, mesmo um query de texto completo com uma restrição em `cq:tags` teria um desempenho ruim, já que os resultados do índice retornariam todas as correspondências de texto completo. A restrição nas tags cq:seria filtrada depois.

Another cause of post-index-filtering is Access Control Lists which often gets missed during development. Tente se certificar de que o query não retorne caminhos que possam estar inacessíveis ao usuário. Isso geralmente pode ser feito por uma estrutura de conteúdo melhor, além de fornecer a restrição de caminho relevante no query.

Uma maneira útil de identificar se o índice Lucene está retornando muitos resultados para retornar um subconjunto muito pequeno como resultado do query é ativar os registros DEBUG para `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` e ver quantos documentos estão sendo carregados do índice. O número de eventuais resultados versus o número de documentos carregados não deve ser desproporcionado. For more information, see [Logging](/help/sites-deploying/configure-logging.md).

#### Pós-implantação {#post-deployment-1}

* Monitore os query `error.log` transversais:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visite o console de operações de Desempenho [do](/help/sites-administering/operations-dashboard.md#query-performance) Query AEM e [Explique](/help/sites-administering/operations-dashboard.md#explain-query) query lentos que procuram planos de query que não resolvam as restrições de propriedade do query para indexar as regras de propriedade.

### Detecção de Query Grandes de Conjunto de Resultados {#detecting-large-result-set-queries}

#### Durante o desenvolvimento {#during-development-2}

Defina limites baixos para oak.queryLimitInMemory (por exemplo, 10000) e oak.queryLimitReads (por exemplo, 5000) e otimize o query caro ao clicar em UnsupportedOperationException dizendo &quot;O query lê mais de x nós...&quot;.

Isso ajuda a evitar query que consomem muitos recursos (ou seja, não suportado por qualquer índice ou apoiado por um índice de cobertura menor). Por exemplo, um query que lê nós 1M levaria a uma grande quantidade de E/S e afetaria negativamente o desempenho geral do aplicativo. Assim, qualquer query que falhe devido aos limites acima devem ser analisados e otimizados.

#### Pós-implantação {#post-deployment-2}

* Monitore os registros em busca de query que acionem um grande nó transversal ou grande consumo de memória heap: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Otimizar o query para reduzir o número de nós atravessados

* Monitore os registros em busca de query que acionem um grande consumo de memória heap:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Otimize o query para reduzir o consumo de memória do heap

Para as versões AEM 6.0 - 6.2, é possível ajustar o limite para a passagem de nó pelos parâmetros JVM no script de start AEM para impedir que query grandes sobrecarreguem o ambiente. Os valores recomendados são:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

No AEM 6.3, os 2 parâmetros acima são pré-configurados por padrão e podem ser modificados por meio do OSGi QueryEngineSettings.

Mais informações disponíveis em: [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Ajuste do desempenho do Query {#query-performance-tuning}

O lema da otimização do desempenho do query no AEM é:

**&quot;Quanto mais restrições, melhor.&quot;**

A seguir, os destaques recomendam os ajustes para garantir o desempenho do query. Primeiro ajuste o query, uma atividade menos intrusiva e, se necessário, ajuste as definições de índice.

### Ajustar a declaração do Query {#adjusting-the-query-statement}

AEM suporta os seguintes idiomas de query:

* Query Builder
* JCR-SQL2
* XPath

O exemplo a seguir usa o Construtor de Query como a linguagem de query mais comum usada pelos desenvolvedores AEM, no entanto, os mesmos princípios se aplicam ao JCR-SQL2 e XPath.

1. Add a nodetype restriction so the query resolves to an existing Lucene Property Index.

* **query não otimizado**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **query otimizado**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   Queries lacking a nodetype restriction force AEM to assume the `nt:base` nodetype, which every node in AEM is a subtype of, effectively resulting in no nodetype restriction.

   A configuração `type=cq:Page` restringe esse query a apenas `cq:Page` nós e resolve o query para AEM cqPageLucene, limitando os resultados a um subconjunto de nós (somente `cq:Page` nós) no AEM.

1. Ajuste a restrição de tipo de query para que o query seja resolvido para um Índice de propriedades Lucene existente.

* **query não otimizado**

   ```js
   type=nt:hierarchyNode
   property=jcr:content/contentType
   property.value=article-page
   ```

* **query otimizado**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   `nt:hierarchyNode` is the parent nodetype of `cq:Page`, and assuming `jcr:content/contentType=article-page` is only applied to `cq:Page` nodes via our custom application, this query will only return `cq:Page` nodes where `jcr:content/contentType=article-page`. This is a suboptimal restriction though, because:

   * Outro nó herda de `nt:hierarchyNode` (por exemplo, `dam:Asset`) adding unnecessarily to the set of potential results.
   * No AEM-provided index exists for `nt:hierarchyNode`, however as there a provided index for `cq:Page`.
   Setting `type=cq:Page` restricts this query to only `cq:Page` nodes, and resolves the query to AEM&#39;s cqPageLucene, limiting the results to a subset of nodes (only cq:Page nodes) in AEM.

1. Or, adjust the property restriction(s) so the query resolves to an existing Property Index.

* **query não otimizado**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **query otimizado**

   ```js
   property=jcr:content/sling:resourceType
   property.value=my-site/components/structure/article-page
   ```

   Changing the property restriction from `jcr:content/contentType` (a custom value) to the well known property `sling:resourceType` lets the query to resolve to the property index `slingResourceType` which indexes all content by `sling:resourceType`.

   Property indexes (opposed to Lucene Property Indexes) are best used when the query does not discern by nodetype, and a single property restriction dominates the result set.

1. Add the tightest path restriction possible to the query. For example, prefer `/content/my-site/us/en` over `/content/my-site`, or `/content/dam` over `/`.

* **query não otimizado**

   ```js
   type=cq:Page
   path=/content
   property=jcr:content/contentType
   property.value=article-page
   ```

* **query otimizado**

   ```js
   type=cq:Page
   path=/content/my-site/us/en
   property=jcr:content/contentType
   property.value=article-page
   ```

   O escopo da restrição de caminho de `path=/content`para `path=/content/my-site/us/en` permite que os índices reduzam o número de entradas de índice que precisam ser inspecionadas. When the query can restrict the path very well, beyond just `/content` or `/content/dam`, ensure the index has `evaluatePathRestrictions=true`.

   Observe que usar `evaluatePathRestrictions` aumenta o tamanho do índice.

1. Sempre que possível, evite funções/operações do query, tais como: `LIKE` e `fn:XXXX` à medida que os seus custos aumentam com o número de resultados baseados em restrições.

* **query não otimizado**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.operation=like
   property.value=%article%
   ```

* **query otimizado**

   ```js
   type=cq:Page
   fulltext=article
   fulltext.relPath=jcr:content/contentType
   ```

   A condição LIKE é lenta para avaliação, pois nenhum índice pode ser usado se o texto start com um curinga (&quot;%...&#39;). A condição jcr:contains permite o uso de um índice de texto completo e, portanto, é preferida. Isso requer que o Índice de propriedades do Lucene resolvido tenha indexRule para `jcr:content/contentType` with `analayzed=true`.

   Using query functions like `fn:lowercase(..)` may be harder to optimize as there are not faster equivalents (outside more complex and obtrusive index analyzer configurations). It is best to identify other scoping restrictions to improve improve the overal query performance, requiring the functions to operate on the smallest set of potential results possible.

1. ***This adjustment is Query Builder specific, and does not apply to JCR-SQL2 or XPath.***

   Use [Query Builder&#39; guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) when the full set of results is **not** immediately needed.

   * **query não otimizado**

      ```js
      type=cq:Page
      path=/content
      ```

   * **query otimizado**

      ```js
      type=cq:Page
      path=/content
      p.guessTotal=100
      ```
   For cases where query execution is fast but the number of results are large, p. `guessTotal` is a critical optimization for Query Builder queries.

   `p.guessTotal=100` tells Query Builder to only collect only the first 100 results, and set a boolean flag indicating if at least one more results exist (but not how many more, as counting this number would be be result in slowness). This optimization excels for pagination or infinite loading use cases, where only a subset of results are incrementally displayed.

## Existing Index Tuning {#existing-index-tuning}

1. Se o query ideal for resolvido para um Índice de propriedades, não haverá mais nada a ser feito, pois os Índices de propriedades são minimamente ajustáveis.
1. Otherwise, the query should resolve to a Lucene Property Index. If no index can be resolved, jump to Creating a new Index.
1. Conforme necessário, converta o query em XPath ou JCR-SQL2.

   * **Query Builder query**

      ```js
      query type=cq:Page
      path=/content/my-site/us/en
      property=jcr:content/contentType
      property.value=article-page
      orderby=@jcr:content/publishDate
      orderby.sort=desc
      ```

   * **XPath gerado do query Construtor de Query**

      ```js
      /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
      ```

1. Forneça o XPath (ou JCR-SQL2) para o Gerador [de Definição de Índice de](https://oakutils.appspot.com/generate/index) Oak para gerar a definição otimizada do Índice de Propriedades de Lucene.

   **Generated Lucene Property Index definition**

   ```xml
   - evaluatePathRestrictions = true
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + cq:Page
           + properties
           + contentType
               - name = "jcr:content/contentType"
               - propertyIndex = true
           + publishDate
               - ordered = true
               - name = "jcr:content/publishDate"
   ```

1. Manually merge the generated definition into the existing Lucene Property Index in an additive fashion. Tenha cuidado para não remover configurações existentes, pois elas podem ser usadas para satisfazer outros query.

   1. Locate the existing Lucene Property Index that covers cq:Page (using Index Manager). In this case, `/oak:index/cqPageLucene`.
   1. Identify the configuration delta between the optimized index definition (Step #4) and the existing index (/oak:index/cqPageLucene), and add the missing configurations from the optimized Index to the existing index definition.
   1. Per AEM&#39;s Re-indexing Best Practices, either a refresh or re-index is in order, based on if existing content will be effected by this index configuration change.

## Create a New Index {#create-a-new-index}

1. Verify the query does not resolve to an existing Lucene Property Index. Se isso acontecer, consulte a seção acima sobre ajuste e índice existente.
1. Conforme necessário, converta o query em XPath ou JCR-SQL2.

   * **Query Builder query**

      ```js
      type=myApp:Author
      property=firstName
      property.value=ira
      ```

   * **XPath gerado do query Construtor de Query**

      ```js
      //element(*, myApp:Page)[@firstName = 'ira']
      ```

1. Forneça o XPath (ou JCR-SQL2) para o Gerador [de Definição de Índice de](https://oakutils.appspot.com/generate/index) Oak para gerar a definição otimizada do Índice de Propriedades de Lucene.

   **Definição do índice de propriedade do Lucene gerado**

   ```xml
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + myApp:AuthorModel
           + properties
           + firstName
               - name = "firstName"
               - propertyIndex = true
   ```

1. Deploy the generated Lucene Property Index definition.

   Add the XML definition provided by Oak Index Definition Generator for the new index to the AEM project that manages Oak index definitions (remember, treat Oak index definitions as code, since code depends on them).

   Deploy and test the new index following the usual AEM software development lifecycle and verify the query resolves to the index and the query is performant.

   Após a implantação inicial desse índice, AEM preencherá o índice com os dados necessários.

## Quando são query sem índice e transversais, ok? {#when-index-less-and-traversal-queries-are-ok}

Due to AEM&#39;s flexible content architecture, it&#39;s difficult to predict and ensure traversals of content structures will not evolve over time to be unacceptably large.

Therefore, ensure an indexes satisfy queries, except if the combination of path restriction and nodetype restriction guarantees that **less than 20 nodes are ever traversed.**

## Query Development Tools {#query-development-tools}

### Adobe Suportado {#adobe-supported}

* **Query Builder Debugger**

   * A WebUI for executing Query Builder queries and generate the supporting XPath (for use in Explain Query or Oak Index Definition Generator).
   * Located on AEM at [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - Query Tool**

   * A WebUI for executing XPath and JCR-SQL2 queries.
   * Located on AEM at [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Tools > Query...

* **[Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query)**

   * An AEM Operations dashboard that provides a detailed explanation (Query plan, query time, and # of results) for any given XPATH or JCR-SQL2 query.

* **[Slow/Popular Queries](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Um painel AEM Operations que lista os query lentos e populares recentes executados no AEM.

* **[Gerenciador de índice](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * Uma interface Web do AEM Operations que exibe os índices na instância AEM; facilita a compreensão de quais índices já existem, podem ser direcionados ou aumentados.

* **[Registro](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Query Builder logging

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Registro de execução de query Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Configuração OSGi do mecanismo de Query do Apache Jackrabbit**

   * Configuração do OSGi que configura o comportamento de falha para query de percurso.
   * Localizado no AEM em [/system/console/configMgr#org.apache.Jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * O MBean JMX usado para estimar o número de nós nas árvores de conteúdo no AEM.
   * Localizado no AEM em [/system/console/jmx/org.apache.Jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Comunidade suportada {#community-supported}

* **[Gerador de definição de índice Oak](https://oakutils.appspot.com/generate/index)**

   * Gere o índice ideal de propriedades Lucence a partir das instruções do query XPath ou JCR-SQL2.

* **[Plug-in AEM Chrome](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * A extensão do navegador da Web do Google Chrome que expõe dados de log por solicitação, incluindo query executados e seus planos de query, no console de ferramentas dev do navegador.
   * Requer que o [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) seja instalado e ativado no AEM.
