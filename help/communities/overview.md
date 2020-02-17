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
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# Visão geral do AEM Communities{#aem-communities-overview}

O Adobe Experience Manager (AEM) Communities oferece a capacidade de criar rapidamente um site local da comunidade com o melhor desempenho, gerenciamento de site, e estimula a conversão de visitantes do site em membros de alto valor da Comunidade.

Entre em contato com seu representante de conta para obter informações sobre o licenciamento do AEM Communities, além de licenças adicionais para recursos de ativação e Adobe Analytics.

## Recursos das comunidades {#communities-features}

O AEM Communities permite o desenvolvimento de uma relação com os visitantes do site, que:

* **informa** por meio de blogs, P&amp;R e calendários de eventos,
* enquanto **obtêm insights **através de fóruns, comentários e outros conteúdos da comunidade, geralmente conhecidos como conteúdo gerado pelo usuário (UGC).
* Permite** moderação **por membros confiáveis no ambiente de publicação,
* **login social **com Twitter e Facebook,
* **tradução** em linha do conteúdo comunitário,
* **criação de grupos comunitários **a partir do site da comunidade publicada,
* **pontuação **para atribuir cartões,
* **partilha** de ficheiros,
* **notificações **e fluxos **de atividade**,

* permite que a **marcação** (@menção) de outros membros registrados no Conteúdo gerado pelo usuário chame a atenção deles.
* Suporta a navegação **pelo** teclado em componentes de ativação (por exemplo, Catálogo e Reprodução do curso, Atribuições, Biblioteca de arquivos).

Os recursos das comunidades podem ser demonstrados usando a Máquina [de demonstração do](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) AEM disponível publicamente em GitHub.com ou com a nova implementação de referência We.Retail.

## Sites da comunidade {#community-sites}

Um site da comunidade é um site do AEM criado usando um assistente simples que resulta em um site com muitos recursos comuns pré-conectados ao site.

O assistente [de criação de](/help/communities/sites-console.md)site:

* reúne recursos do site, com base no modelo [de site da](/help/communities/sites.md) comunidade selecionado, que é:

   * criado a partir de funções [comunitárias](#community-functions)
   * recurso opcional [de grupos](#communitygroups) da comunidade

* usa configurações para configurar:

   * moderação
   * login
   * tradução

* fornece recursos essenciais:

   * design responsivo:
usa temas do [Twitter Bootstrap](https://getbootstrap.com)

   * login :
autorregistro, login [](/help/communities/social-login.md)social, perfis de usuário

   * notificações:
os membros veem eventos de relevância para eles e conteúdo gerado pelo usuário onde eles são [@mencionados](/help/communities/overview.md#mentionssupport).

   * mensagens:
os membros podem enviar ou receber mensagens no site da comunidade
   * pesquisa:
capacidade de pesquisar no site da comunidade
   * mudança de idioma:
capacidade de selecionar um idioma para um site [multilíngue](/help/sites-administering/translation.md)

   * administração:
acesso de membros autorizados para moderar e gerenciar usuários no site da comunidade

* elimina várias etapas de criação em nível de página:

   * marca:
carregamento opcional de uma imagem de banner para exibição em todas as páginas do site da comunidade
   * menu de navegação:
links de navegação são fornecidos para os recursos incluídos no modelo de site da comunidade

Para experimentar a facilidade de criar rapidamente um novo site da comunidade, visite [Introdução ao AEM Communities](/help/communities/getting-started.md).

## Persistência do conteúdo da comunidade {#community-content-persistence}

Para melhorar o desempenho e a sincronização do conteúdo da comunidade, o AEM Communities exige uma loja comum especificamente para o conteúdo gerado pelo usuário (UGC) compartilhado entre todas as instâncias do AEM (autor e publicação).

O conteúdo da comunidade é facilmente acessado pelo SRP (Storage Resource Provider, provedor de recursos de armazenamento), que fornece uma camada para separar o acesso da topologia subjacente e oferece suporte a uma loja comum para UGC.

Para saber mais sobre a persistência do conteúdo da comunidade e as implantações recomendadas, consulte:

* [Community Content Storage](/help/communities/working-with-srp.md), que discute as opções de armazenamento SRP disponíveis para UGC.
* [Topologias](/help/communities/topologies.md)recomendadas, que discute topologias com base no caso de uso e na escolha do SRP.
* [Atualização para o AEM 6.5 Communities](/help/communities/upgrade.md), que fornece informações úteis sobre o UGC ao mudar para o AEM 6.5.

## Consoles de comunidades {#communities-consoles}

No ambiente do autor, o console de navegação global fornece acesso ao console [](/help/communities/consoles.md)Comunidades, que contém:

* [Console de sites](/help/communities/sites-console.md)

   * criação de site
   * edição do site
   * gerenciamento do site
   * [Console de grupos](/help/communities/groups.md) da comunidade

* [Console de moderação](/help/communities/moderation.md)

   * interface comum de moderação em massa para ambientes de criação e publicação
   * novos critérios de filtragem

* [Consoles de gerenciamento de membros e grupos](/help/communities/members.md)

   * fornece a capacidade de criar e gerenciar usuários do lado da publicação (membros) a partir do ambiente do autor
   * permite proibir membros
   * fornece a capacidade de criar e gerenciar grupos de usuários do lado da publicação (grupos de membros) a partir do ambiente do autor

* [Console de relatórios](/help/communities/reports.md)

   * fornece a capacidade de gerar relatórios em atribuições, postagens e exibições

* [Console de recursos](/help/communities/resources.md)

   * fornece a capacidade de criar recursos de ativação e caminhos de aprendizagem
   * fornece acesso a relatórios sobre recursos de ativação e caminhos de aprendizagem

O console de ferramentas globais fornece acesso às seguintes ferramentas de Comunidades:

* [console Modelos](/help/communities/tools.md#sitetemplatesconsole) de site

   * criar e gerenciar modelos de site da comunidade

* [Console Modelos](/help/communities/tools.md#grouptemplatesconsole) de grupo

   * criar e gerenciar modelos de grupos da comunidade

* [Console de funções](/help/communities/tools.md#communityfunctionsconsole) da comunidade

   * criar e gerenciar funções da comunidade

* [Console de configuração](/help/communities/tools.md#storageconfiguratonconsole) de armazenamento

   * selecionar e configurar a loja [](/help/communities/working-with-srp.md) comum do site

* [Guia do componente](/help/communities/components-guide.md)

   * um site de amostra, [Community Components](https://localhost:4502/editor.html/content/community-components/en.html), que fornece uma amostra de todos os componentes das Comunidades com sua configuração padrão e a capacidade de experimentar com eles

## Modelos do site da comunidade {#community-site-templates}

A criação de site da comunidade é baseada na seleção de um modelo de site da comunidade para configurar rapidamente um site da comunidade que é independente de qualquer site de amostra.

Um modelo de site da comunidade, composto de funções da comunidade e modelos de grupo da comunidade, fornece a estrutura para um site da comunidade, incluindo logon, perfis de usuário, mensagens, menu do site, pesquisa, temas e recursos de marca.

Consulte o console [Modelos de](/help/communities/sites.md)site.

## Funções da comunidade {#community-functions}

Os recursos esperados de uma experiência da comunidade são bem conhecidos. Com o AEM Communities, esses recursos estão disponíveis como blocos de construção, conhecidos como funções da comunidade.

As funções da comunidade são páginas normais do AEM que incluem componentes conectados em conjunto em um recurso que é facilmente incorporado em um modelo de site da comunidade.

Consulte o console [Funções da](/help/communities/functions.md)comunidade.

## Grupos da comunidade e modelos de grupo {#community-groups-and-group-templates}

O recurso de grupos da comunidade é a capacidade de uma subcomunidade ser criada dinamicamente dentro de um site da comunidade por usuários autorizados e membros da comunidade dos ambientes de autor e publicação.

No ambiente do autor, grupos da comunidade (subcomunidades) podem ser criados dentro de um site da comunidade existente ou aninhados dentro de um grupo existente, quando a estrutura do modelo contém a função [](/help/communities/functions.md#groups-function)Grupos.

A criação de um grupo da comunidade requer a seleção de um modelo de grupo da comunidade que forneça o design das páginas de grupo da comunidade. Quando uma função Grupos é adicionada a uma estrutura de modelo, ela é configurada para especificar um modelo de grupo ou para fornecer uma opção de modelos no momento em que um novo grupo da comunidade é criado.

Consulte também:

* [Console](/help/communities/groups.md) de grupos de sites para criar subcomunidades no ambiente do autor
* [Console](/help/communities/tools-groups.md) de modelos de grupo para criar a estrutura do site para grupos
* [Introdução ao AEM Communities](/help/communities/getting-started.md) para tutorial para criar rapidamente um site da comunidade, incluindo grupos aninhados

## Componentes da comunidade {#community-components}

Os componentes [da](/help/communities/author-communities.md) comunidade a partir dos quais um site da comunidade é criado podem ser usados para adicionar recursos das Comunidades a qualquer site do AEM.

O guia [de componentes da](/help/communities/components-guide.md) comunidade está disponível para exploração interativa dos componentes.

## Tipos de comunidades {#types-of-communities}

### Comunidade de envolvimento {#engagement-community}

Uma comunidade de envolvimento é um site da comunidade focado em envolver os clientes a informar, solicitar feedback e permitir que eles interajam como membros da comunidade.

Os recursos de uma comunidade de envolvimento podem incluir:

* login
* mensagem
* fóruns
* comentários
* análises
* classificações
* votação
* blogs
* grupos
* calendários
* tradução
* moderação
* notificações
* pontuação e símbolos
* relatórios de análise

Para experimentar a facilidade de criar rapidamente uma nova comunidade de envolvimento, visite [Introdução ao AEM Communities](/help/communities/getting-started.md).

### Comunidade de ativação {#enablement-community}

Uma comunidade de capacitação é um site da comunidade que inclui recursos para aprendizagem online.

Os recursos de uma comunidade de ativação podem incluir:

* todos os recursos de uma comunidade de [envolvimento](#engagement-community)
* capacidade de atribuir conteúdo e recursos de aprendizado a membros e grupos de membros
* suporta conteúdo SCORM, como testes e testes
* acompanhamento da conclusão das atribuições
* acesso a relatórios e análises
* a capacidade de conversar sobre um recurso de aprendizado através de fóruns, mensagens, comentários e classificações

Uma comunidade de ativação pode ser criada quando o complemento [Ativação é configurado](/help/communities/enablement.md), o que requer licenciamento adicional para uso em um ambiente de produção. Um site de comunidade de ativação incluirá a função [de](#community-functions)atribuições.

Para experimentar a facilidade de criar uma nova comunidade de ativação, visite [Introdução ao AEM Communities para Ativação](/help/communities/getting-started-enablement.md).

## Computador de demonstração AEM {#aem-demo-machine}

A máquina [de demonstração do](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) AEM gerencia e executa demonstrações para [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)do AEM, [Ativos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Comunidades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Aplicativos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)e Formulários, que geralmente exigem mais configuração do que simplesmente iniciar uma instância do QuickStart. A máquina de demonstração do AEM irá configurar [infraestrutura](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) adicional, como os servidores MongoDB, Solr, MySQL, FFmpeg e email.

A máquina de demonstração do AEM inclui:

* uma interface [gráfica do usuário](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)
* Scripts do Apache ANT com [propriedades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) e [destinos configuráveis](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)

* pacotes a instalar

A máquina de demonstração do AEM foi testada com êxito com CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 e AEM 6.4 no Windows, Mac OS e Linux.

A máquina de demonstração AEM exige uma licença AEM válida.

>[!NOTE]
>
>Veja uma introdução [em](https://www.youtube.com/watch?v=zEE_zkR9fVQ&feature=youtu.be) vídeo ao AEM Demo Machine (13:26).

## Documentação do AEM Communities {#aem-communities-documentation}

* Visite [Implantação de comunidades](/help/communities/deploy-communities.md) para saber mais sobre implantações recomendadas.
* Visite [Administrando sites](/help/communities/administer-landing.md) de comunidades para saber mais sobre como criar um site da comunidade, adicionar grupos da comunidade, configurar modelos de site da comunidade, moderar conteúdo da comunidade, gerenciar membros, marcar, notificações, pontuação e emblemas.
* Visite Comunidades [em desenvolvimento](/help/communities/communities.md) para saber mais sobre a estrutura de componentes sociais (SCF) e como personalizar componentes e recursos das Comunidades.
* Visite Componentes [de comunidades de](/help/communities/author-communities.md) criação para saber como criar e configurar componentes de Comunidades.

