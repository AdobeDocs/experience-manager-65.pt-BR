---
title: Práticas recomendadas para consultas e indexação
description: Este artigo fornece diretrizes sobre como otimizar seus índices e consultas.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '4613'
ht-degree: 7%

---

# Práticas recomendadas para consultas e indexação{#best-practices-for-queries-and-indexing}

Juntamente com a transição para o Oak no AEM 6, foram feitas algumas mudanças importantes na forma como as consultas e os índices são gerenciados. Em Jackrabbit 2, todo o conteúdo era indexado por padrão e podia ser consultado livremente. No Oak, os índices devem ser criados manualmente no `oak:index` nó. Uma consulta pode ser executada sem um índice, mas, para conjuntos de dados grandes, ela será executada lentamente ou até mesmo anulada.

Este artigo descreve quando criar índices e quando eles não são necessários, truques para evitar o uso de consultas quando eles não são necessários e dicas para otimizar seu desempenho com o máximo de eficiência possível.

Além disso, leia a [Documentação do Oak sobre gravação de consultas e índices](/help/sites-deploying/queries-and-indexing.md). Além de os índices serem um novo conceito no AEM 6, há diferenças sintáticas nas consultas do Oak que precisam ser consideradas ao migrar o código de uma instalação anterior do AEM.

## Quando utilizar consultas {#when-to-use-queries}

### Design de repositório e taxonomia {#repository-and-taxonomy-design}

Ao projetar a taxonomia de um repositório, vários fatores precisam ser considerados. Isso inclui controles de acesso, localização, componente e herança de propriedade da página, entre outros.

Ao projetar uma taxonomia que atenda a essas questões, também é importante considerar a flexibilidade do design de indexação. Nesse contexto, a flexibilidade é a capacidade de uma taxonomia que permite que o conteúdo seja acessado de forma previsível com base em seu caminho. Isso tornará o sistema mais eficiente e fácil de manter do que um que requer a execução de muitas consultas.

Além disso, ao projetar uma taxonomia, é importante considerar se a ordenação é importante. Nos casos em que a ordenação explícita não é obrigatória e muitos nós semelhantes são esperados, é preferível usar um tipo de nó não ordenado, como `sling:Folder` ou `oak:Unstructured`. Nos casos em que a ordenação é obrigatória, `nt:unstructured`, e `sling:OrderedFolder` são mais adequadas.

### Consultas em componentes {#queries-in-components}

Como as consultas podem ser uma das operações mais exigentes realizadas em um sistema AEM, é recomendável evitá-las em seus componentes. A execução de várias consultas cada vez que uma página é renderizada pode prejudicar o desempenho do sistema. Há duas estratégias que podem ser usadas para evitar a execução de consultas ao renderizar componentes: **nós de passagem** e **resultados de busca prévia**.

#### Nós de passagem {#traversing-nodes}

Se o repositório for projetado de forma que permita o conhecimento prévio da localização dos dados necessários, o código que recupera esses dados nos caminhos necessários poderá ser implantado sem a necessidade de executar consultas para encontrá-los.

Um exemplo disso seria a renderização de um conteúdo que se encaixe em uma determinada categoria. Uma abordagem seria organizar o conteúdo com uma propriedade de categoria que possa ser consultada para preencher um componente que mostre itens em uma categoria.

No entanto, uma melhor abordagem seria estruturar esse conteúdo em uma taxonomia por categoria para que ele possa ser recuperado manualmente.

Por exemplo, se o conteúdo for armazenado em uma taxonomia semelhante a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

A variável `/content/myUnstructuredContent/parentCategory/childCategory` O nó pode simplesmente ser recuperado e seus secundários podem ser analisados e usados para renderizar o componente.

Além disso, ao lidar com um conjunto de resultados pequeno ou homogêneo, pode ser mais rápido percorrer o repositório e coletar os nós necessários, em vez de criar uma consulta para retornar o mesmo conjunto de resultados. Como consideração geral, as consultas devem ser evitadas sempre que possível.

#### Resultados de busca prévia {#prefetching-results}

Às vezes, o conteúdo ou os requisitos do componente não permitirão o uso de nós de passagem como um método de recuperação dos dados necessários. Nesses casos, as consultas necessárias precisam ser executadas antes que o componente seja renderizado para garantir o desempenho ideal para o usuário final.

Se os resultados obrigatórios para o componente puderem ser calculados no momento da criação e não houver expectativa de que o conteúdo seja alterado, a consulta poderá ser executada quando o autor aplicar configurações na caixa de diálogo.

Se os dados ou o conteúdo forem alterados regularmente, a consulta poderá ser executada de acordo com uma programação ou por meio de um ouvinte para obter atualizações sobre os dados subjacentes. Em seguida, os resultados podem ser gravados em um local compartilhado no repositório. Qualquer componente que precise desses dados pode extrair os valores desse único nó, sem precisar executar uma consulta em tempo de execução.

## Otimização de consulta {#query-optimization}

Ao executar uma consulta que não esteja usando um índice, serão registrados avisos sobre o percurso do nó. Se esta for uma consulta que vai ser executada com frequência, crie um índice. Para determinar qual índice uma determinada consulta está usando, a variável [Ferramenta Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query) é recomendada. Para obter informações adicionais, o log de DEPURAÇÃO pode ser ativado para as APIs de pesquisa relevantes.

>[!NOTE]
>
>Após modificar uma definição de índice, o índice deve ser recriado (reindexado). Dependendo do tamanho do índice, isso pode levar algum tempo para ser concluído.

Ao executar consultas complexas, pode haver casos em que o detalhamento da consulta em várias consultas menores e a associação dos dados por meio de código após o fato ter maior desempenho. A recomendação para esses casos é comparar o desempenho das duas abordagens para determinar qual opção seria melhor para o caso de uso em questão.

O AEM permite escrever consultas de uma das três formas a seguir:

* Através do [APIs QueryBuilder](/help/sites-developing/querybuilder-api.md) (recomendado)
* Usar XPath (recomendado)
* Usando o SQL2

Embora todas as consultas sejam convertidas para o SQL2 antes de serem executadas, a sobrecarga da conversão de consultas é mínima e, portanto, a maior preocupação ao escolher um idioma de consulta será a legibilidade e o nível de conforto da equipe de desenvolvimento.

>[!NOTE]
>
>Ao usar o QueryBuilder, ele determina a contagem de resultados por padrão, que é mais lenta no Oak em comparação às versões anteriores do Jackrabbit. Para compensar isso, você pode usar o [parâmetro guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results).

### A Ferramenta Explicar Consulta {#the-explain-query-tool}

Como em qualquer linguagem de consulta, a primeira etapa para otimizar uma consulta é entender como ela será executada. Para habilitar esta atividade, você pode usar o [Ferramenta Explicar consulta](/help/sites-administering/operations-dashboard.md#explain-query) que faz parte do Painel de operações. Com essa ferramenta, um query pode ser conectado e explicado. Um aviso será exibido se a consulta causar problemas com um repositório grande e o tempo de execução e os índices que serão usados. A ferramenta também pode carregar uma lista de consultas lentas e populares que podem ser explicadas e otimizadas.

### Log de DEPURAÇÃO para consultas {#debug-logging-for-queries}

Para obter algumas informações adicionais sobre como o Oak está escolhendo qual índice usar e como o mecanismo de consulta está executando uma consulta, um **DEPURAR** a configuração de registro pode ser adicionada para os seguintes pacotes:

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Certifique-se de remover este agente de log quando terminar de depurar a consulta. Ela tende a produzir uma grande quantidade de atividade e pode eventualmente preencher seu disco com arquivos de log.

Para obter mais informações sobre como fazer isso, consulte a [Documentação de registro](/help/sites-deploying/configure-logging.md).

### Estatísticas de índice {#index-statistics}

A Lucene registra um bean JMX que fornecerá detalhes sobre o conteúdo indexado, incluindo o tamanho e o número de documentos presentes em cada um dos índices.

Você pode acessá-lo acessando o Console JMX em `https://server:port/system/console/jmx`

Depois de fazer logon no console JMX, procure **Estatísticas do índice Lucene** para encontrá-lo. Outras estatísticas de índice podem ser encontradas no **IndexStats** MBean.

Para estatísticas de consulta, verifique o MBean chamado **Estatísticas de consulta do Oak**.

Se você quiser pesquisar seus índices usando uma ferramenta como [Luke](https://code.google.com/archive/p/luke/), você deve usar o console do Oak para despejar o índice do `NodeStore` para um diretório do sistema de arquivos. Para obter instruções sobre como fazer isso, leia o [Documentação do Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

Você também pode extrair os índices no seu sistema no formato JSON. Para fazer isso, é necessário acessar `https://server:port/oak:index.tidy.-1.json`

### Limites de consulta {#query-limits}

**Durante o desenvolvimento**

Definir limites baixos para `oak.queryLimitInMemory` (por exemplo, 10000) e Oak. `queryLimitReads` (por exemplo, 5000) e otimize a consulta cara ao acessar um UnsupportedOperationException dizendo &quot;A consulta lê mais de x nós...&quot;

Isso ajuda a evitar consultas que consomem muitos recursos (ou seja, sem o suporte de qualquer índice ou com menos índice de cobertura). Por exemplo, uma consulta que lê 1 milhão de nós resultaria em maior I/O e teria um impacto negativo no desempenho geral do aplicativo. Qualquer query que falhar devido aos limites acima deve ser analisada e otimizada.

#### **Pós-implantação** {#post-deployment}

* Monitore os logs de consultas que acionam travessia de nó grande ou consumo de memória de heap grande : &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Otimizar a consulta para reduzir o número de nós percorridos

* Monitore os logs para consultas que acionam grande consumo de memória de heap:

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Otimizar o query para reduzir o consumo de memória da pilha

Para versões do AEM 6.0 - 6.2, é possível ajustar o limite para passagem de nó por meio de parâmetros JVM no script de inicialização do AEM para evitar que grandes consultas sobrecarreguem o ambiente.

Os valores recomendados são:

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

No AEM 6.3, os dois parâmetros acima são pré-configurados e podem ser mantidos por meio do OSGi QueryEngineSettings.

Mais informações disponíveis em : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Dicas para Criar Índices Eficientes {#tips-for-creating-efficient-indexes}

### Devo criar um índice? {#should-i-create-an-index}

A primeira pergunta a ser feita ao criar ou otimizar índices é se eles são necessários para uma determinada situação. Se você executar o query em questão apenas uma vez ou apenas ocasionalmente e fora do horário de pico do sistema por meio de um processo em lote, talvez seja melhor não criar um índice.

Após a criação de um índice, sempre que os dados indexados forem atualizados, o índice também deverá ser atualizado. Como isso traz implicações de desempenho para o sistema, os índices só devem ser criados quando forem necessários.

Além disso, os índices só serão úteis se os dados contidos no índice forem exclusivos o suficiente para garantir isso. Considere um índice em um livro e os tópicos que ele aborda. Ao indexar um conjunto de tópicos em um texto, geralmente haverá centenas ou milhares de entradas, o que permite saltar rapidamente para um subconjunto de páginas para encontrar rapidamente as informações que você está procurando. Se esse índice tivesse apenas duas ou três entradas, cada uma apontando para várias centenas de páginas, o índice não seria útil. Esse mesmo conceito se aplica aos índices de banco de dados. Se houver apenas alguns valores únicos, o índice não será útil. Dito isso, um índice também pode se tornar grande demais para ser útil. Para analisar as estatísticas de índice, consulte [Estatísticas de índice](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) acima.

### Índices Lucene ou Propriedade? {#lucene-or-property-indexes}

Os índices Lucene foram introduzidos no Oak 1.0.9 e oferecem algumas otimizações poderosas sobre os índices de propriedade que foram introduzidos no lançamento inicial do AEM 6. Ao decidir se usará índices Lucene ou índices de propriedade, considere o seguinte:

* Os índices Lucene oferecem muito mais recursos do que os índices de propriedade. Por exemplo, um índice de propriedade só pode indexar uma única propriedade, enquanto um índice Lucene pode incluir muitos. Para obter mais informações sobre todos os recursos disponíveis nos índices Lucene, consulte o [documentação](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Os índices Lucene são assíncronos. Embora isso ofereça um aumento de desempenho considerável, também pode induzir um atraso entre o momento em que os dados são gravados no repositório e o momento em que o índice é atualizado. Se for vital que as consultas retornem resultados 100% precisos, será necessário um índice de propriedade.
* Por serem assíncronos, os índices Lucene não podem impor restrições de exclusividade. Se isso for necessário, um índice de propriedade precisará ser implementado.

Em geral, é recomendável usar índices Lucene, a menos que haja uma necessidade urgente de usar índices de propriedade para que você possa obter os benefícios de maior desempenho e flexibilidade.

### Indexação Solr {#solr-indexing}

O AEM também oferece suporte à indexação Solr por padrão. Ele é usado para oferecer suporte à pesquisa de texto completo, mas também pode ser usado para qualquer tipo de consulta JCR. O Solr deve ser considerado quando as instâncias AEM não têm a capacidade de CPU para lidar com o número de consultas necessárias em implantações intensivas de pesquisa, como sites orientados por pesquisa com um alto número de usuários simultâneos. Como alternativa, o Solr pode ser implementado em uma abordagem baseada em crawler para usar alguns dos recursos mais avançados da plataforma.

Os índices Solr podem ser configurados para execução incorporada no servidor AEM para ambientes de desenvolvimento ou podem ser descarregados em uma instância remota para melhorar a escalabilidade de pesquisa nos ambientes de produção e preparo. Embora a descarga de pesquisa melhore a escalabilidade, ela introduz latência e, por causa disso, não é recomendada, a menos que seja necessária. Para obter mais informações sobre como configurar a integração Solr e como criar índices Solr, consulte o [Documentação de consultas e indexação do Oak](/help/sites-deploying/queries-and-indexing.md#the-solr-index).

>[!NOTE]
>
>A adoção da abordagem de pesquisa integrada do Solr permitiria o descarregamento da indexação para um servidor Solr. Se os recursos mais avançados do servidor Solr forem usados por meio de uma abordagem baseada em crawler, será necessário um trabalho de configuração adicional.

A desvantagem de adotar essa abordagem é que, embora por padrão, as consultas de AEM respeitem as ACLs e, portanto, ocultem resultados aos quais um usuário não tem acesso, externalizar a pesquisa para um servidor Solr não oferecerá suporte a esse recurso. Se a pesquisa for externalizada dessa maneira, é necessário ter cuidado extra para garantir que os usuários não tenham resultados que não deveriam ver.

Os possíveis casos de uso em que essa abordagem pode ser adequada são aqueles em que os dados de pesquisa de várias fontes podem precisar ser agregados. Por exemplo, você pode ter um site sendo hospedado no AEM e um segundo site sendo hospedado em uma plataforma de terceiros. O Solr pode ser configurado para rastrear o conteúdo de ambos os sites e armazená-los em um índice agregado. Isso permitiria pesquisas entre sites.

### Considerações sobre design {#design-considerations}

A documentação do Oak para índices Lucene lista várias considerações a serem feitas ao criar índices:

* Se a consulta usar restrições de caminho diferentes, use `evaluatePathRestrictions`. Isso permite que a consulta retorne o subconjunto de resultados no caminho especificado e, em seguida, filtre-os com base na consulta. Caso contrário, a consulta procurará todos os resultados que correspondam aos parâmetros de consulta no repositório e os filtrará com base no caminho.
* Se a consulta usar classificação, tenha uma definição de propriedade explícita para a propriedade classificada e defina `ordered` para `true` para ele. Isso permite que os resultados sejam ordenados como tal no índice e salve em operações de classificação dispendiosas no tempo de execução da consulta.

* Coloque apenas o que é necessário no índice. Adicionar recursos ou propriedades desnecessários faz com que o índice aumente e diminua o desempenho.
* Em um índice de propriedade, ter um nome de propriedade exclusivo ajudaria a reduzir o tamanho em um índice, mas para índices Lucene, o uso de `nodeTypes` e `mixins` para obter índices coesos. Consulta de um específico `nodeType` ou `mixin` terá melhor desempenho do que consultar `nt:base`. Ao usar essa abordagem, defina `indexRules` para o `nodeTypes` em questão.

* Se as consultas estiverem sendo executadas somente em determinados caminhos, crie esses índices nesses caminhos. Os índices não precisam estar localizados na raiz do repositório.
* É recomendável usar um único índice quando todas as propriedades que estão sendo indexadas estão relacionadas para permitir que Lucene avalie quantas restrições de propriedade forem possíveis nativamente. Além disso, uma consulta usará apenas um índice, mesmo ao executar uma associação.

### CopyOnRead {#copyonread}

Nos casos em que a `NodeStore` é armazenado remotamente, uma opção chamada `CopyOnRead` pode ser ativado. A opção faz com que o índice remoto seja gravado no sistema de arquivos local quando ele é lido. Isso pode ajudar a melhorar o desempenho de consultas que geralmente são executadas nesses índices remotos.

Isso pode ser configurado no console OSGi na **LuceneIndexProvider** e está habilitado por padrão a partir do Oak 1.0.13.

### Remoção de Índices {#removing-indexes}

Ao remover um índice, é sempre recomendável desativar temporariamente o índice definindo o `type` propriedade para `disabled` e realize testes para garantir que seu aplicativo funcione corretamente antes de realmente excluí-lo. Um índice não é atualizado enquanto está desativado, portanto, talvez ele não tenha o conteúdo correto se estiver reativado e precise ser reindexado.

Após remover um índice de propriedade em uma instância TarMK, a compactação deve ser executada para recuperar qualquer espaço em disco que estava em uso. Para índices Lucene, o conteúdo real do índice fica no BlobStore, portanto, uma coleta de lixo do armazenamento de dados seria necessária.

Ao remover um índice em uma instância do MongoDB, o custo da exclusão é proporcional ao número de nós no índice. Como a exclusão de um índice grande pode causar problemas, a abordagem recomendada é desativar o índice e excluí-lo somente durante uma janela de manutenção, usando uma ferramenta como **oak-mongo.js**. Observe que essa abordagem não deve ser empregada para conteúdo de nó regular, pois pode introduzir inconsistências de dados.

>[!NOTE]
>
>Para obter mais informações sobre oak-mongo.js, consulte o [Seção Ferramentas de Linha de Comando](https://jackrabbit.apache.org/oak/docs/command_line.html) da documentação do Oak.

### A Folha de características de consulta JCR {#jcrquerycheatsheet}

Para auxiliar na criação de consultas JCR e definições de índice eficientes, a [Folha de características de consulta JCR](assets/JCR_query_cheatsheet-v1.1.pdf) está disponível para download e uso como referência durante o desenvolvimento. Ela contém exemplos de consulta para o QueryBuilder, XPath e SQL-2, e abrange vários cenários que se comportam de maneira diferente em termos de desempenho de consulta. Ela também fornece recomendações sobre como criar ou personalizar índices do Oak. O conteúdo desta Folha de características se aplica ao AEM 6.5 e ao AEM as a Cloud Service.

## Reindexação {#re-indexing}

Esta seção descreve as **somente** motivos aceitáveis para reindexar índices Oak.

Fora dos motivos descritos abaixo, iniciar reindexações de índices Oak faz **não** alterar o comportamento ou resolver problemas e aumentar desnecessariamente as cargas no AEM.

A reindexação de índices Oak deve ser evitada, a menos que seja feita por uma razão nas tabelas abaixo.

>[!NOTE]
>
>Antes de consultar as tabelas abaixo para determinar se a reindexação é útil, **sempre** verifique:
>
>* a consulta está correta
>* a consulta é resolvida para o índice esperado (usando [Explicar consulta](/help/sites-administering/operations-dashboard.md#diagnosis-tools))
>* o processo de indexação foi concluído
>

### Alterações na configuração do índice Oak {#oak-index-configuration-changes}

As únicas condições aceitáveis de não-erro para reindexar índices Oak são se a configuração de um índice Oak tiver sido alterada.

*A reindexação deve ser sempre abordada com consideração adequada sobre seu impacto no desempenho geral do AEM e realizada durante períodos de baixa atividade ou janelas de manutenção.*

Veja a seguir os detalhes de possíveis problemas, juntamente com as resoluções:

* [Alteração na definição do índice de propriedade](#property-index-definition-change)
* [Alteração na definição do índice Lucene](#lucene-index-definition-change)

#### Alteração na definição do índice de propriedade {#property-index-definition-change}

* Aplica-se a/se:

   * Todas as versões do Oak
   * Somente [índices de propriedade](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* Sintomas:

   * Nós existentes antes da atualização da definição do índice de propriedade ausentes nos resultados

* Como verificar:

   * Determine se os nós ausentes foram criados/modificados antes da implantação da definição de índice atualizada.
   * Verifique se `jcr:created` ou `jcr:lastModified` propriedades de qualquer nó ausente em relação ao tempo modificado do índice

* Como resolver:

   * [Reindexar](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) o índice lucene
   * Como alternativa, toque (execute uma operação de gravação benigna) nos nós ausentes

      * Requer toques manuais ou código personalizado
      * Requer que o conjunto de nós ausentes seja conhecido
      * Exige a alteração de qualquer propriedade no nó

#### Alteração na definição do índice Lucene {#lucene-index-definition-change}

* Aplica-se a/se:

   * Todas as versões do Oak
   * Somente [índices Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomas:

   * O índice Lucene não contém os resultados esperados
   * Os resultados da consulta não refletem o comportamento esperado da definição do índice
   * O plano de consulta não relata a saída esperada com base na definição do índice

* Como verificar:

   * Verifique se a definição do índice foi alterada usando o Mbean JMX (LuceneIndex) de estatísticas do Índice Lucene, método `diffStoredIndexDefinition`.

* Como resolver:

   * Versões do Oak anteriores à 1.6:

      * [Reindexar](#how-to-re-index) o índice lucene

   * Oak versões 1.6+

      * Se o conteúdo existente não for afetado pelas alterações, apenas uma atualização será necessária

         * [Atualizar](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) o índice lucene definindo [oak:queryIndexDefinition]@refresh=true

      * Senão, [reindexar](#how-to-re-index) o índice lucene

         * Observação: o estado do índice da última reindexação válida (ou indexação inicial) será usado até que uma nova reindexação seja acionada

### Situações de erro e excepcionais {#erring-and-exceptional-situations}

A tabela a seguir descreve os únicos erros aceitáveis e as situações excepcionais em que a reindexação de índices do Oak resolve o problema.

Se houver um problema no AEM que não corresponda aos critérios descritos abaixo, **não** reindexe os índices, pois isso não resolverá o problema.

Veja a seguir os detalhes de possíveis problemas, juntamente com as resoluções:

* [O binário do índice Lucene está ausente](#lucene-index-binary-is-missing)
* [O binário do índice Lucene está corrompido](#lucene-index-binary-is-corrupt)

#### O binário do índice Lucene está ausente {#lucene-index-binary-is-missing}

* Aplica-se a/se:

   * Todas as versões do Oak
   * Somente [índices Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomas:

   * O índice Lucene não contém os resultados esperados

* Como verificar:

   * O arquivo de log de erros contém uma exceção informando que um binário do índice Lucene está ausente

* Como resolver:

   * Executar uma verificação de repositório de passagem; por exemplo:

     [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

     percorrer o repositório determina se outros binários (além dos arquivos do lucene) estão ausentes

   * Se binários diferentes dos índices Lucene estiverem ausentes, restaurar do backup
   * Caso contrário, [reindexar](#how-to-re-index) *all* índices Lucene
   * Nota:

     Essa condição indica um armazenamento de dados configurado incorretamente que pode resultar na ausência DE QUALQUER binário (por exemplo, binários de ativos).

     Nesse caso, restaure para a última versão válida do repositório para recuperar todos os binários ausentes.

#### O binário do índice Lucene está corrompido {#lucene-index-binary-is-corrupt}

* Aplica-se a/se:

   * Todas as versões do Oak
   * Somente [índices Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Sintomas:

   * O índice Lucene não contém os resultados esperados

* Como verificar:

   * A variável `AsyncIndexUpdate` (a cada cinco segundos) falhará com uma exceção no error.log:

     `...a Lucene index file is corrupt...`

* Como resolver:

   * Remover a cópia local do índice Lucene

      1. Parar AEM
      1. Excluir a cópia local do índice Lucene em `crx-quickstart/repository/index`
      1. Reiniciar o AEM

   * Se isso não resolver o problema e a variável `AsyncIndexUpdate` as exceções persistem, então:

      1. [Reindexar](#how-to-re-index) o índice de erros
      1. Também arquive um [Suporte para Adobe](https://helpx.adobe.com/support.html) tíquete

### Como reindexar {#how-to-re-index}

>[!NOTE]
>
>No AEM 6.5, [oak-run.jar é o ÚNICO método compatível](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) para reindexação em repositórios MongoMK ou RDBMK.

#### Reindexação de índices de propriedade {#re-indexing-property-indexes}

* Uso [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) para reindexar o índice de propriedade
* Definir a propriedade async-reindex como verdadeira no índice de propriedade

   * `[oak:queryIndexDefinition]@reindex-async=true`

* Reindexe o índice de propriedade de forma assíncrona usando o Console da Web por meio da **PropertyIndexAsyncReindex** MBean;

  por exemplo,

  [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Reindexação de índices de propriedade do Lucene {#re-indexing-lucene-property-indexes}

* Uso [oak-run.jar para reindexar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) o índice de propriedade Lucene.
* Defina a propriedade async-reindex como true no índice de propriedade lucene

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>A seção anterior resume e enquadra a orientação de reindexação do Oak do [Documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) no contexto do AEM.

### Pré-extração de texto de binários {#text-pre-extraction-of-binaries}

A pré-extração de texto é o processo de extrair e processar texto de binários, diretamente do Armazenamento de dados por meio de um processo isolado e expor diretamente o texto extraído a reindexações subsequentes de índices Oak.

* A pré-extração de texto Oak é recomendada para reindexação de índices Lucene em repositórios com grandes volumes de arquivos (binários) que contenham texto extraível (por exemplo, PDF, documentos do Word, PPTs, TXT e assim por diante) que se qualificam para pesquisa de texto completo por meio de índices Oak implantados; por exemplo, `/oak:index/damAssetLucene`.
* A pré-extração de texto beneficia apenas a reindexação/indexação de índices Lucene e NÃO índices de propriedade Oak, já que os índices de propriedade não extraem texto de binários.
* A pré-extração de texto tem um alto impacto positivo quando a reindexação de texto completo de binários com muitos textos (PDF, Doc, TXT e assim por diante), enquanto um repositório de imagens não desfrutará da mesma eficiência, já que as imagens não contêm texto extraível.
* A pré-extração de texto executa a extração de texto completo relacionado à pesquisa de maneira extra eficiente e o expõe ao processo de reindexação/indexação do Oak de forma extra eficiente para o consumo.

#### Quando a pré-extração de texto PODE ser usada? {#when-can-text-pre-extraction-be-used}

Reindexação de um **existente** índice lucene com extração binária ativada

* Reindexação em processamento **all** conteúdo candidato no repositório; quando os binários dos quais extrair o texto completo são numerosos ou complexos, um aumento na carga computacional para realizar a extração de texto completo é colocado no AEM. A pré-extração de texto move o &quot;trabalho computacional dispendioso&quot; da extração de texto para um processo isolado que acessa diretamente o AEM Data Store, evitando sobrecarga e contenção de recursos no AEM.

O apoio à implantação de um **novo** índice de lucene para AEM com extração binária ativada

* Quando um novo índice (com extração binária ativada) é implantado no AEM, o Oak indexa automaticamente todo o conteúdo candidato na próxima execução assíncrona do índice de texto completo. Pelos mesmos motivos descritos na reindexação acima, isso pode resultar em carga indevida no AEM.

#### Quando o texto pré-extração NÃO pode ser usado? {#when-can-text-pre-extraction-not-be-used}

A pré-extração de texto não pode ser usada para novo conteúdo adicionado ao repositório, nem é necessária.

O novo conteúdo adicionado ao repositório será indexado natural e incrementalmente pelo processo assíncrono de indexação de texto completo (por padrão, a cada 5 segundos).

Em operação normal do AEM, por exemplo, fazer upload de ativos por meio da interface da Web ou assimilação programática de ativos, o AEM indexará automática e incrementalmente o novo conteúdo binário em texto completo. Como a quantidade de dados é incremental e relativamente pequena (aproximadamente a quantidade de dados que pode ser mantida no repositório em 5 segundos), o AEM pode realizar a extração de texto completo dos binários durante a indexação sem afetar o desempenho geral do sistema.

#### Pré-requisitos para usar a pré-extração de texto {#prerequisites-to-using-text-pre-extraction}

* Você reindexará um índice Lucene que executa extração binária de texto completo ou implantará um novo índice que irá indexar binários de texto completo de conteúdo existente
* O conteúdo (binários) do qual o texto será pré-extraído deve estar no repositório
* Uma janela de manutenção para gerar o arquivo CSV E executar a reindexação final
* Versão do Oak: 1.0.18+, 1.2.3+
* [oak-run.jar](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)versão 1.7.4+
* Uma pasta/compartilhamento do sistema de arquivos para armazenar o texto extraído acessível das instâncias de indexação do AEM

   * A configuração OSGi de pré-extração de texto requer um caminho de sistema de arquivos para os arquivos de texto extraídos, de modo que eles devem ser acessíveis diretamente da instância AEM (unidade local ou montagem de compartilhamento de arquivos)

#### Como executar a pré-extração de texto {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***Os comandos oak-run.jar descritos abaixo são totalmente enumerados em [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>O diagrama acima e as etapas abaixo servem para explicar e complementar as etapas de pré-extração do texto técnico descritas na documentação do Apache Oak.

![Fluxo do processo de pré-extração de texto](assets/chlimage_1-139.png)

**Gerar lista de conteúdo para pré-extrair**

*Execute a Etapa 1(a-b) durante uma janela de manutenção/período de pouco uso, pois o Armazenamento de nós é percorrido durante essa operação, o que pode incorrer em carga significativa no sistema.*

1a. Executar `oak-run.jar --generate` para criar uma lista de nós que terão o texto pré-extraído.

1b. A lista de nós (1a) é armazenada no sistema de arquivos como um arquivo CSV

Todo o armazenamento de nós é percorrido (conforme especificado pelos caminhos no comando oak-run) todas as vezes `--generate` é executado e uma **novo** Arquivo CSV criado. O arquivo CSV é **não** reutilizado entre execuções discretas do processo de pré-extração de texto (Etapas 1 - 2).

**Pré-extrair texto para o sistema de arquivos**

*A etapa 2(a-c) pode ser executada durante a operação normal do AEM se ele interagir somente com o Armazenamento de dados.*

2a. Executar `oak-run.jar --tika` para pré-extrair o texto para os nós binários enumerados no arquivo CSV gerado em (1b)

2b. O processo iniciado no (2a) acessa os nós binários definidos no CSV no Armazenamento de dados diretamente e extrai o texto.

2-C. O texto extraído é armazenado no sistema de arquivos em um formato assimilável pelo processo de reindexação do Oak (3a)

O texto pré-extraído é identificado no CSV pela impressão digital binária. Se o arquivo binário for o mesmo, o mesmo texto pré-extraído poderá ser usado em instâncias AEM. Como a Publicação do AEM geralmente é um subconjunto do Autor do AEM, o texto pré-extraído do Autor do AEM também pode ser usado para reindexar a Publicação do AEM (supondo que a Publicação do AEM tenha acesso ao sistema de arquivos para os arquivos de texto extraídos).

O texto pré-extraído pode ser adicionado de forma incremental ao ao longo do tempo. A pré-extração de texto ignorará a extração de binários extraídos anteriormente, portanto, é prática recomendada manter o texto pré-extraído para o caso de a reindexação ocorrer novamente no futuro (supondo que o conteúdo extraído não seja muito grande. Se for, avalie o compactação do conteúdo nesse ínterim, já que o texto é bem compactado).

**Reindexar índices Oak, obtendo texto completo de arquivos de texto extraído**

*Execute a reindexação (Etapas 3a-b) durante um período de manutenção/baixo uso, pois o Armazenamento de nós é percorrido durante essa operação, o que pode incorrer em carga significativa no sistema.*

3a. [Reindexar](#how-to-re-index) de índices Lucene é invocado no AEM.

3b. A configuração OSGi Apache Jackrabbit Oak DataStore PreExtractingTextProvider (configurada para apontar para o texto extraído por meio de um caminho de sistema de arquivos) instrui o Oak para o texto completo de origem dos arquivos extraídos, e evita atingir diretamente e processar os dados armazenados no repositório.
