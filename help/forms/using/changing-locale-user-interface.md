---
title: Alteração da localidade da interface do usuário da área de trabalho do AEM Forms
seo-title: Alteração da localidade da interface do usuário da área de trabalho do AEM Forms
description: Como modificar a área de trabalho do AEM Forms para localizar texto, categorias recolhidas, filas e processos, e o seletor de datas na interface.
seo-description: Como modificar a área de trabalho do AEM Forms para localizar texto, categorias recolhidas, filas e processos, e o seletor de datas na interface.
uuid: c89ff150-a36e-45cc-99a6-8768dbe58eab
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 89f9d666-28e2-4201-8467-ae90693ca5d2
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Alteração da localidade da interface do usuário da área de trabalho do AEM Forms{#changing-the-locale-of-aem-forms-workspace-user-interface}

A área de trabalho do AEM Forms fornece suporte imediato para idiomas inglês, francês, alemão e japonês. Ele também oferece a capacidade de localizar a interface de usuário do espaço de trabalho do AEM Forms para qualquer outro idioma.

Para localizar a interface de usuário do espaço de trabalho do AEM Forms para o idioma de sua escolha:

* Localize o texto da área de trabalho do AEM Forms.
* Localize categorias recolhidas, filas e processos.
* Localizar o seletor de datas

Antes de executar as etapas acima, siga as etapas listadas em Etapas [genéricas para personalização](../../forms/using/generic-steps-html-workspace-customization.md)da área de trabalho do AEM Forms.

>[!NOTE]
>
>Para alterar o idioma da tela de logon da área de trabalho do AEM Forms, consulte [Criar uma nova tela](../../forms/using/creating-new-login-screen.md)de logon.

## Localização de texto {#localizing-text}

Execute as seguintes etapas para adicionar suporte para um idioma *Novo* e o código de idioma do navegador *agora*.

1. Faça logon no CRXDE Lite.
O URL padrão do CRXDE Lite é `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Navegue até o local `apps/ws/locales` e crie uma nova pasta `nw.`
1. Copie o arquivo `translation.json`do local `/apps/ws/locales/en-US` para o local `/apps/ws/locales/nw` .
1. Navegue até `/apps/ws/locales/nw` e abra `translation.json` para edição. Faça alterações específicas à localidade no arquivo Translation.json.

   Os exemplos a seguir contêm o arquivo Translation.json para localidades inglesas e francesas da área de trabalho do AEM Forms.

   ![Translation_json_in_en](assets/translation_json_in_en.png) ![Translation_json_in_fr](assets/translation_json_in_fr.png)

## Localização de categorias, filas e processos recolhidos {#localizing-collapsed-categories-queues-and-processes}

A área de trabalho do AEM Forms usa imagens para exibir cabeçalhos de categorias, filas e processos. Você precisa de um pacote de desenvolvimento para localizar esses cabeçalhos. Para obter informações detalhadas sobre como criar um pacote de desenvolvimento, consulte [Criar código de espaço de trabalho do AEM Forms.](../../forms/using/introduction-customizing-html-workspace.md#main-pars-heading-3)

Nas etapas a seguir, presume-se que os novos arquivos de imagem localizados sejam *Categoria_nw.png*, *Queue_nw.png* e *Processes_nw.png*. A largura recomendada das imagens é de 19x.

>[!NOTE]
>
>Para localizar o código de idioma do navegador do seu navegador. Abrir `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![collapsing_panel_image](assets/collapsing_panels_image.png)

Execute as seguintes etapas para localizar as imagens:

1. Usando um cliente WebDAV, coloque os arquivos de imagem na pasta */apps/ws/images* .
1. Navegue até */apps/ws/css*. Abra *newStyle.css* para editar e adicione as seguintes entradas:

   ```
   #categoryListBar .content.nw {
        background: #3e3e3e url(../images/Categories_nw.png) no-repeat 10px 10px;
    }
   
   #filterListBar .content.nw {
       background: #3e3e3e url(../images/Queues_nw.png) no-repeat 10px 10px;
   }
   
   #processNameListBar .content.nw {
       background: #3e3e3e url(../images/Processes_nw.png) no-repeat 10px 10px;
   }
   ```

1. Execute todas as alterações semânticas listadas no artigo Personalização [da](../../forms/using/introduction-customizing-html-workspace.md) Workspace.
1. Navegue até a pasta *js/runtime/utility* e abra o arquivo *usersession.js* para edição.
1. Localize o código listado no bloco de código original e adicione a condição *lang !== &#39;new&#39;* para a declaração if:

   ```
   // Orignal code
   setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

   ```
   //new code
    setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP' && lang !== 'nw')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

## Localizando o seletor de datas {#localizing-date-picker}

Você precisa de um pacote de desenvolvimento para localizar a API *datepicker* . Para obter informações detalhadas sobre como criar um pacote de desenvolvimento, consulte [Criar código](../../forms/using/introduction-customizing-html-workspace.md#main-pars-heading-3)de área de trabalho do AEM Forms.

1. Baixe e extraia o Pacote [da interface do usuário do](https://jqueryui.com/download/all/)jQuery, navegue até *&lt;pacote da interface do usuário jquery extraída>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n.
1. Copie o arquivo jquery.ui.datepicker-nw.js para código de localidade agora em apps/ws/js/libs/jqueryui e faça alterações específicas de localidade no arquivo.
1. Navegue até `apps/ws/js` `jquery.ui.datepicker-nw.js` o arquivo e abra-o para edição.
1. No arquivo main.js, crie um alias para `jquery.ui.datepicker-nw.js.` O código para criar um alias para o `jquery.ui.datepicker-nw.js` arquivo é:

   ```
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. Use o alias `jqueryuidatepickernw` para incluir o `jquery.ui.datepicker-nw.js` arquivo em todos os arquivos que usam o datepicker. O datepicker é usado nos seguintes arquivos:

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`
   O código de amostra abaixo mostra como adicionar a entrada de jquery.ui.datepicker-nw.js:

   ```
   //Original Code
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, slimScroll, UserSearch, LogManager, Logger) {
   ```

   ```
   // Code with Date Picker alias for new language
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'jqueryuidatepickernw', // Date Picker alias
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, jQueryUIDatePickerNW, slimScroll, UserSearch, LogManager, Logger) {
   ```

1. Em todos os arquivos que usam a API datepicker, altere as configurações padrão da API datepicker. A API datepicker é usada nos seguintes arquivos:

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js
   Altere o seguinte código para adicionar a nova localidade:

   ```
   if (locale === 'ja-JP') {
      $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
      $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
      $.datepicker.setDefaults($.datepicker.regional.fr);
   } else {
      $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```

   ```
   if (locale === 'ja-JP') {
       $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
       $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
       $.datepicker.setDefaults($.datepicker.regional.fr);
   } else if (locale === 'nw') {
       $.datepicker.setDefaults($.datepicker.regional.nw);
   } else {
       $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```

[Entre em contato com o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
