---
title: Integração com a Adobe Experience Cloud
description: Saiba como integrar o Adobe Experience Manager com o Adobe Experience Cloud.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: a51a863a4edf7e8b951a8361c5c7f0517b09f12a
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 4%

---

# Integração com a Adobe Experience Cloud{#integrating-with-the-adobe-marketing-cloud}

O [Adobe Experience Cloud](https://business.adobe.com/products/marketing-cloud/main.html)O , inclui análises da Web eficientes e produtos de otimização de sites que fornecem dados acionáveis e em tempo real e insights para impulsionar iniciativas online bem-sucedidas. Ele oferece uma plataforma integrada e aberta para otimização de negócios online. A nuvem consiste em aplicativos integrados para coletar e liberar o poder do insight do cliente para otimizar os esforços de aquisição, conversão e retenção do cliente, bem como a criação e distribuição de conteúdo.

Com o Adobe Experience Manager (AEM), você pode integrar-se perfeitamente aos seguintes produtos da Adobe Experience Cloud:

* O Adobe Analytics fornece aos profissionais de marketing inteligência acionável em tempo real sobre estratégias online e iniciativas de marketing.
* A Adobe Target oferece aos profissionais de marketing a capacidade de tornar o conteúdo online continuamente mais relevante para seus clientes — gerando uma conversão maior.
* O Adobe Dynamic Media Classic automatiza o gerenciamento de mídia, simplifica a publicação da Web e aprimora as experiências da Web, tudo isso em um ambiente hospedado.
* O Adobe Dynamic Tag Management oferece aos profissionais de marketing ferramentas intuitivas para gerenciar com rapidez e facilidade um número ilimitado de tags de Adobe e de terceiros.
<!-- Search&Promote is end of life as of September 1, 2022 * Adobe Search&Promote gives marketers the ability to control and optimize the search results on their sites. -->
* O Adobe Campaign permite gerenciar o conteúdo de delivery de email diretamente no Adobe Experience Manager.

Além disso, você pode [integrar AEM com Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) e com [serviços de terceiros](/help/sites-administering/third-party-services.md).

## Integração ao Adobe Analytics {#integrating-with-adobe-analytics}

[Adobe Analytics](https://business.adobe.com/products/analytics/adobe-analytics.html) O é a solução líder do setor que fornece aos profissionais de marketing digital um único local para medir, analisar e otimizar dados integrados de todas as iniciativas online em vários canais de marketing. Ele fornece aos profissionais de marketing informações de análise da Web acionáveis e em tempo real sobre estratégias digitais e iniciativas de marketing. O Adobe Analytics ajuda os profissionais de marketing a identificar rapidamente os caminhos mais rentáveis por meio de um site, segmentar o tráfego para detectar visitantes de alto valor na Web, determinar onde os visitantes estão indo para fora do site e identificar métricas de sucesso críticas para campanhas de marketing online.

Você pode usar o Adobe Analytics para analisar dados de seus sites.

A integração com o Adobe Analytics permite fazer o seguinte:

* Ative o rastreamento de usuários do Analytics.
* Mapeie seus modos de execução (por exemplo, autor, publicar) para conjuntos de relatórios diferentes.
* Enviar variáveis de contexto do cliente como variáveis de conversão ou propriedades de tráfego.
* Use mapeamentos de variável predefinidos.
* Configure seções completas do site de uma só vez.
* Rastreie eventos definidos por personalização.

Para obter informações sobre a integração de AEM com o Analytics, consulte [Integração com o Adobe Analytics](/help/sites-administering/adobeanalytics.md).

Também é possível usar a variável [Assistente de opt-in](/help/sites-administering/opt-in.md) para realizar facilmente a integração.

## Integração com o Adobe Target {#integrating-with-adobe-target}

[O Adobe Target é usado pelos profissionais de marketing para projetar e executar testes online, criar segmentos de público instantaneamente (com base no comportamento) e automatizar o direcionamento de conteúdo e experiências online.](https://business.adobe.com/products/target/adobe-target.html)

Os consumidores online hoje têm necessidades constantemente crescentes e esperam conteúdo relevante, até mesmo personalizado, da grande variedade de sites e fontes de conteúdo que podem escolher. Para engajar um público-alvo online, é fundamental que os profissionais de marketing online identifiquem rapidamente quais ofertas e conteúdo são relevantes e atraentes para seus públicos-alvo. Munidos desse conhecimento, os profissionais de marketing precisam da capacidade de desenvolver continuamente seus sites e direcionar o conteúdo apropriado para diferentes públicos-alvo.

[Integração com o Adobe Target](/help/sites-administering/target.md) explica como integrar seu site com o Target.

Também é possível usar a variável [Assistente de opt-in](/help/sites-administering/opt-in.md) para realizar facilmente a integração.

## Aceitação no Analytics e no Target {#opting-in-to-analytics-and-target}

O AEM oferece um procedimento de aceitação simples para integrar com o Adobe Analytics e o Adobe Target. Ao fazer logon como administrador e visitar o console Projetos , você verá um assistente de aceitação.

![chlimage_1-107](assets/chlimage_1-107a.png)

Opte pela integração com o Analytics e/ou Target para permitir o uso de seus recursos de rastreamento e análise de página e recursos de personalização. Ao aceitar, forneça as informações da conta de usuário e especifique as páginas que são rastreadas.

Para obter mais informações, consulte [Aceitação no Adobe Analytics e Adobe Target.](/help/sites-administering/opt-in.md)

## Integração com o Adobe Dynamic Media Classic {#integrating-with-scene}

O Adobe Dynamic Media Classic é uma solução hospedada para publicar, gerenciar, aprimorar e fornecer ativos de marketing dinâmico e merchandising visual avançado para Web, dispositivos móveis, email, redes sociais, telas conectadas à Internet e impressão.

No Adobe Experience Manager, é possível publicar ativos digitais diretamente do Adobe Experience Manager para o Dynamic Media Classic e publicar ativos digitais do Dynamic Media Classic para o Adobe Experience Manager.

Além disso, é possível visualizar ativos do Adobe Experience Manager publicados no Dynamic Media Classic em vários visualizadores, como Zoom básico e Vídeo.

Para obter mais informações sobre como o Adobe Experience Manager se integra ao Dynamic Media Classic, consulte o [Integração com o Dynamic Media Classic](/help/sites-administering/scene7.md) documentação.

## Integração com o Adobe Dynamic Tag Management {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag Management](https://business.adobe.com/products/experience-platform/adobe-experience-platform.html) O oferece aos profissionais de marketing ferramentas intuitivas para gerenciar com rapidez e facilidade um número ilimitado de tags de Adobe e de terceiros. Você tem mais controle e flexibilidade para otimizar praticamente qualquer coisa online, reduzindo ao mesmo tempo a dependência dos recursos de TI.

[Integrar Adobe Dynamic Tag Management](/help/sites-administering/dtm.md) com o AEM para que você possa usar suas propriedades da Web do Dynamic Tag Management para rastrear AEM sites.

## Integração com o Adobe Audience Manager {#integrating-with-adobe-audience-manager}

A integração do Audience Manager foi removida no AEM 6.3.

<!-- Search&Promote is end of life as of September 1, 2022 ## Integrating with Search&Promote {#integrating-with-search-promote} -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote enables marketers to optimizehow visitors browse, find, compare, and select relevant products and content on web and mobile sites. Businesses can easily promote priority items based on business objectives and visitor intent, as well as automate merchandising and promotions activity via KPI-based triggers or metrics. -->

<!-- Search&Promote is end of life as of September 1, 2022 Adobe Search&Promote is a reliable and scalable hosted site search application, capable of scaling to millions of pages or products, for heavily visited online businesses ranging from retail to news sites. It offers unprecedented levels of marketer control and metrics-based relevance. -->

<!-- Search&Promote is end of life as of September 1, 2022 For information about integrating AEM and Search&Promote, see [Integrating with Adobe Search&Promote](/help/sites-administering/search-and-promote.md). -->

## Integração ao Adobe Campaign {#integrating-with-adobe-campaign}

[Adobe Campaign](https://business.adobe.com/products/campaign/adobe-campaign.html) permite gerenciar conteúdo de delivery de email diretamente no Adobe Experience Manager.

Para obter informações sobre como o AEM se integra ao Adobe Campaign, consulte [Integração com o Adobe Campaign](/help/sites-administering/campaignstandard.md).