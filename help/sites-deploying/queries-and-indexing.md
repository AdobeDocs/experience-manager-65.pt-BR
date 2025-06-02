---
title: Consultas e indexação do Oak
description: Saiba como configurar índices no Adobe Experience Manager (AEM) 6.5.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: eeeb31d81c22f8dace7a170953bf45a709f5ac73
workflow-type: tm+mt
source-wordcount: '3051'
ht-degree: 0%

---

# Consultas e indexação do Oak{#oak-queries-and-indexing}

>[!NOTE]
>
>Este artigo é sobre como configurar índices no AEM 6. Para obter as práticas recomendadas sobre otimização do desempenho de consulta e indexação, consulte [Práticas recomendadas para consultas e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## Introdução {#introduction}

Ao contrário do Jackrabbit 2, o Oak não indexa conteúdo por padrão. Os índices personalizados devem ser criados quando necessário, assim como com os bancos de dados relacionais tradicionais. Se não houver índice para uma consulta específica, muitos nós possivelmente serão percorridos. A query ainda pode funcionar, mas provavelmente está lenta.

Se o Oak encontrar uma consulta sem um índice, uma mensagem de log de nível WARN será impressa:

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## Idiomas de consulta compatíveis {#supported-query-languages}

O mecanismo de consulta do Oak é compatível com os seguintes idiomas:

* XPath (recomendado)
* SQL-2
* SQL (obsoleto)
* JQOM

## Tipos de indexador e cálculo de custo {#indexer-types-and-cost-calculation}

O back-end baseado no Apache Oak permite que indexadores diferentes sejam conectados ao repositório.

Um indexador é o **Índice de Propriedade**, para o qual a definição de índice é armazenada no próprio repositório.

As implementações para **Apache Lucene** e **Solr** também estão disponíveis por padrão, pois ambas oferecem suporte à indexação de texto completo.

O **Índice de Travessia** será usado se nenhum outro indexador estiver disponível. Isso significa que o conteúdo não é indexado e os nós de conteúdo são percorridos para encontrar correspondências para a consulta.

Se houver vários indexadores disponíveis para um query, cada indexador disponível estimará o custo de execução do query. O Oak escolhe o indexador com o menor custo estimado.

![chlimage_1-148](assets/chlimage_1-148.png)

O diagrama acima é uma representação de alto nível do mecanismo de execução de consulta do Apache Oak.

Primeiro, a consulta é analisada em uma Árvore de sintaxe abstrata. Em seguida, a consulta é verificada e transformada em SQL-2, que é a linguagem nativa para consultas do Oak.

Em seguida, cada índice é consultado para estimar o custo do query. Depois de concluído, os resultados do índice mais barato são recuperados. Finalmente, os resultados são filtrados para garantir que o usuário atual tenha acesso de leitura ao resultado e que o resultado corresponda à consulta completa.

## Configuração dos índices {#configuring-the-indexes}

>[!NOTE]
>
>Para um repositório grande, criar um índice é uma operação demorada. Isso é verdade para a criação inicial de um índice e para a reindexação (reconstrução de um índice depois de alterar a definição). Consulte também [Solução de problemas de índices do Oak](/help/sites-deploying/troubleshooting-oak-indexes.md) e [Prevenção da reindexação lenta](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

Se a reindexação for necessária em repositórios grandes, especialmente ao usar MongoDB e para índices de texto completo, considere a pré-extração de texto e o uso do oak-run para criar o índice inicial e reindexar.

Os índices são configurados como nós no repositório no nó **Oak:index**.

O tipo do nó de índice deve ser **oak:QueryIndexDefinition.** Várias opções de configuração estão disponíveis para cada indexador como propriedades de nó. Para obter mais informações, consulte os detalhes de configuração de cada tipo de indexador abaixo.

### O índice de propriedade {#the-property-index}

O Índice de propriedade é útil para consultas que têm restrições de propriedade, mas não são de texto completo. Ela pode ser configurada seguindo o procedimento abaixo:

1. Abra o CRXDE acessando `http://localhost:4502/crx/de/index.jsp`
1. Criar um nó em **oak:index**
1. Nomeie o nó **PropertyIndex** e defina o tipo de nó como **oak:QueryIndexDefinition**
1. Defina as seguintes propriedades para o novo nó:

   * **tipo:** `property` (do tipo String)
   * **propertyNames:** `jcr:uuid` (do tipo Nome)

   Este exemplo específico indexa a propriedade `jcr:uuid`, cujo trabalho é expor o identificador exclusivo universalmente (UUID) do nó ao qual está anexado.

1. Salve as alterações.

O Índice de propriedades tem as seguintes opções de configuração:

* A propriedade **type** especifica o tipo de índice e, nesse caso, deve ser definida como **property**

* A propriedade **propertyNames** indica a lista de propriedades armazenadas no índice. Caso esteja ausente, o nome do nó é usado como um valor de referência do nome da propriedade. Neste exemplo, a propriedade **jcr:uuid** cujo trabalho é expor o identificador exclusivo (UUID) de seu nó é adicionada ao índice.

* O sinalizador **unique** que, se definido como **true**, adiciona uma restrição de exclusividade no índice de propriedade.

* A propriedade **declaringNodeTypes** permite especificar um determinado tipo de nó ao qual o índice se aplica somente.
* O sinalizador **reindex** que, se definido como **true**, aciona uma reindexação de conteúdo completa.

### O índice ordenado {#the-ordered-index}

O índice Ordenado é uma extensão do índice Propriedade. No entanto, foi descontinuado. Índices deste tipo devem ser substituídos pelo [Índice de Propriedade Lucene](#the-lucene-property-index).

### Índice de texto completo Lucene {#the-lucene-full-text-index}

Um indexador de texto completo com base no Apache Lucene está disponível no AEM 6.

Se um índice de texto completo for configurado, todas as consultas que têm uma condição de texto completo usarão o índice de texto completo, independentemente de haver outras condições indexadas e independentemente de haver uma restrição de caminho.

Se nenhum índice de texto completo estiver configurado, as consultas com condições de texto completo não funcionarão conforme esperado.

Como o índice é atualizado por meio de um thread em segundo plano assíncrono, algumas pesquisas de texto completo ficam indisponíveis por uma pequena janela de tempo até que os processos em segundo plano sejam concluídos.

Você pode configurar um índice de texto completo Lucene seguindo o procedimento abaixo:

1. Abra o CRXDE e crie um nó em **oak:index**.
1. Nomeie o nó **LuceneIndex** e defina o tipo de nó como **oak:QueryIndexDefinition**
1. Adicione as seguintes propriedades ao nó:

   * **tipo:** `lucene` (do tipo String)
   * **async:** `async` (do tipo String)

1. Salve as alterações.

O Índice Lucene tem as seguintes opções de configuração:

* A propriedade **type** que especifica o tipo de índice deve ser definida como **lucene**
* A propriedade **async** que deve ser definida como **async**. Isso envia o processo de atualização do índice para uma thread em segundo plano.
* A propriedade **includePropertyTypes**, que define qual subconjunto de tipos de propriedade está incluído no índice.
* A propriedade **excludePropertyNames** que define uma lista de nomes de propriedades - propriedades que devem ser excluídas do índice.
* O sinalizador **reindex** que, quando definido como **true**, aciona uma reindexação de conteúdo completa.

### Compreensão da pesquisa de texto completo {#understanding-fulltext-search}

A documentação desta seção se aplica aos índices Apache Lucene, Elasticsearch e texto completo do PostgreSQL, SQLite e MySQL, por exemplo. O exemplo a seguir é para AEM / Oak / Lucene.

<b>Dados a serem indexados</b>

O ponto inicial são os dados que devem ser indexados. Considere os seguintes documentos, como exemplo:

| <b>ID do documento</b> | <b>Caminho</b> | <b>Texto completo</b> |
| --- | --- | --- |
| 100 | /content/rubik | &quot;Rubik é uma marca finlandesa.&quot; |
| 200 | /content/rubiksCube | &quot;O Cubo Mágico foi inventado em 1974.&quot; |
| 300 | /content/cube | &quot;Um cubo é um objeto tridimensional.&quot; |


<b>Índice invertido</b>

O mecanismo de indexação divide o texto completo em palavras chamadas &quot;tokens&quot; e cria um índice chamado &quot;índice invertido&quot;. Este índice contém a lista de documentos onde ele aparece para cada palavra.

Palavras curtas e comuns (também chamadas de &quot;palavras irrelevantes&quot;) não são indexadas. Todos os tokens são convertidos em minúsculas e a raiz é aplicada.

Caracteres especiais, como *&quot;-&quot;*, não são indexados.

| <b>Token</b> | <b>IDs de documento</b> |
| --- | --- |
| 194 | ..., 200,... |
| marca | ..., 100,... |
| cubo | ..., 200, 300,... |
| dimension | 300 |
| finish | ..., 100,... |
| inventar | 200 |
| objeto | ..., 300,... |
| rubik | ..., 100, 200,... |

A lista de documentos está classificada. Isso é útil ao consultar.

<b>Pesquisando</b>

Veja abaixo um exemplo de query. Observe que todos os caracteres especiais (como *&#39;*) foram substituídos por um espaço:

```
/jcr:root/content//element(\*; cq:Page)`[` jcr:contains('Rubik s Cube')`]`
```

As palavras são tokenizadas e filtradas da mesma forma que na indexação (palavras de caractere único são removidas, por exemplo). Nesse caso, a busca é por:

```
+:fulltext:rubik +:fulltext:cube
```

O índice consulta a lista de documentos para essas palavras. Se houver muitos documentos, a lista poderá ser grande. Como exemplo, suponha que eles contenham o seguinte:


| <b>Token</b> | <b>IDs de documento</b> |
| --- | --- |
| rubik | 10, 100, 200, 1000 |
| cubo | 30, 200, 300, 2000 |


A Lucene inverte de um lado para o outro entre as duas listas (ou listas `n` de revezamento, ao pesquisar por `n` palavras):

* Lido no &quot;rubik&quot; recebe a primeira entrada: encontra 10
* A leitura no &quot;cubo&quot; obtém a primeira entrada `>` = 10. 10 não é encontrado, então o próximo é 30.
* A leitura em &quot;rubik&quot; obtém a primeira entrada `>` = 30: encontra 100.
* A leitura no &quot;cubo&quot; obtém a primeira entrada `>` = 100: encontra 200.
* A leitura em &quot;rubik&quot; obtém a primeira entrada `>` = 200. 200 é encontrado. Portanto, o documento 200 é uma combinação para ambos os termos. Isso é lembrado.
* Lido no &quot;rubik&quot; recebe a próxima entrada: 1000.
* A leitura no &quot;cubo&quot; obtém a primeira entrada `>` = 1000: encontra 2000.
* A leitura no &quot;rubik&quot; obtém a primeira entrada `>` = 2000: fim da lista.
* Por fim, você pode interromper a pesquisa.

O único documento encontrado que contém ambos os termos é 200, como no exemplo abaixo:

| 200 | /content/rubiksCube | &quot;O Cubo Mágico foi inventado em 1974.&quot; |
| --- | --- | --- |

Quando várias entradas são encontradas, elas são classificadas por pontuação.

>[!NOTE]
>
>O mecanismo de pesquisa descrito nesta seção usa a indexação Lucene, não a correspondência parcial como o comando `grep` do Linux.

### O índice de propriedade Lucene {#the-lucene-property-index}

Desde **Oak 1.0.8**, o Lucene pode ser usado para criar índices que envolvam restrições de propriedade que não sejam de texto completo.

Para obter um Índice de Propriedade Lucene, a propriedade **fulltextEnabled** sempre deve ser definida como false.

Dê o exemplo de consulta a seguir:

```xml
select * from [nt:base] where [alias] = '/admin'
```

Para definir um Índice de Propriedade Lucene para a consulta acima, você pode adicionar a seguinte definição criando um nó sob **`oak:index`:**

* **Nome:** `LucenePropertyIndex`
* **Tipo:** `oak:QueryIndexDefinition`

Depois que o nó for criado, adicione as seguintes propriedades:

* **tipo:**

  ```xml
  lucene (of type String)
  ```

* **assíncrono:**

  ```xml
  async (of type String)
  ```

* **textoCompletoHabilitado:**

  ```xml
  false (of type Boolean)
  ```

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>Comparado ao Índice de propriedades normal, o Índice de propriedades Lucene é sempre configurado no modo assíncrono. Portanto, os resultados retornados pelo índice nem sempre podem refletir o estado mais atualizado do repositório.

>[!NOTE]
>
>Para obter informações mais específicas sobre o Índice de propriedades Lucene, consulte a [página de documentação do Apache Jackrabbit Oak Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Analisadores Lucene {#lucene-analyzers}

Desde a versão 1.2.0, o Oak é compatível com analisadores Lucene.

Os analisadores são usados quando um documento é indexado e no momento da consulta. Um analisador examina o texto dos campos e gera um fluxo de token. Os analisadores Lucene são compostos de uma série de classes de tokenizador e filtro.

Os analisadores podem ser configurados por meio do nó `analyzers` (do tipo `nt:unstructured`) dentro da definição `oak:index`.

O analisador padrão de um índice está configurado no filho `default` do nó de analisadores.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>Para obter uma lista de analisadores disponíveis, consulte a documentação da API da versão do Lucene que você está usando.

#### Especificação direta da classe do analisador {#specifying-the-analyzer-class-directly}

Se quiser usar qualquer analisador pronto para uso, você poderá configurá-lo seguindo o procedimento abaixo:

1. Localize o índice com o qual você deseja usar o analisador no nó `oak:index`.

1. No índice, crie um nó filho chamado `default` do tipo `nt:unstructured`.

1. Adicione uma propriedade ao nó padrão com as seguintes propriedades:

   * **Nome:** `class`
   * **Tipo:** `String`
   * **Valor:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   O valor é o nome da classe do analisador que você deseja usar.

   Você também pode definir o analisador a ser usado com uma versão do lucene específica usando a propriedade de cadeia de caracteres `luceneMatchVersion` opcional. Uma sintaxe válida para usá-la com o Lucene 4.7 seria:

   * **Nome:** `luceneMatchVersion`
   * **Tipo:** `String`
   * **Valor:** `LUCENE_47`

   Se `luceneMatchVersion` não for fornecido, a Oak usará a versão do Lucene com a qual foi enviado.

1. Se quiser adicionar um arquivo de palavras irrelevantes às configurações do analisador, você poderá criar um nó no `default` com as seguintes propriedades:

   * **Nome:** `stopwords`
   * **Tipo:** `nt:file`

#### Criação de analisadores por meio de composição {#creating-analyzers-via-composition}

Os analisadores também podem ser compostos com base em `Tokenizers`, `TokenFilters` e `CharFilters`. Você pode fazer isso especificando um analisador e criando nós secundários de seus tokenizers e filtros opcionais que são aplicados na ordem listada. Consulte também [https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

Considere essa estrutura de nó como um exemplo:

* **Nome:** `analyzers`

   * **Nome:** `default`

      * **Nome:** `charFilters`
      * **Tipo:** `nt:unstructured`

         * **Nome:** `HTMLStrip`
         * **Nome:** `Mapping`

      * **Nome:** `tokenizer`

         * **Nome da Propriedade:** `name`

            * **Tipo:** `String`
            * **Valor:** `Standard`

      * **Nome:** `filters`
      * **Tipo:** `nt:unstructured`

         * **Nome:** `LowerCase`
         * **Nome:** `Stop`

            * **Nome da propriedade:** `words`

               * **Tipo:** `String`
               * **Valor:** `stop1.txt, stop2.txt`

            * **Nome:** `stop1.txt`

               * **Tipo:** `nt:file`

            * **Nome:** `stop2.txt`

               * **Tipo:** `nt:file`

O nome dos filtros, charFilters e tokenizers são formados pela remoção dos sufixos de fábrica. Assim:

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` torna-se `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` torna-se `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` torna-se `Stop`

Qualquer parâmetro de configuração necessário para a fábrica é especificado como a propriedade do nó em questão.

Para casos como o carregamento de palavras de interrupção em que o conteúdo de arquivos externos deve ser carregado, o conteúdo pode ser fornecido criando um nó filho do tipo `nt:file` para o arquivo em questão.

### O índice Solr {#the-solr-index}

A finalidade do índice Solr é a pesquisa de texto completo, mas ele também pode ser usado para indexar a pesquisa por caminho, restrições de propriedade e restrições de tipo principal. Isso significa que o índice Solr no Oak pode ser usado para qualquer tipo de consulta JCR.

A integração no AEM acontece no nível do repositório, de modo que Solr é um dos possíveis índices que podem ser usados no Oak, a nova implementação de repositório fornecida com o AEM.

Ele pode ser configurado para funcionar como um servidor remoto com a instância do AEM.

### Configuração do AEM com um único servidor Solr remoto {#configuring-aem-with-a-single-remote-solr-server}

O AEM também pode ser configurado para funcionar com uma instância remota do servidor Solr:

1. Baixe e extraia a versão mais recente do Solr. Para obter mais informações sobre como fazer isso, consulte a [documentação de instalação do Apache Solr](https://solr.apache.org/guide/6_6/installing-solr.html).
1. Agora, crie dois fragmentos Solr. Você pode fazer isso criando pastas para cada fragmento na pasta em que o Solr foi desempacotado:

   * Para o primeiro fragmento, crie a pasta:

   `<solrunpackdirectory>\aemsolr1\node1`

   * Para o segundo fragmento, crie a pasta:

   `<solrunpackdirectory>\aemsolr2\node2`

1. Localize a instância de exemplo no pacote Solr. Está em uma pasta chamada &quot; `example`&quot; na raiz do pacote.
1. Copie as seguintes pastas da instância de exemplo para as duas pastas compartilhadas ( `aemsolr1\node1` e `aemsolr2\node2`):

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. Crie uma pasta chamada &quot; `cfg`&quot; em cada uma das duas pastas compartilhadas.
1. Coloque os arquivos de configuração Solr e Zookeeper nas pastas `cfg` recém-criadas.

   >[!NOTE]
   >
   >Para obter mais informações sobre a configuração do Solr e do ZooKeeper, consulte a [documentação de Configuração do Solr](https://cwiki.apache.org/confluence/display/solr/ConfiguringSolr) e o [Guia de Introdução do ZooKeeper](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

1. Inicie o primeiro fragmento com suporte do ZooKeeper indo para `aemsolr1\node1` e executando o seguinte comando:

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. Inicie o segundo fragmento indo até `aemsolr2\node2` e executando o seguinte comando:

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. Depois que ambos os fragmentos forem iniciados, teste se tudo está funcionando, conectando-se à interface Solr em `http://localhost:8983/solr/#/`
1. Inicie o AEM e acesse o Console da Web em `http://localhost:4502/system/console/configMgr`
1. Defina a seguinte configuração em **Configuração do servidor remoto Oak Solr**:

   * URL HTTP Solr: `http://localhost:8983/solr/`

1. Escolha **Solr Remoto** na lista suspensa em **Solr do Oak** provedor de servidor.

1. Acesse o CRXDE e faça logon como administrador.
1. Crie um nó chamado **solrIndex** em **oak:index** e defina as seguintes propriedades:

   * **tipo:** solr (do tipo String)
   * **async:** async (do tipo String)
   * **reindex:** true (do tipo Booleano)

1. Salve as alterações.

#### Configuração recomendada para Solr {#recommended-configuration-for-solr}

Veja abaixo um exemplo de uma configuração básica que pode ser usada com todas as três implantações Solr descritas neste artigo. Ele acomoda os índices de propriedade dedicados que já estão presentes no AEM; não use com outros aplicativos.

Para usá-lo corretamente, você deve colocar o conteúdo do arquivo diretamente no Diretório Home Solr. Se houver implantações com vários nós, ela deverá ir diretamente para a pasta raiz de cada nó.

Arquivos de configuração Solr recomendados

[Obter arquivo](assets/recommended-conf.zip)

### Ferramentas de indexação do AEM {#aem-indexing-tools}

O AEM 6.1 também integra duas ferramentas de indexação presentes no AEM 6.0 como parte do conjunto de ferramentas do Adobe Consulting Services Commons:

1. **Explicar consulta**, uma ferramenta projetada para ajudar os administradores a entender como as consultas são executadas;
1. **Oak Index Manager**, uma interface de usuário da Web para manter índices existentes.

Agora você pode contatá-los acessando **Ferramentas - Operações - Painel - Diagnóstico** na tela de boas-vindas do AEM.

Para obter mais informações sobre como usá-los, consulte a [documentação do Painel de Operações](/help/sites-administering/operations-dashboard.md).

#### Criação de índices de propriedade por meio do OSGi {#creating-property-indexes-via-osgi}

O pacote ACS Commons também expõe as configurações de OSGi que podem ser usadas para criar índices de propriedade.

Você pode acessá-lo no Console da Web procurando por &quot;**Verifique o Índice de Propriedade do Oak**&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### Solução de problemas de indexação {#troubleshooting-indexing-issues}

Podem surgir situações em que as consultas demoram muito para serem executadas e o tempo geral de resposta do sistema é lento.

Esta seção apresenta um conjunto de recomendações sobre o que deve ser feito para rastrear a causa desses problemas e conselhos sobre como resolvê-los.

#### Preparando informações de depuração para análise {#preparing-debugging-info-for-analysis}

A maneira mais fácil de obter as informações necessárias para a consulta que está sendo executada é por meio da [Explicar ferramenta de consulta](/help/sites-administering/operations-dashboard.md#explain-query). Isso permite coletar as informações precisas necessárias para depurar uma consulta lenta sem a necessidade de consultar as informações de nível de log. Isso é desejável se você souber a query que está sendo depurada.

Se isso não for possível por algum motivo, você poderá coletar os logs de indexação em um único arquivo e usá-lo para solucionar seu problema específico.

#### Ativar registro {#enable-logging}

Para habilitar o log, você deve habilitar logs de nível **DEBUG** para as categorias relacionadas a consultas e indexação do Oak. Essas categorias são:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

A categoria **com.day.cq.search** só será aplicável se você estiver usando o utilitário QueryBuilder fornecido pela AEM.

>[!NOTE]
>
>É importante que os logs sejam definidos como DEBUG somente enquanto a consulta que você deseja solucionar problemas estiver sendo executada. Caso contrário, muitos eventos serão gerados nos logs ao longo do tempo. Por causa disso, uma vez coletados os registros necessários, volte para o registro em nível INFO para as categorias mencionadas acima.

Você pode ativar o registro seguindo este procedimento:

1. Aponte seu navegador para `https://serveraddress:port/system/console/slinglog`
1. Clique no botão **Adicionar novo Agente** na parte inferior do console.
1. Na linha recém-criada, adicione as categorias mencionadas acima. Você pode usar o sinal **+** para adicionar mais de uma categoria a um único agente.
1. Escolha **DEBUG** na lista suspensa **Nível de log**.
1. Defina o arquivo de saída como `logs/queryDebug.log`. Isso correlaciona todos os eventos DEBUG em um único arquivo de log.
1. Execute a consulta ou renderize a página que está usando a consulta que você deseja depurar.
1. Depois de executar a consulta, volte para o console de log e altere o nível de log do agente de log recém-criado para **INFO**.

#### Configuração do índice {#index-configuration}

A maneira como a consulta é avaliada é amplamente afetada pela configuração do índice. É importante analisar a configuração do índice ou enviá-la para o suporte. Você pode obter a configuração como um pacote de conteúdo ou uma representação JSON.

Normalmente, a configuração de indexação é armazenada no nó `/oak:index` no CRXDE. Você pode obter a versão JSON em:

`https://serveraddress:port/oak:index.tidy.-1.json`

Se o índice estiver configurado em um local diferente, altere o caminho de acordo.

#### Saída do MBean {#mbean-output}

Às vezes, é útil fornecer a saída de MBeans relacionados ao índice para depuração. Você pode fazer isso ao:

1. Indo para o console JMX em:
   `https://serveraddress:port/system/console/jmx`

1. Procurar os seguintes MBeans:

   * Estatísticas do Índice Lucene
   * Estatísticas de suporte a CopyOnRead
   * Estatísticas de consulta do Oak
   * IndexStats

1. Clique em cada um dos MBeans para obter estatísticas de desempenho. Crie uma captura de tela ou anote-as caso seja necessário enviar um suporte.

Você também pode obter a variante JSON dessas estatísticas nos seguintes URLs:

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

Você também pode fornecer saída JMX consolidada por meio de `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. Isso incluiria todos os detalhes do MBean relacionados ao Oak no formato JSON.

#### Outros detalhes {#other-details}

Você pode coletar detalhes adicionais para ajudar a solucionar o problema, como:

1. A versão do Oak em que sua instância está sendo executada. Você pode ver isso abrindo o CRXDE e observando a versão no canto inferior direito da página de boas-vindas ou verificando a versão do pacote `org.apache.jackrabbit.oak-core`.
1. A saída do depurador do QueryBuilder da consulta com problema. O depurador pode ser acessado em: `https://serveraddress:port/libs/cq/search/content/querydebug.html`
