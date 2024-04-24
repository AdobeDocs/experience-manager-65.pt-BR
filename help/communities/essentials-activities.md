---
title: Fundamentos do fluxo de atividades
description: Lista de atividades recentes executadas por um membro ou uma lista de atividades recentes em um único thread de conteúdo
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---

# Fundamentos do fluxo de atividades {#activity-stream-essentials}

As atividades de um membro da comunidade conectado, como postar em um fórum ou blog, são coletadas em um fluxo que pode ser filtrado e exibido de várias maneiras por meio da configuração do componente de fluxos de atividade.

A capacidade de seguir o adiciona outro conjunto de atividades quando os membros da comunidade seguem postagens de interesse ou outros membros da comunidade.

Todos [sites da comunidade](/help/communities/overview.md#communitiessites) inclua uma página de perfil do usuário para o membro conectado que exibirá as atividades do membro da mesma maneira.

## Conceitos  {#concepts}

Um *fluxo de atividades* é a lista de atividades recentes executadas por um membro ou uma lista de atividades recentes em um único thread de conteúdo, como um tópico de fórum ou blog.

Um membro pode seguir um fluxo de atividade, seguindo outro indivíduo ou conteúdo.

A *feed de notícias* é uma mesclagem dos fluxos de atividade que estão sendo seguidos por um membro em um único fluxo.

A *[gráfico social](/help/communities/essentials-socialgraph.md)* captura os seguintes relacionamentos de um membro para outro.

## Essentials para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>incluível</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> propriedades</strong></td>
   <td>Consulte <a href="/help/communities/activities.md">Recurso de fluxos de atividade</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](/help/communities/client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [API de fluxos de atividade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API do ouvinte de fluxos de atividade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Personalizações do lado do servidor](/help/communities/server-customize.md)

### Função de fluxo de atividades {#activity-stream-function}

Uma estrutura de site da comunidade que inclui o [Função de fluxo de atividades](/help/communities/functions.md#activity-stream-function), inclui um configurado `activity streams` componente.
