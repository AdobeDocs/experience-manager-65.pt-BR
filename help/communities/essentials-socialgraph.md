---
title: Essenciais do gráfico social
seo-title: Essenciais do gráfico social
description: seguir a visão geral do componente e do componente
seo-description: seguir a visão geral do componente e do componente
uuid: 8ea33760-62b1-4de2-b07f-bc2417ade156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f8d85d72-0215-4680-a334-e37a530fba58
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Essenciais do gráfico social {#social-graph-essentials}

A capacidade de um membro da Comunidade seguir as [atividades](essentials-activities.md) , bem como as  a seguir, é estabelecida através de dois componentes:

O `following` componente deve ser associado a outro recurso, e essa associação já está estabelecida para os membros e recursos das Comunidades existentes em um site [da](overview.md#communitiessites)comunidade.

O `following` componente lista os membros que seguem o membro atual ou que estão sendo seguidos pelo membro atual. Este gráfico social das relações entre os membros é incluído no perfil do usuário estabelecido para um site da comunidade.

## Essenciais para o lado do cliente {#essentials-for-client-side}

### Seguindo {#following}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/socialógrafo/componentes/hbs/relações</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusivo</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.socialógrafo</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
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
   <td><strong> propriedade opcional<br /></strong></td>
   <td>
    <ul>
     <li>Nome: <strong><code>outgoing</code></strong></li>
     <li>Tipo: booliano</li>
     <li>Valor:<br />
      <ul>
       <li><i>Verdadeiro </i>- O <code>following</code> componente lista os membros que o membro conectado no momento <code>follows</code></li>
       <li><i>Falso </i>- O <code>following</code> componente lista os membros que <code>follow </code>o membro atualmente conectado</li>
      </ul> </li>
    </ul> <p>O padrão é <i>true</i> se a propriedade estiver ausente. Atualmente, não é possível definir essa propriedade usando a caixa de diálogo de edição no modo de autor. A propriedade deve ser adicionada a uma instância do <code>following </code>nó usando <a href="../../help/sites-developing/developing-with-crxde-lite.md">CRXDE|Lite</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Seguir {#follow}

| **resourceType** | `social/socialgraph/components/hbs/following` |
|---|---|
| [**inclusivo **](scf.md#add-or-include-a-communities-component) | Não |
| **templates** | `/libs/social/socialgraph/components/hbs/following/following.hbs` |
| **css** | `/libs/social/socialgraph/components/hbs/following/clientlibs/following.css` |

* [Personalizações do cliente](client-customize.md)

## Fundamentos para servidor {#essentials-for-server-side}

* [API de gráfico social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/api/package-frame.html)

* [Pontos finais do gráfico social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/graph/client/endpoint/package-frame.html)

* [Personalizações do servidor](server-customize.md)

