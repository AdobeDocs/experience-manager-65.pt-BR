---
title: Fundamentos de tags
description: Saiba mais sobre quando os componentes das Comunidades são configurados com a marcação ativada, os membros da comunidade podem marcar o conteúdo que publicam no ambiente de publicação.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 3%

---

# Fundamentos de tags {#tag-essentials}

Quando os componentes do AEM Communities são configurados com a marcação ativada, os membros da comunidade podem marcar o conteúdo que publicam no ambiente de publicação.

A infraestrutura subjacente das tags aplicadas no ambiente de publicação é a mesma que as tags aplicadas ao conteúdo no ambiente de criação, como páginas e ativos:

* Consulte [Administrando tags](../../help/sites-administering/tags.md) e [Marcando o conteúdo gerado pelo usuário](tag-ugc.md) (UGC) para obter informações sobre como criar e gerenciar tags.

* Consulte [Marcação para desenvolvedores](../../help/sites-developing/tags.md) para obter informações sobre a [estrutura de marcação](../../help/sites-developing/framework.md) e sobre como incluir e estender marcas em [aplicativos personalizados](../../help/sites-developing/building.md).

* Consulte [Usando a Nuvem da Marca Social](tagcloud.md) para obter informações para autores sobre como adicionar um componente `social tag cloud` a uma página para destacar as marcas aplicadas ao UGC no ambiente de publicação.

A marcação de UGC pode ser habilitada ao configurar um [site da comunidade](sites-console.md#tagging) ou um dos seguintes recursos:

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
   <td>Consulte <a href="tagcloud.md">Usando a Nuvem de Tags Sociais</a></td>
  </tr>
 </tbody>
</table>

* [Personalizações do lado do cliente](client-customize.md)

## Essentials para o lado do servidor {#essentials-for-server-side}

* [API da Nuvem da Marca Social](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [Gerenciador de marcas sociais](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [Personalizações do lado do servidor](server-customize.md)

## Pesquisa de tags {#tag-searching}

Desde o [feature pack 1](deploy-communities.md#latestfeaturepack) (FP1), a pesquisa de tags é executada usando [títulos de tags](../../help/sites-developing/framework.md#tag-characteristics).

Antes do FP1, a pesquisa era realizada usando [ids de tag](../../help/sites-developing/framework.md#tagid).
