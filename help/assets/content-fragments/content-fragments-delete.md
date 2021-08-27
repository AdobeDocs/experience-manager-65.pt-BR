---
title: Fragmentos de conteúdo - excluir considerações
description: Revise essas importantes considerações antes de definir as políticas de exclusão dos Fragmentos de conteúdo no AEM. Os Fragmentos de conteúdo são uma ferramenta poderosa para fornecer conteúdo sem interface, e as implicações de excluí-los devem ser cuidadosamente consideradas.
feature: Content Fragments
role: User
source-git-commit: 94145c6428f61e31f6784a3d6ea67aa8d81cedd6
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 9%

---

# Fragmentos de conteúdo - excluir considerações {#content-fragments-delete-considerations}

Revise essas importantes considerações antes de definir as políticas de exclusão dos Fragmentos de conteúdo no AEM. Os Fragmentos de conteúdo são uma ferramenta poderosa para fornecer conteúdo sem interface, e as implicações de excluí-los devem ser cuidadosamente consideradas.

## Permissões - Excluir ou não excluir {#permissions-delete-or-not-delete}

A capacidade de excluir conteúdo é poderosa, mas potencialmente sensível, com muitos setores precisando restringir e controlar a distribuição desses privilégios.

Em relação às permissões de exclusão, os Fragmentos de conteúdo devem ser considerados em dois níveis:

1. **O Fragmento do conteúdo como uma única entidade.**

   * **Caso** de uso: Um usuário que precisa editar/atualizar um fragmento de conteúdo  **e excluir um fragmento** inteiro.
   * **Permissões**: A permissão  [](/help/sites-administering/security.md#actions) Excluir pode ser  [atribuída por meio do Gerenciamento de usuários e/ou grupos](/help/sites-administering/security.md#managing-permissions).

2. **As várias subentidades que compõem um fragmento de conteúdo; por exemplo, variações, subnós.**

   A operação básica do editor de fragmentos de conteúdo requer que esses subelementos transitórios possam ser excluídos. Por exemplo, ao manipular variações; também ao editar metadados ou gerenciar conteúdo associado.

   * **Caso** de uso: Um usuário que precisa editar/atualizar um fragmento de conteúdo -  **sem ter permissão para excluir um fragmento** inteiro.
   * **Permissões**: Consulte  [Permissões necessárias somente para a funcionalidade do editor](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>Quando um usuário não tem nenhuma permissão [Delete](/help/sites-administering/security.md#actions), o editor de Fragmento de conteúdo opera no modo *somente leitura*.

>[!NOTE]
>
>Consulte também [Como auditar operações de gerenciamento de usuários em AEM](/help/sites-administering/audit-user-management-operations.md).

## Permissões necessárias somente para a funcionalidade do editor {#permissions-required-for-editor-functionality-only}

Para usuários que precisam editar/atualizar um fragmento de conteúdo, **sem permitir que excluam um fragmento inteiro**, permissões específicas devem ser atribuídas, já que a operação básica do editor de fragmentos de conteúdo requer que elementos transitórios secundários possam ser excluídos.

Por exemplo, ao manipular variações; também ao editar metadados ou gerenciar conteúdo associado.

>[!NOTE]
>
>As permissões de exclusão, necessárias para editar/atualizar um Fragmento de conteúdo, estão incluídas na permissão de exclusão [atribuída por meio de Gerenciamento de usuários e/ou grupos](/help/sites-administering/security.md#managing-permissions).

As permissões necessárias para editar/atualizar um fragmento precisam ser aplicadas ao nó que contém o fragmento de conteúdo ou a um nó pai apropriado (em qualquer nível em `/content/dam`). Quando atribuídas a esse nó pai, as permissões serão aplicadas a todos os nós dentro dessa ramificação.

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

Esses privilégios `remove` devem ser [administrados usando Listas de Controle de Acesso, dentro de CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management).

Os privilégios `add` e `modify` também podem ser administrados no CRXDE Lite, ou usando o console de Gerenciamento de Usuário.

Por exemplo, a definição dos privilégios `remove` para um grupo `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
