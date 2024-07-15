---
title: Sites de comunidades
description: Saiba mais sobre os fundamentos das comunidades Adobe Experience Manager (AEM) para administradores que já estão familiarizados com seus recursos básicos.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 4%

---

# Sites de comunidades {#communities-sites}

Esta seção é para quem administra o AEM Communities e presume familiaridade com os recursos do AEM Communities.

## Visão geral {#overview}

Para obter uma visão geral e tutoriais de introdução, visite:

* [Visão geral do AEM Communities](overview.md)
* [Introdução ao AEM Communities](getting-started.md)

## Tópicos de Administração e Configuração {#administration-and-configuration-topics}

### Criação e gerenciamento de sites de comunidades {#communities-site-creation-and-management}

* Comunidades [consoles](consoles.md)

   * [Sites](sites-console.md)

      * [Grupos (subcomunidades)](groups.md)

   * [Moderação](moderation.md)
   * [Gerenciamento de Membros e Grupos](members.md)
   * [Relatórios](reports.md)

* Comunidades [*ferramentas*](tools.md):

   * [Modelos de site](sites.md)
   * [Modelos de grupo](tools-groups.md)
   * [Funções da comunidade](functions.md)
   * [Configuração de armazenamento](srp-config.md)
   * [Guia do componente](components-guide.md)
   * [Selos](badges.md)


### Conteúdo gerado pelo usuário {#user-generated-content}

Um recurso importante do AEM Communities é a geração de conteúdo gerado pelo usuário (UGC) por visitantes do site conectados (membros). Para saber mais sobre como trabalhar com UGC, visite:

* [Repositório UGC Comum](working-with-srp.md): escolha de SRP para armazenamento compartilhado de UGC
* [UGC de moderação](moderate-ugc.md): membros confiáveis podem moderar UGC em massa ou no contexto
* [Marcando UGC](tag-ugc.md): os recursos podem ser configurados para permitir que os membros marquem o conteúdo
* [Traduzindo UGC](translate-ugc.md): os recursos podem ser configurados para traduzir todos os UGC ou permitir que membros traduzam postagens selecionadas
* [Configuração do Analytics](analytics.md): permitir que o Adobe Analytics relate várias métricas relacionadas à atividade do membro

### Membros da comunidade {#community-members}

* [Gerenciamento de Usuários e Grupos de Usuários](users.md): detalhes de membros da comunidade e grupos de membros, incluindo membros privilegiados.
* [Limites de contribuição](limits.md): capacidade de restringir a postagem por novos membros.
* [Serviço de Túnel](deploy-communities.md#tunnel-service-on-author): permite que membros do lado da publicação e grupos de membros sejam acessados do ambiente de criação.
* [Consoles de membros e grupos](members.md): permite que membros do lado da publicação e grupos de membros sejam criados e gerenciados no ambiente de criação.
* [Sincronização de Usuário](sync.md): para sincronizar membros e grupos de membros em várias instâncias de publicação.
* [Logon no Social com o Facebook e o Twitter](social-login.md): capacidade de os visitantes do site se tornarem membros da comunidade usando suas credenciais do Facebook ou do Twitter.
* [Pontuação e medalhas](implementing-scoring.md): capacidade de atribuir medalhas para identificar funções de um membro e para que os membros ganhem medalhas por meio de sua participação na comunidade.
* [Notificações](notifications.md): capacidade de os membros serem notificados sobre as atividades que seguem.
* [Assinaturas](subscriptions.md): capacidade de os membros interagirem com a comunidade usando email externo.
* [Mensagens](messaging.md): capacidade de os membros interagirem com a comunidade usando mensagens internas.

### Implantação {#deployment}

A seção de implantação contém informações específicas do AEM Communities.

A natureza do trabalho com conteúdo da comunidade influencia a estrutura da implantação:

* [Topologias recomendadas para comunidades](topologies.md)

É importante instalar a versão mais recente do Communities na plataforma AEM:

* [Pacote de recursos mais recente do Communities](deploy-communities.md#latestfeaturepack)

Consulte a página de implantação para outras informações específicas das comunidades, como para [Atualização](upgrade.md), [Dispatcher](dispatcher.md) e [Replicação](deploy-communities.md#replication-agents-on-author).

## Documentação de comunidades relacionadas {#related-communities-documentation}

* Visite [Implantando Comunidades](deploy-communities.md), onde você pode obter mais informações sobre as implantações recomendadas.

* Visite [Comunidades de Desenvolvimento](communities.md), onde você pode saber mais sobre a estrutura do componente social (SCF) e sobre como personalizar componentes e recursos das Comunidades.

* Visite [Criação de componentes das comunidades](author-communities.md), onde você pode aprender a criar e configurar componentes das comunidades.
