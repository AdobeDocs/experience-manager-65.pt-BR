---
title: Participar de fluxos de trabalho
description: Os fluxos de trabalho normalmente incluem etapas que exigem que uma pessoa execute uma atividade em uma página ou ativo. O fluxo de trabalho seleciona um usuário ou grupo para executar a atividade e lhe atribui um item de trabalho.
uuid: 04dcc8f2-dc11-430f-b0ae-47ef2cb069a2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 1d7a4889-82c5-4096-8567-8f66215a8458
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 52%

---

# Participar de fluxos de trabalho{#participating-in-workflows}

Os fluxos de trabalho normalmente incluem etapas que exigem que uma pessoa execute uma atividade em uma página ou ativo. O fluxo de trabalho seleciona um usuário ou grupo para executar a atividade e lhe atribui um item de trabalho.

## Processando seus itens de trabalho {#processing-your-work-items}

Você pode executar as seguintes ações para processar um item de trabalho:

* **Concluir**

  É possível concluir um item para permitir que o fluxo de trabalho avance para a próxima etapa.

* **Delegar**

  Se uma etapa tiver sido atribuída a você, mas por qualquer motivo você não puder trabalhar nela, é possível delegá-la a outro usuário ou grupo.

  Os usuários disponíveis para delegação dependem de quem recebeu o item de trabalho:

   * Se o item de trabalho foi atribuído a um grupo, os membros do grupo ficarão disponíveis.
   * Se o item de trabalho tiver sido atribuído a um grupo e depois delegado a um usuário, os membros desse grupo e esse usuário estarão disponíveis.
   * Se o item de trabalho foi atribuído a um único usuário, ele não poderá ser delegado.

* **Retroceder**

  Se descobrir que uma etapa, ou uma série de etapas, precisa ser repetida, você poderá retroceder. Isso permite selecionar uma etapa, ocorrida anteriormente no workflow, para reprocessamento. O fluxo de trabalho retornará à etapa especificada e prosseguirá de lá.

## Participar de um fluxo de trabalho {#participating-in-a-workflow}

### Notificações de Ações de Fluxo de Trabalho Atribuídas {#notifications-of-assigned-workflow-actions}

Quando um item de trabalho é atribuído a você (por exemplo, **Aprovar conteúdo**), vários alertas e/ou notificações são exibidos:

* A variável **Status** A coluna do console Sites indica quando uma página está em um workflow:

  ![workflowstatus-1](assets/workflowstatus-1.png)

* Quando você ou um grupo ao qual você pertence é atribuído a um item de trabalho como parte de um fluxo de trabalho, o item de trabalho aparece na Caixa de entrada do fluxo de trabalho do AEM.

  ![workflowinbox](assets/workflowinbox.png)

### Conclusão de uma etapa do participante {#completing-a-participant-step}

Depois de executar a ação indicada, é possível concluir o item de trabalho, permitindo que o fluxo de trabalho continue. Use o procedimento a seguir para concluir o item de trabalho.

1. Selecione a etapa do fluxo de trabalho e clique no link **Concluído** na barra de navegação superior.
1. Na caixa de diálogo resultante, selecione o **Próxima etapa**; ou seja, a próxima etapa a ser executada. Uma lista suspensa mostra todos os destinos apropriados. A **Comentário** também podem ser inseridos.

   ![workflowcomplete](assets/workflowcomplete.png)

   O número de etapas listadas depende do design do modelo de fluxo de trabalho.

1. Clique em **OK** para confirmar a ação

### Delegação de uma etapa do participante {#delegating-a-participant-step}

Use o procedimento a seguir para delegar um item de trabalho.

1. Clique em **Delegar** na barra de navegação superior.
1. Na caixa de diálogo, use a lista suspensa para selecionar a variável **Usuário** para delegar o item de trabalho. Você também pode adicionar um **Comentário**.

   ![workflowdelegate](assets/workflowdelegate.png)

1. Clique em **OK** para confirmar a ação

### Realização de um retrocesso em uma etapa do participante {#performing-step-back-on-a-participant-step}

Use o procedimento a seguir para retroceder.

1. Clique no botão Retroceder na barra de navegação superior.
1. Na caixa de diálogo resultante, selecione a Etapa anterior; ou seja, a etapa a ser executada em seguida, mesmo que seja uma etapa que ocorra anteriormente no fluxo de trabalho. Uma lista suspensa mostra todos os destinos apropriados.

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. Clique em OK para confirmar a ação.
