---
title: Desenvolvimento de conteúdo direcionado
description: Tópicos sobre o desenvolvimento de componentes para uso com direcionamento de conteúdo
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 92b62532-4f79-410d-903e-d2bca6d0fd1c
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 3%

---

# Desenvolvimento de conteúdo direcionado{#developing-for-targeted-content}

Esta seção descreve tópicos sobre o desenvolvimento de componentes para uso com direcionamento de conteúdo.

* Para obter informações sobre como se conectar com o Adobe Target, consulte [Integração com o Adobe Target](/help/sites-administering/target.md).
* Para obter informações sobre a criação de conteúdo direcionado, consulte [Criação de Conteúdo Direcionado Usando o Modo de Direcionamento](/help/sites-authoring/content-targeting-touch.md).

>[!NOTE]
>
>Ao direcionar um componente no autor do AEM, o componente faz uma série de chamadas do lado do servidor para o Adobe Target registrar a campanha, configurar ofertas e recuperar segmentos do Adobe Target (se configurado). Nenhuma chamada do lado do servidor é feita do ambiente de publicação do AEM para o Adobe Target.

## Ativação do direcionamento com o Adobe Target nas suas páginas {#enabling-targeting-with-adobe-target-on-your-pages}

Para usar componentes direcionados em suas páginas que interagem com o Adobe Target, inclua um código específico do lado do cliente no elemento &lt;head>.

### A seção da cabeça {#the-head-section}

Adicione ambos os blocos de código a seguir à seção &lt;head> da página:

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

Esse código adiciona os objetos JavaScript necessários do Analytics e carrega as bibliotecas do Cloud Service associadas ao site. Para o serviço do Target, as bibliotecas são carregadas via `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

O conjunto de bibliotecas carregadas depende do tipo de biblioteca do cliente do Target (mbox.js ou at.js) usada na configuração do Target:

**Para mbox.js** padrão

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/mbox.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**Para mbox.js personalizada**

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
>Somente a versão de `at.js` que acompanha o produto tem suporte. A versão do `at.js` enviada com o produto pode ser obtida com o arquivo `at.js` no local:
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**.

**Para at.js** personalizada

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

A funcionalidade de Destino no lado do cliente é gerenciada pelo objeto `CQ_Analytics.TestTarget`. Portanto, a página conterá algum código inicial, como no exemplo a seguir:

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

O JSP adiciona os objetos JavaScript do Analytics necessários e as referências às bibliotecas JavaScript do lado do cliente. O arquivo testandtarget.js contém as funções da mbox.js. O HTML gerado pelo script é semelhante ao seguinte exemplo:

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

#### A seção do corpo (início) {#the-body-section-start}

Adicione o seguinte código imediatamente após a tag &lt;body> para adicionar os recursos de contexto do cliente à página:

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### A seção do corpo (fim) {#the-body-section-end}

Adicione o seguinte código imediatamente antes da tag &lt;/body> terminar:

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

O script JSP desse componente gera chamadas para a API javascript do Target e implementa outras configurações necessárias. O HTML gerado pelo script é semelhante ao seguinte exemplo:

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

### Uso de um arquivo da biblioteca de Destino personalizado {#using-a-custom-target-library-file}

>[!NOTE]
>
>Se você não estiver usando o DTM ou outro sistema de marketing do Target, poderá usar arquivos personalizados da biblioteca do Target.

>[!NOTE]
>
>Por padrão, as mboxes estão ocultas - a classe mboxDefault determina esse comportamento. Ocultar as mboxes garante que os visitantes não vejam o conteúdo padrão antes que ele seja trocado; no entanto, ocultar as mboxes afeta o desempenho percebido.

O arquivo mbox.js padrão usado para criar mboxes está localizado em /etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js. Para usar um arquivo mbox.js do cliente, adicione o arquivo à configuração da nuvem do Target. Para adicionar o arquivo, o arquivo mbox.js deve estar disponível no sistema de arquivos.

Por exemplo, se você deseja usar o [serviço de ID de Marketing Cloud](https://experienceleague.adobe.com/docs/id-service/using/home.html), é necessário baixar a mbox.js para que ela contenha o valor correto para a variável `imsOrgID`, que é baseada no seu locatário. Essa variável é necessária para a integração com o serviço de ID de Marketing Cloud. Para obter informações, consulte [Adobe Analytics como Source de Relatórios para Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) e [Antes de Implementar](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html).

>[!NOTE]
>
>Se uma mbox personalizada for definida em uma configuração de Destino, todos deverão ter acesso de leitura a **/etc/cloudservices** nos servidores de publicação. Sem esse acesso, carregar arquivos mbox.js no site de publicação resulta em um erro 404.

1. Vá para a página **Ferramentas** do CQ e selecione **Cloud Service**. ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. Na árvore, selecione Adobe Target e, na lista de configurações, clique duas vezes na configuração do Target.
1. Na página de configuração, clique em Editar.
1. Para a propriedade mbox.js personalizada, clique em Procurar e selecione o arquivo.
1. Para aplicar as alterações, digite a senha da conta do Adobe Target, clique em Reconectar ao Target e em OK quando a conexão for bem-sucedida. Em seguida, clique em OK na caixa de diálogo Editar componente.

Sua configuração do Target inclui um arquivo mbox.js personalizado, [o código necessário na seção de cabeçalho](/help/sites-developing/target.md#p-the-head-section-p) de sua página adiciona o arquivo à estrutura da biblioteca do cliente em vez de uma referência à biblioteca testandtarget.js.

## Desativar o comando Direcionar para componentes {#disabling-the-target-command-for-components}

A maioria dos componentes pode ser convertida em componentes direcionados usando o comando Direcionar no menu de contexto.

![chlimage_1-21](assets/chlimage_1-21.png)

Para remover o comando Target do menu de contexto, adicione a seguinte propriedade ao nó cq:editConfig do componente:

* Nome: cq:disableTargeting
* Tipo: Booleano
* Value: True

Por exemplo, para desativar o direcionamento dos componentes de título das páginas do site de demonstração do Geometrixx, adicione a propriedade ao nó /apps/geometrixx/components/title/cq:editConfig.

![chlimage_1-22](assets/chlimage_1-22.png)

## Enviando informações de confirmação de pedido para a Adobe Target {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>Se não estiver usando o DTM, você envia a confirmação do pedido para a Adobe Target.

Para rastrear o desempenho do seu site, envie informações de compra da página de confirmação de pedido para a Adobe Target. (Consulte [Criar uma mbox orderConfirmPage](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager/?lang=en) e [Mbox de confirmação de pedido - Adicionar parâmetros personalizados.](https://experienceleaguecommunities.adobe.com/t5/adobe-target-questions/order-confirmation-mbox-add-custom-parameters/m-p/275779)) A Adobe Target reconhece os dados da mbox como dados de confirmação de pedido quando o seu nome de MBox é `orderConfirmPage` e usa os seguintes nomes de parâmetros específicos:

* productPurchasedId: uma lista de IDs que identificam os produtos comprados.
* orderId: a ID do pedido.
* orderTotal: a quantia total da compra.

O código na página de HTML renderizada que cria a mbox é semelhante ao seguinte exemplo:

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

Os valores de cada parâmetro são diferentes para cada ordem. Portanto, você precisa de um componente que gere o código com base nas propriedades da compra. A [Estrutura de integração de comércio eletrônico](/help/commerce/cif-classic/administering/ecommerce.md) do CQ permite que você se integre ao catálogo de produtos e implemente um carrinho de compras e uma página de check-out.

O exemplo de Geometrixx Outdoors exibe a seguinte página de confirmação quando um visitante compra produtos:

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

Quando o componente é incluído na página de check-out no exemplo anterior, a origem da página inclui o script a seguir que cria a mbox:

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## Noções básicas sobre o componente de Direcionamento {#understanding-the-target-component}

O componente de Direcionamento permite que os autores criem mboxes dinâmicas a partir de componentes de conteúdo do CQ. (Consulte [Direcionamento de conteúdo](/help/sites-authoring/content-targeting-touch.md).) O componente de Direcionamento está localizado em /libs/cq/personalization/components/target.

O script target.jsp acessa as propriedades da página para determinar o mecanismo de direcionamento a ser usado para o componente e, em seguida, executa o script apropriado:

* Adobe Target: /libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target com AT.JS](/help/sites-administering/target.md): /libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md): /libs/cq/personalization/components/target/engine_cq_campaign.jsp
* Regras do lado do cliente/ContextHub: /libs/cq/personalization/components/target/engine_cq.jsp

### A criação de mboxes {#the-creation-of-mboxes}

>[!NOTE]
>
>Por padrão, as mboxes estão ocultas - a classe mboxDefault determina esse comportamento. Ocultar as mboxes garante que os visitantes não vejam o conteúdo padrão antes que ele seja trocado; no entanto, ocultar as mboxes afeta o desempenho percebido.

Quando o Adobe Target direciona o direcionamento de conteúdo, o script engine_tnt.jsp cria mboxes que contêm o conteúdo da experiência direcionada:

* Adiciona um elemento `div` com a classe de `mboxDefault`, conforme exigido pela API do Adobe Target.

* Adiciona o conteúdo da mbox (o conteúdo da experiência direcionada) dentro do elemento `div`.

Após o elemento div `mboxDefault`, o javascript que cria a mbox é inserido:

* O nome, a ID e o local da mbox se baseiam no caminho do repositório do componente.
* O script obtém os nomes e valores dos parâmetros do Client Context.
* As chamadas são feitas às funções que a mbox.js e outras bibliotecas de clientes definem para criar mboxes.

#### Bibliotecas de clientes para direcionamento de conteúdo {#client-libraries-for-content-targeting}

Estas são as categorias das bibliotecas de clientes disponíveis:

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
