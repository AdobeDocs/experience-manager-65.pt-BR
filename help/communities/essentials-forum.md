---
title: Fundamentos do fórum
seo-title: Fundamentos do fórum
description: Visão geral do fórum
seo-description: Visão geral do fórum
uuid: 68849582-8742-40be-9e7e-0b574ae38815
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 059c5bbe-07eb-4873-8157-2196df887b27
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Fundamentos do fórum {#forum-essentials}

Esta página fornece as informações essenciais para trabalhar com o recurso do fórum.

## Essenciais para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceTypes</strong></td>
   <td>social/fórum/components/hbs/forum<br /> social/forum/components/hbs/tópico<br /> social/fórum/components/hbs/post</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusivo</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vote<br /> cq.social.hbs.forum</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/forum/components/hbs/forum/forum.hbs<br /> /libs/social/forum/components/hbs/post/post.hbs<br /> /libs/social/forum/components/hbs/topic/topic.hbs<br /> /libs/social/forum/components/hbs/topic/list-item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/forum/components/hbs/forum/clientlibs/forum.css</td>
  </tr>
  <tr>
   <td><strong> propriedades</strong></td>
   <td>Consulte Recurso <a href="forum.md">do fórum</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do cliente](client-customize.md)

## Fundamentos para servidor {#essentials-for-server-side}

* [API do fórum](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/api/package-summary.html)

* [Pontos finais do fórum](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/forum/client/endpoints/package-summary.html)

* [Personalizações do servidor](server-customize.md)

### Função do fórum {#forum-function}

Uma estrutura de site da comunidade que inclui a função [](functions.md#forum-function)Fórum, inclui um `forum` componente configurado, bem como configurações que afetam a moderação, marcação e tradução.

### Acessar publicações do fórum (UGC) {#accessing-forum-posts-ugc}

O UGC deve ser moderado usando um dos métodos padrão de moderação.
Consulte [Moderação de conteúdo](moderate-ugc.md)gerado pelo usuário.

A partir das comunidades do AEM 6.1, o uso de uma loja [](working-with-srp.md) comum para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso prévio**.

Consulte:

* [Visão geral](srp.md) do provedor de recursos do Armazenamento - Introdução e visão geral de uso do repositório
* [SRP e UGC Essentials](srp-and-ugc.md) - métodos e exemplos de utilitários SRP
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação
* [Refatoração](socialutils.md) do SocialUtils - mapeamento de métodos de utilitário obsoletos para os métodos atuais do utilitário SRP

