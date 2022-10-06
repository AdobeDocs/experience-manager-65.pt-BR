---
title: Commerce Cloud SAP
seo-title: SAP Commerce Cloud
description: Saiba como usar o AEM com o SAP Commerce Cloud.
seo-description: Learn how to use AEM with SAP Commerce Cloud.
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
source-git-commit: 61691c300322edcdee33b121ca400e4c89256e45
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 1%

---

# Commerce Cloud SAP{#sap-commerce-cloud}

Após a instalação, você pode configurar sua instância:

1. [Configurar a pesquisa falhada para Geometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [Configurar a versão do catálogo](#configure-the-catalog-version).
1. [Configurar a estrutura de importação](#configure-the-import-structure).
1. [Configure os atributos do produto para serem carregados](#configure-the-product-attributes-to-load).
1. [Importação dos dados do produto](#importing-the-product-data).
1. [Configurar o Importador de Catálogo](#configure-the-catalog-importer).
1. Use o [importador para importar o catálogo](#catalog-import) em um local específico no AEM.

## Configurar a pesquisa falhada para Geometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>Isso não é necessário para os híbridos 5.3.0.1 e posteriores.

1. No seu navegador, navegue até o **console de gerenciamento de híbridos** em:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. Na barra lateral, selecione **Sistema**, em seguida **Pesquisa de facetas**, em seguida **Configuração de pesquisa de faceta**.
1. **Abrir editor** para **Exemplo de configuração Solr para o catálogo de roupas**.

1. Em **Versões do catálogo** use **Adicionar versão do catálogo** para adicionar `outdoors-Staged` e `outdoors-Online` à lista.
1. **Salve a configuração.**
1. Abrir **Tipos de item SOLR** para adicionar **Classificações SOLR** para `ClothesVariantProduct`:

   * relevância (&quot;Relevância&quot;, pontuação)
   * name-asc (&quot;Nome (crescente)&quot;, nome)
   * name-desc (&quot;Name (descending)&quot;, name)
   * price-asc (&quot;Price (crescente)&quot;, priceValue)
   * price-desc (&quot;Price (decrescente)&quot;, priceValue)

   >[!NOTE]
   >
   >Use o menu de contexto (geralmente, clique com o botão direito do mouse) para selecionar `Create Solr sort`.
   >
   >Para Hybris 5.0.0, abra o `Indexed Types` , clique duas vezes em `ClothesVariantProduct`, em seguida, na guia `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. No **Tipos indexados** defina a guia **Tipo composto** para:

   `Product - Product`

1. No **Tipos indexados** ajuste a guia **Consultas de indexador** para `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. No **Tipos indexados** ajuste a guia **Consultas de indexador** para `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. No **Tipos indexados** ajuste a guia `category` faceta. Clique duas vezes na última entrada na lista de categorias para abrir o **Propriedade indexada** guia :

   >[!NOTE]
   >
   >Para os híbridos 5.2, verifique se a variável `Facet` na tabela Propriedades é selecionado de acordo com a captura de tela abaixo:

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. Abra o **Configurações de faceta** e ajuste os valores do campo:

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **Salve as alterações.**
1. Novamente de **Tipos de item SOLR** ajuste o `price` faceta de acordo com as seguintes capturas de tela. Como com `category`, clique duas vezes em `price` para abrir o **Propriedade indexada** guia :

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. Abra o **Configurações de faceta** e ajuste os valores do campo:

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **Salve as alterações.**
1. Abrir **Sistema**, **Pesquisa de facetas**, em seguida **Assistente de operação do indexador**. Inicie um cronjob:

   * **Operação do indexador**: `full`
   * **Configuração Solr**: `Sample Solr Config for Clothes`

## Configurar a versão do catálogo {#configure-the-catalog-version}

O **Versão do catálogo** ( `hybris.catalog.version`) que é importado pode ser configurado para o serviço OSGi:

**Configuração de híbrido comercial do CQ do dia**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**Versão do catálogo** geralmente é definido como `Online` ou `Staged` (padrão).

>[!NOTE]
>
>Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; see [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos. Consulte também o console para obter uma lista completa de parâmetros configuráveis e seus padrões.

A saída do log fornece feedback sobre as páginas e os componentes criados e relata possíveis erros.

## Configurar a estrutura de importação {#configure-the-import-structure}

A listagem a seguir mostra uma estrutura de exemplo (de ativos, páginas e componentes) que é criada por padrão:

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

Essa estrutura é criada pelo serviço OSGi `DefaultImportHandler` que implementa o `ImportHandler` interface. Um manipulador de importação é chamado pelo importador real para criar produtos, variações de produto, categorias, ativos, etc.

>[!NOTE]
>
>Você pode [personalize esse processo implementando seu próprio manipulador de importação](#configure-the-import-structure).

A estrutura a ser gerada ao importar pode ser configurada para:

&quot;**Manipulador de Importação Padrão de Híbris do Comércio do Day CQ**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; see [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos. Consulte também o console para obter uma lista completa de parâmetros configuráveis e seus padrões.

## Configure os atributos do produto para serem carregados {#configure-the-product-attributes-to-load}

O analisador de resposta pode ser configurado para definir as propriedades e os atributos a serem carregados para produtos (variante):

1. Configure o pacote OSGi:

   **Analisador de resposta padrão de híbris de comércio do CQ do dia**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   Aqui você pode definir várias opções e atributos necessários para carregar e mapear.

   >[!NOTE]
   >
   >Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; see [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos. Consulte também o console para obter uma lista completa de parâmetros configuráveis e seus padrões.

## Importação dos dados do produto {#importing-the-product-data}

Há várias maneiras de importar os dados do produto. Os dados do produto podem ser importados ao configurar inicialmente o ambiente ou após alterações serem feitas nos dados de híbridos:

* [Importação completa](#full-import)
* [Importação incremental](#incremental-import)
* [Atualização expressa](#express-update)

As informações reais do produto importadas de híbridos são mantidas no repositório em:

`/etc/commerce/products`

As seguintes propriedades indicam o link com híbridos:

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>A implementação de híbridos (ou seja, `geometrixx-outdoors/en_US`) armazena somente IDs de produtos e outras informações básicas em `/etc/commerce`.
>
>O servidor hybris é referenciado sempre que as informações sobre um produto são solicitadas.

### Importação completa {#full-import}

1. Se necessário, exclua todos os dados do produto existentes usando o CRXDE Lite.

   1. Navegue até a subárvore que contém os dados do produto:

      `/etc/commerce/products`

      Por exemplo:

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. Exclua o nó que retém os dados do produto; por exemplo, `outdoors`.
   1. **Salvar tudo** para persistir a alteração.

1. Abra o importador de híbridos em AEM:

   `/etc/importers/hybris.html`

   Por exemplo:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Configurar os parâmetros necessários; por exemplo:

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. Clique em **Importar Catálogo** para iniciar a importação.

   Ao concluir, é possível verificar os dados importados em:

   ```
       /etc/commerce/products/outdoors
   ```

   Você pode abrir isso no CRXDE Lite; por exemplo:

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### Importação incremental {#incremental-import}

1. Verificar, na subárvore adequada, as informações constantes AEM para o(s) produto(s) em causa:

   `/etc/commerce/products`

   Você pode abrir isso no CRXDE Lite; por exemplo:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. Em híbridos, atualizar a informação contida no(s) produto(s) revelador(es).

1. Abra o importador de híbridos em AEM:

   `/etc/importers/hybris.html`

   Por exemplo:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Selecionar a caixa de clique **Importação incremental**.
1. Clique em **Importar Catálogo** para iniciar a importação.

   Ao concluir, você pode verificar os dados atualizados em AEM em:

   ```
       /etc/commerce/products
   ```


### Atualização expressa {#express-update}

O processo de importação pode demorar muito tempo, portanto, como uma extensão da Sincronização de produto, você pode selecionar áreas específicas do catálogo para uma atualização expressa que é acionada manualmente. Isso usa o feed de exportação junto com a configuração de atributos padrão.

1. Verificar, na subárvore adequada, as informações constantes AEM para o(s) produto(s) em causa:

   `/etc/commerce/products`

   Você pode abrir isso no CRXDE Lite; por exemplo:

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. Em híbridos, atualizar a informação contida no(s) produto(s) revelador(es).

1. Em hybris, adicione o(s) produto(s) à fila expressa; por exemplo:

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. Abra o importador de híbridos em AEM:

   `/etc/importers/hybris.html`

   Por exemplo:

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. Selecionar a caixa de clique **Atualização expressa**.
1. Clique em **Importar Catálogo** para iniciar a importação.

   Ao concluir, você pode verificar os dados atualizados em AEM em:

   ```
       /etc/commerce/products
   ```

## Configurar o Importador de Catálogo {#configure-the-catalog-importer}

O catálogo de híbridos pode ser importado para o AEM, usando o importador de lote para catálogos de híbridos, categorias e produtos.

Os parâmetros usados pelo importador podem ser configurados para:

**Importador de Catálogo de Híbris do Comércio do Day CQ**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; see [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos. Consulte também o console para obter uma lista completa de parâmetros configuráveis e seus padrões.

## Importação de catálogo {#catalog-import}

O pacote de híbridos vem com um importador de catálogo para configurar a estrutura da página inicial.

Isso está disponível em:

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

Devem ser fornecidas as seguintes informações:

* **Loja base**
O identificador do armazenamento base configurado em híbridos.

* **Catálogo**
O identificador do catálogo a ser importado.

* **Caminho raiz**
O caminho para onde o catálogo deve ser importado.

## Removendo um produto do catálogo {#removing-a-product-from-the-catalog}

Para remover um ou mais produtos do catálogo:

1. [Configurar o para serviço OSGi](/help/sites-deploying/configuring-osgi.md) **Importador de Catálogo de Híbris do Comércio do Day CQ**; consulte também [Configurar o Importador de Catálogo](#configure-the-catalog-importer).

   Ative as seguintes propriedades:

   * **Habilitar remoção de produto**
   * **Habilitar remoção de ativos de produtos**

   >[!NOTE]
   >
   >Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; see [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos. Consulte também o console para obter uma lista completa de parâmetros configuráveis e seus padrões.

1. Inicialize o importador executando duas atualizações adicionais (consulte [Importação de catálogo](#catalog-import)):

   * A primeira execução resulta em um conjunto de produtos alterados - indicado na lista de log.
   * Pela segunda vez, nenhum produto deve ser atualizado.

   >[!NOTE]
   >
   >A primeira importação é inicializar as informações do produto. A segunda importação verifica se tudo funcionou e o conjunto de produtos está pronto.

1. Verifique a página de categoria que contém o produto que deseja remover. Os detalhes do produto devem ser visíveis.

   Por exemplo, a categoria a seguir mostra detalhes do produto Cajamara:

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. Remova o produto no console hybris. Use a opção **Alterar status de aprovação** para definir o status como `unapproved`. O produto será removido do feed ao vivo.

   Por exemplo:

   * Abra a página [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * Selecionar o catálogo `Outdoors Staged`
   * Pesquisar `Cajamara`
   * Selecione este produto e altere o status de aprovação para `unapproved`

1. Execute outra atualização incremental (consulte [Importação de catálogo](#catalog-import)). O log listará o produto excluído.
1. [Implantação](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) O catálogo adequado. A página do produto e do produto será removida do AEM.

   Por exemplo:

   * Abrir:

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * Implemente o `Hybris Base` catálogo
   * Abrir:

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * O `Cajamara` o produto terá sido removido do `Bike` categoria

1. Para reinstalar o produto:

   1. Em híbridos, defina o status de aprovação novamente como **aprovado**
   1. No AEM:

      1. executar uma atualização incremental
      1. implementar o catálogo apropriado novamente
      1. atualizar a página de categoria apropriada

## Adicionar característica do histórico de pedidos ao contexto do cliente {#add-order-history-trait-to-the-client-context}

Para adicionar o histórico de pedidos à [contexto do cliente](/help/sites-developing/client-context.md):

1. Abra o [página de design de contexto do cliente](/help/sites-administering/client-context.md), por:

   * Abra uma página para edição e, em seguida, abra o contexto do cliente usando **Ctrl-Alt-c** (janelas) ou **control-option-c** (Mac). Use o ícone de lápis no canto superior esquerdo do contexto do cliente para **Abra a página de design do ClientContext**.
   * Navegue diretamente para [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [Adicione o **Histórico de pedidos** componente](/help/sites-administering/client-context.md#adding-a-property-component) para **Carro de compras** componente t do contexto do cliente.
1. Você pode confirmar que o contexto do cliente está mostrando detalhes do histórico do pedido. Por exemplo:

   1. Abra o [contexto do cliente](/help/sites-administering/client-context.md).
   1. Adicione um item ao carrinho.
   1. Conclua o check-out.
   1. Verifique o contexto do cliente.
   1. Adicione outro item ao carrinho.
   1. Navegue até a página de finalização:

      * O contexto do cliente mostra um resumo do histórico do pedido.
      * A mensagem &quot;Você é um cliente recorrente&quot; é exibida.

   >[!NOTE]
   >
   >A mensagem é realizada por:
   >
   >* Navegar para [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  A campanha consiste em uma experiência.
   >
   >* Clique no segmento ([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
   >
   >* O segmento é criado usando o **Propriedade do Histórico do Pedido** característica.

