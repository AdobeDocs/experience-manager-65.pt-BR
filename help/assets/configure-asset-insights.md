---
title: Configure o Asset Insights para obter análises.
description: Configure o Asset Insights em [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Administrator
feature: Insights de ativos,Relatórios de ativos
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: c07467feb96c25a4bac1916f88f04fdb37979ee1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 6%

---

# Configurar o Asset Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] busca dados de uso em ativos digitais usados por sites de terceiros do  [!DNL Adobe Analytics]. Para permitir que o Asset Insights recupere esses dados e gere insights, primeiro configure o recurso para integrar com [!DNL Adobe Analytics]. Para usar esse recurso, compre a licença [!DNL Adobe Analytics] separadamente. Os clientes em [!DNL Managed Services] recebem [!DNL Analytics] licença fornecida com [!DNL Experience Manager]. Consulte [Descrição do produto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

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
