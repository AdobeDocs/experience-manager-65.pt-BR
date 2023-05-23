---
title: Nomeação de convenções de nós no repositório de conteúdo Jave
description: Os nós no repositório estão sujeitos às convenções de nomenclatura do Repositório de conteúdo Java
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
exl-id: 01c6bb29-1d2d-4a45-b291-0e8d97c01a08
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 7%

---

# Convenções de nomenclatura{#naming-conventions}

Os nós no repositório estão sujeitos às convenções de nomenclatura da [Repositório de conteúdo Java](/help/sites-developing/the-basics.md#java-content-repository). No entanto, o AEM impõe mais convenções para o nome dos nós da página.

## Convenções de nomenclatura para páginas {#naming-conventions-for-pages}

Essas convenções de nomenclatura são implementadas em vários níveis:

* JcrUtil: a implementação do AEM do [Utilitários JCR](#jcr-utilities).
* PageManager: a [Gerenciador de páginas](#page-manager) O fornece métodos para operações em nível de página.
* De acordo com a interface que está sendo usada:

   * [Interface de usuário padrão habilitada para toque](#standard-ui)
   * [IU Clássica](#classic-ui)

### Utilitários JCR {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) é a implementação AEM dos utilitários JCR. De especial interesse para validar nomes são os mapeamentos de caracteres que ele controla e as seguintes validações:

* `isValidName`

   * Verifica se o nome não está vazio e contém apenas caracteres válidos.
   * Pode ser usado para verificar se um nome proposto é válido.

* `createValidName`

   * Isso cria um rótulo válido de uma sequência arbitrária.
   * Ela pode ser usada para criar um nome a partir de um título.

### Gerenciador de páginas {#page-manager}

[PageManager](https://helpx.adobe.com/br/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) O fornece métodos para operações no nível da página, com base em [JCRUtil](#jcr-utilities).

### Interface do usuário padrão {#standard-ui}

A interface padrão habilitada para toque:

* Valida o nome de acordo com as restrições impostas pelo PageManager quando:

   * um título de página é fornecido para conversão no nome do nó
   * um nome de nó explícito é fornecido

### IU Clássica {#classic-ui}

A interface clássica impõe restrições mais rigorosas:

* Valida o nome quando um nome de nó explícito:

   * um título de página é fornecido para conversão no nome do nó
   * um nome de nó explícito é fornecido

* Caracteres válidos (somente esses caracteres são realmente válidos quando uma página é criada na interface clássica, mesmo que `PageManagerImpl` permitiria caracteres adicionais):

   * &#39;a&#39; a &#39;z&#39;
   * &#39;A&#39; a &#39;Z&#39;
   * &#39;0&#39; a &#39;9&#39;
   * _ (sublinhado)
   * `-` (traço/sinal de menos)
