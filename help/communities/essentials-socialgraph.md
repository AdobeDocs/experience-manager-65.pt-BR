---
title: Fundamentos do gráfico social
seo-title: Social Graph Essentials
description: seguir o componente e a seguinte visão geral do componente
seo-description: follow component and following component overview
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---

# Fundamentos do gráfico social  {#social-graph-essentials}

A capacidade de um membro da Comunidade de seguir [atividades](essentials-activities.md) e ser seguida é estabelecida por meio de dois componentes:

A variável `following` deve ser associado a outro recurso, e essa associação já está estabelecida para membros e recursos existentes das Comunidades em um [site da comunidade](overview.md#communitiessites).

A variável `following` componente lista os membros que estão seguindo o membro atual ou que estão sendo seguidos pelo membro atual. Este gráfico social dos relacionamentos entre membros é incluído no perfil do usuário estabelecido para um site da comunidade.

## Essentials para o lado do cliente {#essentials-for-client-side}

### Seguindo {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialgraph/components/hbs/relationship</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluível</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.socialgraph</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/relationships.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/socialgraph/components/hbs/relationships/clientlibs/relationships.css</td>
  </tr>
  <tr>
   <td><strong> propriedades</strong></td>
   <td>Consulte <a href="socialgraph.md">Uso do gráfico social</a></td>
  </tr>
  <tr>
   <td><strong> opcional<br /> propriedade</strong></td>
   <td>
    <ul>
     <li>Nome: <strong><code>outgoing</code></strong></li>
     <li>Tipo: Booleano</li>
     <li>Valor:<br />
      <ul>
       <li><i>True </i>- A <code>following</code> componente listará os membros que o membro conectado no momento <code>follows</code></li>
       <li><i>Falso </i>- A <code>following</code> componente listará os membros que <code>follow </code>o membro conectado no momento</li>
      </ul> </li>
    </ul> <p>O padrão é <i>true</i> se a propriedade estiver ausente. Atualmente, não é possível definir essa propriedade usando a caixa de diálogo de edição no modo de autor. A propriedade deve ser adicionada a uma instância do <code>following </code>nó usando <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Seguir {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**incluível**](scf.md#add-or-include-a-communities-component) | Não |
| **modelos** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [Personalizações do lado do cliente](client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [API do gráfico social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Endpoints do gráfico social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Personalizações do lado do servidor](server-customize.md)
