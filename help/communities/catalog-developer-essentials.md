---
title: Princípios básicos do catálogo
seo-title: Princípios básicos do catálogo
description: Visão geral do catálogo
seo-description: Visão geral do catálogo
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
translation-type: tm+mt
source-git-commit: 41de9fff615b5b2f77d835740dfb1d33aa81e59b
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 3%

---


# Princípios básicos do catálogo {#catalog-essentials}

Esta página fornece as informações essenciais para trabalhar com o recurso de catálogo de sites da comunidade de ativação.

O recurso de catálogo, quando incluído em um site da comunidade, permite que os membros da comunidade naveguem e selecionem os recursos de ativação listados em um catálogo.

O componente [ `enablement catalog`](catalog.md) permite que os membros da comunidade acessem um catálogo de [recursos de ativação](resources.md). O uso de tags AEM é uma parte importante do gerenciamento da aparência dos recursos de ativação em um catálogo.

Consulte [Marcando recursos de ativação](tag-resources.md).

## Essentials for Client-Side {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/ativação/componentes/hbs/catálogo</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusivo</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.ativlement.hbs.breadcrumbs<br /> cq.social.ativlement.hbs.Catalog<br /> cq.social.ativlement.hbs.resource<br /> cq.social.ativlement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/catalog.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/catalog/clientlibs/catalog.css</td>
  </tr>
  <tr>
   <td><strong> propriedades</strong></td>
   <td>Consulte <a href="catalog.md">Recurso de catálogo</a></td>
  </tr>
 </tbody>
</table>

## Essentials for Server-Side {#essentials-for-server-side}

### Função do catálogo {#catalog-function}

Uma estrutura de site da comunidade que inclui a [função Catalog](functions.md#catalog-function), inclui um componente `enablement catalog` configurado.

### Pré-Filtros {#pre-filters}

Quando uma função de Catálogo é adicionada a um site da comunidade, é possível restringir os recursos de ativação e os caminhos de aprendizado que aparecem no catálogo especificando um pré-filtro. Isso é feito configurando propriedades na instância do recurso de catálogo do site.

Usando o exemplo do [Tutorial de ativação](getting-started-enablement.md):

* Sobre o autor
* Usando [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Como [https://&lt;servidor>:&lt;porta>/crx/de](http://localhost:4502/crx/de)

* Navegue até o recurso de catálogo na página de catálogo

   * Por exemplo, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* Adicionar um nó filtros filho

   * Selecione o nó `catalog`
   * Selecione **[!UICONTROL Criar Nó]**

      * Nome: `filters`
      * Tipo: `nt:unstructured`
      * Selecione **[!UICONTROL Salvar tudo]**

* Adicionar a propriedade `se_resource-tags` ao nó `filters`

   * Selecione o nó `filters`
   * Adicionar uma propriedade Multi

      * Nome: `se_resource-tags`
      * Tipo: String
      * Valor: *&lt;introduza um [TagID](#pre-filter-tagids)>*
         * Selecione **[!UICONTROL Multi]**
         * Selecione **[!UICONTROL Adicionar]**

            * Na caixa de diálogo pop-up, selecione `+` para adicionar TagIDs de pré-filtro adicionais

* Publicar novamente o site da comunidade

![configure-Catalog](assets/configure-catalog.png)

#### TagIDs de pré-filtro {#pre-filter-tagids}

O pré-filtro [TagIDs](../../help/sites-developing/framework.md#tagid) deve corresponder exatamente às tags aplicadas aos recursos de ativação. Eles estão visíveis na pasta `resources` do site como os valores da propriedade `se_resource-tags`.

![configure-filtros](assets/configure-catalog1.png)

### APIs de referência {#reference-apis}

* [API de ativação](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [API do relatórios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [API do Relatórios Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)

