---
title: Observações essenciais
seo-title: Comments Essentials
description: Visão geral do componente Comentários
seo-description: Comments component overview
uuid: 58b7bb58-f598-4bcb-93ae-b7795cab51cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 18f54a1c-52aa-414d-b494-1f19b5c10345
exl-id: 8b4034f7-2f97-45ad-96d4-51cfbeae5991
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 4%

---

# Observações essenciais {#comments-essentials}

Esta página fornece os fundamentos de trabalhar com o sistema de comentários (componente de comentários) e as opções para gerenciar o conteúdo gerado pelo usuário (UGC) produzido quando os membros postam comentários ou respostas.

O componente de comentários estabelece um sistema de comentários de modo que cada publicação individual seja representada por um componente de comentário (singular). É o sistema de comentários incluído na página. O sistema de comentários criará os comentários individuais quando forem chamados.

## Fundamentos para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td> social/commons/components/hbs/comments</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incondicional</strong></a></td>
   <td>Sim - as propriedades podem ser editadas em <i>projeto </i>modo</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.comments<br /> cq.social.hbs.vote</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
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

A paginação e o uso de URLs para armazenamento em cache e vinculação exigem que o URL seja único por sistema de comentários. Portanto, somente uma instância de um sistema de comentários é permitida por página.

Outros recursos já incluem o sistema de comentários. São eles:

* [Blog](blog-developer-basics.md)
* [Calendário](calendar-basics-for-developers.md)
* [Biblioteca de arquivos](essentials-file-library.md)
* [Fórum](essentials-forum.md)
* [Perguntas e respostas](qna-essentials.md)
* [Revisões](reviews-basics.md)

### Sinalizar lista de motivo {#flag-reason-list}

A lista de motivos de sinalização pode ser personalizada adicionando flagrazoavelmente list.hbs ao seu aplicativo para substituir o que está em

* `/libs/social/commons/components/hbs/comments/comment/flagreasonlist.hbs`

Isso se aplica a qualquer componente que estenda um sistema de comentários.

## Fundamentos para o lado do servidor {#essentials-for-server-side}

* [API de comentários](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/api/package-summary.html)

* [Endpoints de comentários](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/comments/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Acessar Comentários Publicados (UGC) {#accessing-posted-comments-ugc}

O UGC deve ser moderado usando um dos métodos padrão de moderação.
Consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).

A partir AEM 6.1 Comunidades, uso de um [loja comum](working-with-srp.md) O para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso prévio**.

Consulte:

* [Visão geral do provedor de recursos de armazenamento](srp.md) - Introdução e visão geral do uso do repositório.
* [Princípios básicos de SRP e UGC](srp-and-ugc.md) - métodos e exemplos de utilitários SRP.
* [Acesso ao UGC com SRP](accessing-ugc-with-srp.md) - Diretrizes de codificação.
* [Refatoração do SocialUtils](socialutils.md) - Mapeamento de métodos de utilitário obsoletos para os métodos de utilitário SRP atuais.
