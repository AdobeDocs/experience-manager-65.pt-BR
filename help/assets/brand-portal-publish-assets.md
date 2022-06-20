---
title: Publicar ativos no Brand Portal
seo-title: Publish assets to Brand Portal
description: Saiba como publicar e cancelar a publicação de ativos no Brand Portal.
seo-description: Learn how to publish and unpublish assets to Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
feature: Brand Portal
role: User
exl-id: 76652a16-cad6-4e95-9e66-41efec452b03
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 42%

---

# Publicar ativos no Brand Portal {#publish-assets-to-brand-portal}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/brandportal/brand-portal-publish-assets.html?lang=en) |

Como administrador do Adobe Experience Manager (AEM) Assets, você pode publicar ativos e pastas na instância do AEM Assets Brand Portal (ou agendar o fluxo de trabalho de publicação para uma data/hora posterior) para sua organização. No entanto, primeiro você deve configurar o AEM Assets com o Brand Portal. Para obter detalhes, consulte [Configurar o AEM Assets com o Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Depois que a replicação for bem-sucedida, você poderá publicar ativos, pastas e Coleções no Brand Portal. Para publicar ativos no Brand Portal, siga estas etapas:

>[!NOTE]
>
>A Adobe recomenda uma publicação escalonada, de preferência durante horários que não sejam de pico, para que o autor do AEM não ocupe recursos excessivos.

1. No console Assets, selecione os ativos/pastas que deseja publicar e clique em **[!UICONTROL Publicação rápida]** na barra de ferramentas.

   Como alternativa, selecione os ativos que deseja publicar no Brand Portal.

   ![publish2bp-2](assets/publish2bp.png)

1. Para publicar os ativos no Brand Portal, as duas opções a seguir estão disponíveis:
   * [Publicar ativos imediatamente](#publish-to-bp-now)
   * [Publicar ativos mais tarde](#publish-to-bp-now)

## Publicar ativos agora {#publish-to-bp-now}

Para publicar os ativos selecionados no Brand Portal, siga um dos procedimentos a seguir:

* Na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**. Em seguida, no menu, selecione **[!UICONTROL Publicar no Brand Portal]**.

* Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**.

   1. Em seguida, da **[!UICONTROL Ação]** select **[!UICONTROL Publicar no Brand Portal]** e de **[!UICONTROL Agendamento]** select **[!UICONTROL Agora]**. Clique em **[!UICONTROL Avançar]**.

   2. Within **[!UICONTROL Escopo]**, confirme a seleção e clique em **[!UICONTROL Publicar no Brand Portal]**.

Será exibida uma mensagem informando que os ativos foram enfileirados para publicação no Brand Portal. Faça logon na interface do Brand Portal para ver os ativos publicados.

## Publicar ativos mais tarde {#publish-to-bp-later}

Para agendar a publicação dos ativos no Brand Portal para uma data ou hora posterior:

1. Depois de selecionar os ativos/pastas para publicar, selecione **[!UICONTROL Gerenciar publicação]** na barra de ferramentas, na parte superior.

1. Ligado **[!UICONTROL Gerenciar publicação]** página, selecione **[!UICONTROL Publicar no Brand Portal]** from **[!UICONTROL Ação]** e selecione **[!UICONTROL Mais tarde]** from **[!UICONTROL Agendamento]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Selecione uma **[!UICONTROL Data de ativação]** e especifique a hora. Clique em **[!UICONTROL Avançar]**.

1. Selecione uma **Data de ativação** e especifique a hora. Clique em **Avançar**.

1. Especifique um **[!UICONTROL Título de fluxo de trabalho]** em **[!UICONTROL Fluxos de trabalho]**. Clique em **[!UICONTROL Publicar mais tarde]**.

   ![publishworkflow](assets/publishworkflow.png)

Agora, faça logon no Brand Portal para ver se os ativos publicados estão disponíveis na interface da Brand Portal.

![bp_landingpage](assets/bp_landingpage.png)
