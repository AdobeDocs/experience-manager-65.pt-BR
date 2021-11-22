---
title: 'Desenvolvimento sem periféricos para AEM 6.5 Sites '
description: Saiba como os poderosos recursos headless AEM 6.5, como Modelos de conteúdo, Fragmentos de conteúdo e a API GraphQL, funcionam juntos para permitir que você gerencie suas experiências centralmente e as disponibilize entre canais.
source-git-commit: a95cf285be84f6aed194f3ae904556f5d017c7be
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---


# Desenvolvimento sem periféricos para AEM 6.5 Sites {#headless-development}

Saiba como os poderosos recursos headless AEM 6.5, como Modelos de conteúdo, Fragmentos de conteúdo e a API GraphQL, funcionam juntos para permitir que você gerencie suas experiências centralmente e as disponibilize entre canais.

## Visão geral {#overview}

A implementação sem periféricos está se tornando cada vez mais importante para fornecer experiências ao seu público-alvo, onde quer que estejam e independentemente do canal.

A implementação sem cabeçalho perde o gerenciamento de página e componente, como é tradicional em soluções de pilha completa e híbridas, e se concentra na criação de fragmentos de conteúdo neutros em canais e reutilizáveis, além de seu delivery entre canais. É um padrão de desenvolvimento moderno e dinâmico para implementar experiências da Web.

![Modelos de implementação de AEM](assets/aem-implementation-models.png)

## Comparação entre headful e headless {#headful-headless}

Este documento se concentra no modelo de implementação sem periféricos de AEM. No entanto, o headful versus headless não precisam ser uma escolha binária no AEM. Os recursos headless podem ser usados para gerenciar e entregar seu conteúdo a uma variedade de endpoints, além de permitir que os autores de conteúdo editem aplicativos de página única. Tudo em AEM.

<!--
>[!TIP]
>
>See the document [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) for more information.
-->

## AEM 6.5 e sem cabeça {#aem-headless}

AEM as a Cloud Service é uma ferramenta flexível para o modelo de implementação sem periféricos, oferecendo três serviços poderosos:

1. Modelos de conteúdo
   * Os Modelos de conteúdo são representação estruturada do conteúdo.
   * Eles são definidos pelos arquitetos de informações no editor AEM do Modelo de fragmento de conteúdo.
   * Os Modelos de conteúdo são a base dos Fragmentos de conteúdo.
1. Fragmentos de conteúdo
   * Fragmentos de conteúdo são instanciações de modelos de conteúdo.
   * Eles são criados por autores de conteúdo usando o editor AEM Fragmento de conteúdo .
   * Eles são armazenados no AEM Assets e gerenciados na interface do usuário do administrador do Assets.
1. API de conteúdo para entrega
   * A API GraphQL da AEM é compatível com a entrega de Fragmento de conteúdo.
   * A API REST do AEM Assets suporta operações CRUD de Fragmento de conteúdo.
   * A entrega de conteúdo direto também é possível com a variável [Exportação JSON do Componente principal do fragmento de conteúdo.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## Seus primeiros passos com AEM headless {#first-steps}

Há vários recursos disponíveis para você começar a usar AEM recursos headless. Elas são destinadas a casos de uso diferentes, mas todas fornecem uma visão geral sólida AEM recursos sem periféricos.

| Recurso | Descrição | Tipo | Público | Est. Hora |
|---|---|---|---|---|
| [Introdução ao AEM tutorial prático](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **Se preferir uma abordagem prática e estiver familiarizado com AEM**, este tutorial mergulha diretamente na criação de um projeto sem periféricos simples. | Tutorial | Desenvolvedores | 2 horas |

<!--
|Resource|Description|Type|Audience|Est. Time|
|---|---|---|---|---|
|[Headless Developer Journey](/help/journey-headless/developer/overview.md)|**For users new to AEM and headless** technologies, start here for a comprehensive introduction to AEM and its headless features from the theory of headless through going live with your first headless project.|Guide|Developers **new to AEM and headless**|1 hour|
|[Headless Getting Started Guide](/help/implementing/developing/headless/getting-started/introduction.md)|**For experienced AEM users** who need a short summary of the key AEM headless features, check out this quick start overview.|Quick Start|Developers, Administrators **with AEM experience**|20 minutes|
|[Getting Started with AEM Headless hands-on tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)|**If you prefer a hands-on approach and are familiar with AEM**, this tutorial dives directly into creating a simple headless project.|Tutorial|Developers|2 hours|
-->
