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
   <td> <strong>tiposDeRecursos</strong></td>
   <td>social/forum/components/hbs/forum<br /> social/forum/components/hbs/topic<br /> social/forum/components/hbs/post</td>
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
   <td>Consulte <a href="forum.md">Recurso do fórum</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [API do fórum](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/forum/client/api/package-summary.html)

* [Pontos de Extremidade do Fórum](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/forum/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Função do fórum {#forum-function}

Uma estrutura de site de comunidade que inclui a [função de Fórum](functions.md#forum-function), um componente `forum` configurado e configurações que afetam a moderação, a marcação e a tradução.

### Acessar publicações do fórum (UGC) {#accessing-forum-posts-ugc}

A UGC deve ser moderada usando um dos métodos padrão para moderação.
Consulte [Moderando Conteúdo Gerado Pelo Usuário](moderate-ugc.md).

A partir do Adobe Experience Manager 6.1 Communities, o uso de um [armazenamento comum](working-with-srp.md) para UGC inclui acesso programático a UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso**.

Consulte:

* [Visão Geral do Provedor de Recursos de Armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Fundamentos do SRP e do UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário SRP.
* [Acessando UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração de SocialUtils](socialutils.md) - Mapeando métodos de utilitário obsoletos para métodos de utilitário SRP atuais.
