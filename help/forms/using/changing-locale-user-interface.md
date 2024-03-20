---
title: Alterando o local da interface do usuário do espaço de trabalho do AEM Forms
description: Como modificar o espaço de trabalho do AEM Forms para localizar texto, categorias recolhidas, filas e processos e o seletor de datas na interface.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 9a069486-02a8-4058-adfb-4e0e49d8c0cf
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Alterando o local da interface do usuário do espaço de trabalho do AEM Forms{#changing-the-locale-of-aem-forms-workspace-user-interface}

O espaço de trabalho do AEM Forms oferece suporte imediato para os idiomas inglês, francês, alemão e japonês. Ela também permite localizar a interface do usuário do AEM Forms Workspace em qualquer outro idioma.

Para localizar a interface do usuário do espaço de trabalho do AEM Forms no idioma de sua escolha:

* Localize o texto do espaço de trabalho do AEM Forms.
* Localizar categorias, filas e processos recolhidos.
* Localizar Seletor de Data

Antes de executar as etapas acima, siga as etapas listadas em [Etapas genéricas para personalização do espaço de trabalho do AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md).

>[!NOTE]
>
>Para alterar o idioma da tela de logon do espaço de trabalho do AEM Forms, consulte [Criar uma tela de logon](../../forms/using/creating-new-login-screen.md).

## Localização de texto {#localizing-text}

Execute as seguintes etapas para adicionar suporte a um idioma *Novo* e o código de localidade do navegador *novo*.

1. Efetue logon no CRXDE Lite.
O URL padrão do CRXDE Lite é `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Navegue até o local `apps/ws/locales` e criar uma pasta `nw.`
1. Copie o arquivo `translation.json`do local `/apps/ws/locales/en-US` para o local `/apps/ws/locales/nw` .
1. Navegue até `/apps/ws/locales/nw` e aberto `translation.json` para edição. Faça alterações específicas da localidade no arquivo translation.json.

   Os exemplos a seguir contêm o arquivo translation.json para os códigos de idioma inglês e francês do espaço de trabalho do AEM Forms.

   ![translation_json_in_br](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## Localização de categorias, filas e processos recolhidos {#localizing-collapsed-categories-queues-and-processes}

O AEM Forms workspace usa imagens para exibir cabeçalhos de categorias, filas e processos. Você precisa de um pacote de desenvolvimento para localizar esses cabeçalhos. Para obter informações detalhadas sobre como criar um pacote de desenvolvimento, consulte [Criação do código do espaço de trabalho do AEM Forms.](introduction-customizing-html-workspace.md#building-html-workspace-code)

Nas etapas a seguir, presume-se que os novos arquivos de imagem localizados sejam *Categories_nw.png*, *Fila_nw.png*, e *Processes_nw.png*. A largura recomendada das imagens deve ser definida como 19 pixels.

>[!NOTE]
>
>Para encontrar o código de localidade do idioma do navegador do seu navegador. Abertura `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![recolhimento_panels_image](assets/collapsing_panels_image.png)

Para localizar as imagens, execute as seguintes etapas:

1. Usando um cliente WebDAV, coloque os arquivos de imagem na */apps/ws/images* pasta.
1. Navegue até */apps/ws/css*. Abertura *newStyle.css* para editar e adicionar as seguintes entradas:

   ```css
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

1. Execute todas as alterações semânticas listadas no [Personalização do Workspace](../../forms/using/introduction-customizing-html-workspace.md) artigo.
1. Navegue até a *js/runtime/utility* e abra a *usersession.js* arquivo para edição.
1. Localize o código listado no bloco de código original e adicione a condição *lang!== &#39;nw&#39;* para a instrução if:

   ```javascript
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

   ```javascript
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

## Seletor de Data de Localização {#localizing-date-picker}

Você precisa de um pacote de desenvolvimento para localizar o *datepicker* API. Para obter informações detalhadas sobre como criar um pacote de desenvolvimento, consulte [Criação do código do espaço de trabalho do AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

1. Baixe e extraia o [Pacote de interface do usuário jQuery](https://jqueryui.com/download/all/), navegue até *&lt;extracted jquery=&quot;&quot; ui=&quot;&quot; package=&quot;&quot;>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n.
1. Copie o arquivo jquery.ui.datepicker-nw.js do código de localidade nw para apps/ws/js/libs/jqueryui e faça alterações específicas de localidade no arquivo.
1. Navegue até `apps/ws/js` e abra o `jquery.ui.datepicker-nw.js` arquivo para edição.
1. No arquivo main.js, crie um alias para `jquery.ui.datepicker-nw.js.` O código para criar um alias para o `jquery.ui.datepicker-nw.js` o arquivo é:

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. Usar alias `jqueryuidatepickernw` para incluir o `jquery.ui.datepicker-nw.js` em todos os arquivos que usam o datepicker. O seletor de datas é usado nos seguintes arquivos:

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   O código de amostra abaixo mostra como adicionar a entrada de jquery.ui.datepicker-nw.js:

   ```json
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

   ```json
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

1. Em todos os arquivos que usam a API do datepicker, altere as configurações padrão da API do datepicker. A API do datepicker é usada nos seguintes arquivos:

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   Altere o código a seguir para adicionar o novo local:

   ```javascript
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

   ```javascript
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
