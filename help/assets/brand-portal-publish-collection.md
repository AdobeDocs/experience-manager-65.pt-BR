---
title: Publicar coleções no Brand Portal
seo-title: Publish collections to Brand Portal
description: Saiba como publicar e cancelar a publicação de coleções no Brand Portal.
seo-description: Learn how to publish and unpublish collections to Brand Portal.
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
feature: Brand Portal
role: User
exl-id: 8f426012-d9ec-418e-8ab6-78e4aeff7538
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 36%

---

# Publicar coleções no Brand Portal {#publish-collections-to-brand-portal}

Como administrador do Adobe Experience Manager (AEM) Assets, você pode publicar coleções na instância do AEM Assets Brand Portal para sua organização. No entanto, primeiro você deve integrar o AEM Assets com o Brand Portal. Para obter detalhes, consulte [Configurar o AEM Assets com o Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Se fizer modificações subsequentes na coleção original no AEM Assets, as alterações não serão refletidas no Brand Portal até que publique a coleção novamente. Essa característica garante que as alterações de trabalho em andamento não estejam disponíveis no Brand Portal. Somente as alterações aprovadas publicadas por um administrador são disponibilizadas no Brand Portal.

>[!NOTE]
>
>Os fragmentos de conteúdo não podem ser publicados no Brand Portal. Portanto, se você selecionar fragmentos de conteúdo no AEM Author, então **Publicar no Brand Portal** não está disponível.
>
>Se as coleções que contêm fragmentos de conteúdo forem publicadas do AEM Author para o Brand Portal, todo o conteúdo da pasta, exceto fragmentos de conteúdo, será replicado para a interface do Brand Portal.

## Publicar uma coleção no Brand Portal {#publish-a-collection-to-brand-portal}

1. Na interface do usuário do AEM Assets, clique no logotipo do AEM.
1. Na página **Navegação**, acesse **Ativos > Coleções**.
1. No console Coleções , selecione a coleção que deseja publicar no Brand Portal.

   ![select_collection](assets/select_collection.png)

1. Na barra de ferramentas, clique em **Publicar no Brand Portal**.
1. Na caixa de diálogo de confirmação, clique em **Publicar**.
1. Feche a mensagem de confirmação.
1. Faça logon no Brand Portal como administrador. A coleção publicada está disponível no console Coleções.

   ![coleção publicada](assets/published_collection.png)

## Cancelar publicação de coleções {#unpublish-collections}

Você pode cancelar a publicação de coleções que você publica do AEM Assets para o Brand Portal. Após cancelar a publicação da coleção original, a cópia não estará mais disponível para os usuários do Brand Portal.

1. No console Coleções da instância do AEM Assets, selecione a coleção que deseja cancelar a publicação.

   ![select_collection-1](assets/select_collection-1.png)

1. Na barra de ferramentas, clique no ícone **Remover do Brand Portal**.
1. Na caixa de diálogo, clique em **Cancelar publicação**.
1. Feche a mensagem de confirmação. A coleção é removida da interface do Brand Portal.
