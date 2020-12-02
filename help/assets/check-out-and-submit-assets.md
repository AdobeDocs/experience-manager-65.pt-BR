---
title: Fazer check-in e check-out de ativos para edição
description: Saiba como fazer check-out dos ativos para edição e check-in deles novamente após a conclusão das alterações.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Arquivos de check-in e check-out no [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] permite que você faça check-out dos ativos para edição e faça check-in deles novamente depois de concluir a realização das alterações. Depois de fazer check-out de um ativo, somente você pode editar, anotar, publicar, mover ou excluir o ativo. Fazer check-out de um ativo bloqueia o ativo. Outros usuários não podem executar nenhuma dessas operações no ativo até que você faça check-in do ativo novamente em [!DNL Assets]. No entanto, eles ainda podem alterar os metadados do ativo bloqueado.

Para poder fazer check-out/check-in de ativos, você precisa ter acesso de gravação neles.

Esse recurso ajuda a impedir que outros usuários substituam as alterações feitas por um autor, onde vários usuários colaboram na edição de workflows entre equipes.

## Verificar ativos {#checking-out-assets}

1. Na interface do usuário [!DNL Assets], selecione o ativo que deseja fazer check-out. Você também pode selecionar vários ativos para fazer check-out.
1. Na barra de ferramentas, clique em **[!UICONTROL Check-out]**.
A opção **[!UICONTROL Check-out]** alterna para **[!UICONTROL Check-in]**.
Para verificar se outros usuários podem editar o ativo que você fez check-out, faça logon como um usuário diferente. Um símbolo de cadeado é exibido na miniatura do ativo que você deu baixa.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Selecione o ativo. Observe que a barra de ferramentas não exibe nenhuma opção que permita editar, anotar, publicar ou excluir o ativo.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   Você pode clicar em **[!UICONTROL Propriedades da Visualização]** para editar os metadados do ativo bloqueado.

1. Clique em **[!UICONTROL Editar]** para abrir o ativo no modo de edição.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Edite o ativo e salve as alterações. Por exemplo, recorte a imagem e salve-a.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   Você também pode optar por anotar ou publicar o ativo.

1. Selecione o ativo editado na interface [!DNL Assets] e clique em **[!UICONTROL Check-in]** na barra de ferramentas. O ativo modificado é feito check-in em [!DNL Assets] e está disponível para outros usuários para edição.

## Verificação forçada em {#forced-check-in}

Os administradores podem fazer check-in de ativos cujo check-out foi feito por outros usuários.

1. Faça logon em [!DNL Assets] como administrador.
1. Na interface do usuário [!DNL Assets], selecione um ou mais ativos cujo check-out foi feito por outros usuários.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Na barra de ferramentas, clique em **[!UICONTROL Liberar Bloqueio]**. O ativo é devolvido e está disponível para edição para outros usuários.

## Práticas recomendadas e limitações {#tips-limitations}

* É possível excluir uma *pasta* que contenha arquivos de ativos com check-out. Antes de excluir uma pasta, verifique se nenhum ativo digital foi retirado pelos usuários.

>[!MORELIKETHIS]
>
>* [Entenda o check-in e o check-out no aplicativo de desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#how-app-works2)
>* [Tutorial em vídeo para entender o check-in e o check-out nos ativos](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

