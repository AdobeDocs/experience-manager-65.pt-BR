---
title: Criação de pop-ups personalizados usando o Quickviews
seo-title: Uso do Quickviews para criar pop-ups personalizados
description: O Quickview padrão é usado em experiências de comércio eletrônico, onde uma pop-up é exibida com informações do produto para impulsionar uma compra. Você pode acionar a exibição de conteúdo personalizado nos pop-ups.
seo-description: O Quickview padrão é usado em experiências de comércio eletrônico, onde uma pop-up é exibida com informações do produto para impulsionar uma compra. Você pode acionar a exibição de conteúdo personalizado nos pop-ups.
uuid: b906cfff-ac44-4989-b6da-8a9bbf02af03
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
feature: Espectadores
role: Business Practitioner, Administrator
exl-id: 4e7f17ea-6985-4644-b91c-2c1299d01321
source-git-commit: a4e9a4003bf0ce686578d3f8b3fddc19bc49dfb4
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 2%

---

# Uso do Quickviews para criar pop-ups personalizados {#using-quickviews-to-create-custom-pop-ups}

O Quickview padrão é usado em experiências de comércio eletrônico, onde uma pop-up é exibida com informações do produto para impulsionar uma compra. No entanto, você pode acionar a exibição de conteúdo personalizado nas janelas pop-ups. Dependendo do visualizador, essa funcionalidade permite que os usuários toquem em um ponto de acesso ou em uma imagem em miniatura, ou em um mapa de imagem para ver informações ou conteúdo relacionado.

As visualizações rápidas são compatíveis com os seguintes visualizadores no Dynamic Media:

* Imagens interativas (pontos de conexão clicáveis)
* Vídeo interativo (imagens em miniatura clicáveis durante a reprodução do vídeo)
* Banners em carrossel (pontos de conexão clicáveis ou mapas de imagens)

Embora a funcionalidade de cada visualizador seja diferente, o processo de criação de uma exibição rápida é o mesmo em todos os três visualizadores compatíveis.

**Para usar o Quickviews para criar pop-ups personalizados:**

1. Crie uma Exibição rápida para um ativo carregado.

   Geralmente, você cria um Quickview ao mesmo tempo em que edita um ativo para uso com o visualizador que está usando.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizador que você está usando</strong></td>
    <td><strong>Conclua essas etapas se desejar criar o Quickview</strong></td>
    </tr>
    <tr>
    <td>Imagens interativas</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">Adicionar pontos de acesso a um banner</a> de imagem.</td>
    </tr>
    <tr>
    <td>Vídeos interativos</td>
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">Adição de interatividade ao vídeo</a>.</td>
    </tr>
    <tr>
    <td>Banners em carrossel</td>
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">Adição de pontos de acesso ou mapas de imagem a um banner</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Obtenha o código incorporado do visualizador para Integrar o visualizador em seu site.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizador que você está usando</strong><br /> </td>
    <td><strong>Conclua essas etapas se desejar integrar o visualizador ao seu site</strong></td>
    </tr>
    <tr>
    <td>Imagem interativa</td>
    <td><a href="/help/assets/interactive-images.md#integrating-an-interactive-image-with-your-website" target="_blank">Integração de uma imagem interativa ao seu site</a>.<br /> </td>
    </tr>
    <tr>
    <td>Vídeo interativo<br /> </td>
    <td><a href="/help/assets/interactive-videos.md#integrating-an-interactive-video-with-your-website" target="_blank">Integração de um vídeo interativo ao seu site</a>.<br /> </td>
    </tr>
    <tr>
    <td>Banner do carrossel</td>
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Adicionar um banner de carrossel à página</a> do site.<br /> </td>
    </tr>
    </tbody>
   </table>

1. O visualizador que você está usando agora deve saber como usar o Quickview.

   O visualizador usa um manipulador chamado `QuickViewActive`.

   ****
Exemplo de código incorporadoSuponha que você use o seguinte exemplo de código incorporado na sua página da Web para uma imagem interativa:

   ![chlimage_1-291](assets/chlimage_1-291.png)

   O manipulador é carregado no visualizador usando `setHandlers`:

   `*viewerInstance*.setHandlers({ *handler 1*, *handler 2*}, ...`

   **Usando o exemplo de código incorporado de exemplo acima, há o seguinte código:**

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

   Saiba mais sobre o método `setHandlers()` no link a seguir:

   * Visualizador de Imagem Interativa: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * Visualizador de vídeo interativo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. Agora você deve configurar o manipulador `quickViewActivate`.

   O manipulador `quickViewActivate` controla as visualizações rápidas no visualizador. O manipulador contém a lista de variáveis e as chamadas de função para uso com o Quickview. O código incorporado fornece o mapeamento para a variável SKU definida no Quickview e uma chamada de função `loadQuickView` de amostra.

   **Variável**
mappingMap variáveis para uso na sua página da Web para o valor SKU e variáveis genéricas contidas no Quickview:

   `var *variable1*= inData.*quickviewVariable*`

   O código incorporado fornecido tem um mapeamento de amostra para a variável SKU:

   `var sku=inData.sku`

   Mapeie variáveis adicionais do Quickview também, como em:

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   ****
Chamada de funçãoO manipulador também requer uma chamada de função para que o Quickview funcione. A função é considerada acessível pela página de host. O código incorporado fornece uma chamada de função de exemplo:

   `loadQuickView(sku)`

   A chamada de função de amostra assume que a função `loadQuickView()` existe e está acessível.

   Saiba mais sobre o método `quickViewActivate` no link a seguir:

   * Visualizador de Imagem Interativa: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * Visualizador de vídeo interativo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * Suporte a dados interativos no visualizador de Vídeo interativo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. Faça o seguinte:

   * Exclua a seção setHandlers do código incorporado.
   * Mapeie quaisquer variáveis adicionais contidas no Quickview.

      * Atualize a chamada `loadQuickView(sku,*var1*,*var2*)` se você estiver adicionando variáveis adicionais.
   * Crie uma função `loadQuickView` () simples na página, fora do visualizador.

      Por exemplo, o item a seguir grava o valor de SKU no console do navegador:

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Carregue uma página de teste HTML em um servidor da Web e abra.

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

1. Coloque o pop-up `DIV` no corpo da página HTML.

   Um dos elementos é definido com uma ID que é atualizada com o valor SKU quando o usuário chama uma Quickview. O exemplo também inclui um botão simples para ocultar a pop-up novamente depois que ela se tornar visível.

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Adicione uma função para atualizar o valor SKU no pop-up; torne a pop-up visível, substituindo a função simples criada na etapa 5. com o seguinte:

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Faça upload de uma página HTML de teste no seu servidor da Web e abra o . O visualizador exibe a janela pop-up `DIV` quando um usuário chama uma exibição rápida.
1. **Como exibir o pop-up personalizado no modo de tela cheia**

   Alguns visualizadores, como o visualizador de Vídeo interativo, suportam a exibição no modo de tela cheia. No entanto, usar a pop-up conforme descrito nas etapas anteriores faz com que seja exibido atrás do visualizador no modo de tela cheia.

   Para exibir o pop-up nos modos de tela cheia e padrão, anexe o pop-up ao contêiner do visualizador. Use um segundo método de manipulador, `initComplete`.

   O manipulador `initComplete` é chamado após a inicialização do visualizador.

   ```xml
   "initComplete":function() { code block }
   ```

   Saiba mais sobre o método `init()` no link a seguir:

   * Visualizador de Imagem Interativa: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
   * Visualizador de vídeo interativo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-init.html)

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

   No código acima, o seguinte foi feito:

   * Exibição personalizada identificada.
   * Removido-o do DOM.
   * Identificado o contêiner do visualizador.
   * Anexado o pop-up ao contêiner do visualizador.

1. Todo o código setHandlers é semelhante ao seguinte (o visualizador de Vídeo interativo foi usado):

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

1. Após carregar os manipuladores, inicialize o visualizador:

   `*viewerInstance.*init()`

   ****
Exemplo: este exemplo usa o visualizador de imagens interativas.

   `s7interactiveimageviewer.init()`

   Depois de incorporar o visualizador em sua página de host, verifique se a instância do visualizador foi criada e se os manipuladores foram carregados antes que o visualizador seja chamado usando `init()`.
