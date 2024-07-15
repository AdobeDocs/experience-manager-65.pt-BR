---
title: Personalização de mensagens de erro para formulários HTML5
description: Saiba como personalizar a exibição de mensagens de erro para formulários HTML5, incluindo como alterar sua posição e aparência.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
feature: HTML5 Forms,Mobile Forms
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# Personalização de mensagens de erro para formulários HTML5 {#customizing-error-messages-for-html-forms}

Nos formulários HTML5, fora da caixa, as mensagens de erro e os avisos têm uma posição e aparência fixas (fonte e cor), o erro é exibido somente para um campo selecionado e apenas um erro é exibido.

O artigo fornece as etapas para personalizar mensagens de erro de formulários HTML5 para que você possa fazer o seguinte:

* alterar a aparência e a posição das mensagens de erro. Você pode cometer um erro ao aparecer na parte superior, inferior e direita de qualquer campo.
* exibir mensagens de erro para vários campos em um determinado momento.
* exibir o erro independentemente de um campo estar selecionado ou não.

## Personalização de mensagens de erro  {#customizing-error-messages-nbsp}

Antes de personalizar as mensagens de erro, baixe e extraia o pacote anexado (CustomErrorManager-1.0-SNAPSHOT.zip).

Após extrair o pacote, abra a pasta CustomErrorManager-1.0-SNAPSHOT. Ele contém as pastas jcr_root e META-INF. Essas pastas contêm os arquivos CSS e .JS necessários para personalizar a mensagem de erro.

[Obter arquivo](assets/customerrormanager-1.0-snapshot.zip)

### Personalização da posição das mensagens de erro  {#customizing-the-position-of-error-messages-nbsp}

Para personalizar a posição da mensagem de erro, adicione uma tag &lt;div> para cada campo de erro e aviso, posicione a tag &lt;div> à esquerda ou à direita e aplique estilos de css à tag &lt;div>. Para obter etapas detalhadas, consulte o procedimento listado abaixo:

1. Navegue até a pasta `CustomErrorManager-1.0-SNAPSHOT` e abra a pasta `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript`.
1. Abra o arquivo `customErrorManager.js` para edição. A função `markError` no arquivo aceita os seguintes parâmetros:

   |   |  |
   |---|---|
   | jqWidget | O jqWidget é o identificador de um widget. |
   | msg | contém a mensagem de erro |
   | tipo | indica se é um erro ou aviso |

1. Na implementação pronta para uso, as mensagens de erro são exibidas à direita do campo. Para fazer com que as mensagens de erro apareçam na parte superior, use o código a seguir.

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

1. Salvar e fechar o arquivo.
1. Navegue até a pasta `CustomErrorManager-1.0-SNAPSHOT` e crie um arquivo das pastas jcr_root e META-INF. Renomeie o arquivo para CustomErrorManager-1.0-SNAPSHOT.zip.
1. Use o Gerenciador de pacotes para fazer upload e instalar o pacote.

## Exibir mensagens de erro para vários campos  {#display-error-messages-for-multiple-fields-nbsp}

Use o pacote anexado para exibir simultaneamente mensagens de erro para todos os campos. Para exibir uma única mensagem de erro, use o perfil padrão.

### Personalizar a aparência de mensagens de erro.  {#customizing-the-appearance-of-error-messages-nbsp}

1. Navegue até a pasta etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css.

1. Abra o arquivo sample.css para edição. O arquivo css contém 2 ids - #customError, #customWarning. Você pode usar essas IDs para alterar várias propriedades, como cor e tamanho da fonte.

   Use o código a seguir para alterar o tamanho da fonte e a cor das mensagens de erro/aviso.

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

1. Salvar e fechar o arquivo.
1. Navegue até a pasta CustomErrorManager-1.0-SNAPSHOT e crie um arquivo das pastas jcr_root e META-INF. Renomeie o arquivo para CustomErrorManager-1.0-SNAPSHOT.zip.
1. Use o Gerenciador de pacotes para fazer upload e instalar o pacote.

## Renderize o formulário com o novo perfil.  {#render-the-form-with-the-new-profile-nbsp}

Os formulários html5 prontos para uso usam um perfil padrão: `https://&lt;server&gt;/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

Para exibir um formulário com as mensagens de erro personalizadas, renderize o formulário com o perfil de erro: `https://&lt;server&gt;/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

>[!NOTE]
>
>O pacote anexado instala o perfil de erro.
