---
title: Painel de operações
seo-title: Operations Dashboard
description: Saiba como usar o Painel de operações.
seo-description: Learn how to use the Operations Dashboard.
uuid: ef24813f-a7a8-4b26-a496-6f2a0d9efef6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: b210f5d7-1d68-49ee-ade7-667c6ab11d2b
docset: aem65
exl-id: f9a88156-91a2-4c85-9bc9-8f23700c2cbd
feature: Operations
source-git-commit: 891cb5bb8cc9b7114d23617c9164fd428718b302
workflow-type: tm+mt
source-wordcount: '6200'
ht-degree: 2%

---

# Painel de operações {#operations-dashboard}

## Introdução {#introduction}

O Painel de Operações no AEM 6 ajuda os operadores do sistema a monitorar AEM integridade do sistema imediatamente. Ele também fornece informações de diagnóstico geradas automaticamente sobre aspectos relevantes do AEM e permite configurar e executar automação de manutenção independente para reduzir significativamente as operações do projeto e os casos de suporte. O Painel de Operações pode ser estendido com verificações de integridade personalizadas e tarefas de manutenção. Além disso, os dados do Painel de operações podem ser acessados a partir de ferramentas de monitoramento externas via JMX.

**O Painel de Operações:**

* É um status de sistema com um clique para ajudar os departamentos de operações a aumentar a eficiência
* Fornece uma visão geral da integridade do sistema em um único local centralizado
* Reduz o tempo para localizar, analisar e corrigir problemas
* Fornece automação de manutenção independente que ajuda a reduzir significativamente os custos das operações do projeto

Ele pode ser acessado indo até **Ferramentas** - **Operações** na tela AEM Welcome .

>[!NOTE]
>
>Para poder acessar o Painel de Operações, o usuário conectado deve fazer parte do grupo de usuários &quot;Operadores&quot;. Para obter mais informações, consulte a documentação em [Administração de usuário, grupo e direito de acesso](/help/sites-administering/user-group-ac-admin.md).

## Relatórios de integridade {#health-reports}

O sistema de Relatório de Integridade fornece informações sobre a integridade de uma instância de AEM por meio de Sling Health Checks. Isso pode ser feito por meio de solicitações OSGI, JMX, HTTP (via JSON) ou pela interface de toque. Ele oferece medidas e o limite de determinados contadores configuráveis e, em alguns casos, oferecerá informações sobre como resolver o problema.

Ela tem vários recursos, descritos abaixo.

## Verificações de integridade {#health-checks}

O **Relatórios de integridade** são um sistema de cartões que indica uma boa ou má saúde em relação a uma determinada área de produtos. Esses cartões são visualizações das Verificações de integridade do Sling, que agregam dados do JMX e de outras fontes e expõem as informações processadas novamente como MBeans. Esses MBeans também podem ser inspecionados no [Console da Web JMX](/help/sites-administering/jmx-console.md)nos termos do **org.apache.sling.health.check** domínio.

A interface dos Relatórios de integridade pode ser acessada por meio do **Ferramentas** - **Operações** - **Relatórios de integridade** na tela de Boas-vindas AEM ou diretamente pelo seguinte URL:

`https://<serveraddress>:port/libs/granite/operations/content/healthreports/healthreportlist.html`

![chlimage_1-116](assets/chlimage_1-116.png)

O sistema de cartões expõe três estados possíveis: **OK**, **AVISO** e **CRÍTICO**. Os estados são resultado de regras e limites, que podem ser configurados ao passar o mouse sobre o cartão e clicar no ícone de engrenagem na barra de ação:

![chlimage_1-117](assets/chlimage_1-117.png)

### Tipos de Verificação de Integridade {#health-check-types}

Existem dois tipos de controlos sanitários no AEM 6:

1. Verificações de integridade individual
1. Verificações de integridade composta

Um **Verificação de integridade individual** é uma única verificação de integridade que corresponde a um cartão de status. As Verificações de Integridade Individual podem ser configuradas com regras ou limites e podem fornecer uma ou mais dicas e links para resolver problemas de integridade identificados. Vamos considerar a verificação &quot;Erros de registro&quot; como um exemplo: se houver entradas ERROR nos logs da instância, você as encontrará na página de detalhes da verificação de integridade. Na parte superior da página, você verá um link para o analisador de &quot;Mensagem de log&quot; na seção Ferramentas de diagnóstico, que permitirá que você analise esses erros com mais detalhes e reconfigure os registradores.

A **Verificação de integridade composta** é uma verificação que agrega informações de várias verificações individuais.

Os controlos sanitários compostos são configurados com o auxílio de **filtrar tags**. Em essência, todas as verificações únicas que têm a mesma tag de filtro serão agrupadas como uma verificação de integridade composta. Uma Verificação de integridade composta terá um status OK somente se todas as verificações únicas que ela agregar tiverem status OK também.

### Como criar verificações de integridade {#how-to-create-health-checks}

No Painel de Operações, é possível visualizar o resultado de Verificações de Integridade individuais e compostas.

### Criação de uma verificação de integridade individual {#creating-an-individual-health-check}

A criação de uma Verificação de Integridade individual envolve duas etapas: implementando uma Verificação de Integridade do Sling e adicionando uma entrada para a Verificação de Integridade nos nós de configuração do Dashboard.

1. Para criar uma Verificação de Integridade do Sling, é necessário criar um componente OSGI implementando a interface do Sling HealthCheck. Você adicionará esse componente dentro de um pacote. As propriedades do componente identificarão totalmente a Verificação de integridade. Quando o componente estiver instalado, um MBean JMX será criado automaticamente para a verificação de integridade. Consulte a [Documentação de verificação de integridade do Sling](https://sling.apache.org/documentation/bundles/sling-health-check-tool.html) para obter mais informações.

   Exemplo de um componente de Verificação de integridade do Sling, gravado com anotações do componente de serviço OSGI:

   ```java
   @Component(service = HealthCheck.class,
   property = {
       HealthCheck.NAME + "=Example Check",
       HealthCheck.TAGS + "=example",
       HealthCheck.TAGS + "=test",
       HealthCheck.MBEAN_NAME + "=exampleHealthCheckMBean"
   })
    public class ExampleHealthCheck implements HealthCheck {
       @Override
       public Result execute() {
           // health check code
       }
    }
   ```

   >[!NOTE]
   >
   >O `MBEAN_NAME` define o nome do mbean que será gerado para esta verificação de integridade.

1. Depois de criar uma Verificação de integridade, um novo nó de configuração precisa ser criado para torná-lo acessível na interface do Painel de operações. Para esta etapa, é necessário conhecer o nome do Feijão JMX da Verificação de Integridade (o `MBEAN_NAME` propriedade). Para criar uma configuração para a Verificação de integridade, abra o CRXDE e adicione um novo nó (do tipo **nt:unstructured**) no seguinte caminho: `/apps/settings/granite/operations/hc`

   As seguintes propriedades devem ser definidas no novo nó:

   * **Nome:** `sling:resourceType`

      * **Tipo:** `String`
      * **Valor:** `granite/operations/components/mbean`
   * **Nome:** `resource`

      * **Tipo:** `String`
      * **Valor:** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/exampleHealthCheck`

   >[!NOTE]
   >
   >O caminho do recurso acima é criado da seguinte maneira: se o nome do bean da sua verificação de integridade for &quot;teste&quot;, adicione &quot;teste&quot; ao final do caminho `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck`
   >
   >Assim, o caminho final será:
   >
   >`/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/test`

   >[!NOTE]
   >
   >Certifique-se de que a variável `/apps/settings/granite/operations/hc` path tem as seguintes propriedades definidas como true:
   >
   >
   >`sling:configCollectionInherit`
   >
   >`sling:configPropertyInherit`
   >
   >
   >Isso instruirá o gerenciador de configuração a mesclar as novas configurações com as existentes de `/libs`.

### Criando uma Verificação de Integridade Composta {#creating-a-composite-health-check}

A função de uma verificação de integridade composta é agregar várias verificações de integridade individuais que compartilham um conjunto de recursos comuns. Por exemplo, a Verificação de Integridade Composta de Segurança agrupa todas as verificações de integridade individuais que realizam verificações relacionadas com a segurança. A primeira etapa para criar uma verificação composta é adicionar uma nova configuração OSGI. Para ser exibido no Painel de operações, um novo nó de configuração precisa ser adicionado, da mesma forma que fizemos para uma verificação simples.

1. Vá para o Web Configuration Manager no console OSGI. Você pode fazer isso acessando `https://serveraddress:port/system/console/configMgr`
1. Procure a entrada chamada **Verificação de integridade composta do Apache Sling**. Depois de encontrá-lo, observe que há duas configurações já disponíveis: um para as verificações do sistema e outro para as verificações de segurança.
1. Crie uma nova configuração pressionando o botão &quot;+&quot; no lado direito da configuração. Uma nova janela será exibida, conforme mostrado abaixo:

   ![chlimage_1-23](assets/chlimage_1-23.jpeg)

1. Crie uma configuração e salve-a. Um Mbean será criado com a nova configuração.

   A finalidade de cada propriedade de configuração é a seguinte:

   * **Nome (hc.name):** O nome da verificação de integridade composta. Recomenda-se um nome significativo.
   * **Tags (hc.tags):** As tags para esta Verificação de Integridade. Se esta verificação de integridade composta se destinar a ser parte de outra verificação de integridade composta (como em uma hierarquia de verificações de integridade), adicione as tags às quais esse composto está relacionado.
   * **Nome do MBean (hc.mbean.name):** O nome do Mbean que será fornecido ao MBean JMX dessa verificação de integridade composta.
   * **Tags de filtro (filter.tags):** Esta é uma propriedade específica para verificações de integridade compostas. Essas são as tags que o compósito deve agregar. A verificação de integridade composta agregará sob seu grupo todas as verificações de integridade que tenham qualquer tag correspondente a qualquer uma das tags de filtro desse composto. Por exemplo, uma verificação de integridade composta com as tags de filtro **teste** e **check** agregará todos os controlos de saúde individuais e compostos que tenham qualquer um dos **teste** e **check** tags em sua propriedade de tags ( `hc.tags`).

   >[!NOTE]
   >
   >Um novo Mbean JMX é criado para cada nova configuração da Verificação de integridade composta do Apache Sling.**

1. Finalmente, a entrada da verificação de integridade composta que acabou de ser criada precisa ser adicionada nos nós de configuração do Painel de Operações . O procedimento para o efeito é o mesmo que os controlos sanitários individuais: um nó do tipo **nt:unstructured** precisa ser criada em `/apps/settings/granite/operations/hc`. A propriedade resource do nó será definida pelo valor de **hc.average.name** na configuração OSGI.

   Se, por exemplo, você criou uma configuração e definiu a variável **hc.mbean.name** para **diskusage**, os nós de configuração terão esta aparência:

   * **Nome:** `Composite Health Check`

      * **Tipo:** `nt:unstructured`

   Com as seguintes propriedades:

   * **Nome:** `sling:resourceType`

      * **Tipo:** `String`
      * **Valor:** `granite/operations/components/mbean`
   * **Nome:** `resource`

      * **Tipo:** `String`
      * **Valor:** `/system/sling/monitoring/mbeans/org/apache/sling/healthcheck/HealthCheck/diskusage`

   >[!NOTE]
   >
   >Se você criar verificações de integridade individuais que logicamente pertencem a uma verificação composta que já está presente no Painel por padrão, elas serão automaticamente capturadas e agrupadas na respectiva verificação composta. Por causa disso, não há necessidade de criar um novo nó de configuração para essas verificações.
   >
   >Por exemplo, se você criar uma verificação de integridade de segurança individual, tudo o que precisa fazer é atribuir a ela o &quot;**segurança**&quot; e estiver instalado, ele aparecerá automaticamente na verificação composta de Verificações de Segurança no Painel de Operações.

### Verificações de integridade fornecidas com AEM {#health-checks-provided-with-aem}

<table>
 <tbody>
  <tr>
   <td><strong>Nome da verificação de integridade</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Desempenho da consulta</td>
   <td><p>Este exame de saúde foi simplificado <strong>no AEM 6.4</strong>e agora verifica a função recém-refatorada <code>Oak QueryStats</code> MBean, mais especificamente o <code>SlowQueries </code>atributo. Se as estatísticas contiverem queries lentos, a verificação de integridade retornará um aviso. Caso contrário, retorna o status OK.<br /> </p> <p>O MBean para esta verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueriesStatus%2Ctype%3DHealthCheck">org.apache.sling.health check:name=queriesStatus,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Comprimento da fila de observação</td>
   <td><p>A Duração da Fila de Observação é repetida em todos os Ouvintes de Eventos e Observadores de Plano de Fundo, e compara seus <code>queueSize </code>para <code>maxQueueSize</code> e:</p>
    <ul>
     <li>retorna o status Crítico se a variável <code>queueSize</code> excede o valor <code>maxQueueSize</code> valor (é quando os eventos são soltos)</li>
     <li>retorna Avisar se a variável <code>queueSize</code> é maior que <code>maxQueueSize * WARN_THRESHOLD</code> (o valor padrão é 0,75) </li>
    </ul> <p>O comprimento máximo de cada fila provém de configurações separadas (Oak e AEM) e não é configurável a partir dessa verificação de integridade. O MBean para esta verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DObservationQueueLengthHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.health check:name=ObservationQueueLengthHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Limites de cruzamento da consulta</td>
   <td><p>Limites de passagem de consulta verifica o <code>QueryEngineSettings</code> MBean, mais especificamente o <code>LimitInMemory</code> e <code>LimitReads</code> e retorna o seguinte status:</p>
    <ul>
     <li>retorna o status Warn se um dos limites for igual ou superior a <code>Integer.MAX_VALUE</code></li>
     <li>retorna o status Warn se um dos limites for menor que 10000 (a configuração recomendada do Oak)</li>
     <li>retorna o status Crítico se a variável <code>QueryEngineSettings</code> ou qualquer um dos limites não pode ser recuperado</li>
    </ul> <p>O Mbean para este exame de saúde é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DqueryTraversalLimitsBundle%2Ctype%3DHealthCheck">org.apache.sling.health check:name=queryTraversalLimitsBundle,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Relógios sincronizados</td>
   <td><p>Esta verificação é relevante apenas para <a href="https://github.com/apache/sling-old-svn-mirror/blob/4df9ab2d6592422889c71fa13afd453a10a5a626/bundles/extensions/discovery/oak/src/main/java/org/apache/sling/discovery/oak/SynchronizedClocksHealthCheck.java">clusters de nodestore de documentos</a>. Ele retorna o seguinte status:</p>
    <ul>
     <li>retorna o status Warn quando os relógios da instância ficam fora de sincronia e passam por um limite baixo predefinido</li>
     <li>retorna o status Crítico quando os relógios de instância ficam fora de sincronia e ultrapassam um limite alto predefinido</li>
    </ul> <p>O Mbean para este exame de saúde é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingDiscoveryOakSynchronizedClocks%2Ctype%3DHealthCheck">org.apache.sling.health check:name=slingDiscoveryOakSynchronizedClocks,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Índices assíncronos</td>
   <td><p>A verificação de Índices Assíncronos:</p>
    <ul>
     <li>retorna o status Crítico se pelo menos uma faixa de indexação estiver falhando</li>
     <li>verifica a <code>lastIndexedTime</code> para todas as vias de indexação e:
      <ul>
       <li>retorna o status Crítico se tiver mais de 2 horas atrás </li>
       <li>retorna o status Warning se estiver entre 2 horas e 45 minutos atrás </li>
       <li>retorna o status OK se for inferior a 45 minutos atrás </li>
      </ul> </li>
     <li>se nenhuma dessas condições for atendida, retornará o status OK</li>
    </ul> <p>Os limites de status Crítico e Aviso podem ser configurados. O Mbean para este exame de saúde é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DasyncIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.health check:name=asyncIndexHealthCheck,type=HealthCheck</a>.</p> <p><strong>Observação: </strong>Esta verificação de integridade está disponível com o AEM 6.4 e foi transferida para o AEM 6.3.0.1.</p> </td>
  </tr>
  <tr>
   <td>Índices Lucene grandes</td>
   <td><p>Essa verificação usa os dados expostos pela variável <code>Lucene Index Statistics</code> MBean para identificar índices e retornos grandes:</p>
    <ul>
     <li>um status de Aviso se houver um índice com mais de 1 bilhão de documentos</li>
     <li>um status Crítico se houver um índice com mais de 1,5 bilhão de documentos</li>
    </ul> <p>Os limites são configuráveis e o MBean para a verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlargeIndexHealthCheck%2Ctype%3DHealthCheck">org.apache.sling.health check:name=largeIndexHealthCheck,type=HealthCheck.</a></p> <p><strong>Observação: </strong>Essa verificação está disponível com o AEM 6.4 e foi transferida para o AEM 6.3.2.0.</p> </td>
  </tr>
  <tr>
   <td>Manutenção do sistema</td>
   <td><p>System Maintenance (Manutenção do sistema) é uma verificação composta que retorna o OK se todas as tarefas de manutenção estiverem sendo executadas como configuradas. Lembre-se:</p>
    <ul>
     <li>cada tarefa de manutenção é acompanhada de um exame de saúde associado</li>
     <li>se uma tarefa não for adicionada a uma janela de manutenção, sua verificação de integridade retornará Crítico</li>
     <li>é necessário configurar as tarefas de manutenção Log de auditoria e Expurgação do fluxo de trabalho ou removê-las das janelas de manutenção. Se deixadas não configuradas, essas tarefas falharão na primeira execução tentada, de modo que a verificação de Manutenção do Sistema retornará o status Crítico.</li>
     <li><strong>Com AEM 6.4</strong>, também há uma verificação para o <a href="/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks">Manutenção de binários Lucene</a> tarefa</li>
     <li>em AEM 6.2 e inferior, a verificação de manutenção do sistema retorna um status Warning logo após a inicialização, pois as tarefas nunca são executadas. A partir da versão 6.3, eles retornarão OK se a primeira janela de manutenção ainda não tiver sido atingida.</li>
    </ul> <p>O MBean para esta verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsystemchecks%2Ctype%3DHealthCheck">org.apache.sling.health check:name=systemcontrols,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Fila de replicação</td>
   <td><p>Essa verificação repete os agentes de replicação e observa suas filas. Para o item na parte superior da fila, a verificação verifica quantas vezes o agente tentou novamente a replicação. Se o agente tiver tentado novamente a replicação mais do que o valor da <code>numberOfRetriesAllowed</code> , retorna um aviso. O <code>numberOfRetriesAllowed</code> é configurável. </p> <p>O MBean para esta verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DreplicationQueue%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health check:name=replicationQueue,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Sling Jobs</td>
   <td>
    <div>
      O Sling Jobs verifica o número de tarefas enfileiradas no JobManager, o compara ao
     <code>maxNumQueueJobs</code> limite e:
    </div>
    <ul>
     <li>retorna Crítico se for maior que a variável <code>maxNumQueueJobs</code> estão na fila</li>
     <li>retorna Crítico se houver trabalhos ativos de longa duração com mais de 1 hora</li>
     <li>retorna Crítico se houver trabalhos em fila e o último horário de trabalho concluído for superior a 1 hora</li>
    </ul> <p>Somente o parâmetro de número máximo de trabalhos em fila é configurável e tem o valor padrão de 1000.</p> <p>O MBean para esta verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingJobs%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health check:name=slingJobs,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Desempenho da solicitação</td>
   <td><p>Essa verificação analisa o <code>granite.request.metrics.timer</code> <a href="http://localhost:4502/system/console/slingmetrics" target="_blank">Métrica Sling </a>e:</p>
    <ul>
     <li>retorna Crítico se o valor do percentil 75 estiver acima do limite crítico (o valor padrão é 500 milissegundos)</li>
     <li>retorna Warn se o valor do percentil 75 estiver acima do limite de aviso (o valor padrão é 200 milissegundos)</li>
    </ul> <p>O MBean para esta verificação de integridade é<em> </em><a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DrequestsStatus%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health check:name=requestsStatus,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Erros de log</td>
   <td><p>Essa verificação retorna o status Warn se houver erros no log.</p> <p>O MBean para esta verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DlogErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health check:name=logErrorHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Espaço em disco</td>
   <td><p>A verificação do Espaço em Disco verifica o <code>FileStoreStats</code> O MBean recupera o tamanho do armazenamento de nós e a quantidade de espaço em disco utilizável na partição do armazenamento de nós, e:</p>
    <ul>
     <li>retorna Warn se a proporção de espaço em disco utilizável para o tamanho do repositório for menor que o limite de aviso (o valor padrão é 10)</li>
     <li>retorna Crítico se a proporção de espaço em disco utilizável para o tamanho do repositório for menor que o limite crítico (o valor padrão é 2)</li>
    </ul> <p>Ambos os limites são configuráveis. A verificação só funciona em instâncias com uma Loja de segmentos.</p> <p>O MBean para esta verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DDiskSpaceHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health check:name=DiskSpaceHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Verificação de integridade do assistente de agendamento</td>
   <td><p>Essa verificação retornará um aviso se a instância tiver trabalhos do Quartz em execução por mais de 60 segundos. O limite de duração aceitável é configurável.</p> <p>O MBean para esta verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DslingCommonsSchedulerHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health check:name=slingCommonsSchedulerHealthCheck,type=HealthCheck</a><em>.</em></p> </td>
  </tr>
  <tr>
   <td>Verificações de segurança</td>
   <td><p>A verificação de segurança é um composto que agrega os resultados de várias verificações relacionadas à segurança. Estes controlos de saúde individuais abordam preocupações diferentes da lista de controlo de segurança disponível no <a href="/help/sites-administering/security-checklist.md">Página de documentação da Lista de verificação de segurança.</a> A verificação é útil como um teste de segurança de fumaça quando a instância é iniciada. </p> <p>O MBean para esta verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3Dsecuritychecks%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health check:name=securityCheck,type=HealthCheck</a></p> </td>
  </tr>
  <tr>
   <td>Grupos ativos</td>
   <td><p>Os Pacotes Ativos verificam o estado de todos os pacotes e:</p>
    <ul>
     <li>retorna o status Warn se qualquer um dos pacotes não estiver ativo ou (iniciando, com ativação lenta)</li>
     <li>ele ignora o status dos pacotes na lista de ignorados</li>
    </ul> <p>O parâmetro ignore list pode ser configurado.</p> <p>O MBean para esta verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DinactiveBundles%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health check:name=inativeBundles,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Verificação do Cache de Código</td>
   <td><p>Esta é uma Verificação de integridade que verifica várias condições da JVM que podem acionar um bug do CodeCache presente no Java 7:</p>
    <ul>
     <li>retorna Avisar se a instância estiver sendo executada no Java 7, com a limpeza do Cache de Código ativada</li>
     <li>retorna Avisar se a instância estiver sendo executada no Java 7 e o tamanho do Cache de Código Reservado for menor que um limite mínimo (o valor padrão é 90 MB)</li>
    </ul> <p>O <code>minimum.code.cache.size</code> limite é configurável. Para obter mais informações sobre o erro, <a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547">check</a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"></a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"></a><a href="https://bugs.java.com/bugdatabase/view_bug.do?bug_id=8012547"> esta página</a>.</p> <p>O MBean para esta verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DcodeCacheHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health check:name=codeCacheHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
  <tr>
   <td>Recurso Buscar erros de caminho</td>
   <td><p>Verifica se há recursos no caminho <code>/apps/foundation/components/primary</code> e:</p>
    <ul>
     <li>retorna Avisar se houver nós secundários em <code>/apps/foundation/components/primary</code></li>
    </ul> <p>O MBean para esta verificação de integridade é <a href="http://localhost:4502/system/console/jmx/org.apache.sling.healthcheck%3Aname%3DresourceSearchPathErrorHealthCheck%2Ctype%3DHealthCheck" target="_blank">org.apache.sling.health check:name=resourceSearchPathErrorHealthCheck,type=HealthCheck</a>.</p> </td>
  </tr>
 </tbody>
</table>

## Monitoramento com o Nagios {#monitoring-with-nagios}

O Painel de verificação de integridade pode se integrar ao Nagios por meio do Granite JMX Mbeans. O exemplo abaixo ilustra como adicionar uma verificação que mostra a memória usada no servidor que está executando o AEM.

1. Configure e instale o Nagios no servidor de monitoramento.
1. Em seguida, instale o NRPE (Executor de Plug-in Remoto do Nagios).

   >[!NOTE]
   >
   >Para obter mais informações sobre como instalar Nagios e NRPE em seu sistema, consulte o [Documentação do Nagios](https://library.nagios.com/library/products/nagioscore/manuals/).

1. Adicione uma definição de host para o servidor AEM. Isso pode ser feito por meio da Interface Web Nagios XI, usando o Gerenciador de configuração:

   1. Abra um navegador e aponte para o servidor Nagios.
   1. Pressione a tecla **Configurar** no menu superior.
   1. No painel esquerdo, pressione a tecla **Gerenciador de configuração principal** under **Configuração avançada**.
   1. Pressione a tecla **Hosts** sob o **Monitoramento** seção.
   1. Adicione a definição de host:

   ![chlimage_1-118](assets/chlimage_1-118.png)

   Veja abaixo um exemplo de um arquivo de configuração de host, caso você esteja usando o Nagios Core:

   ```xml
   define host {
      address 192.168.0.5
      max_check_attempts 3
      check_period 24x7
      check-command check-host-alive
      contacts admin
      notification_interval 60
      notification_period 24x7
   }
   ```

1. Instale o Nagios e o NRPE no servidor AEM.
1. Instale o [check_http_json](https://github.com/phrawzty/check_http_json) em ambos os servidores.
1. Defina um comando genérico de verificação JSON em ambos os servidores:

   ```xml
   define command{
   
       command_name    check_http_json-int
   
       command_line    /usr/lib/nagios/plugins/check_http_json --user "$ARG1$" --pass "$ARG2$" -u 'https://$HOSTNAME$:$ARG3$/$ARG4$' -e '$ARG5$' -w '$ARG6$' -c '$ARG7$'
   
   }
   ```

1. Adicione um serviço para memória usada no servidor AEM:

   ```xml
   define service {
   
       use generic-service
   
       host_name my.remote.host
   
       service_description AEM Author Used Memory
   
       check_command  check_http_json-int!<cq-user>!<cq-password>!<cq-port>!system/sling/monitoring/mbeans/java/lang/Memory.infinity.json!{noname}.mbean:attributes.HeapMemoryUsage.mbean:attributes.used.mbean:value!<warn-threshold-in-bytes>!<critical-threshold-in-bytes>
   
       }
   ```

1. Verifique o painel Nagios quanto ao serviço recém-criado:

   ![chlimage_1-119](assets/chlimage_1-119.png)

## Ferramentas de diagnóstico {#diagnosis-tools}

O Painel de Operações também fornece acesso às Ferramentas de Diagnóstico, que podem ajudar a encontrar e solucionar problemas de causas raiz dos avisos provenientes do Painel de Verificação de Integridade, além de fornecer informações importantes de depuração para operadores do sistema.

Entre as suas características mais importantes estão:

* Um analisador de mensagens de log
* A capacidade de acessar despejos de heap e thread
* Analisadores de desempenho de solicitações e consultas

Você pode acessar a tela Ferramentas de diagnóstico acessando **Ferramentas - Operações - Diagnóstico** na tela AEM Welcome . Você também pode acessar a tela acessando diretamente o seguinte URL: `https://serveraddress:port/libs/granite/operations/content/diagnosis.html`

![chlimage_1-120](assets/chlimage_1-120.png)

### Mensagens de registro {#log-messages}

Por padrão, a Interface do usuário das mensagens de log exibirá todas as mensagens de ERRO. Se desejar que mais mensagens de log sejam exibidas, será necessário configurar um agente de log com o nível de log apropriado.

As mensagens de log usam um appender no log de memória e, portanto, não estão relacionadas aos arquivos de log. Outra consequência é que alterar os níveis de log nessa interface não alterará as informações que são registradas nos arquivos de log tradicionais. Adicionar e remover loggers nesta interface do usuário afetará somente o logger da memória. Além disso, observe que a alteração das configurações do agente de log será refletida no futuro do agente de log da memória - as entradas que já estão registradas e não são mais relevantes não são excluídas, mas entradas semelhantes não serão registradas no futuro.

Você pode configurar o que é registrado fornecendo configurações de logger do botão de engrenagem superior esquerdo na interface do usuário. Lá, você pode adicionar, remover ou atualizar configurações do agente de log. Uma configuração de logger é composta por um **nível de log** (AVISO / INFORMAÇÕES / DEBUG) e um **nome do filtro**. O **nome do filtro** tem a função de filtrar a fonte das mensagens de log que são registradas. Como alternativa, se um agente de log deve capturar todas as mensagens de log do nível especificado, o nome do filtro deve ser &quot;**root**&quot;. Definir o nível de um agente de log acionará a captura de todas as mensagens com um nível igual ou superior ao especificado.

Exemplos:

* Se você planeja capturar todas as **ERRO** messages - nenhuma configuração é necessária. Todas as mensagens de ERRO são capturadas por padrão.
* Se você planeja capturar todas as **ERRO**, **AVISO** e **INFO** messages - o nome do logger deve ser definido como: &quot;**root**&quot; e o nível do logger para: **INFO**.

* Se você planeja capturar todas as mensagens provenientes de um determinado pacote (por exemplo, com.adobe.granite), o nome do logger deve ser definido como: &quot;com.adobe.granite&quot; e o nível do agente de log para: **DEPURAR** (isso capturará todas as **ERRO**, **AVISO**, **INFO** e **DEPURAR** mensagens), conforme mostrado na imagem abaixo.

![chlimage_1-121](assets/chlimage_1-121.png)

>[!NOTE]
>
>Não é possível definir um nome de agente de log para capturar apenas mensagens ERROR por meio de um filtro especificado. Por padrão, todas as mensagens de ERRO são capturadas.

>[!NOTE]
>
>A interface do usuário das mensagens de log não reflete o log de erros real. A menos que esteja configurando outros tipos de mensagens de log na interface do usuário, você verá apenas mensagens de ERRO. Para saber como exibir mensagens de log específicas, consulte as instruções acima.

>[!NOTE]
>
>As configurações na página de diagnóstico não influenciam o que está registrado nos arquivos de log e vice-versa. Portanto, embora o log de erros possa capturar mensagens INFO, talvez você não as veja na interface do usuário de mensagens de log. Além disso, por meio da interface do usuário, é possível capturar mensagens DEBUG de determinados pacotes sem afetar o log de erros. Para obter mais informações sobre como configurar os arquivos de log, consulte [Registro](/help/sites-deploying/configure-logging.md).

>[!NOTE]
>
>**Com AEM 6.4**, as tarefas de manutenção são desconectadas da caixa em um formato mais avançado de informações no nível INFO. Isso permite uma melhor visibilidade do estado das tarefas de manutenção.
>
>Caso esteja usando ferramentas de terceiros (como o Splunk) para monitorar e reagir à atividade de tarefa de manutenção, você pode usar as seguintes instruções de log:

```
Log level: INFO
DATE+TIME [MaintanceLogger] Name=<MT_NAME>, Status=<MT_STATUS>, Time=<MT_TIME>, Error=<MT_ERROR>, Details=<MT_DETAILS>
```

### Solicitar desempenho {#request-performance}

A página Desempenho da solicitação permite a análise das solicitações de página mais lentas processadas. Somente solicitações de conteúdo serão registradas nesta página. Mais especificamente, as seguintes solicitações serão capturadas:

1. Solicitações de acesso a recursos em `/content`
1. Solicitações de acesso a recursos em `/etc/design`
1. Pedidos com `".html"` extensão

![chlimage_1-122](assets/chlimage_1-122.png)

A página é exibida:

* A hora em que a solicitação foi feita
* O URL e o método de solicitação
* A duração em milissegundos

Por padrão, as 20 solicitações de página mais lentas são capturadas, mas o limite pode ser modificado no Configuration Manager.

### Desempenho da consulta {#query-performance}

A página Desempenho da Consulta permite a análise das consultas mais lentas realizadas pelo sistema. Essas informações são fornecidas pelo repositório em um Mbean JMX. Em Jackrabbit, a `com.adobe.granite.QueryStat` O JMX Mbean fornece essas informações, enquanto no repositório Oak, ele é oferecido por `org.apache.jackrabbit.oak.QueryStats.`

A página é exibida:

* A hora em que o query foi feito
* O idioma do query
* O número de vezes que o query foi emitido
* A instrução do query
* A duração em milissegundos

![chlimage_1-123](assets/chlimage_1-123.png)

### Explicar consulta {#explain-query}

Para qualquer query, o Oak tenta descobrir a melhor maneira de executar com base nos índices do Oak definidos no repositório no **oak:index** nó . Dependendo da query, índices diferentes podem ser escolhidos pelo Oak. Entender como o Oak está executando um query é a primeira etapa para otimizar o query.

O Explain Query é uma ferramenta que explica como o Oak está executando um query. Ele pode ser acessado indo até **Ferramentas - Operações - Diagnóstico** na tela de boas-vindas AEM, em seguida, clicando em **Desempenho da consulta** e alternando para o **Explicar Consulta** guia .

**Recursos**

* Suporta os idiomas de consulta Xpath, JCR-SQL e JCR-SQL2
* Relata o tempo de execução real da consulta fornecida
* Detecta consultas lentas e avisa sobre consultas que podem ser potencialmente lentas
* Relata o índice Oak usado para executar a consulta
* Exibe a explicação real do mecanismo Oak Query
* Fornece uma lista click-to-load de consultas lentas e populares

Quando estiver na interface do usuário do Explain Query, tudo o que você precisa fazer para usá-la é inserir o query e pressionar o **Explicar** botão:

![chlimage_1-124](assets/chlimage_1-124.png)

A primeira entrada na seção Explicação da Consulta é a explicação real. A explicação mostrará o tipo de índice usado para executar a query.

A segunda entrada é o plano de execução.

Marcar o **Incluir tempo de execução** antes de executar o query, também mostrará a quantidade de tempo em que o query foi executado. O **Incluir contagem de nós** reportará a contagem de nós. Isso permite obter mais informações, que podem ser usadas para otimizar os índices para seu aplicativo ou implantação.

![chlimage_1-125](assets/chlimage_1-125.png)

### O Gerenciador de Índice {#the-index-manager}

A finalidade do Gerenciador de índice é facilitar o gerenciamento do índice, como manter índices ou visualizar seu status.

Ele pode ser acessado indo até **Ferramentas - Operações - Diagnóstico **na tela de boas-vindas e clicando no botão **Gerenciador de índice** botão.

Ele também pode ser acessado diretamente neste URL: `https://serveraddress:port/libs/granite/operations/content/diagnosistools/indexManager.html`

![screen-shot_2019-06-18at154754](assets/screen-shot_2019-06-18at154754.png)

A interface do usuário pode ser usada para filtrar índices na tabela, digitando os critérios de filtro na caixa de pesquisa no canto superior esquerdo da tela.

### Baixar o ZIP de status {#download-status-zip}

Isso acionará o download de um zip contendo informações úteis sobre o status e a configuração do sistema. O arquivo contém configurações de instância, uma lista de pacotes, OSGI, métricas e estatísticas de Sling e isso pode resultar em um arquivo grande. Você pode reduzir o impacto de arquivos de status grandes usando o **ZIP de status de download** janela. A janela pode ser acessada de:**AEM > Ferramentas > Operações > Diagnóstico > Baixar ZIP de status.**

Nessa janela, você pode selecionar o que exportar (arquivos de log e/ou despejos de thread) e o número de dias de logs incluídos no download em relação à data atual.

![download_status_zip](assets/download_status_zip.png)

### Baixar o despejo de encadeamento {#download-thread-dump}

Isso acionará o download de um zip contendo informações sobre os threads presentes no sistema. Informações sobre cada thread são fornecidas, como seu status, o carregador de classe e o rastreamento de pilha.

### Baixar o despejo da pilha {#download-heap-dump}

Você também pode baixar um instantâneo do heap para analisá-lo posteriormente. Observe que isso acionará o download de um arquivo grande, da ordem de centenas de megabytes.

## Tarefas de manutenção automatizada {#automated-maintenance-tasks}

A página Tarefas de manutenção automatizada é um local onde você pode visualizar e rastrear tarefas de manutenção recomendadas programadas para execução periódica. As tarefas são integradas ao sistema de verificação de integridade. As tarefas também podem ser executadas manualmente na interface.

Para acessar a página Manutenção no Painel de Operações, você precisa acessar **Ferramentas - Operações - Painel - Manutenção** na tela AEM Welcome ou siga diretamente este link:

`https://serveraddress:port/libs/granite/operations/content/maintenance.html`

As seguintes tarefas estão disponíveis no Painel de Operações:

1. O **Revisão de limpeza** tarefa, localizada na **Janela de manutenção diária** menu.
1. O **Limpeza de binários Lucene** tarefa, localizada na **Janela de manutenção diária** menu.
1. O **Limpeza de fluxo de trabalho** tarefa, localizada na **Janela de manutenção semanal** menu.
1. O **Coleta de lixo do armazenamento de dados** tarefa, localizada na **Janela de manutenção semanal** menu.
1. O **Manutenção do log de auditoria** tarefa, localizada na **Janela de manutenção semanal** menu.
1. O **Manutenção da limpeza de versão** tarefa, localizada na **Janela de manutenção semanal** menu.

O tempo padrão para a janela de manutenção diária é de 2 a 5 horas. As tarefas configuradas para serem executadas na janela de manutenção semanal serão executadas entre 1 e 2 AM aos sábados.

Você também pode configurar os tempos pressionando o ícone de engrenagem em qualquer uma das duas placas de manutenção:

![chlimage_1-126](assets/chlimage_1-126.png)

>[!NOTE]
>
>Desde o AEM 6.1, as janelas de manutenção existentes também podem ser configuradas para serem executadas mensalmente.

### Limpeza da revisão {#revision-clean-up}

Para obter mais informações sobre como executar a Revisão de limpeza, [consulte este artigo dedicado](/help/sites-deploying/revision-cleanup.md).

### Limpeza de binários do Lucene {#lucene-binaries-cleanup}

Ao usar a tarefa Limpeza de binários do Lucene, é possível limpar binários do lucene e reduzir o requisito de tamanho do armazenamento de dados em execução. Isso ocorre porque o churn binário do lucene será reivindicado diariamente em vez da dependência anterior em um [coleta de lixo do armazenamento de dados](/help/sites-administering/data-store-garbage-collection.md) executar.

Embora a tarefa de manutenção tenha sido desenvolvida para reduzir o lixo de revisão relacionado ao Lucene, há ganhos gerais de eficiência ao executar a tarefa:

* A execução semanal da tarefa de coleta de lixo do armazenamento de dados será concluída mais rapidamente
* Também pode melhorar ligeiramente o desempenho geral do AEM

Você pode acessar a tarefa Limpeza de binários Lucene a partir de: **AEM > Ferramentas > Operações > Manutenção > Janela de manutenção diária > Limpeza de binários do Lucene**.

### Coleta de lixo do armazenamento de dados {#data-store-garbage-collection}

Para obter detalhes sobre a Coleta de lixo do Data Store, consulte o [página de documentação](/help/sites-administering/data-store-garbage-collection.md).

### Limpeza de fluxo de trabalho {#workflow-purge}

Os fluxos de trabalho também podem ser removidos do Painel de manutenção. Para executar a tarefa Expurgação de Fluxo de Trabalho, é necessário:

1. Clique no botão **Janela de manutenção semanal** página.
1. Na página a seguir, clique no link **Reproduzir** no botão **Limpeza de fluxo de trabalho** cartão.

>[!NOTE]
>
>Para obter informações mais detalhadas sobre a Manutenção do Fluxo de Trabalho, consulte [esta página](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances).

### Manutenção do log de auditoria {#audit-log-maintenance}

Para a Manutenção do Log de Auditoria, consulte o [página de documentação separada.](/help/sites-administering/operations-audit-log.md)

### Remoção da versão {#version-purge}

Você pode agendar a tarefa de manutenção da limpeza de versão para excluir automaticamente as versões antigas. Como resultado, isso minimiza a necessidade de usar manualmente a variável [Ferramentas de limpeza de versão](/help/sites-deploying/version-purging.md). Você pode agendar e configurar a tarefa de limpeza de versão acessando **Ferramentas > Operações > Manutenção > Janela de manutenção semanal** e seguindo estas etapas:

1. Clique no botão **Adicionar** botão.
1. Choose **Limpeza de versão** no menu suspenso.

   ![version_purge_maintenanceask](assets/version_purge_maintenancetask.png)

1. Para configurar a tarefa de limpeza de versão, clique no botão **engrenagens** no cartão de manutenção Version Purge recém-criado.

   ![version_purge_taskconfiguration](assets/version_purge_taskconfiguration.png)

**Com AEM 6.4**, você pode interromper a tarefa de manutenção da limpeza de versão da seguinte maneira:

* Automaticamente - Se a janela de manutenção agendada for fechada antes que a tarefa possa ser concluída, a tarefa será interrompida automaticamente. Ele será retomado quando a próxima janela de manutenção for aberta.
* Manualmente - Para interromper manualmente a tarefa, no cartão de manutenção Expurgação de Versão, clique no botão **Stop** ícone . Na próxima execução, a tarefa será retomada com segurança.

>[!NOTE]
>
>Parar a tarefa de manutenção significa suspender sua execução sem perder o controle da tarefa já em andamento.

>[!CAUTION]
>
>Para otimizar o tamanho do repositório, você deve executar a tarefa de limpeza de versão com frequência. A tarefa deve ser agendada fora do horário comercial, quando houver uma quantidade limitada de tráfego.

## Tarefas de manutenção personalizadas {#custom-maintenance-tasks}

As tarefas de manutenção personalizadas podem ser implementadas como serviços OSGi. Como a infraestrutura da tarefa de manutenção se baseia no manuseio de tarefas do Apache Sling, uma tarefa de manutenção deve implementar a interface java ` [org.apache.sling.event.jobs.consumer.JobExecutor](https://sling.apache.org/apidocs/sling7/org/apache/sling/event/jobs/consumer/JobExecutor.html)`. Além disso, deve declarar várias propriedades de registro de serviço a serem detectadas como uma tarefa de manutenção, conforme listado abaixo:

<table>
 <tbody>
  <tr>
   <td><strong>Nome da Propriedade do Serviço</strong><br /> </td>
   <td><strong>Descrição</strong></td>
   <td><strong>Exemplo</strong><br /> </td>
   <td><strong>Tipo</strong></td>
  </tr>
  <tr>
   <td>granite.maintenance.isStoppable</td>
   <td>Atributo booleano que define se a tarefa pode ser interrompida pelo usuário. Se uma tarefa declarar que é parável, ela deverá verificar, durante sua execução, se foi interrompida e agir de acordo. O padrão é false.</td>
   <td>verdadeiro</td>
   <td>Opcional</td>
  </tr>
  <tr>
   <td>granite.maintenance.mandatory</td>
   <td>Atributo booleano que define se uma tarefa é obrigatória e deve ser executada periodicamente. Se uma tarefa for obrigatória, mas não estiver em nenhuma janela de programação ativa, uma Verificação de integridade relatará isso como um erro. O padrão é false.</td>
   <td>verdadeiro</td>
   <td>Opcional</td>
  </tr>
  <tr>
   <td>granite.maintenance.name</td>
   <td>Um nome exclusivo para a tarefa - é usado para fazer referência à tarefa. Esse geralmente é um nome simples.</td>
   <td>MyMaintenanceTask</td>
   <td>Obrigatório</td>
  </tr>
  <tr>
   <td>granite.maintenance.title</td>
   <td>Um título exibido para esta tarefa</td>
   <td>Minha Tarefa de Manutenção Especial</td>
   <td>Obrigatório</td>
  </tr>
  <tr>
   <td>job.topics</td>
   <td>Este é um tópico exclusivo da tarefa de manutenção.<br /> A manipulação do trabalho do Apache Sling iniciará um trabalho com exatamente este tópico para executar a tarefa de manutenção e, à medida que a tarefa for registrada para este tópico, ele será executado.<br /> O tópico deve começar com <i>com/adobe/granite/maintenance/job/</i></td>
   <td>com/adobe/granite/maintenance/job/MyMaintenanceTask</td>
   <td>Obrigatório</td>
  </tr>
 </tbody>
</table>

Além das propriedades de serviço acima, a função `process()` do método `JobConsumer` A interface precisa ser implementada adicionando o código que deve ser executado para a tarefa de manutenção. O `JobExecutionContext` pode ser usado para gerar informações de status, verificar se o trabalho foi interrompido pelo usuário e criar um resultado (sucesso ou falha).

Para situações em que uma tarefa de manutenção não deve ser executada em todas as instalações (por exemplo, executar somente na instância de publicação), é possível fazer com que o serviço exija uma configuração para estar ativo, adicionando `@Component(policy=ConfigurationPolicy.REQUIRE)`. Em seguida, você pode marcar a configuração de acordo como sendo o modo de execução dependente no repositório. Para obter mais informações, consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md#creating-the-configuration-in-the-repository).

Veja abaixo um exemplo de uma tarefa de manutenção personalizada que exclui arquivos de um diretório temporário configurável que foi modificado nas últimas 24 horas:

src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java

<table>
 <tbody>
  <tr>
   <td><p> </p> <p><code>/*</code></p> <p><code> * #%L</code></p> <p><code> * sample-maintenance-task</code></p> <p><code> * %%</code></p> <p><code> * Copyright (C) 2014 Adobe</code></p> <p><code> * %%</code></p> <p><code> * Licensed under the Apache License, Version 2.0 (the "License");</code></p> <p><code> * you may not use this file except in compliance with the License.</code></p> <p><code> * You may obtain a copy of the License at</code></p> <p><code> * </code></p> <p><code> * <a href="https://www.apache.org/licenses/LICENSE-2.0">https://www.apache.org/licenses/LICENSE-2.0</a></code></p> <p><code> * </code></p> <p><code> * Unless required by applicable law or agreed to in writing, software</code></p> <p><code> * distributed under the License is distributed on an "AS IS" BASIS,</code></p> <p><code> * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.</code></p> <p><code> * See the License for the specific language governing permissions and</code></p> <p><code> * limitations under the License.</code></p> <p><code> * #L%</code></p> <p><code> */</code></p> <p><code> </code></p> <p><code>package com.adobe.granite.samples.maintenance.impl;</code></p> <p><code> </code></p> <p><code>import java.io.File;</code></p> <p><code>import java.util.Calendar;</code></p> <p><code>import java.util.Collection;</code></p> <p><code>import java.util.Map;</code></p> <p><code> </code></p> <p><code>import org.apache.commons.io.FileUtils;</code></p> <p><code>import org.apache.commons.io.filefilter.IOFileFilter;</code></p> <p><code>import org.apache.commons.io.filefilter.TrueFileFilter;</code></p> <p><code>import org.apache.felix.scr.annotations.Activate;</code></p> <p><code>import org.apache.felix.scr.annotations.Component;</code></p> <p><code>import org.apache.felix.scr.annotations.Properties;</code></p> <p><code>import org.apache.felix.scr.annotations.Property;</code></p> <p><code>import org.apache.felix.scr.annotations.Service;</code></p> <p><code>import org.apache.sling.commons.osgi.PropertiesUtil;</code></p> <p><code>import org.apache.sling.event.jobs.Job;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobConsumer;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionContext;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutionResult;</code></p> <p><code>import org.apache.sling.event.jobs.consumer.JobExecutor;</code></p> <p><code>import org.slf4j.Logger;</code></p> <p><code>import org.slf4j.LoggerFactory;</code></p> <p><code> </code></p> <p><code>import com.adobe.granite.maintenance.MaintenanceConstants;</code></p> <p><code> </code></p> <p><code>@Component(metatype = true,</code></p> <p><code> label = "Delete Temp Files Maintenance Task",</code></p> <p><code> description = "Maintatence Task which deletes files from a configurable temporary directory which have been modified in the last 24 hours.")</code></p> <p><code>@Service</code></p> <p><code>@Properties({</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_NAME, value = "DeleteTempFilesTask", propertyPrivate = true),</code></p> <p><code> @Property(name = MaintenanceConstants.PROPERTY_TASK_TITLE, value = "Delete Temp Files", propertyPrivate = true),</code></p> <p><code> @Property(name = JobConsumer.PROPERTY_TOPICS, value = MaintenanceConstants.TASK_TOPIC_PREFIX</code></p> <p><code> + "DeleteTempFilesTask", propertyPrivate = true) })</code></p> <p><code>public class DeleteTempFilesTask implements JobExecutor {</code></p> <p><code> </code></p> <p><code> private static final Logger log = LoggerFactory.getLogger(DeleteTempFilesTask.class);</code></p> <p><code> </code></p> <p><code> @Property(label = "Temporary Directory", description="Temporary Directory. Defaults to the java.io.tmpdir system property.")</code></p> <p><code> private static final String PROP_TEMP_DIR = "temp.dir";</code></p> <p><code> </code></p> <p><code> private File tempDir;</code></p> <p><code> </code></p> <p><code> @Activate</code></p> <p><code> private void activate(Map&lt;string, object=""&gt; properties) {</code></p> <p><code> this.tempDir = new File(PropertiesUtil.toString(properties.get(PROP_TEMP_DIR),</code></p> <p><code> System.getProperty("java.io.tmpdir")));</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public JobExecutionResult process(Job job, JobExecutionContext context) {</code></p> <p><code> log.info("Deleting old temp files from {}.", tempDir.getAbsolutePath());</code></p> <p><code> Collection&lt;file&gt; files = FileUtils.listFiles(tempDir, new LastModifiedBeforeYesterdayFilter(),</code></p> <p><code> TrueFileFilter.INSTANCE);</code></p> <p><code> int counter = 0;</code></p> <p><code> for (File file : files) {</code></p> <p><code> log.debug("Deleting file {}.", file.getAbsolutePath());</code></p> <p><code> counter++;</code></p> <p><code> file.delete();</code></p> <p><code> // TODO - capture the output of delete() and do something useful with it</code></p> <p><code> }</code></p> <p><code> return context.result().message(String.format("Deleted %s files.", counter)).succeeded();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> /**</code></p> <p><code> * IOFileFilter which filters out files which have been modified in the last 24 hours.</code></p> <p><code> *</code></p> <p><code> */</code></p> <p><code> private static class LastModifiedBeforeYesterdayFilter implements IOFileFilter {</code></p> <p><code> </code></p> <p><code> private final long minTime;</code></p> <p><code> </code></p> <p><code> private LastModifiedBeforeYesterdayFilter() {</code></p> <p><code> Calendar cal = Calendar.getInstance();</code></p> <p><code> cal.add(Calendar.DATE, -1);</code></p> <p><code> this.minTime = cal.getTimeInMillis();</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File dir, String name) {</code></p> <p><code> // this method is never actually called.</code></p> <p><code> return false;</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code> @Override</code></p> <p><code> public boolean accept(File file) {</code></p> <p><code> return file.lastModified() <= this.minTime;</code></p> <p><code> }</code></p> <p><code> }</code></p> <p><code> </code></p> <p><code>}</code></p> <p><code>&lt;file&gt;&lt;/string,&gt;</code></p> <p> </p> </td>
  </tr>
 </tbody>
</table>

[experiencemanager-java-maintenance-ask-sample](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample)- [src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-maintenancetask-sample/blob/master/src/main/java/com/adobe/granite/samples/maintenance/impl/DeleteTempFilesTask.java)

Após a implantação do serviço, ele é exposto à interface do usuário do Painel de Operações. Você pode adicioná-lo a uma das programações de manutenção disponíveis:

![chlimage_1-127](assets/chlimage_1-127.png)

Isso adicionará um recurso correspondente em /apps/granite/operations/config/maintenance/`schedule`/`taskname`. Se a tarefa for dependente do modo de execução, a propriedade granite.operations.conditions.runmode precisará ser definida nesse nó com os valores dos runmodes que precisam estar ativos para esta tarefa de manutenção.

## Visão geral do sistema {#system-overview}

O **Painel Visão geral do sistema** exibe uma visão geral de alto nível da configuração, hardware e integridade da instância do AEM. Isso significa que o status de integridade do sistema é transparente e todas as informações são agregadas em um único painel.

>[!NOTE]
>
>Você também pode [assistir a este vídeo](https://video.tv.adobe.com/v/21340) para obter uma introdução ao Painel de visão geral do sistema.

### Como acessar {#how-to-access}

Para acessar o Painel Visão geral do sistema, navegue até **Ferramentas > Operações > Visão geral do sistema**.

![system_overview_dashboard](assets/system_overview_dashboard.png)

### Explicação do painel Visão geral do sistema {#system-overview-dashboard-explained}

A tabela abaixo descreve todas as informações exibidas no Painel de visão geral do sistema. Lembre-se de que quando não houver informações relevantes para mostrar (por exemplo, o backup não está em andamento, não há verificações de integridade críticas) a respectiva seção exibirá a mensagem &quot;Nenhuma entrada&quot;.

Também é possível baixar uma `JSON` arquivo que resume as informações do painel clicando no **Baixar** no canto superior direito do painel. `JSON` endpoint é `/libs/granite/operations/content/systemoverview/export.json` e pode ser usado em um `curl` script para monitoramento externo.

<table>
 <tbody>
  <tr>
   <td><strong>Seção</strong></td>
   <td><strong>Quais informações são exibidas</strong></td>
   <td><strong>Quando é crítico</strong></td>
   <td><strong>Links para</strong></td>
  </tr>
  <tr>
   <td>Verificações de integridade</td>
   <td>
    <ul>
     <li>uma lista de verificações que estão em estado Crítico</li>
     <li>uma lista de verificações que estão no status Warn</li>
    </ul> </td>
   <td>Indicado visualmente:<br />
    <ul>
     <li>uma marca vermelha para verificações Críticas</li>
     <li>uma tag laranja para as verificações de Aviso</li>
    </ul> </td>
   <td>
    <ul>
     <li>Página Relatórios de integridade</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tarefas de manutenção</td>
   <td>
    <ul>
     <li>uma lista de tarefas que falharam</li>
     <li>uma lista de tarefas que estão em execução no momento</li>
     <li>uma lista de tarefas que tiveram êxito na última execução</li>
     <li>uma lista de tarefas que nunca foram executadas</li>
     <li>uma lista de tarefas que não estão agendadas</li>
    </ul> </td>
   <td><p>Indicado visualmente:</p>
    <ul>
     <li>uma tag vermelha para tarefas com falha</li>
     <li>uma tag laranja para executar tarefas (pois elas podem afetar o desempenho)</li>
     <li>tags cinza para todos os outros status</li>
    </ul> </td>
   <td>
    <ul>
     <li>Página Tarefas de manutenção</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Sistema</td>
   <td>
    <ul>
     <li>sistema operacional e versão do sistema operacional (por exemplo, Mac OS X)</li>
     <li>média de carga do sistema, conforme recuperado de <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/OperatingSystemMXBean.html#getSystemLoadAverage--">OperatingSystemMXBeable</a></li>
     <li>espaço em disco (na partição onde o diretório inicial está localizado)</li>
     <li>heap máximo, como retornado por <a href="https://docs.oracle.com/javase/8/docs/api/java/lang/management/MemoryMXBean.html#getHeapMemoryUsage--">MemoryMXBean</a></li>
    </ul> </td>
   <td>N/A</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Instância</td>
   <td>
    <ul>
     <li>a versão AEM</li>
     <li>lista de modos de execução</li>
     <li>a data em que a instância foi iniciada</li>
    </ul> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Repositório</td>
   <td>
    <ul>
     <li>a versão Oak</li>
     <li>tipo de armazenamento de nó (Segment Tar ou Document)
      <ul>
       <li>se o tipo for documento, o tipo de armazenamento de documento será exibido (RDB ou Mongo)</li>
      </ul> </li>
     <li>se houver um armazenamento de dados personalizado:
      <ul>
       <li>para um Armazenamento de dados de arquivo, o caminho é exibido</li>
       <li>para um armazenamento de dados S3, o nome do bucket S3 é exibido</li>
       <li>para um armazenamento de dados S3 compartilhado, o nome do bucket S3 é exibido</li>
       <li>para um Data Store do Azure, o contêiner é exibido</li>
      </ul> </li>
     <li>se não houver um armazenamento de dados externo personalizado, uma mensagem indicando esse fato será exibida</li>
    </ul> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Agentes de distribuição</td>
   <td>
    <ul>
     <li>uma lista de agentes com filas bloqueadas</li>
     <li>uma lista de agentes mal configurados ("Erro de configuração")</li>
     <li>uma lista de agentes com processamento de fila pausado</li>
     <li>uma lista de agentes ociosos</li>
     <li>uma lista de agentes em execução (que estão processando entradas no momento)</li>
    </ul> </td>
   <td><p>Indicado visualmente:</p>
    <ul>
     <li>uma tag vermelha para agentes bloqueados ou erros de configuração</li>
     <li>uma tag laranja para agentes pausados</li>
     <li>uma tag cinza para agentes pausados, ociosos ou em execução<br /> </li>
    </ul> </td>
   <td>Página Distribuição<br /> </td>
  </tr>
  <tr>
   <td>Agentes de replicação</td>
   <td>
    <ul>
     <li>uma lista de agentes com filas bloqueadas</li>
     <li>uma lista de agentes ociosos</li>
     <li>uma lista de agentes em execução (que estão processando entradas no momento)</li>
    </ul> </td>
   <td><p>Indicado visualmente:<br /> </p>
    <ul>
     <li>uma marca vermelha para agentes bloqueados</li>
     <li>uma tag cinza para agentes pausados</li>
    </ul> </td>
   <td>Página Replicação</td>
  </tr>
  <tr>
   <td>Fluxos de trabalhos</td>
   <td>
    <ul>
     <li>Trabalhos do fluxo de trabalho:
      <ul>
       <li>número de tarefas de fluxo de trabalho com falha (se houver)</li>
       <li>número de trabalhos de fluxo de trabalho cancelados (se houver)</li>
      </ul> </li>
    </ul>
    <ul>
     <li>Contagens de workflow - número de workflows em um determinado status (se houver):
      <ul>
       <li>em execução</li>
       <li>Falha</li>
       <li>suspenso</li>
       <li>abortado</li>
      </ul> </li>
    </ul> <p>Para cada um dos status apresentados acima, é realizada uma query com um limite de 400 milissegundos. Em 400 milissegundos, o número de entradas obtidas até esse ponto é exibido.</p> </td>
   <td><p>Não interpretado:</p>
    <ul>
     <li>o usuário deve investigar quando há workflows e trabalhos em status inesperados.</li>
    </ul> </td>
   <td>Página Falhas do fluxo de trabalho</td>
  </tr>
  <tr>
   <td>Trabalhos Sling</td>
   <td><p>Contagens de tarefas Sling - número de tarefas em um determinado status (se houver):</p>
    <ul>
     <li>Falha</li>
     <li>em fila</li>
     <li>cancelado</li>
     <li>ativo</li>
    </ul> </td>
   <td><p>Não interpretado:</p>
    <ul>
     <li>o usuário deve investigar quando houver trabalhos em status inesperado ou com contagens altas.</li>
    </ul> </td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Contagens estimadas de nós</td>
   <td><p>Número estimado de:</p>
    <ul>
     <li>páginas</li>
     <li>ativos</li>
     <li>tags</li>
     <li>autorizáveis</li>
     <li>número total de nós<br /> </li>
    </ul> <p>O número total de nós é obtido a partir do nodeCounterMBean, enquanto o resto das estatísticas são obtidas a partir de IndexInfoService.</p> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Backup</td>
   <td>Exibe "Backup online em andamento", se for o caso.</td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Indexação</td>
   <td><p>Exibições:</p>
    <ul>
     <li>"Indexação em andamento"</li>
     <li>"Consulta em andamento"</li>
    </ul> <p>Se um encadeamento de indexação ou consulta estiver presente no despejo de encadeamento.</p> </td>
   <td>N/D</td>
   <td>N/D</td>
  </tr>
 </tbody>
</table>
