---
title: Configurar insights de ativos
description: Configurar insights de ativos nos ativos AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 44daaa61f7328e79fd4e11a503b0eef3ff9ffb56

---


# Configurar insights de ativos {#configure-asset-insights}

O Adobe Experience Manager (AEM) Assets obtém dados de uso em ativos AEM usados por sites de terceiros do Adobe Analytics. Para permitir que o Asset Insights recupere esses dados e gere insights, configure primeiro o recurso para integrar-se ao Adobe Analytics.

>[!NOTE]
>
>Os insights só são suportados e fornecidos para imagens.

1. No AEM, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Clique no cartão **[!UICONTROL Configuração do Insights]**.
1. No assistente, selecione um centro de dados e forneça suas credenciais, incluindo o nome de sua organização, o nome de usuário e o segredo compartilhado.

   ![Configurar o Adobe Analytics para insights de ativos no AEM](assets/insights_config2.png)

   *Figura:Configurar o Adobe Analytics para insights de ativos no AEM*

1. Clique/toque em **[!UICONTROL Autenticar]**.
1. Depois que o AEM autenticar suas credenciais, na lista **[!UICONTROL Report Suite]** , escolha um conjunto de relatórios do Adobe Analytics de onde deseja que o Asset Insights busque dados. Clique em **[!UICONTROL Adicionar]**.
1. Depois que o AEM configurar seu conjunto de relatórios, clique/toque em **[!UICONTROL Concluído]**.

## Rastreador de páginas {#page-tracker}

Depois de configurar sua conta do Adobe Analytics, o código do rastreador de páginas é gerado para você. Para ativar o Assets Insights para rastrear ativos AEM usados em sites de terceiros, inclua o código do rastreador de página no código do site. Use o utilitário do rastreador de páginas nos ativos AEM para gerar o código do rastreador de páginas. Para obter mais informações sobre como incluir o código do Rastreador de páginas em páginas da Web de terceiros, consulte [Usar o rastreador de páginas e incorporar o código em páginas](/help/assets/touch-ui-using-page-tracker.md)da Web.

1. No AEM, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Na página **[!UICONTROL Navegação]**, clique no cartão do **[!UICONTROL Rastreador de páginas do Insights]**.
1. Clique em **[!UICONTROL Download]** para baixar o código do rastreador de página.
