---
title: API para chamar o serviço de modelo de dados de formulário a partir de formulários adaptáveis
seo-title: API para chamar o serviço de modelo de dados de formulário a partir de formulários adaptáveis
description: Explica a API invokeWebServices que pode ser usada para invocar serviços da Web escritos em WSDL a partir de um campo de formulário adaptável.
seo-description: Explica a API invokeWebServices que pode ser usada para invocar serviços da Web escritos em WSDL a partir de um campo de formulário adaptável.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Formulários adaptáveis
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# API para chamar o serviço de modelo de dados de formulário a partir de formulários adaptáveis {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Visão geral {#overview}

O AEM Forms permite que os autores de formulários simplifiquem e aprimorem ainda mais a experiência de preenchimento de formulários, chamando serviços configurados em um modelo de dados de formulário de um campo de formulário adaptável. Para chamar um serviço de modelo de dados, você pode criar uma regra no editor visual ou especificar um JavaScript usando a API `guidelib.dataIntegrationUtils.executeOperation` no editor de códigos do [editor de regras](/help/forms/using/rule-editor.md).

Este documento foca em escrever um JavaScript usando a API `guidelib.dataIntegrationUtils.executeOperation` para chamar um serviço.

## Uso da API {#using-the-api}

A API `guidelib.dataIntegrationUtils.executeOperation` chama um serviço de dentro de um campo de formulário adaptável. A sintaxe da API é a seguinte:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

A estrutura da API `guidelib.dataIntegrationUtils.executeOperation` especifica detalhes sobre a operação do serviço. A sintaxe da estrutura é a seguinte.

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

A estrutura da API especifica os seguintes detalhes sobre a operação do serviço.

<table>
 <tbody>
  <tr>
   <th>Parâmetro</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>Estrutura para especificar o identificador do modelo de dados de formulário, o título da operação e o nome da operação</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>Especifica o caminho do repositório para o modelo de dados de formulário, incluindo seu nome</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Especifica o nome da operação de serviço a ser executada</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>Mapeia um ou mais objetos de formulário para os argumentos de entrada para a operação de serviço</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>Mapeia um ou mais objetos de formulário para valores de saída da operação de serviço para preencher campos de formulário<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Retorna valores com base nos argumentos de entrada para a operação de serviço. É um parâmetro opcional usado como uma função de retorno de chamada.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Exibe uma mensagem de erro se a função de retorno de chamada de sucesso não exibir os valores de saída com base nos argumentos de entrada. É um parâmetro opcional usado como uma função de retorno de chamada.<br /> </td>
  </tr>
 </tbody>
</table>

## Exemplo de script para chamar um serviço {#sample-script-to-invoke-a-service}

O script de amostra a seguir usa a API `guidelib.dataIntegrationUtils.executeOperation` para chamar a operação de serviço `getAccountById` configurada no modelo de dados de formulário `employeeAccount`.

A operação `getAccountById` assume o valor no campo de formulário `employeeID` como entrada para o argumento `empId` e retorna o nome do funcionário, o número da conta e o saldo da conta do funcionário correspondente. Os valores de saída são preenchidos nos campos de formulário especificados. Por exemplo, o valor no argumento `name` é preenchido no elemento de formulário `fullName` e no valor do argumento `accountNumber` no elemento de formulário `account`.

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## Uso da API com função de retorno de chamada {#using-the-api-callback}

Você também pode chamar o serviço de modelo de dados de formulário usando a API `guidelib.dataIntegrationUtils.executeOperation` com uma função de retorno de chamada. A sintaxe da API é a seguinte:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

A função de retorno de chamada pode ter `success` e `failure` funções de retorno de chamada.

### Exemplo de script com funções de retorno de chamada de sucesso e falha {#callback-function-success-failure}

O script de amostra a seguir usa a API `guidelib.dataIntegrationUtils.executeOperation` para chamar a operação de serviço `GETOrder` configurada no modelo de dados de formulário `employeeOrder`.

A operação `GETOrder` pega o valor no campo de formulário `Order ID` como entrada para o argumento `orderId` e retorna o valor da quantidade da ordem na função de retorno de chamada `success`.  Se a função de retorno de chamada `success` não retornar a quantidade do pedido, a função de retorno de chamada `failure` exibirá a mensagem `Error occured`.

>[!NOTE]
>
> Se você usar a função de retorno de chamada `success`, os valores de saída não serão preenchidos nos campos de formulário especificados.

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
