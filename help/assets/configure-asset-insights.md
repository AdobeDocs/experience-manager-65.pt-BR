---
title: Configure o Assets Insights para obter análises.
description: Configurar o Assets Insights no [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 6%

---

# Configurar o Assets Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] busca dados de uso em ativos digitais usados por sites de terceiros da [!DNL Adobe Analytics]. Para permitir que o Assets Insights recupere esses dados e gere insights, primeiro configure o recurso para integrar com o [!DNL Adobe Analytics]. Para usar esse recurso em uma instalação local, compre [!DNL Adobe Analytics] licença separadamente. Clientes em [!DNL Managed Services] receive [!DNL Analytics] licença fornecida com [!DNL Experience Manager]. Consulte [Descrição do produto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Os insights são suportados e fornecidos apenas para imagens.

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Clique no cartão **[!UICONTROL Configuração do Insights]**.
1. No assistente, selecione um data center e forneça suas credenciais, incluindo o nome da organização, o nome de usuário e o Segredo compartilhado.

   ![Configurar o Adobe Analytics para o Assets Insights no Experience Manager](assets/insights_config2.png)

   *Figura: Configurar [!DNL Adobe Analytics] para o Assets Insights no [!DNL Experience Manager].*

1. Clique em **[!UICONTROL Autenticar]**.
1. Depois [!DNL Experience Manager] autentica suas credenciais no **[!UICONTROL Conjunto de relatórios]** escolha uma [!DNL Adobe Analytics] conjunto de relatórios de onde você deseja que o Assets Insights busque dados. Clique em **[!UICONTROL Adicionar]**.
1. Depois [!DNL Experience Manager] configure seu conjunto de relatórios, clique em **[!UICONTROL Concluído]**.

## Rastreador de página {#page-tracker}

Depois de configurar o [!DNL Adobe Analytics] , o código do Rastreador de página é gerado para você. Para permitir que o Assets Insights rastreie [!DNL Experience Manager] ativos usados em sites de terceiros, inclua o código do rastreador de página no código do site. Use o [!UICONTROL Rastreador de página] utilitário em [!DNL Experience Manager Assets] para gerar o código do rastreador de página. Para obter mais informações sobre como incluir o código do Rastreador de página em páginas da Web de terceiros, consulte [Usar o rastreador de páginas e o código incorporado em páginas da Web](/help/assets/use-page-tracker.md).

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Na página **[!UICONTROL Navegação]**, clique no cartão do **[!UICONTROL Rastreador de páginas do Insights]**.
1. Clique em **[!UICONTROL Baixar]** para baixar o código do rastreador de página.
