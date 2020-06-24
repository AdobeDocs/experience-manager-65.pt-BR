---
title: Desenvolvimento de conteúdo direcionado
seo-title: Desenvolvimento de conteúdo direcionado
description: Tópicos sobre o desenvolvimento de componentes para uso com direcionamento de conteúdo
seo-description: Tópicos sobre o desenvolvimento de componentes para uso com direcionamento de conteúdo
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '1287'
ht-degree: 0%

---


# Desenvolvimento de conteúdo direcionado{#developing-for-targeted-content}

Esta seção descreve tópicos sobre o desenvolvimento de componentes para uso com direcionamento de conteúdo.

* Para obter informações sobre como se conectar ao Adobe Target, consulte [Integração com o Adobe Target](/help/sites-administering/target.md).
* Para obter informações sobre como criar conteúdo direcionado, consulte [Criação de conteúdo direcionado usando o modo](/help/sites-authoring/content-targeting-touch.md)de definição de metas.

>[!NOTE]
>
>Quando você público alvo um componente no autor de AEM, o componente faz uma série de chamadas do lado do servidor para o Adobe Target para registrar a campanha, configurar o oferta e recuperar segmentos de Adobe Target (se configurado). Nenhuma chamada do lado do servidor é feita da publicação do AEM para o Adobe Target.

## Habilitar a definição de metas com Adobe Target em suas páginas {#enabling-targeting-with-adobe-target-on-your-pages}

Para usar componentes direcionados em suas páginas que interagem com o Adobe Target, inclua um código específico do lado do cliente no elemento &lt;head>.

### Seção principal {#the-head-section}

Adicione ambos os blocos de código a seguir à seção &lt;head> da sua página:

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

Esse código adiciona os objetos javascript do Analytics necessários e carrega as bibliotecas de serviços em nuvem associadas ao site. Para o serviço de Públicos alvos, as bibliotecas são carregadas por meio de `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

O conjunto de bibliotecas carregadas depende do tipo de biblioteca do cliente de público alvo (mbox.js ou at.js) usada na configuração do Público alvo:

**Para mbox.js padrão**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/mbox.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**Para mbox.js personalizado**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/mbox.js"></script>
        <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**Para at.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs.js"></script>
```

>[!NOTE]
>
>Somente a versão do `at.js` enviado com o produto é suportada. A versão do `at.js` enviado com o produto pode ser obtida consultando o `at.js` arquivo no local:
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**.

**Para o at.js personalizado**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

A funcionalidade do Público alvo no lado do cliente é gerenciada pelo `CQ_Analytics.TestTarget` objeto. Portanto, a página conterá algum código init, como no exemplo a seguir:

```
<script type="text/javascript">
            if ( !window.CQ_Analytics ) {
                window.CQ_Analytics = {};
            }
            if ( !CQ_Analytics.TestTarget ) {
                CQ_Analytics.TestTarget = {};
            }
            CQ_Analytics.TestTarget.clientCode = 'my_client_code';
        </script>
      ...

    <div class="cloudservice testandtarget">
  <script type="text/javascript">
  CQ_Analytics.TestTarget.maxProfileParams = 11;

  if (CQ_Analytics.CCM) {
   if (CQ_Analytics.CCM.areStoresInitialized) {
    CQ_Analytics.TestTarget.registerMboxUpdateCalls();
   } else {
    CQ_Analytics.CCM.addListener("storesinitialize", function (e) {
     CQ_Analytics.TestTarget.registerMboxUpdateCalls();
    });
   }
  } else {
   // client context not there, still register calls
   CQ_Analytics.TestTarget.registerMboxUpdateCalls();
  }
  </script>
 </div>
```

O JSP adiciona os objetos javascript de análise e as referências às bibliotecas javascript do lado do cliente. O arquivo testandtarget.js contém as funções mbox.js. O HTML gerado pelo script é semelhante ao seguinte exemplo:

```xml
<script type="text/javascript">
        if ( !window.CQ_Analytics ) {
            window.CQ_Analytics = {};
        }
        if ( !CQ_Analytics.TestTarget ) {
            CQ_Analytics.TestTarget = {};
        }
        CQ_Analytics.TestTarget.clientCode = 'MyClientCode';
</script>
<link rel="stylesheet" href="/etc/clientlibs/foundation/testandtarget/testandtarget.css" type="text/css">
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/testandtarget.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/init.js"></script>
```

#### Seção do corpo (start) {#the-body-section-start}

Adicione o seguinte código imediatamente após a tag &lt;body> para adicionar os recursos de contexto do cliente à página:

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### Seção do corpo (fim) {#the-body-section-end}

Adicione o seguinte código imediatamente antes da tag &lt;/body> final:

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

O script JSP desse componente gera chamadas para a API javascript do Público alvo e implementa outras configurações necessárias. O HTML gerado pelo script é semelhante ao seguinte exemplo:

```xml
<div class="servicecomponents cloudservices">
  <div class="cloudservice testandtarget">
    <script type="text/javascript">
      CQ_Analytics.TestTarget.maxProfileParams = 11;
      CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
        CQ_Analytics.TestTarget.registerMboxUpdateCalls();
      });
    </script>
    <div id="cq-analytics-texthint" style="background:white; padding:0 10px; display:none;">
      <h3 class="cq-texthint-placeholder">Component clientcontext is missing or misplaced.</h3>
    </div>
    <script type="text/javascript">
      $CQ(function(){
      if( CQ_Analytics &&
          CQ_Analytics.ClientContextMgr &&
          !CQ_Analytics.ClientContextMgr.isConfigLoaded )
        {
          $CQ("#cq-analytics-texthint").show();
        }
      });
    </script>
  </div>
</div>
```

### Uso de um arquivo de biblioteca de Públicos alvos personalizado {#using-a-custom-target-library-file}

>[!NOTE]
>
>Se você não estiver usando o DTM ou outro sistema de marketing de públicos alvos, poderá usar arquivos personalizados da biblioteca de públicos alvos.

>[!NOTE]
>
>Por padrão, as mboxes ficam ocultas - a classe mboxDefault determina esse comportamento. Ocultar mboxes garante que os visitantes não vejam o conteúdo padrão antes de ser trocado; entretanto, ocultar mboxes afeta o desempenho percebido.

O arquivo mbox.js padrão usado para criar mboxes está localizado em /etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js. Para usar um arquivo mbox.js do cliente, adicione o arquivo à configuração da nuvem do Público alvo. Para adicionar o arquivo, o arquivo mbox.js deve estar disponível no sistema de arquivos.

Por exemplo, se você quiser usar o serviço [da](https://docs.adobe.com/content/help/en/id-service/using/home.html) Marketing Cloud ID, é necessário baixar o arquivo mbox.js para que ele contenha o valor correto para a `imsOrgID` variável, que se baseia no seu locatário. Essa variável é necessária para integração com o serviço da Marketing Cloud ID. Para obter informações, consulte [Adobe Analytics como a Fonte do Relatórios para Adobe Target](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html) e [Antes de implementar](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/before-implement.html).

>[!NOTE]
>
>Se uma mbox personalizada estiver definida em uma configuração de Público alvo, todos devem ter acesso de leitura a **/etc/cloudservices** nos servidores de publicação. Sem esse acesso, carregar arquivos mbox.js no site de publicação resulta em um erro 404.

1. Vá para a página **Ferramentas** do CQ e selecione **Cloud Service**. ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. Na árvore, selecione Adobe Target e, na lista das configurações, clique com o duplo do mouse na configuração do Público alvo.
1. Na página de configuração, clique em Editar.
1. Para a propriedade Custom mbox.js, clique em Procurar e selecione o arquivo.
1. Para aplicar as alterações, digite a senha da sua conta de Adobe Target, clique em Reconectar ao Público alvo e clique em OK quando a conexão for bem-sucedida. Em seguida, clique em OK na caixa de diálogo Editar componente.

Sua configuração de Público alvo inclui um arquivo mbox.js personalizado, [o código necessário na seção](/help/sites-developing/target.md#p-the-head-section-p) de cabeçalho da sua página adiciona o arquivo à estrutura da biblioteca do cliente em vez de uma referência à biblioteca testandtarget.js.

## Desativação do comando Público alvo para componentes {#disabling-the-target-command-for-components}

A maioria dos componentes pode ser convertida em componentes direcionados usando o comando Público alvo no menu de contexto.

![chlimage_1-21](assets/chlimage_1-21.png)

Para remover o comando Público alvo do menu de contexto, adicione a seguinte propriedade ao nó cq:editConfig do componente:

* Nome: cq:disableTargeting
* Tipo: booliano
* Valor: True

Por exemplo, para desativar a definição de metas dos componentes de título das páginas do Site de demonstração Geometrixx, adicione a propriedade ao nó /apps/geometrixx/components/title/cq:editConfig.

![chlimage_1-22](assets/chlimage_1-22.png)

## Enviando informações de confirmação de pedido para o Adobe Target {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>Se você não estiver usando o DTM, envie a confirmação do pedido para o Adobe Target.

Para rastrear o desempenho de seu site, envie as informações de compra da página de confirmação do pedido para o Adobe Target. (Consulte [Criar uma mbox orderConfirmPage](https://docs.adobe.com/content/help/en/dtm/implementing/target/configure-target/mboxes/order-confirmation-mbox.html) na documentação do Adobe Target.) O Adobe Target reconhece os dados da mbox como dados de confirmação de pedido quando seu nome MBox é exibido `orderConfirmPage` e usa os seguintes nomes de parâmetro específicos:

* productPurchasedId: Uma lista de IDs que identificam os produtos comprados.
* orderId: A ID do pedido.
* orderTotal: O valor total da compra.

O código na página HTML renderizada que cria a mbox é semelhante ao seguinte exemplo:

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

Os valores de cada parâmetro são diferentes para cada pedido. Portanto, é necessário um componente que gera o código com base nas propriedades da compra. A Estrutura [de integração do CQ](/help/sites-administering/ecommerce.md) eCommerce permite a integração com seu catálogo de produtos e a implementação de um carrinho de compras e de uma página de checkout.

A amostra do Geometrixx Outdoors exibe a seguinte página de confirmação quando um visitante compra produtos:

![chlimage_1-23](assets/chlimage_1-23.png)

O código a seguir para o script JSP de um componente acessa as propriedades do carrinho de compras e imprime o código para criar a mbox.

```java
<%--

  confirmationmbox component.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
          import="com.adobe.cq.commerce.api.CommerceService,
                  com.adobe.cq.commerce.api.CommerceSession,
                  com.adobe.cq.commerce.common.PriceFilter,
                  com.adobe.cq.commerce.api.Product,
                  java.util.List, java.util.Iterator"%><%

/* obtain the CommerceSession object */
CommerceService commerceservice = resource.adaptTo(CommerceService.class);
CommerceSession session = commerceservice.login(slingRequest, slingResponse);

/* obtain the cart items */
List<CommerceSession.CartEntry> entries = session.getCartEntries();
Iterator<CommerceSession.CartEntry> cartiterator = entries.iterator();

/* iterate the items and get the product IDs */
String productIDs = new String();
while(cartiterator.hasNext()){
 CommerceSession.CartEntry entry = cartiterator.next();
 productIDs = productIDs + entry.getProduct().getSKU();
    if (cartiterator.hasNext()) productIDs = productIDs + ", ";
}

/* get the cart price and orderID */
String total = session.getCartPrice(new PriceFilter("CART", "PRE_TAX"));
String orderID = session.getOrderId();

%><div class="mboxDefault"></div>
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=<%= productIDs %>',
     'orderId=<%= orderID %>',
     'orderTotal=<%= total %>');
</script>
```

Quando o componente é incluído na página de checkout do exemplo anterior, a fonte da página inclui o seguinte script que cria a mbox:

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## Como entender o componente Público alvo {#understanding-the-target-component}

O componente de Público alvo permite que os autores criem mboxes dinâmicas a partir de componentes de conteúdo do CQ. (Consulte Definição de metas [de conteúdo](/help/sites-authoring/content-targeting-touch.md).) O componente do Público alvo está localizado em /libs/cq/personalization/components/público alvo.

O script público alvo.jsp acessa as propriedades da página para determinar o mecanismo de definição de metas a ser usado para o componente e, em seguida, executa o script apropriado:

* Adobe Target: /libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target com AT.JS](/help/sites-administering/target.md): /libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md): /libs/cq/personalization/components/target/engine_cq_campaign.jsp
* Regras/ContextHub do cliente: /libs/cq/personalization/components/target/engine_cq.jsp

### A criação de mboxes {#the-creation-of-mboxes}

>[!NOTE]
>
>Por padrão, as mboxes ficam ocultas - a classe mboxDefault determina esse comportamento. Ocultar mboxes garante que os visitantes não vejam o conteúdo padrão antes de ser trocado; entretanto, ocultar mboxes afeta o desempenho percebido.

Quando o Adobe Target direciona o conteúdo, o script engine_tnt.jsp cria mboxes que contêm o conteúdo da experiência direcionada:

* Adiciona um `div` elemento com a classe de `mboxDefault`, conforme exigido pela API Adobe Target.

* Adiciona o conteúdo da mbox (o conteúdo da experiência direcionada) dentro do `div` elemento.

Após o elemento `mboxDefault` div, o javascript que cria a mbox é inserido:

* O nome, a ID e o local da mbox são baseados no caminho do repositório do componente.
* O script obtém valores e nomes de parâmetros de Contexto do Cliente.
* São feitas chamadas para as funções que mbox.js e outras bibliotecas clientes definem para criar mboxes.

#### Bibliotecas do cliente para direcionamento de conteúdo {#client-libraries-for-content-targeting}

Veja a seguir as categorias clientlib disponíveis:

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
