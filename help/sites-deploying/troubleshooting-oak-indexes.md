---
title: Solução de problemas de índices do Oak
description: Saiba como identificar se a indexação está lenta, encontrar a causa e resolver o problema.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---

# Solução de problemas de índices do Oak{#troubleshooting-oak-indexes}

## Reindexação lenta  {#slow-re-indexing}

O processo de reindexação interna do AEM coleta dados do repositório e os armazena em índices Oak para oferecer suporte à consulta eficiente do conteúdo. Em circunstâncias excepcionais, o processo pode ficar lento ou até travado. Esta página atua como um guia de solução de problemas para ajudar a identificar se a indexação está lenta, encontrar a causa e resolver o problema.

É importante distinguir entre a reindexação, que leva um tempo inadequadamente longo, e a reindexação, que leva um tempo longo, pois está indexando grandes quantidades de conteúdo. Por exemplo, o tempo necessário para indexar o conteúdo é dimensionado com a quantidade de conteúdo, portanto, repositórios de produção grandes demoram mais para reindexar do que repositórios de desenvolvimento pequenos.

Consulte as [Práticas recomendadas de consultas e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md) para obter mais informações sobre quando e como reindexar o conteúdo.

## Detecção inicial {#initial-detection}

A indexação lenta da detecção inicial requer a revisão dos `IndexStats` MBeans JMX. Na instância afetada do AEM, faça o seguinte:

1. Abra o Console da Web e clique na guia JMX ou vá para https://&lt;host>:&lt;port>/system/console/jmx (por exemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Navegue até os `IndexStats` Mbeans.
1. Abra os `IndexStats` MBeans para &quot; `async`&quot; e &quot; `fulltext-async`&quot;.

1. Para ambos os MBeans, verifique se o carimbo de data/hora **Concluído** e o carimbo de data/hora **LastIndexTime** estão a menos de 45 minutos da hora atual.

1. Para qualquer MBean, se o valor de tempo (**Concluído** ou **LastIndexedTime**) for maior que 45 minutos a partir da hora atual, o trabalho de índice está falhando ou demorando muito. Esse problema faz com que os índices assíncronos fiquem obsoletos.

## A indexação está pausada após um desligamento forçado {#indexing-is-paused-after-a-forced-shutdown}

Um desligamento forçado faz com que o AEM suspenda a indexação assíncrona por até 30 minutos após a reinicialização. E, normalmente, leva mais 15 minutos para concluir a primeira passagem de reindexação, para um total de cerca de 45 minutos (vinculando ao período de 45 minutos da [Detecção inicial](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection)). Se a indexação for pausada após um desligamento forçado:

1. Primeiro, determine se a instância do AEM foi desligada de maneira forçada (o processo AEM foi interrompido à força ou ocorreu uma falha de energia) e mais tarde reiniciada.

   * O [log de AEM](/help/sites-deploying/configure-logging.md) pode ser revisado para esta finalidade.

1. Se o desligamento forçado ocorrer, após a reinicialização, o AEM suspende automaticamente a reindexação por até 30 minutos.
1. Aguarde aproximadamente 45 minutos para que o AEM retome as operações normais de indexação assíncrona.

## Pool de threads sobrecarregado {#thread-pool-overloaded}

>[!NOTE]
>
>Para o AEM 6.1, verifique se o [AEM 6.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=pt-BR) está instalado.

Em circunstâncias excepcionais, o pool de threads usado para gerenciar a indexação assíncrona pode ficar sobrecarregado. Para isolar o processo de indexação, um pool de threads pode ser configurado para impedir que outro trabalho do AEM interfira na capacidade da Oak de indexar conteúdo em tempo hábil. Nesses casos, faça o seguinte:

1. Defina um novo pool de threads isolado para o Apache Sling Scheduler usar para indexação assíncrona:

   * Na instância de AEM afetada, navegue até AEM OSGi Web Console>OSGi>Configuration>Apache Sling Scheduler ou acesse https://&lt;host>:&lt;port>/system/console/configMgr (por exemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * Adicione uma entrada ao campo &quot;Pools de threads permitidos&quot; com o valor de &quot;oak&quot;.
   * Para salvar as alterações, clique em **Salvar** no canto inferior direito.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Verifique se o novo pool de threads do Apache Sling Scheduler está registrado e é exibido no console da Web Status do Apache Sling Scheduler.

   * Navegue até o console da Web AEM OSGi>Status>Sling Scheduler ou acesse https://&lt;host>:&lt;port>/system/console/status-slingscheduler (por exemplo, [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * Verifique se as seguintes entradas de pool existem:

      * ApacheSlingoak
      * ApacheSlingDefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## A fila de observação está cheia {#observation-queue-is-full}

Se muitas alterações e confirmações forem feitas no repositório em um curto período de tempo, a indexação poderá ser atrasada devido a uma fila de observação cheia. Primeiro, determine se a fila de observação está cheia:

1. Vá para o Console da Web e clique na guia JMX ou vá para https://&lt;host>:&lt;port>/system/console/jmx (por exemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Abra o MBean de Estatísticas do Repositório do Oak e determine se qualquer valor `ObservationQueueMaxLength` é maior que 10.000.

   * Em operações normais, esse valor máximo sempre deve ser reduzido a zero (especialmente na seção `per second`), portanto, verifique se as métricas de segundos de `ObservationQueueMaxLength` são 0.
   * Se os valores forem 10.000 ou mais e aumentarem constantemente, isso indicará que pelo menos uma (possivelmente mais) fila não poderá ser processada tão rápido quanto ocorrerem novas alterações (confirmações).
   * Cada fila de observação tem um limite (10.000 por padrão) e, se a fila atingir esse limite, seu processamento será degradado.
   * Ao usar o MongoMK, à medida que os comprimentos das filas aumentam, o desempenho do cache interno do Oak diminui. Esta correlação pode ser vista em um `missRate` aumentado para o cache `DocChildren` no MBean de estatísticas `Consolidated Cache`.

1. Para evitar exceder os limites aceitáveis da fila de observação, recomenda-se:

   * Diminua a taxa constante de confirmações. Pequenos picos nas confirmações são aceitáveis, mas a taxa constante deve ser reduzida.
   * Aumente o tamanho do `DiffCache` conforme descrito em [Dicas de ajuste de desempenho > Ajuste de Armazenamento Mongo > Tamanho do cache de documentos](/help/sites-deploying/configuring-performance.md).

## Identificação e correção de um processo de reindexação paralisado {#identifying-and-remediating-a-stuck-re-indexing-process}

A reindexação pode ser considerada &quot;completamente paralisada&quot; sob duas condições:

* A reindexação é lenta, a ponto de não ser relatado nenhum progresso significativo nos arquivos de log em relação ao número de nós percorridos.

   * Por exemplo, se não houver mensagens no período de uma hora ou se o progresso estiver tão lento que leve uma semana ou mais para ser concluído.

* A reindexação fica presa em um loop infinito se exceções repetidas aparecerem nos arquivos de log (por exemplo, `OutOfMemoryException`) no thread de indexação. A repetição de uma ou mais exceções idênticas no log indica que o Oak tenta indexar a mesma coisa repetidamente, mas falha no mesmo problema.

Para identificar e corrigir um processo de reindexação paralisado, faça o seguinte:

1. Para identificar a causa da indexação paralisada, as seguintes informações devem ser coletadas:

   * Colete 5 minutos de despejo de thread, um despejo de thread a cada 2 segundos.
   * [Definir nível DEBUG e logs para os anexadores](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*

   * Coletar dados do MBean assíncrono `IndexStats`:

      * Navegue até AEM OSGi Web Console>Main>JMX>IndexStat>async

        ou vá para [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)

   * Use o [modo de console do oak-run.jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) para coletar os detalhes do que existe no nó * `/:async`*.
   * Colete uma lista de pontos de verificação do repositório usando o MBean `CheckpointManager`:

      * AEM OSGi Web Console>Main>JMX>CheckpointManager>listCheckpoints()

        ou vá para [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)

1. Depois de coletar todas as informações descritas na Etapa 1, reinicie o AEM.

   * Reiniciar o AEM pode resolver o problema se houver alta carga simultânea (estouro da fila de observação ou algo semelhante).
   * Se uma reinicialização não resolver o problema, abra um problema no [Adobe Customer Care](https://experienceleague.adobe.com/pt-br?support-solution=General&support-tab=home#support) e forneça todas as informações coletadas na Etapa 1.

## Anular com segurança a reindexação assíncrona {#safely-aborting-asynchronous-re-indexing}

A reindexação pode ser anulada com segurança (interrompida antes de ser concluída) através das `async, async-reindex` e das `ulltext-async` faixas de indexação ( `IndexStats` Mbean). Para obter mais informações, consulte também a documentação do Apache Oak em [Como suspender a reindexação](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Além disso, considere o seguinte:

* A reindexação de índices de propriedades Lucene e Lucene pode ser anulada, pois eles são naturalmente assíncronos.
* A reindexação de Índices de Propriedades do Oak só poderá ser anulada se a reindexação tiver sido iniciada por meio de `PropertyIndexAsyncReindexMBean`.

Para interromper com segurança a reindexação, siga estas etapas:

1. Identifique o MBean IndexStats que controla a faixa de reindexação que deve ser interrompida.

   * Navegue até o MBean IndexStats apropriado pelo console JMX, acessando AEM OSGi Web Console>Main>JMX ou https://&lt;host>:&lt;port>/system/console/jmx (por exemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * Abra o MBean IndexStats com base na faixa de reindexação que você deseja parar ( `async`, `async-reindex` ou `fulltext-async`)

      * Para identificar a faixa apropriada e, portanto, a instância MBean IndexStats, verifique a propriedade &quot;async&quot; dos Índices Oak. A propriedade &quot;async&quot; contém o nome da faixa: `async`, `async-reindex` ou `fulltext-async`.
      * A faixa também está disponível ao acessar o AEM Index Manager na coluna &quot;Async&quot;. Para acessar o Gerenciador de índice, navegue até Operações>Diagnóstico>Gerenciador de índice.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Invoque o comando `abortAndPause()` no `IndexStats` MBean apropriado.
1. Marque a definição do índice Oak de maneira apropriada para evitar a retomada da reindexação quando a faixa de indexação for retomada.

   * Ao reindexar um índice **existente**, defina a propriedade reindex como false

      * `/oak:index/someExistingIndex@reindex=false`

   * Ou então, para um índice **novo**:

      * Defina a propriedade type como disabled

         * `/oak:index/someNewIndex@type=disabled`

      * ou remova a definição do índice totalmente

   Confirmar as alterações no repositório ao concluir.

1. Por fim, retome a indexação assíncrona na faixa de indexação anulada.

   * No MBean `IndexStats` que emitiu o comando `abortAndPause()` na Etapa 2, chame o comando `resume()`.

## Como evitar a reindexação lenta {#preventing-slow-re-indexing}

É melhor reindexar durante períodos de silêncio (por exemplo, não durante uma grande assimilação de conteúdo) e, idealmente, durante as janelas de manutenção quando a carga do AEM é conhecida e controlada. Além disso, certifique-se de que a reindexação não ocorra durante outras atividades de manutenção.
