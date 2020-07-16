---
title: API para chamar o serviço de modelo de dados de formulário a partir de formulários adaptáveis
seo-title: API para chamar o serviço de modelo de dados de formulário a partir de formulários adaptáveis
description: Explica a API invokeWebServices que você pode usar para chamar serviços da Web escritos em WSDL de dentro de um campo de formulário adaptável.
seo-description: Explica a API invokeWebServices que você pode usar para chamar serviços da Web escritos em WSDL de dentro de um campo de formulário adaptável.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
translation-type: tm+mt
source-git-commit: adf1ac2cb84049ca7e42921ce31135a6149ef510
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---


# API para chamar o serviço de modelo de dados de formulário a partir de formulários adaptáveis {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Visão geral {#overview}

O AEM Forms permite que os autores de formulários simplifiquem e aprimorem ainda mais a experiência de preenchimento de formulários, chamando os serviços configurados em um modelo de dados de formulário a partir de um campo de formulário adaptável. Para chamar um serviço de modelo de dados, você pode criar uma regra no editor visual ou especificar um JavaScript usando a `guidelib.dataIntegrationUtils.executeOperation` API no editor de código do editor [de](/help/forms/using/rule-editor.md)regras.

Esse documento se concentra em escrever um JavaScript usando a `guidelib.dataIntegrationUtils.executeOperation` API para chamar um serviço.

## Uso da API {#using-the-api}

A `guidelib.dataIntegrationUtils.executeOperation` API chama um serviço de dentro de um campo de formulário adaptável. A sintaxe da API é a seguinte:

```
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

A estrutura da `guidelib.dataIntegrationUtils.executeOperation` API especifica detalhes sobre a operação do serviço. A sintaxe da estrutura é a seguinte.

```
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
   <td>Estrutura para especificar o identificador do modelo de dados do formulário, o título da operação e o nome da operação</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>Especifica o caminho do repositório para o modelo de dados do formulário, incluindo seu nome</td>
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
   <td>Retorna valores com base nos argumentos de entrada para a operação de serviço. É um parâmetro opcional usado como função de retorno de chamada.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Exibe uma mensagem de erro se a função de retorno de sucesso não exibir os valores de saída com base nos argumentos de entrada. É um parâmetro opcional usado como função de retorno de chamada.<br /> </td>
  </tr>
 </tbody>
</table>

## Exemplo de script para chamar um serviço {#sample-script-to-invoke-a-service}

O script de amostra a seguir usa a `guidelib.dataIntegrationUtils.executeOperation` API para chamar a operação de `getAccountById` serviço configurada no modelo de dados de `employeeAccount` formulário.

A `getAccountById` operação usa o valor no campo de `employeeID` formulário como entrada para o `empId` argumento e retorna o nome do funcionário, o número da conta e o saldo da conta do funcionário correspondente. Os valores de saída são preenchidos nos campos de formulário especificados. Por exemplo, o valor no `name` argumento é preenchido no elemento de `fullName` formulário e no valor do `accountNumber` argumento no elemento de `account` formulário.

```
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

## Uso da API com a função de retorno de chamada {#using-the-api-callback}

Também é possível chamar o serviço de modelo de dados de formulário usando a `guidelib.dataIntegrationUtils.executeOperation` API com uma função de retorno de chamada. A sintaxe da API é a seguinte:

```
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

A função de retorno de chamada pode ter funções `success` e `failure` retorno de chamada.

### Exemplo de script com funções de retorno de sucesso e falha {#callback-function-success-failure}

O script de amostra a seguir usa a `guidelib.dataIntegrationUtils.executeOperation` API para chamar a operação de `GETOrder` serviço configurada no modelo de dados de `employeeOrder` formulário.

A `GETOrder` operação usa o valor no campo de `Order ID` formulário como entrada para o `orderId` argumento e retorna o valor da quantidade da ordem na função de `success` callback.  Se a função de `success` retorno de chamada não retornar a quantidade da ordem, a função de `failure` retorno de chamada exibirá a `Error occured` mensagem.

>[!NOTE]
>
> Se você usar a função `success` callback, os valores de saída não serão preenchidos nos campos de formulário especificados.

```
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
