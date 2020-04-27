---
title: Resenhas essenciais
seo-title: Resenhas essenciais
description: Análises e componentes do Resumo da revisão
seo-description: Análises e componentes do Resumo da revisão
uuid: 540c106e-ee3b-4261-82b2-a909d254dbf7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 62669a9d-2107-4644-a4bf-143d0ac148b3
translation-type: tm+mt
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# Resenhas essenciais {#reviews-essentials}

Este recurso consiste em dois componentes que trabalham juntos: revisões e resumo da revisão.

As revisões são um componente composto baseado em um sistema [de](essentials-comments.md) comentários que contém um ou mais componentes de [classificação](rating-basics.md) (tally).

Não há suporte para a publicação anônima de uma revisão. Os visitantes do site devem se registrar e fazer logon para adicionar uma revisão. O visitante conectado (membro) pode atualizar sua revisão a qualquer momento.

## Essenciais para o lado do cliente {#essentials-for-client-side}

### Revisões {#reviews}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/resenhas/componentes/hbs/resenhas</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusivo</strong></a></td>
   <td>Sim - as propriedades são editáveis no <i>modo </i>de design</td>
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
   <td>Consulte <a href="reviews.md">Usando Revisões</a></td>
  </tr>
 </tbody>
</table>

### Resumo da análise {#review-summary}

| **resourceType** | social/resenhas/componentes/hbs/summary |
|---|---|
| [**inclusivo **](scf.md#add-or-include-a-communities-component) | Sim - as propriedades podem ser editadas no modo *design * |
| [**clientllibs **](client-customize.md#clientlibs-for-scf) | cq.social.hbs.reviews |
| **templates** | /libs/social/reviews/components/hbs/summary/summary.hbs |
| **css** | /libs/social/reviews/components/hbs/reviews/clientlibs/review.css |
| **propriedades** | Consulte [Usando Revisões](reviews.md) |

* [Personalizações do cliente](client-customize.md)

## Fundamentos para servidor {#essentials-for-server-side}

* [API de revisão](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/api/package-summary.html)

* [Analisar Pontos de Extremidade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/review/client/endpoints/package-summary.html)

* [Personalizações do servidor](server-customize.md)

### Acessar revisões publicadas (UGC) {#accessing-posted-reviews-ugc}

O UGC deve ser moderado usando um dos métodos padrão de moderação.
Consulte [Moderação de conteúdo](moderate-ugc.md)gerado pelo usuário.

A partir das comunidades do AEM 6.1, o uso de uma loja [](working-with-srp.md) comum para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso prévio**.

Consulte:

* [Visão geral](srp.md) do provedor de recursos do Armazenamento - Introdução e visão geral de uso do repositório.
* [SRP e UGC Essentials](srp-and-ugc.md) - métodos e exemplos de utilitários SRP.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - diretrizes de codificação.
* [Refatoração](socialutils.md) SocialUtils - mapeamento de métodos de utilitários obsoletos para métodos de utilitários SRP atuais.

