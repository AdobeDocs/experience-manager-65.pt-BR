---
title: Solução de problemas de índices Oak
seo-title: Solução de problemas de índices Oak
description: Como detectar e corrigir a reindexação lenta.
seo-description: Como detectar e corrigir a reindexação lenta.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Solução de problemas de índices Oak{#troubleshooting-oak-indexes}

## Reindexação lenta {#slow-re-indexing}

O processo interno de reindexação do AEM coleta dados do repositório e os armazena em índices Oak para oferecer suporte à consulta de conteúdo do executor. Em circunstâncias excepcionais, o processo pode tornar-se lento ou mesmo emperrado. Esta página atua como um guia de solução de problemas para ajudar a identificar se a indexação está lenta, localizar a causa e resolver o problema.

É importante distinguir entre reindexação que leva um tempo inadequadamente longo, e reindexação que leva um longo tempo porque indexa grandes quantidades de conteúdo. Por exemplo, o tempo necessário para indexar as escalas de conteúdo com a quantidade de conteúdo, de modo que os repositórios de produção grandes levarão mais tempo para reindexar do que os pequenos repositórios de desenvolvimento.

Consulte as Práticas [recomendadas para consultas e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md) para obter informações adicionais sobre quando e como indexar novamente o conteúdo.

## Detecção inicial {#initial-detection}

A indexação lenta da detecção inicial requer a revisão dos MBeans `IndexStats` JMX. Na instância do AEM afetada, faça o seguinte:

1. Abra o Console da Web e clique na guia JMX ou vá para https://&lt;host>:&lt;porta>/system/console/jmx (por exemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)).
1. Navegue até o `IndexStats` Mbeans.
1. Abra os `IndexStats` MBeans para &quot; `async`&quot; e &quot; `fulltext-async`&quot;.

1. Para ambos os MBeans, verifique se o carimbo de data e hora **Done** e o carimbo de data e hora **LastIndexTime** estão a menos de 45 minutos do tempo atual.

1. Para MBean, se o valor de tempo (**Done** ou **LastIndexedTime**) for maior que 45 minutos do tempo atual, o trabalho de índice falhará ou demorará muito. Isso faz com que os índices assíncronos sejam obsoletos.

## A indexação é pausada após um encerramento forçado {#indexing-is-paused-after-a-forced-shutdown}

Um desligamento forçado resulta na suspensão assíncrona da indexação do AEM por até 30 minutos após a reinicialização, e geralmente requer mais 15 minutos para concluir a primeira reindexação de aprovação, por um total de aproximadamente 45 minutos (retornando ao período de tempo de Detecção [](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) inicial de 45 minutos). Caso suspeite que a indexação esteja pausada após um encerramento forçado:

1. Primeiro, determine se a instância do AEM foi desligada de maneira forçada (o processo do AEM foi fortalecida ou ocorreu uma falha de energia) e, subsequentemente, reiniciado.

   * [O registro em log](/help/sites-deploying/configure-logging.md) do AEM pode ser revisado para esse fim.

1. Se o encerramento forçado tiver ocorrido, após a reinicialização, o AEM suspende automaticamente a reindexação por até 30 minutos.
1. Aguarde aproximadamente 45 minutos para que o AEM retome as operações normais de indexação assíncrona.

## Pool de threads sobrecarregado {#thread-pool-overloaded}

>[!NOTE]
>
>Para o AEM 6.1, verifique se o [AEM 6.1 CFP 11](https://helpx.adobe.com/experience-manager/release-notes-aem-6-1-cumulative-fix-pack.html) está instalado.

Em circunstâncias excepcionais, o pool de threads usado para gerenciar a indexação assícrona pode ficar sobrecarregado. Para isolar o processo de indexação, um pool de threads pode ser configurado para impedir que outros trabalhos do AEM interfiram na capacidade do Oak de indexar conteúdo em tempo hábil. Para fazer isso, você deve:

1. Defina um novo pool de threads isolado para que o Apache Sling Scheduler use para indexação assíncrona:

   * Na instância AEM afetada, navegue até AEM OSGi Web Console>OSGi>Configuração>Apache Sling Scheduler ou vá para https://&lt;host>:&lt;porta>/system/console/configMgr (por exemplo, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr))
   * Adicione uma entrada ao campo &quot;Pools de threads permitidos&quot; com o valor de &quot;carvalho&quot;.
   * Clique em Salvar na parte inferior direita para salvar as alterações.
   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Verifique se o novo pool de threads do Apache Sling Scheduler está registrado e é exibido no console da Web Apache Sling Scheduler Status.

   * Navegue até o console Web do AEM OSGi>Status>Sling Scheduler ou vá para https://&lt;host>:&lt;porta>/system/console/status-slingScheduler (por exemplo, [http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler))
   * Verifique se as seguintes entradas de pool existem:

      * ApacheSlingoak
      * ApacheSlingdefault
   ![chlimage_1-120](assets/chlimage_1-120.png)

## A fila de observação está cheia {#observation-queue-is-full}

Se forem efetuadas demasiadas alterações e compromissos no repositório num curto espaço de tempo, a indexação pode ser atrasada devido a uma fila de observação completa. Primeiro, determinar se a fila de observação está cheia:

1. Vá para o Console da Web e clique na guia JMX ou vá para https://&lt;host>:&lt;porta>/system/console/jmx (por exemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
1. Abra o MBean de estatísticas do repositório Oak e determine se qualquer `ObservationQueueMaxLength` valor é maior que 10.000.

   * Em operações normais, esse valor máximo sempre deve ser reduzido para zero (especialmente na `per second` seção) para verificar se as métricas de segundos `ObservationQueueMaxLength`do são 0.
   * Se os valores forem 10.000 ou mais e aumentarem continuamente, isso indica que pelo menos uma (possivelmente mais) filas não pode ser processada tão rápido quanto novas alterações (confirmações) ocorrerem.
   * Cada fila de observação tem um limite (10.000 por padrão) e se a fila atingir esse limite, seu processamento diminui.
   * Ao usar MongoMK, à medida que os comprimentos da fila crescem, o desempenho interno do cache Oak diminui. Essa correlação pode ser vista em um aumento `missRate` para o `DocChildren` cache no MBean de `Consolidated Cache` estatísticas.

1. Para evitar exceder os limites aceitáveis da fila de observação, recomenda-se:

   * Diminua a taxa constante de autorizações. Picos curtos de compromissos são aceitáveis, mas a taxa constante deve ser reduzida.
   * Aumente o tamanho do arquivo, conforme descrito em `DiffCache` Dicas de ajuste de desempenho > Ajuste do armazenamento mongo > Tamanho [](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html#main-pars_text_3)do cache do documento.

## Como identificar e corrigir um processo de reindexação travado {#identifying-and-remediating-a-stuck-re-indexing-process}

A reindexação pode ser considerada como &quot;completamente emperrada&quot; sob duas condições:

* A reindexação é muito lenta, a ponto de não ser reportado nenhum progresso significativo nos arquivos de registro em relação ao número de nós atravessados.

   * Por exemplo, se não houver mensagens durante uma hora, ou se o progresso for tão lento que levará uma semana ou mais para ser concluído.

* A reindexação fica presa em um loop sem fim se exceções repetidas forem exibidas nos arquivos de log (por exemplo, `OutOfMemoryException`) no thread de indexação. A repetição das mesmas exceções no registro indica que Oak tenta indexar a mesma coisa repetidamente, mas falha no mesmo problema.

Para identificar e corrigir um processo de reindexação travado, faça o seguinte:

1. Para identificar a causa da indexação travada, as seguintes informações devem ser coletadas:

   * Colete 5 minutos de despejo de thread, um despejo de thread a cada 2 segundos.
   * [Defina o nível de DEBUG e os registros para os anexos](/help/sites-deploying/configure-logging.md).

      * *org.apache.Jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.Jackrabbit.oak.plugins.index.IndexUpdate*
   * Colete dados do `IndexStats` MBean assíncrono:

      * Navegue até AEM OSGi Web Console>Main>JMX>IndexStat>async

         ou vá para [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats)
   * Use o modo [de console](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) oak-run.jar para coletar os detalhes do que existe no nó * `/:async`*.
   * Colete uma lista de pontos de verificação do repositório usando o `CheckpointManager` MBean:

      * Console Web do AEM OSGi>Main>JMX>CheckpointManager>listCheckpoints()

         ou vá para [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager)



1. Após coletar todas as informações descritas na Etapa 1, reinicie o AEM.

   * Reiniciar o AEM pode resolver o problema no caso de uma carga alta simultânea (sobrefluxo da fila de observação ou algo semelhante).
   * Se uma reinicialização não resolver o problema, abra um problema com o Atendimento [ao cliente da](https://helpx.adobe.com/marketing-cloud/contact-support.html) Adobe e forneça todas as informações coletadas na Etapa 1.

## Interrompendo com segurança a reindexação assíncrona {#safely-aborting-asynchronous-re-indexing}

A reindexação pode ser abortada com segurança (parada antes de ser concluída) por meio das vias `async, async-reindex`e `ulltext-async` de indexação ( `IndexStats` Mbean). Para obter mais informações, consulte também a documentação do Apache Oak sobre [Como abortar a reindexação](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex). Além disso, ter em conta que:

* A reindexação dos Índices de propriedades Lucene e Lucene pode ser abortada, pois eles são naturalmente assícronos.
* A reindexação de Índices de Propriedades Oak só pode ser abortada se a reindexação tiver sido iniciada por meio do `PropertyIndexAsyncReindexMBean`.

Para suspender a reindexação com segurança, siga estas etapas:

1. Identifique o MBean IndexStats que controla a linha de reindexação que precisa ser interrompida.

   * Navegue até o MBean IndexStats apropriado por meio do console JMX, acessando o console da Web AEM OSGi>Main>JMX ou https://&lt;host>:&lt;porta>/system/console/jmx (por exemplo, [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
   * Abra o MBean IndexStats com base na linha de reindexação que você deseja interromper ( `async`, `async-reindex`ou `fulltext-async`)

      * Para identificar a faixa apropriada e, portanto, a instância MBean IndexStats, verifique a propriedade &quot;async&quot; dos Índices Oak. A propriedade &quot;async&quot; conterá o nome da faixa: `async`, `async-reindex`ou `fulltext-async`.
      * A faixa também está disponível acessando o Gerenciador de índice do AEM na coluna &quot;Assíncrono&quot;. Para acessar o Gerenciador de índice, navegue até Operations>Diagnosis>Gerenciador de índice.
   ![chlimage_1-121](assets/chlimage_1-121.png)

1. Chame o `abortAndPause()` comando no `IndexStats` MBean apropriado.
1. Marque a definição do índice Oak apropriadamente para impedir a retomada da reindexação quando a linha de indexação for retomada.

   * Ao reindexar um índice **existente** , defina a propriedade reindex como false

      * `/oak:index/someExistingIndex@reindex=false`
   * Ou então, para um **novo** índice:

      * Defina a propriedade type como disabled

         * `/oak:index/someNewIndex@type=disabled`
      * ou remover a definição de índice totalmente
   Confirme as alterações no repositório ao concluir.

1. Finalmente, retome a indexação assíncrona na linha de indexação abortada.

   * No `IndexStats` MBean que emitiu o `abortAndPause()` comando na Etapa 2, chame o `resume()`comando.

## Impedir a reindexação lenta {#preventing-slow-re-indexing}

É melhor reindexar durante períodos silenciosos (por exemplo, não durante uma grande assimilação de conteúdo) e idealmente durante janelas de manutenção quando a carga do AEM é conhecida e controlada. Além disso, verifique se a reindexação não ocorre durante outras atividades de manutenção.
