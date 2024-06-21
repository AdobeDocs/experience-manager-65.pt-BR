---
title: Monitoramento de implantações de formulários AEM
description: Você pode monitorar implantações de formulários AEM tanto no nível do sistema quanto no nível interno. Saiba mais sobre o monitoramento de implantações de formulários AEM neste documento.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 931e8095-5c7c-4c1f-b95b-75ac2827d4f3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# Monitoramento de implantações de formulários AEM {#monitoring-aem-forms-deployments}

Você pode monitorar implantações de formulários AEM tanto no nível do sistema quanto no nível interno. Você pode usar ferramentas de gerenciamento especializadas, como HP OpenView, IBM® Tivoli e CA UniCenter, e um monitor JMX de terceiros chamado *JConsole* para monitorar especificamente a atividade do Java™. A implementação de uma estratégia de monitoramento melhora a disponibilidade, a confiabilidade e o desempenho das implantações de formulários AEM.

<!-- For more information about monitoring AEM forms deployments, see [A technical guide for monitoring AEM forms deployments](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

## Monitorando usando MBeans {#monitoring-using-mbeans}

O AEM Forms fornece dois MBeans registrados que fornecem informações de navegação e estatística. Essas partes são os únicos MBeans compatíveis com integração e inspeção:

* **ServiceStatistic:** Este MBean fornece informações sobre o nome do serviço e sua versão.
* **Estatística da Operação:** Este MBean fornece as estatísticas de cada serviço do servidor do AEM Forms. Este MBean é onde os administradores podem obter informações sobre um serviço específico, como o tempo de chamada e o número de erros.

### Interfaces públicas ServiceStatisticMbean {#servicestatisticmbean-public-interfaces}

Essas interfaces públicas do ServiceStatistic MBean podem ser acessadas para fins de teste:

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### Interfaces públicas de OperationStatisticMbean {#operationstatisticmbean-public-interfaces}

Essas interfaces públicas do MBean OperationStatistic podem ser acessadas para fins de teste:

```java
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### Árvore MBean e estatísticas da operação {#mbean-tree-operation-statistics}

Usando um console JMX (JConsole), as estatísticas do MBean OperationStatistic estão disponíveis. Essas estatísticas são atributos de MBean e podem ser navegadas sob a seguinte árvore hierárquica:

**Árvore MBean**

**Nome do domínio do Adobe:** Depende do servidor de aplicativos. Se o Servidor de Aplicativos não definir o domínio, o padrão será adobe.com.

**ServiceType:** AdobeService é o nome usado para listar todos os serviços.

**AdobeServiceName:** Nome do serviço ou ID do serviço.

**Versão:** Versão do serviço.

**Estatísticas da operação**

**Hora da Chamada:** Tempo decorrido para a execução do método. Essa chamada não inclui o tempo em que a solicitação é serializada, transferida do cliente para o servidor e desserializada.

**Contagem de chamadas:** O número de vezes que o serviço é chamado.

**Tempo médio de invocação:** Tempo médio de todas as invocações executadas desde a inicialização do servidor.

**Tempo máximo de invocação:** A duração da invocação mais longa executada desde a inicialização do servidor.

**Tempo mínimo de invocação:** A duração da invocação mais curta executada desde a inicialização do servidor.

**Contagem de Exceções:** Número de invocações que resultaram em falhas.

**Mensagem de exceção:** A mensagem de erro da última exceção que ocorreu.

**Data e hora da última amostragem:** A data da última invocação.

**Unidade de tempo:** O padrão é milissegundo.

Para ativar o monitoramento JMX, os servidores de aplicações normalmente precisam de alguma configuração. Consulte a documentação do servidor de aplicativos para obter informações específicas.

### Exemplos de como configurar o acesso JMX aberto {#examples-of-how-to-set-up-open-jmx-access}

**JBoss® 4.0.3/4.2.0 - configurar a inicialização da JVM**

Para exibir MBeans do JConsole, configure os parâmetros de inicialização do JVM do servidor de aplicações JBoss. Certifique-se de que o JBoss foi iniciado a partir do arquivo run.bat/sh.

1. Edite o arquivo run.bat localizado em InstallJBoss/bin.
1. Localize a linha JAVA_OPTS e adicione o seguinte:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 - configurar a inicialização da JVM**

1. Edite o arquivo startWebLogic.bat localizado em `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`.
1. Localize a linha JAVA_OPTS e adicione o seguinte:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. Reinicie o WebLogic.

>[!NOTE]
>
>Para o WebLogic, você pode acessar o MBean usando remoto ou IIOP.

**Acessar o MBean remotamente**

1. Inicie o JConsole para nova conexão e clique na guia remoto.
1. Insira o nome do host e a porta (9088, o número especificado durante as opções de inicialização da JVM).

**WebSphere® 6.1 - configurar a inicialização da JVM**

1. No Admin Console (Servidor de aplicativos > server1 > Definição de processo > JVM), adicione a seguinte linha no campo Argumento JVM Genérico:

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. Adicione ou remova o comentário das três linhas a seguir no arquivo /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties (ou &lt;your websphere=&quot;&quot; jre=&quot;&quot;>/ lib/management/management.properties):

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. Reinicie o WebSphere.
