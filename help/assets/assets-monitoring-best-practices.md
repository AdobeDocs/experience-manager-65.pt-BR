---
title: 'Práticas recomendadas para monitorar a implantação de  [!DNL Assets] '
description: Práticas recomendadas para monitorar o ambiente e o desempenho da sua implantação  [!DNL Adobe Experience Manager] após a implantação.
contentOwner: AG
role: Admin, Architect
feature: Gerenciamento de ativos
exl-id: a9e1bd6b-c768-4faa-99a3-7110693998dc
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---

# Práticas recomendadas para monitorar a implantação de [!DNL Adobe Experience Manager Assets] {#assets-monitoring-best-practices}

Do ponto de vista [!DNL Experience Manager Assets], o monitoramento deve incluir a observação e o relatório dos seguintes processos e tecnologias:

* CPU do sistema
* Uso da memória do sistema
* Tempo de espera de E/S do disco do sistema
* E/S de rede do sistema
* MBeans JMX para utilização de heap e processos assíncronos, como workflows
* Verificações de integridade do console OSGi

Normalmente, [!DNL Experience Manager Assets] pode ser monitorado de duas formas, monitoramento ao vivo e monitoramento de longo prazo.

## Monitoramento ao vivo {#live-monitoring}

Você deve executar o monitoramento ao vivo durante a fase de teste de desempenho do seu desenvolvimento ou durante situações de alta carga para entender as características de desempenho do seu ambiente. Normalmente, o monitoramento ao vivo deve ser executado usando um conjunto de ferramentas. Estas são algumas recomendações:

* [VM](https://visualvm.github.io/) visual: A VM visual permite que você visualize informações detalhadas da VM Java, incluindo uso da CPU, uso da memória Java. Além disso, ele permite que você exemplifique e avalie o código que é executado em uma implantação.
* [Parte superior](https://man7.org/linux/man-pages/man1/top.1.html): Top é um comando Linux que abre um painel, que exibe estatísticas de uso, incluindo CPU, memória e uso de E/S. Ele fornece uma visão geral de alto nível do que está acontecendo em uma instância.
* [Cabeça](https://hisham.hm/htop/): O Htop é um visualizador de processo interativo. Ele fornece uso detalhado da CPU e da memória, além do que o Top pode fornecer. O htop pode ser instalado na maioria dos sistemas Linux usando `yum install htop` ou `apt-get install htop`.

* Iotop: Iotop é um painel detalhado para uso de E/S de disco. Ele exibe barras e medidores que representam os processos que usam E/S de disco e a quantidade que eles usam. O Iotop pode ser instalado na maioria dos sistemas Linux usando `yum install iotop` ou `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/): O Iftop exibe informações detalhadas sobre o uso da rede/Ethernet. O ftop exibe as estatísticas por canal de comunicação nas entidades que usam ethernet e a quantidade de largura de banda que usam. O Iftop pode ser instalado na maioria dos sistemas Linux usando `yum install iftop` ou `apt-get install iftop`.

* Gravador de Voo Java (JFR): Uma ferramenta comercial do Oracle que pode ser usada gratuitamente em ambientes não relacionados à produção. Para obter mais detalhes, consulte [Como usar o Gravador de Voo Java para Diagnosticar problemas de tempo de execução do CQ](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] `error.log` arquivo: Você pode investigar o  [!DNL Experience Manager] `error.log` arquivo para obter detalhes dos erros registrados no sistema. Use o comando `tail -F quickstart/logs/error.log` para identificar erros a serem investigados.
* [Console](/help/sites-administering/workflows.md) de fluxo de trabalho: Aproveite o console do workflow para monitorar os workflows que ficam atrasados ou travados.

Normalmente, você usa essas ferramentas em conjunto para obter uma ideia abrangente sobre o desempenho de sua implantação [!DNL Experience Manager].

>[!NOTE]
>
>Essas ferramentas são ferramentas padrão e não são suportadas diretamente pelo Adobe. Eles não exigem licenças adicionais.

![chlimage_1-33](assets/chlimage_1-143.png)

*Figura: Monitoramento ao vivo usando a ferramenta Visual VM.*

![chlimage_1-32](assets/chlimage_1-142.png)

## Monitorização a longo prazo {#long-term-monitoring}

O monitoramento de longo prazo de uma implantação [!DNL Experience Manager] envolve o monitoramento por um período mais longo das mesmas partes que são monitoradas ao vivo. Também inclui definir alertas específicos para o seu ambiente.

### Agregação de logs e relatórios {#log-aggregation-and-reporting}

Há várias ferramentas disponíveis para agregar logs, por exemplo Splunk(TM) e Elastic Search, Logstash e Kabana (ELK). Para avaliar o tempo de atividade da sua implantação [!DNL Experience Manager], é importante entender os eventos de log específicos ao seu sistema e criar alertas com base neles. Um bom conhecimento das práticas de desenvolvimento e operações pode ajudá-lo a entender melhor como ajustar o processo de agregação de log para gerar alertas críticos.

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

O monitoramento interno de aplicativos inclui o monitoramento dos componentes do aplicativo que compõem a pilha [!DNL Experience Manager], incluindo a JVM, o repositório de conteúdo e o monitoramento por meio do código de aplicativo personalizado criado na plataforma. Em geral, ele é executado por meio de Mbeans JMX que podem ser monitorados diretamente por muitas soluções de monitoramento populares, como SolarWinds (TM), HP OpenView(TM), Hyperic(TM), Zabbix(TM) e outras. Para sistemas que não suportam uma conexão direta com o JMX, você pode gravar scripts de shell para extrair os dados JMX e expô-los a esses sistemas em um formato que eles nativamente compreendem.

O acesso remoto ao JMX Mbeans não está habilitado por padrão. Para obter mais informações sobre o monitoramento por meio do JMX, consulte [Monitoramento e gerenciamento usando a tecnologia JMX](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

Em muitos casos, é necessária uma linha de base para monitorar efetivamente uma estatística. Para criar uma linha de base, observe o sistema em condições normais de trabalho por um período predeterminado e identifique a métrica normal.

**Monitoramento da JVM**

Assim como em qualquer pilha de aplicativos baseada em Java, [!DNL Experience Manager] depende dos recursos que são fornecidos a ela por meio da máquina virtual Java subjacente. Você pode monitorar o status de muitos desses recursos por meio de MXBeans da plataforma expostos pela JVM. Para obter mais informações sobre MXBeans, consulte [Usando o Servidor MBean de plataforma e o MXBeans](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html) de plataforma.

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

[!DNL Experience Manager] também expõe um conjunto de estatísticas e operações por meio do JMX. Eles podem ajudar a avaliar a integridade do sistema e identificar possíveis problemas antes que afetem os usuários. Para obter mais informações, consulte a [documentação](/help/sites-administering/jmx-console.md) em [!DNL Experience Manager] MBeans JMX.

Estes são alguns parâmetros de linha de base que você pode monitorar para [!DNL Experience Manager]:

Agentes de replicação

* MBean: `com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>”`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>"`
* Instâncias: Um autor e todas as instâncias de publicação (para agentes de limpeza)
* Limiar de alarme: Quando o valor de `QueueBlocked` for `true` ou o valor de `QueueNumEntries` for maior que 150% da linha de base.

* Definição do alarme: Presença de uma fila bloqueada no sistema, indicando que o destino de replicação está inativo ou inacessível. Geralmente, problemas de rede ou infraestrutura fazem com que entradas excessivas sejam enfileiradas, o que pode afetar negativamente o desempenho do sistema.

>[!NOTE]
>
>Para os parâmetros MBean e URL, substitua `<AGENT_NAME>` pelo nome do agente de replicação que deseja monitorar.

Contador de sessões

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;Estatísticas OakRepository&quot;,type*=&quot;RepositoryStats&quot;
* Instâncias: Todos os servidores
* Limiar de alarme: Quando as sessões abertas excedem a linha de base em mais de 50%.
* Definição do alarme: As sessões podem ser abertas por meio de um pedaço de código e nunca fechar. Isso pode acontecer lentamente ao longo do tempo e eventualmente causar vazamentos de memória no sistema. Embora o número de sessões deva flutuar em um sistema, elas não devem aumentar continuamente.

Verificações de integridade

As verificações de integridade disponíveis no [painel de operações](/help/sites-administering/operations-dashboard.md#health-reports) têm MBeans JMX correspondentes para monitoramento. No entanto, você pode gravar verificações de integridade personalizadas para expor estatísticas adicionais do sistema.

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

No processo de monitoramento, se encontrar problemas, veja algumas tarefas de solução de problemas que você pode executar para resolver problemas comuns com implantações de [!DNL Experience Manager]:

* Se estiver usando TarMK, execute a compactação Tar com frequência. Para obter mais detalhes, consulte [Manter o repositório](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* Verifique os registros `OutOfMemoryError`. Para obter mais informações, consulte [Analisar problemas de memória](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html).

* Verifique os logs em busca de referências a consultas não indexadas, navegações em árvore ou navegações de índice. Elas indicam consultas não indexadas ou consultas indexadas inadequadamente. Para obter as práticas recomendadas sobre otimização do desempenho de consulta e indexação, consulte [Práticas recomendadas para consultas e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* Use o console do workflow para verificar se os workflows funcionam como esperado. Se possível, condensar vários workflows em um único workflow.
* Revise o monitoramento ao vivo e procure por gargalos adicionais ou grandes consumidores de recursos específicos.
* Investigue os pontos de saída da rede do cliente e a entrada aponta para a rede de implantação [!DNL Experience Manager], incluindo o dispatcher. Frequentemente, essas são áreas de gargalo. Para obter mais informações, consulte [Considerações de rede do Assets](/help/assets/assets-network-considerations.md).
* Aumente o tamanho do servidor [!DNL Experience Manager]. Você pode ter um tamanho inadequado para sua implantação [!DNL Experience Manager]. O Atendimento ao cliente do Adobe pode ajudá-lo a identificar se o servidor está abaixo do tamanho.
* Examine os arquivos `access.log` e `error.log` para entradas no momento em que algo deu errado. Procure padrões que podem indicar anomalias de código personalizado. Adicione-os à lista de eventos que você monitorar.
