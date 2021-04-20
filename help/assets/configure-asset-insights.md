---
title: Configure o Asset Insights para obter análises.
description: Configure o Asset Insights em [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Administrator
feature: Asset Insights,Asset Reports
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 7%

---


# Configurar o Asset Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] busca dados de uso em ativos digitais usados por sites de terceiros do  [!DNL Adobe Analytics]. Para permitir que o Asset Insights recupere esses dados e gere insights, primeiro configure o recurso para se integrar ao Adobe Analytics.

>[!NOTE]
>
>Os insights são suportados e fornecidos apenas para imagens.

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Clique no cartão **[!UICONTROL Configuração do Insights]**.
1. No assistente, selecione um data center e forneça suas credenciais, incluindo o nome da organização, o nome de usuário e o Segredo compartilhado.

   ![Configurar o Adobe Analytics para o Assets Insights no Experience Manager](assets/insights_config2.png)

   *Figura: Configurar  [!DNL Adobe Analytics] para o Assets Insights no  [!DNL Experience Manager].*

1. Clique em **[!UICONTROL Autenticar]**.
1. Depois que [!DNL Experience Manager] autenticar suas credenciais, na lista **[!UICONTROL Report Suite]**, escolha um conjunto de relatórios [!DNL Adobe Analytics] de onde deseja que o Asset Insights busque dados. Clique em **[!UICONTROL Adicionar]**.
1. Depois de [!DNL Experience Manager] configurar seu conjunto de relatórios, clique em **[!UICONTROL Concluído]**.

## Rastreador de página {#page-tracker}

Depois de configurar sua conta [!DNL Adobe Analytics], o código do Rastreador de página é gerado para você. Para permitir que o Assets Insights rastreie [!DNL Experience Manager] ativos usados em sites de terceiros, inclua o código do rastreador de página no código do site. Use o utilitário [!UICONTROL Rastreador de página] em [!DNL Experience Manager Assets] para gerar o código do rastreador de página. Para obter mais informações sobre como incluir o código do Rastreador de página em páginas da Web de terceiros, consulte [Usar o rastreador de página e o código incorporado em páginas da Web](/help/assets/use-page-tracker.md).

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Na página **[!UICONTROL Navegação]**, clique no cartão do **[!UICONTROL Rastreador de páginas do Insights]**.
1. Clique em **[!UICONTROL Download]** para baixar o código do rastreador de página.
