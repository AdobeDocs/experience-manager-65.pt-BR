---
title: Pastas privadas para compartilhar ativos
description: Saiba como criar uma pasta privada no [!DNL Adobe Experience Manager Assets] site e compartilhá-la com outros usuários e atribuir vários privilégios a eles.
contentOwner: AG
translation-type: tm+mt
source-git-commit: ce43c49f8f7d4509e414554b8f4eba368ff66e95
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---


# Pasta privada em [!DNL Adobe Experience Manager Assets] {#private-folder}

Você pode criar uma pasta privada na interface do [!DNL Adobe Experience Manager Assets] usuário que esteja disponível exclusivamente para você. Você pode compartilhar essa pasta privada com outros usuários e atribuir vários privilégios a eles. Com base no nível de privilégio atribuído, os usuários podem executar várias tarefas na pasta, por exemplo, visualização de ativos na pasta ou editar os ativos.

>[!NOTE]
>
>A pasta privada tem pelo menos um membro com a função Proprietário.

## Criação e compartilhamento de pastas privadas {#create-share-private-folder}

Para criar e compartilhar pasta privada:

1. No [!DNL Assets] console, clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Pasta]** no menu.

   ![Criar pasta de ativos](assets/Create-folder.png)

1. Na caixa de diálogo **[!UICONTROL Criar pasta]** , digite um título e um nome (opcional) para a pasta e selecione a opção **[!UICONTROL Privado]** .

1. Clique em **[!UICONTROL Criar]**. Uma pasta particular é criada.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. To share the folder with other users and the assign privileges to them, select the folder, and click **[!UICONTROL Properties]** from the toolbar.

   ![opção info](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >A pasta não estará visível para nenhum outro usuário até que você a compartilhe.

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Você pode atribuir várias funções, como `Editor`, `Owner`ou `Viewer` ao usuário com quem você compartilha a pasta. Se você atribuir uma `Owner` função ao usuário, este terá `Editor` privilégios na pasta. Além disso, o usuário pode compartilhar a pasta com outras pessoas. Se você atribuir uma `Editor` função, o usuário poderá editar os ativos em sua pasta particular. Se você atribuir uma função de visualizador, o usuário poderá apenas visualização os ativos em sua pasta particular.

   >[!NOTE]
   >
   >A pasta privada tem pelo menos um membro com `Owner` função. Portanto, o administrador não pode remover todos os membros proprietários de uma pasta privada. No entanto, para remover os proprietários existentes (e o próprio administrador) da pasta privada, o administrador deve adicionar outro usuário como proprietário.

1. Clique em **[!UICONTROL Salvar]**. Dependendo da função atribuída, o usuário recebe um conjunto de privilégios em sua pasta particular quando o usuário faz logon em [!DNL Assets].
1. Clique em **[!UICONTROL Ok]** para fechar a mensagem de confirmação.
1. O usuário com quem você compartilha a pasta recebe uma notificação de compartilhamento. Faça logon [!DNL Assets] com as credenciais do usuário para visualização da notificação.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Clique em [!UICONTROL Notificações] para abrir uma lista de notificações.

   ![Lista das notificações](assets/Assets-Notification.png)

1. Clique na entrada da pasta privada compartilhada pelo administrador para abrir a pasta.

>[!NOTE]
>
>Para criar uma pasta privada, você precisa de permissões [de Leitura e Modificação de](/help/sites-administering/security.md#permissions-in-aem) controles de acesso na pasta pai na qual deseja criar uma pasta privada. Se você não for um administrador, essas permissões não serão ativadas para você por padrão em `/content/dam`. Nesse caso, primeiro obtenha essas permissões para a ID/grupo do usuário antes de tentar criar pastas privadas.

## Exclusão de pasta particular {#delete-private-folder}

Você pode excluir uma pasta selecionando a pasta e a opção [!UICONTROL Excluir] no menu superior ou usando a tecla Backspace no teclado.

![opção Excluir no menu superior](assets/delete-option.png)

>[!CAUTION]
>
>Se você excluir uma pasta privada do CRXDE Lite, os grupos de usuários redundantes serão deixados no repositório.

>[!NOTE]
>
>Se você excluir uma pasta usando o método acima da interface do usuário, os grupos de usuários associados também serão excluídos.
>
>No entanto, os grupos de usuários redundantes, não utilizados e gerados automaticamente existentes podem ser removidos do repositório usando o `clean` método em JMX na instância do autor (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).
