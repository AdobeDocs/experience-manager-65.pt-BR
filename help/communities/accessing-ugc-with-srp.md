---
title: Acesso ao UGC com SRP
seo-title: Accessing UGC with SRP
description: Quando um site é configurado para usar o ASRP ou o MSRP, o UGC real não é armazenado AEM armazenamento de nós (JCR)
seo-description: When a site is configured to use ASRP or MSRP, the actual UGC is not be stored in AEM's node store (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Acesso ao UGC com SRP {#accessing-ugc-with-srp}

## Sobre SRP {#about-srp}

Todos os componentes e recursos do AEM Communities são criados na [quadro de componentes sociais (SCF)](/help/communities/scf.md), que chama a API SocialResourceProvider para acessar todo o conteúdo gerado pelo usuário (UGC).

Antes de criar um site da comunidade, a variável [provedor de recursos de armazenamento (SRP)](/help/communities/working-with-srp.md) deve ser configurado para selecionar uma implementação consistente com o subjacente [topologia](/help/communities/topologies.md). As implementações de SRP são baseadas em três opções de armazenamento :

1. [ASRP](/help/communities/asrp.md) - Adobe on Demand Storage
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Sobre o armazenamento UGC {#about-ugc-storage}

O que é importante saber sobre o armazenamento do UGC é que, quando um site é configurado para usar o ASRP ou o MSRP, o UGC real não é armazenado no AEM [armazenamento de nó](/help/sites-deploying/data-store-config.md) (JCR).

Embora possa haver nós no JCR que somem o UGC para fornecer metadados úteis, esses nós não devem ser confundidos com o UGC real.

Consulte [Visão geral do provedor de recursos de armazenamento.](/help/communities/srp.md)

## Prática recomendada {#best-practice}

Ao desenvolver componentes personalizados, os desenvolvedores devem ter cuidado para codificar independentemente da topologia escolhida atualmente, mantendo assim a flexibilidade para migrar para uma nova topologia no futuro.

### Suponha que o JCR não esteja disponível {#assume-jcr-not-available}

Os métodos específicos do JCR devem ser evitados.

Métodos para usar :

* API Sling (Recurso Sling)

   * não suponha que haja nós JCR

* Eventos OSGi

   * não suponha que haja eventos JCR

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Métodos para evitar :

* API de nó
* Eventos JCR
* inicializadores de fluxo de trabalho (que usam eventos JCR)

### Usar Coleções de Pesquisa {#use-search-collections}

Diferentes SRPs podem ter diferentes linguagens de consulta nativas. É recomendável usar métodos do [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) para executar o idioma de consulta apropriado.

Para obter mais informações, consulte [Fundamentos da pesquisa](/help/communities/search-implementation.md).

## Recursos {#resources}

* [Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md) - discute as opções de SRP disponíveis para uma loja comum UGC
* [Visão geral do provedor de recursos de armazenamento](/help/communities/srp.md) - introdução e visão geral do uso do repositório
* [Princípios básicos de SRP e UGC](/help/communities/srp-and-ugc.md) - Métodos e exemplos de utilitários SRP
* [Fundamentos da pesquisa](/help/communities/search-implementation.md) - informações essenciais para a pesquisa de UGC
* [Refatoração do SocialUtils](/help/communities/socialutils.md) - mapeamento de métodos de utilitário obsoletos para os métodos de utilitário SRP atuais
