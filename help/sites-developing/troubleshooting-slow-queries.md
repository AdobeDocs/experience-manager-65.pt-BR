---
title: Solução de problemas de consultas lentas
description: Saiba como solucionar problemas de consultas lentas no Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 0%

---

# Solução de problemas de consultas lentas{#troubleshooting-slow-queries}

## Classificações de consulta lenta {#slow-query-classifications}

Há três classificações principais de consultas lentas no AEM, listadas por gravidade:

1. **Consultas sem índice**

   * Consultas que fazem **não** resolva para um índice e percorra o conteúdo do JCR para coletar resultados

1. **Consultas pouco restritas (ou com escopo)**

   * Consultas que resolvem um índice, mas devem percorrer todas as entradas de índice para coletar resultados

1. **Consultas de conjunto de resultados grandes**

   * Consultas que retornam um grande número de resultados

As duas primeiras classificações de consultas (sem índice e pouco restritas) são lentas. Elas são lentas porque forçam o mecanismo de consulta do Oak a inspecionar cada **potencial** (nó de conteúdo ou entrada de índice) para identificar quais pertencem à **real** conjunto de resultados.

O ato de inspecionar cada resultado potencial é o que é chamado de Travessia.

Como cada resultado potencial deve ser inspecionado, o custo para determinar o conjunto de resultados real cresce linearmente com o número de resultados potenciais.

A adição de restrições de consulta e índices de ajuste permite que os dados de índice sejam armazenados em um formato otimizado, permitindo uma recuperação rápida de resultados e reduz ou elimina a necessidade de inspeção linear de conjuntos de resultados em potencial.

No AEM 6.3, por padrão, quando um percurso de 100.000 é atingido, o query falha e lança uma exceção. Esse limite não existe por padrão nas versões AEM anteriores ao AEM 6.3, mas pode ser definido por meio da configuração OSGi Apache Rabbit Query Engine Settings e do bean JMX QueryEngineSettings (propriedade LimitReads).

### Detecção de consultas sem índice {#detecting-index-less-queries}

#### Durante o desenvolvimento {#during-development}

Explicar **all** consultas e garantir que seus planos de consulta não contenham a variável **/&amp;ast; traverse** explicações neles. Exemplo de plano de consulta de passagem:

* **PLANO:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Pós-implantação {#post-deployment}

* Monitore o `error.log` para consultas de percurso sem índice:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Essa mensagem só será registrada se nenhum índice estiver disponível e se a consulta potencialmente atravessar muitos nós. As mensagens não são registradas se um índice estiver disponível, mas a quantidade de passagem é pequena e, portanto, rápida.

* Visite o AEM [Desempenho da consulta](/help/sites-administering/operations-dashboard.md#query-performance) console de operações e [Explicar](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas que procuram explicação de percurso ou nenhuma consulta de índice.

### Detecção de consultas mal restritas {#detecting-poorly-restricted-queries}

#### Durante o desenvolvimento {#during-development-1}

Explique todas as consultas e verifique se elas são resolvidas em um índice ajustado para corresponder às restrições de propriedade da consulta.

* A cobertura do plano de consulta ideal tem `indexRules` para todas as restrições de propriedade e, no mínimo, para as restrições de propriedade mais rigorosas na consulta.
* As consultas que classificam os resultados devem ser resolvidas em um Índice de propriedades Lucene com regras de índice para as propriedades classificadas por propriedades que definem `orderable=true.`

#### Por exemplo, o padrão `cqPageLucene` não tem uma regra de índice para `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Antes de adicionar a regra de índice cq:tags

* **cq:regra de índice de tags**

   * Não existe pronto para uso

* **Consulta do Construtor de consultas**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=my:tag
  ```

* **Plano de consulta**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Essa consulta resolve para o `cqPageLucene` índice, mas porque não existe nenhuma regra de índice de propriedade para `jcr:content` ou `cq:tags`, quando essa restrição for avaliada, cada registro no `cqPageLucene` índice é verificado para determinar uma correspondência. Como tal, se o índice contiver 1 milhão de `cq:Page` nós, então 1 milhão de registros são verificados para determinar o conjunto de resultados.

Depois de adicionar a regra de índice cq:tags

* **cq:regra de índice de tags**

  ```js
  /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
  @name=jcr:content/cq:tags
  @propertyIndex=true
  ```

* **Consulta do Construtor de consultas**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=myTagNamespace:myTag
  ```

* **Plano de consulta**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

A adição de indexRule para `jcr:content/cq:tags` no `cqPageLucene` o índice permite `cq:tags` dados a serem armazenados de forma otimizada.

Quando uma consulta com o `jcr:content/cq:tags` for executada, o índice poderá pesquisar resultados por valor. Isso significa que se 100 `cq:Page` os nós têm `myTagNamespace:myTag` como valor, somente esses 100 resultados são retornados e os outros 999.000 são excluídos das verificações de restrição, melhorando o desempenho por um fator de 10.000.

Mais restrições de consulta reduzem os conjuntos de resultados qualificados e otimizam ainda mais a otimização da consulta.

Da mesma forma, sem uma regra de índice extra para o `cq:tags` propriedade, até mesmo uma consulta de texto completo com uma restrição em `cq:tags` teria um desempenho insatisfatório, pois os resultados do índice retornariam todas as correspondências de texto completo. A restrição em cq:tags seria filtrada após.

Outra causa da filtragem pós-índice são as Listas de controle de acesso, que muitas vezes são perdidas durante o desenvolvimento. Tente garantir que a consulta não retorne caminhos que podem ser inacessíveis para o usuário. Isso pode ser feito por uma estrutura de conteúdo melhor, juntamente com o fornecimento de restrições de caminho relevantes na consulta.

Uma maneira útil de identificar se o índice Lucene está retornando muitos resultados para retornar um pequeno subconjunto como resultado de consulta é ativar os logs DEBUG para `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`. Isso permite que você veja quantos documentos estão sendo carregados a partir do índice. O número de resultados eventuais versus o número de documentos carregados não deve ser desproporcional. Para obter mais informações, consulte [Logs](/help/sites-deploying/configure-logging.md).

#### Pós-implantação {#post-deployment-1}

* Monitore o `error.log` para consultas de percurso:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visite o AEM [Desempenho da consulta](/help/sites-administering/operations-dashboard.md#query-performance) console de operações e [Explicar](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas que procuram planos de consulta que não resolvem restrições de propriedade de consulta para regras de propriedade de índice.

### Detecção de consultas grandes de conjuntos de resultados {#detecting-large-result-set-queries}

#### Durante o desenvolvimento {#during-development-2}

Defina limites baixos para oak.queryLimitInMemory (por exemplo, 10000) e oak.queryLimitReads (por exemplo, 5000) e otimize a consulta cara ao acessar um UnsupportedOperationException dizendo &quot;A consulta leu mais do que x nós...&quot;

A definição de limites baixos ajuda a evitar consultas que consomem muitos recursos (ou seja, sem o suporte de qualquer índice ou com o suporte de um índice de cobertura menor). Por exemplo, uma consulta que lê um milhão de nós levaria a muita I/O e afetaria negativamente o desempenho geral do aplicativo. Portanto, qualquer query que falhar devido aos limites acima devem ser analisados e otimizados.

#### Pós-implantação {#post-deployment-2}

* Monitore os logs de consultas que acionam travessia de nó grande ou consumo de memória de heap grande : &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Otimize a query para reduzir o número de nós percorridos.

* Monitore os logs para consultas que acionam grande consumo de memória de heap:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Otimize o query para reduzir o consumo de memória da pilha.

Para versões do AEM 6.0 - 6.2, é possível ajustar o limite para passagem de nó por meio de parâmetros JVM no script de inicialização do AEM para evitar que grandes consultas sobrecarreguem o ambiente. Os valores recomendados são:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

No AEM 6.3, os dois parâmetros acima são pré-configurados por padrão e podem ser modificados por meio do OSGi QueryEngineSettings.

Mais informações disponíveis em : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Ajuste do desempenho da consulta {#query-performance-tuning}

O lema da otimização do desempenho da consulta no AEM é:

**&quot;Quanto mais restrições, melhor.&quot;**

Os itens a seguir descrevem ajustes recomendados para garantir o desempenho da consulta. Primeiro, ajuste a consulta, uma atividade menos invasiva e, em seguida, se necessário, ajuste as definições de índice.

### Ajustando a Instrução Query {#adjusting-the-query-statement}

O AEM é compatível com os seguintes idiomas de consulta:

* Query Builder
* JCR-SQL2
* XPath

O exemplo a seguir usa o Construtor de consultas porque é a linguagem de consulta mais comum usada por desenvolvedores do AEM. No entanto, os mesmos princípios são aplicáveis ao JCR-SQL2 e ao XPath.

1. Adicione uma restrição nodetype para que a consulta seja resolvida para um Índice de Propriedade Lucene existente.

* **Consulta não otimizada**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Consulta otimizada**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  Consultas sem uma restrição de tipo de nó forçam o AEM a assumir o `nt:base` Nodetype, que todos os nós no AEM são um subtipo de, resultando efetivamente em nenhuma restrição de nodetype.

  Configuração `type=cq:Page` restringe esta consulta a apenas `cq:Page` e resolve a consulta para AEM cqPageLucene, limitando os resultados a um subconjunto de nós (somente `cq:Page` nós) no AEM.

1. Ajuste a restrição nodetype da consulta para que a consulta seja resolvida como um Índice de propriedade Lucene existente.

* **Consulta não otimizada**

  ```js
  type=nt:hierarchyNode
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Consulta otimizada**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  `nt:hierarchyNode` é o nodetipo pai de `cq:Page`. Presumindo `jcr:content/contentType=article-page` é aplicado somente a `cq:Page` nós por meio do aplicativo personalizado Adobe, essa consulta só retorna `cq:Page` nós onde `jcr:content/contentType=article-page`. No entanto, esse fluxo é uma restrição abaixo do ideal, pois:

   * Outro nó herdado de `nt:hierarchyNode` (por exemplo, `dam:Asset`) adicionando desnecessariamente ao conjunto de resultados potenciais.
   * Não existe índice fornecido pelo AEM para `nt:hierarchyNode`, no entanto, uma vez que existe um índice `cq:Page`.

  Configuração `type=cq:Page` restringe esta consulta a apenas `cq:Page` e resolve a consulta para AEM cqPageLucene, limitando os resultados a um subconjunto de nós (somente nós cq:Page) no AEM.

1. Ou ajuste as restrições de propriedade para que a consulta seja resolvida como um Índice de propriedade existente.

* **Consulta não otimizada**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Consulta otimizada**

  ```js
  property=jcr:content/sling:resourceType
  property.value=my-site/components/structure/article-page
  ```

  Alteração da restrição de propriedade de `jcr:content/contentType` (um valor personalizado) para a propriedade bem conhecida `sling:resourceType` permite que a consulta resolva para o índice de propriedade `slingResourceType` que indexa todo o conteúdo por `sling:resourceType`.

  Os índices de propriedade (em oposição aos índices de propriedade Lucene) são usados melhor quando a consulta não discerne por nodetype e uma única restrição de propriedade domina o conjunto de resultados.

1. Adicione a restrição de caminho mais estreita possível à consulta. Por exemplo, prefira `/content/my-site/us/en` sobre `/content/my-site`ou `/content/dam` sobre `/`.

* **Consulta não otimizada**

  ```js
  type=cq:Page
  path=/content
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Consulta otimizada**

  ```js
  type=cq:Page
  path=/content/my-site/us/en
  property=jcr:content/contentType
  property.value=article-page
  ```

  Escopo da restrição de caminho de `path=/content`para `path=/content/my-site/us/en` permite que os índices reduzam o número de entradas de índice que devem ser inspecionadas. Quando a consulta pode restringir bem o caminho, além de apenas `/content` ou `/content/dam`, verifique se o índice `evaluatePathRestrictions=true`.

  Observação usando `evaluatePathRestrictions` aumenta o tamanho do índice.

1. Quando possível, evite funções de consulta e operações de consulta como: `LIKE` e `fn:XXXX` à medida que seus custos são escalonados com o número de resultados baseados em restrições.

* **Consulta não otimizada**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.operation=like
  property.value=%article%
  ```

* **Consulta otimizada**

  ```js
  type=cq:Page
  fulltext=article
  fulltext.relPath=jcr:content/contentType
  ```

  A condição LIKE é lenta para ser avaliada porque nenhum índice pode ser usado se o texto começar com um curinga (&quot;%...&#39;). A condição jcr:contains permite o uso de um índice de texto completo e, portanto, é preferível. É necessário que o Índice de Propriedade Lucene resolvido tenha indexRule para `jcr:content/contentType` com `analayzed=true`.

  Usar funções de consulta como `fn:lowercase(..)` pode ser mais difícil de otimizar, pois não há equivalentes mais rápidos (fora de configurações mais complexas e invasivas do analisador de índice). É melhor identificar outras restrições de escopo para melhorar o desempenho geral da consulta, exigindo que as funções operem no menor conjunto possível de resultados em potencial.

1. ***Esse ajuste é específico do Construtor de consultas e não se aplica a JCR-SQL2 ou XPath.***

   Uso [guessTotal do Construtor de Consulta](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) quando o conjunto completo de resultados for **não** imediatamente necessário.

   * **Consulta não otimizada**

     ```js
     type=cq:Page
     path=/content
     ```

   * **Consulta otimizada**

     ```js
     type=cq:Page
     path=/content
     p.guessTotal=100
     ```

   Para casos em que a execução da consulta é rápida, mas o número de resultados é grande, p. `guessTotal` é uma otimização crítica para consultas do Construtor de consultas.

   `p.guessTotal=100` instrui o Query Builder a coletar apenas os primeiros 100 resultados. E, para definir um sinalizador booleano indicando se pelo menos mais um resultado existe (mas não quantos mais, já que contar esse número resulta em lentidão). Essa otimização é excelente para casos de uso de paginação ou carregamento infinito, em que apenas um subconjunto de resultados é exibido de forma incremental.

## Ajuste de índice existente {#existing-index-tuning}

1. Se a consulta ideal for resolvida como um Índice de propriedade, não há mais nada a ser feito, pois os Índices de propriedade são ajustáveis minimamente.
1. Caso contrário, a consulta deve ser resolvida para um Índice de propriedades Lucene. Se nenhum índice puder ser resolvido, vá para Criação de um índice.
1. Conforme necessário, converta a consulta para XPath ou JCR-SQL2.

   * **Consulta do Construtor de consultas**

     ```js
     query type=cq:Page
     path=/content/my-site/us/en
     property=jcr:content/contentType
     property.value=article-page
     orderby=@jcr:content/publishDate
     orderby.sort=desc
     ```

   * **XPath gerado a partir da consulta do Construtor de Consultas**

     ```js
     /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
     ```

1. Forneça o XPath (ou JCR-SQL2) ao Gerador de definição de índice do Oak em `https://oakutils.appspot.com/generate/index` para que você possa gerar a definição otimizada do Índice de propriedades Lucene. <!-- The above URL is 404 as of April 24, 2023 -->

   **Definição de índice de propriedade Lucene gerada**

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

1. Mescle manualmente a definição gerada no Índice de propriedades Lucene existente de forma aditiva. Tenha cuidado para não remover configurações existentes, pois elas podem ser usadas para atender a outras consultas.

   1. Localize o Índice de propriedades Lucene existente que cobre cq:Page (usando o Gerenciador de índice). Nesse caso, `/oak:index/cqPageLucene`.
   1. Identifique o delta de configuração entre a definição de índice otimizado (Etapa #4) e o índice existente (/oak:index/cqPageLucene) e adicione as configurações ausentes do índice otimizado à definição de índice existente.
   1. De acordo com as Práticas recomendadas de reindexação de AEM, uma atualização ou reindexação está em ordem, com base no fato de o conteúdo existente poder ser afetado por essa alteração de configuração de índice.

## Criar um novo índice {#create-a-new-index}

1. Verifique se a consulta não resolve um Índice de Propriedade Lucene existente. Se isso acontecer, consulte a seção acima sobre ajuste e índice existente.
1. Conforme necessário, converta a consulta para XPath ou JCR-SQL2.

   * **Consulta do Construtor de consultas**

     ```js
     type=myApp:Author
     property=firstName
     property.value=ira
     ```

   * **XPath gerado a partir da consulta do Construtor de Consultas**

     ```js
     //element(*, myApp:Page)[@firstName = 'ira']
     ```

1. Forneça o XPath (ou JCR-SQL2) ao Gerador de definição de índice do Oak em `https://oakutils.appspot.com/generate/index` para que você possa gerar a definição otimizada do Índice de propriedades Lucene. <!-- The above URL is 404 as of April 24, 2023 -->

   **Definição de índice de propriedade Lucene gerada**

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

1. Implante a definição do Índice de propriedade Lucene gerada.

   Adicione a definição XML fornecida pelo Gerador de definição de índice Oak para o novo índice ao projeto AEM que gerencia as definições de índice Oak (lembre-se, trate as definições de índice Oak como código, já que o código depende delas).

   Implante e teste o novo índice seguindo o ciclo de vida normal de desenvolvimento de software AEM e verifique se a consulta é resolvida para o índice e se a consulta tem desempenho.

   Na implantação inicial desse índice, o AEM preenche o índice com os dados necessários.

## Quando as consultas sem índice e de percurso estão OK? {#when-index-less-and-traversal-queries-are-ok}

Devido à arquitetura de conteúdo flexível do AEM, é difícil prever e garantir que os percursos das estruturas de conteúdo não evoluam ao longo do tempo para serem inaceitavelmente grandes.

Portanto, verifique se os índices atendem a consultas, exceto se a combinação de restrição de caminho e restrição de tipo de nó garantir que **menos de 20 nós são percorridos.**

## Ferramentas de desenvolvimento de query {#query-development-tools}

### Adobe suportado {#adobe-supported}

* **Depurador do Construtor de consultas**

   * Uma WebUI para executar consultas do Construtor de consultas e gerar o XPath de suporte (para uso em Consulta de explicação ou Gerador de definição de índice Oak).
   * No AEM em [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - Ferramenta de consulta**

   * Uma WebUI para executar consultas XPath e JCR-SQL2.
   * No AEM em [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Ferramentas > Consulta...

* **[Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query)**

   * Um painel de Operações do AEM que fornece uma explicação detalhada (Plano de consulta, tempo de consulta e número de resultados) para qualquer consulta XPATH ou JCR-SQL2.

* **[Consultas lentas/populares](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Um painel de operações do AEM listando as recentes consultas lentas e populares executadas no AEM.

* **[Gerenciador de índice](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * Uma WebUI de operações de AEM que exibe os índices na instância de AEM; facilita a compreensão de quais índices existem; pode ser direcionada ou aumentada.

* **[Logs](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Log do Construtor de consultas

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`

   * Log de execução de consulta do Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`

* **Configurações de OSGi do mecanismo de consulta do Apache Jackrabbit**

   * Configuração OSGi que define o comportamento de falha para consultas de passagem.
   * No AEM em [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * MBean JMX usado para estimar o número de nós em árvores de conteúdo no AEM.
   * No AEM em [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Comunidade suportada {#community-supported}

* **Gerador de definição de índice Oak em`https://oakutils.appspot.com/generate/index`** <!-- The above URL is 404 as of April 24, 2023 -->

   * Gerar Índice de Propriedade de Lucência ideal a partir de instruções de consulta XPath ou JCR-SQL2.

* **_Plug-in AEM Chrome_** <!-- For whatever reason, the URL to this extension was causing too many redirects when doing the request so it was removed entirely to get rid of the error; users can easily look up the extension in Google instead. DO NOT ADD THE URL AGAIN!-->

   * A variável _Plug-in AEM Chrome_ é uma extensão de navegador da Web do Google Chrome que expõe dados de log por solicitação, incluindo consultas de execução e seus planos de consulta, no console de ferramentas de desenvolvimento do navegador.
   * Exige que você instale e habilite [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) sobre o AEM.
