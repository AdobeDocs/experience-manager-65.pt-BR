---
title: Trabalhar com o espaço de trabalho do AEM Forms
description: Introdução ao espaço de trabalho do AEM Forms com esta visão geral rápida dos fluxos de trabalho de processo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# Trabalhar com o espaço de trabalho do AEM Forms{#working-with-aem-forms-workspace}

## Introdução {#introduction}

O espaço de trabalho do AEM Forms faz parte do AEM Forms. O Workspace facilita a representação do HTML Forms, além do PDF forms. Agora você pode se envolver em processos de negócios a partir de interfaces móveis e aplicativos da Web.

Além disso, o espaço de trabalho da AEM Forms é altamente personalizável usando o HTML padrão e as metodologias de desenvolvimento JavaScript™. É um software baseado em componentes que se integra facilmente a outros aplicativos da Web.

Para obter mais informações, consulte [Introdução ao AEM Forms workspace](/help/forms/using/introduction-html-workspace.md).

## Familiarizando-se {#getting-familiar}

Para conhecer o processo completo de criação de aplicativos de formulários para automatizar um processo de negócios, siga o passo a passo. Você pode criar, gerenciar e testar um aplicativo usando o espaço de trabalho do Workbench, Designer e AEM Forms depois de seguir a apresentação. Para obter detalhes sobre a implementação, consulte [Criando seu Primeiro Aplicativo AEM Forms](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## Visão geral funcional {#functional-overview}

Você pode usar o espaço de trabalho do AEM Forms para executar as seguintes tarefas:

**Iniciar um processo comercial:** o espaço de trabalho do AEM Forms classifica seus processos como criados e configurados pela sua organização. Você pode adicionar as categorias usadas com frequência aos favoritos para acessar as categorias rapidamente. Ao iniciar um processo, você normalmente preenche um formulário para iniciar um processo de negócios que forma controles de fluxo de trabalho. Para obter mais informações, consulte [Iniciando Processos](/help/forms/using/starting-processes.md).

**Exibir e agir sobre tarefas:** ao exibir suas listas de tarefas pendentes, você verá tarefas de um processo comercial atribuídas a você, a qualquer grupo ao qual você pertença ou que sejam tarefas compartilhadas de outros usuários. Você pode abrir, trabalhar e concluir as tarefas conforme necessário. Normalmente, concluir uma tarefa envolve fornecer informações, aprovar um formulário ou rejeitar um formulário. Para obter mais informações, consulte [Trabalhando com listas de tarefas](/help/forms/using/todo-lists.md).

**Rastrear tarefas**: para rastrear suas tarefas, use a guia Rastreamento do espaço de trabalho do AEM Forms. Você pode pesquisar processos ativos ou concluídos nos quais iniciou ou participou. É possível exibir as tarefas, atribuições e formulários que fizeram parte do processo. Você também pode iniciar novos processos usando dados de formulário de um processo iniciado anteriormente. Para obter mais informações, consulte [Processos de rastreamento](/help/forms/using/tracking-processes.md).

## Nova oferta do espaço de trabalho do AEM Forms {#new-offering-of-aem-forms-workspace}

**Suporte para aprovação em massa de tarefas**:

É possível aprovar várias tarefas do mesmo tipo. Depois de selecionar uma tarefa para aprovação, somente as tarefas com o mesmo processo, com os mesmos nomes de tarefa e as mesmas opções de roteiro permanecerão ativadas. Consulte [Trabalhando com listas de tarefas](/help/forms/using/todo-lists.md) para obter detalhes sobre a implementação.

## Migração do Flex Workspace para o AEM Forms workspace {#migrating-from-flex-workspace-to-aem-forms-workspace}

O Flex Workspace não é compatível com clientes da AEM Forms. Todos os clientes que usam o Flex Workspace devem migrar para o AEM Forms Workspace.

No espaço de trabalho do AEM Forms, os serviços padrão de renderização e envio, no perfil de ação padrão, associados aos formulários XDP foram alterados e novos serviços foram introduzidos. Para obter detalhes, consulte [Novo serviço de renderização e envio](/help/forms/using/new-render-submit-service.md). Para migrar seus processos existentes, que funcionam com formulários XDP, para usar esses serviços, siga [estas etapas](new-render-submit-service.md).

**Mapeando personalizações do Flex Workspace com o espaço de trabalho do AEM Forms**

O mapeamento entre vários tipos de personalizações em ambos os espaços de trabalho é o seguinte:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de personalização </strong></td>
   <td><strong>Personalizações abrangidas </strong></td>
   <td><strong>Cenário de personalização do espaço de trabalho do AEM Forms correspondente</strong></td>
  </tr>
  <tr>
   <td>Personalização de localização</td>
   <td>
    <ol>
     <li>Alteração do local do Workspace</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">Alterar a localidade do espaço de trabalho do AEM Forms</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalização de tema</td>
   <td>
    <ol>
     <li>Substituição de imagens</li>
     <li>Modificação de cores</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">Alterando o Logotipo da Organização</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">Alteração do esquema de cores</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalização de layout</td>
   <td>
    <ol>
     <li>Simplificando a interface de usuário do Workspace<br /> </li>
     <li>Criando uma Nova Tela de Login</li>
     <li>Criação de um contêiner de aprovação personalizado</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">Trabalho com componentes reutilizáveis</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">Tela de criação de logon</a></li>
     <li>O contêiner de aprovação está obsoleto.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Alguns dos recursos do Flex Workspace que não estão disponíveis no espaço de trabalho do AEM Forms incluem: mensagens e notificações, página de boas-vindas, contêiner de aprovação e opção para gerenciar cabeçalhos de coluna. Para obter uma lista completa, consulte [Recursos do Flex Workspace não disponíveis no espaço de trabalho do AEM Forms](/help/forms/using/features-flex-workspace-available-html.md).

## Desenvolvimento com o espaço de trabalho AEM Forms {#developing-with-aem-forms-workspace}

### Arquitetura {#architecture}

O espaço de trabalho do AEM Forms é um aplicativo web baseado em HTML e JavaScript™ hospedado na CRX™. Quando o URL do Workspace é aberto em um navegador, um recurso do CRX™ é acessado e o aplicativo é renderizado como uma página de HTML no navegador. As bibliotecas JavaScript e o código JavaScript personalizado gerenciam o comportamento interno e externo do aplicativo, como a interface do usuário, a interação do usuário e a comunicação com o servidor do AEM Forms. Para obter mais detalhes, consulte a [arquitetura](/help/forms/using/html-workspace-architecture.md) do espaço de trabalho do AEM Forms.

### Personalização do espaço de trabalho do AEM Forms {#aem-forms-workspace-customization}

O espaço de trabalho do AEM Forms oferece suporte a uma grande variedade de personalizações para atualizar o layout da interface do usuário, sua aparência, funcionalidade e muito mais. As personalizações envolvem a atualização de um ou mais dos itens a seguir:

* Aparências da interface do usuário
* Funcionalidade usando personalizações semânticas
* Reutilização de componentes HTML em outros aplicativos web

O artigo [personalização](introduction-customizing-html-workspace.md#types-of-customizations) explica os tipos dessas personalizações.

### Configurar o ambiente do desenvolvedor {#set-up-the-developer-environment}

Os materiais de entrega do espaço de trabalho do AEM Forms incluem um pacote do CRX implantado no CRX, um arquivo SDK que contém o código fonte completo, bibliotecas JavaScript de terceiros e scripts de build do espaço de trabalho do AEM Forms. Use-as para configurar o ambiente do desenvolvedor para executar as personalizações mencionadas acima. Para obter mais detalhes, consulte [Criação do código do espaço de trabalho do AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

É possível personalizar uma parte importante da interface e da funcionalidade principal, como fontes, esquema de cores, logotipo, tela de logon, caixas de diálogo de erro, integração com aplicativos de terceiros e reutilização de componentes em aplicativos de terceiros. Você também pode aprimorar o conteúdo exibido na página Resumo da tarefa, mostrar imagens para ações de rota de tarefa e até modificar os Modelos e Exibições de backbone de baixo nível que criam o aplicativo de espaço de trabalho do AEM Forms.

### Renderização de HTML do XDP Forms {#html-rendering-of-xdp-forms}

Por padrão, para um novo processo, um formulário XDP é renderizado no formato PDF em um desktop e no formato HTML em um tablet. É possível renderizar um formulário XDP no formato HTML sempre. Para obter detalhes, consulte [Novos serviços de renderização e envio](/help/forms/using/new-render-submit-service.md).

O recurso [Forms Móvel](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html), que funciona com [perfis](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html), habilita a representação HTML de formulários XDP. Por padrão, o &quot;Renderizar novo formulário de HTML&quot; usa o perfil `default.html`, que você pode alterar. Você também pode adicionar alterações personalizadas que ocorrem antes de renderizar um formulário XDP no formato HTML.

## aplicativo de espaço de trabalho do AEM Forms {#aem-forms-workspace-app}

Para trabalhar em seus processos comerciais em um dispositivo móvel, você pode usar a oferta de aplicativo do espaço de trabalho do AEM Forms do AEM Forms. Para obter mais informações, consulte a [visão geral do aplicativo do AEM Forms workspace](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html).
