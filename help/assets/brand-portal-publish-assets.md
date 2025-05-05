---
title: Ativos do Publish para o Brand Portal
description: Saiba como publicar e desfazer a publicação de ativos no Brand Portal.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 76652a16-cad6-4e95-9e66-41efec452b03
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: cbf8a5ac22049b3372a8282b9c061d7abeacc5dc
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 40%

---

# Ativos do Publish para o Brand Portal {#publish-assets-to-brand-portal}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

Como administrador do Adobe Experience Manager (AEM) Assets, você pode publicar ativos e pastas na instância do AEM Assets Brand Portal (ou agendar o fluxo de trabalho de publicação para uma data/hora posterior) para sua organização. No entanto, primeiro você deve configurar o AEM Assets com o Brand Portal. Para obter detalhes, consulte [Configurar o AEM Assets com o Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Após o sucesso da replicação, você pode publicar ativos, pastas e coleções no Brand Portal. Para publicar ativos no Brand Portal, siga estas etapas:

>[!NOTE]
>
>A Adobe recomenda uma publicação escalonada, de preferência durante horários que não sejam de pico, para que o autor do AEM não ocupe recursos excessivos.

1. No console Assets, selecione os ativos/pastas que deseja publicar e clique na opção **[!UICONTROL Publish Rápido]** na barra de ferramentas.

   Como alternativa, selecione os ativos que deseja publicar no Brand Portal.

   ![publish2bp-2](assets/publish2bp.png)

1. Para publicar os ativos no Brand Portal, as duas opções a seguir estão disponíveis:
   * [Ativos do Publish imediatamente](#publish-to-bp-now)
   * [Ativos do Publish mais tarde](#publish-to-bp-now)

## Ativos do Publish agora {#publish-to-bp-now}

Para publicar os ativos selecionados no Brand Portal, siga um dos procedimentos a seguir:

* Na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**. Em seguida, no menu, selecione **[!UICONTROL Publish to Brand Portal]**.

* Na barra de ferramentas, selecione **[!UICONTROL Gerenciar publicação]**.

   1. Em seguida, em **[!UICONTROL Ação]**, selecione **[!UICONTROL Publish para Brand Portal]** e, em **[!UICONTROL Agendamento]**, selecione **[!UICONTROL Agora]**. Clique em **[!UICONTROL Avançar]**.

   2. No **[!UICONTROL Escopo]**, confirme sua seleção e clique em **[!UICONTROL Publish to Brand Portal]**.

Será exibida uma mensagem informando que os ativos foram enfileirados para publicação no Brand Portal. Faça logon na interface do Brand Portal para ver os ativos publicados.

## Ativos do Publish mais tarde {#publish-to-bp-later}

Para agendar a publicação dos ativos no Brand Portal para uma data ou hora posterior:

1. Depois de selecionar os ativos/pastas a serem publicados, selecione **[!UICONTROL Gerenciar publicação]** na barra de ferramentas na parte superior.

1. Na página **[!UICONTROL Gerenciar Publicação]**, selecione **[!UICONTROL Publish para Brand Portal]** em **[!UICONTROL Ação]** e selecione **[!UICONTROL Depois]** em **[!UICONTROL Agendamento]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. Selecione uma **[!UICONTROL Data de ativação]** e especifique a hora. Clique em **[!UICONTROL Avançar]**.

1. Selecione uma **Data de ativação** e especifique a hora. Clique em **Avançar**.

1. Especifique um **[!UICONTROL Título de fluxo de trabalho]** em **[!UICONTROL Fluxos de trabalho]**. Clique em **[!UICONTROL Publicar mais tarde]**.

   ![publishworkflow](assets/publishworkflow.png)

Agora, faça logon no Brand Portal para ver se os ativos publicados estão disponíveis na interface do Brand Portal.

![bp_landingpage](assets/bp_landingpage.png)

## Exibir arquivo ou pasta publicada no Brand Portal {#view-published-file-folder}

1. Faça logon na interface do Brand Portal para ver os ativos publicados (dependendo da data ou hora agendadas).

   ![bp_landingpage](assets/bp_landingpage.png)

1. Alterne para o Modo de exibição de lista ![Modo de exibição de lista](assets/list-view.svg) para ver o status de publicação atual do ativo.

<!--2. On the [Asset Reports page](#https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/admin/asset-reports), you can see the current state of the report job, for example, Success, Failed, Queued, or Scheduled.-->

![status do relatório gerado](assets/report-status.JPG)
