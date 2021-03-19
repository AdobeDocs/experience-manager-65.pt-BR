---
title: Detectar o tipo MIME de ativos usando o Apache Tika
description: Ative o Apache Tika para ajudar [!DNL Experience Manager Assets] detectar o tipo MIME de ativos do fluxo de conteúdo durante a operação de upload, em vez da extensão de arquivo.
contentOwner: AG
role: Administrador, Arquiteto
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Detectar tipo MIME de ativos usando [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] detecta o tipo MIME de ativos que você faz upload de sua extensão de arquivo.

Se você usar [!DNL Apache Tika] para fazer upload de ativos, [!DNL Assets] detectará seu tipo MIME do fluxo de conteúdo durante a operação de upload, em vez da extensão de arquivo.

Esse recurso é desativado por padrão. Para ativar o recurso, configure o serviço **[!UICONTROL Day CQ DAM Mime Type]** de [!UICONTROL Configuration Manager].

>[!NOTE]
>
>A detecção de tipo MIME usando a biblioteca [!DNL Apache Tika] é uma operação que consome muitos recursos.

1. Para abrir o console da Web do Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.

1. Na lista de serviços, localize **[!UICONTROL Day CQ DAM Mime Type Service]** e clique em **[!UICONTROL Editar]**.

1. Selecione a opção **[!UICONTROL Detectar MIME do conteúdo]** para habilitar a análise de ativos carregados para determinar seu tipo MIME ao ignorar as extensões de arquivo. Por padrão, essa opção não está selecionada.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Clique em **[!UICONTROL Save]** para salvar as alterações.
