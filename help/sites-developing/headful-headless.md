---
title: Headful e Headless no AEM
description: Os Projetos do AEM podem ser implementados em um modelo headful ou headless, mas a escolha não precisa ser binária. O AEM oferece a flexibilidade para explorar as vantagens de ambos os modelos em um projeto.
exl-id: c9597c78-be05-42ff-84fe-f7451119e83d
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 71%
---
# Headful e Headless no AEM {#headful-headless}

Os projetos do Adobe Experience Manager podem ser implementados em modelos headful ou headless, mas a escolha não precisa ser binária. O AEM oferece a flexibilidade para explorar as vantagens de ambos os modelos em um projeto. Este documento fornece uma visão geral dos diferentes modelos e descreve os níveis de integração de SPA.

## Visão geral {#overview}

O AEM oferece ferramentas eficientes para gerenciar a criação de conteúdo e sua entrega em uma única plataforma. É um modelo “headful” tradicional de gerenciamento de conteúdo, em que os autores e desenvolvedores de conteúdo trabalham na mesma plataforma para fornecer as experiências aos consumidores de conteúdo.

O AEM também pode ser usado para simplesmente gerenciar o conteúdo, permitindo que a apresentação e a entrega do conteúdo sejam gerenciadas por outra plataforma. Esse é o modelo “headless” de gerenciamento de conteúdo, em que os autores e desenvolvedores de conteúdo trabalham em plataformas diferentes para fornecer experiência aos consumidores de conteúdo.

Mas essa não precisa ser uma escolha binária. O AEM oferece flexibilidade sem precedentes, permitindo explorar as vantagens de ambos os modelos para o seu projeto.

![Modelos de implementação do AEM](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

Em um modelo com cabeçalho ou de pilha completa, o conteúdo é gerenciado no repositório do AEM e os componentes do AEM com base em Java, HTL e assim por diante são usados para renderizar o conteúdo para a experiência do usuário. Neste modelo, a criação de conteúdo, o estilo, a apresentação e a entrega acontecem no AEM.

Em um modelo headless, o conteúdo é gerenciado no repositório do AEM, mas entregue por APIs, como REST e GraphQL, a outro sistema para renderizar o conteúdo da experiência do usuário. Neste modelo, o conteúdo é criado no AEM, mas a estilização, a apresentação e a entrega acontecem em outra plataforma.

Aplicativos de página única (SPAs) geralmente são o destino para o conteúdo entregue de forma headless pelo AEM. No entanto, esses SPAs não precisam ser totalmente externos ao AEM. O AEM permite decidir em que grau seus SPAs são integrados ao AEM. Vamos ver um exemplo.

## Exemplo de loja virtual {#web-shop-example}

Digamos que você tem uma loja virtual para sua empresa como SPA. Nela, você tem todos os detalhes e imagens do produto. Em seguida, você apresenta o AEM para potencializar seus esforços de marketing, como sites promocionais, blogs e conteúdo da campanha. Como integrar os dois? O AEM permite várias opções:

* **Permite que os sistemas funcionem de forma independente.**
* **Forneça à loja na Web um conteúdo limitado do AEM via GraphQL.** O conteúdo pode ser criado por autores no AEM, mas somente visto por meio do SPA da loja na Web.
* **Incorporar o SPA da loja na Web no AEM.** O conteúdo pode ser criado por autores no AEM e exibido no AEM no contexto da loja na Web, mas não pode ser manipulado.
* **Incorpore o SPA da loja na AEM e habilite os pontos editáveis.** O conteúdo pode ser criado por autores no AEM e exibido no AEM no contexto da loja na Web, e os autores têm capacidade limitada para manipular o conteúdo da loja na Web SPA no AEM.
* **Incorpore o SPA da loja de webs no AEM e habilite zonas inteiras para edição.** O conteúdo pode ser criado por autores no AEM e exibido no AEM no contexto da loja na Web, e os autores têm capacidade limitada para manipular o conteúdo da loja na Web SPA no AEM.

A próxima seção explora esses níveis de integração com mais detalhes.

>[!NOTE]
>
>É claro que você também pode reimplementar o SPA da loja na Web como um SPA do AEM totalmente funcional [usando a estrutura do Editor SPA do AEM.](/help/sites-developing/spa-walkthrough.md) Se você já tiver o AEM e quiser criar uma loja na Web ou outro SPA, esse é o método recomendado, mas está fora do escopo desse documento.

## Níveis de integração de SPA {#integration-levels}

A integração de SPA se enquadra em quatro níveis no AEM.

* **Nível 0: sem integração**
  * O SPA e o AEM existem separadamente e não trocam informações.
  * O conteúdo é criado, gerenciado e entregue de maneira independente em dois sistemas separados.
* **Nível 1: integração de fragmento de conteúdo**
  * [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) são usados no AEM para criar e gerenciar conteúdo limitado para o SPA.
  * O SPA recupera esse conteúdo por meio da [API GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) do AEM.
  * Alguns conteúdos são gerenciados no AEM e outros em um sistema externo.
  * O conteúdo só pode ser visualizado no SPA.
* **Nível 2: incorporar o SPA no AEM**
  * [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) são usados no AEM para criar e gerenciar conteúdo para o SPA.
  * O SPA recupera esse conteúdo por meio da [API GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) do AEM.
  * Alguns conteúdos são gerenciados no AEM e outros em um sistema externo.
  * O conteúdo pode ser visualizado em contexto no AEM.
  * Conteúdo limitado pode ser editado no AEM.
* **Nível 3: incorporar e habilitar totalmente o SPA no AEM**
  * [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) são usados no AEM para criar e gerenciar conteúdo para o SPA.
  * O SPA recupera esse conteúdo por meio da [API GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) do AEM.
  * O conteúdo pode ser visualizado em contexto no AEM.
  * Grande parte do conteúdo pode ser editado no AEM.

O Nível 1 é um exemplo de uma implementação headless típica. No entanto, os autores de conteúdo só podem visualizar seu conteúdo no contexto no SPA. O AEM é apenas uma ferramenta de criação.

A vantagem e a flexibilidade do AEM tornam-se evidentes com os níveis 2 e 3, mantendo as vantagens do SPA. Os autores de conteúdo podem criar o conteúdo no AEM, mas também visualizá-lo no contexto no AEM. O SPA ganha a capacidade de ser criado no AEM, mas ainda pode ser entregue como um SPA.

## Implementar os níveis de integração {#implementing}

Há diferentes ferramentas no AEM disponíveis dependendo do nível de integração escolhido. Cada nível se baseia nas ferramentas usadas no anterior. A lista a seguir contém links para os recursos relevantes.

* **Nível 1:** Os Fragmentos de conteúdo e a [estrutura headless do AEM](/help/sites-developing/headless/introduction.md) podem ser usados para fornecer conteúdo do AEM ao SPA.
* **Nível 2:** além do nível um:
  * [O componente RemotePage](/help/sites-developing/spa-remote-page.md) pode ser usado para incorporar o SPA externo ao AEM, em que o conteúdo do AEM pode ser visualizado no contexto.
  * Alguns pontos no SPA também podem ser habilitados para [permitir a edição limitada no AEM.](/help/sites-developing/spa-edit-external.md)
* **Nível 3:** além do nível dois:
  * Zonas inteiras do SPA podem ser habilitadas para permitir uma edição abrangente no AEM.
