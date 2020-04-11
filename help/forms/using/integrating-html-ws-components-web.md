---
title: Integração de componentes do espaço de trabalho do AEM Forms em aplicativos da Web
seo-title: Integração de componentes do espaço de trabalho do AEM Forms em aplicativos da Web
description: Como reutilizar os componentes do espaço de trabalho do AEM Forms em seus próprios aplicativos da Web para aproveitar a funcionalidade e fornecer integração total.
seo-description: Como reutilizar os componentes do espaço de trabalho do AEM Forms em seus próprios aplicativos da Web para aproveitar a funcionalidade e fornecer integração total.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Integração de componentes do espaço de trabalho do AEM Forms em aplicativos da Web {#integrating-aem-forms-workspace-components-in-web-applications}

Você pode usar [componentes](/help/forms/using/description-reusable-components.md) de espaço de trabalho do AEM Forms em seu próprio aplicativo da Web. A seguinte implementação de exemplo usa componentes de um pacote de desenvolvimento de espaço de trabalho do AEM Forms instalado em uma instância do CRX™ para criar um aplicativo da Web. Personalize a solução abaixo para atender às suas necessidades específicas. A implementação de amostra reutiliza `UserInfo`, `FilterList`e `TaskList`componentes dentro de um portal da Web.

1. Efetue login no ambiente CRXDE Lite em `https://'[server]:[port]'/lc/crx/de/`. Verifique se você tem um pacote de desenvolvimento de espaço de trabalho do AEM Forms instalado.
1. Crie um caminho `/apps/sampleApplication/wscomponents`.
1. Copie css, imagens, js/libs, js/runtime e js/registry.js

   * from `/libs/ws`
   * para `/apps/sampleApplication/wscomponents`.

1. Crie um arquivo demomain.js dentro da pasta /apps/sampleApplication/wscomponents/js. Copie o código de /libs/ws/js/main.js para demomain.js.
1. Em demomain.js, remova o código para inicializar o roteador e adicione o seguinte código:

   ```
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. Crie um nó em /content por nome `sampleApplication` e digite `nt:unstructured`. Nas propriedades desse nó, adicione `sling:resourceType` o tipo String e o valor `sampleApplication`. Na Lista de Controles de acesso desse nó, adicione uma entrada para `PERM_WORKSPACE_USER` permitir privilégios de jcr:read. Além disso, na Lista Controle de acesso de `/apps/sampleApplication` adicionar uma entrada para `PERM_WORKSPACE_USER` permitir privilégios de jcr:read.
1. Em caminhos de `/apps/sampleApplication/wscomponents/js/registry.js` atualização de `/lc/libs/ws/` para `/lc/apps/sampleApplication/wscomponents/` valores de modelo.
1. No arquivo JSP do home page do portal em `/apps/sampleApplication/GET.jsp`, adicione o seguinte código para incluir os componentes necessários dentro do portal.

   ```as3
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   Inclua também os arquivos CSS necessários para os componentes da área de trabalho do AEM Forms.

   >[!NOTE]
   >
   >Cada componente é adicionado à tag do componente (tendo um componente de classe) durante a renderização. Certifique-se de que seu home page contenha essas tags. Consulte o `html.jsp` arquivo da área de trabalho do AEM Forms para saber mais sobre essas tags de controle básicas.

1. Para personalizar os componentes, você pode estender as visualizações existentes para o componente necessário da seguinte forma:

   ```as3
   define([
       ‘jquery’,
       ‘underscore’,
       ‘backbone’,
       ‘runtime/views/userinfo'],
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

1. Modifique o CSS do portal para configurar o layout, o posicionamento e o estilo dos componentes necessários no portal. Por exemplo, você gostaria de manter a cor do plano de fundo como preta para este portal para visualização bem do componente userInfo. Você pode fazer isso alterando a cor do plano de fundo da `/apps/sampleApplication/wscomponents/css/style.css` seguinte maneira:

   ```as3
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
