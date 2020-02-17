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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# API para chamar o serviço de modelo de dados de formulário a partir de formulários adaptáveis {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Visão geral {#overview}

O AEM Forms permite que os autores de formulários simplifiquem e aprimorem ainda mais a experiência de preenchimento de formulários, chamando os serviços configurados em um modelo de dados de formulário de um campo de formulário adaptável. Para chamar um serviço de modelo de dados, você pode criar uma regra no editor visual ou especificar um JavaScript usando a `guidelib.dataIntegrationUtils.executeOperation` API no editor de código do editor [de](/help/forms/using/rule-editor.md)regras.

Este documento foca em gravar um JavaScript usando a `guidelib.dataIntegrationUtils.executeOperation` API para chamar um serviço.

## Uso da API {#using-the-api}

A `guidelib.dataIntegrationUtils.executeOperation` API chama um serviço de dentro de um campo de formulário adaptável. A sintaxe da API é a seguinte:

```
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

A API exige os seguintes parâmetros.

| Parâmetro | Descrição |
|---|---|
| `operationInfo` | Estrutura para especificar o identificador do modelo de dados do formulário, o título da operação e o nome da operação |
| `inputs` | Estrutura para especificar objetos de formulário cujos valores são inseridos na operação de serviço |
| `outputs` | Estrutura para especificar objetos de formulário que serão preenchidos com os valores retornados pela operação de serviço |

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
   <td><code>forDataModelId</code></td>
   <td>Especifique o caminho do repositório para o modelo de dados do formulário, incluindo seu nome</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Especifique o nome da operação de serviço a ser executada</td>
  </tr>
  <tr>
   <td><code>input</code></td>
   <td>Mapeie um ou mais objetos de formulário para os argumentos de entrada para a operação de serviço</td>
  </tr>
  <tr>
   <td>Saída</td>
   <td>Mapeie um ou mais objetos de formulário para valores de saída da operação de serviço para preencher campos de formulário<br /> </td>
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

