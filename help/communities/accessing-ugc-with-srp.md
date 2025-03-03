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
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Acesso ao UGC com SRP {#accessing-ugc-with-srp}

## Sobre o SRP {#about-srp}

Todos os componentes e recursos do AEM Communities são criados na [estrutura de componente social (SCF)](/help/communities/scf.md), que chama a API SocialResourceProvider para acessar todo o conteúdo gerado pelo usuário (UGC).

Antes de criar um site da comunidade, o [provedor de recursos de armazenamento (SRP)](/help/communities/working-with-srp.md) deve ser configurado para selecionar uma implementação consistente com a [topologia](/help/communities/topologies.md) subjacente. As implementações do SRP são baseadas em três opções de armazenamento:

1. [ASRP](/help/communities/asrp.md) - armazenamento Adobe sob demanda
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## Sobre o armazenamento de UGC {#about-ugc-storage}

O que é importante saber sobre o armazenamento de UGC é que, quando um site é configurado para usar ASRP ou MSRP, o UGC real não será armazenado no [armazenamento de nós](/help/sites-deploying/data-store-config.md) (JCR) do AEM.

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
