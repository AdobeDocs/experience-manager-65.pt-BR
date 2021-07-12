---
title: Sites das comunidades
seo-title: Sites das comunidades
description: Visão geral da documentação da AEM Communities
seo-description: Visão geral da documentação da AEM Communities
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 5%

---

# Sites das comunidades {#communities-sites}

Esta seção é para aqueles que administram o AEM Communities e assume familiaridade com recursos do AEM Communities.

## Visão geral {#overview}

Para obter uma visão geral e tutoriais de introdução, visite:

* [Visão geral da AEM Communities](overview.md)
* [Introdução ao AEM Communities](getting-started.md)
* [Introdução ao AEM Communities para ativação](getting-started-enablement.md)

## Tópicos de administração e configuração {#administration-and-configuration-topics}

### Criação e gerenciamento de sites das comunidades {#communities-site-creation-and-management}

* Comunidades [consoles](consoles.md)

   * [Sites](sites-console.md)

      * [Grupos (subcomunidades)](groups.md)
   * [Moderação](moderation.md)
   * [Gerenciamento de membros e grupos](members.md)
   * [Recursos de habilitação](resources.md)
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

* [Loja](working-with-srp.md) UGC comum: escolha do SRP para armazenamento compartilhado do UGC
* [Moderação do UGC](moderate-ugc.md): membros confiáveis podem moderar o UGC em massa ou no contexto
* [Marcação do UGC](tag-ugc.md): podem ser configurados para permitir que os membros marquem o conteúdo
* [Traduzindo UGC](translate-ugc.md): podem ser configurados para traduzir todos os UGC ou permitir que membros traduzam postagens selecionadas
* [Configuração](analytics.md) do Analytics: permitindo que o Adobe Analytics relate várias métricas relacionadas à atividade do membro

### Membros da comunidade {#community-members}

* [Gerenciando usuários e grupos](users.md) de usuários: detalhes dos membros da comunidade e dos grupos de membros, incluindo os membros privilegiados.
* [Limites](limits.md) de contribuição: capacidade de restringir a publicação por novos membros.
* [Serviço](deploy-communities.md#tunnel-service-on-author) de túnel: permite que membros do lado da publicação e grupos de membros sejam acessados do ambiente de criação.
* [consoles](members.md) Membros e Grupos: permite que membros do lado da publicação e grupos de membros sejam criados e gerenciados a partir do ambiente de criação.
* [Sincronização](sync.md) de usuários: para sincronizar membros e grupos de membros em várias instâncias de publicação.
* [Logon no Social com Facebook e Twitter](social-login.md): capacidade de os visitantes do site se tornarem membros da comunidade usando suas credenciais de Facebook ou Twitter.
* [Pontuação e emblemas](implementing-scoring.md): Capacidade de atribuição de cartões para identificar funções de um membro e para que os membros ganhem cartões através da sua participação na comunidade.
* [Notificações](notifications.md): capacidade de notificação de atividades por parte dos membros.
* [Assinaturas](subscriptions.md): capacidade de os membros interagirem com a comunidade usando email externo.
* [Mensagens](messaging.md): capacidade de membros interagirem com a comunidade usando mensagens internas.

### Recursos de habilitação {#enablement-features}

* [Configurando a ativação](enablement.md): as informações necessárias para configurar corretamente os recursos de ativação.
* [Configuração](analytics.md) do Analytics: informações necessárias para ativar os recursos do Adobe Analytics for Communities.
* [Marcar recursos de habilitação](tag-resources.md): necessário para criar catálogos de ativação.

### Implantação {#deployment}

A seção implantação contém informações específicas do AEM Communities.

A natureza do trabalho com conteúdo da comunidade influencia a estrutura da implantação:

* [Topologias recomendadas para comunidades](topologies.md)

É importante instalar a versão mais recente das Comunidades na plataforma AEM:

* [Pacote de recursos das Comunidades mais recentes](deploy-communities.md#latestfeaturepack)

Consulte a página de implantação para obter outras informações específicas das Comunidades, como para [Upgrade](upgrade.md), [Dispatcher](dispatcher.md) e [Replication](deploy-communities.md#replication-agents-on-author).

## Documentação de comunidades relacionadas {#related-communities-documentation}

* Visite [Implantação de comunidades](deploy-communities.md) para saber mais sobre as implantações recomendadas.

* Visite [Desenvolvimento de comunidades](communities.md) para saber mais sobre a estrutura de componentes sociais (SCF) e a personalização de componentes e recursos das Comunidades.

* Visite [Criação de componentes do Communities](author-communities.md) para saber como criar com e configurar componentes do Communities.
