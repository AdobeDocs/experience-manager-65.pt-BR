---
title: Descrição dos componentes reutilizáveis
seo-title: Description of reusable components
description: Uma lista completa de componentes reutilizáveis com nomes de arquivo e dependências, para ajudar a integrar o componente do espaço de trabalho do AEM Forms em seus aplicativos da Web.
seo-description: A complete list of reusable components with filenames and dependencies, to help you integrate AEM Forms workspace component in your web applications.
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
exl-id: b8cb7233-3d9e-41d4-85c5-8e8c2481f89c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 9%

---

# Descrição dos componentes reutilizáveis {#description-of-reusable-components}

O espaço de trabalho do AEM Forms é composto por [reutilizável](/help/forms/using/integrating-html-ws-components-web.md) componentes organizados em um [estrutura de pastas](/help/forms/using/folder-structure.md) no CRX™. Cada componente tem modelo, visualização e arquivo de modelo no local especificado na estrutura da pasta, o JavaScript™ depende de outros arquivos de componente, eventos ouvidos pelo componente e objetos JavaScript que acionam esses eventos no espaço de trabalho do AEM Forms. A lista completa de componentes reutilizáveis com nomes de arquivo e dependências constituintes é fornecida aqui.

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
   <td><p>Dependências de JS</p></td>
   <td>
    <ul>
     <li><p>modelo de tarefa</p></li>
     <li><p>modelo de tarefa de equipe</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
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
>Esse componente pode ser usado independentemente do espaço de trabalho do AEM Forms, desde que você acione o evento filterSeleted para esse componente do seu aplicativo personalizado.

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
   <td><p>Dependências de JS</p></td>
   <td>
    <ul>
     <li><p>modelo da lista de tarefas</p></li>
     <li><p>utilitário taskactions</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>submitComplete - modelo de tarefa</p></li>
     <li><p>Reject - modelo de tarefa</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O Workspace chama a função fetchTasks do modelo TaskList para criar modelos Task para este componente.

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
   <td><p>Dependências de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
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
   <td><p>Dependências de JS</p> </td>
   <td>
    <ul>
     <li><p>Campo: fila: { name, qid, isDefault, type}</p> </li>
     <li><p>Campo: query: string</p> </li>
     <li><p>Campo: parentView: exibição de lista de filtros</p> </li>
     <li><p>Campo: parentModel: modelo da lista de tarefas</p> </li>
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
   <td><p>Dependências de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
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
   <td><p>Dependências de JS</p> </td>
   <td>
    <ul>
     <li><p>Estende : visualização de filtro</p> </li>
     <li><p>Campo : fila :{ nome, qid, isDefault, tipo }</p> </li>
     <li><p>Campo : query : string</p> </li>
     <li><p>Campo : parentView : exibição de lista de filtros</p> </li>
     <li><p>Campo : parentModel : modelo da lista de tarefas</p> </li>
     <li><p>Campo : utilitário</p> </li>
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
>TeamFilter obtém o evento indicando qual tarefa foi selecionada do componente TaskList. Embora esses componentes compartilhem a classe do modelo, não há outra dependência.

## Detalhes da tarefa {#taskdetails}

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
   <td><p>A maioria das classes do Utilitário</p> </td>
  </tr>
  <tr>
   <td><p>Dependências de JS</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>formrendering utility</p> </li>
     <li><p>utilitário de notas</p> </li>
     <li><p>utilitário de anexos</p> </li>
     <li><p>utilitário taskactions</p> </li>
     <li><p>utilitário de histórico</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p> </td>
   <td>
    <ul>
     <li><p>encaminhado - modelo de tarefa</p> </li>
     <li><p>shared - modelo de tarefa</p> </li>
     <li><p>consultado - modelo de tarefa</p> </li>
     <li><p>rejeitada - modelo de tarefa</p> </li>
     <li><p>abandonado - modelo de tarefa</p> </li>
     <li><p>desbloqueado - modelo de tarefa</p> </li>
     <li><p>bloqueado - modelo de tarefa</p> </li>
     <li><p>reivindicado - modelo de tarefa</p> </li>
     <li><p>alterar:selecionar tarefa - modelo da lista de tarefas</p> </li>
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
   <td><p>startprocess.html (na pasta de rotas)</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>Categoria</p></td>
  </tr>
  <tr>
   <td><p>Dependências de JS</p></td>
   <td>
    <ul>
     <li><p>modelo favoritecategoryfatory</p></li>
     <li><p>modelo alcategoryfatory</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetched - modelo de lista de categorias </p></li>
     <li><p>adicionar - modelo de lista de categorias </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Esse componente usa classes de modelo de alguns outros componentes, como StartPointList, StartPoint e Task. Além dessa dependência, CategoryList pode ser usada de maneira independente.

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
   <td><p>Dependências de JS</p></td>
   <td>
    <ul>
     <li><p>modelo de lista de categorias</p></li>
     <li><p>modelo startpoint</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>alterado - modelo de categoria </p></li>
     <li><p>childrenFetched - modelo de categoria </p></li>
     <li><p>categoria:selecionada - modelo de lista de categorias </p></li>
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
   <td><p>startprocess.html (na pasta de rotas)</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências de JS</p></td>
   <td>
    <ul>
     <li><p>modelo de categoria</p></li>
     <li><p>modelo favoritecategoryfatory</p></li>
     <li><p>modelo alcategoryfatory</p></li>
     <li><p>visualização do ponto de partida</p></li>
     <li><p>modelo startpoint</p></li>
     <li><p>modelo de ponto de partida</p></li>
     <li><p>modelo de tarefa</p></li>
     <li><p>modelo de tarefa</p></li>
     <li><p>modelo da lista de tarefas</p></li>
     <li><p>modelo de tarefa de equipe</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
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
>Os componentes StartPointList e CategoryList compartilham a classe modelo, portanto, a primeira depende da última. CategoryList acessa as informações sobre quais pontos iniciais da categoria são mostrados. Para usar StartPointList independentemente, simule o acionador de evento de CategoryList.

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
   <td><p>Dependências de JS</p></td>
   <td><p>modelo de tarefa</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
   <td><p>change - modelo de ponto de partida </p></td>
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
     <li><p>A maioria das classes do Utilitário</p> </li>
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Dependências de JS</p> </td>
   <td>
    <ul>
     <li><p>modelo de categoria</p> </li>
     <li><p>modelo favoritecategoryfatory</p> </li>
     <li><p>modelo alcategoryfatory</p> </li>
     <li><p>formrendering utility</p> </li>
     <li><p>utilitário de notas</p> </li>
     <li><p>utilitário de anexos</p> </li>
     <li><p>utilitário taskactions</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p> </td>
   <td>
    <ul>
     <li><p>categoria:selecionada - modelo de lista de categorias</p> </li>
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
     <li><p>allStartpointsFetched - modelo de lista de categorias</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os componentes StartProcess e StartPointList compartilham a classe do modelo. Esse componente se torna relevante ao selecionar um ponto de partida em StartPointList.

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
   <td><p>tracking.html (na pasta de rota)</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências de JS</p></td>
   <td><p>modelo processname</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>adicionar - modelo processnamelist </p></li>
     <li><p>fetch:processnames - modelo processnamelist </p></li>
     <li><p>change - modelo processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList não depende de outros componentes. No entanto, internamente, depende da classe de modelo ProcessInstanceList que, por sua vez, depende de outros componentes. Assim, ProcessNameList usa muitas classes de modelo como ProcessInstanceList, ProcessInstance, TaskList, Teamtask e Task. Além dessas dependências, ProcessNameList pode ser usado independentemente.

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
   <td><p>Dependências de JS</p></td>
   <td><p>modelo processinstancelist</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
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
   <td><p>tracking.html (na pasta de rota)</p></td>
  </tr>
  <tr>
   <td><p>Requer componentes</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dependências de JS</p></td>
   <td><p>modelo processname</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>processname:seleted - modelo processnamelist </p></li>
     <li><p>processname:instancesfetched - modelo processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList espera um evento de ProcessNameList indicando o nome do processo para buscar e exibir instâncias. Para usar ProcessInstanceList independentemente, simule o acionador de evento separadamente.

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
   <td><p>Dependências de JS</p></td>
   <td><p>modelo da lista de tarefas</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
   <td><p>change - modelo processinstance </p></td>
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
   <td><p>Dependências de JS</p></td>
   <td>
    <ul>
     <li><p>modelo processname</p></li>
     <li><p>utilitário de histórico</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>processname:seleted - modelo processnamelist </p></li>
     <li><p>processinstance:seleted - modelo processinstancelist </p></li>
     <li><p>tasksFetched - modelo de instância de processamento </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory espera um evento de ProcessInstanceList indicando qual histórico da instância de processo deve ser exibido. Além dessa dependência, o componente pode ser usado independentemente.

## Fora do Escritório {#outofoffice}

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
   <td><p>Dependências de JS</p> </td>
   <td><p>exibição de pesquisa de usuário</p> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched - modelo de saída</p> </li>
     <li><p>outOfOfficeSettingsSaved - modelo de saída</p> </li>
     <li><p>processesFetched - modelo de saída</p> </li>
     <li><p>principalSeleted - exibição de pesquisa principal</p> </li>
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
   <td><p>Dependências de JS</p> </td>
   <td><p>exibição de pesquisa de usuário</p> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGrananted - modelo de compartilhamento</p> </li>
     <li><p>queueAccessRequested - modelo de compartilhamento</p> </li>
     <li><p>givenUsersFetched - modelo de compartilhamento</p> </li>
     <li>accessibleUsersFetched - modelo de compartilhamento</li>
     <li><p>queueAccessRevoks - modelo de compartilhamento</p> </li>
     <li><p>queueAccessRemoved - modelo de compartilhamento</p> </li>
     <li><p>principalSeleted - exibição de pesquisa principal</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue pode ser usada de forma independente.

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
   <td><p>Dependências de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
   <td>
    <ul>
     <li><p>preferencesFetched - modelo de configurações de usuário </p></li>
     <li><p>settingsUpdated - modelo de configurações </p></li>
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
   <td><p>Dependências de JS</p></td>
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
>AppNavigation pode ser usada de maneira independente.

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
   <td><p>Dependências de JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched - modelo de informações de usuário</li>
     <li>sessionRenewed - modelo de informações de usuário <br /> </li>
     <li>sessionExpirou - modelo userinfo </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo pode ser usada independentemente.

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
   <td><p>Dependências de JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p></td>
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
   <td><p>Dependências de JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p> </td>
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
   <td><p>Dependências de JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p> </td>
   <td><p>templateFetched- modelo de pesquisa</p> </td>
  </tr>
 </tbody>
</table>

## ListaModeloDePesquisa {#searchtemplatelist}

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
   <td><p>tracking.html (na pasta de rota)</p> </td>
  </tr>
  <tr>
   <td><p>Requer componentes</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dependências de JS</p> </td>
   <td><p>modelo do searchtemplate</p> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p> </td>
   <td><p>change - modelo searchtemplatelist</p> </td>
  </tr>
 </tbody>
</table>

## PesquisarDetalhesModelo {#searchtemplatedetails}

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
   <td><p>Dependências de JS</p> </td>
   <td>ND<br /> </td>
  </tr>
  <tr>
   <td><p>Eventos ouvidos (Nome do evento - Acionador)</p> </td>
   <td><p>searchTemplate:seleted - modelo de modelo de pesquisa</p> </td>
  </tr>
 </tbody>
</table>
