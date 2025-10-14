---
title: Visão geral do AEM Communities
description: Saiba mais sobre os fundamentos de recursos e configuração do Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 2%

---

# Visão geral do AEM Communities {#aem-communities-overview}

As comunidades do Adobe Experience Manager (AEM) permitem criar rapidamente um site da comunidade local que tem melhorado o desempenho, melhorado o gerenciamento do site e incentiva a conversão de visitantes do site em membros valiosos da comunidade.

## Recursos das comunidades {#communities-features}

O AEM Communities permite o desenvolvimento de uma relação com visitantes do site, que:

* **Informa** por meio de blogs, Q&amp;A e calendários de eventos,
* Ao **obter insights** por meio de fóruns, comentários e outros conteúdos da comunidade, geralmente chamados de conteúdo gerado pelo usuário (UGC).
* Permite a **moderação** por membros confiáveis no ambiente do Publish,
* **Logon social** com o Twitter e o Facebook,
* **Tradução integrada** de conteúdo da comunidade,
* **Criação de grupos da comunidade** a partir do site da comunidade publicado,
* **Pontuação** para medalhas de prêmio,
* **Compartilhamento de arquivos**,
* **Notificações** e **fluxos de atividade**,
* Permite a **marcação** (@mention) de outros membros registrados no Conteúdo Gerado pelo Usuário para chamar sua atenção.

Os recursos das comunidades podem ser demonstrados usando a [Máquina de demonstração do AEM](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponível publicamente em GitHub.com ou com a nova implementação de referência `We.Retail`.

## Sites da comunidade {#community-sites}

Um site da comunidade é um site AEM criado com um assistente simples que resulta em um site com vários recursos comuns pré-conectados ao site.

O [assistente de criação de site](/help/communities/sites-console.md):

* Reúne recursos do site, com base no [modelo de site de comunidade](/help/communities/sites.md) selecionado, que é:

   * compilado de [funções da comunidade](#community-functions)
   * recurso [grupos de comunidades](#communitygroups) opcional

* Usa configurações para definir:

   * moderação
   * fazer logon
   * tradução

* Oferece recursos essenciais:

   * Design responsivo: usa [temas de Bootstrap do Twitter](https://getbootstrap.com)

   * Logon: autorregistro, [logon social](/help/communities/social-login.md), perfis de usuário

      * Notificações:
os membros veem eventos de relevância para eles e conteúdo gerado pelo usuário onde eles são [@mentioned](/help/communities/overview.md#mentionssupport).

      * Mensagens: os membros podem enviar ou receber mensagens no site da comunidade.
      * Pesquisa: capacidade de pesquisar no site da comunidade.
      * Alternância de idioma: capacidade de selecionar um idioma para um [site multilíngue](/help/sites-administering/translation.md).

      * Administração: acesso para membros autorizados moderar e gerenciar usuários no site da comunidade.

* Elimina muitas etapas de criação no nível da página:

   * Marca: upload opcional de uma imagem de banner para exibição em todas as páginas do site da comunidade
   * Menu de navegação: são fornecidos links de navegação para os recursos incluídos no modelo de site da comunidade.

Para experimentar a facilidade de criar rapidamente um site da comunidade, visite [Introdução ao AEM Communities](/help/communities/getting-started.md).

## Persistência de conteúdo da comunidade {#community-content-persistence}

Para melhorar o desempenho e a sincronização do conteúdo da comunidade, o AEM Communities exige um armazenamento comum especificamente para conteúdo gerado pelo usuário (UGC) compartilhado entre todas as instâncias AEM (autor e publicação).

O conteúdo da comunidade é facilmente acessado por meio do SRP (Storage Resource Provider, provedor de recursos de armazenamento), que fornece uma camada para separar o acesso da topologia subjacente e oferece suporte a um armazenamento comum para UGC.

Para saber mais sobre a persistência de conteúdo da comunidade e as implantações recomendadas, consulte:

* [Armazenamento do Conteúdo da Comunidade](/help/communities/working-with-srp.md)—discute as opções de armazenamento SRP disponíveis para UGC.
* [Topologias recomendadas](/help/communities/topologies.md)—discute topologias com base no caso de uso e na escolha do SRP.
* [Atualização para Comunidades AEM 6.5](/help/communities/upgrade.md)—fornece informações úteis sobre UGC ao mudar para AEM 6.5.

## Consoles das comunidades {#communities-consoles}

No ambiente de criação, o console de navegação global fornece acesso ao [console Comunidades](/help/communities/consoles.md), que contém:

* Console do [Sites](/help/communities/sites-console.md)

   * Criação do site
   * Edição do site
   * Gerenciamento do site
   * Console [Grupos de comunidades](/help/communities/groups.md)

* Console de [Moderação](/help/communities/moderation.md)

   * Interface de moderação em massa comum para ambientes do Author e do Publish.
   * Novos critérios de filtragem.

* [Consoles de gerenciamento de Membros e Grupos](/help/communities/members.md)

   * Permite criar e gerenciar usuários (membros) do lado da publicação no ambiente do Autor.
   * Permite proibir membros.
   * Permite criar e gerenciar grupos de usuários do lado da publicação (grupos de membros) no ambiente de criação.

* Console de [Relatórios](/help/communities/reports.md)

   * Permite gerar relatórios sobre atribuições, publicações e visualizações.

O console de ferramentas globais fornece acesso às seguintes ferramentas do Communities:

* Console de [Modelos de Site](/help/communities/tools.md#sitetemplatesconsole)

   * Crie e gerencie modelos de site da comunidade.

* Console [Modelos de grupo](/help/communities/tools.md#grouptemplatesconsole)

   * Crie e gerencie modelos do grupo da comunidade.

* Console [Funções da comunidade](/help/communities/tools.md#communityfunctionsconsole)

   * Crie e gerencie funções da comunidade.

* Console [Configuração de Armazenamento](/help/communities/tools.md#storageconfiguratonconsole)

   * Selecione e configure o [armazenamento comum](/help/communities/working-with-srp.md) para o site.

* [Guia do componente](/help/communities/components-guide.md)

   * Um site de exemplo, [Componentes da Comunidade](https://localhost:4502/editor.html/content/community-components/en.html) fornece uma amostra de todos os componentes das Comunidades com sua configuração padrão e a capacidade de experimentar com eles.

## Modelos do site da comunidade {#community-site-templates}

A criação do site da comunidade é baseada na seleção de um modelo de site da comunidade para configurar rapidamente um site da comunidade que seja independente de qualquer site de amostra.

Um modelo de site da comunidade, composto por funções da comunidade e modelos de grupo da comunidade, fornece a estrutura de um site da comunidade. Ele inclui recursos de logon, perfis de usuário, mensagens, menu do site, pesquisa, temas e marca.

Consulte o [console Modelos de Site](/help/communities/sites.md).

## Funções da comunidade {#community-functions}

Os recursos esperados de uma experiência da comunidade são bem conhecidos. Com o AEM Communities, esses recursos estão disponíveis como blocos de construção, conhecidos como funções da comunidade.

As funções da comunidade são páginas AEM normais e incluem componentes conectados em um recurso que é facilmente incorporado a um modelo de site da comunidade.

Consulte o [console de Funções da comunidade](/help/communities/functions.md).

## Grupos de comunidades e modelos de grupo {#community-groups-and-group-templates}

O recurso de grupos da comunidade é a capacidade de uma subcomunidade ser criada dinamicamente em um site da comunidade por usuários autorizados e membros da comunidade dos ambientes do autor e de publicação.

No ambiente de criação, os grupos da comunidade (subcomunidades) poderão ser criados em um site da comunidade existente ou aninhados em um grupo existente, quando a estrutura do modelo contiver a [função Grupos](/help/communities/functions.md#groups-function).

A criação de um grupo da comunidade exige a seleção de um modelo de grupo da comunidade que forneça o design das páginas do grupo da comunidade. Quando uma função Grupos é adicionada a uma estrutura de modelo, ela é configurada para especificar um modelo de grupo ou para fornecer uma seleção de modelos no momento em que um novo grupo da comunidade é criado.

Consulte também:

* [Console de Grupos de Sites](/help/communities/groups.md) para criar subcomunidades no ambiente de criação.
* [Console de Modelos de Grupo](/help/communities/tools-groups.md) para criar estruturas de site para grupos.
* [Introdução ao AEM Communities](/help/communities/getting-started.md) para obter um tutorial sobre como criar rapidamente um site da comunidade, incluindo grupos aninhados.

## Componentes da comunidade {#community-components}

Os [componentes da comunidade](/help/communities/author-communities.md) a partir dos quais um site da comunidade é criado podem ser usados para adicionar recursos das Comunidades a qualquer Site AEM.

O [guia de componentes da comunidade](/help/communities/components-guide.md) está disponível para exploração interativa dos componentes.

## Comunidade de engajamento {#engagement-community}

Uma comunidade de engajamento é um site da comunidade cujo objetivo é envolver os clientes para informar, solicitar feedback e permitir que eles interajam como membros da comunidade.

Os recursos de uma comunidade de engajamento podem incluir:

* Logon
* Mensagens
* Fóruns
* Comentários
* Revisões
* Classificações
* Votação
* Blogs
* Grupos
* Calendários
* Tradução
* Moderação
* Notificações
* Pontuação e medalhas
* Relatórios do Analytics

Para experimentar a facilidade de criar rapidamente uma comunidade de envolvimento, visite [Introdução ao AEM Communities](/help/communities/getting-started.md).

## Máquina de demonstração AEM {#aem-demo-machine}

A [Máquina de Demonstração do AEM](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) gerencia e executa demonstrações para AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) e [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), que geralmente exigem mais configuração do que simplesmente iniciar uma instância do QuickStart. A Máquina de Demonstração do AEM configura uma [infraestrutura](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) adicional, como MongoDB, Solr, MySQL, FFmpeg e servidores de email.

A máquina de demonstração AEM inclui:

* Uma [interface gráfica](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Apache ANT scripts com [propriedades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) e [destinos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line) configuráveis.

* Pacotes a serem instalados.

A máquina de demonstração do AEM foi testada com sucesso com CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM AEM AEM 6.2, 6.3 e 6.4 no Windows, macOS e Linux®.

A máquina de demonstração AEM requer uma licença AEM válida.

>[!NOTE]
>
>Assista a uma [introdução ao vídeo](https://www.youtube.com/watch?v=zEE_zkR9fVQ&feature=youtu.be) da máquina de demonstração do AEM (13:26).

## Documentação do AEM Communities {#aem-communities-documentation}

* Visite [Implantando Comunidades](deploy-communities.md), onde você pode obter mais informações sobre as implantações recomendadas.
* Visite [Administrando sites de comunidades](administer-landing.md), onde você pode aprender a criar um site de comunidade, adicionar grupos de comunidade, configurar modelos de site de comunidade, moderar conteúdo de comunidade, gerenciar membros, marcar, notificações, pontuação e medalhas.
* Visite [Comunidades de Desenvolvimento](communities.md), onde você pode saber mais sobre a estrutura do componente social (SCF) e sobre como personalizar componentes e recursos das Comunidades.
* Visite [Criação de componentes das comunidades](author-communities.md), onde você pode aprender a criar e configurar componentes das comunidades.
