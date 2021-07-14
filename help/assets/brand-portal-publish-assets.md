---
title: Publicar ativos no Brand Portal
seo-title: Publicar ativos no Brand Portal
description: Saiba como publicar e cancelar a publicação de ativos no Brand Portal.
seo-description: Saiba como publicar e cancelar a publicação de ativos no Brand Portal.
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
source-git-commit: 39a44c4b706f68d2f4f220811aa9bcc80aec55e4
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 43%

---

# Publicar ativos no Brand Portal {#publish-assets-to-brand-portal}

Como administrador do Adobe Experience Manager (AEM) Assets, você pode publicar ativos e pastas na instância do AEM Assets Brand Portal (ou agendar o fluxo de trabalho de publicação para uma data/hora posterior) para sua organização. No entanto, primeiro você deve configurar o AEM Assets com o Brand Portal. Para obter detalhes, consulte [Configurar o AEM Assets com o Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Depois que a replicação for bem-sucedida, você poderá publicar ativos, pastas e Coleções no Brand Portal. Para publicar ativos no Brand Portal, siga estas etapas:

>[!NOTE]
>
>A Adobe recomenda uma publicação escalonada, de preferência durante horários que não sejam de pico, para que o autor do AEM não ocupe recursos excessivos.

1. No console Assets, selecione os ativos/pastas que deseja publicar e clique na opção **[!UICONTROL Publicação rápida]** na barra de ferramentas.

   Como alternativa, selecione os ativos que deseja publicar no Brand Portal.

   ![publish2bp-2](assets/publish2bp.png)

1. Para publicar os ativos no Brand Portal, as duas opções a seguir estão disponíveis:
   * [Publicar ativos imediatamente](#publish-to-bp-now)
   * [Publicar ativos mais tarde](#publish-to-bp-now)

## Publicar ativos agora {#publish-to-bp-now}

Para publicar os ativos selecionados no Brand Portal, siga um dos procedimentos a seguir:

* Na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**. Em seguida, no menu, selecione **[!UICONTROL Publish to Brand Portal]**.

* Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**.

   1. Em seguida, no **[!UICONTROL Action]** selecione **[!UICONTROL Publish to Brand Portal]** e, em **[!UICONTROL Scheduling]**, selecione **[!UICONTROL Now]**. Clique em **[!UICONTROL Avançar]**.

   2. Dentro de **[!UICONTROL Scope]**, confirme a seleção e clique em **[!UICONTROL Publish to Brand Portal]**.

Será exibida uma mensagem informando que os ativos foram enfileirados para publicação no Brand Portal. Faça logon na interface do Brand Portal para ver os ativos publicados.

## Publicar ativos mais tarde {#publish-to-bp-later}

Para agendar a publicação dos ativos no Brand Portal para uma data ou hora posterior:

1. Depois de selecionar os ativos/pastas para publicar, selecione **[!UICONTROL Gerenciar publicação]** na barra de ferramentas na parte superior.

1. Na página **[!UICONTROL Gerenciar publicação]**, selecione **[!UICONTROL Publicar no Brand Portal]** a partir de **[!UICONTROL Ação]** e selecione **[!UICONTROL Mais Tarde]** a partir de **[!UICONTROL Programação]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Selecione uma **[!UICONTROL Data de ativação]** e especifique a hora. Clique em **[!UICONTROL Avançar]**.

1. Selecione uma **Data de ativação** e especifique a hora. Clique em **Avançar**.

1. Especifique um **[!UICONTROL Título de fluxo de trabalho]** em **[!UICONTROL Fluxos de trabalho]**. Clique em **[!UICONTROL Publicar mais tarde]**.

   ![publishworkflow](assets/publishworkflow.png)

Agora, faça logon no Brand Portal para ver se os ativos publicados estão disponíveis na interface da Brand Portal.

![bp_landingpage](assets/bp_landingpage.png)
