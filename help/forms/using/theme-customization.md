---
title: Personalização de tema
description: Saiba como personalizar o tema do aplicativo do AEM Forms. Você pode personalizar o código HTML e o arquivo CSS para fornecer aparência e comportamento específicos da organização.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Personalização de tema {#theme-customization}

Você pode personalizar o código HTML e o arquivo CSS para fornecer uma aparência distinta específica da organização para o aplicativo AEM Forms. Por exemplo, é possível alterar a cor do plano de fundo e a altura das tarefas ou dos pontos iniciais. O exemplo a seguir fornece instruções para alteração:

* exibir instruções no lugar da descrição
* número de roteiros de exibição
* cor do gradiente do plano de fundo

## Etapas {#steps}

1. Abra o projeto.

   * Para o iOS, abra `Capture.xcodeproj` no Xcode
   * Para Android, abra o projeto Android no Eclipse.
   * Para Windows, abra `MWSWindows.sln` no Visual Studio.

1. Navegue até a pasta de modelos.

   * No XCode, navegue até a guia **Capture > www > wsmobile > js > tempo de execução > templates** pasta.
   * No Eclipse, navegue até o **ativos > www > wsmobile > js > tempo de execução > modelos** pasta.
   * No Visual Studio, navegue até o **MWSWindows > www > wsmobile > js > tempo de execução > modelos** pasta.

1. Abra o `template.html` arquivo para edição.
1. Localize a seguinte string:

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Substituir por `<%`.

1. Localize o seguinte código na `template.html` arquivo:

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
   * No Eclipse, acesse **assets > www > wsmobile > css**.
   * No Visual Studio, navegue até **MWSWindows > www > wsmobile > css**.

1. Abra o `_style.css` arquivo para edição.
1. Para Imagem de fundo, altere `#323232` para `#fff`.
1. Salvar as alterações e fechar `_style.css` arquivo.
1. Abra o aplicativo AEM Forms.

   O aplicativo AEM Forms agora exibe instruções em vez de descrição.
