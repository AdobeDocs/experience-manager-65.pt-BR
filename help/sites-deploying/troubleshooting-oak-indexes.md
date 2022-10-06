---
title: Solução de problemas de índices do Oak
seo-title: Troubleshooting Oak Indexes
description: Como detectar e corrigir a reindexação lenta.
seo-description: How to detect and fix slow re-indexing.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 1%

---

# Solução de problemas de índices do Oak{#troubleshooting-oak-indexes}

## Reindexação lenta  {#slow-re-indexing}

AEM processo interno de reindexação coleta dados do repositório e os armazena em índices Oak para oferecer suporte à consulta de conteúdo executante. Em circunstâncias excepcionais, o processo pode ficar lento ou mesmo travado. Esta página atua como um guia de solução de problemas para ajudar a identificar se a indexação está lenta, localizar a causa e resolver o problema.

É importante distinguir entre reindexação que leva um tempo inadequadamente longo e reindexação que leva um longo período porque indexa grandes quantidades de conteúdo. Por exemplo, o tempo necessário para indexar escalas de conteúdo com a quantidade de conteúdo, de modo que repositórios de produção grandes levarão mais tempo para reindexar do que repositórios de desenvolvimento pequenos.

Consulte a [Práticas recomendadas em consultas e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md) para obter mais informações sobre quando e como reindexar o conteúdo.

## Detecção inicial {#initial-detection}

A indexação lenta da detecção inicial requer a revisão da `IndexStats` MBeans JMX. Na instância de AEM afetada, faça o seguinte:

1. Abra o Console da Web e clique na guia JMX ou acesse https://&lt;host>:&lt;port>/system/console/jmx (por exemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Navegue até o `IndexStats` Feijão.
1. Abra o `IndexStats` MBeans para &quot; `async`&quot; e &quot; `fulltext-async`&quot;.

1. Para ambos os MBeans, verifique se a variável **Concluído** timestamp e **LastIndexTime** o carimbo de data e hora está a menos de 45 minutos da hora atual.

1. Para MBean, se o valor de tempo (**Concluído** ou **LastIndexedTime**) é maior que 45 minutos a partir do momento atual, então o trabalho de índice está falhando ou demorando muito. Isso faz com que os índices assíncronos sejam obsoletos.

## A indexação é pausada após um desligamento forçado {#indexing-is-paused-after-a-forced-shutdown}

Um desligamento forçado resulta em AEM suspensão da indexação assíncrona por até 30 minutos após a reinicialização e normalmente requer mais 15 minutos para concluir a primeira passagem de reindexação, por um total de aproximadamente 45 minutos (ligando de volta ao [Detecção inicial](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) período de 45 minutos). Caso suspeite que a indexação esteja pausada após um desligamento forçado:

1. Em primeiro lugar, determine se a instância de AEM foi encerrada de forma forçada (o processo de AEM foi violado com força, ou ocorreu uma falha de energia) e, em seguida, reiniciada.

   * [Registro de AEM](/help/sites-deploying/configure-logging.md) podem ser revistas para esse fim.

1. Se o desligamento forçado tiver ocorrido, após a reinicialização, o AEM suspende automaticamente a reindexação por até 30 minutos.
1. Aguarde aproximadamente 45 minutos para AEM retomar as operações normais de indexação assíncrona.

## Pool de threads sobrecarregado {#thread-pool-overloaded}

>[!NOTE]
>
>Para o AEM 6.1, verifique se [AEM 6.1 CFP 11](https://helpx.adobe.com/experience-manager/release-notes-aem-6-1-cumulative-fix-pack.html) está instalado.

Em circunstâncias excepcionais, o pool de threads usado para gerenciar a indexação assíncrona pode ficar sobrecarregado. Para isolar o processo de indexação, um conjunto de threads pode ser configurado para impedir que outros AEM trabalho interfiram com a capacidade do Oak de indexar o conteúdo em tempo hábil. Para fazer isso, você deve:

1. Defina um novo conjunto de encadeamentos isolado para que o Apache Sling Scheduler use para indexação assíncrona:

   * Na instância de AEM afetada, navegue até AEM console da Web OSGi>OSGi>Configuração>Apache Sling Scheduler ou acesse https://&lt;host>:&lt;port>/system/console/configMgr (por exemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * Adicione uma entrada ao campo &quot;Pools de Threads Permitidos&quot; com o valor de &quot;oak&quot;.
   * Clique em Salvar na parte inferior direita para salvar as alterações.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Verifique se o novo conjunto de encadeamentos do Apache Sling Scheduler está registrado e é exibido no console da Web Apache Sling Scheduler Status .

   * Navegue até AEM console da Web OSGi>Status>Sling Scheduler ou acesse https://&lt;host>:&lt;port>/system/console/status-slingscheduler (por exemplo, [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * Verifique se as seguintes entradas de pool existem:

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## A fila de observação está cheia {#observation-queue-is-full}

Se muitas alterações e compromissos forem feitas no repositório em um curto período, a indexação pode ser atrasada devido a uma fila de observação completa. Primeiro, determine se a fila de observação está cheia:

1. Vá para o Console da Web e clique na guia JMX ou vá para https://&lt;host>:&lt;port>/system/console/jmx (por exemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Abra o MBean de estatísticas do repositório do Oak e determine se existe algum `ObservationQueueMaxLength` for maior que 10.000.

   * Em operações normais, esse valor máximo sempre deve reduzir para zero (especialmente no `per second` (seção) para verificar se a variável `ObservationQueueMaxLength`As métricas de segundos da são 0.
   * Se os valores forem 10.000 ou mais e aumentarem continuamente, isso indica que pelo menos uma (possivelmente mais) fila não poderá ser processada tão rápido quanto novas alterações (commits) ocorrerem.
   * Cada fila de observação tem um limite (10.000 por padrão) e se a fila atingir esse limite, seu processamento será degradado.
   * Ao usar o MongoMK, à medida que os comprimentos da fila aumentam, o desempenho interno do cache do Oak diminui. Esta correlação pode ser vista em um aumento de `missRate` para `DocChildren` no `Consolidated Cache` estatísticas MBean.

1. Para evitar exceder os limites aceitáveis da fila de observação, recomenda-se:

   * Diminua a taxa constante de commits. Picos curtos em compromissos são aceitáveis, mas a taxa constante deve ser reduzida.
   * Aumente o tamanho da variável `DiffCache` conforme descrito em [Dicas para ajuste de desempenho > Ajuste de armazenamento do Mongo > Tamanho do cache do documento](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html#main-pars_text_3).

## Identificação e correção de um processo de reindexação travado {#identifying-and-remediating-a-stuck-re-indexing-process}

A reindexação pode ser considerada como &quot;completamente presa&quot; sob duas condições:

* A reindexação é muito lenta, até o ponto em que nenhum progresso significativo é relatado nos arquivos de log em relação ao número de nós atravessados.

   * Por exemplo, se não houver mensagens ao longo de uma hora, ou se o progresso for tão lento que levará uma semana ou mais para ser concluído.

* A reindexação fica presa em um loop infinito se exceções repetidas aparecerem nos arquivos de log (por exemplo, `OutOfMemoryException`) no thread de indexação. A repetição das mesmas exceções no log indica que o Oak tenta indexar a mesma coisa repetidamente, mas falha no mesmo problema.

Para identificar e corrigir um processo de reindexação travado, faça o seguinte:

1. Para identificar a causa da indexação paralisada, as seguintes informações devem ser coletadas:

   * Colete 5 minutos de despejo de thread, um despejo de thread a cada 2 segundos.
   * [Definir nível DEBUG e registros para os appenders](/help/sites-deploying/configure-logging.md).

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * Coletar dados do assíncrono `IndexStats` MBean:

      * Navegue até AEM console da Web OSGi>Principal>JMX>IndexStat>async

         ou vá para [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * Use [modo de console do oak-run.jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) para obter os detalhes do que existe no * `/:async`*.
   * Colete uma lista de pontos de verificação do repositório usando o `CheckpointManager` MBean:

      * AEM Console da Web OSGi>Principal>JMX>CheckpointManager>listCheckpoints()

         ou vá para [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. Depois de coletar todas as informações descritas na Etapa 1, reinicie o AEM.

   * Reiniciar AEM pode resolver o problema em caso de alta carga simultânea (estouro da fila de observação ou similar).
   * Se uma reinicialização não resolver o problema, abra um problema com [Atendimento ao cliente do Adobe](https://helpx.adobe.com/br/marketing-cloud/contact-support.html) e fornecer todas as informações coletadas na Etapa 1.

## Interromper com segurança a reindexação assíncrona {#safely-aborting-asynchronous-re-indexing}

A reindexação pode ser abortada com segurança (interrompida antes de ser concluída) por meio do `async, async-reindex`e f `ulltext-async` vias de indexação ( `IndexStats` Feijão). Para obter mais informações, consulte também a documentação do Apache Oak em [Como abortar a reindexação](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Além disso, ter em conta que:

* A reindexação dos Índices de Propriedades Lucene e Lucene pode ser abortada, pois são naturalmente assíncronas.
* A reindexação de índices de propriedades do Oak só pode ser abortada se a reindexação tiver sido iniciada por meio do `PropertyIndexAsyncReindexMBean`.

Para interromper a reindexação com segurança, siga estas etapas:

1. Identifique o MBean IndexStats que controla a faixa de reindexação que precisa ser interrompida.

   * Navegue até o IndexStats MBean apropriado por meio do console JMX, acessando AEM console da Web OSGi>Main>JMX ou https://&lt;host>:&lt;port>/system/console/jmx (por exemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * Abra o IndexStats MBean baseado na faixa de reindexação que você deseja parar ( `async`, `async-reindex`ou `fulltext-async`)

      * Para identificar a faixa apropriada e, portanto, a instância MBean IndexStats, verifique a propriedade &quot;async&quot; dos Índices Oak. A propriedade &quot;async&quot; conterá o nome da faixa: `async`, `async-reindex`ou `fulltext-async`.
      * A faixa também está disponível acessando AEM Gerenciador de Índice na coluna &quot;Assíncrono&quot;. Para acessar o Gerenciador de índice, navegue até Operations>Diagnosis>Index Manager.

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Chame o `abortAndPause()` no comando adequado `IndexStats` MBean.
1. Marque a definição do índice Oak apropriadamente para impedir a reindexação quando a faixa de indexação for retomada.

   * Ao reindexar um **existente** , defina a propriedade reindex como false

      * `/oak:index/someExistingIndex@reindex=false`
   * Ou senão, para um **novo** índice:

      * Defina a propriedade type como disabled

         * `/oak:index/someNewIndex@type=disabled`
      * ou remover a definição de índice totalmente

   Confirme as alterações no repositório ao concluir.

1. Finalmente, retome a indexação assíncrona na faixa de indexação abortada.

   * No `IndexStats` MBean que emitiu o `abortAndPause()` na Etapa 2, chame o `resume()`comando.

## Impedindo a reindexação lenta {#preventing-slow-re-indexing}

É melhor reindexar durante períodos silenciosos (por exemplo, não durante uma assimilação de conteúdo grande) e idealmente durante janelas de manutenção quando AEM carga é conhecida e controlada. Além disso, assegure-se de que a reindexação não ocorra durante outras atividades de manutenção.
