---
title: Fundamentos de QnA
description: Saiba mais sobre os fundamentos do trabalho com o recurso Fórum de perguntas e respostas (QnA) nas comunidades do Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%

---

# Fundamentos de QnA {#qna-essentials}

Esta página fornece as informações essenciais para trabalhar com o recurso de fórum de perguntas e respostas (QnA).

## Essentials para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">incluir</a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientllibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> modelos</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> propriedades</td>
   <td>Consulte <a href="working-with-qna.md">Recurso do Fórum de Perguntas e Respostas</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [API QnA](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [Pontos de Extremidade QnA](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Função QnA {#qna-function}

Uma estrutura de site de comunidade que inclui a [função QnA](functions.md#qna-function) tem um componente `QnA` configurado, além de configurações que afetam a moderação e a marcação. A função QnA oferece suporte à identificação de um [grupo de usuários membro privilegiado](users.md#privileged-members-group).

### Acessar publicações do fórum QnA (UGC) {#accessing-qna-forum-posts-ugc}

A UGC deve ser moderada usando um dos métodos padrão para moderação.
Consulte [Moderando Conteúdo Gerado Pelo Usuário](moderate-ugc.md).

Desde o AEM 6.1 Communities, o uso de um [armazenamento comum](working-with-srp.md) para UGC inclui acesso programático a UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso**.

Consulte:

* [Visão Geral do Provedor de Recursos de Armazenamento](srp.md) - introdução e visão geral do uso do repositório.
* [Fundamentos do SRP e do UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário SRP.
* [Acessando UGC com SRP](accessing-ugc-with-srp.md) - diretrizes de codificação.
* [Refatoração de SocialUtils](socialutils.md) - mapeando métodos de utilitário obsoletos para métodos de utilitário SRP atuais.
