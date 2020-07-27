---
title: Personalização de ações de Tarefa
seo-title: Personalização de ações de Tarefa
description: Você pode personalizar a aparência das ações de tarefa, usar somente imagens para ações e personalizar as imagens usadas em ações de rota.
seo-description: Você pode personalizar a aparência das ações de tarefa, usar somente imagens para ações e personalizar as imagens usadas em ações de rota.
uuid: f6aebcd5-beac-41bf-95bf-2c07d36afa8b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ca3f6025-7e17-4173-8267-e24a338ea4a1
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Personalização de ações de Tarefa {#customizing-task-actions}

A área de trabalho do AEM Forms permite que os usuários personalizem as ações de tarefa. Antes de personalizar as ações de tarefa, siga as etapas listadas em Etapas [genéricas para personalização](/help/forms/using/generic-steps-html-workspace-customization.md)da área de trabalho do AEM Forms.

## Personalização do estilo de texto {#customizing-text-style}

Para personalizar o estilo de texto, adicione o seguinte trecho de código no `/apps/ws/css/newStyle.css` arquivo:

```css
/*-------- For Task Actions visible in task list task action popup ----------------------------------------------------*/
#taskarea .taskActionsPopUp{
    position:absolute;
    right: 78px;
    top: 16px;
    display: none;
}

#taskarea .taskActionsPopUp ul{
    list-style-type: none;
    padding: 0px;
    margin: 0px;
    border: 1px solid #B2B2B2;
    background: #1D1D1D;
    box-shadow: inset 0px 0px 11px 2px #1C1C1C;
    height:34px;
}

#taskarea .taskActionsPopUp li{
    width: auto;
    height: 34px;
    float: left;
    border-right: 1px solid #B2B2B2;
}

#taskarea .taskActionsPopUp li i{
    height: 34px;
    width: 20px;
    float: left;
    cursor: pointer;
}

#taskarea .taskActionsPopUp li a{
    color: white;
    text-decoration: none;
    display: inline-block;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    text-align: left;
    max-width: 150px;
    margin: 8px 10px 0px 4px;
}

/*-------- For Task Actions visible in task Details task action popup ----------------------------------------------------*/
.task .taskActionsPopUp {
    position: absolute;
    border: 1px solid #1D1D1D;
    z-index: 110;
    right: 5px;
    top : 35px;
    background: #2f2f2f;
    display:none;
}

.task .taskActionsPopUp ul{
    list-style: none outside none;
    font-size: 13px;
    width: 160px;
}

.task .taskActionsPopUp li{
    height: 33px;
    border-bottom: 1px solid #474747;
    width: 20px
}

.task .taskActionsPopUp ul a{
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    color: white;
    text-decoration: none;
    height: 26px;
    width: 133px;
    padding: 7px 0px 0px 27px;
    display: block;
    text-align: left;
    cursor: pointer;
    border-bottom: 1px solid #474747;
}
```

## Personalização de imagens {#customizing-images}

Para personalizar as imagens, adicione o seguinte trecho de código no `/apps/ws/css/newStyle.css` arquivo. O trecho de código a seguir personaliza a imagem para a ação de *bloqueio* :

```css
#taskarea .taskActionsPopUp .lock, .task .taskActionsPopUp .lock{
    background: url(../images/icons.png) no-repeat -265px -6px;
}
```

>[!NOTE]
>
>Adicione estilos separados para exibir imagens diferentes ou imagens de resolução diferente para as ações de detalhes de lista e Tarefa. Por exemplo, para alterar a ação &quot;bloquear&quot;:

```css
#taskarea .taskActionsPopUp .lock{
    background: url(../images/icons1.png) no-repeat -265px -6px;
}
.task .taskActionsPopUp .lock{
    background: url(../images/icons2.png) no-repeat -265px -6px;
}
```

## Mostrar somente imagens para ações {#showing-only-images-for-actions}

Para mostrar apenas imagens para ações, personalize as imagens usadas em ações de roteamento. Para obter informações detalhadas, consulte [Imagens para ações](/help/forms/using/images-route-actions.md)de rota.

### Menu pop-up Ação da tarefa da Lista da Tarefa {#task-list-task-action-nbsp-pop-up-menu}

1. Você precisa de um pacote de desenvolvimento para personalizar os itens do menu pop-up de ação tarefa de Tarefa da área de trabalho do AEM Forms. Para obter informações detalhadas sobre como criar o pacote de desenvolvimento, consulte [Criar código de espaço de trabalho de AEM Forms.](/help/forms/using/introduction-customizing-html-workspace.md#building-html-workspace-code)

1. Copie /libs/ws/js/runtime/templates/task.html para `/apps/ws/js/runtime/templates/task.html`substituir o seguinte trecho de código:

   ```html
   // Orignal code
   <div class="taskActionsPopUp">
           <!--START_TASKACTIONS-->
           <ul>
               <li class="arrow"></li>
               <%if(!isMustOpenToComplete && window.lcWorkspace != undefined && window.lcWorkspace.currentUser != undefined && window.lcWorkspace.currentUser.properties != undefined && window.lcWorkspace.currentUser.properties['/client/routes/formViewOnly'] == 'false'){%>
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
               <%}%>
               <%for(var i = 0; i<availableCommands.taskACLCommands.length; i++){%>
               <li class="<%= availableCommands.taskACLCommands[i]%>" alt="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.tooltip')%>" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"><%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.value')%></a>
               </li>
               <%}%>
               <%for(var i = 0; i<availableCommands.otherCommands.length; i++){%>
               <li class="<%= availableCommands.otherCommands[i]%>" alt="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.tooltip')%>" value="<%= availableCommands.otherCommands[i]%>" data-action="other"><%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.value')%></a>
               </li>
               <%}%>
           </ul>
           <!--END_TASKACTIONS-->
           <%}%>
       </div>
   ```

   ```html
   //New code
   
   <div class="taskActionsPopUp">
           <!--START_TASKACTIONS-->
           <ul>
               <li class="arrow"></li>
               <%if(!isMustOpenToComplete && window.lcWorkspace != undefined && window.lcWorkspace.currentUser != undefined && window.lcWorkspace.currentUser.properties != undefined && window.lcWorkspace.currentUser.properties['/client/routes/formViewOnly'] == 'false'){%>
               <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"></a>
               </li>
               <%}%>
               <%}%>
               <%}%>
               <%for(var i = 0; i<availableCommands.taskACLCommands.length; i++){%>
               <li class="<%= availableCommands.taskACLCommands[i]%>" alt="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.tooltip')%>" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"></a>
               </li>
               <%}%>
               <%for(var i = 0; i<availableCommands.otherCommands.length; i++){%>
               <li class="<%= availableCommands.otherCommands[i]%>" alt="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.tooltip')%>" value="<%= availableCommands.otherCommands[i]%>" data-action="other"></a>
               </li>
               <%}%>
           </ul>
           <!--END_TASKACTIONS-->
           <%}%>
       </div>
   ```

1. Remova a largura fixa atribuída a uma tag de âncora do `/apps/ws/css/newStyle.css` arquivo:

   ```css
   .task .taskActionsPopUp ul{
       list-style: none outside none;
       font-size: 13px;
       width: 160px;
   }
   
   To
   .task .taskActionsPopUp ul{
       list-style: none outside none;
       font-size: 13px;
   }
   
   AND
   
   .task .taskActionsPopUp ul a{
       white-space: nowrap;
       overflow: hidden;
       text-overflow: ellipsis;
       color: white;
       text-decoration: none;
       height: 26px;
       width: 133px;
       padding: 7px 0px 0px 27px;
       display: block;
       text-align: left;
       cursor: pointer;
       border-bottom: 1px solid #474747;
   }
   
   To
   
   .task .taskActionsPopUp ul a{
       white-space: nowrap;
       overflow: hidden;
       text-overflow: ellipsis;
       color: white;
       text-decoration: none;
       height: 26px;
       width: 0px;
       padding: 7px 0px 0px 27px;
       display: block;
       text-align: left;
       cursor: pointer;
       border-bottom: 1px solid #474747;
   }
   ```

### Menu pop-up Detalhes da Tarefa Ação da tarefa {#task-details-task-action-pop-up-menu}

Execute as seguintes etapas para personalizar o menu pop-up de ações de tarefa Detalhes:

* Copie o arquivo /libs/ws/js/runtime/templates/taskdetails.html para a `/apps/ws/js/runtime/templates/` pasta:
* Encapsule a tag do ícone dentro da tag de âncora em vez de texto. Por exemplo, o *novo código* listado abaixo encapsula a tag de ícone dentro da tag de âncora:

```html
// Original code
<div class="taskActionsPopUp">
        <!--START_ACTIONBUTTONGROUP-->
        <ul>
            <li class="leftArrow"><a href="javascript:void(0);"><</a></li>

            <% if (isOwner && showDirectActions) { %>
                <% if (routeList === null) {%>
                    <li class="routeAction">
                        <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
                    </li>
                <% } else { %>
                    <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                        <li class="routeAction">
                            <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                        </li>
                    <%}%>
                <%}%>
             <%}%>

            <% if (isOwner || (showACLActions && availableCommands.taskACLCommands !== null && availableCommands.taskACLCommands !== undefined && availableCommands.taskACLCommands.length > 0) ||  availableCommands.otherCommands.length > 2) { %>
                <%for (var i = 0; showACLActions && i < availableCommands.taskACLCommands.length; i++) {%>
                    <li title="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.tooltip')%>">
                        <i class="<%= availableCommands.taskACLCommands[i]%>" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"/>
                        <a href="javascript:void(0);" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"><%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.value')%></a>
                    </li>
                <%}%>

                <%for (var i = 0; i < availableCommands.otherCommands.length; i++) {%>
                    <li title="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.tooltip')%>">
                        <i class="<%= availableCommands.otherCommands[i]%>" value="<%= availableCommands.otherCommands[i]%>" data-action="other"/>
                        <a href="javascript:void(0);" value="<%= availableCommands.otherCommands[i]%>" data-action="other"><%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.value')%></a>
                    </li>
                <%}%>
            <%}%>

            <li class="rightArrow"><a href="javascript:void(0);">></a></li>
        </ul>
        <!--END_ACTIONBUTTONGROUP-->
    </div>
```

```html
//New code

<div class="taskActionsPopUp">
        <!--START_ACTIONBUTTONGROUP-->
        <ul>
            <li class="leftArrow"><a href="javascript:void(0);"><</a></li>

            <% if (isOwner && showDirectActions) { %>
                <% if (routeList === null) {%>
                    <li class="routeAction">
                        <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
                    </li>
                <% } else { %>
                    <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                        <li class="routeAction">
                            <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                        </li>
                    <%}%>
                <%}%>
             <%}%>

            <% if (isOwner || (showACLActions && availableCommands.taskACLCommands !== null && availableCommands.taskACLCommands !== undefined && availableCommands.taskACLCommands.length > 0) ||  availableCommands.otherCommands.length > 2) { %>
                <%for (var i = 0; showACLActions && i < availableCommands.taskACLCommands.length; i++) {%>
                    <li title="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.tooltip')%>">
                        <a href="javascript:void(0);" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL">
                            <i class="<%= availableCommands.taskACLCommands[i]%>" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"/>
                        </a>
                    </li>
                <%}%>

                <%for (var i = 0; i < availableCommands.otherCommands.length; i++) {%>
                    <li title="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.tooltip')%>">
                        <a href="javascript:void(0);" value="<%= availableCommands.otherCommands[i]%>" data-action="other">
                            <i class="<%= availableCommands.otherCommands[i]%>" value="<%= availableCommands.otherCommands[i]%>" data-action="other"/>
                        </a>
                    </li>
                <%}%>
            <%}%>

            <li class="rightArrow"><a href="javascript:void(0);">></a></li>
        </ul>
        <!--END_ACTIONBUTTONGROUP-->
    </div>
```

* Abra o arquivo /apps/ws/js/registry.js para edição.
* Localize o seguinte texto: `text!/lc/libs/ws/js/runtime/templates/taskdetails.html`
* Substitua o texto localizado pelo seguinte texto: `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`
