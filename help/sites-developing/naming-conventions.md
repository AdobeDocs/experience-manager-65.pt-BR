---
title: Convenções de nomenclatura
seo-title: Convenções de nomenclatura
description: Os nós no repositório estão sujeitos às convenções de nomenclatura do Java Content Repository
seo-description: Os nós no repositório estão sujeitos às convenções de nomenclatura do Java Content Repository
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 19%

---


# Nomeando Convenções{#naming-conventions}

Os nós no repositório estão sujeitos às convenções de nomenclatura do [repositório de conteúdo Java](/help/sites-developing/the-basics.md#java-content-repository). No entanto, AEM impõem outras convenções para o nome dos nós de página.

## Convenções de nomenclatura para páginas {#naming-conventions-for-pages}

Essas convenções de nomenclatura são implementadas em vários níveis:

* JcrUtil: a implementação AEM de [utilitários JCR](#jcr-utilities).
* PageManager: o [Page Manager](#page-manager) fornece métodos para operações de nível de página.
* De acordo com a interface que está sendo usada:

   * [Interface de usuário padrão e habilitada para toque](#standard-ui)
   * [Interface clássica](#classic-ui)

### Utilitários JCR {#jcr-utilities}

[O ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) JcrUtilis é a implementação AEM dos utilitários do JCR. De especial interesse para validar nomes são os mapeamentos de caracteres que ele controla e as seguintes validações:

* `isValidName`

   * Verifica se o nome não está vazio e contém apenas caracteres válidos.
   * Pode ser usado para verificar se um nome proposto é válido.

* `createValidName`

   * Isso cria um rótulo válido a partir de uma string arbitrária.
   * Ele pode ser usado para criar um nome a partir de um título.

### Gerenciador de páginas {#page-manager}

[O ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) PageManager fornece métodos para operações de nível de página, com base em  [JCRUtil](#jcr-utilities).

### Interface do usuário padrão {#standard-ui}

A interface de usuário padrão e habilitada para toque:

* Valida o nome de acordo com as restrições impostas pelo PageManager quando:

   * um título de página é fornecido para conversão no nome do nó
   * um nome de nó explícito é fornecido

### Interface clássica {#classic-ui}

A interface do usuário clássica impõe restrições mais severas:

* Valida o nome quando um nome de nó explícito é exibido quando:

   * um título de página é fornecido para conversão no nome do nó
   * um nome de nó explícito é fornecido

* Caracteres válidos (somente esses caracteres são válidos quando uma página é criada na interface clássica, mesmo que `PageManagerImpl` permita caracteres adicionais):

   * “a” a “z”
   * “A” a “Z”
   * “0” a “9”
   * _ (sublinhado)
   * `-` (traço/subtração)

