---
title: Detectar tipos MIME de ativos usando o Apache Tika
description: Ativar o Apache Tika para ajudar [!DNL Experience Manager Assets] detecte o tipo MIME de ativos do fluxo de conteúdo durante a operação de upload em vez da extensão de arquivo.
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Detectar tipos MIME de ativos usando [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] O detecta o tipo MIME de ativos que você faz upload a partir da extensão de arquivo.

Se você usar [!DNL Apache Tika] para fazer upload de ativos, [!DNL Assets] O detecta o tipo MIME do fluxo de conteúdo durante a operação de upload em vez da extensão de arquivo.

Esse recurso está desativado por padrão. Para habilitar o recurso, configure o **[!UICONTROL Tipo de Mime do DAM CQ do dia]** serviço de [!UICONTROL Gerenciador de configurações].

>[!NOTE]
>
>Detecção de tipo MIME usando o [!DNL Apache Tika] A biblioteca do é uma operação que consome muitos recursos.

1. Para abrir o console da Web do Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.

1. Na lista de serviços, localize **[!UICONTROL Serviço de tipo DAM Mime do DAM do Day CQ]** e clique em **[!UICONTROL Editar]**.

1. Selecione o **[!UICONTROL Detectar MIME do conteúdo]** opção para habilitar a análise de ativos carregados para determinar seu tipo MIME ao ignorar as extensões de arquivo. Por padrão, essa opção não está selecionada.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.
