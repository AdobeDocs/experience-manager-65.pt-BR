---
title: Configurar restrições de upload de ativos
description: 'Restringir o tipo de ativos (arquivos) que os usuários podem carregar '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 15%

---


# Configurar restrições de upload de ativos {#configuring-asset-upload-restrictions}

Você pode configurar [!DNL Adobe Experience Manager Assets] para restringir o tipo de ativos que os usuários podem carregar. Ajuda a impedir carregamentos acidentais de formato indesejado e arquivos mal-intencionados. O serviço `Day CQ DAM Asset Upload Restriction` permite controlar o tipo de arquivos que os usuários podem carregar. Por padrão, [!DNL Assets] permite que os usuários façam upload de ativos de todos os tipos MIME. No entanto, você pode configurar o serviço para restringir usuários a carregarem somente arquivos de tipos MIME específicos.

1. Abra o console da Web do Configuration Manager. Acesso `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o serviço **[!UICONTROL Day CQ DAM Asset Upload Restriction]** no modo Editar. Por padrão, a opção **Permitir todos os MIME** está selecionada, o que permite que os usuários carreguem arquivos de todos os tipos MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Para restringir usuários a fazer upload de arquivos de determinados tipos MIME apenas, desmarque a opção **[!UICONTROL Permitir todos os tipos MIME]** e especifique os tipos MIME permitidos nos campos **[!UICONTROL MIMEs de ativos permitidos (regex)]** usando expressões regulares.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações. Se você especificar cadeias de caracteres MIME para os tipos MIME permitidos, a operação de upload falhará todos os ativos de tipo MIME que não correspondam às cadeias de caracteres MIME configuradas nesses campos.
