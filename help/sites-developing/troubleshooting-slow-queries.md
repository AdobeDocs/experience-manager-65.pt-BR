---
title: Solução de problemas de consultas lentas
seo-title: Solução de problemas de consultas lentas
description: Solução de problemas de consultas lentas
seo-description: 'null'
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2269'
ht-degree: 0%

---


# Solução de problemas de consultas lentas{#troubleshooting-slow-queries}

## Classificações de consulta lentas {#slow-query-classifications}

Há 3 classificações principais de consultas lentas no AEM, listadas por gravidade:

1. **Consultas sem índice**

   * Consultas que **not** resolvem para um índice e atravessam o conteúdo do JCR para coletar resultados

1. **Consultas restritas incorretamente (ou com escopo)**

   * Consultas que são resolvidas em um índice, mas devem atravessar todas as entradas de índice para coletar resultados

1. **Grandes consultas de conjunto de resultados**

   * Consultas que retornam números muito grandes de resultados

As primeiras 2 classificações de consultas (sem índice e pouco restritas) são lentas, pois forçam o mecanismo de consulta Oak a inspecionar cada resultado **potencial** (nó de conteúdo ou entrada de índice) para identificar qual pertence ao conjunto de resultados **real**.

O ato de inspecionar cada resultado potencial é o chamado Traversing.

Uma vez que cada resultado potencial deve ser inspecionado, o custo para determinar o conjunto de resultados real cresce linearmente com o número de resultados potenciais.

A adição de restrições de consulta e índices de ajuste permite que os dados do índice sejam armazenados em um formato otimizado, permitindo uma recuperação rápida do resultado e reduz ou elimina a necessidade da inspeção linear de conjuntos de resultados potenciais.

No AEM 6.3, por padrão, quando uma travessia de 100.000 é atingida, o query falha e gera uma exceção. Esse limite não existe por padrão nas versões AEM anteriores ao AEM 6.3, mas pode ser definido por meio das Configurações do mecanismo de consulta Apache Jackrabbit Configuração OSGi e QueryEngineSettings JMX bean (propriedade LimitReads).

### Detectando consultas sem índice {#detecting-index-less-queries}

#### Durante o desenvolvimento {#during-development}

Explicar **todas as** consultas e garantir que seus planos de consulta não contenham o **/&amp;ast; explicação traverse** neles. Exemplo de plano de consulta de percurso:

* **PLANO:** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Pós-implantação {#post-deployment}

* Monitore o `error.log` para consultas transversais sem índice:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Essa mensagem só será registrada se nenhum índice estiver disponível e se a consulta potencialmente atravessar muitos nós. As mensagens não são registradas se um índice estiver disponível, mas a quantidade de travamento é pequena e, portanto, rápida.

* Visite o AEM console [Desempenho da Consulta](/help/sites-administering/operations-dashboard.md#query-performance) e [Explicar](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas procurando traversal ou nenhuma explicação de consulta de índice.

### Detectando Consultas Mal Restritas {#detecting-poorly-restricted-queries}

#### Durante o desenvolvimento {#during-development-1}

Explicar todas as consultas e garantir que elas sejam resolvidas em um índice ajustado para corresponder às restrições de propriedade da consulta.

* A cobertura do plano de consulta ideal tem `indexRules` para todas as restrições de propriedade e, no mínimo, para as restrições de propriedade mais restritas na query.
* As consultas que classificam resultados devem ser resolvidas para um Índice de propriedades do Lucene com regras de índice para as propriedades classificadas por que definem `orderable=true.`

#### Por exemplo, o padrão `cqPageLucene` não tem uma regra de índice para `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Antes de adicionar a regra de índice cq:tags

* **cq:tags Regra de índice**

   * Não existe imediatamente

* **Query Builder**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **Plano de consulta**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Esta consulta resolve o índice `cqPageLucene`, mas como nenhuma regra de índice de propriedade existe para `jcr:content` ou `cq:tags`, quando essa restrição é avaliada, cada registro no índice `cqPageLucene` é verificado para determinar uma correspondência. Isso significa que, se o índice contiver 1 milhão de nós `cq:Page`, 1 milhão de registros serão verificados para determinar o conjunto de resultados.

Após adicionar a regra de índice cq:tags

* **cq:tags Regra de índice**

   ```js
   /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
   @name=jcr:content/cq:tags
   @propertyIndex=true
   ```

* **Query Builder**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=myTagNamespace:myTag
   ```

* **Plano de consulta**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

A adição do indexRule para `jcr:content/cq:tags` no índice `cqPageLucene` permite que os dados `cq:tags` sejam armazenados de maneira otimizada.

Quando uma consulta com a restrição `jcr:content/cq:tags` é executada, o índice pode procurar resultados por valor. Isso significa que se 100 `cq:Page` nós tiverem `myTagNamespace:myTag` como um valor, apenas esses 100 resultados serão retornados e os outros 999.000 serão excluídos das verificações de restrição, melhorando o desempenho em um fator de 10.000.

É claro que outras restrições de query reduzem os conjuntos de resultados qualificados e otimizam ainda mais a otimização de query.

Da mesma forma, sem uma regra de índice adicional para a propriedade `cq:tags`, mesmo uma consulta de texto completo com uma restrição em `cq:tags` teria um desempenho inadequado, pois os resultados do índice retornariam todas as correspondências de texto completo. A restrição em cq:tags seria filtrada depois.

Outra causa da filtragem pós-índice são as Listas de Controle de Acesso que geralmente são perdidas durante o desenvolvimento. Tente garantir que a consulta não retorne caminhos que possam estar inacessíveis ao usuário. Isso geralmente pode ser feito por uma melhor estrutura de conteúdo, juntamente com a disponibilização de uma restrição de caminho relevante na query.

Uma maneira útil de identificar se o índice Lucene está retornando muitos resultados para retornar um subconjunto muito pequeno como resultado de query é ativar logs DEBUG para `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` e ver quantos documentos estão sendo carregados do índice. O número de eventuais resultados versus o número de documentos carregados não deve ser desproporcionado. Para obter mais informações, consulte [Registro](/help/sites-deploying/configure-logging.md).

#### Pós-implantação {#post-deployment-1}

* Monitore o `error.log` para consultas transversais:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visite o console AEM [Desempenho da Consulta](/help/sites-administering/operations-dashboard.md#query-performance) e [Explicar](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas procurando por planos de consulta que não resolvem as restrições de propriedade de consulta para indexar regras de propriedade.

### Detectando consultas de conjunto de resultados grandes {#detecting-large-result-set-queries}

#### Durante o desenvolvimento {#during-development-2}

Defina limites baixos para oak.queryLimitInMemory (por exemplo, 10000) e oak.queryLimitReads (por exemplo, 5000) e otimizar a consulta cara ao hit de um UnsupportedOperationException dizendo &quot;A consulta leu mais de x nós...&quot;

Isso ajuda a evitar consultas que consomem muitos recursos (ou seja, não é suportada por qualquer índice ou pelo índice de cobertura inferior). Por exemplo, uma consulta que lê nós 1M levaria a muitas E/S e afetaria negativamente o desempenho geral do aplicativo. Portanto, qualquer query que falhe devido a limites acima deve ser analisada e otimizada.

#### Pós-implantação {#post-deployment-2}

* Monitore os logs para consultas que acionam grande passagem de nó ou grande consumo de memória heap : &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Otimizar a consulta para reduzir o número de nós atravessados

* Monitore os logs para consultas que acionam grande consumo de memória heap :

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Otimizar a consulta para reduzir o consumo de memória heap

Para AEM versões 6.0 - 6.2, você pode ajustar o limite para a travessia do nó por meio de parâmetros da JVM no script de início de AEM para impedir que consultas grandes sobrecarreguem o ambiente. Os valores recomendados são :

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

No AEM 6.3, os 2 parâmetros acima são pré-configurados por padrão e podem ser modificados por meio do QueryEngineSettings do OSGi.

Mais informações disponíveis em : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Ajuste do desempenho da consulta {#query-performance-tuning}

O lema da otimização de desempenho de consulta no AEM é:

**&quot;Quanto mais restrições, melhor.&quot;**

A seguir, são apresentados os ajustes recomendados para garantir o desempenho da consulta. Primeiro ajuste a consulta, uma atividade menos intrusiva e, em seguida, se necessário, ajuste as definições de índice.

### Ajustando a instrução de consulta {#adjusting-the-query-statement}

AEM suporta os seguintes idiomas de consulta:

* Query Builder
* JCR-SQL2
* XPath

O exemplo a seguir usa o Query Builder como a linguagem de consulta mais comum usada por AEM desenvolvedores, no entanto, os mesmos princípios são aplicáveis a JCR-SQL2 e XPath.

1. Adicione uma restrição do tipo de nó para que a consulta resolva para um Índice de propriedades do Lucene existente.

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

   Consultas sem uma força de restrição de tipo de nó AEM assumir o tipo de nó `nt:base`, que cada nó no AEM é um subtipo de, resultando efetivamente em nenhuma restrição de tipo de nó.

   Configurar `type=cq:Page` restringe esta consulta a apenas nós `cq:Page` e resolve a consulta para AEM cqPageLucene, limitando os resultados a um subconjunto de nós (somente nós `cq:Page`) em AEM.

1. Ajuste a restrição do tipo de nó da consulta para que ela seja resolvida para um Índice de propriedades Lucene existente.

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

   `nt:hierarchyNode` é o tipo de nó pai de  `cq:Page`, e supondo que  `jcr:content/contentType=article-page` seja aplicado somente a  `cq:Page` nós por meio de nosso aplicativo personalizado, essa consulta retornará apenas  `cq:Page` nós onde  `jcr:content/contentType=article-page`. No entanto, essa é uma restrição subideal, pois:

   * Outro nó herda de `nt:hierarchyNode` (por exemplo, `dam:Asset`) adicionar desnecessariamente ao conjunto de resultados potenciais.
   * Não existe um índice fornecido AEM para `nt:hierarchyNode`, no entanto, já que há um índice fornecido para `cq:Page`.
   Configurar `type=cq:Page` restringe esta consulta a apenas nós `cq:Page` e resolve a consulta para AEM cqPageLucene, limitando os resultados a um subconjunto de nós (somente nós cq:Page) em AEM.

1. Ou ajuste as restrições de propriedade para que a consulta resolva para um Índice de propriedades existente.

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

   Alterar a restrição de propriedade de `jcr:content/contentType` (um valor personalizado) para a propriedade conhecida `sling:resourceType` permite que a query resolva para o índice de propriedade `slingResourceType` que indexa todo o conteúdo por `sling:resourceType`.

   Os índices de propriedade (em vez de Índices de propriedades do Lucene) são melhor usados quando a consulta não é discernível por tipo de nó e uma única restrição de propriedade domina o conjunto de resultados.

1. Adicione a restrição de caminho mais estrita possível ao query. Por exemplo, prefira `/content/my-site/us/en` em `/content/my-site` ou `/content/dam` em vez de `/`.

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

   O escopo da restrição de caminho de `path=/content`para `path=/content/my-site/us/en` permite que os índices reduzam o número de entradas de índice que precisam ser inspecionadas. Quando a query puder restringir muito bem o caminho, além de `/content` ou `/content/dam`, verifique se o índice tem `evaluatePathRestrictions=true`.

   Observe que usar `evaluatePathRestrictions` aumenta o tamanho do índice.

1. Sempre que possível, evite funções/operações de query como: `LIKE` e `fn:XXXX`, pois seus custos são escaláveis com o número de resultados baseados em restrições.

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

   A condição LIKE é lenta para avaliar, pois nenhum índice pode ser usado se o texto começar com um curinga (&quot;%..&#39;). A condição jcr:contains permite usar um índice de texto completo e, portanto, é preferível. Isso requer que o Índice de propriedades do Lucene resolvido tenha indexRule para `jcr:content/contentType` com `analayzed=true`.

   O uso de funções de consulta como `fn:lowercase(..)` pode ser mais difícil de otimizar, pois não há equivalentes mais rápidos (fora das configurações mais complexas e discretas do analisador de índice). É melhor identificar outras restrições de escopo para melhorar o desempenho geral da consulta, exigindo que as funções operem no menor conjunto possível de resultados potenciais.

1. ***Esse ajuste é específico do Query Builder e não se aplica a JCR-SQL2 ou XPath.***

   Use [ViewTotal do Construtor de Consultas](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) quando o conjunto completo de resultados for **não** necessário imediatamente.

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
   Para casos em que a execução da consulta é rápida, mas o número de resultados é grande, p `guessTotal` é uma otimização crítica para consultas do Query Builder.

   `p.guessTotal=100` instrui o Query Builder a coletar apenas os primeiros 100 resultados e definir um sinalizador booleano indicando se existem pelo menos mais um resultado (mas não quantos mais, já que a contagem desse número resultaria em lentidão). Essa otimização se sobressai para paginação ou casos de uso de carregamento infinito, onde apenas um subconjunto de resultados é exibido de forma incremental.

## Ajuste de índice existente {#existing-index-tuning}

1. Se a consulta ideal for resolvida para um Índice de propriedades, não há mais nada para fazer, pois os Índices de propriedades são minimamente ajustáveis.
1. Caso contrário, a consulta deve ser resolvida para um Índice de propriedades do Lucene. Se nenhum índice puder ser resolvido, vá para Criação de um novo Índice.
1. Conforme necessário, converta a consulta para XPath ou JCR-SQL2.

   * **Query Builder**

      ```js
      query type=cq:Page
      path=/content/my-site/us/en
      property=jcr:content/contentType
      property.value=article-page
      orderby=@jcr:content/publishDate
      orderby.sort=desc
      ```

   * **XPath gerado da consulta do Query Builder**

      ```js
      /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
      ```

1. Forneça o XPath (ou JCR-SQL2) para [Oak Index Definition Generator](https://oakutils.appspot.com/generate/index) para gerar a definição otimizada do Índice de propriedades do Lucene.

   **Definição de índice de propriedade do Lucene gerada**

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

1. Mescle manualmente a definição gerada no Índice de propriedades do Lucene existente de forma aditiva. Tenha cuidado para não remover configurações existentes, pois elas podem ser usadas para atender a outros queries.

   1. Localize o Índice de propriedades do Lucene existente que abrange cq:Page (usando o Gerenciador de índices). Nesse caso, `/oak:index/cqPageLucene`.
   1. Identifique o delta de configuração entre a definição de índice otimizada (Etapa 4) e o índice existente (/oak:index/cqPageLucene) e adicione as configurações ausentes do Índice otimizado à definição de índice existente.
   1. De acordo com AEM Práticas recomendadas de reindexação, uma atualização ou reindexação está em ordem, com base em se o conteúdo existente será afetado por essa alteração de configuração de índice.

## Criar um novo índice {#create-a-new-index}

1. Verifique se a consulta não resolve um Índice de propriedades do Lucene existente. Se isso acontecer, consulte a seção acima sobre ajuste e índice existente.
1. Conforme necessário, converta a consulta para XPath ou JCR-SQL2.

   * **Query Builder**

      ```js
      type=myApp:Author
      property=firstName
      property.value=ira
      ```

   * **XPath gerado da consulta do Query Builder**

      ```js
      //element(*, myApp:Page)[@firstName = 'ira']
      ```

1. Forneça o XPath (ou JCR-SQL2) para [Oak Index Definition Generator](https://oakutils.appspot.com/generate/index) para gerar a definição otimizada do Índice de propriedades do Lucene.

   **Definição de índice de propriedade do Lucene gerada**

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

1. Implante a definição do Índice de propriedades do Lucene gerado.

   Adicione a definição XML fornecida pelo Gerador de Definição de Índice Oak para o novo índice ao projeto AEM que gerencia as definições de índice Oak (lembre-se de tratar as definições de índice Oak como código, já que o código depende delas).

   Implante e teste o novo índice seguindo o ciclo de vida normal de desenvolvimento de software AEM e verifique se a consulta resolve o índice e se a consulta é executada.

   Após a implantação inicial desse índice, o AEM preencherá o índice com os dados necessários.

## Quando as consultas de índice e travessia estão corretas? {#when-index-less-and-traversal-queries-are-ok}

Devido a AEM arquitetura de conteúdo flexível, é difícil prever e garantir que as travessias das estruturas de conteúdo não evoluam ao longo do tempo para serem inaceitavelmente grandes.

Portanto, assegure-se de que um índice atenda a queries, exceto se a combinação de restrição de caminho e restrição de tipo de nó garantir que **menos de 20 nós nunca serão atravessados.**

## Ferramentas de Desenvolvimento de Consulta {#query-development-tools}

### Adobe Suportado {#adobe-supported}

* **Query Builder Debugger**

   * Uma WebUI para executar consultas do Query Builder e gerar o XPath de suporte (para uso em Explain Query ou Oak Index Definition Generator).
   * Localizado em AEM em [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - Ferramenta de consulta**

   * Uma WebUI para executar consultas XPath e JCR-SQL2.
   * Localizado em AEM em [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Ferramentas > Consulta...

* **[Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query)**

   * Um painel de Operações de AEM que fornece uma explicação detalhada (Plano de consulta, tempo de consulta e número de resultados) para qualquer consulta XPATH ou JCR-SQL2 específica.

* **[Consultas lentas/populares](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Um painel AEM Operations listando as consultas lentas e populares recentes executadas em AEM.

* **[Gerenciador de índice](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * Uma WebUI AEM Operations exibindo os índices na instância AEM; facilita a compreensão de quais índices já existem, podem ser direcionados ou aumentados.

* **[Logs](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Registro do construtor de consultas

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Log de execução da consulta Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Configuração OSGi das configurações do mecanismo de consulta Apache Jackrabbit**

   * Configuração do OSGi que configura o comportamento de falha para consultas de percurso.
   * Localizado em AEM em [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **Mbean JMX NodeCounter**

   * MBean JMX usado para estimar o número de nós em árvores de conteúdo em AEM.
   * Localizado em AEM em [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Comunidade suportada {#community-supported}

* **[Gerador de definição de índice Oak](https://oakutils.appspot.com/generate/index)**

   * Gere o índice ideal de propriedades do Lucence a partir das instruções de consulta XPath ou JCR-SQL2.

* **[Plug-in do AEM Chrome](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * A extensão do navegador da Web Google Chrome que expõe os dados de log por solicitação, incluindo consultas executadas e seus planos de query, no console de ferramentas dev do navegador.
   * Requer que [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) seja instalado e ativado no AEM.
