---
title: Revisões essenciais
seo-title: Reviews Essentials
description: Revisar e analisar componentes do resumo
seo-description: Reviews and Review Summary components
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
exl-id: 91e0e245-a2f1-4bd7-b38f-7641fd94a547
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 2%

---

# Revisões essenciais {#reviews-essentials}

Esse recurso consiste em dois componentes que trabalham juntos: revisões e resumo da revisão.

As revisões são um componente composto baseado em um [sistema de comentários](essentials-comments.md) que contém um ou mais [classificação](rating-basics.md) (tally) componentes.

A publicação anônima de uma revisão não é suportada. Os visitantes do site devem se registrar e fazer logon para adicionar uma revisão. O visitante conectado (membro) pode atualizar sua revisão a qualquer momento.

## Fundamentos para o lado do cliente {#essentials-for-client-side}

### Revisões {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/resenhas/componentes/hbs/resenhas</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incondicional</strong></a></td>
   <td>Sim - as propriedades podem ser editadas em <i>projeto </i>modo</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.reviews</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/reviews.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/review.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/status.hbs<br /> /libs/social/reviews/components/hbs/reviews/review/toolbar.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/reviews/components/hbs/reviews/clientlibs/review.css</td>
  </tr>
  <tr>
   <td><strong>propriedades</strong></td>
   <td>Consulte <a href="reviews.md">Uso de revisões</a></td>
  </tr>
 </tbody>
</table>

### Resumo da análise {#review-summary}

| **resourceType** | social/resenhas/componentes/hbs/summary |
|---|---|
| [**incondicional**](scf.md#add-or-include-a-communities-component) | Sim - as propriedades podem ser editadas no modo *design* |
| [**clientllibs**](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **modelos** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **propriedades** | Consulte [Uso de revisões](reviews.md) |

* [Personalizações do lado do cliente](client-customize.md)

## Fundamentos para o lado do servidor {#essentials-for-server-side}

* [Revisar API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Revisar Pontos de Extremidade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Acesso a Revisões Publicadas (UGC) {#accessing-posted-reviews-ugc}

O UGC deve ser moderado usando um dos métodos padrão de moderação.
Consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).

A partir AEM 6.1 Comunidades, uso de um [loja comum](working-with-srp.md) O para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso prévio**.

Consulte:

* [Visão geral do provedor de recursos de armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Princípios básicos de SRP e UGC](srp-and-ugc.md) - métodos e exemplos de utilitários SRP.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração do SocialUtils](socialutils.md) - Mapeamento de métodos de utilitário obsoletos para os métodos de utilitário SRP atuais.
