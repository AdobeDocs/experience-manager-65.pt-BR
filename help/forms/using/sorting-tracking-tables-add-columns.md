---
title: Personalizar tabelas de rastreamento
description: Como personalizar a exibição dos detalhes dos processos do usuário na tabela de tarefas exibida na guia de rastreamento do espaço de trabalho do AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 9ab657cc-fa8e-4168-8a68-e38ac5c51b29
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---

# Personalizar tabelas de rastreamento{#customize-tracking-tables}

A guia de rastreamento no espaço de trabalho do AEM Forms é usada para exibir os detalhes de instâncias de processo nas quais o usuário conectado está envolvido. Para exibir as tabelas de rastreamento, primeiro selecione um nome de processo no painel esquerdo para ver sua lista de instâncias no painel do meio. Selecione uma instância de processo para ver uma tabela de tarefas geradas por essa instância no painel direito. Por padrão, as colunas da tabela exibem os seguintes atributos de tarefa (o atributo correspondente no modelo de tarefa é fornecido entre parênteses):

* ID ( `taskId`)
* Nome ( `stepName`)
* Instruções ( `instructions`)
* Ação selecionada ( `selectedRoute`)
* Hora de Criação ( `createTime`)
* Hora de conclusão ( `completeTime`)
* Proprietário ( `currentAssignment.queueOwner`)

Os atributos restantes no modelo de tarefa disponível para exibição na tabela de tarefas são:

<table>
 <tbody>
  <tr>
   <td><p>actionInstanceId</p> </td>
   <td><p>isOpenFullScreen</p> </td>
   <td><p>reminderCount</p> </td>
  </tr>
  <tr>
   <td><p>classOfTask</p> </td>
   <td><p>isOwner</p> </td>
   <td><p>routeList</p> </td>
  </tr>
  <tr>
   <td><p>consultGroupId</p> </td>
   <td><p>isRouteSelectionRequired</p> </td>
   <td><p>savedFormCount</p> </td>
  </tr>
  <tr>
   <td><p>contentType</p> </td>
   <td><p>isShowAttachments</p> </td>
   <td><p>serializedImageTicket</p> </td>
  </tr>
  <tr>
   <td><p>createTime</p> </td>
   <td><p>isStartTask</p> </td>
   <td><p>serviceName</p> </td>
  </tr>
  <tr>
   <td><p>creationId</p> </td>
   <td><p>isVisible</p> </td>
   <td><p>serviceTitle</p> </td>
  </tr>
  <tr>
   <td><p>currentAssignment</p> </td>
   <td><p>nextReminder</p> </td>
   <td><p>showACLActions</p> </td>
  </tr>
  <tr>
   <td><p>prazo</p> </td>
   <td><p>numForms</p> </td>
   <td><p>showDirectActions</p> </td>
  </tr>
  <tr>
   <td><p>descrição</p> </td>
   <td><p>numFormsToBeSaved</p> </td>
   <td><p>status</p> </td>
  </tr>
  <tr>
   <td><p>displayName</p> </td>
   <td><p>outOfOfficeUserId</p> </td>
   <td><p>summaryUrl</p> </td>
  </tr>
  <tr>
   <td><p>forwardGroupId</p> </td>
   <td><p>outOfOfficeUserName</p> </td>
   <td><p>supportedSave</p> </td>
  </tr>
  <tr>
   <td><p>isApprovalUI</p> </td>
   <td><p>prioridade</p> </td>
   <td><p>taskACL</p> </td>
  </tr>
  <tr>
   <td><p>isCustomUI</p> </td>
   <td><p>processInstanceId</p> </td>
   <td><p>taskFormType</p> </td>
  </tr>
  <tr>
   <td><p>isDefaultImage</p> </td>
   <td><p>processInstanceStatus</p> </td>
   <td><p>taskUserInfo</p> </td>
  </tr>
  <tr>
   <td><p>isLocked</p> </td>
   <td><p>processVariables</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p>isMustOpenToComplete</p> </td>
   <td><p>readerSubmitOptions</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Para as seguintes personalizações na tabela de tarefas, você precisa fazer alterações semânticas no código-fonte. Consulte [Introdução à personalização do espaço de trabalho do AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md) para saber como fazer alterações semânticas usando o SDK do espaço de trabalho e criar um pacote minificado a partir da origem alterada.

## Alteração de colunas da tabela e sua ordem {#changing-table-columns-and-their-order}

1. Para modificar os atributos de tarefa exibidos na tabela e sua ordem, configure o arquivo /ws/js/runtime/templates/processinstancehistory.html :

   ```html
   <table>
       <thead>
           <tr>
               <!-- put the column headings in order here, for example-->
               <th><%= $.t('history.fixedTaskTableHeader.taskName')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskInstructions')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskRoute')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCreateTime')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCompleteTime')%></th>
           </tr>
       </thead>
   </table>
   ```

   ```html
   <table>
       <tbody>
           <%_.each(obj, function(task){%>
           <tr>
               <!-- Put the task attributes in the order of headings, for example, -->
               <td><%= task.stepName %></td>
               <td><%= task.instructions %></td>
               <td><%= !task.selectedRoute?'':(task.selectedRoute=='null'?'Default':task.selectedRoute) %></td>
               <td><%= task.createTime?task.formattedCreateTime:'' %></td>
               <td><%= task.completeTime? task.formattedCompleteTime:'' %></td>
           </tr>
           <%});%>
       </tbody>
   </table>
   ```

## Classificação de uma tabela de rastreamento {#sorting-a-tracking-table}

Para classificar a tabela da lista de tarefas ao clicar no cabeçalho da coluna:

1. Registre um manipulador de cliques para `.fixedTaskTableHeader th` no arquivo `js/runtime/views/processinstancehistory.js`.

   ```javascript
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   No manipulador, chame a função `onTaskTableHeaderClick` de `js/runtime/util/history.js`.

   ```javascript
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. Exponha o método `TaskTableHeaderClick` em `js/runtime/util/history.js`.

   O método localiza o atributo de tarefa do evento click, classifica a lista de tarefas nesse atributo e renderiza a tabela de tarefa com a lista de tarefas classificada.

   A classificação é feita usando a função de classificação Backbone na coleção de listas de tarefas, fornecendo uma função de comparação.

   ```javascript
       return {
           //other methods
           onTaskTableHeaderClick  : onTaskTableHeaderClick,
           //other methods
       };
   ```

   ```javascript
   onTaskTableHeaderClick = function (event) {
           var target = $(event.target),
            comparator,
               attribute;
           if(target.hasClass('taskName')){
            attribute = 'stepName';
           } else if(target.hasClass('taskInstructions')){
               attribute = 'instructions';
           } else if(target.hasClass('taskRoute')){
               attribute = 'selectedRoute';
           } else if(target.hasClass('taskCreateTime')){
               attribute = 'createTime';
           } else if(target.hasClass('taskCompleteTime')){
               attribute = 'completeTime';
           }
           taskList.comparator = function (task) {
            return task.get(attribute);
           };
           taskList.sort();
           render();
       };
   ```
