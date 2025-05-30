---
title: Administração de comércio eletrônico genérico
description: A solução genérica AEM fornece métodos de gerenciamento das informações comerciais mantidas no repositório.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '2907'
ht-degree: 2%

---

# Administração de comércio eletrônico genérico {#administering-generic-ecommerce}

A solução genérica Adobe Experience Manager (AEM) fornece métodos de gerenciamento das informações comerciais mantidas no repositório (em vez de usar um mecanismo de comércio eletrônico externo). Isso inclui:

* [Produtos](/help/commerce/cif-classic/administering/concepts.md#products)
* [Variantes do produto](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [Catálogos](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [Promoções](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [Vouchers](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [Pedidos](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [Páginas de proxy](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>A instalação padrão do AEM inclui a implementação de comércio eletrônico genérico AEM (JCR).
>
>Ele é destinado a fins de demonstração ou como base para uma implementação personalizada de acordo com seus requisitos.

## Produtos e variações de produtos {#products-and-product-variations}

>[!NOTE]
>
>Os procedimentos a seguir se aplicam a Produtos e Variações de Produtos.

Antes de criar produtos, defina um [scaffold](/help/sites-authoring/scaffolding.md). Isso especifica os campos que você deve definir, os produtos e como eles são editados.

É necessário um scaffold para cada tipo de produto distinto. O suporte apropriado está associado aos produtos por meio de:

* caminho
* o produto pode fazer referência ao scaffold

>[!NOTE]
>
>A loja Geometrixx-Outdoors tem um único tipo de produto (e, portanto, um único scaffold):
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>O tipo de produto Geometrixx-Outdoors está ativo em:
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>Você pode criar uma definição de produto em qualquer lugar sob essa licença sem qualquer configuração adicional.

### Importando produtos {#importing-products}

#### Importação de produtos - Interface otimizada para toque {#importing-products-touch-optimized-ui}

1. Navegue até o console **Produtos**, via **Commerce**.
1. Usando o console **Produtos**, navegue até o local necessário.
1. Use o ícone **Importar Produtos** para abrir o assistente.

   ![Ícone Importar Produtos](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Especifique:

   * **Importador**

     O importador para o [provedor de comércio](/help/commerce/cif-classic/administering/concepts.md#commerce-providers) específico, por padrão `Geometrixx`.

   * **Origem**

     O arquivo que você deseja importar; você pode usar o navegador para selecionar um arquivo.

   * **Importação incremental**

     Indique se é uma importação incremental (em vez de completa).

   >[!NOTE]
   >
   >A importação incremental (do importador geometrixx-outdoor da amostra) opera ao nível do produto.
   >
   >Um importador personalizado pode ser definido para operar conforme necessário.

1. Selecione **Avançar** para importar os produtos; será mostrado um log das ações realizadas.

   >[!NOTE]
   >
   >Os produtos são importados para o local atual ou são relativos a ele.

   >[!NOTE]
   >
   >O uso repetido de **Próximo** e **Voltar** importa repetidamente as definições de produto. No entanto, como eles têm os mesmos SKUs, as informações existentes no repositório são substituídas.

1. Selecione **Concluído** para fechar o assistente.

#### Importação de produtos - Interface clássica {#importing-products-classic-ui}

1. Usando o console **Ferramentas**, abra a pasta **Commerce**.
1. Clique duas vezes para abrir o **Importador de Produtos**:

   ![Console do importador do produto](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. Especifique:

   * **Nome do Repositório**

     Os produtos são importados para:

     `/etc/commerce/products/<*store name*>/`

   * **Provedor do Commerce**

     O importador do seu [provedor de comércio](/help/commerce/cif-classic/administering/concepts.md#commerce-providers); por padrão, Geometrixx.

   * **Arquivo Source**

     O local no repositório do arquivo que você deseja importar.

   * **Importação incremental**

     Indique se é uma importação incremental (em vez de completa).

1. Clique em **Importar produtos**.

### Criação de informações do produto {#creating-product-information}

>[!NOTE]
>
>O gerenciamento padrão de produtos é básico, pois o conjunto de produtos Geometrixx-Outdoors foi mantido básico. A complexidade é baseada no [andaime](/help/sites-authoring/scaffolding.md) de produto, portanto, com seu próprio andaime de produto é possível obter uma edição mais sofisticada.

#### Criação de informações do produto - Interface otimizada para toque {#creating-product-information-touch-optimized-ui}

1. Usando o console **Produtos** (via **Commerce**), navegue até o local necessário.
1. Use o ícone **Criar** para selecionar (dependendo da estrutura e do local):

   * **Criar produto**
   * **Criar Variação de Produto**

   ![Ícone de criação com forma de adição](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. O assistente é aberto. Use as **Guias Básicas** e **Guias de Produto** para inserir os [atributos de produto](/help/commerce/cif-classic/administering/concepts.md#product-attributes) para o novo produto ou variante de produto.

   >[!NOTE]
   >
   >**Título** e **SKU** são o mínimo necessário para criar um produto ou uma variante.

1. Selecione **Criar** para salvar as informações.

>[!NOTE]
>
>Muitos produtos são oferecidos em uma variedade de cores e/ou tamanhos. As informações sobre o produto básico e as variantes de produto relacionadas podem ser gerenciadas no console **Produtos**.
>
>Os produtos e suas variantes são armazenados como uma estrutura em árvore, as informações do produto estão na parte superior, com as variantes abaixo (essa estrutura é aplicada pela interface do usuário).

### Edição de informações do produto {#editing-product-information}

>[!NOTE]
>
>As imagens do produto no geometrixx-outdoors são servidas de:
>
>`/etc/commerce/products/...`
>
>Isso significa que, por padrão, eles estão bloqueados pelo [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR), portanto, configure conforme necessário.

#### Edição de informações do produto - Interface otimizada para toque {#editing-product-information-touch-optimized-ui}

1. Usando o console **Produtos** (via **Commerce**), navegue até as informações do produto.
1. Usando:

   * [ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de seleção](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Selecione o ícone **Exibir dados do produto**:

   ![ícone exibir dados do produto - ícone de informações](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. Os [atributos do produto](/help/commerce/cif-classic/administering/concepts.md#product-attributes) são mostrados. Use **Editar** e **Concluído** para fazer alterações.

### Mostrando referências do produto {#showing-product-references}

#### Exibição de referências de produto - Interface otimizada para toque {#showing-product-references-touch-optimized-ui}

1. Usando o console **Produtos** (via **Commerce**), navegue até as informações do produto.
1. Abra o painel secundário para Referências com o ícone:

   ![ícone de seta dupla](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. Selecione o produto desejado - as atualizações do painel secundário mostrando os tipos de referência disponíveis:

   ![console de produtos com referências abertas](/help/sites-administering/assets/chlimage_1-88.png)

1. Clique no tipo de referência (por exemplo, Páginas de produto) para expandir a lista.
1. Selecione uma referência específica para poder mostrar as opções:

   * Navegar até a página do produto
   * Editar página do produto

   ![Painel de referência do Console de Produtos](/help/sites-administering/assets/chlimage_1-89.png)

### Pesquisar por produtos {#search-for-products}

1. Navegue até o console **Produtos**, via **Commerce**.
1. Abra o painel secundário para Pesquisar com o ícone:

   ![ícone de lupa](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. Várias facetas estão disponíveis para você pesquisar por produtos. Você pode usar apenas uma ou várias facetas para uma pesquisa. Os produtos encontrados aparecem:

   ![Dados do produto no console de produtos](/help/sites-administering/assets/chlimage_1-90.png)

1. Clicar/tocar em um produto o abre. Você também pode publicá-los ou visualizar os dados do produto.

#### Extensão da pesquisa {#extending-search}

Você pode modificar uma faceta existente ou adicionar novas, usando o CRXDE Lite:

1. Vá até:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. É possível editar, por exemplo, os tamanhos exibidos na página de pesquisa do produto. Clique no nó `sizegroup`.
1. Clique no nó `items` e depois clique no nó `propertypredicate`.
1. Você pode editar o `propertyValues`. Por exemplo, você pode adicionar XS ou XXL, ou remover um tamanho.
1. Clique em **Salvar tudo** e navegue até a página de pesquisa de produtos. As alterações devem ser exibidas.

### Vários Assets {#multiple-assets}

É possível adicionar vários ativos no componente do produto e especificar o ativo que você deseja que apareça na página do produto.

>[!NOTE]
>
>Tudo relacionado a vários ativos é feito com a interface otimizada para toque.

#### Adição de vários Assets {#adding-multiple-assets}

1. Navegue até o console **Produtos**, via **Commerce**.
1. Usando o console **Produtos**, navegue até o produto necessário.

   >[!NOTE]
   >
   >Você deve estar no nível do produto, não no nível da variante.

1. Selecione o ícone **Exibir Dados do Produto** com o modo de seleção ou ações rápidas.
1. Selecione o ícone Edit.
1. Role para **Adicionar**.

   ![Adicionando captura de tela de dados do produto](/help/sites-administering/assets/chlimage_1-91.png)

1. Selecione **Adicionar**. Um novo espaço reservado de ativo é exibido.
1. Selecionar **Alterar** abre uma caixa de diálogo que permite escolher um ativo.
1. Selecione o ativo que deseja adicionar.

   >[!NOTE]
   >
   >Os ativos que você pode selecionar são do [Assets](/help/assets/assets.md).

1. Selecione o ícone Concluído.

Dois ativos agora são armazenados no componente do produto. Você pode configurar qual aparece na página do produto. Funciona com um sistema de categorias. Primeiro, é necessário adicionar uma categoria aos ativos individuais:

1. Selecione **Exibir Dados Do Produto**.
1. Digite uma **Categoria de ativos** sob os ativos, por exemplo, `cat1` e `cat2`.

   >[!NOTE]
   >
   >Também é possível usar tags para categorias.

1. Selecione o ícone Concluído. Agora você precisa [implantar](#rolling-out-a-catalog) suas alterações.

Agora, seus ativos no componente do produto têm uma categoria. Você pode configurar qual categoria é exibida em três níveis diferentes:

* [Página do Produto](#product-page)
* [Catálogo](#catalog)
* [Console de produtos](#products-console)

>[!NOTE]
>
>Se você não definir categorias, o primeiro ativo será exibido na página do produto.

O mecanismo para selecionar a imagem a ser exibida é o seguinte:

1. Verifique se uma categoria está definida para a Página do produto.
1. Caso contrário, verifique se uma categoria está definida para o Catálogo.
1. Caso contrário, verifique se uma categoria está definida para o console Produtos.

>[!NOTE]
>
>Tanto para o nível do Catálogo quanto para o nível do Console de produtos, é necessário implantar as alterações para aplicar as modificações e ver a diferença na página do produto.

#### Página do Produto {#product-page}

1. Navegue até a página do produto.
1. **Editar** o componente do produto.
1. Digite a **Categoria da Imagem** escolhida ( `cat1` por exemplo).
1. Selecione **Concluído**. A página é atualizada e o ativo correto deve ser exibido.

#### Catálogo  {#catalog}

1. Navegue até o catálogo.
1. Selecione **Exibir Propriedades**.
1. Selecione **Editar**.
1. Selecione a guia **Assets**.
1. Digite a **Categoria do Ativo do Produto** necessária.
1. Selecione **Concluído**.
1. [Implantação](#rolling-out-a-catalog) suas alterações.

#### Console de produtos {#products-console}

1. Usando o console **Produtos**, navegue até o Produto necessário.
1. Selecione **Exibir Dados Do Produto**.
1. Selecione **Editar**.
1. Digite uma **Categoria de ativo padrão**.
1. Selecione **Concluído**.
1. [Implantação](#rolling-out-a-catalog) suas alterações.

### Publicar/Desfazer publicação de informações do produto {#publishing-unpublishing-product-information}

#### Publicar/desfazer publicação de informações do produto - Interface otimizada para toque {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>Geralmente, as informações do produto são publicadas pelas páginas que fazem referência a elas. Por exemplo, ao publicar a página X, que faz referência ao produto Y, o AEM pergunta se você também deseja publicar o produto Y.
>
>Para casos especiais, o AEM também oferece suporte à publicação direta dos dados do produto.

1. Usando o console **Produtos** (via **Commerce**), navegue até as informações do produto.
1. Usando:

   * [ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de seleção](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Selecione o ícone **Publish** ou **Cancelar publicação**, conforme necessário:

   ![ícone do mundo](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![ícone do mundo com uma cruz - sem sinal](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   As informações do produto são publicadas ou não, conforme apropriado.

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration lets you: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### Manipulador de eventos para atualizações de produtos {#event-handler-for-product-updates}

Há um Manipulador de eventos que registra um evento quando um produto é adicionado, editado ou excluído e quando uma página de produto é adicionada, editada ou excluída. Há os seguintes eventos OSGi:

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

Para os eventos `PRODUCT_*`, o caminho aponta para o produto base em `/etc/commerce/products`. Para os eventos `PRODUCT_PAGE_*`, o caminho aponta para o nó `cq:Page`.

Você pode vê-las no Console da Web em eventos OSGI ( `/system/console/events`), por exemplo:

![exemplos de eventos OSGI](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>Leia também [Manipulação de eventos no AEM](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/).

### Imagem com Links para adicionar ao carrinho {#image-with-add-to-cart-links}

O componente Imagem com links para adicionar ao carrinho permite adicionar rapidamente um produto ao carrinho criando um ponto de acesso vinculado a um produto em uma imagem.

Clicar no ponto de acesso abre uma caixa de diálogo que permite escolher o tamanho e a quantidade do produto.

1. Navegue até a página onde deseja adicionar o componente.
1. Arraste e solte o componente na página.
1. Arraste e solte uma imagem no componente do [navegador de ativos](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Você pode:

   * clique no componente e, em seguida, clique no ícone Editar
   * clique duas vezes lento

1. Clique no ícone de tela cheia.

   ![ícone de tela cheia](/help/sites-administering/assets/chlimage_1-92.png)

1. Clique no ícone Launch Map.

   ![ícone do mapa de inicialização](/help/sites-administering/assets/chlimage_1-93.png)

1. Clique em um dos ícones de forma.

   ![ícones de forma](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. Modifique e mova a forma conforme necessário.
1. Clique na forma.
1. Clicar no ícone de procura abre o [Seletor de ativos](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >Como alternativa, você pode digitar diretamente o caminho do produto, que deve estar no nível do produto, não no nível da variante.

   ![caminho do tipo](/help/sites-administering/assets/chlimage_1-94.png)

1. Clique no ícone de confirmação duas vezes e clique em sair da tela cheia.
1. Clique em algum lugar na página ao lado do componente. A página deve ser atualizada e você deve ver o seguinte símbolo na imagem:

   ![símbolo de adição](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. Alternar para o modo [visualização](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui).
1. Clique no ponto de acesso +. Uma caixa de diálogo é aberta, onde você pode escolher o tamanho e a quantidade do produto inserido no **Caminho**.

   ![exemplo de produto: poncho](/help/sites-administering/assets/chlimage_1-95.png)

1. Insira um tamanho e uma quantidade.
1. Clique no botão Add to cart. A caixa de diálogo é fechada.
1. Navegue até o carrinho. O produto deve estar aqui.

#### Opções de configuração {#configuration-options}

Você pode configurar a aparência da caixa de diálogo ao clicar no ponto de acesso:

1. Clique no componente e clique no ícone de configuração.

   ![ícone de configuração](/help/sites-administering/assets/chlimage_1-96.png)

1. Role para baixo. Há uma guia **ADICIONAR AO CARRINHO**.

   ![adicionar à guia do carrinho](/help/sites-administering/assets/chlimage_1-97.png)

1. Clique em **ADICIONAR AO CARRINHO**. Há três opções de configuração que podem ser usadas.

   ![opções de configuração](/help/sites-administering/assets/chlimage_1-98.png)

1. Clique no ícone Concluído.

## Catálogos {#catalogs}

### Gerar um catálogo {#generating-a-catalog}

#### Geração de um catálogo - Interface otimizada para toque {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>O catálogo faz referência aos dados do produto.

Para gerar um catálogo:

1. Abra o console Sites (por exemplo, [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. Navegue até o local onde deseja criar a página.
1. Para abrir a lista de opções, use o ícone **Criar**:

   ![ícone de criação](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. Na lista, selecione **Criar catálogo**. O assistente Criar catálogo é aberto.

   ![criar assistente de catálogo](/help/sites-administering/assets/chlimage_1-99.png)

1. Navegue até o Blueprint do catálogo necessário.
1. Selecione o botão **Selecionar** e clique no Blueprint do catálogo necessário.
1. Selecione **Próximo**.

   ![assistente de propriedades do catálogo](/help/sites-administering/assets/chlimage_1-100.png)

1. Digite um **Título** e um **Nome**.
1. Selecione o botão **Criar**. O catálogo é criado e uma caixa de diálogo é aberta.

   ![caixa de diálogo criada pelo catálogo](/help/sites-administering/assets/chlimage_1-101.png)

1. Selecionar o botão **Concluído** o levará de volta ao console Sites, onde você poderá ver seu catálogo.

   Tocar/clicar no botão **Abrir Catálogo** abre seu catálogo (por exemplo, `http://localhost:4502/editor.html/content/test-catalog.html`).

#### Gerar um catálogo - Interface clássica {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>O catálogo faz referência aos [Dados do Produto](#products-and-product-variants).

1. Usando o console **Sites**, navegue até o **Blueprint do Catálogo** e, em seguida, até o Catálogo Básico.

   Por exemplo:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. Crie uma página usando o modelo **Blueprint de Seção**.

   Por exemplo, `Swimwear`.

1. Abra a nova página `Swimwear` e clique em **Editar blueprint**. A caixa de diálogo **Propriedades** é aberta para que você possa configurar a seleção de **Produtos**.

   Por exemplo, abra o campo **Tags/Palavras-chave** para selecionar Atividade e Natação na seção Geometrixx-Outdoors.

1. Clique em **OK** para salvar suas propriedades. Exemplos de produtos são mostrados em **Critérios de Seleção de Produtos** na página do blueprint.
1. Clique em **Implantar Alterações...**, selecione **Implantar página e todas as subpáginas** e clique em **Avançar** e depois em **Implantação**. Depois que a implantação for concluída com êxito, o indicador **Status** será exibido em verde.
1. Agora você pode clicar em **Fechar** e verificar a nova seção de catálogo; por exemplo, em e sob:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. Novamente, na página de blueprints, clique em **Editar Blueprint** e, na caixa de diálogo **Propriedades**, abra a guia **Página Gerada**. No campo Lista de banners, selecione a imagem que deseja mostrar; por exemplo, `summer.jpg`
1. Clique em **OK** para salvar suas propriedades; as informações do banner são mostradas nos **Critérios de Seleção do Produto** na página do blueprint.
1. Implante essas novas alterações.

### Lançando um catálogo {#rolling-out-a-catalog}

#### Implantação de um catálogo - interface otimizada para toque {#rolling-out-a-catalog-touch-optimized-ui}

Para implantar um catálogo:

1. Navegue até o console **Catálogos**, via **Commerce**.
1. Navegue até o catálogo que deseja implantar.
1. Usando:

   * [ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de seleção](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Selecione o ícone **Alterações de implantação**:

   ![implantação](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. No assistente, defina a implantação conforme necessário e clique em **Implantar Alterações**.
1. Uma caixa de diálogo é aberta. Selecione **Concluído** quando o processo for concluído.

#### Implantação de um catálogo - Interface clássica {#rolling-out-a-catalog-classic-ui}

Para implantar um catálogo:

1. Navegue até o catálogo que deseja implantar. Por exemplo:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. Clique em **Implantar alterações...**
1. Defina a implantação conforme necessário.
1. Clique em **Implantação**.

### Importador de blueprint {#blueprint-importer}

#### Importador de blueprint - Interface otimizada para toque {#blueprint-importer-touch-optimized-ui}

1. Navegue até o console **Catálogos**, via **Commerce**.
1. Navegue até o local onde deseja importar o blueprint do catálogo.
1. Selecione o ícone **Importar blueprints**.

   ![Ícone Importar blueprints](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. No assistente, selecione o Source conforme necessário e clique em **Avançar**.

   ![assistente de blueprint](/help/sites-administering/assets/chlimage_1-102.png)

1. Selecione **Concluído** quando a importação for concluída.

#### Importador de blueprint - Interface clássica {#blueprint-importer-classic-ui}

1. Usando o console **Ferramentas**, navegue até **Commerce**.

   Por exemplo:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. Abra o **Importador de blueprint de catálogo**.
1. Defina a importação conforme necessário.
1. Clique em **Importar blueprints do catálogo**.

## Promoções {#promotions}

### Criação de uma promoção {#creating-a-promotion}

#### Criação de uma promoção - Interface clássica {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>O exemplo a seguir trata de uma promoção realizada diretamente em uma [campanha](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md), que é usada para comprovantes.
>
>Uma promoção também pode estar em uma [experiência](/help/sites-authoring/personalization.md) em uma campanha.
>
>Para obter mais informações, consulte [Promoções e Cupons](#promotions-and-vouchers).

1. Abra o console **Sites** da instância do autor.
1. No painel esquerdo, selecione a **Campanha** necessária.
1. Clique em **Novo**, selecione o modelo **Promoção** e especifique um **Título** (e **Nome**, se necessário) para o novo cupom.
1. Clique em **Criar**. A nova página de promoção é exibida no painel direito.

1. Edite as **Propriedades** da seguinte maneira:

   * abrindo a página e clicando no botão Editar para abrir a caixa de diálogo Propriedades
   * selecionando a página no console Sites e, em seguida, usando o menu de contexto (geralmente o botão direito do mouse) para selecionar **Propriedades...** e abrir a caixa de diálogo propriedades

   Especifique o **Tipo de Promoção**, **Tipo de Desconto**, **Valor de Desconto** e quaisquer outros campos conforme necessário.

1. Clique em **OK** para salvar.

1. Agora você pode ativar sua promoção para que os compradores possam vê-la na instância de publicação.

## Vouchers {#vouchers}

### Criação de um voucher {#creating-a-voucher}

#### Criação de um voucher - Interface clássica {#creating-a-voucher-classic-ui}

1. Abra o console **Sites** da instância do autor.
1. No painel esquerdo, selecione a **Campanha** necessária.
1. Clique em **Novo**, selecione o modelo **Voucher** e especifique um **Título** (e **Nome**, se necessário) para o seu novo comprovante.
1. Clique em **Criar**. A nova página de voucher é mostrada no painel direito.

1. Abra a nova página do cupom com um clique duplo, clique em **Editar** e configure as informações conforme necessário.
1. Clique em **OK** para salvar.

1. Agora é possível ativar o cupom, para que os compradores possam usá-lo em seus carrinhos na instância de publicação.

### Remoção de Cupons {#removing-vouchers}

#### Remoção de vouchers - Interface clássica {#removing-vouchers-classic-ui}

Para tornar um voucher indisponível para os clientes, você pode:

* Desativar o cupom - ele permanece disponível no ambiente de criação para que você possa reativá-lo posteriormente.
* Excluí-lo completamente.

Ambas as ações podem ser realizadas no console **Sites**.

### Modificação de Cupons {#modifying-vouchers}

#### Modificação de vouchers - Interface clássica {#modifying-vouchers-classic-ui}

Para alterar as propriedades de um cupom ou promoção, clique duas vezes nele no console **Sites** e clique em **Editar**. Depois de salvá-lo, você deve ativá-lo para que as alterações sejam enviadas para as instâncias de publicação.

### Adicionar vouchers a um Carrinho {#adding-vouchers-to-a-cart}

Para permitir que os usuários adicionem vouchers aos seus carrinhos, você pode usar o componente **Vouchers** integrado (categoria Commerce). Adicione isso à mesma página de onde o carrinho é exibido (mas isso não é obrigatório). O componente de vouchers é apenas um formulário no qual o usuário pode inserir um código de voucher, é o componente do carrinho de compras que realmente mostra a lista de vouchers aplicados e seu desconto.

No site de demonstração (Geometrixx Outdoors - Inglês), você pode ver o formulário de voucher na página do carrinho, sob o carrinho de compras real.

## Pedidos {#orders}

>[!NOTE]
>
>Deve-se lembrar que o AEM pronto para uso não tem ações necessárias para a funcionalidade padrão relacionada a pedidos, como devolver mercadorias, atualizar o status do pedido, fazer o atendimento, gerar guias de remessa. Ela tem como objetivo principal uma visualização de tecnologia.
>
>O Order Management genérico no AEM foi mantido básico; os campos disponíveis no assistente dependem do scaffold:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>Se você criar um scaffold personalizado, poderá armazenar mais informações do pedido.

>[!NOTE]
>
>O console de pedidos expõe as informações de pedido do fornecedor, que nunca são publicadas.
>
>As informações sobre pedidos de clientes são mantidas nos diretórios iniciais e são expostas pelo Histórico de pedidos da conta. Essas informações são publicadas junto com o restante do diretório inicial.

### Criando Informações da Ordem {#creating-order-information}

#### Criação de informações do pedido - Interface otimizada para toque {#creating-order-information-touch-optimized-ui}

1. Usando o console **Pedidos**, navegue até o local necessário.
1. Use o ícone **Criar** para selecionar **Criar pedido**.

   ![Ícone de criação com forma de adição](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. O assistente é aberto. Use as guias **Básico**, **Conteúdo**, **Pagamento** e **Atendimento** para inserir as [informações sobre o novo pedido](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. Selecione **Criar** para salvar as informações.

### Editando Informações da Ordem {#editing-order-information}

#### Edição de informações da ordem - Interface otimizada para toque {#editing-order-information-touch-optimized-ui}

1. Usando o console **Pedidos**, navegue até o pedido.
1. Usando:

   * [ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de seleção](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Selecione o ícone **Exibir dados do pedido**:

   ![ícone de informações](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. As [informações do pedido](/help/commerce/cif-classic/administering/concepts.md#order-information) são mostradas. Use **Editar** e **Concluído** para fazer alterações.

