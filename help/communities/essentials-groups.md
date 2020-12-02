---
title: Essenciais do grupo comunitário
seo-title: Essenciais do grupo comunitário
description: Criação dinâmica de sites da comunidade
seo-description: Criação dinâmica de sites da comunidade
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---


# Princípios básicos do grupo da comunidade {#community-group-essentials}

O recurso de grupos da comunidade é a capacidade de uma subcomunidade ser criada dinamicamente em um site da comunidade por usuários autorizados dos ambientes de publicação e autor.

A partir de Communities [feature pack 1](deploy-communities.md#latestfeaturepack), é possível que os grupos sejam aninhados dentro de outros grupos

## Essentials for Client-Side {#essentials-for-client-side}

### Lista de membro de grupos da comunidade {#community-groups-member-list}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/grupo/componentes/hbs/communitygroupmemberlist</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
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
   <td>social/grupo/componentes/hbs/community groups</td>
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

* [Personalizações do cliente](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API do grupo da comunidade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Pontos finais do grupo da comunidade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Personalizações do servidor](server-customize.md)

### Função de grupos {#groups-function}

Uma estrutura de site da comunidade que inclui uma [função de grupos](functions.md#groups-function) oferecerá suporte à criação de novos `community groups` a partir dos ambientes de publicação e autor. O grupo de comunidade criado incluirá um componente `community groups member list` que lista os membros do grupo.

Um ou mais [modelos de grupo da comunidade](tools-groups.md), que fornecem o design das páginas de grupo da comunidade, podem ser configurados para a função Grupos quando a função está sendo adicionada a [modelo de site da comunidade](sites.md) ou aninhada em um modelo de grupo da comunidade.

A inclusão de vários modelos de grupos da comunidade resulta na apresentação de uma escolha de design ao usuário autorizado no momento em que um novo grupo da comunidade é criado para o site da comunidade, conforme mostrado na seção [grupos da comunidade](creating-groups.md) para autores.

### Grupos aninhados {#nested-groups}

A partir de Communities [FP1](deploy-communities.md#latestfeaturepack), é possível que uma função de Grupos seja incluída em um modelo de grupo, permitindo assim grupos aninhados (subcomunidades).

Quando um site da comunidade ou modelo de grupo inclui a função Grupos, é possível:

* Crie uma subcomunidade no ambiente do autor.

* Crie um grupo no ambiente de publicação, quando configurado para permitir.

Ao criar um grupo no ambiente do autor, é necessário primeiro publicar o site da comunidade e depois publicar o grupo. A publicação do site da comunidade publicará as páginas do grupo, sem criar os grupos de membros da subcomunidade aos quais as ACLs estão definidas. Assim, um grupo restrito (secreto) pode ser visível até que o grupo seja explicitamente publicado.

## Links e informações relacionadas {#links-and-related-information}

* [Gerenciamento de usuários e grupos de usuários](users.md)
* [Console de grupos de comunidades](groups.md)
* [Função Grupos](functions.md#groups-function)
* [Modelos de grupo](tools-groups.md)

