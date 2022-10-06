---
title: Publicar pastas no Brand Portal
seo-title: Publish folders to Brand Portal
description: Saiba como publicar e desfazer a publicação de pastas no Brand Portal.
seo-description: Learn how to publish and unpublish folders to Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
feature: Brand Portal
role: User
exl-id: 92a156f0-ce2a-4c83-bd57-0c29efbf784f
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 38%

---

# Publicar pastas no Brand Portal{#publish-folders-to-brand-portal}

Como administrador do Adobe Experience Manager (AEM) Assets, você pode publicar ativos e pastas na instância do AEM Assets Brand Portal (ou agendar o fluxo de trabalho de publicação para uma data/hora posterior) para sua organização. No entanto, primeiro você deve integrar o AEM Assets com o Brand Portal. Para obter detalhes, consulte [Configurar o AEM Assets com o Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Após publicar um ativo ou uma pasta, ele fica disponível para os usuários no Brand Portal.

Se você fizer modificações subsequentes no ativo ou pasta original no AEM Assets, as alterações não serão refletidas no Brand Portal até que você publique novamente o ativo ou a pasta. Esse recurso garante que as alterações de trabalho em andamento não estejam disponíveis no Brand Portal. Somente as alterações aprovadas publicadas por um administrador são disponibilizadas no Brand Portal.

## Publicar pastas no Brand Portal {#publish-folders-to-brand-portal-1}

1. Na interface do AEM Assets, passe o mouse sobre a pasta desejada e selecione **Publicar** nas ações rápidas.

   Como alternativa, selecione a pasta desejada e siga as etapas adicionais.

   ![publish2bp](assets/publish2bp.png)

1. **Publicar pastas agora**

   Para publicar as pastas selecionadas no Brand Portal, siga um dos procedimentos a seguir:

   * Na barra de ferramentas, selecione **Publicação rápida**. Em seguida, no menu, selecione **Publicar no Brand Portal**.

   * Na barra de ferramentas, selecione **Gerenciar publicação**.
   1. De **Ação** select **Publicar no Brand Portal**, de **Agendamento** select **Agora** e clique em **Próximo.**
   1. Confirme sua seleção no **Escopo** e clique em **Publicar no Brand Portal**.

   Será exibida uma mensagem informando que a pasta foi colocada na fila para publicação no Brand Portal. Faça logon na interface do Brand Portal para ver a pasta publicada.

   **Publicar pastas mais tarde**

   Para agendar a publicação no fluxo de trabalho do Brand Portal de pastas de ativos para uma data ou hora posterior:

   1. Depois de selecionar os ativos/pastas para publicar, selecione **Gerenciar publicação** na barra de ferramentas, na parte superior.
   1. De **Ação** select **Publicar no Brand Portal**, de **Agendamento** select **Mais tarde**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Selecione uma **Data de ativação** e especifique a hora. Clique em **Avançar**.
   1. Confirme sua seleção no **Escopo**. Clique em **Avançar**.
   1. Especifique um título de Fluxo de trabalho em **Fluxos de trabalho**. Clique em **Publicar mais tarde**.

      ![manageschedulepub](assets/manageschedulepub.png)



## Cancelar publicação de pastas do Brand Portal {#unpublish-folders-from-brand-portal}

Você pode remover qualquer pasta de ativos publicada no Brand Portal ao cancelar a publicação da instância do autor do AEM. Após cancelar a publicação da pasta original, a cópia não estará mais disponível para os usuários do Brand Portal.

Você tem a opção de cancelar a publicação de pastas do Brand Portal rapidamente ou agendá-las para uma data e hora posteriores. Para cancelar a publicação de pastas de ativos do Brand Portal:

1. Na interface do AEM Assets na instância do AEM Author, selecione a pasta que deseja cancelar a publicação.

   ![publish2bp-1](assets/publish2bp.png)

1. Na barra de ferramentas, clique em **Gerenciar publicação**.

1. **Cancelar a publicação do Brand Portal agora**

   Para cancelar a publicação rapidamente da pasta desejada do Brand Portal:

   1. Na barra de ferramentas, selecione **Gerenciar publicação**.
   1. De **Ação** select **Cancelar publicação do Brand Portal**, de **Agendamento** select **Agora** e clique em **Próximo.**
   1. Confirme sua seleção no **Escopo** e clique em **Cancelar publicação no Brand Portal**.

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **Cancelar a publicação do Brand Portal mais tarde**

   Para agendar a publicação de uma pasta do Brand Portal para uma data e hora posteriores:

   1. Na barra de ferramentas, selecione **Gerenciar publicação**.
   1. De **Ação** select **Cancelar publicação do Brand Portal** e de **Agendamento** select **Mais tarde**.
   1. Selecione uma **Data de ativação** e especifique a hora. Clique em **Avançar**.
   1. Confirme a seleção no **Escopo** e clique em **Avançar**.
   1. Especifique um **Título de fluxo de trabalho** em **Fluxos de trabalho**. Clique em **Cancelar publicação mais tarde.**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>O procedimento para publicar/cancelar a publicação de um ativo de/para o Brand Portal é semelhante ao procedimento correspondente para uma pasta.
