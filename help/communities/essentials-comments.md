---
title: Fundamentos de comentários
description: Visão geral do componente Comentários
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 4%

---

# Fundamentos de comentários {#comments-essentials}

Esta página fornece os fundamentos para trabalhar com o sistema de comentários (componente de comentários) e as opções para gerenciar o conteúdo gerado pelo usuário (UGC) produzido quando os membros postam comentários ou respostas.

A componente de comentários estabelece um sistema de comentários de forma que cada postagem individual seja representada por um componente de comentário (singular). É o sistema de comentários que está incluído na página. O sistema de comentários cria comentários individuais quando chamado.

## Essentials para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluível</strong></a></td>
   <td>Sim - as propriedades são editáveis no <i>design </i>modo</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
   <td> /libs/social/commons/components/hbs/comments/comments.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>CSS</strong></td>
   <td> /libs/social/commons/components/hbs/comments/clientlibs/commentsystem.css</td>
  </tr>
  <tr>
   <td><strong> propriedades</strong></td>
   <td> Consulte <a href="comments.md">Uso de comentários</a></td>
  </tr>
 </tbody>
</table>

[Personalizações do lado do cliente](client-customize.md)

### Uma instância por página {#one-instance-per-page}

A paginação e o uso de URLs para armazenamento em cache e vinculação exigem que o URL seja exclusivo por sistema de comentários. Portanto, somente uma instância de um sistema de comentários é permitida por página.

Outros recursos já incluem o sistema de comentários. São eles:

* [Blog](blog-developer-basics.md)
* [Calendário](calendar-basics-for-developers.md)
* [Biblioteca de arquivo](essentials-file-library.md)
* [Fórum](essentials-forum.md)
* [QnA](qna-essentials.md)
* [Revisões](reviews-basics.md)

### Sinalizar lista de motivo {#flag-reason-list}

A lista de motivos da sinalização pode ser personalizada adicionando flagreasonlist.hbs ao aplicativo para substituir o que está em

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

Isso se aplica a qualquer componente que estende um sistema de comentários.

## Essentials para o lado do servidor {#essentials-for-server-side}

* [API de comentários](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [Endpoints de comentários](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Acesso a comentários publicados (UGC) {#accessing-posted-comments-ugc}

A UGC deve ser moderada usando um dos métodos padrão para moderação.
Consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).

A partir do AEM 6.1 Communities, o uso de um [armazenamento comum](working-with-srp.md) O para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso**.

Consulte:

* [Visão geral do provedor de recursos de armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Fundamentos de SRP e UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário SRP.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração de SocialUtils](socialutils.md) - Mapeamento de métodos de utilitário obsoletos para métodos de utilitário SRP atuais.
