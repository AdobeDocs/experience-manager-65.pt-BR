---
title: Campaign Management
seo-title: Campaign Management
description: O gerenciamento de campanhas oferece aos profissionais de marketing digital a oportunidade de fornecer conteúdo personalizado e, assim, criar experiências dedicadas para os visitantes. Ele permite que você orquestre suas campanhas de marketing na Web, no email e nos serviços móveis e, assim, envolva seus visitantes.
seo-description: Campaign management provides digital marketers the opportunity to deliver personalized content and so create dedicated experiences for visitors. It allows you to orchestrate your marketing campaigns across the web, email and mobile services and so engage your visitors.
uuid: 202d614b-a607-45de-8c24-1ee66b230315
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: e8b70971-4f23-45f8-8c23-e147413243c2
exl-id: d1741525-a475-4a76-bd16-55318023495e
source-git-commit: 1ba34f95cf3ce3f136482075802d2e4372f28917
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 1%

---


# Campaign Management{#campaign-management}

O gerenciamento de campanhas oferece aos profissionais de marketing digital a oportunidade de fornecer conteúdo personalizado e, assim, criar experiências dedicadas para os visitantes.

Ele permite que você orquestre suas campanhas de marketing na Web, no email e nos serviços móveis e, assim, envolva seus visitantes. Você pode criar conteúdo, segmentar visitantes, enviar e promover conteúdo direcionado para perfis de usuário específicos e gerenciar campanhas em vários canais.

Este documento descreve os vários elementos que compõem as campanhas. Informações mais detalhadas estão disponíveis nos seguintes documentos:

* [Teasers e estratégias](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [Marketing por email](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [Landing Pages](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Ofertas do Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Trabalhar com o gerente de campanha de marketing](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [Noções sobre segmentação](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [Configuração da campanha](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

O gerenciamento de campanhas é composto de vários elementos:

* **Marcas**
No AEM, as marcas são a unidade de nível superior e formam uma coleção de **Campanhas**.

* **Campanhas**
Uma campanha é uma coleção de dados **Experiências**.

* **Experiências**
O conteúdo focado forma as várias experiências, apresentadas ao visitante no **Pontos de contato**. Há vários tipos de experiência disponíveis:

   * **Teasers**
     [Páginas/parágrafos do teaser](#teasers) são usados para orientar visitantes específicos **Segmentos** conteúdo focado nos interesses deles.

     As páginas de teaser podem:

      * apresentar uma variedade de opções para o visitante escolher
      * mostrar apenas um parágrafo de teaser que seja baseado no segmento de visitante específico; por exemplo, o parágrafo de teaser mostrado pode ser dependente da idade do visitante.

     Normalmente, uma página de teaser é uma ação temporária que durará um período específico, até ser substituída pela próxima página de teaser.

   * **Boletins informativos**

     [Comunicações por e-mail](#emailmarketing) são usados para engajar os usuários e incentivá-los a visitar seu site. Normalmente, assumem a forma de um boletim informativo, enviado para o **Clientes potenciais** (que normalmente são agrupados em **Listas**). **Nota:** A Adobe não planeja aprimorar ainda mais esse recurso. A recomendação é [aproveitar o Adobe Campaign e a integração com o AEM](/help/sites-administering/campaign.md).

   * **Adobe Target**

     Isso permite a integração com o Adobe Target (antigo Test&amp;Target), que fornece aos profissionais de marketing uma ferramenta de otimização para a conversão de sites com os recursos necessários para tornar o conteúdo online mais relevante aos clientes, gerando uma conversão maior. O Adobe Target fornece uma interface intuitiva para projetar e executar testes, criar segmentos de público-alvo e direcionar conteúdo, tudo a partir de um único aplicativo.

* **Touchpoints**

  Esses são os pontos de contato entre o visitante e sua campanha. Os pontos de contato são conectados às experiências criadas por você.

  Por exemplo, para teasers, é a página de conteúdo na qual o parágrafo de teaser está localizado; para um boletim informativo, é a lista de mala direta.

* **Clientes em potencial**

  As informações que você coletou sobre seus visitantes e como contatá-los formam a base para seus leads. **Nota:** A Adobe não planeja aprimorar ainda mais esse recurso.

  A recomendação é [aproveitar o Adobe Campaign e a integração com o AEM](/help/sites-administering/campaign.md).

* **Listas**

  Em geral, os clientes em potencial são agrupados em listas para que seja possível realizar ações coletivas neles. Nota: **Nota:** A Adobe não planeja aprimorar ainda mais esse recurso.

  A recomendação é [aproveitar o Adobe Campaign e a integração com o AEM.](/help/sites-administering/campaign.md)

* **Segmentos**

  Os visitantes do site têm interesses e objetivos diferentes quando chegam a um site. A análise disso de acordo com fatores como atividade no site, informações de perfil registradas e atividade em outros sites ajuda a definir segmentos. O conteúdo pode então ser direcionado especificamente para as necessidades e os interesses do visitante de acordo com os segmentos aos quais ele corresponde.

* **MCM**

  O Gerenciador de campanha de marketing (MCM) é um console que permite acessar toda a funcionalidade necessária para criar e controlar suas campanhas, marcas, experiências, pontos de contato, leads, listas, segmentos e relatórios.

  Ele pode ser acessado de vários locais (rotulados como **Campanhas**) ou com, por exemplo, o URL:

  `http://localhost:4502/libs/mcm/content/admin.html`
