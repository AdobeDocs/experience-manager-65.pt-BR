---
title: Desenvolvimento com Commerce Cloud SAP
description: A estrutura de integração do SAP Commerce Cloud inclui uma camada de integração com uma API.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: b3de1a4a-f334-44bd-addc-463433204c99
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2287'
ht-degree: 0%

---

# Desenvolvimento com Commerce Cloud SAP {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>A estrutura de comércio eletrônico pode ser usada com qualquer solução de comércio eletrônico. Certos pormenores e exemplos aqui tratados [hybris](https://www.sap.com/products/crm.html) solução.

A estrutura de integração inclui uma camada de integração com uma API. Isso permite:

* conectar um sistema de comércio eletrônico e extrair dados do produto no Adobe Experience Manager (AEM)

* criar componentes do AEM para recursos de comércio, independentemente do mecanismo de comércio eletrônico específico

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[Documentação da API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) O também está disponível.

Vários componentes AEM prontos para uso são fornecidos para usar a camada de integração. Atualmente, são eles:

* um componente de exibição do produto
* um carrinho de compras
* check-out

Para pesquisa, é fornecido um gancho de integração que permite usar a pesquisa AEM, a pesquisa do sistema de comércio eletrônico, uma pesquisa de terceiros ou uma combinação dessas opções.

## Seleção de mecanismo de comércio eletrônico {#ecommerce-engine-selection}

A estrutura de comércio eletrônico pode ser usada com qualquer solução de comércio eletrônico, o mecanismo usado deve ser identificável pelo AEM:

* Mecanismos de comércio eletrônico são serviços OSGi que oferecem suporte ao `CommerceService` interface

   * Os motores podem ser distinguidos por uma `commerceProvider` propriedade de serviço

* Suporte para AEM `Resource.adaptTo()` para `CommerceService` e `Product`

   * A variável `adaptTo` A implementação procura um `cq:commerceProvider` propriedade na hierarquia do recurso:

      * Se encontrado, o valor é usado para filtrar a pesquisa de serviço de comércio.

      * Se não for encontrado, será usado o serviço de comércio com a classificação mais alta.

   * A `cq:Commerce` mixin é usado para que o `cq:commerceProvider` podem ser adicionados a recursos fortemente tipados.

* A variável `cq:commerceProvider` A propriedade também é usada para fazer referência à definição apropriada da fábrica de comércio.

   * Por exemplo, uma variável `cq:commerceProvider` propriedade com o valor `hybris` correlaciona-se com a configuração do OSGi para **Fábrica Day CQ Commerce para Hybris** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory) - onde o parâmetro `commerceProvider` também tem o valor `hybris`.

   * Aqui, outras propriedades, como **Versão do catálogo** O pode ser configurado (quando apropriado e disponível).

Consulte os seguintes exemplos abaixo:

| `cq:commerceProvider = geometrixx` | em uma instalação padrão com AEM, é necessária uma implementação específica. Por exemplo, o exemplo do Geometrixx, que inclui extensões mínimas para a API genérica |
|--- |--- |
| `cq:commerceProvider = hybris` | implementação hybris |

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
>Usando o CRXDE Lite, você pode ver como isso é tratado no componente de produto para a implementação hybris:
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### Desenvolvimento do hybris 4 {#developing-for-hybris}

A extensão hybris da Estrutura de integração de comércio eletrônico foi atualizada para oferecer suporte ao Hybris 5, mantendo a compatibilidade com versões anteriores do Hybris 4.

As configurações padrão no código são ajustadas para Hybris 5.

Para desenvolver o Hybris 4, é necessário o seguinte:

* Ao invocar o maven, adicione o seguinte argumento de linha de comando ao comando

  `-P hybris4`

  Ele baixa a distribuição pré-configurada do Hybris 4 e a incorpora ao pacote `cq-commerce-hybris-server`.

* No gerenciador de configurações do OSGi:

   * Desative o suporte ao Hybris 5 para o serviço Default Response Parser.

   * Certifique-se de que o serviço Manipulador de autenticação básica do Hybris tenha uma classificação de serviço inferior ao serviço Manipulador OAuth do Hybris.

### Tratamento de sessão {#session-handling}

o hybris usa uma sessão de usuário para armazenar informações, como o carrinho de compras do cliente. A ID da sessão é retornada do hybris em um `JSESSIONID` cookie que deve ser enviado em solicitações subsequentes para hybris. Para evitar o armazenamento da ID da sessão no repositório, ela é codificada em outro cookie armazenado no navegador do comprador. As seguintes etapas são executadas:

* Na primeira solicitação, nenhum cookie é definido na solicitação do comprador; portanto, uma solicitação é enviada para a instância hybris para criar uma sessão.

* Os cookies de sessão são extraídos da resposta e codificados em um novo cookie (por exemplo, `hybris-session-rest`) e definido na resposta ao comprador. A codificação em um novo cookie é necessária, pois o cookie original é válido apenas para um determinado caminho e, caso contrário, não seria enviado de volta do navegador em solicitações subsequentes. As informações de caminho devem ser adicionadas ao valor do cookie.

* Em solicitações subsequentes, os cookies são decodificados do `hybris-session-<*xxx*>` e definido no cliente HTTP que é usado para solicitar dados do hybris.

>[!NOTE]
>
>Uma nova sessão anônima é criada quando a sessão original não é mais válida.

#### CommerceSession {#commercesession}

* Esta sessão é &quot;proprietária&quot; do **carrinho de compras**

   * executa adicionar/remover/etc

   * realiza os vários cálculos no carrinho;

     `commerceSession.getProductPrice(Product product)`

* É proprietário do *local de armazenamento* para o **pedido** dados

  `CommerceSession.getUserContext()`

* É proprietário do **pagamento** processando conexão

* É proprietário do **preenchimento** conexão

### Sincronização e publicação do produto {#product-synchronization-and-publishing}

Os dados do produto mantidos em híbridos devem estar disponíveis no AEM. O seguinte mecanismo foi implementado:

* Uma carga inicial de IDs é fornecida pelo hybris como um feed. Pode haver atualizações neste feed.
* a hybris fornece informações de atualização por meio de um feed (que o AEM pesquisa).
* Quando o AEM está usando dados do produto, ele envia solicitações de volta para o hybris dos dados atuais (solicitação de obtenção condicional usando a data da última modificação).
* No Hybris, é possível especificar o conteúdo do feed de maneira declarativa.
* O mapeamento da estrutura do feed para o modelo de conteúdo de AEM ocorre no adaptador do feed no lado do AEM.

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* O importador (b) é usado para a configuração inicial da estrutura da árvore de página no AEM para catálogos.
* Alterações no catálogo em hibris são indicadas ao AEM por meio de um feed, que então se propagam para AEM (b)

   * Produto adicionado/excluído/alterado em relação à versão do catálogo.

   * Produto aprovado.

* A extensão hybris fornece um importador de pesquisa (&quot;esquema hybris&quot;), que pode ser configurado para importar alterações no AEM em um intervalo especificado (por exemplo, a cada 24 horas em que o intervalo é especificado em segundos):

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

* A sincronização de produtos entre versões de catálogo exige uma ativação ou desativação da página do AEM correspondente (a, c)

   * Adicionar um produto a um **Online** a versão do catálogo requer a ativação da página do produto.

   * A remoção de um produto requer desativação.

* Ativar uma página no AEM (c) requer uma verificação (b) e só é possível se

   * O produto está em um estado **Online** versão de catálogo para páginas de produto.

   * Os produtos referenciados estão disponíveis em uma **Online** versão de catálogo para outras páginas (por exemplo, páginas de campanha).

* As páginas de produtos ativadas devem acessar o da **Online** versão (d).

* A instância de publicação do AEM requer acesso a hybris para a recuperação de produtos e dados personalizados (d).

### Arquitetura {#architecture}

#### Arquitetura de produtos e variantes {#architecture-of-product-and-variants}

Um único produto pode ter várias variações; por exemplo, pode variar por cor e/ou tamanho. Um produto deve definir quais propriedades impulsionam a variação; os termos de Adobe *eixos variantes*.

No entanto, nem todas as propriedades são eixos de variantes. As variações também podem afetar outras propriedades; por exemplo, o preço pode depender do tamanho. Essas propriedades não podem ser selecionadas pelo comprador e, portanto, não são consideradas eixos de variante.

Cada produto e/ou variante é representado por um recurso e, portanto, mapeia 1:1 para um nó de repositório. É um corolário que um produto e/ou variante específica possa ser identificado exclusivamente por seu caminho.

O recurso produto/variante nem sempre mantém os dados reais do produto. Pode ser uma representação dos dados mantidos em outro sistema (como hibris). Por exemplo, as descrições e os preços dos produtos não são armazenados no AEM, mas recuperados em tempo real do mecanismo de comércio eletrônico.

Qualquer recurso do produto pode ser representado por um `Product API`. A maioria das chamadas na API do produto é específica da variação (embora as variações possam herdar valores compartilhados de um ancestral), mas também há chamadas que listam o conjunto de variações ( `getVariantAxes()`, `getVariants()`e assim por diante).

>[!NOTE]
>
>Com efeito, um eixo variante é determinado por qualquer `Product.getVariantAxes()` devoluções:
>* hybris o define para a implementação hybris
>
>Embora os produtos (em geral) possam ter muitos eixos de variantes, o componente de produto pronto para uso lida apenas com dois:
>
>1. `size`
>
>1. mais um
>
>Essa variante adicional é selecionada por meio da variável `variationAxis` propriedade da referência do produto (geralmente `color` para Geometrixx Outdoors).

#### Referências do produto e dados do produto {#product-references-and-product-data}

Em geral, os dados do produto estão localizados em `/etc`e referências de produto em `/content`.

Deve haver um mapa 1:1 entre as variações de produtos e os nós de dados do produto.

As referências de produto também devem ter um nó para cada variação apresentada, mas não há necessidade de apresentar todas as variações. Por exemplo, se um produto tiver variações S, M, L, os dados do produto podem ser:

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

Embora um catálogo &quot;Grande e Alto&quot; possa ter apenas:

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
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

   * Os nós do produto são `nt:unstructured`.

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

   * A variável `CommerceSession` executa adicionar/remover/etc.
   * A variável `CommerceSession` também realiza os vários cálculos no carrinho. &quot;

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

   * No caso hybris, o servidor hybris é o proprietário do carrinho.
   * No caso genérico do AEM, os carrinhos de são armazenados no [ClientContext](/help/sites-administering/client-context.md).

**Personalização**

* Sempre impulsionar a personalização por meio do [ClientContext](/help/sites-administering/client-context.md).
* Um ClientContext `/version/` do carrinho é criado em todos os casos:

   * Os produtos devem ser adicionados usando o `CommerceSession.addCartEntry()` método.

* A seguir, há um exemplo de informações sobre o carrinho no carrinho de ClientContexts:

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### Arquitetura do Check-out {#architecture-of-checkout}

**Dados do carrinho e do pedido**

A variável `CommerceSession` O é proprietário dos três elementos:

1. Conteúdo do carrinho
1. Preços
1. Os detalhes do pedido

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
   * Pode recuperar/atualizar detalhes do delivery usando `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>Você pode implementar um seletor de entrega; por exemplo:
>
>`yourProject/commerce/components/shippingpicker`:
>
>* Basicamente, isso pode ser uma cópia de `foundation/components/form/radio`, mas com retornos de chamada para o `CommerceSession` para:
>
>* Verificação da disponibilidade do método
>* Adição de informações de preço
>* Para permitir que os compradores atualizem a página do pedido em AEM (incluindo o superconjunto de métodos de envio e o texto que os descreve), embora ainda tendo o controle para expor as informações relevantes `CommerceSession` informações.

**Processamento de pagamento**

* A variável `CommerceSession` também é proprietária da conexão de processamento de pagamento.

* Os implementadores devem adicionar chamadas específicas (ao serviço de processamento de pagamentos escolhido) à `CommerceSession` execução.

**Atendimento de Pedidos**

* A variável `CommerceSession` também é proprietária da conexão de preenchimento.
* Os implementadores devem adicionar chamadas específicas (para o serviço de processamento de pagamento escolhido) à `CommerceSession` execução.

### Definição de pesquisa {#search-definition}

Seguindo o modelo padrão de API de serviço, o projeto de comércio eletrônico fornece um conjunto de APIs relacionadas à pesquisa que podem ser implementadas por mecanismos de comércio individuais.

>[!NOTE]
>
>Atualmente, apenas o mecanismo hybris implementa a API de pesquisa pronta para uso.
>
>No entanto, a API de pesquisa é genérica e pode ser implementada por cada CommerceService individualmente.

O projeto de comércio eletrônico contém um componente de pesquisa padrão em:

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

Isso usa a API de pesquisa para consultar o mecanismo de comércio selecionado (consulte [Seleção de mecanismo de comércio eletrônico](#ecommerce-engine-selection)):

#### API de pesquisa {#search-api}

Há várias classes genéricas/auxiliares fornecidas pelo projeto principal:

1. `CommerceQuery`

   Descreve uma consulta de pesquisa (contém informações sobre o texto da consulta, página atual, tamanho da página, classificação e aspectos selecionados). Todos os serviços de comércio eletrônico que implementam a API de pesquisa recebem instâncias dessa classe para realizar sua pesquisa. A `CommerceQuery` pode ser instanciado a partir de um objeto de solicitação ( `HttpServletRequest`).

1. `FacetParamHelper`

   É uma classe de utilitário que fornece um método estático - `toParams` - que é utilizado para gerar `GET` strings de parâmetro de uma lista de facetas e um valor alternado. Isso é útil no lado da interface do usuário, em que você deve exibir um hiperlink para cada valor de cada faceta, de modo que, quando o usuário clicar no hiperlink, o respectivo valor seja alternado. Ou seja, se ela foi selecionada, é removida da query; caso contrário, é adicionada. Isso cuida de toda a lógica de lidar com facetas de vários/valores únicos, substituir valores e assim por diante.

O ponto de entrada para a API de pesquisa é o `CommerceService#search` método que retorna um `CommerceResult` objeto. Consulte a [Documentação da API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) para obter mais informações sobre esse tópico.

### Integração de usuários {#user-integration}

A integração é fornecida entre o AEM e vários sistemas de comércio eletrônico. Isso requer uma estratégia para sincronizar compradores entre os vários sistemas para que o código específico do AEM só tenha que saber sobre AEM e vice-versa:

* Autenticação

  Presume-se que o AEM seja o *somente* front-end da web e, portanto, executa *all* autenticação.

* Contas no Hybris

  O AEM cria uma conta correspondente (subordinada) em híbridos para cada comprador. O nome de usuário dessa conta é igual ao nome de usuário do AEM. Uma senha aleatória criptograficamente é gerada automaticamente e armazenada (criptografada) no AEM.

#### Usuários pré-existentes {#pre-existing-users}

Um front-end AEM pode ser posicionado na frente de uma implementação hybris existente. Além disso, um mecanismo hybris pode ser adicionado a uma instalação existente do AEM. Para fazer isso, os sistemas devem ser capazes de lidar com os usuários existentes em ambos os sistemas:

* AEM -> hibris

   * Ao fazer logon no hybris, se o usuário AEM não existir:

      * criar um usuário hybris com uma senha aleatória criptograficamente
      * armazene o nome de usuário hybris no diretório de usuário do AEM

   * Consulte: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`

* hybris -> AEM

   * Ao fazer logon no AEM, se o sistema reconhecer o usuário:

      * tentativa de fazer logon no hybris com o nome de usuário/pwd fornecido
      * se for bem-sucedido, criar o usuário no AEM com a mesma senha (salt específico de AEM resulta em hash específico de AEM)

   * O algoritmo acima é implementado em um Sling `AuthenticationInfoPostProcessor`

      * Consulte: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`

### Personalização do Processo de Importação {#customizing-the-import-process}

Para criar com base na funcionalidade existente, seu manipulador de importação personalizado:

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

Para que o manipulador personalizado seja reconhecido pelo importador, ele deve especificar o `service.ranking`com um valor maior que 0, por exemplo.

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
