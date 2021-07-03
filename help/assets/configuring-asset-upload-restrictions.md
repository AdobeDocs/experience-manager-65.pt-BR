---
title: Configurar restrições de upload de ativos
description: 'Restringir o tipo de ativos (arquivos) que os usuários podem fazer upload '
contentOwner: AG
role: Developer, Admin, Architect
feature: Gerenciamento de ativos,Fazer upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 15%

---

# Configurar restrições de upload de ativos {#configuring-asset-upload-restrictions}

Você pode configurar [!DNL Adobe Experience Manager Assets] para restringir o tipo de ativos que os usuários podem fazer upload. Ajuda a evitar uploads acidentais de formato indesejado e arquivos mal-intencionados. O serviço `Day CQ DAM Asset Upload Restriction` permite controlar o tipo de arquivos que os usuários podem fazer upload. Por padrão, [!DNL Assets] permite que os usuários façam upload de ativos de todos os tipos MIME. No entanto, você pode configurar o serviço para restringir usuários a fazerem upload de arquivos apenas de tipos MIME específicos.

1. Abra o console da Web do Configuration Manager. Acesso `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o serviço **[!UICONTROL Day CQ DAM Asset Upload Restriction]** no modo de Edição. Por padrão, a opção **Allow all MIME** é selecionada, o que permite que os usuários façam upload de arquivos de todos os tipos MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Para impedir que usuários façam upload de arquivos apenas de determinados tipos MIME, desmarque a opção **[!UICONTROL Permitir todos os tipos MIME]** e especifique os tipos MIME permitidos nos campos **[!UICONTROL MIMEs de ativos permitidos (regex)]** usando expressões regulares.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Clique em **[!UICONTROL Save]** para salvar as alterações. Se você especificar cadeias de caracteres MIME para os tipos MIME permitidos, a operação de upload falhará todos os ativos de tipo MIME que não correspondam às cadeias de caracteres MIME configuradas nesses campos.
