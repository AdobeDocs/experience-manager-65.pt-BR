---
title: Práticas recomendadas para monitorar [!DNL Assets] implantação
description: Práticas recomendadas para monitorar o ambiente e o desempenho de seu [!DNL Adobe Experience Manager] implantação após a implantação.
contentOwner: AG
role: Admin, Architect
feature: Asset Management
exl-id: a9e1bd6b-c768-4faa-99a3-7110693998dc
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---

# Práticas recomendadas para monitorar [!DNL Adobe Experience Manager Assets] implantação {#assets-monitoring-best-practices}

No [!DNL Experience Manager Assets] do ponto de vista do , o acompanhamento deve incluir a observação e a comunicação dos seguintes processos e tecnologias:

* CPU do sistema
* Uso da memória do sistema
* Tempo de espera de E/S do disco do sistema
* E/S de rede do sistema
* MBeans JMX para utilização de heap e processos assíncronos, como workflows
* Verificações de integridade do console OSGi

Normalmente, [!DNL Experience Manager Assets] pode ser monitorizado de duas formas, monitoramento ao vivo e monitoramento a longo prazo.

## Monitoramento ao vivo {#live-monitoring}

Você deve executar o monitoramento ao vivo durante a fase de teste de desempenho do seu desenvolvimento ou durante situações de alta carga para entender as características de desempenho do seu ambiente. Normalmente, o monitoramento ao vivo deve ser executado usando um conjunto de ferramentas. Estas são algumas recomendações:

* [VM visual](https://visualvm.github.io/): A VM visual permite que você visualize informações detalhadas da VM Java, incluindo uso da CPU, uso da memória Java. Além disso, ele permite que você exemplifique e avalie o código que é executado em uma implantação.
* [Topo](https://man7.org/linux/man-pages/man1/top.1.html): Top é um comando Linux que abre um painel, que exibe estatísticas de uso, incluindo CPU, memória e uso de E/S. Ele fornece uma visão geral de alto nível do que está acontecendo em uma instância.
* [Cabeça](https://hisham.hm/htop/): O Htop é um visualizador de processo interativo. Ele fornece uso detalhado da CPU e da memória, além do que o Top pode fornecer. O htop pode ser instalado na maioria dos sistemas Linux usando `yum install htop` ou `apt-get install htop`.

* Iotop: Iotop é um painel detalhado para uso de E/S de disco. Ele exibe barras e medidores que representam os processos que usam E/S de disco e a quantidade que eles usam. O Iotop pode ser instalado na maioria dos sistemas Linux usando `yum install iotop` ou `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/): O Iftop exibe informações detalhadas sobre o uso da rede/Ethernet. O ftop exibe as estatísticas por canal de comunicação nas entidades que usam ethernet e a quantidade de largura de banda que usam. O Iftop pode ser instalado na maioria dos sistemas Linux usando `yum install iftop` ou `apt-get install iftop`.

* Gravador de Voo Java (JFR): Uma ferramenta comercial do Oracle que pode ser usada gratuitamente em ambientes não relacionados à produção. Para obter mais detalhes, consulte [Como usar o Gravador de Voo Java para diagnosticar problemas de tempo de execução do CQ](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] `error.log` arquivo: Você pode investigar o [!DNL Experience Manager] `error.log` para obter detalhes de erros registrados no sistema. Use o comando `tail -F quickstart/logs/error.log` para identificar erros a serem investigados.
* [Console de fluxo de trabalho](/help/sites-administering/workflows.md): Aproveite o console do workflow para monitorar os workflows que ficam atrasados ou travados.

Normalmente, você usa essas ferramentas em conjunto para obter uma ideia abrangente sobre o desempenho de sua [!DNL Experience Manager] implantação.

>[!NOTE]
>
>Essas ferramentas são ferramentas padrão e não são suportadas diretamente pelo Adobe. Eles não exigem licenças adicionais.

![chlimage_1-33](assets/chlimage_1-143.png)

*Figura: Monitoramento ao vivo usando a ferramenta Visual VM.*

![chlimage_1-32](assets/chlimage_1-142.png)

## Monitorização a longo prazo {#long-term-monitoring}

Monitorização a longo prazo de um [!DNL Experience Manager] a implantação envolve o monitoramento por mais tempo das mesmas partes que são monitoradas ao vivo. Também inclui definir alertas específicos para o seu ambiente.

### Agregação de logs e relatórios {#log-aggregation-and-reporting}

Há várias ferramentas disponíveis para agregar logs, por exemplo Splunk(TM) e Elastic Search, Logstash e Kabana (ELK). Para avaliar o tempo de atividade de seu [!DNL Experience Manager] , é importante entender os eventos de log específicos do seu sistema e criar alertas com base neles. Um bom conhecimento das práticas de desenvolvimento e operações pode ajudá-lo a entender melhor como ajustar o processo de agregação de log para gerar alertas críticos.

### Monitoramento do ambiente {#environment-monitoring}

O monitoramento do ambiente inclui o monitoramento do seguinte:

* Taxa de transferência da rede
* E/S de disco
* Memória
* Utilização da CPU
* MBeans JMX
* Sites externos

Você precisa de ferramentas externas, como NewRelic(TM) e AppDynamics(TM) para monitorar cada item. Usando essas ferramentas, você pode definir alertas específicos para seu sistema, por exemplo, alta utilização do sistema, backup do fluxo de trabalho, falhas na verificação de integridade ou acesso não autenticado a seu site. O Adobe não recomenda ferramentas específicas sobre outras. Encontre a ferramenta que funciona para você e aproveite-a para monitorar os itens discutidos.

#### Monitoramento interno de aplicativos {#internal-application-monitoring}

O monitoramento interno de aplicativos inclui o monitoramento dos componentes do aplicativo que compõem a variável [!DNL Experience Manager] pilha, incluindo a JVM, o repositório de conteúdo e o monitoramento por meio do código de aplicativo personalizado criado na plataforma. Em geral, ele é executado por meio de Mbeans JMX que podem ser monitorados diretamente por muitas soluções de monitoramento populares, como SolarWinds (TM), HP OpenView(TM), Hyperic(TM), Zabbix(TM) e outras. Para sistemas que não suportam uma conexão direta com o JMX, você pode gravar scripts de shell para extrair os dados JMX e expô-los a esses sistemas em um formato que eles nativamente compreendem.

O acesso remoto ao JMX Mbeans não está habilitado por padrão. Para obter mais informações sobre o monitoramento por meio do JMX, consulte [Monitoramento e gerenciamento com a tecnologia JMX](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

Em muitos casos, é necessária uma linha de base para monitorar efetivamente uma estatística. Para criar uma linha de base, observe o sistema em condições normais de trabalho por um período predeterminado e identifique a métrica normal.

**Monitoramento da JVM**

Como em qualquer pilha de aplicativos baseada em Java, [!DNL Experience Manager] depende dos recursos que são fornecidos por meio da máquina virtual Java subjacente. Você pode monitorar o status de muitos desses recursos por meio de MXBeans da plataforma expostos pela JVM. Para obter mais informações sobre MXBeans, consulte [Uso do servidor MBean da plataforma e do MXBeans da plataforma](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

Estes são alguns parâmetros de linha de base que você pode monitorar para JVM:

Memória

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* Instâncias: Todos os servidores
* Limiar de alarme: Quando a utilização da memória heap ou não heap excede 75% da memória máxima correspondente.
* Definição do alarme: A memória do sistema é insuficiente ou há um vazamento de memória no código. Analise um despejo de thread para chegar a uma definição.

>[!NOTE]
>
>As informações fornecidas por esse bean são expressas em bytes.

Threads

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* Instâncias: Todos os servidores
* Limiar de alarme: Quando o número de threads é maior que 150% da linha de base.
* Definição do alarme: Existe um processo de execução ativo ou uma operação ineficiente consome uma grande quantidade de recursos. Analise um despejo de thread para chegar a uma definição.

**Monitorar[!DNL Experience Manager]**

[!DNL Experience Manager] O também expõe um conjunto de estatísticas e operações por meio do JMX. Eles podem ajudar a avaliar a integridade do sistema e identificar possíveis problemas antes que afetem os usuários. Para obter mais informações, consulte [documentação](/help/sites-administering/jmx-console.md) on [!DNL Experience Manager] MBeans JMX.

Estes são alguns parâmetros de linha de base que você pode monitorar para [!DNL Experience Manager]:

Agentes de replicação

* MBean: `com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* Instâncias: Um autor e todas as instâncias de publicação (para agentes de limpeza)
* Limiar de alarme: Quando o valor de `QueueBlocked` é `true` ou o valor de `QueueNumEntries` for superior a 150% da linha de base.

* Definição do alarme: Presença de uma fila bloqueada no sistema, indicando que o destino de replicação está inativo ou inacessível. Geralmente, problemas de rede ou infraestrutura fazem com que entradas excessivas sejam enfileiradas, o que pode afetar negativamente o desempenho do sistema.

>[!NOTE]
>
>Para os parâmetros MBean e URL, substitua `<AGENT_NAME>` com o nome do agente de replicação que você deseja monitorar.

Contador de sessões

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;OakRepository Statistics&quot;,type*=&quot;RepositoryStats&quot;
* Instâncias: Todos os servidores
* Limiar de alarme: Quando as sessões abertas excedem a linha de base em mais de 50%.
* Definição do alarme: As sessões podem ser abertas por meio de um pedaço de código e nunca fechar. Isso pode acontecer lentamente ao longo do tempo e eventualmente causar vazamentos de memória no sistema. Embora o número de sessões deva flutuar em um sistema, elas não devem aumentar continuamente.

Verificações de integridade

Verificações de integridade disponíveis no [painel de operações](/help/sites-administering/operations-dashboard.md#health-reports) têm MBeans JMX correspondentes para monitoramento. No entanto, você pode gravar verificações de integridade personalizadas para expor estatísticas adicionais do sistema.

Estas são algumas verificações de integridade prontas para uso que são úteis para monitorar:

* Verificações do sistema
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * Instâncias: Um autor, todos servidores de publicação
   * Limiar de alarme: Quando o status não estiver OK
   * Definição do alarme: O status de uma das métricas é AVISO ou CRÍTICO. Verifique o atributo log para obter mais informações sobre a causa do problema.

* Fila de replicação

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * Instâncias: Um autor, todos servidores de publicação
   * Limiar de alarme: Quando o status não estiver OK
   * Definição do alarme: O status de uma das métricas é AVISO ou CRÍTICO. Verifique o atributo de log para obter mais informações sobre a fila que causou o problema.

* Desempenho da resposta

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * Instâncias: Todos os servidores
   * Duração do alarme: Quando o status não estiver OK
   * Definição do alarme: O status de uma das métricas é AVISO ou CRÍTICO. Verifique o atributo de log para obter mais informações sobre a fila que causou o problema.

* Desempenho da consulta

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * Instâncias: Um autor, todos servidores de publicação
   * Limiar de alarme: Quando o status não estiver OK
   * Definição do alarme: Um ou mais queries sendo executados lentamente no sistema. Verifique o atributo log para obter mais informações sobre as consultas que causaram o problema.

* Grupos ativos

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * Instâncias: Todos os servidores
   * Limiar de alarme: Quando o status não estiver OK
   * Definição do alarme: Presença de pacotes OSGi inativos ou não resolvidos no sistema. Verifique o atributo log para obter mais informações sobre os pacotes que causaram o problema.

* Erros de log

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * Instâncias: Todos os servidores
   * Limiar de alarme: Quando o status não estiver OK
   * Definição do alarme: Há erros nos arquivos de log. Verifique o atributo log para obter mais informações sobre a causa do problema.

## Questões comuns e resoluções  {#common-issues-and-resolutions}

No processo de monitoramento, se você encontrar problemas, veja algumas tarefas de solução de problemas que você pode executar para resolver problemas comuns com o [!DNL Experience Manager] implantações:

* Se estiver usando TarMK, execute a compactação Tar com frequência. Para obter mais detalhes, consulte [Manter o repositório](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* Verificar `OutOfMemoryError` logs. Para obter mais informações, consulte [Analise problemas de memória](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html).

* Verifique os logs em busca de referências a consultas não indexadas, navegações em árvore ou navegações de índice. Elas indicam consultas não indexadas ou consultas indexadas inadequadamente. Para obter as práticas recomendadas sobre otimização do desempenho de consulta e indexação, consulte [Práticas recomendadas para consultas e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* Use o console do workflow para verificar se os workflows funcionam como esperado. Se possível, condensar vários workflows em um único workflow.
* Revise o monitoramento ao vivo e procure por gargalos adicionais ou grandes consumidores de recursos específicos.
* Investigue os pontos de saída da rede do cliente e a entrada aponta para o [!DNL Experience Manager] rede de implantação, incluindo o dispatcher. Frequentemente, essas são áreas de gargalo. Para obter mais informações, consulte [Considerações sobre a rede de ativos](/help/assets/assets-network-considerations.md).
* Dimensione [!DNL Experience Manager] servidor. Pode ter um tamanho inadequado [!DNL Experience Manager] implantação. O Suporte ao cliente do Adobe pode ajudar você a identificar se o servidor está com menos tamanho.
* Examine a `access.log` e `error.log` os arquivos para entradas no momento em que algo deu errado. Procure padrões que podem indicar anomalias de código personalizado. Adicione-os à lista de eventos que você monitorar.
