---
title: Visão geral de comércio eletrônico
description: O eCommerce genérico do AEM está disponível como parte da instalação padrão e fornece a funcionalidade completa da estrutura de eCommerce.
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
solution: Experience Manager,Commerce
role: Admin, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%
---
# Visão geral de comércio eletrônico{#ecommerce-overview}

O eCommerce genérico da AEM está disponível como parte de uma instalação padrão e fornece a funcionalidade completa da estrutura de eCommerce.

O Adobe fornece duas versões do Commerce integration framework:

|                         | CIF no local | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versões compatíveis do AEM | AEM no local ou AMS 6.x | AEM AMS 6.4 e 6.5 |
| Back-end | - AEM, Java™ <br> - Integração monolítica, mapeamento de pré-compilação (modelo)<br> - Repositório JCR | - Adobe Commerce <br>- Java e JavaScript <br>- Nenhum dado do Commerce armazenado no repositório JCR |
| Front-end | Páginas renderizadas do lado do servidor do AEM | Aplicativo de página mista (renderização híbrida) |
| Catálogo de produtos | - Importador de produto, editor, armazenamento em cache no AEM <br> - Catálogos regulares com páginas do AEM ou proxy | - Nenhuma importação de produto <br>- Modelos genéricos <br>- Dados sob demanda via conector |
| Escalabilidade | - Pode oferecer suporte a alguns milhões de produtos (depende do caso de uso) <br> - Armazenamento em cache no Dispatcher | - Sem limitação de volume <br> - Armazenamento em cache no Dispatcher ou CDN |
| Modelo de dados padronizado | Não | Sim, esquema do Adobe Commerce GraphQL |
| Disponibilidade | Sim:<br> - SAP Commerce Cloud (Extensão atualizada para oferecer suporte ao AEM 6.4 e Hybris 5 (padrão) e mantém compatibilidade com o Hybris 4 <br>- Salesforce Commerce Cloud (Conector de código aberto para oferecer suporte ao AEM 6.4) | Sim, via código aberto via GitHub. <br> Adobe Commerce (Suporta 2.3.2 (padrão) e compatível com 2.3.1). |
| Quando usar | Casos de uso limitados: para cenários em que pequenos, importe catálogos estáticos conforme necessário | Solução preferida na maioria dos casos de uso |


## Implantar outras implementações {#deploying-other-implementations}

Para AEM e Adobe Commerce, consulte [integração do AEM e do Adobe Commerce](/help/commerce/cif/integrating/magento.md) usando o [Commerce integration framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Para obter informações sobre conceitos e administração de implementações de comércio eletrônico, consulte [Administração de comércio eletrônico](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Para obter informações sobre como estender os recursos de comércio eletrônico, consulte [Desenvolvimento do comércio eletrônico](/help/commerce/cif-classic/developing/ecommerce.md).
