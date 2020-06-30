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
source-git-commit: 82affd528f2526384b319fe89082e0f574ab5855
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 2%

---


# Princípios básicos do catálogo {#catalog-essentials}

Esta página fornece as informações essenciais para trabalhar com o recurso de catálogo de sites da comunidade de ativação.

O recurso de catálogo, quando incluído em um site da comunidade, permite que os membros da comunidade naveguem e selecionem os recursos de ativação listados em um catálogo.

O [ componente `enablement catalog` permite que os membros da comunidade acessem um catálogo de recursos](catalog.md) de [](resources.md)ativação. O uso de tags AEM é uma parte importante do gerenciamento da aparência dos recursos de ativação em um catálogo.

Consulte [Marcação de recursos](tag-resources.md)de ativação.

## Essenciais para o lado do cliente {#essentials-for-client-side}

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
   <td>Consulte Recurso <a href="catalog.md">do catálogo</a></td>
  </tr>
 </tbody>
</table>

## Fundamentos para servidor {#essentials-for-server-side}

### Função do catálogo {#catalog-function}

Uma estrutura de site da comunidade que inclui a função [](functions.md#catalog-function)Catalog, inclui um `enablement catalog` componente configurado.

### Pré-Filtros {#pre-filters}

Quando uma função de Catálogo é adicionada a um site da comunidade, é possível restringir os recursos de ativação e os caminhos de aprendizado que aparecem no catálogo especificando um pré-filtro. Isso é feito configurando propriedades na instância do recurso de catálogo do site.

Usando o exemplo do Tutorial de [ativação](getting-started-enablement.md):

* Sobre o autor
* Uso do [CRXDE](../../help/sites-developing/developing-with-crxde-lite.md)

   * Como [https://&lt;servidor>:&lt;porta>/crx/de](http://localhost:4502/crx/de)

* Navegue até o recurso de catálogo na página de catálogo

   * Por exemplo, `/content/sites/enable/en/catalog/jcr:content/content/primary/catalog`

* Adicionar um nó filtros filho

   * Selecionar o `catalog`nó
   * Selecionar nó **[!UICONTROL Criar]**

      * Nome: `filters`
      * Tipo: `nt:unstructured`
      * Selecione **[!UICONTROL Salvar tudo]**

* Adicionar `se_resource-tags` propriedade ao `filters` nó

   * Selecione o `filters` nó
   * Adicionar uma propriedade Multi

      * Nome: `se_resource-tags`
      * Tipo: String
      * Valor: *&lt;insira uma[TagID](#pre-filter-tagids)>*
         * Selecionar **[!UICONTROL vários]**
         * Selecionar **[!UICONTROL Adicionar]**

            * Na caixa de diálogo pop-up, selecione `+` para adicionar TagIDs de pré-filtro adicionais

* Publicar novamente o site da comunidade

![chlimage_1-189](assets/chlimage_1-189.png)

#### TagIDs de pré-filtro {#pre-filter-tagids}

As [TagIDs](../../help/sites-developing/framework.md#tagid) pré-filtradas devem corresponder exatamente às tags aplicadas aos recursos de ativação. Elas estão visíveis na `resources` pasta do site como os valores da propriedade `se_resource-tags`.

![chlimage_1-190](assets/chlimage_1-190.png)

### APIs de referência {#reference-apis}

* [API de ativação](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/api/package-summary.html)

* [API do Relatórios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/api/package-summary.html)

* [API do Relatórios Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/client/reporting/analytics/api/package-summary.html)

