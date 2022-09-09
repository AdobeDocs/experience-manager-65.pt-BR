---
title: Administração de eCommerce genérico
seo-title: Administering generic eCommerce
description: A solução genérica AEM fornece métodos para gerenciar as informações comerciais contidas no repositório.
seo-description: The AEM generic solution provides methods of managing the commerce information held within the repository.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '2910'
ht-degree: 4%

---

# Administração de eCommerce genérico {#administering-generic-ecommerce}

A solução genérica de AEM fornece métodos para gerenciar as informações comerciais contidas no repositório (em vez de usar um mecanismo de comércio externo). Isso inclui:

* [Produtos](/help/commerce/cif-classic/administering/concepts.md#products)
* [Variantes do produto](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [Catálogo(s)](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [Promoções](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [Vouchers](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [Pedidos](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [Páginas de proxy](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>A instalação padrão do AEM inclui a implementação genérica do AEM (JCR) eCommerce.
>
>Atualmente, isso é destinado a fins de demonstração ou como base básica para uma implementação personalizada de acordo com suas necessidades.

## Produtos e variações de produtos {#products-and-product-variations}

>[!NOTE]
>
>Os procedimentos a seguir aplicam-se tanto a produtos como a variações de produtos.

Antes de criar produtos, você precisa definir um [andaime](/help/sites-authoring/scaffolding.md). Isso especifica os campos necessários para definir os produtos e como eles são editados.

Um scaffold é necessário para cada tipo de produto distinto. O scaffold apropriado é associado aos produtos por:

* path
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
>Você pode criar uma nova definição de produto em qualquer lugar sob ela, sem nenhuma configuração adicional.

### Importação de produtos {#importing-products}

#### Importação de produtos - Interface otimizada para toque {#importing-products-touch-optimized-ui}

1. Navegue até o **Produtos** , via **Comércio**.
1. Usar o **Produtos** navegue até o local desejado.
1. Use o **Produtos de importação** para abrir o assistente.

   ![chlimage_1-1](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. Especifique:

   * **Importador**

      O importador para [fornecedor de comércio](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)por padrão `Geometrixx`.

   * **Origem**

      O arquivo que deseja importar; você pode usar o navegador para selecionar um arquivo.

   * **Importação incremental**

      Indique se essa é uma importação incremental (em vez de completa).
   >[!NOTE]
   >
   >A importação incremental (do importador geometrixx de amostra para o exterior) opera no nível do produto.
   >
   >Um importador personalizado pode ser definido para operar conforme necessário.

1. Selecionar **Próximo** para importar os produtos, será mostrado um log das ações realizadas.

   >[!NOTE]
   >
   >Os produtos serão importados para o local atual ou de acordo com ele.

   >[!NOTE]
   >
   >Uso repetido **Próximo** e **Voltar** O importará repetidamente as definições do produto. No entanto, como eles têm os mesmos SKUs, as informações existentes no repositório serão simplesmente substituídas.

1. Selecionar **Concluído** para fechar o assistente.

#### Importação de produtos - Interface clássica {#importing-products-classic-ui}

1. Usar o **Ferramentas** abra o **Comércio** pasta.
1. Clique duas vezes para abrir o **Importador de produto**:

   ![chlimage_1-22](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. Especifique:

   * **Armazenar nome**

      Os produtos serão importados para:

      `/etc/commerce/products/<*store name*>/`

   * **Provedor de comércio**

      O importador de seu [fornecedor de comércio](/help/commerce/cif-classic/administering/concepts.md#commerce-providers); por padrão, Geometrixx.

   * **Arquivo de origem**

      O local no repositório do arquivo que você deseja importar.

   * **Importação incremental**

      Indique se essa é uma importação incremental (em vez de completa).

1. Clique em **Produtos de importação**.

### Criação de informações sobre o produto {#creating-product-information}

>[!NOTE]
>
>O gerenciamento de produtos padrão é básico, pois o conjunto de produtos Geometrixx-Outdoors foi mantido básico. A complexidade se baseia no produto [andaime](/help/sites-authoring/scaffolding.md), portanto, com seu próprio scaffolding de produto, é possível obter uma edição mais sofisticada.

#### Criar informações do produto - IU otimizada ao toque {#creating-product-information-touch-optimized-ui}

1. Usar o **Produtos** console (via **Comércio**) navegue até o local desejado.
1. Use o **Criar** ícone para selecionar qualquer um (dependendo da estrutura e do local):

   * **Criar produto**
   * **Criar variação de produto**

   ![chlimage_1-14](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. O assistente será aberto. Use o **Básico** e **Guias do produto** para inserir o [atributos do produto](/help/commerce/cif-classic/administering/concepts.md#product-attributes) para o novo produto ou variante de produto.

   >[!NOTE]
   >
   >**Título** e **SKU** são o mínimo necessário para criar um produto ou variante.

1. Selecionar **Criar** para salvar as informações.

>[!NOTE]
>
>Muitos produtos são oferecidos em diversas cores e/ou tamanhos. As informações sobre o produto básico e as variantes do produto relacionadas podem ser gerenciadas no **Produtos** console.
>
>Os produtos e suas variantes são armazenados como uma estrutura em árvore, as informações do produto ficam na parte superior, com as variantes abaixo (essa estrutura é aplicada pela interface do usuário).

### Editar informações de produto {#editing-product-information}

>[!NOTE]
>
>As imagens de produto no geometrixx-outdoors são veiculadas a partir de:
>
>`/etc/commerce/products/...`
>
>Isso significa que, por padrão, eles são bloqueados pela variável [dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html), configure-a conforme necessário.

#### Editar informações de produto - IU otimizada ao toque {#editing-product-information-touch-optimized-ui}

1. Usar o **Produtos** console (via **Comércio**) navegue até as informações do produto.
1. Usar:

   * [ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de seleção](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Selecione o **Exibir dados do produto** ícone :

   ![chlimage_1-3](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. O [atributos do produto](/help/commerce/cif-classic/administering/concepts.md#product-attributes) será exibido. Use **Editar** e **Concluído** para fazer qualquer alteração.

### Mostrando as referências do produto {#showing-product-references}

#### Referências de produto exibidas - IU otimizada ao toque {#showing-product-references-touch-optimized-ui}

1. Usar o **Produtos** console (via **Comércio**) navegue até as informações do produto.
1. Abra o trilho secundário para Referências com o ícone:

   ![chlimage_1-4](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. Selecione o produto necessário - o trilho secundário será atualizado para mostrar os tipos de referência disponíveis:

   ![chlimage_1-88](/help/sites-administering/assets/chlimage_1-88.png)

1. Clique/toque no tipo de referência (por exemplo, Páginas de produto) para expandir a lista.
1. Selecione uma referência específica para mostrar as opções:

   * Navegar até a página do produto
   * Editar página do produto

   ![chlimage_1-89](/help/sites-administering/assets/chlimage_1-89.png)

### Procurar produtos {#search-for-products}

1. Navegue até o **Produtos** , via **Comércio**.
1. Abra o trilho secundário para Pesquisa com o ícone:

   ![](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. Várias facetas estão disponíveis para você procurar produtos. Você pode usar somente uma ou várias facetas para uma pesquisa. Os produtos encontrados serão exibidos:

   ![chlimage_1-90](/help/sites-administering/assets/chlimage_1-90.png)

1. Clicar/tocar em um produto o abre. Você também pode publicá-la ou exibir os dados do produto.

#### Extensão da pesquisa {#extending-search}

Você pode modificar uma faceta existente ou adicionar novas, usando o CRXDE Lite:

1. Vá até:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. Você pode modificar, por exemplo, os tamanhos que aparecerão na página de pesquisa do produto. Clique no botão `sizegroup` nó .
1. Clique em `items` , em seguida, clique em `propertypredicate` nó .
1. Você pode modificar o `propertyValues`. Por exemplo, você pode adicionar XS, ou XXL, ou remover um tamanho.
1. Clique em **Salvar tudo** e navegue até a página de pesquisa de produtos. Suas alterações devem aparecer.

### Vários ativos {#multiple-assets}

Você pode adicionar vários ativos no componente do produto e, em seguida, especificar o ativo que será exibido na página do produto.

>[!NOTE]
>
>Tudo relacionado a vários ativos é feito com a interface otimizada para toque.

#### Adicionar vários ativos {#adding-multiple-assets}

1. Navegue até o **Produtos** , via **Comércio**.
1. Usar o **Produtos** , navegue até o produto desejado.

   >[!NOTE]
   >
   >Você deve estar no nível do produto, não no nível da variante.

1. Toque/clique **Exibir dados do produto** ícone com o modo de seleção ou ações rápidas.
1. Toque/clique no ícone Editar .
1. Rolar para **Adicionar**.

   ![chlimage_1-91](/help/sites-administering/assets/chlimage_1-91.png)

1. Toque/clique **Adicionar**. Um novo espaço reservado para ativos é exibido.
1. Tocar/clicar em **Alterar **abre uma caixa de diálogo que permite escolher um ativo.
1. Selecione o ativo que deseja adicionar.

   >[!NOTE]
   >
   >Os ativos que você pode selecionar são de [Ativos](/help/assets/assets.md).

1. Toque/clique no ícone Concluído .

Dois ativos agora são armazenados no componente do produto. Você pode configurar qual delas aparecerá na página do produto. Funciona com um sistema de categoria. Primeiro, é necessário adicionar uma categoria aos ativos individuais:

1. Toque/clique **Exibir dados do produto**.
1. Digite um **Categoria do ativo** nos ativos, por exemplo `cat1` e `cat2`.

   >[!NOTE]
   >
   >Também é possível usar tags para categorias.

1. Toque/clique no ícone Concluído . Agora você tem que [implantação](#rolling-out-a-catalog) suas alterações.

Agora, seus ativos no componente do produto têm uma categoria. Você pode configurar qual categoria será exibida em três níveis diferentes:

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
>No nível do Catálogo e no nível do Console de Produtos, é necessário implantar as alterações para aplicar as modificações e ver a diferença na página do produto.

#### Página do Produto {#product-page}

1. Navegue até a página do produto.
1. **Editar** o componente do produto.
1. Digite o **Categoria de imagem** você escolheu ( `cat1` por exemplo).
1. Toque/clique **Concluído**. A página é atualizada e o ativo correto deve ser exibido.

#### Catálogo  {#catalog}

1. Navegue até o catálogo.
1. Toque/clique **Propriedades da exibição**.
1. Toque/clique em **Editar**.
1. Toque/clique no botão **Ativos** guia .
1. Digite o **Categoria do ativo do produto**.
1. Toque/clique **Concluído**.
1. [Implantação](#rolling-out-a-catalog) suas alterações.

#### Console de produtos {#products-console}

1. Usar o **Produtos** navegue até o Produto necessário.
1. Toque/clique **Exibir dados do produto**.
1. Toque/clique em **Editar**.
1. Digite um **Categoria de ativo padrão**.
1. Toque/clique **Concluído**.
1. [Implantação](#rolling-out-a-catalog) suas alterações.

### Publicar/desfazer a publicação de informações do produto {#publishing-unpublishing-product-information}

#### Publicar/desfazer a publicação de informações do produto - Interface otimizada para toque {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>Frequentemente, as informações do produto são publicadas por meio das páginas que as referenciam. Por exemplo, ao publicar a página X que faz referência ao produto Y, AEM perguntará se você também deseja publicar o produto Y.
>
>Para casos especiais, o AEM também oferece suporte à publicação direta dos dados do produto.

1. Usar o **Produtos** console (via **Comércio**) navegue até as informações do produto.
1. Usar:

   * [ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de seleção](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Selecione o **Publicar** ou **Cancelar publicação** ícone conforme necessário:

   ![chlimage_1-6](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![chlimage_1-7](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   As informações sobre o produto serão publicadas ou não serão publicadas, conforme adequado.

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration allows you to: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### Manipulador de eventos para atualizações de produtos {#event-handler-for-product-updates}

Existe um Manipulador de eventos que registra um evento quando um produto é adicionado, modificado ou excluído e quando uma página de produto é adicionada, modificada ou excluída. Há os seguintes eventos OSGi:

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

Para o `PRODUCT_*` , o caminho aponta para o produto base em `/etc/commerce/products`. Para o `PRODUCT_PAGE_*` , o caminho aponta para a variável `cq:Page` nó .

Você pode observá-los no Console da Web em eventos OSGI ( `/system/console/events`), por exemplo:

![](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>Leia também [Manuseio de evento em AEM](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/).

### Imagem com Links para adicionar ao carrinho {#image-with-add-to-cart-links}

O componente Imagem com links para adicionar ao carrinho permite adicionar rapidamente um produto ao carrinho, criando um ponto de acesso vinculado a um produto em uma imagem.

Clicar no ponto de acesso abre uma caixa de diálogo que permite escolher o tamanho e a quantidade do produto.

1. Navegue até a página onde deseja adicionar o componente.
1. Arraste e solte o componente na página.
1. Arraste e solte uma imagem no componente do [navegador de ativos](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. Você pode:

   * clique no componente e, em seguida, clique no ícone Editar
   * faça um clique duplo lento

1. Clique no ícone de tela cheia.

   ![chlimage_1-92](/help/sites-administering/assets/chlimage_1-92.png)

1. Clique no ícone do Mapa de lançamento.

   ![chlimage_1-93](/help/sites-administering/assets/chlimage_1-93.png)

1. Clique em um dos ícones da forma.

   ![chlimage_1-21](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. Modifique e mova a forma conforme necessário.
1. Clique na forma.
1. Clicar no ícone de navegação abre o [Seletor de ativos](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >Como alternativa, você pode digitar diretamente o caminho do produto, que deve estar no nível do produto, não no nível da variante.

   ![chlimage_1-94](/help/sites-administering/assets/chlimage_1-94.png)

1. Clique no ícone confirmar duas vezes e em sair da tela cheia.
1. Clique em algum lugar na página ao lado do componente. A página deve ser atualizada e você deve ver o seguinte símbolo na imagem:

   ![](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. Mudar para [visualização](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) modo.
1. Clique no ponto de acesso +. Uma caixa de diálogo é aberta onde você pode escolher o tamanho e a quantidade do produto inserido em **Caminho**.

   ![chlimage_1-95](/help/sites-administering/assets/chlimage_1-95.png)

1. Insira um tamanho e uma quantidade.
1. Clique no botão Add to cart . A caixa de diálogo é fechada.
1. Navegue até o carrinho. O produto deve estar aqui.

#### Opções de configuração {#configuration-options}

Você pode configurar a aparência da caixa de diálogo ao clicar no ponto de acesso:

1. Clique no componente e clique no ícone configurar .

   ![chlimage_1-96](/help/sites-administering/assets/chlimage_1-96.png)

1. Rolar para baixo. Existe um **ADICIONAR AO CARRINHO** guia .

   ![chlimage_1-97](/help/sites-administering/assets/chlimage_1-97.png)

1. Clique em **ADICIONAR AO CARRINHO**. Há 3 opções de configuração que você pode usar.

   ![chlimage_1-98](/help/sites-administering/assets/chlimage_1-98.png)

1. Clique no ícone Concluído .

## Catálogos {#catalogs}

### Gerar um catálogo {#generating-a-catalog}

#### Gerar um catálogo - IU otimizada ao toque {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>O catálogo fará referência aos dados do produto.

Para gerar um catálogo:

1. Abra o console Sites (por exemplo, [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)).
1. Navegue até o local onde deseja criar a nova página.
1. Para abrir a lista de opções, use o ícone **Criar**:

   ![ícone criar](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. Na lista, selecione **Criar catálogo**, o assistente Criar catálogo será aberto.

   ![chlimage_1-99](/help/sites-administering/assets/chlimage_1-99.png)

1. Navegue até o esquema de catálogo necessário.
1. Toque/clique **Selecionar** e toque/clique no Catalog Blueprint necessário.
1. Toque/clique **Próximo**.

   ![chlimage_1-100](/help/sites-administering/assets/chlimage_1-100.png)

1. Digite um **Título** e **Nome**.
1. Toque/clique no botão **Criar** botão. O catálogo é criado e uma caixa de diálogo é aberta.

   ![chlimage_1-101](/help/sites-administering/assets/chlimage_1-101.png)

1. Tocar/clicar **Concluído** O botão o traz de volta ao console Sites, onde você poderá ver seu catálogo.

   Tocar/clicar **Abrir catálogo** abre seu catálogo (por exemplo `http://localhost:4502/editor.html/content/test-catalog.html`).

#### Gerar um catálogo - Interface clássica {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>O catálogo fará referência ao seu [Dados do produto](#products-and-product-variants).

1. Usar o **Sites** , navegue até o **Blueprint do catálogo**, depois o Catálogo básico.

   Por exemplo:

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. Crie uma nova página usando o **Blueprint de Seção** modelo .

   Por exemplo, `Swimwear`.

1. Abra o novo `Swimwear` e, em seguida, clique em **Editar Blueprint** para abrir o **Propriedades** , onde é possível configurar a variável **Produtos** seleção.

   Por exemplo, abra o **Tags/Palavras-chave** para selecionar Atividade, em seguida, Nadar na seção Geometrixx-Outdoors .

1. Clique em **OK** para salvar suas propriedades; Por exemplo, os produtos serão mostrados na variável **Critérios de seleção do produto** na página do blueprint.
1. Clique em **Alterações na implantação...**, selecione **Página de implantação e todas as subpáginas**, depois clique em **Próximo** then **Implantação**. Quando a implantação for concluída com sucesso, a variável **Status** será exibido como verde.
1. Agora você pode clicar em **Fechar** e verificar a nova seção de catálogo; por exemplo, em e em:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. Novamente, na página de blueprints, clique **Editar Blueprint** e na **Propriedades** abrir a caixa de diálogo **Página gerada** guia . No campo Banner list , selecione a imagem que deseja mostrar; por exemplo, `summer.jpg`
1. Clique em **OK** para salvar suas propriedades; as informações do banner serão mostradas abaixo da variável **Critérios de seleção do produto** na página do blueprint.
1. Implemente essas novas alterações.

### Implantação de um catálogo {#rolling-out-a-catalog}

#### Implementar um catálogo - IU otimizada ao toque {#rolling-out-a-catalog-touch-optimized-ui}

Para implantar um catálogo:

1. Navegue até o **Catálogos** , via **Comércio**.
1. Navegue até o catálogo que deseja implantar.
1. Usar:

   * [ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de seleção](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Selecione o **Alterações na implantação** ícone :

   ![implantação](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. No assistente, defina a implantação conforme necessário e toque/clique **Alterações na implantação**.
1. Uma caixa de diálogo é aberta. Toque/clique **Concluído** quando o processo estiver concluído.

#### Implementar um catálogo - Interface clássica {#rolling-out-a-catalog-classic-ui}

Para implantar um catálogo:

1. Navegue até o Catálogo que deseja implantar. Por exemplo:

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. Clique em **Alterações na implantação...**
1. Defina a implantação conforme necessário.
1. Clique em **Implantação**.

### Importador de Blueprint {#blueprint-importer}

#### Importador de Blueprint - Interface otimizada ao toque {#blueprint-importer-touch-optimized-ui}

1. Navegue até o **Catálogos** , via **Comércio**.
1. Navegue até o local onde deseja importar o blueprint do catálogo.
1. Toque/clique no botão **Importar Blueprints** ícone .

   ![](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. No assistente, selecione a Origem conforme necessário e toque/clique em **Próximo**.

   ![chlimage_1-340](/help/sites-administering/assets/chlimage_1-102.png)

1. Toque/clique **Concluído** após a conclusão da importação.

#### Importador de Blueprint - Interface clássica {#blueprint-importer-classic-ui}

1. Usar o **Ferramentas** , navegue até **Comércio**.

   Por exemplo:

   `http://localhost:4502/miscadmin#/etc/commerce`

1. Abra o **Importador de bluprint do catálogo**.
1. Defina a importação conforme necessário.
1. Clique em **Importar Esquemas De Catálogo**.

## Promoções {#promotions}

### Criação de uma promoção {#creating-a-promotion}

#### Criar uma promoção - Interface clássica {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>O exemplo a seguir trata de uma promoção realizada diretamente em uma [campanha](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md), isto é usado para comprovantes.
>
>Uma promoção também pode estar em um [experiência](/help/sites-authoring/personalization.md) em uma campanha.
>
>Para obter mais informações, consulte [Promoções e Vouchers](#promotions-and-vouchers).

1. Abra o **Sites** console da instância do autor.
1. No painel esquerdo, selecione o **Campanha**.
1. Clique em **Novo**, selecione o **Promoção** e especifique um **Título** e **Nome** se necessário) para seu novo comprovante.
1. Clique em **Criar**. A nova página promocional será exibida no painel direito.

1. Edite o **Propriedades** por:

   * abrir a página e clicar no botão Editar para abrir a caixa de diálogo Propriedades
   * selecionar a página no console Sites e usar o menu de contexto (geralmente, o botão direito do mouse) para selecionar **Propriedades...** e abra a caixa de diálogo propriedades

   Especifique a **Tipo de promoção**, **Tipo de desconto**, **Valor do Desconto** e quaisquer outros campos, conforme necessário.

1. Clique em **OK** para salvar.

1. Agora é possível ativar sua promoção, de modo que os compradores a vejam na instância de publicação.

## Vouchers {#vouchers}

### Criação de um comprovante {#creating-a-voucher}

#### Criar um comprovante - Interface clássica {#creating-a-voucher-classic-ui}

1. Abra o **Sites** console da instância do autor.
1. No painel esquerdo, selecione o **Campanha**.
1. Clique em **Novo**, selecione o **Voucher** e especifique um **Título** e **Nome** se necessário) para seu novo comprovante.
1. Clique em **Criar**. A nova página de comprovante será exibida no painel direito.

1. Abra a nova página do comprovante com um clique duplo e clique em **Editar** para configurar as informações conforme necessário.
1. Clique em **OK** para salvar.

1. Agora você pode ativar seu comprovante, para que os compradores possam usá-lo em seus carrinhos na instância de publicação.

### Removendo Vouchers {#removing-vouchers}

#### Remover Vouchers - Interface clássica {#removing-vouchers-classic-ui}

Para tornar um comprovante indisponível para os clientes, é possível:

* Desative o comprovante - ele permanecerá disponível no ambiente de criação para que você possa reativá-lo posteriormente.
* Exclua-o completamente.

Ambas as ações podem ser realizadas no **Sites** console.

### Modificando Vouchers {#modifying-vouchers}

#### Modificar Vouchers - Interface clássica {#modifying-vouchers-classic-ui}

Para alterar as propriedades de um comprovante ou promoção, você pode clicar duas vezes nela no link **Sites** e clique em **Editar**. Depois de salvá-lo, você deve ativá-lo para que as alterações sejam enviadas para a(s) instância(s) de publicação.

### Adicionar vendedores a um carrinho {#adding-vouchers-to-a-cart}

Para permitir que os usuários adicionem comprovantes aos carrinhos, você pode usar o plug-in **Vouchers** componente (categoria Comércio). Você precisa adicionar isso à mesma página em que o carrinho é exibido (mas não é obrigatório). O componente de comprovantes é apenas um formulário no qual o usuário pode inserir um código de comprovante, é o componente de carrinho de compras que mostra a lista de comprovantes aplicados e seu desconto.

No site de demonstração (Geometrixx Outdoors - Inglês), é possível ver o formulário de comprovante na página do carrinho, abaixo do carrinho de compras real.

## Pedidos {#orders}

>[!NOTE]
>
>Convém lembrar que AEM predefinidas não têm ações necessárias para a funcionalidade padrão relacionada a pedidos, como devolução de mercadorias, atualização do status do pedido, realização, geração de guias de remessa. Ele é destinado principalmente como uma visualização de tecnologia.
>
>A gestão genérica de pedidos no AEM foi mantida básica; os campos disponíveis no assistente dependem do scaffold:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>Se você criar um scaffold personalizado, poderá armazenar mais informações sobre pedidos.

>[!NOTE]
>
>O console Pedidos expõe as informações do pedido do fornecedor, que nunca é publicado.
>
>As informações de pedido do cliente são mantidas em seus diretórios domésticos e são expostas pelo Histórico de pedidos de sua conta. Essas informações são publicadas junto com o resto do diretório inicial.

### Criando Informações de Pedido {#creating-order-information}

#### Criar informações de pedido - IU otimizada ao toque {#creating-order-information-touch-optimized-ui}

1. Usar o **Pedidos** navegue até o local desejado.
1. Use o **Criar** ícone para selecionar **Criar pedido**.

   ![](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. O assistente será aberto. Use o **Básico**, **Conteúdo**, **Pagamento** e **Cumprimento** para inserir o [informações sobre o novo pedido](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. Selecionar **Criar** para salvar as informações.

### Editar informações de pedido {#editing-order-information}

#### Editar informações de pedido - IU otimizada ao toque {#editing-order-information-touch-optimized-ui}

1. Usar o **Pedidos** navegue até a ordem.
1. Usar:

   * [ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions)
   * [modo de seleção](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   Selecione o **Exibir dados do pedido** ícone :

   ![](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. O [informações de pedido](/help/commerce/cif-classic/administering/concepts.md#order-information) será exibido. Use **Editar** e **Concluído** para fazer qualquer alteração.

