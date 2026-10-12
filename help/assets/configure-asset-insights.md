---
title: Configure o Assets Insights para obter análises.
description: Configurar o Assets Insights no [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Developer, Admin
feature: Asset Insights,Asset Reports
exl-id: 67be0ae6-5939-40fe-bf8a-b8a2c2f68f15
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: a4e1c1f5-18fc-592e-bfc7-453ce6ae0030
    internal-label: Asset Insights
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c29e3a96-cd2b-4e21-b382-a8279aa04553
    internal-label: Asset reports
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 5%
---
# Configurar o Assets Insights {#configure-asset-insights}

[!DNL Adobe Experience Manager Assets] busca dados de uso sobre ativos digitais usados por sites de terceiros de [!DNL Adobe Analytics]. Para permitir que o Assets Insights recupere esses dados e gere insights, primeiro configure o recurso para integrar com o [!DNL Adobe Analytics]. Para usar este recurso em uma instalação local, compre a licença do [!DNL Adobe Analytics] separadamente. Os clientes no [!DNL Managed Services] recebem a licença [!DNL Analytics] agrupada com o [!DNL Experience Manager]. Consulte [descrição do produto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Os insights só são aceitos e fornecidos para imagens.

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]**.

   ![chlimage_1-72](assets/chlimage_1-210.png)

1. Clique no cartão **[!UICONTROL Configuração do Insights]**.
1. No assistente, selecione um data center e forneça suas credenciais, incluindo o nome da organização, o nome de usuário e o Segredo compartilhado.

   ![Configurar o Adobe Analytics para o Assets Insights no Experience Manager](assets/insights_config2.png)

   *Figura: Configurar o [!DNL Adobe Analytics] para o Assets Insights no [!DNL Experience Manager].*

1. Clique em **[!UICONTROL Autenticar]**.
1. Depois que o [!DNL Experience Manager] autenticar suas credenciais, na lista **[!UICONTROL Conjunto de Relatórios]**, escolha um conjunto de relatórios [!DNL Adobe Analytics] de onde deseja que o Assets Insights busque dados. Clique em **[!UICONTROL Adicionar]**.
1. Depois que [!DNL Experience Manager] configurar seu conjunto de relatórios, clique em **[!UICONTROL Concluído]**.

## Rastreador de páginas {#page-tracker}

Após configurar sua conta do [!DNL Adobe Analytics], o código do Rastreador de páginas é gerado para você. Para permitir que o Assets Insights rastreie [!DNL Experience Manager] ativos usados em sites de terceiros, inclua o código do rastreador de página no código do site. Use o utilitário [!UICONTROL Rastreador de Páginas] em [!DNL Experience Manager Assets] para gerar o código do rastreador de páginas. Para obter mais informações sobre como incluir o código do Rastreador de páginas em páginas da Web de terceiros, consulte [Usar o rastreador de páginas e incorporar o código nas páginas da Web](/help/assets/use-page-tracker.md).

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]**.

   ![chlimage_1-73](assets/chlimage_1-214.png)

1. Na página **[!UICONTROL Navegação]**, clique no cartão do **[!UICONTROL Rastreador de páginas do Insights]**.
1. Clique em **[!UICONTROL Baixar]** para baixar o código do rastreador de página.
