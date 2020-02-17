---
title: Solução de problemas de consultas lentas
seo-title: Solução de problemas de consultas lentas
description: 'null'
seo-description: 'null'
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Solução de problemas de consultas lentas{#troubleshooting-slow-queries}

## Classificações de consulta lentas {#slow-query-classifications}

Há três classificações principais de consultas lentas no AEM, listadas por gravidade:

1. **Consultas sem índice**

   * Consultas que **não** são resolvidas para um índice e navegam pelo conteúdo do JCR para coletar resultados

1. **Consultas restritas incorretamente (ou com escopo)**

   * Consultas que são resolvidas para um índice, mas devem atravessar todas as entradas de índice para coletar resultados

1. **Consultas de conjunto de resultados grandes**

   * Consultas que retornam números muito grandes de resultados

As primeiras 2 classificações de consultas (sem índice e com pouca restrição) são lentas, pois forçam o mecanismo de consulta Oak a inspecionar cada resultado **potencial** (nó de conteúdo ou entrada de índice) para identificar qual pertence ao conjunto de resultados **real** .

O ato de inspecionar cada resultado potencial é o que se chama de Navegação.

Uma vez que cada resultado potencial deve ser inspecionado, o custo para determinar o conjunto de resultados real cresce linearmente com o número de resultados potenciais.

A adição de restrições de consulta e índices de ajuste permite que os dados de índice sejam armazenados em um formato otimizado, permitindo uma rápida recuperação de resultados e reduz ou elimina a necessidade de inspeção linear de conjuntos de resultados potenciais.

No AEM 6.3, por padrão, quando uma passagem de 100.000 é atingida, a consulta falha e lança uma exceção. Esse limite não existe por padrão nas versões do AEM anteriores ao AEM 6.3, mas pode ser definido por meio das Configurações do mecanismo de consulta do Apache Jackrabbit Configuração do OSGi e do bean QueryEngineSettings JMX (propriedade LimitReads).

### Detectando consultas sem índice {#detecting-index-less-queries}

#### Durante o desenvolvimento {#during-development}

Explicar **todas** as consultas e garantir que seus planos de consulta não contenham o **/&amp;ast; uma explicação transversal** . Exemplo de plano de consulta de percurso:

* **** PLANO: `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Pós-implantação {#post-deployment}

* Monitore o `error.log` para consultas transversais sem índice:

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Essa mensagem será registrada somente se nenhum índice estiver disponível e se a consulta potencialmente atravessar muitos nós. As mensagens não são registradas se um índice estiver disponível, mas o valor de passagem é pequeno e, portanto, rápido.

* Visite o console de operações de Desempenho [de](/help/sites-administering/operations-dashboard.md#query-performance) consulta do AEM e [explique](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas que procuram explicações de consulta de índice ou transversais.

### Detecção de Consultas Restritas {#detecting-poorly-restricted-queries}

#### Durante o desenvolvimento {#during-development-1}

Explique todas as consultas e verifique se elas foram resolvidas para um índice ajustado para corresponder às restrições de propriedade da consulta.

* A cobertura do plano de consulta ideal tem `indexRules` para todas as restrições de propriedade e, no mínimo, para as restrições de propriedade mais restritas na consulta.
* As consultas que classificam os resultados devem ser resolvidas para um Índice de propriedades Lucene com regras de índice para as propriedades classificadas por `orderable=true.`

#### Por exemplo, o padrão `cqPageLucene` não tem uma regra de índice para `jcr:content/cq:tags`{#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Antes de adicionar a regra de índice cq:tags

* **cq:regras de índice de tags**

   * Não existe fora da caixa

* **Consulta do Construtor de consultas**

   * 
      ```
      type=cq:Page
       property=jcr:content/cq:tags
       property.value=my:tag
      ```

* **Plano de consulta**

   * `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Essa consulta é resolvida para o `cqPageLucene` índice, mas como não existe uma regra de índice de propriedade para `jcr:content` ou `cq:tags`, quando essa restrição é avaliada, todos os registros no `cqPageLucene` índice são verificados para determinar uma correspondência. Isso significa que se o índice contiver 1 milhão de `cq:Page` nós, 1 milhão de registros serão verificados para determinar o conjunto de resultados.

Após adicionar a regra de índice cq:tags

* **cq:regras de índice de tags**

   * 
      ```
      /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
       @name=jcr:content/cq:tags
       @propertyIndex=true
      ```

* **Consulta do Construtor de consultas**

   * 
      ```
      type=cq:Page
       property=jcr:content/cq:tags
       property.value=myTagNamespace:myTag
      ```

* **Plano de consulta**

   * `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

A adição de indexRule para `jcr:content/cq:tags` no `cqPageLucene` índice permite que `cq:tags` os dados sejam armazenados de forma otimizada.

Quando uma consulta com a `jcr:content/cq:tags` restrição é executada, o índice pode procurar resultados por valor. Isso significa que se 100 `cq:Page` nós tiverem `myTagNamespace:myTag` como valor, apenas esses 100 resultados serão retornados, e os outros 999.000 serão excluídos das verificações de restrições, melhorando o desempenho em um fator de 10.000.

É claro que outras restrições de consulta reduzem os conjuntos de resultados elegíveis e otimizam ainda mais a otimização de consulta.

Da mesma forma, sem uma regra de índice adicional para a `cq:tags` propriedade, mesmo uma consulta de texto completo com uma restrição ativada `cq:tags` teria um desempenho ruim, já que os resultados do índice retornariam todas as correspondências de texto completo. A restrição nas tags cq:seria filtrada depois.

Outra causa da filtragem pós-índice é as Listas de Controle de Acesso que geralmente são perdidas durante o desenvolvimento. Tente garantir que a consulta não retorne caminhos que possam estar inacessíveis ao usuário. Isso geralmente pode ser feito por uma melhor estrutura de conteúdo, além de fornecer a restrição de caminho relevante na consulta.

Uma maneira útil de identificar se o índice Lucene está retornando muitos resultados para retornar um subconjunto muito pequeno como resultado da consulta é ativar os registros DEBUG para `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` e ver quantos documentos estão sendo carregados do índice. O número de resultados finais versus o número de documentos carregados não deve ser desproporcionado. For more information, see [Logging](/help/sites-deploying/configure-logging.md).

#### Pós-implantação {#post-deployment-1}

* Monitore as consultas `error.log` transversais:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visite o console de operações de Desempenho [de](/help/sites-administering/operations-dashboard.md#query-performance) consulta do AEM e [explique](/help/sites-administering/operations-dashboard.md#explain-query) consultas lentas que buscam planos de consulta que não resolvam restrições de propriedade de consulta para indexar regras de propriedade.

### Detecção de Consultas de Conjunto de Resultados Grandes {#detecting-large-result-set-queries}

#### Durante o desenvolvimento {#during-development-2}

Defina limites baixos para oak.queryLimitInMemory (por exemplo, 10000) e oak.queryLimitReads (por exemplo, 5000) e otimize a consulta cara ao clicar em UnsupportedOperationException dizendo &quot;A consulta leu mais de x nós...&quot;

Isso ajuda a evitar consultas de uso intensivo de recursos (ou seja, não suportado por qualquer índice ou apoiado por um índice de cobertura menor). Por exemplo, uma consulta que lê nós 1M levaria a muitas E/S e afetaria negativamente o desempenho geral do aplicativo. Portanto, qualquer consulta que falhe devido aos limites acima deve ser analisada e otimizada.

#### Pós-implantação {#post-deployment-2}

* Monitore os registros para obter consultas que acionam o grande consumo de memória do nó transversal ou grande: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Otimizar a consulta para reduzir o número de nós atravessados

* Monitore os registros para obter consultas que acionam grande consumo de memória heap:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Otimizar a consulta para reduzir o consumo de memória heap

Para versões do AEM 6.0 - 6.2, é possível ajustar o limite para a passagem de nó pelos parâmetros JVM no script de início do AEM para impedir que consultas grandes sobrecarreguem o ambiente. Os valores recomendados são:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

No AEM 6.3, os 2 parâmetros acima são pré-configurados por padrão e podem ser modificados por meio do OSGi QueryEngineSettings.

Mais informações disponíveis em: [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Ajuste do desempenho da consulta {#query-performance-tuning}

O lema da otimização do desempenho da consulta no AEM é:

**&quot;Quanto mais restrições, melhor.&quot;**

O seguinte descreve os ajustes recomendados para garantir o desempenho da consulta. Primeiro ajuste a consulta, uma atividade menos intrusiva e, em seguida, se necessário, ajuste as definições de índice.

### Ajustando a Instrução de Consulta {#adjusting-the-query-statement}

O AEM oferece suporte aos seguintes idiomas de consulta:

* Query Builder
* JCR-SQL2
* XPath

O exemplo a seguir usa o Query Builder como a linguagem de consulta mais comum usada pelos desenvolvedores do AEM, no entanto, os mesmos princípios se aplicam ao JCR-SQL2 e XPath.

1. Adicione uma restrição de tipo de nó para que a consulta seja resolvida em um Índice de propriedades do Lucene existente.

   * **Consulta não otimizada**

      * 
         ```
          property=jcr:content/contentType
          property.value=article-page
         ```
   * **Consulta otimizada**

      * 
         ```
          type=cq:Page
          property=jcr:content/contentType
          property.value=article-page
         ```
   As consultas sem uma restrição de tipo de nó obrigam o AEM a assumir o `nt:base` tipo de nó, que cada nó no AEM é um subtipo de, resultando efetivamente em nenhuma restrição de tipo de nó.

   A configuração `type=cq:Page` restringe essa consulta a apenas `cq:Page` nós e resolve a consulta para o cqPageLucene do AEM, limitando os resultados a um subconjunto de nós (somente `cq:Page` nós) no AEM.

1. Ajuste a restrição de tipo de nó da consulta para que ela seja resolvida em um Índice de propriedades Lucene existente.

   * **Consulta não otimizada**

      * 
         ```
         type=nt:hierarchyNode
         property=jcr:content/contentType
         property.value=article-page
         ```
   * **Consulta otimizada**

      * 
         ```
         type=cq:Page
         property=jcr:content/contentType
         property.value=article-page
         ```
   `nt:hierarchyNode` é o tipo de nó pai de `cq:Page`, e supondo que `jcr:content/contentType=article-page` seja aplicado somente a `cq:Page` nós por meio de nosso aplicativo personalizado, essa consulta retornará apenas `cq:Page` nós onde `jcr:content/contentType=article-page`. No entanto, esta é uma restrição subótima porque:

   * Outro nó herda de `nt:hierarchyNode` (por exemplo, `dam:Asset`) adicionando desnecessariamente ao conjunto de resultados potenciais.
   * Não há índice fornecido pelo AEM para `nt:hierarchyNode`, no entanto, como há um índice fornecido para `cq:Page`.
   A configuração `type=cq:Page` restringe essa consulta a apenas `cq:Page` nós e resolve a consulta para o cqPageLucene do AEM, limitando os resultados a um subconjunto de nós (somente nós cq:Page) no AEM.

1. Ou ajuste as restrições de propriedade para que a consulta seja resolvida para um Índice de propriedades existente.

   * **Consulta não otimizada**

      * 
         ```
         property=jcr:content/contentType
         property.value=article-page
         ```
   * **Consulta otimizada**

      * 
         ```
         property=jcr:content/sling:resourceType
         property.value=my-site/components/structure/article-page
         ```
   Alterar a restrição de propriedade de `jcr:content/contentType` (um valor personalizado) para a propriedade bem conhecida `sling:resourceType` permite que a consulta resolva para o índice de propriedade `slingResourceType` que indexa todo o conteúdo por `sling:resourceType`.

   Os índices de propriedade (em oposição aos Índices de propriedades Lucene) são melhor usados quando a consulta não é discernível por tipo de nó e uma única restrição de propriedade domina o conjunto de resultados.

1. Adicione a restrição de caminho mais estrita possível à consulta. Por exemplo, preferir `/content/my-site/us/en` sobre `/content/my-site`ou `/content/dam` sobre `/`.

   * **Consulta não otimizada**

      * 
         ```
         type=cq:Page
         path=/content
         property=jcr:content/contentType
         property.value=article-page
         ```
   * **Consulta otimizada**

      * 
         ```
         type=cq:Page
         path=/content/my-site/us/en
         property=jcr:content/contentType
         property.value=article-page
         ```
   O escopo da restrição de caminho de `path=/content`para `path=/content/my-site/us/en` permite que os índices reduzam o número de entradas de índice que precisam ser inspecionadas. Quando a consulta puder restringir muito bem o caminho, além de apenas `/content` ou `/content/dam`, verifique se o índice tem `evaluatePathRestrictions=true`.

   Observe que usar `evaluatePathRestrictions` aumenta o tamanho do índice.

1. Quando possível, evite funções/operações de consulta, como: `LIKE` e `fn:XXXX` à medida que seus custos aumentam com o número de resultados baseados em restrições.

   * **Consulta não otimizada**

      * 
         ```
         type=cq:Page
         property=jcr:content/contentType
         property.operation=like
         property.value=%article%
         ```
   * **Consulta otimizada**

      * 
         ```
         type=cq:Page
         fulltext=article
         fulltext.relPath=jcr:content/contentType
         ```
   A condição LIKE é lenta para avaliação, pois nenhum índice pode ser usado se o texto começar com um curinga (&quot;%..&#39;). A condição jcr:contains permite o uso de um índice de texto completo e, portanto, é preferida. Isso requer que o Índice de propriedades do Lucene resolvido tenha indexRule para `jcr:content/contentType` with `analayzed=true`.

   O uso de funções de consulta como `fn:lowercase(..)` pode ser mais difícil de otimizar, pois não há equivalentes mais rápidos (fora de configurações mais complexas e discretas do analisador de índice). É melhor identificar outras restrições de escopo para melhorar o desempenho geral da consulta, exigindo que as funções operem no menor conjunto possível de resultados potenciais.

1. ***Esse ajuste é específico do Query Builder e não se aplica a JCR-SQL2 ou XPath.***

   Use o [thinkTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) do Query Builder quando o conjunto completo de resultados for **não **necessário imediatamente.

   * **Consulta não otimizada**

      * 
         ```
         type=cq:Page
         path=/content
         ```
   * **Consulta otimizada**

      * 
         ```
         type=cq:Page
         path=/content
         p.guessTotal=100
         ```
   Para casos em que a execução da consulta é rápida, mas o número de resultados é grande, p. `guessTotal` é uma otimização crítica para consultas do Query Builder.

   `p.guessTotal=100` instrui o Query Builder a coletar apenas os primeiros 100 resultados e a definir um sinalizador booleano indicando se existem pelo menos mais um resultado (mas não quantos mais, já que a contagem desse número resultaria em lentidão). Essa otimização se sobressai para paginação ou casos de uso de carregamento infinito, onde apenas um subconjunto de resultados é exibido incrementalmente.

## Ajuste de índice existente {#existing-index-tuning}

1. Se a consulta ideal for resolvida para um Índice de propriedades, não há mais nada a fazer, pois os Índices de propriedades são minimamente ajustáveis.
1. Caso contrário, a consulta deve ser resolvida para um Índice de propriedades Lucene. Se nenhum índice puder ser resolvido, vá para Criar um novo índice.
1. Conforme necessário, converta a consulta em XPath ou JCR-SQL2.

   * **Consulta do Construtor de consultas**

      * 
         ```
         query type=cq:Page
         path=/content/my-site/us/en
         property=jcr:content/contentType
         property.value=article-page
         orderby=@jcr:content/publishDate
         orderby.sort=desc
         ```
   * **XPath gerado da consulta do Query Builder**

      * 
         ```
         /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
         ```


1. Forneça o XPath (ou JCR-SQL2) para o Gerador [de Definição de Índice](https://oakutils.appspot.com/generate/index) Oak para gerar a definição otimizada do Índice de Propriedades Lucene.

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

1. Unir manualmente a definição gerada no Índice de propriedades do Lucene existente de forma aditiva. Tenha cuidado para não remover configurações existentes, pois elas podem ser usadas para satisfazer outras consultas.

   1. Localize o Índice de propriedades do Lucene existente que abrange cq:Page (usando o Gerenciador de índice). Neste caso, `/oak:index/cqPageLucene`.
   1. Identifique o delta de configuração entre a definição de índice otimizada (Etapa 4) e o índice existente (/oak:index/cqPageLucene) e adicione as configurações ausentes do Índice otimizado à definição de índice existente.
   1. As Práticas recomendadas de reindexação de acordo com o AEM são atualizadas ou reindexadas, com base em se o conteúdo existente será afetado por essa alteração de configuração de índice.

## Criar um novo índice {#create-a-new-index}

1. Verifique se a consulta não é resolvida para um Índice de propriedades do Lucene existente. Se isso acontecer, consulte a seção acima sobre ajuste e índice existente.
1. Conforme necessário, converta a consulta em XPath ou JCR-SQL2.

   * **Consulta do Construtor de consultas**

      * 
         ```
         type=myApp:Author
         property=firstName
         property.value=ira
         ```
   * **XPath gerado da consulta do Query Builder**

      * 
         ```
         //element(*, myApp:Page)[@firstName = 'ira']
         ```


1. Forneça o XPath (ou JCR-SQL2) para o Gerador [de Definição de Índice](https://oakutils.appspot.com/generate/index) Oak para gerar a definição otimizada do Índice de Propriedades Lucene.

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

   Adicione a definição XML fornecida pelo Oak Index Definition Generator para o novo índice ao projeto AEM que gerencia definições de índice Oak (lembre-se de tratar as definições de índice Oak como código, já que o código depende delas).

   Implante e teste o novo índice após o ciclo de vida normal de desenvolvimento do software AEM e verifique se a consulta é resolvida para o índice e se a consulta é executada.

   Após a implantação inicial desse índice, o AEM preencherá o índice com os dados necessários.

## Quando as consultas sem índice e transversais estão OK? {#when-index-less-and-traversal-queries-are-ok}

Devido à arquitetura de conteúdo flexível do AEM, é difícil prever e garantir que os transversais das estruturas de conteúdo não evoluam ao longo do tempo para serem inaceitavelmente grandes.

Portanto, certifique-se de que um índice atenda a consultas, exceto se a combinação de restrição de caminho e restrição de tipo de nó garantir que **menos de 20 nós sejam atravessados.**

## Ferramentas de desenvolvimento de consulta {#query-development-tools}

### Adobe com suporte {#adobe-supported}

* **Depurador do Query Builder**

   * Uma WebUI para executar consultas do Query Builder e gerar o XPath de suporte (para uso em Explicar consulta ou no Oak Index Definition Generator).
   * Localizado no AEM em [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - Ferramenta de consulta**

   * Uma WebUI para executar consultas XPath e JCR-SQL2.
   * Localizado no AEM em [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Ferramentas > Consulta...

* **[Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query)**

   * Um painel de Operações do AEM que fornece uma explicação detalhada (plano de consulta, tempo de consulta e número de resultados) para qualquer consulta XPATH ou JCR-SQL2.

* **[Consultas lentas/populares](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Um painel de Operações do AEM que lista as recentes consultas lentas e populares executadas no AEM.

* **[Gerenciador de índice](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * Uma Web UI do AEM Operations que exibe os índices na instância do AEM; facilita a compreensão de quais índices já existem, podem ser direcionados ou aumentados.

* **[Registro](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Log do Query Builder

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Log de execução de consulta de erro

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Configuração do mecanismo de consulta OSGi do Apache Jackrabbit**

   * Configuração do OSGi que configura o comportamento de falha para consultas cruzadas.
   * Localizado no AEM em [/system/console/configMgr#org.apache.Jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * O JMX MBean usado para estimar o número de nós nas árvores de conteúdo no AEM.
   * Localizado no AEM em [/system/console/jmx/org.apache.Jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Comunidade suportada {#community-supported}

* **[Gerador de definição de índice Oak](https://oakutils.appspot.com/generate/index)**

   * Gere o índice ideal de propriedades Lucence a partir das instruções de consulta XPath ou JCR-SQL2.

* **[Plug-in do AEM Chrome](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * A extensão do navegador da Web do Google Chrome que expõe dados de log por solicitação, incluindo consultas executadas e seus planos de consulta, no console de ferramentas dev do navegador.
   * Requer que o [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) seja instalado e ativado no AEM.

