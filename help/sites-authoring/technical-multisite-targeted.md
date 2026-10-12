---
title: Como o gerenciamento multisite para conteúdo direcionado está estruturado
description: Um diagrama mostra como o suporte a vários sites para conteúdo direcionado está estruturado
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: d8ba91ff-ad6e-4540-baff-a2c0c764a299
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
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
