---
title: Criar e compartilhar uma pasta privada no AEM
description: Saiba como criar uma pasta privada nos ativos Adobe Experience Manager (AEM) e compartilhá-la com outros usuários e atribuir vários privilégios a eles.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# Compartilhamento de pasta particular {#private-folder-sharing}

Você pode criar uma pasta privada na interface do usuário dos ativos Adobe Experience Manager (AEM) que está disponível exclusivamente para você. Você pode compartilhar essa pasta privada com outros usuários e atribuir vários privilégios a eles. Com base no nível de privilégio atribuído, os usuários podem executar várias tarefas na pasta, por exemplo, visualização de ativos na pasta ou editar os ativos.

>[!NOTE]
>
> A pasta privada tem pelo menos um membro com a função Proprietário.


1. No console Ativos, clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Pasta]** no menu.

   ![Criar pasta de ativos](assets/Create-folder.png)

1. Na caixa de diálogo **[!UICONTROL Criar pasta]** , digite um título e nome (opcional) para a pasta e selecione **[!UICONTROL Privado]**.

   ![Marque a caixa de seleção Privado para tornar a pasta privada](assets/private-folder.png)

1. Clique em **[!UICONTROL Criar]**. Uma pasta particular é criada na interface do usuário.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. To share the folder with other users and the assign privileges to them, select the folder, and click the **[!UICONTROL Properties]** icon from the toolbar.

   ![chlimage_1-414](assets/chlimage_1-414.png)

   >[!NOTE]
   >
   >A pasta não estará visível para nenhum outro usuário até que você a compartilhe.

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Você pode atribuir várias funções, como Editor, Proprietário ou Visualizador ao usuário com quem você compartilha a pasta. Se você atribuir uma função Proprietário ao usuário, este terá privilégios de Editores na pasta. Além disso, o usuário pode compartilhar a pasta com outras pessoas. Se você atribuir uma função de Editor, o usuário poderá editar os ativos em sua pasta particular. Se você atribuir uma função de Visualizador, o usuário poderá apenas visualização os ativos em sua pasta particular.

   >[!NOTE]
   >
   > A pasta privada tem pelo menos um membro com a função Proprietário. Portanto, o administrador não pode remover todos os membros proprietários de uma pasta privada. No entanto, para remover proprietários existentes (e o próprio administrador) da pasta privada, o administrador deve adicionar outro usuário como proprietário.

1. Clique em **[!UICONTROL Salvar]**. Dependendo da função atribuída, o usuário recebe um conjunto de privilégios em sua pasta particular quando o usuário faz logon nos ativos AEM.
1. Clique em **[!UICONTROL Ok]** para fechar a mensagem de confirmação.
1. O usuário com quem você compartilha a pasta recebe uma notificação de compartilhamento. Faça logon nos ativos AEM com as credenciais do usuário para visualização a notificação.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Clique no ícone Notificação para abrir a lista de notificações.

   ![Lista das notificações](assets/Assets-Notification.png)

1. Clique na entrada da pasta privada compartilhada pelo administrador para abrir a pasta.

>[!NOTE]
>
>Para poder criar uma pasta privada, você precisa de permissões de Ler e Editar ACL na pasta pai na qual deseja criar uma pasta privada. Se você não for um administrador, essas permissões não serão ativadas para você por padrão em `/content/dam`. Nesse caso, primeiro obtenha essas permissões para sua ID/grupo de usuários antes de tentar criar pastas privadas ou configurações de pastas de visualização.
