---
title: Cockpit do produto
description: Trabalhar com o Cockpit do produto
exl-id: 05ef2604-1d52-4397-a696-0b64717cc3cc
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 1%

---

# Cockpit do produto {#product-cockpit}

## Visão geral {#overview}

O Cockpit de produto fornece uma visão geral unificada de catálogos de produtos vinculados e conteúdo associado. Todo o conteúdo associado tem links para acessá-lo rapidamente do cockpit.

Os dados de produtos preparados incluem qualquer mutação no futuro, como novas categorias, produtos ou propriedades atualizadas.

>[!NOTE]
>
>O termo catálogo de produto é intercambiável com comércio, loja, loja e expressões semelhantes.

## Configuração {#configuration}

Os catálogos de produtos precisam ser configurados no AEM. Consulte [configuração de lojas e catálogos](/help/commerce/cif/getting-started.md#catalog) para obter mais informações.

Habilitar recursos de catálogo preparado requer autenticação. Consulte [Introdução](/help/commerce/cif/getting-started.md) para obter mais informações.

>[!NOTE]
>
>Os recursos do catálogo preparo só estão disponíveis com conectores Adobe Commerce e de terceiros que oferecem suporte à autenticação baseada em token.

## Abrir a caixa do produto {#opening-product-cockpit}

A maneira mais fácil de acessar o Cockpit do produto é através do menu &quot;Comércio&quot; AEM menu principal. Também é possível usar Omnisearch (search for Commerce) ou abrir `https://<yourAEMInstance>/commerce.html`.

![Menu AEM](/help/commerce/cif/assets/aem-menu.png)

## Como navegar nos catálogos de produtos {#browsing-product-catalogs}

O Cockpit de Produtos é organizado de forma hierárquica, seguindo a estrutura do catálogo de produtos. O primeiro nível mostra o nível raiz do catálogo de todos os catálogos de produtos configurados, incluindo informações meta do backend de comércio.

![Catálogos configurados](/help/commerce/cif/assets/catalog-overview.png)

Clicar em uma categoria carregará os filhos da categoria clicada.

![Filhos de categoria](/help/commerce/cif/assets/catalog-category-children.png)

Clicar em um produto carregará variações de produto, se disponíveis.

![Alterações do produto](/help/commerce/cif/assets/catalog-product-variation.png)

>[!NOTE]
>
>Os dados do catálogo de produtos no AEM são dados recuperados em tempo real por meio do endpoint de comércio configurado. Nenhum dado de catálogo de produtos é armazenado no AEM.

## Como pesquisar catálogos de produtos {#searching-product-catalog}

Uma pesquisa de texto completo sobre o catálogo de produtos completo é fornecida na guia do filtro à esquerda para encontrar produtos rapidamente.

![pesquisa](/help/commerce/cif/assets/search-cockpit.png)

## Navegando pelo catálogo de produtos preparados {#staged-product-catalogs}

Por padrão, o cockpit de produtos mostra dados do catálogo de produtos ao vivo. Usar o &quot;CATÁLOGO PREPARADO&quot; na guia do filtro à esquerda carregará o catálogo de produtos para qualquer data selecionada.

![catálogo preparado](/help/commerce/cif/assets/staged-cockpit.png)

## Propriedades do Catálogo de Produtos {#catalog-properties}

Clicar no ícone de propriedades de um produto ou categoria abrirá a visualização de propriedade do objeto selecionado. Propriedades abertas de uma variante de produto são iguais para abrir as propriedades principais do produto.

### Guias de comércio {#tabs}

As guias geral e variante mostram propriedades de comércio predefinidas que vêm do backend de comércio. Esses dados (incl. variants) são dados somente leitura no AEM, pois o sistema de registro é o backend de comércio. A guia variante é exibida somente para produtos com variantes e mostra uma lista de todas as variantes.

![propriedades do catálogo](/help/commerce/cif/assets/catalog-properties.png)

### Guias Conteúdo AEM {#content-tabs}

Essas guias, agrupadas por tipos de conteúdo AEM (Fragmentos de experiência, Fragmentos de conteúdo, Ativos associados), mostram AEM conteúdo associado ao objeto de comércio. A ação &quot;Exibir detalhes&quot; abre uma nova guia do navegador com o conteúdo selecionado.

![propriedades de conteúdo](/help/commerce/cif/assets/content-properties.png)
