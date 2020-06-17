---
title: Query Oak e indexação
seo-title: Query Oak e indexação
description: Saiba como configurar índices no AEM.
seo-description: Saiba como configurar índices no AEM.
uuid: a1233d2e-1320-43e0-9b18-cd6d1eeaad59
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 492741d5-8d2b-4a81-8f21-e621ef3ee685
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
translation-type: tm+mt
source-git-commit: b01f6d3726fd6aa06ffedaf10dfde9526479a2a3
workflow-type: tm+mt
source-wordcount: '2880'
ht-degree: 1%

---


# Query Oak e indexação{#oak-queries-and-indexing}

>[!NOTE]
>
>Este artigo trata da configuração de índices no AEM 6. Para obter as práticas recomendadas de otimização do desempenho de query e indexação, consulte Práticas [recomendadas para Query e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## Introdução {#introduction}

Ao contrário do Jackrabbit 2, o Oak não indexa o conteúdo por padrão. Os índices personalizados precisam ser criados quando necessário, assim como os bancos de dados relacionais tradicionais. Se não houver um índice para um query específico, possivelmente muitos nós serão atravessados. O query ainda pode funcionar, mas provavelmente é muito lento.

Se Oak encontrar um query sem um índice, uma mensagem de registro de nível WARN será impressa:

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## Idiomas de query suportados {#supported-query-languages}

O mecanismo de query Oak suporta os seguintes idiomas:

* XPath (recomendado)
* SQL-2
* SQL (obsoleto)
* JQOM

## Tipos de indexador e cálculo de custo {#indexer-types-and-cost-calculation}

O backend baseado no Apache Oak permite que diferentes indexadores sejam conectados ao repositório.

Um indexador é o Índice **de** propriedades, para o qual a definição de índice é armazenada no próprio repositório.

As implementações para o **Apache Lucene** e o **Solr** também estão disponíveis por padrão, que suportam a indexação de texto completo.

O Índice **** transversal será usado se nenhum outro indexador estiver disponível. Isso significa que o conteúdo não é indexado e os nós de conteúdo são atravessados para localizar correspondências ao query.

Se vários indexadores estiverem disponíveis para um query, cada indexador disponível estima o custo de execução do query. Oak escolhe o indexador com o menor custo estimado.

![chlimage_1-148](assets/chlimage_1-148.png)

O diagrama acima é uma representação de alto nível do mecanismo de execução do query do Apache Oak.

Primeiro, o query é analisado em uma Árvore de sintaxe abstrata. Em seguida, o query é verificado e transformado em SQL-2, que é o idioma nativo para query Oak.

Em seguida, cada índice é consultado para estimar o custo do query. Uma vez concluída, são obtidos os resultados do índice mais barato. Por fim, os resultados são filtrados, tanto para garantir que o usuário atual tenha acesso de leitura ao resultado quanto que o resultado corresponda ao query completo.

## Configuração dos índices {#configuring-the-indexes}

>[!NOTE]
>
>Para um repositório grande, construir um índice é uma operação demorada. Isso vale tanto para a criação inicial de um índice quanto para a reindexação (reconstrução de um índice após a alteração da definição). Consulte também [Solução de problemas de índices](/help/sites-deploying/troubleshooting-oak-indexes.md) de Oak e [Prevenção de reindexação](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing)lenta.

Se a reindexação for necessária em repositórios muito grandes, especialmente ao usar o MongoDB e para índices de texto completo, considere a pré-extração de texto e use o oak-run para criar o índice inicial e reindexar.

Os índices são configurados como nós no repositório no nó **oak:index** .

O tipo do nó de índice deve ser **oak:QueryIndexDefinition.** Várias opções de configuração estão disponíveis para cada indexador como propriedades de nó. Para obter mais informações, consulte os detalhes de configuração de cada tipo de indexador abaixo.

### O índice de propriedades {#the-property-index}

O Índice de propriedades geralmente é útil para query que têm restrições de propriedade, mas não são de texto completo. Ele pode ser configurado seguindo o procedimento abaixo:

1. Abra o CRXDE acessando `http://localhost:4502/crx/de/index.jsp`
1. Criar um novo nó em **oak:index**
1. Nomeie o nó **PropertyIndex** e defina o tipo de nó como **oak:QueryIndexDefinition**
1. Defina as seguintes propriedades para o novo nó:

   * **tipo:**  `property` (do tipo String)
   * **propertyNames:**  `jcr:uuid` (do tipo Nome)

   Este exemplo específico indexará a `jcr:uuid` propriedade, cujo trabalho é expor o identificador universalmente exclusivo (UUID) do nó ao qual está anexado.

1. Salve as alterações.

O Índice de propriedades tem as seguintes opções de configuração:

* A propriedade **type** especificará o tipo de índice e, nesse caso, deve ser definida como **propriedade**

* A propriedade **propertyNames** indica a lista das propriedades que serão armazenadas no índice. Caso esteja ausente, o nome do nó será usado como um valor de referência de nome de propriedade. Neste exemplo, a propriedade **jcr:uuid** cuja tarefa é expor o identificador exclusivo (UUID) de seu nó é adicionada ao índice.

* O sinalizador **exclusivo** que, se definido como **true** , adiciona uma restrição de exclusividade ao índice de propriedade.

* A propriedade **declareNodeTypes** permite que você especifique um tipo de nó ao qual o índice será aplicado somente.
* O sinalizador de **reindexação** que, se definido como **true**, acionará uma reindexação completa do conteúdo.

### O índice solicitado {#the-ordered-index}

O índice Ordered é uma extensão do índice Property. No entanto, ele foi substituído. Os índices desse tipo precisam ser substituídos pelo Índice [de propriedades](#the-lucene-property-index)Lucene.

### O Índice de texto completo do Lucene {#the-lucene-full-text-index}

Um indexador de texto completo baseado no Apache Lucene está disponível no AEM 6.

Se um índice de texto completo estiver configurado, todos os query que têm uma condição de texto completo usarão o índice de texto completo, independentemente de haver outras condições indexadas e de haver uma restrição de caminho.

Se nenhum índice de texto completo estiver configurado, os query com condições de texto completo não funcionarão como esperado.

Como o índice é atualizado por meio de um thread em segundo plano assíncrono, algumas pesquisas em texto completo estarão indisponíveis por uma pequena janela de tempo até que os processos em segundo plano sejam concluídos.

Você pode configurar um índice de texto completo do Lucene seguindo o procedimento abaixo:

1. Abra o CRXDE e crie um novo nó em **oak:index**.
1. Nomeie o nó **LuceneIndex** e defina o tipo de nó como **oak:QueryIndexDefinition**
1. Adicione as seguintes propriedades ao nó:

   * **tipo:**  `lucene` (do tipo String)
   * **assíncrono:**  `async` (do tipo String)

1. Salve as alterações.

O Índice Lucene tem as seguintes opções de configuração:

* A propriedade **type** que especificará o tipo de índice deve ser definida como **lucene**
* A propriedade **async** que deve ser definida como **async**. Isso enviará o processo de atualização de índice para um thread em segundo plano.
* A propriedade **includePropertyTypes** , que definirá qual subconjunto de tipos de propriedade será incluído no índice.
* A propriedade **excludePropertyNames** que definirá uma lista de nomes de propriedades - propriedades que devem ser excluídas do índice.
* O sinalizador de **reindexação** que, quando definido como **verdadeiro**, aciona um reíndice de conteúdo completo.

### O Índice De Propriedades Lucene {#the-lucene-property-index}

Desde o **Oak 1.0.8**, o Lucene pode ser usado para criar índices que envolvem restrições de propriedade que não são texto completo.

Para obter um Índice de propriedades Lucene, a propriedade **fulltextEnabled** deve sempre ser definida como false.

Veja o exemplo de query a seguir:

```xml
select * from [nt:base] where [alias] = '/admin'
```

Para definir um Índice de propriedades do Lucene para o query acima, é possível adicionar a seguinte definição criando um novo nó em **oak:index:**

* **Nome:** `LucenePropertyIndex`
* **Tipo:** `oak:QueryIndexDefinition`

Depois que o nó tiver sido criado, adicione as seguintes propriedades:

* **tipo:**

   ```
   lucene (of type String)
   ```

* **async:**

   ```
   async (of type String)
   ```

* **fulltextEnabled:**

   ```
   false (of type Boolean)
   ```

* **includePropertyNames:** `["alias"] (of type String)`

>[!NOTE]
>
>Comparado ao Índice de propriedades normal, o Índice de propriedades do Lucene é sempre configurado no modo assíncrono. Assim, os resultados retornados pelo índice podem nem sempre refletir o estado mais atualizado do repositório.

>[!NOTE]
>
>Para obter informações mais específicas sobre o Índice de propriedades do Lucene, consulte a página [de documentação do](https://jackrabbit.apache.org/oak/docs/query/lucene.html)Apache Jackrabbit Oak Lucene.

### Analisadores Lucene {#lucene-analyzers}

Desde a versão 1.2.0, o Oak suporta analisadores Lucene.

Os analisadores são usados tanto quando um documento é indexado quanto no momento do query. Um analisador examina o texto dos campos e gera um fluxo de token. Os analisadores de Lucene são compostos por uma série de classes de filtros e de tokenizer.

Os analisadores podem ser configurados pelo `analyzers` nó (do tipo `nt:unstructured`) dentro da `oak:index` definição.

O analisador padrão para um índice é configurado no `default` filho do nó do analisador.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>Para obter uma lista de analisadores disponíveis, consulte a documentação da API da versão do Lucene que você está usando.

#### Especificação direta da classe do analisador {#specifying-the-analyzer-class-directly}

Se quiser usar qualquer analisador de caixa, você pode configurá-lo seguindo o procedimento abaixo:

1. Localize o índice com o qual você deseja usar o analisador no `oak:index` nó.

1. No índice, crie um nó filho chamado `default` de tipo `nt:unstructured`.

1. Adicione uma propriedade ao nó padrão com as seguintes propriedades:

   * **Nome:** `class`
   * **Tipo:** `String`
   * **Valor:** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   O valor é o nome da classe do analisador que você deseja usar.

   Você também pode definir o analisador para ser usado com uma versão específica de lúceno usando a propriedade de `luceneMatchVersion` string opcional. Uma sintaxe válida para usá-la com Lucene 4.7 seria:

   * **Nome:** `luceneMatchVersion`
   * **Tipo:** `String`
   * **Valor:** `LUCENE_47`

   Se não `luceneMatchVersion` for fornecido, o Oak usará a versão do Lucene que acompanha.

1. Se desejar adicionar um arquivo de palavras de interrupção às configurações do analisador, você poderá criar um novo nó sob o `default` com as seguintes propriedades:

   * **Nome:** `stopwords`
   * **Tipo:** `nt:file`

#### Criação de analistas por meio da composição {#creating-analyzers-via-composition}

Os analisadores também podem ser compostos com base em `Tokenizers`, `TokenFilters` e `CharFilters`. Você pode fazer isso especificando um analisador e criando nós filhos de seus tokens e filtros opcionais que serão aplicados em ordem listada. Consulte também [https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

Considere esta estrutura de nó como um exemplo:

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





O nome dos filtros, charFilters e tokenizers é formado pela remoção dos sufixos de fábrica. Assim:

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` changes `standard`

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` changes `Mapping`

* `org.apache.lucene.analysis.core.StopFilterFactory` changes `Stop`

Qualquer parâmetro de configuração necessário para a fábrica é especificado como propriedade do código em questão.

Para casos como o carregamento de palavras de interrupção em que o conteúdo de arquivos externos precisa ser carregado, o conteúdo pode ser fornecido criando um nó filho do `nt:file` tipo para o arquivo em questão.

### O Índice Solr {#the-solr-index}

A finalidade do índice Solr é principalmente a pesquisa de texto completo, mas também pode ser usada para indexar a pesquisa por caminho, restrições de propriedade e restrições de tipo primário. Isso significa que o índice Solr no Oak pode ser usado para qualquer tipo de query JCR.

A integração no AEM ocorre no nível do repositório para que o Solr seja um dos possíveis índices que podem ser usados no Oak, a nova implementação do repositório fornecida com o AEM.

Ele pode ser configurado para funcionar como um servidor incorporado com a instância do AEM ou como um servidor remoto.

### Configuração do AEM com um servidor integrado do Solr {#configuring-aem-with-an-embedded-solr-server}

>[!CAUTION]
>
>Não use um servidor Solr incorporado em um ambiente de produção. Só deve ser utilizado num ambiente de desenvolvimento.

O AEM pode ser usado com um servidor de Solr incorporado que pode ser configurado por meio do console da Web. Nesse caso, o servidor Solr será executado na mesma JVM que a instância do AEM à qual está incorporado.

Você pode configurar o servidor Solar incorporado:

1. Ir para o Web Console em `https://serveraddress:4502/system/console/configMgr`
1. Procure &quot;Provedor **de servidor** Oak Solr&quot;.
1. Pressione o botão de edição e, na janela a seguir, defina o tipo de servidor como **Embedded Solr** na lista suspensa.

1. Em seguida, edite &quot;Configuração **de servidor integrado do** Oak Solr&quot; e crie uma configuração. Para obter mais informações sobre as opções de configuração, visite o site [do](https://lucene.apache.org/solr/documentation.html)Apache Solr.

   >[!NOTE]
   >
   >A configuração do diretório inicial do Solr (solr.home.path) procurará uma pasta com o mesmo nome na pasta de instalação do AEM.

1. Abra o CRXDE e faça logon como Administrador.
1. Adicione um nó chamado **solrlndex** do tipo **oak:QueryIndexDefinition** em **oak:index** com as seguintes propriedades:

   * **tipo:** `solr`(do tipo String)
   * **assíncrono:** `async`(do tipo String)
   * **reindexar:** `true`(do tipo Boolean)

1. Salve as alterações.

### Configuração do AEM com um único servidor remoto Solr {#configuring-aem-with-a-single-remote-solr-server}

O AEM também pode ser configurado para funcionar com uma instância remota do servidor Solr:

1. Baixe e extraia a versão mais recente do Solr. Para obter mais informações sobre como fazer isso, consulte a documentação [Instalação do](https://cwiki.apache.org/confluence/display/solr/Installing+Solr)Apache Solr.
1. Agora, crie dois fragmentos Solr. Você pode fazer isso criando pastas para cada compartilhamento na pasta onde a Solr foi descompactada:

   * Para o primeiro compartilhamento, crie a pasta:

   `<solrunpackdirectory>\aemsolr1\node1`

   * Para o segundo compartilhamento, crie a pasta:

   `<solrunpackdirectory>\aemsolr2\node2`

1. Localize a instância de exemplo no pacote Solr. Normalmente, ele está localizado em uma pasta chamada &quot; `example`&quot; na raiz do pacote.
1. Copie as seguintes pastas da instância de exemplo para as duas pastas compartilhadas ( `aemsolr1\node1` e `aemsolr2\node2`):

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. Crie uma nova pasta chamada &quot; `cfg`&quot; em cada uma das duas pastas compartilhadas.
1. Coloque os arquivos de configuração do Solr e do Zookeeper nas `cfg` pastas recém-criadas.

   >[!NOTE]
   >
   >Para obter mais informações sobre a configuração do Solr e do ZooKeeper, consulte a documentação [Configuração do](https://wiki.apache.org/solr/ConfiguringSolr) Solr e o Guia [de Introdução do](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html)ZooKeeper.

1. Start o primeiro compartilhamento com o suporte ao ZooKeeper, acessando `aemsolr1\node1` e executando o seguinte comando:

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. Start o segundo compartilhamento, acessando `aemsolr2\node2` e executando o seguinte comando:

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. Depois que ambos os fragmentos tiverem sido iniciados, teste se tudo está funcionando, conectando-se à interface Solr em `http://localhost:8983/solr/#/`
1. Start AEM e vá para o console da Web em `http://localhost:4502/system/console/configMgr`
1. Defina a seguinte configuração em Configuração **do servidor remoto** Oak Solr:

   * URL HTTP Solr: `http://localhost:8983/solr/`

1. Escolha **Remote Solr** na lista suspensa em **Oak Solr** Server Provider.

1. Vá para CRXDE e faça logon como Administrador.
1. Crie um novo nó chamado **solrIndex** em **oak:index** e defina as seguintes propriedades:

   * **tipo:** solr (do tipo String)
   * **assíncrono:** async (do tipo String)
   * **reindexar:** true (do tipo Boolean)

1. Salve as alterações.

#### Configuração recomendada para Solr {#recommended-configuration-for-solr}

Veja abaixo um exemplo de uma configuração básica que pode ser usada com todas as três implantações Solr descritas neste artigo. Ele acomoda os índices de propriedade dedicados que já estão presentes no AEM e não devem ser usados com outros aplicativos.

Para usá-lo corretamente, é necessário colocar o conteúdo do arquivo diretamente no diretório inicial do Solr. No caso de implantações de vários nós, elas devem ir diretamente para a pasta raiz de cada nó.

Arquivos de configuração de Solr recomendados

[Obter arquivo](assets/recommended-conf.zip)

### Ferramentas de indexação do AEM {#aem-indexing-tools}

O AEM 6.1 também integra duas ferramentas de indexação presentes no AEM 6.0 como parte do conjunto de ferramentas do Adobe Consulting Services Commons:

1. **Explique o Query**, uma ferramenta projetada para ajudar os administradores a entender como os query são executados;
1. **Oak Index Manager**, uma interface de usuário da Web para manter índices existentes.

Agora você pode atingi-los indo até **Ferramentas - Operações - Painel - Diagnóstico** na tela de boas-vindas do AEM.

Para obter mais informações sobre como usá-las, consulte a documentação [do Painel de](/help/sites-administering/operations-dashboard.md)Operações.

#### Criação de índices de propriedade via OSGi {#creating-property-indexes-via-osgi}

O pacote ACS Commons também expõe configurações OSGi que podem ser usadas para criar índices de propriedade.

Você pode acessá-lo pelo Console da Web pesquisando &quot;**Garantir índice** de propriedades do Oak&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### Solução de problemas de indexação {#troubleshooting-indexing-issues}

Podem surgir situações em que query demoram muito para serem executados e o tempo de resposta geral do sistema é lento.

A presente seção apresenta um conjunto de recomendações sobre o que deve ser feito para identificar a causa de tais questões e conselhos sobre a forma de as resolver.

#### Preparando informações de depuração para Análise {#preparing-debugging-info-for-analysis}

A maneira mais fácil de obter as informações necessárias para o query que está sendo executado é através da ferramenta [](/help/sites-administering/operations-dashboard.md#explain-query)Explicar Query. Isso permitirá que você colete as informações precisas necessárias para depurar um query lento, sem precisar consultar as informações de nível de log. Isso é desejável se você souber o query que está sendo depurado.

Se isso não for possível por qualquer motivo, você pode coletar os logs de indexação em um único arquivo e usá-los para solucionar seu problema específico.

#### Ativar registro {#enable-logging}

Para ativar o registro em log, é necessário ativar registros de nível **DEBUG** para as categorias pertencentes à indexação e query Oak. Essas categorias são:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

A categoria **com.day.cq.search** só é aplicável se você estiver usando o utilitário QueryBuilder fornecido pelo AEM.

>[!NOTE]
>
>É importante que os registros sejam definidos como DEBUG somente durante a execução do query que você deseja solucionar, caso contrário, uma grande quantidade de eventos será gerada nos registros ao longo do tempo. Por esse motivo, uma vez que os registros necessários sejam coletados, alterne de volta para o registro em nível INFO para as categorias mencionadas acima.

Você pode ativar o registro seguindo este procedimento:

1. Aponte seu navegador para `https://serveraddress:port/system/console/slinglog`
1. Clique no botão **Adicionar novo agente de log** na parte inferior do console.
1. Na linha recém-criada, adicione as categorias mencionadas acima. Você pode usar o sinal **+** para adicionar mais de uma categoria a um único registrador.
1. Escolha **DEBUG** na lista suspensa de nível **** Log.
1. Defina o arquivo de saída como `logs/queryDebug.log`. Isso correlacionará todos os eventos DEBUG em um único arquivo de log.
1. Execute o query ou renderize a página que está usando o query que deseja depurar.
1. Depois de executar o query, volte ao console de registro e altere o nível de log do registrador recém-criado para **INFO**.

#### Configuração de índice {#index-configuration}

A forma como o query é avaliado é amplamente afetada pela configuração do índice. É importante obter a configuração do índice para que seja analisado ou enviado para suporte. Você pode obter a configuração como um pacote de conteúdo ou uma execução JSON.

Como na maioria dos casos, a configuração de indexação é armazenada sob o `/oak:index` nó no CRXDE, você pode obter a versão JSON em:

`https://serveraddress:port/oak:index.tidy.-1.json`

Se o índice estiver configurado em um local diferente, altere o caminho de acordo.

#### Saída MBean {#mbean-output}

Em alguns casos, é útil fornecer a saída de MBeans relacionados ao índice para depuração. Você pode fazer isso:

1. Ir para o console JMX em:
   `https://serveraddress:port/system/console/jmx`

1. Procure os seguintes MBeans:

   * Estatísticas do Índice Lucene
   * Estatísticas de suporte do CopyOnRead
   * Estatísticas do Query Oak
   * IndexStats

1. Clique em cada MBeans para obter as estatísticas de desempenho. Crie uma captura de tela ou anote-as caso o envio para suporte seja necessário.

Você também pode obter a variante JSON dessas estatísticas nos seguintes URLs:

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

Você também pode fornecer saída JMX consolidada via `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. Isso incluiria todos os detalhes de MBean relacionados ao Oak no formato JSON.

#### Outros detalhes {#other-details}

Você pode coletar detalhes adicionais para ajudar a solucionar o problema, como:

1. A versão Oak em que sua instância está sendo executada. Você pode ver isso abrindo o CRXDE e observando a versão no canto inferior direito da página de boas-vindas, ou verificando a versão do `org.apache.jackrabbit.oak-core` pacote.
1. A saída do Depurador do QueryBuilder do query com problemas. O depurador pode ser acessado em: `https://serveraddress:port/libs/cq/search/content/querydebug.html`

