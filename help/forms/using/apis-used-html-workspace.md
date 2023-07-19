---
title: APIs usadas no espaço de trabalho do AEM Forms
seo-title: APIs used in AEM Forms workspace
description: APIs públicas de Java e JavaScript e métodos do espaço de trabalho do LiveCycle AEM Forms, expostos para personalização e automação.
seo-description: Public Java and JavaScript APIs and methods of LiveCycle AEM Forms workspace, exposed for customization and automation.
uuid: 9602990e-8ac7-42eb-b507-50b3594055ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 4a73a973-fccf-466b-b4a0-47652a14a080
exl-id: 9034f73a-83f3-498e-b6a6-ad6577aa1a3a
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---

# APIs usadas no espaço de trabalho do AEM Forms {#apis-used-in-aem-forms-workspace}

As APIs a seguir são usadas no espaço de trabalho do AEM Forms.

<table>
 <tbody>
  <tr>
   <td><strong>Método JavaScript</strong></td>
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
   <td>Pesquisa usuários e grupos. Ele retorna uma lista de todos os usuários e grupos se nada for especificado, caso contrário, retorna usuários e grupos com o nome especificado.</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>Ele é chamado antes do envio do formulário por meio do DocumentSubmitServlet. Ele define a ID da tarefa em uma variável de sessão (juntamente com o tempo de expiração) que é recuperada durante o envio real.</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>enviar</td>
   <td>Ele envia o objeto do documento associado a uma tarefa (e envia o processo por sua vez).</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>Ele busca todas as categorias raiz presentes no servidor.</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>Ele busca todos os filhos diretos de uma categoria.</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>Ele busca todos os pontos de partida presentes no servidor em todas as categorias.</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>Isso chama um ponto inicial e cria uma nova tarefa correspondente a um ponto inicial</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>getAllActionableTasks</td>
   <td>Ele busca todas as tarefas que são criadas e encaminhadas ou consultadas, salvas, atribuídas, atribuídas e salvas para o usuário conectado.</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>getTask</td>
   <td>Busca uma tarefa específica.</td>
  </tr>
  <tr>
   <td>renderTask</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>renderizar</td>
   <td>Ela renderiza uma tarefa e retorna as informações necessárias para renderizar o formulário como URL do formulário, tipo de formulário, URL de dados, se necessário, etc.</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>submitWithPriorData</td>
   <td>Ele retorna o resultado da API de envio do TaskManager usando a chave de resultado.</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>submitWithData</td>
   <td>Ele envia os dados de formulário (transmitidos como uma sequência de caracteres) associados à tarefa usando a API de envio do TaskManager. É usado para formulários flexíveis que não chamam a API de envio do TaskManager.</td>
  </tr>
  <tr>
   <td>save</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>save</td>
   <td>Ele salva uma tarefa no servidor.</td>
  </tr>
  <tr>
   <td>concluído</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>concluído</td>
   <td>Ele conclui uma tarefa e a tarefa é passada para a próxima etapa de acordo com o design do processo.</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>getAttachment</td>
   <td>Retorna o URL de um anexo em que o anexo está disponível.</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>getAllActionableAttachment</td>
   <td>Ele busca todos os anexos e notas de uma tarefa.</td>
  </tr>
  <tr>
   <td>compartilhar</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>compartilhar</td>
   <td>Ele compartilha uma tarefa com outro usuário. Outro usuário pode reivindicar a tarefa e se tornar proprietário da tarefa.</td>
  </tr>
  <tr>
   <td>avançar</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>avançar</td>
   <td>Ele encaminha uma tarefa para outro usuário.</td>
  </tr>
  <tr>
   <td>consultar</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>consultar</td>
   <td>Ele consulta uma tarefa com outro usuário.</td>
  </tr>
  <tr>
   <td>declaração</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>declaração</td>
   <td>Reivindica uma tarefa disponível na fila compartilhada.</td>
  </tr>
  <tr>
   <td>desbloquear</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>desbloquear</td>
   <td>Desbloqueia uma tarefa.</td>
  </tr>
  <tr>
   <td>bloquear</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>bloquear</td>
   <td>Ela bloqueia uma tarefa, e a tarefa não pode ser reivindicada por outro usuário se compartilhada.</td>
  </tr>
  <tr>
   <td>Rejeitar</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>Rejeitar</td>
   <td>Retorna a tarefa ao proprietário anterior da tarefa.</td>
  </tr>
  <tr>
   <td>abandonar</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>abandonar</td>
   <td>Ele exclui uma tarefa.</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>setVisibility</td>
   <td>Ela define a visibilidade de uma tarefa. Se a visibilidade for definida como falsa, a tarefa não estará visível para o usuário posteriormente.</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>É usado para pesquisar usuários. Retorna todos os usuários se nenhum nome for especificado, caso contrário retorna os usuários com o nome especificado.</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersInGroupByName</td>
   <td>Retorna todos os usuários em um grupo.</td>
  </tr>
  <tr>
   <td>grantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>grantQueueAccess</td>
   <td>Concede acesso da fila do usuário conectado ao usuário especificado. É basicamente compartilhar sua própria fila com outro usuário.</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>Ele faz uma solicitação de acesso da fila de um usuário especificado para o usuário conectado. Se o usuário aprovar a solicitação, a fila do usuário será compartilhada com o usuário conectado.</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>Retorna todos os usuários que têm acesso à fila do usuário conectado.</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>Retorna todos os usuários cuja fila está acessível a um usuário.</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>Ele remove um usuário da lista de usuários que têm acesso à fila do usuário conectado.</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>Remove um usuário da lista de usuários cuja fila está acessível ao usuário conectado.</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>Ele torna todas as filas (próprias, compartilhadas e de grupo) acessíveis ao usuário logado.<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>Ele fica fora das configurações do escritório de um usuário.</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>Ele salva as configurações de ausência temporária de um usuário.</td>
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
   <td>Retorna uma lista de todos os nomes de processos participados pelo usuário conectado.</td>
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
   <td>Ele busca todas as instâncias de um processo.</td>
  </tr>
  <tr>
   <td>getPendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getPendingTasksForProcessInstance</td>
   <td>Ele obtém tarefas pendentes para uma instância de processo.</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>Ele obtém todas as tarefas para uma instância de processo.</td>
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
   <td>ServiçoTarefaDeGerenciamentoDeProcesso</td>
   <td>getAssignmentsForTask</td>
   <td>Ele obtém todas as atribuições de uma tarefa. Por exemplo, :- Se o usuário encaminhar ou consultar uma tarefa com outro usuário, então ela será uma atribuição para uma tarefa.</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>ServiçoGerenciadorTarefa</td>
   <td>deleteAttachment</td>
   <td>Ele exclui um anexo.</td>
  </tr>
  <tr>
   <td>inicializar</td>
   <td>ProcessManagementClientSessionService</td>
   <td>inicializar</td>
   <td>Se necessário, renova a afirmação. Autentica o usuário. Define parâmetros de sessão para informações do servidor/cliente. Retorna as informações do usuário e o intervalo de pesquisa.</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessarGerenciamentoEquipeTarefasServiço</td>
   <td>getTasksForDirectReports</td>
   <td>Retorna todas as tarefas de subordinados diretos de gerente conectado.</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessarGerenciamentoEquipeTarefasServiço</td>
   <td>getDirectReportTask</td>
   <td>Retorna a tarefa do subordinado direto especificado do gerente conectado.</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessarGerenciamentoEquipeTarefasServiço</td>
   <td>forwardTaskOfDirectReport</td>
   <td>Ele encaminha uma tarefa de subordinação direta a outro usuário.</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessarGerenciamentoEquipeTarefasServiço</td>
   <td>rejectTaskOfDirectReport</td>
   <td>Retorna uma tarefa de um subordinado direto ao usuário anterior.</td>
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
   <td>excluir</td>
   <td>Remove uma propriedade do Workspace para um usuário.</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>Retorna todas as propriedades do Workspace de um usuário.</td>
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
   <td>Ele obtém o URL da imagem do usuário para o usuário conectado.</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>Ele obtém o URL da imagem do usuário para o usuário especificado.</td>
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
   <td>Ele obtém a imagem para um processo.</td>
  </tr>
 </tbody>
</table>
