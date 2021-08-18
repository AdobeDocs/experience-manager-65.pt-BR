---
title: Fundamentos do catálogo
seo-title: Fundamentos do catálogo
description: Visão geral do catálogo
seo-description: Visão geral do catálogo
uuid: 788512bb-fa38-48fb-a769-1eaae6bb95a1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 542467ef-3793-4347-8424-c365c5a166f6
exl-id: 4ca76b50-d56d-4f4d-be92-bf8929c5d754
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 3%

---

# Fundamentos do catálogo {#catalog-essentials}

Esta página fornece as informações essenciais para trabalhar com o recurso de catálogo dos sites da comunidade de ativação.

O recurso de catálogo, quando incluído em um site da comunidade, permite que os membros da comunidade naveguem e selecionem recursos de capacitação listados em um catálogo.

O [ `enablement catalog` componente](catalog.md) permite que os membros da comunidade acessem um catálogo de [recursos de ativação](resources.md). O uso de tags de AEM é uma parte importante do gerenciamento da aparência dos recursos de ativação em um catálogo.

Consulte [Marcando recursos de ativação](tag-resources.md).

## Fundamentos para o lado do cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/ativation/components/hbs/catalog</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>incondicional</strong></a></td>
   <td>Não</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.catalog<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
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

## Fundamentos para o lado do servidor {#essentials-for-server-side}

### Função do catálogo {#catalog-function}

Uma estrutura de site da comunidade que inclui a [função de Catálogo](functions.md#catalog-function), inclui um componente `enablement catalog` configurado.

### Pré-filtros {#pre-filters}

Quando uma função de Catálogo é adicionada a um site da comunidade, é possível restringir os recursos de ativação e os caminhos de aprendizado que aparecem no catálogo especificando um pré-filtro. Isso é feito definindo propriedades na instância do recurso de catálogo do site.

Usando o exemplo do [Tutorial de ativação](getting-started-enablement.md):

* Sobre o autor
* Usando [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Como [https://&lt;server>:&lt;port>/crx/de](http://localhost:4502/crx/de)

* Navegue até o recurso de catálogo na página de catálogo

   * Por exemplo, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* Adicionar um nó de filtros filho

   * Selecione o nó `catalog`
   * Selecione **[!UICONTROL Criar Nó]**

      * Nome: `filters`
      * Tipo: `nt:unstructured`
      * Selecione **[!UICONTROL Salvar tudo]**

* Adicione a propriedade `se_resource-tags` ao nó `filters`

   * Selecione o nó `filters`
   * Adicionar uma multipropriedade

      * Nome: `se_resource-tags`
      * Tipo: String
      * Valor: *&lt;insira um [TagID](#pre-filter-tagids)>*
         * Selecione **[!UICONTROL Multi]**
         * Selecione **[!UICONTROL Adicionar]**

            * Na caixa de diálogo de pop-up, selecione `+` para adicionar TagIDs de pré-filtro adicionais

* Publicar novamente o site da comunidade

![configure-catalog](assets/configure-catalog.png)

#### TagIDs pré-filtradas {#pre-filter-tagids}

O pré-filtro [TagIDs](../../help/sites-developing/framework.md#tagid) deve corresponder exatamente às tags aplicadas aos recursos de ativação. Eles estão visíveis na pasta `resources` do site como os valores da propriedade `se_resource-tags`.

![configure-filters](assets/configure-catalog1.png)

### APIs de referência {#reference-apis}

* [API de ativação](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [API de relatórios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API de relatórios do Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
