---
title: Visão geral do AEM Communities
description: Uma visão geral dos recursos e da configuração do AEM Communities
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 1%

---

# Visão geral do AEM Communities {#aem-communities-overview}

As comunidades do Adobe Experience Manager (AEM) oferecem a capacidade de criar rapidamente um site da comunidade local que melhorou o desempenho e o gerenciamento do site, além de incentivar a conversão de visitantes do site em membros valiosos da comunidade.

## Recursos das comunidades {#communities-features}

O AEM Communities permite o desenvolvimento de uma relação com visitantes do site, que:

* **Informa** por meio de blogs, perguntas e respostas e calendários de eventos,
* Enquanto **obtendo insights** por meio de fóruns, comentários e outros conteúdos da comunidade, geralmente chamados de conteúdo gerado pelo usuário (UGC).
* Ele permite **moderação** por membros confiáveis no ambiente de publicação,
* **Logon no Social** com Twitter e Facebook,
* **Tradução integrada** de conteúdo da comunidade,
* **Criação de grupos da comunidade** no site da comunidade publicado,
* **Pontuação** para conceder medalhas,
* **Compartilhamento de arquivos**,
* **Notificação** e **fluxos de atividade**,
* Permite **marcação** (@mention) outros membros registrados em Conteúdo gerado pelo usuário, para chamar a atenção deles.

Os recursos do Communities podem ser demonstrados usando o [Máquina de demonstração AEM](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponível publicamente em GitHub.com ou com a nova implementação de referência do We.Retail.

## Sites da comunidade {#community-sites}

Um site da comunidade é um site AEM criado com um assistente simples que resulta em um site com vários recursos comuns pré-conectados ao site.

A variável [assistente de criação de site](/help/communities/sites-console.md):

* Reúne recursos do site, com base no site selecionado [modelo do site da comunidade](/help/communities/sites.md) que é:

   * criado de [funções da comunidade](#community-functions)
   * opcional [grupos da comunidade](#communitygroups) recurso

* Usa configurações para definir:

   * moderação
   * fazer logon
   * tradução

* Oferece recursos essenciais:

   * Design responsivo: usos [Temas do twitter Bootstrap](https://getbootstrap.com)

   * Logon : autorregistro, [login social](/help/communities/social-login.md), perfis de usuário

      * Notificações: os membros veem eventos de relevância para eles e conteúdo gerado pelo usuário onde estão [@mentioned](/help/communities/overview.md#mentionssupport).

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

* [Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md)— discute as opções de armazenamento SRP disponíveis para UGC.
* [Topologias recomendadas](/help/communities/topologies.md)— discute topologias com base no caso de uso e na escolha do SRP.
* [Atualização para comunidades do AEM 6.5](/help/communities/upgrade.md)— fornece informações úteis sobre UGC ao mudar para AEM 6.5.

## Consoles das comunidades {#communities-consoles}

No ambiente de criação, o console de navegação global fornece acesso às [Console Communities](/help/communities/consoles.md), que contém:

* [Sites](/help/communities/sites-console.md) console

   * Criação do site
   * Edição do site
   * Gerenciamento do site
   * [Grupos de comunidades](/help/communities/groups.md) console

* [Moderação](/help/communities/moderation.md) console

   * Interface de moderação em massa comum para ambientes de autor e publicação.
   * Novos critérios de filtragem.

* [Membros e grupos](/help/communities/members.md) consoles de gerenciamento

   * Fornece a capacidade de criar e gerenciar usuários do lado da publicação (membros) a partir do ambiente do autor.
   * Fornece a capacidade de proibir membros.
   * Fornece a capacidade de criar e gerenciar grupos de usuários do lado da publicação (grupos de membros) a partir do ambiente de criação.

* [Relatórios](/help/communities/reports.md) console

   * Fornece a capacidade de gerar relatórios sobre atribuições, publicações e visualizações.

O console de ferramentas globais fornece acesso às seguintes ferramentas do Communities:

* [Modelos de site](/help/communities/tools.md#sitetemplatesconsole) console

   * Crie e gerencie modelos de site da comunidade.

* [Modelos de grupo](/help/communities/tools.md#grouptemplatesconsole) console

   * Crie e gerencie modelos do grupo da comunidade.

* [Funções da comunidade](/help/communities/tools.md#communityfunctionsconsole) console

   * Crie e gerencie funções da comunidade.

* [Configuração de armazenamento](/help/communities/tools.md#storageconfiguratonconsole) console

   * Selecione e configure o [armazenamento comum](/help/communities/working-with-srp.md) para o site.

* [Guia do componente](/help/communities/components-guide.md)

   * Um site de exemplo, [Componentes da comunidade](https://localhost:4502/editor.html/content/community-components/en.html) O fornece uma amostra de todos os componentes das Comunidades com sua configuração padrão e a capacidade de experimentar com eles.

## Modelos do site da comunidade {#community-site-templates}

A criação do site da comunidade é baseada na seleção de um modelo de site da comunidade para configurar rapidamente um site da comunidade que seja independente de qualquer site de amostra.

Um modelo de site da comunidade, composto por funções da comunidade e modelos de grupo da comunidade, fornece a estrutura de um site da comunidade, incluindo logon, perfis de usuário, mensagens, menu do site, pesquisa, temas e recursos de marca.

Consulte a [Console de Modelos de site](/help/communities/sites.md).

## Funções da comunidade {#community-functions}

Os recursos esperados de uma experiência da comunidade são bem conhecidos. Com o AEM Communities, esses recursos estão disponíveis como blocos de construção, conhecidos como funções da comunidade.

As funções da comunidade são páginas AEM normais e incluem componentes conectados em um recurso que é facilmente incorporado a um modelo de site da comunidade.

Consulte a [Console de funções da comunidade](/help/communities/functions.md).

## Grupos de comunidades e modelos de grupo {#community-groups-and-group-templates}

O recurso de grupos da comunidade é a capacidade de uma subcomunidade ser criada dinamicamente em um site da comunidade por usuários autorizados e membros da comunidade dos ambientes do autor e de publicação.

No ambiente de criação, os grupos da comunidade (subcomunidades) podem ser criados em um site da comunidade existente ou aninhados em um grupo existente, quando a estrutura do modelo contiver a variável [Função Grupos](/help/communities/functions.md#groups-function).

A criação de um grupo da comunidade exige a seleção de um modelo de grupo da comunidade que forneça o design das páginas do grupo da comunidade. Quando uma função Grupos é adicionada a uma estrutura de modelo, ela é configurada para especificar um modelo de grupo ou para fornecer uma seleção de modelos no momento em que um novo grupo da comunidade é criado.

Consulte também:

* [Console de Grupos de Sites](/help/communities/groups.md) para criar subcomunidades no ambiente de criação.
* [Console de modelos de grupo](/help/communities/tools-groups.md) para criar a estrutura do site para grupos.
* [Introdução ao AEM Communities](/help/communities/getting-started.md) para obter um tutorial sobre como criar rapidamente um site da comunidade, incluindo grupos aninhados.

## Componentes da comunidade {#community-components}

A variável [componentes da comunidade](/help/communities/author-communities.md) a partir do qual um site da comunidade é criado, pode ser usado para adicionar recursos do Communities a qualquer site AEM.

A variável [guia de componentes da comunidade](/help/communities/components-guide.md) O está disponível para exploração interativa dos componentes.

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

A variável [Máquina de demonstração AEM](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) gerencia e executa demonstrações para AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Aplicativos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) e [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), que geralmente exigem mais configuração do que apenas iniciar uma instância do QuickStart. A máquina de demonstração do AEM configurará [infraestrutura](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) como MongoDB, Solr, MySQL, FFmpeg e servidores de email.

A máquina de demonstração AEM inclui:

* A [interface gráfica do usuário](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Scripts Apache ANT com configurações [propriedades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) e [targets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* Pacotes a serem instalados.

A máquina de demonstração do AEM foi testada com sucesso com CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM AEM AEM 6.2, 6.3 e 6.4 no Windows, MacOS e Linux®.

A máquina de demonstração AEM requer uma licença AEM válida.

>[!NOTE]
>
>Exibir um [introdução ao vídeo](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) ao AEM Demo Machine (13:26).

## Documentação do AEM Communities {#aem-communities-documentation}

* Visita [Implantação de comunidades](deploy-communities.md) para saber mais sobre implantações recomendadas.
* Visita [Administração dos sites das comunidades](administer-landing.md) para saber mais sobre como criar um site da comunidade, adicionar grupos da comunidade, configurar modelos de site da comunidade, moderar conteúdo da comunidade, gerenciar membros, marcar, notificações, pontuação e medalhas.
* Visita [Comunidades de desenvolvimento](communities.md) para saber mais sobre a estrutura de componente social (SCF) e a personalização de componentes e recursos do Communities.
* Visita [Criação de componentes das comunidades](author-communities.md) para saber como criar com e configurar componentes das Comunidades.
