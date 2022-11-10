---
title: Receitas do AEM Livefyre
seo-title: AEM Livefyre Recipes
description: Instruções passo a passo sobre casos de uso comuns do Adobe Experience Manager Livefyre.
seo-description: Step-by-step instructions on common use cases for Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
exl-id: 7ccd67a7-9945-48c1-9986-f4eaf0f2b961
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 4%

---

# Receitas do AEM Livefyre{#aem-livefyre-recipes}

Instruções passo a passo sobre casos de uso comuns do Adobe Experience Manager Livefyre.

## Prepare o UGC usando os componentes prontos para uso do Livefyre AEM e a exibição usando o Livefyre Media Wall {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

O Media Wall transmite conteúdo social e nativo do Livefyre em um mural social em tempo real. Há várias maneiras de implementar o Mural de mídia no AEM, dependendo do caso de uso e dos requisitos.

O AEM Pacote Livefyre fornece uma implementação predefinida, enquanto a integração tradicional fornece a capacidade de criar componentes personalizados do AEM Livefyre.

### Integração de AEM {#aem-integration}

O Pacote Livefyre Adobe Experience Manager está disponível para AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 não são compatíveis. Para obter instruções detalhadas, consulte [Integração com o Livefyre](https://helpx.adobe.com/br/experience-manager/6-4/sites/administering/using/livefyre.html).

Para saber quais aplicativos do Livefyre são compatíveis, consulte [Matriz de suporte AEM para aplicativos do Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Implementação tradicional (para componentes de AEM personalizados) {#traditional-implementation-for-customized-aem-components}

Há três maneiras de implementar o Livefyre em um componente de AEM personalizado ou outros CMSs como WordPress, Sitecore ou DemandWare. Uma integração tradicional do Livefyre é agnóstica do CMS.

**Método 1: Implementação do aplicativo Designer**

* **O que:** A maneira mais fácil e rápida de integrar um aplicativo Livefyre. Você pode projetar, configurar e gerar um código incorporado JavaScript personalizado para integrar um Aplicativo de mural de mídia em uma página em minutos.
* **Como:**  [Criar, visualizar, publicar e incorporar um aplicativo de mural de mídia](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **Exemplo:** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**Método 2: Implementação do SDK**

* **O que:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) é a biblioteca principal que alimenta aplicativos e o Auth em um site. Ela define o *window.Livefyre* objeto e um método público único, *Livefyre.require*, que pode ser usada para carregar outras bibliotecas JavaScript do Livefyre que ajudam a incorporar aplicativos do Livefyre e a integrar com plataformas de autenticação de usuário de terceiros.

* **How**: [Use o pacote simplificado do SDK do JavaScript do Livefyre](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **Exemplo**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

Para personalizações avançadas usando o SDK, consulte [SDKs do StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 3: Implementação de API**

* Para criar experiências personalizadas e visualizações de dados, os aplicativos do Livefyre podem ser criados do zero ao consumir o Livefyre e os dados sociais usando o [API de fluxo e do Bootstrap](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Certifique-se de seguir [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand)e [Instagram](https://en.instagram-brand.com/) exiba as diretrizes ao criar a interface do usuário para UGC.

### Integração da autenticação do mural de mídia {#media-wall-authentication-integration}

Para integrações de mural de mídia que exigem autenticação, consulte:

* [Personalizar logon único na integração](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) para AEM Identity Management
* [Integração de identidade](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticação de terceiros

### Visão geral dos casos de uso {#use-case-overview}

Como cliente AEM, desejo preparar o UGC usando os componentes prontos para uso do Livefyre AEM e exibir usando o Livefyre Media Wall:

Etapas para implementar:

1. [Introdução](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Configurar AEM para usar o Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Arraste e solte AEM componente Mural de mídia em sua página](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [Configurar fluxos e adicionar regras para preparar o UGC e exibir o componente Mural de mídia](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html)

Para assistir a vídeos de treinamento no streaming de UGC, consulte [Criar fluxos de conteúdo automático e Pesquisar conteúdo social no Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

### Exemplos de cliente {#customer-examples}

* [Mural de mídia CNN](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [Mural de mídia de turnê PGA](https://www.pgatour.com/social-hub.html)

Para criar experiências personalizadas e visualizações de dados, os aplicativos do Livefyre podem ser criados do zero ao consumir o Livefyre e os dados sociais usando o [API de fluxo e do Bootstrap](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

Para aplicativos Livefyre que exigem autenticação, consulte [Integração de identidade](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticação de terceiros.

* [Mural de mídia de turnê PGA](https://www.pgatour.com/social-hub.html)
* [Tempo limite](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## Integre os comentários do Livefyre usando componentes AEM ou a integração tradicional do Livefyre {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### Integração de AEM {#aem-integration-1}

O Pacote Livefyre Adobe Experience Manager está disponível para AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 não são compatíveis. Para obter instruções detalhadas, consulte [Integração com o Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

### Implementação tradicional (para componentes de AEM personalizados) {#traditional-implementation-for-customized-aem-components-1}

Há três maneiras de implementar o aplicativo Comentários do Livefyre em um componente de AEM personalizado ou outros CMSs como WordPress, Sitecore ou DemandWare. Uma integração tradicional do Livefyre é agnóstica do CMS.

**Método 1: Implementação do aplicativo Designer**

* **O que:** A maneira mais fácil e rápida de integrar um aplicativo Livefyre. Você pode projetar, configurar e gerar um código incorporado JavaScript personalizado para integrar um Aplicativo de mural de mídia em uma página em minutos.
* **Como:** [Criar, visualizar, publicar e incorporar um aplicativo de comentários](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **Exemplo:** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**Método 2: Implementação do SDK**

* **O que:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) é a biblioteca principal que alimenta aplicativos e o Auth em um site. Ela define o *window.Livefyre* objeto e um método público único, *Livefyre.require*, que pode ser usada para carregar outras bibliotecas JavaScript do Livefyre que ajudam a incorporar aplicativos do Livefyre e a integrar com plataformas de autenticação de usuário de terceiros.

* **Como:**

   * Criar uma coleção/aplicativo usando [Token CollectionMeta](https://experienceleague.adobe.com/docs/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html).
   * Integrar [Aplicativo de comentários](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/comments/c-comments-integration.html) em sites que usam a estrutura de código incorporado do Livefyre.js.

* **Exemplo:**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

Para personalizações avançadas usando o SDK, consulte [SDKs do StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 3: Implementação de API**

* Para criar experiências personalizadas e visualizações de dados, os aplicativos do Livefyre podem ser criados do zero ao consumir o Livefyre e os dados sociais usando o [API de fluxo e do Bootstrap](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

### Comentários da integração de autenticação do aplicativo {#comments-app-authentication-integration}

* [Personalizar logon único na integração](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) para AEM Identity Management
* [Integração de identidade](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticação de terceiros

### Exemplos de cliente {#customer-examples-1}

* [Poise (Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Usar a integração do Livefyre AEM Assets para importar o UGC no AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Configuração do Livefyre (para curadoria UGC e Rights Management):**

1. [Configurar fluxos e adicionar regras para preparar o UGC para as pastas da biblioteca de ativos do Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html).

   1. Para assistir a vídeos de treinamento no streaming de UGC, consulte [Criar fluxos de conteúdo automático e Pesquisar conteúdo social no Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Colete, organize e gerencie o UGC com curadoria nas pastas da Biblioteca de ativos do Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/library/assets/c-assets.html).

   1. Para obter vídeos de treinamento sobre como criar e gerenciar pastas na Biblioteca de ativos do Livefyre Studio, consulte [Trabalhe com ativos no Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Direitos de solicitação para UGC preparado usando o Livefyre Studio](https://experienceleague.adobe.com/docs/livefyre/using/rights-requests/c-how-requesting-rights-works.html).

**Configuração de AEM (para importar UGC para AEM Assets):**

1. [Introdução](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Configurar AEM para usar o Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Importar UGC curado pelo Livefyre no AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Turismo Austrália](https://www.australia.com/en-us)

## Integrar revisões do Livefyre usando componentes AEM ou a integração tradicional do Livefyre {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### Integração de AEM {#aem-integration-2}

O Pacote Livefyre Adobe Experience Manager está disponível para AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 não são compatíveis. Para obter instruções detalhadas, consulte [Integração com o Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

O Componente de revisões não é um componente suportado para o AEM 6.1. Verifique a [AEM matriz de suporte para todos os aplicativos Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### Implementação tradicional (para componentes de AEM personalizados) {#traditional-implementation-for-customized-aem-components-2}

Há duas maneiras de implementar o aplicativo Livefyre Reviews em um componente de AEM personalizado ou outros CMSs como WordPress, Sitecore ou DemandWare. Uma integração tradicional do Livefyre é agnóstica do CMS.

**Método 1: Implementação do SDK**

* **O que:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) é a biblioteca principal que alimenta aplicativos e o Auth em um site. Ela define o *window.Livefyre* objeto e um método público único, *Livefyre.require*, que pode ser usada para carregar outras bibliotecas JavaScript do Livefyre que ajudam a incorporar aplicativos do Livefyre e a integrar com plataformas de autenticação de usuário de terceiros.

* **Como:**

   * Criar as revisões [Token CollectionMeta](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) para especificar metadados a serem armazenados na Coleção de Revisões.
   * Integrar [Aplicativo de revisões](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) nos Sites usando o *Livefyre.js* estrutura do código incorporado

* **Exemplo:**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

Para personalizações avançadas usando o SDK, consulte [SDKs do StreamHub](https://github.com/Livefyre/streamhub-sdk).

**Método 2: Implementação de API**

* Para criar experiências personalizadas e visualizações de dados, os aplicativos do Livefyre podem ser criados do zero ao consumir o Livefyre e os dados sociais usando a API de fluxo e o Bootstrap.

É possível encontrar outras APIs de Classificações e Revisões [here](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Comentários da integração de autenticação do aplicativo {#comments-app-authentication-integration-1}

* [Personalizar logon único na integração](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) para AEM Identity Management
* [Integração de identidade](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) para plataformas de autenticação de terceiros

### Exemplos de cliente {#customer-examples-2}

* [Tempo limite](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [myrecipes](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)
