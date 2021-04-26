---
title: Integração de comércio de terceiros com o AEM usando a Commerce Integration Framework
description: Corporações podem exigir outras soluções comerciais de terceiros para potencializar a loja. A Commerce Integration Framework (CIF) pode ser usada em tais cenários de integração para conectar uma solução comercial de terceiros à Adobe Experience Manager usando a I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 14%

---

# Integração de comércio de terceiros com o AEM usando a Commerce Integration Framework {#aem-third-party}

A integração da solução de comércio não-Adobe é um cenário comum para a CIF. Soluções de terceiros com APIs e esquemas diferentes são conectadas por meio de uma camada de integração.

## Arquitetura {#architecture}

Esta é a arquitetura geral:

![Visão geral da arquitetura do AEM sem a Magento e com soluções de terceiros](../assets//AEM_nonMagento_Architecture.png)

A finalidade dessa camada de integração é mapear APIs e esquemas de terceiros em relação às APIs GraphQL do Adobe Commerce compatíveis e aos esquemas fora do Experience Manager. Graças a esse encapsulamento, a lógica e os sistemas de integração podem ser atualizados sem alterar o código dentro do Experience Manager.

## Requisitos da solução para uma integração

Como o Experience Manager recupera dados sob demanda, são necessárias APIs em tempo real para o catálogo de produtos.

>[!TIP]
>
>Se nenhuma API em tempo real estiver disponível, um cache de produto externo com APIs deverá ser usado para a integração. Exemplo [Magento open-source](https://magento.com/products/magento-open-source).

Não há necessidade de implementar o esquema GraphQL completo, apenas os objetos do esquema para permitir os casos de uso desejados.

## Casos de uso de backend

A CIF amplia o Experience Manager com acesso a catálogos de produtos em tempo real e ferramentas de gerenciamento de experiência de produtos. Essa integração perfeita permite que os autores acessem dados de comércio usando interfaces de usuário incorporadas, sempre que necessário, sem deixar o contexto de conteúdo.

A integração das APIs do catálogo de produtos é necessária para desbloquear esses casos de uso.

## Casos de uso de fronteira

[AEM ](https://github.com/adobe/aem-core-cif-components) os Componentes principais da CIF recuperam e trocam dados por meio das APIs de comércio do Adobe compatíveis com a CIF. Para reutilizar componentes, as respectivas APIs precisam ser implementadas.

A recomendação para componentes essenciais de desempenho do lado do cliente é comunicar diretamente com a solução de terceiros para evitar latência.

## Desenvolvimento de uma integração {#develop-integration}

Recomendamos usar [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) para a camada de integração. Ele está incluído no complemento CIF para terceiros. Como funciona com uma abordagem semelhante a um microsserviço, é adequado integrar facilmente várias soluções.

A [implementação de referência](https://github.com/adobe/commerce-cif-graphql-integration-reference) é um excelente ponto de partida para criar a integração na sua solução comercial. Embora seja compatível com GraphQL, também pode ser integrado a qualquer outro tipo de API, como REST.

Essa camada de integração não é necessária se uma camada de terceiros estiver disponível (por exemplo, mulesoft) ou se a integração for criada sobre a solução de terceiros.
