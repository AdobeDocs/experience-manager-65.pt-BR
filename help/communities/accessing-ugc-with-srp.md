---
title: Acessar UGC com SRP
seo-title: Acessar UGC com SRP
description: Quando um site é configurado para usar ASRP ou MSRP, o UGC real não é armazenado AEM armazenamento de nós (JCR)
seo-description: Quando um site é configurado para usar ASRP ou MSRP, o UGC real não é armazenado AEM armazenamento de nós (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Acessar UGC com SRP {#accessing-ugc-with-srp}

## Sobre SRP {#about-srp}

Todos os componentes e recursos do AEM Communities são criados na [estrutura de componentes sociais (SCF)](/help/communities/scf.md), que chama a API SocialResourceProvider para acessar todo o conteúdo gerado pelo usuário (UGC).

Antes de um site da comunidade ser criado, o [provedor de recursos do armazenamento (SRP)](/help/communities/working-with-srp.md) deve ser configurado para selecionar uma implementação consistente com a [topologia](/help/communities/topologies.md) subjacente. As implementações SRP são baseadas em três opções de armazenamento:

1. [ASRP](/help/communities/asrp.md)  - armazenamento por demanda Adobe
1. [MSRP](/help/communities/msrp.md)  - MongoDB
1. [JSRP](/help/communities/jsrp.md)  - JCR

## Sobre o Armazenamento UGC {#about-ugc-storage}

O que é importante saber sobre o armazenamento do UGC é que, quando um site é configurado para usar o ASRP ou o MSRP, o UGC real não é armazenado AEM [armazenamento de nó](/help/sites-deploying/data-store-config.md) (JCR).

Embora possa haver nós no JCR que sombream o UGC para fornecer metadados úteis, esses nós não devem ser confundidos com o UGC real.

Consulte [Visão Geral do Fornecedor de Recursos de Armazenamento.](/help/communities/srp.md)

## Prática recomendada {#best-practice}

Ao desenvolver componentes personalizados, os desenvolvedores devem tomar cuidado para codificar independentemente da topologia atual escolhida, mantendo assim a flexibilidade para migrar para uma nova topologia no futuro.

### Considere que o JCR não está disponível {#assume-jcr-not-available}

Devem ser evitados métodos específicos para o JCR.

Métodos para usar :

* Sling API (Sling Resource)

   * não suponha que haja nós JCR

* Eventos OSGi

   * não suponha que haja eventos JCR

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

Métodos para evitar :

* API de nó
* Eventos JCR
* iniciadores de fluxo de trabalho (que usam eventos JCR)

### Usar coleções de pesquisa {#use-search-collections}

Diferentes SRPs podem ter diferentes idiomas de query nativos. É recomendável usar métodos do pacote [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) para executar a linguagem de query apropriada.

Para obter mais informações, consulte [Search Essentials](/help/communities/search-implementation.md).

## Recursos {#resources}

* [Armazenamento](/help/communities/working-with-srp.md)  de conteúdo da comunidade - discute as opções de SRP disponíveis para uma loja comum UGC
* [Visão geral](/help/communities/srp.md)  do provedor de recursos do armazenamento - introdução e visão geral do uso do repositório
* [SRP e UGC Essentials](/help/communities/srp-and-ugc.md)  - métodos e exemplos de utilitários SRP
* [Search Essentials](/help/communities/search-implementation.md)  - informações essenciais para a pesquisa no UGC
* [Refatoração](/help/communities/socialutils.md)  do SocialUtils - mapeamento de métodos de utilitário obsoletos para os métodos atuais do utilitário SRP

