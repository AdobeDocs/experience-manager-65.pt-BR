---
title: Configure o Asset Insights para obter análises.
description: Configure o Asset Insights no [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 7%

---


# Configurar insights de ativos {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] busca dados de uso em ativos digitais usados por sites de terceiros [!DNL Adobe Analytics]. Para permitir que o Asset Insights recupere esses dados e gere insights, configure primeiro o recurso para integrar-se à Adobe Analytics.

>[!NOTE]
>
>Os insights só são suportados e fornecidos para imagens.

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Clique no cartão **[!UICONTROL Configuração do Insights]**.
1. No assistente, selecione um centro de dados e forneça suas credenciais, incluindo o nome de sua organização, o nome de usuário e o Segredo compartilhado.

   ![Configurar o Adobe Analytics para insights do Assets no Experience Manager](assets/insights_config2.png)

   *Figura: Configurar[!DNL Adobe Analytics]para insights do Assets em[!DNL Experience Manager].*

1. Clique em **[!UICONTROL Autenticar]**.
1. Depois de [!DNL Experience Manager] autenticar suas credenciais, na lista **[!UICONTROL Report Suite]** , escolha um conjunto de [!DNL Adobe Analytics] relatórios de onde deseja que o Asset Insights busque dados. Clique em **[!UICONTROL Adicionar]**.
1. Depois de [!DNL Experience Manager] configurar seu conjunto de relatórios, clique em **[!UICONTROL Concluído]**.

## Rastreador de páginas {#page-tracker}

Depois de configurar sua [!DNL Adobe Analytics] conta, o código do rastreador de páginas é gerado para você. Para permitir que o Assets Insights rastreie [!DNL Experience Manager] ativos usados em sites de terceiros, inclua o código do rastreador de página no código do site. Use o utilitário [!UICONTROL do rastreador] de páginas em [!DNL Experience Manager Assets] para gerar o código do rastreador de páginas. Para obter mais informações sobre como incluir o código do Rastreador de páginas em páginas da Web de terceiros, consulte [Usar o rastreador de páginas e incorporar o código em páginas](/help/assets/touch-ui-using-page-tracker.md)da Web.

1. In [!DNL Experience Manager], click **[!UICONTROL Tools]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Na página **[!UICONTROL Navegação]**, clique no cartão do **[!UICONTROL Rastreador de páginas do Insights]**.
1. Clique em **[!UICONTROL Download]** para baixar o código do rastreador de página.
