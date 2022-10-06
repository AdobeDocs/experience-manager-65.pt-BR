---
title: Descrição do objeto JSON do espaço de trabalho do AEM Forms
seo-title: AEM Forms workspace JSON object description
description: Informações conceituais sobre os objetos JavaScript JSON usados na área de trabalho do LiveCycle AEM Forms para personalização, extensão, modificação e reutilização.
seo-description: Conceptual information about the JSON JavaScript objects used in LiveCycle AEM Forms workspace for customization, extension, modification, and reuse.
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
exl-id: f837a2b3-4650-4261-84c6-291bb2a46dc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2109'
ht-degree: 9%

---

# Descrição do objeto JSON do espaço de trabalho do AEM Forms {#aem-forms-workspace-json-object-description}

Os objetos JSON usados no AEM Forms workspace são descritos abaixo.

1. Categoria

   As categorias estão presentes na guia Iniciar processo do espaço de trabalho. Essas categorias são usadas para classificar os pontos de partida.

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
   <td>Nome da categoria</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>ID da categoria<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>descrição<br type="_moz" /> </td>
   <td>F</td>
   <td>Descrição da categoria<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>Contém oid da categoria principal<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>Contém a lista de todos os pontos iniciais presentes em uma categoria</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>Contém a lista de categorias secundárias diretas de uma categoria<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Todos os pontos de partida e Favoritos são categorias definidas no lado do cliente. A categoria favorita contém todos os pontos de partida que são marcados pelo usuário como favorito. A categoria Todos os pontos de partida contém todos os pontos de partida.

1. Ponto de partida

   O ponto de partida é usado para iniciar um processo do espaço de trabalho quando chamado.

   | **Propriedade** | **Somente cliente** | **Comentários** |
   |---|---|---|
   | categoryId | F | Ele contém o ID da categoria à qual o ponto de partida pertence. |
   | descrição | F | Ele contém a descrição de um ponto de partida. |
   | name | F | Ele contém o nome do ponto de partida. |
   | serializedImageTicket | F | Ele contém o tíquete de imagem correspondente ao ponto de partida. Esse tíquete de imagem é usado no campo imageUrl do ponto de partida para obter a imagem do ponto de partida do servidor. |
   | serviceName | F | Ele contém o nome do serviço para ponto de partida. |
   | startpointId | F | Ele contém ID do ponto de partida. |
   | isFavorite | T | Indica se o ponto de partida é favorito ou não. Verdadeiro se o ponto de partida for o favorito ou falso. |
   | isDefaultImage | T | Indica se há uma imagem especificada para processo ou não. Verdadeiro se não houver imagem associada ao processo; caso contrário, falso. |
   | tarefa | T | Ela contém a tarefa criada quando o ponto de partida é chamado. |
   | imageUrl | T | Ele contém o url da imagem correspondente ao ponto de partida. |

1. Tarefa

   As tarefas são atribuídas a usuários/grupos e incluem uma interface de usuário — um formulário ou um Guia (obsoleto) — que pode ser preenchida com dados. Quando os usuários recebem uma tarefa, eles recebem o formulário ou o Guia para concluir e enviar.

<table>
 <tbody>
  <tr>
   <td>Propriedade<br /> </td>
   <td>Somente cliente<br /> </td>
   <td>Comentários<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>A classe de tarefa é 'LC8' quando a tarefa é lc8 task else 'Standard'.<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>Ele contém o carimbo de data e hora em que a tarefa é concluída.<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>Ele contém a ID de um grupo para o qual a tarefa pode ser consultada. Ele é definido durante o design do processo.<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>Ele contém o carimbo de data e hora em que a tarefa é criada.<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>F</td>
   <td>Ele contém a id do usuário que criou a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>Ele contém detalhes sobre a atribuição atual da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>prazo<br /> </td>
   <td>F</td>
   <td>Ele contém o carimbo de data e hora que uma tarefa atingirá seu prazo final.<br /> </td>
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
   <td>Ele contém a ID de um grupo para o qual a tarefa pode ser encaminhada. Ele é definido durante o design do processo.<br /> </td>
  </tr>
  <tr>
   <td>instruções<br /> </td>
   <td>F</td>
   <td>Ele contém instruções para uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>True se a tarefa estiver bloqueada.<br /> </td>
  </tr>
  <tr>
   <td>ismustOpenToComplete<br /> </td>
   <td>F</td>
   <td>True se o formulário de tarefa tiver de ser aberto para concluir a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>Se verdadeiro, ao abrir a tarefa, o formulário ocupa a tela completa primeiro.<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>Se true, a rota deverá ser selecionada para concluir a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>Os anexos são mostrados se for verdadeiro.<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>Se true, a tarefa será criada a partir do ponto de início.<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>True se a tarefa estiver visível no espaço de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>nextLembreder<br /> </td>
   <td>F</td>
   <td>Carimbo de data/hora do próximo lembrete.<br /> </td>
  </tr>
  <tr>
   <td>priority<br /> </td>
   <td>F</td>
   <td>Ele contém prioridade de tarefa.<br /> 1 = Prioridade mais alta<br /> 2 = Prioridade alta<br /> 3 = Prioridade normal<br /> 4 = Prioridade baixa<br /> 5 = Prioridade mais baixa<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>Id da instância do processo da qual a tarefa faz parte.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>Status da instância de processo da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>reminderCount<br /> </td>
   <td>F</td>
   <td>Ele contém a contagem de lembretes para a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>Ele contém a lista de rotas associadas à tarefa. O usuário pode concluir a tarefa selecionando qualquer uma das rotas da lista de rotas.<br /> </td>
  </tr>
  <tr>
   <td>seletedRoute<br /> </td>
   <td>F</td>
   <td>Ele contém o nome da rota selecionada quando a tarefa foi concluída.<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>Ele contém o tíquete de imagem correspondente à tarefa. Esse tíquete de imagem é usado no campo imageUrl da tarefa para obter a imagem da tarefa do servidor.<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>Ele contém o nome do serviço para a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>Ele contém o título do serviço para a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>status<br /> </td>
   <td>F</td>
   <td>1 = Criado (a tarefa é criada a partir do ponto de início.)<br /> 2 = Criada e salva (a tarefa é criada a partir do ponto de início e salva.)<br /> 3 = Atribuído (a tarefa é atribuída ao usuário após o início do processo.)<br /> 4 = Atribuído e salvo (a tarefa é atribuída e salva.)<br /> 100 = Concluído (Tarefa concluída.)<br /> 101 = Prazo final (a tarefa atingiu o prazo final.)<br /> 102 = Terminado<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>Ele contém o nome do conjunto de tarefas durante a criação do processo.<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>Ele contém o url de resumo de tarefa.<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>É uma lista de controle de acesso para uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>ID de uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>Carimbo de data/hora em que a tarefa foi atualizada pela última vez.<br /> </td>
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
   <td>Se true, as ações de rota estarão visíveis no espaço de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>Se verdadeiro, ações como encaminhar, consultar, compartilhar ficam visíveis no espaço de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>supportOffline<br /> </td>
   <td>T</td>
   <td>Se verdadeiro, o formulário pode ser colocado offline. Isso é somente para formulários pdf.<br /> </td>
  </tr>
  <tr>
   <td>supportSave<br /> </td>
   <td>T</td>
   <td>Se true, o usuário poderá salvar a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>Esse objeto contém opções usadas para enviar formulários pdf pelo leitor, caso o formulário pdf não contenha nenhum botão Enviar.<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>Indica se há uma imagem especificada para processo ou não. Verdadeiro se não houver imagem associada ao processo; caso contrário, falso.<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>Ele contém a lista de tarefas que são usadas na guia Histórico dos detalhes da tarefa.<br /> </td>
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
   <td>Ele contém informações sobre a instância do processo da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>Ela contém matriz de objetos de variáveis de processo, se presentes.<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>Ele contém uma lista de tarefas pendentes para a instância de processo da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>É uma matriz de objetos. Cada objeto contém detalhes sobre a rota e sua mensagem de confirmação correspondente, se presente.<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>É url para os dados do formulário de uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>Essa é a configuração para formulários de aplicativos de terceiros.<br /> </td>
  </tr>
  <tr>
   <td>submetido<br /> </td>
   <td>T</td>
   <td>True se a tarefa for enviada.<br /> </td>
  </tr>
  <tr>
   <td>anexos<br /> </td>
   <td>T</td>
   <td>Lista de anexos para uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>Atribuições<br /> </td>
   <td>T</td>
   <td>Lista de atribuições de uma tarefa.<br /> </td>
  </tr>
 </tbody>
</table>

1. Filtro

   O filtro é basicamente a fila de usuários ou grupos. Quando uma tarefa é atribuída ao usuário/grupo, a tarefa é adicionada na fila correspondente.

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
   <td>True se a fila for uma fila padrão do usuário conectado, caso contrário false.<br type="_moz" /> </td>
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
   <td>Ele contém o tipo da fila.<br /> 0 - Fila do usuário.<br /> 1. Fila compartilhada.<br /> 2. Fila de grupo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>query</td>
   <td>T</td>
   <td>Isso contém uma consulta associada a um filtro. Esta consulta é usada para pesquisar tarefas a partir de uma lista de tarefas completa.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tarefas</td>
   <td>T</td>
   <td>Ele contém uma lista de todas as tarefas que pertencem a um filtro.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Fora do escritório

   Você pode gerenciar seu agendamento de ausência do escritório e controlar o fluxo de tarefas atribuídas a você na sua ausência.

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
   <td>Ele contém objetos de matriz de agendamentos esgotados de um usuário. Em cada objeto de programação, o campo startDate contém a data inicial da programação e o campo endDate contém a data final da programação. Se endDate for nulo na programação, isso significa que o usuário não agendou a data final da programação de ausência do escritório.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>Verdadeiro se não houver um designado principal caso o usuário esteja fora do escritório.<br type="_moz" /> </td>
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
   <td>processSpecificDesigates<br type="_moz" /> </td>
   <td>F</td>
   <td>Ele contém vários objetos para designar fora do escritório específico do processo. Em cada objeto designado específico do processo, processName contém o nome do processo, isNotDesignated será verdadeiro se nenhum usuário for atribuído ao processo correspondente e userDesignated será nulo se nenhum usuário tiver atribuído mais detalhes do usuário atribuído para o processo correspondente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processos<br type="_moz" /> </td>
   <td>T</td>
   <td>Ele contém uma lista de todos os processos que estão disponíveis para o usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Ele contém as configurações iniciais de ausência do escritório do usuário que são buscadas inicialmente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Ele contém configurações remotas do escritório modificadas.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>Ele contém a lista de usuários pesquisados pelo usuário conectado até a data.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Instância do processo

   Uma instância do processo é criada quando um processo é chamado pelo espaço de trabalho ou pelo workbench.

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
   <td>Nome do iniciador de uma instância de processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>ID do iniciador da instância do processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Carimbo de data/hora quando o processo é concluído.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID da instância do processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Iniciado<br /> 1 = Em Execução<br /> 2 = Concluído<br /> 3 = Concluindo<br /> 4 = Terminado<br /> 5 = Terminando<br /> 6 = Suspenso<br /> 7 = Suspensão<br /> 8 = Suspensão<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome do processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Carimbo de data/hora quando o processo foi iniciado.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>Matriz de objetos de variáveis de processo. Cada objeto de variável de processo contém o nome que é a variável de processo, o valor que é o valor da variável de processo e o tipo que é o tipo de variável de processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lista de tarefas<br type="_moz" /> </td>
   <td>T</td>
   <td>Tarefas geradas por esta instância de processo.<br type="_moz" /> </td>
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
   <td>Lista de instâncias de processo para esse processo.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Objeto de Atribuição de Tarefa

   O objeto de atribuição de tarefa contém informações sobre a atribuição de tarefa. A seguir estão as propriedades da atribuição da tarefa.

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
   <td>Carimbo de data/hora quando esta atribuição de uma tarefa é criada.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Atribuição inicial<br /> 1 = Encaminhar (A tarefa foi encaminhada para o proprietário atual da tarefa.)<br /> 2 = Retornado (a tarefa foi retornada ao proprietário atual da tarefa pelo proprietário anterior da tarefa.)<br /> 3 = Solicitado (a tarefa foi reivindicada pelo proprietário atual da tarefa.)<br /> 4 = Escalonamento (a tarefa foi atribuída ao proprietário atual da tarefa após o escalonamento.)<br /> 5 = Administrador Atribuído (a tarefa foi atribuída pelo administrador ao proprietário atual da tarefa.)<br /> 6 = Consultado ( A tarefa foi consultada ao proprietário atual da tarefa.)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Carimbo de data/hora quando esta atribuição de uma tarefa é atualizada.<br type="_moz" /> </td>
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

1. Objeto ACL da tarefa

   O objeto ACL de tarefa contém informações sobre permissões, como encaminhar, compartilhar, consultar etc. de uma tarefa. A seguir estão as propriedades da ACL da tarefa.

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
   <td>Se true, as notas poderão ser adicionadas à tarefa.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>Se true, a tarefa poderá ser reivindicada.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>Se true, a tarefa poderá ser consultada.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>Se true, a tarefa poderá ser encaminhada.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>Se true, a tarefa poderá ser compartilhada.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Anexo da tarefa

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
   <td>Carimbo de data/hora ao criar o anexo.<br type="_moz" /> </td>
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
   <td>Se true, a nota será estendida (longa).<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>permissões<br type="_moz" /> </td>
   <td>F</td>
   <td>Permissões associadas a um anexo. O campo allowRead é para permissão de leitura, allowWrite é para permissão de gravação, allowDelete é para permissão de exclusão.<br type="_moz" /> </td>
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
   <td>Ele contém a data de criação do anexo de acordo com as configurações da interface do usuário do usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>Descrição do anexo formatado. Usado para exibir caracteres especiais presentes na descrição do anexo no espaço de trabalho do AEM Forms.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>Nome do anexo formatado. Usado para exibir caracteres especiais presentes no nome do anexo no espaço de trabalho do AEM Forms. Isso é somente para notas.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Usuário

   A seguir estão as propriedades do objeto do usuário.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente cliente</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>endereço<br type="_moz" /> </td>
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
   <td>directGroupMembership<br type="_moz" /> </td>
   <td>F</td>
   <td>Lista do grupo de usuários.<br type="_moz" /> </td>
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
   <td>Sobrenome do usuário.<br type="_moz" /> </td>
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
   <td>Endereço postal do utilizador.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telefone<br type="_moz" /> </td>
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
