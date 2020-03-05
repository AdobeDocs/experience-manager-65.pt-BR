---
title: Publicar pastas no Brand Portal
seo-title: Publicar pastas no Brand Portal
description: Saiba como publicar e cancelar a publicação de pastas no Brand Portal.
seo-description: Saiba como publicar e cancelar a publicação de pastas no Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
translation-type: tm+mt
source-git-commit: 9f923782d3d0a7bdf45b18e8025bd2d083acf77c

---


# Publish folders to Brand Portal{#publish-folders-to-brand-portal}

Como administrador dos ativos Adobe Experience Manager (AEM), você pode publicar ativos e pastas na instância do AEM Assets Brand Portal (ou agendar o fluxo de trabalho de publicação para uma data/hora posterior) para sua organização. No entanto, primeiro é necessário integrar os ativos AEM ao Portal de marcas. Para obter detalhes, consulte [Configurar ativos AEM com o Portal](/help/assets/configure-aem-assets-with-brand-portal.md)da marca.

Depois de publicar um ativo ou pasta, ele estará disponível para os usuários no Brand Portal.

Se você fizer modificações subsequentes no ativo ou pasta original nos ativos AEM, as alterações não serão refletidas no Portal de marcas até que você publique novamente o ativo ou a pasta. Esse recurso garante que as alterações do trabalho em andamento não estejam disponíveis no Brand Portal. Somente as alterações aprovadas publicadas por um administrador estão disponíveis no Brand Portal.

## Publish folders to Brand Portal {#publish-folders-to-brand-portal-1}

1. Na interface dos ativos AEM, passe o mouse sobre a pasta desejada e selecione a opção **Publicar** nas ações rápidas.

   Como alternativa, selecione a pasta desejada e siga as etapas seguintes.

   ![publish2bp](assets/publish2bp.png)

1. **Publicar pastas agora**

   Para publicar as pastas selecionadas no Brand Portal, execute um dos procedimentos a seguir:

   * Na barra de ferramentas, selecione Publicação **rápida**. Em seguida, no menu, selecione **Publicar no Brand Portal**.

   * Na barra de ferramentas, selecione **Gerenciar publicação**.
   1. Em **Ação** , selecione **Publicar no Brand Portal**, em **Agendamento** , selecione **Agora** e clique em **Avançar.**
   1. Confirme sua seleção no **Escopo** e clique em **Publicar no portal** da marca.
   Será exibida uma mensagem informando que a pasta foi colocada na fila para publicação no Brand Portal. Faça logon na interface do Brand Portal para ver a pasta publicada.

   **Publicar pastas mais tarde**

   Para agendar a publicação no fluxo de trabalho do Brand Portal das pastas de ativos para uma data ou hora posterior:

   1. Depois de selecionar os ativos/ pastas a serem publicados, selecione **Gerenciar publicação** na barra de ferramentas na parte superior.
   1. Em **Ação** , selecione **Publicar no Brand Portal**, em **Agendamento** , selecione **Mais tarde**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Selecione uma data **de** ativação e especifique a hora. Clique em **Avançar**.
   1. Confirme sua seleção no **Escopo**. Clique em **Avançar**.
   1. Especifique um título de Fluxo de trabalho em **Fluxos de trabalho**. Clique em **Publicar mais tarde**.

      ![manager chedulepub](assets/manageschedulepub.png)



## Unpublish folders from Brand Portal {#unpublish-folders-from-brand-portal}

Você pode remover qualquer pasta de ativos publicada no Brand Portal, desfazendo a publicação da instância do autor de AEM. Após desfazer a publicação da pasta original, a cópia não estará mais disponível para os usuários do Brand Portal.

Você tem a opção de cancelar a publicação rápida de pastas do Brand Portal ou agendá-las para uma data e hora posteriores. Para cancelar a publicação de pastas de ativos do Portal de marcas:

1. Na interface dos ativos AEM na instância do autor de AEM, selecione a pasta que deseja cancelar a publicação.

   ![publish2bp-1](assets/publish2bp.png)

1. Na barra de ferramentas, clique em **Gerenciar publicação**.

1. **Cancelar a publicação do Brand Portal agora**

   Para cancelar a publicação rápida da pasta desejada no Portal de marcas:

   1. Na barra de ferramentas, selecione **Gerenciar publicação**.
   1. Em **Ação** , selecione **Cancelar publicação do Brand Portal**, em **Agendamento** , selecione **Agora** e clique em **Avançar.**
   1. Confirme sua seleção no **Escopo** e clique em **Cancelar publicação no Portal** da marca.
   ![confirmar-desfazer a publicação](assets/confirm-unpublish.png)

   **Cancelar a publicação do Brand Portal mais tarde**

   Para agendar a publicação de uma pasta do Brand Portal para uma data e hora posteriores:

   1. Na barra de ferramentas, selecione **Gerenciar publicação**.
   1. Em **Ação** , selecione **Cancelar publicação do Brand Portal** e, em **Agendamento** , selecione **Mais Tarde**.
   1. Selecione uma data **de** ativação e especifique a hora. Clique em **Avançar**.
   1. Confirme sua seleção no **Escopo** e clique em **Avançar**.
   1. Especifique um título **de** Fluxo de trabalho em **Fluxos de trabalho**. Clique em **Cancelar publicação mais tarde.**

      ![despublicar fluxos de trabalho](assets/unpublishworkflows.png)


>[!NOTE]
>
>O procedimento para publicar/desfazer a publicação de um ativo do/para o Portal da Marca é semelhante ao procedimento correspondente para uma pasta.

