---
title: Adicionar rastreamento do Adobe Analytics aos componentes
description: Adicionar rastreamento do Adobe Analytics aos componentes
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: e6c1258c-81d5-48e4-bdf1-90d7cc13a22d
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 0%

---

# Adicionar rastreamento do Adobe Analytics aos componentes{#adding-adobe-analytics-tracking-to-components}

## Inclusão do módulo Adobe Analytics em um componente de Página {#including-the-adobe-analytics-module-in-a-page-component}

Componentes do modelo de página (por exemplo, `head.jsp, body.jsp`) precisa de JSP para carregar o ContextHub e a integração do Adobe Analytics (que faz parte do Cloud Services). Tudo inclui carregar arquivos JavaScript.

A entrada do ContextHub deve ser incluída imediatamente abaixo de `<head>` tag, enquanto os Cloud Services devem ser incluídos na variável `<head>` e antes da `</body>` seção; por exemplo:

```xml
<head>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub" />
...
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
...
</head>
<body>
...
    <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
</body>
```

A variável `contexthub` script que você insere após a variável `<head>` O elemento adiciona os recursos do ContextHub à página.

A variável `cloudservices` scripts adicionados na variável `<head>` e a variável `<body>` as seções se aplicam às configurações dos serviços em nuvem adicionadas à página. (Se a página usar mais de uma configuração Cloud Services, você deverá incluir a jsp do ContextHub e a jsp Cloud Services apenas uma vez.)

Quando uma estrutura Adobe Analytics é adicionada à página, a variável `cloudservices` Os scripts geram JavaScript relacionado à Adobe Analytics e referências a bibliotecas do lado do cliente, semelhantes ao seguinte exemplo:

```xml
<div class="sitecatalyst cloudservice">
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/util.js"></script>
<script type="text/javascript" src="/content/geometrixx-outdoors/_jcr_content/analytics.sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/mac/mac-sc.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/plugins.js"></script>
<script type="text/javascript">
<!--
CQ_Analytics.Sitecatalyst.frameworkComponents = ['foundation/components/page'];
/**
 * Sets Adobe Analytics variables accordingly to mapped components. If <code>options</code>
 * object is provided only variables matching the options.componentPath are set.
 *
 * @param {Object} options Parameter object from CQ_Analytics.record() call. Optional.
 */
CQ_Analytics.Sitecatalyst.updateEvars = function(options) {
    this.frameworkMappings = [];
 this.frameworkMappings.push({scVar:"pageName",cqVar:"pagedata.title",resourceType:"foundation/components/page"});
    for (var i=0; i<this.frameworkMappings.length; i++){
  var m = this.frameworkMappings[i];
  if (!options || options.compatibility || (options.componentPath == m.resourceType)) {
   CQ_Analytics.Sitecatalyst.setEvar(m);
  }
    }
}

CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
 var collect = true;
    var lte = s.linkTrackEvents;
    s.pageName="content:geometrixx-outdoors:en";
    CQ_Analytics.Sitecatalyst.collect(collect);
    if (collect) {
  CQ_Analytics.Sitecatalyst.updateEvars();
     /************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
     var s_code=s.t();if(s_code)document.write(s_code);
     s.linkTrackEvents = lte;
     if(s.linkTrackVars.indexOf('events')==-1){delete s.events};
     $CQ(document).trigger("sitecatalystAfterCollect");
    }
});
//-->
</script>
<script type="text/javascript">
<!--
if(navigator.appVersion.indexOf('MSIE')>=0)document.write(unescape('%3C')+'\!-'+'-')
//-->
</script>
<noscript><img src="https://daydocumentation.112.2o7.net/b/ss/daydocumentation/1/H.25--NS/1380120772954?cdp=3&gn=content%3Ageometrixx-outdoors%3Aen" height="1" width="1" border="0" alt=""/></noscript>
<span data-tracking="{event:'pageView', values:{}, componentPath:'foundation/components/page'}"></span>
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
```

Todos os sites de amostra de AEM, como Geometrixx Outdoors, têm esse código incluído.

### O evento sitecatalystAfterCollect {#the-sitecatalystaftercollect-event}

A variável `cloudservices` O script aciona o `sitecatalystAfterCollect` evento:

```
$CQ(document).trigger("sitecatalystAfterCollect");
```

Esse evento é acionado para indicar que o rastreamento da página foi concluído. Se você estiver executando operações de rastreamento adicionais nessa página, deverá ouvir esse evento em vez do evento de carregamento de documento ou de documento pronto. Usar o `sitecatalystAfterCollect` Evita colisões ou outros comportamentos imprevisíveis.

>[!NOTE]
>
>A variável `/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js` A biblioteca inclui o código da Adobe Analytics `s_code.js` arquivo.

## Implementação do Adobe Analytics Tracking para componentes personalizados {#implementing-adobe-analytics-tracking-for-custom-components}

Permitir que os componentes do AEM interajam com a estrutura do Adobe Analytics. Em seguida, configure sua estrutura para que o Adobe Analytics rastreie os dados do componente.

Os componentes que interagem com a estrutura do Adobe Analytics aparecem no Sidekick quando você está editando uma estrutura. Depois de arrastar o componente para a estrutura, as propriedades do componente são exibidas e você pode mapeá-las com as propriedades do Adobe Analytics. (Consulte [Configuração de uma estrutura para rastreamento básico](/help/sites-administering/adobeanalytics-connect.md#creating-a-adobe-analytics-framework).)

Os componentes podem interagir com a estrutura do Adobe Analytics quando o componente tem um nó secundário chamado `analytics`. A variável `analytics` possui as seguintes propriedades:

* `cq:trackevents`: identifica os eventos CQ que o componente expõe. (Consulte Eventos personalizados.)
* `cq:trackvars`: nomeia as variáveis do CQ que são mapeadas com as propriedades do Adobe Analytics.
* `cq:componentName`: O nome do componente que aparece no Sidekick.
* `cq:componentGroup`: o grupo no Sidekick que inclui o componente.

O código no componente JSP adiciona o JavaScript à página que aciona o rastreamento e define os dados que são rastreados. O nome do evento e os nomes de dados usados no JavaScript devem corresponder aos valores correspondentes do `analytics` propriedades do nó.

* Use o atributo de rastreamento de dados para rastrear dados de evento quando uma página é carregada. (Consulte [Rastreamento de eventos personalizados no carregamento da página](/help/sites-developing/extending-analytics.md#tracking-custom-events-on-page-load).)
* Use a função CQ_Analytics.record para rastrear dados do evento quando os usuários interagem com recursos da página. (Consulte [Rastreamento de eventos personalizados após o carregamento da página](/help/sites-developing/extending-analytics.md#tracking-custom-events-after-page-load).)

Quando você usa esses métodos de rastreamento de dados, o módulo de integração do Adobe Analytics executa automaticamente as chamadas para o Adobe Analytics registrar os eventos e dados.

### Exemplo: Rastreamento de cliques de navegação superior {#example-tracking-topnav-clicks}

Estenda o componente de navegação superior de base para que o Adobe Analytics rastreie cliques nos links de navegação na parte superior da página. Quando um link de navegação é clicado, o Adobe Analytics registra o link que foi clicado e a página em que ele foi clicado.

Os procedimentos a seguir exigem que você já tenha executado as seguintes tarefas:

* Criado um aplicativo do CQ.
* Criação de uma configuração do Adobe Analytics e de uma estrutura Adobe Analytics.

#### Copiar o componente de navegação superior {#copy-the-topnav-component}

Copie o componente de navegação superior para o aplicativo CQ. O procedimento exige que o aplicativo esteja configurado no CRXDE Lite.

1. Clique com o botão direito do mouse no `/libs/foundation/components/topnav` e clique em Copiar.
1. Clique com o botão direito do mouse na pasta Componentes abaixo da pasta do aplicativo e clique em Colar.
1. Clique em Salvar tudo.

#### Integração Do topnav À Estrutura Do Adobe Analytics {#integrating-topnav-with-the-adobe-analytics-framework}

Configure o componente de navegação superior e edite o arquivo JSP para definir os eventos e dados de rastreamento.

1. Clique com o botão direito do mouse no nó de navegação superior e clique em Criar > Criar nó. Especifique os seguintes valores de propriedade e clique em OK:

   * Nome: `analytics`
   * Tipo: `nt:unstructured`

1. Adicione a seguinte propriedade ao nó do Analytics para nomear o evento de rastreamento:

   * Nome: cq:trackevents
   * Tipo: String
   * Valor: topnavClick

1. Adicione a seguinte propriedade ao nó do Analytics para nomear as variáveis de dados:

   * Nome: cq:trackvars
   * Tipo: String
   * Valor: topnavTarget,topnavLocation

1. Adicione a seguinte propriedade ao nó do Analytics para nomear o componente para o Sidekick:

   * Nome: cq:componentName
   * Tipo: String
   * Value: topnav (tracking)

1. Adicione a seguinte propriedade ao nó do Analytics para nomear o grupo de componentes para o Sidekick:

   * Nome: cq:componentGroup
   * Tipo: String
   * Valor: Geral

1. Clique em Salvar tudo.
1. Abra o `topnav.jsp` arquivo.
1. No elemento, adicione o seguinte atributo:

   ```xml
   onclick = "tracknav('<%= child.getPath() %>.html')"
   ```

1. Na parte inferior da página, adicione o seguinte código JavaScript:

   ```xml
   <script type="text/javascript">
       function tracknav(target) {
               if (CQ_Analytics.Sitecatalyst) {
                   CQ_Analytics.record({
                       event: 'topnavClick',
                       values: {
                           topnavTarget: target,
                           topnavLocation:'<%=currentPage.getPath() %>.html'
                       },
                       componentPath: '<%=resource.getResourceType()%>'
                   });
               }
       }
   </script>
   ```

1. Clique em Salvar tudo.

O conteúdo do `topnav.jsp` arquivo deve aparecer da seguinte maneira:

```xml
<%@page session="false"%><%--
  Copyright 1997-2008 Day Management AG
  Barfuesserplatz 6, 4001 Basel, Switzerland
  All Rights Reserved.

  This software is the confidential and proprietary information of
  Day Management AG, ("Confidential Information"). You shall not
  disclose such Confidential Information and shall use it only in
  accordance with the terms of the license agreement you entered into
  with Day.

  ==============================================================================

  Top Navigation component

  Draws the top navigation

--%><%@include file="/libs/foundation/global.jsp"%><%
%><%@ page import="java.util.Iterator,
        com.day.text.Text,
        com.day.cq.wcm.api.PageFilter,
        com.day.cq.wcm.api.Page,
        com.day.cq.commons.Doctype,
        org.apache.commons.lang3.StringEscapeUtils" %><%

    // get starting point of navigation
    long absParent = currentStyle.get("absParent", 2L);
    String navstart = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);

    //if not deep enough take current node
    if (navstart.equals("")) navstart=currentPage.getPath();

    Resource rootRes = slingRequest.getResourceResolver().getResource(navstart);
    Page rootPage = rootRes == null ? null : rootRes.adaptTo(Page.class);
    String xs = Doctype.isXHTML(request) ? "/" : "";
    if (rootPage != null) {
        Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
        while (children.hasNext()) {
            Page child = children.next();
            %><a onclick = "tracknav('<%= child.getPath() %>.html')"  href="<%= child.getPath() %>.html"><%
            %><img alt="<%= StringEscapeUtils.escapeXml(child.getTitle()) %>" src="<%= child.getPath() %>.navimage.png"<%= xs %>></a><%
        }
    }
%><script type="text/javascript">
    function tracknav(target) {
            if (CQ_Analytics.Sitecatalyst) {
                CQ_Analytics.record({
                    event: 'topnavClick',
                    values: {
                        topnavTarget:target,
                        topnavLocation:'<%=currentPage.getPath() %>.html'
                    },
                    componentPath: '<%=resource.getResourceType()%>'
                });
            }
    }
</script>
```

>[!NOTE]
>
>Geralmente, é desejável rastrear dados do ContextHub. Para obter informações sobre como usar o JavaScript para obter essas informações, consulte [Acesso a valores no ContextHub](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).

#### Adição do componente de rastreamento ao Sidekick {#adding-the-tracking-component-to-sidekick}

Adicione componentes habilitados para rastreamento com o Adobe Analytics ao Sidekick para poder adicioná-los à estrutura.

1. Abra a estrutura do Adobe Analytics na configuração do Adobe Analytics. ([http://localhost:4502/etc/cloudservices/sitecatalyst.html](http://localhost:4502/etc/cloudservices/sitecatalyst.html))
1. No Sidekick, clique no botão Design.

   ![O botão Design com um quadrado de ângulo reto.](assets/chlimage_1a.png)

1. Na área Configuração de rastreamento de link, clique em Configurar herança.

   ![chlimage_1](assets/chlimage_1aa.png)

1. Na lista Componentes permitidos, selecione navegação superior (rastreamento) na seção Geral e clique em OK.
1. Expanda Sidekick para entrar no modo de edição. O componente agora está disponível no grupo Geral.

#### Adicionar o componente de navegação superior à sua estrutura {#adding-the-topnav-component-to-your-framework}

Arraste o componente de navegação superior para a estrutura do Adobe Analytics e mapeie as variáveis e os eventos do componente para variáveis e eventos do Adobe Analytics. (Consulte [Configuração de uma estrutura para rastreamento básico](/help/sites-administering/adobeanalytics-connect.md).)

![chlimage_1-1](assets/chlimage_1-1a.png)

O componente de navegação superior agora está integrado à estrutura do Adobe Analytics. Ao adicionar o componente a uma página, clicar nos itens na barra de navegação superior faz com que os dados de rastreamento sejam enviados ao Adobe Analytics.

### Envio de dados do s.products para o Adobe Analytics {#sending-s-products-data-to-adobe-analytics}

Os componentes podem gerar dados para a variável s.products enviada para o Adobe Analytics. Projete seus componentes para contribuir com a variável s.products:

* Registre um valor chamado `product` estrutura específica.
* Expor os membros de dados do `product` para que possam ser mapeadas com variáveis Adobe Analytics na estrutura do Adobe Analytics.

A variável s.products do Adobe Analytics usa a seguinte sintaxe:

```
s.products="category;product;quantity;price;eventY={value}|eventZ={value};evarA={value}|evarB={value}"
```

O módulo de integração do Adobe Analytics constrói a `s.products` usando o `product` valores gerados por componentes AEM. A variável `product` O valor no JavaScript que os componentes AEM geram é uma matriz de valores que tem a seguinte estrutura:

```
"product": [{
    "category": "",
    "sku"     : "path to product node",
    "quantity": quantity,
    "price"   : price,
    "events   : {
      "eventName1": "eventValue1",
      "eventName_n": "eventValue_n"
    }
    "evars"   : {
      "eVarName1": "eVarValue1",
      "eVarName_n": "eVarValue_n"
    }
}]
```

Quando um item de dados é omitido da variável `product` é enviado como uma cadeia de caracteres vazia em s.products.

>[!NOTE]
>
>Quando nenhum evento é associado a um valor de produto, o Adobe Analytics usa o `prodView` por padrão.

A variável `analytics` o nó do componente deve expor os nomes das variáveis usando o `cq:trackvars` propriedade:

* product.category
* product.sku
* product.quantity
* product.price
* product.events.eventName1
* product.events.eventName_n
* product.evars.eVarName1
* product.evars.eVarName_n

O módulo de comércio eletrônico fornece vários componentes que geram dados variáveis de s.products. Por exemplo, a variável `submitorder` componente ([http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp](http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp)) gera um JavaScript semelhante ao seguinte exemplo:

```
<script type="text/javascript">
    function trackCartPurchase() {
        if (CQ_Analytics.Sitecatalyst) {
            CQ_Analytics.record({
                "event": ["productsCartPurchase"],
                "values": {
                    "product": [
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/1",
                            "quantity": 3,
                            "price"   : 179.7,
                            "evars"   : {
                                "childSku": "/path/to/prod/1/green/xs",
                                "size"    : "XS"
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/2",
                            "quantity": 10,
                            "price"   : 150,
                            "evars"   : {
                                "childSku": "/path/to/prod/2",
                                "size"    : ""
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/3",
                            "quantity": 2,
                            "price"   : 102,
                            "evars"   : {
                                "childSku": "/path/to/prod/3/m",
                                "size"    : "M"
                            }
                        }
                    ]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["discountRedemption"],
                "values": {
                    "discount": "/path/to/discount/1 - /path/to/discount/2",
                    "product" : [{
                        "category": "",
                        "sku"     : "Promotional Discount",
                        "events"  : {"discountRedemption": 20.00}
                    }]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["cartPurchase"],
                "values": {
                    "orderId"       : "00e40e2d-13a2-4a00-a8ee-01a9ebb0bf68",
                    "shippingMethod": "overnight",
                    "paymentMethod" : "Amex",
                    "billingState"  : "NY",
                    "billingZip"    : "10458",
                    "product"       : [{"category": "", "sku": "", "quantity": "", "price": ""}]
                },
                "componentPath": "commerce/components/submitorder"
            });
        }
        return true;
    }
</script>
```

#### Limitar o tamanho das chamadas de rastreamento {#limiting-the-size-of-tracking-calls}

Geralmente, os navegadores da Web limitam o tamanho de solicitações do GET. Como os valores de produto CQ e SKU são caminhos de repositório, os arrays de produtos que incluem vários valores podem exceder o limite de tamanho da solicitação. Portanto, seus componentes devem limitar o número de itens na variável `product` matriz de cada `CQ_Analytics.record function`. Crie várias funções se o número de itens que você deve rastrear puder exceder o limite.

Por exemplo, o eCommerce `submitorder` O componente limita o número de `product` itens em uma chamada para quatro. Quando o carrinho contém mais de quatro produtos, ele gera vários `CQ_Analytics.record` funções.
