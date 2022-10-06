---
title: Convenções de nomenclatura
seo-title: Naming Conventions
description: Os nós no repositório estão sujeitos às convenções de nomenclatura do Java Content Repository
seo-description: Nodes in the repository are subject to naming conventions of the Java Content Repository
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
exl-id: 01c6bb29-1d2d-4a45-b291-0e8d97c01a08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 21%

---

# Convenções de nomenclatura{#naming-conventions}

Os nós no repositório estão sujeitos às convenções de nomenclatura da variável [Repositório de conteúdo Java](/help/sites-developing/the-basics.md#java-content-repository). No entanto, AEM impõe mais convenções para o nome dos nós da página.

## Convenções de nomenclatura para páginas {#naming-conventions-for-pages}

Essas convenções de nomenclatura são implementadas em vários níveis:

* JcrUtil: a AEM da aplicação do [Utilitários JCR](#jcr-utilities).
* PageManager: o [Gerenciador de página](#page-manager) O fornece métodos para operações no nível da página.
* De acordo com a interface do usuário que está sendo usada:

   * [Interface do usuário padrão e habilitada para toque](#standard-ui)
   * [Interface do usuário clássica](#classic-ui)

### Utilitários JCR {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) é a AEM implementação dos utilitários JCR. De especial interesse para validar nomes são os mapeamentos de caracteres que ele controla e as seguintes validações:

* `isValidName`

   * Verifica se o nome não está vazio e contém apenas caracteres válidos.
   * Pode ser usado para verificar se um nome proposto é válido.

* `createValidName`

   * Isso cria um rótulo válido de uma cadeia de caracteres arbitrária.
   * Ele pode ser usado para criar um nome a partir de um título.

### Gerenciador de página {#page-manager}

[PageManager](https://helpx.adobe.com/br/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) O fornece métodos para operações de nível de página, com base em [JCRUtil](#jcr-utilities).

### Interface do usuário padrão {#standard-ui}

A interface de usuário padrão habilitada para toque:

* Valida o nome de acordo com as restrições impostas pelo PageManager quando:

   * um título de página é fornecido para conversão no nome do nó
   * um nome de nó explícito é fornecido

### Interface do usuário clássica {#classic-ui}

A interface do usuário clássica impõe restrições mais severas:

* Valida o nome quando um nome de nó explícito é:

   * um título de página é fornecido para conversão no nome do nó
   * um nome de nó explícito é fornecido

* Caracteres válidos (somente esses caracteres são válidos quando uma página é criada na interface clássica, mesmo que `PageManagerImpl` permitiria caracteres adicionais):

   * “a” a “z”
   * “A” a “Z”
   * “0” a “9”
   * _ (sublinhado)
   * `-` (traço/subtração)
