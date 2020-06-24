---
title: Receitas do AEM Livefyre
seo-title: Receitas do AEM Livefyre
description: Instruções passo a passo sobre casos de uso frequentes relativos ao Adobe Experience Manager Livefyre.
seo-description: Instruções passo a passo sobre casos de uso frequentes relativos ao Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
translation-type: tm+mt
source-git-commit: 072898f18d418eac8e9d9e94453db34d62dd3ed9
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 2%

---


# Receitas do AEM Livefyre{#aem-livefyre-recipes}

Instruções passo a passo sobre casos de uso frequentes relativos ao Adobe Experience Manager Livefyre.

## Preparar o UGC usando os componentes predefinidos do Livefyre AEM e exibir usando o Livefyre Media Wall {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

O Media Wall transmite conteúdo social e nativo do Livefyre para um mural social em tempo real. Existem várias maneiras de implementar o Media Wall no AEM, dependendo do caso de uso e dos requisitos.

O pacote do AEM Livefyre fornece uma implementação predefinida, enquanto a integração tradicional oferece a capacidade de criar componentes personalizados do Livefyre AEM.

### Integração do AEM {#aem-integration}

O Pacote Livefyre Adobe Experience Manager está disponível para AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 não são compatíveis. Para obter instruções detalhadas, consulte [Integração com o Livefyre](https://helpx.adobe.com/br/experience-manager/6-4/sites/administering/using/livefyre.html).

Para saber quais aplicativos Livefyre são compatíveis, consulte a Matriz de suporte do [AEM para aplicativos](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)Livefyre.

### Implementação tradicional (para componentes personalizados do AEM) {#traditional-implementation-for-customized-aem-components}

Há três maneiras de implementar o Livefyre em um componente AEM personalizado ou em outros CMSs como WordPress, Sitecore ou DemandWare. Uma integração tradicional do Livefyre é agnóstico do CMS.

**Método 1: Implementação do aplicativo Designer**

* **O que:** A maneira mais fácil e rápida de integrar um aplicativo Livefyre. Você pode projetar, configurar e gerar um código incorporado JavaScript personalizado para integrar um aplicativo Media Wall em uma página em minutos.
* **Como:**  [Criar, Pré-visualização, publicar e incorporar um aplicativo Media Wall](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **Exemplo:** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**Método 2: Implementação do SDK**

* **O que:** [O Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) é a biblioteca principal que alimenta o Apps e o Auth em um site. Ele define o objeto global *window.Livefyre* e um único método público, *Livefyre.requirements*, que pode ser usado para carregar outras bibliotecas do Livefyre JavaScript que ajudam a incorporar aplicativos Livefyre e a integrar-se a plataformas de autenticação de usuário de terceiros.

* **Como**: [Use o pacote simplificado do Livefyre JavaScript SDK](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **Exemplo**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

Para personalizações avançadas que usam o SDK, consulte SDKs [do](https://github.com/Livefyre/streamhub-sdk)StreamHub.

**Método 3: Implementação da API**

* Para criar experiências personalizadas e visualizações de dados, os aplicativos Livefyre podem ser criados do zero, consumindo o Livefyre e os dados sociais usando o [Bootstrap e a API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html)de fluxo.

Certifique-se de seguir as diretrizes de exibição do [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand)e [Instagram](https://en.instagram-brand.com/) ao criar a interface para UGC.

### Integração da autenticação do Media Wall {#media-wall-authentication-integration}

Para integrações de mural de mídia que exigem autenticação, consulte:

* [Personalizar a integração](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) de logon único para o AEM Identity Management
* [Integração](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) de identidade para plataformas de autenticação de terceiros

### Visão geral do caso de uso {#use-case-overview}

Como cliente do AEM, desejo preparar o UGC usando os componentes prontos para uso do Livefyre AEM e exibir usando o Livefyre Media Wall:

Etapas para implementar:

1. [Introdução](https://helpx.adobe.com/br/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Configurar o AEM para usar o Livefyre](https://helpx.adobe.com/br/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Arraste e solte o componente Mídia do AEM em sua página](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [Configure os fluxos e adicione regras para preparar o UGC e exibir no componente Media Wall](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html)

Para assistir a vídeos de treinamento em streaming de UGC, consulte [Criar fluxos de conteúdo automático e Pesquisar conteúdo social no Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

### Exemplos de cliente {#customer-examples}

* [CNN Media Wall](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [Mídia de tour PGA](https://www.pgatour.com/social-hub.html)

Para criar experiências personalizadas e visualizações de dados, os aplicativos Livefyre podem ser criados do zero, consumindo o Livefyre e os dados sociais usando o [Bootstrap e a API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html)de fluxo.

Para aplicativos Livefyre que exigem autenticação, consulte Integração [de](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) identidade para plataformas de autenticação de terceiros.

* [Mídia de tour PGA](https://www.pgatour.com/social-hub.html)
* [Tempo limite](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## Integre os comentários do Livefyre usando os componentes do AEM ou a integração tradicional do Livefyre {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### Integração do AEM {#aem-integration-1}

O Pacote Livefyre Adobe Experience Manager está disponível para AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 não são compatíveis. Para obter instruções detalhadas, consulte [Integração com o Livefyre](https://helpx.adobe.com/br/experience-manager/6-4/sites/administering/using/livefyre.html).

### Implementação tradicional (para componentes personalizados do AEM) {#traditional-implementation-for-customized-aem-components-1}

Há três maneiras de implementar o aplicativo Livefyre Comments em um componente AEM personalizado ou em outros CMSs como WordPress, Sitecore ou DemandWare. Uma integração tradicional do Livefyre é agnóstico do CMS.

**Método 1: Implementação do aplicativo Designer**

* **O que:** A maneira mais fácil e rápida de integrar um aplicativo Livefyre. Você pode projetar, configurar e gerar um código incorporado JavaScript personalizado para integrar um aplicativo Media Wall em uma página em minutos.
* **Como:** [Criar, Pré-visualização, publicar e incorporar um aplicativo de comentários](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **Exemplo:** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**Método 2: Implementação do SDK**

* **O que:** [O Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) é a biblioteca principal que alimenta o Apps e o Auth em um site. Ele define o objeto global *window.Livefyre* e um único método público, *Livefyre.requirements*, que pode ser usado para carregar outras bibliotecas do Livefyre JavaScript que ajudam a incorporar aplicativos Livefyre e a integrar-se a plataformas de autenticação de usuário de terceiros.

* **Como:**

   * Crie uma coleção/aplicativo usando o token [](https://docs.adobe.com/content/help/en/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html)CollectionMeta.
   * Integre o aplicativo [](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/comments/c-comments-integration.html) Comments a sites usando a estrutura de código incorporada do Livefyre.js.

* **Exemplo:**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

Para personalizações avançadas usando o SDK, consulte SDKs [do](https://github.com/Livefyre/streamhub-sdk)StreamHub.

**Método 3: Implementação da API**

* Para criar experiências personalizadas e visualizações de dados, os aplicativos Livefyre podem ser criados do zero, consumindo o Livefyre e os dados sociais usando o [Bootstrap e a API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html)de fluxo.

### Integração de autenticação de aplicativos de comentários {#comments-app-authentication-integration}

* [Personalizar a integração](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) de logon único para o AEM Identity Management
* [Integração](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) de identidade para plataformas de autenticação de terceiros

### Exemplos de cliente {#customer-examples-1}

* [Poise (Kimberly Klark)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Use a integração do Livefyre AEM Assets para importar o UGC em AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Configuração do Livefyre (para Curadoria UGC e Gerenciamento de Direitos):**

1. [Configure os fluxos e adicione regras para preparar o UGC às pastas](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html)da biblioteca de ativos do Livefyre.

   1. Para assistir a vídeos de treinamento em streaming de UGC, consulte [Criar fluxos de conteúdo automático e Pesquisar conteúdo social no Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Reúna, organize e gerencie o UGC com curadoria nas pastas](https://docs.adobe.com/content/help/en/livefyre/using/library/assets/c-assets.html)da Biblioteca de ativos do Livefyre.

   1. Para obter vídeos de treinamento sobre como criar e gerenciar pastas na Biblioteca de ativos do Livefyre Studio, consulte [Trabalhar com ativos no Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Solicite direitos para UGC com curadoria usando o Livefyre Studio](https://docs.adobe.com/content/help/en/livefyre/using/rights-requests/c-how-requesting-rights-works.html).

**Configuração do AEM (para importar UGC para AEM Assets):**

1. [Introdução](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Configurar o AEM para usar o Livefyre](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Importar UGC curado pelo Livefyre em AEM Assets](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Turismo Austrália](https://www.australia.com/en-us)

## Integrar revisões do Livefyre usando componentes do AEM ou integração tradicional do Livefyre {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### Integração do AEM {#aem-integration-2}

O Pacote Livefyre Adobe Experience Manager está disponível para AEM 6.1, 6.2SP1, 6.3, 6.4 e 6.4 SP1. AEM 5.x e 6.0 não são compatíveis. Para obter instruções detalhadas, consulte [Integração com o Livefyre](https://helpx.adobe.com/br/experience-manager/6-4/sites/administering/using/livefyre.html).

O Componente de revisões não é um componente compatível com o AEM 6.1. Verifique a matriz de suporte do [AEM para todos os aplicativos](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)Livefyre.

### Implementação tradicional (para componentes personalizados do AEM) {#traditional-implementation-for-customized-aem-components-2}

Há duas maneiras de implementar o aplicativo Livefyre Reviews em um componente AEM personalizado ou outros CMSs como WordPress, Sitecore ou DemandWare. Uma integração tradicional do Livefyre é agnóstico do CMS.

**Método 1: Implementação do SDK**

* **O que:** [O Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) é a biblioteca principal que alimenta o Apps e o Auth em um site. Ele define o objeto global *window.Livefyre* e um único método público, *Livefyre.requirements*, que pode ser usado para carregar outras bibliotecas do Livefyre JavaScript que ajudam a incorporar aplicativos Livefyre e a integrar-se a plataformas de autenticação de usuário de terceiros.

* **Como:**

   * Crie o token [Reviews](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html) CollectionMeta para especificar metadados a serem armazenados na Coleção de revisões.
   * Integre o aplicativo [](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html) Reviews aos sites usando a estrutura de código incorporada do *Livefyre.js*

* **Exemplo:**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

Para personalizações avançadas usando o SDK, consulte SDKs [do](https://github.com/Livefyre/streamhub-sdk)StreamHub.

**Método 2: Implementação da API**

* Para criar experiências personalizadas e visualizações de dados, os aplicativos Livefyre podem ser criados do zero, consumindo o Livefyre e os dados sociais usando a API Bootstrap e Stream.

As APIs de classificações e revisões adicionais podem ser encontradas [aqui](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### Integração de autenticação de aplicativos de comentários {#comments-app-authentication-integration-1}

* [Personalizar a integração](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) de logon único para o AEM Identity Management
* [Integração](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) de identidade para plataformas de autenticação de terceiros

### Exemplos de cliente {#customer-examples-2}

* [Tempo limite](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [minhas receitas](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)

