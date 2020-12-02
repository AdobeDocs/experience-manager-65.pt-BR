---
title: Armadilhas de código
seo-title: Armadilhas de código
description: armadilhas comuns de codificação a serem evitadas ao desenvolver para AEM
seo-description: armadilhas comuns de codificação a serem evitadas ao desenvolver para AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# Armadilhas de código{#code-pitfalls}

## Evite vincular no código Java {#avoid-sling-bindings-in-java-code}

Vinculações Sling são uma forma inadequada de obter acesso a um serviço em 90% dos casos. Em vez disso, você deve usar as anotações *@Reference* ou *@Inject*.

## Evite Thread.interrupt no código Java {#avoid-thread-interrupt-in-java-code}

*Thread.* interruptions é perigoso porque pode fechar arquivos, incluindo arquivos Lucene e arquivos de cache persistente, quando chamados no momento errado.

## Evite misturar sincronização do Java com ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}

Isso pode levar a uma condição de raça na qual o código eventualmente ficará bloqueado.
