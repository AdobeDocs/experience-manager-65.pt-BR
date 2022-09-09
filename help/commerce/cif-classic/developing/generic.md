---
title: Desenvolvimento (genérico)
seo-title: Developing (generic)
description: A estrutura de integração inclui uma camada de integração com uma API, permitindo criar componentes AEM para recursos de eCommerce
seo-description: The integration framework includes an integration layer with an API, allowing you to build AEM components for eCommerce capabilities
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: 1138a548-d112-4446-b0e1-b7a9ea7c7604
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Desenvolvimento (genérico){#developing-generic}

>[!NOTE]
>
>[Documentação da API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) também está disponível.

A estrutura de integração inclui uma camada de integração com uma API. Isso permite criar componentes de AEM para recursos de comércio eletrônico (independentemente do mecanismo de comércio eletrônico específico). Ele também permite usar o banco de dados interno do CRX ou conectar um sistema de eCommerce e extrair dados do produto no AEM.

Vários componentes de AEM prontos para uso são fornecidos para usar a camada de integração. Atualmente, são:

* Um componente de exibição do produto
* Um carrinho de compras
* Promoções e comprovantes
* Projetos de catálogo e seção
* Check-out
* Pesquisar

Para pesquisar, é fornecido um gancho de integração que permite usar a pesquisa de AEM, uma pesquisa de terceiros ou uma combinação deles.

## Seleção do mecanismo de comércio eletrônico {#ecommerce-engine-selection}

A estrutura de eCommerce pode ser usada com qualquer solução de eCommerce, o mecanismo usado precisa ser identificado pelo AEM - mesmo quando o mecanismo genérico AEM é usado:

* Os mecanismos de comércio eletrônico são serviços OSGi compatíveis com o `CommerceService` interface

   * Os motores podem ser distinguidos por um `commerceProvider` propriedade de serviço

* AEM compatível `Resource.adaptTo()` para `CommerceService` e `Product`

   * O `adaptTo` a implementação procura uma `cq:commerceProvider` na hierarquia do recurso:

      * Se for encontrado, o valor será usado para filtrar a pesquisa do serviço de comércio.
      * Se não for encontrado, o serviço de comércio de maior classificação será usado.
   * A `cq:Commerce` A mixin é usada para que a variável `cq:commerceProvider` podem ser adicionados a recursos com muitos tipos.


* O `cq:commerceProvider` é também usada para fazer referência à definição de fábrica de comércio apropriada.

   * Por exemplo, um `cq:commerceProvider` com o valor geometrixx estará correlacionado à configuração OSGi para **Day CQ Commerce Fatory for Geometrixx Outdoors** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`) - onde o parâmetro `commerceProvider` também tem o valor `geometrixx`.
   * Aqui, outras propriedades podem ser configuradas (quando apropriado e disponível).

Em uma instalação padrão AEM é necessária uma implementação específica, por exemplo:

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | exemplo de geometrixx; isso inclui extensões mínimas para a API genérica |

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
>Com o CRXDE Lite, você pode ver como isso é tratado no componente do produto para a implementação genérica de AEM:
>
>`/apps/geometrixx-outdoors/components/product`

### Manuseio de sessão {#session-handling}

Uma sessão para armazenar informações relacionadas ao carrinho de compras do cliente.

O **CommerceSession**:

* Possui o **carrinho de compras**

   * executa adicionar/remover/etc
   * realiza os vários cálculos no carrinho;

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* Persistência dos proprietários do **pedido** dados:

   `CommerceSession.getUserContext()`

* Pode recuperar/atualizar detalhes do delivery usando `updateOrder(Map<String, Object> delta)`
* Também é proprietária da **pagamento** conexão de processamento
* Também é proprietária da **cumprimento** conexão

### Arquitetura {#architecture}

#### Arquitetura de produto e variantes {#architecture-of-product-and-variants}

Um único produto pode apresentar variações múltiplas; por exemplo, pode variar de acordo com a cor e/ou o tamanho. Um produto deve definir as propriedades que determinam a variação; nós os designamos *eixos de variantes*.

No entanto, nem todas as propriedades são eixos de variante. As variações também podem afetar outras propriedades; por exemplo, o preço pode depender do tamanho. Essas propriedades não podem ser selecionadas pelo comprador e, portanto, não são consideradas eixos de variante.

Cada produto e/ou variante é representado por um recurso e, portanto, mapeia 1:1 para um nó de repositório. É um corolário que um produto e/ou variante específico pode ser identificado exclusivamente pelo seu caminho.

Qualquer recurso de produto pode ser representado por um `Product API`. A maioria das chamadas na API de produto é específica para a variação (embora as variações possam herdar valores compartilhados de um ancestral), mas também há chamadas que listam o conjunto de variações ( `getVariantAxes()`, `getVariants()`, etc.).

>[!NOTE]
>
>Com efeito, os eixos de variantes são determinados pelo `Product.getVariantAxes()` retorna:
>
>* para a implementação genérica, o AEM o lê de uma propriedade nos dados do produto ( `cq:productVariantAxes`)
>
>Embora os produtos (em geral) possam ter vários eixos de variantes, o componente de produto pronto para uso trata apenas de dois:
>
>1. `size`
>1. mais um

>
>   Essa variante adicional é selecionada por meio da variável `variationAxis` propriedade da referência do produto (normalmente `color` para Geometrixx Outdoors).

#### Referências do produto e dados do PIM {#product-references-and-pim-data}

Em geral:

* Os dados do PIM estão localizados em `/etc`

* Referências de produto em `/content`.

Deve haver um mapa 1:1 entre variações de produto e nós de dados de produto.

As referências de produto também devem ter um nó para cada variação apresentada, mas não há necessidade de apresentar todas as variações. Por exemplo, se um produto tiver variações de S, M, L, os dados do produto podem ser:

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

Enquanto um catálogo &quot;Grande e alto&quot; pode ter apenas:

```shell
content
  big-and-tall
    shirt
      shirt-l
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

   * Os nós do produto não são:não estruturados.
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

   * O `CommerceSession` O executa adicionar, remover, etc.
   * O `CommerceSession` O também executa os vários cálculos no carrinho.
   * O `CommerceSession` também aplica comprovantes e promoções que foram disparados para o carrinho.

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

   * Nos carrinhos de AEM genéricos de são armazenados no [ClientContext](/help/sites-administering/client-context.md)

**Personalização**

* A personalização deve sempre ser conduzida pelo [ClientContext](/help/sites-administering/client-context.md).
* Um ClientContext `/version/` do carrinho é criado em todos os casos:

   * Os produtos devem ser adicionados usando o `CommerceSession.addCartEntry()` método .

* O exemplo a seguir ilustra as informações do carrinho no carrinho do ClientContext:

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### Arquitetura do Check-out {#architecture-of-checkout}

**Dados do carrinho e pedido**

O `CommerceSession` é proprietária dos três elementos:

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
   * Use `updateOrder(Map<String, Object> delta)` para recuperar/atualizar os detalhes do delivery.

### Definição de Pesquisa {#search-definition}

Seguindo o modelo padrão de API de serviço, o projeto de eCommerce fornece um conjunto de APIs relacionadas à pesquisa que podem ser implementadas por mecanismos de comércio individuais.

>[!NOTE]
>
>Atualmente, somente o mecanismo de híbridos implementa a API de pesquisa pronta para uso.
>
>No entanto, a API de pesquisa é genérica e pode ser implementada por cada CommerceService individualmente.
>
>Portanto, embora a implementação genérica fornecida pronta para uso não implemente essa API, você pode estendê-la e adicionar a funcionalidade de pesquisa.

O projeto de comércio eletrônico contém um componente de pesquisa padrão, localizado em:

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

Isso usa a API de pesquisa para consultar o mecanismo de comércio selecionado (consulte [Seleção do mecanismo de comércio eletrônico](#ecommerce-engine-selection)):

#### API de pesquisa {#search-api}

Há várias classes genéricas/auxiliares fornecidas pelo projeto principal:

1. `CommerceQuery`

   É usado para descrever uma consulta de pesquisa (contém informações sobre o texto da consulta, página atual, tamanho da página, classificação e aspectos selecionados). Todos os serviços de eCommerce que implementam a API de pesquisa receberão instâncias dessa classe para realizar sua pesquisa. A `CommerceQuery` pode ser instanciado de um objeto de solicitação ( `HttpServletRequest`).

1. `FacetParamHelper`

   É uma classe de utilitário que fornece um método estático - `toParams` - que é utilizado para gerar `GET` strings de parâmetro de uma lista de facetas e um valor alternado. Isso é útil na interface do usuário, onde é necessário exibir um hiperlink para cada valor de cada faceta, de modo que, quando o usuário clica no hiperlink, o respectivo valor é alternado (ou seja, se foi selecionado, ele é removido da consulta, caso contrário, é adicionado). Isso cuida de toda a lógica de lidar com várias facetas/valores únicos, substituir valores etc.

O ponto de entrada da API de pesquisa é o `CommerceService#search` método que retorna um `CommerceResult` objeto. Consulte a Documentação da API para obter mais informações sobre este tópico.

### Desenvolvendo promoções e comprovantes {#developing-promotions-and-vouchers}

* Vouchers:

   * Um Voucher é um componente baseado em página criado/editado com o console Sites e armazenado em:

      `/content/campaigns`

   * Fornecimento de cupom:

      * Um código de comprovante (a ser digitado no carrinho pelo comprador).
      * Um rótulo de comprovante (a ser exibido depois que o comprador o tiver inserido no carrinho).
      * Um caminho de promoção (que define a ação que o comprovante aplica).
   * Os vendedores não têm suas próprias datas/horas de início e término, mas usam aquelas de suas campanhas pai.
   * Os motores de comércio externo podem igualmente fornecer vales; estes requisitos exigem um mínimo de:

      * Um código de voucher
      * Um `isValid()` método
   * O **Voucher** componente ( `/libs/commerce/components/voucher`) fornece:

      * Um renderizador para a administração de vouchers; isso mostra os comprovantes que estão no carrinho.
      * As caixas de diálogo de edição (formulário) para administrar (adicionar/remover) os comprovantes.
      * As ações necessárias para adicionar/remover comprovantes ao/do carrinho.



* Promoções:

   * Uma Promoção é um componente baseado em página criado/editado com o console Sites e armazenado em:

      `/content/campaigns`

   * Fornecimento de promoções:

      * Uma prioridade
      * Um caminho de manipulador de promoção
   * É possível conectar promoções a uma campanha para definir sua data/hora de ativação/desativação.
   * É possível conectar promoções a uma experiência para definir seus segmentos.
   * As promoções não conectadas a uma experiência não serão acionadas por conta própria, mas ainda podem ser acionadas por um Voucher.
   * O componente Promoção ( `/libs/commerce/components/promotion`) contém:

      * renderizadores e diálogos para administração de promoção
      * subcomponentes para renderizar e editar parâmetros de configuração específicos dos manipuladores de promoção
   * Dois manipuladores de promoção são fornecidos imediatamente:

      * `DiscountPromotionHandler`, que aplica um desconto absoluto ou percentual em todo o carrinho
      * `PerfectPartnerPromotionHandler`, que aplica um desconto de produto absoluto ou percentual se o produto do parceiro também estiver no carrinho
   * O ClientContext `SegmentMgr` resolve segmentos e o ClientContext `CartMgr` resolve promoções. Cada promoção sujeita a pelo menos um segmento resolvido será acionada.

      * As Promoções Acionadas são enviadas de volta ao servidor por meio de uma chamada AJAX para calcular novamente o carrinho.
      * As Promoções acionadas (e os Vouchers adicionados) também são mostrados no painel ClientContext.




A adição/remoção de um comprovante de um carrinho é realizada por meio do `CommerceSession` API:

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

Assim, o `CommerceSession` é responsável por verificar se um comprovante existe e se pode ser aplicado ou não. Pode ser o caso de vales que só podem ser aplicados se uma determinada condição for preenchida; por exemplo, quando o preço total do carrinho é maior que US$ 100). Se um comprovante não puder ser aplicado por qualquer motivo, a variável `addVoucher` O método lançará uma exceção. Além disso, a variável `CommerceSession` é responsável por atualizar o(s) preço(s) do carrinho após a adição/remoção de um comprovante.

O `Voucher` é uma classe semelhante a bean que contém campos para:

* Código do cupom
* Uma breve descrição
* Fazendo referência à promoção relacionada que indica o tipo e o valor de desconto

O `AbstractJcrCommerceSession` fornecido pode aplicar comprovantes. Os comprovantes retornados pela classe `getVouchers()` são instâncias de `cq:Page` contendo um nó jcr:content com as seguintes propriedades (entre outras):

* `sling:resourceType` (String) - isso precisa ser `commerce/components/voucher`

* `jcr:title` (String) - para a descrição do comprovante
* `code` (String) - o código que o usuário precisa inserir para aplicar esse comprovante
* `promotion` (String) - a promoção a ser aplicada; por exemplo `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

Os manipuladores de promoção são serviços OSGi que modificam o carrinho de compras. O carrinho oferecerá suporte a vários ganchos que serão definidos na variável `PromotionHandler` interface.

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

Três manipuladores de promoção são fornecidos prontos para uso:

* `DiscountPromotionHandler` aplica um desconto absoluto ou percentual em todo o carrinho
* `PerfectPartnerPromotionHandler` aplica um desconto absoluto ou percentual do produto se o parceiro do produto também estiver no carrinho
* `FreeShippingPromotionHandler` aplica transporte gratuito
