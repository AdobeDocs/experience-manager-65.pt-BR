---
title: Criação de experiências comerciais
description: Experiências comerciais de trabalho
exl-id: 2db51bd7-8fc7-4ae8-8d6f-e5035fbe954d
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# Criação de experiências comerciais {#authoring-commerce-experiences}

## Visão geral {#overview}

O complemento CIF amplia AEM criação com recursos específicos do comércio. Isso permite que os autores criem e gerenciem experiências relacionadas ao comércio com eficiência, obtendo acesso aos dados e ao conteúdo do produto sem deixar o contexto.

## Seletores {#pickers}

Os seletores de produto e categoria são caixas de diálogo modais da interface do usuário que oferecem uma maneira confortável para os autores de AEM encontrarem e selecionarem produtos ou categorias quando necessário. Componentes principais, associação de conteúdo e modelos de produto são as áreas típicas com configurações que exigem dados de catálogo de produtos. Os seletores são compatíveis com várias opções de configuração, como seleção múltipla, seleção de variação e pré-seleção de valores.

### Seletor de produtos {#product-picker}

Esse seletor oferece a navegação pela estrutura do catálogo ou a pesquisa de texto completo para localizar o produto. Os produtos com variação oferecem um ícone de pasta na coluna &quot;Tipo&quot;. Clicar no ícone de pasta abre as variações do produto selecionado.

![Seletor de produto](/help/commerce/cif/assets/authoring/product-picker.png)

Clicar na categoria principal levará o autor de volta ao nível do produto.

![Seletor de produto](/help/commerce/cif/assets/authoring/product-picker-variation.png)

**Exemplo de teaser de produto**

![Componente Teaser sem seleção](/help/commerce/cif/assets/authoring/teaser_component_without_selection.png)

A caixa de diálogo de configuração desse componente requer um produto. A CIF usa o SKU como o identificador de produto. Os autores podem inserir o sku manualmente ou clicar no ícone da pasta para abrir o seletor de produtos. Após selecionar e fechar o seletor, a caixa de diálogo do componente mostra o nome do produto selecionado

![Componente Teaser com seleção](/help/commerce/cif/assets/authoring/teaser_component_with_selection.png)

### Seletor de categoria {#category-picker}

Esse seletor oferece navegar pela estrutura do catálogo para localizar a categoria.

![Seletor de categoria](/help/commerce/cif/assets/authoring/category-picker.png)

**Exemplo de carrossel de categoria**

![Componente carrossel sem seleção](/help/commerce/cif/assets/authoring/carousel_component_without_selection.png)

A caixa de diálogo de configuração desse componente requer 1 : n categorias. A CIF usa a UID/ID como o identificador de categoria. Os autores podem inserir a UID manualmente ou clicar no ícone da pasta para abrir o seletor de categorias. Depois de selecionar e fechar o seletor, a caixa de diálogo do componente mostra o nome da categoria selecionada.

![Componente carrossel com seleção](/help/commerce/cif/assets/authoring/carousel_component_with_selection.png)

## Editor universal {#universal-editor}

O Editor Universal é estendido com recursos para acessar os dados do produto em tempo real e o conteúdo associado do produto.

### Acesso aos dados do produto {#access-product-data}

A guia &quot;Ativos&quot; no painel lateral do editor oferece acesso aos dados do produto ao selecionar o tipo &quot;Produtos&quot;. Os dados são obtidos ao vivo do ponto de extremidade de comércio configurado. O filtro é uma pesquisa de texto completo no endpoint de comércio para localizar produtos específicos.

![Painel lateral de dados do produto](/help/commerce/cif/assets/authoring/products-side-panel.png)

Analógico a ativos, os produtos podem ser adicionados em uma página (que cria um componente de teaser de produto como padrão) ou em componentes (atualmente compatíveis são o teaser de produto e o carrossel de produtos).

### Adição de links em campos de texto usando o RTE {#rte}

As páginas do catálogo de produtos da CIF são páginas virtuais renderizadas dinamicamente. Assim, não é possível incorporar hiperlinks como para páginas de AEM comuns. A CIF adiciona uma nova ação &quot;Links de comércio&quot; ao RTE (Editor de Rich Text). Essa ação funciona exatamente como a ação &quot;Hiperlink&quot; normal, mas permite que os autores selecionem um produto ou categoria usando os seletores.

![RTE](/help/commerce/cif/assets/authoring/RTE.png)

    >[!OBSERVAÇÃO]
    >
    > Se a categoria e o produto forem selecionados, o produto será obtido.

Isso cria um link de espaço reservado que é substituído por um link real quando a página é renderizada.

### Acesso ao conteúdo associado do produto {#associated-content}

Se o Editor Universal reconhecer produtos 1:n em uma página, o painel lateral mostrará automaticamente a guia &quot;Conteúdo de comércio associado&quot;. Essa guia permite que os autores acessem rapidamente AEM conteúdo que foi marcado com o produto (Consulte [enriquecer dados do produto com conteúdo de AEM associado](./enrich-product-associated-content.md) para obter mais informações). Esta guia oferece menus suspensos para filtrar por tipo de conteúdo e produtos específicos se vários produtos estiverem na página. Usar o conteúdo funciona exatamente como usar o conteúdo da guia &quot;Ativos&quot;.

![Painel lateral de dados do produto](/help/commerce/cif/assets/authoring/associated-commerce-content-tab.png)

### Visualizar dados de produto preparados {#staged-data}

O modo Timewarp no editor permite que os autores visualizem e naveguem em uma experiência AEM com dados de catálogo de produtos preparados com base na data do Timewarp.

![Timewarp  ](/help/commerce/cif/assets/authoring/timewarp.png)

Os componentes mostrarão um indicador visual se a data usada for preparada.

![Indicador de etapas](/help/commerce/cif/assets/authoring/staged-indicator.png)

## Omnisearch {#omnisearch}

O uso do Omnisearch é uma maneira fácil de os profissionais encontrarem dados AEM de conteúdo e catálogo de produtos usando a pesquisa de texto completo. O Omnisearch executará a pesquisa de texto completo no AEM e no backend de comércio para localizar objetos de catálogo de produtos no back-end de comércio e conteúdo AEM. AEM resultados também incluem conteúdo que foi marcado com dados de produto/categoria.

![Omnisearch](/help/commerce/cif/assets/authoring/omnisearch.png)

O resultado é agrupado por tipo.

    >[!OBSERVAÇÃO]
    >
    > Pesquisa de texto completo no Omnisearch não oferece suporte aos Fragmentos de conteúdo associados. Use SKU ou UID para localizar Fragmentos de conteúdo associados.
