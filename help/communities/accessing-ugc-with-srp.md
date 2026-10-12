---
title: Acesso ao UGC com SRP
description: Quando um site é configurado para usar ASRP ou MSRP, o UGC real não é armazenado no armazenamento de nós do AEM (JCR)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%
---
# Acesso ao UGC com SRP {#accessing-ugc-with-srp}

## Sobre o SRP {#about-srp}

Todos os componentes e recursos do AEM Communities são criados na [estrutura de componente social (SCF)](/help/communities/scf.md), que chama a API SocialResourceProvider para acessar todo o conteúdo gerado pelo usuário (UGC).

Antes de criar um site da comunidade, o [provedor de recursos de armazenamento (SRP)](/help/communities/working-with-srp.md) deve ser configurado para selecionar uma implementação consistente com a [topologia](/help/communities/topologies.md) subjacente. As implementações do SRP são baseadas em três opções de armazenamento:

1. [ASRP](/help/communities/asrp.md) - armazenamento sob demanda do Adobe
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Sobre o armazenamento de UGC {#about-ugc-storage}

O que é importante saber sobre o armazenamento de UGC é que, quando um site é configurado para usar ASRP ou MSRP, o UGC real não será armazenado no [armazenamento de nós](/help/sites-deploying/data-store-config.md) (JCR) da AEM.

Embora possa haver nós no JCR que fazem sombra do UGC para fornecer metadados úteis, esses nós não devem ser confundidos com o UGC real.

Consulte [Visão Geral do Provedor de Recursos de Armazenamento.](/help/communities/srp.md)

## Prática recomendada {#best-practice}

Ao desenvolver componentes personalizados, os desenvolvedores devem ter cuidado com o código independentemente da topologia escolhida no momento, mantendo assim a flexibilidade para mudar para uma nova topologia no futuro.

### Assumir JCR não disponível {#assume-jcr-not-available}

Métodos específicos para JCR devem ser evitados.

Métodos a utilizar :

* API Sling (recurso Sling)

  * não suponha que haja nós JCR

* Eventos OSGi

  * não suponha que haja eventos JCR

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [Utilitários SCFU](/help/communities/socialutils.md#scfutilities-package)

Métodos a evitar:

* API de nó
* Eventos JCR
* inicializadores de fluxo de trabalho (que usam eventos JCR)

### Usar coleções de pesquisa {#use-search-collections}

Diferentes SRPs podem ter diferentes idiomas de consulta nativos. Use métodos do pacote [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) para executar o idioma de consulta apropriado.

Para obter mais informações, consulte [Search Essentials](/help/communities/search-implementation.md).

## Recursos {#resources}

* [Armazenamento do Conteúdo da Comunidade](/help/communities/working-with-srp.md) - discute as opções de SRP disponíveis para um armazenamento comum de UGC
* [Visão Geral do Provedor de Recursos de Armazenamento](/help/communities/srp.md) - introdução e visão geral do uso do repositório
* [Fundamentos do SRP e do UGC](/help/communities/srp-and-ugc.md) - Métodos e exemplos do utilitário SRP
* [Search Essentials](/help/communities/search-implementation.md) - informações essenciais para pesquisar UGC
* [Refatoração de SocialUtils](/help/communities/socialutils.md) - mapeando métodos de utilitário obsoletos para métodos de utilitário SRP atuais
