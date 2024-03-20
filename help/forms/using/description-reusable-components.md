---
title: Descrição de componentes reutilizáveis
description: Uma lista completa de componentes reutilizáveis com nomes de arquivo e dependências, para ajudar você a integrar o componente do espaço de trabalho do AEM Forms em suas aplicações Web.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b8cb7233-3d9e-41d4-85c5-8e8c2481f89c
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 9%

---

# Descrição de componentes reutilizáveis {#description-of-reusable-components}

O espaço de trabalho do AEM Forms é composto de [reutilizável](/help/forms/using/integrating-html-ws-components-web.md) componentes organizados em uma [estrutura de pastas](/help/forms/using/folder-structure.md) no CRX™. Cada componente tem modelo, visualização e arquivo de modelo no local especificado na estrutura de pastas, dependências do JavaScript™ em outros arquivos de componente, eventos acompanhados pelo componente e objetos JavaScript que acionam esses eventos no espaço de trabalho do AEM Forms. A lista completa de componentes reutilizáveis com nomes de arquivo e dependências constituintes é fornecida aqui.

## ListaTarefas {#tasklist}

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
     <li><p>Tarefa de equipe</p></li>
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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>filterSelected - modelo de lista de tarefas</p></li>
     <li><p>remover - modelo de lista de tarefas</p></li>
     <li><p>updateQueue - modelo de lista de tarefas</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Esse componente pode ser usado independentemente do espaço de trabalho do AEM Forms, desde que você acione o evento filterSelected para esse componente do aplicativo personalizado.

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
     <li><p>modelo de lista de tarefas</p></li>
     <li><p>utilitário taskactions</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
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
>O Workspace chama a função fetchTasks do modelo TaskList para criar modelos de tarefa para esse componente.

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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>buscado - modelo de lista de tarefas </p></li>
     <li><p>remover - modelo de lista de tarefas </p></li>
     <li><p>updateQueue - modelo de lista de tarefas </p></li>
     <li><p>refreschedQueue - modelo de lista de tarefas </p></li>
     <li><p>filterSelected - modelo de lista de tarefas</p></li>
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
     <li><p>Campo: parentView: exibição em lista de filtros</p> </li>
     <li><p>Campo: parentModel: modelo de lista de tarefas</p> </li>
     <li><p>Campo: utilitário</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos acompanhados</p> </td>
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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>buscado - modelo de lista de tarefas </p></li>
     <li><p>remover - modelo de lista de tarefas </p></li>
     <li><p>updateQueue - modelo de lista de tarefas </p></li>
     <li><p>teamQueuesFetched - modelo de lista de tarefas </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## FiltroEquipe {#teamfilter}

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
     <li><p>Estende : exibição de filtro</p> </li>
     <li><p>Campo : fila :{ name, qid, isDefault, type }</p> </li>
     <li><p>Campo : consulta : cadeia de caracteres</p> </li>
     <li><p>Campo : parentView : modo de exibição de lista de filtros</p> </li>
     <li><p>Campo : parentModel : modelo de lista de tarefas</p> </li>
     <li><p>Campo: utilitário</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos acompanhados</p> </td>
   <td><p>ND</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter obtém o evento indicando qual tarefa foi selecionada do componente Lista de tarefas. Embora esses componentes compartilhem a classe do modelo, não há outra dependência.

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
     <li><p>utilitário notes</p> </li>
     <li><p>utilitário anexos</p> </li>
     <li><p>utilitário taskactions</p> </li>
     <li><p>utilitário de histórico</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p> </td>
   <td>
    <ul>
     <li><p>encaminhado - modelo de tarefa</p> </li>
     <li><p>compartilhado - modelo de tarefa</p> </li>
     <li><p>consultado - modelo de tarefa</p> </li>
     <li><p>rejeitado - modelo de tarefa</p> </li>
     <li><p>abandonado - modelo de tarefa</p> </li>
     <li><p>desbloqueado - modelo de tarefa</p> </li>
     <li><p>bloqueado - modelo de tarefa</p> </li>
     <li><p>solicitado - modelo de tarefa</p> </li>
     <li><p>alterar:taskseleted - modelo de lista de tarefas</p> </li>
     <li><p>alteração:formUrl - modelo de tarefa</p> </li>
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
   <td><p>startprocess.html (na pasta rota)</p></td>
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
     <li><p>modelo allcategoryfatory</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetched - modelo de lista de categorias </p></li>
     <li><p>adicionar - modelo de categorylist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Este componente usa classes de modelo de alguns outros componentes, como StartPointList, StartPoint e Task. Além dessa dependência, CategoryList pode ser usado independentemente.

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
     <li><p>modelo startpointlist</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>alterado - modelo de categoria </p></li>
     <li><p>childrenFetched - modelo de categoria </p></li>
     <li><p>categoria:selecionada - modelo de lista de categorias </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## ListaDePontosIniciais {#startpointlist}

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
   <td><p>startprocess.html (na pasta rota)</p></td>
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
     <li><p>modelo allcategoryfatory</p></li>
     <li><p>exibição de ponto inicial</p></li>
     <li><p>modelo startpointlist</p></li>
     <li><p>modelo de ponto inicial</p></li>
     <li><p>modelo de tarefa</p></li>
     <li><p>modelo de tarefa</p></li>
     <li><p>modelo de lista de tarefas</p></li>
     <li><p>modelo teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>categoria:selecionada - modelo de lista de categorias </p></li>
     <li><p>allStartpointsFetched - modelo de lista de categorias </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os componentes StartPointList e CategoryList compartilham a classe do modelo, portanto, o primeiro depende do segundo. CategoryList acessa as informações sobre quais pontos iniciais da categoria são mostrados. Para usar StartPointList de forma independente, simule o acionador de evento de CategoryList.

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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td><p>alteração - modelo de ponto inicial </p></td>
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
     <li><p>modelo allcategoryfatory</p> </li>
     <li><p>utilitário formrendering</p> </li>
     <li><p>utilitário notes</p> </li>
     <li><p>utilitário anexos</p> </li>
     <li><p>utilitário taskactions</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p> </td>
   <td>
    <ul>
     <li><p>categoria:selecionada - modelo de lista de categorias</p> </li>
     <li><p>alteração:invokedTask - modelo startpointlist</p> </li>
     <li><p>alteração:formUrl - modelo de tarefa</p> </li>
     <li><p>ponto inicial:selecionado - modelo de lista de pontos inicial</p> </li>
     <li><p>encaminhado - modelo de tarefa</p> </li>
     <li><p>abandonado - modelo de tarefa</p> </li>
     <li><p>desbloqueado - modelo de tarefa</p> </li>
     <li><p>bloqueado - modelo de tarefa</p> </li>
     <li>attachmentURLFetched - modelo de tarefa</li>
     <li>newAttachment - modelo de tarefa</li>
     <li>prepareForSubmitComplete - modelo de tarefa </li>
     <li><p>submitComplete - modelo de tarefa</p> </li>
     <li><p>allStartpointsFetched - modelo de lista de categorias</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os componentes StartProcess e StartPointList compartilham a classe do modelo. Este componente se torna relevante quando você seleciona um ponto inicial em StartPointList.

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
   <td><p>tracking.html (na pasta da rota)</p></td>
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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>adicionar - modelo processnamelist </p></li>
     <li><p>buscado:processnames - modelo processnamelist </p></li>
     <li><p>alteração - modelo processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList não depende de outros componentes. No entanto, internamente depende da classe de modelo ProcessInstanceList que, por sua vez, depende de outros componentes. Portanto, ProcessNameList usa muitas classes de modelo como ProcessInstanceList, ProcessInstance, TaskList, Teamtask e Task. Além dessas dependências, ProcessNameList pode ser usado independentemente.

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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td><p>alteração - modelo de processname </p></td>
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
   <td><p>tracking.html (na pasta da rota)</p></td>
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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>processname:selecionado - modelo processnamelist </p></li>
     <li><p>processname:instancesfetched - modelo processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList espera um evento de ProcessNameList indicando o nome do processo para buscar e exibir instâncias. Para usar ProcessInstanceList de maneira independente, simule o acionador de evento separadamente.

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>Modelo</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>Exibir</p></td>
   <td><p>processname dentro de processnamelist.js</p></td>
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
   <td><p>modelo de lista de tarefas</p></td>
  </tr>
  <tr>
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td><p>alteração - modelo de instância de processo </p></td>
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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>processname:selecionado - modelo processnamelist </p></li>
     <li><p>processinstance:seleted - modelo processinstancelist </p></li>
     <li><p>tasksFetched - modelo de instância de processo </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory espera um evento de ProcessInstanceList indicando qual histórico de instância de processo deve ser mostrado. Além dessa dependência, o componente pode ser usado de forma independente.

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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched - modelo do outooffice</p> </li>
     <li><p>outOfOfficeSettingsSaved - modelo do outooffice</p> </li>
     <li><p>processesFetched - modelo do outooffice</p> </li>
     <li><p>principalSelected - exibição de pesquisa principal</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O OutOfOffice pode ser usado independentemente.

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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - modelo sharequeue</p> </li>
     <li><p>queueAccessRequested - modelo sharequeue</p> </li>
     <li><p>grantedUsersFetched - modelo sharequeue</p> </li>
     <li>accessibleUsersFetched - modelo de fila compartilhada</li>
     <li><p>queueAccessRevoked - modelo sharequeue</p> </li>
     <li><p>queueAccessRemoved - modelo sharequeue</p> </li>
     <li><p>principalSelected - exibição de pesquisa principal</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue pode ser usado independentemente.

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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>preferênciasBuscado - modelo uisettings </p></li>
     <li><p>settingUpdated - modelo uisettings </p></li>
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
   <td><p>Eventos acompanhados</p></td>
   <td><p>ND</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O AppNavigation pode ser usado de maneira independente.

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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched - modelo de informações do usuário</li>
     <li>sessionReneved - modelo de informações do usuário <br /> </li>
     <li>sessionExpired - modelo de informações do usuário </li>
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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p></td>
   <td><p>newWsError - modelo wserror </p></td>
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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p> </td>
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
   <td><p>searchtemplate (em searchtemplatelist.js) </p> </td>
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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p> </td>
   <td><p>templateFetched- modelo de pesquisa</p> </td>
  </tr>
 </tbody>
</table>

## ListaDeModelosDePesquisa {#searchtemplatelist}

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
   <td><p>tracking.html (na pasta da rota)</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependências JS</p> </td>
   <td><p>modelo de searchtemplate</p> </td>
  </tr>
  <tr>
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p> </td>
   <td><p>alterar - modelo searchtemplatelist</p> </td>
  </tr>
 </tbody>
</table>

## DetalhesModeloPesquisa {#searchtemplatedetails}

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
   <td><p>Eventos acompanhados (Nome do evento - Acionador)</p> </td>
   <td><p>searchTemplate:seleted - modelo de searchtemplate</p> </td>
  </tr>
 </tbody>
</table>
