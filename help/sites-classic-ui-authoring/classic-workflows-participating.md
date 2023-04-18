---
title: Participar de fluxos de trabalho
description: Os fluxos de trabalho normalmente incluem etapas que exigem que uma pessoa execute uma atividade em uma página ou ativo. O fluxo de trabalho seleciona um usuário ou grupo para executar a atividade e atribui um item de trabalho a essa pessoa ou grupo.
uuid: 04dcc8f2-dc11-430f-b0ae-47ef2cb069a2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 1d7a4889-82c5-4096-8567-8f66215a8458
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 9%

---

# Participar de fluxos de trabalho{#participating-in-workflows}

Os fluxos de trabalho normalmente incluem etapas que exigem que uma pessoa execute uma atividade em uma página ou ativo. O fluxo de trabalho seleciona um usuário ou grupo para executar a atividade e atribui um item de trabalho a essa pessoa ou grupo.

## Processamento dos itens de trabalho {#processing-your-work-items}

Você pode executar as seguintes ações para processar um item de trabalho:

* **Concluir**

   Você pode concluir um item para permitir que o fluxo de trabalho avance para a próxima etapa.

* **Delegar**

   Se uma etapa tiver sido atribuída a você, mas por qualquer motivo você não puder realizar uma ação, poderá delegar a etapa a outro usuário ou grupo.

   Os usuários que estão disponíveis para delegação dependem de quem recebeu o item de trabalho:

   * Se o item de trabalho foi atribuído a um grupo, os membros do grupo estão disponíveis.
   * Se o item de trabalho tiver sido atribuído a um grupo e depois delegado a um usuário, os membros desse grupo e esse usuário estarão disponíveis.
   * Se o item de trabalho foi atribuído a um único usuário, ele não pode ser delegado.

* **Retroceder**

   Se você descobrir que uma etapa, ou uma série de etapas, precisa ser repetida, é possível retroceder. Isso permite selecionar uma etapa, que ocorreu anteriormente no fluxo de trabalho, para reprocessamento. O workflow retorna à etapa especificada e prossegue a partir daí.

## Participar de um fluxo de trabalho {#participating-in-a-workflow}

### Notificações de ações de fluxo de trabalho atribuídas {#notifications-of-assigned-workflow-actions}

Quando um item de trabalho é atribuído a você (por exemplo, **Aprovar conteúdo**), vários alertas e/ou notificações são exibidos:

* O **Status** coluna do console Sites indica quando uma página está em um fluxo de trabalho:

   ![workflowstatus-1](assets/workflowstatus-1.png)

* Quando você, ou um grupo ao qual você pertence, recebe um item de trabalho como parte de um fluxo de trabalho, o item de trabalho é exibido na Caixa de entrada AEM do fluxo de trabalho.

   ![caixa de fluxo de trabalho](assets/workflowinbox.png)

### Conclusão de uma etapa do participante {#completing-a-participant-step}

Depois de realizar a ação indicada, é possível concluir o item de trabalho, permitindo que o fluxo de trabalho continue. Use o procedimento a seguir para concluir o item de trabalho.

1. Selecione a etapa do fluxo de trabalho e clique no botão **Concluído** na barra de navegação superior.
1. Na caixa de diálogo resultante, selecione a variável **Próxima etapa**; ou seja, a etapa a ser executada em seguida. Uma lista suspensa mostra todos os destinos apropriados. A **Comentário** também pode ser inserido.

   ![workflow](assets/workflowcomplete.png)

   O número de etapas listadas depende do design do modelo de fluxo de trabalho.

1. Clique em **OK** para confirmar a ação.

### Delegação de uma etapa do participante {#delegating-a-participant-step}

Use o procedimento a seguir para delegar um item de trabalho.

1. Clique no botão **Delegar** na barra de navegação superior.
1. Na caixa de diálogo, use a lista suspensa para selecionar a variável **Usuário** para delegar o item de trabalho. Você também pode adicionar uma **Comentário**.

   ![workflowdelegate](assets/workflowdelegate.png)

1. Clique em **OK** para confirmar a ação.

### Retroceder em uma etapa do participante {#performing-step-back-on-a-participant-step}

Use o procedimento a seguir para retroceder.

1. Clique no botão Retroceder na barra de navegação superior.
1. Na caixa de diálogo resultante, selecione a Etapa anterior; ou seja, a etapa para executar a próxima - mesmo que seja uma etapa que ocorre anteriormente no fluxo de trabalho. Uma lista suspensa mostra todos os destinos apropriados.

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. Clique em OK para confirmar a ação.
