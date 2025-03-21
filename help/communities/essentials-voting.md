---
title: Fundamentos para votação
description: Saiba como usar o componente de Votação, que permite que os membros classifiquem um conteúdo específico selecionando setas para cima ou para baixo para indicar sua opinião.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e8ff751f-404a-498d-8e90-62a13ab593ff
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 1%

---

# Fundamentos para votação {#voting-essentials}

O componente de votação, uma subclasse [tally](tally.md), é uma ferramenta útil que permite que os membros classifiquem um conteúdo específico simplesmente selecionando setas para cima ou para baixo para indicar sua opinião.

É permitido colocar várias instâncias de um componente de votação na mesma página; cada instância deve ser configurada com uma propriedade `tally name` exclusiva.

Não há suporte para postagem anônima de um voto. Os visitantes do site devem se registrar e fazer logon para participar da votação apenas uma vez. O visitante conectado (membro) pode alterar seu voto a qualquer momento.

## Essentials para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/voting</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluível</strong></a></td>
   <td>Sim - as propriedades são editáveis no modo <i>design </i></td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>propriedades</strong></td>
   <td><p>Consulte <a href="voting.md">Usando a Votação</a></p> </td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [Tally APIs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [Pontos de Extremidade da Tally](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Acessando a votação publicada (UGC) {#accessing-posted-voting-ugc}

A UGC deve ser moderada usando um dos métodos padrão para moderação.
Consulte [Moderando Conteúdo Gerado por Usuário](moderate-ugc.md).

Desde o AEM 6.1 Communities, o uso de um [armazenamento comum](working-with-srp.md) para UGC inclui acesso programático a UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso**.

Consulte:

* [Visão Geral do Provedor de Recursos de Armazenamento](srp.md) - introdução e visão geral do uso do repositório.
* [Fundamentos do SRP e do UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário SRP.
* [Acessando UGC com SRP](accessing-ugc-with-srp.md) - diretrizes de codificação.
* [Refatoração de SocialUtils](socialutils.md) - mapeando métodos de utilitário obsoletos para métodos de utilitário SRP atuais.
