---
title: Comunidades de desenvolvimento
seo-title: Developing Communities
description: Crie e personalize recursos da comunidade, como fóruns, grupos de usuários e muito mais
seo-description: Create and customize community features such as forums, user groups, and more
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 5%

---

# Comunidades de desenvolvimento  {#developing-communities}

## Visão geral {#overview}

O AEM Communities simplifica a criação e a personalização de recursos da comunidade, como fóruns, grupos de usuários, blogs, perguntas e respostas, calendários, comentários, revisões, votos, classificações e atribuições. Esses recursos resultam em conteúdo gerado pelo usuário (UGC) sendo inserido no ambiente de publicação.

A fundação de um [site da comunidade](overview.md#communitiessites) é o [estrutura da componente social](scf.md) (SCF). A criação de um site da comunidade começa com a seleção de um [modelo do site da comunidade](sites-console.md) que é composto por [funções da comunidade](functions.md).

Para obter uma visão geral e tutoriais de introdução, visite:

* [Visão geral do AEM Communities](overview.md)
* [Introdução ao AEM Communities](getting-started.md)

>[!NOTE]
> 
>É altamente recomendável manter-se atualizado [versões mais recentes](deploy-communities.md#latest-releases).

## Implantações recomendadas {#recommended-deployments}

* [Armazenamento de conteúdo da comunidade](working-with-srp.md): discute as opções de SRP disponíveis para um armazenamento comum de UGC
* [Topologias recomendadas para comunidades](topologies.md): discute topologias com base no caso de uso e na escolha do SRP

## Estrutura do componente social {#social-component-framework}

* [Estrutura do componente social](scf.md): visão geral da estrutura e das APIs.
* [Auxiliares de Handlebars SCF](handlebars-helpers.md): auxiliares padrão e como gravar auxiliares personalizados.
* [Personalização do lado do cliente](client-customize.md): personalização do código que é executado no navegador.
* [Personalização do lado do servidor](server-customize.md): personalização do código que é executado no servidor.
* [Provedor de recurso de armazenamento (SRP, Storage Resource Provider)](srp.md): visão geral do armazenamento de conteúdo da comunidade.
* [Diretrizes de codificação](code-guide.md): diretrizes, dicas e truques.
* [Guia de componentes da comunidade](components-guide.md): ferramenta de desenvolvimento interativa.

## Fundamentos de componentes, funções e recursos {#component-function-and-feature-essentials}

Os componentes, funções e recursos do AEM Communities fornecem os componentes básicos para [sites da comunidade](sites-console.md).

* [Fundamentos de componentes, funções e recursos](essentials.md)
* [Clientlibs para componentes das comunidades](clientlibs.md)
* [Funções da comunidade](functions.md)
* [Modelos de grupo da comunidade](tools-groups.md)
* [Modelos do site da comunidade](sites.md)

## Membros da comunidade {#community-members}

* [Gerenciar usuários e grupos de usuários](users.md)
* [Logon social com a Facebook e o Twitter](social-login.md)

## Grupos de comunidades {#community-groups}

[Grupos de comunidades](overview.md#communitygroups) é o conceito de permitir que membros da comunidade formem subcomunidades no site da comunidade. A criação de um grupo da comunidade pode ocorrer no ambiente de publicação ou criação.

* [Fundamentos do grupo da comunidade](essentials-groups.md)
* [Função Grupos](functions.md#groups-function)
* [Modelos de grupo da comunidade](tools-groups.md)
* [Gerenciar usuários e grupos de usuários](users.md)
* [Grupos da comunidade para autores](creating-groups.md)

## Gerenciamento de dados {#managing-data}

* [Fundamentos de SRP e UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário SRP API
* [Fundamentos de tags](tag.md) - capacidade dos membros da comunidade de marcar recursos de ativação catalogados e/ou UGC

## Tutoriais {#tutorials}

* [Tutoriais do lado do cliente](tutorials.md#client-side-customization)
* [Tutoriais do lado do servidor](tutorials.md#server-side-customization)
* [Instruções passo a passo](tutorials.md#how-to-instructions)

## Resolução de problemas {#troubleshooting}

* [Resolução de problemas](troubleshooting.md)
* [Problemas conhecidos](/help/release-notes/release-notes.md)

## Documentação de comunidades relacionadas {#related-communities-documentation}

* Visita [Implantação de comunidades](deploy-communities.md) para saber mais sobre as implantações recomendadas e a configuração do dispatcher.

* Visita [Administração dos sites das comunidades](administer-landing.md) para saber mais sobre como criar um site da comunidade, configurar modelos de site da comunidade, moderar o conteúdo da comunidade, gerenciar membros e configurar mensagens.

* Visita [Criação de componentes das comunidades](author-communities.md) para saber como criar com e configurar componentes das Comunidades.
