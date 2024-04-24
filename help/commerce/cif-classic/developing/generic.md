---
title: Desenvolvimento (genérico)
description: A estrutura de integração inclui uma camada de integração com uma API, permitindo a criação de componentes de AEM para recursos de comércio eletrônico.
contentOwner: Guillaume Carlino
exl-id: 1138a548-d112-4446-b0e1-b7a9ea7c7604
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 0%

---

# Desenvolvimento (genérico){#developing-generic}

>[!NOTE]
>
>[Documentação da API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) O também está disponível.

A estrutura de integração inclui uma camada de integração com uma API. Isso permite criar componentes de AEM para recursos de comércio eletrônico (independentemente do mecanismo de comércio eletrônico específico). Ele também permite usar o banco de dados CRX interno ou conectar um sistema de comércio eletrônico e transmitir dados do produto para o AEM.

Vários componentes AEM prontos para uso são fornecidos para usar a camada de integração. Atualmente, são eles:

* Um componente de exibição do produto
* Um carrinho de compras
* Promoções e vouchers
* Blueprints de catálogo e seção
* Check-out
* Pesquisar

Para pesquisa, é fornecido um gancho de integração que permite usar a pesquisa do Adobe Experience Manager (AEM), uma pesquisa de terceiros ou uma combinação dessas pesquisas.

## Seleção de mecanismo de comércio eletrônico {#ecommerce-engine-selection}

A estrutura de comércio eletrônico pode ser usada com qualquer solução de comércio eletrônico, o mecanismo usado deve ser identificado pelo AEM - mesmo quando o mecanismo genérico AEM é usado:

* Mecanismos de comércio eletrônico são serviços OSGi que oferecem suporte ao `CommerceService` interface

   * Os motores podem ser distinguidos por uma `commerceProvider` propriedade de serviço

* Suporte para AEM `Resource.adaptTo()` para `CommerceService` e `Product`

   * A variável `adaptTo` A implementação procura um `cq:commerceProvider` propriedade na hierarquia do recurso:

      * Se encontrado, o valor é usado para filtrar a pesquisa de serviço de comércio.
      * Se não for encontrado, será usado o serviço de comércio com a classificação mais alta.

   * A `cq:Commerce` mixin é usado para que o `cq:commerceProvider` podem ser adicionados a recursos fortemente tipados.

* A variável `cq:commerceProvider` A propriedade também é usada para fazer referência à definição apropriada da fábrica de comércio.

   * Por exemplo, uma variável `cq:commerceProvider` propriedade com o valor Geometrixx correlaciona-se à configuração OSGi para **Fábrica Day CQ Commerce para Geometrixx-Outdoors** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`) - em que o parâmetro `commerceProvider` também tem o valor `geometrixx`.
   * Aqui, outras propriedades podem ser configuradas (quando apropriado e disponível).

Em uma instalação padrão com AEM, é necessária uma implementação específica, por exemplo:

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | exemplo do geometrixx; isso inclui extensões mínimas para a API genérica |

### Exemplo {#example}

```shell
/etc/commerce/products/geometrixx-outdoors
+ cq:commerceProvider = geometrixx
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
>Com o CRXDE Lite você pode ver como isso é tratado no componente do produto para a implementação genérica do AEM:
>
>`/apps/geometrixx-outdoors/components/product`

### Tratamento de sessão {#session-handling}

Uma sessão para armazenar informações relacionadas ao carrinho de compras do cliente.

A variável **CommerceSession**:

* É proprietário do **carrinho de compras**

   * executa adicionar/remover/etc
   * realiza os vários cálculos no carrinho;

     `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* Possui a persistência do **pedido** dados:

  `CommerceSession.getUserContext()`

* Pode recuperar/atualizar detalhes do delivery usando `updateOrder(Map<String, Object> delta)`
* É proprietário do **pagamento** processando conexão
* É proprietário do **preenchimento** conexão

### Arquitetura {#architecture}

#### Arquitetura de produtos e variantes {#architecture-of-product-and-variants}

Um único produto pode ter várias variações; por exemplo, pode variar por cor e/ou tamanho. Um produto deve definir quais propriedades impulsionam a variação; os termos de Adobe *eixos variantes*.

No entanto, nem todas as propriedades são eixos de variantes. As variações também podem afetar outras propriedades; por exemplo, o preço pode depender do tamanho. Essas propriedades não podem ser selecionadas pelo comprador e, portanto, não são consideradas eixos de variante.

Cada produto e/ou variante é representado por um recurso e, portanto, mapeia 1:1 para um nó de repositório. É um corolário que um produto e/ou variante específica possa ser identificado exclusivamente por seu caminho.

Qualquer recurso do produto pode ser representado por um `Product API`. A maioria das chamadas na API do produto é específica da variação (embora as variações possam herdar valores compartilhados de um ancestral), mas também há chamadas que listam o conjunto de variações ( `getVariantAxes()`, `getVariants()`e assim por diante).

>[!NOTE]
>
>Com efeito, um eixo variante é determinado por qualquer `Product.getVariantAxes()` devoluções:
>
>* para a implementação genérica, o AEM o lê de uma propriedade nos dados do produto ( `cq:productVariantAxes`)
>
>Embora os produtos (em geral) possam ter muitos eixos de variantes, o componente de produto pronto para uso lida apenas com dois:
>
>1. `size`
>1. mais um
>
>   Essa variante adicional é selecionada por meio da variável `variationAxis` propriedade da referência do produto (geralmente `color` para Geometrixx Outdoors).

#### Referências do produto e dados PIM {#product-references-and-pim-data}

Em geral:

* Os dados do PIM estão localizados em `/etc`

* Referências do produto em `/content`.

Deve haver um mapa 1:1 entre as variações de produtos e os nós de dados do produto.

As referências de produto também devem ter um nó para cada variação apresentada, mas não há necessidade de apresentar todas as variações. Por exemplo, se um produto tiver variações S, M, L, os dados do produto podem ser:

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

Embora um catálogo &quot;Grande e Alto&quot; possa ter apenas:

```shell
content
  big-and-tall
    shirt
      shirt-l
```

Por fim, não há necessidade de usar dados do produto. Você pode colocar todos os dados do produto sob as referências no catálogo, mas não pode realmente ter vários catálogos sem duplicar todos os dados do produto.

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
 * for example, when using {@link Product#getVariants(VariantFilter filter)}.
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

   * Os nós do produto não estão:não estruturados.
   * Um nó de produto pode ser:

      * Uma referência, com os dados do produto armazenados em outro lugar:

         * As referências de produto contêm um `productData` propriedade, que aponta para os dados do produto (normalmente sob `/etc/commerce/products`).
         * Os dados do produto são hierárquicos; os atributos do produto são herdados dos ancestrais de um nó de dados do produto.
         * As referências de produto também podem conter propriedades locais, que substituem as especificadas nos dados do produto.

      * Um produto em si:

         * Sem um `productData` propriedade.
         * Um nó de produto que armazena todas as propriedades localmente (e não contém uma propriedade productData ) herda atributos de produto diretamente de seus próprios antecessores.

* **Estrutura de produto genérica do AEM**

   * Cada variante deve ter seu próprio nó folha.
   * A interface do produto representa produtos e variantes, mas o nó do repositório relacionado é específico sobre o qual ele é.
   * O nó product descreve os atributos do produto e os eixos da variante.

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

* O carrinho de compras é de propriedade da `CommerceSession:`

   * A variável `CommerceSession` executa adicionar, remover, etc.
   * A variável `CommerceSession` também realiza os vários cálculos no carrinho.
   * A variável `CommerceSession` também aplica vouchers e promoções que foram acionados no carrinho.

* Embora não esteja diretamente relacionado ao carrinho, a variável `CommerceSession` também deve fornecer informações sobre preços de catálogo (já que possui preços)

   * A precificação pode ter vários modificadores:

      * Descontos por quantidade.
      * Moedas diferentes.
      * IVA e isento de IVA.

   * Os modificadores são abertos com a seguinte interface:

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`

**Armazenamento**

* Armazenamento

   * No caso genérico do AEM, os carrinhos são armazenados no [ClientContext](/help/sites-administering/client-context.md)

**Personalização**

* Sempre impulsionar a personalização por meio do [ClientContext](/help/sites-administering/client-context.md).
* Um ClientContext `/version/` do carrinho é criado em todos os casos:

   * Os produtos devem ser adicionados usando o `CommerceSession.addCartEntry()` método.

* A seguir, há um exemplo de informações sobre o carrinho no carrinho de ClientContexts:

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### Arquitetura do Check-out {#architecture-of-checkout}

**Dados do carrinho e do pedido**

A variável `CommerceSession` O é proprietário dos três elementos:

1. **Conteúdo do carrinho**

   O schema de conteúdo do carrinho é corrigido pela API:

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **Preços**

   O esquema de preços também é corrigido pela API:

   ```java
       public String getCartPreTaxPrice();
       public String getCartTax();
       public String getCartTotalPrice();
       public String getOrderShipping();
       public String getOrderTotalTax();
       public String getOrderTotalPrice();
   ```

1. **Detalhes do pedido**

   No entanto, os detalhes do pedido são *não* corrigido pela API:

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**Cálculos de envio**

* Os formulários de pedido geralmente devem apresentar várias opções de envio (e preços).
* Os preços podem ser baseados em itens e detalhes do pedido, como peso e/ou endereço de entrega.
* A variável `CommerceSession` O tem acesso a todas as dependências, portanto, pode ser tratado de maneira semelhante ao preço do produto:

   * A variável `CommerceSession` possui preços de envio.
   * Uso `updateOrder(Map<String, Object> delta)` para recuperar/atualizar os detalhes do delivery.

### Definição de pesquisa {#search-definition}

Seguindo o modelo padrão de API de serviço, o projeto de comércio eletrônico fornece um conjunto de APIs relacionadas à pesquisa que podem ser implementadas por mecanismos de comércio individuais.

>[!NOTE]
>
>Atualmente, apenas o mecanismo hybris implementa a API de pesquisa pronta para uso.
>
>No entanto, a API de pesquisa é genérica e pode ser implementada por cada CommerceService individualmente.
>
>Portanto, embora a implementação genérica fornecida pronta para uso não implemente essa API, é possível estendê-la e adicionar a funcionalidade de pesquisa.

O projeto de comércio eletrônico contém um componente de pesquisa padrão em:

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

Use a API de pesquisa para consultar o mecanismo de comércio selecionado (consulte [Seleção de mecanismo de comércio eletrônico](#ecommerce-engine-selection)):

#### API de pesquisa {#search-api}

Há várias classes genéricas/auxiliares fornecidas pelo projeto principal:

1. `CommerceQuery`

   Usado para descrever uma consulta de pesquisa (contém informações sobre o texto da consulta, a página atual, o tamanho da página, a classificação e as facetas selecionadas). Todos os serviços de comércio eletrônico que implementam a API de pesquisa recebem instâncias dessa classe para realizar sua pesquisa. A `CommerceQuery` pode ser instanciado a partir de um objeto de solicitação ( `HttpServletRequest`).

1. `FacetParamHelper`

   É uma classe de utilitário que fornece um método estático - `toParams` - que é utilizado para gerar `GET` strings de parâmetro de uma lista de facetas e um valor alternado. Isso é útil no lado da interface do usuário, em que é necessário exibir um hiperlink para cada valor de cada faceta, de modo que, quando o usuário clicar no hiperlink, o respectivo valor seja alternado. Ou seja, se foi selecionada, ela é removida da query; caso contrário, é adicionada. Isso cuida de toda a lógica de lidar com facetas de vários/valores únicos, substituir valores e assim por diante.

O ponto de entrada para a API de pesquisa é o `CommerceService#search` método que retorna um `CommerceResult` objeto. Consulte a Documentação da API para obter mais informações sobre esse tópico.

### Desenvolvimento de promoções e vouchers {#developing-promotions-and-vouchers}

* Vouchers:

   * Um Cupom é um componente baseado em páginas criado/editado com o console Sites e armazenado em:

     `/content/campaigns`

   * Fornecimento de vouchers:

      * Um código de voucher (a ser digitado no carrinho pelo comprador).
      * Um rótulo de voucher (a ser exibido depois que o comprador o inserir no carrinho).
      * Um caminho de promoção (que define a ação que o voucher aplica).

   * Os vouchers não têm suas próprias datas/horas de ativação e desativação, mas usam os das campanhas principais.
   * Os mecanismos de comércio externo também podem fornecer vouchers; eles exigem no mínimo:

      * Um código de voucher
      * Um `isValid()` método

   * A variável **Voucher** componente ( `/libs/commerce/components/voucher`) fornece:

      * Um renderizador para administração de vouchers; mostra todos os vouchers que estão no carrinho.
      * As caixas de diálogo de edição (formulário) para administrar (adicionar/remover) os vouchers.
      * As ações necessárias para adicionar/remover vouchers do carrinho.

* Promoções:

   * Uma promoção é um componente baseado em páginas, criado/editado com o console Sites e armazenado em:

     `/content/campaigns`

   * Fornecimento de promoções:

      * Uma prioridade
      * Um caminho de manipulador de promoção

   * É possível conectar promoções a uma campanha para definir suas datas/horas de ativação/desativação.
   * É possível conectar promoções a uma experiência para definir seus segmentos.
   * As promoções não conectadas a uma experiência do não são acionadas por conta própria, mas ainda podem ser acionadas por um Voucher.
   * O componente de Promoção ( `/libs/commerce/components/promotion`) contém:

      * renderizadores e caixas de diálogo para administração de promoção
      * subcomponentes para renderização e edição de parâmetros de configuração específicos para os manipuladores de promoção

   * Dois manipuladores de promoção são fornecidos imediatamente:

      * `DiscountPromotionHandler`, que aplica um desconto absoluto ou percentual em todo o carrinho
      * `PerfectPartnerPromotionHandler`, que aplica um desconto absoluto ou percentual do produto se o produto do parceiro também estiver no carrinho

   * O CLIENTCONTEXT `SegmentMgr` resolve segmentos e o ClientContext `CartMgr` resolve promoções. Cada promoção que está sujeita a pelo menos um segmento resolvido é acionada.

      * As promoções acionadas são enviadas de volta ao servidor por meio de uma chamada AJAX para recalcular o carrinho.
      * As Promoções acionadas (e os Cupons adicionados) também são mostrados no painel ClientContext.

A adição/remoção de um voucher de um carrinho é realizada por meio do `CommerceSession` API:

```java
/**
 * Apply a voucher to this session's cart.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void addVoucher(String code) throws CommerceException;

/**
 * Remove a voucher that was previously added with {@link #addVoucher(String)}.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void removeVoucher(String code) throws CommerceException;

/**
 * Get a list of vouchers that were added to this cart via {@link #addVoucher(String)}.
 *
 * @throws CommerceException
 */
public List<Voucher> getVouchers() throws CommerceException;
```

Desta forma, a `CommerceSession` A é responsável por verificar se um voucher existe e se pode ser aplicado ou não. Isso pode ser para vouchers que só podem ser aplicados se uma determinada condição for atendida. Por exemplo, quando o preço total do carrinho é maior que US$ 100. Se um comprovante não puder ser aplicado por algum motivo, a variável `addVoucher` O método lança uma exceção. Além disso, a variável `CommerceSession` O é responsável por atualizar os preços do carrinho depois que um voucher é adicionado/removido.

A variável `Voucher` é uma classe semelhante a um bean que contém campos para:

* Código do voucher
* Uma descrição curta
* Fazendo referência à promoção relacionada que indica o tipo e o valor do desconto

A variável `AbstractJcrCommerceSession` fornecido pode aplicar vouchers. Os comprovantes devolvidos pela classe `getVouchers()` são instâncias de `cq:Page` contendo um nó jcr:content com as seguintes propriedades (entre outras):

* `sling:resourceType` (String) - precisa ser `commerce/components/voucher`

* `jcr:title` (Sequência de caracteres) - para a descrição do voucher
* `code` (String) - o código que o usuário deve inserir para aplicar este voucher
* `promotion` (String) - a promoção a ser aplicada; por exemplo, `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

Os manipuladores de promoção são serviços OSGi que modificam o carrinho de compras. O carrinho suporta vários ganchos definidos na variável `PromotionHandler` interface.

```java
/**
 * Apply promotion to a cart line item. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @param cartEntry The cart line item
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyCartEntryPromotion(CommerceSession commerceSession,
                                         Promotion promotion, CartEntry cartEntry)
    throws CommerceException;

/**
 * Apply promotion to an order. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyOrderPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

public PriceInfo applyShippingPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

/**
 * Allows a promotion handler to define a custom, author-oriented message for a promotion.
 * The {@link com.adobe.cq.commerce.common.promotion.PerfectPartnerPromotionHandler}, for instance,
 * uses this to list the qualifying pairs of products in the current cart.
 * @param commerceSession
 * @param promotion
 * @return A message to display
 * @throws CommerceException
 */
public String getMessage(SlingHttpServletRequest request, CommerceSession commerceSession, Promotion promotion) throws CommerceException;

/**
 * Informs the promotion handler that something under the promotions root has been edited, and the handler
 * should invalidate any caches it might be keeping.
 */
public void invalidateCaches();
```

Três manipuladores de promoção são fornecidos imediatamente:

* `DiscountPromotionHandler` aplica um desconto absoluto ou percentual em todo o carrinho
* `PerfectPartnerPromotionHandler` aplica um desconto absoluto ou percentual do produto se o parceiro de produto também estiver no carrinho
* `FreeShippingPromotionHandler` aplica frete grátis
