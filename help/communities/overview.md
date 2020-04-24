---
title: Visão geral do AEM Communities
seo-title: Visão geral do AEM Communities
description: Uma visão geral dos recursos e da configuração do AEM Communities
seo-description: Uma visão geral dos recursos e da configuração do AEM Communities
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
translation-type: tm+mt
source-git-commit: 48afa2146d0dcbab4beaa1044645c269b49fd7ff

---


# Visão geral do AEM Communities {#aem-communities-overview}

O Adobe Experience Manager (AEM) Communities oferece a capacidade de criar rapidamente um site local da comunidade com o melhor desempenho, gerenciamento de site, e estimula a conversão de visitantes do site em membros de alto valor da Comunidade.

Entre em contato com seu representante de conta para obter informações sobre o licenciamento do AEM Communities, além de licenças adicionais para recursos de ativação e Adobe Analytics.

## Recursos das comunidades {#communities-features}

O AEM Communities permite o desenvolvimento de uma relação com visitantes do site, que:

* **Informa** por meio de blogs, P&amp;R e calendários de eventos,
* Ao **obter insights** por meio de fóruns, comentários e outros conteúdos da comunidade, geralmente conhecidos como conteúdo gerado pelo usuário (UGC).
* Permite a **moderação** por membros confiáveis no ambiente de publicação,
* **Logon** social com Twitter e Facebook,
* **tradução** em linha do conteúdo comunitário,
* **criação** de grupos comunitários a partir do sítio da comunidade publicada,
* **Pontuação** para atribuir cartões,
* **Partilha** de ficheiros,
* **Notificações** e fluxos de **atividade**,
* Permite **marcar** (@menção) outros membros registrados no Conteúdo gerado pelo usuário, para chamar a atenção deles.
* Suporta a navegação **pelo** teclado em componentes de ativação (por exemplo, Catálogo e Reprodução do curso, Atribuições, Biblioteca de arquivos).

Os recursos das comunidades podem ser demonstrados usando a Máquina [de demonstração do](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) AEM disponível publicamente em GitHub.com ou com a nova implementação de referência We.Retail.

## Sites da comunidade {#community-sites}

Um site da comunidade é um site do AEM criado usando um assistente simples que resulta em um site com muitos recursos comuns pré-conectados ao site.

O assistente [de criação de](/help/communities/sites-console.md)site:

* Reúne os recursos do site, com base no modelo [de site da](/help/communities/sites.md) comunidade selecionada, que é:

   * criado a partir de funções de [comunidade](#community-functions)
   * recurso opcional [de grupos](#communitygroups) da comunidade

* Usa as configurações para configurar:

   * moderação
   * login
   * tradução

* Fornece recursos essenciais:

   * Design responsivo: usa temas [do Twitter Bootstrap](https://getbootstrap.com)

   * Logon : autorregistro, login [](/help/communities/social-login.md)social, perfis do usuário

      * Notificações:
os membros veem eventos de relevância para eles e conteúdo gerado pelo usuário onde eles são [@mencionados](/help/communities/overview.md#mentionssupport).

      * Mensagens: os membros podem enviar ou receber mensagens no site da comunidade.
      * Pesquisar: capacidade de pesquisar no site da comunidade.
      * Mudança de idioma: capacidade de selecionar um idioma para um site [](/help/sites-administering/translation.md)multilíngue.

      * Administração: acesso de membros autorizados para moderar e gerenciar usuários no site da comunidade.

* Elimina várias etapas de criação no nível da página:

   * Marca: carregamento opcional de uma imagem de banner para exibição em todas as páginas do site da comunidade
      * Menu de navegação: os links de navegação são fornecidos para os recursos incluídos no modelo de site da comunidade.

Para experimentar a facilidade de criar rapidamente um novo site da comunidade, visite [Introdução ao AEM Communities](/help/communities/getting-started.md).

## Persistência do conteúdo da comunidade {#community-content-persistence}

Para melhorar o desempenho e a sincronização do conteúdo da comunidade, o AEM Communities exige uma loja comum especificamente para o conteúdo gerado pelo usuário (UGC) compartilhado entre todas as instâncias do AEM (autor e publicação).

O conteúdo da comunidade é facilmente acessado por meio do SRP (armazenamento Resource Provider, provedor de recursos do ), que fornece uma camada para separar o acesso da topologia subjacente e oferece suporte a uma loja comum para UGC.

Para saber mais sobre a persistência do conteúdo da comunidade e as implantações recomendadas, consulte:

* [Community Content Armazenamento](/help/communities/working-with-srp.md), que discute as opções disponíveis do armazenamento SRP para UGC.
* [Topologias](/help/communities/topologies.md)recomendadas, que discute topologias com base no caso de uso e na escolha do SRP.
* [Atualização para o AEM 6.5 Communities](/help/communities/upgrade.md), que fornece informações úteis sobre o UGC ao mudar para o AEM 6.5.

## Consoles de comunidades {#communities-consoles}

No ambiente do autor, o console de navegação global fornece acesso ao console [](/help/communities/consoles.md)Comunidades, que contém:

* [Console de sites](/help/communities/sites-console.md)

   * Criação de sites
   * Edição de site
   * Gerenciamento de sites
   * [Console de grupos](/help/communities/groups.md) da comunidade

* [Console de moderação](/help/communities/moderation.md)

   * Interface do usuário comum de moderação em massa para ambientes de autor e publicação.
   * Novos critérios de filtragem.

* [Consoles de gerenciamento de membros e grupos](/help/communities/members.md)

   * Fornece a capacidade de criar e gerenciar usuários do lado da publicação (membros) a partir do ambiente do autor.
   * Permite proibir membros.
   * Fornece a capacidade de criar e gerenciar grupos de usuários do lado da publicação (grupos de membros) a partir do ambiente do autor.

* [Console de relatórios](/help/communities/reports.md)

   * Fornece a capacidade de gerar relatórios em atribuições, publicações e visualizações.

* [Console de recursos](/help/communities/resources.md)

   * Fornece a capacidade de criar recursos de ativação e caminhos de aprendizado.
   * Fornece acesso a relatórios sobre recursos de ativação e caminhos de aprendizado.

O console de ferramentas globais fornece acesso às seguintes ferramentas de Comunidades:

* [Console de Modelos](/help/communities/tools.md#sitetemplatesconsole) de site

   * Crie e gerencie modelos de site da comunidade.

* [Console Modelos](/help/communities/tools.md#grouptemplatesconsole) de grupo

   * Crie e gerencie modelos de grupos da comunidade.

* [Console de funções](/help/communities/tools.md#communityfunctionsconsole) da comunidade

   * Crie e gerencie funções da comunidade.

* [Console de configuração](/help/communities/tools.md#storageconfiguratonconsole) do Armazenamento

   * Selecione e configure a loja [](/help/communities/working-with-srp.md) comum do site.

* [Guia do componente](/help/communities/components-guide.md)

   * Um site de amostra, [Community Components](https://localhost:4502/editor.html/content/community-components/en.html), que fornece uma amostra de todos os componentes das Comunidades com sua configuração padrão e a capacidade de experimentar com eles.

## Modelos do site da comunidade {#community-site-templates}

A criação de site da comunidade é baseada na seleção de um modelo de site da comunidade para configurar rapidamente um site da comunidade que é independente de qualquer site de amostra.

Um modelo de site da comunidade, composto de funções da comunidade e modelos de grupo da comunidade, fornece a estrutura para um site da comunidade, incluindo login, perfis do usuário, mensagens, menu do site, pesquisa, temas e recursos de marca.

Consulte o console [Modelos de](/help/communities/sites.md)site.

## Funções da comunidade {#community-functions}

Os recursos esperados de uma experiência da comunidade são bem conhecidos. Com o AEM Communities, esses recursos estão disponíveis como blocos de construção, conhecidos como funções da comunidade.

As funções da comunidade são páginas normais do AEM que incluem componentes conectados em conjunto em um recurso que é facilmente incorporado em um modelo de site da comunidade.

Consulte o console [Funções da](/help/communities/functions.md)comunidade.

## Grupos da comunidade e modelos de grupo {#community-groups-and-group-templates}

O recurso de grupos da comunidade é a capacidade de uma subcomunidade ser criada dinamicamente em um site da comunidade por usuários autorizados e membros da comunidade do autor e dos ambientes de publicação.

No ambiente do autor, grupos da comunidade (subcomunidades) podem ser criados dentro de um site da comunidade existente ou aninhados dentro de um grupo existente, quando a estrutura do modelo contém a função [](/help/communities/functions.md#groups-function)Grupos.

A criação de um grupo da comunidade requer a seleção de um modelo de grupo da comunidade que forneça o design das páginas de grupo da comunidade. Quando uma função Grupos é adicionada a uma estrutura de modelo, ela é configurada para especificar um modelo de grupo ou para fornecer uma opção de modelos no momento em que um novo grupo da comunidade é criado.

Consulte também:

* [Console](/help/communities/groups.md) de grupos de sites para criar subcomunidades no ambiente do autor.
* [Console](/help/communities/tools-groups.md) Modelos de grupo para criar a estrutura do site para grupos.
* [Introdução ao AEM Communities](/help/communities/getting-started.md) para tutorial para criar rapidamente um site da comunidade, incluindo grupos aninhados.

## Componentes da comunidade {#community-components}

Os componentes [da](/help/communities/author-communities.md) comunidade a partir dos quais um site da comunidade é criado podem ser usados para adicionar recursos das Comunidades a qualquer site do AEM.

O guia [de componentes da](/help/communities/components-guide.md) comunidade está disponível para exploração interativa dos componentes.

## Tipos de comunidades {#types-of-communities}

### Comunidade de envolvimento {#engagement-community}

Uma comunidade de envolvimento é um site da comunidade focado em envolver os clientes a informar, solicitar feedback e permitir que eles interajam como membros da comunidade.

Os recursos de uma comunidade de envolvimento podem incluir:

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
* Pontuação e emblemas
* relatórios do Analytics

Para experimentar a facilidade de criar rapidamente uma nova comunidade de envolvimento, visite [Introdução ao AEM Communities](/help/communities/getting-started.md).

### Comunidade de ativação {#enablement-community}

Uma comunidade de capacitação é um site da comunidade que inclui recursos para aprendizado online.

Os recursos de uma comunidade de ativação podem incluir:

* Todos os recursos de uma comunidade [de](#engagement-community)envolvimento.
* capacidade de atribuir conteúdo e aprendizado. recursos para membros e grupos membros.
* Suporta conteúdo SCORM, como testes e testes.
* Rastreamento da conclusão das atribuições.
* Acesso a relatórios e análises.
* A capacidade de conversar sobre um recurso de aprendizado através de fóruns, mensagens, comentários e classificações.

Uma comunidade de ativação pode ser criada quando o complemento [Ativação é configurado](/help/communities/enablement.md), o que requer licenciamento adicional para uso em um ambiente de produção. Um site de comunidade de ativação incluirá a função [de](#community-functions)atribuições.

Para experimentar a facilidade de criar uma nova comunidade de ativação, visite [Introdução ao AEM Communities for Enablement](/help/communities/getting-started-enablement.md).

## Computador de demonstração AEM {#aem-demo-machine}

A máquina [de demonstração do](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) AEM gerencia e executa demonstrações para [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)do AEM, [Ativos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Comunidades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Aplicativos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)e Formulários, que geralmente exigem mais configuração do que simplesmente iniciar uma instância do QuickStart. A máquina de demonstração do AEM irá configurar [infraestrutura](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) adicional, como os servidores MongoDB, Solr, MySQL, FFmpeg e email.

A máquina de demonstração do AEM inclui:

* Uma interface [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)gráfica do usuário.
* Scripts do Apache ANT com [propriedades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) e [públicos alvos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)configuráveis.

* Pacotes a instalar.

A máquina de demonstração do AEM foi testada com êxito com CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 e AEM 6.4 no Windows, Mac OS e Linux.

A máquina de demonstração AEM exige uma licença AEM válida.

>[!NOTE]
>
>Visualização uma introdução [de](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) vídeo à máquina de demonstração do AEM (13:26).


## Documentação do AEM Communities {#aem-communities-documentation}

* Visite [Implantação de comunidades](deploy-communities.md) para saber mais sobre implantações recomendadas.
* Visite [Administrando sites](administer-landing.md) de comunidades para saber mais sobre como criar um site da comunidade, adicionar grupos da comunidade, configurar modelos de site da comunidade, moderar conteúdo da comunidade, gerenciar membros, marcar, notificações, pontuação e emblemas.
* Visite Comunidades [em desenvolvimento](communities.md) para saber mais sobre a estrutura de componentes sociais (SCF) e como personalizar componentes e recursos das Comunidades.
* Visite Componentes [de comunidades de](author-communities.md) criação para saber como criar e configurar componentes de Comunidades.

