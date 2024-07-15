---
title: API para chamar o serviço de modelo de dados de formulário a partir de formulários adaptáveis
description: Explica a API invokeWebServices que você pode usar para chamar serviços da Web escritos em WSDL de dentro de um campo de formulário adaptável.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms,Foundation Components
exl-id: cf037174-3153-486f-85b1-c974cd5a1ace
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# API para chamar o serviço de modelo de dados de formulário a partir de formulários adaptáveis {#api-to-invoke-form-data-model-service-from-adaptive-forms}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

## Visão geral {#overview}

O AEM Forms permite que os autores de formulários simplifiquem e aprimorem ainda mais a experiência de preenchimento, chamando serviços configurados em um modelo de dados de formulário de dentro de um campo de formulário adaptável. Para invocar um serviço de modelo de dados, você pode criar uma regra no editor visual ou especificar um JavaScript usando a API `guidelib.dataIntegrationUtils.executeOperation` no editor de códigos do [editor de regras](/help/forms/using/rule-editor.md).

Este documento se concentra na gravação de um JavaScript usando a API `guidelib.dataIntegrationUtils.executeOperation` para invocar um serviço.

## Uso da API {#using-the-api}

A API `guidelib.dataIntegrationUtils.executeOperation` invoca um serviço de dentro de um campo de formulário adaptável. A sintaxe da API é a seguinte:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

A estrutura da API `guidelib.dataIntegrationUtils.executeOperation` especifica detalhes sobre a operação de serviço. A sintaxe da estrutura é a seguinte:

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

A estrutura da API especifica os seguintes detalhes sobre a operação de serviço.

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
   <td>Mapeia um ou mais objetos de formulário para os argumentos de entrada da operação de serviço</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>Mapeia um ou mais objetos de formulário para valores de saída da operação de serviço para preencher campos de formulário<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Retorna valores com base nos argumentos de entrada da operação de serviço. É um parâmetro opcional usado como função de retorno de chamada.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Exibe uma mensagem de erro se a função de retorno de chamada bem-sucedida falhar ao exibir os valores de saída com base nos argumentos de entrada. É um parâmetro opcional usado como função de retorno de chamada.<br /> </td>
  </tr>
 </tbody>
</table>

## Exemplo de script para chamar um serviço {#sample-script-to-invoke-a-service}

O exemplo de script a seguir usa a API `guidelib.dataIntegrationUtils.executeOperation` para invocar a operação de serviço `getAccountById` configurada no modelo de dados de formulário `employeeAccount`.

A operação `getAccountById` usa o valor no campo de formulário `employeeID` como entrada para o argumento `empId` e retorna o nome do funcionário, o número da conta e o saldo da conta para o funcionário correspondente. Os valores de saída são preenchidos nos campos de formulário especificados. Por exemplo, o valor no argumento `name` é preenchido no elemento de formulário `fullName` e o valor para o argumento `accountNumber` no elemento de formulário `account`.

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

Você também pode invocar o serviço de modelo de dados de formulário usando a API `guidelib.dataIntegrationUtils.executeOperation` com uma função de retorno de chamada. A sintaxe da API é a seguinte:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

A função de retorno de chamada pode ter `success` e `failure` funções de retorno de chamada.

### Exemplo de script com funções de retorno de chamada de sucesso e falha {#callback-function-success-failure}

O exemplo de script a seguir usa a API `guidelib.dataIntegrationUtils.executeOperation` para invocar a operação de serviço `GETOrder` configurada no modelo de dados de formulário `employeeOrder`.

A operação `GETOrder` usa o valor no campo de formulário `Order ID` como entrada para o argumento `orderId` e retorna o valor da quantidade da ordem na função de retorno de chamada `success`.  Se a função de retorno de chamada `success` não retornar a quantidade da ordem, a função de retorno de chamada `failure` exibirá a mensagem `Error occured`.

>[!NOTE]
>
>Se você usar a função de retorno de chamada `success`, os valores de saída não serão preenchidos nos campos de formulário especificados.

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
