---
title: Revisar ativos e coleções de pastas
description: Configure workflows de revisão para ativos em uma pasta ou coleção e compartilhe-os com revisores ou parceiros criativos para obter feedback.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# Revisar ativos e coleções de pastas {#review-folder-assets-and-collections}

Configure workflows de revisão para ativos em uma pasta ou coleção e compartilhe-os com revisores ou parceiros criativos para obter feedback.

Os ativos Adobe Experience Manager (AEM) permitem configurar um fluxo de trabalho de revisão ad hoc para ativos em uma pasta ou coleção e compartilhá-lo com revisores ou parceiros criativos para buscar feedback.

Você pode associar o fluxo de trabalho de revisão a um projeto ou criar uma tarefa de revisão independente.

Depois de compartilhar os ativos, os revisores podem aprová-los ou rejeitá-los. As notificações são enviadas em vários estágios do fluxo de trabalho para notificar recipient pretendidos sobre a conclusão de várias tarefas. Por exemplo, quando você compartilha uma pasta ou coleção, o revisor recebe uma notificação de que uma pasta/coleção foi compartilhada para revisão.

Depois que o revisor concluir a revisão (aprova ou rejeita ativos), você receberá uma notificação de conclusão da revisão.

## Criar uma tarefa de revisão para pastas {#creating-a-review-task-for-folders}

1. Na interface do usuário Ativos, selecione a pasta para a qual deseja criar uma tarefa de revisão.
1. From the toolbar, click **[!UICONTROL Create Review Task]** to open the **[!UICONTROL Review Task]** page. If you cannot see the option in the toolbar, click **[!UICONTROL More]** and then select the option.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Opcional) Na lista **[!UICONTROL Projeto]** , selecione o projeto ao qual deseja associar a tarefa de revisão. Por padrão, a opção **[!UICONTROL Nenhum]** está selecionada. Se você não quiser associar qualquer projeto à tarefa de revisão, mantenha essa seleção.

   >[!NOTE]
   >
   >Somente os projetos para os quais você tem permissões no nível do Editor (ou superior) estão visíveis na lista **[!UICONTROL Projetos]** .

1. Insira um nome para a tarefa de revisão e selecione um aprovador na lista **[!UICONTROL Atribuir]** .

   >[!NOTE]
   >
   >Os membros/grupos do projeto selecionado estão disponíveis como aprovadores na lista **[!UICONTROL Atribuir]** .

1. Informe uma descrição, a prioridade da tarefa e a data de vencimento da tarefa de revisão.

   ![tarefa_details](assets/task_details.png)

1. Na guia Avançado, digite um rótulo a ser usado para criar o URI.

   ![review_name](assets/review_name.png)

1. Click **[!UICONTROL Submit]**, and then click **[!UICONTROL Done]** to close the confirmation message. Uma notificação para a nova tarefa é enviada ao aprovador.
1. Faça logon nos ativos AEM como aprovador e navegue até a interface do usuário dos ativos. Para aprovar ativos, clique em **[!UICONTROL Notificações]** e selecione a tarefa de revisão na lista.

   ![Notificação de ativos](assets/aemAssetsNotification.png)

1. In the **[!UICONTROL Review Task]** page, examine the details of the review task, and then click **[!UICONTROL Review]**.
1. In the **[!UICONTROL Review Task]** page, select assets, and click **[!UICONTROL Approve/Reject]** to approve or reject, as appropriate.

   ![review_tarefa](assets/review_task.png)

1. Click **[!UICONTROL Complete]** from the toolbar. Na caixa de diálogo, digite um comentário e clique em **[!UICONTROL Concluir]** para confirmar.
1. Navegue até a interface do usuário Ativos e abra a pasta. Os ícones de status de aprovação dos ativos são exibidos na visualização do cartão e na visualização da lista.

   **Exibição de cartão**

   ![Rever o estado como visto na visualização do cartão](assets/chlimage_1-404.png)

   **Exibição de lista**

   ![Status da revisão conforme visto na visualização da lista](assets/review_status_listview.png)

## Criar uma tarefa de revisão para coleções {#creating-a-review-task-for-collections}

1. Na página Coleções, selecione a coleção para a qual deseja criar uma tarefa de revisão.
1. From the toolbar, click **[!UICONTROL Create Review Task]** to open the **[!UICONTROL Review Task]** page. If you cannot see the option on the toolbar, click **[!UICONTROL More]** and then select the option.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Opcional) Na lista **[!UICONTROL Projeto]** , selecione o projeto ao qual deseja associar a tarefa de revisão. Por padrão, a opção **[!UICONTROL Nenhum]** está selecionada. Se você não quiser associar qualquer projeto à tarefa de revisão, mantenha essa seleção.

   >[!NOTE]
   >
   >Somente os projetos para os quais você tem permissões no nível do Editor (ou superior) estão visíveis na lista **[!UICONTROL Projetos]** .

1. Insira um nome para a tarefa de revisão e selecione um aprovador na lista **[!UICONTROL Atribuir]** .

   >[!NOTE]
   >
   >Os membros/grupos do projeto selecionado estão disponíveis como aprovadores na lista **[!UICONTROL Atribuir]** .

1. Informe uma descrição, a prioridade da tarefa e a data de vencimento da tarefa de revisão.

   ![tarefa_details-collection](assets/task_details-collection.png)

1. Click **[!UICONTROL Submit]**, and then click **[!UICONTROL Done]** to close the confirmation message. Uma notificação para a nova tarefa é enviada ao aprovador.
1. Faça logon nos ativos AEM como aprovador e navegue até o console Ativos. Para aprovar ativos, clique em **[!UICONTROL Notificações]** e selecione a tarefa de revisão na lista.
1. In the **[!UICONTROL Review Task]** page, examine the details of the review task, and then click **[!UICONTROL Review]**.
1. Todos os ativos na coleção estão visíveis na página de revisão. Selecione os ativos e clique em **[!UICONTROL Aprovar/Rejeitar]** para aprovar ou rejeitar ativos, conforme apropriado.

   ![review_tarefa_collection](assets/review_task_collection.png)

1. Click **[!UICONTROL Complete]** from the toolbar. Na caixa de diálogo, digite um comentário e clique em **[!UICONTROL Concluir]** para confirmar.
1. Navegue até o console Coleções e abra a coleção. Os ícones de status de aprovação dos ativos são exibidos nas visualizações Cartão e Lista.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *Figura: visualização da placa.*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *Figura: visualização da Lista.*
