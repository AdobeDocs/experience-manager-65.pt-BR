---
title: Práticas recomendadas para Query e indexação
seo-title: Práticas recomendadas para Query e indexação
description: Este artigo fornece orientações sobre como otimizar seus índices e query.
seo-description: Este artigo fornece orientações sobre como otimizar seus índices e query.
uuid: 0609935a-4a72-4b8e-a28e-daede9fc05f4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3f06f7a1-bdf0-4700-8a7f-1d73151893ba
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '4618'
ht-degree: 0%

---


# Práticas recomendadas para Query e indexação{#best-practices-for-queries-and-indexing}

Juntamente com a transição de Oak no AEM 6, foram feitas algumas mudanças importantes na forma como query e índices são gerenciados. Em Jackrabbit 2, todo o conteúdo era indexado por padrão e podia ser consultado livremente. No Oak, os índices devem ser criados manualmente no nó `oak:index`. Um query pode ser executado sem um índice, mas para grandes conjuntos de dados, ele será executado muito lentamente, ou até mesmo aborta.

Este artigo destacará quando criar índices e quando eles não forem necessários, truques para evitar o uso de query quando eles não forem necessários e dicas para otimizar seus índices e query a serem executados da melhor forma possível.

Além disso, leia a documentação [Oak sobre como gravar query e índices](/help/sites-deploying/queries-and-indexing.md). Além de os índices serem um novo conceito no AEM 6, há diferenças sintáticas nos query Oak que precisam ser levadas em conta ao migrar o código de uma instalação AEM anterior.

## Quando usar Query {#when-to-use-queries}

### Design de repositório e taxonomia {#repository-and-taxonomy-design}

Ao conceber a taxonomia de um repositório, devem ser tidos em conta vários fatores. Isso inclui controles de acesso, localização, herança de propriedade de componente e página, entre outros.

Ao projetar uma taxonomia que aborde essas preocupações, também é importante considerar a &quot;versabilidade&quot; do design de indexação. Neste contexto, a navegabilidade é a capacidade de uma taxonomia que permite que o conteúdo seja acessado previsivelmente com base em seu caminho. Isso permitirá um sistema mais eficiente, mais fácil de manter do que um que exigirá a execução de muitos query.

Além disso, ao projetar uma taxonomia, é importante considerar se a ordem é importante. Nos casos em que a ordem explícita não é necessária e um grande número de nós irmãos é esperado, é preferível usar um tipo de nó não ordenado, como `sling:Folder` ou `oak:Unstructured`. Nos casos em que a solicitação é obrigatória, `nt:unstructured` e `sling:OrderedFolder` seriam mais apropriados.

### Query nos componentes {#queries-in-components}

Como os query podem ser uma das operações de taxação mais realizadas em um sistema AEM, convém evitá-los em seus componentes. Ter vários query executados cada vez que uma página é renderizada pode, com frequência, diminuir o desempenho do sistema. Há duas estratégias que podem ser usadas para evitar a execução de query ao renderizar componentes: **atravessando nós** e **pré-busca de resultados**.

#### Nós de cruzamento {#traversing-nodes}

Se o repositório for projetado de modo a permitir o conhecimento prévio da localização dos dados necessários, o código que recupera esses dados dos caminhos necessários pode ser implantado sem a necessidade de executar query para encontrá-los.

Um exemplo disso seria a renderização de conteúdo que se encaixe em uma determinada categoria. Uma abordagem seria organizar o conteúdo com uma propriedade de categoria que possa ser consultada para preencher um componente que mostre itens em uma categoria.

Uma melhor abordagem seria estruturar esse conteúdo em uma taxonomia por categoria para que possa ser recuperado manualmente.

Por exemplo, se o conteúdo for armazenado em uma taxonomia semelhante a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

o nó `/content/myUnstructuredContent/parentCategory/childCategory` pode ser recuperado, seus filhos podem ser analisados e usados para renderizar o componente.

Além disso, ao lidar com um conjunto de resultados pequeno ou homogêneo, pode ser mais rápido atravessar o repositório e coletar os nós necessários, em vez de criar um query para retornar o mesmo conjunto de resultados. De um modo geral, os query devem ser evitados sempre que possível.

#### Resultados da Pré-busca {#prefetching-results}

Às vezes, o conteúdo ou os requisitos em torno do componente não permitirão o uso do nó transversal como um método de recuperação dos dados necessários. Nesses casos, os query necessários precisam ser executados antes da renderização do componente para que o desempenho ideal seja garantido para o usuário final.

Se os resultados necessários para o componente puderem ser calculados no momento da criação e não houver expectativa de que o conteúdo será alterado, o query poderá ser executado quando o autor aplicar as configurações na caixa de diálogo.

Se os dados ou o conteúdo forem alterados regularmente, o query poderá ser executado de acordo com um cronograma ou por meio de um ouvinte para atualizações dos dados subjacentes. Em seguida, os resultados podem ser gravados em um local compartilhado no repositório. Qualquer componente que precise desses dados pode então retirar os valores desse único nó sem precisar executar um query em tempo de execução.

## Otimização do query {#query-optimization}

Ao executar um query que não esteja usando um índice, os avisos serão registrados em relação ao nó transversal. Se esse for um query que será executado com frequência, um índice deverá ser criado. Para determinar qual índice determinado query está usando, a [ferramenta Explorar Query](/help/sites-administering/operations-dashboard.md#explain-query) é recomendada. Para obter informações adicionais, o registro DEBUG pode ser ativado para as APIs de pesquisa relevantes.

>[!NOTE]
>
>Depois de modificar uma definição de índice, o índice precisa ser reconstruído (reindexado). Dependendo do tamanho do índice, isso pode levar algum tempo para ser concluído.

Durante a execução de query complexos, pode haver casos em que dividir o query em vários query menores e unir os dados por meio do código depois que o fato for mais eficiente. A recomendação para estes casos é comparar o desempenho das duas abordagens para determinar qual opção seria melhor para o caso de utilização em questão.

AEM permite escrever query de uma das três maneiras:

* Por meio das [APIs do QueryBuilder](/help/sites-developing/querybuilder-api.md) (recomendado)
* Uso do XPath (recomendado)
* Uso do SQL2

Embora todos os query sejam convertidos para SQL2 antes de serem executados, a sobrecarga da conversão de query é mínima e, portanto, a maior preocupação ao escolher um idioma de query será a capacidade de leitura e o nível de conforto da equipe de desenvolvimento.

>[!NOTE]
>
>Ao usar o QueryBuilder, ele determinará a contagem de resultados por padrão, que é mais lenta no Oak em comparação às versões anteriores do Jackrabbit. Para compensar isso, você pode usar o parâmetro [supyTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results).

### A ferramenta Explorar Query {#the-explain-query-tool}

Como em qualquer idioma do query, a primeira etapa para otimizar um query é entender como ele será executado. Para habilitar essa atividade, você pode usar a [ferramenta Explorar Query](/help/sites-administering/operations-dashboard.md#explain-query) que faz parte do Painel Operações. Com essa ferramenta, um query pode ser conectado e explicado. Será exibido um aviso se o query causar problemas em um repositório grande, bem como no tempo de execução e nos índices que serão usados. A ferramenta também pode carregar uma lista de query lentos e populares que podem ser explicados e otimizados.

### Registro DEBUG para Query {#debug-logging-for-queries}

Para obter informações adicionais sobre como o Oak está escolhendo qual índice usar e como o mecanismo de query está executando um query, uma configuração de registro **DEBUG** pode ser adicionada para os seguintes pacotes:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Certifique-se de remover esse registrador quando terminar de depurar seu query, pois ele resultará em muita atividade e poderá eventualmente preencher seu disco com arquivos de registro.

Para obter mais informações sobre como fazer isso, consulte a [Documentação de registro](/help/sites-deploying/configure-logging.md).

### Estatísticas do Índice {#index-statistics}

Lucene registra um Bean JMX que fornecerá detalhes sobre o conteúdo indexado, incluindo o tamanho e o número de documentos presentes em cada um dos índices.

Você pode acessá-la acessando o Console JMX em `https://server:port/system/console/jmx`

Depois de fazer logon no console JMX, procure **Estatísticas do Índice Lucene** para encontrá-lo. Outras estatísticas de índice podem ser encontradas no MBean **IndexStats**.

Para obter estatísticas de query, consulte o MBean chamado **Oak Query Statistics**.

Se você quiser acessar seus índices usando uma ferramenta como [Luke](https://code.google.com/p/luke/), será necessário usar o console Oak para descarregar o índice de `NodeStore` para um diretório de sistema de arquivos. Para obter instruções sobre como fazer isso, leia a [documentação do Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

Você também pode extrair os índices no seu sistema no formato JSON. Para fazer isso, você precisa acessar `https://server:port/oak:index.tidy.-1.json`

### Limites de consulta {#query-limits}

**Durante o desenvolvimento**

Defina limites baixos para `oak.queryLimitInMemory` (por exemplo, 10000) e carvalho. `queryLimitReads` (por exemplo, 5000) e otimize o query caro ao clicar em UnsupportedOperationException dizendo &quot;O query lê mais de x nós...&quot;.

Isso ajuda a evitar query que consomem muitos recursos (ou seja, não suportado por qualquer índice ou apoiado por um índice de cobertura menor). Por exemplo, um query que lê 1 milhão de nós levaria ao aumento da E/S e afetaria negativamente o desempenho geral do aplicativo. Qualquer query que falhar devido aos limites acima deve ser analisado e otimizado.

#### **Pós-implantação** {#post-deployment}

* Monitore os registros em busca de query que acionem um grande nó transversal ou grande consumo de memória heap: &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Otimizar o query para reduzir o número de nós atravessados

* Monitore os registros em busca de query que acionem um grande consumo de memória heap:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Otimize o query para reduzir o consumo de memória do heap

Para as versões AEM 6.0 - 6.2, é possível ajustar o limite para a passagem de nó pelos parâmetros JVM no script de start AEM para impedir que query grandes sobrecarreguem o ambiente.

Os valores recomendados são:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

No AEM 6.3, os 2 parâmetros acima são OOTB pré-configurados e podem ser mantidos por meio das Configurações do QueryEngine do OSGi.

Mais informações disponíveis em: [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Dicas para criar índices eficientes {#tips-for-creating-efficient-indexes}

### Devo criar um índice? {#should-i-create-an-index}

A primeira pergunta a ser feita ao criar ou otimizar índices é se eles são realmente necessários para uma determinada situação. Se você só executará o query em questão uma vez ou apenas ocasionalmente e fora do horário de pico do sistema por um processo em lote, talvez seja melhor não criar um índice.

Depois de criar um índice, sempre que os dados indexados forem atualizados, o índice também deverá ser atualizado. Uma vez que isso acarreta implicações de desempenho para o sistema, os índices só devem ser criados quando forem realmente necessários.

Além disso, os índices só são úteis se os dados contidos no índice forem exclusivos o suficiente para garantir que sejam válidos. Considere um índice em um livro e os tópicos que ele aborda. Ao indexar um conjunto de tópicos em um texto, normalmente haverá centenas ou milhares de entradas, o que permite que você pule rapidamente para um subconjunto de páginas para encontrar rapidamente as informações que está procurando. Se esse índice tivesse apenas duas ou três entradas, cada uma apontando para várias centenas de páginas, o índice não seria muito útil. Esse mesmo conceito se aplica aos índices do banco de dados. Se houver apenas alguns valores únicos, o índice não será muito útil. Dito isto, um índice também pode tornar-se demasiado grande para ser útil. Para consultar as estatísticas de índice, consulte [Estatísticas de índice](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) acima.

### Índices Lucene ou de propriedade? {#lucene-or-property-indexes}

Os índices de Lucene foram introduzidos no Oak 1.0.9 e ofertas algumas otimizações poderosas sobre os índices de propriedade que foram introduzidas na primeira inicialização do AEM 6. Ao decidir se usar índices Lucene ou índices de propriedade, considere o seguinte:

* Lucene indexa oferta com muito mais recursos do que índices de propriedade. Por exemplo, um índice de propriedade só pode indexar uma única propriedade enquanto um índice Lucene pode incluir muitos. Para obter mais informações sobre todos os recursos disponíveis nos índices Lucene, consulte a [documentação](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Os índices de Lucene são assíncronos. Embora isso oferta um aumento considerável no desempenho, também pode induzir um atraso entre quando os dados são gravados no repositório e quando o índice é atualizado. Se for vital que os query retornem resultados 100% precisos, um índice de propriedade será necessário.
* Por serem assíncronos, os índices de Lucene não conseguem impor restrições de exclusividade. Se isso for necessário, um índice de propriedade precisará ser implementado.

Em geral, recomenda-se usar índices Lucene, a menos que haja uma necessidade imperiosa de usar índices de propriedade para que você possa obter os benefícios de maior desempenho e flexibilidade.

### Indexação Solr {#solr-indexing}

AEM também oferece suporte para indexação Solr por padrão. Isso é aproveitado principalmente para suportar a pesquisa de texto completo, mas também pode ser usado para suportar qualquer tipo de query JCR. A Solr deve ser considerada quando as instâncias de AEM não têm capacidade de CPU para lidar com o número de query necessários em implantações de pesquisa intensiva, como sites orientados por pesquisa com um alto número de usuários simultâneos. Como alternativa, a Solr pode ser implementada em uma abordagem baseada em rastreador para aproveitar alguns dos recursos mais avançados da plataforma.

Os índices solr podem ser configurados para serem executados no servidor AEM para ambientes de desenvolvimento ou podem ser descarregados para uma instância remota para melhorar a escalabilidade da pesquisa nos ambientes de produção e preparo. Embora a descarga da pesquisa melhore a escalabilidade, ela introduzirá latência e, por isso, não é recomendada, a menos que seja necessário. Para obter mais informações sobre como configurar a integração do Solr e como criar índices do Solr, consulte a documentação [Oak Query and Indexing](/help/sites-deploying/queries-and-indexing.md#the-solr-index).

>[!NOTE]
>
>Ao utilizar a abordagem de pesquisa integrada do Solr, será possível descarregar a indexação em um servidor Solr. Se os recursos mais avançados do servidor Solr forem usados por meio de uma abordagem baseada em crawler, será necessário um trabalho de configuração adicional. O cabo de alimentação criou um [conector de fonte aberta](https://www.aemsolrsearch.com/#/) para acelerar esses tipos de implementações.

O lado negativo dessa abordagem é que, embora por padrão, os query AEM respeitarão as ACLs e, portanto, ocultarão os resultados aos quais um usuário não tem acesso, a externalização da pesquisa para um servidor Solr não oferecerá suporte a esse recurso. Para que a pesquisa seja externalizada desta forma, é necessário ter um cuidado especial para garantir que os utilizadores não sejam apresentados com resultados que não devem ver.

Casos de utilização potencial em que esta abordagem possa ser adequada são casos em que podem ser necessários agregados dados de pesquisa de várias fontes. Por exemplo, você pode ter um site sendo hospedado em AEM, bem como um segundo site sendo hospedado em uma plataforma de terceiros. A Solr pode ser configurada para rastrear o conteúdo de ambos os sites e armazená-los em um índice agregado. Isso permitiria pesquisas entre sites.

### Considerações sobre design {#design-considerations}

A documentação do Oak para Lucene indexa várias considerações a serem feitas ao projetar índices:

* Se o query usar restrições de caminho diferentes, utilize `evaluatePathRestrictions`. Isso permitirá que o query retorne o subconjunto de resultados sob o caminho especificado e, em seguida, filtre-os com base no query. Caso contrário, o query pesquisará todos os resultados que correspondem aos parâmetros do query no repositório e os filtrará com base no caminho.
* Se o query usar a classificação, tenha uma definição de propriedade explícita para a propriedade classificada e defina `ordered` como `true` para ela. Isso permitirá que os resultados sejam ordenados como tal no índice e economizados em operações de classificação dispendiosas no momento da execução do query.

* Coloque apenas o que é necessário no índice. Adicionar recursos ou propriedades desnecessárias fará com que o índice cresça e diminua o desempenho.
* Em um índice de propriedade, ter um nome de propriedade exclusivo ajudaria a reduzir o tamanho em um índice, mas para índices Lucene, o uso de `nodeTypes` e `mixins` deve ser feito para alcançar índices coesos. A consulta de um `nodeType` ou `mixin` específico terá maior desempenho do que a consulta de `nt:base`. Ao usar essa abordagem, defina `indexRules` para `nodeTypes` em questão.

* Se seus query estiverem sendo executados somente sob determinados caminhos, crie esses índices nesses caminhos. Os índices não precisam permanecer na raiz do repositório.
* Recomenda-se usar um único índice quando todas as propriedades que estão sendo indexadas estiverem relacionadas para permitir que Lucene avalie de forma nativa quantas restrições de propriedade forem possíveis. Além disso, um query usará apenas um índice, mesmo ao executar uma junção.

### CopyOnRead {#copyonread}

Nos casos em que `NodeStore` é armazenado remotamente, uma opção chamada `CopyOnRead` pode ser ativada. A opção fará com que o índice remoto seja gravado no sistema de arquivos local quando ele for lido. Isso pode ajudar a melhorar o desempenho de query que geralmente são executados em relação a esses índices remotos.

Isso pode ser configurado no console OSGi sob o serviço **LuceneIndexProvider** e está ativado por padrão a partir do Oak 1.0.13.

### Removendo Índices {#removing-indexes}

Ao remover um índice, é sempre recomendável desativar temporariamente o índice definindo a propriedade `type` como `disabled` e fazer testes para garantir que seu aplicativo funcione corretamente antes de excluí-lo. Observe que um índice não é atualizado enquanto está desativado, portanto, talvez ele não tenha o conteúdo correto se for reativado e talvez precise ser indexado novamente.

Após remover um índice de propriedade em uma instância TarMK, será necessário executar a compactação para recuperar qualquer espaço em disco que estivesse em uso. Para índices Lucene, o conteúdo de índice real fica no BlobStore, portanto, seria necessário uma coleta de lixo do armazenamento de dados.

Ao remover um índice em uma instância MongoDB, o custo da exclusão é proporcional ao número de nós no índice. Como a exclusão de um índice grande pode causar problemas, a abordagem recomendada é desativar o índice e excluí-lo somente durante uma janela de manutenção, usando uma ferramenta como **oak-mongo.js**. Observe que essa abordagem não deve ser empregada para o conteúdo normal de nós, pois pode introduzir inconsistências de dados.

>[!NOTE]
>
>Para obter mais informações sobre oak-mongo.js, consulte a seção [Ferramentas de Linha de Comando](https://jackrabbit.apache.org/oak/docs/command_line.html) da documentação do Oak.

## Indexação novamente {#re-indexing}

Esta seção descreve os motivos aceitáveis **only** para reindexar os índices Oak.

Fora dos motivos descritos abaixo, iniciar reíndices de índices Oak **não** alterará o comportamento ou resolverá problemas e aumentará desnecessariamente a carga em AEM.

A reindexação de índices Oak deve ser evitada, a menos que seja coberta por uma razão nas tabelas abaixo.

>[!NOTE]
>
>Antes de consultar as tabelas abaixo para determinar se a reindexação é útil,** sempre **verifique:
>
>* o query está correto
>* o query é resolvido para o índice esperado (usando [Explicar Query](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* o processo de indexação foi concluído

>



### Alterações na configuração do índice Oak {#oak-index-configuration-changes}

As únicas condições de não erro aceitáveis para reindexar os índices Oak são se a configuração de um índice Oak tiver sido alterada.

*A reindexação deve ser sempre abordada com a devida consideração sobre o seu impacto no desempenho AEM geral e executada durante períodos de baixas atividades ou janelas de manutenção.*

Os seguintes detalhes podem ser discutidos em conjunto com as resoluções:

* [Alteração da Definição do Índice de Propriedades](#property-index-definition-change)
* [Alteração da Definição do Índice Lucene](#lucene-index-definition-change)

#### Alteração na Definição do Índice de Propriedades {#property-index-definition-change}

* Aplica-se a/se:

   * Todas as versões do Oak
   * Somente [índices de propriedade](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* Sintomas:

   * Nós existentes antes da atualização de definição do índice de propriedade ausentes dos resultados

* Como verificar:

   * Determine se nós ausentes foram criados/modificados antes da implantação da definição de índice atualizada.
   * Verifique as propriedades `jcr:created` ou `jcr:lastModified` de qualquer nó ausente em relação à hora modificada do índice

* Como resolver:

   * [Indexar novamente ](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) o índice de lúcene
   * Como alternativa, toque (execute uma operação de gravação benigna) nos nós ausentes

      * Requer toques manuais ou código personalizado
      * Requer que o conjunto de nós ausentes seja conhecido
      * Exige alterar qualquer propriedade no nó

#### Alteração de Definição de Índice Lucene {#lucene-index-definition-change}

* Aplica-se a/se:

   * Todas as versões do Oak
   * Somente [índices de lúcene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomas:

   * O índice Lucene não contém os resultados esperados
   * Os resultados do query não refletem o comportamento esperado da definição do índice
   * O plano de query não informa a saída esperada com base na definição do índice

* Como verificar:

   * Verifique se a definição do índice foi alterada usando as estatísticas do Índice Lucene JMX Mbean (LuceneIndex), método `diffStoredIndexDefinition`.

* Como resolver:

   * Versões de carvalho anteriores à versão 1.6:

      * [Indexar novamente ](#how-to-re-index) o índice de lúcene
   * Oak versões 1.6+

      * Se o conteúdo existente não for afetado pelas alterações, somente uma atualização será necessária

         * [Atualize ](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) o índice de lúcene definindo  [oak:queryIndexDefinition]@refresh=true
      * Caso contrário, [reindexar](#how-to-re-index) o índice de lúcene

         * Observação: O estado do índice da última reindexação boa (ou indexação inicial) será usado até que uma nova reindexação seja acionada



### Erros e situações excepcionais {#erring-and-exceptional-situations}

A tabela a seguir descreve as únicas situações de erro aceitáveis e excepcionais em que a reindexação de índices Oak resolverá o problema.

Se ocorrer um problema em AEM que não corresponda aos critérios descritos abaixo, faça **not** reindexar qualquer índice, pois isso não resolverá o problema.

Os seguintes detalhes podem ser discutidos em conjunto com as resoluções:

* [Binário do Índice Lucene ausente](#lucene-index-binary-is-missing)
* [O Binário do Índice Lucene está corrompido](#lucene-index-binary-is-corrupt)

#### O Binário do Índice Lucene está ausente {#lucene-index-binary-is-missing}

* Aplica-se a/se:

   * Todas as versões do Oak
   * Somente [índices de lúcene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomas:

   * O índice Lucene não contém os resultados esperados

* Como verificar:

   * O arquivo de log de erros contém uma exceção informando que um binário do índice Lucene está ausente

* Como resolver:

   * Executar uma verificação de repositório de percurso; por exemplo:

      [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

      atravessar o repositório determina se outros binários (além de arquivos de lucene) estão ausentes

   * Se estiverem faltando binários diferentes de índices de lúcene, restaure a partir do backup
   * Caso contrário, [reindexar](#how-to-re-index) *todos* índices de lúcene
   * Nota:

      Essa condição é indicativa de um armazenamento de dados configurado incorretamente que pode resultar em QUALQUER binário (por exemplo, binários de ativos) para ficar ausente.

      Nesse caso, restaure para a última versão em boas condições do repositório para recuperar todos os binários ausentes.

#### O Binário do Índice Lucene está corrompido {#lucene-index-binary-is-corrupt}

* Aplica-se a/se:

   * Todas as versões do Oak
   * Somente [índices de lúcene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomas:

   * O índice Lucene não contém os resultados esperados

* Como verificar:

   * O `AsyncIndexUpdate` (a cada 5s) falhará com uma exceção no error.log:

      `...a Lucene index file is corrupt...`

* Como resolver:

   * Remover a cópia local do índice de lúcene

      1. Parar AEM
      1. Exclua a cópia local do índice de lucene em `crx-quickstart/repository/index`
      1. Reiniciar AEM
   * Se isso não resolver o problema e as exceções `AsyncIndexUpdate` persistirem, então:

      1. [Indexar novamente ](#how-to-re-index) o índice de erro
      1. Também arquivar um ticket [Suporte ao Adobe](https://helpx.adobe.com/support.html)


### Como reindexar {#how-to-re-index}

>[!NOTE]
>
>No AEM 6.5, [oak-run.jar é o ÚNICO método suportado](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) para reindexação em repositórios MongoMK ou RDBMK.

#### Indexação dos índices de propriedade {#re-indexing-property-indexes}

* Use [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) para indexar novamente o índice de propriedade
* Defina a propriedade async-reindex como true no índice da propriedade

   * `[oak:queryIndexDefinition]@reindex-async=true`

* Indexar novamente o índice de propriedade de forma assíncrona usando o Console da Web por meio do MBean **PropertyIndexAsyncReindex**;

   por exemplo,

   [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Indexando novamente os índices de propriedade do Lucene {#re-indexing-lucene-property-indexes}

* Use [oak-run.jar para reindexar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) o índice da propriedade Lucene.
* Defina a propriedade async-reindex como true no índice da propriedade lucene

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>A seção anterior resume e enquadra a orientação de reindexação do Oak a partir da [documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) no contexto da AEM.

### Pré-extração de Texto de Binários {#text-pre-extraction-of-binaries}

A pré-extração de texto é o processo de extração e processamento de texto de binários, diretamente do Data Store por meio de um processo isolado e a exposição direta do texto extraído a reindexações subsequentes de índices Oak.

* É recomendável pré-extração de texto de carvalho para reindexar os índices Lucene em repositórios com grandes volumes de arquivos (binários) que contêm texto extraível (por exemplo, PDFs, Word Docs, PPTs, TXT etc.) que se qualificam para pesquisa em texto completo por meio de índices Oak implantados; por exemplo `/oak:index/damAssetLucene`.
* A pré-extração de texto beneficiará apenas a reindexação de índices Lucene e de índices de propriedade NOT Oak, já que os índices de propriedade não extraem texto de binários.
* A pré-extração de texto tem um impacto positivo alto quando a reindexação de texto completo de binários com texto pesado (PDF, Doc, TXT etc.), onde, como repositório de imagens, não terá a mesma eficiência, pois as imagens não contêm texto extraível.
* A pré-extração de texto executa a extração do texto de pesquisa de texto completo de maneira eficiente e o expõe ao processo de re-indexação Oak de uma forma que é extremamente eficiente de consumir.

#### Quando a pré-extração de texto pode ser usada? {#when-can-text-pre-extraction-be-used}

Indexação novamente de um índice de lucene **existente** com extração binária ativada

* Indexando novamente o processamento de **todo** conteúdo candidato no repositório; quando os binários dos quais extrair o texto completo são numerosos ou complexos, uma carga computacional aumentada para executar a extração de texto completo é colocada no AEM. A pré-extração de texto move o &quot;trabalho computacional dispendioso&quot; da extração de texto em um processo isolado que acessa diretamente AEM Data Store, evitando a sobrecarga e a contenção de recursos na AEM.

Suporte à implantação de um índice de lucene **new** para AEM com extração binária ativada

* Quando um novo índice (com extração binária ativada) é implantado no AEM, o Oak indexa automaticamente todo o conteúdo candidato na próxima execução do índice de texto completo assíncrono. Pelas mesmas razões descritas na reindexação acima, isso pode resultar em carga excessiva sobre a AEM.

#### Quando a pré-extração de texto NÃO pode ser usada? {#when-can-text-pre-extraction-not-be-used}

A pré-extração de texto não pode ser usada para novo conteúdo adicionado ao repositório, nem é necessária.

O novo conteúdo é adicionado ao repositório será indexado de forma natural e incremental pelo processo de indexação assíncrona de texto completo (por padrão, a cada 5 segundos).

Em operação normal de AEM, por exemplo, fazer upload de Ativos por meio da interface do usuário da Web ou da assimilação programática de Ativos, AEM indexará automaticamente e incrementalmente o novo conteúdo binário. Como a quantidade de dados é incremental e relativamente pequena (aproximadamente a quantidade de dados que pode ser mantida no repositório em 5 segundos), AEM pode executar a extração de texto completo dos binários durante a indexação sem afetar o desempenho geral do sistema.

#### Pré-requisitos para usar a pré-extração de texto {#prerequisites-to-using-text-pre-extraction}

* Você reindexará um índice de lucene que executa extração binária de texto completo ou implantará um novo índice que fará binários de índice de texto completo do conteúdo existente
* O conteúdo (binários) a partir do qual extrair o texto deve estar no repositório
* Uma janela de manutenção para gerar o arquivo CSV E executar a reindexação final
* Versão do Oak: 1.0.18+, 1.2.3+
* [oak-run.](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)jarversion 1.7.4+
* Uma pasta/compartilhamento do sistema de arquivos para armazenar o texto extraído acessível da(s) instância(s) de indexação AEM

   * A configuração de OSGi pré-extração de texto exige um caminho do sistema de arquivos para os arquivos de texto extraídos, de modo que eles devem estar acessíveis diretamente da instância AEM (unidade local ou montagem de compartilhamento de arquivos)

#### Como executar pré-extração de texto {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***Os comandos oak-run.jar descritos abaixo são completamente enumerados em  [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>O diagrama acima e as etapas abaixo servem para explicar e complementar as etapas de pré-extração do texto técnico descritas na documentação do Apache Oak.

![Fluxo do processo de pré-extração de texto](assets/chlimage_1-139.png)

**Gerar lista de conteúdo para pré-extração**

*Execute a Etapa 1(a-b) durante uma janela de manutenção/período de baixo uso, à medida que o armazenamento de nós for percorrido durante essa operação, o que pode causar carga significativa no sistema.*

1 bis. Execute `oak-run.jar --generate` para criar uma lista de nós que terão seu texto pré-extraído.

1 ter. A lista de nós (1a) é armazenada no sistema de arquivos como um arquivo CSV

Observe que todo o Node Store é atravessado (conforme especificado pelos caminhos no comando oak-run) sempre que `--generate` é executado e um arquivo CSV **new** é criado. O arquivo CSV é **e não** reutilizado entre execuções discretas do processo de pré-extração de texto (Etapas 1 - 2).

**Pré-extrair texto para o sistema de arquivos**

*A Etapa 2(a-c) pode ser executada durante a operação normal de AEM se interage somente com o Data Store.*

2 bis. Execute `oak-run.jar --tika` para pré-extrair o texto dos nós binários enumerados no arquivo CSV gerado em (1b)

2 ter. O processo iniciado em (2a) acessa diretamente os nós binários definidos no CSV no Data Store e extrai o texto.

2-C.  O texto extraído é armazenado no sistema de arquivos em um formato ingerível pelo processo de reindexação Oak (3a)

O texto pré-extraído é identificado no CSV pela impressão digital binária. Se o arquivo binário for o mesmo, o mesmo texto pré-extraído poderá ser usado em instâncias AEM. Como a publicação de AEM é normalmente um subconjunto do autor de AEM, o texto pré-extraído do autor de AEM também pode ser usado para reindexar a publicação de AEM (supondo que a publicação de AEM tenha acesso do sistema de arquivos aos arquivos de texto extraídos).

O texto pré-extraído pode ser adicionado gradualmente ao longo do tempo. A pré-extração de texto ignorará a extração de binários extraídos anteriormente, portanto, a prática recomendada é manter o texto pré-extraído caso a reindexação deva ocorrer novamente no futuro (supondo que o conteúdo extraído não seja proibitivamente grande). Se estiver, avalie o zipamento do conteúdo no intervalo, já que o texto compacta bem).

**Indexar novamente índices Oak, obter texto completo de arquivos de Texto extraído**

*Execute a reindexação (Etapas 3a-b) durante um período de manutenção/baixo uso, à medida que o armazenamento de nós for percorrido durante essa operação, o que pode acarretar uma carga significativa no sistema.*

3-A. [A reindexação ](#how-to-re-index) dos índices Lucene é invocada em AEM

3 ter. A configuração do Apache Jackrabbit Oak DataStore PreExtractedTextProvider OSGi (configurada para apontar para o texto extraído por um caminho de sistema de arquivos) instrui o Oak a obter o texto de texto completo dos arquivos extraídos e evita que os dados armazenados no repositório sejam acessados e processados diretamente.

