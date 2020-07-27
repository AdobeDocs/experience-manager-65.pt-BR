---
title: Monitoramento de implantações de formulários do AEM
seo-title: Monitoramento de implantações de formulários do AEM
description: Você pode monitorar implantações de formulários AEM de um nível de sistema e de um nível interno. Saiba mais sobre como monitorar implantações de formulários do AEM a partir desse documento.
seo-description: Você pode monitorar implantações de formulários AEM de um nível de sistema e de um nível interno. Saiba mais sobre como monitorar as implantações de formulários do AEM a partir desse documento.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Monitoramento de implantações de formulários do AEM {#monitoring-aem-forms-deployments}

Você pode monitorar implantações de formulários AEM de um nível de sistema e de um nível interno. Você pode usar ferramentas de gerenciamento especializadas como HP OpenView, IBM Tivoli e CA UniCenter e um monitor JMX de terceiros chamado *JConsole* para monitorar especificamente a atividade Java. A implementação de uma estratégia de monitoramento melhora a disponibilidade, a confiabilidade e o desempenho das implantações de formulários do AEM.

Para obter mais informações sobre como monitorar implantações de formulários do AEM, consulte [Um guia técnico para monitorar implantações](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf)de formulários do AEM.

## Monitoramento usando MBeans {#monitoring-using-mbeans}

Os formulários AEM fornecem dois MBeans registrados que fornecem informações de navegação e estatísticas. Esses são os únicos MBeans suportados para integração e inspeção:

* **ServiceStatistics:** Este MBean fornece informações sobre o nome do serviço e sua versão.
* **OperationStatistics:** Este MBean fornece a estatística de cada serviço de servidor de formulários. É aqui que os administradores podem obter informações sobre um serviço específico, como tempo de invocação, número de erros e assim por diante.

### Interfaces públicas ServiceStatisticalMbean {#servicestatisticmbean-public-interfaces}

Essas interfaces públicas do ServiceStatistics MBean podem ser acessadas para fins de teste:

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### Interfaces públicas OperationStatisticalMbean {#operationstatisticmbean-public-interfaces}

Essas interfaces públicas do OperationStatistical MBean podem ser acessadas para fins de teste:

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

### Estatísticas de árvore e operação MBean {#mbean-tree-operation-statistics}

Usando um console JMX (JConsole), as estatísticas do MBean OperationStatistics estão disponíveis. Essas estatísticas são atributos do MBean e podem ser navegadas na seguinte árvore hierárquica:

**Árvore MBean**

**Nome de domínio da Adobe:** Depende do servidor de aplicativos. Se o Servidor de aplicativos não definir o domínio, o padrão será adobe.com.

**ServiceType:** O AdobeService é o nome usado para lista de todos os serviços.

**AdobeServiceName:** Nome do serviço ou ID do serviço.

**Versão:** Versão do serviço.

**Estatísticas da Operação**

**Hora da Chamada:** Tempo necessário para a execução do método. Isso não inclui o momento em que a solicitação é serializada, transferida do cliente para o servidor e desserializada.

**Contagem de chamada:** O número de vezes que o serviço é chamado.

**Tempo médio de invocação:** Tempo médio de todas as invocações executadas desde que o servidor foi iniciado.

**Tempo máximo de invocação:** A duração da invocação mais longa executada desde que o servidor foi iniciado.

**Tempo mínimo de invocação:** A duração da invocação mais curta executada desde que o servidor foi iniciado.

**Contagem de Exceções:** Número de invocações que resultaram em falhas.

**Mensagem de exceção:** A mensagem de erro da última exceção que ocorreu.

**Data da Última Amostragem Hora:** A data da última invocação.

**Unidade de tempo:** O padrão é milissegundos.

Para habilitar o monitoramento JMX, os servidores de aplicativos geralmente precisam de alguma configuração. Consulte a documentação do servidor de aplicativos para obter as especificações.

### Exemplos de como configurar o acesso JMX aberto {#examples-of-how-to-set-up-open-jmx-access}

**JBoss 4.0.3/4.2.0 - configurar a inicialização do JVM**

Para visualização de MBeans do JConsole, configure os parâmetros de inicialização JVM do servidor de aplicativos JBoss. Verifique se o JBoss foi iniciado a partir do arquivo run.bat/sh.

1. Edite o arquivo run.bat localizado em InstallJBoss/bin.
1. Localize a linha JAVA_OPTS e adicione o seguinte:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2/10 - configurar a inicialização do JVM**

1. Edite o arquivo startWebLogic.bat localizado em `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`.
1. Localize a linha JAVA_OPTS e adicione o seguinte:

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. Reinicie o WebLogic.

>[!NOTE]
>
>Para WebLogic, você pode acessar o MBean usando remoto ou IIOP.

**Acesse o MBean remotamente**

1. Inicie o JConsole para uma nova conexão e clique na guia remota.
1. Digite o nome do host e a porta (9088, o número que você especificou durante as opções de start para cima da JVM).

**Webphere 6.1 - configurar a inicialização do JVM**

1. No console de administração (Servidor de aplicativos > servidor1 > Definição de processo > JVM), adicione a seguinte linha ao campo Argumento JVM genérico:

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. Adicione ou exclua as barras de comentário das três linhas a seguir no arquivo /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties (ou &lt;Your Webphere JRE>/ lib/management/management.properties):

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. Reinicie o WebSphere.

