---
title: Visão geral dos relatórios de transação do AEM Forms no JEE
description: Mantenha uma contagem de todos os formulários enviados, renderizados, documentos convertidos em um formato para outro e muito mais.
feature: Transaction Reports
exl-id: 77e95631-6b0d-406e-a1b8-78f8d9cceb63
role: Admin, User, Developer
solution: "Experience Manager, Experience Manager Forms"
source-git-commit: 5699f5814daf16a397eb6129b881ac2035456e39
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Ativação e visualização de relatórios de transações para o AEM Forms no JEE {#transaction-reports-overview}

<span> O recurso de Relatório de Transações foi introduzido para o [AEM Forms no JEE pela AEM Forms 6.5.20.0](/help/release-notes/previous/6-5-20.md#forms). Este recurso está desabilitado por padrão e pode ser habilitado na Interface do Usuário do Administrador.</span>

Os relatórios de transações no AEM Forms no JEE permitem que você mantenha uma contagem de todas as transações realizadas na implantação do AEM Forms. O objetivo é fornecer informações sobre o uso do produto e ajudar as partes interessadas a entender seus volumes de processamento digital. Exemplos de uma transação incluem:

* Apresentação de um documento
* Representação de um documento
* Conversão de um documento de um formato de arquivo para outro

Para obter mais informações sobre o que é considerado uma transação, consulte [APIs faturáveis](../../forms/using/transaction-reports-billable-apis-jee.md).

## Habilitar relatório de transações {#enable-transaction-reporting}

Por padrão, a gravação da transação está desativada. Para ativar a emissão de relatórios de transação, execute as seguintes etapas:

1. Navegue até o `/adminui` no seu AEM Forms no JEE, por exemplo, `http://10.14.18.10:8080/adminui`.
1. Fazer logon como **Administrador**.
1. Vá para **Configurações** > **Configurações Principais do Sistema** > **Configurações**.
1. Clique na caixa de seleção para **Habilitar relatórios de transações** e **Salvar** as configurações.

   ![exemplo-transação-relatório-jee](assets/enable-transaction-jee.png)

1. Reinicie o servidor.
1. Além das alterações no servidor, no lado do cliente, você deve atualizar o arquivo `adobe-livecycle-client.jar` no seu projeto, se estiver usando o mesmo.

<!--
* You can [enable transaction recording](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) from AEM Web Console. view transaction reports on author, processing, or publish instances. View transaction reports on author or processing instances for an aggregated sum of all transactions. View transaction reports on the publish instances for a count of all transactions that take place only on that publish instance from where the report is run.
-->

<!--Do not author content (Create adaptive forms, interactive communication, themes, and other authoring activities) and process documents (Use workflows, document services, and other processing activities) on the same AEM instance. Keep the transaction recording disabled for AEM Forms servers used to author content. Keep the transaction recording enabled for AEM Forms servers used to process documents.-->

## Exibição do relatório de transações {#view-transaction-report}

Ao habilitar o relatório de transações, as informações sobre as contagens de transações ficam acessíveis por meio do [relatório de transações por meio do painel](#transaction-report-dashboard) e de um [relatório de transações detalhado por meio do arquivo de log](#transaction-report-logfile). Ambos são explicados abaixo:

### Relatório de transações via painel {#transaction-report-dashboard}

O relatório de transações via painel fornece o número total de contagens de transações para cada tipo de transação. Por exemplo, você obtém as informações sobre o número total de formulários renderizados, convertidos e enviados conforme mostrado na imagem. Para obter o relatório de transações:

1. Navegue até o `/adminui` no seu AEM Forms no JEE, por exemplo: `http://10.13.15.08:8080/adminui`.
1. Fazer logon como **Administrador**.
1. Clique em Monitor de integridade.
1. Navegue até a guia **Repórter de Transações**, clique em **Calcular Total de Transações**. Agora você verá que um gráfico de pizza representa o número de PDF forms - enviadas, renderizadas ou convertidas.

![exemplo-transação-relatório-jee](assets/transaction-piechart.png)


### Relatório de transações via arquivo de log {#transaction-report-logfile}

O relatório de transações via arquivo de registro fornece informações detalhadas sobre cada transação. Para acessar os logs de transação, siga o caminho do contexto relativo à inicialização do servidor. As transações são capturadas em um arquivo de log separado `transaction_log.log` por padrão. O **caminho do arquivo** é relativo ao contexto de início do servidor. O caminho padrão para servidores diferentes é fornecido abaixo:

```
For Jboss Turnkey:
"<AEM_Forms_Installation>/jboss/bin/transaction_log.log"

For IBM Websphere: 
"<IBM_WAS_Profile_path>/transaction_log.log"

For Oracle Weblogic:
"<Weblogic_Domain_path>/transaction_log.log"

For Jboss Cluster:
"<Jboss home>/transaction_log.log"
```

Exemplo de um registro de transação de amostra:
`[2024-02-28 06:11:27] [INFO] TransactionRecord{service='GeneratePDFService', operation='HtmlFileToPDF', internalService='GeneratePDFService', internalOperation='HtmlFileToPDF', transactionOperationType='CONVERT', transactionCount=1, elapsedTime=1906, transactionDate=Wed Feb 28 06:11:25 UTC 2024}`

#### Registro da transação {#transaction-record-structure-jee}

A estrutura do log de transações define como cada transação é registrada por meio de seus vários parâmetros, como serviço, operação, tipo de transação e outros. Cada uma é apresentada em detalhes abaixo. A estrutura do registro de transação é a seguinte:

```
TransactionRecord
{
    service='...', 
    operation='...', 
    internalService='...', 
    internalOperation='...', 
    transactionOperationType='...', 
    transactionCount=..., 
    elapsedTime=..., 
    transactionDate=...
}
```

* **serviço**: nome do serviço.
* **operação**: nome da operação.
* **internalService**: nome do receptor da chamada se houver uma chamada interna, caso contrário, igual ao nome do serviço.
* **internalOperation**: nome do chamado em que há uma chamada interna, caso contrário, igual ao nome da operação.
* **transactionOperationType**: tipo de transação (Enviar, Renderizar, Converter).
* **transactionCount**: Contagem total de transações.
* **elapsedTime**: tempo entre a iniciação da chamada e a resposta recebida.
* **transactionDate**: carimbo de data/hora indicando quando o serviço foi chamado.

**Log de transações de exemplo**:

```
[2024-02-14 14:23:25] [INFO] TransactionRecord
{
    service='BarcodedFormsService', 
    operation='decode', 
    internalService='BarcodedFormsService', 
    internalOperation='decode', 
    transactionOperationType='CONVERT', 
    transactionCount=1, 
    elapsedTime=47405, 
    transactionDate=Wed Feb 14 14:22:37 UTC 2024
}
```

## Frequência de gravação da transação {#transaction-recording-frequency}

<!--Transaction persistence involves updating the total transaction count for SUBMIT, CONVERT, and RENDER operations on the server periodically: -->

A frequência de transações de registro é determinada pelas operações de atualização no servidor para cada formulário enviado, renderizado ou convertido com sucesso.

* No **painel**, a contagem de transações é atualizada periodicamente. O padrão é definido como 1 minuto. Você pode atualizar a frequência definindo a propriedade do sistema como `"com.adobe.idp.dsc.transaction.recordFrequency"`. Por exemplo, no AEM Forms para JEE em JBoss®, adicione `-Dcom.adobe.idp.dsc.transaction.recordFrequency=5` em `JAVA_OPTS` para definir a frequência de atualização para 5 minutos.

* Em **logs de transações**, a atualização para cada transação ocorre instantaneamente quando um formulário é enviado, renderizado ou convertido com êxito.

<!-- A transaction remains in the buffer for a specified period (Flush Buffer time + Reverse replication time). By default, it takes approximately 90 seconds for the transaction count to reflect in the transaction report.

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, or using non-standard form submission methods are not accounted as transactions. AEM Forms provides an API to record such transactions. Call the API from your custom implementations to record a transaction.

## Supported Topology {#supported-topology}

Transaction reports are available only on AEM Forms on OSGi environment. It supports author-publish, author-processing-publish, and only processing topologies. For example, topologies, see [Architecture and deployment topologies for AEM Forms](../../forms/using/transaction-reports-overview.md).

The transaction count is reverse replicated from publish instances to author or processing instances. An indicative author-publish topology is displayed below:

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms transaction reports does not support topologies that contain only publish instances.

### Guidelines for using transaction reports {#guidelines-for-using-transaction-reports}

* Disable transaction reports on all author instances as reports on author instances includes transactions registered during authoring activities.
* Enable the **Show transactions from publish only** option on the author instance to view cumulative transactions from all publish instances. You can also view transaction reports on each publish instance for actual transactions on that particular publish instance only.
* Do not use author instances to run workflows and process documents.
* Before using transaction reporting, if you are have a toplogy with publish servers, ensure that the reverse replication is enabled for all the publish instances.
* Transaction data is reverse-replicated from a publish instance to only corresponding author or processing instance. The author or processing instance cannot further replicate data to another instance. For example, if you have author-processing-publish topology, aggregated transaction data is replicated only to the processing instance.-->

## Artigos relacionados {#related-articles}

* [Lista de APIs faturáveis para o AEM Forms no JEE](../../forms/using/transaction-reports-billable-apis-jee.md)
* [Registrar uma transação para APIs de componente personalizado para AEM Forms no JEE](/help/forms/using/record-transaction-custom-component-jee.md)
