---
title: Alteração da fonte na interface
seo-title: Alteração da fonte na interface
description: Como alterar as fontes na interface do usuário de forma seletiva.
seo-description: Como alterar as fontes na interface do usuário de forma seletiva.
uuid: 421fdd24-441a-4092-8c52-f3ed3d5d5671
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 9fcb80b4-cbc2-48a5-afd1-4f3bc50bc503
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Alteração da fonte na interface{#changing-the-font-on-the-interface}

Você pode alterar a fonte exibida na área de trabalho do AEM Forms. As fontes usadas em uma seção específica da interface do usuário são definidas na seção correspondente da folha de estilos. É possível alterar as fontes na interface do usuário de forma seletiva.

Siga as etapas [genéricas para personalização](../../forms/using/generic-steps-html-workspace-customization.md) do espaço de trabalho do AEM Forms e, dependendo de seus requisitos, siga as etapas para personalizar CSS, HTML ou ambos.

1. Altere ou adicione a família de fontes em um estilo existente.
1. Altere ou adicione a família de fontes em linha para o elemento HTML.
1. Adicione um estilo e use-o para o elemento HTML.

Por exemplo, para alterar a fonte do texto de ancoragem da barra de navegação superior para Courier New, siga estas etapas:

1. Faça logon no CRXDE Lite acessando `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Faça uma das seguintes opções:

   1. Para alterar a família de fontes em um estilo existente, adicione o seguinte no arquivo newStyle.css em /apps/ws/css.

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. Para adicionar a família de fontes em linha para o elemento HTML, copie o `/libs/ws/js/runtime/templates/appnavigation.html` arquivo para `/apps/ws/js/runtime/templates/appnavigation.html`.

      Atualize o arquivo /apps/ws/js/runtime/templates/appnavigation.html da seguinte maneira:

      ```
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

      Para adicionar a família de fontes em linha para o elemento HTML, adicione o seguinte no arquivo appnavigation.html em /apps/ws/js/runtime/models.

      ```css
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

Barra de navegação superior antes da personalização de fontes

![change_font_after](assets/change_font_after.png)

Barra de navegação superior após personalização da primeira guia
