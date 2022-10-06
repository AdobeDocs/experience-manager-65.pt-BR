---
title: Visão geral da AEM Communities
seo-title: AEM Communities Overview
description: Uma visão geral dos recursos e da configuração do AEM Communities
seo-description: An overview of AEM Communities features and setup
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 4%

---

# Visão geral da AEM Communities {#aem-communities-overview}

O Adobe Experience Manager (AEM) Communities oferece a capacidade de criar rapidamente um site local da comunidade com o melhor desempenho, gerenciamento de site, e estimula a conversão de visitantes do site em membros de alto valor da Comunidade.

<!--
Contact your account representative for information regarding licensing of AEM Communities as well as additional licensing for enablement features and Adobe Analytics.
-->

## Recursos das comunidades {#communities-features}

O AEM Communities permite o desenvolvimento de uma relação com visitantes do site, que:

* **Informações** por meio de blogs, perguntas e respostas e calendários de eventos,
* Ao **obter insights** por meio de fóruns, comentários e outros conteúdos da comunidade, geralmente chamados de conteúdo gerado por usuários (UGC).
* Permite **moderação** por membros confiáveis no ambiente de publicação,
* **Logon social** com Twitter e Facebook,
* **Tradução em linha** de conteúdo comunitário,
* **Criação de grupos da comunidade** do site da comunidade publicado,
* **Pontuação** para a atribuição de cartões,
* **Compartilhamento de arquivos**,
* **Notificações** e **fluxos de atividades**,
* Permite **marcação** (@mention) outros membros registrados em Conteúdo gerado pelo usuário, para chamar a atenção deles.
* Suporta **navegação pelo teclado** sobre componentes de ativação (por exemplo, Catálogo e reprodução do curso, atribuições, biblioteca de arquivos) .

Os recursos das comunidades podem ser demonstrados usando o [Máquina de demonstração AEM](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponível publicamente em GitHub.com ou com a nova implementação de referência We.Retail.

## Sites da comunidade {#community-sites}

Um site da comunidade é um site AEM criado por meio de um assistente simples que resulta em um site com muitos recursos comuns pré-conectados ao site.

O [assistente de criação de sites](/help/communities/sites-console.md):

* Reúne recursos do site, com base no [modelo de site da comunidade](/help/communities/sites.md) que é:

   * criado a partir de [funções da comunidade](#community-functions)
   * opcional [grupos da comunidade](#communitygroups) recurso

* Usa configurações para configurar:

   * moderação
   * fazer logon
   * tradução

* Fornece recursos essenciais:

   * Design responsivo: uses [Temas do Bootstrap twitter](https://getbootstrap.com)

   * Logon : registro automático, [logon social](/help/communities/social-login.md), perfis de usuário

      * Notificações: os membros veem eventos de relevância para eles e o conteúdo gerado pelo usuário, onde estão [@mention](/help/communities/overview.md#mentionssupport).

      * Mensagens: membros podem enviar ou receber mensagens no site da comunidade.
      * Pesquisar: capacidade de pesquisar no site da comunidade.
      * Comutação de idioma: capacidade de selecionar um idioma para um [site multilíngue](/help/sites-administering/translation.md).

      * Administração: acesso para membros autorizados para moderar e gerenciar usuários no site da comunidade.

* Elimina muitas etapas de criação no nível da página:

   * Identidade visual: upload opcional de uma imagem de banner para exibição em todas as páginas do site da comunidade
   * Menu de navegação: os links de navegação são fornecidos para os recursos incluídos no modelo de site da comunidade.

Para experimentar a facilidade de criar rapidamente um novo site da comunidade, visite [Introdução ao AEM Communities](/help/communities/getting-started.md).

## Persistência do conteúdo da comunidade {#community-content-persistence}

Para melhorar o desempenho e a sincronização do conteúdo da comunidade, o AEM Communities exige uma loja comum especificamente para o conteúdo gerado pelo usuário (UGC) compartilhado entre todas as instâncias de AEM (autor e publicação).

O conteúdo da comunidade é facilmente acessado por meio do SRP (Storage Resource Provider, provedor de recursos de armazenamento), que fornece uma camada para separar o acesso da topologia subjacente e oferece suporte a uma loja comum para UGC.

Para saber mais sobre a persistência do conteúdo da comunidade e as implantações recomendadas, consulte:

* [Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md), que discute as opções de armazenamento SRP disponíveis para UGC.
* [Topologias recomendadas](/help/communities/topologies.md), que discute topologias com base no caso de uso e na escolha da SRP.
* [Atualização para AEM Comunidades 6.5](/help/communities/upgrade.md), que fornece informações úteis sobre o UGC ao migrar para o AEM 6.5.

## Consoles de comunidades {#communities-consoles}

No ambiente de criação, o console de navegação global fornece acesso ao [Console de comunidades](/help/communities/consoles.md), que contém:

* [Console de sites](/help/communities/sites-console.md)

   * Criação do site
   * Edição do site
   * Gerenciamento do site
   * [Grupos da comunidade](/help/communities/groups.md) console

* [Moderação](/help/communities/moderation.md) console

   * Interface do usuário comum de moderação em massa para ambientes de criação e publicação.
   * Novos critérios de filtragem.

* [Membros e grupos](/help/communities/members.md) consoles de gerenciamento

   * Fornece a capacidade de criar e gerenciar usuários do lado da publicação (membros) a partir do ambiente do autor.
   * Fornece a capacidade de proibir membros.
   * Fornece a capacidade de criar e gerenciar grupos de usuários do lado da publicação (grupos de membros) a partir do ambiente do autor.

* [Relatórios](/help/communities/reports.md) console

   * Fornece a capacidade de gerar relatórios sobre atribuições, postagens e visualizações.

* [Recursos](/help/communities/resources.md) console

   * Fornece a capacidade de criar recursos de capacitação e caminhos de aprendizado.
   * Fornece acesso a relatórios sobre recursos de ativação e caminhos de aprendizado.

O console de ferramentas globais fornece acesso às seguintes ferramentas do Communities:

* [Modelos de site](/help/communities/tools.md#sitetemplatesconsole) console

   * Crie e gerencie modelos de site da comunidade.

* [Modelos de grupo](/help/communities/tools.md#grouptemplatesconsole) console

   * Crie e gerencie modelos de grupo da comunidade.

* [Funções da comunidade](/help/communities/tools.md#communityfunctionsconsole) console

   * Crie e gerencie funções da comunidade.

* [Configuração de armazenamento](/help/communities/tools.md#storageconfiguratonconsole) console

   * Selecione e configure o [loja comum](/help/communities/working-with-srp.md) para o site.

* [Guia do componente](/help/communities/components-guide.md)

   * Um site de exemplo, [Componentes da comunidade](https://localhost:4502/editor.html/content/community-components/en.html), que fornece uma amostra de todos os componentes das Comunidades com sua configuração padrão e a capacidade de experimentar com eles.

## Modelos do site da comunidade {#community-site-templates}

A criação de site da comunidade é baseada na seleção de um modelo de site da comunidade para configurar rapidamente um site da comunidade que não seja independente de nenhum site de amostra.

Um modelo de site da comunidade, composto por funções da comunidade e modelos de grupo da comunidade, fornece a estrutura para um site da comunidade, incluindo logon, perfis de usuário, mensagens, menu do site, pesquisa, tema e recursos de marca.

Consulte a [Console de modelos de site](/help/communities/sites.md).

## Funções da comunidade {#community-functions}

Os recursos esperados de uma experiência da comunidade são bem conhecidos. Com o AEM Communities, esses recursos estão disponíveis como blocos de construção, conhecidos como funções da comunidade.

As funções da comunidade são normais AEM páginas incluem componentes conectados em um recurso que é facilmente incorporado a um modelo de site da comunidade.

Consulte a [Console Funções da comunidade](/help/communities/functions.md).

## Grupos da comunidade e modelos de grupo {#community-groups-and-group-templates}

O recurso de grupos da comunidade é a capacidade de uma subcomunidade ser criada dinamicamente em um site da comunidade por usuários autorizados e membros da comunidade dos ambientes de criação e publicação.

No ambiente de criação, os grupos da comunidade (subcomunidades) podem ser criados em um site da comunidade existente ou aninhados em um grupo existente, quando a estrutura do modelo contém a variável [Função Grupos](/help/communities/functions.md#groups-function).

A criação de um grupo da comunidade requer a seleção de um modelo de grupo da comunidade que fornece o design da(s) página(s) do grupo da comunidade. Quando uma função Grupos é adicionada a uma estrutura de modelo, ela é configurada para especificar um modelo de grupo ou para fornecer uma escolha de modelos no momento em que um novo grupo de comunidade é criado.

Consulte também:

* [Console de grupos de sites](/help/communities/groups.md) para criar subcomunidades no ambiente de criação.
* [Console Modelos de grupo](/help/communities/tools-groups.md) para criar a estrutura do site para grupos.
* [Introdução ao AEM Communities](/help/communities/getting-started.md) para obter um tutorial que permite criar rapidamente um site da comunidade, incluindo grupos aninhados.

## Componentes da comunidade {#community-components}

O [componentes da comunidade](/help/communities/author-communities.md) do qual um site da comunidade é criado pode ser usado para adicionar recursos do Communities a qualquer Site AEM.

O [guia de componentes da comunidade](/help/communities/components-guide.md) está disponível para exploração interativa dos componentes.

## Tipos de comunidades {#types-of-communities}

### Comunidade de envolvimento {#engagement-community}

Uma comunidade de engajamento é um site da comunidade com foco em envolver os clientes para informar, solicitar feedback e permitir que eles interajam como membros da comunidade.

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
* Relatórios do Analytics

Para experimentar a facilidade de criar rapidamente uma nova comunidade de envolvimento, visite [Introdução ao AEM Communities](/help/communities/getting-started.md).

### Comunidade de ativação {#enablement-community}

Uma comunidade de capacitação é um site da comunidade que inclui recursos para aprendizado online.

Os recursos de uma comunidade de ativação podem incluir:

* Todos os recursos de um [comunidade de engajamento](#engagement-community).
* capacidade de atribuir conteúdo e aprendizado. recursos para membros e grupos de membros.
* Suporta conteúdo SCORM, como testes e testes.
* Rastreamento da conclusão das atribuições.
* Acesso a relatórios e análises.
* A capacidade de conversar sobre um recurso de aprendizado através de fóruns, mensagens, comentários e classificações.

Uma comunidade de ativação pode ser criada quando a variável [O complemento de ativação está configurado](/help/communities/enablement.md), que requer licenciamento adicional para uso em um ambiente de produção. Um site da comunidade de ativação incluirá a variável [função atribuições](#community-functions).

Para experimentar a facilidade de criar uma nova comunidade de ativação, visite [Introdução ao AEM Communities para ativação](/help/communities/getting-started-enablement.md).

## Máquina de demonstração AEM {#aem-demo-machine}

O [Máquina de demonstração AEM](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) gerencia e executa demonstrações para AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Ativos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Comunidades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Aplicativos](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) e [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), que geralmente requer mais configuração do que simplesmente iniciar uma instância do QuickStart. A Máquina de Demonstração de AEM irá configurar mais [infraestrutura](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) Como MongoDB, Solr, MySQL, FFmpeg e servidores de email.

A máquina de demonstração AEM inclui:

* A [interface gráfica do usuário](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Scripts Apache ANT com configurável [propriedades](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) e [targets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* Pacotes para instalar.

A máquina de demonstração AEM foi testada com êxito com o CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 e AEM 6.4 no Windows, MacOS e Linux.

A máquina de demonstração AEM requer uma licença de AEM válida.

>[!NOTE]
>
>Exibir um [introdução ao vídeo](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) à máquina de demonstração AEM (13:26).

## Documentação do AEM Communities {#aem-communities-documentation}

* Visita [Implantação de comunidades](deploy-communities.md) para saber mais sobre implantações recomendadas.
* Visita [Administrar sites das comunidades](administer-landing.md) para saber mais sobre como criar um site da comunidade, adicionar grupos da comunidade, configurar modelos de site da comunidade, moderar conteúdo da comunidade, gerenciar membros, marcação, notificações, pontuação e emblemas.
* Visita [Desenvolvimento de comunidades](communities.md) para saber mais sobre a estrutura de componentes sociais (SCF) e personalizar os componentes e recursos das Comunidades.
* Visita [Componentes de comunidades de criação](author-communities.md) para saber como criar e configurar componentes do Communities.
