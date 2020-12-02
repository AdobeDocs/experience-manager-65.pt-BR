---
title: Visão geral do eCommerce
seo-title: Visão geral do eCommerce
description: AEM eCommerce genérico está disponível como parte da instalação padrão e fornece a você toda a funcionalidade da estrutura de eCommerce.
seo-description: AEM eCommerce genérico está disponível como parte da instalação padrão e fornece a você toda a funcionalidade da estrutura de eCommerce.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 5d46836a8b7b66daa8f27bc6fad14319ab1f58a7
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 7%

---


# Visão geral do comércio eletrônico{#ecommerce-overview}

AEM eCommerce genérico está disponível como parte de uma instalação padrão e fornece a você toda a funcionalidade da estrutura de eCommerce.

O Adobe fornece duas versões da Commerce Integration Framework:

|  | CIF no local | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versões compatíveis do AEM | AEM no local ou AMS 6.x | AEM AMS 6.4 e 6.5 |
| Back-end | - AEM, Java <br> - Integração monolítica, mapeamento pré-compilação (modelo)<br> - Repositório JCR | - Magento <br>- Java e Javascript <br>- Nenhum dado de comércio armazenado no repositório JCR |
| Front-end | Páginas renderizadas do servidor AEM | Aplicativo de página mista (renderização híbrida) |
| Catálogo de produtos | - Importador de produtos, editor, cache em AEM <br>- Catálogos regulares com páginas AEM ou proxy | - Nenhuma importação de produto <br>- Modelos genéricos <br>- Dados sob demanda via conector |
| Escalabilidade | - Pode suportar até alguns milhões de produtos (depende do caso de uso) <br> - Armazenamento em cache no Dispatcher | - Nenhuma limitação de volume <br>- Cache no Dispatcher ou CDN |
| Modelo de dados padronizado | Não | Sim, schema Magento GraphQL |
| Disponibilidade | Sim:<br> - Commerce Cloud SAP (extensão atualizada para suportar AEM 6.4 e Hybris 5 (padrão) e mantém a compatibilidade com Hybris 4 <br>- Salesforce Commerce Cloud (conector de fonte aberta para suporte ao AEM 6.4) | Sim via código aberto via GitHub. <br> Magento Commerce (Suporta Magento 2.3.2 (padrão) e compatível com Magento 2.3.1). |
| Quando usar | Casos de utilização limitados: Para situações em que catálogos pequenos e estáticos podem precisar ser importados | Solução preferencial na maioria dos casos de uso |


## Implantação de outras implementações {#deploying-other-implementations}

Para AEM e Magento, consulte [AEM e Magento integration](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md) usando a [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html).

>[!NOTE]
>
>Para obter informações sobre conceitos e como administrar implementações de eCommerce, consulte [Administração de eCommerce](/help/sites-administering/ecommerce.md).
>
>Para obter informações sobre como estender os recursos de comércio eletrônico, consulte [Desenvolvimento do comércio eletrônico](/help/sites-developing/ecommerce.md).

