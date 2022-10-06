---
title: Convenções de nomenclatura para testes de ativos
seo-title: Naming conventions for assets
description: Os nós no repositório estão sujeitos às convenções de nomenclatura do Java Content Repository. No entanto, o Adobe Experience Manager impõe mais convenções para o nome de nós de ativos.
seo-description: Nodes in the repository are subject to naming conventions of the Java Content Repository. However, Adobe Experience Manager imposes further conventions for the name of asset nodes.
uuid: 6b622a60-90e8-461e-9b67-42c11c7038f9
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 55e66c66-0120-4ed4-94c5-d65a434bb59b
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 88%

---

# Convenções de nomenclatura para ativos teste{#naming-conventions-for-assets-testing}

Os nós no repositório estão sujeitos às convenções de nomenclatura da variável [Repositório de conteúdo Java](/help/sites-developing/the-basics.md#java-content-repository). No entanto, o Adobe Experience Manager impõe mais convenções para o nome de nós de ativos.

## Interface do usuário clássica {#classic-ui}

A interface do usuário clássica impõe restrições mais severas:

* Valida o nome do ativo quando:

   * um título de ativo é fornecido para conversão no nome do nó
   * um nome de nó explícito é fornecido

* Caracteres válidos (somente esses caracteres são válidos quando um ativo é criado na interface do usuário clássica):

   * “a” a “z”
   * “A” a “Z”
   * “0” a “9”
   * _ (sublinhado)
   * `-` (traço/subtração)
