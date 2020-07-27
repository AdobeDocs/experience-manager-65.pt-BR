---
title: Personalização do tema
seo-title: Personalização do tema
description: Como personalizar o tema do aplicativo AEM Forms.
seo-description: Como personalizar o tema do aplicativo AEM Forms.
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Personalização do tema {#theme-customization}

Você pode personalizar o código HTML e o arquivo CSS para fornecer uma aparência distinta e específica da organização ao aplicativo AEM Forms. Por exemplo, é possível alterar a cor e a altura do plano de fundo de tarefas ou Pontos de partida. O exemplo a seguir fornece instruções para alterar:

* instruções de exibição no lugar da descrição
* número de rotas de exibição
* cor do gradiente do plano de fundo

## Etapas {#steps}

1. Abra seu projeto.

   * Para iOS, abra `Capture.xcodeproj` no Xcode
   * Para Android, abra o projeto do Android no Eclipse.
   * Para Windows, abra `MWSWindows.sln` no Visual Studio.

1. Navegue até a pasta de modelos.

   * No Xcode, navegue até a pasta **Capture > www > wsmobile > js > tempo de execução > modelos** .
   * No Eclipse, navegue até a pasta **assets > www > wsmobile > js > tempo de execução > modelos** .
   * No Visual Studio, navegue até a pasta **MWSWwindows > www > wsmobile > js > tempo de execução > modelos** .

1. Open the `template.html` file for editing.
1. Localize a seguinte string:

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Substitua-o por `<%`.

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

   * No Xcode, navegue até **Capture > www > wsmobile > css**.
   * No Eclipse, navegue até **assets > www > wsmobile > css**.
   * No Visual Studio, navegue até **MWSWwindows > www > wsmobile > css**.

1. Open the `_style.css` file for editing.
1. Para imagem de plano de fundo, altere `#323232` para `#fff`.
1. Salve as alterações e feche o `_style.css` arquivo.
1. Abra o aplicativo AEM Forms.

   O aplicativo AEM Forms agora exibe instruções em vez de descrição.
