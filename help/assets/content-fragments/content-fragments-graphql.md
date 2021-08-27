---
title: Entrega de conteúdo sem cabeçalho usando Fragmentos de conteúdo com GraphQL
description: Saiba como usar AEM Fragmentos de conteúdo com GraphQL para a entrega de conteúdo sem interface.
feature: Content Fragments
role: User
source-git-commit: 819df6d6123575b378676dda200064725de47b84
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 1%

---

# Entrega de conteúdo sem cabeçalho usando Fragmentos de conteúdo com GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

Com o Adobe Experience Manager (AEM), é possível usar os Fragmentos de conteúdo, juntamente com a API GraphQL AEM (uma implementação personalizada, com base no GraphQL padrão), para fornecer conteúdo estruturado de maneira headless para uso em seus aplicativos. A capacidade de personalizar uma única consulta de API permite recuperar e entregar o conteúdo específico que você deseja/precisa renderizar (como resposta à única consulta de API).

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>O GraphQL é usado atualmente em dois cenários (separados) no Adobe Experience Manager (AEM):
>
>* [O AEM Commerce consome dados de uma plataforma de comércio via GraphQL](/help/commerce/cif/integrating/magento.md).
>* [AEM Fragmentos de conteúdo trabalham com a API GraphQL AEM (uma implementação personalizada, com base no GraphQL padrão), para fornecer conteúdo estruturado para uso em seus aplicativos](/help/assets/content-fragments/graphql-api-content-fragments.md).


## CMS sem periféricos {#headless-cms}

Um Sistema de Gerenciamento de Conteúdo Sem Cabeçalho (CMS) é:

* &quot;*Um sistema de gerenciamento de conteúdo sem periféricos, ou CMS sem periféricos, é um sistema de gerenciamento de conteúdo (CMS) de back-end criado desde o início como um repositório de conteúdo que torna o conteúdo acessível por meio de uma API para exibição em qualquer dispositivo.*

   Consulte [Wikipédia](https://en.wikipedia.org/wiki/Headless_content_management_system).

Em termos de criação de Fragmentos de conteúdo no AEM isso significa que:

* Você pode usar Fragmentos de conteúdo para criar conteúdo que não se destina principalmente a ser publicado diretamente (1:1) em páginas formatadas.

* O conteúdo dos Fragmentos de conteúdo será estruturado de maneira predeterminada, de acordo com os Modelos de fragmento de conteúdo. Isso simplifica o acesso para seus aplicativos, o que processará ainda mais seu conteúdo.

## GraphQL - Uma visão geral {#graphql-overview}

GraphQL é:

* &quot;*...um idioma de consulta para APIs e um tempo de execução para realizar essas consultas com seus dados existentes.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

O [AEM API GraphQL](#aem-graphql-api) permite executar consultas (complexas) nos [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md); com cada query de acordo com um tipo de modelo específico. O conteúdo retornado pode ser usado pelos seus aplicativos.

## AEM API GraphQL {#aem-graphql-api}

Para a Adobe Experience Cloud, uma implementação personalizada da API GraphQL padrão foi desenvolvida. Consulte [AEM API GraphQL para usar com Fragmentos de conteúdo](/help/assets/content-fragments/graphql-api-content-fragments.md) para obter detalhes.

A implementação AEM da API GraphQL é baseada nas [bibliotecas GraphQL Java](https://graphql.org/code/#java).

## Fragmentos de conteúdo para uso com a API GraphQL da AEM {#content-fragments-use-with-aem-graphql-api}

[Os ](#content-fragments) Fragmentos de conteúdo podem ser usados como base para GraphQL para consultas de AEM como:

* Eles permitem projetar, criar, preparar e publicar conteúdo independente da página.
* Os [Modelos de fragmento de conteúdo](#content-fragments-models) fornecem a estrutura necessária por meio de tipos de dados definidos.
* A [Referência do fragmento](#fragment-references), disponível ao definir um modelo, pode ser usada para definir camadas adicionais de estrutura.

![Fragmentos de conteúdo para uso com Fragmentos ](assets/cfm-nested-01.png "GraphQLContent para uso com GraphQL")

### Fragmentos de conteúdo {#content-fragments}

Fragmentos de conteúdo:

* Contém conteúdo estruturado.

* Elas são baseadas em um [Modelo de fragmento de conteúdo](#content-fragments-models), que predefine a estrutura do fragmento resultante.

### Modelos de fragmentos do conteúdo {#content-fragments-models}

Esses [Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md):

* São usados para gerar os [Schemas](https://graphql.org/learn/schema/), uma vez **Enabled**.

* Forneça os tipos de dados e campos necessários para GraphQL. Eles garantem que seu aplicativo solicite apenas o que é possível e receba o que é esperado.

* O tipo de dados **[Referências de fragmento](#fragment-references)** pode ser usado em seu modelo para fazer referência a outro Fragmento de conteúdo e, portanto, introduzir níveis adicionais de estrutura.

### Referências de fragmento {#fragment-references}

A **[Referência do fragmento](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* É de especial interesse em conjunto com GraphQL.

* É um tipo de dados específico que pode ser usado ao definir um Modelo de fragmento de conteúdo.

* Faz referência a outro fragmento, dependendo de um modelo de fragmento de conteúdo específico.

* Permite recuperar dados estruturados.

   * Quando definido como **multifeed**, vários subfragmentos podem ser referenciados (recuperados) pelo fragmento principal.

### Visualização JSON {#json-preview}

Para ajudar na criação e desenvolvimento dos Modelos de fragmento de conteúdo, você pode visualizar [saída JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

## Saiba como usar GraphQL com AEM - Conteúdo de amostra e consultas {#learn-graphql-with-aem-sample-content-queries}

Consulte [Saiba como usar GraphQL com AEM - Conteúdo de amostra e Consultas](/help/assets/content-fragments/content-fragments-graphql-samples.md) para obter uma introdução sobre como usar a API GraphQL AEM.

## Tutorial - Introdução ao AEM Headless e GraphQL

Procurando um tutorial prático? Confira o [Introdução ao AEM Headless e o tutorial GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) completo ilustrando como criar e expor conteúdo usando as APIs GraphQL da AEM e consumidas por um aplicativo externo, em um cenário de CMS sem periféricos.
