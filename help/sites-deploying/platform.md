---
title: Introdução à plataforma de AEM
seo-title: Introduction to the AEM Platform
description: Este artigo fornece uma visão geral da plataforma de AEM e seus componentes mais importantes.
seo-description: This article provides a general overview of the AEM platform and its most important components.
uuid: 214d4c49-1f5c-432c-a2c0-c1fbdceee716
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: fccf9a0f-ebab-45ab-8460-84c86b3c4192
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
exl-id: 8ee5f4ff-648d-45ea-a51e-894cd4385e62
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Introdução à plataforma de AEM{#introduction-to-the-aem-platform}

A plataforma AEM no AEM 6 é baseada no Apache Jackrabbit Oak.

O Apache Jackrabbit Oak é um esforço para implementar um repositório de conteúdo hierárquico escalável e de desempenho para ser usado como a base de sites de classe mundial modernos e outros aplicativos de conteúdo exigentes.

Ele é o sucessor do Jackrabbit 2 e é usado pelo AEM 6 como o back-end padrão para seu repositório de conteúdo, o CRX.

## Princípios e objetivos do projeto {#design-principles-and-goals}

O Oak implementa o [JSR-283](https://www.day.com/day/en/products/jcr/jsr-283.html) (JCR 2.0). Os seus principais objetivos de concepção são:

* Melhor suporte para repositórios grandes
* Vários nós de cluster distribuídos para alta disponibilidade
* Melhor desempenho
* Suporte para vários nós secundários e Níveis de Controle de Acesso

## Conceito de arquitetura {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### Armazenamento {#storage}

O objetivo da camada de armazenamento é:

* Implementar um modelo de árvore
* Tornar o armazenamento plugável
* Fornecer um mecanismo de clustering

### Oak Core {#oak-core}

O Oak Core adiciona várias camadas à camada de armazenamento:

* Controles de nível de acesso
* Pesquisa e indexação
* Observação

### Oak JCR {#oak-jcr}

O principal objetivo do JCR do Oak é transformar a semântica do JCR em operações em árvore. É também responsável por:

* Implementar a API JCR
* Contendo ganchos de confirmação que implementam restrições do JCR

Além disso, agora são possíveis implementações que não são Java e fazem parte do conceito JCR do Oak.

## Visão geral do armazenamento {#storage-overview}

A camada de armazenamento do Oak fornece uma camada de abstração para o armazenamento real do conteúdo.

Atualmente, há duas implementações de armazenamento disponíveis no AEM6: **Armazenamento Tar** e **Armazenamento MongoDB**.

### Armazenamento Tar {#tar-storage}

O armazenamento Tar usa arquivos tar. Ele armazena o conteúdo como vários tipos de registros em segmentos maiores. Os diários são usados para rastrear o estado mais recente do repositório.

Há vários princípios-chave de design que ele foi criado em torno:

* **Segmentos imutáveis**

O conteúdo é armazenado em segmentos que podem ter até 256 KiB. Eles são imutáveis, o que facilita o cache de segmentos acessados com frequência e reduz erros do sistema que podem corromper o repositório.

Cada segmento é identificado por um identificador exclusivo (UUID) e contém um subconjunto contínuo da árvore de conteúdo. Além disso, os segmentos podem fazer referência a outro conteúdo. Cada segmento mantém uma lista de UUIDs de outros segmentos referenciados.

* **Localidade**

Os registros relacionados, como um nó e seus filhos imediatos, geralmente são armazenados no mesmo segmento. Isso torna a pesquisa no repositório muito rápida e evita a maioria das falhas de cache para clientes típicos que acessam mais de um nó relacionado por sessão.

* **Compactação**

A formatação de registros é otimizada para tamanho para reduzir custos de E/S e ajustar o máximo conteúdo possível em caches.

### Armazenamento Mongo {#mongo-storage}

O armazenamento MongoDB aproveita o MongoDB para compartilhamento e clustering. A árvore do repositório é mantida em um banco de dados MongoDB, onde cada nó é um documento separado.

Ela tem várias particularidades:

* Revisões

Para cada atualização (confirmação) do conteúdo, uma nova revisão é criada. Uma revisão é basicamente uma string que consiste em três elementos:

1. Um carimbo de data e hora derivado da hora do sistema da máquina em que foi gerado
1. Um contador para distinguir as revisões criadas com o mesmo carimbo de data e hora
1. O ID do nó do cluster em que a revisão foi criada

* Marcas

Há suporte para ramificações, o que permite que o cliente prepare várias alterações e as torne visíveis com uma única chamada de mesclagem.

* Documentos anteriores

O armazenamento MongoDB adiciona dados a um documento com todas as modificações. No entanto, ela só excluirá dados se uma limpeza for explicitamente acionada. Os dados antigos são movidos quando um determinado limite é atingido. Os documentos anteriores contêm apenas dados imutáveis, o que significa que contêm apenas revisões confirmadas e unidas.

* Metadados do nó do cluster

Os dados sobre nós de cluster ativos e inativos são mantidos no banco de dados para facilitar as operações de cluster.

Uma configuração típica de cluster AEM com o armazenamento MongoDB:

![chlimage_1-85](assets/chlimage_1-85.png)

## O que é diferente do Jackrabbit 2? {#what-is-different-from-jackrabbit}

Como o Oak foi projetado para ser compatível com versões anteriores do JCR 1.0 padrão, quase não haverá alterações no nível do usuário. No entanto, há algumas diferenças notáveis que você precisa levar em conta ao configurar uma instalação de AEM baseada no Oak:

* O Oak não cria índices automaticamente. Por causa disso, os índices personalizados precisarão ser criados quando necessário.
* Ao contrário do Jackrabbit 2, onde as sessões sempre refletem o estado mais recente do repositório, com o Oak uma sessão reflete uma exibição estável do repositório a partir do momento em que a sessão foi adquirida. Isso se deve ao modelo MVCC no qual o Oak se baseia.
* Os irmãos com mesmo nome (SNS) não são suportados no Oak.

## Outra documentação relacionada à plataforma {#other-platform-related-documentation}

Para obter mais informações sobre a plataforma de AEM, verifique também os artigos abaixo:

* [Configuração de armazenamento de nós e armazenamento de dados no AEM 6](/help/sites-deploying/data-store-config.md)
* [Consultas e indexação do Oak](/help/sites-deploying/queries-and-indexing.md)
* [Elementos de armazenamento no AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM com MongoDB](/help/sites-deploying/aem-with-mongodb.md)
