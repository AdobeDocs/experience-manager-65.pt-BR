---
title: Como o gerenciamento multisite para conteúdo direcionado está estruturado
description: Um diagrama mostra como o suporte a vários sites para conteúdo direcionado está estruturado
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '179'
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
* o site3 pesquisa a área principal da marca1 e marca2, pois nenhum outro mapeamento de área foi definido para este site.
