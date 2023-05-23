---
title: Fundamentos de tags
seo-title: Tag Essentials
description: Visão geral da tag
seo-description: Tag overview
uuid: a5d52319-f821-4608-b0ab-abc8a1374343
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d355a3ee-c8a8-4a07-8d28-d1a99bda315c
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 3%

---

# Fundamentos de tags {#tag-essentials}

Quando os componentes do AEM Communities são configurados com a marcação ativada, os membros da comunidade podem marcar o conteúdo que publicam no ambiente de publicação.

A infraestrutura subjacente das tags aplicadas no ambiente de publicação é a mesma que as tags aplicadas ao conteúdo no ambiente de criação, como páginas e ativos:

* Consulte [Administração de tags](../../help/sites-administering/tags.md) e [Marcação do conteúdo gerado pelo usuário](tag-ugc.md) (UGC) para obter informações sobre como criar e gerenciar tags.

* Consulte [Marcação para desenvolvedores](../../help/sites-developing/tags.md) para obter informações sobre o [estrutura de marcação](../../help/sites-developing/framework.md) bem como incluir e estender tags na [aplicativos personalizados](../../help/sites-developing/building.md).

* Consulte [Uso da Social Tag Cloud](tagcloud.md) para obter informações para autores sobre como adicionar uma `social tag cloud` componente a uma página para realçar as tags aplicadas a UGC no ambiente de publicação.

A marcação de UGC pode ser ativada ao configurar um [site da comunidade](sites-console.md#tagging) ou um dos seguintes recursos:

* [Blog](blog-feature.md)
* [Calendário](calendar.md)
* [Biblioteca de arquivos](file-library.md)
* [Fórum](forum.md)
* [QnA](working-with-qna.md)

## Essentials para o lado do cliente {#essentials-for-client-side}

### Tags em nuvem do Social {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incluível</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>modelos</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>propriedades</strong></td>
   <td>Consulte <a href="tagcloud.md">Uso da Social Tag Cloud</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [API da nuvem de tag social](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Gerenciador de tags sociais](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

## Pesquisa de tags {#tag-searching}

Em [pacote de recursos 1](deploy-communities.md#latestfeaturepack) (FP1), a pesquisa de tags é realizada usando [títulos de tags](../../help/sites-developing/framework.md#tag-characteristics).

Antes do FP1, a pesquisa era realizada usando [ids de tag](../../help/sites-developing/framework.md#tagid).
