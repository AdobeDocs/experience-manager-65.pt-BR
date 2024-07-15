---
title: Fundamentos do grupo da comunidade
description: Saiba como os usuários autorizados podem usar o recurso Grupos da comunidade para criar dinamicamente uma subcomunidade em um site da comunidade.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# Fundamentos do grupo da comunidade  {#community-group-essentials}

O recurso de grupos da comunidade é a capacidade de uma subcomunidade ser criada dinamicamente em um site da comunidade por usuários autorizados nos ambientes de publicação e criação.

A partir do Communities [feature pack 1](deploy-communities.md#latestfeaturepack), é possível que grupos sejam aninhados dentro de outros grupos.

## Essentials para o lado do cliente {#essentials-for-client-side}

### Lista de membros dos grupos da comunidade {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/communitygroupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/communitygroupmemberlist.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/memberList.css</td>
  </tr>
  <tr>
   <td><strong>propriedades</strong></td>
   <td>Consulte <a href="creating-groups.md">Grupo da comunidade</a></td>
  </tr>
 </tbody>
</table>

### Grupos de comunidades {#community-groups}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/group/components/hbs/community-groups</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [API do grupo da comunidade](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Pontos de Extremidade do Grupo da Comunidade](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Função Grupos {#groups-function}

Uma estrutura de site da comunidade que inclui uma [função de Grupos](functions.md#groups-function) dá suporte à criação de um novo `community groups` a partir dos ambientes de publicação e criação. O grupo da comunidade criado inclui um componente `community groups member list` que lista os membros do grupo.

Um ou mais [modelos de grupo da comunidade](tools-groups.md), que fornecem o design das páginas de grupo da comunidade, podem ser configurados para a função Grupos. Isso é verdade quando a função está sendo adicionada a um [modelo de site de comunidade](sites.md) ou aninhada em um modelo de grupo de comunidade.

A inclusão de vários modelos de grupo da comunidade resulta em uma escolha. Ou seja, a escolha do design que está sendo apresentado ao usuário autorizado no momento em que um grupo da comunidade é criado para o site da comunidade. Consulte a seção sobre [grupos da comunidade](creating-groups.md) para obter os autores.

### Grupos aninhados {#nested-groups}

A partir de Communities [FP1](deploy-communities.md#latestfeaturepack), é possível que uma função Groups seja incluída em um modelo de grupo, permitindo assim grupos aninhados (subcomunidades).

Quando um site da comunidade ou modelo de grupo inclui a função Grupos, é possível:

* Crie uma subcomunidade no ambiente de criação.

* Crie um grupo no ambiente de publicação, quando configurado para permitir.

Ao criar um grupo no ambiente de criação, é necessário primeiro publicar o site da comunidade e, em seguida, publicar o grupo. A publicação do site da comunidade publica as páginas do grupo, sem criar os grupos de membros da subcomunidade aos quais as ACLs estão definidas. Assim, um grupo restrito (secreto) pode ser visível até que o grupo seja explicitamente publicado.

## Links e informações relacionadas {#links-and-related-information}

* [Gerenciar usuários e grupos de usuários](users.md)
* [Console de grupos de comunidades](groups.md)
* [Função Grupos](functions.md#groups-function)
* [Modelos de grupo](tools-groups.md)
