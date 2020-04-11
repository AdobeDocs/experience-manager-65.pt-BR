---
title: Descrição do objeto JSON da área de trabalho do AEM Forms
seo-title: Descrição do objeto JSON da área de trabalho do AEM Forms
description: Informações conceituais sobre os objetos JavaScript JSON usados na área de trabalho do LiveCycle AEM Forms para personalização, extensão, modificação e reutilização.
seo-description: Informações conceituais sobre os objetos JavaScript JSON usados na área de trabalho do LiveCycle AEM Forms para personalização, extensão, modificação e reutilização.
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Descrição do objeto JSON da área de trabalho do AEM Forms {#aem-forms-workspace-json-object-description}

Os objetos JSON usados na área de trabalho do AEM Forms estão descritos abaixo.

1. Categoria

   As Categorias estão presentes na guia Processo de start da área de trabalho. Essas categorias são usadas para classificar os pontos de partida.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente cliente</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>name</td>
   <td>F</td>
   <td>Nome da Categoria</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>Category ID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>descrição<br type="_moz" /> </td>
   <td>F</td>
   <td>descrição da Categoria<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>Contém oid da categoria pai<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>Contém lista de todos os pontos iniciais presentes em uma categoria</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>Contém lista de categorias secundárias diretas de uma categoria<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Todos os pontos de partida e Favoritos são categorias definidas no lado do cliente. A categoria favorita contém todos os pontos de partida marcados pelo usuário como favorito. A categoria Todos os pontos de partida contém todos os pontos de partida.

1. Ponto de partida

   O ponto inicial é usado para start de um processo do espaço de trabalho quando chamado.

   | **Propriedade** | **Somente cliente** | **Comentários** |
   |---|---|---|
   | categoryId | F | Ele contém a ID da categoria à qual o ponto de partida pertence. |
   | descrição | F | Ele contém a descrição de um ponto de partida. |
   | name | F | Ele contém o nome do ponto de partida. |
   | serializedImageTicket | F | Ele contém o ticket de imagem correspondente ao ponto de partida. Esse ticket de imagem é usado no campo imageUrl do ponto de partida para obter a imagem do ponto de partida do servidor. |
   | serviceName | F | Ele contém o nome do serviço para o ponto de partida. |
   | startpointId | F | Ele contém ID do ponto de partida. |
   | isFavorite | T | Indica se o ponto de partida é o favorito ou não. Verdadeiro se o ponto de partida for o favorito senão falso. |
   | isDefaultImage | T | Indica se há uma imagem especificada para processo ou não. True se não houver imagem associada ao processo; caso contrário, false. |
   | tarefa | T | Ele contém a tarefa criada quando o ponto de partida é chamado. |
   | imageUrl | T | Ele contém o url da imagem correspondente ao ponto de partida. |

1. Tarefa

   As Tarefas são atribuídas a usuários/grupos e incluem uma interface do usuário — um formulário ou um Guia (obsoleto) — que pode ser preenchida com dados. Quando uma tarefa é atribuída aos usuários, eles recebem o formulário ou o Guia para preencher e enviar.

<table>
 <tbody>
  <tr>
   <td>Propriedade<br /> </td>
   <td>Client Only<br /> </td>
   <td>Comentários<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>A classe de tarefa é 'LC8' quando a tarefa é lc8 tarefa else 'Standard'.<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>Ele contém o carimbo de data e hora quando a tarefa é concluída.<br /> </td>
  </tr>
  <tr>
   <td>queryGroupId<br /> </td>
   <td>F</td>
   <td>Ele contém a ID de um grupo para o qual a tarefa pode ser consultada. Ela é definida durante a criação do processo.<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>Ele contém o carimbo de data e hora quando a tarefa é criada.<br /> </td>
  </tr>
  <tr>
   <td>createId<br /> </td>
   <td>F</td>
   <td>Ele contém a ID do usuário que criou a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>Ele contém detalhes sobre a atribuição atual da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>prazo<br /> </td>
   <td>F</td>
   <td>Contém o carimbo de data e hora que uma tarefa atingirá o seu prazo.<br /> </td>
  </tr>
  <tr>
   <td>descrição<br /> </td>
   <td>F</td>
   <td>Ele contém a descrição da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>Ele contém o nome de exibição da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>Ele contém a ID de um grupo para o qual a tarefa pode ser encaminhada. Ela é definida durante a criação do processo.<br /> </td>
  </tr>
  <tr>
   <td>instructions<br /> </td>
   <td>F</td>
   <td>Contém instruções para uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>Verdadeiro se a tarefa estiver bloqueada.<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>True se for necessário abrir um formulário de tarefa para completar a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>Se verdadeiro, ao abrir a tarefa, o formulário é exibido na tela inteira pela primeira vez.<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>Se verdadeiro, a rota deve ser selecionada para concluir a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>Anexos são mostrados se for verdadeiro.<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>Se verdadeiro, a tarefa é criada do ponto de start.<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>True se a tarefa estiver visível no espaço de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>nextLembrete<br /> </td>
   <td>F</td>
   <td>Carimbo de data e hora do próximo lembrete.<br /> </td>
  </tr>
  <tr>
   <td>priority<br /> </td>
   <td>F</td>
   <td>Contém prioridade de tarefas.<br /> 1 = Prioridade<br /> mais alta 2 = Prioridade<br /> alta 3 = Prioridade<br /> normal 4 = Prioridade<br /> baixa 5 = Prioridade mais baixa<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>Id da instância do processo da qual a tarefa faz parte.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>Status da instância do processo de tarefa.<br /> </td>
  </tr>
  <tr>
   <td>memoryCount<br /> </td>
   <td>F</td>
   <td>Contagem de lembretes para a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>Ele contém lista de rotas associadas à tarefa. O usuário pode concluir a tarefa selecionando qualquer uma das rotas da lista de rota.<br /> </td>
  </tr>
  <tr>
   <td>seletedRoute<br /> </td>
   <td>F</td>
   <td>Ele contém o nome da rota selecionada quando a tarefa foi concluída.<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>Ele contém o tíquete de imagem correspondente à tarefa. Esse ticket de imagem é usado no campo imageUrl da tarefa, para obter uma imagem para tarefa do servidor.<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>Ele contém o nome do serviço para tarefa.<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>Ele contém o título do serviço de tarefa.<br /> </td>
  </tr>
  <tr>
   <td>status<br /> </td>
   <td>F</td>
   <td>1 = Criada (a Tarefa é criada a partir do ponto do start.)<br /> 2 = Criada e salva (a Tarefa é criada do ponto de start e salva.)<br /> 3 = Atribuída (a Tarefa é atribuída ao usuário depois que o processo é iniciado.)<br /> 4 = Atribuída e salva (a Tarefa é atribuída e salva.)<br /> 100 = Concluído (a Tarefa é concluída.)<br /> 101 = Prazo (a Tarefa atingiu o prazo.)<br /> 102 = Terminado<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>Ele contém o nome da tarefa definida durante a criação do processo.<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>Contém url de resumo de tarefa.<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>É lista controle de acesso para tarefa.<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>Id de uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>Carimbo de data e hora quando a tarefa foi atualizada pela última vez.<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>Ele contém url de formulário para uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>Ele contém o tipo de formulário de tarefa. Usando esse campo, a tarefa é renderizada no cliente como pdf para, formulário swf etc.<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>Se verdadeiro, as ações de rota estarão visíveis no espaço de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>Se verdadeiro, ações como avançar, consultar, compartilhar são visíveis na área de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>supportedOffline<br /> </td>
   <td>T</td>
   <td>Se verdadeiro, o formulário pode ser colocado offline. Isso é somente para formulários pdf.<br /> </td>
  </tr>
  <tr>
   <td>supportedSave<br /> </td>
   <td>T</td>
   <td>Se verdadeiro, o usuário pode salvar a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>Esse objeto contém opções que são usadas para enviar formulários pdf pelo leitor, caso o formulário pdf não contenha nenhum botão Enviar.<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>Indica se há uma imagem especificada para processo ou não. True se não houver imagem associada ao processo; caso contrário, false.<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>Ele contém listas de tarefas que são usadas na guia Histórico de detalhes da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>True se o usuário conectado for proprietário da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>Ele contém todas as ações que podem ser realizadas na tarefa.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>Ele contém todas as ações de rota disponíveis para uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>Ele contém comandos como encaminhar, compartilhar e consultar se disponível para uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>Ele contém comandos como bloquear, desbloquear, abandonar, retornar, reivindicar e assim por diante, conforme disponível.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>Ele contém informações sobre a instância do processo de tarefa.<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>Ele contém vários objetos de variáveis de processo, se presentes.<br /> </td>
  </tr>
  <tr>
   <td>pendenteTasks<br /> </td>
   <td>T</td>
   <td>Ele contém lista de tarefas pendentes para a instância do processo tarefa.<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>É uma gama de objetos. Cada objeto contém detalhes sobre a rota e sua mensagem de confirmação correspondente, se houver.<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>É url para os dados da forma de uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>Esta é a configuração para formulários de aplicativos de terceiros.<br /> </td>
  </tr>
  <tr>
   <td>submitted<br /> </td>
   <td>T</td>
   <td>Verdadeiro se a tarefa for enviada.<br /> </td>
  </tr>
  <tr>
   <td>attachments<br /> </td>
   <td>T</td>
   <td>Lista de fixação de uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>Atribuições<br /> </td>
   <td>T</td>
   <td>Lista de atribuições de uma tarefa.<br /> </td>
  </tr>
 </tbody>
</table>

1. Filtro

   O filtro é basicamente uma fila de usuários ou grupos. Quando uma tarefa é atribuída ao usuário/grupo, a tarefa é adicionada à fila correspondente.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente cliente</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>True se a fila for a fila padrão do usuário conectado, caso contrário, false.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>name<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome do proprietário da fila.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>Id da fila.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tipo</td>
   <td>F</td>
   <td>Ele contém o tipo da fila.<br /> 0 - Fila de usuários.<br /> 1. Fila compartilhada.<br /> 2. Fila de grupo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>query</td>
   <td>T</td>
   <td>Ele contém o query associado a um filtro. Este query é usado para pesquisar tarefas na lista de tarefas completa.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tarefas</td>
   <td>T</td>
   <td>Ele contém lista de todas as tarefas que pertencem a um filtro.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Fora do escritório

   Você pode gerenciar seu agendamento fora do escritório e controlar o fluxo de tarefas atribuídas a você na sua ausência.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong><br type="_moz" /> </td>
   <td><strong>Somente cliente</strong><br type="_moz" /> </td>
   <td><strong>Comentários</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRanges<br type="_moz" /> </td>
   <td>F</td>
   <td>Ele contém objetos de matriz de agendamentos esgotados de um usuário. Em cada objeto de programação, o campo startDate contém a data do start da programação e o campo endDate contém a data final da programação. Se endDate for nulo na programação, isso implica que o usuário não programou a data final da programação fora do escritório.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>Verdadeiro se não houver nenhum designado primário no caso de o usuário estar fora do escritório.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>Verdadeiro se o usuário estiver fora do escritório.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>Ele contém detalhes do usuário atribuído como principal designado pelo usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>F</td>
   <td>Ele contém uma série de objetos para designá-los fora do escritório específicos do processo. Em cada objeto designado específico do processo, processName contém o nome do processo, isNotDesignated é verdadeiro se nenhum usuário for atribuído ao processo correspondente, e userDesignated é nulo se nenhum usuário tiver atribuído mais detalhes do usuário atribuído ao processo correspondente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processes<br type="_moz" /> </td>
   <td>T</td>
   <td>Ele contém uma lista de todos os processos disponíveis para o usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Ele contém as configurações iniciais do usuário que não estão no escritório, que são buscadas inicialmente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Contém configurações fora do escritório modificadas.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>Contém lista de usuários que são pesquisados pelo usuário conectado até a data.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Instância do processo

   Uma instância do processo é criada quando um processo é chamado via área de trabalho ou bancada.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente cliente</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>descrição<br type="_moz" /> </td>
   <td>F</td>
   <td>Descrição da instância do processo<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>iniciador</td>
   <td>F</td>
   <td>Nome do iniciador de uma instância do processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>ID do iniciador da instância do processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Carimbo de data e hora quando o processo é concluído.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID da instância do processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Iniciado<br /> 1 = Executando<br /> 2 = Concluído<br /> 3 = Concluindo<br /> 4 = Terminado<br /> 5 = Finalizando<br /> 6 = Suspenso<br /> 7 = Suspendendo<br /> 8 = Cancelando a suspensão<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome do processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Carimbo de data e hora quando o processo começou.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>Matriz de objetos de variáveis de processo. Cada objeto de variável de processo contém o nome que é o nome da variável de processo, o valor que é o valor da variável de processo e o tipo que é o tipo de variável de processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lista de tarefas<br type="_moz" /> </td>
   <td>T</td>
   <td>Tarefas geradas por esta instância do processo.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Nome do processo

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente cliente</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>Versão principal de um processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>Versão secundária de um processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome do processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>F</td>
   <td>Título do processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>T</td>
   <td>Lista de instâncias de processo para este processo.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Objeto de Atribuição de Tarefa

   O objeto de atribuição de Tarefa contém informações sobre a atribuição da tarefa. Veja a seguir as propriedades da atribuição de tarefas.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente cliente</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>assignCreateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Carimbo de data e hora quando essa atribuição de uma tarefa é criada.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Atribuição<br /> inicial 1 = Encaminhar (a Tarefa foi encaminhada para o proprietário atual da tarefa.)<br /> 2 = Devolvido (a Tarefa foi devolvida ao proprietário atual da tarefa pelo proprietário anterior da tarefa.)<br /> 3 = Solicitada (a Tarefa foi reivindicada pelo proprietário atual da tarefa.)<br /> 4 = Escalonamento (a Tarefa foi atribuída ao proprietário atual da tarefa após o escalonamento.)<br /> 5 = Administrador atribuído (a Tarefa foi atribuída pelo administrador ao proprietário atual da tarefa.)<br /> 6 = Consultada (a Tarefa foi consultada para o proprietário atual da tarefa.)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Carimbo de data e hora quando esta atribuição de uma tarefa é atualizada.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID da Fila do proprietário atual da tarefa.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome do proprietário atual da tarefa.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID do proprietário atual da tarefa.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Objeto ACL de Tarefa

   O objeto ACL de Tarefa contém informações sobre permissões como encaminhar, compartilhar, consultar etc. de uma tarefa. Veja a seguir as propriedades da ACL de tarefa.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente cliente</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>F</td>
   <td>Se verdadeiro, os anexos podem ser adicionados à tarefa.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>Se verdadeiro, as notas podem ser adicionadas à tarefa.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>Se for verdade, a tarefa pode ser reivindicada.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>Se for verdade, a tarefa pode ser consultada.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>Se verdadeiro, a tarefa pode ser encaminhada.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>Se verdadeiro, a tarefa pode ser compartilhada.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Anexo da Tarefa

   Anexos podem ser adicionados a uma tarefa. O anexo pode ser do tipo anexo e nota. Veja a seguir as propriedades do objeto de anexo.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente cliente</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>F</td>
   <td>Carimbo de data e hora ao criar o anexo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID do usuário que adicionou o anexo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome do usuário que adicionou o anexo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>descrição<br type="_moz" /> </td>
   <td>F</td>
   <td>Descrição do anexo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>fileName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome do anexo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>F</td>
   <td>ID do anexo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>F</td>
   <td>Carimbo de data e hora da última modificação do anexo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>Se verdadeiro, nota é uma nota estendida (longa).<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>permissões<br type="_moz" /> </td>
   <td>F</td>
   <td>Permissões associadas a um anexo. o campo allowRead é para permissão de leitura, allowWrite é para permissão de gravação, allowDelete é para permissão de exclusão.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>size<br type="_moz" /> </td>
   <td>F</td>
   <td>Tamanho do anexo em bytes.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID da tarefa à qual o anexo é adicionado.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tipo<br type="_moz" /> </td>
   <td>F</td>
   <td>Tipo é anexo para arquivos e Tipo é nota para notas.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>Ele contém a data de criação do anexo de acordo com as configurações da interface do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>Descrição do anexo formatado. Usado para exibir caracteres especiais presentes na descrição do anexo na área de trabalho do AEM Forms.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>Nome do anexo formatado. Usado para exibir caracteres especiais presentes no nome do anexo na área de trabalho do AEM Forms. Isto é apenas para notas.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Usuário

   Veja a seguir as propriedades do objeto do usuário.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente cliente</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>address<br type="_moz" /> </td>
   <td>F</td>
   <td>Endereço do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome comum do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>descrição<br type="_moz" /> </td>
   <td>F</td>
   <td>Descrição do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>F</td>
   <td>Lista do grupo do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome de exibição do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de email do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>Verdadeiro se o usuário estiver fora do escritório.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>F</td>
   <td>O sobrenome do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>F</td>
   <td>ID do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome da organização do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>postalAddress<br type="_moz" /> </td>
   <td>F</td>
   <td>Endereço postal do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephone<br type="_moz" /> </td>
   <td>F</td>
   <td>Número de contato do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>phoneNumber<br type="_moz" /> </td>
   <td>F</td>
   <td>Número de contato do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>ID de logon do usuário.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
