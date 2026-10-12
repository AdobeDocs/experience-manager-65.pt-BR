---
title: Fundamentos do Placar de líderes
description: Saiba como configurar a Pontuação e as medalhas das comunidades para poder trabalhar com o componente de Quadro de classificação nas comunidades do Adobe Experience Manager.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: fd1b1749-13f9-4079-ae39-348676105852
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 4%
---
# Fundamentos do Placar de líderes {#leaderboard-essentials}

Esta página fornece as informações essenciais para trabalhar com o recurso de quadro de classificação.

Antes de incluir o componente de quadro de classificação em uma página, é necessário configurar a [Pontuação e as medalhas das comunidades](implementing-scoring.md).

Consulte [Fundamentos de pontuação e medalhas](configure-scoring.md).

## Essentials para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/gamification/components/hbs/leaderboard</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluível</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.gamification.hbs.leaderboard</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/leaderboard.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/gamification/components/hbs/leaderboard/clientlibs/leaderboard.css</td>
  </tr>
  <tr>
   <td><strong> propriedades</strong></td>
   <td>Consulte <a href="enabling-leaderboard.md">Recurso do quadro de classificação</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](client-customize.md)

### Função da biblioteca de arquivo {#file-library-function}

Uma estrutura de site de comunidade que inclui a [função de quadro de classificação](functions.md#leaderboard-function), inclui um componente `leaderboard` configurado.
