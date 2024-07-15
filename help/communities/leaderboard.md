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
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '112'
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
