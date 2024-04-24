---
title: Fundamentos das análises
description: Saiba mais sobre como as Revisões no AEM Communities são um componente composto baseado em um sistema de comentários que contém um ou mais componentes de classificação (tally).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---

# Fundamentos das análises {#reviews-essentials}

Esse recurso consiste em dois componentes que trabalham juntos: revisões e resumo de revisões.

Revisões é um componente composto baseado em uma [sistema de comentários](essentials-comments.md) que contenha um ou mais [avaliação](rating-basics.md) componentes (tally).

Não há suporte para postagem anônima de uma revisão. Os visitantes do site devem se registrar e fazer logon para adicionar uma avaliação. O visitante conectado (membro) pode atualizar sua análise a qualquer momento.

## Essentials para o lado do cliente {#essentials-for-client-side}

### Revisões {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/análises/componentes/hbs/análises</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluível</strong></a></td>
   <td>Sim - as propriedades são editáveis no <i>design </i>modo</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>propriedades</strong></td>
   <td>Consulte <a href="reviews.md">Usar análises</a></td>
  </tr>
 </tbody>
</table>

### Resumo da análise {#review-summary}

| **resourceType** | social/análises/componentes/hbs/resumo |
|---|---|
| [**incluível**](scf.md#add-or-include-a-communities-component) | Sim - as propriedades são editáveis no modo *design * |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **modelos** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **propriedades** | Consulte [Usar análises](reviews.md) |

* [Personalizações do lado do cliente](client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [API de revisão](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Revisar Pontos de Extremidade](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Acesso a análises publicadas (UGC) {#accessing-posted-reviews-ugc}

A UGC deve ser moderada usando um dos métodos padrão para moderação.
Consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).

A partir do AEM 6.1 Communities, o uso de um [armazenamento comum](working-with-srp.md) O para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso**.

Consulte:

* [Visão geral do provedor de recursos de armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Fundamentos de SRP e UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário SRP.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração de SocialUtils](socialutils.md) - Mapeamento de métodos de utilitário obsoletos para métodos de utilitário SRP atuais.
