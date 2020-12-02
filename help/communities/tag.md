---
title: Tag Essentials
seo-title: Tag Essentials
description: Visão geral da tag
seo-description: Visão geral da tag
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 3%

---


# Tag Essentials {#tag-essentials}

Quando os componentes do AEM Communities são configurados com marcação ativada, os membros da comunidade podem marcar o conteúdo que publicaram no ambiente de publicação.

A infraestrutura subjacente para tags aplicadas no ambiente publish é a mesma que para tags aplicadas ao conteúdo no ambiente autor, como páginas e ativos:

* Consulte [Administrando tags](../../help/sites-administering/tags.md) e [Marcando conteúdo gerado pelo usuário](tag-ugc.md) (UGC) para obter informações sobre como criar e gerenciar tags.

* Consulte [Marcação para desenvolvedores](../../help/sites-developing/tags.md) para obter informações sobre a [estrutura de marcação](../../help/sites-developing/framework.md), bem como para incluir e estender tags em [aplicativos personalizados](../../help/sites-developing/building.md).

* Consulte [Usando a Nuvem de tags sociais](tagcloud.md) para obter informações para autores sobre como adicionar um componente `social tag cloud` a uma página para realçar as tags aplicadas ao UGC no ambiente de publicação.

* Consulte [Marcando recursos de ativação](tag-resources.md) para obter informações sobre como marcar recursos para catálogos.

A marcação do UGC pode ser ativada ao configurar um [site da comunidade](sites-console.md#tagging) ou um dos seguintes recursos:

* [Blog](blog-feature.md)
* [Calendário](calendar.md)
* [Biblioteca de arquivos](file-library.md)
* [Fórum](forum.md)
* [Perguntas e respostas](working-with-qna.md)

## Essentials for Client-Side {#essentials-for-client-side}

### Nuvem de tags sociais {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusivo</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>propriedades</strong></td>
   <td>Consulte <a href="tagcloud.md">Usando a Nuvem de tags sociais</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do cliente](client-customize.md)

## Essentials for Server-Side {#essentials-for-server-side}

* [API do Social Tag Cloud](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Gerenciador de tags sociais](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personalizações do servidor](server-customize.md)

## Pesquisa de tags {#tag-searching}

A partir de [pacote de recursos 1](deploy-communities.md#latestfeaturepack) (FP1), a pesquisa de tags é realizada usando [títulos de tags](../../help/sites-developing/framework.md#tag-characteristics).

Antes do FP1, a pesquisa era realizada usando [tags ids](../../help/sites-developing/framework.md#tagid).
