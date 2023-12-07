---
title: Publicar pastas no Brand Portal
description: Saiba como publicar e desfazer a publicação de pastas no Brand Portal.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 92a156f0-ce2a-4c83-bd57-0c29efbf784f
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 34%

---

# Publicar pastas no Brand Portal{#publish-folders-to-brand-portal}

Como administrador do Adobe Experience Manager (AEM) Assets, você pode publicar ativos e pastas na instância do AEM Assets Brand Portal (ou agendar o fluxo de trabalho de publicação para uma data/hora posterior) para sua organização. No entanto, primeiro você deve integrar o AEM Assets ao Brand Portal. Para obter detalhes, consulte [Configurar o AEM Assets com o Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Depois de publicar um ativo ou pasta, ele fica disponível para usuários no Brand Portal.

Se fizer modificações subsequentes no ativo ou pasta original no AEM Assets, as alterações não serão refletidas no Brand Portal até que publique novamente o ativo ou pasta. Esse recurso garante que as alterações de trabalho em andamento não estejam disponíveis no Brand Portal. Somente as alterações aprovadas publicadas por um administrador são disponibilizadas no Brand Portal.

## Publicar pastas no Brand Portal {#publish-folders-to-brand-portal-1}

1. Na interface do AEM Assets, passe o mouse sobre a pasta desejada e selecione **Publish** nas ações rápidas.

   Como alternativa, selecione a pasta desejada e siga as outras etapas.

   ![publish2bp](assets/publish2bp.png)

1. **Publicar pastas agora**

   Para publicar as pastas selecionadas no Brand Portal, siga um dos procedimentos a seguir:

   * Na barra de ferramentas, selecione **Publicação rápida**. Em seguida, no menu, selecione **Publicar no Brand Portal**.

   * Na barra de ferramentas, selecione **Gerenciar publicação**.

   1. De **Ação** selecionar **Publicar no Brand Portal**, de **Agendamento** selecionar **Agora** e clique em **Próximo.**
   1. Confirme sua seleção no **Escopo** e clique em **Publicar no Brand Portal**.

   Será exibida uma mensagem informando que a pasta foi colocada na fila para publicação no Brand Portal. Faça logon na interface do Brand Portal para ver a pasta publicada.

   **Publicar pastas mais tarde**

   Para agendar a publicação de pastas de ativos no fluxo de trabalho do Brand Portal para uma data ou hora posterior:

   1. Depois de selecionar os ativos/pastas a serem publicados, selecione **Gerenciar publicação** na barra de ferramentas na parte superior.
   1. De **Ação** selecionar **Publicar no Brand Portal**, de **Agendamento** selecionar **Mais tarde**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Selecione uma **Data de ativação** e especifique a hora. Clique em **Avançar**.
   1. Confirme sua seleção no **Escopo**. Clique em **Avançar**.
   1. Especifique um título de Fluxo de trabalho em **Fluxos de trabalho**. Clique em **Publicar mais tarde**.

      ![manageschedulepub](assets/manageschedulepub.png)

## Cancelar publicação de pastas do Brand Portal {#unpublish-folders-from-brand-portal}

É possível remover qualquer pasta de ativos publicada no Brand Portal ao cancelar a publicação da instância do autor do AEM. Após cancelar a publicação da pasta original, a cópia não estará mais disponível para os usuários do Brand Portal.

Você tem a opção de cancelar a publicação de pastas do Brand Portal rapidamente ou agendá-la para uma data e hora posteriores. Para cancelar a publicação de pastas de ativos do Brand Portal:

1. Na interface do AEM Assets na instância AEM Author, selecione a pasta da qual deseja cancelar a publicação.

   ![publish2bp-1](assets/publish2bp.png)

1. Na barra de ferramentas, clique em **Gerenciar publicação**.

1. **Cancelar publicação do Brand Portal agora**

   Para cancelar rapidamente a publicação da pasta desejada no Brand Portal:

   1. Na barra de ferramentas, selecione **Gerenciar publicação**.
   1. De **Ação** selecionar **Cancelar publicação no Brand Portal**, de **Agendamento** selecionar **Agora** e clique em **Próximo.**
   1. Confirme sua seleção no **Escopo** e clique em **Cancelar publicação no Brand Portal**.

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **Cancelar a publicação no Brand Portal mais tarde**

   Para agendar a publicação de uma pasta do Brand Portal para uma data e hora posteriores:

   1. Na barra de ferramentas, selecione **Gerenciar publicação**.
   1. De **Ação** selecionar **Cancelar publicação no Brand Portal**, e de **Agendamento** selecionar **Mais tarde**.
   1. Selecione uma **Data de ativação** e especifique a hora. Clique em **Avançar**.
   1. Confirme a seleção no **Escopo** e clique em **Avançar**.
   1. Especifique um **Título de fluxo de trabalho** em **Fluxos de trabalho**. Clique em **Desfazer a publicação mais tarde.**

      ![unpublishworkflows](assets/unpublishworkflows.png)

>[!NOTE]
>
>O procedimento para publicar/desfazer a publicação de um ativo de/para o Brand Portal é semelhante ao procedimento correspondente para uma pasta.
