---
title: Sites das comunidades
seo-title: Communities Sites
description: Visão geral da documentação da AEM Communities
seo-description: Overview of the AEM Communities documentation
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 4%

---

# Sites das comunidades {#communities-sites}

Esta seção é para aqueles que administram o AEM Communities e assume familiaridade com recursos do AEM Communities.

## Visão geral {#overview}

Para obter uma visão geral e tutoriais de introdução, visite:

* [Visão geral da AEM Communities](overview.md)
* [Introdução ao AEM Communities](getting-started.md)

## Tópicos de administração e configuração {#administration-and-configuration-topics}

### Criação e gerenciamento de sites das comunidades {#communities-site-creation-and-management}

* Comunidades [consoles](consoles.md)

   * [Sites](sites-console.md)

      * [Grupos (subcomunidades)](groups.md)
   * [Moderação](moderation.md)
   * [Gerenciamento de membros e grupos](members.md)
   * [Relatórios](reports.md)


* Comunidades [*ferramentas*](tools.md):

   * [Modelos de site](sites.md)
   * [Modelos de grupo](tools-groups.md)
   * [Funções da comunidade](functions.md)
   * [Configuração de armazenamento](srp-config.md)
   * [Guia do componente](components-guide.md)
   * [Selos](badges.md)


### Conteúdo gerado pelo usuário {#user-generated-content}

Um recurso importante do AEM Communities é a geração de conteúdo gerado pelo usuário (UGC) por visitantes do site que fizeram logon (membros). Para saber mais sobre como trabalhar com a visita do UGC:

* [Loja UGC comum](working-with-srp.md): escolha do SRP para armazenamento compartilhado do UGC
* [Moderação do UGC](moderate-ugc.md): membros confiáveis podem moderar o UGC em massa ou no contexto
* [Marcação de UGC](tag-ugc.md): podem ser configurados para permitir que os membros marquem o conteúdo
* [Tradução de UGC](translate-ugc.md): podem ser configurados para traduzir todos os UGC ou permitir que membros traduzam postagens selecionadas
* [Configuração do Analytics](analytics.md): permitindo que o Adobe Analytics relate várias métricas relacionadas à atividade do membro

### Membros da comunidade {#community-members}

* [Gerenciar usuários e grupos de usuários](users.md): detalhes dos membros da comunidade e dos grupos de membros, incluindo os membros privilegiados.
* [Limites de contribuição](limits.md): capacidade de restringir a publicação por novos membros.
* [Serviço de túnel](deploy-communities.md#tunnel-service-on-author): permite que membros do lado da publicação e grupos de membros sejam acessados do ambiente de criação.
* [Consoles Membros e grupos](members.md): permite que membros do lado da publicação e grupos de membros sejam criados e gerenciados a partir do ambiente de criação.
* [Sincronização de usuários](sync.md): para sincronizar membros e grupos de membros em várias instâncias de publicação.
* [Logon no Social com Facebook e Twitter](social-login.md): capacidade de os visitantes do site se tornarem membros da comunidade usando suas credenciais de Facebook ou Twitter.
* [Pontuação e emblemas](implementing-scoring.md): Capacidade de atribuição de cartões para identificar funções de um membro e para que os membros ganhem cartões através da sua participação na comunidade.
* [Notificações](notifications.md): capacidade de notificação de atividades por parte dos membros.
* [Subscrições](subscriptions.md): capacidade de os membros interagirem com a comunidade usando email externo.
* [Mensagens](messaging.md): capacidade de membros interagirem com a comunidade usando mensagens internas.

### Implantação {#deployment}

A seção implantação contém informações específicas do AEM Communities.

A natureza do trabalho com conteúdo da comunidade influencia a estrutura da implantação:

* [Topologias recomendadas para comunidades](topologies.md)

É importante instalar a versão mais recente das Comunidades na plataforma AEM:

* [Pacote de recursos das Comunidades mais recentes](deploy-communities.md#latestfeaturepack)

Consulte a página de implantação para obter outras informações específicas das Comunidades, como para [Atualização](upgrade.md), [Dispatcher](dispatcher.md) e [Replicação](deploy-communities.md#replication-agents-on-author).

## Documentação de comunidades relacionadas {#related-communities-documentation}

* Visita [Implantação de comunidades](deploy-communities.md) para saber mais sobre implantações recomendadas.

* Visita [Desenvolvimento de comunidades](communities.md) para saber mais sobre a estrutura de componentes sociais (SCF) e personalizar os componentes e recursos das Comunidades.

* Visita [Componentes de comunidades de criação](author-communities.md) para saber como criar e configurar componentes do Communities.
