---
title: Visão geral do eCommerce
seo-title: eCommerce Overview
description: AEM eCommerce genérico está disponível como parte da instalação padrão e oferece a você a funcionalidade completa da estrutura do eCommerce.
seo-description: AEM generic eCommerce is available as part of the standard installation and provides you with the full functionality of the eCommerce framework.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 3%

---

# Visão geral do eCommerce{#ecommerce-overview}

AEM eCommerce genérico está disponível como parte de uma instalação padrão e oferece a você toda a funcionalidade da estrutura do eCommerce.

O Adobe fornece duas versões da Estrutura de integração de comércio:

|  | CIF no local | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versões compatíveis do AEM | AEM no local ou AMS 6.x | AEM AMS 6.4 e 6.5 |
| Back-end | - AEM, Java <br> - Integração monolítica, mapeamento pré-criado (modelo)<br> - Repositório JCR | - Adobe Commerce <br>- Java e Javascript <br>- Nenhum dado do Commerce armazenado no repositório JCR |
| Front-end | AEM páginas renderizadas do lado do servidor | Aplicativo de página mista (renderização híbrida) |
| Catálogo de produtos | - Importador de produto, editor, armazenamento em cache em AEM <br>- Catálogos regulares com páginas de AEM ou proxy | - Nenhuma importação de produto <br>- Modelos genéricos <br>- Dados sob demanda via conector |
| Escalabilidade | - Pode suportar até alguns milhões de produtos (depende do caso de uso) <br> - Armazenamento em cache no Dispatcher | - Sem limitação de volume <br>- Armazenamento em cache no Dispatcher ou CDN |
| Modelo de dados padronizado | Não | Sim, esquema Adobe Commerce GraphQL |
| Disponibilidade | Sim:<br> - SAP Commerce Cloud (Extensão atualizada para oferecer suporte ao AEM 6.4 e Hybris 5 (padrão) e mantém compatibilidade com Hybris 4 <br>- Salesforce Commerce Cloud (Conector de software aberto para suporte ao AEM 6.4) | Sim por meio do código aberto via GitHub. <br> Adobe Commerce (Suporta 2.3.2 (padrão) e compatível com 2.3.1). |
| Quando usar | Casos de uso limitados: Para cenários em que catálogos pequenos e estáticos podem precisar ser importados | Solução preferencial na maioria dos casos de uso |


## Implantar Outras Implementações {#deploying-other-implementations}

Para AEM e Adobe Commerce, consulte [Integração do AEM e do Adobe Commerce](/help/commerce/cif/integrating/magento.md) usando o [Estrutura de integração de comércio](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Para obter informações sobre conceitos e como administrar implementações de comércio eletrônico, consulte [Administração de comércio eletrônico](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Para obter informações sobre como estender os recursos de comércio eletrônico, consulte [Desenvolvimento do comércio eletrônico](/help/commerce/cif-classic/developing/ecommerce.md).
