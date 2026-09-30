---
title: Fundamentos do calendário
description: Saiba como trabalhar com o recurso Calendário no Experience Manager Communities. O Calendário oferece suporte à identificação de grupos de usuários membros privilegiados.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 069e379d-c6fd-49ca-b337-df6fd466e023
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%
---
# Fundamentos do calendário {#calendar-essentials}

Esta página fornece informações essenciais sobre como trabalhar com o recurso de calendário.

## Essentials para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/calendar/components/hbs/calendar</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluível</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.calendar</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
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

* [Personalizações do lado do cliente](client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [APIs de calendário](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/calendar/client/api/package-summary.html)

* [Endpoints de calendário](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/cq/social/calendar/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Função do calendário {#calendar-function}

Uma estrutura de site de comunidade que inclui a [função de Calendário](functions.md#calendar-function) tem um componente `calendar` configurado. A função Calendário oferece suporte à identificação de um [grupo de usuários membro privilegiado](users.md#privileged-members-group).

### Acessar publicações do calendário (UGC) {#accessing-calendar-posts-ugc}

A partir do AEM 6.1 Communities, o uso de um [armazenamento comum](working-with-srp.md) para UGC inclui acesso programático a UGC, independentemente da opção de armazenamento escolhida (como ASRP, MSRP ou JSRP).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso**.

Consulte:

* [Visão Geral do Provedor de Recursos de Armazenamento](srp.md) - introdução e visão geral do uso do repositório
* [Fundamentos do SRP e do UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário SRP
* [Acessando UGC com SRP](accessing-ugc-with-srp.md) - diretrizes de codificação
* [Refatoração de SocialUtils](socialutils.md) - mapeando métodos de utilitário obsoletos para métodos de utilitário SRP atuais
