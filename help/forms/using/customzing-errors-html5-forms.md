---
title: Personalização de mensagens de erro para formulários HTML5
seo-title: Personalização de mensagens de erro para formulários HTML5
description: Saiba como personalizar a exibição de mensagens de erro para formulários HTML5, incluindo como alterar sua posição e aparência.
seo-description: Saiba como personalizar a exibição de mensagens de erro para formulários HTML5, incluindo como alterar sua posição e aparência.
uuid: 6f48b64e-858f-4323-ad50-88e25f3c2e3d
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 44e49789-9075-41b3-bce8-03e8efce2d5a
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# Personalização de mensagens de erro para formulários HTML5 {#customizing-error-messages-for-html-forms}

Em formulários HTML5, na caixa, as mensagens de erro e os avisos têm uma posição e aparência fixas (fonte e cor), o erro é exibido somente para um campo selecionado e apenas um erro é exibido.

O artigo fornece as etapas para personalizar mensagens de erro de formulários HTML5 para,

* altere a aparência e a posição das mensagens de erro. Você pode fazer com que um erro apareça na parte superior, inferior e à direita de qualquer campo.
* exibir mensagens de erro para vários campos em qualquer momento.
* exiba o erro independentemente de um campo estar selecionado ou não.

## Personalização de mensagens de erro  {#customizing-error-messages-nbsp}

Antes de personalizar as mensagens de erro, baixe e extraia o pacote anexado (CustomErrorManager-1.0-SNAPSHOT.zip).

Depois de extrair o pacote, abra a pasta CustomErrorManager-1.0-SNAPSHOT. Ele contém pastas jcr_root e META-INF. Essas pastas contêm os arquivos CSS e .JS necessários para personalizar a mensagem de erro.

[Obter arquivo](assets/customerrormanager-1.0-snapshot.zip)

### Personalização da posição das mensagens de erro  {#customizing-the-position-of-error-messages-nbsp}

Para personalizar a posição da mensagem de erro, adicione a tag &lt;div> para cada campo de erro e aviso, posicione a tag &lt;div> à esquerda ou à direita e aplique estilos css na tag &lt;div>. Para ver as etapas detalhadas, consulte o procedimento listado abaixo:

1. Navegue até a `CustomErrorManager-1.0-SNAPSHOT`pasta e abra a `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` pasta.
1. Open the `customErrorManager.js` file for editing. A `markError` função no arquivo aceita os seguintes parâmetros:

   |  |  |
   |---|---|
   | jqWidget | jqWidget é o identificador do widget. |
   | msg | contém a mensagem de erro |
   | tipo | indica se é um erro ou um aviso |

1. Na implementação imediata, mensagens de erro são exibidas à direita do campo. Para que as mensagens de erro apareçam na parte superior, use o seguinte código.

   ```javascript
   markError: function (jqWidget, msg, type) {
               var element = jqWidget.element,                                //Gives the div containing widget
                   pos = $(element).offset(),                          //Calculates the position of the div in the view port
                                                                   msgHeight = xfalib.view.util.TextMetrics.measureExtent(msg).height + 5;  //Calculating the height of the Error Message
                   styles = {};
                   styles.left = pos.left + "px";         // Assign the desired left position using pos.left. Here it is calculated for exact left of the field
                   styles.top = pos.top - msgHeight + "px";  // Assign the desired top position using pos.top. Here it is calculated for top of the field
               if (type != "warning") {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the warning div if it is not present already
                       jqWidget.errorDiv=$("<div id='customError'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the warning div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               } else {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the error div if it is not present already
                       jqWidget.errorDiv=$("<div id='customWarning'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the error div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               }
   
           },
   ```

1. Salve e feche o arquivo.
1. Navegue até a `CustomErrorManager-1.0-SNAPSHOT` pasta e crie um arquivo de pastas jcr_root e META-INF. Renomeie o arquivo como CustomErrorManager-1.0-SNAPSHOT.zip.
1. Use o gerenciador de pacote para fazer upload e instalar o pacote.

## Exibir mensagens de erro para vários campos  {#display-error-messages-for-multiple-fields-nbsp}

Use o pacote anexado para exibir simultaneamente mensagens de erro para todos os campos. Para exibir uma única mensagem de erro, use o perfil padrão.

### Personalizar a aparência de mensagens de erro.  {#customizing-the-appearance-of-error-messages-nbsp}

1. Navegue até o diretório etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css folder.

1. Abra o arquivo sample.css para edição.O arquivo css contém 2 ids - #customError, #customWarning. É possível usar essas IDs para alterar várias propriedades, como cor, tamanho da fonte etc.

   Use o seguinte código para alterar o tamanho e a cor da fonte das mensagens de erro/aviso.

   ```css
   #customError {
   color: #0000FF; // it changes the color of Error Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 24px;  // it changes the font size of Error Message
   z-index:5;
   }
   
   #customWarning {
   color: #00FF00;  // it changes the color of Warning Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 18px;   // it changes the font size of Warning Message
   z-index:5;
   }
   
   Save the changes.
   ```

1. Salve e feche o arquivo.
1. Navegue até a pasta CustomErrorManager-1.0-SNAPSHOT e crie um arquivo de pastas jcr_root e META-INF. Renomeie o arquivo como CustomErrorManager-1.0-SNAPSHOT.zip.
1. Use o gerenciador de pacote para fazer upload e instalar o pacote.

## Renderize o formulário com o novo perfil.  {#render-the-form-with-the-new-profile-nbsp}

Os formulários html5 usam um perfil padrão: https://&lt;servidor>/content/xfaforms/profiles/default.html?contentRoot=&lt;localização xdp>&amp;template=&lt;nome do xdp>

Para visualização um formulário às mensagens de erro personalizadas, renderize o formulário com o perfil de erro: https://&lt;servidor>/content/xfaforms/profiles/error.html?contentRoot=&lt;localização xdp>&amp;template=&lt;nome do xdp>

>[!NOTE]
>
>O pacote anexado instala o perfil de erro.

