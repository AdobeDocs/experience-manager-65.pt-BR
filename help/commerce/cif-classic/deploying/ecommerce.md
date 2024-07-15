---
title: Visão geral de comércio eletrônico
description: O eCommerce genérico do AEM está disponível como parte da instalação padrão e fornece a funcionalidade completa da estrutura de eCommerce.
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 2%

---

# Visão geral de comércio eletrônico{#ecommerce-overview}

O eCommerce genérico do AEM está disponível como parte de uma instalação padrão e fornece a funcionalidade completa da estrutura de eCommerce.

O Adobe fornece duas versões do Commerce integration framework:

|                         | CIF no local | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| Versões compatíveis do AEM | AEM no local ou AMS 6.x | AEM AMS 6.4 e 6.5 |
| Back-end | - AEM, Java™ <br> - Integração monolítica, mapeamento de pré-compilação (modelo)<br> - Repositório JCR | - Adobe Commerce <br>- Java e JavaScript <br>- Nenhum dado do Commerce armazenado no repositório JCR |
| Front-end | Páginas renderizadas do lado do servidor do AEM | Aplicativo de página mista (renderização híbrida) |
| Catálogo de produtos | - Importador de produto, editor e armazenamento em cache no AEM <br> - Catálogos regulares com páginas de AEM ou proxy | - Nenhuma importação de produto <br>- Modelos genéricos <br>- Dados sob demanda via conector |
| Escalabilidade | - Pode oferecer suporte a alguns milhões de produtos (depende do caso de uso) <br> - Armazenamento em cache no Dispatcher | - Sem limitação de volume <br> - Armazenamento em cache no Dispatcher ou CDN |
| Modelo de dados padronizado | Não | Sim, esquema do Adobe Commerce GraphQL |
| Disponibilidade | Sim:<br> - SAP Commerce Cloud (Extensão atualizada para oferecer suporte a AEM 6.4 e Hybris 5 (padrão) e mantém compatibilidade com Hybris 4 <br>- Salesforce Commerce Cloud (Conector de código aberto para oferecer suporte a AEM 6.4) | Sim, via código aberto via GitHub. <br> Adobe Commerce (Suporta 2.3.2 (padrão) e compatível com 2.3.1). |
| Quando usar | Casos de uso limitados: para cenários em que pequenos, importe catálogos estáticos conforme necessário | Solução preferida na maioria dos casos de uso |


## Implantar outras implementações {#deploying-other-implementations}

Para AEM e Adobe Commerce, consulte [integração de AEM e Adobe Commerce](/help/commerce/cif/integrating/magento.md) usando o [Commerce integration framework](/help/commerce/cif/introduction.md).

>[!NOTE]
>
>Para obter informações sobre conceitos e administração de implementações de comércio eletrônico, consulte [Administração de comércio eletrônico](/help/commerce/cif-classic/administering/ecommerce.md).
>
>Para obter informações sobre como estender os recursos de comércio eletrônico, consulte [Desenvolvimento do comércio eletrônico](/help/commerce/cif-classic/developing/ecommerce.md).
