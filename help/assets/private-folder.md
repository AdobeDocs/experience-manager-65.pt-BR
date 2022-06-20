---
title: Pastas privadas para compartilhar ativos
description: Saiba como criar uma pasta privada no [!DNL Adobe Experience Manager Assets] e compartilhá-lo com outros usuários e atribuir vários privilégios a eles.
contentOwner: AG
role: User
feature: Collaboration
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 2%

---

# Pasta privada em [!DNL Adobe Experience Manager Assets] {#private-folder}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/private-folder.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/private-folder.html?lang=en) |

Você pode criar uma pasta privada no [!DNL Adobe Experience Manager Assets] interface do usuário que está disponível exclusivamente para você. Você pode compartilhar essa pasta privada com outros usuários e atribuir vários privilégios a eles. Com base no nível de privilégio atribuído, os usuários podem executar várias tarefas na pasta, por exemplo, visualizar ativos na pasta ou editar os ativos.

>[!NOTE]
>
>A pasta privada tem pelo menos um membro com a função Proprietário.

## Criação e compartilhamento de pasta privada {#create-share-private-folder}

Para criar e compartilhar pasta privada:

1. No [!DNL Assets] , clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Pasta]** no menu .

   ![Criar pasta de ativos](assets/Create-folder.png)

1. No **[!UICONTROL Criar pasta]** , insira um título e nome (opcional) para a pasta e selecione **[!UICONTROL Privado]** opção.

1. Clique em **[!UICONTROL Criar]**. Uma pasta privada é criada.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Para compartilhar a pasta com outros usuários e atribuir privilégios a eles, selecione a pasta e clique em **[!UICONTROL Propriedades]** na barra de ferramentas.

   ![opção de informações](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >A pasta não fica visível para nenhum outro usuário até que você a compartilhe.

1. No **[!UICONTROL Propriedades da pasta]** selecione um usuário na página **[!UICONTROL Adicionar usuário]** , atribua uma função ao usuário na pasta privada e clique em **[!UICONTROL Adicionar]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Você pode atribuir várias funções, como `Editor`, `Owner`ou `Viewer` ao usuário com quem você compartilha a pasta. Se você atribuir uma `Owner` para o usuário, o usuário tem `Editor` na pasta. Além disso, o usuário pode compartilhar a pasta com outras pessoas. Se você atribuir uma `Editor` , o usuário pode editar os ativos em sua pasta privada. Se você atribuir uma função de visualizador, o usuário só poderá visualizar os ativos em sua pasta privada.

   >[!NOTE]
   >
   >A pasta privada tem pelo menos um membro com `Owner` função. Portanto, o administrador não pode remover todos os membros proprietários de uma pasta privada. No entanto, para remover os proprietários existentes (e o próprio administrador) da pasta privada, o administrador deve adicionar outro usuário como proprietário.

1. Clique em **[!UICONTROL Salvar]**. Dependendo da função atribuída, o usuário recebe um conjunto de privilégios em sua pasta privada quando ele faz logon no [!DNL Assets].
1. Clique em **[!UICONTROL Ok]** para fechar a mensagem de confirmação.
1. O usuário com quem você compartilha a pasta recebe uma notificação de compartilhamento. Faça logon em [!DNL Assets] com as credenciais do usuário para exibir a notificação.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Clique em [!UICONTROL Notificações] para abrir uma lista de notificações.

   ![Lista de notificações](assets/Assets-Notification.png)

1. Clique na entrada da pasta privada compartilhada pelo administrador para abrir a pasta.

>[!NOTE]
>
>Para criar uma pasta privada, você precisa ler e modificar [permissões de controle de acesso](/help/sites-administering/security.md#permissions-in-aem) na pasta pai na qual deseja criar uma pasta privada. Se você não for um administrador, essas permissões não serão ativadas para você por padrão em `/content/dam`. Nesse caso, primeiro obtenha essas permissões para sua ID/grupo de usuários antes de tentar criar pastas privadas.

## Exclusão de pasta privada {#delete-private-folder}

Você pode excluir uma pasta selecionando e [!UICONTROL Excluir] no menu superior ou usando a tecla Backspace no teclado.

![excluir opção no menu superior](assets/delete-option.png)

>[!CAUTION]
>
>Se você excluir uma pasta privada do CRXDE Lite, os grupos de usuários redundantes serão deixados no repositório.

>[!NOTE]
>
>Se você excluir uma pasta usando o método acima da interface do usuário, os grupos de usuários associados também serão excluídos.
>
>No entanto, os grupos de usuários redundantes, não utilizados e gerados automaticamente existentes podem ser removidos do repositório usando `clean` no JMX na instância do autor (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).
