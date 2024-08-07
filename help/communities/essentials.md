---
title: Fundamentos de componentes, funções e recursos
description: Como os sites, modelos e grupos da comunidade funcionam
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 15%

---

# Fundamentos de componentes, funções e recursos  {#component-function-and-feature-essentials}

Os recursos do Adobe Experience Manager (AEM) Communities exigem que os visitantes do site se tornem membros e façam logon no [site da comunidade](overview.md#communitiessites) antes de poder publicar conteúdo. Assim, os [modelos de site da comunidade](sites.md), dos quais um site da comunidade é [criado](sites-console.md), foram projetados para incluir um recurso de logon e perfis de usuário, mensagens, pesquisa, moderação e tradução.

Um site da comunidade permite que membros criem grupos da comunidade quando a [função de grupos da comunidade](functions.md#groups-function) é incluída no modelo de site da comunidade selecionado.

A seguir estão links para informações essenciais para componentes, funções e recursos do Communities.

## Componentes de base {#base-components}

* [Comentários](essentials-comments.md)
* [Revisões](reviews-basics.md)
* [Tally](tally.md)

   * [Curtir](essentials-liking.md)
   * [Avaliação](rating-basics.md)
   * [Votação](essentials-voting.md)
   * *Votação (não está mais disponível)*

## Componentes com funções {#components-with-functions}

* [Fluxos de atividade](essentials-activities.md)
* [Blog](blog-developer-basics.md) ( `Journal`)

* [Calendário](calendar-basics-for-developers.md)
* [Conteúdo incluso](essentials-featured.md)
* [Biblioteca de arquivo](essentials-file-library.md)
* [Fórum](essentials-forum.md)
* [Grupos](essentials-groups.md)
* [Ideação](ideation.md)
* [Placar de líderes](leaderboard.md)
* [Perguntas e respostas](qna-essentials.md) `(QnA)`

## Recursos {#features}

* [Bibliotecas do cliente](clientlibs.md)
* [Sites da comunidade](sites-for-developers.md)
* [Eventos OSGi de componente](events.md)
* [Sideload do componente](sideloading.md)
* [Mensagens](essentials-messaging.md)
* [Editor de rich text](rte.md)
* [Pontuação e medalhas](configure-scoring.md)
* [Pesquisar](search-implementation.md)
* [Gráfico social](essentials-socialgraph.md)
* [Provedor de Recursos de Armazenamento](srp-and-ugc.md) `(SRP)`

* [Marcação com tags](tag.md)

## Javadocs {#javadocs}

Os [javadocs online](../../help/sites-developing/reference-materials.md) refletem as APIs disponíveis na versão AEM 6.3.
As APIs das comunidades estão em `com.adobe.cq.social.*` pacotes.

Para cada [pacote de recursos](deploy-communities.md#latestfeaturepack), um jar javadoc é disponibilizado. Para obter mais informações, visite [Usando o Maven para comunidades](maven.md#javadocs).

## Informações adicionais {#additional-information}

* [Estrutura de componente social (SCF)](scf.md)

   * [Personalizações do lado do cliente](client-customize.md)
   * [Personalizações do lado do servidor](server-customize.md)
   * [Visão geral do provedor de recursos de armazenamento](srp.md)

* [Diretrizes de codificação](code-guide.md)
* [Tutoriais](tutorials.md)
* [Resolução de problemas](troubleshooting.md)
