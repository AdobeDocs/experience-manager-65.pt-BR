---
title: Personalizar imagens usadas nas ações de roteiro
description: Como personalizar as imagens usadas nas ações de rota no espaço de trabalho do LiveCycle AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 687c6569-7189-4039-9c7a-bc29658a7756
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Personalizar imagens usadas nas ações de roteiro {#customize-images-used-in-route-actions}

Para personalizar as imagens usadas nas ações de rota, execute as etapas descritas em [Etapas genéricas de personalização](/help/forms/using/generic-steps-html-workspace-customization.md) seguidas pelas etapas descritas neste artigo.

## Imagens para ações de rota {#images-for-route-actions}

1. Adicione os estilos que definem imagens no CSS no seguinte local para as novas ações de rota:

   `/apps/ws/css/newStyle.css`

   Por exemplo: adicione um novo estilo chamado `myStyle1`, como mostrado abaixo, e carregue o arquivo de imagem `myStyleIcon1.png` para a pasta `/apps/ws/image`s usando um cliente WebDAV.

   >[!NOTE]
   >
   >Para obter mais informações, consulte [Acesso ao WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=pt-BR).

   >[!NOTE]
   >
   >Prefira usar o nome do estilo como igual ao nome da ação da rota.

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## Pop-up de ação de tarefa da Lista de Tarefas {#task-list-task-action-popup}

1. Crie um pop-up de ação de lista de tarefas, consulte [Criação do código do espaço de trabalho do AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code). É necessário usar o pacote dev.

1. Copiar `/libs/ws/js/runtime/templates/task.html` para `/apps/ws/js/runtime/templates/task.html`.

1. Se o nome do estilo CSS for igual ao nome da ação de rota proveniente do servidor, modifique o seguinte código em `/apps/ws/js/runtime/templates/task.html`:

   ```jsp
   <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   
   To
   
   <%if(routeList == null){%>
               <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li class="<%= availableCommands.directCommands[i]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   ```

1. Se o nome do estilo CSS for diferente do nome da ação de rota proveniente do servidor, modifique o seguinte código em `/apps/ws/js/runtime/templates/task.html`. Ele adiciona uma pilha das condições do servlet `if-else` para mapear o estilo com o nome da ação de rota.

```jsp
<%if(routeList == null){%>
            <li>
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
            <li>
                <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
            </li>
            <%}%>
            <%}%>

To

<%if(routeList == null){%>
            <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
                <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                     <li class="myStyle1" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                     <li class="myStyle2" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}%>
            <%}%>
            <%}%>
```

## Pop-up de ação de tarefa de Detalhes da Tarefa {#task-details-task-action-popup}

1. Copiar `/libs/ws/js/runtime/templates/taskdetails.html` para `/apps/ws/js/runtime/templates/taskdetails.html`.

1. Se o nome do estilo CSS for igual ao nome da ação de rota proveniente do servidor, modifique o seguinte código em `/apps/ws/js/runtime/templates/taskdetails.html`:

   ```jsp
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                       <%}%>
   ```

1. Se o nome do estilo CSS for diferente do nome da ação de rota proveniente do servidor, modifique o seguinte código em `/apps/ws/js/runtime/templates/taskdetails.html`. Ele adiciona uma pilha de condições de servlet `if-else` para mapear o estilo com o nome da ação de rota.

   ```jsp
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                   <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle1" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle2" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}%>
               <%}%>
   ```

1. Abra `/apps/ws/js/registry.js` para edição e procure o seguinte texto:
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. Substituir o texto pelo seguinte:
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`
