---
title: Opcional - Como criar aplicativos de página única (SPA) com o Adobe Experience Manager
description: Nesta continuação opcional da Jornada de desenvolvedores headless Adobe Experience Manager (AEM), você aprende como o AEM SPA AEM SPA pode combinar a entrega headless com os recursos tradicionais de CMS de pilha completa e como criar editáveis usando a estrutura do editor.
exl-id: 91eadda2-b881-4e4a-867f-8c5c54e8f8b4
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 60%

---

# Como criar aplicativos de página única (SPAs) com o AEM {#create-spa}

Nesta continuação facultativa do [Jornada do desenvolvedor AEM Headless,](overview.md) você aprende como o Adobe Experience Manager (AEM) pode combinar a entrega headless com recursos tradicionais de CMS de pilha completa e como criar SPA AEM SPA SPA editáveis usando a estrutura do editor, além de integrar externo, habilitando recursos de edição conforme necessário.

## A história até agora {#story-so-far}

A esta altura, você deve ter completado toda a [Jornada de desenvolvedor headless do AEM](overview.md) e compreendido as noções básicas de entrega headless no AEM, e deve entender sobre:

* A diferença entre a entrega de conteúdo headless e headful.
* Recursos headless do AEM.
* Como organizar um projeto do AEM Headless.
* Como criar conteúdo headless no AEM.
* Como recuperar e atualizar conteúdo headless no AEM.
* Como ativar um projeto do AEM Headless.

Então vocês ou ativaram seu primeiro projeto AEM Headless, ou têm o conhecimento para fazê-lo. Parabéns!

Sendo assim, por que você está lendo essa seção adicional e opcional da jornada? Provavelmente, você se lembra disso no [Introdução](getting-started.md#integration-levels)No entanto, houve uma breve discussão sobre como o AEM não apenas suporta a entrega headless e os modelos tradicionais de pilha completa, como também pode suportar modelos híbridos que combinam as vantagens de ambos. Embora não sejam o modelo tradicional para headless, esses modelos híbridos podem oferecer uma flexibilidade sem precedentes a certos projetos.

Este artigo desenvolve seu conhecimento sobre AEM Headless, explorando em detalhes como você pode criar seus próprios aplicativos de página única (SPA) que são editáveis no AEM. Dessa forma, você pode criar conteúdo e enviá-lo de forma headless para um SPA, mas esse SPA permanece editável no AEM.

## Objetivo {#objective}

Este documento ajuda você a entender como aplicativos de página única são desenvolvidos usando a estrutura do editor de SPA do AEM. Depois de ler este documento, você deverá:

* Entender a função básica do editor de SPA.
* Saber quais são os requisitos para criar uma SPA totalmente editável para o AEM.
* Entender como SPAs externos podem ser integrados ao AEM.
* Entenda como a renderização do lado do servidor deve ou não ser implementada.

## Requisitos e pré-requisitos {#requirements-prerequisites}

Há vários requisitos antes de começar a trabalhar com o AEM no SPA.

### Conhecimento {#knowledge}

* Experiência de desenvolvimento na criação de SPAs com estruturas React ou Angular
* Habilidades básicas do AEM para criar fragmentos de conteúdo e usar o editor
* Certifique-se de revisar o documento [Headful e Headless no AEM](/help/sites-developing/headful-headless.md) para compreender os vários níveis possíveis de integração do SPA.

### Ferramentas {#tools}

* Acesso à sandbox para testar a implantação do seu projeto
* Instância de desenvolvimento local para modelagem e teste de dados
* SPAs externos existentes (opcional, dependendo do modelo de integração escolhido)
* Arquétipo de projeto do AEM

## O que é um SPA? {#what-is-a-spa}

Um aplicativo de página única (SPA) difere de uma página convencional na medida em que é renderizado no lado do cliente e é principalmente orientado por JavaScript, dependendo de chamadas Ajax para carregar dados e atualizar dinamicamente a página. A maior parte ou todo o conteúdo é recuperado uma vez em um único carregamento de página, com os recursos adicionais sendo carregados de forma assíncrona conforme necessário, com base na interação do usuário com a página.

Isso reduz a necessidade de atualizações de página e apresenta uma experiência ao usuário que é contínua, rápida e se parece mais com uma experiência de aplicativo nativo.

O editor de SPA do AEM permite que desenvolvedores de front-end criem SPAs que possam ser integrados a um site do AEM, possibilitando que os autores de conteúdo editem o conteúdo do SPA tão facilmente quanto qualquer outro conteúdo do AEM.

## Por que um SPA? {#why-spa}

Por ser mais rápido, fluido e mais parecido com um aplicativo nativo, um SPA se torna uma experiência atraente não apenas para o visitante da página da Web, mas também para profissionais de marketing e desenvolvedores, devido à natureza de como o SPA funciona.

Para obter uma descrição completa dos SPAs e por que usá-los, consulte a seção de [recursos adicionais](#additional-resources) que contém links para uma documentação mais detalhada.

## Como o AEM lida com SPAs

O desenvolvimento de aplicativos de página única no AEM parte do princípio de que o desenvolvedor de front-end segue as práticas recomendadas padronizadas ao criar um SPA. Como desenvolvedor de front-end, se seguir essas práticas recomendadas gerais e alguns princípios específicos do AEM, seu SPA estará funcional com o AEM e seus recursos de criação de conteúdo.

* **Portabilidade** - Assim como com qualquer componente, os componentes do SPA devem ser desenvolvidos para serem tão portáteis quanto possível. O SPA deve ser desenvolvido com componentes portáteis e reutilizáveis.
* **AEM direciona a estrutura do site** - O desenvolvedor de front-end cria componentes e tem sua estrutura interna, mas depende do AEM para definir a estrutura de conteúdo do site.
* **Renderização dinâmica** - Todas as renderizações devem ser dinâmicas.
* **Roteamento dinâmico** - O SPA é responsável pelo roteamento e o AEM o escuta e realiza buscas com base nele. Qualquer roteamento também deve ser dinâmico.

Para obter uma descrição completa de como o AEM lida com SPAs, consulte a seção de [recursos adicionais](#additional-resources) que fornece links para uma documentação mais detalhada.

## O editor de SPA do AEM {#aem-spa-editor}

Sites criados usando estruturas de SPA comuns, como React e Angular, carregam seu conteúdo dinamicamente via JSON e não fornecem a estrutura de HTML necessária para que o editor de página do AEM possa estabelecer controles de edição.

Para habilitar a edição de SPAs no AEM, é necessário um mapeamento entre a saída JSON do SPA e o modelo de conteúdo no repositório do AEM para salvar as alterações no conteúdo.

A compatibilidade com SPA no AEM apresenta uma camada de JS sutil que interage com o código JS do SPA quando ele é carregado no editor de página através do qual os eventos podem ser enviados, sendo assim, o local dos controles de edição pode ser ativado para permitir a edição de acordo com o contexto. Esse recurso se baseia no conceito de endpoint da API de serviços de conteúdo, pois o conteúdo do SPA deve ser carregado por meio dos serviços de conteúdo.

Para obter uma descrição completa do editor de SPA do AEM, consulte a seção de [recursos adicionais](#additional-resources) que fornece links para uma documentação mais detalhada.

## Acomodando SPAs existentes {#existing-spas}

Se você tiver um SPA existente, o AEM suporta a incorporação dele no AEM para que seja visível aos autores de conteúdo no Editor de AEM. Isso pode ser útil para visualizar o conteúdo que eles estão criando por meio dos Fragmentos de conteúdo no contexto do aplicativo final em que será consumido.

Além disso, com apenas pequenas alterações, é possível habilitar determinados recursos de edição para o SPA externo no Editor de AEM.

O componente RemotePage permite a renderização de um SPA externo no AEM.

Para obter uma descrição completa de como tornar um SPA externo editável no AEM, consulte a seção de [recursos adicionais](#additional-resources) que fornece links para uma documentação mais detalhada.

## O que vem a seguir {#what-is-next}

Para começar a desenvolver seus próprios SPAs para o AEM, revise os seguintes documentos:

* [Tutorial WKND do SPA](/help/sites-developing/spa-wknd.md)
* [Introdução à utilização do React](/help/sites-developing/spa-getting-started-react.md)
* [Introdução à utilização do Angular](/help/sites-developing/spa-getting-started-angular.md)

Se você precisar adaptar um SPA existente para usá-lo no AEM, revise os seguintes documentos:

* [O componente RemotePage](/help/sites-developing/spa-remote-page.md)
* [Edição de um SPA externo no AEM](/help/sites-developing/spa-edit-external.md)

Veja abaixo os [recursos adicionais](#additional-resources) que abordam tópicos relacionados a SPA no AEM com mais detalhes.

## Recursos adicionais {#additional-resources}

Veja a seguir alguns recursos adicionais que explicam melhor alguns conceitos mencionados neste documento.

* [Headful e headless no AEM](/help/sites-developing/headful-headless.md): uma descrição dos diferentes modelos de entrega disponíveis no AEM
* [Introdução e passo a passo do SPA.](/help/sites-developing/spa-walkthrough.md): uma boa introdução a SPAs no AEM
* [Desenvolvimento de SPAs para o AEM](/help/sites-developing/spa-architecture.md): diretrizes sobre como desenvolver SPAs para o AEM
* [Visão geral do editor de SPA](/help/sites-developing/spa-overview.md): detalhes de como o editor de SPA funciona
* [Renderização do lado do servidor](/help/sites-developing/spa-ssr.md) - Como configurar o SSR para SPA AEM
* [Documentos de referência do SPA](/help/sites-developing/spa-reference-materials.md) AEM - Referências de API JavaScript e links para os projetos de SPA GitHub de código aberto
* [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md): como criar fragmentos de conteúdo
* [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR): modelo do Maven que cria um projeto simples do Adobe Experience Manager (AEM) com base em práticas recomendadas para ser usado como o ponto de partida do seu site
