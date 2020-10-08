---
title: Comunidades em desenvolvimento
seo-title: Comunidades em desenvolvimento
description: Criar e personalizar recursos da comunidade, como fóruns, grupos de usuários e muito mais
seo-description: Criar e personalizar recursos da comunidade, como fóruns, grupos de usuários e muito mais
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 6%

---


# Comunidades em desenvolvimento  {#developing-communities}

## Visão geral {#overview}

A AEM Communities simplifica a criação e personalização de recursos da comunidade, como fóruns, grupos de usuários, blogs, P&amp;R, calendários, comentários, revisões, votação, classificações e atribuições. Esses recursos fazem com que o conteúdo gerado pelo usuário (UGC) seja inserido no ambiente de publicação.

A base de um site [da](overview.md#communitiessites) comunidade é a estrutura [de componentes](scf.md) sociais (SCF). A criação de um site da comunidade começa com a seleção de um modelo [de site da](sites-console.md) comunidade composto por funções [da](functions.md)comunidade.

Para obter uma visão geral e tutoriais de introdução, visite:

* [Visão geral do AEM Communities](overview.md)
* [Introdução ao AEM Communities](getting-started.md)
* [Introdução ao AEM Communities para ativação](getting-started-enablement.md)

>[!NOTE]
> 
>É altamente recomendável manter-se atualizado com as versões [mais recentes](deploy-communities.md#latest-releases).

## Implantações recomendadas {#recommended-deployments}

* [Armazenamento](working-with-srp.md)de conteúdo da comunidade: discute as opções de SRP disponíveis para uma loja comum UGC
* [Topologias recomendadas para comunidades](topologies.md): discute topologias com base no caso de uso e na escolha do SRP

## Estrutura do componente social {#social-component-framework}

* [Estrutura](scf.md)do componente social: visão geral da estrutura e das APIs.
* [Auxiliares](handlebars-helpers.md)de barras de mão SCF: os auxiliares padrão e como escrever os auxiliares personalizados.
* [Personalização](client-customize.md)do cliente: personalização do código executado no navegador.
* [Personalização](server-customize.md)do servidor: personalização do código executado no servidor.
* [Provedor de recursos do armazenamento (SRP)](srp.md): visão geral do armazenamento de conteúdo da comunidade.
* [Diretrizes](code-guide.md)de codificação: orientações, dicas e truques.
* [Guia](components-guide.md)dos componentes da comunidade: ferramenta de desenvolvimento interativo.

## Componentes, funções e recursos básicos {#component-function-and-feature-essentials}

Os componentes, funções e recursos da AEM Communities fornecem os blocos de construção para sites [da](sites-console.md)comunidade.

* [Componentes, funções e recursos básicos](essentials.md)
* [Clientlibs para componentes de comunidades](clientlibs.md)
* [Funções da comunidade](functions.md)
* [Modelos de grupo da comunidade](tools-groups.md)
* [Modelos do site da comunidade](sites.md)

## Membros da comunidade {#community-members}

* [Gerenciamento de usuários e grupos de usuários](users.md)
* [Logon social com Facebook e Twitter](social-login.md)

## Grupos de comunidades {#community-groups}

[Grupos](overview.md#communitygroups) da comunidade é o conceito de permitir que membros da comunidade formem subcomunidades dentro do site da comunidade. A criação de um grupo da comunidade pode ocorrer no ambiente de publicação ou autor.

* [Essenciais do grupo comunitário](essentials-groups.md)
* [Função Grupos](functions.md#groups-function)
* [Modelos de grupo da comunidade](tools-groups.md)
* [Gerenciamento de usuários e grupos de usuários](users.md)
* [Grupos da comunidade para autores](creating-groups.md)

## Gerenciamento de dados {#managing-data}

* [SRP e UGC Essentials](srp-and-ugc.md) - métodos e exemplos do utilitário de API SRP
* [Tag Essentials](tag.md) - possibilidade de membros da comunidade marcarem os recursos de habilitação do UGC e/ou catalogados

## Tutoriais {#tutorials}

* [Tutoriais do cliente](tutorials.md#client-side-customization)
* [Tutoriais do lado do servidor](tutorials.md#server-side-customization)
* [Instruções passo a passo](tutorials.md#how-to-instructions)

## Resolução de problemas {#troubleshooting}

* [Resolução de Problemas](troubleshooting.md)
* [Problemas conhecidos](/help/release-notes/known-issues.md)

## Documentação das Comunidades relacionadas {#related-communities-documentation}

* Visite [Implantação de comunidades](deploy-communities.md) para saber mais sobre as implantações recomendadas e a configuração do dispatcher.

* Visite [Administrando sites](administer-landing.md) de comunidades para saber mais sobre como criar um site da comunidade, configurar modelos de site da comunidade, moderar o conteúdo da comunidade, gerenciar membros e configurar mensagens.

* Visite Componentes [de comunidades de](author-communities.md) criação para saber como criar e configurar componentes de Comunidades.

