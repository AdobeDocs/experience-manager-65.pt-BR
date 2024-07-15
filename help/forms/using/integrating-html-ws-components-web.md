---
title: Integração de componentes do espaço de trabalho do AEM Forms em aplicativos web
description: Como reutilizar componentes do espaço de trabalho do AEM Forms em seus próprios aplicativos da Web para usar a funcionalidade e fornecer uma integração estreita.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Integração de componentes do espaço de trabalho do AEM Forms em aplicativos web {#integrating-aem-forms-workspace-components-in-web-applications}

Você pode usar [componentes](/help/forms/using/description-reusable-components.md) do espaço de trabalho do AEM Forms em seu próprio aplicativo Web. O exemplo de implementação a seguir usa componentes de um pacote de desenvolvimento do espaço de trabalho do AEM Forms instalado em uma instância do CRX™ para criar um aplicativo web. Personalize a solução abaixo para atender às suas necessidades específicas. A implementação de exemplo reutiliza componentes `UserInfo`, `FilterList` e `TaskList` dentro de um portal da Web.

1. Faça logon no ambiente CRXDE Lite em `https://'[server]:[port]'/lc/crx/de/`. Verifique se você tem um pacote de desenvolvimento do AEM Forms Workspace instalado.
1. Criar um caminho `/apps/sampleApplication/wscomponents`.
1. Copie css, imagens, js/libs, js/runtime e js/registry.js

   * de `/libs/ws`
   * para `/apps/sampleApplication/wscomponents`.

1. Crie um arquivo demain.js dentro da pasta /apps/sampleApplication/wscomponents/js. Copie o código do /libs/ws/js/main.js para demomain.js.
1. Em demomain.js, remova o código para inicializar o roteador e adicione o seguinte código:

   ```javascript
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. Crie um nó em /content pelo nome `sampleApplication` e tipo `nt:unstructured`. Nas propriedades deste nó, adicione `sling:resourceType` do tipo Cadeia de Caracteres e valor `sampleApplication`. Na Lista de Controle de Acesso deste nó, adicione uma entrada para `PERM_WORKSPACE_USER` permitindo privilégios jcr:read. Além disso, na Lista de Controle de Acesso de `/apps/sampleApplication`, adicione uma entrada para `PERM_WORKSPACE_USER` permitindo privilégios jcr:read.
1. Em `/apps/sampleApplication/wscomponents/js/registry.js`, atualize os caminhos de `/lc/libs/ws/` a `/lc/apps/sampleApplication/wscomponents/` para valores de modelo.
1. No arquivo JSP da home page do portal em `/apps/sampleApplication/GET.jsp`, adicione o seguinte código para incluir os componentes necessários dentro do portal.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   Inclua também os arquivos CSS necessários para os componentes do espaço de trabalho do AEM Forms.

   >[!NOTE]
   >
   >Cada componente é adicionado à tag do componente (com class gcomponent) durante a renderização. Certifique-se de que a home page contenha essas tags. Consulte o arquivo `html.jsp` do espaço de trabalho do AEM Forms para saber mais sobre essas marcas de controle base.

1. Para personalizar os componentes, é possível estender as exibições existentes para o componente desejado da seguinte maneira:

   ```javascript
   define([
       'jquery',
       'underscore',
       'backbone',
       'runtime/views/userinfo'],
       function($, _, Backbone, UserInfo){
           var demoUserInfo = UserInfo.extend({
               //override the functions to customize the functionality
               render: function() {
                   UserInfo.prototype.render.call(this); // call the render function of the super class
                   …
                   //other tasks
                   …
               }
           });
           return demoUserInfo;
   });
   ```

1. Modifique o CSS do portal para configurar o layout, o posicionamento e o estilo dos componentes necessários no portal. Por exemplo, você gostaria de manter a cor do plano de fundo preta para que este portal exiba bem o componente userInfo. Você pode fazer isso alterando a cor do plano de fundo em `/apps/sampleApplication/wscomponents/css/style.css` da seguinte maneira:

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
