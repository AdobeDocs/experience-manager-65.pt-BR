---
title: Desenvolvimento de comunidades
seo-title: Developing Communities
description: Crie e personalize recursos da comunidade como fóruns, grupos de usuários e muito mais
seo-description: Create and customize community features such as forums, user groups, and more
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 6%

---

# Desenvolvimento de comunidades  {#developing-communities}

## Visão geral {#overview}

O AEM Communities simplifica a criação e personalização de recursos da comunidade, como fóruns, grupos de usuários, blogs, P&amp;A, calendários, comentários, revisões, votação, classificações e atribuições. Esses recursos resultam na inserção do conteúdo gerado pelo usuário (UGC) no ambiente de publicação.

A base de um [site da comunidade](overview.md#communitiessites) é [estrutura de componentes sociais](scf.md) (CCAH). A criação de um site da comunidade começa com a seleção de um [modelo de site da comunidade](sites-console.md) que é composto por [funções da comunidade](functions.md).

Para obter uma visão geral e tutoriais de introdução, visite:

* [Visão geral da AEM Communities](overview.md)
* [Introdução ao AEM Communities](getting-started.md)
* [Introdução ao AEM Communities para ativação](getting-started-enablement.md)

>[!NOTE]
> 
>É altamente recomendável manter-se atualizado com a variável [versões mais recentes](deploy-communities.md#latest-releases).

## Implantações recomendadas {#recommended-deployments}

* [Armazenamento de conteúdo da comunidade](working-with-srp.md): discute as opções de SRP disponíveis para uma loja comum UGC
* [Topologias recomendadas para comunidades](topologies.md): discute topologias com base no caso de uso e na escolha da SRP

## Estrutura do componente social {#social-component-framework}

* [Estrutura do componente social](scf.md): visão geral da estrutura e das APIs.
* [Auxiliares do Handlebars do SCF](handlebars-helpers.md): ajuda padrão e como gravar ajuda personalizada.
* [Personalização do lado do cliente](client-customize.md): personalização do código executado no navegador.
* [Personalização do lado do servidor](server-customize.md): personalização do código executado no servidor.
* [Provedor de recursos de armazenamento (SRP)](srp.md): visão geral do armazenamento de conteúdo da comunidade.
* [Diretrizes de codificação](code-guide.md): orientações, dicas e truques.
* [Guia de componentes da comunidade](components-guide.md): ferramenta de desenvolvimento interativo.

## Componentes, funções e recursos essenciais {#component-function-and-feature-essentials}

Os componentes, funções e recursos do AEM Communities fornecem os blocos de construção para [sites da comunidade](sites-console.md).

* [Componentes, funções e recursos essenciais](essentials.md)
* [Clientlibs para componentes do Communities](clientlibs.md)
* [Funções da comunidade](functions.md)
* [Modelos de grupo da comunidade](tools-groups.md)
* [Modelos do site da comunidade](sites.md)

## Membros da comunidade {#community-members}

* [Gerenciar usuários e grupos de usuários](users.md)
* [Logon no Social com Facebook e Twitter](social-login.md)

## Grupos de comunidades {#community-groups}

[Grupos da comunidade](overview.md#communitygroups) é o conceito de permitir que membros da comunidade formem subcomunidades no site da comunidade. A criação de um grupo da comunidade pode ocorrer no ambiente de publicação ou criação.

* [Fundamentos do grupo comunitário](essentials-groups.md)
* [Função de grupos](functions.md#groups-function)
* [Modelos de grupo da comunidade](tools-groups.md)
* [Gerenciar usuários e grupos de usuários](users.md)
* [Grupos da comunidade para autores](creating-groups.md)

## Gerenciamento de dados {#managing-data}

* [Princípios básicos de SRP e UGC](srp-and-ugc.md) - Métodos e exemplos do utilitário de API SRP
* [Tag Essentials](tag.md) - capacidade de membros da comunidade marcarem recursos de habilitação de UGC e/ou catalogados

## Tutoriais {#tutorials}

* [Tutoriais do lado do cliente](tutorials.md#client-side-customization)
* [Tutoriais do lado do servidor](tutorials.md#server-side-customization)
* [Instruções de instruções](tutorials.md#how-to-instructions)

## Resolução de problemas {#troubleshooting}

* [Resolução de problemas](troubleshooting.md)
* [Problemas conhecidos](/help/release-notes/release-notes.md)

## Documentação de comunidades relacionadas {#related-communities-documentation}

* Visita [Implantação de comunidades](deploy-communities.md) para saber mais sobre as implantações recomendadas e a configuração do dispatcher.

* Visita [Administrar sites das comunidades](administer-landing.md) para saber mais sobre como criar um site da comunidade, configurar modelos de site da comunidade, moderar o conteúdo da comunidade, gerenciar membros e configurar mensagens.

* Visita [Componentes de comunidades de criação](author-communities.md) para saber como criar e configurar componentes do Communities.
