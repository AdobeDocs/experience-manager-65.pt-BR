---
title: Criar pop-ups personalizados usando o Quickview
description: O Quickview padrão é usado em experiências de comércio eletrônico, nas quais um pop-up é exibido com as informações do produto para impulsionar uma compra. Você pode acionar a exibição do conteúdo personalizado nos pop-ups.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4bcab3f4-500f-432e-b16b-cdc26b9bab4d
feature: Viewers
role: User, Admin
exl-id: 4e7f17ea-6985-4644-b91c-2c1299d01321
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 2%

---

# Criar pop-ups personalizados usando o Quickview {#using-quickviews-to-create-custom-pop-ups}

O Quickview padrão é usado em experiências de comércio eletrônico, nas quais um pop-up é exibido com as informações do produto para impulsionar uma compra. No entanto, é possível acionar a exibição do conteúdo personalizado nas janelas pop-up. Dependendo do visualizador, essa funcionalidade permite que os usuários selecionem em um ponto de acesso, uma imagem em miniatura ou um mapa de imagem para ver informações ou conteúdo relacionado.

A exibição rápida é compatível com os seguintes visualizadores no Dynamic Media:

* Imagem interativa (pontos de acesso clicáveis)
* Vídeo interativo (imagens em miniatura clicáveis durante a reprodução do vídeo)
* Banner do carrossel (pontos de acesso clicáveis ou mapas de imagem)

Embora a funcionalidade de cada visualizador seja diferente, o processo de criação de uma Visualização rápida é o mesmo em todos os três visualizadores compatíveis.

**Para criar pop-ups personalizados usando o Quickview:**

1. Crie uma visualização rápida para um ativo carregado.

   Normalmente, você cria uma Visualização rápida ao mesmo tempo em que edita um ativo para uso com o visualizador que está usando.

   <table>
    <tbody>
    <tr>
    <td><strong>Visualizador que você está usando</strong></td>
    <td><strong>Conclua estas etapas se desejar criar a Visão rápida</strong></td>
    </tr>
    <tr>
    <td>Imagens interativas</td>
    <td><a href="/help/assets/interactive-images.md#adding-hotspots-to-an-image-banner" target="_blank">Adicionar pontos de acesso a um banner de imagem</a>.</td>
    </tr>
    <tr>
    <td>Vídeos interativos</td>
    <td><a href="/help/assets/interactive-videos.md#adding-interactivity-to-your-video" target="_blank">Adicionar interatividade ao vídeo</a>.</td>
    </tr>
    <tr>
    <td>Banners em carrossel</td>
    <td><a href="/help/assets/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner" target="_blank">Adicionar pontos de acesso ou mapas de imagem a um banner</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. Obtenha o código de inserção do visualizador para Integrar o visualizador no seu site.

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
    <td><a href="/help/assets/carousel-banners.md#adding-a-carousel-banner-to-your-website-page" target="_blank">Adicionar um banner de carrossel à página do site</a>.<br /> </td>
    </tr>
    </tbody>
   </table>

1. O visualizador que você está usando deve saber como usar o Quickview.

   O visualizador usa um manipulador chamado `QuickViewActive`.

   **Exemplo**
Suponha que você use o seguinte exemplo de código incorporado do na sua página da Web para uma imagem interativa:

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

   Saiba mais sobre `setHandlers()` no seguinte endereço:

   * Visualizador de imagens interativo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-sethandlers.html)
   * Visualizador de vídeo interativo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/jsapi-interactive-video/r-html5-aem-int-video-javascriptapiref-sethandlers.html)

1. Configure o `quickViewActivate` manipulador.

   A variável `quickViewActivate` O manipulador controla o Quickview no visualizador. O manipulador contém a lista de variáveis e chamadas de função para uso com o Quickview. O código incorporado fornece o mapeamento para a variável SKU definida na Visualização rápida e uma amostra `loadQuickView` função.

   **Mapeamento de variáveis**
Mapeie as variáveis a serem usadas na página da Web para o valor SKU e as variáveis genéricas contidas na exibição rápida:

   `var *variable1*= inData.*quickviewVariable*`

   O código incorporado fornecido tem uma amostra de mapeamento para a variável SKU:

   `var sku=inData.sku`

   Mapeie as variáveis adicionais do Quickview também, como no exemplo a seguir:

   ```
   var <i>variable2</i>= inData.<i>quickviewVariable2</i>
    var <i>variable3</i>= inData.<i>quickviewVariable3</i>
   ```

   **Chamada de função**
O manipulador também requer uma chamada de função para que o Quickview funcione. Supõe-se que a função esteja acessível pela página do host. O código incorporado fornece um exemplo de chamada de função:

   `loadQuickView(sku)`

   A chamada de função de amostra assume a função `loadQuickView()` existe e está acessível.

   Saiba mais sobre `quickViewActivate` no seguinte endereço:

   * Visualizador de imagens interativo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-event-callbacks.html)
   * Visualizador de vídeo interativo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-event-callbacks.html)
   * Suporte a dados interativos no visualizador de vídeo interativo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video-int-data-support.html)

1. Faça o seguinte:

   * Remova o comentário da seção setHandlers do código incorporado.
   * Mapeie quaisquer variáveis adicionais contidas na Quickview.

      * Atualize o `loadQuickView(sku,*var1*,*var2*)` chame se você estiver adicionando variáveis adicionais.

   * Criar uma `loadQuickView` () na página, fora do visualizador.

     Por exemplo, o código a seguir grava o valor do SKU no console do navegador:

   ```xml
   function loadQuickView(sku){
       console.log ("quickview sku value is " + sku);
   }
   ```

   * Carregue uma página de HTML de teste em um servidor da Web e abra.

     Com as variáveis do Quickview mapeadas e a chamada de função estabelecida, o console do navegador grava o valor da variável no console do navegador usando a função de exemplo fornecida.

1. Agora você pode usar uma função para chamar um pop-up simples no Quickview. O exemplo a seguir usa um `DIV` para um pop-up.
1. Estilo do pop-up `DIV` da seguinte forma. Adicione seu próprio estilo adicional, conforme desejado.

   ```xml
   <style type="text/css">
       #quickview_div{
           position: absolute;
           z-index: 99999999;
           display: none;
       }
   </style>
   ```

1. Inserir o pop-up `DIV` no corpo da página do HTML.

   Um dos elementos é definido com uma ID que é atualizada com o valor da SKU quando o usuário chama uma Quickview. O exemplo também inclui um botão simples para ocultar o pop-up novamente depois que ele se tornar visível.

   ```xml
   <div id="quickview_div" >
       <table>
           <tr><td><input id="btnClosePopup" type="button" value="Close"        onclick='document.getElementById("quickview_div").style.display="none"' /><br /></td></tr>
           <tr><td>SKU</td><td><input type="text" id="txtSku" name="txtSku"></td></tr>
       </table>
   </div>
   ```

1. Adicione uma função para atualizar o valor SKU no pop-up; torne o pop-up visível substituindo a função simples criada na etapa 5. com o seguinte:

   ```xml
   <script type="text/javascript">
       function loadQuickView(sku){
           document.getElementById("txtSku").setAttribute("value",sku); // write sku value
           document.getElementById("quickview_div").style.display="block"; // show popup
       }
   </script>
   ```

1. Carregue uma página de HTML de teste no servidor Web e abra. O visualizador exibe o pop-up `DIV` quando um usuário invoca uma Quickview.
1. **Como exibir o pop-up personalizado no modo de tela cheia**

   Alguns visualizadores, como o visualizador de Vídeo interativo, oferecem suporte à exibição no modo de tela cheia. Entretanto, usar o pop-up conforme descrito nas etapas anteriores faz com que ele seja exibido atrás do visualizador enquanto está no modo de tela cheia.

   Para que o pop-up seja exibido nos modos padrão e de tela cheia, anexe o pop-up ao contêiner do visualizador. Use um segundo método de manipulador, `initComplete`.

   A variável `initComplete` é chamado depois que o visualizador é inicializado.

   ```xml
   "initComplete":function() { code block }
   ```

   Saiba mais sobre `init()` no seguinte endereço:

   * Visualizador de imagens interativo: [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/jsapi-interactive-image/r-html5-aem-int-image-viewer-javascriptapiref-init.html)
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

   * Identificada a janela pop-up personalizada.
   * Removido do DOM.
   * Identificado o contêiner do visualizador.
   * Anexado o pop-up ao contêiner do visualizador.

1. Seu código setHandlers inteiro é exibido de forma semelhante ao seguinte (o visualizador de Vídeo interativo foi usado):

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

1. Após carregar os manipuladores, você inicializa o visualizador:

   `*viewerInstance.*init()`

   **Exemplo**
Este exemplo usa o visualizador de Imagem interativa.

   `s7interactiveimageviewer.init()`

   Depois de incorporar o visualizador na página do host, verifique se a instância do visualizador foi criada e se os manipuladores foram carregados antes que o visualizador seja chamado usando `init()`.
