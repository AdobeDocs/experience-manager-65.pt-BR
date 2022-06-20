---
title: Revisar ativos e coleções de pastas
description: Configure fluxos de trabalho de revisão para ativos em uma pasta ou coleção e compartilhe-os com revisores ou parceiros criativos para buscar feedback.
contentOwner: AG
feature: Collaboration, Collections
role: User
exl-id: 23c90e10-aa03-450e-9fb0-2f5be0c5066b
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 5%

---

# Revisar ativos e coleções de pastas {#review-folder-assets-and-collections}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/bulk-approval.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/bulk-approval.html?lang=en) |

Configure fluxos de trabalho de revisão para ativos em uma pasta ou coleção e compartilhe-os com revisores ou parceiros criativos para buscar feedback.

[!DNL Adobe Experience Manager Assets] permite configurar um fluxo de trabalho de revisão ad hoc para ativos em uma pasta ou coleção e compartilhá-lo com revisores ou parceiros criativos para buscar feedback.

Você pode associar o fluxo de trabalho de revisão a um projeto ou criar uma tarefa de revisão independente.

Após compartilhar os ativos, os revisores podem aprová-los ou rejeitá-los. As notificações são enviadas em vários estágios do workflow para notificar os recipients pretendidos sobre a conclusão de várias tarefas. Por exemplo, quando você compartilha uma pasta ou coleção, o revisor recebe uma notificação de que uma pasta/coleção foi compartilhada para revisão.

Depois que o revisor concluir a revisão (aprova ou rejeita ativos), você receberá uma notificação de conclusão da revisão.

## Criar uma tarefa de revisão para pastas {#creating-a-review-task-for-folders}

1. No [!DNL Assets] interface do usuário, selecione a pasta para a qual deseja criar uma tarefa de revisão.
1. Na barra de ferramentas, clique em **[!UICONTROL Criar tarefa de revisão]** ![criar tarefa de revisão](assets/do-not-localize/create-review-task.png) para abrir o **[!UICONTROL Tarefa de revisão]** página. Se não conseguir ver a opção na barra de ferramentas, clique em **[!UICONTROL Mais]** e selecione a opção .

1. (Opcional) Na **[!UICONTROL Projeto]** selecione o projeto ao qual deseja associar a tarefa de revisão. Por padrão, a variável **[!UICONTROL Nenhum]** está selecionada. Se não quiser associar um projeto à tarefa de revisão, mantenha essa seleção.

   >[!NOTE]
   >
   >Somente os projetos para os quais você tem permissões de nível de Editor (ou superior) estão visíveis na variável **[!UICONTROL Projetos]** lista.

1. Insira um nome para a tarefa de revisão e selecione um aprovador na **[!UICONTROL Atribuir a]** lista.

   >[!NOTE]
   >
   >Os membros/grupos do projeto selecionado estão disponíveis como aprovadores no **[!UICONTROL Atribuir a]** lista.

1. Insira uma descrição, a prioridade da tarefa e a data de vencimento da tarefa de revisão.

   ![task_details](assets/task_details.png)

1. Na guia Advanced , insira um rótulo a ser usado para criar o URI.

   ![nome_da_revisão](assets/review_name.png)

1. Clique em **[!UICONTROL Enviar]** e, em seguida, clique em **[!UICONTROL Concluído]** para fechar a mensagem de confirmação. Uma notificação para a nova tarefa é enviada ao aprovador.
1. Faça logon em [!DNL Assets] como Aprovador e navegue até a [!DNL Assets] IU. Para aprovar ativos, clique em **[!UICONTROL Notificações]** e selecione a tarefa de revisão na lista.

   ![Notificação de ativos](assets/aemAssetsNotification.png)

1. No **[!UICONTROL Tarefa de revisão]** examine os detalhes da tarefa de revisão e clique em **[!UICONTROL Revisão]**.
1. No **[!UICONTROL Tarefa de revisão]** selecione ativos e clique em **[!UICONTROL Aprovar/Rejeitar]** aprovar ou rejeitar, conforme o caso.

   ![review_task](assets/review_task.png)

1. Clique em **[!UICONTROL Concluído]** na barra de ferramentas. Na caixa de diálogo, insira um comentário e clique em  **[!UICONTROL Concluído]** para confirmar.
1. Navegue até o [!DNL Assets] e abra a pasta. Os ícones de status de aprovação dos ativos aparecem na exibição de cartão e na exibição de lista.

   **Exibição de cartão**

   ![Revisar o status como visto na exibição de cartão](assets/chlimage_1-404.png)

   **Exibição de lista**

   ![Revisar o status como visto na exibição em lista](assets/review_status_listview.png)

## Criar uma tarefa de revisão para coleções {#creating-a-review-task-for-collections}

1. Na página Coleções , selecione a coleção para a qual deseja criar uma tarefa de revisão.
1. Na barra de ferramentas, clique em **[!UICONTROL Criar tarefa de revisão]** ![criar tarefa de revisão](assets/do-not-localize/create-review-task.png) para abrir o **[!UICONTROL Tarefa de revisão]** página. Se não conseguir ver a opção na barra de ferramentas, clique em **[!UICONTROL Mais]** e selecione a opção .

1. (Opcional) Na **[!UICONTROL Projeto]** selecione o projeto ao qual deseja associar a tarefa de revisão. Por padrão, a variável **[!UICONTROL Nenhum]** está selecionada. Se não quiser associar um projeto à tarefa de revisão, mantenha essa seleção.

   >[!NOTE]
   >
   >Somente os projetos para os quais você tem permissões de nível de Editor (ou superior) estão visíveis na variável **[!UICONTROL Projetos]** lista.

1. Insira um nome para a tarefa de revisão e selecione um aprovador na **[!UICONTROL Atribuir a]** lista.

   >[!NOTE]
   >
   >Os membros/grupos do projeto selecionado estão disponíveis como aprovadores no **[!UICONTROL Atribuir a]** lista.

1. Insira uma descrição, a prioridade da tarefa e a data de vencimento da tarefa de revisão.

   ![task_details-collection](assets/task_details-collection.png)

1. Clique em **[!UICONTROL Enviar]** e, em seguida, clique em **[!UICONTROL Concluído]** para fechar a mensagem de confirmação. Uma notificação para a nova tarefa é enviada ao aprovador.
1. Faça logon em [!DNL Assets] como Aprovador e navegue até a [!DNL Assets] console. Para aprovar ativos, clique em **[!UICONTROL Notificações]** e selecione a tarefa de revisão na lista.
1. No **[!UICONTROL Tarefa de revisão]** examine os detalhes da tarefa de revisão e clique em **[!UICONTROL Revisão]**.
1. Todos os ativos na coleção estão visíveis na página de revisão. Selecione os ativos e clique em **[!UICONTROL Aprovar/Rejeitar]** para aprovar ou rejeitar ativos, conforme apropriado.

   ![review_task_collection](assets/review_task_collection.png)

1. Clique em **[!UICONTROL Concluído]** na barra de ferramentas. Na caixa de diálogo, insira um comentário e clique em **[!UICONTROL Concluído]** para confirmar.
1. Navegue até o console Coleções e abra a coleção. Os ícones de status de aprovação dos ativos são exibidos nas exibições Cartão e Lista.

   ![collection_revisewstatuscardview](assets/collection_reviewstatuscardview.png)

   *Figura: Exibição de cartão.*

   ![collection_revisewstatuslistview](assets/collection_reviewstatuslistview.png)

   *Figura: Exibição de lista.*
