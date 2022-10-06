---
title: Exibição de dados adicionais na lista de Tarefas
seo-title: Displaying additional data in ToDo list
description: Como personalizar a exibição da lista de Tarefas do espaço de trabalho do LiveCycle AEM Forms para mostrar mais informações além do padrão.
seo-description: How-to customize the display of the To-do list of LiveCycle AEM Forms workspace to show more information besides the default.
uuid: 9467c655-dce2-43ce-8e8f-54542fe81279
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fed3b562-bcc2-4fb7-8fd2-35b1ac621e16
docset: aem65
exl-id: f8b84f13-02d3-4787-95e1-25fd684e6d3b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Exibição de dados adicionais na lista de Tarefas{#displaying-additional-data-in-todo-list}

Por padrão, a lista de Tarefas a fazer do espaço de trabalho do AEM Forms exibe o nome de exibição e a descrição da tarefa. No entanto, é possível adicionar outras informações, como data de criação e data do prazo. Você também pode adicionar ícones e alterar o estilo da exibição.

![Uma análise da guia HTML Workspace To-do mostrando a configuração padrão](assets/html-todo-list.png)

Este artigo detalha as etapas para adicionar informações para cada tarefa na lista de Tarefas.

## O que pode ser adicionado {#what-can-be-added}

Você pode adicionar as informações disponíveis em `task.json` enviado pelo servidor. As informações podem ser adicionadas como texto sem formatação ou você pode usar estilos para formatar as informações.

Para obter mais informações sobre a descrição do objeto JSON, consulte [this](/help/forms/using/html-workspace-json-object-description.md) artigo 10. o

## Exibição de informações em uma tarefa {#displaying-information-on-a-task}

1. Siga as [Etapas genéricas para personalização do espaço de trabalho do AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md).
1. Para exibir informações adicionais para uma tarefa, os pares de valores chave correspondentes devem ser adicionados no bloco de tarefas de `translation.json`.

   Por exemplo, alterar `/apps/ws/locales/en-US/translation.json` Inglês:

   ```json
   "task" : {
           "reminder" : {
               "value" : "Reminder",
               "tooltip" : "This is reminder __reminderCount__, for this task."
           },
           "deadlined" : {
               "value" : "Deadlined",
               "tooltip" : "This task has deadlined"
           },
           "save" : {
               "message" : "Task has been saved successfully"
           },
           "status" : {
               "deadlined" : "Deadlined",
               "created" : "Created",
               "assignedsaved" : "Draft from assigned task",
               "terminated" : "Terminated",
               "assigned" : "Assigned",
               "unknown" : "Unknown",
               "createdsaved" : "Draft from created task",
               "completed" : "Completed"
           },
           "draft" : {
               "value" : "Saved",
               "tooltip" : "This task is marked as a draft"
           },
           "escalated" : {
               "value" : "Escalated",
               "tooltip" : "This task has been escalated"
           },
           "forward" : {
               "value" : "Forwarded",
               "tooltip" : "This task was forwarded"
           },
           "priority" : {
               "highest" : "Highest priority",
               "normal" : "Normal priority",
               "high" : "High priority",
               "low" : "Low priority",
               "lowest" : "Lowest priority"
           },
           "claimed" : {
               "value" : "Claimed",
               "tooltip" : "This task has been claimed"
           },
           "locked" : {
               "value" : "Locked",
               "tooltip" : "This task is locked"
           },
           "consulted" : {
               "value" : "Consulted",
               "tooltip" : "This task has been consulted"
           },
           "returned" : {
               "value" : "Returned",
               "tooltip" : "This task was returned back"
           },
           "multiplesubmitbuttons" : {
               "message" : "The form associated with this task has multiple submit buttons so the Workspace Complete button will be disabled. Click the appropriate button on the form to submit it."
           },
           "nosubmitbutton" : {
               "message" : "The form associated with this task does not appear to have submit buttons. You may need to upgrade your Adobe Reader version to 9.1 or greater and enable the Reader Submit option in your process."
           },
           "icon" : {
               "tooltip" : "open the task __taskName__"
           }
       }
   ```

   >[!NOTE]
   >
   >Adicione pares de valores chave correspondentes para todos os idiomas compatíveis.

1. Por exemplo, adicione informações dentro do bloco de tarefas:

   ```json
   "stepname" : {
               "value" : "Step Name",
               "tooltip" : "This task belongs to __stepName__ step"
   }
   ```

## Definição de CSS para a nova propriedade {#defining-css-for-the-new-property}

1. É possível aplicar estilo às informações (propriedade) adicionadas a uma tarefa. Para fazer isso, é necessário adicionar informações de estilo para a nova propriedade adicionada a `/apps/ws/css/newStyle.css`.

   Por exemplo, adicione:

   ```css
   .task .taskProperties .stepname{
       width: 25px;
       background: url(../images/stepname.png) no-repeat; /*-------- Or just reuse background image / image-sprite defined .task .taskProperties span of style.css---------------------*/
       background-position: 0px 0px; /*-------- Dummy values, need to be configured as per user background image / image-sprite ---------------------*/
   }
   ```

## Adicionando entrada no modelo HTML {#adding-entry-in-the-html-template}

Por fim, é necessário incluir uma entrada no pacote dev para cada propriedade que você deseja adicionar à tarefa. Para criar uma, consulte Criação do código do espaço de trabalho AEM Forms .

1. Copiar `task.html`:

   * de: `/libs/ws/js/runtime/templates/`
   * para: `/apps/ws/js/runtime/templates/`

1. Adicione as novas informações em `/apps/ws/js/runtime/templates/task.html`.

   Por exemplo, adicione em `div class="taskProperties"`:

   ```jsp
   <span class="stepname" alt="<%= $.t('task.stepname.value')%>" title = '<%= $.t("task.stepname.tooltip",{stepName:stepName})%>'/>
   ```
