---
title: Integração com a Adobe Marketing Cloud
description: Saiba como integrar o Adobe Experience Manager à Adobe Marketing Cloud.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
translation-type: tm+mt
source-git-commit: 4333cfde433d00ddc4cb013b31fe52956791da46
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---


# Integração com o Adobe Marketing Cloud{#integrating-with-the-adobe-marketing-cloud}

O [Adobe Marketing Cloud](https://www.adobe.com/solutions/digital-marketing.html) inclui poderosos produtos de análise da Web e otimização de sites que fornecem informações e dados acionáveis em tempo real para impulsionar iniciativas online bem-sucedidas. Ele oferta uma plataforma integrada e aberta para otimização de negócios online. A Cloud consiste em aplicativos integrados para coletar e liberar o poder do insight do cliente para otimizar os esforços de aquisição, conversão e retenção do cliente, bem como a criação e distribuição de conteúdo.

Com a Adobe Experience Manager (AEM), você pode se integrar perfeitamente aos seguintes produtos da Adobe Marketing Cloud:

* A Adobe Analytics fornece aos comerciantes inteligência acionável e em tempo real sobre estratégias online e iniciativas de marketing.
* A Adobe Target oferece aos comerciantes a capacidade de tornar continuamente o conteúdo online mais relevante para os seus clientes. resultando em maior conversão.
* O Adobe Dynamic Media Classic automatiza o gerenciamento de mídia, simplifica a publicação na Web e aprimora as experiências na Web, tudo isso em um ambiente hospedado.
* O Gerenciamento dinâmico de tags do Adobe oferece aos comerciantes ferramentas intuitivas para gerenciar de forma rápida e fácil um número ilimitado de tags de Adobe e de terceiros.
* O Adobe Search &amp; Promote dá aos comerciantes a capacidade de controlar e otimizar os resultados da pesquisa em seus sites.
* A Adobe Campaign permite que você gerencie o conteúdo do delivery de email diretamente no Adobe Experience Manager.

Além disso, você pode [integrar AEM com Creative Cloud](/help/assets/aem-cc-folder-sharing-best-practices.md) e com [serviços de terceiros](/help/sites-administering/third-party-services.md).

## Integração ao Adobe Analytics {#integrating-with-adobe-analytics}

[O Adobe ](https://www.omniture.com/en/products/analytics/sitecatalyst) Analytics é a solução líder do setor que oferece aos profissionais de marketing digital um único lugar para medir, analisar e otimizar dados integrados de todas as iniciativas online em vários canais de marketing. Ele fornece aos comerciantes inteligência acionável e em tempo real de análise da Web sobre estratégias digitais e iniciativas de marketing. A Adobe Analytics ajuda os profissionais de marketing a identificar rapidamente os caminhos mais lucrativos por meio de um site, segmentar o tráfego para detectar visitantes da Web de alto valor, determinar onde os visitantes estão navegando para fora do site e identificar métricas de sucesso essenciais para campanhas de marketing online.

Você pode usar o Adobe Analytics para analisar dados de seus sites.

A integração com a Adobe Analytics permite fazer o seguinte:

* Ative o rastreamento de usuários do Analytics.
* Mapeie os modos de execução (por exemplo, autor, publicação) para conjuntos de relatórios diferentes.
* Enviar variáveis de contexto do cliente como variáveis de conversão ou propriedades de tráfego.
* Use mapeamentos de variável predefinidos.
* Configure as seções completas do site de uma só vez.
* Rastrear eventos definidos por personalização.

Para obter informações sobre a integração de AEM com o Analytics, consulte [Integração com o Adobe Analytics](/help/sites-administering/adobeanalytics.md).

Você também pode usar o [Assistente de aceitação](/help/sites-administering/opt-in.md) para executar facilmente a integração.

## Integração com o Adobe Target {#integrating-with-adobe-target}

[Adobe ](https://www.omniture.com/en/products/conversion/test-and-target) Metas usadas pelos profissionais de marketing para projetar e executar testes online, criar segmentos de audiência imediatamente (com base no comportamento) e automatizar a definição de metas de conteúdo e experiências online.

Os consumidores online de hoje têm necessidades em constante evolução e esperam conteúdo relevante, até mesmo personalizado, da grande variedade de sites e fontes de conteúdo que eles podem escolher. Para participar de uma audiência on-line, é fundamental que os profissionais de marketing on-line identifiquem rapidamente quais ofertas e conteúdo são relevantes e atraentes para suas audiências. Munidos desse conhecimento, os profissionais de marketing precisam da capacidade de evoluir continuamente seus sites e público alvo o conteúdo apropriado para diferentes audiências.

[Integrar-se ao Adobe ](/help/sites-administering/target.md) Target explica como integrar seu site ao Público alvo.

Você também pode usar o [Assistente de aceitação](/help/sites-administering/opt-in.md) para executar facilmente a integração.

## opt in ao Analytics e Público alvo {#opting-in-to-analytics-and-target}

AEM oferece um procedimento de aceitação simples para integração com a Adobe Analytics e a Adobe Target. Ao fazer logon como administrador e visitar o console Projetos, você receberá um assistente de aceitação.

![chlimage_1-107](assets/chlimage_1-107a.png)

Opte pela integração com o Analytics e/ou o Público alvo para permitir o uso de seus recursos de rastreamento de página e análise, além de recursos de personalização. Ao opt in, é necessário fornecer as informações de sua conta de usuário e especificar as páginas que são rastreadas.

Para obter mais informações, consulte [Optar pelo Adobe Analytics e Adobe Target.](/help/sites-administering/opt-in.md)

## Integração com o Adobe Dynamic Media Classic {#integrating-with-scene}

O Adobe Dynamic Media Classic é uma solução hospedada para publicar, gerenciar, aprimorar e fornecer ativos de marketing dinâmicos e merchandising visual avançado para Web, dispositivos móveis, email, mídia social, telas conectadas à Internet e impressão.

No Adobe Experience Manager, você pode publicar ativos digitais diretamente do Adobe Experience Manager para o Dynamic Media Classic e pode publicar ativos digitais do Dynamic Media Classic para o Adobe Experience Manager.

Além disso, você pode visualização ativos do Adobe Experience Manager publicados no Dynamic Media Classic em vários visualizadores, como Zoom básico e Vídeo.

Para obter mais informações sobre como o Adobe Experience Manager se integra ao Dynamic Media Classic, consulte a documentação [Integração com o Dynamic Media Classic](/help/sites-administering/scene7.md).

## Integração com o Gerenciamento dinâmico de tags do Adobe {#integrating-with-adobe-dynamic-tag-management}

[O Gerenciamento dinâmico de tags do Adobe ](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) oferece aos comerciantes ferramentas intuitivas para gerenciar com rapidez e facilidade um número ilimitado de tags de Adobe e de terceiros. Você terá mais controle e flexibilidade para otimizar praticamente tudo online, tudo isso enquanto reduz a dependência dos recursos de TI.

[Integre o Gerenciamento dinâmico de ](/help/sites-administering/dtm.md) tags do Adobe ao AEM para que você possa usar as propriedades da Web do Gerenciamento dinâmico de tags para rastrear AEM sites.

## Integração com o Adobe Audience Manager {#integrating-with-adobe-audience-manager}

A integração com o Audience Manager foi removida no AEM 6.3.

## Integração com o Search &amp; Promote {#integrating-with-search-promote}

O Search &amp; Promote Adobe permite que os profissionais de marketing otimizem como visitantes navegam, encontram, comparam e selecionam produtos e conteúdo relevantes em sites da Web e móveis. As empresas podem promover facilmente itens prioritários com base em objetivos de negócios e intenção de visitante, bem como automatizar a comercialização e a atividade de promoções por meio de métricas ou acionadores baseados em KPI.

O Adobe Search &amp; Promote é um aplicativo de pesquisa de site hospedado confiável e dimensionável, capaz de dimensionar para milhões de páginas ou produtos, para negócios online altamente visitados, que vão de varejo a sites de notícias. Ele oferta níveis sem precedentes de controle do comerciante e relevância baseada em métricas.

Para obter informações sobre a integração de AEM e Search &amp; Promote, consulte [Integração com Adobe Search &amp; Promote](/help/sites-administering/search-and-promote.md).

## Integração com o Adobe Campaign {#integrating-with-adobe-campaign}

[O Adobe ](https://www.adobe.com/solutions/campaign-management.html) Campaignpermite gerenciar o conteúdo de delivery de email diretamente no Adobe Experience Manager.

Para obter informações sobre como AEM se integra ao Adobe Campaign, consulte [Integração com o Adobe Campaign](/help/sites-administering/campaignstandard.md).

## Integração com o Livefyre {#integrating-with-livefyre}

Saiba mais sobre AEM e Livefyre:

* [Introdução ao Livefyre](https://answers.livefyre.com/developers/getting-started)

* [Livefyre e AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)

