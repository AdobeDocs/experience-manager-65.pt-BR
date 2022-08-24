---
title: Práticas recomendadas para consultas e indexação
seo-title: Best Practices for Queries and Indexing
description: Este artigo fornece diretrizes sobre como otimizar seus índices e consultas.
seo-description: This article provides guidelines on how to optimize your indexes and queries.
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '4679'
ht-degree: 0%

---

# Práticas recomendadas para consultas e indexação{#best-practices-for-queries-and-indexing}

Junto com a transição para o Oak no AEM 6, algumas alterações importantes foram feitas na maneira como consultas e índices são gerenciados. Em Jackrabbit 2, todo o conteúdo foi indexado por padrão e podia ser consultado livremente. No Oak, os índices devem ser criados manualmente no `oak:index` nó . Uma consulta pode ser executada sem um índice, mas para conjuntos de dados grandes, ela será executada muito lentamente ou até mesmo será abortada.

Este artigo destacará quando criar índices e quando eles não forem necessários, truques para evitar o uso de consultas quando não forem necessárias e dicas para otimizar seus índices e consultas a serem executados da melhor maneira possível.

Além disso, leia a [Documentação do Oak sobre gravação de queries e índices](/help/sites-deploying/queries-and-indexing.md). Além de os índices serem um novo conceito no AEM 6, há diferenças sintáticas em consultas do Oak que precisam ser consideradas ao migrar código de uma instalação AEM anterior.

## Quando utilizar queries {#when-to-use-queries}

### Design de repositório e taxonomia {#repository-and-taxonomy-design}

Ao projetar a taxonomia de um repositório, vários fatores precisam ser considerados. Isso inclui controles de acesso, localização, herança de componentes e propriedades da página, entre outros.

Ao projetar uma taxonomia que atenda a essas preocupações, também é importante considerar a &quot;versabilidade&quot; do design de indexação. Nesse contexto, a navegabilidade é a capacidade de uma taxonomia que permite que o conteúdo seja acessado previsivelmente com base em seu caminho. Isso tornará um sistema mais eficiente, mais fácil de manter do que um, que exigirá a execução de muitas consultas.

Além disso, ao projetar uma taxonomia, é importante considerar se a ordem é importante. Nos casos em que a ordenação explícita não é necessária e um grande número de nós irmãos é esperado, é preferível usar um tipo de nó não ordenado, como `sling:Folder` ou `oak:Unstructured`. Nos casos em que a encomenda é obrigatória, `nt:unstructured` e `sling:OrderedFolder` seria mais adequado.

### Consultas nos componentes {#queries-in-components}

Como as consultas podem ser uma das operações de taxação mais realizadas em um sistema de AEM, é recomendável evitá-las em seus componentes. Ter várias consultas executadas sempre que uma página é renderizada pode, com frequência, degradar o desempenho do sistema. Há duas estratégias que podem ser usadas para evitar a execução de consultas ao renderizar componentes: **nós de percurso** e **resultados da busca prévia**.

#### Nós de passagem {#traversing-nodes}

Se o repositório for projetado de forma que permita o conhecimento prévio da localização dos dados necessários, o código que recupera esses dados dos caminhos necessários poderá ser implantado sem a necessidade de executar consultas para encontrá-los.

Um exemplo disso seria renderizar o conteúdo que se encaixe em uma determinada categoria. Uma abordagem seria organizar o conteúdo com uma propriedade de categoria que possa ser consultada para preencher um componente que mostre itens em uma categoria.

Uma melhor abordagem seria estruturar esse conteúdo em uma taxonomia por categoria para que possa ser recuperado manualmente.

Por exemplo, se o conteúdo for armazenado em uma taxonomia semelhante a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

o `/content/myUnstructuredContent/parentCategory/childCategory` simplesmente pode ser recuperado, seus filhos podem ser analisados e usados para renderizar o componente.

Além disso, ao lidar com um conjunto de resultados pequeno ou homogêneo, pode ser mais rápido atravessar o repositório e coletar os nós necessários, em vez de criar um query para retornar o mesmo conjunto de resultados. De um modo geral, devem ser evitadas questões sempre que possível.

#### Resultados da pré-busca {#prefetching-results}

Às vezes, o conteúdo ou os requisitos em torno do componente não permitirão o uso da travessia do nó como um método de recuperação dos dados necessários. Nesses casos, as consultas necessárias precisam ser executadas antes que o componente seja renderizado para garantir o desempenho ideal para o usuário final.

Se os resultados necessários para o componente puderem ser calculados no momento da criação e não houver expectativa de que o conteúdo será alterado, a consulta poderá ser executada quando o autor aplicar as configurações na caixa de diálogo.

Se os dados ou o conteúdo forem alterados regularmente, a consulta poderá ser executada de acordo com uma programação ou por meio de um ouvinte para obter atualizações sobre os dados subjacentes. Em seguida, os resultados podem ser gravados em um local compartilhado no repositório. Qualquer componente que precise desses dados pode extrair os valores desse único nó sem precisar executar um query no tempo de execução.

## Otimização de consulta {#query-optimization}

Ao executar uma consulta que não está usando um índice, avisos serão registrados em relação à travessia do nó. Se esta for uma consulta que será executada com frequência, um índice deverá ser criado. Para determinar qual índice uma determinada consulta está usando, a variável [Explique a ferramenta Query](/help/sites-administering/operations-dashboard.md#explain-query) é recomendada. Para obter mais informações, o registro DEBUG pode ser ativado para as APIs de pesquisa relevantes.

>[!NOTE]
>
>Após modificar uma definição de índice, o índice precisa ser recriado (reindexado). Dependendo do tamanho do índice, isso pode levar algum tempo para ser concluído.

Ao executar consultas complexas, pode haver casos em que analisar a consulta em várias consultas menores e unir os dados por meio do código depois que o fato é mais eficiente. A recomendação para esses casos é comparar o desempenho das duas abordagens para determinar qual opção seria melhor para o caso de uso em questão.

O AEM permite gravar queries de uma das três maneiras:

* Por meio do [APIs do QueryBuilder](/help/sites-developing/querybuilder-api.md) (recomendado)
* Uso de XPath (recomendado)
* Usando o SQL2

Embora todas as consultas sejam convertidas em SQL2 antes de serem executadas, a sobrecarga da conversão de consulta é mínima e, portanto, a maior preocupação ao escolher um idioma de consulta será a legibilidade e o nível de conforto da equipe de desenvolvimento.

>[!NOTE]
>
>Ao usar o QueryBuilder, ele determinará a contagem de resultados por padrão, que é mais lenta no Oak em comparação às versões anteriores do Jackrabbit. Para compensar isso, você pode usar a variável [parâmetro guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results).

### A ferramenta Explain Query {#the-explain-query-tool}

Assim como em qualquer idioma de consulta, a primeira etapa para otimizar um query é entender como ele será executado. Para ativar essa atividade, você pode usar o [Explique a ferramenta Query](/help/sites-administering/operations-dashboard.md#explain-query) que faz parte do Painel de operações. Com essa ferramenta, uma consulta pode ser plugada e explicada. Um aviso será mostrado se o query causar problemas com um repositório grande, bem como tempo de execução e os índices que serão usados. A ferramenta também pode carregar uma lista de consultas lentas e populares que podem ser explicadas e otimizadas.

### Registro DEBUG para Consultas {#debug-logging-for-queries}

Para obter algumas informações adicionais sobre como o Oak está escolhendo qual índice usar e como o mecanismo de consulta está executando um query, uma **DEPURAR** a configuração de registro pode ser adicionada para os seguintes pacotes:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Remova esse agente de log quando terminar de depurar seu query, pois ele produzirá muita atividade e poderá eventualmente preencher seu disco com arquivos de log.

Para obter mais informações sobre como fazer isso, consulte o [Documentação de registro](/help/sites-deploying/configure-logging.md).

### Estatísticas de índice {#index-statistics}

Lucene registra um Bean JMX que fornecerá detalhes sobre o conteúdo indexado, incluindo o tamanho e o número de documentos presentes em cada um dos índices.

Você pode acessá-lo acessando o Console JMX em `https://server:port/system/console/jmx`

Depois de fazer logon no console JMX, execute uma pesquisa por **Estatísticas do Índice Lucene** para encontrá-lo. Outras estatísticas de índice podem ser encontradas na seção **IndexStats** MBean.

Para obter estatísticas de query, consulte o MBean nomeado **Estatísticas de Consulta Oak**.

Se você deseja pesquisar nos índices usando uma ferramenta como [Luke](https://code.google.com/p/luke/), será necessário usar o console Oak para despejar o índice do `NodeStore` para um diretório de sistema de arquivos. Para obter instruções sobre como fazer isso, leia o [Documentação do Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

Você também pode extrair os índices em seu sistema no formato JSON. Para fazer isso, você precisa acessar o `https://server:port/oak:index.tidy.-1.json`

### Limites de consulta {#query-limits}

**Durante o desenvolvimento**

Definir limites baixos para `oak.queryLimitInMemory` (por exemplo, 10000) e carvalho. `queryLimitReads` (por exemplo, 5000) e otimizar a consulta cara ao hit de um UnsupportedOperationException dizendo &quot;A consulta leu mais de x nós...&quot;

Isso ajuda a evitar consultas que consomem muitos recursos (ou seja, não é suportada por qualquer índice ou pelo índice de cobertura inferior). Por exemplo, uma consulta que lê 1 milhão de nós resultaria em maior E/S e afetaria negativamente o desempenho geral do aplicativo. Qualquer query que falhe devido a limites acima deve ser analisada e otimizada.

#### **Pós-implantação** {#post-deployment}

* Monitore os logs para consultas que acionam grande passagem de nó ou grande consumo de memória heap : &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Otimizar a consulta para reduzir o número de nós atravessados

* Monitore os logs para consultas que acionam grande consumo de memória heap :

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Otimizar a consulta para reduzir o consumo de memória heap

Para AEM versões 6.0 - 6.2, você pode ajustar o limite para a travessia do nó por meio de parâmetros da JVM no script de início de AEM para impedir que consultas grandes sobrecarreguem o ambiente.

Os valores recomendados são :

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

No AEM 6.3, os 2 parâmetros acima são pré-configurados OOTB e podem ser mantidos por meio do QueryEngineSettings do OSGi.

Mais informações disponíveis em : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Dicas para criar índices eficientes {#tips-for-creating-efficient-indexes}

### Devo criar um índice? {#should-i-create-an-index}

A primeira pergunta a se fazer ao criar ou otimizar índices é se eles são realmente necessários para uma determinada situação. Se você for executar o query em questão apenas uma vez ou ocasionalmente e fora do horário de pico do sistema por um processo em lote, talvez seja melhor não criar um índice.

Após criar um índice, sempre que os dados indexados forem atualizados, o índice também deverá ser atualizado. Como isso acarreta implicações de desempenho para o sistema, os índices só devem ser criados quando realmente são necessários.

Além disso, os índices são úteis apenas se os dados contidos no índice forem exclusivos o suficiente para justificá-los. Considere um índice em um livro e os tópicos que ele cobre. Ao indexar um conjunto de tópicos em um texto, geralmente haverá centenas ou milhares de entradas, o que permite que você pule rapidamente para um subconjunto de páginas para encontrar rapidamente as informações que está procurando. Se esse índice tivesse apenas duas ou três entradas, cada uma apontando para várias centenas de páginas, o índice não seria muito útil. Esse mesmo conceito se aplica aos índices do banco de dados. Se houver apenas alguns valores únicos, o índice não será muito útil. Dito isto, um índice também pode tornar-se demasiado grande para ser útil. Para ver as estatísticas de índice, consulte [Estatísticas de índice](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) acima.

### Índices Lucene ou de propriedade? {#lucene-or-property-indexes}

Os índices Lucene foram introduzidos no Oak 1.0.9 e oferecem algumas otimizações poderosas sobre os índices de propriedade que foram introduzidas na primeira inicialização do AEM 6. Ao decidir se deseja usar índices Lucene ou índices de propriedade, considere o seguinte:

* Os índices Lucene oferecem muito mais recursos do que os índices de propriedade. Por exemplo, um índice de propriedade só pode indexar uma única propriedade, enquanto um índice Lucene pode incluir muitos. Para obter mais informações sobre todos os recursos disponíveis nos índices Lucene, consulte o [documentação](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Os índices de Lucene são assíncronos. Embora isso ofereça um aumento considerável no desempenho, também pode induzir um atraso entre quando os dados são gravados no repositório e quando o índice é atualizado. Se for vital que as consultas retornem resultados 100% precisos, um índice de propriedade será necessário.
* Em virtude de serem assíncronos, os índices de Lucene não podem impor restrições de exclusividade. Se isso for necessário, um índice de propriedade precisará ser implementado.

Em geral, é recomendável usar os índices do Lucene, a menos que haja uma necessidade imperiosa de usar os índices de propriedade para que você possa obter os benefícios de maior desempenho e flexibilidade.

### Indexação Solr {#solr-indexing}

AEM também oferece suporte para indexação Solr por padrão. Isso é aproveitado principalmente para oferecer suporte à pesquisa de texto completo, mas também pode ser usado para oferecer suporte a qualquer tipo de consulta JCR. A Solr deve ser considerada quando as instâncias de AEM não tiverem a capacidade da CPU para lidar com o número de consultas necessárias em implantações de pesquisa intensiva, como sites orientados por pesquisa com um alto número de usuários simultâneos. Como alternativa, a Solr pode ser implementada em uma abordagem baseada em crawler para aproveitar alguns dos recursos mais avançados da plataforma.

Os índices solr podem ser configurados para serem executados no servidor AEM para ambientes de desenvolvimento ou podem ser descarregados para uma instância remota para melhorar a escalabilidade de pesquisa nos ambientes de produção e de preparo. Embora a descarga da pesquisa aumente a escalabilidade, ela introduzirá latência e, por causa disso, não é recomendada a menos que seja necessário. Para obter mais informações sobre como configurar a integração Solr e como criar índices Solr, consulte a [Documentação de consultas e indexação do Oak](/help/sites-deploying/queries-and-indexing.md#the-solr-index).

>[!NOTE]
>
>Ao utilizar a abordagem de pesquisa integrada do Solr, permitiria descarregar a indexação em um servidor Solr. Se os recursos mais avançados do servidor Solr forem usados por meio de uma abordagem baseada em crawler, será necessário um trabalho de configuração adicional. O Headwire criou uma [conector de fonte aberta](https://www.aemsolrsearch.com/#/) para acelerar esses tipos de implementações.

O lado negativo para adotar essa abordagem é que, embora por padrão, as consultas AEM respeitarão as ACLs e, portanto, ocultarão resultados aos quais um usuário não tem acesso, a externalização da pesquisa para um servidor Solr não oferecerá suporte a esse recurso. Para que a pesquisa seja externalizada dessa forma, é necessário ter cuidado para garantir que os usuários não sejam apresentados com resultados que não devem ver.

Os casos de uso potenciais em que esta abordagem possa ser adequada são casos em que os dados de pesquisa de várias fontes possam ter de ser agregados. Por exemplo, você pode ter um site sendo hospedado em AEM, bem como um segundo site sendo hospedado em uma plataforma de terceiros. A Solr pode ser configurada para rastrear o conteúdo de ambos os sites e armazená-lo em um índice agregado. Isso permitiria pesquisas entre sites.

### Considerações sobre design {#design-considerations}

A documentação do Oak para índices do Lucene lista várias considerações a serem feitas ao projetar índices:

* Se a consulta usar restrições de caminho diferentes, utilize `evaluatePathRestrictions`. Isso permitirá que a query retorne o subconjunto de resultados no caminho especificado e, em seguida, o filtre com base na query. Caso contrário, a query pesquisará todos os resultados que correspondem aos parâmetros de consulta no repositório e os filtrará com base no caminho.
* Se a consulta usar a classificação, tenha uma definição de propriedade explícita para a propriedade classificada e defina `ordered` para `true` para isso. Isso permitirá que os resultados sejam ordenados como tal no índice e economize em operações de classificação dispendiosas no tempo de execução da consulta.

* Coloque apenas o que é necessário no índice. Adicionar recursos ou propriedades desnecessários fará com que o índice cresça e retarde o desempenho.
* Em um índice de propriedade, ter um nome de propriedade exclusivo ajudaria a reduzir o tamanho em um índice, mas para índices Lucene, use `nodeTypes` e `mixins` para alcançar índices coesos. Consulta de um `nodeType` ou `mixin` terá mais desempenho do que consultar `nt:base`. Ao usar essa abordagem, defina `indexRules` para `nodeTypes` em questão.

* Se as consultas estiverem sendo executadas apenas em determinados caminhos, crie esses índices nesses caminhos. Não é necessário que os índices vivam na raiz do repositório.
* Recomenda-se usar um único índice quando todas as propriedades que estão sendo indexadas estiverem relacionadas para permitir que Lucene avalie nativamente quantas restrições de propriedade forem possíveis. Além disso, uma consulta usará apenas um índice, mesmo durante a execução de uma associação.

### CopyOnRead {#copyonread}

Nos casos em que a `NodeStore` é armazenado remotamente, uma opção chamada `CopyOnRead` podem ser ativadas. A opção fará com que o índice remoto seja gravado no sistema de arquivos local quando ele for lido. Isso pode ajudar a melhorar o desempenho de consultas que geralmente são executadas em relação a esses índices remotos.

Isso pode ser configurado no console OSGi sob a **LuceneIndexProvider** e está habilitado por padrão a partir do Oak 1.0.13.

### Removendo Índices {#removing-indexes}

Ao remover um índice, é sempre recomendável desativar temporariamente o índice definindo a variável `type` propriedade para `disabled` e faça testes para garantir que seu aplicativo funcione corretamente antes de realmente excluí-lo. Observe que um índice não é atualizado enquanto está desativado, portanto, pode não ter o conteúdo correto se ele for reativado e pode precisar ser reindexado.

Após remover um índice de propriedade em uma instância TarMK, a compactação precisará ser executada para recuperar qualquer espaço em disco que estivesse em uso. Para índices Lucene, o conteúdo do índice real fica no BlobStore, portanto, uma coleta de lixo do armazenamento de dados seria necessária.

Ao remover um índice em uma instância MongoDB, o custo da exclusão é proporcional ao número de nós no índice. Como a exclusão de um índice grande pode causar problemas, a abordagem recomendada é desabilitar o índice e excluí-lo somente durante uma janela de manutenção, usando uma ferramenta como **oak-mongo.js**. Observe que essa abordagem não deve ser empregada para o conteúdo normal do nó, pois pode introduzir inconsistências de dados.

>[!NOTE]
>
>Para obter mais informações sobre oak-mongo.js, consulte o [Seção Ferramentas da linha de comando](https://jackrabbit.apache.org/oak/docs/command_line.html) da documentação do Oak.

### O Gabarito de Consulta JCR {#jcrquerycheatsheet}

Para dar suporte à criação de consultas JCR eficientes e definições de índice, o [Folha de Consulta JCR](assets/JCR_query_cheatsheet-v1.1.pdf) está disponível para download e uso como referência durante o desenvolvimento. Ele contém consultas de amostra para o QueryBuilder, XPath e SQL-2, abrangendo vários cenários que se comportam de forma diferente em termos de desempenho de consulta. Também fornece recomendações sobre como criar ou personalizar índices do Oak. O conteúdo desta Folha de Cálculo se aplica ao AEM 6.5 e AEM as a Cloud Service.

## Reindexação {#re-indexing}

Esta seção descreve as **only** motivos aceitáveis para reindexar os índices do Oak.

Fora dos motivos descritos abaixo, iniciar reíndices de índices do Oak fará **not** altere o comportamento ou resolva problemas e aumente desnecessariamente a carga no AEM.

A reindexação de índices Oak deve ser evitada, a menos que seja coberta por uma razão nas tabelas abaixo.

>[!NOTE]
>
>Antes de consultar as tabelas abaixo para determinar se a reindexação é útil, **always** verificar:
>
>* a consulta está correta
>* o query resolve para o índice esperado (usando [Explicar Consulta](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* o processo de indexação foi concluído
>


### Alterações na configuração do índice Oak {#oak-index-configuration-changes}

As únicas condições de não erro aceitáveis para reindexação de índices Oak são se a configuração de um índice Oak tiver sido alterada.

*A reindexação deve ser sempre abordada com a devida consideração sobre o seu impacto no desempenho AEM geral e executada durante períodos de baixa atividade ou janelas de manutenção.*

Os seguintes detalhes podem ser os problemas, juntamente com as resoluções:

* [Alteração de Definição de Índice de Propriedade](#property-index-definition-change)
* [Alteração na Definição do Índice Lucene](#lucene-index-definition-change)

#### Alteração de Definição de Índice de Propriedade {#property-index-definition-change}

* Aplica-se a/se:

   * Todas as versões do Oak
   * Somente [índices de propriedade](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* Sintomas:

   * Nós existentes antes da atualização de definição do índice de propriedade ausente dos resultados

* Como verificar:

   * Determine se os nós ausentes foram criados/modificados antes da implantação da definição de índice atualizada.
   * Verifique o `jcr:created` ou `jcr:lastModified` propriedades de quaisquer nós ausentes em relação ao tempo modificado do índice

* Como resolver:

   * [Re-indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) o índice lucene
   * Como alternativa, toque (execute uma operação de gravação benigna) nos nós ausentes

      * Requer toques manuais ou código personalizado
      * Requer que o conjunto de nós ausentes seja conhecido
      * Exige alterar qualquer propriedade no nó

#### Alteração na Definição do Índice Lucene {#lucene-index-definition-change}

* Aplica-se a/se:

   * Todas as versões do Oak
   * Somente [índices de lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomas:

   * O índice Lucene não contém os resultados esperados
   * Os resultados da consulta não refletem o comportamento esperado da definição de índice
   * O plano de consulta não informa a saída esperada com base na definição de índice

* Como verificar:

   * Verifique se a definição do índice foi alterada usando o método Lucene Index statistics JMX Mbean (LuceneIndex) `diffStoredIndexDefinition`.

* Como resolver:

   * Versões do Oak anteriores à 1.6:

      * [Re-indexação](#how-to-re-index) o índice lucene
   * Oak versões 1.6+

      * Se o conteúdo existente não for afetado pelas alterações, somente uma atualização será necessária

         * [Atualizar](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) o índice lucene, definindo [oak:queryIndexDefinition]@refresh=true
      * Else, [reindexar](#how-to-re-index) o índice lucene

         * Observação: O estado do índice da última reindexação válida (ou indexação inicial) será usado até que uma nova reindexação seja acionada



### Erros e situações excepcionais {#erring-and-exceptional-situations}

A tabela a seguir descreve a única erro aceitável e situações excepcionais em que a reindexação de índices Oak resolverá o problema.

Se ocorrer um problema em AEM que não corresponda aos critérios descritos abaixo, faça o seguinte: **not** reindexe todos os índices, pois não resolverá o problema.

Os seguintes detalhes podem ser os problemas, juntamente com as resoluções:

* [O Binário de Índice Lucene está ausente](#lucene-index-binary-is-missing)
* [O binário de índice Lucene está corrompido](#lucene-index-binary-is-corrupt)

#### O Binário de Índice Lucene está ausente {#lucene-index-binary-is-missing}

* Aplica-se a/se:

   * Todas as versões do Oak
   * Somente [índices de lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomas:

   * O índice Lucene não contém os resultados esperados

* Como verificar:

   * O arquivo de log de erro contém uma exceção informando que um binário do índice Lucene está ausente

* Como resolver:

   * Executar uma verificação de repositório de percurso; por exemplo:

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      atravessar o repositório determina se outros binários (além de arquivos lucene) estão ausentes

   * Se estiverem faltando binários diferentes de índices de lucene, restaure a partir do backup
   * Caso contrário, [reindexar](#how-to-re-index) *all* índices de lucene
   * Nota:

      Essa condição é indicativa de um armazenamento de dados configurado incorretamente que pode resultar em QUALQUER binário (por exemplo, binários de ativos) para ficar ausente.

      Nesse caso, restaure para a última versão válida conhecida do repositório para recuperar todos os binários ausentes.

#### O binário de índice Lucene está corrompido {#lucene-index-binary-is-corrupt}

* Aplica-se a/se:

   * Todas as versões do Oak
   * Somente [índices de lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomas:

   * O índice Lucene não contém os resultados esperados

* Como verificar:

   * O `AsyncIndexUpdate` (a cada 5s) falhará com uma exceção no error.log:

      `...a Lucene index file is corrupt...`

* Como resolver:

   * Remova a cópia local do índice lucene

      1. Parar AEM
      1. Exclua a cópia local do índice lucene em `crx-quickstart/repository/index`
      1. Reiniciar AEM
   * Se isso não resolver o problema, e a variável `AsyncIndexUpdate` as exceções persistem, então:

      1. [Re-indexação](#how-to-re-index) o índice de erro
      1. Também registre um [Suporte a Adobe](https://helpx.adobe.com/support.html) ticket


### Como reindexar {#how-to-re-index}

>[!NOTE]
>
>No AEM 6.5, [oak-run.jar é o ÚNICO método suportado](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) para reindexação em repositórios MongoMK ou RDBMK.

#### Reindexação de índices de propriedade {#re-indexing-property-indexes}

* Use [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) para reindexar o índice de propriedade
* Defina a propriedade async-reindex como true no índice de propriedade

   * `[oak:queryIndexDefinition]@reindex-async=true`

* Recrie o índice de propriedade de forma assíncrona usando o Console da Web por meio do **PropertyIndexAsyncReindex** MBean;

   por exemplo,

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Reindexando índices de propriedade do Lucene {#re-indexing-lucene-property-indexes}

* Use [oak-run.jar para reindexar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) o índice Lucene Property .
* Defina a propriedade async-reindex como true no índice de propriedade do lucene

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>A seção anterior resume e enquadra a orientação de reindexação do Oak do [Documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) no contexto da AEM.

### Pré-extração de Texto de Binários {#text-pre-extraction-of-binaries}

A pré-extração de texto é o processo de extração e processamento de texto de binários, diretamente do Data Store por meio de um processo isolado e expondo diretamente o texto extraído a reindexações subsequentes de índices do Oak.

* A pré-extração de texto do Oak é recomendada para reindexar os índices do Lucene em repositórios com grandes volumes de arquivos (binários) que contêm texto extraível (por exemplo, PDF, documentos do Word, PPTs, TXT etc.) que se qualificam para pesquisa de texto completo por meio dos índices do Oak implantados; por exemplo `/oak:index/damAssetLucene`.
* A pré-extração de texto só beneficiará a re/indexação de índices Lucene e NÃO de índices de propriedade Oak, já que os índices de propriedade não extraem texto de binários.
* A pré-extração de texto tem um alto impacto positivo quando a reindexação de texto completo de binários pesados de texto (PDF, Doc, TXT etc.), onde como repositório de imagens não terá a mesma eficiência, pois as imagens não contêm texto extractável.
* A pré-extração de texto executa a extração de texto completo relacionado à pesquisa de maneira eficiente e o expõe ao processo de re-indexação do Oak de uma maneira que é extra eficiente para consumir.

#### Quando a pré-extração de texto pode ser usada? {#when-can-text-pre-extraction-be-used}

Reindexação de um **existente** índice lucene com extração binária ativada

* Reindexação de processamento **all** conteúdo candidato no repositório; quando os binários para extrair texto completo são numerosos ou complexos, uma carga computacional aumentada para executar a extração de texto completo é colocada no AEM. A pré-extração de texto move o &quot;trabalho computacional dispendioso&quot; da extração de texto para um processo isolado que acessa diretamente AEM Data Store, evitando a sobrecarga e a contenção de recursos na AEM.

Suporte à implantação de um **novo** índice lucene para AEM com extração binária ativada

* Quando um novo índice (com extração binária ativada) é implantado em AEM, o Oak indexa automaticamente todo o conteúdo candidato na próxima execução assíncrona do índice de texto completo. Pelos mesmos motivos descritos na reindexação acima, isso pode resultar em carga injustificada no AEM.

#### Quando a pré-extração de texto NÃO pode ser usada? {#when-can-text-pre-extraction-not-be-used}

A pré-extração de texto não pode ser usada para o novo conteúdo adicionado ao repositório, nem é necessária.

O novo conteúdo é adicionado ao repositório será indexado de forma natural e incremental pelo processo de indexação assíncrona de texto completo (por padrão, a cada 5 segundos).

Em operação normal do AEM, por exemplo, o upload de Ativos por meio da interface do usuário da Web ou o assimilação programática de Ativos, o AEM indexará automaticamente e incrementalmente o texto completo do novo conteúdo binário. Como a quantidade de dados é incremental e relativamente pequena (aproximadamente a quantidade de dados que pode ser mantida no repositório em 5 segundos), AEM pode executar a extração de texto completo dos binários durante a indexação sem afetar o desempenho geral do sistema.

#### Pré-requisitos para usar a pré-extração de texto {#prerequisites-to-using-text-pre-extraction}

* Você reindexará um índice de lucene que executa extração binária de texto completo ou implantará um novo índice que fará binários de índice de texto completo do conteúdo existente
* O conteúdo (binários) do qual o texto deve ser pré-extraído deve estar no repositório
* Uma janela de manutenção para gerar o arquivo CSV E executar a reindexação final
* Versão do Oak: 1.0.18+, 1.2.3+
* [oak-run.jar](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)versão 1.7.4+
* Uma pasta/compartilhamento do sistema de arquivos para armazenar o texto extraído acessível da(s) instância(s) de indexação AEM

   * A configuração OSGi de pré-extração de texto requer um caminho de sistema de arquivos para os arquivos de texto extraídos, de modo que eles devem ser acessíveis diretamente da instância de AEM (unidade local ou montagem de compartilhamento de arquivos)

#### Como executar a pré-extração de texto {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***Os comandos oak-run.jar descritos abaixo são completamente enumerados em [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>O diagrama e as etapas acima servem para explicar e complementar as etapas de pré-extração do texto técnico descritas na documentação do Apache Oak.

![Fluxo do processo de pré-extração de texto](assets/chlimage_1-139.png)

**Gerar lista de conteúdo para pré-extrair**

*Execute a Etapa 1(a-b) durante uma janela de manutenção/período de baixo uso, pois o armazenamento de nós é atravessado durante essa operação, o que pode causar carga significativa no sistema.*

1 bis. Executar `oak-run.jar --generate` para criar uma lista de nós que terá seu texto pré-extraído.

1-B. A lista de nós (1a) é armazenada no sistema de arquivos como um arquivo CSV

Observe que todo o armazenamento de nós é percorrido (conforme especificado pelos caminhos no comando oak-run) sempre `--generate` é executada, e uma **novo** O arquivo CSV é criado. O arquivo CSV é **not** reutilizado entre execuções discretas do processo de pré-extração de texto (Etapas 1 - 2).

**Pré-extrair texto para o sistema de arquivos**

*A etapa 2(a-c) pode ser executada durante a operação normal de AEM, pois só interage com o Data Store.*

2 bis. Executar `oak-run.jar --tika` para pré-extrair texto para os nós binários enumerados no arquivo CSV gerado em (1b)

2 ter. O processo iniciado em (2a) acessa diretamente os nós binários definidos no CSV no Data Store e extrai texto.

2-C.  O texto extraído é armazenado no sistema de arquivos em um formato assimilável pelo processo de reindexação do Oak (3a)

O texto pré-extraído é identificado no CSV pela impressão digital binária. Se o arquivo binário for o mesmo, o mesmo texto pré-extraído poderá ser usado em instâncias AEM. Como a Publicação do AEM geralmente é um subconjunto do Autor do AEM, o texto pré-extraído do Autor do AEM também pode ser usado para reindexar a Publicação do AEM (supondo que a Publicação do AEM tenha acesso do sistema de arquivos aos arquivos de texto extraídos).

O texto pré-extraído pode ser adicionado de forma incremental ao longo do tempo. A pré-extração de texto ignorará a extração de binários extraídos anteriormente, portanto, a prática recomendada é manter o texto pré-extraído caso a reindexação precise ocorrer novamente no futuro (supondo que o conteúdo extraído não seja proibitivamente grande. Se estiver, avalie o zipamento do conteúdo no intervalo, já que o texto é bem compactado).

**Reindexe índices do Oak, fornecendo texto completo de arquivos de Texto extraído**

*Execute a reindexação (Etapas 3a-b) durante um período de manutenção/baixo uso, pois o armazenamento de nós é atravessado durante essa operação, o que pode causar carga significativa no sistema.*

3 bis. [Re-indexação](#how-to-re-index) de índices Lucene é chamado em AEM

3 ter. A configuração OSGi do Apache Jackrabbit Oak DataStore PreExtractedTextProvider (configurada para apontar para o texto extraído via caminho do sistema de arquivos) instrui o Oak a obter o texto completo dos arquivos extraídos e evita acessar e processar diretamente os dados armazenados no repositório.
