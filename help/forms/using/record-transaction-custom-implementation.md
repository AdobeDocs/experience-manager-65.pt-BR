---
title: Registrar uma transação para implementações personalizadas
seo-title: Registrar uma transação para implementações personalizadas
description: Use a API TransactionRecorder para registrar ações que não são contabilizadas como transações automaticamente
seo-description: Use a API TransactionRecorder para registrar ações que não são contabilizadas como transações automaticamente
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Registrar uma transação para implementações personalizadas {#record-a-transaction-for-custom-implementations}

Use a API TransactionRecorder para registrar ações que não são contabilizadas como transações automaticamente

Você pode usar um código personalizado para enviar um formulário PDF, enviar um URL de pré-visualização da interface do agente para usuários finais para pré-visualização de uma comunicação interativa ou enviar um formulário usando métodos personalizados em vez de usar métodos de envio fornecidos com AEM Forms. Todas as ações mencionadas anteriormente e implementações personalizadas de APIs do AEM Forms não são contabilizadas como transações. O AEM Forms fornece uma API, [TransactionRecorder](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html), para registrar ações como transações.

Para registrar uma transação, escreva o servlet [](https://helpx.adobe.com/experience-manager/using/custom-sling-servlets.html) sling padrão e chame o servlet de um cliente para registrar uma transação. Você pode chamar o servlet usando AJAX ou qualquer outro método padrão.

## Exemplo de código do lado do servidor {#sample-server-sided-code}

Você pode usar o código de amostra abaixo para executar a API TransactionRecorder de uma classe JAVA usando um pacote OSGi personalizado.

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## Exemplo de código do cliente {#sample-client-side-code}

Você pode usar o código de amostra abaixo para chamar o servlet que tem a `TransactionRecorder`API.

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## Artigos relacionados {#related-articles}

* [Visão geral dos relatórios de transação](/help/forms/using/transaction-reports-overview.md)
* [Exibindo e Entendendo um Relatório de Transação](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [Relatórios de transação APIs faturáveis](/help/forms/using/transaction-reports-billable-apis.md)

