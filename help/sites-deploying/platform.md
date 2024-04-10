---
title: Introdução à plataforma AEM
description: Saiba mais sobre a plataforma AEM e seus componentes mais importantes, incluindo a instalação e implantação do Adobe Experience Manager 6.5, bem como sua arquitetura, incluindo a implantação na nuvem do Adobe Managed Services.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
exl-id: 8ee5f4ff-648d-45ea-a51e-894cd4385e62
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Architect
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 4%

---


# Introdução à plataforma AEM{#introduction-to-the-aem-platform}

A plataforma AEM no AEM 6 é baseada no Apache Jackrabbit Oak.

O Apache Jackrabbit Oak é um esforço para implementar um repositório hierárquico de conteúdo escalável e eficiente para uso como base de sites modernos de classe mundial e outros aplicativos de conteúdo exigentes.

É o sucessor do Jackrabbit 2 e é usado pelo AEM 6 como back-end padrão para seu repositório de conteúdo, o CRX.

## Princípios e objetivos do projeto {#design-principles-and-goals}

O Oak implementa o [JSR-283](https://jcp.org/en/jsr/detail?id=283) (JCR 2.0) Seus principais objetivos de design são:

* Melhor suporte para repositórios grandes
* Vários nós de cluster distribuídos para alta disponibilidade
* Melhor desempenho
* Suporte para muitos nós filhos e níveis de controle de acesso

## Conceito de arquitetura {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### Armazenamento {#storage}

A finalidade da camada de armazenamento é:

* Implementar um modelo de árvore
* Tornar o armazenamento conectável
* Fornecer um mecanismo de clustering

### Oak Core {#oak-core}

O Oak Core adiciona várias camadas à camada de armazenamento:

* Controles de Nível de Acesso
* Pesquisa e indexação
* Observação

### Oak JCR {#oak-jcr}

O principal objetivo do JCR do Oak é transformar a semântica de JCR em operações em árvore. É também responsável por:

* Implementar a API JCR
* Contendo ganchos de confirmação que implementam restrições JCR

Além disso, implementações não-Java agora são possíveis e fazem parte do conceito Oak JCR.

## Visão geral de armazenamento {#storage-overview}

A camada de armazenamento do Oak fornece uma camada de abstração para o armazenamento real do conteúdo.

Atualmente, há duas implementações de armazenamento de dados disponíveis no AEM6: **Armazenamento Tar** e **Armazenamento MongoDB**.

### Armazenamento Tar {#tar-storage}

O armazenamento Tar usa arquivos tar. Ele armazena o conteúdo como vários tipos de registros em segmentos maiores. Os diários são usados para rastrear o estado mais recente do repositório.

Há vários princípios-chave de design que foram criados com base nisso:

* **Segmentos imutáveis**

O conteúdo é armazenado em segmentos que podem ter até 256 KB. Eles são imutáveis, o que facilita o armazenamento em cache de segmentos acessados com frequência e reduz os erros do sistema que podem corromper o repositório.

Cada segmento é identificado por um identificador exclusivo (UUID) e contém um subconjunto contínuo da árvore de conteúdo. Além disso, os segmentos podem fazer referência a outro conteúdo. Cada segmento mantém uma lista de UUIDs de outros segmentos referenciados.

* **Localidade**

Registros relacionados, como um nó e seus secundários imediatos, são armazenados no mesmo segmento. Isso agiliza a pesquisa no repositório e evita a maioria dos erros de cache para clientes típicos que acessam mais de um nó relacionado por sessão.

* **Compactação**

A formatação de registros é otimizada por tamanho para reduzir os custos de E/S e ajustar o máximo de conteúdo em caches possível.

### Armazenamento Mongo {#mongo-storage}

O armazenamento MongoDB usa o MongoDB para fragmentação e clustering. A árvore do repositório é mantida em um banco de dados MongoDB em que cada nó é um documento separado.

Ela tem várias particularidades:

* Revisões

Para cada atualização (confirmação) do conteúdo, uma nova revisão é criada. Uma revisão é basicamente uma string que consiste em três elementos:

1. Um carimbo de data e hora derivado da hora do sistema da máquina em que foi gerado
1. Um contador para distinguir revisões criadas com o mesmo carimbo de data/hora
1. A ID do nó do cluster em que a revisão foi criada

* Marcas

As ramificações são compatíveis, o que permite que o cliente prepare várias alterações e as torne visíveis com uma única chamada de mesclagem.

* Documentos anteriores

O armazenamento MongoDB adiciona dados a um documento com cada modificação. No entanto, ela só excluirá os dados se uma limpeza for acionada explicitamente. Os dados antigos são movidos quando um determinado limite é atingido. Os documentos anteriores contêm apenas dados imutáveis, o que significa que eles contêm apenas revisões confirmadas e mescladas.

* Metadados do nó de cluster

Os dados sobre nós de cluster ativos e inativos são mantidos no banco de dados para facilitar as operações de cluster.

Uma configuração típica de cluster AEM com armazenamento MongoDB:

![chlimage_1-85](assets/chlimage_1-85.png)

## O que é diferente de Jackrabbit 2? {#what-is-different-from-jackrabbit}

Como o Oak é compatível com versões anteriores do JCR 1.0, quase não há alterações no nível do usuário. No entanto, há algumas diferenças notáveis que você deve considerar ao configurar uma instalação do AEM baseada no Oak:

* O Oak não cria índices automaticamente. Dessa forma, os índices personalizados devem ser criados quando necessário.
* Ao contrário do Jackrabbit 2, onde as sessões sempre refletem o estado mais recente do repositório, com o Oak, uma sessão reflete uma visualização estável do repositório desde o momento em que a sessão foi adquirida. O motivo é devido ao modelo MVCC no qual o Oak é baseado.
* Irmãos de mesmo nome (SNS) não são compatíveis com o Oak.

## Outra documentação relacionada à plataforma {#other-platform-related-documentation}

Para obter mais informações sobre a plataforma AEM, consulte também os artigos abaixo:

* [Configuração de armazenamento de nós e armazenamento de dados no AEM 6](/help/sites-deploying/data-store-config.md)
* [Consultas e indexação do Oak](/help/sites-deploying/queries-and-indexing.md)
* [Elementos de armazenamento no AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM com MongoDB](/help/sites-deploying/aem-with-mongodb.md)
