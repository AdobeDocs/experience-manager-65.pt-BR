---
title: Trabalhar com a área de trabalho do AEM Forms
seo-title: Working with AEM Forms workspace
description: Introdução ao AEM Forms workspace com esta rápida visão geral dos fluxos de trabalho do processo.
seo-description: Get started with AEM Forms workspace with this quick overview of the process workflows.
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Trabalhar com a área de trabalho do AEM Forms{#working-with-aem-forms-workspace}

## Introdução {#introduction}

A área de trabalho do AEM Forms faz parte do AEM Forms. O Workspace facilita a representação do HTML Forms, além do PDF forms. Agora você pode participar de processos de negócios de interfaces móveis e aplicativos Web.

Além disso, a AEM Forms workspace é altamente personalizável usando as metodologias de desenvolvimento padrão do HTML e JavaScript™. É um software baseado em componentes que se integra facilmente aos outros aplicativos da Web.

Para obter mais informações, consulte [Introdução à área de trabalho do AEM Forms](/help/forms/using/introduction-html-workspace.md).

## Familiarizar-se {#getting-familiar}

Para se familiarizar com o processo completo de criação de um aplicativo de formulários para automatizar um processo de negócios, siga a apresentação. Você pode criar, gerenciar e testar um aplicativo usando o Workbench, o Designer e o AEM Forms workspace depois de seguir a apresentação. Para obter detalhes sobre a implementação, consulte [Criar seu primeiro aplicativo AEM Forms](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## Visão geral funcional {#functional-overview}

Você pode usar o espaço de trabalho do AEM Forms para executar as seguintes tarefas:

**Iniciar um processo de negócios:** As categorias de espaço de trabalho da AEM Forms de seus processos foram projetadas e configuradas por sua organização. Você pode marcar as categorias usadas com frequência para acessar as categorias rapidamente. Quando você inicia um processo, normalmente preenche um formulário para iniciar um processo de negócios que forma controles de fluxo de trabalho. Para obter mais informações, consulte [Iniciando processos](/help/forms/using/starting-processes.md).

**Exibir e agir de acordo com as tarefas:** Ao exibir suas listas de itens a fazer, você vê tarefas de um processo de negócios que são atribuídas a você, a quaisquer grupos aos quais você pertence ou que são tarefas compartilhadas de outros usuários. Você pode abrir, trabalhar e concluir as tarefas conforme necessário. Normalmente, concluir uma tarefa envolve fornecer informações, aprovar um formulário ou rejeitar um formulário. Para obter mais informações, consulte [Trabalhar com listas de tarefas](/help/forms/using/todo-lists.md).

**Rastrear tarefas**: Para rastrear suas tarefas, use a guia Rastreamento do espaço de trabalho do AEM Forms. Você pode procurar processos ativos ou concluídos nos quais iniciou ou participou. Você pode visualizar as tarefas, atribuições e formulários que faziam parte do processo. Também é possível iniciar novos processos usando dados de formulário de um processo iniciado anteriormente. Para obter mais informações, consulte [Processos de rastreamento](/help/forms/using/tracking-processes.md).

## Nova oferta do espaço de trabalho do AEM Forms {#new-offering-of-aem-forms-workspace}

**Suporte para aprovação de tarefas em massa**:

É possível aprovar várias tarefas do mesmo tipo. Depois de selecionar uma tarefa para aprovação, somente as tarefas com o mesmo processo, com os mesmos nomes de tarefa e as mesmas opções de rota permanecerão ativadas. Consulte [Trabalhar com listas de tarefas](/help/forms/using/todo-lists.md) para obter detalhes sobre a implementação.

## Migração do Flex Workspace para o espaço de trabalho do AEM Forms {#migrating-from-flex-workspace-to-aem-forms-workspace}

O Flex Workspace não é compatível com clientes do AEM Forms. Todos os clientes que usam o Flex Workspace devem migrar para o AEM Forms Workspace.

No espaço de trabalho do AEM Forms, os serviços de renderização e envio padrão, no perfil de ação padrão, associados aos formulários XDP, foram alterados e novos serviços foram introduzidos. Para obter detalhes, consulte [Novo serviço de renderização e envio](/help/forms/using/new-render-submit-service.md). Para migrar seus processos existentes, que funcionam com formulários XDP, para usar esses serviços, você pode seguir [essas etapas](new-render-submit-service.md).

**Mapeamento de personalizações do Flex Workspace com a área de trabalho do AEM Forms**

O mapeamento entre vários tipos de personalizações em ambos os espaços de trabalho é o seguinte.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de personalização </strong></td>
   <td><strong>Personalizações cobertas </strong></td>
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
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">Mudando logotipo da organização</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">Alterar esquema de cores</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalização de layout</td>
   <td>
    <ol>
     <li>Simplificação da interface do usuário do Workspace<br /> </li>
     <li>Criar uma nova tela de logon</li>
     <li>Criação de um contêiner de aprovação personalizado</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">Trabalhar com componentes reutilizáveis</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">Criação de uma nova tela Logon</a></li>
     <li>O Contêiner de aprovação está obsoleto.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Alguns dos recursos do Flex Workspace que não estão disponíveis no AEM Forms workspace incluem: mensagens e notificação, página de boas-vindas, contêiner de aprovação e opção para gerenciar cabeçalhos de coluna. Para obter uma lista completa, consulte [Os recursos do Flex Workspace não estão disponíveis no AEM Forms workspace](/help/forms/using/features-flex-workspace-available-html.md).

## Desenvolvimento com a área de trabalho do AEM Forms {#developing-with-aem-forms-workspace}

### Arquitetura {#architecture}

O AEM Forms workspace é um aplicativo Web baseado em HTML e JavaScript™ hospedado no CRX™. Quando o URL do Workspace é aberto em um navegador, um recurso CRX™ é acessado e o aplicativo é renderizado como uma HTML no navegador. As bibliotecas JavaScript e o código JavaScript personalizado gerenciam o comportamento interno e externo do aplicativo, como interface do usuário, interação do usuário e comunicação com o servidor AEM Forms. Para obter mais detalhes, consulte Espaço de trabalho do AEM Forms [arquitetura](/help/forms/using/html-workspace-architecture.md).

### Personalização do espaço de trabalho do AEM Forms {#aem-forms-workspace-customization}

A área de trabalho do AEM Forms é compatível com uma grande variedade de personalizações para atualizar o layout da interface do usuário, sua aparência, funcionalidade e muito mais. As personalizações envolvem a atualização de um ou mais dos seguintes itens:

* Aspectos da interface do usuário
* Funcionalidade usando personalizações semânticas
* Reutilização de componentes HTML em outros aplicativos da Web

O [personalização](introduction-customizing-html-workspace.md#types-of-customizations) artigo explica os tipos de tais personalizações.

### Configurar o ambiente do desenvolvedor {#set-up-the-developer-environment}

Os deliveries do espaço de trabalho do AEM Forms incluem um pacote CRX implantado no CRX, um arquivo SDK que contém o código fonte completo, bibliotecas JavaScript de terceiros e scripts de criação do espaço de trabalho do AEM Forms. Use-os para configurar o ambiente do desenvolvedor para executar as personalizações mencionadas acima. Para obter mais detalhes, consulte [Criação do código do espaço de trabalho do AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

Você pode personalizar uma parte importante da interface e das funcionalidades principais, como fontes, esquema de cores, logotipo, tela de logon, caixas de diálogo de erros, integração com aplicativos de terceiros e reutilização de componentes em aplicativos de terceiros. Também é possível aprimorar o conteúdo exibido na página Resumo de tarefas, mostrar imagens para ações de roteiro de tarefas e até mesmo modificar Modelos e Exibições de Backbone de baixo nível que criam o aplicativo AEM Forms workspace.

### Renderização de HTML do Forms XDP {#html-rendering-of-xdp-forms}

Por padrão, para um novo processo, um formulário XDP é renderizado no formato PDF em uma área de trabalho e no formato HTML em um tablet. É possível renderizar sempre um formulário XDP no formato HTML. Para obter detalhes, consulte [Novos serviços de renderização e envio](/help/forms/using/new-render-submit-service.md).

[Forms móvel](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) , que funciona com [perfis](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html), permite a representação de HTML de formulários XDP. Por padrão, o &quot;Renderizar novo formulário de HTML&quot; usa `default.html` , que você pode alterar. Você também pode adicionar alterações personalizadas que ocorrem antes de renderizar um formulário XDP no formato HTML.

## Aplicativo do espaço de trabalho do AEM Forms {#aem-forms-workspace-app}

Para trabalhar em seus processos comerciais em um dispositivo móvel, você pode usar a oferta de aplicativo AEM Forms workspace da AEM Forms. Para obter mais informações, consulte o [Visão geral do aplicativo do AEM Forms workspace](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html).
