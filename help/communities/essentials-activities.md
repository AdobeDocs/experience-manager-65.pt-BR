---
title: Princípios básicos de fluxo de Atividade
seo-title: Princípios básicos de fluxo de Atividade
description: Lista de atividades recentes executadas por um membro ou lista de atividades recentes em um único segmento de conteúdo
seo-description: Lista de atividades recentes executadas por um membro ou lista de atividades recentes em um único segmento de conteúdo
uuid: 30c5ac08-0af0-4670-9d81-0beb5c93e00a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 8714b456-527a-457b-82c4-21bd445dfd9c
docset: aem65
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 2%

---


# Princípios básicos de fluxo de Atividade {#activity-stream-essentials}

As atividades de um membro da comunidade conectado, como postar em um fórum ou blog, são coletadas em um fluxo que pode ser filtrado e exibido de várias maneiras pela configuração do componente de fluxos de atividade.

A capacidade de seguir adiciona outro conjunto de atividades quando os membros da comunidade seguem postagens de interesse ou outros membros da comunidade.

Todos os sites [da](/help/communities/overview.md#communitiessites) comunidade incluem uma página de perfil do usuário para o membro conectado que exibirá atividades de membros da mesma maneira.

## Conceitos {#concepts}

Um fluxo *de* atividade é a lista de atividades recentes executadas por um membro ou lista de atividades recentes em um único segmento de conteúdo, como um tópico do fórum ou blog.

Um membro pode seguir um fluxo de atividade seguindo outro indivíduo ou conteúdo.

Um feed *de* notícias é uma união dos fluxos de atividade que um membro segue em um único fluxo.

Um gráfico *[](/help/communities/essentials-socialgraph.md)*social captura os seguintes relacionamentos de um membro para outro.

## Essenciais para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/ative streams/components/hbs/ativitystreams</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclusivo</strong></a></td>
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
   <td>Consulte Recurso <a href="/help/communities/activities.md">Atividades Streams</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do cliente](/help/communities/client-customize.md)

## Fundamentos para servidor {#essentials-for-server-side}

* [API de fluxos de Atividade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/api/package-frame.html)

* [API de ouvinte de fluxos de Atividade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/activitystreams/listener/api/package-frame.html)

* [Personalizações do servidor](/help/communities/server-customize.md)

### Função de fluxo de atividades {#activity-stream-function}

Uma estrutura de site da comunidade que inclui a função [Stream de](/help/communities/functions.md#activity-stream-function)Atividade inclui um `activity streams` componente configurado.
