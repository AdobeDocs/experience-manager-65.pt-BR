---
title: Fundamentos do fluxo de atividade
seo-title: Activity Stream Essentials
description: Lista de atividades recentes executadas por um membro ou uma lista de atividades recentes em um único thread de conteúdo
seo-description: List of recent activites performed by a member or a list of recent activities on a single thread of content
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
exl-id: d98bcbe4-3f80-49ec-b40c-417be0d97350
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 2%

---

# Fundamentos do fluxo de atividade {#activity-stream-essentials}

As atividades de um membro da comunidade assinado, como postar em um fórum ou blog, são coletadas em um fluxo que pode ser filtrado e exibido de várias maneiras pela configuração do componente fluxos de atividade.

A capacidade de seguir adiciona outro conjunto de atividades quando os membros da comunidade seguem postagens de interesse ou outros membros da comunidade.

Todos [sites da comunidade](/help/communities/overview.md#communitiessites) inclua uma página de perfil de usuário para o membro conectado que exibirá as atividades do membro da mesma maneira.

## Conceitos  {#concepts}

Um *fluxo de atividades* é a lista de atividades recentes executadas por um membro ou uma lista de atividades recentes em um único thread de conteúdo, como um tópico ou blog do fórum.

Um membro pode seguir um fluxo de atividade seguindo outro indivíduo ou conteúdo.

A *feed de notícias* é uma mesclagem dos fluxos de atividade que estão sendo seguidos por um membro em um único fluxo.

A *[gráfico social](/help/communities/essentials-socialgraph.md)* captura os seguintes relacionamentos de um membro para outro.

## Fundamentos para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/activitystreams/components/hbs/activitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>incondicional</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.activitystreams</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/activitystreams.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity-title.hbs<br /> /libs/social/activitystreams/components/hbs/activitystreams/activity/activity.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/activitystreams/components/hbs/activitystreams/clientlibs/activitystreams.css</td>
  </tr>
  <tr>
   <td><strong> propriedades</strong></td>
   <td>Consulte <a href="/help/communities/activities.md">Recurso Fluxos de atividade</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](/help/communities/client-customize.md)

## Fundamentos para o lado do servidor {#essentials-for-server-side}

* [API de fluxos de atividade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API do ouvinte de fluxos de atividade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Personalizações do lado do servidor](/help/communities/server-customize.md)

### Função de fluxo de atividades {#activity-stream-function}

Uma estrutura de site da comunidade que inclui a variável [Função de fluxo de atividade](/help/communities/functions.md#activity-stream-function), inclui um `activity streams` componente.
