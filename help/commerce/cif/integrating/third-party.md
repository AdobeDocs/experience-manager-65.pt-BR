---
title: Integração de comércio de terceiros com o AEM usando a Commerce Integration Framework
description: Empresas corporativas podem precisar de soluções comerciais adicionais de terceiros para potencializar sua loja. A Commerce Integration Framework (CIF) pode ser usada em tais cenários de integração para conectar uma solução comercial de terceiros à Adobe Experience Manager usando a I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
exl-id: e99899a4-df86-4108-991a-8b30d303a279
source-git-commit: 885d0763fca9ad4eab499081adca9b83875b27e1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 3%

---

# Integração de comércio de terceiros com o AEM usando a Commerce Integration Framework {#aem-third-party}

A integração de soluções que não sejam da Adobe Commerce é um cenário comum da CIF. soluções de terceiros com diferentes APIs e esquemas são conectadas por meio de uma camada de integração.

## Arquitetura {#architecture}

Esta é a arquitetura geral:

![Visão geral da arquitetura AEM de terceiros/não-Magento](../assets//AEM_nonMagento_Architecture.png)

A finalidade dessa camada de integração é mapear APIs e esquemas de terceiros em relação às APIs e esquemas compatíveis do Adobe Commerce GraphQL fora do Experience Manager. Graças a esse encapsulamento, a lógica e os sistemas de integração podem ser atualizados sem alterar o código dentro do Experience Manager.

## Requisitos da solução para uma integração

À medida que o Experience Manager recupera dados sob demanda, são necessárias APIs em tempo real para catálogos de produtos.

>[!TIP]
>
>Se nenhuma API em tempo real estiver disponível, um cache de produto externo com APIs deverá ser usado para a integração. Exemplo [Magento open-source](https://business.adobe.com/products/magento/open-source.html).

Não há necessidade de implementar o esquema completo do GraphQL, apenas os objetos do esquema para ativar os casos de uso desejados.

## Casos de uso de back-end

A CIF amplia o Experience Manager com acesso ao catálogo de produtos em tempo real e ferramentas de gerenciamento de experiência do produto. Essa integração contínua permite que os autores acessem dados de comércio usando interfaces do usuário incorporadas sempre que necessário, sem sair do contexto do conteúdo.

A integração das APIs de catálogo de produtos é necessária para desbloquear esses casos de uso.

## Casos de uso de front-end

[Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) recuperar e trocar dados por meio das APIs do Adobe Commerce compatíveis com a CIF. Para reutilizar componentes, as respectivas APIs precisam ser implementadas.

A recomendação para componentes do lado do cliente de desempenho crítico é se comunicar diretamente com a solução de terceiros para evitar latência.

## Desenvolvimento de uma integração {#develop-integration}

Recomendamos usar [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) para a camada de integração. Ele está incluído no complemento CIF para terceiros. Como funciona com uma abordagem semelhante a um microsserviço, é adequado para integrar facilmente várias soluções.

A variável [implementação de referência](https://github.com/adobe/commerce-cif-graphql-integration-reference) O é um excelente ponto de partida para criar a integração com sua solução comercial. Embora seja compatível com o GraphQL, ele também pode ser integrado a qualquer outro tipo de API, como REST.

Essa camada de integração não será necessária se uma camada de terceiros estiver disponível (como a Mulesoft) ou se a integração for criada sobre a solução de terceiros.

## Conectores pré-construídos {#connectors}

Os conectores são um bom ponto de partida para os projetos. Eles vêm com uma conexão específica da solução comercial e mapeamento de API padrão. Esses conectores são criados por terceiros e não são mantidos pelo Adobe. Entre em contato com o respectivo parceiro para obter informações.

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris), construído por Diconium
* [Ferramentas comerciais](https://github.com/diconium/commerce-cif-graphql-integration-commercetool), construído por Diconium

>[!TIP]
>
>Embora os conectores ajudem os projetos a acelerar a integração comercial, eles não são plug-in-play. As soluções comerciais corporativas geralmente são altamente personalizadas e exigem uma integração personalizada. É necessário um bom conhecimento da plataforma de comércio, dos esquemas do Adobe Commerce GraphQL e do Adobe I/O Runtime.
