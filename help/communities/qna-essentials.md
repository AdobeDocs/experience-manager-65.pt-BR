---
title: Noções básicas sobre QnA
seo-title: Noções básicas sobre QnA
description: Recurso do fórum de perguntas e respostas
seo-description: Recurso do fórum de perguntas e respostas
uuid: c718a8e3-b3bd-4db9-8c0f-6dd973d40583
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ceace3aa-78a5-485e-b519-630479e087d8
translation-type: tm+mt
source-git-commit: ca15258a5dc7ca99b6c9d6ae85e42c77a3802c87
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---


# QnA Essentials {#qna-essentials}

Esta página fornece as informações essenciais para trabalhar com o recurso de fórum de perguntas e respostas (QnA).

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">inclusivo</a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientllibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vote<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> templates</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> propriedades</td>
   <td>Consulte <a href="working-with-qna.md">Recurso do fórum de perguntas e respostas</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do cliente](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API QnA](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [Pontos finais de QnA](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [Personalizações do servidor](server-customize.md)

### Função QnA {#qna-function}

Uma estrutura de site da comunidade que inclui a função [QnA](functions.md#qna-function) terá um componente `QnA` configurado, bem como configurações que afetam a moderação e a marcação. A função QnA suporta a identificação de um [grupo de usuários membro privilegiado](users.md#privileged-members-group).

### Acessar publicações de fórum QnA (UGC) {#accessing-qna-forum-posts-ugc}

O UGC deve ser moderado usando um dos métodos padrão de moderação.
Consulte [Moderação de conteúdo gerado pelo usuário](moderate-ugc.md).

A partir AEM Comunidades 6.1, o uso de uma [loja comum](working-with-srp.md) para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso prévio**.

Consulte:

* [Visão geral](srp.md)  do provedor de recursos do armazenamento - introdução e visão geral do uso do repositório.
* [SRP e UGC Essentials](srp-and-ugc.md)  - métodos e exemplos de utilitários SRP.
* [Acesso ao UGC com diretrizes de codificação do SRP](accessing-ugc-with-srp.md) .
* [Refatoração](socialutils.md)  do SocialUtils - mapeamento de métodos de utilitários obsoletos para métodos de utilitários SRP atuais.

