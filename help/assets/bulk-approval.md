---
title: Revisar ativos e coleções de pastas
description: Configure fluxos de trabalho de revisão para ativos em uma pasta ou coleção e compartilhe-os com revisores ou parceiros criativos para buscar feedback.
contentOwner: AG
feature: Collaboration, Collections
role: User
exl-id: 23c90e10-aa03-450e-9fb0-2f5be0c5066b
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 6%

---

# Revisar ativos e coleções de pastas {#review-folder-assets-and-collections}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/bulk-approval.html?lang=en) |
| AEM 6.5 | Este artigo |

Configure fluxos de trabalho de revisão para ativos em uma pasta ou coleção e compartilhe-os com revisores ou parceiros criativos para buscar feedback.

O [!DNL Adobe Experience Manager Assets] permite configurar um fluxo de trabalho de revisão ad hoc para ativos em uma pasta ou coleção e compartilhá-lo com revisores ou parceiros criativos para buscar feedback.

Você pode associar o fluxo de trabalho de revisão a um projeto ou criar uma tarefa de revisão independente.

Depois que você compartilhar os ativos, os revisores podem aprová-los ou rejeitá-los. As notificações são enviadas em vários estágios do fluxo de trabalho para notificar os destinatários sobre a conclusão de várias tarefas. Por exemplo, quando você compartilha uma pasta ou coleção, o revisor recebe uma notificação de que uma pasta/coleção foi compartilhada para revisão.

Depois que o revisor concluir a revisão (aprovar ou rejeitar ativos), você receberá uma notificação de conclusão da revisão.

## Criar uma tarefa de revisão para pastas {#creating-a-review-task-for-folders}

1. Na interface do usuário do [!DNL Assets], selecione a pasta para a qual deseja criar uma tarefa de revisão.
1. Na barra de ferramentas, clique em **[!UICONTROL Criar tarefa de revisão]** ![criar tarefa de revisão](assets/do-not-localize/create-review-task.png) para abrir a página **[!UICONTROL Tarefa de revisão]**. Se você não conseguir ver a opção na barra de ferramentas, clique em **[!UICONTROL Mais]** e selecione a opção.

1. (Opcional) Na lista **[!UICONTROL Projeto]**, selecione o projeto ao qual deseja associar a tarefa de revisão. Por padrão, a opção **[!UICONTROL Nenhuma]** está selecionada. Se não quiser associar nenhum projeto à tarefa de revisão, mantenha essa seleção.

   >[!NOTE]
   >
   >Somente os projetos para os quais você tem permissões de nível Editor (ou superior) estão visíveis na lista **[!UICONTROL Projetos]**.

1. Insira um nome para a tarefa de revisão e selecione um aprovador na lista **[!UICONTROL Atribuir a]**.

   >[!NOTE]
   >
   >Os membros/grupos do projeto selecionado estão disponíveis como aprovadores na lista **[!UICONTROL Atribuir a]**.

1. Insira uma descrição, a prioridade da tarefa e a data de vencimento da tarefa de revisão.

   ![detalhes_da_tarefa](assets/task_details.png)

1. Na guia Advanced, insira um rótulo a ser usado para criar o URI.

   ![nome_da_revisão](assets/review_name.png)

1. Clique em **[!UICONTROL Enviar]** e em **[!UICONTROL Concluído]** para fechar a mensagem de confirmação. Uma notificação para a nova tarefa é enviada ao aprovador.
1. Faça logon em [!DNL Assets] como um Aprovador e navegue até a interface do usuário do [!DNL Assets]. Para aprovar ativos, clique em **[!UICONTROL Notificações]** e selecione a tarefa de revisão na lista.

   ![Notificação do Assets](assets/aemAssetsNotification.png)

1. Na página **[!UICONTROL Tarefa de Revisão]**, examine os detalhes da tarefa de revisão e clique em **[!UICONTROL Revisar]**.
1. Na página **[!UICONTROL Tarefa de revisão]**, selecione os ativos e clique em **[!UICONTROL Aprovar/Rejeitar]** para aprovar ou rejeitar, conforme apropriado.

   ![revisar_tarefa](assets/review_task.png)

1. Clique em **[!UICONTROL Concluir]** na barra de ferramentas. Na caixa de diálogo, insira um comentário e clique em **[!UICONTROL Concluir]** para confirmar.
1. Navegue até a interface de usuário [!DNL Assets] e abra a pasta. Os ícones de status de aprovação dos ativos aparecem na exibição de cartão e na exibição de lista.

   **Exibição de cartão**

   ![Revisar status como visto na exibição de cartão](assets/chlimage_1-404.png)

   **Exibição de lista**

   ![Revisar status como visto na exibição de lista](assets/review_status_listview.png)

## Criar uma tarefa de revisão para coleções {#creating-a-review-task-for-collections}

1. Na página Coleções, selecione a coleção para a qual deseja criar uma tarefa de revisão.
1. Na barra de ferramentas, clique em **[!UICONTROL Criar tarefa de revisão]** ![criar tarefa de revisão](assets/do-not-localize/create-review-task.png) para abrir a página **[!UICONTROL Tarefa de revisão]**. Se você não conseguir ver a opção na barra de ferramentas, clique em **[!UICONTROL Mais]** e selecione a opção.

1. (Opcional) Na lista **[!UICONTROL Projeto]**, selecione o projeto ao qual deseja associar a tarefa de revisão. Por padrão, a opção **[!UICONTROL Nenhuma]** está selecionada. Se não quiser associar nenhum projeto à tarefa de revisão, mantenha essa seleção.

   >[!NOTE]
   >
   >Somente os projetos para os quais você tem permissões de nível Editor (ou superior) estão visíveis na lista **[!UICONTROL Projetos]**.

1. Insira um nome para a tarefa de revisão e selecione um aprovador na lista **[!UICONTROL Atribuir a]**.

   >[!NOTE]
   >
   >Os membros/grupos do projeto selecionado estão disponíveis como aprovadores na lista **[!UICONTROL Atribuir a]**.

1. Insira uma descrição, a prioridade da tarefa e a data de vencimento da tarefa de revisão.

   ![coleção_de_detalhes_da_tarefa](assets/task_details-collection.png)

1. Clique em **[!UICONTROL Enviar]** e em **[!UICONTROL Concluído]** para fechar a mensagem de confirmação. Uma notificação para a nova tarefa é enviada ao aprovador.
1. Faça logon em [!DNL Assets] como um Aprovador e navegue até o console [!DNL Assets]. Para aprovar ativos, clique em **[!UICONTROL Notificações]** e selecione a tarefa de revisão na lista.
1. Na página **[!UICONTROL Tarefa de Revisão]**, examine os detalhes da tarefa de revisão e clique em **[!UICONTROL Revisar]**.
1. Todos os ativos na coleção estão visíveis na página de revisão. Selecione os ativos e clique em **[!UICONTROL Aprovar/Rejeitar]** para aprovar ou rejeitar ativos, conforme apropriado.

   ![review_task_collection](assets/review_task_collection.png)

1. Clique em **[!UICONTROL Concluir]** na barra de ferramentas. Na caixa de diálogo, insira um comentário e clique em **[!UICONTROL Concluir]** para confirmar.
1. Navegue até o console Coleções e abra a coleção. Os ícones de status de aprovação dos ativos aparecem nas exibições Cartão e Lista.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *Figura: exibição de cartão.*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *Figura: exibição em lista.*
