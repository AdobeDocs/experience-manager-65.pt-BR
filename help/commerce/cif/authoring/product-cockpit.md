---
title: Cockpit do produto
description: Trabalhar com o Cockpit de produtos, que fornece uma visão geral unificada de catálogos de produtos vinculados e conteúdo associado.
exl-id: 05ef2604-1d52-4397-a696-0b64717cc3cc
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 1%

---

# Cockpit do produto {#product-cockpit}

## Visão geral {#overview}

O Product Cockpit fornece uma visão geral unificada de catálogos de produtos vinculados e conteúdo associado. Todo o conteúdo associado tem links para acessá-lo rapidamente a partir do cockpit.

Os dados por etapas do produto incluem qualquer mutação no futuro, como novas categorias, produtos ou propriedades atualizadas.

>[!NOTE]
>
>O termo catálogo de produtos é intercambiável com lojas de comércio, visualizações de loja e expressões semelhantes.

## Configuração {#configuration}

Os catálogos de produtos devem ser configurados no AEM. Consulte [configurando armazenamento e catálogos](/help/commerce/cif/getting-started.md#catalog) para obter mais informações.

A habilitação de recursos de catálogo em etapas requer autenticação. Consulte [Introdução](/help/commerce/cif/getting-started.md) para obter mais informações.

>[!NOTE]
>
>Os recursos de catálogo por etapas só estão disponíveis com conectores do Adobe Commerce e de terceiros que oferecem suporte à autenticação baseada em token.

## Abrindo a cabine do produto {#opening-product-cockpit}

A maneira mais fácil de acessar o Cockpit do produto é por meio do menu &quot;Commerce&quot; no menu principal do AEM. Também é possível usar o Omnisearch (pesquisa para Commerce) ou abrir o `https://<yourAEMInstance>/commerce.html`.

![Menu AEM](/help/commerce/cif/assets/aem-menu.png)

## Procurar Catálogos de produtos {#browsing-product-catalogs}

O Cockpit do produto é organizado de forma hierárquica, seguindo a estrutura do catálogo de produtos. O primeiro nível mostra o nível raiz do catálogo de todos os catálogos de produtos configurados, incluindo as informações meta do back-end de comércio.

![Catálogos configurados](/help/commerce/cif/assets/catalog-overview.png)

Clicar em uma categoria carrega os filhos da categoria clicada.

![Filhos da categoria](/help/commerce/cif/assets/catalog-category-children.png)

Clicar em um produto carrega variações de produto, se disponíveis.

![Variações de produto](/help/commerce/cif/assets/catalog-product-variation.png)

>[!NOTE]
>
>Os dados do catálogo de produtos no AEM são dados recuperados em tempo real pelo endpoint de comércio configurado. Nenhum dado de catálogo de produtos é armazenado no AEM.

## Pesquisando Catálogos de Produtos {#searching-product-catalog}

Uma pesquisa de texto completo no catálogo de produtos completo é fornecida na guia de filtro à esquerda para localizar produtos rapidamente.

![pesquisar](/help/commerce/cif/assets/search-cockpit.png)

## Catálogo de produtos por etapa de navegação {#staged-product-catalogs}

Por padrão, o cockpit de produtos mostra dados do catálogo de produtos em tempo real. O uso do &quot;CATÁLOGO PREPARADO&quot; na guia de filtro à esquerda carrega o catálogo de produtos para qualquer data selecionada.

![catálogo em etapas](/help/commerce/cif/assets/staged-cockpit.png)

## Propriedades do catálogo de produtos {#catalog-properties}

Clicar no ícone de propriedades de um produto ou categoria abre a visualização de propriedade do objeto selecionado. Abrir propriedades de uma variante de produto é igual a abrir as principais propriedades do produto.

### Guias Comércio {#tabs}

As guias geral e variante mostram propriedades de comércio predefinidas que vêm do back-end de comércio. Esses dados (incluindo variantes) são dados somente leitura no AEM, pois o sistema de registro é o back-end de comércio. A guia de variante é exibida apenas para produtos com variantes e mostra uma lista de todas as variantes.

![propriedades do catálogo](/help/commerce/cif/assets/catalog-properties.png)

### Guias de conteúdo do AEM {#content-tabs}

Essas guias, agrupadas por tipos de conteúdo AEM (Fragmentos de experiência, Fragmentos de conteúdo, Ativos associados), mostram o conteúdo AEM associado ao objeto de comércio. A ação &quot;Exibir detalhes&quot; abre uma nova guia do navegador com o conteúdo selecionado.

![propriedades de conteúdo](/help/commerce/cif/assets/content-properties.png)
