---
title: Headful e Headless no AEM
description: AEM projetos podem ser implementados em um modelo headful e sem interface, mas a escolha não é binária. AEM oferece a flexibilidade para explorar as vantagens de ambos os modelos em um projeto.
exl-id: c9597c78-be05-42ff-84fe-f7451119e83d
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 1%

---

# Headful e Headless no AEM {#headful-headless}

Os projetos do Adobe Experience Manager podem ser implementados em modelos headful e sem periféricos, mas a escolha não é binária. AEM oferece a flexibilidade para explorar as vantagens de ambos os modelos em um projeto. Este documento fornece uma visão geral dos diferentes modelos e descreve os níveis de integração SPA.

## Visão geral {#overview}

O AEM oferece ferramentas poderosas para gerenciar a criação de conteúdo e seu delivery em uma única plataforma. Esse é um modelo &quot;headful&quot; tradicional de gestão de conteúdo, em que os autores e desenvolvedores de conteúdo trabalham na mesma plataforma para fornecer as experiências aos consumidores de conteúdo.

AEM também pode ser usado para simplesmente gerenciar o conteúdo, permitindo que a apresentação e a entrega do conteúdo sejam gerenciadas por outra plataforma. Esse é o modelo &quot;sem interface&quot; de gerenciamento de conteúdo, em que os autores e desenvolvedores de conteúdo trabalham em plataformas diferentes para fornecer experiência aos consumidores de conteúdo.

Mas isso não precisa ser uma escolha binária. AEM oferece flexibilidade sem precedentes, permitindo explorar as vantagens de ambos os modelos para o seu projeto.

![Modelos de implementação do AEM](headless/assets/aem-implementation-models.png)

Em um modelo com pilha completa ou headful, o conteúdo é gerenciado no repositório AEM e AEM componentes com base em Java, HTL etc. são usados para renderizar o conteúdo da experiência do usuário. Neste modelo, a criação de conteúdo, o estilo, a apresentação e o delivery tudo acontece em AEM.

Em um modelo sem cabeçalho, o conteúdo é gerenciado no repositório de AEM, mas entregue por APIs, como REST e GraphQL, a outro sistema para renderizar o conteúdo da experiência do usuário. Neste modelo, o conteúdo é criado em AEM, mas o estiliza, a apresentação e o delivery tudo acontece em outra plataforma.

Aplicativos de página única (SPA) geralmente são o destino para o conteúdo entregue de forma headless por AEM. No entanto, estas SPA não têm de ser totalmente externas à AEM. AEM permite decidir em que grau seus SPA estão integrados ao AEM. Vejamos um exemplo.

## Exemplo de compra da Web {#web-shop-example}

Digamos que você tem uma web shop existente para sua empresa como SPA. Você tem todos os detalhes e imagens do seu produto. Em seguida, você apresenta o AEM para potencializar seus esforços de marketing, como sites promocionais, blogs e conteúdo da campanha. Como o senhor integra os dois? AEM permite um espectro de opções:

* **Permitir que os sistemas funcionem de forma independente.**
* **Forneça conteúdo limitado à loja da Web via GraphQL.** O conteúdo pode ser criado por autores no AEM, mas somente visto por meio da SPA da loja na Web.
* **Incorpore o SPA da web shop no AEM.** O conteúdo pode ser criado por autores no AEM e visualizado no AEM no contexto da loja da Web, mas não manipulado.
* **Incorpore o SPA da web shop no AEM e ative pontos editáveis.** O conteúdo pode ser criado por autores no AEM e visualizado no AEM no contexto da loja da Web, e os autores têm capacidade limitada de manipular o conteúdo da loja da Web SPA dentro do AEM.
* **Incorpore o SPA da loja da Web no AEM e ative zonas inteiras para edição.** O conteúdo pode ser criado por autores no AEM e visualizado no AEM no contexto da loja da Web, e os autores têm capacidade limitada de manipular o conteúdo da loja da Web SPA dentro do AEM.

A próxima seção explora esses níveis de integração com mais detalhes.

>[!NOTE]
>
>É claro que você também poderia reimplementar o SPA da web shop como um AEM totalmente funcional SPA [usando a estrutura AEM SPA Editor .](/help/sites-developing/spa-walkthrough.md) Se você já tiver AEM e quiser criar uma nova web shop ou outra SPA, esse será o método recomendado, mas ele estará fora do escopo deste documento.

## Níveis de integração de SPA {#integration-levels}

SPA integração se enquadra em um espectro de quatro níveis em AEM.

* **Nível 0: Sem integração**
   * Os SPA e AEM existem separadamente e não trocam informações.
   * O conteúdo é criado, gerenciado e entregue de maneira independente em dois sistemas separados.
* **Nível 1: Integração do fragmento de conteúdo**
   * [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) são usados no AEM para criar e gerenciar conteúdo limitado para o SPA.
   * O SPA recupera esse conteúdo via AEM [API GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Alguns conteúdos são gerenciados no AEM e outros em um sistema externo.
   * O conteúdo só pode ser visualizado no SPA.
* **Nível 2: Incorpore o SPA no AEM**
   * [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) são usados no AEM para criar e gerenciar conteúdo para o SPA.
   * O SPA recupera esse conteúdo via AEM [API GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Alguns conteúdos são gerenciados no AEM e outros em um sistema externo.
   * O conteúdo pode ser visualizado em contexto no AEM.
   * Conteúdo limitado pode ser editado no AEM.
* **Nível 3: Incorporar e ativar totalmente o SPA no AEM**
   * [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) são usados no AEM para criar e gerenciar conteúdo para o SPA.
   * O SPA recupera esse conteúdo via AEM [API GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * O conteúdo pode ser visualizado em contexto no AEM.
   * A maioria do conteúdo pode ser editada no AEM.

O Nível 1 é um exemplo de uma implementação sem cabeçalho típica. No entanto, os autores de conteúdo só podem visualizar seu conteúdo no contexto da SPA. AEM é apenas uma ferramenta de criação.

A vantagem e a flexibilidade da AEM tornam-se evidentes com os níveis 2 e 3, mantendo ao mesmo tempo as vantagens da SPA. Os autores de conteúdo podem criar o conteúdo no AEM, mas também visualizá-lo no contexto do AEM. O SPA ganha a capacidade de ser criado em AEM, mas ainda pode ser entregue como um SPA.

## Implementar os níveis de integração {#implementing}

Há diferentes ferramentas no AEM disponíveis, dependendo do nível de integração escolhido. Cada nível se baseia nas ferramentas usadas no anterior. A lista a seguir vincula-se aos recursos relevantes.

* **Nível 1:** Fragmentos de conteúdo e o [AEM estrutura headless](/help/sites-developing/headless/introduction.md) pode ser usado para fornecer conteúdo AEM ao SPA.
* **Nível 2:** Além do nível um:
   * [O componente RemotePage](/help/sites-developing/spa-remote-page.md) pode ser usado para incorporar o SPA externo ao AEM, onde AEM conteúdo pode ser visualizado em contexto.
   * Alguns pontos no SPA também podem ser habilitados para [permitir edição limitada no AEM.](/help/sites-developing/spa-edit-external.md)
* **Nível 3:** Além do nível dois:
   * Zonas inteiras do SPA podem ser habilitadas para permitir uma edição abrangente no AEM.
