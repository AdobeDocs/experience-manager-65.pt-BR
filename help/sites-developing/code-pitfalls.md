---
title: Armadilhas de código
description: Erros comuns de codificação a serem evitados ao desenvolver para AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Armadilhas de código{#code-pitfalls}

## Evite vinculações Sling no código Java {#avoid-sling-bindings-in-java-code}

Os Vínculos Sling são uma maneira inadequada de obter acesso a um serviço em 90% dos casos. Em vez disso, use *@Reference* ou *@Inject* anotações.

## Evitar Thread.interrupt no código Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* é perigoso porque pode fechar arquivos, incluindo arquivos Lucene e arquivos de cache persistentes, quando chamado na hora errada.

## Evite misturar a sincronização do Java com ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Isso pode levar a uma condição de corrida na qual o código acabará bloqueando.
