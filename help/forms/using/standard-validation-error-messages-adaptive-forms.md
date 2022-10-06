---
title: Mensagens de erro de validação padrão para formulários adaptáveis
seo-title: Standard validation error messages for adaptive forms
description: Transformar as mensagens de erro de validação para formulários adaptáveis em formato padrão usando manipuladores de erro personalizados
seo-description: Transform the validation error messages for adaptive forms into standard format using custom error handlers
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Adaptive Forms
exl-id: 54a76d5c-d19b-4026-b71c-7b9e862874bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---

# Mensagens de erro de validação padrão para formulários adaptáveis {#standard-validation-error-messages}

Os formulários adaptáveis validam as entradas fornecidas nos campos com base em um critério de validação predefinido. Os critérios de validação se referem aos valores de entrada aceitáveis para campos em um formulário adaptável. Você pode definir os critérios de validação com base na fonte de dados usada com o formulário adaptável. Por exemplo, se você usar serviços Web RESTful como fonte de dados, poderá definir os critérios de validação em um arquivo de definição Swagger.

Se os valores de entrada atenderem aos critérios de validação, eles serão enviados para a fonte de dados. Caso contrário, o formulário adaptável exibe uma mensagem de erro.

Semelhante a essa abordagem, os formulários adaptáveis agora podem se integrar a serviços personalizados para executar validações de dados. Se os valores de entrada não atenderem aos critérios de validação e a mensagem de erro de validação retornada pelo servidor estiver no formato de mensagem padrão, as mensagens de erro serão exibidas no nível do campo no formulário.

Se os valores de entrada não atenderem aos critérios de validação e a mensagem de erro de validação do servidor não estiver no formato de mensagem padrão, os formulários adaptáveis fornecerão um mecanismo para transformar as mensagens de erro de validação em um formato padrão, para que sejam exibidas no nível do campo no formulário. Você pode transformar a mensagem de erro no formato padrão usando qualquer um dos dois métodos a seguir:

* Adicionar manipulador de erro personalizado no envio do formulário adaptável
* Adicionar manipulador personalizado à ação Invocar serviço usando o Editor de regras

Este artigo descreve o formato padrão para as mensagens de erro de validação e as instruções para transformar as mensagens de erro de um formato personalizado para o padrão.

## Formato de mensagem de erro de validação padrão {#standard-validation-message-format}

Os formulários adaptáveis exibem os erros no nível do campo se as mensagens de erro de validação do servidor estiverem no seguinte formato padrão:

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             somExpression  : <somexpr>
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]

        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
}
```

Em que:

* `errorCausedBy` descreve a razão da falha
* `errors` menção à expressão SOM dos campos que falharam nos critérios de validação junto com a mensagem de erro de validação
* `originCode` contém o código de erro retornado pelo serviço externo
* `originMessage` contém os dados de erro brutos retornados pelo serviço externo

## Configurar o envio de formulário adaptável para adicionar manipuladores personalizados {#configure-adaptive-form-submission}

Se a mensagem de erro de validação do servidor não for exibida no formato padrão, é possível habilitar o envio assíncrono e adicionar um manipulador de erros personalizado no envio do formulário adaptável para converter a mensagem em um formato padrão.

### Configurar envio de formulário adaptável assíncrono {#configure-asynchronous-adaptive-form-submission}

Antes de adicionar um manipulador personalizado, é necessário configurar o formulário adaptável para envio assíncrono. Execute as seguintes etapas:

1. No modo de criação de formulário adaptável, selecione o objeto Contêiner de formulário e toque em ![propriedades do formulário adaptável](assets/configure_icon.png) para abrir suas propriedades.
1. No **[!UICONTROL Submissão]** seção propriedades, habilitar **[!UICONTROL Usar envio assíncrono]**.
1. Selecionar **[!UICONTROL Revalidar no servidor]** para validar os valores do campo de entrada no servidor antes do envio.
1. Selecione a ação Enviar:

   * Selecionar **[!UICONTROL Enviar usando o Modelo de dados de formulário]** e selecione o modelo de dados apropriado, se estiver usando o serviço Web RESTful baseado [modelo de dados de formulário](work-with-form-data-model.md) como fonte de dados.
   * Selecionar **[!UICONTROL Enviar para ponto de extremidade REST]** e especifique o **[!UICONTROL Redirecionar URL/caminho]**, se estiver usando serviços da Web RESTful como a fonte de dados.

   ![propriedades de envio de formulário adaptável](assets/af_submission_properties.png)

1. Toque ![Salvar](assets/save_icon.png) para salvar as propriedades.

### Adicionar manipulador de erro personalizado no envio do formulário adaptável {#add-custom-error-handler-af-submission}

O AEM Forms fornece manipuladores de erros e sucesso prontos para uso para envios de formulários. Os manipuladores são funções do lado do cliente que são executadas com base na resposta do servidor. Quando um formulário é enviado, os dados são transmitidos ao servidor para validação, o que retorna uma resposta ao cliente com informações sobre o sucesso ou o evento de erro do envio. As informações são passadas como parâmetros para o manipulador relevante para executar a função.

Execute as etapas a seguir para adicionar o manipulador de erros personalizado no envio do formulário adaptável:

1. Abra o formulário adaptável no modo de criação, selecione qualquer objeto de formulário e toque em <!--![Rule Editor](assets/af_edit_rules.png)--> para abrir o editor de regras.
1. Selecionar **[!UICONTROL Formulário]** na árvore Objetos de formulário e toque em **[!UICONTROL Criar]**.
1. Selecionar **[!UICONTROL Erro no envio]** na lista suspensa Evento .
1. Escreva uma regra para converter a estrutura de erro personalizada na estrutura de erro padrão e toque em **[!UICONTROL Concluído]** para salvar a regra.

Veja a seguir um exemplo de código para converter uma estrutura de erro personalizada na estrutura de erro padrão:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

O `var som_map` lista a expressão SOM dos campos de formulário adaptáveis que você deseja transformar no formato padrão. Você pode exibir a expressão SOM de qualquer campo em um formulário adaptável tocando no campo e selecionando **[!UICONTROL Exibir expressão SOM]**.

Usando esse manipulador de erros personalizado, o formulário adaptável converte os campos listados em `var som_map` para o formato padrão de mensagem de erro. Como resultado, as mensagens de erro de validação são exibidas no nível do campo no formulário adaptável.

## Adicionar manipulador personalizado usando a ação Invoque Service

Execute as etapas a seguir para adicionar o manipulador de erros para converter uma estrutura de erro personalizada na estrutura de erro padrão usando [Editor de regras](rule-editor.md) Invocar ação do Serviço:

1. Abra o formulário adaptável no modo de criação, selecione qualquer objeto de formulário e toque em ![Editor de regras](assets/rule_editor_icon.png) para abrir o editor de regras.
1. Toque **[!UICONTROL Criar]**.
1. Crie uma condição no **[!UICONTROL When]** da regra. Por exemplo, Quando[Nome do campo] é alterada. Selecionar **[!UICONTROL é alterado]** do **[!UICONTROL Selecionar Estado]** lista suspensa para atingir essa condição.
1. No **[!UICONTROL Então]** seção , selecione **[!UICONTROL Chamar serviço]** do **[!UICONTROL Selecionar ação]** lista suspensa.
1. Selecione um Serviço de postagem e seus vínculos de dados correspondentes no **[!UICONTROL Entrada]** seção. Por exemplo, se você deseja validar **Nome**, **ID** e **Status** no formulário adaptável, selecione um Serviço de publicação (pet) e selecione pet.name, pet.id e pet.status na **[!UICONTROL Entrada]** seção.

Como resultado dessa regra, os valores inseridos para **Nome**, **ID** e **Status** Os campos são validados, assim que o campo definido na etapa 2 é alterado e você sai do campo do formulário.

1. Selecionar **[!UICONTROL Editor de códigos]** na lista suspensa seleção de modo .
1. Toque **[!UICONTROL Editar código]**.
1. Exclua a seguinte linha do código existente:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. Escreva uma regra para converter a estrutura de erro personalizada na estrutura de erro padrão e toque em **[!UICONTROL Concluído]** para salvar a regra.
Por exemplo, adicione o seguinte código de amostra no final para converter uma estrutura de erro personalizada na estrutura de erro padrão:

   ```javascript
   var errorHandler = function(jqXHR, data) {
   var som_map = {
       "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
       "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
       "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
   };
   
   
   var errorJson = {};
   errorJson.errors = [];
   
   if (data) {
       if (data.originMessage) {
           var errorData;
           try {
               errorData = JSON.parse(data.originMessage);
           } catch (err) {
               // not in json format
           }
   
           if (errorData) {
               Object.keys(errorData).forEach(function(key) {
                   var som_key = som_map[key];
                   if (som_key) {
                       var error = {};
                       error.somExpression = som_key;
                       error.errorMessage = errorData[key];
                       errorJson.errors.push(error);
                   }
               });
           }
           window.guideBridge.handleServerValidationError(errorJson);
       } else {
           window.guideBridge.handleServerValidationError(data);
       }
     }
   };
   
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   O `var som_map` lista a expressão SOM dos campos de formulário adaptáveis que você deseja transformar no formato padrão. Você pode exibir a expressão SOM de qualquer campo em um formulário adaptável tocando no campo e selecionando **[!UICONTROL Exibir expressão SOM]** from **[!UICONTROL Mais opções]** (...).

   Certifique-se de copiar a seguinte linha do código de amostra para o manipulador de erros personalizado:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   A API executeOperation inclui a variável `null` e `errorHandler` parâmetros com base no novo manipulador de erros personalizado.

   Usando esse manipulador de erros personalizado, o formulário adaptável converte os campos listados em `var som_map` para o formato padrão de mensagem de erro. Como resultado, as mensagens de erro de validação são exibidas no nível do campo no formulário adaptável.
