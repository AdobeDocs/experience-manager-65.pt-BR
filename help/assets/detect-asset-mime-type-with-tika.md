---
title: Detectar o tipo MIME de ativos usando o Apache Tika
description: Ative o Apache Tika para [!DNL Experience Manager Assets] ajudar a detectar o tipo MIME de ativos do fluxo de conteúdo durante a operação de upload em vez da extensão do arquivo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Detectar o tipo MIME de ativos usando [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] detecta o tipo MIME de ativos que você carrega de sua extensão de arquivo.

Se você usar [!DNL Apache Tika] para fazer upload de ativos, [!DNL Assets] detectará o tipo MIME do fluxo de conteúdo durante a operação de upload em vez da extensão do arquivo.

Esse recurso é desativado por padrão. Para ativar o recurso, configure o serviço **[!UICONTROL Day CQ DAM Mime Type]** do [!UICONTROL Configuration Manager].

>[!NOTE]
>
>A detecção de tipo MIME usando a [!DNL Apache Tika] biblioteca é uma operação que consome muitos recursos.

1. Para abrir o console da Web do Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.

1. Na lista de serviços, localize o **[!UICONTROL Dia CQ DAM Mime Type Service]** e clique em **[!UICONTROL Editar]**.

1. Selecione a opção **[!UICONTROL Detectar MIME do conteúdo]** para permitir a análise de ativos carregados para determinar seu tipo MIME ao ignorar extensões de arquivo. Por padrão, essa opção não está selecionada.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Click **[!UICONTROL Save]** to save the changes.
