---
title: Desenvolvimento com o SAP Commerce Cloud
seo-title: Developing with SAP Commerce Cloud
description: A estrutura de integração do SAP Commerce Cloud inclui uma camada de integração com uma API
seo-description: The SAP Commerce Cloud integration framework includes an integration layer with an API
uuid: a780dd17-027a-4a61-af8f-3e2f600524c7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: b3de1a4a-f334-44bd-addc-463433204c99
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Desenvolvimento com o SAP Commerce Cloud {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>A estrutura de comércio eletrônico pode ser usada com qualquer solução de comércio eletrônico. Certas especificações e exemplos aqui abordados se referem à [híbris](https://www.hybris.com/) solução.

A estrutura de integração inclui uma camada de integração com uma API. Isso permite:

* conecte um sistema de eCommerce e extraia os dados do produto no AEM

* criar componentes de AEM para recursos de comércio, independentemente do mecanismo de comércio eletrônico específico

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[Documentação da API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) também está disponível.

Vários componentes de AEM prontos para uso são fornecidos para usar a camada de integração. Atualmente, são:

* um componente de exibição do produto
* um carrinho de compras
* check-out

Para pesquisar, é fornecido um gancho de integração que permite usar a pesquisa de AEM, a pesquisa do sistema de eCommerce, uma pesquisa de terceiros ou uma combinação desse sistema.

## Seleção do mecanismo de comércio eletrônico {#ecommerce-engine-selection}

A estrutura de eCommerce pode ser usada com qualquer solução de eCommerce, o mecanismo usado precisa ser identificado por AEM:

* Os mecanismos de comércio eletrônico são serviços OSGi compatíveis com o `CommerceService` interface

   * Os motores podem ser distinguidos por um `commerceProvider` propriedade de serviço

* AEM compatível `Resource.adaptTo()` para `CommerceService` e `Product`

   * O `adaptTo` a implementação procura uma `cq:commerceProvider` na hierarquia do recurso:

      * Se for encontrado, o valor será usado para filtrar a pesquisa do serviço de comércio.

      * Se não for encontrado, o serviço de comércio de maior classificação será usado.
   * A `cq:Commerce` A mixin é usada para que a variável `cq:commerceProvider` podem ser adicionados a recursos com muitos tipos.


* O `cq:commerceProvider` é também usada para fazer referência à definição de fábrica de comércio apropriada.

   * Por exemplo, um `cq:commerceProvider` propriedade com o valor `hybris` estará correlacionado à configuração do OSGi para **Day CQ Commerce Fatory for Hybris** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory) - onde o parâmetro `commerceProvider` também tem o valor `hybris`.

   * Aqui estão outras propriedades, como **Versão do catálogo** pode ser configurado (quando apropriado e disponível).

Consulte os seguintes exemplos abaixo:

| `cq:commerceProvider = geometrixx` | numa instalação-padrão AEM é necessária uma implementação específica; por exemplo, o exemplo geometrixx, que inclui extensões mínimas para a API genérica |
|--- |--- |
| `cq:commerceProvider = hybris` | implementação de híbridos |

### Exemplo {#example}

```shell
/content/store
+ cq:commerceProvider = hybris
  + mens
    + polo-shirt-1
    + polo-shirt-2
    + employee
+ cq:commerceProvider = jcr
  + adobe-logo-shirt
    + cq:commerceType = product
    + price = 12.50
  + adobe-logo-shirt_S
    + cq:commerceType = variant
    + size = S
  + adobe-logo-shirt_XL
    + cq:commerceType = variant
    + size = XL
    + price = 14.50
```

>[!NOTE]
>
>Com o CRXDE Lite, você pode ver como isso é feito no componente de produto para a implementação de híbridos:
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### Desenvolvimento de híbridos 4 {#developing-for-hybris}

A extensão hybris da estrutura de integração de comércio eletrônico foi atualizada para oferecer suporte ao Hybris 5, mantendo a compatibilidade com o Hybris 4.

As configurações padrão no código são ajustadas para Hybris 5.

Para desenvolver o Hybris 4 é necessário:

* Ao chamar maven, adicione o seguinte argumento de linha de comando ao comando

   `-P hybris4`

   Ele baixa a distribuição pré-configurada do Hybris 4 e a incorpora ao pacote `cq-commerce-hybris-server`.

* No gerenciador de configuração do OSGi:

   * Desative o suporte do Hybris 5 para o serviço Analisador de resposta padrão.

   * Certifique-se de que o serviço Hybris Basic Authentication Handler tem uma classificação de serviço inferior à do Hybris OAuth Handler.

### Manuseio de sessão {#session-handling}

hybris usa uma sessão do usuário para armazenar informações como o carrinho de compras do cliente. A ID da sessão é retornada de híbridos em um `JSESSIONID` cookie que precisa ser enviado em solicitações subsequentes para híbridos. Para evitar armazenar a id da sessão no repositório, ela é codificada em outro cookie que é armazenado no navegador do comprador. As seguintes etapas são executadas:

* Na primeira solicitação, nenhum cookie é definido na solicitação do comprador; assim, uma solicitação é enviada para a instância hybris para criar uma sessão.

* Os cookies da sessão são extraídos da resposta, codificados em um novo cookie (por exemplo, `hybris-session-rest`) e defina na resposta ao comprador. A codificação em um novo cookie é necessária, pois o cookie original é válido apenas para um determinado caminho e, caso contrário, não seria enviado de volta do navegador em solicitações subsequentes. As informações de caminho também devem ser adicionadas ao valor do cookie.

* Em solicitações subsequentes, os cookies são decodificados do `hybris-session-<*xxx*>` cookies e definido no cliente HTTP que é usado para solicitar dados de híbridos.

>[!NOTE]
>
>Uma nova sessão anônima é criada quando a sessão original não é mais válida.

#### CommerceSession {#commercesession}

* Esta sessão é &quot;proprietária&quot; da **carrinho de compras**

   * executa adicionar/remover/etc

   * realiza os vários cálculos no carrinho;

      `commerceSession.getProductPrice(Product product)`

* Possui o *local de armazenamento* para **pedido** dados

   `CommerceSession.getUserContext()`

* Também é proprietária da **pagamento** conexão de processamento

* Também é proprietária da **cumprimento** conexão

### Sincronização e publicação do produto {#product-synchronization-and-publishing}

Os dados do produto que são mantidos em híbridos precisam estar disponíveis em AEM. Foi implementado o seguinte mecanismo:

* Uma carga inicial de IDs é fornecida por híbridos como um feed. Pode haver atualizações neste feed.
* os hybris fornecerão informações de atualização por meio de um feed (que AEM pesquisas).
* Quando o AEM estiver usando dados de produto, ele enviará solicitações para híbridos para os dados atuais (solicitação de obtenção condicional usando a data da última modificação).
* Em híbridos, é possível especificar o conteúdo do feed de uma maneira declarativa.
* Mapear a estrutura de feed para o modelo de conteúdo AEM acontece no adaptador de feed no lado AEM.

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* O importador (b) é usado para a configuração inicial da estrutura da árvore de páginas em AEM para catálogos.
* As alterações no catálogo em híbridos são indicadas para AEM por meio de um feed, propagando-se então para AEM (b)

   * Produto adicionado/excluído/alterado em relação à versão do catálogo.

   * Produto aprovado.

* A extensão hybris fornece um importador de pesquisa (esquema &quot;hybris&quot;), que pode ser configurado para importar alterações para AEM em um intervalo especificado (por exemplo, a cada 24 horas, onde o intervalo é especificado em segundos):

   ```JavaScript
       http://localhost:4502/content/geometrixx-outdoors/en_US/jcr:content.json
        {
        * "jcr:mixinTypes": ["cq:PollConfig"],
        * "enabled": true,
        * "source": "hybris:outdoors",
        * "jcr:primaryType": "cq:PageContent",
        * "interval": 86400
        }
   ```

* A configuração do catálogo no AEM reconhece **Preparado** e **Online** versões de catálogo.

* A sincronização de produtos entre versões de catálogo exigirá uma (des)ativação da página de AEM correspondente (a, c)

   * Adicionar um produto a um **Online** a versão do catálogo requer a ativação da página do produto.

   * A remoção de um produto requer desativação.

* Ativar uma página no AEM c) requer uma verificação b) e só é possível se

   * O produto está em um **Online** versão de catálogo para páginas de produto.

   * Os produtos referenciados estão disponíveis em um **Online** versão de catálogo para outras páginas (por exemplo, páginas de campanha).

* As páginas de produtos ativadas precisam acessar os dados do produto **Online** versão d).

* A instância de publicação de AEM requer acesso a híbridos para a recuperação de dados personalizados e do produto (d).

### Arquitetura {#architecture}

#### Arquitetura de produto e variantes {#architecture-of-product-and-variants}

Um único produto pode apresentar variações múltiplas; por exemplo, pode variar de acordo com a cor e/ou o tamanho. Um produto deve definir as propriedades que determinam a variação; nós os designamos *eixos de variantes*.

No entanto, nem todas as propriedades são eixos de variante. As variações também podem afetar outras propriedades; por exemplo, o preço pode depender do tamanho. Essas propriedades não podem ser selecionadas pelo comprador e, portanto, não são consideradas eixos de variante.

Cada produto e/ou variante é representado por um recurso e, portanto, mapeia 1:1 para um nó de repositório. É um corolário que um produto e/ou variante específico pode ser identificado exclusivamente pelo seu caminho.

O recurso produto/variante nem sempre contém os dados reais do produto. Pode ser uma representação de dados realmente mantidos em outro sistema (como híbridos). Por exemplo, descrições de produtos, preços etc. não são armazenados em AEM, mas recuperados em tempo real do mecanismo de comércio eletrônico.

Qualquer recurso de produto pode ser representado por um `Product API`. A maioria das chamadas na API de produto é específica para a variação (embora as variações possam herdar valores compartilhados de um ancestral), mas também há chamadas que listam o conjunto de variações ( `getVariantAxes()`, `getVariants()`, etc.).

>[!NOTE]
>
>Com efeito, os eixos de variantes são determinados pelo `Product.getVariantAxes()` retorna:
>* hybris o define para a implementação hybris
>
>Embora os produtos (em geral) possam ter vários eixos de variantes, o componente de produto pronto para uso trata apenas de dois:
>
>1. `size`
>
>1. mais um

>
>Essa variante adicional é selecionada por meio da variável `variationAxis` propriedade da referência do produto (normalmente `color` para Geometrixx Outdoors).

#### Referências do produto e dados do produto {#product-references-and-product-data}

Em geral:

* os dados do produto estão localizados em `/etc`

* e as referências de produto nos termos do `/content`.

Deve haver um mapa 1:1 entre variações de produto e nós de dados de produto.

As referências de produto também devem ter um nó para cada variação apresentada, mas não há necessidade de apresentar todas as variações. Por exemplo, se um produto tiver variações de S, M, L, os dados do produto podem ser:

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

Enquanto um catálogo &quot;Grande e alto&quot; pode ter apenas:

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
```

Finalmente, não há requisito para usar dados do produto. Você pode colocar todos os dados do produto sob as referências no catálogo; mas não é possível ter vários catálogos sem duplicar todos os dados do produto.

**API**

#### com.adobe.cq.commerce.api.Interface do produto {#com-adobe-cq-commerce-api-product-interface}

```java
public interface Product extends Adaptable {

    public String getPath();            // path to specific variation
    public String getPagePath();        // path to presentation page for all variations
    public String getSKU();             // unique ID of specific variation

    public String getTitle();           // shortcut to getProperty(TITLE)
    public String getDescription();     // shortcut to getProperty(DESCRIPTION)
    public String getImageUrl();        // shortcut to getProperty(IMAGE_URL)
    public String getThumbnailUrl();    // shortcut to getProperty(THUMBNAIL_URL)

    public <T> T getProperty(String name, Class<T> type);

    public Iterator<String> getVariantAxes();
    public boolean axisIsVariant(String axis);
    public Iterator<Product> getVariants(VariantFilter filter) throws CommerceException;
}
```

#### com.adobe.cq.commerce.api.VariantFilter  {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * e.g. when using {@link Product#getVariants(VariantFilter filter)}.
 */
public interface VariantFilter {
    public boolean includes(Product product);
}

/**
 * A {@link VariantFilter} for filtering variants by the given
 * axis and value. The following example returns a list of
 * variant products that have a value of <i>blue</i> on the
 * <i>color</i> axis.
 *
 * <p>
 * <code>product.getVariants(new AxisFilter("color", "blue"));</code>
 */
public class AxisFilter implements VariantFilter {

    private String axis;
    private String value;

    public AxisFilter(String axis, String value) {
        this.axis = axis;
        this.value = value;
    }

    /**
     * {@inheritDoc}
     */
    public boolean includes(Product product) {
        ValueMap values = product.adaptTo(ValueMap.class);

        if(values != null) {
            String v = values.get(axis, String.class);

            return v != null && v == value;
        }

        return false;
    }
}
```

* **Mecanismo geral de armazenamento**

   * Os nós do produto são `nt:unstructured`.

   * Um nó de produto pode ser:

      * Uma referência, com os dados do produto armazenados em outro lugar:

         * As referências de produto contêm um `productData` , que aponta para os dados do produto (normalmente em `/etc/commerce/products`).

         * Os dados do produto são hierárquicos; os atributos do produto são herdados dos ancestrais de um nó de dados do produto.

         * As referências de produto também podem conter propriedades locais, que substituem as especificadas nos dados do produto.
      * Um produto em si:

         * Sem um `productData` propriedade.

         * Um nó de produto que armazena todas as propriedades localmente (e não contém uma propriedade productData ) herda atributos de produto diretamente de seus próprios ancestrais.


* **Estrutura AEM-genérica do produto**

   * Cada variante deve ter seu próprio nó de folha.

   * A interface do produto representa produtos e variantes, mas o nó do repositório relacionado é específico sobre o qual ele é.

   * O nó produto descreve os atributos do produto e os eixos da variante.

#### Exemplo {#example-1}

```shell
+ banyan_shirt
    - cq:commerceType = product
    - cq:productAttributes = [jcr:title, jcr:description, size, price, color]
    - cq:productVariantAxes = [color, size]
    - jcr:title = Banyan Shirt
    - jcr:description = Flowery, all-cotton shirt.
    - price = 14.00
    + banyan_shirt_s
        - cq:commerceType = variant
        - size = S
        + banyan_shirt_s_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_s_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_m
        - cq:commerceType = variant
        - size = M
        + banyan_shirt_m_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_m_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_l
        - cq:commerceType = variant
        - size = L
        + banyan_shirt_l_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_l_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_xl
        - cq:commerceType = variant
        - size = XL
        - price = 18.00
```

#### Arquitetura do carrinho de compras {#architecture-of-the-shopping-cart}

**Componentes**

* O carrinho de compras é de propriedade do `CommerceSession:`

   * O `CommerceSession` O executa adicionar/remover/etc.
   * O `CommerceSession` O também executa os vários cálculos no carrinho. &quot;

* Embora não esteja diretamente relacionado ao carrinho, a variável `CommerceSession` também deve fornecer informações sobre preços de catálogo (já que possui preços)

   * Os preços podem ter vários modificadores:

      * Descontos de quantidade.
      * Moedas diferentes.
      * IVA e sem IVA.
   * Os modificadores são completamente abertos com a seguinte interface:

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**Armazenamento**

* Armazenamento

   * No caso de híbridos, o servidor de híbridos é proprietário do carrinho.
   * Nos carrinhos de AEM genéricos de são armazenados no [ClientContext](/help/sites-administering/client-context.md).

**Personalização**

* A personalização deve sempre ser conduzida pelo [ClientContext](/help/sites-administering/client-context.md).
* Um ClientContext `/version/` do carrinho é criado em todos os casos:

   * Os produtos devem ser adicionados usando o `CommerceSession.addCartEntry()` método .

* O exemplo a seguir ilustra as informações do carrinho no carrinho do ClientContext:

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### Arquitetura do Check-out {#architecture-of-checkout}

**Dados do carrinho e pedido**

O `CommerceSession` é proprietária dos três elementos:

1. Conteúdo do carrinho
1. Preços
1. Os detalhes do pedido

1. **Conteúdo do carrinho**

   O esquema de conteúdo do carrinho é corrigido pela API:

   ```java
   public void addCartEntry(Product product, int quantity);
   public void modifyCartEntry(int entryNumber, int quantity);
   public void deleteCartEntry(int entryNumber);
   ```

1. **Preços**

   O schema de preços também é corrigido pela API:

   ```java
   public String getCartPreTaxPrice();
   public String getCartTax();
   public String getCartTotalPrice();
   public String getOrderShipping();
   public String getOrderTotalTax();
   public String getOrderTotalPrice();
   ```

1. **Detalhes do pedido**

   No entanto, os detalhes do pedido são *not* corrigido pela API:

   ```java
   public void updateOrderDetails(Map<String, String> orderDetails);
   public Map<String, String> getOrderDetails();
   public void submitOrder();
   ```

**Cálculos de Entrega**

* Os formulários de pedido geralmente precisam apresentar várias opções de envio (e preços).
* Os preços podem ser baseados em itens e detalhes do pedido, como peso e/ou endereço de entrega.
* O `CommerceSession` O tem acesso a todas as dependências, portanto, pode ser tratado de maneira semelhante como o preço do produto:

   * O `CommerceSession` é proprietária de preços de envio.
   * Pode recuperar/atualizar detalhes do delivery usando `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>Você poderia implementar um seletor de envio; por exemplo:
>
>`yourProject/commerce/components/shippingpicker`:
>
>* Essencialmente, isto pode ser uma cópia de `foundation/components/form/radio`, mas com retornos de chamada para a `CommerceSession` a favor:
>
>* Verificando se o método está disponível
>* Adicionar informações sobre preços
>* Para permitir que os compradores atualizem a página de pedido em AEM (incluindo o superconjunto de métodos de envio e o texto que os descreve), mantendo o controle para expor a `CommerceSession` informações.


**Processamento de pagamento**

* O `CommerceSession` é igualmente proprietária da ligação de processamento de pagamentos.

* Os implementadores devem adicionar chamadas específicas (ao serviço de processamento de pagamentos por eles escolhido) ao `CommerceSession` implementação.

**Cumprimento do pedido**

* O `CommerceSession` é também proprietária da ligação de execução.
* Os implementadores terão de adicionar chamadas específicas (ao serviço de processamento de pagamentos por eles escolhido) ao `CommerceSession` implementação.

### Definição de Pesquisa {#search-definition}

Seguindo o modelo padrão de API de serviço, o projeto de eCommerce fornece um conjunto de APIs relacionadas à pesquisa que podem ser implementadas por mecanismos de comércio individuais.

>[!NOTE]
>
>Atualmente, somente o mecanismo de híbridos implementa a API de pesquisa pronta para uso.
>
>No entanto, a API de pesquisa é genérica e pode ser implementada por cada CommerceService individualmente.

O projeto de comércio eletrônico contém um componente de pesquisa padrão, localizado em:

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

Isso usa a API de pesquisa para consultar o mecanismo de comércio selecionado (consulte [Seleção do mecanismo de comércio eletrônico](#ecommerce-engine-selection)):

#### API de pesquisa {#search-api}

Há várias classes genéricas/auxiliares fornecidas pelo projeto principal:

1. `CommerceQuery`

   É usado para descrever uma consulta de pesquisa (contém informações sobre o texto da consulta, página atual, tamanho da página, classificação e aspectos selecionados). Todos os serviços de eCommerce que implementam a API de pesquisa receberão instâncias dessa classe para realizar sua pesquisa. A `CommerceQuery` pode ser instanciado de um objeto de solicitação ( `HttpServletRequest`).

1. `FacetParamHelper`

   É uma classe de utilitário que fornece um método estático - `toParams` - que é utilizado para gerar `GET` strings de parâmetro de uma lista de facetas e um valor alternado. Isso é útil na interface do usuário, onde é necessário exibir um hiperlink para cada valor de cada faceta, de modo que, quando o usuário clica no hiperlink, o respectivo valor é alternado (ou seja, se foi selecionado, ele é removido da consulta, caso contrário, é adicionado). Isso cuida de toda a lógica de lidar com várias facetas/valores únicos, substituir valores etc.

O ponto de entrada da API de pesquisa é o `CommerceService#search` método que retorna um `CommerceResult` objeto. Consulte a [Documentação da API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) para obter mais informações sobre este tópico.

### Integração de usuários {#user-integration}

A integração é fornecida entre o AEM e vários sistemas de eCommerce. Isso requer uma estratégia para sincronizar compradores entre os vários sistemas, de modo que o código específico do AEM tenha que saber apenas sobre AEM e vice-versa:

* Autenticação

   Presume-se que AEM é o *only* front-end da Web e, portanto, desempenho *all* autenticação.

* Contas em Hybris

   AEM cria uma conta correspondente (secundária) em híbridos para cada comprador. O nome de usuário desta conta é igual ao nome de usuário AEM. Uma senha aleatória criptograficamente é gerada automaticamente e armazenada (criptografada) no AEM.

#### Usuários pré-existentes {#pre-existing-users}

Um front-end AEM pode ser posicionado na frente de uma implementação de hybris existente. Também é possível adicionar um mecanismo hybris a uma instalação AEM existente. Para fazer isso, os sistemas devem ser capazes de lidar com os usuários existentes em qualquer um dos sistemas:

* AEM -> híbridos

   * Ao fazer logon em híbridos, se o usuário do AEM ainda não existir:

      * criar um novo usuário hybris com uma senha aleatória criptograficamente
      * armazene o nome de usuário do hybris no diretório de usuário do AEM
   * Consulte: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`


* hybris -> AEM

   * Ao fazer logon no AEM, se o sistema reconhecer o usuário:

      * tentativa de fazer logon em híbridos com nome de usuário/pwd fornecido
      * se bem-sucedido, crie o novo usuário em AEM com a mesma senha (sal específico de AEM resultará em hash específico de AEM)
   * O algoritmo acima é implementado em um Sling `AuthenticationInfoPostProcessor`

      * Consulte: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`


### Personalização do processo de importação {#customizing-the-import-process}

Para basear-se na funcionalidade existente, o manipulador de importação personalizado:

* tem de implementar a `ImportHandler` interface

* pode estender o `DefaultImportHandler`.

```java
/**
 * Services implementing the <code>ImportHandler</code> interface are
 * called by the {@link HybrisImporter} to create actual commerce entities
 * such as products.
 */
public interface ImportHandler {

  /**
  * Not used.
  */
  public void createTaxonomie(ImporterContext ctx);

  /**
  * Creates a catalog with the given name.
  * @param ctx   The importer context
  * @param name  The catalog's name
  * @return Path of created catalog
  */
  public String createCatalog(ImporterContext ctx, String name) throws Exception;

  /**
  * Creates a product from the given values.
  * @param ctx                The importer context
  * @param values             The product's properties
  * @param parentCategoryPath The containing category's path
  * @return Path of created product
  */
  public String createProduct(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;

  /**
  * Creates a variant product from the given values.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The base product's path
  * @return Path of created product
  */
  public String createVariantProduct(ImporterContext ctx, ValueMap values, String baseProductPath) throws Exception;

  /**
  * Creates an asset for a product. This is usually a product
  * image.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The product's path
  * @return Path of created asset
  */
  public String createAsset(ImporterContext ctx, ValueMap values, String productPath) throws Exception;

  /**
  * Creates a category from the given values.
  * @param ctx           The importer context
  * @param values        The category's properties
  * @param parentPath    Path of parent category or base path of import in case of root category
  * @return Path of created category
  */
  public String createCategory(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;
}
```

Para que seu manipulador personalizado seja reconhecido pelo importador, ele deve especificar a variável `service.ranking`propriedade com valor superior a 0; por exemplo.

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
