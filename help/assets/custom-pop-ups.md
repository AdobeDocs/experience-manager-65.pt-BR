---
title: Uso do Quickviews para criar pop-ups personalizados
seo-title: Uso do Quickviews para criar pop-ups personalizados
description: A exibição rápida padrão é usada em experiências de comércio eletrônico, em que uma janela pop-up é exibida com informações do produto para acionar uma compra. Você pode acionar a exibição de conteúdo personalizado nos pop-ups.
seo-description: A exibição rápida padrão é usada em experiências de comércio eletrônico, em que uma janela pop-up é exibida com informações do produto para acionar uma compra. Você pode acionar a exibição de conteúdo personalizado nos pop-ups.
uuid: b906cfff-ac44-4989-b6da-8a9bbf02af03
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
translation-type: tm+mt
source-git-commit: 7e9dcebc654e63e171e2baacfe53081f58676f8d
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 2%

---


# Uso do Quickviews para criar pop-ups personalizados {#using-quickviews-to-create-custom-pop-ups}

A exibição rápida padrão é usada em experiências de comércio eletrônico, em que uma janela pop-up é exibida com informações do produto para acionar uma compra. No entanto, é possível acionar a exibição de conteúdo personalizado nos pop-ups. Dependendo do visualizador usado, essa funcionalidade permite que os usuários cliquem em um ponto de acesso ou em uma imagem em miniatura, ou em um mapa de imagem para ver informações ou conteúdo relacionado.

As exibições rápidas são suportadas pelos seguintes visualizadores no Dynamic Media:

* Imagens interativas (pontos de acesso clicáveis)
* Vídeo interativo (imagens em miniatura clicáveis durante a reprodução do vídeo)
* Banners de carrossel (pontos de conexão clicáveis ou mapas de imagem)

Embora a funcionalidade de cada visualizador seja diferente, o processo de criação de uma exibição rápida é o mesmo entre os três visualizadores suportados.

**Para usar o Quickviews para criar pop-ups personalizados**

1. Criar uma exibição rápida para um ativo carregado.

   Geralmente, você cria uma exibição rápida ao mesmo tempo que edita um ativo para uso com o visualizador que está usando.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizador que você está usando</strong></td>
    <td><strong>Conclua estas etapas para criar o Quickview</strong></td>
    </tr>
    <tr>
    <td>Imagens interativas</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">Adicionar pontos de acesso a um banner</a>de imagem.</td>
    </tr>
    <tr>
    <td>Vídeos interativos</td>
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">Adicionando interatividade ao vídeo</a>.</td>
    </tr>
    <tr>
    <td>Banners em carrossel</td>
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">Adicionar pontos de conexão ou mapas de imagem a um banner</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Obtenha o código incorporado do visualizador para integrar o visualizador dentro do seu site.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizador que você está usando</strong><br /> </td>
    <td><strong>Complete estas etapas para integrar o visualizador ao seu site</strong></td>
    </tr>
    <tr>
    <td>Imagem interativa</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">Integração de uma imagem interativa com seu site</a>.<br /> </td>
    </tr>
    <tr>
    <td>Vídeo interativo<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">Integração de um vídeo interativo com seu site</a>.<br /> </td>
    </tr>
    <tr>
    <td>Banner do carrossel</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Adicionar um banner de carrossel à página</a>do site.<br /> </td>
    </tr>
    </tbody>
   </table>

1. O visualizador que você está usando agora precisa saber como usar o Quickview.

   Para fazer isso, o visualizador usa um manipulador chamado `QuickViewActive`.

   **Exemplo** Suponha que você esteja usando a seguinte amostra de código incorporado em sua página da Web para uma imagem interativa:

   ![chlimage_1-291](assets/chlimage_1-291.png)

   O manipulador é carregado no visualizador usando `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **Usando o exemplo de código incorporado de exemplo acima, temos o seguinte código:**

   ```xml
   s7interactiveimageviewer.setHandlers({
       quickViewActivate": function(inData) {
           var sku=inData.sku;
           var genericVariable1=inData.genericVariable1;
           var genericVariable2=inData.genericVariable2;
          loadQuickView(sku,genericVariable1,genericVariable2);
       }
   })
   ```

   Saiba mais sobre o `setHandlers()` método no seguinte:

   * Visualizador de imagens interativas: [https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * Visualizador de vídeo interativo: [https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. Agora é necessário configurar o `quickViewActivate` manipulador.

   O `quickViewActivate` manipulador controla as exibições rápidas no visualizador. O manipulador contém a lista variável e as chamadas de função para uso com o Quickview. O código incorporado fornece mapeamento para a variável SKU definida no Quickview, bem como uma chamada de `loadQuickView` função de amostra.

   **Variável mapeando variáveis** do mapa para uso na sua página da Web para o valor SKU e variáveis genéricas contidas no Quickview:

   `var *variable1*= inData.*quickviewVariable*`

   O código incorporado fornecido tem um mapeamento de amostra para a variável SKU:

   `var sku=inData.sku`

   Mapeie variáveis adicionais do Quickview também, como a seguir:

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **Chamada** de função O manipulador também requer uma chamada de função para que o Quickview funcione. Pressupõe-se que a função seja acessível pela página de host. O código incorporado fornece uma chamada de função de exemplo:

   `loadQuickView(sku)`

   A chamada de função de exemplo considera que a função `loadQuickView()` existe e está acessível.

   Saiba mais sobre o `quickViewActivate` método no seguinte:

   * Visualizador de imagens interativas: [https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * Visualizador de vídeo interativo: [https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * Suporte a dados interativos no Visualizador de vídeo interativo: [https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. Faça o seguinte:

   * Exclua as barras de comentário da seção setHandlers do código incorporado.
   * Mapeie quaisquer variáveis adicionais contidas no Quickview.

      * Atualize a `loadQuickView(sku,*var1*,*var2*)` chamada se você estiver adicionando variáveis adicionais.
   * Crie uma função simples `loadQuickView` () na página, fora do visualizador.

      Por exemplo, o seguinte grava o valor de sku no console do navegador:

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Carregue uma página HTML de teste em um servidor Web e abra.

      Com as variáveis do Quickview mapeadas e a chamada de função instalada, o console do navegador grava o valor da variável no console do navegador usando a função de amostra fornecida.



1. Agora você pode usar uma função para invocar um pop-up simples no Quickview. O exemplo a seguir usa um `DIV` para um pop-up.
1. Estilo do pop-up `DIV` da seguinte maneira. Adicione seu próprio estilo adicional, conforme desejado.

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. Coloque o pop-up `DIV` no corpo da sua página HTML.

   Um dos elementos é definido com uma ID que é atualizada com valor de sku quando o usuário chama uma exibição rápida. O exemplo também inclui um botão simples para ocultar o pop-up novamente depois que ele se torna visível.

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Adicione uma função para atualizar o valor de sku no pop-up; torne o pop-up visível, substituindo a função simples criada na etapa 5. com o seguinte:

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Carregue uma página HTML de teste no seu servidor Web e abra. O visualizador exibe o pop-up `DIV` quando um usuário chama uma exibição rápida.
1. **Como exibir o pop-up personalizado no modo de tela cheia**

   Alguns visualizadores, como o Visualizador de vídeo interativo, suportam a exibição no modo de tela cheia. No entanto, usar o pop-up conforme descrito nas etapas anteriores faz com que ele seja exibido atrás do visualizador no modo de tela cheia.

   Para ter a exibição pop-up nos modos padrão e de tela cheia, anexe a pop-up ao container do visualizador. Para fazer isso, você pode usar um segundo método handler, `initComplete`.

   O `initComplete` hander é chamado depois que o visualizador é inicializado.

   ```xml
   "initComplete":function() { code block }
   ```

   Saiba mais sobre o `init()` método no seguinte:

   * Visualizador de imagens interativas: [https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * Visualizador de vídeo interativo: [https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

1. Para anexar o pop-up descrito nas etapas anteriores ao visualizador, use o seguinte código:

   ```xml
   "initComplete":function() {
       var popup = document.getElementById('quickview_div');
       popup.parentNode.removeChild(popup);
       var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
       var inner_container = document.getElementById(sdkContainerId);
       inner_container.appendChild(popup);
   }
   ```

   No código acima, fizemos o seguinte:

   * Identificado nosso pop-up personalizado.
   * Removido do DOM.
   * Identificado o container do visualizador.
   * O pop-up foi anexado ao container do visualizador.

1. O código de setHandlers inteiro agora deve ser semelhante ao seguinte (o visualizador de vídeo interativo foi usado):

   ```xml
   s7interactivevideoviewer.setHandlers({
       "quickViewActivate": function(inData) {
           var sku=inData.sku;
           loadQuickView(sku);
   
       },
       "initComplete":function() {
           var popup = document.getElementById('quickview_div'); // get custom quick view container
           popup.parentNode.removeChild(popup); // remove it from current DOM
           var sdkContainerId = s7interactivevideoviewer.getComponent("container").getInnerContainerId();
           var inner_container = document.getElementById(sdkContainerId);
           inner_container.appendChild(popup);
       }
   });
   ```

1. Depois que os manipuladores forem carregados, você inicializará o visualizador:

   `*viewerInstance.*init()`

   **Exemplo** Este exemplo usa o visualizador de imagem Interativo.

   `s7interactiveimageviewer.init()`

   Depois de incorporar o visualizador à página de host, verifique se a instância do visualizador foi criada e se os manipuladores foram carregados antes que o visualizador seja chamado usando `init()`.

