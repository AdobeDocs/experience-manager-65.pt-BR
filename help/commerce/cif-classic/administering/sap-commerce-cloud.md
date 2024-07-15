---
title: Usar AEM com Commerce Cloud SAP
description: Saiba como usar o Adobe Experience Manager com o SAP Commerce Cloud.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 1%

---

# COMMERCE CLOUD SAP{#sap-commerce-cloud}

Após a instalação, é possível configurar sua instância:

1. [Configurar a Pesquisa Facetada para Geometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [Configurar a Versão de Catálogo](#configure-the-catalog-version).
1. [Configurar a estrutura de importação](#configure-the-import-structure).
1. [Configurar os Atributos do Produto a serem Carregados](#configure-the-product-attributes-to-load).
1. [Importando os dados do produto](#importing-the-product-data).
1. [Configurar o Importador de Catálogo](#configure-the-catalog-importer).
1. Use o [importador para importar o catálogo](#catalog-import) para um local específico no AEM.

## Configurar a pesquisa facetada para Geometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>Isso não é necessário para o hybris 5.3.0.1 e posteriores.

1. Em seu navegador, navegue até o **console de gerenciamento de hibris** em:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. Na barra lateral, selecione **Sistema**, depois **Pesquisa de facetas** e depois **Configuração de pesquisa de facetas**.
1. **Abrir Editor** para a **Configuração Solr de Exemplo para clothescatalog**.

1. Em **Versões de catálogo**, use **Adicionar versão de catálogo** para adicionar `outdoors-Staged` e `outdoors-Online` à lista.
1. **Salve** a configuração.
1. Abra **Tipos de item da SOLR** para adicionar **Classificações da SOLR** a `ClothesVariantProduct`:

   * relevância (&quot;Relevância&quot;, pontuação)
   * name-asc (&quot;Name (ascending)&quot;, name)
   * name-desc (&quot;Name (descending)&quot;, name)
   * price-asc (&quot;Preço (crescente)&quot;, priceValue)
   * price-desc (&quot;Preço (decrescente)&quot;, priceValue)

   >[!NOTE]
   >
   >Use o menu de contexto (normalmente, clique com o botão direito do mouse) para selecionar `Create Solr sort`.
   >
   >Para o Hybris 5.0.0, abra a guia `Indexed Types`, clique duas vezes em `ClothesVariantProduct` e, em seguida, na guia `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. Na guia **Tipos Indexados**, defina o **Tipo Composto** como:

   `Product - Product`

1. Na guia **Tipos Indexados**, ajuste as **consultas do Indexador** para `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. Na guia **Tipos Indexados**, ajuste as **consultas do Indexador** para `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. Na guia **Tipos Indexados**, ajuste a faceta `category`. Clique duas vezes na última entrada da lista de categorias para abrir a guia **Propriedade indexada**:

   >[!NOTE]
   >
   >Para o hybris 5.2, verifique se o atributo `Facet` na tabela Propriedades está selecionado de acordo com a captura de tela abaixo:

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. Abra a guia **Configurações da faceta** e ajuste os valores do campo:

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **Salve** as alterações.
1. Novamente de **tipos de Item SOLR**, ajuste a faceta `price` de acordo com as seguintes capturas de tela. Assim como em `category`, clique duas vezes em `price` para abrir a guia **Propriedade indexada**:

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. Abra a guia **Configurações da faceta** e ajuste os valores do campo:

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **Salve** as alterações.
1. Abrir **Sistema**, **Pesquisa de facetas** e **Assistente de operação do indexador**. Inicie um cronjob:

   * **Operação do indexador**: `full`
   * **Configuração Solr**: `Sample Solr Config for Clothes`

## Configurar a versão do catálogo {#configure-the-catalog-version}

A **versão de catálogo** ( `hybris.catalog.version`) importada pode ser configurada para o serviço OSGi:

**Configuração CQ Commerce Hybris de**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**Versão de catálogo** definida como `Online` ou `Staged` (o padrão).

>[!NOTE]
>
>Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos. Consulte também o console para obter uma lista completa de parâmetros configuráveis e seus padrões.

A saída do log fornece feedback sobre as páginas e os componentes criados e relata possíveis erros.

## Configurar a estrutura de importação {#configure-the-import-structure}

A lista a seguir mostra uma estrutura de exemplo (de ativos, páginas e componentes) que é criada por padrão:

```shell
+ /content/dam/path/to/images
  + 12345.jpg (dam:Asset)
    + ...
  + ...
+ /content/site/en
  - cq:commerceProvider = "hybris"
  - cq:hybrisBaseStore = "basestore"
  - cq:hybrisCatalogId = "catalog"
  + category1 (cq:Page)
    + jcr:content (cq:PageContent)
      - jcr:title = "Category 1"
    + category11 (cq:Page)
      + jcr:content (cq:PageContent)
        - jcr:title = "Category 1.1"
      + 12345 (cq:Page)
        + jcr:content (cq:PageContent)
          + par
            + product (nt:unstructured)
              - cq:hybrisProductId = "12345"
              - sling:resourceType = "commerce/components/product"
              + image (nt:unstructured)
                - sling:resourceType = "commerce/components/product/image"
                - fileReference = "/content/dam/path/to/images/12345.jpg"
              + 12345.1-S (nt:unstructured)
                - cq:hybrisProductId = "12345.1-S"
                - sling:resourceType = "commerce/components/product"
                + image (nt:unstructured)
                  - sling:resourceType = "commerce/components/product/image"
                  - fileReference = "/content/dam/path/to/images/12345.1-S.jpg"
              + ...
```

Essa estrutura foi criada pelo serviço OSGi `DefaultImportHandler` que implementa a interface `ImportHandler`. Um manipulador de importação é chamado pelo importador real para criar produtos, variações de produtos, categorias, ativos e assim por diante.

>[!NOTE]
>
>Você pode [personalizar este processo implementando seu próprio manipulador de importação](#configure-the-import-structure).

A estrutura a ser gerada ao importar pode ser configurada para:

&quot;**Manipulador de Importação Padrão do Commerce Hybris do Day CQ**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos. Consulte também o console para obter uma lista completa de parâmetros configuráveis e seus padrões.

## Configurar os atributos do produto para carregar {#configure-the-product-attributes-to-load}

O analisador de resposta pode ser configurado para definir as propriedades e os atributos a serem carregados para produtos (variantes):

1. Configure o pacote OSGi:

   **Analisador de Resposta Padrão do Commerce Hybris do CQ**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   Aqui é possível definir várias opções e atributos necessários para carregar e mapear.

   >[!NOTE]
   >
   >Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos. Consulte também o console para obter uma lista completa de parâmetros configuráveis e seus padrões.

## Importação dos dados do produto {#importing-the-product-data}

Há várias maneiras de importar os dados do produto. Os dados do produto podem ser importados ao configurar inicialmente o ambiente ou após alterações serem feitas nos dados híbridos:

* [Importação completa](#full-import)
* [Importação incremental](#incremental-import)
* [Atualização expressa](#express-update)

As informações reais do produto importadas do hybris são mantidas no repositório em:

`/etc/commerce/products`

As seguintes propriedades indicam o link com hybris:

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>A implementação hybris (ou seja, `geometrixx-outdoors/en_US`) armazena apenas IDs de produto e outras informações básicas em `/etc/commerce`.
>
>O servidor hybris é referenciado sempre que as informações sobre um produto são solicitadas.

### Importação completa {#full-import}

1. Se necessário, exclua todos os dados existentes do produto usando o CRXDE Lite.

   1. Navegue até a subárvore que contém os dados do produto:

      `/etc/commerce/products`

      Por exemplo:

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. Exclua o nó que contém os dados do seu produto; por exemplo, `outdoors`.
   1. **Salvar tudo** para confirmar a alteração.

1. Abra o importador hybris no AEM:

   `/etc/importers/hybris.html`

   Por exemplo:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Configure os parâmetros necessários; por exemplo:

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. Clique em **Importar catálogo** para iniciar a importação.

   Quando terminar, você poderá verificar os dados importados em:

   ```
       /etc/commerce/products/outdoors
   ```

   Você pode abrir isso em CRXDE Lite; por exemplo:

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### Importação incremental {#incremental-import}

1. Verifique as informações contidas no AEM para os produtos relevantes, na subárvore apropriada em:

   `/etc/commerce/products`

   Você pode abrir isso em CRXDE Lite; por exemplo:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. No hybris, atualize as informações mantidas sobre os produtos relevantes.

1. Abra o importador hybris no AEM:

   `/etc/importers/hybris.html`

   Por exemplo:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Marque a caixa de seleção **Importação incremental**.
1. Clique em **Importar catálogo** para iniciar a importação.

   Quando terminar, você pode verificar os dados atualizados no AEM em:

   ```
       /etc/commerce/products
   ```


### Atualização expressa {#express-update}

O processo de importação pode levar muito tempo. Assim, como uma extensão da Sincronização de produto, você pode selecionar áreas específicas do catálogo para uma atualização expressa que é acionada manualmente. Isso usa o feed de exportação junto com a configuração de atributos padrão.

1. Verifique as informações contidas no AEM para os produtos relevantes, na subárvore apropriada em:

   `/etc/commerce/products`

   Você pode abrir isso em CRXDE Lite; por exemplo:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. No hybris, atualize as informações mantidas sobre os produtos relevantes.

1. Em hybris, adicione um ou mais produtos à Express Queue; por exemplo:

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. Abra o importador hybris no AEM:

   `/etc/importers/hybris.html`

   Por exemplo:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Marque a caixa de seleção **Atualização Expressa**.
1. Clique em **Importar catálogo** para iniciar a importação.

   Quando terminar, você pode verificar os dados atualizados no AEM em:

   ```
       /etc/commerce/products
   ```

## Configurar o importador de catálogo {#configure-the-catalog-importer}

O catálogo hybris pode ser importado para AEM, usando o importador em lote para catálogos hybris, categorias e produtos.

Os parâmetros usados pelo importador podem ser configurados para:

**Importador de Catálogo Commerce Hybris CQ do Dia**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos. Consulte também o console para obter uma lista completa de parâmetros configuráveis e seus padrões.

## Importação do catálogo {#catalog-import}

O pacote hybris vem com um importador de catálogo para configurar a estrutura da página inicial.

Isso está disponível em:

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

Devem ser fornecidas as seguintes informações:

* **Repositório base**
O identificador do armazenamento base configurado no hybris.

* **Catálogo**
O identificador do catálogo a ser importado.

* **Caminho raiz**
O caminho onde o catálogo deve ser importado.

## Remoção de um produto do catálogo {#removing-a-product-from-the-catalog}

Para remover um ou mais produtos do catálogo:

1. [Configurar o para o serviço OSGi](/help/sites-deploying/configuring-osgi.md) **Importador do Catálogo Commerce Hybris do Day CQ**; consulte também [Configurar o Importador do Catálogo](#configure-the-catalog-importer).

   Ative as seguintes propriedades:

   * **Habilitar remoção de produto**
   * **Habilitar remoção de ativos de produtos**

   >[!NOTE]
   >
   >Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos. Consulte também o console para obter uma lista completa de parâmetros configuráveis e seus padrões.

1. Inicialize o importador executando duas atualizações incrementais (consulte [Importação de Catálogo](#catalog-import)):

   * A primeira execução resulta em um conjunto de produtos alterados - indicado na lista de log.
   * Nenhum produto deve ser atualizado pela segunda vez.

   >[!NOTE]
   >
   >A primeira importação é inicializar as informações do produto. A segunda importação verifica se tudo funcionou e se o conjunto de produtos está pronto.

1. Verifique a página de categoria que contém o produto que você deseja remover. Os detalhes do produto devem estar visíveis.

   Por exemplo, a categoria a seguir mostra detalhes do produto Cajamara:

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Remova o produto no console hybris. Use a opção **Alterar status de aprovação** para definir o status como `unapproved`. O produto é removido do feed ao vivo.

   Por exemplo:

   * Abra a página [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * Selecionar o catálogo `Outdoors Staged`
   * Pesquisar por `Cajamara`
   * Selecione este produto e altere o status de aprovação para `unapproved`

1. Execute outra atualização incremental (consulte [Importação de catálogo](#catalog-import)). O log lista o produto excluído.
1. [Implante](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) o catálogo apropriado. A página do produto e do produto foi removida do AEM.

   Por exemplo:

   * Abrir:

     [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * Implantar o catálogo `Hybris Base`
   * Abrir:

     [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * O produto `Cajamara` foi removido da categoria `Bike`

1. Para restaurar o produto:

   1. No hybris, defina o status de aprovação novamente como **aprovado**
   1. No AEM:

      1. executar uma atualização incremental
      1. implante o catálogo apropriado novamente
      1. atualizar a página de categoria apropriada

## Adicionar a característica do histórico do pedido ao contexto do cliente {#add-order-history-trait-to-the-client-context}

Para adicionar o histórico de pedidos ao [contexto do cliente](/help/sites-developing/client-context.md):

1. Abra a [página de design de contexto do cliente](/help/sites-administering/client-context.md), através:

   * Abra uma página para edição e, em seguida, abra o contexto do cliente usando **Ctrl-Alt-c** (windows) ou **control-option-c** (Mac). Use o ícone de lápis no canto superior esquerdo do contexto do cliente para **Abrir a página de design do ClientContext**.
   * Navegue diretamente para [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [Adicione o **Componente de Histórico de Pedidos**](/help/sites-administering/client-context.md#adding-a-property-component) ao **Carro de Compras** t componente do contexto do cliente.
1. Você pode confirmar que o contexto do cliente está mostrando detalhes do seu histórico de pedidos. Por exemplo:

   1. Abra o [contexto do cliente](/help/sites-administering/client-context.md).
   1. Adicione um item ao carrinho.
   1. Conclua o check-out.
   1. Verifique o contexto do cliente.
   1. Adicione outro item ao carrinho.
   1. Navegue até a página de check-out:

      * O contexto do cliente mostra um resumo do histórico do pedido.
      * A mensagem &quot;Você é um cliente recorrente&quot; é exibida.

   >[!NOTE]
   >
   >A mensagem é percebida por:
   >
   >* Navegue até [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  A campanha consiste em uma experiência.
   >
   >* Clique no segmento ([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
   >
   >* O segmento é criado usando a característica **Order History Property**.
