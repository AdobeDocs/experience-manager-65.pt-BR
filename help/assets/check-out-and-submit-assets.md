---
title: Fazer check-in e check-out de arquivos em [!DNL Assets]
description: Saiba como fazer check-out de ativos para edição e check-in depois que as alterações forem concluídas.
contentOwner: AG
role: User
feature: Asset Management
exl-id: 544ef73c-4e4b-433f-a173-fdf1c8f45d8e
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 3%

---

# Arquivos de check-in e check-out em [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/check-out-and-submit-assets.html?lang=en) |
| AEM 6.5 | Este artigo |

[!DNL Adobe Experience Manager Assets] O permite fazer check-out de ativos para edição e check-in depois que você concluir as alterações. Depois de fazer check-out de um ativo, somente você pode editar, anotar, publicar, mover ou excluir o ativo. Fazer o check-out de um ativo bloqueia o ativo. Outros usuários não podem executar nenhuma dessas operações no ativo até que você faça check-in do ativo novamente em [!DNL Assets]. No entanto, eles ainda podem alterar os metadados do ativo bloqueado.

Para fazer check-out/check-in de ativos, é necessário ter acesso de gravação a eles.

Este recurso ajuda a impedir que outros usuários substituam as alterações feitas por um autor, em que vários usuários colaboram na edição de workflows entre equipes.

## Fazer check-out dos ativos {#checking-out-assets}

1. No [!DNL Assets] selecione o ativo que deseja retirar. Você também pode selecionar vários ativos para fazer check-out.
1. Na barra de ferramentas, clique em **[!UICONTROL Check-out]**. A variável **[!UICONTROL Check-out]** opção alterna para **[!UICONTROL Check-in]**.
Para verificar se outros usuários podem editar o ativo do qual você fez check-out, faça logon como um usuário diferente. Um símbolo de bloqueio é exibido na miniatura do ativo do qual você fez check-out.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Selecione o ativo. Observe que a barra de ferramentas não exibe nenhuma opção que permita editar, anotar, publicar ou excluir o ativo.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   Para editar os metadados do ativo bloqueado, clique em **[!UICONTROL Propriedades da exibição]**.

1. Clique em **[!UICONTROL Editar]** para abrir o ativo no modo de edição.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Edite o ativo e salve as alterações. Por exemplo, recorte a imagem e salve.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   Também é possível optar por anotar ou publicar o ativo.

1. Selecione o ativo editado na [!DNL Assets] e clique em **[!UICONTROL Check-in]** na barra de ferramentas. O ativo modificado foi submetido a check-in para [!DNL Assets] e está disponível para edição por outros usuários.

## Check-in forçado {#forced-check-in}

Os administradores podem fazer check-in de ativos que passaram por check-out por outros usuários.

1. Efetue logon no [!DNL Assets] como administrador.
1. No [!DNL Assets] interface do usuário selecione um ou mais ativos que foram verificados por outros usuários.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Na barra de ferramentas, clique em **[!UICONTROL Liberar Bloqueio]**. É feito check-in do ativo e ele fica disponível para edição para outros usuários.

## Práticas recomendadas e limitações {#tips-limitations}

* É possível excluir um *pasta* que contém arquivos de ativos com check-out. Antes de excluir uma pasta, verifique se nenhum ativo digital foi retirado por usuários.

>[!MORELIKETHIS]
>
>* [Entender o check-in e o check-out [!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [Vídeo tutorial para entender o check-in e o check-out [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)
