---
title: Mensagens de erro de validação padrão para formulários adaptáveis
seo-title: Mensagens de erro de validação padrão para formulários adaptáveis
description: Transforme as mensagens de erro de validação para formulários adaptáveis em formato padrão usando manipuladores de erro personalizados
seo-description: Transforme as mensagens de erro de validação para formulários adaptáveis em formato padrão usando manipuladores de erro personalizados
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 0%

---


# Mensagens de erro de validação padrão para formulários adaptáveis {#standard-validation-error-messages}

Os formulários adaptáveis validam as entradas fornecidas nos campos com base em um critério de validação predefinido. Os critérios de validação se referem aos valores de entrada aceitáveis para campos em um formulário adaptável. É possível definir os critérios de validação com base na fonte de dados usada com o formulário adaptável. Por exemplo, se você usar os serviços Web RESTful como a fonte de dados, poderá definir os critérios de validação em um arquivo de definição Swagger.

Se os valores de entrada atenderem aos critérios de validação, eles serão enviados para a fonte de dados. Caso contrário, o formulário adaptativo exibirá uma mensagem de erro.

Semelhante a essa abordagem, os formulários adaptáveis agora podem se integrar aos serviços personalizados para executar validações de dados. Se os valores de entrada não atenderem aos critérios de validação e a mensagem de erro de validação retornada pelo servidor estiver no formato de mensagem padrão, as mensagens de erro serão exibidas no nível do campo no formulário.

Se os valores de entrada não atenderem aos critérios de validação e a mensagem de erro de validação do servidor não estiver no formato de mensagem padrão, os formulários adaptativos fornecerão um mecanismo para transformar as mensagens de erro de validação em um formato padrão, de modo que sejam exibidas no nível do campo no formulário. É possível transformar a mensagem de erro no formato padrão usando qualquer um dos dois métodos a seguir:

* Adicionar manipulador de erros personalizado no envio de formulário adaptável
* Adicionar manipulador personalizado à ação Chamar serviço usando o Editor de regras

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

* `errorCausedBy` descreve o motivo da falha
* `errors` mencionar a expressão SOM dos campos que falharam nos critérios de validação junto com a mensagem de erro de validação
* `originCode` contém o código de erro retornado pelo serviço externo
* `originMessage` contém os dados de erro brutos retornados pelo serviço externo

## Configurar envio de formulário adaptável para adicionar manipuladores personalizados {#configure-adaptive-form-submission}

Se a mensagem de erro de validação do servidor não for exibida no formato padrão, você poderá ativar o envio assíncrono e adicionar um manipulador de erros personalizado no envio do formulário adaptável para converter a mensagem em um formato padrão.

### Configurar envio de formulário adaptável assíncrono {#configure-asynchronous-adaptive-form-submission}

Antes de adicionar o manipulador personalizado, é necessário configurar o formulário adaptável para envio assíncrono. Execute as seguintes etapas:

1. No modo de criação de formulário adaptável, selecione o objeto Container de formulário e toque em Propriedades ![de formulário](assets/configure_icon.png) adaptável para abrir suas propriedades.
1. Na seção Propriedades de **[!UICONTROL envio]** , ative **[!UICONTROL Usar envio]** assíncrono.
1. Selecione **[!UICONTROL Revalidar no servidor]** para validar os valores de campo de entrada no servidor antes do envio.
1. Selecione a Ação Enviar:

   * Selecione **[!UICONTROL Enviar usando o Modelo]** de dados de formulário e selecione o modelo de dados apropriado se estiver usando o modelo [de dados de](work-with-form-data-model.md) formulário com base no serviço Web RESTful como fonte de dados.
   * Selecione **[!UICONTROL Enviar para ponto de extremidade]** REST e especifique o URL/caminho **[!UICONTROL de]** redirecionamento se você estiver usando os serviços Web RESTful como a fonte de dados.

   ![propriedades adaptáveis de envio de formulário](assets/af_submission_properties.png)

1. Toque em ![Salvar](assets/save_icon.png) para salvar as propriedades.

### Adicionar manipulador de erros personalizado no envio de formulário adaptável {#add-custom-error-handler-af-submission}

O AEM Forms fornece controladores de erros e sucesso prontos para uso para envios de formulário. Os manipuladores são funções do lado do cliente que são executadas com base na resposta do servidor. Quando um formulário é submetido, os dados são transmitidos ao servidor para validação, o que retorna uma resposta ao cliente com informações sobre o evento bem-sucedido ou erro para o envio. As informações são passadas como parâmetros para o manipulador relevante para executar a função.

Execute as seguintes etapas para adicionar o manipulador de erros personalizado no envio do formulário adaptável:

1. Abra o formulário adaptável no modo de criação, selecione qualquer objeto de formulário e toque em <!--![Rule Editor](assets/af_edit_rules.png)--> para abrir o editor de regras.
1. Selecione **[!UICONTROL Formulário]** na árvore Objetos de formulário e toque em **[!UICONTROL Criar]**.
1. Selecione **[!UICONTROL Erro no envio]** na lista suspensa Evento.
1. Grave uma regra para converter a estrutura de erro personalizada para a estrutura de erro padrão e toque em **[!UICONTROL Concluído]** para salvar a regra.

A seguir está um exemplo de código para converter uma estrutura de erro personalizada para a estrutura de erro padrão:

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

O `var som_map` lista a expressão SOM dos campos de formulário adaptáveis que você deseja transformar no formato padrão. Você pode visualização a expressão SOM de qualquer campo em um formulário adaptável tocando no campo e selecionando Expressão **[!UICONTROL SOM de]** Visualização.

Usando esse manipulador de erros personalizado, o formulário adaptável converte os campos listados em `var som_map` para o formato de mensagem de erro padrão. Como resultado, as mensagens de erro de validação são exibidas no nível do campo no formulário adaptável.

## Adicionar manipulador personalizado usando a ação Chamar serviço

Execute as seguintes etapas para adicionar o manipulador de erros para converter uma estrutura de erro personalizada na estrutura de erro padrão usando a ação Invocar serviço do Editor de [regras](rule-editor.md) :

1. Abra o formulário adaptável no modo de criação, selecione qualquer objeto de formulário e toque em Editor ![de](assets/rule_editor_icon.png) regras para abrir o editor de regras.
1. Toque em **[!UICONTROL Criar]**.
1. Crie uma condição na seção **[!UICONTROL Quando]** da regra. Por exemplo,[WhenName do campo] é alterado. A seleção **[!UICONTROL é alterada]** na lista suspensa **[!UICONTROL Selecionar estado]** para obter essa condição.
1. Na seção **[!UICONTROL Então]** , selecione **[!UICONTROL Chamar serviço]** na lista suspensa **[!UICONTROL Selecionar ação]** .
1. Selecione um serviço de Postagem e seus vínculos de dados correspondentes na seção **[!UICONTROL Entrada]** . Por exemplo, se você quiser validar os campos **Nome**, **ID** e **Status** no formulário adaptável, selecione um serviço de Post (pet) e selecione pet.name, pet.id e pet.status na seção **[!UICONTROL Input]** .

Como resultado dessa regra, os valores inseridos para os campos **Nome**, **ID** e **Status** são validados, assim que o campo definido na etapa 2 é alterado e você sai do campo do formulário.

1. Selecione Editor **[!UICONTROL de]** código na lista suspensa de seleção de modo.
1. Toque em **[!UICONTROL Editar código]**.
1. Exclua a seguinte linha do código existente:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. Grave uma regra para converter a estrutura de erro personalizada para a estrutura de erro padrão e toque em **[!UICONTROL Concluído]** para salvar a regra.
Por exemplo, adicione o seguinte código de amostra no final para converter uma estrutura de erro personalizada para a estrutura de erro padrão:

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

   O `var som_map` lista a expressão SOM dos campos de formulário adaptáveis que você deseja transformar no formato padrão. Você pode visualização a expressão SOM de qualquer campo em um formulário adaptável tocando no campo e selecionando **[!UICONTROL Visualização]** SOM no menu **[!UICONTROL Mais opções]** (...).

   Certifique-se de copiar a seguinte linha do código de amostra para o manipulador de erros personalizado:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   A API executeOperation inclui os parâmetros `null` e `errorHandler` com base no novo manipulador de erros personalizado.

   Usando esse manipulador de erros personalizado, o formulário adaptável converte os campos listados em `var som_map` para o formato de mensagem de erro padrão. Como resultado, as mensagens de erro de validação são exibidas no nível do campo no formulário adaptável.