---
title: Alteração da fonte na interface
description: Como alterar as fontes na interface do usuário de forma seletiva.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 226f70f0-8eb4-4724-b496-5801dc6b436f
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# Alteração da fonte na interface{#changing-the-font-on-the-interface}

Você pode alterar a fonte exibida no espaço de trabalho do AEM Forms. As fontes usadas em uma seção específica da interface do usuário são definidas na seção correspondente da folha de estilos. É possível alterar as fontes na interface do usuário seletivamente.

Siga as [etapas genéricas para personalização do espaço de trabalho do AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md) e, dependendo de seus requisitos, siga as etapas para personalizar CSS, HTML ou ambos.

1. Alterar ou adicionar a família de fontes em um estilo existente.
1. Altere ou adicione a família de fontes integrada para o elemento HTML.
1. Adicione um estilo e use-o para o elemento HTML.

Por exemplo, para alterar a fonte do texto de âncora da barra de navegação superior para Courier New, siga estas etapas:

1. Faça logon no CRXDE Lite acessando `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Siga uma das seguintes opções:

   1. Para alterar a família de fontes em um estilo existente, adicione o seguinte no arquivo newStyle.css em /apps/ws/css.

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. Para adicionar a família de fontes em linha para o elemento HTML, copie o arquivo `/libs/ws/js/runtime/templates/appnavigation.html` para `/apps/ws/js/runtime/templates/appnavigation.html`.

      Atualize o arquivo /apps/ws/js/runtime/templates/appnavigation.html da seguinte maneira:

      ```jsp
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      Abra o arquivo /apps/ws/js/registry.js para edição e substitua `text!/lc/libs/ws/js/runtime/templates/appnavigation.html` por `text!/lc/apps/ws/js/runtime/templates/appnavigation.html`.

   1. Para adicionar um estilo que defina a família de fontes, adicione o seguinte no arquivo newStyle.css em /apps/ws/css.

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      Para adicionar a família de fontes em linha para o elemento HTML, adicione o seguinte no arquivo appnavigation.html em /apps/ws/js/runtime/templates.

      ```jsp
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. Reinicie o espaço de trabalho e limpe o cache do navegador para que as alterações fiquem visíveis.

![change_font_before](assets/change_font_before.png)

Barra de navegação superior antes da personalização da fonte

![alterar_fonte_após](assets/change_font_after.png)

Barra de navegação superior após a personalização da primeira guia
