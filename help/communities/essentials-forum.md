---
title: Fundamentos do fórum
description: Saiba mais sobre os fundamentos do trabalho com o recurso Fórum nas comunidades do Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 622cf6ca-f119-4310-ad14-537576bd6f6d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---

# Fundamentos do fórum {#forum-essentials}

Esta página fornece as informações essenciais para trabalhar com o recurso de fórum.

## Essentials para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceTypes</strong></td>
   <td>social/fórum/components/hbs/forum<br /> social/fórum/components/hbs/topic<br /> social/fórum/components/hbs/post</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluível</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.forum</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
   <td> /libs/social/forum/components/hbs/forum/forum.hbs<br /> /libs/social/forum/components/hbs/post/post.hbs<br /> /libs/social/forum/components/hbs/topic/topic.hbs<br /> /libs/social/forum/components/hbs/topic/list-item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/forum/components/hbs/forum/clientlibs/forum.css</td>
  </tr>
  <tr>
   <td><strong> propriedades</strong></td>
   <td>Consulte <a href="forum.md">Recurso de fórum</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [API do fórum](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/forum/client/api/package-summary.html)

* [Endpoints do fórum](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/forum/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Função do fórum {#forum-function}

Uma estrutura de site da comunidade que inclui o [Função Fórum](functions.md#forum-function), inclui um configurado `forum` e configurações que afetam moderação, marcação e tradução.

### Acessar publicações do fórum (UGC) {#accessing-forum-posts-ugc}

A UGC deve ser moderada usando um dos métodos padrão para moderação.
Consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).

A partir do Adobe Experience Manager 6.1 Communities, o uso de um [armazenamento comum](working-with-srp.md) O para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso**.

Consulte:

* [Visão geral do provedor de recursos de armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Fundamentos de SRP e UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário SRP.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração de SocialUtils](socialutils.md) - Mapeamento de métodos de utilitário obsoletos para métodos de utilitário SRP atuais.
