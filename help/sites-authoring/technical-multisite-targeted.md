---
title: Como o gerenciamento multisite para conteúdo direcionado está estruturado
seo-title: How Multisite Management for Targeted Content is Structured
description: Um diagrama mostra como o suporte a vários sites para conteúdo direcionado está estruturado
seo-description: A diagram shows how multisite support for targeted content is structured
uuid: 2d30cdf0-ab77-490d-aac0-db3a0d417a58
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 7dd851ab-3fa7-426e-89cb-08b67e9b5999
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 36%

---

# Como o gerenciamento multisite para conteúdo direcionado está estruturado{#how-multisite-management-for-targeted-content-is-structured}

O diagrama a seguir mostra como o suporte multisite para conteúdo direcionado está estruturado.

As áreas aparecem dentro de **/conteúdo/campanhas/&lt;marca>** e, por padrão, cada marca tem uma área principal, que é criada automaticamente. Cada área contém seu próprio conjunto de atividades, experiências e ofertas.

![chlimage_1-268](assets/chlimage_1-268.png)

Para pesquisar conteúdo direcionado, as páginas ou os sites podem mapear para uma área. Se não houver uma área configurada, o AEM voltará para a área principal dessa marca específica.

O diagrama a seguir é um exemplo de como a lógica funciona para três sites, chamados de site1, site2 e site3.

![chlimage_1-269](assets/chlimage_1-269.png)

* site1 procura myarea1 para brand1 e otherarea2 para brand2 com base no area mapping.
* site2 procura myarea1 para brand1 e área principal para brand2 pois somente o mapeamento de área para brand1 é definido.
* site3 procura a área principal para marca1 e marca2 já que nenhum outro mapeamento de área foi definido para este site.
