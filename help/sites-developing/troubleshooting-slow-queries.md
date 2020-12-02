---
title: Solução de problemas de Query lentos
seo-title: Solução de problemas de Query lentos
description: 'null'
seo-description: nulo
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

1. **Query sem índice**

   * Query que **não** são resolvidos em um índice e atravessam o conteúdo do JCR para coletar resultados

1. **Query com pouca restrição (ou com escopo)**

   * Query que são resolvidos para um índice, mas devem atravessar todas as entradas de índice para coletar resultados

1. **Grandes query de conjunto de resultados**

   * Query que retornam números muito grandes de resultados

As primeiras 2 classificações de query (sem índice e com pouca restrição) são lentas, pois forçam o mecanismo de query Oak a inspecionar cada resultado **potencial** (nó de conteúdo ou entrada de índice) para identificar qual pertence ao conjunto de resultados **real**.

O ato de inspecionar cada resultado potencial é o que se chama de Navegação.

Uma vez que cada resultado potencial deve ser inspecionado, o custo para determinar o conjunto de resultados real cresce linearmente com o número de resultados potenciais.

A adição de restrições de query e índices de ajuste permite que os dados de índice sejam armazenados em um formato otimizado, permitindo uma recuperação rápida de resultados e reduz ou elimina a necessidade de inspeção linear de conjuntos de resultados potenciais.

No AEM 6.3, por padrão, quando uma passagem de 100.000 é atingida, o query falha e lança uma exceção. Esse limite não existe por padrão em versões AEM anteriores à AEM 6.3, mas pode ser definido por meio das Configurações do mecanismo de Query Apache Jackrabbit Configuração OSGi e do bean QueryEngineSettings JMX (propriedade LimitReads).

### Detecção de Query sem índice {#detecting-index-less-queries}

#### Durante o desenvolvimento {#during-development}

Explique **todos** os query e certifique-se de que seus planos de query não contêm o **/&amp;ast; explicação traverse** neles. Exemplo de plano de query de percurso:

* **PLANO:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Pós-implantação {#post-deployment}

* Monitore `error.log` para query transversais sem índice:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Essa mensagem será registrada somente se nenhum índice estiver disponível e se o query potencialmente atravessar muitos nós. As mensagens não são registradas se um índice estiver disponível, mas o valor de passagem é pequeno e, portanto, rápido.

* Visite o console de operações AEM [Desempenho do Query](/help/sites-administering/operations-dashboard.md#query-performance) e [Explique](/help/sites-administering/operations-dashboard.md#explain-query) query lentos que procuram explicações transversais ou de query de índice.

### Detecção de Query com restrições insuficientes {#detecting-poorly-restricted-queries}

#### Durante o desenvolvimento {#during-development-1}

Explique todos os query e verifique se eles foram resolvidos para um índice ajustado para corresponder às restrições de propriedade do query.

* A cobertura do plano de query ideal tem `indexRules` para todas as restrições de propriedade e, no mínimo, para as restrições de propriedade mais restritas no query.
* Query que classificam resultados devem ser resolvidos para um Índice de propriedades Lucene com regras de índice para as propriedades classificadas por `orderable=true.`

#### Por exemplo, o padrão `cqPageLucene` não tem uma regra de índice para `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Antes de adicionar a regra de índice cq:tags

* **cq:regras de índice de tags**

   * Não existe fora da caixa

* **Query Construtor de query**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **plano de query**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Este query resolve o índice `cqPageLucene`, mas como não existe uma regra de índice de propriedade para `jcr:content` ou `cq:tags`, quando esta restrição é avaliada, todos os registros no índice `cqPageLucene` são verificados para determinar uma correspondência. Isso significa que, se o índice contiver 1 milhão de nós `cq:Page`, 1 milhão de registros serão verificados para determinar o conjunto de resultados.

Após adicionar a regra de índice cq:tags

* **cq:regras de índice de tags**

   ```js
   /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
   @name=jcr:content/cq:tags
   @propertyIndex=true
   ```

* **Query Construtor de query**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=myTagNamespace:myTag
   ```

* **plano de query**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

A adição de indexRule para `jcr:content/cq:tags` no índice `cqPageLucene` permite que os dados `cq:tags` sejam armazenados de forma otimizada.

Quando um query com a restrição `jcr:content/cq:tags` é executado, o índice pode procurar os resultados por valor. Isso significa que se 100 `cq:Page` nós tiverem `myTagNamespace:myTag` como valor, apenas esses 100 resultados serão retornados e os outros 999.000 serão excluídos das verificações de restrições, melhorando o desempenho em um fator de 10.000.

É claro que novas restrições ao query reduzem os conjuntos de resultados elegíveis e otimizam ainda mais a otimização do query.

Da mesma forma, sem uma regra de índice adicional para a propriedade `cq:tags`, mesmo um query de texto completo com uma restrição em `cq:tags` teria um desempenho ruim, pois os resultados do índice retornariam todas as correspondências de texto completo. A restrição nas tags cq:seria filtrada depois.

Outra causa da filtragem pós-índice são Listas Controles de acesso que muitas vezes se perdem durante o desenvolvimento. Tente se certificar de que o query não retorne caminhos que possam estar inacessíveis ao usuário. Isso geralmente pode ser feito por uma estrutura de conteúdo melhor, além de fornecer a restrição de caminho relevante no query.

Uma maneira útil de identificar se o índice Lucene está retornando muitos resultados para retornar um subconjunto muito pequeno como resultado do query é habilitar registros DEBUG para `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` e ver quantos documentos estão sendo carregados do índice. O número de eventuais resultados versus o número de documentos carregados não deve ser desproporcionado. Para obter mais informações, consulte [Registro](/help/sites-deploying/configure-logging.md).

#### Pós-implantação {#post-deployment-1}

* Monitore `error.log` para query transversais:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visite o console de operações AEM [Desempenho do Query](/help/sites-administering/operations-dashboard.md#query-performance) e [Explique](/help/sites-administering/operations-dashboard.md#explain-query) query lentos que procuram planos de query que não resolvam as restrições de propriedade do query para indexar as regras de propriedade.

### Detectando Query de Conjunto de Resultados Grandes {#detecting-large-result-set-queries}

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

## Ajuste do desempenho do query {#query-performance-tuning}

O lema da otimização do desempenho do query no AEM é:

**&quot;Quanto mais restrições, melhor.&quot;**

A seguir, são apresentados os ajustes recomendados para garantir o desempenho do query. Primeiro ajuste o query, uma atividade menos intrusiva e, se necessário, ajuste as definições de índice.

### Ajustar a instrução do Query {#adjusting-the-query-statement}

AEM suporta os seguintes idiomas de query:

* Query Builder
* JCR-SQL2
* XPath

O exemplo a seguir usa o Construtor de Query como a linguagem de query mais comum usada pelos desenvolvedores AEM, no entanto, os mesmos princípios se aplicam ao JCR-SQL2 e XPath.

1. Adicione uma restrição de tipo de nó para que o query seja resolvido em um Índice de propriedades do Lucene existente.

* **Query não otimizado**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **Query otimizado**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   Query sem uma restrição de tipo nodetype AEM assumir o tipo de nó `nt:base`, do qual cada nó no AEM é um subtipo de, resultando efetivamente em nenhuma restrição de tipo de nó.

   A configuração `type=cq:Page` restringe esse query a apenas nós `cq:Page` e resolve o query para AEM cqPageLucene, limitando os resultados a um subconjunto de nós (somente nós `cq:Page`) no AEM.

1. Ajuste a restrição de tipo de query para que o query seja resolvido para um Índice de propriedades Lucene existente.

* **Query não otimizado**

   ```js
   type=nt:hierarchyNode
   property=jcr:content/contentType
   property.value=article-page
   ```

* **Query otimizado**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.value=article-page
   ```

   `nt:hierarchyNode` é o tipo de nó pai de  `cq:Page`e, supondo que  `jcr:content/contentType=article-page` seja aplicado somente a  `cq:Page` nós por meio de nosso aplicativo personalizado, esse query retornará apenas  `cq:Page` nós onde  `jcr:content/contentType=article-page`. No entanto, esta é uma restrição subótima, porque:

   * Outro nó herda de `nt:hierarchyNode` (por exemplo, `dam:Asset`) adicionando desnecessariamente ao conjunto de resultados potenciais.
   * Não existe um índice fornecido AEM para `nt:hierarchyNode`, no entanto, como existe um índice fornecido para `cq:Page`.
   A configuração `type=cq:Page` restringe esse query a apenas nós `cq:Page` e resolve o query para AEM cqPageLucene, limitando os resultados a um subconjunto de nós (somente nós cq:Page) no AEM.

1. Ou ajuste as restrições de propriedade para que o query seja resolvido como um Índice de propriedades existente.

* **Query não otimizado**

   ```js
   property=jcr:content/contentType
   property.value=article-page
   ```

* **Query otimizado**

   ```js
   property=jcr:content/sling:resourceType
   property.value=my-site/components/structure/article-page
   ```

   Alterar a restrição de propriedade de `jcr:content/contentType` (um valor personalizado) para a propriedade conhecida `sling:resourceType` permite que o query resolva para o índice de propriedade `slingResourceType` que indexa todo o conteúdo por `sling:resourceType`.

   Os índices de propriedade (ao contrário de Índices de propriedades Lucene) são melhor usados quando o query não é discernido por nodetype e uma única restrição de propriedade domina o conjunto de resultados.

1. Adicione a restrição de caminho mais estrita possível ao query. Por exemplo, prefira `/content/my-site/us/en` em `/content/my-site` ou `/content/dam` em `/`.

* **Query não otimizado**

   ```js
   type=cq:Page
   path=/content
   property=jcr:content/contentType
   property.value=article-page
   ```

* **Query otimizado**

   ```js
   type=cq:Page
   path=/content/my-site/us/en
   property=jcr:content/contentType
   property.value=article-page
   ```

   O escopo da restrição de caminho de `path=/content`para `path=/content/my-site/us/en` permite que os índices reduzam o número de entradas de índice que precisam ser inspecionadas. Quando o query puder restringir muito bem o caminho, além de apenas `/content` ou `/content/dam`, verifique se o índice tem `evaluatePathRestrictions=true`.

   Observe que usar `evaluatePathRestrictions` aumenta o tamanho do índice.

1. Sempre que possível, evite funções/operações do query, tais como: `LIKE` e `fn:XXXX` à medida que seus custos são dimensionados com o número de resultados baseados em restrições.

* **Query não otimizado**

   ```js
   type=cq:Page
   property=jcr:content/contentType
   property.operation=like
   property.value=%article%
   ```

* **Query otimizado**

   ```js
   type=cq:Page
   fulltext=article
   fulltext.relPath=jcr:content/contentType
   ```

   A condição LIKE é lenta para avaliação, pois nenhum índice pode ser usado se o texto start com um curinga (&quot;%...&#39;). A condição jcr:contains permite o uso de um índice de texto completo e, portanto, é preferida. Isso requer que o Índice de propriedades de Lucene resolvido tenha indexRule para `jcr:content/contentType` com `analayzed=true`.

   O uso de funções de query como `fn:lowercase(..)` pode ser mais difícil de otimizar, pois não há equivalentes mais rápidos (fora das configurações mais complexas e discretas do analisador de índice). É melhor identificar outras restrições de escopo para melhorar o desempenho geral do query, exigindo que as funções funcionem no menor conjunto possível de resultados potenciais.

1. ***Esse ajuste é específico do Construtor de Query e não se aplica a JCR-SQL2 ou XPath.***

   Use [palavras-chave do Construtor de Query&#39;, oTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) quando o conjunto completo de resultados for **e não** necessário imediatamente.

   * **Query não otimizado**

      ```js
      type=cq:Page
      path=/content
      ```

   * **Query otimizado**

      ```js
      type=cq:Page
      path=/content
      p.guessTotal=100
      ```
   Nos casos em que a execução do query é rápida, mas o número de resultados é grande, p. `guessTotal` é uma otimização crítica para query do Construtor de Query.

   `p.guessTotal=100` instrui o Construtor de Query a coletar apenas os primeiros 100 resultados e a definir um sinalizador booleano indicando se existem pelo menos mais um resultado (mas não quantos mais, já que a contagem desse número resultaria em lentidão). Essa otimização se sobressai para paginação ou casos de uso de carregamento infinito, onde apenas um subconjunto de resultados é exibido incrementalmente.

## Ajuste de índice existente {#existing-index-tuning}

1. Se o query ideal for resolvido para um Índice de propriedades, não haverá mais nada a ser feito, pois os Índices de propriedades são minimamente ajustáveis.
1. Caso contrário, o query deve ser resolvido como um Índice de propriedades do Lucene. Se nenhum índice puder ser resolvido, vá para Criar um novo índice.
1. Conforme necessário, converta o query em XPath ou JCR-SQL2.

   * **Query Construtor de query**

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

1. Forneça o XPath (ou JCR-SQL2) para [Oak Index Definition Generator](https://oakutils.appspot.com/generate/index) gerar a definição otimizada do Índice de Propriedades do Lucene.

   **Definição do índice de propriedade do Lucene gerado**

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

1. Unir manualmente a definição gerada no Índice de propriedades do Lucene existente de forma aditiva. Tenha cuidado para não remover configurações existentes, pois elas podem ser usadas para satisfazer outros query.

   1. Localize o Índice de propriedades do Lucene existente que abrange cq:Page (usando o Gerenciador de índice). Nesse caso, `/oak:index/cqPageLucene`.
   1. Identifique o delta de configuração entre a definição de índice otimizada (Etapa 4) e o índice existente (/oak:index/cqPageLucene) e adicione as configurações ausentes do Índice otimizado à definição de índice existente.
   1. Por AEM Práticas recomendadas de reindexação, uma atualização ou reindexação está em ordem, com base em se o conteúdo existente será afetado por essa alteração de configuração de índice.

## Criar um novo índice {#create-a-new-index}

1. Verifique se o query não é resolvido para um Índice de propriedades do Lucene existente. Se isso acontecer, consulte a seção acima sobre ajuste e índice existente.
1. Conforme necessário, converta o query em XPath ou JCR-SQL2.

   * **Query Construtor de query**

      ```js
      type=myApp:Author
      property=firstName
      property.value=ira
      ```

   * **XPath gerado do query Construtor de Query**

      ```js
      //element(*, myApp:Page)[@firstName = 'ira']
      ```

1. Forneça o XPath (ou JCR-SQL2) para [Oak Index Definition Generator](https://oakutils.appspot.com/generate/index) gerar a definição otimizada do Índice de Propriedades do Lucene.

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

1. Implante a definição gerada do Índice de propriedades do Lucene.

   Adicione a definição XML fornecida pelo Oak Index Definition Generator para o novo índice ao projeto AEM que gerencia as definições de índice Oak (lembre-se de tratar as definições de índice Oak como código, já que o código depende delas).

   Implante e teste o novo índice após o ciclo de vida normal de desenvolvimento do software AEM e verifique se o query é resolvido no índice e se o query é executado.

   Após a implantação inicial desse índice, AEM preencherá o índice com os dados necessários.

## Quando são query sem índice e transversais, ok? {#when-index-less-and-traversal-queries-are-ok}

Devido à AEM arquitetura de conteúdo flexível, é difícil prever e garantir que os cruzamentos entre estruturas de conteúdo não evoluam ao longo do tempo para serem inaceitavelmente grandes.

Portanto, verifique se um índice atende aos query, exceto se a combinação de restrição de caminho e restrição de tipo de nó garantir que **menos de 20 nós já tenham sido atravessados.**

## Ferramentas de desenvolvimento de query {#query-development-tools}

### Adobe Suportado {#adobe-supported}

* **Depurador do Construtor de query**

   * Uma WebUI para executar query do Construtor de Query e gerar o XPath de suporte (para uso em Explorar Query ou Oak Index Definition Generator).
   * Localizado no AEM em [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - Ferramenta Query**

   * Uma WebUI para executar query XPath e JCR-SQL2.
   * Localizado em AEM em [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Ferramentas > Query...

* **[Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query)**

   * Um painel AEM Operations que fornece uma explicação detalhada (plano do Query, tempo do query e número de resultados) para qualquer query XPATH ou JCR-SQL2.

* **[Query lentos/populares](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Um painel AEM Operations que lista os query lentos e populares recentes executados no AEM.

* **[Gerenciador de índice](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * Uma interface Web do AEM Operations que exibe os índices na instância AEM; facilita a compreensão de quais índices já existem, podem ser direcionados ou aumentados.

* **[Logs](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Registro do Construtor de query

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Registro de execução de query Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Configuração OSGi do mecanismo de Query do Apache Jackrabbit**

   * Configuração do OSGi que configura o comportamento de falha para query de percurso.
   * Localizado no AEM em [/system/console/configMgr#org.apache.Jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * O MBean JMX usado para estimar o número de nós nas árvores de conteúdo no AEM.
   * Localizado em AEM em [/system/console/jmx/org.apache.Jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Comunidade suportada {#community-supported}

* **[Gerador de definição de índice Oak](https://oakutils.appspot.com/generate/index)**

   * Gere o índice ideal de propriedades Lucence a partir das instruções do query XPath ou JCR-SQL2.

* **[Plug-in AEM Chrome](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * A extensão do navegador da Web do Google Chrome que expõe dados de log por solicitação, incluindo query executados e seus planos de query, no console de ferramentas dev do navegador.
   * Requer que [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) seja instalado e ativado no AEM.
