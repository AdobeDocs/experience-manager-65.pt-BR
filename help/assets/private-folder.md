---
title: Pastas privadas para compartilhar ativos
description: Saiba como criar uma pasta privada no  [!DNL Adobe Experience Manager Assets] e compartilhá-la com outros usuários e atribuir vários privilégios a eles.
contentOwner: AG
role: Profissional
feature: Colaboração
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 1%

---


# Pasta privada em [!DNL Adobe Experience Manager Assets] {#private-folder}

Você pode criar uma pasta privada na interface do usuário [!DNL Adobe Experience Manager Assets] que está disponível exclusivamente para você. Você pode compartilhar essa pasta privada com outros usuários e atribuir vários privilégios a eles. Com base no nível de privilégio atribuído, os usuários podem executar várias tarefas na pasta, por exemplo, visualizar ativos na pasta ou editar os ativos.

>[!NOTE]
>
>A pasta privada tem pelo menos um membro com a função Proprietário.

## Criação e compartilhamento de pasta privada{#create-share-private-folder}

Para criar e compartilhar pasta privada:

1. No console [!DNL Assets], clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Pasta]** no menu.

   ![Criar pasta de ativos](assets/Create-folder.png)

1. Na caixa de diálogo **[!UICONTROL Create Folder]**, insira um título e nome (opcional) para a pasta e selecione a opção **[!UICONTROL Private]**.

1. Clique em **[!UICONTROL Criar]**. Uma pasta privada é criada.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Para compartilhar a pasta com outros usuários e atribuir privilégios a eles, selecione a pasta e clique em **[!UICONTROL Properties]** na barra de ferramentas.

   ![opção de informações](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >A pasta não fica visível para nenhum outro usuário até que você a compartilhe.

1. Na página **[!UICONTROL Propriedades da pasta]**, selecione um usuário na lista **[!UICONTROL Adicionar usuário]**, atribua uma função ao usuário na pasta privada e clique em **[!UICONTROL Adicionar]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Você pode atribuir várias funções, como `Editor`, `Owner` ou `Viewer` ao usuário com o qual compartilha a pasta. Se você atribuir uma função `Owner` ao usuário, ele terá privilégios `Editor` na pasta. Além disso, o usuário pode compartilhar a pasta com outras pessoas. Se você atribuir uma função `Editor`, o usuário poderá editar os ativos em sua pasta privada. Se você atribuir uma função de visualizador, o usuário só poderá visualizar os ativos em sua pasta privada.

   >[!NOTE]
   >
   >A pasta privada tem pelo menos um membro com a função `Owner`. Portanto, o administrador não pode remover todos os membros proprietários de uma pasta privada. No entanto, para remover os proprietários existentes (e o próprio administrador) da pasta privada, o administrador deve adicionar outro usuário como proprietário.

1. Clique em **[!UICONTROL Salvar]**. Dependendo da função atribuída, o usuário recebe um conjunto de privilégios em sua pasta privada quando ele faz logon em [!DNL Assets].
1. Clique em **[!UICONTROL Ok]** para fechar a mensagem de confirmação.
1. O usuário com quem você compartilha a pasta recebe uma notificação de compartilhamento. Faça logon em [!DNL Assets] com as credenciais do usuário para exibir a notificação.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Clique em [!UICONTROL Notifications] para abrir uma lista de notificações.

   ![Lista de notificações](assets/Assets-Notification.png)

1. Clique na entrada da pasta privada compartilhada pelo administrador para abrir a pasta.

>[!NOTE]
>
>Para criar uma pasta privada, você precisa ler e modificar [permissões de controle de acesso](/help/sites-administering/security.md#permissions-in-aem) na pasta pai na qual deseja criar uma pasta privada. Se você não for um administrador, essas permissões não serão ativadas para você por padrão em `/content/dam`. Nesse caso, primeiro obtenha essas permissões para sua ID/grupo de usuários antes de tentar criar pastas privadas.

## Exclusão de pasta privada {#delete-private-folder}

Você pode excluir uma pasta selecionando a pasta e a opção [!UICONTROL Delete] no menu superior ou usando a tecla Backspace no teclado.

![excluir opção no menu superior](assets/delete-option.png)

>[!CAUTION]
>
>Se você excluir uma pasta privada do CRXDE Lite, os grupos de usuários redundantes serão deixados no repositório.

>[!NOTE]
>
>Se você excluir uma pasta usando o método acima da interface do usuário, os grupos de usuários associados também serão excluídos.
>
>No entanto, os grupos de usuários redundantes, não utilizados e gerados automaticamente existentes podem ser removidos do repositório usando o método `clean` no JMX na instância do autor (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).
