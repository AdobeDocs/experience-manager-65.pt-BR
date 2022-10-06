---
title: Alteração do local da interface do usuário do AEM Forms workspace
seo-title: Changing the locale of AEM Forms workspace user interface
description: Como modificar o espaço de trabalho do AEM Forms para localizar texto, categorias recolhidas, filas e processos, e o seletor de datas na interface.
seo-description: How to modify the AEM Forms workspace to localize text, collapsed categories, queues, and processes, and the date picker on the interface.
uuid: c89ff150-a36e-45cc-99a6-8768dbe58eab
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 89f9d666-28e2-4201-8467-ae90693ca5d2
docset: aem65
exl-id: 9a069486-02a8-4058-adfb-4e0e49d8c0cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Alteração do local da interface do usuário do AEM Forms workspace{#changing-the-locale-of-aem-forms-workspace-user-interface}

A AEM Forms workspace oferece suporte pronto para uso para idiomas inglês, francês, alemão e japonês. Também fornece a capacidade de localizar a interface do usuário do AEM Forms workspace para qualquer outro idioma.

Para localizar a interface do usuário do AEM Forms workspace para o idioma de sua escolha:

* Localizar texto do espaço de trabalho do AEM Forms.
* Localize categorias, filas e processos recolhidos.
* Localizar Selecionador de Datas

Antes de executar as etapas acima, siga as etapas listadas em [Etapas genéricas para personalização do espaço de trabalho do AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md).

>[!NOTE]
>
>Para alterar o idioma da tela de logon do espaço de trabalho do AEM Forms, consulte [Criação de uma nova tela de logon](../../forms/using/creating-new-login-screen.md).

## Localização de texto {#localizing-text}

Execute as etapas a seguir para adicionar suporte a um idioma *Novo* e o código de local do navegador *nw*.

1. Faça logon no CRXDE Lite.
O URL padrão do CRXDE Lite é `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Navegar até o local `apps/ws/locales` e criar uma nova pasta `nw.`
1. Copiar o arquivo `translation.json`do local `/apps/ws/locales/en-US` para localização `/apps/ws/locales/nw` .
1. Navegar para `/apps/ws/locales/nw` e abrir `translation.json` para edição. Faça alterações específicas da localidade no arquivo translation.json.

   Os exemplos a seguir contêm o arquivo translation.json para as localidades em inglês e francês do espaço de trabalho do AEM Forms.

   ![translation_json_in_en](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## Localização de categorias, filas e processos recolhidos {#localizing-collapsed-categories-queues-and-processes}

O espaço de trabalho do AEM Forms usa imagens para exibir cabeçalhos de categorias, filas e processos. Você precisa de um pacote de desenvolvimento para localizar esses cabeçalhos. Para obter informações detalhadas sobre a criação de pacotes de desenvolvimento, consulte [Criação do código do espaço de trabalho do AEM Forms.](introduction-customizing-html-workspace.md#building-html-workspace-code)

Nas etapas a seguir, presume-se que os novos arquivos de imagem localizados sejam *Categories_nw.png*, *Queue_nw.png* e *Processes_nw.png*. A largura recomendada das imagens é de 19px.

>[!NOTE]
>
>Para localizar o código do idioma do navegador do código do idioma do navegador. Abrir `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![recolher_painéis_imagem](assets/collapsing_panels_image.png)

Execute as seguintes etapas para localizar as imagens:

1. Usando um cliente WebDAV, coloque os arquivos de imagem no */apps/ws/images* pasta.
1. Navegar para */apps/ws/css*. Abrir *newStyle.css* para editar e adicionar as seguintes entradas:

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

1. Execute todas as alterações semânticas listadas no [Personalização do Workspace](../../forms/using/introduction-customizing-html-workspace.md) artigo 10. o
1. Navegue até o *js/runtime/utility* e abra o *usersession.js* para edição.
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

## Localizando seletor de datas {#localizing-date-picker}

Você precisa que o pacote de desenvolvimento localize o *datepicker* API. Para obter informações detalhadas sobre a criação de pacotes de desenvolvimento, consulte [Criação do código do espaço de trabalho do AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

1. Baixe e extraia o [Pacote da interface do usuário do jQuery](https://jqueryui.com/download/all/), navegue até *&lt;extracted jquery=&quot;&quot; ui=&quot;&quot; package=&quot;&quot;>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n.
1. Copie o arquivo jquery.ui.datepicker-new.js para código de localidade agora em apps/ws/js/libs/jqueryui e faça alterações específicas de localidade no arquivo .
1. Navegar para `apps/ws/js` e abra o `jquery.ui.datepicker-nw.js` para edição.
1. No arquivo main.js, crie um alias para `jquery.ui.datepicker-nw.js.` O código para criar um alias para a variável `jquery.ui.datepicker-nw.js` O arquivo é:

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. Usar alias `jqueryuidatepickernw` para incluir a `jquery.ui.datepicker-nw.js` em todos os arquivos que usam datepicker. O datepicker é usado nos seguintes arquivos:

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   O código de amostra abaixo mostra como adicionar a entrada de jquery.ui.datepicker-new.js:

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

   Altere o seguinte código para adicionar a nova localidade:

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
