---
title: Fragmentos de conteúdo - excluir considerações
seo-title: Fragmentos de conteúdo - excluir considerações
description: Fragmentos de conteúdo - excluir considerações
seo-description: Fragmentos de conteúdo - excluir considerações
uuid: e7ac1809-159f-4d02-ad30-dc6c246e8a04
contentOwner: aheimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: ec21237f-9186-49b4-8039-99df4db7c14a
docset: aem65
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 12%

---


# Fragmentos de conteúdo - excluir considerações{#content-fragments-delete-considerations}

## Permissões - Excluir ou Não Excluir {#permissions-delete-or-not-delete}

A capacidade de excluir conteúdo é poderosa, mas potencialmente sensível, com muitos setores precisando restringir e controlar como esses privilégios são distribuídos.

No que se refere a excluir permissões, os Fragmentos de conteúdo devem ser considerados em dois níveis:

1. **O Fragmento do conteúdo como uma única entidade.**

   * **Caso** de uso: Um usuário que precisa editar/atualizar um fragmento de conteúdo  **e excluir um fragmento** inteiro.
   * **Permissões**: A permissão  [](/help/sites-administering/security.md#actions) Excluir pode ser  [atribuída por meio do Gerenciamento](/help/sites-administering/security.md#managing-permissions) de usuários e/ou grupos.

1. **As várias subentidades que compõem um fragmento de conteúdo; por exemplo, variações, subnós.**

   A operação básica do editor de fragmentos de conteúdo requer que esses subelementos transitórios possam ser excluídos. Por exemplo, ao manipular variações; também ao editar metadados ou gerenciar conteúdo associado.

   * **Caso** de uso: Um usuário que precisa editar/atualizar um fragmento de conteúdo -  **sem ter permissão para excluir um fragmento** inteiro.
   * **Permissões**: Consulte  [Permissões necessárias somente](/help/assets/content-fragments/content-fragments-delete.md#permissions-required-for-editor-functionality-only) para a funcionalidade do editor.

>[!NOTE]
>
>Quando um usuário não tem nenhuma permissão [Excluir](/help/sites-administering/security.md#actions), o editor de Fragmento de conteúdo opera no modo *somente leitura*.

>[!NOTE]
>
>Consulte também [Como auditar operações de gerenciamento de usuários em AEM](/help/sites-administering/audit-user-management-operations.md).

## Permissões necessárias somente para a funcionalidade do editor {#permissions-required-for-editor-functionality-only}

Para usuários que precisam editar/atualizar um fragmento de conteúdo, **sem permitir que excluam um fragmento inteiro**, permissões específicas devem ser atribuídas, já que a operação básica do editor de fragmentos de conteúdo requer que elementos transitórios secundários possam ser excluídos.

Por exemplo, ao manipular variações; também ao editar metadados ou gerenciar conteúdo associado.

>[!NOTE]
>
>As permissões de exclusão, necessárias para editar/atualizar um Fragmento de conteúdo, estão incluídas na permissão Excluir [atribuída por meio do Gerenciamento de usuários e/ou grupos](/help/sites-administering/security.md#managing-permissions).

As permissões necessárias para editar/atualizar um fragmento precisam ser aplicadas ao nó que contém o fragmento de conteúdo ou a um nó pai apropriado (em qualquer nível em `/content/dam`). Quando atribuídas a esse nó pai, as permissões serão aplicadas a todos os nós dentro desse ramo.

Por exemplo, uma pasta que manterá todos os fragmentos de conteúdo, como:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>A configuração das permissões em `/content/dam` também é possível, pois todos os fragmentos de conteúdo são armazenados aqui.
>
>No entanto, essa ação aplica as mesmas permissões de exclusão a *todos* outros tipos de ativos também.

Os pré-requisitos de permissões para permitir que um usuário e/ou grupo específico edite/atualize um fragmento de conteúdo são:

>[!NOTE]
>
>Esta lista mostra todos os privilégios necessários, não apenas os privilégios de exclusão.

* Para os nós ou pastas do Fragmento de conteúdo:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* Para o nó `jcr:content`de todos os Fragmentos de conteúdo:

   * `jcr:addChildNodes`,  `jcr:modifyProperties` e  `jcr:removeChildNodes`

* Para todos os nós abaixo de `jcr:content` de todos os Fragmentos de conteúdo:

   * `jcr:addChildNodes`,  `jcr:modifyProperties` e  `jcr:removeChildNodes`,  `jcr:removeNode`

Esses privilégios `remove` devem ser [administrados usando Listas Controles de acesso, dentro de CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management).

Os privilégios `add` e `modify` também podem ser administrados no CRXDE Lite ou usando o console de Gerenciamento de usuários.

Por exemplo, a definição dos privilégios `remove` para um grupo `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)

