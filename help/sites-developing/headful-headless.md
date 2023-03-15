---
title: Headful e Headless no AEM
description: AEM projetos podem ser implementados em um modelo headful e sem interface, mas a escolha não é binária. O AEM oferece a flexibilidade para explorar as vantagens de ambos os modelos em um projeto.
exl-id: c9597c78-be05-42ff-84fe-f7451119e83d
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 94%

---

# Headful e Headless no AEM {#headful-headless}

Os projetos do Adobe Experience Manager podem ser implementados em modelos headful e sem periféricos, mas a escolha não é binária. O AEM oferece a flexibilidade para explorar as vantagens de ambos os modelos em um projeto. Este documento fornece uma visão geral dos diferentes modelos e descreve os níveis de integração SPA.

## Visão geral {#overview}

O AEM oferece ferramentas eficientes para gerenciar a criação de conteúdo e sua entrega em uma única plataforma. É um modelo “headful” tradicional de gestão de conteúdo, em que os autores e desenvolvedores de conteúdo trabalham na mesma plataforma para fornecer as experiências aos consumidores de conteúdo.

O AEM também pode ser usado para simplesmente gerenciar o conteúdo, permitindo que a apresentação e a entrega do conteúdo sejam gerenciadas por outra plataforma. Esse é o modelo “headless” de gerenciamento de conteúdo, em que os autores e desenvolvedores de conteúdo trabalham em plataformas diferentes para fornecer experiência aos consumidores de conteúdo.

Mas isso não precisa ser uma escolha binária. O AEM oferece flexibilidade sem precedentes, permitindo explorar as vantagens de ambos os modelos para o seu projeto.

![Modelos de implementação do AEM](headless/assets/aem-implementation-models.png)

Em um modelo com pilha completa ou headful, o conteúdo é gerenciado no repositório do AEM, e os componentes do AEM com base em Java, HTL etc. são usados para renderizar o conteúdo da experiência do usuário. Neste modelo, a criação de conteúdo, o estilo, a apresentação e a entrega acontecem no AEM.

Em um modelo headless, o conteúdo é gerenciado no repositório do AEM, mas entregue por APIs, como REST e GraphQL, a outro sistema para renderizar o conteúdo da experiência do usuário. Neste modelo, o conteúdo é criado no AEM, mas a estilização, a apresentação e a entrega acontecem em outra plataforma.

Aplicativos de página única (SPAs) geralmente são o destino para o conteúdo entregue de forma headless pelo AEM. No entanto, estes SPAs não têm de ser totalmente externos ao AEM. O AEM permite decidir em que grau os SPAs estão integrados ao AEM. Vamos ver um exemplo.

## Exemplo de loja virtual {#web-shop-example}

Digamos que você tem uma loja virtual para sua empresa como SPA. Nela, você tem todos os detalhes e imagens do produto. Em seguida, você apresenta o AEM para potencializar seus esforços de marketing, como sites promocionais, blogs e conteúdo da campanha. Como integrar os dois? O AEM permite várias opções:

* **Permite que os sistemas funcionem de forma independente.**
* **Forneça conteúdo limitado à loja virtual do AEM via GraphQL.** O conteúdo pode ser criado por autores no AEM, mas pode ser visto apenas por meio do SPA da loja virtual.
* **Incorpore o SPA da loja virtual no AEM.** O conteúdo pode ser criado por autores no AEM e visualizado no AEM no contexto da loja virtual, mas não pode ser manipulado.
* **Incorpore o SPA da loja virtual no AEM e ative pontos editáveis.** O conteúdo pode ser criado por autores no AEM e visualizado no AEM no contexto da loja virtual, e os autores têm capacidade limitada de manipular o conteúdo do SPA da loja virtual no AEM.
* **Incorpore o SPA da loja virtual no AEM e ative zonas inteiras para edição.** O conteúdo pode ser criado por autores no AEM e visualizado no AEM no contexto da loja virtual, e os autores têm capacidade limitada de manipular o conteúdo do SPA da loja virtual no AEM.

A próxima seção explora esses níveis de integração com mais detalhes.

>[!NOTE]
>
>É claro que você também poderia reimplementar o SPA da loja virtual como um SPA totalmente funcional do AEM [usando a estrutura do Editor de SPA do AEM.](/help/sites-developing/spa-walkthrough.md) Se você já tem o AEM e quer criar uma nova loja virtual ou outro SPA, esse é o método recomendado, mas ele está fora do escopo deste documento.

## Níveis de integração de SPA {#integration-levels}

A integração de SPA se enquadra em quatro níveis no AEM.

* **Nível 0: sem integração**
   * O SPA e o AEM existem separadamente e não trocam informações.
   * O conteúdo é criado, gerenciado e entregue de maneira independente em dois sistemas separados.
* **Nível 1: integração de fragmento de conteúdo**
   * [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) são usados no AEM para criar e gerenciar conteúdo limitado para o SPA.
   * O SPA recupera esse conteúdo por meio da [API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) do AEM.
   * Alguns conteúdos são gerenciados no AEM e outros em um sistema externo.
   * O conteúdo só pode ser visualizado no SPA.
* **Nível 2: incorporar o SPA no AEM**
   * [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) são usados no AEM para criar e gerenciar conteúdo para o SPA.
   * O SPA recupera esse conteúdo por meio da [API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) do AEM.
   * Alguns conteúdos são gerenciados no AEM e outros em um sistema externo.
   * O conteúdo pode ser visualizado em contexto no AEM.
   * Conteúdo limitado pode ser editado no AEM.
* **Nível 3: incorporar e ativar totalmente o SPA no AEM**
   * [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) são usados no AEM para criar e gerenciar conteúdo para o SPA.
   * O SPA recupera esse conteúdo por meio da [API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) do AEM.
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
