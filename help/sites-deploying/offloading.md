---
title: Descarregamento de trabalhos
description: Saiba como configurar e usar instâncias de AEM em uma topologia para executar tipos específicos de processamento.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 429c96ff-4185-4215-97e8-9bd2c130a9b1
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '2317'
ht-degree: 1%

---

# Descarregamento de trabalhos{#offloading-jobs}

## Introdução {#introduction}

A descarga distribui tarefas de processamento entre instâncias de Experience Manager em uma topologia. Com a descarga, você pode usar instâncias de Experience Manager específicas para executar tipos específicos de processamento. O processamento especializado permite maximizar o uso dos recursos disponíveis do servidor.

A descarga é baseada na variável [Apache Sling Discovery](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) e Sling JobManager. Para usar a descarga, você adiciona clusters de Experience Manager a uma topologia e identifica os tópicos de trabalho que o cluster processa. Os clusters são compostos de uma ou mais instâncias de Experience Manager, de modo que uma única instância é considerada um cluster.

Para obter informações sobre como adicionar instâncias a uma topologia, consulte [Administração de topologias](/help/sites-deploying/offloading.md#administering-topologies).

### Distribuição de tarefas {#job-distribution}

O Sling JobManager e o JobConsumer permitem a criação de trabalhos processados em uma topologia:

* JobManager: um serviço que cria processos para tópicos específicos.
* JobConsumer: um serviço que executa processos de um ou mais tópicos. Vários serviços JobConsumer podem ser registrados para o mesmo tópico.

Quando o JobManager cria um job, a estrutura de Descarregamento seleciona um cluster de Experience Manager na topologia para executar o job:

* O cluster deve incluir uma ou mais instâncias que estejam executando um JobConsumer registrado para o tópico de trabalho.
* O tópico deve ser ativado para pelo menos uma instância no cluster.

Consulte [Configuração do Consumo de Tópico](/help/sites-deploying/offloading.md#configuring-topic-consumption) para obter informações sobre como refinar a distribuição de jobs.

![chlimage_1-109](assets/chlimage_1-109.png)

Quando a estrutura de descarregamento seleciona um cluster para executar um trabalho e o cluster é composto por várias instâncias, a Distribuição de sling determina qual instância no cluster executa o trabalho.

### Cargas de trabalho {#job-payloads}

A estrutura de descarregamento suporta cargas de trabalho que associam trabalhos a recursos no repositório. As cargas de trabalho são úteis quando os trabalhos são criados para recursos de processamento e o trabalho é descarregado em outro computador.

Após a criação de um trabalho, é garantido que a carga esteja localizada apenas na instância que cria o trabalho. Ao descarregar o trabalho, os agentes de replicação garantem que a carga seja criada na instância que eventualmente consome o trabalho. Quando a execução do job é concluída, a replicação reversa faz com que a carga seja copiada de volta para a instância que criou o job.

## Administração de topologias {#administering-topologies}

As topologias são clusters de Experience Manager livremente acoplados que estão participando da descarga. Um cluster consiste em uma ou mais instâncias do servidor Experience Manager (uma única instância é considerada um cluster).

Cada instância do Experience Manager executa os seguintes serviços relacionados à descarga:

* Serviço Descoberta: envia solicitações a um Conector de Topologia para ingressar na topologia.
* Conector de topologia: recebe as solicitações de associação e aceita ou recusa cada solicitação.

O Serviço de Descoberta de todos os membros da topologia apontam para o Conector de Topologia em um dos membros. Nas seções seguintes, esse membro é chamado de membro raiz.

![chlimage_1-110](assets/chlimage_1-110.png)

Cada cluster na topologia contém uma instância reconhecida como líder. O líder do cluster interage com a topologia em nome dos outros membros do cluster. Quando o líder deixa o cluster, um novo líder para o cluster é escolhido automaticamente.

### Exibindo a Topologia {#viewing-the-topology}

Use o Navegador de Topologia para explorar o estado da topologia em que a instância Experience Manager está participando. O Navegador de Topologia mostra os clusters e as instâncias da topologia.

Para cada cluster, você verá uma lista de membros do cluster que indica a ordem em que cada membro se associou ao cluster e qual membro é o Líder. A propriedade Current indica a instância que você está administrando no momento.

Para cada instância do cluster, você pode ver várias propriedades relacionadas à topologia:

* Uma lista de permissões de tópicos para o consumidor de jobs da instância.
* Os pontos de extremidade expostos para conexão com a topologia.
* Os tópicos de trabalho para os quais a instância está registrada para descarregamento.
* Os tópicos de job que a instância processa.

1. Usando a interface para toque, clique na guia Ferramentas. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. Na área Operações do Granite, clique em Descarregamento de navegador.
1. No painel de navegação, clique em Navegador de Topologia.

   Os clusters que estão participando da topologia são exibidos.

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. Clique em um cluster para ver uma lista das instâncias no cluster e seus status ID, Status atual e Líder.
1. Clique em uma ID de instância para ver propriedades mais detalhadas.

Você também pode usar a Console da Web para exibir informações de topologia. O console fornece mais informações sobre os clusters de topologia:

* Qual instância é a instância local.
* Os serviços do Conector de Topologia que esta instância usa para se conectar à topologia (saída) e os serviços que se conectam a esta instância (entrada).
* Altere o histórico da topologia e as propriedades da instância.

Use o procedimento a seguir para abrir a página Gerenciamento de Topologia da Console Web:

1. Abra o Console da Web no navegador. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Clique em Principal > Gerenciamento de Topologia.

   ![chlimage_1-112](assets/chlimage_1-112.png)

### Configuração de associação de topologia {#configuring-topology-membership}

O Apache Sling Resource-Based Discovery Service é executado em cada instância para controlar como as instâncias Experience Manager interagem com uma topologia.

O Serviço de Descoberta envia solicitações de POST periódicas (heartbeats) aos serviços do Conector de Topologia para estabelecer e manter conexões com a topologia. O serviço do Conector de topologia mantém uma lista de permissões de endereços IP ou nomes de host que têm permissão para ingressar na topologia:

* Para unir uma instância a uma topologia, especifique o URL do serviço do Conector de Topologia do membro raiz.
* Para permitir que uma instância ingresse em uma topologia, adicione-a à lista de permissões do serviço Conector de Topologia do membro raiz.

Use o Console da Web ou um nó sling:OsgiConfig para configurar as seguintes propriedades do serviço org.apache.sling.discovery.impt.Config:

<table>
 <tbody>
  <tr>
   <th>Nome de propriedade</th>
   <th>Nome OSGi</th>
   <th>Descrição</th>
   <th>Valor padrão</th>
  </tr>
  <tr>
   <td>Tempo limite do Heartbeat (segundos)</td>
   <td>heartbeatTimeout</td>
   <td>O tempo em segundos para aguardar uma resposta de heartbeat antes que a instância direcionada seja considerada indisponível. </td>
   <td>20</td>
  </tr>
  <tr>
   <td>Intervalo do Heartbeat (segundos)</td>
   <td>heartbeatInterval</td>
   <td>A quantidade de tempo em segundos entre as pulsações.</td>
   <td>15</td>
  </tr>
  <tr>
   <td>Atraso mínimo do evento (segundos)</td>
   <td>minEventDelay</td>
   <td><p>Quando ocorre uma alteração na topologia, o tempo necessário para atrasar a alteração de estado de TOPOLOGY_CHANGING para TOPOLOGY_CHANGED. Cada alteração que ocorre quando o estado é TOPOLOGY_CHANGING aumenta o atraso nessa quantidade de tempo.</p> <p>Esse atraso impede que os ouvintes sejam inundados por eventos. </p> <p>Para não usar atraso, especifique 0 ou um número negativo.</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>URLs do Conector de Topologia</td>
   <td>topologyConnectorUrls</td>
   <td>Os URLs dos serviços do Conector de Topologia para enviar mensagens de heartbeat.</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>Lista de permissões do Conector de Topologia</td>
   <td>topologyConnectorWhitelist</td>
   <td>A lista de endereços IP ou nomes de host permitidos pelo serviço do Conector de Topologia local na topologia. </td>
   <td><p>localhost</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>Nome do descritor de repositório</td>
   <td>leaderElectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;no value&gt;</td>
  </tr>
 </tbody>
</table>

Use o procedimento a seguir para conectar uma instância do CQ ao membro raiz de uma topologia. O procedimento aponta a instância para o URL do Conector de Topologia do membro da topologia raiz. Execute este procedimento em todos os membros da topologia.

1. Abra o Console da Web no navegador. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Clique em Principal > Gerenciamento de Topologia.
1. Clique em Configurar Serviço de Descoberta.
1. Adicione um item à propriedade URLs do Conector de Topologia e especifique o URL do serviço do Conector de Topologia do membro da topologia raiz. A URL está no formato https://rootservername:4502/libs/sling/topology/connector.

Execute o procedimento a seguir no membro raiz da topologia. O procedimento adiciona os nomes dos outros membros da topologia à sua lista de permissões do Serviço de Descoberta.

1. Abra o Console da Web no navegador. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Clique em Principal > Gerenciamento de Topologia.
1. Clique em Configurar Serviço de Descoberta.
1. Para cada membro da topologia, adicione um item à propriedade de lista de permissões do Conector de Topologia e especifique o nome do host ou o endereço IP do membro da topologia.

## Configuração do Consumo de Tópico {#configuring-topic-consumption}

Use o Offloading Browser para configurar o consumo de tópicos para as instâncias de Experience Manager na topologia. Para cada instância, você pode especificar os tópicos que ela consome. Por exemplo, para configurar sua topologia para que apenas uma instância consuma tópicos de um tipo específico, desative o tópico em todas as instâncias, exceto uma.

Os processos são distribuídos entre instâncias que têm o tópico associado ativado usando a lógica de revezamento.

1. Usando a interface para toque, clique na guia Ferramentas. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. Na área Operações do Granite, clique em Descarregamento de navegador.
1. No painel de navegação, clique em Descarregamento de navegador.

   Os tópicos de descarga e as instâncias do servidor que podem consumir os tópicos são exibidos.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. Para desativar o consumo de um tópico para uma instância, abaixo do nome do tópico, clique em Desativar ao lado da instância.
1. Para configurar todo o consumo de tópico para uma instância, clique no identificador de instância abaixo de qualquer tópico.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. Clique em um dos seguintes botões ao lado de um tópico para configurar o comportamento de consumo da instância e, em seguida, clique em Salvar:

   * Ativado: Essa instância consome jobs desse tópico.
   * Desativado: essa instância não consome tarefas desse tópico.
   * Exclusivo: essa instância consome trabalhos somente deste tópico.

   **Nota:** Quando você seleciona Exclusivo para um tópico, todos os outros tópicos são automaticamente definidos como Desativado.

### Consumidores de Trabalho Instalados {#installed-job-consumers}

Várias implementações do JobConsumer são instaladas com o Experience Manager. Os tópicos para os quais esses Consumidores de trabalho estão registrados aparecem em Descarregamento de navegador. Tópicos adicionais exibidos são aqueles que os Consumidores de trabalho personalizados registraram. A tabela a seguir descreve os JobConsumers padrão.

| Tópico de trabalho | PID do serviço | Descrição |
|---|---|---|
| / | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | Instalado com o Apache Sling. Processa trabalhos gerados pelo administrador de eventos OSGi para oferecer compatibilidade com versões anteriores. |
| com/day/cq/replication/job/&amp;ast; | com.day.cq.replication.impl.AgentManagerImpl | Um agente de replicação que replica cargas de trabalho. |

<!--
| com/adobe/granite/workflow/offloading |com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer |Processes jobs that the DAM Update Asset Offloader workflow generates. |
-->

### Desativando e Ativando Tópicos para uma Instância {#disabling-and-enabling-topics-for-an-instance}

O serviço Apache Sling Job Consumer Manager fornece lista de permissões de tópico e propriedades de lista de bloqueios. Configure essas propriedades para ativar ou desativar o processamento de tópicos específicos em uma instância de Experience Manager.

**Nota:** Se a instância pertencer a uma topologia, você também poderá usar o Descarregamento de Navegador em qualquer computador da topologia para ativar ou desativar tópicos.

A lógica que cria a lista de tópicos ativados permite primeiro todos os tópicos que estão na lista de permissões e, em seguida, remove os tópicos que estão na lista de bloqueios. Por padrão, todos os tópicos são ativados (o valor da lista de permissões é `*`) e nenhum tópico está desativado (a lista de bloqueios não tem valor).

Use o Console da Web ou um `sling:OsgiConfig` para configurar as seguintes propriedades. Para `sling:OsgiConfig` nós, o PID do serviço Gerenciador de Consumidores de Jobs é org.apache.sling.event.impl.jobs.JobConsumerManager.

| Nome da propriedade no Console da Web | ID OSGi | Descrição |
|---|---|---|
| Lista de permissões de tópico | job.consumermanager.whitelist | Uma lista de tópicos que o serviço JobManager local processa. O valor padrão de &amp;ast; faz com que todos os tópicos sejam enviados para o serviço TopicConsumer registrado. |
| Lista de bloqueios de tópico | job.consumermanager.blacklist | Uma lista de tópicos que o serviço JobManager local não processa. |

## Criação De Agentes De Replicação Para Descarregamento {#creating-replication-agents-for-offloading}

A estrutura de descarregamento usa replicação para transportar recursos entre o autor e o trabalhador. A estrutura de descarga cria agentes de replicação automaticamente quando as instâncias se associam à topologia. Os agentes são criados com valores padrão. Altere manualmente a senha que os agentes usam para autenticação.

>[!CAUTION]
>
>Um problema conhecido com os agentes de replicação gerados automaticamente requer a criação manual de novos agentes de replicação.

Crie os agentes de replicação que transportam cargas de trabalho entre instâncias para descarregamento. A ilustração a seguir mostra os agentes necessários para descarregar do autor para uma instância de trabalho. O autor tem uma Sling ID de 1 e a instância do trabalhador tem uma Sling ID de 2:

![chlimage_1-115](assets/chlimage_1-115.png)

Essa configuração exige os três agentes a seguir:

1. Um agente de saída na instância do autor que é replicado para a instância do trabalhador.
1. Um agente reverso na instância do autor que extrai da caixa de saída na instância do trabalhador.
1. Um agente de caixa de saída na instância do trabalhador.

Esse esquema de replicação é semelhante ao usado entre as instâncias de autor e de publicação. No entanto, para a situação de descarregamento, todas as instâncias envolvidas são instâncias de criação.

>[!NOTE]
>
>A estrutura de descarregamento usa a topologia para obter os endereços IP das instâncias de descarregamento. Em seguida, a estrutura cria automaticamente os agentes de replicação com base nesses endereços IP. Se os endereços IP das instâncias de descarregamento forem alterados posteriormente, a alteração será propagada automaticamente na topologia após a reinicialização da instância. No entanto, a estrutura de descarga não atualiza automaticamente os agentes de replicação para refletir os novos endereços IP. Para evitar essa situação, use endereços IP fixos para todas as instâncias na topologia.

### Nomear os agentes de replicação para descarga {#naming-the-replication-agents-for-offloading}

Use um formato específico para o ***Nome*** dos agentes de replicação para que a estrutura de descarga use automaticamente o agente correto para instâncias de trabalho específicas.

**Nomear o agente de saída na instância do autor:**

`offloading_<slingid>`, onde `<slingid>` é a Sling ID da instância do trabalhador.

Exemplo: `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**Nomear o agente reverso na instância do autor:**

`offloading_reverse_<slingid>`, onde `<slingid>` é a Sling ID da instância do trabalhador.

Exemplo: `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**Nomear a caixa de saída na instância do trabalhador:**

`offloading_outbox`

### Criando o agente de saída {#creating-the-outgoing-agent}

1. Criar um **Agente de replicação** no autor. (Consulte a [documentação dos agentes de replicação](/help/sites-deploying/replication.md)). Especifique qualquer **Título**. A variável **Nome** deve seguir a convenção de nomenclatura.
1. Crie o agente usando as seguintes propriedades:

   | Propriedade | Valor |
   |---|---|
   | Configurações > Tipo de serialização | Padrão |
   | Transporte >URI de transporte | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | Transporte >Transporte de usuário | Usuário de replicação na instância de destino |
   | Transporte >Senha de Transporte | Senha do usuário de replicação na instância de destino |
   | Estendido > Método HTTP | POST |
   | Acionadores > Ignorar padrão | Verdadeiro |

### Criação do agente reverso {#creating-the-reverse-agent}

1. Criar um **Reverter agente de replicação** no autor. (Consulte a [documentação dos agentes de replicação](/help/sites-deploying/replication.md).) Especifique qualquer **Título**. A variável **Nome** deve seguir a convenção de nomenclatura.
1. Crie o agente usando as seguintes propriedades:

   | Propriedade | Valor |
   |---|---|
   | Configurações > Tipo de serialização | Padrão |
   | Transporte >URI de transporte | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | Transporte >Transporte de usuário | Usuário de replicação na instância de destino |
   | Transporte >Senha de Transporte | Senha do usuário de replicação na instância de destino |
   | Estendido > Método HTTP | GET |

### Criação do agente de caixa de saída {#creating-the-outbox-agent}

1. Criar um **Agente de replicação** na instância do trabalhador. (Consulte a [documentação dos agentes de replicação](/help/sites-deploying/replication.md).) Especifique qualquer **Título**. A variável **Nome** deve ser `offloading_outbox`.
1. Crie o agente usando as propriedades a seguir.

   | Propriedade | Valor |
   |---|---|
   | Configurações > Tipo de serialização | Padrão |
   | Transporte >URI de transporte | repo://var/replication/outbox |
   | Acionar > Ignorar padrão | Verdadeiro |

### Encontrar a ID do Sling {#finding-the-sling-id}

Obtenha a Sling ID de uma instância do Experience Manager usando um dos seguintes métodos:

* Abra o Console da Web e, nas Configurações do Sling, localize o valor da propriedade ID do Sling ([http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings)). Esse método é útil se a instância ainda não fizer parte da topologia.
* Use o navegador de Topologia se a instância já fizer parte da topologia.

<!--
## Offloading the Processing of DAM Assets {#offloading-the-processing-of-dam-assets}

Configure the instances of a topology so that specific instances perform the background processing of assets that are added or updated in DAM.

By default, Experience Manager executes the [!UICONTROL DAM Update Asset] workflow when a DAM asset changes or one is added to DAM. Change the default behavior so that Experience Manager instead executes the [!UICONTROL DAM Update Asset Offloader] workflow. This workflow generates a JobManager job that has a topic of `com/adobe/granite/workflow/offloading`. Then, configure the topology so that the job is offloaded to a dedicated worker.

>[!CAUTION]
>
>No workflow should be transient when used with workflow offloading. For example, the [!UICONTROL DAM Update Asset] workflow must not be transient when used for asset offloading. To set/unset the transient flag on a workflow, see [Transient Workflows](/help/assets/performance-tuning-guidelines.md#workflows).

The following procedure assumes the following characteristics for the offloading topology:

* One or more Experience Manager instance are authoring instances that users interact with for adding or updating DAM assets.
* Users to do not directly interact with one or more Experience Manager instances that process the DAM assets. These instances are dedicated to the background processing of DAM assets.

1. On each Experience Manager instance, configure the Discovery Service so that it points to the root Topography Connector. (See [Configuring Topology Membership](#title4).)
1. Configure the root Topography Connector so that the connecting instances are on the allow list.
1. Open Offloading Browser and disable the `com/adobe/granite/workflow/offloading` topic on the instances with which users interact to upload or change DAM assets.

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. On each instance that users interact with to upload or change DAM assets, configure workflow launchers to use the [!UICONTROL DAM Update Asset Offloading] workflow:

    1. Open the Workflow console.
    1. Click the Launcher tab.
    1. Locate the two Launcher configurations that execute the [!UICONTROL DAM Update Asset] workflow. One launcher configuration event type is Node Created, and the other type is Node Modified.
    1. Change both event types so that they execute the [!UICONTROL DAM Update Asset Offloading] workflow. (For information about launcher configurations, see [Starting Workflows When Nodes Change](/help/sites-administering/workflows-starting.md).)

1. On the instances that perform the background processing of DAM assets, disable the workflow launchers that execute the [!UICONTROL DAM Update Asset] workflow.
-->

## Leitura adicional {#further-reading}

Além dos detalhes apresentados nesta página, você também pode ler o seguinte:

* Para obter informações sobre como usar APIs Java para criar jobs e consumidores de jobs, consulte [Criando e Consumindo Jobs para Descarregamento](/help/sites-developing/dev-offloading.md).
