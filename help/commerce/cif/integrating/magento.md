---
title: Integração do AEM e do Adobe Commerce (Magento) usando a Commerce Integration Framework
description: O AEM e o Adobe Commerce (Magento) são perfeitamente integrados usando a Commerce Integration Framework (CIF). A CIF permite que o AEM acesse uma instância da Magento e estabeleça uma comunicação via GraphQL. Ela também permite que os autores do AEM usem seletores de produtos e categorias e o console de produtos para navegar pelos dados de produto e categoria obtidos da Magento sob demanda. Além disso, a CIF fornece uma loja pronta para uso que agiliza projetos de comércio.
thumbnail: aem-magento-architecture.jpg
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 42%

---

# Integração do AEM e do Adobe Commerce (Magento) usando a Commerce Integration Framework {#aem-magento-framework}

O Experience Manager e o Adobe Commerce (Magento) são perfeitamente integrados usando a Commerce Integration Framework (CIF). A CIF permite que o AEM acesse e comunique diretamente com a instância principal usando as [APIs GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) do Adobe Commerce.

## Visão geral da arquitetura {#overview}

Esta é a arquitetura geral:

![Visão geral da arquitetura da CIF](../assets/AEM_Magento_Architecture.png)

A CIF oferece suporte para padrões de comunicação do lado do servidor e do lado do cliente.
As chamadas de APIs do lado do servidor são implementadas usando o cliente integrado e genérico [GraphQL](https://github.com/adobe/commerce-cif-graphql-client) em combinação com um [conjunto de modelos de dados gerados](https://github.com/adobe/commerce-cif-magento-graphql) para o esquema GraphQL de comércio Além disso, qualquer consulta ou mutação GraphQL no formato GQL pode ser usada.

Para os componentes do lado do cliente, que são criados usando o [React](https://reactjs.org/), o [cliente Apollo](https://www.apollographql.com/docs/react/) é usado.

## Arquitetura dos Componentes principais da CIF do AEM {#cif-core-components}

![Arquitetura dos Componentes principais da CIF do AEM](../assets/cif-component-architecture.jpg)

[AEM ](https://github.com/adobe/aem-core-cif-components) Os Componentes principais da CIF seguem padrões de design e práticas recomendadas muito semelhantes aos dos Componentes principais do  [AEM WCM](https://github.com/adobe/aem-core-wcm-components).

A lógica de negócios e a comunicação de back-end com o Adobe Commerce para os Componentes principais da CIF do AEM são implementadas nos Modelos do Sling. Caso seja necessário personalizar essa lógica para atender aos requisitos específicos do projeto, o padrão de delegação para Modelos do Sling pode ser usado.

>[!TIP]
>
>A página [Personalizar os Componentes principais da CIF do AEM](../customizing/customize-cif-components.md) tem um exemplo detalhado e oferece as práticas recomendadas para personalizar os componentes principais da CIF.

Nos projetos, AEM os Componentes principais da CIF e os componentes do projeto personalizado podem recuperar facilmente o cliente configurado para uma loja do Adobe Commerce associada a uma página AEM por meio da configuração com reconhecimento de contexto do Sling.
