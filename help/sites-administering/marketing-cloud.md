---
title: Integração com a Adobe Marketing Cloud
description: Saiba como integrar o Adobe Experience Manager com o Adobe Marketing Cloud.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ba518290-dd82-44dc-ae7c-c8152df89179
source-git-commit: d19b203ffe75a5628f350113d4d74a2916beffc8
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---

# Integração com a Adobe Marketing Cloud{#integrating-with-the-adobe-marketing-cloud}

O [Adobe Marketing Cloud](https://www.adobe.com/solutions/digital-marketing.html) inclui análises web eficientes e produtos de otimização de sites que fornecem dados e insights acionáveis e em tempo real para impulsionar iniciativas online bem-sucedidas. Ele oferece uma plataforma integrada e aberta para otimização de negócios online. A nuvem consiste em aplicativos integrados para coletar e liberar o poder do insight do cliente para otimizar os esforços de aquisição, conversão e retenção do cliente, bem como a criação e distribuição de conteúdo.

Com o Adobe Experience Manager (AEM), você pode integrar-se perfeitamente aos seguintes produtos da Adobe Marketing Cloud:

* O Adobe Analytics fornece aos profissionais de marketing inteligência acionável em tempo real sobre estratégias online e iniciativas de marketing.
* A Adobe Target oferece aos profissionais de marketing a capacidade de tornar o conteúdo online continuamente mais relevante para seus clientes — gerando uma conversão maior.
* O Adobe Dynamic Media Classic automatiza o gerenciamento de mídia, simplifica a publicação da Web e aprimora as experiências da Web, tudo em um ambiente hospedado.
* O Adobe Dynamic Tag Management oferece aos profissionais de marketing ferramentas intuitivas para gerenciar de forma rápida e fácil um número ilimitado de tags de Adobe e de terceiros.
* O Adobe Search &amp; Promote fornece aos profissionais de marketing a capacidade de controlar e otimizar os resultados da pesquisa em seus sites.
* O Adobe Campaign permite gerenciar o conteúdo de delivery de email diretamente no Adobe Experience Manager.

Além disso, você pode [integrar AEM com Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) e com [serviços de terceiros](/help/sites-administering/third-party-services.md).

## Integração ao Adobe Analytics {#integrating-with-adobe-analytics}

[O Adobe ](https://www.omniture.com/en/products/analytics/sitecatalyst) Analytics é a solução líder do setor que fornece aos profissionais de marketing digital um único local para medir, analisar e otimizar dados integrados de todas as iniciativas online em vários canais de marketing. Ele fornece aos profissionais de marketing informações de análise da Web acionáveis e em tempo real sobre estratégias digitais e iniciativas de marketing. O Adobe Analytics ajuda os profissionais de marketing a identificar rapidamente os caminhos mais rentáveis por meio de um site, segmentar o tráfego para detectar visitantes de alto valor na Web, determinar onde os visitantes estão indo para fora do site e identificar métricas de sucesso críticas para campanhas de marketing online.

Você pode usar o Adobe Analytics para analisar dados de seus sites.

A integração com o Adobe Analytics permite fazer o seguinte:

* Ative o rastreamento de usuários do Analytics.
* Mapeie seus modos de execução (por exemplo, autor, publicar) para conjuntos de relatórios diferentes.
* Enviar variáveis de contexto do cliente como variáveis de conversão ou propriedades de tráfego.
* Use mapeamentos de variável predefinidos.
* Configure seções completas do site de uma só vez.
* Rastreie eventos definidos por personalização.

Para obter informações sobre a integração de AEM com o Analytics, consulte [Integração com o Adobe Analytics](/help/sites-administering/adobeanalytics.md).

Você também pode usar o [Assistente de Opt-in](/help/sites-administering/opt-in.md) para executar facilmente a integração.

## Integração com o Adobe Target {#integrating-with-adobe-target}

[Adobe ](https://www.omniture.com/en/products/conversion/test-and-target) Metas usadas pelos profissionais de marketing para projetar e executar testes online, criar segmentos de público-alvo instantâneos (com base em comportamento) e automatizar o direcionamento de conteúdo e experiências online.

Os consumidores online hoje têm necessidades constantemente crescentes e esperam conteúdo relevante, até mesmo personalizado, da grande variedade de sites e fontes de conteúdo que podem escolher. Para engajar um público-alvo online, é fundamental que os profissionais de marketing online identifiquem rapidamente quais ofertas e conteúdo são relevantes e atraentes para seus públicos-alvo. Munidos desse conhecimento, os profissionais de marketing precisam da capacidade de desenvolver continuamente seus sites e direcionar o conteúdo apropriado para diferentes públicos-alvo.

[Integração com o Adobe ](/help/sites-administering/target.md) Target explica como integrar seu site com o Target.

Você também pode usar o [Assistente de Opt-in](/help/sites-administering/opt-in.md) para executar facilmente a integração.

## Aceitar o Analytics e o Target {#opting-in-to-analytics-and-target}

O AEM oferece um procedimento de aceitação simples para integrar com o Adobe Analytics e o Adobe Target. Ao fazer logon como administrador e visitar o console Projetos , você verá um assistente de aceitação.

![chlimage_1-107](assets/chlimage_1-107a.png)

Opte pela integração com o Analytics e/ou Target para permitir o uso de seus recursos de rastreamento e análise de página e recursos de personalização. Ao aceitar, você precisa fornecer as informações da conta de usuário e especificar as páginas que são rastreadas.

Para obter mais informações, consulte [Aceitação no Adobe Analytics e Adobe Target.](/help/sites-administering/opt-in.md)

## Integração com o Adobe Dynamic Media Classic {#integrating-with-scene}

O Adobe Dynamic Media Classic é uma solução hospedada para publicar, gerenciar, aprimorar e fornecer ativos de marketing dinâmico e merchandising visual avançado para Web, dispositivos móveis, email, redes sociais, vídeos conectados à Internet e impressão.

No Adobe Experience Manager, você pode publicar ativos digitais diretamente do Adobe Experience Manager para o Dynamic Media Classic e publicar ativos digitais do Dynamic Media Classic para o Adobe Experience Manager.

Além disso, é possível visualizar ativos do Adobe Experience Manager publicados no Dynamic Media Classic em vários visualizadores, como Zoom básico e Vídeo.

Para obter mais informações sobre como o Adobe Experience Manager se integra ao Dynamic Media Classic, consulte a documentação [Integração com o Dynamic Media Classic](/help/sites-administering/scene7.md) .

## Integração com o Adobe Dynamic Tag Management {#integrating-with-adobe-dynamic-tag-management}

[O Adobe Dynamic Tag ](https://www.adobe.com/solutions/digital-marketing/dynamic-tag-management.html) Management fornece aos profissionais de marketing ferramentas intuitivas para gerenciar de modo fácil e rápido um número ilimitado de tags de Adobe e de terceiros. Você terá mais controle e flexibilidade para otimizar praticamente tudo online, reduzindo ao mesmo tempo a dependência dos recursos de TI.

[Integre o Adobe Dynamic Tag ](/help/sites-administering/dtm.md) Management ao AEM para que você possa usar as propriedades da Web do Dynamic Tag Management para rastrear AEM sites.

## Integração com o Adobe Audience Manager {#integrating-with-adobe-audience-manager}

A integração do Audience Manager foi removida no AEM 6.3.

## Integração com o Search &amp; Promote {#integrating-with-search-promote}

O Adobe Search &amp; Promote permite que os profissionais de marketing otimizem como os visitantes navegam, encontram, comparam e selecionam produtos e conteúdo relevantes em sites na web e móveis. As empresas podem promover facilmente itens de prioridade com base em objetivos de negócios e intenção de visitante, bem como automatizar a atividade de comercialização e promoção por meio de métricas ou acionadores baseados em KPI.

O Adobe Search &amp; Promote é um aplicativo de pesquisa de site hospedado confiável e escalável, capaz de dimensionar para milhões de páginas ou produtos, para negócios online altamente visitados, que vão de varejo a sites de notícias. Ele oferece níveis sem precedentes de controle de profissionais de marketing e relevância baseada em métricas.

Para obter informações sobre a integração de AEM e Search &amp; Promote, consulte [Integração com Adobe Search &amp; Promote](/help/sites-administering/search-and-promote.md).

## Integração com o Adobe Campaign {#integrating-with-adobe-campaign}

[O Adobe ](https://www.adobe.com/solutions/campaign-management.html) Campaign permite gerenciar conteúdo de delivery de email diretamente no Adobe Experience Manager.

Para obter informações sobre como o AEM se integra ao Adobe Campaign, consulte [Integração com o Adobe Campaign](/help/sites-administering/campaignstandard.md).

## Integração com o Livefyre {#integrating-with-livefyre}

Saiba mais sobre AEM e Livefyre:

* [Introdução ao Livefyre](https://answers.livefyre.com/developers/getting-started)

* [Livefyre e AEM](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)
