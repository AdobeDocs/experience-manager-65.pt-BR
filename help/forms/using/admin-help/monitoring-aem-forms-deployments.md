---
title: Monitoramento AEM implantações de formulários
seo-title: Monitoring AEM forms deployments
description: É possível monitorar AEM implantações de formulários a partir de um nível de sistema e de um nível interno. Saiba mais sobre como monitorar AEM implantações de formulários neste documento.
seo-description: You can monitor AEM forms deployments from both a system level and an internal level. Learn more about monitoring AEM forms deployments from this document.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
exl-id: 931e8095-5c7c-4c1f-b95b-75ac2827d4f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# Monitoramento AEM implantações de formulários {#monitoring-aem-forms-deployments}

É possível monitorar AEM implantações de formulários a partir de um nível de sistema e de um nível interno. Você pode usar ferramentas de gerenciamento especializadas como HP OpenView, IBM Tivoli e CA UniCenter e um monitor JMX de terceiros chamado *JConsole* para monitorar especificamente a atividade do Java. A implementação de uma estratégia de monitoramento melhora a disponibilidade, confiabilidade e desempenho de suas implantações de formulários AEM.

Para obter mais informações sobre o monitoramento AEM implantações de formulários, consulte [Um guia técnico para monitorar AEM implantações de formulários](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf).

## Monitoramento com MBeans {#monitoring-using-mbeans}

AEM formulários fornece dois MBeans registrados que fornecem informações de navegação e estatísticas. Esses são os únicos MBeans compatíveis com integração e inspeção:

* **ServiceStatistics:** Este MBean fornece informações sobre o nome do serviço e sua versão.
* **OperationStatistics:** Este MBean fornece a estatística de cada serviço de servidor de formulários. É aqui que os administradores podem obter informações sobre um serviço específico, como tempo de invocação, número de erros e assim por diante.

### Interfaces públicas ServiceStatisticsMbean {#servicestatisticmbean-public-interfaces}

Essas interfaces públicas do ServiceStatistics MBean podem ser acessadas para fins de teste:

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### Interfaces públicas OperationStatisticsMbean {#operationstatisticmbean-public-interfaces}

Essas interfaces públicas do OperationStatistics MBean podem ser acessadas para fins de teste:

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

### Estatísticas de Operação e Árvore do MBean {#mbean-tree-operation-statistics}

Usando um console JMX (JConsole), as estatísticas do MBean OperationStatistics estão disponíveis. Essas estatísticas são atributos do MBean e podem ser navegadas na seguinte árvore de hierarquia:

**Árvore do MBean**

**Nome do domínio Adobe:** Depende do Servidor de Aplicativos. Se o Servidor de Aplicativos não definir o domínio, o padrão será adobe.com.

**ServiceType:** AdobeService é o nome usado para listar todos os serviços.

**AdobeServiceName:** Nome do serviço ou ID do serviço.

**Versão:** Versão do serviço.

**Estatísticas da Operação**

**Hora da Chamada:** Tempo necessário para a execução do método. Isso não inclui o momento em que a solicitação é serializada, transferida de cliente para servidor e desserializada.

**Contagem de invocações:** O número de vezes que o serviço é chamado.

**Tempo médio de invocação:** Tempo médio de todas as invocações executadas desde que o servidor foi iniciado.

**Tempo máximo de invocação:** A duração da invocação mais longa que foi executada desde que o servidor foi iniciado.

**Tempo mínimo de invocação:** A duração da invocação mais curta que foi executada desde que o servidor foi iniciado.

**Contagem de Exceções:** Número de invocações que resultaram em falhas.

**Mensagem de exceção:** A mensagem de erro da última exceção que ocorreu.

**Data/Hora da Última Amostragem:** A data da última invocação.

**Unidade de Tempo:** O padrão é milissegundos.

Para ativar o monitoramento JMX, os servidores de aplicativos normalmente precisam de alguma configuração. Consulte a documentação do servidor de aplicativos para obter as especificações.

### Exemplos de como configurar o acesso JMX aberto {#examples-of-how-to-set-up-open-jmx-access}

**JBoss 4.0.3/4.2.0 - configurar a inicialização da JVM**

Para exibir MBeans do JConsole, configure os parâmetros de inicialização da JVM do servidor de aplicativos JBoss. Verifique se o JBoss foi iniciado a partir do arquivo run.bat/sh.

1. Edite o arquivo run.bat localizado em InstallJBoss/bin.
1. Encontre a linha JAVA_OPTS e adicione o seguinte:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2/10 - configure a inicialização da JVM**

1. Edite o arquivo startWebLogic.bat localizado em `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`.
1. Encontre a linha JAVA_OPTS e adicione o seguinte:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. Reinicie o WebLogic.

>[!NOTE]
>
>Para o WebLogic, você pode acessar o MBean usando remoto ou IIOP.

**Acesse o MBean remotamente**

1. Inicie o JConsole para nova conexão e clique na guia remota.
1. Insira o nome do host e a porta (9088, o número que você especifica durante as opções de inicialização da JVM).

**Websphere 6.1 - configurar a inicialização da JVM**

1. No Admin Console (Servidor de Aplicativos > servidor1 > Definição de Processos > JVM), adicione a seguinte linha no campo Argumento da JVM Genérica:

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. Adicione ou exclua o comentário das três linhas a seguir no arquivo /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties (ou &lt;your websphere=&quot;&quot; jre=&quot;&quot;>/ lib/management/management.properties):

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. Reinicie o WebSphere.
