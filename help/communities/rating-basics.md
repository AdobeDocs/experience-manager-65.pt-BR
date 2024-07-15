---
title: Fundamentos de classificação
description: Saiba como o componente de Classificação, uma subclasse Tally, permite que os membros da comunidade conectados avaliem um recurso no site.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 49456944-ff0d-4507-b3b8-143c90067573
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# Fundamentos de classificação {#rating-essentials}

O componente de classificação, uma subclasse [tally](tally.md), permite que membros da comunidade conectados avaliem um recurso no site.

É permitido colocar várias instâncias de um componente de votação na mesma página; cada instância deve ser configurada com uma propriedade `tally name` exclusiva.

Não há suporte para postagem anônima de uma classificação. Os visitantes do site devem se registrar e fazer logon para participar de uma classificação apenas uma vez. O visitante conectado (membro) pode alterar sua classificação a qualquer momento.

## Essentials para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/tally/components/hbs/rating</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluível</strong></a></td>
   <td>Sim - as propriedades são editáveis no modo <i>design </i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.rating</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
   <td><p> /libs/social/tally/components/hbs/rating/rating.hbs<br /> /libs/social/tally/components/hbs/rating/display.hbs<br /> /libs/social/tally/components/hbs/rating/histogram.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/rating/clientlibs/ratingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>propriedades</strong></td>
   <td><p>Consulte <a href="rating.md">Usando a Classificação</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [Tally APIs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Pontos de Extremidade da Tally](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Acesso às classificações publicadas (UGC) {#accessing-posted-ratings-ugc}

A UGC deve ser moderada usando um dos métodos padrão para moderação.
Consulte [Moderando Conteúdo Gerado por Usuário](moderate-ugc.md).

Desde o AEM 6.1 Communities, o uso de um [armazenamento comum](working-with-srp.md) para UGC inclui acesso programático a UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso**.

Consulte:

* [Visão Geral do Provedor de Recursos de Armazenamento](srp.md) - introdução e visão geral do uso do repositório.
* [Fundamentos do SRP e do UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário SRP.
* [Acessando UGC com SRP](accessing-ugc-with-srp.md) - diretrizes de codificação.
* [Refatoração de SocialUtils](socialutils.md) - mapeando métodos de utilitário obsoletos para métodos de utilitário SRP atuais.
