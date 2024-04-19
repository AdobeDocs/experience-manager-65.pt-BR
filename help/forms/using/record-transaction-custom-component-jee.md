---
title: Registre uma transação para API de componente personalizado para AEM Forms no JEE.
description: Saiba mais sobre como usar a API TransactionRecorder para registrar transações para o componente personalizado.
feature: Transaction Reports
exl-id: 33e1868a-2a7f-4785-8571-95651e661e21
source-git-commit: bf99ad3710638ec823d3b17967e1c750d0405c77
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Registrar uma transação para APIs de componente personalizado para AEM Forms no JEE {#record-a-transaction-for-custom-components}

Quando você usa APIs faturáveis no componente personalizado, é possível ativar o relatório de transações para o componente. Para habilitar o relatório de transações, modifique o `component.xml` arquivo do componente e adicione a tag fornecida abaixo na operação para a qual o relatório de transação deve ser ativado.

**Tag**: `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| Marca de operação antiga | Nova marca de operação |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

Se você precisar capturar mais de uma transação para uma API, como uma API em lote, em que a contagem de transações varia com o número de contagens de entrada, manipule a contagem de transações no nível da API.

**Para registrar a contagem de transações variadas:**

1. Importar classe `"com.adobe.idp.dsc.InvocationContextStack"` no código. A classe faz parte do `adobe-livecycle-client.jar` arquivo sdk. O arquivo sdk está disponível em `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > Atualize o arquivo do cliente compartilhado acima no projeto do cliente com o novo arquivo caso ele já esteja empacotado.

1. Na API para a qual transações variadas devem ser registradas:
   1. Adicione lógica para armazenar a contagem de transações em alguma variável de número inteiro, como, `transaction_count`.
   1. Quando a operação for bem-sucedida, adicionar `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## Artigos relacionados

* [Ativação e visualização de relatórios de transações para o AEM Forms no JEE](/help/forms/using/transaction-report-overview-jee.md)
* [Lista de APIs faturáveis para o AEM Forms no JEE](/help/forms/using/transaction-reports-billable-apis-jee.md)
