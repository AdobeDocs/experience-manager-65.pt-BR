---
title: Fundamentos do gráfico social
description: Saiba mais sobre os fundamentos do Gráfico social usando os componentes Seguir e Seguir em um site da comunidade.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: c037a788-c943-4f95-a028-1fcb0ef48f86
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 2%

---

# Fundamentos do gráfico social  {#social-graph-essentials}

A capacidade de um membro da Comunidade seguir [atividades](essentials-activities.md) e ser seguido é estabelecida por meio de dois componentes:

O componente `following` deve ser associado a outro recurso, e essa associação já está estabelecida para membros e recursos existentes das Comunidades em um [site da comunidade](overview.md#communitiessites).

O componente `following` lista os membros que estão seguindo o membro atual ou que estão sendo seguidos pelo membro atual. Este gráfico social dos relacionamentos entre membros é incluído no perfil do usuário estabelecido para um site da comunidade.

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
   <td>Consulte <a href="socialgraph.md">Usando o Gráfico Social</a></td>
  </tr>
  <tr>
   <td><strong> propriedade <br /> opcional</strong></td>
   <td>
    <ul>
     <li>Nome: <strong><code>outgoing</code></strong></li>
     <li>Tipo: Booleano</li>
     <li>Valor:<br />
      <ul>
       <li><i>True </i>- O componente <code>following</code> lista os membros que o membro conectado <code>follows</code></li>
       <li><i>Falso </i>- O componente <code>following</code> lista os membros que <code>follow </code>o membro conectado</li>
      </ul> </li>
    </ul> <p>O padrão é <i>true</i> se a propriedade estiver ausente. Não é possível definir essa propriedade usando a caixa de diálogo de edição no modo Autor. A propriedade deve ser adicionada a uma instância do nó <code>following</code> usando <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
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

* [API de gráfico social](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Pontos de Extremidade do Gráfico Social](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Personalizações do lado do servidor](server-customize.md)
