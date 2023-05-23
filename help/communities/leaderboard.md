---
title: Fundamentos do Placar de líderes
seo-title: Leaderboard Essentials
description: Visão geral do recurso de quadro de classificação
seo-description: Leaderboard feature overview
uuid: 815a6928-b147-496d-9751-13159ad1304d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 7449f99e-77d7-4c0f-96d5-b67d5e1f124a
exl-id: fd1b1749-13f9-4079-ae39-348676105852
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 5%

---

# Fundamentos do Placar de líderes {#leaderboard-essentials}

Esta página fornece as informações essenciais para trabalhar com o recurso de quadro de classificação.

Antes de incluir o componente de quadro de classificação em uma página, é necessário configurar [Pontuação e medalhas das comunidades](implementing-scoring.md).

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
   <td>Consulte <a href="enabling-leaderboard.md">Recurso de quadro de classificação</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](client-customize.md)

### Função da biblioteca de arquivo {#file-library-function}

Uma estrutura de site da comunidade que inclui o [Função de placar de líderes](functions.md#leaderboard-function), inclui um configurado `leaderboard` componente.
