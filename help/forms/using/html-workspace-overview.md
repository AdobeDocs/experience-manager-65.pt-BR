---
title: Trabalhar com a área de trabalho do AEM Forms
seo-title: Trabalhar com a área de trabalho do AEM Forms
description: Comece com a área de trabalho da AEM Forms com esta rápida visão geral dos workflows do processo.
seo-description: Comece com a área de trabalho da AEM Forms com esta rápida visão geral dos workflows do processo.
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
translation-type: tm+mt
source-git-commit: 21efe30c6a69d04c737bc523aeaab504db8f605b
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---


# Trabalhar com a área de trabalho do AEM Forms{#working-with-aem-forms-workspace}

## Introdução {#introduction}

A área de trabalho do AEM Forms faz parte do AEM Forms. O Workspace facilita a execução do HTML Forms, além de PDF forms. Agora você pode envolver-se em processos comerciais de interfaces móveis e aplicativos da Web.

Além disso, a área de trabalho da AEM Forms é altamente personalizável usando as metodologias de desenvolvimento padrão HTML e JavaScript™. É um software baseado em componentes que se integra facilmente com seus outros aplicativos da Web.

Para obter mais informações, consulte [Introdução ao espaço de trabalho AEM Forms](/help/forms/using/introduction-html-workspace.md).

## Familiarizar-se {#getting-familiar}

Para se familiarizar com o processo completo de criação de um aplicativo de formulários para automatizar um processo de negócios, siga as orientações. Você pode criar, gerenciar e testar um aplicativo usando o Workbench, o Designer e a área de trabalho do AEM Forms depois de seguir a apresentação. Para obter detalhes sobre a implementação, consulte [Criando seu primeiro aplicativo AEM Forms](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## Visão geral funcional {#functional-overview}

Você pode usar a área de trabalho do AEM Forms para executar as seguintes tarefas:

**Start de um processo de negócios:A área de trabalho** AEM Forms categoria seus processos conforme projetado e configurado pela sua organização. Você pode marcar as categorias usadas com frequência para acessar as categorias rapidamente. Quando você start um processo, normalmente preenche um formulário para start de um processo de negócios que forma controles de fluxo de trabalho. Para obter mais informações, consulte [Iniciando processos](/help/forms/using/starting-processes.md).

**Visualização e agir de acordo com as tarefas:** ao visualização das listas de Tarefas Pendentes, você verá tarefas de um processo de negócios que são atribuídas a você ou a quaisquer grupos aos quais você pertence ou que são tarefas compartilhadas de outros usuários. Você pode abrir, trabalhar e concluir as tarefas, conforme necessário. Normalmente, preencher uma tarefa envolve fornecer informações, aprovar um formulário ou rejeitar um formulário. Para obter mais informações, consulte [Trabalhar com listas de tarefas](/help/forms/using/todo-lists.md).

**Tarefas** de rastreamento: Para rastrear suas tarefas, use a guia Rastreamento da área de trabalho do AEM Forms. Você pode pesquisar por processos ativos ou concluídos nos quais iniciou ou participou. Você pode visualização as tarefas, atribuições e formulários que faziam parte do processo. Também é possível start de novos processos usando dados de formulário de um processo iniciado anteriormente. Para obter mais informações, consulte [Processos de rastreamento](/help/forms/using/tracking-processes.md).

## Nova oferta de espaço de trabalho AEM Forms {#new-offering-of-aem-forms-workspace}

**Suporte para aprovação em massa de tarefas**:

Você pode aprovar várias tarefas do mesmo tipo. Depois de selecionar uma tarefa para aprovação, somente as tarefas com o mesmo processo, com os mesmos nomes de tarefa e as mesmas opções de rota permanecem ativadas. Consulte [Trabalhar com listas de tarefas](/help/forms/using/todo-lists.md) para obter detalhes sobre a implementação.

## Migração do Flex Workspace para o espaço de trabalho do AEM Forms {#migrating-from-flex-workspace-to-aem-forms-workspace}

O Flex Workspace não é compatível com clientes AEM Forms. Todos os clientes que usam o Flex Workspace devem mudar para o AEM Forms Workspace.

Na área de trabalho do AEM Forms, os serviços padrão de renderização e envio, no perfil de ação padrão, associados aos formulários XDP, foram alterados e novos serviços foram introduzidos. Para obter detalhes, consulte [Novo serviço de renderização e envio](/help/forms/using/new-render-submit-service.md). Para migrar seus processos existentes, que funcionam com formulários XDP, para usar esses serviços, você pode seguir [essas etapas](new-render-submit-service.md).

**Mapeamento de personalizações do Flex Workspace com a área de trabalho do AEM Forms**

O mapeamento entre vários tipos de personalizações em ambos os espaços de trabalho é o seguinte.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de personalização </strong></td>
   <td><strong>Personalizações cobertas </strong></td>
   <td><strong>Cenário de personalização do espaço de trabalho AEM Forms correspondente</strong></td>
  </tr>
  <tr>
   <td>personalização da localização</td>
   <td>
    <ol>
     <li>Alteração da localidade da Workspace</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">Alteração da localidade da área de trabalho do AEM Forms</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalização do tema</td>
   <td>
    <ol>
     <li>Substituição de imagens</li>
     <li>Modificação de cores</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">Mudando o logotipo da organização</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">Alterar esquema de cores</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalização de layout</td>
   <td>
    <ol>
     <li>Simplificando a interface do usuário do Workspace<br /> </li>
     <li>Criando uma nova tela de logon</li>
     <li>Criação de um Container de aprovação personalizado</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">Trabalhar com componentes reutilizáveis</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">Criação de uma nova tela de logon</a></li>
     <li>O Container de aprovação está obsoleto.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Alguns dos recursos do Flex Workspace que não estão disponíveis na área de trabalho do AEM Forms incluem: mensagens e notificação, página de boas-vindas, container de aprovação e opção para gerenciar cabeçalhos de coluna. Para obter uma lista completa, consulte [Recursos do Flex Workspace não disponíveis na área de trabalho do AEM Forms](/help/forms/using/features-flex-workspace-available-html.md).

## Desenvolvimento com o espaço de trabalho AEM Forms {#developing-with-aem-forms-workspace}

### Arquitetura {#architecture}

O espaço de trabalho AEM Forms é um aplicativo da Web baseado em HTML e JavaScript™ hospedado no CRX™. Quando o URL da Workspace é aberto em um navegador, um recurso CRX™ é acessado e o aplicativo é renderizado como uma página HTML no navegador. As bibliotecas JavaScript e o código JavaScript personalizado gerenciam o comportamento interno e externo do aplicativo, como interface do usuário, interação do usuário e comunicação com o servidor AEM Forms. Para obter mais detalhes, consulte Espaço de trabalho AEM Forms [arquitetura](/help/forms/using/html-workspace-architecture.md).

### Personalização da área de trabalho do AEM Forms {#aem-forms-workspace-customization}

A área de trabalho do AEM Forms oferece suporte a uma grande variedade de personalizações para atualizar o layout da interface do usuário, sua aparência, funcionalidade e muito mais. As personalizações envolvem a atualização de um ou mais dos seguintes:

* Aparências da interface do usuário
* Funcionalidade usando personalizações semânticas
* Reutilização de componentes HTML em outros aplicativos da Web

O artigo [customization](introduction-customizing-html-workspace.md#types-of-customizations) explica os tipos de tais personalizações.

### Configure o ambiente do desenvolvedor {#set-up-the-developer-environment}

Os produtos do espaço de trabalho AEM Forms incluem um pacote CRX implantado no CRX, um arquivo SDK que contém o código fonte completo, bibliotecas JavaScript de terceiros e scripts de criação da área de trabalho do AEM Forms. Use-os para configurar o ambiente do desenvolvedor para executar as personalizações mencionadas acima. Para obter mais detalhes, consulte [Criação do código do espaço de trabalho AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

Você pode personalizar uma parte importante da interface e da funcionalidade principal, como fontes, esquema de cores, logotipo, tela de login, caixas de diálogo de erros, integração com aplicativos de terceiros e reutilização de componentes em aplicativos de terceiros. Você também pode aprimorar o conteúdo exibido na página Resumo da Tarefa, mostrar imagens para ações de rota da tarefa e até modificar os Modelos de Backbone de baixo nível e as Visualizações que criam o aplicativo de área de trabalho da AEM Forms.

### Renderização HTML do XDP Forms {#html-rendering-of-xdp-forms}

Por padrão, para um novo processo, um formulário XDP é renderizado no formato PDF em um desktop e no formato HTML em um tablet. É possível renderizar sempre um formulário XDP no formato HTML. Para obter detalhes, consulte [Novos serviços de renderização e envio](/help/forms/using/new-render-submit-service.md).

[O recurso ](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) Formulários móveis, que funciona com  [perfis](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html), permite a execução HTML de formulários XDP. Por padrão, o perfil &quot;Renderizar novo formulário HTML&quot; usa `default.html`, que você pode alterar. Também é possível adicionar alterações personalizadas que ocorrem antes da renderização de um formulário XDP no formato HTML.

## Aplicativo do espaço de trabalho AEM Forms {#aem-forms-workspace-app}

Para trabalhar nos processos de sua empresa em um dispositivo móvel, você pode usar a oferta de aplicativos para área de trabalho da AEM Forms da AEM Forms. Para obter mais informações, consulte a [visão geral do aplicativo do espaço de trabalho AEM Forms](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html).
