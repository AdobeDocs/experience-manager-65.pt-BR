---
title: Como o gerenciamento multisite para conteúdo direcionado está estruturado
seo-title: Como o gerenciamento multisite para conteúdo direcionado está estruturado
description: Um diagrama mostra como o suporte multisite para conteúdo direcionado está estruturado
seo-description: Um diagrama mostra como o suporte multisite para conteúdo direcionado está estruturado
uuid: 2d30cdf0-ab77-490d-aac0-db3a0d417a58
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 7dd851ab-3fa7-426e-89cb-08b67e9b5999
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 89%

---


# Como o gerenciamento multisite para conteúdo direcionado está estruturado{#how-multisite-management-for-targeted-content-is-structured}

O diagrama a seguir mostra como o suporte multisite para conteúdo direcionado está estruturado.

As áreas aparecem abaixo de **/content/campanha/&lt;brand>** e, por padrão, cada marca tem uma área principal, que é criada automaticamente. Cada área contém seu próprio conjunto de atividades, experiências e ofertas.

![chlimage_1-268](assets/chlimage_1-268.png)

Para procurar conteúdo direcionado, páginas ou sites podem ser mapeados para uma área. Se não houver nenhuma área configurada, o AEM recuará para a área mestre dessa marca específica.

O diagrama a seguir é um exemplo de como a lógica funciona para três sites, chamados de site1, site2 e site3.

![chlimage_1-269](assets/chlimage_1-269.png)

* Site1 pesquisa myarea1 em busca de brand1 e otherarea2 em busca de brand2 com base no mapeamento de áreas.
* Site2 pesquisa myarea1 em busca de brand1 e a área mestra em busca de brand2, pois apenas o mapeamento de áreas para brand1 está definido.
* Site3 pesquisa a área mestra para brand1 e brand2, pois nenhum outro mapeamento de área é definido para esse site.

