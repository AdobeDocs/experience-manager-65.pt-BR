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
translation-type: tm+mt
source-git-commit: 4c00385984a0ac315a60c768cb517832ab4289b4

---


# Publish assets to Brand Portal {#publish-assets-to-brand-portal}

Como administrador dos ativos Adobe Experience Manager (AEM), você pode publicar ativos e pastas na instância do AEM Assets Brand Portal (ou agendar o fluxo de trabalho de publicação para uma data/hora posterior) para sua organização. No entanto, você deve primeiro configurar os ativos AEM com o Portal da marca. Para obter detalhes, consulte [Configurar ativos AEM com o Portal](/help/assets/configure-aem-assets-with-brand-portal.md)da marca.

Depois que a replicação for bem-sucedida, você poderá publicar ativos, pastas e coleções no Brand Portal. Para publicar ativos no Brand Portal, siga estas etapas:

>[!NOTE]
>
>A Adobe recomenda uma publicação escalonada, de preferência durante horas que não sejam de pico, para que o autor do AEM não ocupe recursos excessivos.

1. No console Ativos, selecione os ativos/pastas que deseja publicar e clique na opção Publicação **** rápida na barra de ferramentas.

   Como alternativa, selecione os ativos que deseja publicar no Brand Portal.

   ![publish2bp-2](assets/publish2bp.png)

1. Para publicar os ativos no Brand Portal, duas opções estão disponíveis:
   * [Publicar ativos imediatamente](#publish-to-bp-now)
   * [Publicar ativos mais tarde](#publish-to-bp-now)

## Publicar ativos agora {#publish-to-bp-now}

Para publicar os ativos selecionados no Brand Portal, execute um dos procedimentos a seguir:

* Na barra de ferramentas, selecione Publicação **[!UICONTROL rápida]**. Em seguida, no menu, selecione **[!UICONTROL Publicar no Brand Portal]**.

* Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**.

   1. Em seguida, na **[!UICONTROL Ação]** , selecione **[!UICONTROL Publicar no Brand Portal]** e, em **[!UICONTROL Agendamento]** , selecione **[!UICONTROL Agora]**. Clique em **[!UICONTROL Avançar]**.

   2. Dentro do **[!UICONTROL Escopo]**, confirme sua seleção e clique em **[!UICONTROL Publicar no Portal]** da Marca.

Será exibida uma mensagem informando que os ativos foram enfileirados para publicação no Brand Portal. Faça logon na interface do Brand Portal para ver os ativos publicados.

## Publicar ativos mais tarde {#publish-to-bp-later}

Para agendar a publicação dos ativos no Brand Portal para uma data ou hora posterior:

1. Depois de selecionar os ativos/ pastas a serem publicados, selecione **[!UICONTROL Gerenciar publicação]** na barra de ferramentas na parte superior.

1. Na página **[!UICONTROL Gerenciar publicação]** , selecione **[!UICONTROL Publicar no portal]** da marca em **[!UICONTROL Ação]** e selecione **[!UICONTROL Mais tarde]** em **[!UICONTROL Agendamento]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Selecione uma data **[!UICONTROL de]** ativação e especifique a hora. Clique em **[!UICONTROL Avançar]**.

1. Selecione uma data **de** ativação e especifique a hora. Clique em **Avançar**.

1. Especifique um título **[!UICONTROL de]** Fluxo de trabalho em **[!UICONTROL Fluxos de trabalho]**. Clique em **[!UICONTROL Publicar mais tarde]**.

   ![publishworkflow](assets/publishworkflow.png)

Agora, faça logon no Brand Portal para verificar se os recursos publicados estão disponíveis na interface do Brand Portal.

![bp_landing_page](assets/bp_landing_page.png)

