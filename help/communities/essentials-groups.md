---
title: Fundamentos do grupo comunitário
seo-title: Community Group Essentials
description: Criação dinâmica de sites da comunidade
seo-description: Creating community sites dynamically
uuid: 168e7aeb-6e9a-468d-8ac4-274007cea252
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4f85cd3c-5158-4f23-abe2-7e375fd0c8d4
exl-id: f45ae7be-a500-463a-ab3e-81f281651a9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---

# Fundamentos do grupo comunitário  {#community-group-essentials}

O recurso de grupos da comunidade é a capacidade de uma subcomunidade ser criada dinamicamente em um site da comunidade por usuários autorizados dos ambientes de publicação e criação.

Comunidades [pacote de recursos 1](deploy-communities.md#latestfeaturepack), é possível que os grupos sejam aninhados em outros grupos

## Fundamentos para o lado do cliente {#essentials-for-client-side}

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
   <td>social/grupo/componentes/hbs/community/groups</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.communitygroups</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/group/components/hbs/communitygroups/communitygroups.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/group/components/hbs/communitygroupmemberlist/clientlibs/communitygroups.css</td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](client-customize.md)

## Fundamentos para o lado do servidor {#essentials-for-server-side}

* [API do grupo da comunidade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/api/package-summary.html)

* [Endpoints do grupo da comunidade](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/group/client/endpoints/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

### Função de grupos {#groups-function}

Uma estrutura de site da comunidade que inclui uma [Função Grupos](functions.md#groups-function) apoiará a criação de novos `community groups` nos ambientes de publicação e criação . O grupo da comunidade criado incluirá um `community groups member list` que listará os membros do grupo.

Um ou mais [modelos de grupo da comunidade](tools-groups.md), que fornecem o design da(s) página(s) do grupo da comunidade, podem ser configuradas para a função Grupos quando a função está sendo adicionada a um [modelo de site da comunidade](sites.md) ou aninhados dentro de um modelo de grupo da comunidade.

A inclusão de vários modelos de grupo da comunidade resulta na apresentação de uma escolha de design ao usuário autorizado no momento em que um novo grupo da comunidade é criado para o site da comunidade, conforme mostrado na seção sobre [grupos da comunidade](creating-groups.md) para autores.

### Grupos aninhados {#nested-groups}

Comunidades [FP1](deploy-communities.md#latestfeaturepack), é possível que uma função Grupos seja incluída em um modelo de grupo, permitindo assim grupos aninhados (subcomunidades).

Quando um site da comunidade ou modelo de grupo inclui a função Grupos , é possível:

* Crie uma subcomunidade no ambiente de criação.

* Crie um grupo no ambiente de publicação, quando configurado para permitir isso.

Ao criar um grupo no ambiente de criação, é necessário primeiro publicar o site da comunidade e, em seguida, publicar o grupo. A publicação do site da comunidade publicará as páginas do grupo, sem criar os grupos de membros da subcomunidade aos quais as ACLs estão definidas. Assim, um grupo restrito (secreto) pode estar visível até que o grupo seja explicitamente publicado.

## Links e informações relacionadas {#links-and-related-information}

* [Gerenciar usuários e grupos de usuários](users.md)
* [Console de grupos de comunidades](groups.md)
* [Função de grupos](functions.md#groups-function)
* [Modelos de grupo](tools-groups.md)
