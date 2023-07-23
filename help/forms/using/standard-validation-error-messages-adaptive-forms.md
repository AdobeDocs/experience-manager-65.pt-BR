---
title: Mensagens de erro de validação padrão para formulários adaptáveis
seo-title: Standard validation error messages for adaptive forms
description: Transforme as mensagens de erro de validação para formulários adaptáveis em formato padrão usando manipuladores de erro personalizados
seo-description: Transform the validation error messages for adaptive forms into standard format using custom error handlers
uuid: 0d1f9835-3e28-41d3-a3b1-e36d95384328
contentOwner: anujkapo
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
discoiquuid: ec062567-1c6b-497b-a1e7-1dbac2d60852
feature: Adaptive Forms
exl-id: 54a76d5c-d19b-4026-b71c-7b9e862874bc
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---

# Mensagens de erro de validação padrão para formulários adaptáveis {#standard-validation-error-messages}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-br) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | Este artigo |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/add-custom-error-handler-adaptive-forms.html) |

Os formulários adaptáveis validam as entradas que você fornece nos campos com base em um critério de validação predefinido. Os critérios de validação se referem aos valores de entrada aceitáveis para campos em um formulário adaptável. Você pode definir os critérios de validação com base na fonte de dados usada com o formulário adaptável. Por exemplo, se você usar os serviços Web RESTful como fonte de dados, poderá definir os critérios de validação em um arquivo de definição do Swagger.

Se os valores de entrada atenderem aos critérios de validação, os valores serão enviados à fonte de dados. Caso contrário, o formulário adaptável exibirá uma mensagem de erro.

Semelhante a essa abordagem, os formulários adaptáveis agora podem se integrar aos serviços personalizados para executar validações de dados. Se os valores de entrada não atenderem aos critérios de validação e a mensagem de erro de validação que o servidor retornar estiver no formato de mensagem padrão, as mensagens de erro serão exibidas no nível do campo do formulário.

Se os valores de entrada não atenderem aos critérios de validação e a mensagem de erro de validação do servidor não estiver no formato de mensagem padrão, os formulários adaptáveis fornecerão um mecanismo para transformar as mensagens de erro de validação em um formato padrão para que sejam exibidas no nível de campo do formulário. Você pode transformar a mensagem de erro no formato padrão usando um dos dois métodos a seguir:

* Adicionar manipulador de erro personalizado no envio de formulário adaptável
* Adicionar manipulador personalizado à ação Chamar serviço usando o Editor de regras

Este artigo descreve o formato padrão das mensagens de erro de validação e as instruções para transformar as mensagens de erro de um formato personalizado no formato padrão.

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
* `errors` menção à expressão SOM dos campos que falharam nos critérios de validação junto com a mensagem de erro de validação
* `originCode` contém o código de erro retornado pelo serviço externo
* `originMessage` contém os dados de erro brutos retornados pelo serviço externo

## Configurar o envio de formulários adaptáveis para adicionar manipuladores personalizados {#configure-adaptive-form-submission}

Se a mensagem de erro de validação do servidor não for exibida no formato padrão, você poderá habilitar o envio assíncrono e adicionar um manipulador de erro personalizado no envio de formulário adaptável para converter a mensagem em um formato padrão.

### Configurar o envio assíncrono de formulários adaptáveis {#configure-asynchronous-adaptive-form-submission}

Antes de adicionar um manipulador personalizado, você deve configurar o formulário adaptável para envio assíncrono. Execute as seguintes etapas:

1. No modo de criação de formulário adaptável, selecione o objeto Contêiner de formulário e toque em ![propriedades do formulário adaptável](assets/configure_icon.png) para abrir suas propriedades.
1. No **[!UICONTROL Envio]** seção de propriedades, ativar **[!UICONTROL Usar envio assíncrono]**.
1. Selecionar **[!UICONTROL Revalidar no servidor]** para validar os valores do campo de entrada no servidor antes do envio.
1. Selecione a ação enviar:

   * Selecionar **[!UICONTROL Enviar usando modelo de dados do formulário]** e selecione o modelo de dados apropriado, se você estiver usando o serviço Web RESTful baseado [modelo de dados de formulário](work-with-form-data-model.md) como a fonte de dados.
   * Selecionar **[!UICONTROL Enviar para endpoint REST]** e especificar a **[!UICONTROL URL/caminho de redirecionamento]**, se você estiver usando os serviços Web RESTful como fonte de dados.

   ![propriedades de envio do formulário adaptável](assets/af_submission_properties.png)

1. Toque ![Salvar](assets/save_icon.png) para salvar as propriedades.

### Adicionar manipulador de erro personalizado no envio de formulário adaptável {#add-custom-error-handler-af-submission}

O AEM Forms fornece manipuladores de sucesso e erro prontos para uso para envios de formulários. Os manipuladores são funções do lado do cliente executadas com base na resposta do servidor. Quando um formulário é enviado, os dados são transmitidos ao servidor para validação, o que retorna uma resposta ao cliente com informações sobre o evento bem-sucedido ou com erro para o envio. As informações são passadas como parâmetros para o manipulador relevante para executar a função.

Execute as seguintes etapas para adicionar um manipulador de erro personalizado no envio de um formulário adaptável:

1. Abra o formulário adaptável no modo de criação, selecione qualquer objeto de formulário e toque em <!--![Rule Editor](assets/af_edit_rules.png)--> para abrir o editor de regras.
1. Selecionar **[!UICONTROL Formulário]** na árvore Objetos de formulário e toque em **[!UICONTROL Criar]**.
1. Selecionar **[!UICONTROL Erro no envio]** na lista suspensa Evento.
1. Escreva uma regra para converter a estrutura de erro personalizada na estrutura de erro padrão e toque em **[!UICONTROL Concluído]** para salvar a regra.

Este é um exemplo de código para converter uma estrutura de erro personalizada em uma estrutura de erro padrão:

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

A variável `var som_map` lista a expressão SOM dos campos de formulário adaptáveis que você deseja transformar no formato padrão. Você pode exibir a expressão SOM de qualquer campo em um formulário adaptável tocando no campo e selecionando **[!UICONTROL Exibir expressão SOM]**.

Usando esse manipulador de erros personalizado, o formulário adaptável converte os campos listados em `var som_map` para o formato padrão de mensagem de erro. Como resultado, as mensagens de erro de validação são exibidas no nível do campo no formulário adaptável.

## Adicionar manipulador personalizado usando a ação Chamar serviço

Execute as seguintes etapas para adicionar um manipulador de erros para converter uma estrutura de erros personalizada em uma estrutura de erros padrão usando [do Editor de regras](rule-editor.md) Chamar ação de serviço:

1. Abra o formulário adaptável no modo de criação, selecione qualquer objeto de formulário e toque em ![Editor de regras](assets/rule_editor_icon.png) para abrir o editor de regras.
1. Toque **[!UICONTROL Criar]**.
1. Crie uma condição no **[!UICONTROL Quando]** seção da regra. Por exemplo, Quando[Nome do campo] foi alterado. Selecionar **[!UICONTROL foi alterado]** do **[!UICONTROL Selecionar Estado]** para atingir essa condição.
1. No **[!UICONTROL Depois]** , selecione **[!UICONTROL Chamar serviço]** do **[!UICONTROL Selecionar ação]** lista suspensa.
1. Selecione um serviço de Postagem e seus vínculos de dados correspondentes na **[!UICONTROL Entrada]** seção. Por exemplo, se você deseja validar **Nome**, **ID**, e **Status** no formulário adaptável, selecione um Serviço de publicação (pet) e selecione pet.name, pet.id e pet.status no **[!UICONTROL Entrada]** seção.

Como resultado dessa regra, os valores inseridos para **Nome**, **ID**, e **Status** Os campos são validados assim que o campo definido na etapa 2 é alterado e você faz a tabulação para fora do campo no formulário.

1. Selecionar **[!UICONTROL Editor de código]** na lista suspensa de seleção de modo.
1. Toque **[!UICONTROL Editar código]**.
1. Exclua a seguinte linha do código existente:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
   ```

1. Escreva uma regra para converter a estrutura de erro personalizada na estrutura de erro padrão e toque em **[!UICONTROL Concluído]** para salvar a regra.
Por exemplo, adicione o seguinte código de amostra no final para converter uma estrutura de erro personalizada em estrutura de erro padrão:

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

   A variável `var som_map` lista a expressão SOM dos campos de formulário adaptáveis que você deseja transformar no formato padrão. Você pode exibir a expressão SOM de qualquer campo em um formulário adaptável tocando no campo e selecionando **[!UICONTROL Exibir expressão SOM]** de **[!UICONTROL Mais opções]** (...).

   Certifique-se de copiar a seguinte linha do código de amostra para o manipulador de erros personalizado:

   ```javascript
   guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, null, errorHandler);
   ```

   A API executeOperation inclui a variável `null` e `errorHandler` parâmetros com base no novo manipulador de erros personalizado.

   Usando esse manipulador de erros personalizado, o formulário adaptável converte os campos listados em `var som_map` para o formato padrão de mensagem de erro. Como resultado, as mensagens de erro de validação são exibidas no nível do campo no formulário adaptável.
