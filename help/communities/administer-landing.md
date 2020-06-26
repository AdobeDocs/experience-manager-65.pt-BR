---
title: Sites de comunidades
seo-title: Sites de comunidades
description: Visão geral da documentação dos AEM Communities
seo-description: Visão geral da documentação dos AEM Communities
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
translation-type: tm+mt
source-git-commit: 2bd74d5e90aff1146de5c5a0dffd99fc7dd9031c
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 5%

---


# Communities Sites {#communities-sites}

Esta seção destina-se àqueles que administram AEM Communities e assumem familiaridade com os recursos do AEM Communities.

## Visão geral {#overview}

Para obter uma visão geral e tutoriais de introdução, visite:

* [Visão geral dos AEM Communities](overview.md)
* [Introdução ao AEM Communities](getting-started.md)
* [Introdução a AEM Communities para ativação](getting-started-enablement.md)

## Tópicos de administração e configuração {#administration-and-configuration-topics}

### Criação e gerenciamento de sites das comunidades {#communities-site-creation-and-management}

* Consoles [de comunidades](consoles.md)

   * [Sites](sites-console.md)

      * [Grupos (subcomunidades)](groups.md)
   * [Moderação](moderation.md)
   * [Gerenciamento de membros e grupos](members.md)
   * [Recursos de ativação](resources.md)
   * [Relatórios](reports.md)


* [*Ferramentas *](tools.md)das comunidades:

   * [Modelos de site](sites.md)
   * [Modelos de grupo](tools-groups.md)
   * [Funções da comunidade](functions.md)
   * [Configuração de armazenamento](srp-config.md)
   * [Guia do componente](components-guide.md)
   * [Selos](badges.md)


### Conteúdo gerado pelo usuário {#user-generated-content}

Um recurso principal do AEM Communities é a geração de conteúdo gerado pelo usuário (UGC) por visitantes do site (membros) conectados. Para saber mais sobre como trabalhar com o UGC, visite:

* [Loja](working-with-srp.md)UGC comum: escolha de SRP para armazenamento compartilhado de UGC
* [Moderação do UGC](moderate-ugc.md): membros confiáveis podem moderar o UGC em massa ou no contexto
* [Marcação de UGC](tag-ugc.md): os recursos podem ser configurados para permitir que os membros marcem o conteúdo
* [Traduzindo UGC](translate-ugc.md): os recursos podem ser configurados para traduzir todo o UGC ou permitir que os membros traduzam postagens selecionadas
* [Configuração](analytics.md)Analytics: habilitar o Adobe Analytics a relatar várias métricas relacionadas à atividade de membros

### Membros da comunidade {#community-members}

* [Gerenciando usuários e grupos](users.md)de usuários: detalhes sobre membros da comunidade e grupos de membros, incluindo membros privilegiados.
* [Limites](limits.md)de contribuição: capacidade de restringir a publicação por novos membros.
* [Serviço](deploy-communities.md#tunnel-service-on-author)de túnel: permite que membros do lado da publicação e grupos de membros sejam acessados a partir do ambiente do autor.
* [consoles](members.md)de membros e grupos: permite que membros do lado da publicação e grupos de membros sejam criados e gerenciados a partir do ambiente do autor.
* [Sincronização](sync.md)do usuário: para sincronizar membros e grupos de membros em várias instâncias de publicação.
* [Logon social com Facebook e Twitter](social-login.md): capacidade de visitantes do site se tornarem membros da comunidade usando suas credenciais do Facebook ou Twitter.
* [Pontuação e símbolos](implementing-scoring.md): capacidade de atribuição de emblemas para identificar funções de um membro e para que os membros ganhem emblemas através da sua participação na comunidade.
* [Notificações](notifications.md): capacidade de os membros serem notificados da atividade que seguem.
* [Subscrições](subscriptions.md): capacidade de os membros interagirem com a comunidade usando email externo.
* [Mensagens](messaging.md): capacidade de os membros interagirem com a comunidade usando mensagens internas.

### Recursos de ativação {#enablement-features}

* [Configurando a ativação](enablement.md): informações necessárias para configurar corretamente os recursos de ativação.
* [Configuração](analytics.md)Analytics: informações necessárias para ativar os recursos do Adobe Analytics para Comunidades.
* [Marcação de recursos](tag-resources.md)de habilitação: necessário para criar catálogos de ativação.

### Implantação {#deployment}

A seção de implantação contém informações específicas para AEM Communities.

A natureza do trabalho com conteúdo da comunidade influencia a estrutura da implantação:

* [Topologias recomendadas para comunidades](topologies.md)

É importante instalar a versão mais recente das Comunidades na plataforma AEM:

* [Pacote de recursos das Comunidades mais recentes](deploy-communities.md#latestfeaturepack)

Consulte a página de implantação para obter outras informações específicas das Comunidades, como para [Atualização](upgrade.md), [Dispatcher](dispatcher.md) e [Replicação](deploy-communities.md#replication-agents-on-author).

## Documentação das Comunidades relacionadas {#related-communities-documentation}

* Visite [Implantação de comunidades](deploy-communities.md) para saber mais sobre implantações recomendadas.

* Visite Comunidades [em desenvolvimento](communities.md) para saber mais sobre a estrutura de componentes sociais (SCF) e como personalizar componentes e recursos das Comunidades.

* Visite Componentes [de comunidades de](author-communities.md) criação para saber como criar e configurar componentes de Comunidades.
