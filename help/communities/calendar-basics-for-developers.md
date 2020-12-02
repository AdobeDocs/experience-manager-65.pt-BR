---
title: Essenciais do calendário
seo-title: Essenciais do calendário
description: Visão geral dos recursos do calendário
seo-description: Visão geral dos recursos do calendário
uuid: 14ff7a83-b2a7-4f7e-8ee7-88f336329a1a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 88932a3c-ba7f-47ba-9e0b-206755c2d42e
translation-type: tm+mt
source-git-commit: 82affd528f2526384b319fe89082e0f574ab5855
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---


# Essenciais do calendário {#calendar-essentials}

Esta página fornece informações essenciais sobre como trabalhar com o recurso de calendário.

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/calendário/componentes/hbs/calendário</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusivo</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.calendar</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/calendar.hbs</td>
   <td> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td>/libs/social/calendar/components/hbs/calendar/clientlibs/css/calendar.css<br /> /libs/social/calendar/components/hbs/calendar/clientlibs/css/jqueryui.css</td>
  </tr>
  <tr>
   <td><strong> propriedades</strong></td>
   <td>consulte <a href="calendar.md">Usando Calendários</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do cliente](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [APIs de calendário](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [Pontos finais do calendário](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [Personalizações do servidor](server-customize.md)

### Função do calendário {#calendar-function}

Uma estrutura de site da comunidade que inclui a [função Calendar](functions.md#calendar-function) terá um componente `calendar` configurado. A função Calendar suporta a identificação de um [grupo de usuários membro privilegiado](users.md#privileged-members-group).

### Acessar publicações de calendário (UGC) {#accessing-calendar-posts-ugc}

A partir AEM Comunidades 6.1, o uso de uma [loja comum](working-with-srp.md) para UGC inclui acesso programático ao UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso prévio**.

Consulte:

* [Visão geral](srp.md)  do provedor de recursos do armazenamento - introdução e visão geral do uso do repositório
* [SRP e UGC Essentials](srp-and-ugc.md)  - métodos e exemplos de utilitários SRP
* [Acesso ao UGC com diretrizes de codificação do SRP](accessing-ugc-with-srp.md) 
* [Refatoração](socialutils.md)  do SocialUtils - mapeamento de métodos de utilitário obsoletos para os métodos atuais do utilitário SRP

