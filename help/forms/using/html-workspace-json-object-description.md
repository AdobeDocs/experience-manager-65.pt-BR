---
title: Descrição do objeto JSON do espaço de trabalho do AEM Forms
description: Informações conceituais sobre os objetos JSON JavaScript usados no espaço de trabalho do LiveCycle AEM Forms para personalização, extensão, modificação e reutilização.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: f837a2b3-4650-4261-84c6-291bb2a46dc7
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2113'
ht-degree: 2%

---

# Descrição do objeto JSON do espaço de trabalho do AEM Forms {#aem-forms-workspace-json-object-description}

Os objetos JSON usados no espaço de trabalho do AEM Forms são descritos abaixo.

1. Categoria

   As categorias estão presentes na guia iniciar processo do espaço de trabalho. Essas categorias são usadas para classificar os pontos de partida.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente Cliente</strong></td>
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
   <td>Contém a lista de todos os pontos de partida presentes em uma categoria</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>Contém a lista de categorias filho diretas de uma categoria<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Todos os pontos iniciais e favoritos são categorias definidas no lado do cliente. A categoria Favorito contém todos os pontos iniciais marcados pelo usuário como favoritos. A categoria Todos os pontos iniciais contém todos os pontos iniciais.

1. Ponto inicial

   O ponto inicial é usado para iniciar um processo no espaço de trabalho quando chamado.

   | **Propriedade** | **Somente Cliente** | **Comentários** |
   |---|---|---|
   | categoryId | F | Ele contém a ID da categoria à qual o ponto inicial pertence. |
   | descrição | F | Contém a descrição de um ponto inicial. |
   | name | F | Contém o nome do ponto inicial. |
   | serializedImageTicket | F | Ele contém um tíquete de imagem correspondente ao ponto inicial. Este tíquete de imagem é usado no campo imageUrl do ponto inicial, para obter a imagem do ponto inicial do servidor. |
   | serviceName | F | Ele contém o nome do serviço para o ponto inicial. |
   | startpointId | F | Ele contém a ID do ponto inicial. |
   | isFavorite | T | Indica se o ponto inicial é favorito ou não. Verdadeiro se o ponto inicial for favorito ou falso. |
   | isDefaultImage | T | Indica se há uma imagem especificada para o processo ou não. Verdadeiro se não houver imagem associada ao processo; caso contrário, é falso. |
   | tarefa | T | Ela contém tarefas criadas quando o ponto inicial é chamado. |
   | imageUrl | T | Ele contém o url da imagem correspondente ao ponto inicial. |

1. Tarefa

   As tarefas são atribuídas a usuários/grupos e incluem uma interface de usuário — um formulário ou um Guia (obsoleto) — que pode ser preenchida com dados. Quando uma tarefa é atribuída a um usuário, ele recebe o formulário ou Guia para preencher e enviar.

<table>
 <tbody>
  <tr>
   <td>Propriedade<br /> </td>
   <td>Somente Cliente<br /> </td>
   <td>Comentários<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>A classe de tarefa é 'LC8' quando a tarefa é lc8 e não 'Standard'.<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>Ele contém o carimbo de data e hora de conclusão da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>Ela contém a ID de um grupo para o qual a tarefa pode ser consultada. Ele é definido durante o design do processo.<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>Ela contém o carimbo de data e hora de criação da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
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
   <td>Ela contém o carimbo de data e hora que quando uma tarefa atingirá seu prazo final.<br /> </td>
  </tr>
  <tr>
   <td>descrição<br /> </td>
   <td>F</td>
   <td>Contém a descrição da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>Ele contém o nome de exibição da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>Ela contém a ID de um grupo para o qual a tarefa pode ser encaminhada. Ele é definido durante o design do processo.<br /> </td>
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
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>Verdadeiro se o formulário de tarefa deve ser aberto para concluir a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>Se verdadeiro, ao abrir a tarefa, o formulário ocupa tela completa na primeira vez.<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>Se verdadeiro, a rota deve ser selecionada para concluir a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>Os anexos serão exibidos se for verdadeiro.<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>Se verdadeiro, a tarefa é criada a partir do ponto inicial.<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>True se a tarefa estiver visível no espaço de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>F</td>
   <td>Carimbo de data/hora para o próximo lembrete.<br /> </td>
  </tr>
  <tr>
   <td>prioridade<br /> </td>
   <td>F</td>
   <td>Ela contém a prioridade da tarefa.<br /> 1 = Maior prioridade<br /> 2 = Alta Prioridade<br /> 3 = Prioridade normal<br /> 4 = Prioridade baixa<br /> 5 = Prioridade Mais Baixa<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>Id da instância do processo da qual a tarefa faz parte.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>Status da instância do processo da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>reminderCount<br /> </td>
   <td>F</td>
   <td>Contém a contagem de lembretes para a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>Ela contém a lista de rotas associadas à tarefa. O usuário pode concluir a tarefa selecionando qualquer um dos roteiros na lista de roteiros.<br /> </td>
  </tr>
  <tr>
   <td>seletedRoute<br /> </td>
   <td>F</td>
   <td>Contém o nome da rota selecionada quando a tarefa foi concluída.<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>Ele contém um tíquete de imagem correspondente à tarefa. Este tíquete de imagem é usado no campo imageUrl da tarefa, para obter imagem para tarefa do servidor.<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>Ele contém o nome do serviço da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>Ela contém o título do serviço da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>status<br /> </td>
   <td>F</td>
   <td>1 = Criada (a tarefa é criada a partir do ponto inicial.)<br /> 2 = Criada e salva (a tarefa é criada a partir do ponto inicial e salva).<br /> 3 = Atribuída (a tarefa é atribuída ao usuário após o início do processo.)<br /> 4 = Atribuído e Salvo (a tarefa é atribuída e salva.)<br /> 100 = Concluído (a tarefa está concluída.)<br /> 101 = Prazo final (a tarefa atingiu o prazo final).<br /> 102 = Encerrado<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>Ele contém o nome do conjunto de tarefas durante o design do processo.<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>Ele contém o URL de resumo da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>É uma lista de controle de acesso para uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>Id de uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>Carimbo de data/hora da última atualização da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>Ele contém a URL do formulário de uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>Ele contém o tipo de formulário de tarefa. Usando esse campo, a tarefa é renderizada no cliente como pdf para, formulário swf e assim por diante.<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>Se verdadeiro, as ações de roteiro são visíveis no espaço de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>Se true, ações como encaminhar, consultar, compartilhar estarão visíveis no espaço de trabalho.<br /> </td>
  </tr>
  <tr>
   <td>supportedOffline<br /> </td>
   <td>T</td>
   <td>Se verdadeiro, o formulário pode ser usado offline. Isso é somente para formulários pdf.<br /> </td>
  </tr>
  <tr>
   <td>supportedSave<br /> </td>
   <td>T</td>
   <td>Se verdadeiro, o usuário pode salvar a tarefa.<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>Esse objeto contém opções que são usadas para enviar formulários pdf por meio do reader quando o formulário pdf não contém um botão de envio.<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>Indica se há uma imagem especificada para o processo ou não. Verdadeiro se não houver imagem associada ao processo; caso contrário, é falso.<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>Ele contém a lista de tarefas que são usadas na guia histórico de detalhes da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>Verdadeiro se o usuário conectado for o proprietário da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>Ele contém todas as ações que podem ser executadas na tarefa.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>Ele contém todas as ações de roteiro disponíveis para uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>Ela contém comandos como forward, share e consult, se disponíveis para uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>Ele contém comandos como bloquear, desbloquear, abandonar, retornar, reivindicar e assim por diante, conforme disponível.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>Ela contém informações sobre a instância do processo da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>Ela contém a matriz de objetos de variáveis de processo, se presentes.<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>Ela contém uma lista de tarefas pendentes para a instância do processo da tarefa.<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>É uma matriz de objetos. Cada objeto contém detalhes sobre a rota e sua mensagem de confirmação correspondente, se presente.<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>É o URL para os dados do formulário de uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>Essa é a configuração para formulários de aplicativos de terceiros.<br /> </td>
  </tr>
  <tr>
   <td>enviado<br /> </td>
   <td>T</td>
   <td>Verdadeiro se a tarefa for enviada.<br /> </td>
  </tr>
  <tr>
   <td>anexos<br /> </td>
   <td>T</td>
   <td>Lista de anexos de uma tarefa.<br /> </td>
  </tr>
  <tr>
   <td>Atribuições<br /> </td>
   <td>T</td>
   <td>Lista de atribuições de uma tarefa.<br /> </td>
  </tr>
 </tbody>
</table>

1. Filtro

   O filtro é basicamente uma fila de usuário ou grupo. Quando uma tarefa é atribuída a um usuário/grupo, ela é adicionada à fila correspondente.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente Cliente</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>True se a fila for a fila padrão do usuário conectado, caso contrário false.<br type="_moz" /> </td>
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
   <td>Ele contém query associada a um filtro. Esta consulta é usada para pesquisar tarefas a partir da lista de tarefas completa.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tarefas</td>
   <td>T</td>
   <td>Ele contém uma lista de todas as tarefas que pertencem a um filtro.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Fora do escritório

   Você pode gerenciar sua programação de ausência temporária e controlar o fluxo de tarefas atribuídas a você em sua ausência.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong><br type="_moz" /> </td>
   <td><strong>Somente Cliente</strong><br type="_moz" /> </td>
   <td><strong>Comentários</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRanges<br type="_moz" /> </td>
   <td>F</td>
   <td>Ele contém objetos de matriz de agendamentos de um usuário fora do escritório. Em cada objeto de agendamento, o campo startDate contém a data inicial do agendamento e o campo endDate contém a data final do agendamento. Se endDate for nulo na programação, isso implica que o usuário não programou a data final da programação fora do escritório.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>Verdadeiro se não houver um representante principal no caso de o usuário estar ausente do escritório.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>Verdadeiro se o usuário estiver ausente do escritório.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>Ele contém detalhes do usuário que é atribuído como designado principal pelo usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>F</td>
   <td>Ele contém uma matriz de objetos para designados fora do escritório específicos do processo. Em cada objeto designado específico do processo, processName contém o nome do processo, isNotDesignated é verdadeiro se nenhum usuário for atribuído ao processo correspondente e userDesignated é nulo se nenhum usuário tiver atribuído outros detalhes do usuário para o processo correspondente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processos<br type="_moz" /> </td>
   <td>T</td>
   <td>Ela contém uma lista de todos os processos que estão disponíveis para o usuário.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Ele contém as configurações iniciais fora do escritório do usuário, que são buscadas inicialmente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Ele contém configurações fora do escritório modificadas.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>Ele contém a lista de usuários que são pesquisados pelo usuário conectado até a data de hoje.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Instância do processo

   Uma instância de processo é criada quando um processo é chamado por meio de um espaço de trabalho ou bancada.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente Cliente</strong></td>
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
   <td>0 = Iniciado<br /> 1 = Em execução<br /> 2 = Concluído<br /> 3 = Concluindo<br /> 4 = Terminado<br /> 5 = Encerrando<br /> 6 = Suspenso<br /> 7 = Suspensão<br /> 8 = Cancelando Suspensão<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome do processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Carimbo de data/hora de início do processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>Matriz de objetos de variáveis de processo. Cada objeto de variável de processo contém um nome que é o nome da variável de processo, um valor que é o valor da variável de processo e um tipo que é o tipo da variável de processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lista de tarefas<br type="_moz" /> </td>
   <td>T</td>
   <td>Tarefas geradas por essa instância do processo.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Nome do processo

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente Cliente</strong></td>
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
   <td>Lista de instâncias deste processo.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Objeto de Atribuição de Tarefa

   O objeto de atribuição da tarefa contém informações sobre a atribuição da tarefa. A seguir estão as propriedades da atribuição da tarefa.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente Cliente</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>assignmentCreateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Carimbo de data/hora quando esta atribuição de uma tarefa é criada.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Atribuição inicial<br /> 1 = Encaminhar (a tarefa foi encaminhada ao proprietário atual da tarefa.)<br /> 2 = Retornado (a tarefa foi retornada ao proprietário atual da tarefa pelo proprietário anterior da tarefa).<br /> 3 = Reclamado (a tarefa foi reclamada pelo proprietário atual da tarefa.)<br /> 4 = Escalação (a tarefa foi atribuída ao proprietário atual da tarefa após a escalação.)<br /> 5 = Administrador atribuído (a tarefa foi atribuída pelo administrador ao proprietário atual da tarefa.)<br /> 6 = Consultado ( a tarefa foi consultada para o proprietário atual da tarefa.)<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
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

1. Objeto ACL de Tarefa

   O objeto de ACL da tarefa contém informações sobre permissões como encaminhamento, compartilhamento, consulta e assim por diante de uma tarefa. A seguir estão as propriedades da ACL da tarefa.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente Cliente</strong></td>
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
   <td>Se verdadeiro, as observações podem ser adicionadas à tarefa.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>Se verdadeiro, a tarefa pode ser solicitada.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>Se verdadeiro, a tarefa pode ser consultada.<br type="_moz" /> </td>
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

1. Anexo da tarefa

   Os anexos podem ser adicionados a uma tarefa. O anexo pode ser do tipo anexo e nota. A seguir estão as propriedades do objeto de anexo.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Somente Cliente</strong></td>
   <td><strong>Comentários</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>F</td>
   <td>Carimbo de data/hora quando o anexo foi criado.<br type="_moz" /> </td>
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
   <td>Carimbo de data/hora da última modificação do anexo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>Se verdadeiro, a nota será uma nota estendida (longa).<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>permissões<br type="_moz" /> </td>
   <td>F</td>
   <td>Permissões associadas a um anexo. O campo allowRead é para permissão de leitura, allowWrite é para permissão de gravação, allowDelete é para permissão de exclusão.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tamanho<br type="_moz" /> </td>
   <td>F</td>
   <td>Tamanho do anexo em bytes.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID da tarefa à qual o anexo foi adicionado.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tipo<br type="_moz" /> </td>
   <td>F</td>
   <td>Tipo é o anexo para arquivos e Tipo é uma observação para notas.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>Ele contém a data de criação do anexo de acordo com as configurações da interface do usuário.<br type="_moz" /> </td>
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
   <td><strong>Somente Cliente</strong></td>
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
   <td>Verdadeiro se o usuário estiver ausente do escritório.<br type="_moz" /> </td>
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
   <td>Endereço postal do usuário.<br type="_moz" /> </td>
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
