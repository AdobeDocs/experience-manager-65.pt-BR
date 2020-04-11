---
title: Personalizar tabelas de rastreamento
seo-title: Personalizar tabelas de rastreamento
description: Como personalizar a exibição dos detalhes dos processos do usuário na tabela tarefa exibida na guia de rastreamento da área de trabalho do AEM Forms.
seo-description: Como personalizar a exibição dos detalhes dos processos do usuário na tabela tarefa exibida na guia de rastreamento da área de trabalho do AEM Forms.
uuid: 13d6ebf2-99d5-434f-85f9-b0cba5f5751a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: bb7a6e9f-4f28-4d97-8a0c-949259fd6857
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Personalizar tabelas de rastreamento{#customize-tracking-tables}

A guia de rastreamento na área de trabalho do AEM Forms é usada para exibir os detalhes das instâncias de processo nas quais o usuário conectado está envolvido. Para visualização das tabelas de rastreamento, primeiro selecione um nome de processo no painel esquerdo para ver sua lista de instâncias no painel do meio. Selecione uma instância do processo para ver uma tabela de tarefas gerada por essa instância no painel direito. Por padrão, as colunas da tabela exibem os seguintes atributos de tarefa (o atributo correspondente no modelo de tarefa é fornecido entre parênteses):

* ID ( `taskId`)
* Nome ( `stepName`)
* Instruções ( `instructions`)
* Ação selecionada ( `selectedRoute`)
* Hora de criação ( `createTime`)
* Tempo de conclusão ( `completeTime`)
* Proprietário ( `currentAssignment.queueOwner`)

Os atributos restantes no modelo de tarefa disponíveis para exibição na tabela de tarefa são:

<table>
 <tbody>
  <tr>
   <td><p>actionInstanceId</p> </td>
   <td><p>isOpenFullScreen</p> </td>
   <td><p>memoryCount</p> </td>
  </tr>
  <tr>
   <td><p>classOfTask</p> </td>
   <td><p>isOwner</p> </td>
   <td><p>routeList</p> </td>
  </tr>
  <tr>
   <td><p>queryGroupId</p> </td>
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
   <td><p>createId</p> </td>
   <td><p>isVisible</p> </td>
   <td><p>serviceTitle</p> </td>
  </tr>
  <tr>
   <td><p>currentAssignment</p> </td>
   <td><p>nextLembrete</p> </td>
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
   <td><p>priority</p> </td>
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

Para as seguintes personalizações na tabela tarefa, é necessário fazer alterações semânticas no código-fonte. Consulte [Introdução à personalização da área de trabalho](/help/forms/using/introduction-customizing-html-workspace.md) do AEM Forms para saber como fazer alterações semânticas usando o SDK da área de trabalho e criar um pacote minified a partir da fonte alterada.

## Alteração das colunas da tabela e sua ordem {#changing-table-columns-and-their-order}

1. Para modificar os atributos de tarefa exibidos na tabela e sua ordem, configure o arquivo /ws/js/runtime/templates/processinstancehistory.html :

   ```as3
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

   ```as3
   <table>
       <tbody>
           <%_.each(obj, function(task){%>
           <tr>
               <!-- Put the task attributes in the order of headings, for example -->
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

Para classificar a tabela de lista de tarefa ao clicar no cabeçalho da coluna:

1. Registre um manipulador de cliques para `.fixedTaskTableHeader th` o no arquivo `js/runtime/views/processinstancehistory.js`.

   ```as3
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   No manipulador, chame a `onTaskTableHeaderClick` função de `js/runtime/util/history.js`.

   ```as3
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. Exponha o `TaskTableHeaderClick` método em `js/runtime/util/history.js`.

   O método encontra o atributo tarefa do evento click, classifica a lista de tarefas desse atributo e renderiza a tabela tarefa com a lista de tarefas classificada.

   A classificação é feita usando a função de classificação Backbone na coleção da lista de tarefas, fornecendo uma função de comparação.

   ```as3
       return {
           //other methods
           onTaskTableHeaderClick  : onTaskTableHeaderClick,
           //other methods
       };
   ```

   ```as3
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
