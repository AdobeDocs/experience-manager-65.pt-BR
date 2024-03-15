---
title: Registre uma transação para API de componente personalizado para AEM Forms no JEE.
description: Use a API TransactionRecorder para registrar a transação para o componente personalizado.
feature: Transaction Reports
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# Registrar uma transação para APIs de componente personalizado para AEM Forms no JEE {#record-a-transaction-for-custom-components}

Quando você usa APIs faturáveis no componente personalizado, é possível ativar os relatórios de transações para o componente. Para habilitar o relatório de transações, modifique o `component.xml` arquivo do componente e adicione a tag fornecida abaixo na operação para a qual o relatório de transação precisa ser ativado.

**Tag**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| Marca de operação antiga | Nova marca de operação |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

Se houver um requisito para capturar mais de uma transação para uma API, por exemplo, no caso de uma API em lote em que a contagem de transações pode variar com o número de contagens de entrada, nesses casos, é necessário lidar com a contagem de transações no nível da API. Abaixo estão as etapas fornecidas para registrar a contagem de transações variadas:

1. Importar classe `"com.adobe.idp.dsc.InvocationContextStack"` no código. A classe faz parte do `adobe-livecycle-client.jar` arquivo sdk. O arquivo sdk está disponível em `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > Atualize o arquivo do cliente compartilhado acima no projeto do cliente com o novo arquivo, caso ele já esteja empacotado.

1. Na API para a qual transações variadas precisam ser registradas:
   1. Adicione uma lógica para armazenar a contagem de transações em alguma variável de número inteiro, como, `transaction_count`.
   1. Quando a operação for bem-sucedida, adicionar `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## Artigos relacionados

* [Ativação e exibição do relatório de transações do AEM Forms no JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Lista de APIs faturáveis para o AEM Forms no JEE](/help/forms/using/transaction-reports-billable-apis-jee.md)


