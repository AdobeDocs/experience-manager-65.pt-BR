---
title: Visão geral de comércio eletrônico
seo-title: eCommerce Overview
description: O eCommerce genérico do AEM está disponível como parte da instalação padrão e fornece a funcionalidade completa da estrutura de eCommerce.
seo-description: AEM generic eCommerce is available as part of the standard installation and provides you with the full functionality of the eCommerce framework.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 3%

---

# Visão geral de comércio eletrônico{#ecommerce-overview}

O eCommerce genérico do AEM está disponível como parte de uma instalação padrão e fornece a funcionalidade completa da estrutura de eCommerce.

O Adobe fornece duas versões da Commerce Integration Framework:

|                         | CIF no local | Nuvem da CIF |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versões compatíveis do AEM | AEM no local ou AMS 6.x | AEM AMS 6.4 e 6.5 |
| Back-end | - AEM, Java <br> - Integração monolítica, mapeamento pré-compilação (modelo)<br> - Repositório JCR | - ADOBE COMMERCE <br>- Java e JavaScript <br>- Nenhum dado do Commerce armazenado no repositório JCR |
| Front-end | Páginas renderizadas do lado do servidor do AEM | Aplicativo de página mista (renderização híbrida) |
| Catálogo de produtos | - Importador de produto, editor, armazenamento em cache no AEM <br>- Catálogos regulares com AEM ou páginas de proxy | - Nenhuma importação de produto <br>- Modelos genéricos <br>- Dados sob demanda por meio do conector |
| Escalabilidade | - Pode oferecer suporte a até alguns milhões de produtos (depende do caso de uso) <br> - Armazenamento em cache no Dispatcher | - Sem limitação de volume <br>- Armazenamento em cache no Dispatcher ou CDN |
| Modelo de dados padronizado | Não | Sim, esquema do Adobe Commerce GraphQL |
| Disponibilidade | Sim:<br> - SAP Commerce Cloud (Extensão atualizada para oferecer suporte a AEM 6.4 e Hybris 5 (padrão) e mantém compatibilidade com o Hybris 4 <br>- Commerce Cloud do Salesforce (conector de código aberto para suporte ao AEM 6.4) | Sim, via código aberto via GitHub. <br> Adobe Commerce (Suporta 2.3.2 (padrão) e compatível com 2.3.1). |
| Quando usar | Casos de uso limitados: para cenários em que catálogos pequenos e estáticos podem precisar ser importados | Solução preferida na maioria dos casos de uso |


## Implantar outras implementações {#deploying-other-implementations}

Para AEM e Adobe Commerce, consulte [Integração entre AEM e Adobe Commerce](/help/commerce/cif/integrating/magento.md) usando o [Estrutura de integração do Commerce](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Para obter informações sobre conceitos e administração de implementações de comércio eletrônico, consulte [Administração de comércio eletrônico](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Para obter informações sobre como estender os recursos de comércio eletrônico, consulte [Desenvolvimento do comércio eletrônico](/help/commerce/cif-classic/developing/ecommerce.md).
