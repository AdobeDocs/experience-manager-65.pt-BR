---
title: Pastas privadas para compartilhar ativos
description: Saiba como criar uma pasta privada no  [!DNL Adobe Experience Manager Assets] e compartilhá-la com outros usuários e atribuir vários privilégios a eles.
contentOwner: AG
translation-type: tm+mt
source-git-commit: ce43c49f8f7d4509e414554b8f4eba368ff66e95
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---


# Pasta privada em [!DNL Adobe Experience Manager Assets] {#private-folder}

Você pode criar uma pasta particular na interface do usuário [!DNL Adobe Experience Manager Assets] que esteja disponível exclusivamente para você. Você pode compartilhar essa pasta privada com outros usuários e atribuir vários privilégios a eles. Com base no nível de privilégio atribuído, os usuários podem executar várias tarefas na pasta, por exemplo, visualização de ativos na pasta ou editar os ativos.

>[!NOTE]
>
>A pasta privada tem pelo menos um membro com a função Proprietário.

## Criação e compartilhamento de pasta particular {#create-share-private-folder}

Para criar e compartilhar pasta privada:

1. No console [!DNL Assets], clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Pasta]** no menu.

   ![Criar pasta de ativos](assets/Create-folder.png)

1. Na caixa de diálogo **[!UICONTROL Criar pasta]**, digite um título e um nome (opcional) para a pasta e selecione a opção **[!UICONTROL Privado]**.

1. Clique em **[!UICONTROL Criar]**. Uma pasta particular é criada.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Para compartilhar a pasta com outros usuários e atribuir privilégios a eles, selecione a pasta e clique em **[!UICONTROL Propriedades]** na barra de ferramentas.

   ![opção info](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >A pasta não estará visível para nenhum outro usuário até que você a compartilhe.

1. Na página **[!UICONTROL Propriedades da pasta]**, selecione um usuário da lista **[!UICONTROL Adicionar usuário]**, atribua uma função ao usuário em sua pasta particular e clique em **[!UICONTROL Adicionar]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Você pode atribuir várias funções, como `Editor`, `Owner` ou `Viewer` ao usuário com quem você compartilha a pasta. Se você atribuir uma função `Owner` ao usuário, este terá `Editor` privilégios na pasta. Além disso, o usuário pode compartilhar a pasta com outras pessoas. Se você atribuir uma função `Editor`, o usuário poderá editar os ativos em sua pasta particular. Se você atribuir uma função de visualizador, o usuário poderá apenas visualização os ativos em sua pasta particular.

   >[!NOTE]
   >
   >A pasta privada tem pelo menos um membro com a função `Owner`. Portanto, o administrador não pode remover todos os membros proprietários de uma pasta privada. No entanto, para remover os proprietários existentes (e o próprio administrador) da pasta privada, o administrador deve adicionar outro usuário como proprietário.

1. Clique em **[!UICONTROL Salvar]**. Dependendo da função atribuída, o usuário recebe um conjunto de privilégios em sua pasta particular quando o usuário faz logon em [!DNL Assets].
1. Clique em **[!UICONTROL Ok]** para fechar a mensagem de confirmação.
1. O usuário com quem você compartilha a pasta recebe uma notificação de compartilhamento. Faça logon em [!DNL Assets] com as credenciais do usuário para visualização da notificação.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Clique em [!UICONTROL Notificações] para abrir uma lista de notificações.

   ![Lista das notificações](assets/Assets-Notification.png)

1. Clique na entrada da pasta privada compartilhada pelo administrador para abrir a pasta.

>[!NOTE]
>
>Para criar uma pasta privada, você precisa ler e modificar [permissões de controle de acesso](/help/sites-administering/security.md#permissions-in-aem) na pasta pai na qual deseja criar uma pasta particular. Se você não for um administrador, essas permissões não serão ativadas para você por padrão em `/content/dam`. Nesse caso, primeiro obtenha essas permissões para a ID/grupo do usuário antes de tentar criar pastas privadas.

## Exclusão de pasta privada {#delete-private-folder}

Você pode excluir uma pasta selecionando a pasta e selecionando a opção [!UICONTROL Excluir] no menu superior, ou usando a tecla Backspace no teclado.

![opção Excluir no menu superior](assets/delete-option.png)

>[!CAUTION]
>
>Se você excluir uma pasta privada do CRXDE Lite, os grupos de usuários redundantes serão deixados no repositório.

>[!NOTE]
>
>Se você excluir uma pasta usando o método acima da interface do usuário, os grupos de usuários associados também serão excluídos.
>
>No entanto, os grupos de usuários redundantes, não utilizados e gerados automaticamente existentes podem ser removidos do repositório usando o método `clean` no JMX na instância do autor (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).
