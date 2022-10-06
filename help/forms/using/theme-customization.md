---
title: Personalização de Tema
seo-title: Theme Customization
description: Como personalizar o tema do seu aplicativo AEM Forms.
seo-description: How to customize the theme of your AEM Forms app.
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
source-git-commit: 6bc228866aca785ec768daefb73970fc24568ef0
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Personalização de Tema {#theme-customization}

Você pode personalizar o código do HTML e o arquivo CSS para fornecer uma aparência distinta e específica da organização ao aplicativo AEM Forms. Por exemplo, você pode alterar a cor e a altura do plano de fundo de tarefas ou pontos de partida. O exemplo a seguir fornece instruções para a alteração:

* instruções de exibição no lugar da descrição
* número de rotas de exibição
* cor do gradiente de fundo

## Etapas {#steps}

1. Abra o projeto.

   * Para iOS, abra `Capture.xcodeproj` no Xcode
   * Para Android, abra o projeto Android no Eclipse.
   * Para Windows, abra `MWSWindows.sln` no Visual Studio.

1. Navegue até a pasta de modelos.

   * No XCode, navegue até o **Capturar > www > wsmobile > js > tempo de execução > modelos** pasta.
   * No Eclipse, navegue até o **ativos > www > wsmobile > js > tempo de execução > modelos** pasta.
   * No Visual Studio, navegue até o **Windows > www > wsmobile > js > tempo de execução > modelos** pasta.

1. Abra o `template.html` para edição.
1. Localize a seguinte string:

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Substitua por `<%`.

1. Localize o seguinte código no `template.html` arquivo:

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. Comente a linha a seguir e salve o arquivo.

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. Navegue até a pasta css.

   * No Xcode, navegue até **Capturar > www > wsmobile > css**.
   * No Eclipse, navegue até **ativos > www > wsmobile > css**.
   * No Visual Studio, navegue até **Windows MWSW > www > wsmobile > css**.

1. Abra o `_style.css` para edição.
1. Para imagem de plano de fundo, altere `#323232` para `#fff`.
1. Salve as alterações e feche `_style.css` arquivo.
1. Abra o aplicativo AEM Forms.

   O aplicativo AEM Forms agora exibe instruções em vez de descrição.
