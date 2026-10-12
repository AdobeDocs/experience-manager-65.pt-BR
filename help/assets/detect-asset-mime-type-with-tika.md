---
title: Detectar tipos MIME de ativos usando o Apache Tika
description: Habilite o Apache Tika para ajudar o [!DNL Experience Manager Assets] a detectar o tipo MIME de ativos do fluxo de conteúdo durante a operação de carregamento em vez da extensão de arquivo.
contentOwner: AG
role: Admin, Developer
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: ed6971a3-2c12-4fd2-81f4-ff329c416250
    internal-label: Metadata
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '167'
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
