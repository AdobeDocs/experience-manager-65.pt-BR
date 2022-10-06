---
title: armadilhas de código
seo-title: Code pitfalls
description: Problemas comuns de codificação a serem evitados ao desenvolver para AEM
seo-description: Common coding pitfalls to avoid when developing for AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# armadilhas de código{#code-pitfalls}

## Evite vínculos Sling no código Java {#avoid-sling-bindings-in-java-code}

Os Sling Bindings são uma maneira inadequada de obter acesso a um serviço em 90% dos casos. Em vez disso, você deve usar *@Reference* ou *@Inject* anotações.

## Evite Thread.interrupt no código Java {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* O é perigoso porque pode fechar arquivos, incluindo arquivos Lucene e arquivos de cache persistentes, quando chamados no momento errado.

## Evite misturar a sincronização Java com ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Isso pode levar a uma condição de corrida na qual o código eventualmente ficará bloqueado.
