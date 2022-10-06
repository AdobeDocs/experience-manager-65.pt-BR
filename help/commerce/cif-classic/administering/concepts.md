---
title: Conceitos
description: Conceitos gerais de comércio eletrônico com AEM.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: 290b2af6-257f-42f2-b809-1248227a4795
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '4514'
ht-degree: 1%

---

# Conceitos {#concepts}

A estrutura de integração fornece os mecanismos e componentes para:

* conexão com um mecanismo de comércio eletrônico
* transferir dados para o AEM
* exibir esses dados e coletar as respostas do comprador
* retornar detalhes da transação
* pesquisar os dados de ambos os sistemas

Isso significa que:

* Os compradores podem se registrar e fazer compras sem esperar.
* As alterações de preço serão vistas pelos compradores sem demora.
* Os produtos podem ser adicionados conforme necessário.

>[!NOTE]
>
>A estrutura de comércio eletrônico pode ser usada com:
>
>* [Adobe Commerce](/help/commerce/cif/integrating/magento.md)
>* [Commerce Cloud SAP](/help/commerce/cif-classic/administering/sap-commerce-cloud.md)
>* [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)
>


>[!CAUTION]
>
>O [Estrutura de integração do comércio eletrônico](https://www.adobe.com/solutions/web-experience-management/commerce.html) é um complemento AEM.
>
>Seu representante de vendas poderá fornecer todos os detalhes, de acordo com o mecanismo apropriado.

>[!CAUTION]
>
>A estrutura fornece os requisitos básicos para seu próprio projeto.
>
>É sempre necessário um certo trabalho de desenvolvimento para adaptar a estrutura às suas especificações.

>[!CAUTION]
>
>A instalação padrão do AEM inclui a implementação genérica do AEM (JCR) eCommerce.
>
>Atualmente, isso é destinado a fins de demonstração ou como base básica para uma implementação personalizada de acordo com suas necessidades.

Para otimizar a operação, tanto o AEM quanto o mecanismo de comércio eletrônico se concentram em sua própria área de conhecimento. As informações são transferidas entre os dois em tempo real; por exemplo:

* AEM pode:

   * Solicitação:

      * Informações do produto do mecanismo de comércio eletrônico.
   * Fornecer:

      * O usuário exibe informações do produto, carrinho de compras e check-out.
      * Carrinho de compras e informações de check-out para o mecanismo de comércio eletrônico.
      * Otimização do mecanismo de pesquisa (SEO).
      * Funcionalidade da comunidade.
      * Interações de marketing não estruturadas.


* O mecanismo de comércio eletrônico pode:

   * Fornecer:

      * Informações do produto do banco de dados.
      * Gerenciamento de variantes do produto.
      * Gerenciamento de pedidos.
      * ERP (Planejamento de Recursos Empresariais).
      * Pesquise nas informações do produto.
   * Processo:

      * O carrinho de compras.
      * O check-out.
      * Cumprimento do pedido.


>[!NOTE]
>
>Os detalhes exatos dependerão do mecanismo de comércio eletrônico e da implementação do projeto.

Vários componentes de AEM prontos para uso são fornecidos para usar a camada de integração. Atualmente, incluem:

* Informações do produto
* Carrinho de compras
* Check-out
* Minha conta

Várias opções de pesquisa também estão disponíveis.

## Arquitetura {#architecture}

A estrutura de integração fornece a API, uma variedade de componentes para ilustrar a funcionalidade e várias extensões para fornecer exemplos de métodos de conexão:

![chlimage_1-4](/help/sites-administering/assets/chlimage_1-4.png)

A estrutura fornece acesso a funcionalidades como:

![chlimage_1-5](/help/sites-administering/assets/chlimage_1-5.png)

### Implementações {#implementations}

AEM comércio eletrônico é implementado com um mecanismo de comércio eletrônico:

* A estrutura de integração do eCommerce foi criada para permitir que você integre facilmente um mecanismo de eCommerce ao AEM. O mecanismo de comércio eletrônico criado com o objetivo controla os dados do produto, os carrinhos de compras, o check-out e o cumprimento de pedidos, enquanto AEM controla a exibição de dados e as campanhas de marketing.


>[!NOTE]
>
>A instalação padrão do AEM inclui a implementação genérica do AEM (JCR) eCommerce.
>
>Atualmente, isso é destinado a fins de demonstração ou como base básica para uma implementação personalizada de acordo com suas necessidades.
>
>AEM eCommerce implementado no AEM usando desenvolvimento genérico com base no JCR é:
>
>* Um exemplo de comércio eletrônico independente e AEM nativo para ilustrar o uso da API. Isso pode ser usado para controlar dados do produto, carrinhos de compras e check-out junto com a exibição de dados e campanhas de marketing existentes. Nesse caso, o banco de dados do produto é armazenado no repositório nativo do AEM (a implementação do Adobe de [JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html)).
>
>  A instalação padrão do AEM contém os fundamentos da [implementação genérica do eCommerce](/help/commerce/cif-classic/administering/generic.md).

### Provedores de comércio {#commerce-providers}

Ao importar dados de um mecanismo de comércio para o site de comércio eletrônico AEM, um provedor de comércio é usado para fornecer dados aos importadores. Um provedor de comércio pode suportar vários importadores.

Um provedor de comércio é AEM código personalizado a:

* interface em um mecanismo de comércio back-end
* implementar um sistema de comércio sobre o repositório JCR

Dois exemplos de provedores de comércio estão disponíveis no momento para AEM:

* um para geometrixx-hybris
* outro para geometrixx-generic (JCR)

Embora normalmente um projeto precise desenvolver seu próprio provedor de comércio personalizado e específico para o PIM e o schema de dados do produto.

>[!NOTE]
>
>Os importadores geometrixx usam arquivos CSV; há uma descrição do schema aceito (com propriedades personalizadas permitidas) nos comentários acima de sua implementação.

O [ProductServicesManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductServicesManager.html) mantém (por meio de [OSGi](/help/sites-deploying/configuring.md#osgi-configuration-settings)) uma lista de implementações da  [ProductImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/ProductImporter.html) e [CatalogBlueprintImporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/commerce/pim/api/CatalogBlueprintImporter.html) interfaces. Eles estão listados na variável **Importador/Provedor de Comércio** campo suspenso do assistente do importador (usando o `commerceProvider` como um nome).

Quando um importador/provedor de comércio específico estiver disponível na lista suspensa, todos os dados complementares necessários devem ser definidos (dependendo do tipo de importador) em:

* `/apps/commerce/gui/content/catalogs/importblueprintswizard/importers`
* `/apps/commerce/gui/content/products/importproductswizard/importers`

A pasta sob o `importers` A pasta deve corresponder ao nome do importador; por exemplo:

* `.../importproductswizard/importers/geometrixx/.content.xml`

O formato do arquivo de importação de origem é definido pelo importador. Ou o importador pode estabelecer uma conexão (por exemplo, WebDAV ou http) com o mecanismo de comércio.

## Funções {#roles}

O sistema integrado atende às seguintes funções para manter os dados:

* Usuário do Gerenciamento de Informações do Produto (PIM) que mantém:

   * Informações do produto.
   * Taxonomia, categorização, aprovação.
   * Interage com o gerenciamento de ativos digitais.
   * Preços - geralmente, isso vem de um sistema ERP e não é explicitamente mantido no sistema de comércio.

* Autor/Gerente de marketing que mantém:

   * Conteúdo de marketing para todos os canais.
   * Promoções.
   * Vouchers.
   * Campanhas.

* Surfista/consumidor que:

   * Exibe as informações do produto.
   * Coloca itens no carrinho de compras.
   * Verifica seus pedidos.
   * Espera-se o cumprimento do pedido.

Embora a localização real possa depender da implementação; por exemplo, genérico ou com um mecanismo de comércio eletrônico:

![chlimage_1-6](/help/sites-administering/assets/chlimage_1-6.png)

## Produtos {#products}

### Dados do produto versus dados de marketing {#product-data-versus-marketing-data}

#### Categorias estruturais versus de marketing {#structural-versus-marketing-categories}

Se as duas categorias a seguir puderem ser diferenciadas, isso permitirá esclarecer os URLs com uma estrutura significativa (árvores de `cq:Page` nós) e, portanto, muito próximo do gerenciamento de conteúdo AEM clássico):

* *Categorias estruturais

   A árvore de categorias que define *o que é um produto*; por exemplo:

   `/products/mens/shoes/sneakers`

* *Marketing* categorias

   Todas as outras categorias a *o produto pode pertencer a*; por exemplo:

   `/special-offers/christmas/shoes`)

### Data do produto {#product-data}

Para retratar e gerenciar seu produto, você precisará ter uma variedade de informações sobre ele.

Os dados do produto podem ser:

* mantida diretamente no AEM (genérico).
* mantido no mecanismo de comércio eletrônico e disponibilizado no AEM.

   Dependendo do tipo de dados, ele está [sincronizado](#catalog-maintenance-data-synchronization) se necessário, ou acessado diretamente; por exemplo, dados altamente voláteis e críticos, como preços de produtos, são recuperados do mecanismo de comércio eletrônico em cada solicitação de página para garantir que eles estejam sempre atualizados.

Em ambos os casos, quando os dados do produto foram inseridos/importados para o AEM, eles podem ser vistos na variável **Produtos** console. Aqui, as visualizações de cartão e lista de um produto mostram informações como:

* a imagem
* o código SKU
* quando modificada pela última vez

![chlimage_1-7](/help/sites-administering/assets/chlimage_1-7.png)

### Variantes do produto {#product-variants}

Para os produtos adequados, também podem ser mantidas informações sobre as variantes. Por exemplo, para roupas, as diferentes cores disponíveis são mantidas como variantes:

![ecommerceproductvariants](/help/sites-administering/assets/ecommerceproductvariants.png)

### Atributos do produto {#product-attributes}

Os atributos individuais mantidos sobre cada produto podem depender do mecanismo de comércio eletrônico que está sendo usado e da implementação AEM. Elas estão disponíveis (conforme o caso) ao visualizar as páginas do produto e/ou editar as informações do produto e podem incluir:

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

   Informações sobre ERP (Enterprise Resource Planning, planejamento de recursos empresariais).

   * **SKU**

      Informações sobre a unidade de manutenção de estoque (SKU).

   * **Cor**
   * **Tamanho**
   * **Preço**

      O preço unitário do produto.

* **Resumo**

   Um resumo dos recursos do produto.

* **Recursos**

   Detalhes mais completos sobre os recursos do produto.

### Ativos do produto {#product-assets}

Uma seleção de ativos pode ser mantida para produtos individuais. Geralmente, isso inclui imagens e vídeos.

## Catálogos {#catalogs}

Um catálogo agrupa os dados do produto para facilitar o gerenciamento e a representação no comprador. Muitas vezes um catálogo é estruturado de acordo com atributos como idioma, área geográfica, marca, estação, hobby, esporte, entre muitos outros.

### Estrutura do catálogo {#catalog-structure}

#### Catálogos em vários idiomas {#catalogs-in-multiple-languages}

AEM suporta conteúdo de produto em vários idiomas. Ao solicitar dados, a estrutura de integração recupera o idioma da árvore atual (por exemplo, `en_US` para páginas em `/content/geometrixx-outdoors/en_US`).

Para uma loja em vários idiomas, você pode importar o catálogo para cada árvore de idioma individualmente (ou copiá-lo por meio de [MSM](/help/sites-administering/msm.md)).

#### Catálogos para várias marcas {#catalogs-for-multiple-brands}

Assim como em idiomas, grandes empresas multinacionais podem precisar atender a várias marcas.

#### Catálogos por tags {#catalogs-by-tags}

Tags também podem ser usadas para agrupar produtos em um catálogo. Eles podem ser usados para catálogos mais dinâmicos, como ofertas sazonais.

### Configuração do Catálogo (Importação Inicial) {#catalog-setup-initial-import}

Dependendo da sua implementação, você pode importar os dados do produto necessários para o seu catálogo básico para o AEM de:

* um arquivo CSV (para a implementação genérica)
* o mecanismo de comércio eletrônico

### Manutenção do catálogo (Sincronização de dados) {#catalog-maintenance-data-synchronization}

Outras alterações nos dados do produto serão inevitáveis:

* para a implementação genérica, eles podem ser gerenciados com o [editor de produto](/help/commerce/cif-classic/administering/generic.md#editing-product-information)
* ao usar um [Mecanismo de comércio eletrônico as alterações devem ser sincronizadas](#data-synchronization-with-an-ecommerce-engine-ongoing)

#### Sincronização de dados com um mecanismo de comércio eletrônico (em andamento) {#data-synchronization-with-an-ecommerce-engine-ongoing}

Após a importação inicial, as alterações nos dados do produto são inevitáveis.

Ao usar um mecanismo de comércio eletrônico, os dados do produto são mantidos lá e precisam estar disponíveis no AEM. Esses dados do produto precisam ser sincronizados quando as atualizações forem feitas.

Isso pode depender do tipo de dados:

* A [a sincronização periódica é usada juntamente com um feed de dados de alterações](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#product-synchronization-and-publishing).

   Além disso, é possível selecionar atualizações específicas para uma atualização expressa.

* Dados altamente voláteis, como informações de preço, são recuperados do mecanismo de comércio para cada solicitação de página, para garantir que estejam sempre atualizados.

### Catálogos - Desempenho e dimensionamento {#catalogs-performance-and-scaling}

Importar um catálogo grande com um alto número de produtos (geralmente mais de 100.000) de um mecanismo de comércio eletrônico (PIM) pode afetar o sistema devido ao grande número de nós. Ela também pode retardar a instância de criação se os produtos tiverem ativos associados (por exemplo, imagens de produto). Isso se deve ao fato de que o pós-processamento desses ativos consome muita CPU e memória.

Há várias estratégias que você pode escolher para solucionar esses problemas:

* [Agrupamento](#bucketing) - para atender ao grande número de nós
* [Descarregar o pós-processamento do ativo para uma instância dedicada](#offload-asset-post-processing-to-a-dedicated-instance)
* [Importar somente dados do produto](#only-import-product-data)
* [Importar controle e salvar em lote](#import-throttling-and-batch-saves)
* [Teste de desempenho](#performance-testing)
* [Desempenho - Diversos](#performance-miscellaneous)

#### Agrupamento {#bucketing}

Se um nó JCR tiver muitos nós filhos diretos (por exemplo, 1000 e mais), os buckets (pastas fantasmas) serão necessários para garantir que o desempenho não seja afetado. Elas são geradas de acordo com um algoritmo ao importar.

Esses buckets assumem a forma de pastas fantasmas que são introduzidas na estrutura do catálogo, mas podem ser configuradas para que não apareçam em URLs públicos.

#### Descarregar o pós-processamento do ativo para uma instância dedicada {#offload-asset-post-processing-to-a-dedicated-instance}

Esse cenário envolve a configuração de duas instâncias de autor:

1. Instância de autor principal

   Importa dados do produto do PIM, em que o pós-processamento dos caminhos de ativos está desativado.

1. Instância dedicada do autor do DAM

   Importa e pós-processa ativos de produto do PIM, em seguida, os replica de volta para a instância do autor principal para uso.

![Diagrama de arquitetura](/help/sites-administering/assets/chlimage_1-8.png)

#### Importar somente dados do produto {#only-import-product-data}

Nos casos em que os produtos não contêm ativos (imagens) a serem importados, é possível importar os dados do produto sem ser afetado pelo pós-processamento do ativo.

![Diagrama de arquitetura](/help/sites-administering/assets/chlimage_1-9.png)

#### Teste de desempenho {#performance-testing}

Os testes de desempenho devem ser considerados nas implementações AEM eCommerce:

* Ambiente do autor:

   A atividade de segundo plano (por exemplo, importação) pode ocorrer ao mesmo tempo que a atividade normal do usuário (por exemplo, edição de página) e mesmo que o desempenho de front-end seja (em geral) dado uma prioridade mais alta, o mau desempenho visto por autores online pode levar à frustração capaz de bloquear uma decisão de ativação.

* Ambiente de publicação:

   A replicação é um processo essencial para garantir que o conteúdo seja publicado de forma rápida e confiável. Isso pode ser afetado pela forma como o autor agrupa o conteúdo a ser publicado.

* Front-end:

   A mistura de invalidações de front-end e cache pode levar a surpresas de desempenho. Testar ajuda a evitar isso.

Observe que esse teste de desempenho requer conhecimento e análise de seu público-alvo:

* Volumes de conteúdo

   * Assets
   * Produtos e SKUs da I18ned localizados

* Atividade do usuário:

   * Edição em massa
   * Publicação em massa
   * Solicitações de pesquisa intensa

* Processos em segundo plano

   * Importações
   * Atualizações de sincronização (por exemplo, preços)

* Requisitos de manutenção (backup, otimização do Tar PM, coleta de lixo do armazenamento de dados etc.)

#### Desempenho - Diversos {#performance-miscellaneous}

Para todas as implementações, os seguintes pontos podem ser considerados:

* Como produtos, unidades de manutenção de estoque e categorias podem ser numerosas, tente usar o menor número possível de nós para modelar o conteúdo.

   Quanto mais nós você tiver, mais flexível será o seu conteúdo (por exemplo, parsys). No entanto, tudo é uma compensação e você precisa de flexibilidade individual (por padrão) ao manipular (por exemplo) produtos 30 mil?

* Evite a duplicação o máximo possível (consulte a localização) ou, quando fizer isso, pense em quantos nós a duplicação resultará.
* Tente marcar o conteúdo o máximo possível para preparar a otimização do query.

   Por exemplo:

   `/content/products/france/fr/shoe/reebok/pump/46 SKU`

   deve ter uma tag por nível de conteúdo (ou seja, país, idioma, categoria, marca, produto). Procurando por

   `//element(*,my:Sku)[@country=’france’ and @language=’fr’`

   e

   `@category=’shoe’ and @brand=’reebok’ and @product=’pump’]`

   será drasticamente mais rápido do que procurar por

   `/jcr:root/content/france/fr/shoe/reebok/pump/element(*,my:Sku)`

* Em sua pilha técnica, planeje modelos e serviços de acesso a conteúdo muito fatorizados. Essa é uma prática recomendada geral, mas é ainda mais crucial, pois você pode, em fases de otimização, adicionar caches de aplicativos para dados que são lidos com muita frequência (e com os quais não deseja preencher o cache do pacote).

   Por exemplo, o gerenciamento de atributos é frequentemente um bom candidato para armazenamento em cache, pois se refere a dados atualizados por meio da importação de produtos.
* Considere o uso de [páginas de proxy](#proxy-pages).

### Páginas da seção de catálogo {#catalog-section-pages}

As seções de catálogo fornecem a você, por exemplo:

* uma introdução (imagem e/ou texto) à categoria; isso também pode ser usado para banners e teasers para promover ofertas especiais
* links para os produtos individuais dessa categoria
* links para as outras categorias

![ecommerce_categoryrunning](/help/sites-administering/assets/ecommerce_categoryrunning.png)

### Páginas de produto {#product-pages}

As páginas do produto fornecem informações abrangentes sobre produtos individuais. As atualizações dinâmicas do também são refletidas; por exemplo, alterações de preço registradas no mecanismo de comércio eletrônico.

As páginas do produto são páginas AEM que usam a variável **Produto** componente; por exemplo, dentro do **Produto comercial** modelo:

![ecommerce_nairobirunnersgreen](/help/sites-administering/assets/ecommerce_nairobirunnersgreen.png)

O componente Produto fornece:

* Informações gerais sobre o produto; incluindo texto e imagens.
* Preços; isso geralmente é recuperado do mecanismo de comércio eletrônico sempre que a página é exibida/atualizada.
* Informações sobre a variante do produto; por exemplo, cor e tamanho.

Essas informações permitem que o comprador selecione o seguinte ao adicionar um item à sua cesta:

* Variantes de cor e tamanho
* Quantidade

#### Páginas de aterrissagem do produto {#product-landing-pages}

São páginas AEM que fornecem principalmente informações estáticas; por exemplo, uma introdução e uma visão geral com links para as páginas de produto subjacentes.

### Componente do produto {#product-component}

O **Produto** pode ser adicionado a qualquer página com uma página principal que forneça os metadados necessários (ou seja, os caminhos para `cartPage` e `cartObject`). No local da demonstração, Geometrixx Outdoors, isso é fornecido por `UserInfo.jsp`.

O **Produto** também pode ser personalizado de acordo com suas necessidades individuais.

### Páginas de proxy {#proxy-pages}

As páginas de proxy são usadas para simplificar a estrutura do repositório e otimizar o armazenamento para catálogos grandes.

A criação de um catálogo usará dez nós por produto, pois fornece componentes individuais para cada produto que você pode atualizar e personalizar no AEM. Esse grande número de nós pode se tornar um problema se o catálogo contiver centenas ou até mesmo milhares de produtos. Para evitar problemas, você pode criar o catálogo usando páginas de proxy.

As páginas de proxy usam uma estrutura de dois nós ( `cq:Page` e `jcr:content`) que não contém o conteúdo real do produto. O conteúdo é gerado, no momento da solicitação, referenciando os dados do produto e a página do modelo.

No entanto, há uma compensação. Não será possível personalizar as informações do produto no AEM, um modelo padrão (definido para o site) será usado.

>[!NOTE]
>
>Não haverá problemas se você importar um catálogo grande sem páginas de proxy.
>
>Você pode converter de uma metodologia para outra a qualquer momento. Também é possível converter uma subseção do catálogo.

## Promoções e Vouchers {#promotions-and-vouchers}

### Vouchers {#vouchers}

Os vendedores são um método experimentado e testado de oferecer descontos para atrair compradores para realizar uma compra e/ou recompensar a fidelidade do cliente.

* Fornecimento de cupom:

   * Um código de comprovante (a ser digitado no carrinho pelo comprador).
   * Um rótulo de comprovante (a ser exibido depois que o comprador o tiver inserido no carrinho).
   * Um caminho de promoção (que define a ação que o comprovante aplica).

* Os mecanismos de comércio externo também podem fornecer comprovantes.

No AEM:

* Um comprovante é um componente baseado em página criado/editado com o console Sites.
* O **Voucher** componente fornece:

   * Um renderizador para a administração de vouchers; isso mostra os comprovantes que estão no carrinho.
   * As caixas de diálogo de edição (formulário) para administrar (adicionar/remover) os comprovantes.
   * As ações necessárias para adicionar/remover comprovantes ao/do carrinho.

* Os vendedores não têm suas próprias datas/horas de início e término, mas usam aquelas de suas campanhas pai.

>[!NOTE]
>
>AEM usa o termo **Voucher**, isto é sinônimo do termo **Cupom**.

### Promoções {#promotions}

As promoções, juntamente com comprovantes, permitem que você realize cenários como:

* Uma empresa fornece preços personalizados para funcionários, que é uma lista artesanal de usuários.
* Os clientes de longo prazo recebem descontos em todos os pedidos.
* Um preço de venda oferecido durante um período bem definido.
* Um cliente recebe um comprovante quando seu pedido anterior excedeu um valor específico.
* Um cliente que compra *product-X* é oferecido um desconto em *produto-Y* (produtos de par).

Geralmente, as promoções não são mantidas pelos gerentes de informações do produto, mas pelos gerentes de marketing:

* Uma Promoção é um componente baseado em página que é criado/editado com o console Sites. &quot;
* Fornecimento de promoções:

   * Uma prioridade
   * Um caminho de manipulador de promoção

* É possível conectar promoções a uma campanha para definir sua data/hora de ativação/desativação.
* É possível conectar promoções a uma experiência para definir seus segmentos.
* As promoções não conectadas a uma experiência não serão acionadas por conta própria, mas ainda podem ser acionadas por um Voucher.
* O componente Promoção contém:

   * renderizadores e diálogos para administração de promoção
   * subcomponentes para renderizar e editar parâmetros de configuração específicos dos manipuladores de promoção

AEM as promoções também são integradas ao [Campaign Management](/help/sites-authoring/personalization.md):

* a [campanha](/help/sites-authoring/personalization.md) especifica os tempos de ativação/desativação
* [experiências](/help/sites-authoring/personalization.md) *within* a campanha é usada para agrupar ativos (páginas de grupo, promoções etc.) de acordo com o segmento de público-alvo ao qual elas correspondem

Uma promoção pode ser realizada em uma experiência ou diretamente na campanha:

* Se uma promoção for mantida em uma experiência, ela poderá ser aplicada automaticamente a um segmento de público-alvo.

   Por exemplo, no site de amostra geometrixx-outdoors, a promoção:

   `/content/campaigns/geometrixx-outdoors/big-spender/ordervalueover100/free-shipping`

   O está em uma experiência e, portanto, é acionado automaticamente sempre que o segmento ( `ordervalueover100`) resolve.

* Se uma promoção não aparecer em uma experiência (somente na campanha), ela não poderá ser aplicada automaticamente a um público-alvo. No entanto, ele ainda poderá ser acionado se o comprador inserir um comprovante em seu carrinho e esse comprovante fizer referência à promoção.

   Por exemplo, a promoção:

   `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

   O está fora de uma experiência e, portanto, nunca é acionado automaticamente (ou seja: com base na segmentação). No entanto, ele é referenciado pelos comprovantes que podem ser encontrados em várias experiências dentro da campanha do artigo. Inserir esses códigos de comprovante no carrinho resultará no acionamento da promoção.

>[!NOTE]
>
>[promoções de híbridos](https://www.hybris.com/modules/promotion) e [vouchers de híbridos](https://www.hybris.com/en/modules/voucher) cubra tudo o que influencia o carrinho de compras e está relacionado aos preços. O conteúdo de marketing específico de promoção (como banners, etc.) não faz parte da promoção de híbridos.

## Personalização {#personalization}

### Registro e contas do cliente {#customer-registration-and-accounts}

Quando um comprador é registrado, os detalhes da conta precisam ser sincronizados entre o AEM e o mecanismo de comércio eletrônico. Os dados confidenciais são mantidos independentemente, mas os perfis são compartilhados:

![chlimage_1-10](/help/sites-administering/assets/chlimage_1-10.png)

O mecanismo exato pode depender do cenário:

1. As contas de usuário existem em ambos os sistemas:

   1. Nenhuma ação necessária.

1. A conta de usuário existe somente no AEM:

   1. O usuário será criado no mecanismo de comércio eletrônico com a mesma ID de conta e uma senha aleatória que será armazenada no AEM.
   1. A senha aleatória é necessária, já que o AEM tenta fazer logon no mecanismo de comércio eletrônico na primeira chamada (por exemplo, quando uma página de produto é solicitada e o mecanismo de comércio eletrônico é referenciado pelo preço). Como isso acontece após o logon AEM, a senha não está disponível.

1. A conta de usuário só existe no mecanismo de comércio eletrônico:

   1. A conta será criada em AEM com a mesma ID de conta e senha.

Ao usar um mecanismo de comércio eletrônico, o AEM armazena somente a ID da conta e a senha (opcionalmente, um grupo de usuários). Todas as outras informações são armazenadas no mecanismo de comércio eletrônico.

>[!NOTE]
>
>Ao usar um mecanismo de comércio eletrônico, é necessário garantir que as contas criadas para usuários que fazem logon em uma instância de AEM sejam replicadas (por exemplo, via workflows) para qualquer outra instância de AEM que se comunique com esse mecanismo.
>
>Caso contrário, essas outras instâncias de AEM também tentarão criar contas para os mesmos usuários no mecanismo. Essas ações falharão com uma `DuplicateUidException` vindo do motor.

### Inscrição no Cliente {#customer-sign-up}

Geralmente, a inscrição é necessária para o comprador ter acesso ao carrinho de compras. Isso requer o registro (Criar conta) para que uma conta específica do cliente possa ser criada.

![chlimage_1-11](/help/sites-administering/assets/chlimage_1-11.png)

>[!NOTE]
>
>Um carrinho de compras anônimo e o check-out também são suportados.

### Logon do cliente {#customer-sign-in}

Após a inscrição, o comprador pode fazer logon com a conta para que as ações possam ser rastreadas e os pedidos sejam atendidos.

![chlimage_1-12](/help/sites-administering/assets/chlimage_1-12.png)

### Logon único {#single-sign-on}

O Logon único (SSO) é fornecido, para que os autores sejam conhecidos tanto no AEM quanto no sistema de eCommerce, sem ter que fazer logon duas vezes.

### myAccount {#myaccount}

Os dados de transação do mecanismo de comércio eletrônico são combinados com informações pessoais sobre o comprador. O AEM usa alguns desses dados como dados de perfil. A ação de um formulário no AEM grava informações de volta no mecanismo de comércio eletrônico.

Há uma página que permite gerenciar facilmente as informações de sua conta. Você pode acessá-lo clicando em **Minha conta** na parte superior de uma página geometrixx ou navegando até `/content/geometrixx-outdoors/en/user/account.html`.

![chlimage_1-13](/help/sites-administering/assets/chlimage_1-13.png)

### Agenda de endereços {#address-book}

Seu site precisará armazenar uma seleção de endereços; incluindo delivery, cobrança e endereços alternativos. Isso pode ser implementado usando formulários com base no formato de endereço padrão ou você pode usar o componente Catálogo de endereços fornecido pelo AEM.

Este componente Catálogo de Endereços permite:

* editar endereços no livro
* selecione um endereço do livro para o endereço de entrega
* selecione um endereço do livro para o endereço de cobrança

Você pode escolher o endereço que deseja como padrão.

O componente do catálogo de endereços pode ser acessado do **Minha conta** clicando em **Catálogo de endereços** ou navegando até `/content/geometrixx-outdoors/en/user/account/address-book.html`.

![chlimage_1-14](/help/sites-administering/assets/chlimage_1-14.png)

Você pode clicar em **Adicionar novo endereço...** para adicionar um novo endereço em seu catálogo de endereços. Ele abre um formulário que pode ser preenchido e clica em **Adicionar endereço**.

>[!NOTE]
>
>Você pode inserir vários endereços em seu Catálogo de endereços.

O Catálogo de endereços é usado ao fazer check-out do carrinho:

![chlimage_1-15](/help/sites-administering/assets/chlimage_1-15.png)

Os endereços são mantidos abaixo `user_home/profile/addresses`.
Por exemplo, para o Alison Parker, estaria em /home/users/geometrixx/aparker@geometrixx.info/profile/addresses

Você pode escolher qual endereço deseja como padrão, essas informações persistem no perfil do comprador em vez de no endereço . A propriedade do perfil `address.default` é definida com o caminho do endereço selecionado para o valor.

### Preços específicos do cliente {#customer-specific-pricing}

O mecanismo de comércio eletrônico usa o contexto (essencialmente as informações do comprador) para determinar o preço que está retendo e, em seguida, fornece as informações corretas ao AEM.

## Carrinho de compras e pedidos {#shopping-cart-and-orders}

Ao comprar, o comprador navegará pelas páginas do produto e selecionará itens para colocá-los no carrinho de compras. Quando eles prosseguem com o check-out, um pedido pode ser feito.

### Compradores anônimos {#anonymous-shoppers}

Um cliente anônimo pode:

* Exibir produtos
* Adicionar produtos ao carrinho
* Executar check-out para colocar seu pedido

>[!NOTE]
>
>Dependendo da configuração de suas informações de endereço da instância ou do registro do cliente, pode ser necessário antes do check-out.

### Compradores registrados {#registered-shoppers}

Um cliente registrado pode:

* Faça logon em sua conta
* Exibir produtos
* Adicionar produtos ao carrinho
* Executar check-out para colocar seu pedido
* Exibir e rastrear pedidos anteriores

### Visão geral do conteúdo do carrinho de compras {#shopping-cart-content-overview}

O carrinho de compras fornece:

* uma visão geral dos itens selecionados
* links para as páginas do produto para os itens selecionados
* Capacidade para:

   * atualizar o número/a quantidade de itens individuais
   * remover itens individuais

![ecommerce_shoppingcart](/help/sites-administering/assets/ecommerce_shoppingcart.png)

O carrinho de compras é salvo de acordo com o mecanismo que está sendo usado:

* AEM genérico armazena o carrinho em um cookie.
* Determinados mecanismos de comércio eletrônico podem armazenar o carrinho em uma sessão.

Em ambos os casos, os itens permanecem no carrinho (e podem ser restaurados) por meio do logon/logout (mas somente na mesma máquina/navegador). Por exemplo:

* navegar como `anonymous` e adicionar produtos ao carrinho
* fazer logon como `Allison Parker` - o carrinho está vazio
* adicionar produtos ao carrinho
* sair - o carrinho mostrará os produtos para `anonymous`

* entrar novamente como `Allison Parker` - seus produtos são restaurados

>[!NOTE]
>
>Um carrinho anônimo só pode ser restaurado no mesmo computador/navegador.

>[!NOTE]
>
>Não é recomendável testar a restauração do conteúdo do carrinho com a função `admin` , pois isso pode entrar em conflito com a `admin` conta do mecanismo de comércio eletrônico (por exemplo, híbridos).

>[!NOTE]
>
>os híbridos podem ser configurados para remover carrinhos pendentes após um período definido.

Antes do check-out, as alterações de preço são refletidas (em ambos os sistemas) à medida que ocorrem.

### Informações do pedido {#order-information}

Dependendo das informações de implementação sobre um pedido que é mantido no mecanismo de comércio eletrônico ou no AEM, essas informações são renderizadas pelo AEM.

É armazenada uma variedade de informações, que podem incluir:

* **ID do pedido**

   O número de referência do pedido.

* **Instalado**

   A data em que o pedido foi feito.

* **Status**

   O status do pedido; por exemplo, Enviado.

* **Moeda**

   A moeda do pedido.

* **Itens de conteúdo**

   Uma lista de itens pedidos.

* **Subtotal**

   O custo total dos itens solicitados.

* **Imposto**

   A quantia de quaisquer impostos devidos no pedido.

* **Envio**

   Custos de envio.

* **Total**

   O valor total do pedido; itens encomendados, impostos e compras.

* **Endereço de cobrança**

   O endereço para o qual a fatura deve ser enviada.

* **Token de pagamento**

   O método de pagamento.

* **Status do pagamento**

   O status do pagamento.

* **Endereço de envio**

   Endereço para onde as mercadorias devem ser expedidas.

* **Método de envio**

   Método de navegação; por exemplo, terra, mar ou ar.

* **Número de rastreamento**

   Qualquer número de rastreamento usado pela empresa de entrega.

* **Link de rastreamento**

   O link usado para rastrear o pedido enquanto está sendo enviado.

>[!NOTE]
>
>Os campos usados no assistente de criação de pedido dependem de haver um scaffolding otimizado ao toque definido para o local. No exemplo genérico, isso pode ser encontrado em:
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`

Quando a ordem é mantida dentro AEM console Ordem, o mostra o seguinte para cada pedido:

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

Depois de receber o delivery da ordem, os compradores também podem desejar visualizar o histórico de pedidos feitos durante um período.

O cumprimento e o rastreamento do pedido geralmente são gerenciados pelo mecanismo de comércio eletrônico. As informações podem ser exibidas AEM usando o componente Histórico do pedido , que mostra todos os detalhes relevantes, incluindo os comprovantes e as promoções aplicadas. Por exemplo:

![chlimage_1-17](/help/sites-administering/assets/chlimage_1-17.png)

## Check-out {#checkout}

O check-out é implementado com formulários de AEM padrão. Isso permite que o gerente de marketing personalize a experiência com conteúdo de marketing.

O eCommerce gerencia o processo de finalização com entrada dos formulários AEM.

### Segurança de pagamento {#payment-security}

Os detalhes do pagamento, incluindo as informações sobre cartões de crédito, são geralmente geridos pelo mecanismo de comércio eletrônico. AEM encaminhar essas informações transacionais para o motor (a partir do local em que são enviadas para um serviço de processamento de pagamentos).

A conformidade com o PCI (Payment Card Industry, setor de cartões de pagamento) pode ser alcançada.

### Confirmação do despacho {#confirmation-of-order}

A ordem é confirmada na tela e pode ser rastreada com a variável [rastreamento de pedidos](#order-tracking).

## Pesquisar {#search-features}

![chlimage_1-18](/help/sites-administering/assets/chlimage_1-18.png)

Como AEM usa páginas padrão para produtos, você pode usar o componente de pesquisa padrão para criar uma página de pesquisa.

Se você precisar de uma implementação mais completa, poderá:

* Estenda o componente de pesquisa padrão com a funcionalidade necessária.
* Implemente o método de pesquisa no `CommerceService` e, em seguida, use o componente de pesquisa Comércio eletrônico na sua página de pesquisa.

Ao usar um mecanismo de comércio eletrônico, a API de pesquisa de comércio eletrônico pode ser totalmente implementada na solução de mecanismo de comércio eletrônico, para que você possa usar o componente de pesquisa de comércio eletrônico fornecido pronto para uso. A pesquisa facetada permite pesquisar o JCR e/ou o mecanismo:
