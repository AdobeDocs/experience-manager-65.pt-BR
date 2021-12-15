---
title: 'Desenvolvimento sem periféricos para AEM 6.5 Sites '
description: Saiba como os poderosos recursos headless AEM 6.5, como Modelos de conteúdo, Fragmentos de conteúdo e a API GraphQL, funcionam juntos para permitir que você gerencie suas experiências centralmente e as disponibilize entre canais.
source-git-commit: 2f400d209148278f0695f7b9523b58bba6845cfb
workflow-type: tm+mt
source-wordcount: '493'
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

>[!TIP]
>
>Consulte o documento [Cabeça e Sem Cabeça no AEM](/help/sites-developing/headful-headless.md) para obter mais informações.

## AEM 6.5 e sem cabeça {#aem-headless}

O AEM 6.5 é uma ferramenta flexível para o modelo de implementação sem periféricos, oferecendo três serviços poderosos:

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
| [Jornada de desenvolvedores headless](/help/journey-headless/developer/overview.md) | **Para usuários novos em AEM e sem periféricos** tecnologias, comece aqui para obter uma introdução abrangente ao AEM e seus recursos sem periféricos da teoria dos sem periféricos passando a funcionar com seu primeiro projeto sem periféricos. | Guia | Desenvolvedores **novo no AEM e sem periféricos** | 1 hora |
| [Guia de introdução sem cabeçalho](/help/sites-developing/headless/getting-started/introduction.md) | **Para usuários de AEM experientes** que precisam de um breve resumo dos principais recursos AEM sem periféricos, confira esta visão geral de início rápido. | Início rápido | Desenvolvedores, administradores **com AEM experiência** | 20 minutos |
| [Introdução ao AEM tutorial prático](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **Se preferir uma abordagem prática e estiver familiarizado com AEM**, este tutorial mergulha diretamente na criação de um projeto sem periféricos simples. | Tutorial | Desenvolvedores | 2 horas |
