---
title: Visão geral do eCommerce
seo-title: Visão geral do eCommerce
description: AEM eCommerce genérico está disponível como parte da instalação padrão e oferece a você a funcionalidade completa da estrutura do eCommerce.
seo-description: AEM eCommerce genérico está disponível como parte da instalação padrão e oferece a você a funcionalidade completa da estrutura do eCommerce.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Estrutura de integração de comércio
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 8%

---


# Visão geral do eCommerce{#ecommerce-overview}

AEM eCommerce genérico está disponível como parte de uma instalação padrão e oferece a você toda a funcionalidade da estrutura do eCommerce.

O Adobe fornece duas versões da Estrutura de integração de comércio:

|  | CIF no local | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versões compatíveis do AEM | AEM no local ou AMS 6.x | AEM AMS 6.4 e 6.5 |
| Back-end | - AEM, Java <br> - Integração monolítica, mapeamento de pré-compilação (modelo)<br> - Repositório JCR | - Magento <br> - Java e Javascript <br> - Nenhum dado do Commerce armazenado no repositório JCR |
| Front-end | AEM páginas renderizadas do lado do servidor | Aplicativo de página mista (renderização híbrida) |
| Catálogo de produtos | - Importador de produto, editor, armazenamento em cache em AEM <br>- Catálogos regulares com páginas AEM ou proxy | - Nenhuma importação de produto <br>- Modelos genéricos <br>- Dados sob demanda via conector |
| Escalabilidade | - Pode suportar até alguns milhões de produtos (depende do caso de uso) <br> - Armazenamento em cache no Dispatcher | - Sem limitação de volume <br>- Armazenamento em cache no Dispatcher ou CDN |
| Modelo de dados padronizado | Não | Sim, esquema Magento GraphQL |
| Disponibilidade | Sim:<br> - SAP Commerce Cloud (Extensão atualizada para suportar o AEM 6.4 e o Hybris 5 (padrão) e mantém compatibilidade com o Hybris 4 <br>- Salesforce Commerce Cloud (Conector de código aberto para suporte ao AEM 6.4) | Sim por meio do código aberto via GitHub. <br> Magento Commerce (Suporta Magento 2.3.2 (padrão) e compatível com o Magento 2.3.1). |
| Quando usar | Casos de uso limitados: Para cenários em que catálogos pequenos e estáticos podem precisar ser importados | Solução preferencial na maioria dos casos de uso |


## Implantar Outras Implementações {#deploying-other-implementations}

Para AEM e Magento, consulte [AEM e Magento integration](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md) usando o [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html).

>[!NOTE]
>
>Para obter informações sobre conceitos e como administrar implementações de eCommerce, consulte [Administração de eCommerce](/help/sites-administering/ecommerce.md).
>
>Para obter informações sobre como estender os recursos do eCommerce, consulte [Desenvolvendo eCommerce](/help/sites-developing/ecommerce.md).

