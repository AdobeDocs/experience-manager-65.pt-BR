---
title: Uso do seletor de produto e categoria da CIF
description: Saiba como usar o seletor de produto e categoria da CIF nos componentes de comércio do cliente para oferecer suporte a autores e profissionais de marketing que trabalham com eficiência com dados de produtos e catálogos de comércio.
sub-product: Commerce
topics: Development
version: Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Seletores de criação de conteúdo e comércio de AEM {#cif-pickers}

A criação de conteúdo e comércio do AEM fornece um conjunto de ferramentas de criação para ajudar os autores e profissionais de marketing do AEM a trabalhar com eficiência com dados e catálogos de produtos comerciais. O seletor de produtos e o seletor de categorias fazem parte do complemento CIF e são usados pelos Componentes principais da CIF. Os projetos podem usar esses seletores em qualquer caixa de diálogo de componente para selecionar produtos ou categorias.

## Seletor de produtos {#product-picker}

Para usar o seletor de produtos em um componente de projeto, um desenvolvedor deve adicionar `commerce/gui/components/common/cifproductfield` para uma caixa de diálogo de componente. Por exemplo, use o seguinte para o cq:dialog:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

O campo produto permite a navegação até o produto que um usuário deseja selecionar por meio das diferentes visualizações. Por padrão, o campo product retorna a ID do produto, mas pode ser configurado usando o `selectionId` atributo.

O campo seletor de produto oferece suporte às seguintes propriedades opcionais:

- selectionId (id, uid, sku, slug, combineSlug, combineSku) - permite que você escolha o atributo de produto a ser retornado pelo seletor (padrão = id). Usar sku retorna o sku do produto selecionado, ao usar o combineSku e retorna uma string como base#variant com os skus do produto base e a variante selecionada, ou um único sku se um produto base estiver selecionado.
- filtro (folderOrProduct, folderOrProductOrVariant): filtra o conteúdo a ser renderizado pelo seletor ao navegar na árvore do produto. folderOrProduct - renderiza pastas e produtos. folderOrProductOrVariant - renderiza pastas, produtos e variantes de produtos. Se um produto ou variante de produto for renderizado, também se tornará selecionável no seletor. (padrão = folderOrProduct)
- múltiplo (true, false) - habilita a seleção de um ou vários produtos (padrão = false)
- emptyText - para configurar o valor de texto vazio do campo do seletor

Além disso, as propriedades padrão do campo de diálogo, como `name`, `fieldLabel`ou `fieldDescription`, também são compatíveis.

>[!CAUTION]
>
>A variável `cifproductfield` exige que o `cif.shell.picker` clientlib. Para adicionar uma clientlib a uma caixa de diálogo, é possível usar a propriedade extraClientlibs.
>[!CAUTION]
>
>A partir da versão 2.0.0 dos Componentes principais da CIF, o suporte para `id` foi removido e substituído por `uid`. O Adobe recomenda usar `sku` ou `slug` como identificador do produto. O Adobe continua a oferecer suporte `id` somente para projetos que usam os Componentes principais da CIF versão 1.x.

Um exemplo completo de funcionamento do `cifproductfield` pode ser encontrado no [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) projeto. Consulte também [Personalização de caixas de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) da documentação dos Componentes principais do AEM.

## Seletor de Categoria {#category-picker}

O seletor de categorias pode ser usado em uma caixa de diálogo de componente, bem como de maneira semelhante ao seletor de produtos.

O trecho a seguir pode ser usado em uma configuração cq:dialog:

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

O campo do seletor de categoria é compatível com as seguintes propriedades opcionais:

- selectionId(id, uid, slug, urlPath, idAndUrlPath) _(obsoleto)_, uidAndUrlPath _(obsoleto)_) - permite escolher o atributo de categoria a ser retornado pelo seletor (padrão = id).
- multiple (true, false) - habilita a seleção de uma ou várias categorias (padrão = false)

Além disso, as propriedades padrão do campo de diálogo, como `name`, `fieldLabel`ou `fieldDescription` também são compatíveis.

>[!CAUTION]
>
>Igual ao `cifproductfield` componente o `cifcategoryfield` O componente também exige que o `cif.shell.picker` clientlib. Para adicionar uma clientlib a uma caixa de diálogo, você pode usar o `extraClientlibs` propriedade. Consulte [Personalização de caixas de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) da documentação dos Componentes principais do AEM.
>[!CAUTION]
>
>A partir da versão 2.0.0 dos Componentes principais da CIF, o suporte para `id` foi removido e substituído por `uid`. O Adobe recomenda usar `uid` ou `urlPath` como identificador de categoria. O Adobe continua a oferecer suporte `id` &amp; `idAndUrlPath` somente para projetos que usam os Componentes principais da CIF versão 1.x.

Um exemplo completo de funcionamento do `cifcategoryfield` pode ser encontrado no [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) projeto.
