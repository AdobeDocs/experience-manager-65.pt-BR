---
title: Detectar o tipo MIME de ativos usando o Apache Tika
description: Ativar o Apache Tika para ajudar [!DNL Experience Manager Assets] detecte o tipo MIME de ativos do fluxo de conteúdo durante a operação de upload em vez da extensão de arquivo.
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Detectar tipo MIME de ativos usando [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

Normalmente, [!DNL Adobe Experience Manager Assets] O detecta o tipo MIME de ativos que você faz upload da extensão de arquivo.

Se você usar [!DNL Apache Tika] para fazer upload de ativos, [!DNL Assets] O detecta o tipo MIME do fluxo de conteúdo durante a operação de upload, em vez da extensão de arquivo.

Esse recurso é desativado por padrão. Para ativar o recurso, configure a variável **[!UICONTROL Tipo Mime Day CQ DAM]** de [!UICONTROL Gerenciador de configuração].

>[!NOTE]
>
>Detecção de tipo MIME usando o [!DNL Apache Tika] biblioteca é uma operação que usa muitos recursos.

1. Para abrir o console da Web do Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.

1. Na lista de serviços, localize **[!UICONTROL Serviço de Tipo Mime Day CQ DAM]** e clique em **[!UICONTROL Editar]**.

1. Selecione o **[!UICONTROL Detectar MIME do conteúdo]** para permitir a análise de ativos carregados para determinar seu tipo MIME ao ignorar extensões de arquivo. Por padrão, essa opção não está selecionada.

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.
