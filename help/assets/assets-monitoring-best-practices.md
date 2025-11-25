---
title: 'Práticas recomendadas para monitorar a implantação [!DNL Assets] '
description: Práticas recomendadas para monitorar o ambiente e o desempenho da sua implantação [!DNL Adobe Experience Manager] após sua implantação.
contentOwner: AG
role: Admin, Developer
feature: Asset Management
exl-id: a9e1bd6b-c768-4faa-99a3-7110693998dc
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1638'
ht-degree: 0%

---

# Práticas recomendadas para monitorar a implantação do [!DNL Adobe Experience Manager Assets] {#assets-monitoring-best-practices}

Do ponto de vista do [!DNL Experience Manager Assets], o monitoramento deve incluir a observação e os relatórios dos seguintes processos e tecnologias:

* CPU do sistema
* Uso da memória do sistema
* Tempo de espera de E/S e disco do sistema
* E/S de rede do sistema
* MBeans JMX para utilização de heap e processos assíncronos, como workflows
* Verificações de integridade do console OSGi

Normalmente, o [!DNL Experience Manager Assets] pode ser monitorado de duas maneiras: monitoramento em tempo real e monitoramento de longo prazo.

## Monitoramento em tempo real {#live-monitoring}

Você deve executar o monitoramento em tempo real durante a fase de teste de desempenho do seu desenvolvimento ou durante situações de alta carga para entender as características de desempenho do seu ambiente. Normalmente, o monitoramento em tempo real deve ser executado usando um conjunto de ferramentas. Estas são algumas recomendações:

* [Visual VM](https://visualvm.github.io/): o Visual VM permite exibir informações detalhadas do Java VM, incluindo uso do CPU, uso da memória Java. Além disso, permite a amostragem e a avaliação do código executado em uma implantação.
* [Superior](https://man7.org/linux/man-pages/man1/top.1.html): Superior é um comando do Linux que abre um painel, que exibe estatísticas de uso, incluindo CPU, memória e uso de E/S. Ele fornece uma visão geral de alto nível do que está acontecendo em uma instância.
* [Htop](https://hisham.hm/htop/): o Htop é um visualizador de processos interativo. Ele fornece uso detalhado de CPU e memória além do que o Top pode fornecer. O Htop pode ser instalado na maioria dos sistemas Linux usando `yum install htop` ou `apt-get install htop`.

* Iotop: Iotop é um painel detalhado para uso de E/S de disco. Ele exibe barras e medidores que descrevem os processos que usam E/S de disco e a quantidade que eles usam. O Iotop pode ser instalado na maioria dos sistemas Linux usando `yum install iotop` ou `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/): o Iftop exibe informações detalhadas sobre o uso de ethernet/rede. O Iftop exibe estatísticas por canal de comunicação nas entidades que usam ethernet e a quantidade de largura de banda que elas usam. O Iftop pode ser instalado na maioria dos sistemas Linux usando `yum install iftop` ou `apt-get install iftop`.

* Java Flight Recorder (JFR): uma ferramenta comercial do Oracle que pode ser usada livremente em ambientes não relacionados à produção. Para obter mais detalhes, consulte [Como usar o Java Flight Recorder para diagnosticar problemas em tempo de execução do CQ](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] `error.log` arquivo: você pode investigar o arquivo [!DNL Experience Manager] `error.log` para obter detalhes dos erros registrados no sistema. Use o comando `tail -F quickstart/logs/error.log` para identificar erros a serem investigados.
* [Console de fluxo de trabalho](/help/sites-administering/workflows.md): use o console de fluxo de trabalho para monitorar fluxos de trabalho atrasados ou travados.

Normalmente, você usa essas ferramentas em conjunto para obter uma ideia abrangente sobre o desempenho da sua implantação do [!DNL Experience Manager].

>[!NOTE]
>
>Essas ferramentas são ferramentas padrão e não são diretamente compatíveis com o Adobe. Eles não exigem licenças adicionais.

![chlimage_1-33](assets/chlimage_1-143.png)

*Figura: monitoramento em tempo real usando a ferramenta Visual VM.*

![chlimage_1-32](assets/chlimage_1-142.png)

## Monitoramento a longo prazo {#long-term-monitoring}

O monitoramento de longo prazo de uma implantação do [!DNL Experience Manager] envolve o monitoramento por um período mais longo das mesmas partes que são monitoradas em tempo real. Também inclui a definição de alertas específicos para o seu ambiente.

### Agregação e relatórios de logs {#log-aggregation-and-reporting}

Há várias ferramentas disponíveis para agregar logs, por exemplo, Splunk(TM) e Elastic Search, Logstash e Kabana (ELK). Para avaliar o tempo de atividade da sua implantação do [!DNL Experience Manager], é importante que você entenda os eventos de log específicos do seu sistema e crie alertas com base neles. Um bom conhecimento de suas práticas de desenvolvimento e operações pode ajudá-lo a entender melhor como ajustar o processo de agregação de logs para gerar alertas críticos.

### Monitoramento de ambiente {#environment-monitoring}

O monitoramento do ambiente inclui o monitoramento do seguinte:

* Taxa de transferência de rede
* E/S de disco
* Memória
* Utilização do CPU
* MBeans JMX
* Sites externos

São necessárias ferramentas externas, como NewRelic(TM) e AppDynamics(TM), para monitorar cada item. Com essas ferramentas, você pode definir alertas específicos ao seu sistema, por exemplo, alta utilização do sistema, backup do fluxo de trabalho, falhas na verificação de integridade ou acesso não autenticado ao seu site. A Adobe não recomenda nenhuma ferramenta em particular em detrimento de outras. Encontre a ferramenta que funciona para você e use-a para monitorar os itens discutidos.

#### Monitoramento interno de aplicativos {#internal-application-monitoring}

O monitoramento interno de aplicativos inclui o monitoramento dos componentes de aplicativos que compõem a pilha do [!DNL Experience Manager], incluindo o JVM, o repositório de conteúdo e o monitoramento por meio do código de aplicativo personalizado criado na plataforma. Em geral, é realizado através de JMX Mbeans que podem ser monitorados diretamente por muitas soluções de monitoramento populares, tais como SolarWinds (TM), HP OpenView(TM), Hyperic(TM), Zabbix(TM), e outros. Para sistemas que não suportam uma conexão direta com JMX, você pode escrever scripts de shell para extrair os dados JMX e expô-los a esses sistemas em um formato que eles entendem nativamente.

O acesso remoto aos Mbeans JMX não é ativado por padrão. Para obter mais informações sobre monitoramento através de JMX, consulte [Monitoramento e gerenciamento usando a tecnologia JMX](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

Em muitos casos, é necessária uma linha de base para monitorar efetivamente uma estatística. Para criar uma linha de base, observe o sistema em condições normais de trabalho por um período predeterminado e identifique a métrica normal.

**Monitoramento de JVM**

Como em qualquer pilha de aplicativo baseada em Java, o [!DNL Experience Manager] depende dos recursos que são fornecidos a ele por meio da Java Virtual Machine subjacente. Você pode monitorar o status de muitos desses recursos por meio dos MXBeans da plataforma expostos pela JVM. Para obter mais informações sobre MXBeans, consulte [Usando o Servidor MBean da plataforma e MXBeans da plataforma](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

Estes são alguns parâmetros de linha de base que você pode monitorar para a JVM:

Memória

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* Instâncias: todos os servidores
* Limite de alarme: quando a utilização da memória heap ou não heap exceder 75% da memória máxima correspondente.
* Definição do alarme: A memória do sistema é insuficiente ou há um vazamento de memória no código. Analise um despejo de thread para chegar a uma definição.

>[!NOTE]
>
>As informações fornecidas por este bean são expressas em bytes.

Threads

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* Instâncias: todos os servidores
* Limite de alarme: Quando o número de threads for maior que 150% da linha de base.
* Definição de alarme: Há um processo em execução ativo ou uma operação ineficiente consome uma grande quantidade de recursos. Analise um despejo de thread para chegar a uma definição.

**Monitorar[!DNL Experience Manager]**

[!DNL Experience Manager] também expõe um conjunto de estatísticas e operações através de JMX. Eles podem ajudar a avaliar a integridade do sistema e identificar possíveis problemas antes que eles afetem os usuários. Para obter mais informações, consulte a [documentação](/help/sites-administering/jmx-console.md) sobre [!DNL Experience Manager] MBeans JMX.

Estes são alguns parâmetros de linha de base que você pode monitorar para [!DNL Experience Manager]:

Agentes de replicação

* MBean: `com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* Instâncias: um autor e todas as instâncias de publicação (para agentes de limpeza)
* Limite de alarme: Quando o valor de `QueueBlocked` for `true` ou o valor de `QueueNumEntries` for maior que 150% da linha de base.

* Definição de alarme: Presença de uma fila bloqueada no sistema indicando que o destino de replicação está inativo ou inacessível. Geralmente, problemas de rede ou infraestrutura fazem com que entradas excessivas sejam enfileiradas, o que pode afetar negativamente o desempenho do sistema.

>[!NOTE]
>
>Para os parâmetros MBean e URL, substitua `<AGENT_NAME>` pelo nome do agente de replicação que você deseja monitorar.

Contador de sessão

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;Estatísticas do OakRepository&quot;,type*=&quot;RepositoryStats&quot;
* Instâncias: todos os servidores
* Limite de alarme: quando as sessões abertas excedem a linha de base em mais de 50%.
* Definição do alarme: As sessões podem ser abertas através de um código e nunca fechar. Isso pode acontecer lentamente com o tempo e eventualmente causar vazamentos de memória no sistema. Embora o número de sessões deva flutuar em um sistema, ele não deve aumentar continuamente.

Verificações de integridade

As verificações de integridade disponíveis no [painel de operações](/help/sites-administering/operations-dashboard.md#health-reports) têm MBeans JMX correspondentes para monitoramento. No entanto, você pode criar verificações de integridade personalizadas para expor estatísticas adicionais do sistema.

Estas são algumas verificações de integridade prontas para uso que são úteis para monitorar:

* Verificações do sistema
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * Instâncias: um autor, todos os servidores de publicação
   * Limite de alarme: quando o status não é OK
   * Definição de alarme: O status de uma das métricas é AVISO ou CRÍTICO. Verifique o atributo de log para obter mais informações sobre a causa do problema.

* Fila de replicação

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * Instâncias: um autor, todos os servidores de publicação
   * Limite de alarme: quando o status não é OK
   * Definição de alarme: O status de uma das métricas é AVISO ou CRÍTICO. Verifique o atributo de log para obter mais informações sobre a fila que causou o problema.

* Desempenho da resposta

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * Instâncias: todos os servidores
   * Duração do alarme: Quando o estado não estiver OK
   * Definição de alarme: O status de uma das métricas é AVISO ou CRÍTICO. Verifique o atributo de log para obter mais informações sobre a fila que causou o problema.

* Desempenho da consulta

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * Instâncias: um autor, todos os servidores de publicação
   * Limite de alarme: quando o status não é OK
   * Definição do alarme: uma ou mais consultas são executadas lentamente no sistema. Verifique o atributo de log para obter mais informações sobre as consultas que causaram o problema.

* Pacotes ativos

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * Instâncias: todos os servidores
   * Limite de alarme: quando o status não é OK
   * Definição do alarme: Presença de pacotes OSGi inativos ou não resolvidos no sistema. Verifique o atributo de log para obter mais informações sobre os pacotes que causaram o problema.

* Erros de log

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * Instâncias: todos os servidores
   * Limite de alarme: quando o status não é OK
   * Definição do alarme: Existem erros nos arquivos de registro. @ info: whatsthis Verifique o atributo de log para obter mais informações sobre a causa do problema.

## Problemas comuns e resoluções  {#common-issues-and-resolutions}

No processo de monitoramento, se você encontrar problemas, veja a seguir algumas tarefas de solução de problemas que você pode executar para resolver problemas comuns com [!DNL Experience Manager] implantações:

* Se estiver usando TarMK, execute a compactação Tar com frequência. Para obter mais detalhes, consulte [Manter o repositório](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* Verificar `OutOfMemoryError` logs. Para obter mais informações, consulte [Analisar problemas de memória](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=pt-BR).

* Verifique nos logs se há referências a consultas não indexadas, percursos de árvore ou percursos de índice. Isso indica consultas não indexadas ou indexadas inadequadamente. Para obter as práticas recomendadas de otimização do desempenho de consulta e indexação, consulte [Práticas recomendadas para consultas e indexação](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* Use o console de workflows para verificar se seus workflows funcionam conforme esperado. Se possível, condensar vários workflows em um único workflow.
* Revise o monitoramento em tempo real e procure por gargalos adicionais ou grandes consumidores de quaisquer recursos específicos.
* Investigue os pontos de saída da rede do cliente e os pontos de entrada da rede de implantação [!DNL Experience Manager], incluindo o Dispatcher. Frequentemente, essas são áreas de gargalo. Para obter mais informações, consulte [considerações de rede do Assets](/help/assets/assets-network-considerations.md).
* Ajuste o tamanho do servidor [!DNL Experience Manager]. Você pode ter uma implantação do [!DNL Experience Manager] dimensionada de maneira inadequada. O Suporte ao cliente da Adobe pode ajudar você a identificar se o servidor não tem tamanho suficiente.
* Examine os arquivos `access.log` e `error.log` para entradas quando algo der errado. Procure padrões que possam indicar anomalias de código personalizadas. Adicione-os à lista de eventos que você monitora.
