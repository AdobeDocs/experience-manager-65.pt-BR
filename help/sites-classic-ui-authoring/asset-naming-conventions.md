---
title: Convenções de nomenclatura para testes de ativos
description: Os nós no repositório estão sujeitos às convenções de nomenclatura do Repositório de conteúdo Java. No entanto, o Adobe Experience Manager impõe mais convenções para o nome dos nós de ativos.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 1%

---

# Convenções de nomenclatura para testes de ativos{#naming-conventions-for-assets-testing}

Os nós no repositório estão sujeitos às convenções de nomenclatura do [Repositório de conteúdo Java](/help/sites-developing/the-basics.md#java-content-repository). No entanto, o Adobe Experience Manager impõe mais convenções para o nome dos nós de ativos.

## IU Clássica {#classic-ui}

A interface clássica impõe restrições mais rigorosas:

* Valida o nome do ativo quando um nome de nó explícito:

   * um título de ativo é fornecido para conversão no nome do nó
   * um nome de nó explícito é fornecido

* Caracteres válidos (na verdade, somente esses caracteres são válidos quando um ativo é criado na interface clássica):

   * &#39;a&#39; a &#39;z&#39;
   * &#39;A&#39; a &#39;Z&#39;
   * &#39;0&#39; a &#39;9&#39;
   * _ (sublinhado)
   * `-` (traço/sinal de menos)
