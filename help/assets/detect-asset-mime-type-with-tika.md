---
title: Detectar tipos MIME de ativos usando o Apache Tika
description: Habilite o Apache Tika para ajudar [!DNL Experience Manager Assets] a detectar o tipo MIME de ativos do fluxo de conteúdo durante a operação de carregamento, em vez da extensão de arquivo.
contentOwner: AG
role: Admin, Developer
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 3%

---

# Detectar tipo MIME de ativos usando [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, o [!DNL Adobe Experience Manager Assets] detecta o tipo MIME de ativos que você carrega por meio da extensão de arquivo.

Se você usar o [!DNL Apache Tika] para carregar ativos, o [!DNL Assets] detectará o tipo MIME do fluxo de conteúdo durante a operação de carregamento, em vez da extensão de arquivo.

Esse recurso está desativado por padrão. Para habilitar o recurso, configure o serviço **[!UICONTROL Day CQ DAM Mime Type]** no [!UICONTROL Configuration Manager].

>[!NOTE]
>
>A detecção de tipo MIME usando a biblioteca [!DNL Apache Tika] é uma operação que consome muitos recursos.

1. Para abrir o console Web do Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.

1. Na lista de serviços, localize o **[!UICONTROL Day CQ DAM Mime Type Service]** e clique em **[!UICONTROL Editar]**.

1. Selecione a opção **[!UICONTROL Detectar MIME do conteúdo]** para habilitar a análise de ativos carregados para determinar seu tipo MIME ao ignorar as extensões de arquivo. Por padrão, essa opção não está selecionada.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.
