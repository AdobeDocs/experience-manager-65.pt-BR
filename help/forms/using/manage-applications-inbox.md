---
title: Gerenciar aplicativos e tarefas de formulários na Caixa de entrada do AEM
seo-title: Gerenciar aplicativos e tarefas de formulários na Caixa de entrada do AEM
description: A Caixa de entrada do AEM permite que você inicie workflows centrados no Forms por meio do envio de aplicativos e do gerenciamento do tarefa.
seo-description: A Caixa de entrada do AEM permite que você inicie workflows centrados no Forms por meio do envio de aplicativos e do gerenciamento do tarefa.
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Gerenciar aplicativos e tarefas de formulários na Caixa de entrada do AEM{#manage-forms-applications-and-tasks-in-aem-inbox}

Uma das muitas maneiras de iniciar ou acionar um fluxo de trabalho centrado no Forms é através de aplicativos na Caixa de entrada do AEM. É necessário criar um aplicativo de fluxo de trabalho para disponibilizar um fluxo de trabalho do Forms como aplicativo na Caixa de entrada. Para obter mais informações sobre o aplicativo de fluxo de trabalho e outras formas de iniciar workflows do Forms, consulte [Iniciar um fluxo de trabalho centrado no Forms no OSGi](../../forms/using/aem-forms-workflow.md#launch).

Além disso, a Caixa de entrada do AEM consolida notificações e tarefas de vários componentes do AEM, incluindo workflows do Forms. Quando um fluxo de trabalho de formulários contendo uma etapa Atribuir tarefa é acionado, o aplicativo associado é listado como uma tarefa na Caixa de entrada do destinatário. Se o destinatário for um grupo, a tarefa será exibida na Caixa de entrada de todos os membros do grupo até que um indivíduo solicite ou delegue a tarefa.

A interface do usuário Caixa de entrada fornece visualizações de calendário e listas para tarefas de visualização. Você também pode definir as configurações de visualização. É possível filtrar tarefas com base em vários parâmetros. Para obter mais informações sobre visualizações e filtros, consulte [Caixa de entrada](/help/sites-authoring/inbox.md).

Em resumo, a Caixa de entrada permite que você crie um novo aplicativo e gerencie tarefas atribuídas.

>[!NOTE] {graybox=&quot;true&quot;}
>
>Você deve ser um membro do grupo de usuários do fluxo de trabalho para poder usar a Caixa de entrada do AEM.

## Criar aplicativo {#create-application}

1. Vá para Caixa de entrada do AEM em https://&#39;[server]:[port]&#39;/aem/inbox.
1. Na interface da caixa de entrada, toque em **[!UICONTROL Criar > Aplicativo]**. A página Selecionar aplicativo é exibida.
1. Selecione um aplicativo e clique em **[!UICONTROL Criar]**. O formulário adaptável associado ao aplicativo é aberto. Preencha as informações no formulário adaptável e toque em **[!UICONTROL Enviar]**. Ele inicia o fluxo de trabalho associado e cria uma tarefa na Caixa de entrada do destinatário.

## Gerencie tarefas {#manage-tasks}

Quando um fluxo de trabalho do Forms é acionado e você é um destinatário ou parte do grupo destinatário, uma tarefa é exibida em sua Caixa de entrada. Você pode visualização detalhes da tarefa e executar ações disponíveis na tarefa na Caixa de entrada.

### tarefas de solicitação ou delegadas {#claim-or-delegate-tasks}

As Tarefas atribuídas a um grupo são exibidas na Caixa de entrada de todos os membros do grupo. Qualquer membro do grupo pode reivindicar essa tarefa ou delegá-la a outro membro do grupo. Para isso:

1. Toque para selecionar a miniatura da tarefa. As opções para abrir ou delegar a tarefa são exibidas na parte superior.

   ![tarefa de seleção](assets/select-task.png)

1. Faça uma das seguintes opções:

   * Para delegar a tarefa, toque em **[!UICONTROL Delegar]**. A caixa de diálogo Delegar item é aberta. Selecione um usuário, adicione um comentário e toque em **[!UICONTROL OK]**.
   ![delegate](assets/delegate.png)

   * Para reivindicar a tarefa, toque em **[!UICONTROL Abrir]**. A caixa de diálogo Atribuir a si mesmo é aberta. Toque em **[!UICONTROL Prosseguir]** para reclamar a tarefa. A tarefa reivindicada é exibida com você como o destinatário em sua Caixa de entrada.
   ![reclamação](assets/claim.png)

### Detalhes da Visualização e executar ações no tarefa {#view-details-and-perform-actions-on-tasks}

Ao abrir uma tarefa, você pode visualização os detalhes da tarefa e executar as ações disponíveis. As ações disponíveis para uma tarefa são definidas na etapa Atribuir tarefa do fluxo de trabalho do Forms associado.

1. Toque para selecionar a miniatura da tarefa. As opções para abrir ou delegar a tarefa selecionada são exibidas na parte superior.
1. Toque em **Abrir** para obter detalhes da tarefa da visualização e execute ações. A visualização detalhada da tarefa é aberta. Nesta visualização, você pode visualização detalhes da tarefa e realizar ações na tarefa.

   >[!NOTE]
   >
   >Se uma tarefa for atribuída a um grupo, você deverá reivindicar que ele poderá abri-la em visualização detalhada.

![detalhes da tarefa](assets/task-details.png)

A visualização detalhada da tarefa inclui as seguintes seções:

* Detalhes da Tarefa
* Formulário
* Detalhes do fluxo de trabalho
* Barra de ferramentas Ações

#### Task details {#task-details}

A seção Detalhes da Tarefa exibe informações sobre a tarefa. As informações exibidas dependem das configurações da etapa [](/help/sites-developing/workflows-step-ref.md) Atribuir tarefa no fluxo de trabalho. O exemplo acima exibe a descrição, o status, a data do start e o fluxo de trabalho usados para a tarefa. Também permite anexar um arquivo à tarefa.

#### Formulário {#form}

A guia Formulário na área de conteúdo principal exibe o formulário enviado e os anexos em nível de campo, se houver.

#### Workflow details {#workflow-details}

A guia Detalhes do fluxo de trabalho na parte superior mostra o progresso da tarefa por meio de várias etapas no fluxo de trabalho. Mostra os estágios concluídos, atuais e pendentes da tarefa. As etapas de um fluxo de trabalho são definidas na etapa [](/help/sites-developing/workflows-step-ref.md) Atribuir tarefa do fluxo de trabalho associado.

Além disso, a guia exibe o histórico de tarefas para cada estágio concluído no fluxo de trabalho. Você pode tocar em Detalhes **[!UICONTROL da]** Visualização para uma etapa concluída para saber mais detalhes sobre essa etapa. Ele exibe comentários, anexos de formulário e tarefa, status, datas de start e término e assim por diante sobre a tarefa.

![detalhes do fluxo de trabalho](assets/workflow-details.png)

#### Actions toolbar {#actions-toolbar}

A barra de ferramentas Ações mostra todas as opções disponíveis para a tarefa. Enquanto Salvar, Redefinir e Delegar são ações padrão, outras ações disponíveis são configuradas na etapa [](/help/sites-developing/workflows-step-ref.md)Atribuir tarefa. No exemplo acima, Aprovar e Rejeitar são configurados no fluxo de trabalho.

À medida que você age na tarefa, ela continua mais no fluxo de trabalho.

### Visualização concluída tarefas {#view-completed-tasks}

A Caixa de entrada do AEM exibe somente tarefas ativas. tarefas concluídas não são exibidas na lista. No entanto, você pode usar filtros de Caixa de entrada para filtrar tarefas com base em vários parâmetros, como tipo de tarefa, status, datas de start e término e assim por diante. Para visualização de tarefas concluídas:

1. Na Caixa de entrada do AEM, toque em ![alternar no painel lateral1](assets/toggle-side-panel1.png) para abrir o seletor de filtro.
1. Toque em Status **[!UICONTROL da]** Tarefa e selecione **[!UICONTROL Concluir]**. Todas as tarefas concluídas são exibidas.

   ![filter](assets/filter.png)

1. Toque para selecionar uma tarefa e clique em **[!UICONTROL Abrir]**.

A tarefa é aberta para exibir o documento ou o formulário adaptável associado à tarefa. Para formulários adaptáveis, a tarefa exibe o formulário adaptável somente leitura ou seu documento de registro PDF conforme configurado na guia Formulário/Documento da etapa [do fluxo de trabalho](/help/sites-developing/workflows-step-ref.md)Atribuir Tarefa.

A seção de detalhes da tarefa exibe informações como ação executada, status da tarefa, data do start e data de término.

![tarefa concluída](assets/completed-task.png)

A guia Detalhes **[!UICONTROL do]** fluxo de trabalho mostra cada etapa do fluxo de trabalho. Toque em detalhes **[!UICONTROL da]** Visualização para obter informações detalhadas.

![fluxo de trabalho de tarefa concluído](assets/completed-task-workflow.png)

