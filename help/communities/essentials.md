---
title: Componentes, funções e recursos essenciais
seo-title: Component, Function and Feature Essentials
description: Como funcionam os sites, modelos e grupos da comunidade
seo-description: How community sites, templates, and groups function
uuid: 6edfca2d-fe5b-4261-b033-51dc2f9dbfd7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 2d308756-79d1-4d69-b51c-d4b6e692a137
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 18%

---

# Componentes, funções e recursos essenciais  {#component-function-and-feature-essentials}

Os recursos do AEM Communities exigem que os visitantes do site se tornem membros e faça logon no [site da comunidade](overview.md#communitiessites) antes de poder postar conteúdo. Assim, [modelos de site da comunidade](sites.md), do qual um site de comunidade é [criado](sites-console.md), foram projetadas para incluir um recurso de logon, bem como perfis de usuário, mensagens, pesquisa, moderação e tradução.

Um site da comunidade dará suporte a membros criando grupos da comunidade quando a variável [função de grupos da comunidade](functions.md#groups-function) está incluído no modelo de site da comunidade selecionado.

A seguir estão links para informações essenciais de componentes, funções e recursos do Communities.

## Componentes básicos {#base-components}

* [Comentários](essentials-comments.md)
* [Revisões](reviews-basics.md)
* [Tally](tally.md)

   * [Curtir](essentials-liking.md)
   * [Classificação](rating-basics.md)
   * [Votação](essentials-voting.md)
   * *Pesquisa (não está mais disponível)*

## Componentes com funções {#components-with-functions}

* [Fluxos de atividade](essentials-activities.md)
* [Atribuições](essentials-assignments.md)
* [Blog](blog-developer-basics.md) ( `Journal`)

* [Calendário](calendar-basics-for-developers.md)
* [Catálogo](catalog-developer-essentials.md)
* [Conteúdo incluso](essentials-featured.md)
* [Biblioteca de arquivos](essentials-file-library.md)
* [Fórum](essentials-forum.md)
* [Grupos](essentials-groups.md)
* [Ideação](ideation.md)
* [Placar de líderes](leaderboard.md)
* [Perguntas e respostas](qna-essentials.md) `(QnA)`

## Recursos {#features}

* [Bibliotecas do cliente](clientlibs.md)
* [Sites da comunidade](sites-for-developers.md)
* [Eventos OSGi do componente](events.md)
* [Sideload de Componente](sideloading.md)
* [Mensagens](essentials-messaging.md)
* [Editor de rich text](rte.md)
* [Pontuação e emblemas](configure-scoring.md)
* [Pesquisar](search-implementation.md)
* [Gráfico social](essentials-socialgraph.md)
* [Provedor de recursos de armazenamento](srp-and-ugc.md) `(SRP)`

* [Marcação com tags](tag.md)

## Javadocs {#javadocs}

O [javadocs online](../../help/sites-developing/reference-materials.md) reflete as APIs disponíveis na versão AEM 6.3.
As APIs do Communities estão em `com.adobe.cq.social.*` pacotes.

Para cada [pacote de recursos](deploy-communities.md#latestfeaturepack), um jar javadoc é disponibilizado. Para obter mais informações, visite [Uso do Maven para comunidades](maven.md#javadocs).

## Informações adicionais {#additional-information}

* [Estrutura de componentes sociais (SCF)](scf.md)

   * [Personalizações do lado do cliente](client-customize.md)
   * [Personalizações do lado do servidor](server-customize.md)
   * [Visão geral do provedor de recursos de armazenamento](srp.md)

* [Diretrizes de codificação](code-guide.md)
* [Tutoriais](tutorials.md)
* [Resolução de problemas](troubleshooting.md)
