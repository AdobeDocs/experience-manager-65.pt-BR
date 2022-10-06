---
title: Desenvolvimento sem periféricos para AEM 6.5 Sites
description: Saiba como os poderosos recursos headless AEM 6.5, como Modelos de conteúdo, Fragmentos de conteúdo e a API GraphQL, funcionam juntos para permitir que você gerencie suas experiências centralmente e as disponibilize entre canais.
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 38%

---

# Desenvolvimento sem periféricos para AEM 6.5 Sites {#headless-development}

Saiba como os poderosos recursos headless AEM 6.5, como Modelos de conteúdo, Fragmentos de conteúdo e a API GraphQL, funcionam juntos para permitir que você gerencie suas experiências centralmente e as disponibilize entre canais.

## Visão geral {#overview}

A implementação sem periféricos está se tornando cada vez mais importante para fornecer experiências ao seu público-alvo, onde quer que estejam e independentemente do canal.

A implementação headless deixa de lado o gerenciamento de páginas e componentes, como é tradicional em soluções de pilha completa e híbridas, e se concentra na criação de fragmentos de conteúdo reutilizáveis e neutros em relação à canais, assim como na entrega desses fragmentos entre canais. É um padrão de desenvolvimento moderno e dinâmico para implementar experiências na web.

![Modelos de implementação do AEM](assets/aem-implementation-models.png)

## Comparação entre headful e headless {#headful-headless}

Este documento se concentra no modelo de implementação sem periféricos de AEM. No entanto, “headful ou headless” não precisa ser uma escolha binária no AEM. Os recursos headless podem ser usados para gerenciar e entregar seu conteúdo a uma variedade de endpoints, além de permitir que os autores de conteúdo editem aplicativos de página única. Tudo no AEM.

>[!TIP]
>
>Consulte o documento [Headful e Headless no AEM](/help/sites-developing/headful-headless.md) para obter mais informações.

## AEM 6.5 e sem cabeça {#aem-headless}

O AEM 6.5 é uma ferramenta flexível para o modelo de implementação sem periféricos, oferecendo três serviços poderosos:

1. Modelos de conteúdo
   * Os modelos de conteúdo são uma representação estruturada do conteúdo.
   * Eles são definidos pelos arquitetos de informações no editor AEM do Modelo de fragmento de conteúdo.
   * Os modelos de conteúdo são a base para os fragmentos de conteúdo.
1. Fragmentos de conteúdo
   * Fragmentos de conteúdo são instanciações de modelos de conteúdo.
   * Eles são criados por autores de conteúdo usando o editor AEM Fragmento de conteúdo .
   * Eles são armazenados no AEM Assets e gerenciados na interface do usuário do administrador do Assets.
1. API de conteúdo para entrega
   * A API GraphQL do AEM é compatível com a entrega de fragmentos de conteúdo.
   * A API REST do AEM Assets é compatível com operações CRUD de fragmentos de conteúdo.
   * A entrega de conteúdo direto também é possível com a variável [Exportação JSON do Componente principal do fragmento de conteúdo.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=pt-BR)

## Primeiros passos no AEM Headless {#first-steps}

Há vários recursos disponíveis para você começar a usar AEM recursos headless. Elas são destinadas a casos de uso diferentes, mas todas fornecem uma visão geral sólida AEM recursos sem periféricos.

| Recurso | Descrição | Tipo | Público | Est. Hora |
|---|---|---|---|---|
| [Jornada de desenvolvedores headless](/help/journey-headless/developer/overview.md) | **Para usuários novos em AEM e sem periféricos** tecnologias, comece aqui para obter uma introdução abrangente ao AEM e seus recursos sem periféricos da teoria dos sem periféricos passando a funcionar com seu primeiro projeto sem periféricos. | Guia | Desenvolvedores **novatos no AEM e no headless** | 1 hora |
| [Guia de introdução do Headless](/help/sites-developing/headless/getting-started/introduction.md) | **Para usuários experientes do AEM** que precisam de um breve resumo dos principais recursos headless do AEM, confira esta visão geral de início rápido. | Início rápido | Desenvolvedores e administradores **com experiência no AEM** | 20 minutos |
| [Introdução ao AEM tutorial prático](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=pt-BR) | **Se preferir uma abordagem prática e estiver familiarizado com AEM**, este tutorial mergulha diretamente na criação de um projeto sem periféricos simples. | Tutorial | Desenvolvedores | 2 horas |
