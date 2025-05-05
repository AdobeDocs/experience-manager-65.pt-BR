---
title: Registrar uma transação para implementações personalizadas
description: Use a API TransactionRecorder para registrar ações que não são contabilizadas como transações automaticamente.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
feature: Transaction Reports
exl-id: b0c4f72a-e65f-453a-af66-5d9f98a9d6df
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: acb023caf0a7e64fea9cf5d9198d672ee14c8d88
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 6%

---

# Registrar uma transação para implementações personalizadas do AEM Forms no OSGi {#record-a-transaction-for-custom-implementations}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/using-communications/record-transaction-custom-implementation) |
| AEM 6.5 | Este artigo |

Usar a API TransactionRecorder para registrar ações que não são contabilizadas como transações automaticamente

Você pode usar o código personalizado para enviar um Formulário PDF ou enviar o URL de visualização da interface do usuário do agente para os usuários finais visualizarem uma comunicação interativa. Ou você envia um formulário usando métodos personalizados em vez de usar os métodos de envio fornecidos com o AEM Forms. Todas as ações mencionadas anteriormente e implementações personalizadas de APIs do AEM Forms não são contabilizadas como transações. A AEM Forms fornece uma API, [TransactionRecorder](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html), para registrar essas ações, como transações.

Para registrar uma transação, escreva o [servlet sling padrão](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=pt-BR) e chame o servlet de um cliente para registrar uma transação. Você pode chamar o servlet usando AJAX ou qualquer outro método padrão.

## Código de exemplo do lado do servidor {#sample-server-sided-code}

Você pode usar o código de amostra abaixo para executar a API TransactionRecorder a partir de uma classe Java™ usando um pacote OSGi personalizado.

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

## Código de exemplo do lado do cliente {#sample-client-side-code}

Você pode usar o código de amostra abaixo para chamar o servlet que tem a API `TransactionRecorder`.

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

* [Visão geral dos relatórios de transação para o AEM Forms no OSGi](/help/forms/using/transaction-reports-overview.md)
* [Visualização e noções básicas de relatórios de transação para o AEM Forms no OSGi](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [APIs faturáveis de relatórios de transação para o AEM Forms no OSGi](/help/forms/using/transaction-reports-billable-apis.md)
