---
title: Descrição dos componentes reutilizáveis
seo-title: Descrição dos componentes reutilizáveis
description: Uma lista completa de componentes reutilizáveis com nomes de arquivos e dependências, para ajudá-lo a integrar o componente de espaço de trabalho do AEM Forms em seus aplicativos da Web.
seo-description: Uma lista completa de componentes reutilizáveis com nomes de arquivos e dependências, para ajudá-lo a integrar o componente de espaço de trabalho do AEM Forms em seus aplicativos da Web.
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Descrição dos componentes reutilizáveis {#description-of-reusable-components}

A área de trabalho do AEM Forms é composta de componentes [reutilizáveis](/help/forms/using/integrating-html-ws-components-web.md) que são organizados em uma estrutura [de](/help/forms/using/folder-structure.md) pasta específica no CRX™. Cada componente tem um modelo, uma visualização e um arquivo de modelo no local especificado na estrutura da pasta, as dependências JavaScript™ em outros arquivos de componente, eventos ouvidos pelos objetos do componente e JavaScript que acionam esses eventos na área de trabalho do AEM Forms. A lista completa de componentes reutilizáveis com nomes de arquivos e dependências constituintes é fornecida aqui.

## TaskList {#tasklist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>tasklist.html</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td>
    <ul>
     <li><p>UserSearch</p></li>
     <li><p>Tarefa</p></li>
     <li><p>Equipe</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td>
    <ul>
     <li><p>modelo de tarefa</p></li>
     <li><p>modelo teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>filterSeleted - modelo de lista de tarefas</p></li>
     <li><p>remover - modelo da lista de tarefas</p></li>
     <li><p>updateQueue - modelo da lista de tarefas</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Este componente pode ser usado independentemente da área de trabalho do AEM Forms, desde que você dispare o filterevento selecionado para este componente do seu aplicativo personalizado.

## Tarefa {#task}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>task.html</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td>
    <ul>
     <li><p>modelo da lista de tarefas</p></li>
     <li><p>utilitário taskactions</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>submitComplete - modelo de tarefa</p></li>
     <li><p>Rejeitar - modelo de tarefa</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>A Workspace chama a função fetchTasks do modelo TaskList para criar modelos de Tarefa para este componente.

## FilterList {#filterlist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>filterlist.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>filterlist.html</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>buscado - modelo da lista de tarefas </p></li>
     <li><p>remover - modelo da lista de tarefas </p></li>
     <li><p>updateQueue - modelo da lista de tarefas </p></li>
     <li><p>updateQueue - modelo da lista de tarefas </p></li>
     <li><p>filterSeleted - modelo de lista de tarefas</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## Filtro {#filter}

<table>
 <tbody>
  <tr>
   <td><p>Exibir</p> </td>
   <td><p>filter.js</p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>filter.html</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependências JS</p> </td>
   <td>
    <ul>
     <li><p>Campo: fila: { name, qid, isDefault, type}</p> </li>
     <li><p>Campo: query: string</p> </li>
     <li><p>Campo: parentView: visualização filterlist</p> </li>
     <li><p>Campo: parentModel: modelo da lista de tarefas</p> </li>
     <li><p>Campo: utilidade</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos</p> </td>
   <td><p>ND</p> </td>
  </tr>
 </tbody>
</table>

## TeamQueues {#teamqueues}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>teamqueues.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>teamqueues.html</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>buscado - modelo da lista de tarefas </p></li>
     <li><p>remover - modelo da lista de tarefas </p></li>
     <li><p>updateQueue - modelo da lista de tarefas </p></li>
     <li><p>TeamQueuesFetched - modelo da lista de tarefas </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## TeamFilter {#teamfilter}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Exibir</p> </td>
   <td><p>teamfilter.js</p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>teamfilter.html</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependências JS</p> </td>
   <td>
    <ul>
     <li><p>Estende : visualização do filtro</p> </li>
     <li><p>Campo : fila :{ nome, qid, isDefault, tipo }</p> </li>
     <li><p>Campo : query : string</p> </li>
     <li><p>Campo : parentView : visualização filterlist</p> </li>
     <li><p>Campo : parentModel : modelo da lista de tarefas</p> </li>
     <li><p>Campo : utilidade</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos</p> </td>
   <td><p>ND</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter obtém o evento indicando qual tarefa foi selecionada do componente TaskList. Embora esses componentes compartilhem a classe model, não há outra dependência.

## DetalhesDaTarefa {#taskdetails}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>tasklist.js</p> </td>
  </tr>
  <tr>
   <td><p>Exibir</p> </td>
   <td><p>taskdetails.js</p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>taskdetails.html</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td><p>A maioria das classes Utility</p> </td>
  </tr>
  <tr>
   <td><p>Dependências JS</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>utilitário formrendering</p> </li>
     <li><p>utilitário Notes</p> </li>
     <li><p>utilitário de anexos</p> </li>
     <li><p>utilitário taskactions</p> </li>
     <li><p>utilitário de histórico</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p> </td>
   <td>
    <ul>
     <li><p>encaminhado - modelo de tarefa</p> </li>
     <li><p>compartilhado - modelo de tarefa</p> </li>
     <li><p>consultado - modelo de tarefa</p> </li>
     <li><p>rejeitado - modelo de tarefa</p> </li>
     <li><p>abandonado - modelo de tarefa</p> </li>
     <li><p>desbloqueado - modelo de tarefa</p> </li>
     <li><p>bloqueado - modelo de tarefa</p> </li>
     <li><p>reivindicado - modelo de tarefa</p> </li>
     <li><p>alteração:tarefa selecionada - modelo de lista de tarefas</p> </li>
     <li><p>change:formUrl - modelo de tarefa</p> </li>
     <li>attachmentURLFetched - modelo de tarefa</li>
    </ul>
    <ul>
     <li>newAttachment - modelo de tarefa</li>
     <li><p>taskHistoryFetched - modelo de tarefa</p> </li>
     <li>prepareForSubmitComplete - modelo de tarefa</li>
     <li><p>submitComplete - modelo de tarefa</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## CategoryList {#categorylist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>startprocess.html (na pasta route)</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>Categoria</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td>
    <ul>
     <li><p>modelo favoritecategoryfatory</p></li>
     <li><p>modelo de fábrica flexível</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetched - modelo de categorylist </p></li>
     <li><p>adicionar - modelo de lista de categorias </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Este componente usa classes de modelo de alguns outros componentes, como StartPointList, StartPoint e Tarefa. Além dessa dependência, CategoryList pode ser usada independentemente.

## Categoria {#category}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>category.html</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td>
    <ul>
     <li><p>modelo categorylist</p></li>
     <li><p>modelo startpoint</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>alterado - modelo de categoria </p></li>
     <li><p>childFetched - modelo de categoria </p></li>
     <li><p>categoria:selecionado - modelo de lista de categorias </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## StartPointList {#startpointlist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>startpointlist.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>startprocess.html (na pasta route)</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td>
    <ul>
     <li><p>modelo de categoria</p></li>
     <li><p>modelo favoritecategoryfatory</p></li>
     <li><p>modelo de fábrica flexível</p></li>
     <li><p>visualização do ponto de partida</p></li>
     <li><p>modelo startpoint</p></li>
     <li><p>modelo de ponto de partida</p></li>
     <li><p>modelo de tarefa</p></li>
     <li><p>modelo de tarefa</p></li>
     <li><p>modelo da lista de tarefas</p></li>
     <li><p>modelo teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>categoria:selecionado - modelo de lista de categorias </p></li>
     <li><p>allStartpointsFetched - modelo de categorylist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os componentes StartPointList e CategoryList compartilham a classe modelo, portanto, a primeira depende da última. CategoryList acessa as informações sobre quais pontos de start são mostrados. Para usar StartPointList independentemente, simule o acionador do evento de CategoryList.

## StartPoint {#startpoint}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>startpoint.html</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td><p>modelo de tarefa</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td><p>change - Modelo de ponto de partida </p></td>
  </tr>
 </tbody>
</table>

## StartProcess {#startprocess}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>categorylist.js</p> </td>
  </tr>
  <tr>
   <td><p>Exibir</p> </td>
   <td><p>startprocess.js</p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>startprocess.html</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td>
    <ul>
     <li><p>A maioria das classes Utility</p> </li>
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Dependências JS</p> </td>
   <td>
    <ul>
     <li><p>modelo de categoria</p> </li>
     <li><p>modelo favoritecategoryfatory</p> </li>
     <li><p>modelo de fábrica flexível</p> </li>
     <li><p>utilitário formrendering</p> </li>
     <li><p>utilitário Notes</p> </li>
     <li><p>utilitário de anexos</p> </li>
     <li><p>utilitário taskactions</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p> </td>
   <td>
    <ul>
     <li><p>categoria:selecionado - modelo de lista de categorias</p> </li>
     <li><p>change:namedTask - modelo startpoint</p> </li>
     <li><p>change:formUrl - modelo de tarefa</p> </li>
     <li><p>ponto de partida:selecionado - modelo de lista de pontos de partida</p> </li>
     <li><p>encaminhado - modelo de tarefa</p> </li>
     <li><p>abandonado - modelo de tarefa</p> </li>
     <li><p>desbloqueado - modelo de tarefa</p> </li>
     <li><p>bloqueado - modelo de tarefa</p> </li>
     <li>attachmentURLFetched - modelo de tarefa</li>
     <li>newAttachment - modelo de tarefa</li>
     <li>prepareForSubmitComplete - modelo de tarefa </li>
     <li><p>submitComplete - modelo de tarefa</p> </li>
     <li><p>allStartpointsFetched - modelo de categorylist</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os componentes StartProcess e StartPointList compartilham a classe model. Esse componente se torna relevante quando você seleciona um ponto de partida de StartPointList.

## ProcessNameList {#processnamelist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>tracking.html (na pasta route)</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td><p>modelo processname</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>add - modelo processnamelist </p></li>
     <li><p>buscado:processnames - processnamelist model </p></li>
     <li><p>change - modelo processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList não depende de outros componentes. No entanto, internamente depende da classe de modelo ProcessInstanceList que, por sua vez, depende de outros componentes. Portanto, ProcessNameList usa muitas classes de modelo, como ProcessInstanceList, ProcessInstance, TaskList, Teamtask e Tarefa. Além dessas dependências, ProcessNameList pode ser usado independentemente.

## ProcessName {#processname}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>processname (em processnamelist.js)</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processname.html</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td><p>modelo processinstancelist</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td><p>change - modelo processname </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceList {#processinstancelist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>processinstancelist.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>tracking.html (na pasta route)</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td><p>modelo processname</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>nome do processo:selecionado - modelo processnamelist </p></li>
     <li><p>processname:instancesfetched - modelo processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList espera um evento de ProcessNameList indicando o nome do processo para buscar e exibir instâncias. Para usar ProcessInstanceList independentemente, simule o acionador do evento separadamente.

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>processname inside processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processinstance.html</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td><p>modelo da lista de tarefas</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td><p>change - modelo de instância de processamento </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceHistory {#processinstancehistory}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>processinstancehistory.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processinstancehistory.html</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td>
    <ul>
     <li><p>modelo processname</p></li>
     <li><p>utilitário de histórico</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>nome do processo:selecionado - modelo processnamelist </p></li>
     <li><p>processinstance:seleted - processinstancelist model </p></li>
     <li><p>TasksFetched - processinstance model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory espera um evento de ProcessInstanceList que indica qual histórico de instância de processo deve ser exibido. Além dessa dependência, o componente pode ser usado de forma independente.

## Fora do escritório {#outofoffice}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>Exibir</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>outofoffice.html</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>Dependências JS</p> </td>
   <td><p>visualização usersearch</p> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched - modelo do outOfOffice</p> </li>
     <li><p>outOfOfficeSettingsSaved - modelo do outOfOffice</p> </li>
     <li><p>processFetched - modelo externo</p> </li>
     <li><p>principalSeleted - visualização de pesquisa principal</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O OutOffice pode ser usado independentemente.

## ShareQueue {#sharequeue}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>Exibir</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>sharequeue.html</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>Dependências JS</p> </td>
   <td><p>visualização usersearch</p> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - modelo de compartilhamento</p> </li>
     <li><p>queueAccessRequested - modelo de compartilhamento</p> </li>
     <li><p>providedUsersFetched - modelo de compartilhamento</p> </li>
     <li>accessUsersFetched - modelo de compartilhamento</li>
     <li><p>queueAccessRevewed - modelo de compartilhamento</p> </li>
     <li><p>queueAccessRemoved - modelo de compartilhamento</p> </li>
     <li><p>principalSeleted - visualização de pesquisa principal</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O ShareQueue pode ser usado independentemente.

## UISettings {#uisettings}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>uisettings.html</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>preferencesFetched - modelo de configurações de usuário </p></li>
     <li><p>settingUpdates - Modelo de configurações </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings podem ser usados independentemente.

## AppNavigation {#appnavigation}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>appnavigation.html</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos</p></td>
   <td><p>ND</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O AppNavigation pode ser usado independentemente.

## UserInfo {#userinfo}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>Exibir</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>userinfo.html</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependências JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched - modelo userinfo</li>
     <li>sessionRenewed - modelo userinfo <br /> </li>
     <li>sessionExpired - modelo userinfo </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo pode ser usado independentemente.

## WSError {#wserror}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>wserror.html</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p></td>
   <td><p>newWsError - modelo de erro </p></td>
  </tr>
 </tbody>
</table>

## UserSearch {#usersearch}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>Exibir</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>usersearch.html</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependências JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p> </td>
   <td>
    <ul>
     <li>principalSearched - modelo de pesquisa principal</li>
     <li>outOfOfficeInfoFetched - modelo de pesquisa de usuário</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SearchTemplate {#searchtemplate}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>searchtemplate.js</p> </td>
  </tr>
  <tr>
   <td><p>Exibir</p> </td>
   <td><p>search template (em search templatelist.js) </p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>searchtemplate.html</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependências JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p> </td>
   <td><p>templateFetched- modelo search</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateList {#searchtemplatelist}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Exibir</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>tracking.html (na pasta route)</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependências JS</p> </td>
   <td><p>modelo de pesquisa</p> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p> </td>
   <td><p>change - Modelo searchTemplatelist</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateDetails {#searchtemplatedetails}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Exibir</p> </td>
   <td><p>searchtemplatedetails.js</p> </td>
  </tr>
  <tr>
   <td><p>Modelo</p> </td>
   <td><p>searchtemplatedetails.html</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependências JS</p> </td>
   <td>ND<br /> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (nome do Evento - Acionador)</p> </td>
   <td><p>searchTemplate:seleted - modelo de pesquisa</p> </td>
  </tr>
 </tbody>
</table>
