---
title: APIs usadas na área de trabalho do AEM Forms
seo-title: APIs usadas na área de trabalho do AEM Forms
description: APIs públicas Java e JavaScript e métodos da área de trabalho do LiveCycle AEM Forms, expostos para personalização e automação.
seo-description: APIs públicas Java e JavaScript e métodos da área de trabalho do LiveCycle AEM Forms, expostos para personalização e automação.
uuid: 9602990e-8ac7-42eb-b507-50b3594055ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 4a73a973-fccf-466b-b4a0-47652a14a080
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# APIs usadas na área de trabalho do AEM Forms {#apis-used-in-aem-forms-workspace}

As APIs a seguir são usadas na área de trabalho do AEM Forms.

<table>
 <tbody>
  <tr>
   <td><strong>Método Javascript</strong></td>
   <td><strong>Nome do serviço</strong></td>
   <td><strong>Nome da API</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getGroups</td>
   <td>Pesquisa grupos. retorna uma lista de todos os grupos se nada for especificado, caso contrário, retorna grupos com o nome especificado.</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>Pesquisa usuários e grupos. Ele retorna uma lista de todos os usuários e grupos, se nada for especificado, caso contrário, retorna usuários e grupos com o nome especificado.</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>É chamado antes de enviar o formulário por meio do DocumentSubmitServlet. Ela define a ID da tarefa em uma variável de sessão (junto com o tempo de expiração) que é recuperada durante o envio real.</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>submit</td>
   <td>Ele submete o objeto de documento associado a uma tarefa (e, por sua vez, envia o processo).</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>Ele obtém todas as categorias raiz presentes no servidor.</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>Ele traz todas as crianças diretas para uma categoria.</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>Ele obtém todos os pontos de partida presentes no servidor em todas as categorias.</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>Isso chama um Ponto de partida e cria uma nova tarefa correspondente a um ponto de partida</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableTasks</td>
   <td>Ele busca todas as tarefas que são criadas e encaminhadas ou consultadas, salvas, atribuídas, atribuídas e salvas para o usuário conectado.</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getTask</td>
   <td>Ele busca uma tarefa específica.</td>
  </tr>
  <tr>
   <td>renderTask</td>
   <td>ProcessManagementTaskService</td>
   <td>renderizar</td>
   <td>Ele renderiza uma tarefa e retorna as informações necessárias para renderizar formulários como url de formulário, tipo de formulário, url de dados, se necessário, etc.</td>
  </tr>
  <tr>
   <td>submitWithBeforeData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithBeforeData</td>
   <td>Ele retorna o resultado da API de envio do TaskManager usando a chave de resultado.</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>Ele envia os dados do formulário (passados como sequência de caracteres) associados à tarefa usando a API de envio do TaskManager. É usado para formulários flexíveis que não chamam a API de envio do TaskManager.</td>
  </tr>
  <tr>
   <td>save</td>
   <td>ProcessManagementTaskService</td>
   <td>save</td>
   <td>Salva uma tarefa no servidor.</td>
  </tr>
  <tr>
   <td>complete</td>
   <td>ProcessManagementTaskService</td>
   <td>complete</td>
   <td>Ele conclui uma tarefa e a tarefa é passada para a próxima etapa de acordo com o projeto do processo.</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>Retorna o url de um anexo no qual o anexo está disponível.</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableAttachments</td>
   <td>Ele obtém todos os anexos e anotações de uma tarefa.</td>
  </tr>
  <tr>
   <td>participação</td>
   <td>ProcessManagementTaskService</td>
   <td>participação</td>
   <td>Ele compartilha uma tarefa com outro usuário. Outro usuário pode reivindicar a tarefa e se tornar proprietário da tarefa.</td>
  </tr>
  <tr>
   <td>avançar</td>
   <td>ProcessManagementTaskService</td>
   <td>avançar</td>
   <td>Ele encaminha uma tarefa para outro usuário.</td>
  </tr>
  <tr>
   <td>consulte</td>
   <td>ProcessManagementTaskService</td>
   <td>consulte</td>
   <td>Consulta uma tarefa com outro usuário.</td>
  </tr>
  <tr>
   <td>reclamação</td>
   <td>ProcessManagementTaskService</td>
   <td>reclamação</td>
   <td>Ele alega uma tarefa disponível na fila compartilhada.</td>
  </tr>
  <tr>
   <td>desbloqueio</td>
   <td>ProcessManagementTaskService</td>
   <td>desbloqueio</td>
   <td>Desbloqueia uma tarefa.</td>
  </tr>
  <tr>
   <td>bloqueio</td>
   <td>ProcessManagementTaskService</td>
   <td>bloqueio</td>
   <td>Bloqueia uma tarefa e a tarefa não pode ser reivindicada por outro usuário se compartilhada.</td>
  </tr>
  <tr>
   <td>rejeição</td>
   <td>ProcessManagementTaskService</td>
   <td>rejeição</td>
   <td>Retorna tarefa ao proprietário anterior da tarefa.</td>
  </tr>
  <tr>
   <td>abandono</td>
   <td>ProcessManagementTaskService</td>
   <td>abandono</td>
   <td>Ela exclui uma tarefa.</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisibility</td>
   <td>Ela define a visibilidade de uma tarefa. Se a visibilidade for definida como false, a tarefa não estará visível para o usuário depois.</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>É usado para pesquisar usuários. Retorna todos os usuários se nenhum nome for especificado; caso contrário, retorna usuários com o nome especificado.</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersInGroupByName</td>
   <td>Retorna todos os usuários em um grupo.</td>
  </tr>
  <tr>
   <td>GrantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>GrantQueueAccess</td>
   <td>Ele concede acesso da fila do usuário conectado ao usuário especificado. Ele basicamente está compartilhando sua própria fila com outro usuário.</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>Ele faz uma solicitação de acesso de fila de usuários especificados para usuários conectados. Se o usuário aprovar a solicitação, a fila do usuário será compartilhada com o usuário conectado.</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>Ele retorna todos os usuários que têm acesso à fila de usuários conectados.</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>Ele retorna todos os usuários cuja fila está acessível a um usuário.</td>
  </tr>
  <tr>
   <td>revogaQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revogaQueueAccess</td>
   <td>Ela remove um usuário da lista de usuários que têm acesso à fila de usuários conectados.</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>Ela remove um usuário da lista de usuários cuja fila está acessível ao usuário conectado.</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>Ele obtém todas as filas (filas próprias, compartilhadas e de grupo) acessíveis ao usuário conectado.<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>Ele sai das configurações de um usuário.</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>Salva as configurações de um usuário fora do escritório.</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>Retorna a lista de todos os processos.</td>
  </tr>
  <tr>
   <td>getParticipatedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getParticipatedProcesses</td>
   <td>Retorna a lista de todos os nomes de processos que tenham participado do usuário conectado.</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>Ele busca detalhes de uma instância do processo.<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>Ele busca todas as instâncias de processo para um processo.</td>
  </tr>
  <tr>
   <td>getCurrentTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getCurrentTasksForProcessInstance</td>
   <td>Ele obtém tarefas pendentes para uma instância do processo.</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>Ele obtém todas as tarefas para uma instância do processo.</td>
  </tr>
  <tr>
   <td>getAllSearchTemplates</td>
   <td>ProcessManagementQueryService</td>
   <td>getAllSearchTemplates</td>
   <td>Ele retorna a lista de todos os modelos de pesquisa.</td>
  </tr>
  <tr>
   <td>getTemplate</td>
   <td>ProcessManagementQueryService</td>
   <td>getTemplate</td>
   <td>Ele retorna o conteúdo de um modelo de pesquisa.</td>
  </tr>
  <tr>
   <td>findTasksJson<br /> </td>
   <td>ProcessManagementQueryService</td>
   <td>findTasksJson</td>
   <td>Ele pesquisa e retorna todas as tarefas que satisfazem todas as condições de um modelo de pesquisa.</td>
  </tr>
  <tr>
   <td>getAssignmentsForTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAssignmentsForTask</td>
   <td>Recebe todas as atribuições de uma tarefa. Por exemplo:- Se o usuário encaminha ou consulta uma tarefa a outro usuário, então é uma atribuição para uma tarefa.</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>TaskManagerService</td>
   <td>deleteAttachment</td>
   <td>Exclui um anexo.</td>
  </tr>
  <tr>
   <td>initialize</td>
   <td>ProcessManagementClientSessionService</td>
   <td>initialize</td>
   <td>Renovará a afirmação, se necessário. Autentica o usuário. Define parâmetros de sessão para informações do servidor/cliente. Retorna as informações do usuário e o intervalo de pesquisa.</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>Ele retorna todas as tarefas de relatórios diretos do gerenciador conectado.</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>Ele retorna a tarefa do relatório direto especificado do gerenciador conectado.</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>Ele encaminha uma tarefa de um relatório direto para outro usuário.</td>
  </tr>
  <tr>
   <td>cancelTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>cancelTaskOfDirectReport</td>
   <td>Ele retorna uma tarefa de um relatório direto para o usuário anterior.</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>Ele obtém uma propriedade do Workspace para um usuário.</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>delete</td>
   <td>Ela remove uma propriedade do Workspace para um usuário.</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>Retorna todas as propriedades do Workspace para um usuário.</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>WorkspacePropertyService</td>
   <td>setProperty</td>
   <td>Ela define uma propriedade do Workspace para um usuário.</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>Ele obtém o url da imagem do usuário para o usuário conectado.</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>Ele obtém o url de imagem do usuário para o usuário especificado.</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>Ele carrega uma nota no servidor para uma tarefa.</td>
  </tr>
  <tr>
   <td>uploadRMAToServer (também é chamado diretamente do modelo html)<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>Ele carrega um anexo no servidor para uma tarefa.</td>
  </tr>
  <tr>
   <td>getImageURL (também é chamado diretamente do modelo html)</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>Ele obtém imagem para um processo.</td>
  </tr>
 </tbody>
</table>
