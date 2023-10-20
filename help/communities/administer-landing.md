---
title: Sites de comunidades
description: Saiba mais sobre os fundamentos das comunidades Adobe Experience Manager (AEM) para administradores que já estão familiarizados com seus recursos básicos.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
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

* Communities [consoles](consoles.md)

   * [Sites](sites-console.md)

      * [Grupos (subcomunidades)](groups.md)

   * [Moderação](moderation.md)
   * [Gerenciamento de Membros e Grupos](members.md)
   * [Relatórios](reports.md)

* Communities [*ferramentas*](tools.md):

   * [Modelos de site](sites.md)
   * [Modelos de grupo](tools-groups.md)
   * [Funções da comunidade](functions.md)
   * [Configuração de armazenamento](srp-config.md)
   * [Guia do componente](components-guide.md)
   * [Selos](badges.md)


### Conteúdo gerado pelo usuário {#user-generated-content}

Um recurso importante do AEM Communities é a geração de conteúdo gerado pelo usuário (UGC) por visitantes do site conectados (membros). Para saber mais sobre como trabalhar com UGC, visite:

* [Armazenamento de UGC comum](working-with-srp.md): opção de SRP para armazenamento compartilhado de UGC
* [Moderação de UGC](moderate-ugc.md): membros confiáveis podem moderar o UGC em massa ou no contexto
* [Marcação de UGC](tag-ugc.md): recursos podem ser configurados para permitir que os membros marquem o conteúdo
* [Tradução de UGC](translate-ugc.md): os recursos podem ser configurados para traduzir todos os UGC ou permitir que os membros traduzam postagens selecionadas
* [Configuração do Analytics](analytics.md): permitir que o Adobe Analytics relate várias métricas relacionadas à atividade do membro

### Membros da comunidade {#community-members}

* [Gerenciar usuários e grupos de usuários](users.md): detalhes de membros da comunidade e grupos de membros, incluindo membros privilegiados.
* [Limites de contribuição](limits.md): capacidade de restringir a publicação por novos membros.
* [Serviço de túnel](deploy-communities.md#tunnel-service-on-author): permite que membros do lado da publicação e grupos de membros sejam acessados do ambiente de criação.
* [Consoles Membros e grupos](members.md): permite que membros do lado da publicação e grupos de membros sejam criados e gerenciados no ambiente de criação.
* [Sincronização de usuário](sync.md): para sincronizar membros e grupos de membros em várias instâncias de publicação.
* [Social Faça logon com o Facebook e o Twitter](social-login.md): capacidade dos visitantes do site de se tornarem membros da comunidade usando suas credenciais do Facebook ou do Twitter.
* [Pontuação e medalhas](implementing-scoring.md): capacidade de atribuir medalhas para identificar funções de um membro e de os membros ganharem medalhas por meio de sua participação na comunidade.
* [Notificação](notifications.md): capacidade de os membros serem notificados sobre a atividade que seguem.
* [Assinaturas](subscriptions.md): capacidade de os membros interagirem com a comunidade usando email externo.
* [Mensagens](messaging.md): capacidade dos membros de interagir com a comunidade usando mensagens internas.

### Implantação {#deployment}

A seção de implantação contém informações específicas do AEM Communities.

A natureza do trabalho com conteúdo da comunidade influencia a estrutura da implantação:

* [Topologias recomendadas para comunidades](topologies.md)

É importante instalar a versão mais recente do Communities na plataforma AEM:

* [Pacote de recursos mais recente do Communities](deploy-communities.md#latestfeaturepack)

Consulte a página de implantação para outras informações específicas das comunidades, como para [Atualizando](upgrade.md), [Dispatcher](dispatcher.md), e [Replicação](deploy-communities.md#replication-agents-on-author).

## Documentação de comunidades relacionadas {#related-communities-documentation}

* Visita [Implantação de comunidades](deploy-communities.md) onde você pode saber mais sobre implantações recomendadas.

* Visita [Comunidades de desenvolvimento](communities.md) onde você pode saber mais sobre a estrutura do componente social (SCF) e personalização de componentes e recursos do Communities.

* Visita [Criação de componentes das comunidades](author-communities.md) onde você pode aprender a criar com e configurar componentes de Comunidades.
