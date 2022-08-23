---
title: Uso do seletor de produto e categoria da CIF
description: Saiba como usar o seletor de produto e categoria da CIF em seus componentes de comércio com o cliente para auxiliar autores e profissionais de marketing a trabalhar com dados de produtos e catálogos de comércio de maneira eficiente.
sub-product: Commerce
topics: Development
version: Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 1e7c3748-92b5-45f1-8dd9-f1816e3e34aa
source-git-commit: dceb187ba28ad7c377e98d29d6c815fe37e23077
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Seletores de criação de conteúdo e comércio AEM {#cif-pickers}

A criação de conteúdo e comércio AEM oferece um conjunto de ferramentas de criação para ajudar AEM autores e profissionais de marketing a trabalharem com dados e catálogos de produtos comerciais. O Seletor de produto e o Seletor de categoria fazem parte do complemento CIF e são usados pelos Componentes principais da CIF. Os projetos podem usar esses seletores em qualquer caixa de diálogo de componente para selecionar produtos ou categorias.

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

O campo de produto permite navegar até o produto que um usuário deseja selecionar por meio das diferentes visualizações. Por padrão, o campo do produto retorna a ID do produto, mas pode ser configurado usando a variável `selectionId` atributo.

O campo seletor de produto oferece suporte às seguintes propriedades opcionais:

- selectionId (id, uid, sku, lesma, Combinar, CombinarSku) - permite escolher o atributo do produto a ser retornado pelo seletor (padrão = id). Usar o sku retorna o sku do produto selecionado, enquanto usa o CombinationSku e retorna uma string como base#variant com os SKUs do produto base e a variante selecionada, ou um único sku se um produto base for selecionado.
- filter (folderOrProduct, folderOrVariant) - filtra o conteúdo a ser renderizado pelo seletor ao navegar na árvore do produto. folderOrProduct - renderiza pastas e produtos. folderOrProductOrVariant - renderiza pastas, produtos e variantes de produtos. Se um produto ou uma variante de produto for renderizada, ela também poderá ser selecionada no seletor. (padrão = folderOrProduct)
- vários (true, false) - habilita a seleção de um ou vários produtos (padrão = false)
- emptyText - para configurar o valor de texto vazio do campo do seletor

Além disso, as propriedades padrão de campos de diagnóstico, como `name`, `fieldLabel`ou `fieldDescription` também são compatíveis.

>[!CAUTION]
>
>O `cifproductfield` O componente exige que `cif.shell.picker` clientlib. Para adicionar uma clientlib a uma caixa de diálogo, você pode usar a propriedade extraClientlibs.
>[!CAUTION]
>
>A partir da versão 2.0.0 dos Componentes principais da CIF, o suporte para o `id` foi removido e substituído por `uid`. Recomendamos usar `sku` ou `slug` como identificador de produto. Continuamos a apoiar `id` somente para projetos que usam os Componentes principais da CIF versão 1.x.

Um exemplo completo de trabalho da `cifproductfield` podem ser encontradas no [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) projeto. Consulte também [Personalização de caixas de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) da documentação dos Componentes principais do AEM.

## Seletor de categoria {#category-picker}

O seletor de categoria pode ser usado em uma caixa de diálogo de componente, bem como de maneira semelhante ao seletor de produto.

O seguinte trecho pode ser usado em uma configuração cq:dialog:

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

O campo do seletor de categoria oferece suporte às seguintes propriedades opcionais:

- selectionId(id, uid, lesma, urlPath, idAndUrlPath _(obsoleto)_, uidAndUrlPath _(obsoleto)_) - permite escolher o atributo de categoria a ser retornado pelo seletor (padrão = id).
- várias (true, false) - habilita a seleção de uma ou várias categorias (padrão = false)

Além disso, as propriedades padrão de campos de diagnóstico, como `name`, `fieldLabel`ou `fieldDescription` também são compatíveis.

>[!CAUTION]
>
>Igual a `cifproductfield` componente `cifcategoryfield` também exige que o `cif.shell.picker` clientlib. Para adicionar uma clientlib a uma caixa de diálogo, você pode usar o `extraClientlibs` propriedade. Consulte [Personalização de caixas de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) da documentação dos Componentes principais do AEM.
>[!CAUTION]
>
>A partir da versão 2.0.0 dos Componentes principais da CIF, o suporte para o `id` foi removido e substituído por `uid`. Recomendamos usar `uid` ou `urlPath` como identificador de categoria. Continuamos a apoiar `id` &amp; `idAndUrlPath` somente para projetos que usam os Componentes principais da CIF versão 1.x.

Um exemplo completo de trabalho da `cifcategoryfield` podem ser encontradas no [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) projeto.
