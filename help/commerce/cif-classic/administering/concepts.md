---
title: Conceitos
description: Conceitos gerais de comércio eletrônico com o Adobe Experience Manager.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '4478'
ht-degree: 1%

---

# Conceitos {#concepts}

A estrutura de integração fornece os mecanismos e os componentes para:

* conexão com um mecanismo de comércio eletrônico
* envio de dados para o Adobe Experience Manager (AEM)
* exibir esses dados e coletar as respostas do comprador
* detalhes da transação de devolução
* pesquisar os dados de ambos os sistemas

Isso significa que:

* Os compradores podem se registrar e comprar sem esperar.
* As variações de preços são vistas pelos compradores sem demora.
* Os produtos podem ser adicionados conforme necessário.

>[!NOTE]
>
>A estrutura de comércio eletrônico pode ser usada com:
>
>* [Adobe Commerce](/help/commerce/cif/integrating/magento.md)
>* [COMMERCE CLOUD SAP](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
>* [Commerce Cloud do Salesforce](https://github.com/adobe/commerce-salesforce)
>

>[!CAUTION]
>
>A variável [Estrutura de integração de comércio eletrônico](https://business.adobe.com/products/experience-manager/sites/ecommerce-integrations.html) O é um complemento do AEM.
>
>Seu representante de vendas pode fornecer todos os detalhes, de acordo com o mecanismo apropriado.

>[!CAUTION]
>
>A estrutura fornece os requisitos básicos para o seu próprio projeto.
>
>Uma certa quantidade de trabalho de desenvolvimento é sempre necessária para adaptar a estrutura às suas especificações.

>[!CAUTION]
>
>A instalação padrão do AEM inclui a implementação de comércio eletrônico genérico AEM (JCR).
>
>Ele é destinado a fins de demonstração ou como base para uma implementação personalizada de acordo com seus requisitos.

Para otimizar a operação, tanto o AEM quanto o mecanismo de comércio eletrônico se concentram em sua própria área de especialização. As informações são transferidas entre os dois em tempo real; por exemplo:

* O AEM pode:

   * Solicitação:

      * Informações do produto do mecanismo de comércio eletrônico.

   * Fornecer:

      * Exibições do usuário para informações do produto, carrinho de compras e check-out.
      * Carrinho de compras e informações de check-out para o mecanismo de comércio eletrônico.
      * Otimização do mecanismo de pesquisa (SEO).
      * Funcionalidade da comunidade.
      * Interações de marketing não estruturadas.

* O mecanismo de comércio eletrônico pode:

   * Fornecer:

      * Informações do produto do banco de dados.
      * Gerenciamento de variantes de produtos.
      * Order Management.
      * ERP (Enterprise Resource Planning, planejamento de recursos corporativos).
      * Pesquise nas informações do produto.

   * Processo:

      * O carrinho.
      * O check-out.
      * Atendimento do pedido.

>[!NOTE]
>
>Os detalhes exatos dependem do mecanismo de comércio eletrônico e da implementação do projeto.

Vários componentes AEM prontos para uso são fornecidos para usar a camada de integração. Atualmente, eles incluem:

* Informações do produto
* Carrinho de compras
* Check-out
* Minha conta

Várias opções de pesquisa também estão disponíveis.

## Arquitetura {#architecture}

A estrutura de integração fornece a API, uma variedade de componentes para ilustrar a funcionalidade e várias extensões para fornecer exemplos de métodos de conexão:

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

A estrutura oferece acesso a funcionalidades como:

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### Implementações {#implementations}

O eCommerce AEM é implementado com um mecanismo de eCommerce:

* A estrutura de integração de comércio eletrônico foi criada para permitir a fácil integração de um mecanismo de comércio eletrônico com AEM. O mecanismo de comércio eletrônico criado com a finalidade controla dados de produtos, carrinhos de compras, check-out e atendimento de pedidos, enquanto o AEM controla a exibição de dados e campanhas de marketing.


>[!NOTE]
>
>A instalação padrão do AEM inclui a implementação de comércio eletrônico genérico AEM (JCR).
>
>Ele é destinado a fins de demonstração ou como base para uma implementação personalizada de acordo com seus requisitos.
>
>O eCommerce AEM implementado no AEM usando desenvolvimento genérico com base em JCR é:
>
>* Um exemplo de comércio eletrônico independente e nativo de AEM para ilustrar o uso da API. Isso pode ser usado para controlar dados do produto, carrinhos de compras e check-out com a exibição de dados existente e campanhas de marketing. Nesse caso, o banco de dados do produto é armazenado no repositório nativo do AEM (Adobe implementation of [JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)).
>
>  A instalação padrão do AEM contém as noções básicas do [implementação de comércio eletrônico genérico](/help/commerce/cif-classic/administering/generic.md).

### Provedores de comércio {#commerce-providers}

Ao importar dados de um mecanismo de comércio para o site de comércio eletrônico AEM, um provedor de comércio é usado para fornecer dados aos importadores. Um único provedor de comércio pode oferecer suporte a vários importadores.

Um provedor de comércio é um código AEM personalizado para:

* interface para um mecanismo de comércio back-end
* implementar um sistema de comércio sobre o repositório JCR

Dois exemplos de provedores de comércio estão disponíveis atualmente para o AEM:

* um para geometrixx-hybris
* outro para geometrixx-generic (JCR)

Embora geralmente um projeto precise desenvolver seu próprio provedor de comércio personalizado específico para seu PIM e esquema de dados do produto.

>[!NOTE]
>
>Geometrixx Os importadores usam arquivos CSV; há uma descrição do schema aceito (com propriedades personalizadas permitidas) nos comentários acima de sua implementação.

A variável [ProductServicesManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) mantém (até [OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings)uma lista das implementações do [ProductImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) e [CatalogBlueprintImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html) interfaces. Elas estão listadas no **Importador/Provedor de comércio** campo suspenso do assistente de importador (usando o `commerceProvider` como um nome).

Quando um importador/provedor de comércio específico estiver disponível na lista suspensa, todos os dados complementares necessários deverão ser definidos (dependendo do tipo de importador) no:

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

A pasta na pasta apropriada `importers` a pasta deve corresponder ao nome do importador; por exemplo:

* `.../importproductswizard/importers/geometrixx/.content.xml`

O formato do arquivo de importação de origem é definido pelo importador. Ou o importador pode estabelecer uma conexão (por exemplo, WebDAV ou http) com o mecanismo de comércio.

## Funções {#roles}

O sistema integrado atende às seguintes funções para manter os dados:

* Usuário do Gerenciamento de informações do produto (PIM) que mantém:

   * Informações sobre o produto.
   * Taxonomia, categorização, aprovação.
   * Interage com o gerenciamento de ativos digitais.
   * Preços - geralmente advêm de um sistema ERP e não são explicitamente mantidos no sistema comercial.

* Autor/Gerente de marketing que mantém:

   * Conteúdo de marketing para todos os canais.
   * Promoções.
   * Vouchers.
   * Campanhas.

* Surfista/consumidor que:

   * Visualiza as informações do seu produto.
   * Coloca itens no carrinho de compras.
   * Verifica seus pedidos.
   * Aguarde o atendimento do pedido.

Embora a localização real possa depender da sua implementação; por exemplo, genérico ou com um mecanismo de comércio eletrônico:

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## Produtos {#products}

### Dados do produto versus Dados de marketing {#product-data-versus-marketing-data}

#### Categorias estruturais versus de marketing {#structural-versus-marketing-categories}

Se as duas categorias a seguir puderem ser diferenciadas, isso permitirá definir URLs claros com uma estrutura significativa (árvores de `cq:Page` nós) e, portanto, muito próximo da gestão clássica de conteúdo do AEM):

* *Categorias * estruturais

  A árvore de categorias definindo *o que é um produto*; por exemplo:

  `/products/mens/shoes/sneakers`

* *Marketing* categorias

  Todas as outras categorias que um *o produto pode pertencer a*; por exemplo:

  `/special-offers/christmas/shoes`)

### Data do produto {#product-data}

Para representar e gerenciar seu produto, você desejará manter uma variedade de informações sobre ele.

Os dados do produto podem ser:

* mantida diretamente no AEM (genérico).
* mantido no mecanismo de comércio eletrônico e disponibilizado no AEM.

  Dependendo do tipo de dados, é [sincronizado](#catalog-maintenance-data-synchronization) conforme necessário, ou acessados diretamente; por exemplo, dados altamente voláteis e críticos, como preços de produtos, são recuperados do mecanismo de comércio eletrônico em cada solicitação de página para garantir que estejam sempre atualizados.

Em ambos os casos, quando os dados do produto forem inseridos/importados no AEM, eles poderão ser vistos no **Produtos** console. Aqui, as exibições de cartão e lista de um produto mostram informações como:

* a imagem
* o código SKU
* quando modificado pela última vez

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### Variantes do produto {#product-variants}

Para produtos apropriados, informações sobre variantes também podem ser mantidas. Por exemplo, para artigos de vestuário, as diferentes cores disponíveis são mantidas como variantes:

![ecommerce productvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### Atributos do produto {#product-attributes}

Os atributos individuais mantidos sobre cada produto podem depender do mecanismo de eCommerce sendo usado e da implementação de AEM. Eles estão disponíveis (conforme apropriado) ao visualizar páginas de produtos e/ou editar informações sobre produtos e podem incluir:

* **Imagem**

  Uma imagem do produto.

* **Título**

  O nome do produto.

* **Descrição**

  Uma descrição textual do produto.

* **Tags**

  Tags usadas para agrupar produtos relacionados.

* **Categoria do ativo padrão**

  Uma categoria padrão para ativos.

* **Dados de ERP**

  Informações de ERP (Enterprise Resource Planning, planejamento de recursos corporativos).

   * **SKU**

     Informações da unidade de manutenção de estoque (SKU).

   * **Cor**
   * **Tamanho**
   * **Preço**

     O preço unitário do produto.

* **Resumo**

  Um resumo dos recursos do produto.

* **Recursos**

  Detalhes mais completos dos recursos do produto.

### Ativos do produto {#product-assets}

Uma seleção de ativos pode ser mantida para produtos individuais. Geralmente, eles incluem imagens e vídeos.

## Catálogos {#catalogs}

Um catálogo agrupa os dados do produto para facilitar o gerenciamento e a representação ao comprador. Muitas vezes, um catálogo é estruturado de acordo com atributos como idioma, área geográfica, marca, estação, hobby, esporte, entre muitos outros.

### Estrutura do catálogo {#catalog-structure}

#### Catálogos em vários idiomas {#catalogs-in-multiple-languages}

O AEM oferece suporte ao conteúdo do produto em vários idiomas. Ao solicitar dados, a estrutura de integração recupera o idioma da árvore atual (por exemplo, `en_US` para páginas em `/content/geometrixx-outdoors/en_US`).

Para um armazenamento em vários idiomas, você pode importar o catálogo para cada árvore de idioma individualmente (ou copiá-lo com [MSM](/help/sites-administering/msm.md)).

#### Catálogos para várias marcas {#catalogs-for-multiple-brands}

Assim como com os idiomas, grandes empresas multinacionais devem atender a várias marcas.

#### Catálogos por tags {#catalogs-by-tags}

As tags também podem ser usadas para agrupar produtos em um catálogo. Eles podem ser usados para catálogos mais dinâmicos, como ofertas sazonais.

### Configuração do catálogo (importação inicial) {#catalog-setup-initial-import}

Dependendo da sua implementação, você pode importar os dados do produto necessários para o catálogo base no AEM de:

* um arquivo CSV (para a implementação genérica)
* o mecanismo de comércio eletrônico

### Manutenção de Catálogo (Sincronização de Dados) {#catalog-maintenance-data-synchronization}

São inevitáveis novas alterações nos dados do produto:

* para a implementação genérica, elas podem ser gerenciadas com o [editor de produto](/help/commerce/cif-classic/administering/generic.md#editing-product-information)
* ao usar um [Mecanismo de comércio eletrônico, as alterações devem ser sincronizadas](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### Sincronização de dados com um mecanismo de comércio eletrônico (em andamento) {#data-synchronization-with-an-ecommerce-engine-ongoing}

Após a importação inicial, as alterações nos dados do produto são inevitáveis.

Ao usar um mecanismo de comércio eletrônico, os dados do produto são mantidos lá e devem estar disponíveis no AEM. Esses dados do produto devem ser sincronizados quando as atualizações forem feitas.

Isso pode depender do tipo de dados:

* A [a sincronização periódica é usada junto com um feed de dados de alterações](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing).

  Além disso, é possível selecionar atualizações específicas para uma atualização expressa.

* Dados altamente voláteis, como informações de preço, são recuperados do mecanismo de comércio para cada solicitação de página, para garantir que estejam sempre atualizados.

### Catálogos - Desempenho e dimensionamento {#catalogs-performance-and-scaling}

A importação de um grande catálogo com um alto número de produtos (mais de 100.000) de um mecanismo de comércio eletrônico (PIM) pode afetar o sistema devido ao grande número de nós. Ela também pode retardar a instância de criação se os produtos tiverem ativos associados (por exemplo, imagens de produtos). Isso ocorre porque o pós-processamento desses ativos consome muita CPU e memória.

Há várias estratégias que você pode escolher para contornar esses problemas:

* [Classificação](#bucketing) - para atender ao grande número de nós
* [Descarregar o pós-processamento de ativo para uma instância dedicada](#offload-asset-post-processing-to-a-dedicated-instance)
* [Importar somente dados do produto](#only-import-product-data)
* [Limitação de importação e salvamentos em lote](#import-throttling-and-batch-saves)
* [Teste de desempenho](#performance-testing)
* [Desempenho - Diversos](#performance-miscellaneous)

#### Classificação {#bucketing}

Se um nó JCR tiver muitos nós secundários diretos (por exemplo, 1000 ou mais), os buckets (pastas fantasmas) serão necessários para garantir que o desempenho não seja afetado. Eles são gerados de acordo com um algoritmo ao importar.

Esses buckets tomam a forma de pastas fantasmas que são introduzidas na estrutura do catálogo, mas podem ser configurados para que não fiquem aparentes em URLs públicos.

#### Descarregar o pós-processamento de ativo para uma instância dedicada {#offload-asset-post-processing-to-a-dedicated-instance}

Esse cenário envolve a configuração de duas instâncias de autor:

1. Instância do autor principal

   Importa dados de produto do PIM, no qual o pós-processamento dos caminhos de ativos está desativado.

1. Instância de autor DAM dedicada

   Importa e pós-processa ativos de produtos do PIM e os replica de volta na instância do autor principal para uso.

![Diagrama de arquitetura](/help/sites-administering/assets/chlimage_1-8.png)

#### Importar somente dados do produto {#only-import-product-data}

Para os casos em que os produtos não contêm ativos (imagens) a serem importados, é possível importar os dados do produto sem ser afetado pelo pós-processamento de ativos.

![Diagrama de arquitetura](/help/sites-administering/assets/chlimage_1-9.png)

#### Teste de desempenho {#performance-testing}

O teste de desempenho deve ser considerado em implementações de comércio eletrônico AEM:

* Ambiente do autor:

  A atividade em segundo plano (por exemplo, importação) pode ocorrer ao mesmo tempo que a atividade normal do usuário (por exemplo, edição de página) e mesmo que o desempenho de front-end receba (em geral) uma prioridade mais alta, o desempenho inadequado visto por autores online pode levar à frustração capaz de bloquear uma decisão de publicação.

* Ambiente de publicação:

  A replicação é um processo essencial para garantir que o conteúdo seja publicado de forma rápida e confiável. Isso pode ser afetado pela forma como o autor agrupa o conteúdo a ser publicado.

* Front-end:

  A combinação de invalidações de front-end e cache pode levar a surpresas no desempenho. Testes ajudam a evitá-los.

Observe que este teste de desempenho requer conhecimento e análise do público-alvo:

* Volumes de conteúdo

   * Assets
   * Produtos I18ned e SKUs localizados

* Atividade do usuário:

   * Edição em massa
   * Publicação em massa
   * Muitas solicitações de pesquisa

* Processos de segundo plano

   * Importações
   * Atualizações de sincronização (por exemplo, preços)

* Requisitos de manutenção (backup, otimização de PM do Tar, coleta de lixo do armazenamento de dados etc.)

#### Desempenho - Diversos {#performance-miscellaneous}

Para todas as implementações, os seguintes pontos podem ser considerados:

* Como os produtos, as unidades de manutenção de estoque e as categorias podem ser numerosas, tente usar o menor número possível de nós para modelar o conteúdo.

  Quanto mais nós você tiver, mais flexível será seu conteúdo (por exemplo, parsys). No entanto, tudo é uma escolha e você precisa de flexibilidade individual (por padrão) ao manipular (por exemplo) produtos de 30 mil?

* Evite a duplicação o máximo possível (consulte a localização) ou, quando fizer isso, pense em quantos nós a duplicação leva.
* Tente marcar seu conteúdo o máximo possível para preparar a otimização da consulta.

  Por exemplo:

  `/content/products/france/fr/shoe/reebok/pump/46 SKU`

  deve ter uma tag por nível de conteúdo (ou seja, país, idioma, categoria, marca, produto). Pesquisando

  `//element(*,my:Sku)[@country='france' and @language='fr'`

  e

  `@category='shoe' and @brand='reebok' and @product='pump']`

  será drasticamente mais rápido do que pesquisar por

  `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* Em seu conjunto técnico, planeje o modelo e os serviços de acesso ao conteúdo fatorados. Esta é uma prática recomendada geral, mas é ainda mais importante aqui, pois você pode, em fases de otimização, adicionar caches de aplicativo para dados que são lidos com frequência (e que você não deseja preencher o cache do pacote com).

  Por exemplo, o gerenciamento de atributos frequentemente é um bom candidato para armazenamento em cache, pois trata de dados atualizados por meio da importação de produtos.
* Considere o uso de [páginas de proxy](#proxy-pages).

### Páginas de seção do catálogo {#catalog-section-pages}

As seções de Catálogo fornecem, por exemplo:

* uma introdução (imagem e/ou texto) à categoria; também pode ser usada para banners e teasers para promover ofertas especiais
* links para produtos individuais dessa categoria
* links para outras categorias

![ecommerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### Páginas de produto {#product-pages}

As páginas de produtos fornecem informações abrangentes sobre produtos individuais. Atualizações dinâmicas do também são refletidas; por exemplo, alterações de preço registradas no mecanismo de comércio eletrônico.

As páginas de produto são páginas AEM que usam **Produto** componente; por exemplo, dentro do **Produto do Commerce** modelo:

![ecommerce_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

O componente do produto fornece:

* Informações gerais sobre o produto, incluindo texto e imagens.
* Preços; são recuperados do mecanismo de comércio eletrônico sempre que a página é exibida/atualizada.
* Informações sobre a variante do produto; por exemplo, cor e tamanho.

Essas informações permitem que o comprador selecione o seguinte ao adicionar um item à sua cesta:

* Variantes de cor e tamanho
* Quantidade

#### Páginas de aterrissagem do produto {#product-landing-pages}

Essas são páginas AEM que fornecem informações principalmente estáticas; por exemplo, uma introdução e uma visão geral com links para as páginas de produto subjacentes.

### Componente do produto {#product-component}

A variável **Produto** pode ser adicionado a qualquer página com uma página principal que forneça os metadados necessários (ou seja, os caminhos para `cartPage` e `cartObject`). No site de demonstração, Geometrixx Outdoors, isso é fornecido pela `UserInfo.jsp`.

A variável **Produto** componente também pode ser personalizado de acordo com suas necessidades individuais.

### Páginas de proxy {#proxy-pages}

As páginas proxy são usadas para simplificar a estrutura do repositório e otimizar o armazenamento para catálogos grandes.

A criação de um catálogo usa dez nós por produto, pois fornece componentes individuais para cada produto que você pode atualizar e personalizar no AEM. Esse grande número de nós pode se tornar um problema se o catálogo contiver centenas ou até mesmo milhares de produtos. Para evitar problemas, você pode criar seu catálogo usando páginas de proxy.

As páginas proxy usam uma estrutura de dois nós ( `cq:Page` e `jcr:content`) que não contém nenhum conteúdo real do produto. O conteúdo é gerado, no momento da solicitação, referenciando os dados do produto e a página do modelo.

No entanto, há uma compensação. Você não será capaz de personalizar as informações do seu produto dentro do AEM, um modelo padrão (definido para o seu site) será usado.

>[!NOTE]
>
>Você não terá problemas se importar um catálogo grande sem páginas de proxy.
>
>É possível converter de uma metodologia para outra a qualquer momento. Também é possível converter uma subseção do catálogo.

## Promoções e vouchers {#promotions-and-vouchers}

### Vouchers {#vouchers}

Os vouchers são um método experimentado e testado de oferecer descontos para atrair os compradores a fazer uma compra e/ou recompensar a fidelidade do cliente.

* Fornecimento de vouchers:

   * Um código de voucher (a ser digitado no carrinho pelo comprador).
   * Um rótulo de voucher (a ser exibido depois que o comprador o inserir no carrinho).
   * Um caminho de promoção (que define a ação à qual o voucher se aplica).

* Mecanismos de comércio externo também podem fornecer vouchers.

No AEM:

* Um voucher é um componente baseado em páginas que é criado / editado com o console Sites.
* A variável **Voucher** O componente fornece:

   * Um renderizador para administração de vouchers; mostra todos os vouchers que estão no carrinho.
   * As caixas de diálogo de edição (formulário) para administrar (adicionar/remover) os vouchers.
   * As ações necessárias para adicionar/remover vouchers do carrinho.

* Os vouchers não têm suas próprias datas/horas de ativação e desativação, mas usam os das campanhas principais.

>[!NOTE]
>
>AEM usa o termo **Voucher**, é sinônimo do termo **Cupom**.

### Promoções {#promotions}

As promoções, juntamente com vouchers, permitem que você realize cenários como:

* Uma empresa fornece preços personalizados para funcionários, que é uma lista de usuários artesanal.
* Os clientes de longo prazo recebem descontos em todos os pedidos.
* Um preço de venda oferecido por um período de tempo bem definido.
* Um cliente recebe um voucher quando seu pedido anterior excedeu um valor específico.
* Um cliente que compra *product-X* recebe um desconto em *produto-Y* (produtos de pares).

As promoções não são mantidas por gerentes de informações do produto, mas por gerentes de marketing:

* Uma promoção é um componente baseado em páginas, criado/editado com o console Sites. &quot;
* Fornecimento de promoções:

   * Uma prioridade
   * Um caminho de manipulador de promoção

* É possível conectar promoções a uma campanha para definir suas datas/horas de ativação/desativação.
* É possível conectar promoções a uma experiência para definir seus segmentos.
* As promoções não conectadas a uma experiência não serão acionadas por conta própria, mas ainda poderão ser acionadas por um Voucher.
* O componente de Promoção contém:

   * renderizadores e caixas de diálogo para administração de promoção
   * subcomponentes para renderização e edição de parâmetros de configuração específicos para os manipuladores de promoção

No AEM, as promoções também estão integradas no [Campaign Management](/help/sites-authoring/personalization.md):

* a [campaign](/help/sites-authoring/personalization.md) especifica os horários de ativação/desativação
* [experiências](/help/sites-authoring/personalization.md) *no prazo de* a campanha é usada para agrupar ativos (páginas de teaser, promoções etc.) de acordo com o segmento de público ao qual eles correspondem

Uma promoção pode ser realizada em uma experiência ou diretamente na campanha:

* Se uma promoção for realizada em uma experiência, ela poderá ser aplicada automaticamente a um segmento de público-alvo.

  Por exemplo, no site de amostra geometrixx-outdoors, a promoção:

  `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

  está em uma experiência e, portanto, é acionado automaticamente sempre que o segmento ( `ordervalueover100`) resolve.

* Se uma promoção não aparecer em uma experiência (somente na campanha), ela não poderá ser aplicada automaticamente a um público-alvo. No entanto, ainda poderá ser acionado se o comprador inserir um voucher no carrinho e esse voucher fizer referência à promoção.

  Por exemplo, a promoção:

  `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

  O está fora de uma experiência e, portanto, nunca é acionado automaticamente (ou seja: com base na segmentação). No entanto, é referenciado pelos vouchers que podem ser encontrados em várias das experiências dentro da campanha de artigos. Inserir esses códigos de voucher no carrinho resulta no acionamento da promoção.

>[!NOTE]
>
>[promoções hybris](https://www.hybris.com/modules/promotion) e [vouchers hybris](https://www.hybris.com/en/modules/voucher) abranja tudo o que influencia o carrinho de compras e está relacionado a preços. Conteúdo de marketing específico para promoções (como banners etc.) não faz parte da promoção hybris.

## Personalização {#personalization}

### Registro e contas do cliente {#customer-registration-and-accounts}

Quando um comprador se registra, os detalhes da conta devem ser sincronizados entre o AEM e o mecanismo de eCommerce. Os dados confidenciais são mantidos independentemente, mas os perfis são compartilhados:

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

O mecanismo exato pode depender do cenário:

1. As contas de usuário existem em ambos os sistemas:

   1. Nenhuma ação necessária.

1. A conta de usuário existe apenas no AEM:

   1. O usuário é criado no mecanismo de comércio eletrônico com a mesma ID de conta e uma senha aleatória que será armazenada no AEM.
   1. A senha aleatória é necessária, pois o AEM tenta fazer logon no mecanismo de eCommerce na primeira chamada (por exemplo, quando uma página de produto é solicitada e o mecanismo de eCommerce é indicado pelo preço). Como isso acontece após o logon com o AEM, a senha não está disponível.

1. A conta de usuário existe apenas no mecanismo de comércio eletrônico:

   1. A conta é criada no AEM com a mesma ID de conta e senha.

Ao usar um mecanismo de comércio eletrônico, o AEM armazena somente a ID da conta e a senha (opcionalmente, um grupo de usuários). Todas as outras informações são armazenadas no mecanismo de comércio eletrônico.

>[!NOTE]
>
>Ao usar um mecanismo de comércio eletrônico, você deve garantir que as contas criadas para usuários que fazem logon em uma instância do AEM sejam replicadas (por exemplo, por meio de workflows) para qualquer outra instância do AEM que se comunique com esse mecanismo.
>
>Caso contrário, essas outras instâncias do AEM também tentarão criar contas para os mesmos usuários no mecanismo. Essas ações falham com uma `DuplicateUidException` vem do motor.

### Inscrição do cliente {#customer-sign-up}

Muitas vezes, a inscrição é necessária para que o comprador tenha acesso ao carrinho de compras. Isso requer registro (Criar conta) para que uma conta específica do cliente possa ser criada.

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>Um carrinho de compras anônimo e um check-out também são compatíveis.

### Logon do cliente {#customer-sign-in}

Após a inscrição, o comprador pode fazer logon com sua conta para que suas ações possam ser rastreadas e seus pedidos atendidos.

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### Logon único {#single-sign-on}

O Logon único (SSO) é fornecido, para que os autores sejam conhecidos no AEM e no sistema de comércio eletrônico sem precisar fazer logon duas vezes.

### myAccount {#myaccount}

Os dados de transação do mecanismo de comércio eletrônico são combinados com informações pessoais sobre o comprador. O AEM usa alguns desses dados como dados de perfil. A ação de um formulário no AEM grava as informações de volta no mecanismo de comércio eletrônico.

Há uma página que permite gerenciar facilmente as informações da sua conta. Você pode acessá-lo clicando em **Minha conta** na parte superior de uma página do Geometrixx ou navegando até `/content/geometrixx-outdoors/en/user/account.html`.

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### Catálogo de endereços {#address-book}

Seu site precisa armazenar uma seleção de endereços, incluindo entrega, cobrança e endereços alternativos. Isso pode ser implementado usando formulários com base no formato de endereço padrão ou você pode usar o componente Catálogo de endereços fornecido pelo AEM.

Esse componente do Catálogo de Endereços permite:

* editar endereços no livro
* selecionar um endereço do livro para o endereço de entrega
* selecionar um endereço do livro para o endereço de cobrança

Você pode escolher qual endereço deseja como padrão.

O componente do catálogo de endereços pode ser acessado de **Minha conta** clicando em **Catálogo de Endereços** ou navegando até `/content/geometrixx-outdoors/en/user/account/address-book.html`.

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

Você pode clicar em **Adicionar novo endereço...** para adicionar um endereço no seu catálogo de endereços. Ele abre um formulário que pode ser preenchido e, em seguida, clique em **Adicionar endereço**.

>[!NOTE]
>
>Você pode inserir vários endereços no seu Catálogo de Endereços.

O Catálogo de endereços é usado ao &quot;finalizar a compra&quot; do carrinho:

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

Os endereços são mantidos abaixo `user_home/profile/addresses`.
Por exemplo, para Alison Parker, seria em /home/users/geometrixx/aparker@geometrixx.info/profile/addresses

Você pode escolher qual endereço deseja como padrão, essas informações são mantidas no perfil do comprador em vez do endereço. A propriedade do perfil `address.default` é definido com o caminho do endereço selecionado para o valor.

### Preços específicos do cliente {#customer-specific-pricing}

O mecanismo de comércio eletrônico usa o contexto (essencialmente as informações do comprador) para determinar o preço que está retendo e, em seguida, fornece as informações corretas ao AEM.

## Carrinho de compras e pedidos {#shopping-cart-and-orders}

Ao fazer compras, o comprador navega pelas páginas do produto e seleciona itens para colocá-los em seu carrinho de compras. Quando eles prosseguirem com o check-out, um pedido poderá ser feito.

### Compradores anônimos {#anonymous-shoppers}

Um cliente anônimo pode:

* Exibir produtos
* Adicionar produtos ao carrinho
* Execute o check-out para fazer seu pedido

>[!NOTE]
>
>Dependendo da configuração das informações de endereço da instância ou do registro do cliente, pode ser necessário antes da finalização da compra.

### Compradores registrados {#registered-shoppers}

Um cliente registrado pode:

* Faça logon em sua conta
* Exibir produtos
* Adicionar produtos ao carrinho
* Execute o check-out para fazer seu pedido
* Exibir e rastrear pedidos anteriores

### Visão geral do conteúdo do carrinho de compras {#shopping-cart-content-overview}

O carrinho de compras fornece:

* uma visão geral dos itens selecionados
* links para as páginas de produto dos itens selecionados
* a capacidade de:

   * atualizar o número/quantidade de itens individuais
   * remover itens individuais

![ecommerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

O carrinho de compras é salvo de acordo com o mecanismo que está sendo usado:

* O genérico da AEM armazena o carrinho em um cookie.
* Determinados mecanismos de comércio eletrônico podem armazenar o carrinho em uma sessão.

Em ambos os casos, os itens ficam no carrinho (e podem ser restaurados) durante o logon/logout (mas somente na mesma máquina/navegador). Por exemplo:

* procurar como `anonymous` e adicionar produtos ao carrinho
* fazer logon como `Allison Parker` - O carrinho de Allison está vazio
* adicionar produtos ao carrinho de Allison
* sair - o carrinho mostra os produtos para `anonymous`

* entrar novamente como `Allison Parker` - Os produtos da Allison são restaurados.

>[!NOTE]
>
>Um carrinho anônimo só pode ser restaurado na mesma máquina/navegador.

>[!NOTE]
>
>Não é recomendável testar a restauração do conteúdo do carrinho com o `admin` conta, pois isso pode entrar em conflito com a `admin` conta do mecanismo de comércio eletrônico (por exemplo, hybris).

>[!NOTE]
>
>o hybris pode ser configurado para remover carrinhos pendentes após um período definido.

Antes do check-out, as alterações de preço são refletidas (em ambos os sistemas) à medida que ocorrem.

### Informações do pedido {#order-information}

Dependendo de suas informações de implementação sobre um pedido que é mantido no mecanismo de eCommerce ou no AEM, essas informações são renderizadas pelo AEM.

Várias informações são armazenadas, que podem incluir:

* **ID do pedido**

  O número de referência do pedido.

* **Instalado**

  A data em que o pedido foi feito.

* **Status**

  O status do pedido; por exemplo, Enviado.

* **Moeda**

  A moeda do pedido.

* **Itens de conteúdo**

  Uma lista de itens ordenados.

* **Subtotal**

  O custo total dos itens solicitados.

* **Imposto**

  O valor de quaisquer impostos devidos sobre o pedido.

* **Envio**

  Custos de envio.

* **Total**

  O valor total do pedido; itens solicitados, impostos e remessa.

* **Endereço de cobrança**

  O endereço para o qual a fatura deve ser enviada.

* **Token de pagamento**

  O método de pagamento.

* **Status do pagamento**

  O status do pagamento.

* **Endereço de envio**

  O endereço para o qual as mercadorias devem ser enviadas.

* **Método de envio**

  O método de envio; por exemplo, terra, mar ou ar.

* **Número de rastreamento**

  Qualquer número de rastreamento usado pela empresa de remessa.

* **Link de rastreamento**

  O link usado para rastrear o pedido enquanto é enviado.

>[!NOTE]
>
>Os campos usados no assistente de criação de pedidos dependem de um andaime otimizado para toque definido para o local. No exemplo genérico, ele pode ser encontrado em:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

Quando o pedido é mantido no AEM, o console Pedido mostra o seguinte para cada pedido:

* o número de itens no carrinho
* o valor total do pedido
* quando o pedido foi feito
* o status

![chlimage_1-16](/help/sites-administering/assets/chlimage_1-16.png)

### Rastreamento de pedidos {#order-tracking}

Depois de fazer um pedido, os compradores geralmente retornam para:

* Verificar o status do pedido
* Remover produtos do pedido
* Adicionar produtos ao pedido

Depois de receber a entrega do pedido, os compradores também podem querer visualizar o histórico de pedidos feitos durante um período de tempo.

O atendimento e o rastreamento de pedidos são gerenciados pelo mecanismo de comércio eletrônico. As informações podem ser exibidas pelo AEM usando o componente Histórico de pedidos, que mostra todos os detalhes relevantes, incluindo os vouchers e as promoções aplicadas. Por exemplo:

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## Check-out {#checkout}

A finalização é implementada com formulários AEM padrão. Isso permite que o gerente de marketing personalize a experiência com conteúdo de marketing.

Em seguida, o eCommerce gerencia o processo de finalização com a entrada dos formulários AEM.

### Segurança de pagamento {#payment-security}

Os detalhes do pagamento, incluindo informações de cartão de crédito, geralmente são gerenciados pelo mecanismo de comércio eletrônico. O AEM encaminha essas informações transacionais para o mecanismo (de onde elas são encaminhadas para um serviço de processamento de pagamentos).

Conformidade com o PCI (Payment Card Industry, setor de cartões de pagamento) pode ser alcançada.

### Confirmação do pedido {#confirmation-of-order}

O pedido é confirmado na tela e pode ser rastreado com o [rastreamento de pedidos](#order-tracking).

## Pesquisar {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

Como o AEM usa páginas padrão para produtos, você pode usar o componente de pesquisa padrão para criar uma página de pesquisa.

Se você precisar de uma implementação mais completa, é possível:

* Estenda o componente de pesquisa padrão com a funcionalidade necessária.
* Implemente o método de pesquisa no `CommerceService` e, em seguida, use o componente de pesquisa de comércio eletrônico na página de pesquisa.

Ao usar um mecanismo de comércio eletrônico, a API de pesquisa de comércio eletrônico pode ser totalmente implementada na solução de mecanismo de comércio eletrônico, para que você possa usar o componente de pesquisa de comércio eletrônico fornecido pronto para uso. A pesquisa facetada permite pesquisar JCR e/ou o mecanismo:
