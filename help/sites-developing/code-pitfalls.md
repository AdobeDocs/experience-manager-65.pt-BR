---
title: Armadilhas de código
description: Erros comuns de codificação a serem evitados ao desenvolver para o AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%
---
# Armadilhas de código{#code-pitfalls}

## Evite vinculações Sling no código Java {#avoid-sling-bindings-in-java-code}

Os Vínculos Sling são uma maneira inadequada de obter acesso a um serviço em 90% dos casos. Em vez disso, você deve usar anotações *@Reference* ou *@Inject*.

## Evitar Thread.interrupt no código Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* é perigoso porque pode fechar arquivos, incluindo arquivos Lucene e arquivos de cache persistente, quando chamados na hora errada.

## Evite misturar a sincronização do Java com ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Isso pode levar a uma condição de corrida na qual o código acabará bloqueando.
