---
title: Gerenciar predefinições do visualizador
description: Como criar e gerenciar predefinições do visualizador
uuid: 64fcf16a-7c4a-435b-bf1a-f27b8b39a715
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: cf7823f4-82c2-4e36-9b65-3c58359b8104
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/dynamic-media/viewer-presets
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '4353'
ht-degree: 15%

---


# Managing Viewer Presets{#managing-viewer-presets}

Uma predefinição do visualizador é uma coleção de configurações que determinam como os usuários visualizações ativos de mídia avançada em suas telas de computadores e dispositivos móveis. Se você for um administrador, poderá criar Predefinições do visualizador. As configurações estão disponíveis para uma matriz de opções de configuração do visualizador. Por exemplo, você pode alterar o tamanho de exibição ou o comportamento de zoom do visualizador.

Para obter instruções sobre como criar e personalizar suas próprias predefinições do visualizador HTML5, consulte o SDK *do visualizador HTML5 da* Adobe Scene7. O SDK está disponível no servidor de publicação IS incorporado ao próprio SDK. Cada versão da biblioteca tem sua própria documentação do SDK incluída.

Caminho: `<scene7_domain>/s7sdk/<library_version>/docs/jsdocs/index.html`.
Por exemplo, 3.5 SDK: [https://s7d1.scene7.com/s7sdk/3.5/docs/jsdoc/index.html](https://s7d1.scene7.com/s7sdk/3.5/docs/jsdoc/index.html)

Consulte também o Guia [de referência para visualizadores de](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html)Adobe.

Esta seção descreve como criar, editar e gerenciar predefinições do visualizador. Você pode aplicar uma predefinição do visualizador a um ativo sempre que o pré-visualização. See [Applying Viewer Presets](#applying-a-viewer-preset-to-an-asset).

>[!NOTE]
>
>Observe que a edição de predefinições ** predefinidas e predefinidas do visualizador não é um cenário compatível. Se você tentar editar uma predefinição de visualizador predefinida, será solicitado que você salve a predefinição do visualizador usando um novo nome.

## Acessibilidade do teclado para visualizadores {#keyboard-accessibility-for-viewers}

Todos os visualizadores prontos para uso suportam a acessibilidade do teclado.

Consulte também [Acessibilidade e navegação](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html)do teclado.

## Managing Viewer Presets {#managing-viewer-presets-1}

You can add, edit, delete, publish, unpublish, and preview viewer presets in AEM by tapping **[!UICONTROL Tools]** (hammer icon) > **[!UICONTROL Assets > Viewer Presets.]**

![6_5_tools-assets-viewerpresets](assets/6_5_tools-assets-viewerpresets.png)

>[!NOTE]
>
>Por padrão, o sistema mostra 15 predefinições do visualizador quando você seleciona Visualizadores na visualização detalhada de um ativo. Você pode aumentar esse limite. Consulte [Aumentar o número de predefinições do visualizador exibidas](#increasing-the-number-of-viewer-presets-that-display).

### Suporte do visualizador para páginas da Web com design responsivo {#viewer-support-for-responsive-designed-web-pages}

Páginas da Web diferentes têm necessidades diferentes. Por exemplo, às vezes você deseja uma página da Web que forneça um link que abra o Visualizador HTML5 em uma janela separada do navegador. Em outros casos, pode ser necessário incorporar o Visualizador HTML5 diretamente na página de hospedagem. No último caso, a página da Web pode ter um layout estático. Ou pode ser &quot;responsivo&quot; e exibido de forma diferente em dispositivos diferentes ou para tamanhos diferentes de janelas do navegador. Para acomodar essas necessidades, todos os visualizadores HTML5 predefinidos e prontos para uso que acompanham o Dynamic Media suportam páginas da Web estáticas e páginas da Web responsivas projetadas.

Consulte Biblioteca [de imagens](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/responsive-static-image-library/c-about-responsive-static-image-library.html) responsivas na Ajuda *da API de disponibilização de imagens da* Scene7 para obter mais informações sobre como incorporar visualizadores responsivos às suas páginas da Web.

>[!NOTE]
>
>Observe que você deve publicar todos os visualizadores prontos para uso antes de usá-los pela primeira vez.
>See [Publishing Viewer Presets.](#publishing-viewer-presets)

### Compatibilidade do sistema do Viewer Preset  {#viewer-preset-system-compatibility}

Todas as predefinições de visualizador prontas para uso que acompanham o Dynamic Media são totalmente compatíveis com os seguintes sistemas:

* Desktops
* Apple iPhone
* Apple iPad
* Android Smartphone
* Tablet Android
* Para vídeo, é fornecido suporte adicional para reprodução MP4 para o [Blackberry](https://developer.blackberry.com/devzone/develop/supported_media/bb_media_support_at_a_glance.html#kba1328730952678) e o [Windows Phone](https://msdn.microsoft.com/library/windows/apps/ff462087%28v=vs.105%29.aspx).

### Tipos de mídia avançada para predefinições de visualizador {#rich-media-types-for-viewer-presets}

Os administradores podem adicionar e personalizar os seguintes tipos de mídia avançada ao criar novas predefinições do visualizador.

<table>
 <tbody>
  <tr>
   <td><strong>Conjunto do Carousel</strong><br /> </td>
   <td><p>Pontos de acesso, mapas de imagem ou ambos são adicionados a uma série de duas ou mais imagens. Um cliente pode deslocar as imagens para a esquerda ou para a direita e, em seguida, clicar em um ponto de acesso em uma imagem para obter detalhes adicionais ou para comprar diretamente da categoria, da casa ou das landings page de um site.</p> </td>
  </tr>
  <tr>
   <td><strong>Dimensional</strong><br /> </td>
   <td><p>Exibe cenas 3D que permitem girar, deslocar, aplicar zoom ou reentrar sua câmera.</p> </td>
  </tr>
  <tr>
   <td><strong>Flyout Zoom</strong></td>
   <td><p>Exibe uma segunda imagem da área com zoom ao lado da imagem original. Não há controles para usar - os usuários movem a seleção para a área que desejam visualização.</p> <p>Ao determinar o uso total da largura de banda para esse visualizador, considere que a imagem principal e a imagem flyout são servidas no visualizador. O tamanho da imagem principal (Largura e Altura do palco) e o Fator de zoom determinam o tamanho da imagem de flyout. Para impedir que o tamanho do arquivo de menu suspenso se torne muito grande, equilibre estes dois valores: se você tiver um tamanho de imagem principal grande, abaixe o valor do Fator de zoom. (A Largura do Flyout e a Altura do Flyout determinam o tamanho da janela do flyout, mas não o tamanho da imagem do flyout fornecida para o visualizador.)</p> <p>Por exemplo, se o tamanho da sua imagem principal for 350 por 350 pixels, com um Fator de zoom de 3, a imagem de flyout resultante será de 1050 por 1050 pixels. Se o tamanho da imagem principal for 300 por 300 pixels, com um Fator de zoom de 4, a imagem de flyout será de 1200 por 1200 pixels. Dependendo da configuração de qualidade JPEG (as configurações recomendadas estão entre 80 e 90), é possível diminuir o tamanho do arquivo significativamente. Os fatores de zoom recomendados são de 2,5 a 4, dependendo do tamanho da imagem principal.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom em linha</strong></td>
   <td>Exibe uma imagem da área com zoom no visualizador original. Não há controles para usar. Ou seja, os usuários movem a seleção para a área que desejam visualização.</td>
  </tr>
  <tr>
   <td><strong>Definição de imagem</strong></td>
   <td>No visualizador Conjunto de imagens, os usuários podem ver visualizações ou variações de cor diferentes de um item clicando em uma imagem em miniatura. Este visualizador também oferta ferramentas de zoom para examinar imagens com atenção.</td>
  </tr>
  <tr>
   <td><strong>Imagem interativa</strong></td>
   <td>Os hotspots são adicionados a partes de uma imagem em que um cliente pode clicar para obter detalhes adicionais ou para comprar diretamente da categoria, da casa ou do landing page de um site.</td>
  </tr>
  <tr>
   <td><strong>Vídeo interativo</strong></td>
   <td>As miniaturas são adicionadas aos segmentos da linha do tempo em um vídeo em que um cliente pode clicar para obter detalhes adicionais ou para comprar diretamente da categoria, da página inicial ou das landings page de um site.</td>
  </tr>
  <tr>
   <td><strong>Mix de mídia</strong></td>
   <td>Exibe tipos diferentes de mídia em um visualizador. Você pode incluir conjuntos de rotação, conjunto de imagens, imagens e vídeos.</td>
  </tr>
  <tr>
   <td><strong>Imagem panorâmica</strong></td>
   <td><p>Os visualizadores de Imagem panorâmica e PanorâmicaVR renderizam imagens panorâmicas esféricas para mergulhar os usuários em uma experiência de visualização de 360° de uma sala, propriedade, local ou paisagem.</p> <p>Para que uma imagem carregada seja qualificada como um panorama esférico, ela deve ter um ou ambos os seguintes:</p>
    <ul>
     <li>Uma proporção largura/altura de 2:1.</li>
     <li>Marcado com as palavras-chave <code>equirectangular</code>, ou <code>spherical</code> e <code>panorama</code>, ou <code>spherical </code>e <code>panoramic</code>. Consulte <a href="/help/sites-authoring/tags.md">Uso de tags</a>.</li>
    </ul> <p>Tanto a proporção quanto os critérios de palavra-chave se aplicam aos ativos panorâmicos para a página de detalhes do ativo e o componente WCM "Mídia panorâmica".</p> <p><strong>Importante</strong>: Este visualizador só está disponível no modo Dynamic Media - Scene7.</p> </td>
  </tr>
  <tr>
   <td><strong>Corte inteligente de vídeo</strong><br /> </td>
   <td><p>Use esse visualizador para detectar e recortar automaticamente para o ponto focal em qualquer vídeo.</p> </td>
  </tr>
  <tr>
   <td><strong>Grupo de rotação</strong></td>
   <td>Fornece várias visualizações de uma imagem para que os usuários possam girar o objeto para examinar os diferentes lados e ângulos.</td>
  </tr>
  <tr>
   <td><strong>Vídeo 360</strong></td>
   <td><p>Use o visualizador de vídeo 360/VR para renderizar vídeos necessários para uma experiência de visualização imersiva de uma sala, propriedade, local, paisagem ou procedimento médico.</p> <p>Durante a reprodução num visor plano, o utilizador controla o ângulo de visualização; a reprodução em dispositivos móveis normalmente aproveita seus controles giroscópicos incorporados.</p> <p>O visualizador inclui suporte nativo para o delivery de 360 ativos de vídeo. Por padrão, nenhuma configuração adicional é necessária para exibir ou reproduzir. Você fornece 360 vídeos usando extensões de vídeo padrão, como .mp4, .mkv e .mov. O codec mais comum é H.264.</p> <p><strong>Importante</strong>: Este visualizador só está disponível no modo Dynamic Media - Scene7.</p> </td>
  </tr>
  <tr>
   <td><strong>Vídeo</strong></td>
   <td><p>Reproduz vídeo usando streaming de taxa de bits progressiva ou adaptável. O streaming adaptável de taxa de bits executa automaticamente a detecção de dispositivos e largura de banda para fornecer o vídeo de qualidade correta no formato correto.</p> </td>
  </tr>
  <tr>
   <td><strong>Zoom vertical</strong></td>
   <td><p>O visualizador de zoom vertical permite maximizar uma experiência de visualização de imagem de produto para fornecer aos usuários a melhor representação de um produto. A localização vertical das amostras faz o seguinte:</p>
    <ul>
     <li>Certifique-se de que as amostras estejam "acima da dobra".<br/> Com amostras horizontais, dependendo do tamanho da tela da área de trabalho do usuário, as amostras não ficavam visíveis até que o usuário rolasse para baixo na página. Ao colocar as amostras verticalmente no visualizador, ele garante que elas fiquem visíveis, independentemente do tamanho da tela do usuário.</li>
     <li>Maximiza o tamanho da imagem principal.<br /> Com amostras horizontais, é necessário reservar espaço na página para garantir que elas estejam visíveis. Esse posicionamento diminuiu o tamanho da imagem principal. No entanto, com um layout de amostra vertical, não é necessário alocar esse espaço. Assim, você pode maximizar o tamanho da imagem principal.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Zoom</strong></td>
   <td>Permite que os usuários aumentem o zoom na área clicando nela. Os usuários podem clicar em controles para aumentar o zoom, diminuir o zoom e redefinir a imagem para seu tamanho padrão.</td>
  </tr>
 </tbody>
</table>

### Lista das predefinições do visualizador predefinidas {#list-of-out-of-the-box-viewer-presets}

A tabela a seguir identifica todas as predefinições de visualizador predefinidas e predefinidas que vêm com o Dynamic Media.

Consulte também Demos [ao](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html)vivo.

Para obter informações sobre o navegador da Web e as versões do sistema operacional compatíveis para visualizadores, consulte as Notas de versão dos visualizadores.

Consulte &quot;Notas de versão dos visualizadores&quot; no sumário do Guia [de referência dos](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html)visualizadores.

>[!NOTE]
>
>Todas as predefinições do visualizador predefinidas no Dynamic Media já estão ativadas (ativadas), mas é necessário publicá-las.
>See [Publishing Viewer Presets](#publishing-viewer-presets).
>
>Todas as novas predefinições do visualizador que você criar e adicionar devem estar ativadas *e *publicadas.
>Consulte [Ativando ou Desativando predefinições](#activating-or-deactivating-viewer-presets) do visualizador e predefinições [do visualizador de](#publishing-viewer-presets)publicação.

<table>
 <tbody>
  <tr>
   <td><strong>Título predefinido do visualizador</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Nome do arquivo CSS</strong><br /> </td>
  </tr>
  <tr>
   <td>Carrossel_Dotted_black</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_dotted_dark.css</code></td>
  </tr>
  <tr>
   <td>Carrossel_Dotted_light</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_dotted_light.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_black</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_numeric_dark.css</code></td>
  </tr>
  <tr>
   <td>Carousel_Numeric_light</td>
   <td>Carousel_Set</td>
   <td><code>html5_carouselviewer_numeric_light.css</code></td>
  </tr>
  <tr>
   <td>Dimensional</td>
   <td>Dimensional</td>
   <td><code>html5_dimensionalviewer.css</code></td>
  </tr>
  <tr>
   <td>Flyout</td>
   <td>Flyout_Zoom</td>
   <td><code>html5_flyoutviewer.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_black</td>
   <td>Definição de imagem</td>
   <td><code>html5_zoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ImageSet_light</td>
   <td>Definição de imagem</td>
   <td><code>html5_zoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_black</td>
   <td>Mixed_Media</td>
   <td><code>html5_inlinemixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>InlineMixedMedia_light</td>
   <td>Mixed_Media</td>
   <td><code>html5_inlinemixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomEmLinha</td>
   <td>Flyout_Zoom</td>
   <td><code>html5_inlinezoomviewer.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_black</td>
   <td>Mixed_Media</td>
   <td><code>html5_mixedmediaviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>MixedMedia_light</td>
   <td>Mixed_Media</td>
   <td><code>html5_mixedmediaviewer_light.css</code></td>
  </tr>
  <tr>
   <td>PanorâmicaImage</td>
   <td>Panorâmico_Imagem</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>PanorâmicaImageVR</td>
   <td>Panorâmico_Imagem</td>
   <td><code>html5_panoramicimage.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Banner</td>
   <td>Interative_Image</td>
   <td><code>html5_interactiveimage.css</code></td>
  </tr>
  <tr>
   <td>Comprável_Vídeo_escuro</td>
   <td>Interative_Video</td>
   <td><code>html5_interactivevideoviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Shoppable_Video_light</td>
   <td>Interative_Video</td>
   <td><code>html5_interactivevideovewer_light.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewer.css</code></td>
  </tr>
  <tr>
   <td>SmartCropVideo_social</td>
   <td>Smart_Crop_Video</td>
   <td><code>html5_smartcropvideoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_black</td>
   <td>Spin_Set</td>
   <td><code>html5_spinviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>SpinSet_light</td>
   <td>Spin_Set</td>
   <td><code>html5_spinviewer_light.css</code></td>
  </tr>
  <tr>
   <td><p>Vídeo</p> <p>(Inclui suporte para legendagem fechada)</p> </td>
   <td>Vídeo</td>
   <td><code>html5_videoviewer.css</code></td>
  </tr>
  <tr>
   <td><p>Video360_social</p> <p>(Inclui controles básicos de reprodução de vídeo, renderização de vídeo feita no modo estéreo, controle manual de ponto de visualização desativado, mas controle giroscópico ativado e nenhum recurso de mídia social)</p> </td>
   <td>Vídeo_360</td>
   <td><code>html5_video360viewersocial.css</code></td>
  </tr>
  <tr>
   <td><p>Video360VR</p> <p>(Projetado para usuários finais que usam óculos de realidade virtual. Inclui controles básicos de reprodução de vídeo e recursos de mídia social)</p> </td>
   <td>Vídeo_360</td>
   <td><code>html5_video360viewer.css</code></td>
  </tr>
  <tr>
   <td><p>Vídeo_social</p> <p>(Inclui suporte para legendagem fechada e mídia social)</p> </td>
   <td>Vídeo</td>
   <td><code>html5_videoviewersocial.css</code></td>
  </tr>
  <tr>
   <td>Zoom_escuro<br /> </td>
   <td>Zoom<br /> </td>
   <td><code>html5_basiczoomviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>Zoom_light<br /> </td>
   <td>Zoom</td>
   <td><code>html5_basiczoomviewer_light.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_escuro<br /> </td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_dark.css</code></td>
  </tr>
  <tr>
   <td>ZoomVertical_light</td>
   <td>Vertical_Zoom</td>
   <td><code>html5_zoomverticalviewer_light.css</code></td>
  </tr>
 </tbody>
</table>

### Matriz de gestos de visualizadores móveis compatíveis {#supported-mobile-viewers-gestures-matrix}

A tabela a seguir identifica os gestos do visualizador móvel compatíveis com dispositivos iOS, Android 2.x e Android 3.x.

<table>
 <tbody>
  <tr>
   <td><strong>Gesto</strong></td>
   <td><strong>Flyout Zoom</strong></td>
   <td><strong>Zoom</strong></td>
   <td><strong>Rotação</strong></td>
  </tr>
  <tr>
   <td><p><strong>Arrastar</strong></p> </td>
   <td><p>Panfletos</p> </td>
   <td><p>Panfletos</p> </td>
   <td><p>Panfletos</p> </td>
  </tr>
  <tr>
   <td><p><strong>Tocar</strong></p> </td>
   <td><p>Mostra a janela do flyout</p> </td>
   <td><p>Mostra ou oculta a interface do usuário</p> </td>
   <td><p>Mostra ou oculta a interface do usuário</p> </td>
  </tr>
  <tr>
   <td><p><strong>Duplo-toque</strong></p> </td>
   <td><p>Não se aplica</p> </td>
   <td><p>Amplia ou redefine</p> </td>
   <td><p>Amplia ou redefine</p> </td>
  </tr>
  <tr>
   <td><p><strong>Pinch open</strong></p> </td>
   <td><p>Não se aplica</p> </td>
   <td><p>Aumenta o zoom (somente iOS e Android 3x)</p> </td>
   <td><p>Aumenta o zoom (somente iOS e Android 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>Aperte para fechar</strong></p> </td>
   <td><p>Não se aplica</p> </td>
   <td><p>Diminui o zoom (somente iOS e Android 3x)</p> </td>
   <td><p>Diminui o zoom (somente iOS e Android 3x)</p> </td>
  </tr>
  <tr>
   <td><p><strong>Deslizar</strong></p> </td>
   <td><p>Barra de amostras de rolagem</p> </td>
   <td><p>Rolar imagens</p> </td>
   <td><p>Gira</p> </td>
  </tr>
  <tr>
   <td><p><strong>Flick</strong></p> </td>
   <td><p>Barra de amostras de rolagem</p> </td>
   <td><p>Rolar imagens</p> </td>
   <td><p>Gira</p> </td>
  </tr>
 </tbody>
</table>

## Increasing the number of Viewer Presets that display {#increasing-the-number-of-viewer-presets-that-display}

AEM mostra uma grande variedade de predefinições do visualizador ao exibir ativos de Visualização **[!UICONTROL Detalhada > Visualizadores.]** Você pode aumentar ou diminuir o número de visualizadores exibidos.

**Para aumentar o número de predefinições do visualizador exibidas**

1. Navegue até CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Navegue até o nó de listagem predefinido do visualizador em `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist`

   ![chlimage_1-221](assets/chlimage_1-221.png)

1. Na propriedade **[!UICONTROL limit]**, altere o **[!UICONTROL Value]**, que é definido como 15 por padrão, para o número desejado.
1. Navegue até a fonte de dados predefinida do visualizador em `/libs/dam/gui/coral/content/commons/sidepanels/viewerpresets/viewerpresetslist/datasource`

   ![chlimage_1-222](assets/chlimage_1-222.png)

1. Na propriedade limit, altere o número para o número desejado, por exemplo `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Toque em **[!UICONTROL Salvar tudo.]**

## Criação de uma predefinição do visualizador {#creating-a-new-viewer-preset}

A criação de predefinições do visualizador permite que você aplique várias configurações à visualização e interaja com ativos. No entanto, não é necessário criar novas predefinições do visualizador. Se preferir, você pode usar as predefinições padrão e predefinidas do visualizador que já vêm com o AEM Assets.

Se você optar por criar uma nova predefinição do visualizador, depois de salvá-la, o estado do visualizador será ativado automaticamente (definido como **[!UICONTROL Ligado]**) na página Predefinições do visualizador. Esse estado significa que está visível no componente Mídia dinâmica e no componente Mídia interativa e sempre que você pré-visualização uma imagem ou vídeo.

Algumas predefinições do visualizador têm configurações exclusivas que podem afetar o uso e o comportamento geral do visualizador. Dependendo da predefinição do visualizador que você estiver criando, talvez você queira estar ciente dessas considerações especiais.

Consulte Considerações [especiais para criar uma predefinição](#special-considerations-for-creating-an-interactive-viewer-preset)do Visualizador interativo.

Consulte Considerações [especiais para criar uma predefinição](#special-considerations-for-creating-a-carousel-banner-viewer-preset)do Visualizador de banner do carrossel.

**Para criar uma predefinição do visualizador**

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Tools]** (hammer icon) > **[!UICONTROL Assets]>[!UICONTROL Viewer Presets]**.

   ![6_5_viewerpresets](assets/6_5_viewerpresets.png)

1. Na página Predefinições do visualizador, na barra de ferramentas, toque em **[!UICONTROL Criar.]**
1. In the **[!UICONTROL New Viewer Preset]** dialog box, in the **[!UICONTROL Preset Name]** field, enter the name of the new preset. Escolha um nome com cuidado, eles não são editáveis depois de tocar em **[!UICONTROL Criar.]**

   Quando você salvar a predefinição posteriormente nessas etapas, o nome será exibido na página Predefinições do visualizador sob o cabeçalho da coluna Título da predefinição.

1. No menu suspenso Rich Media Type (Tipo de mídia avançada), selecione o tipo de predefinição do visualizador que deseja criar e, no canto superior direito da página, toque em **[!UICONTROL Criar.]**

   Consulte Tipos de mídia [avançada para predefinições](#rich-media-types-for-viewer-presets)do visualizador.

1. Na página Editor de predefinições do visualizador, toque na guia **[!UICONTROL Aparência]**.
1. Faça uma das seguintes opções:

   * In the **[!UICONTROL Selected Type]** pull-down menu, select a component whose visual design you want to customize. Como alternativa, toque ou clique em qualquer elemento visual no visualizador para selecioná-lo para configuração.

      O editor visual permite que você veja qual o efeito que determinada propriedade tem em um estilo. Basta definir ou ajustar qualquer propriedade para ver instantaneamente o efeito que ela tem no visualizador usando a amostra à esquerda do editor.

      As propriedades de estilização de CSS para cada tipo de predefinição do visualizador são descritas no tópico da Ajuda &quot;Personalizando o *`<viewer name>`* visualizador&quot; no Guia [de Referência dos](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html)visualizadores. Por exemplo, se você estiver criando uma predefinição do visualizador do tipo `Mixed_Media`, consulte [Personalizar o visualizador](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/mixed-media/customing-mixed-media/c-html5-mixedmedia-viewer-customizingviewer.html) de mídia mista para obter uma lista e uma descrição de cada propriedade.

   * Se você tiver definido as configurações de estilo em um arquivo CSS separado, é possível fazer upload do arquivo CSS para o AEM Assets. Tap **[!UICONTROL Import CSS]** below the **[!UICONTROL Selected Type]** pull-down menu (you may need to scroll the visual editor up to see it) to find the uploaded CSS file and associate it with the viewer preset.

      Ao importar um arquivo CSS, o editor visual verifica se o CSS usa os marcadores do visualizador corretos. Por exemplo, se você estiver criando um visualizador de zoom, todas as regras de CSS que importar deverão ser definidas usando seu nome de classe do visualizador `.s7mixedmediaviewer` definido em um elemento do visualizador pai.

      É possível importar CSS arbitrário e feito à mão, desde que ele defina corretamente os marcadores CSS para um determinado visualizador. (Os marcadores de CSS são descritos em qualquer tópico da Ajuda &quot;Personalizando *&lt;nome do visualizador>* &quot; no Guia [de referência](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/home.html)dos visualizadores. Por exemplo, se você quiser ler sobre marcadores CSS para o Visualizador de zoom, consulte [Personalização do Visualizador](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/zoom/customizing-zoom/c-html5-20-zoom-viewer-customizingviewer.html)de zoom.) É possível, no entanto, que o editor visual não entenda alguns valores de CSS. Nesses casos, o editor visual tenta substituir os erros para que o CSS ainda funcione.
   >[!NOTE]
   >
   >Se preferir editar o CSS diretamente em sua forma bruta, toque em **[!UICONTROL Mostrar/Ocultar CSS]** abaixo do menu suspenso Tipo selecionado (talvez seja necessário rolar o editor visual para cima para vê-lo).
   >Como o editor visual, quando você altera uma propriedade diretamente no CSS, pode ver instantaneamente qual efeito ela tem na amostra do visualizador. E essa mesma propriedade é automaticamente atualizada ao mesmo tempo no editor visual. Dessa forma, você pode usar o editor CSS bruto, o editor visual ou ambos alternadamente.

   >[!NOTE]
   >
   >Para arte-final de botão, escolha a imagem 2x e carregue a arte-final de alta resolução. Ao trabalhar com imagens interativas e banners que podem ser comprados, você também pode selecionar entre uma variedade de botões predefinidos de ponto de acesso.

1. (Opcional) Próximo à parte superior da página Editar predefinição do visualizador, toque em **[!UICONTROL Desktop]**, **[!UICONTROL Tablet]** ou **[!UICONTROL Telefone]** para definir estilos visuais de forma exclusiva para diferentes tipos de dispositivos e telas.
1. On the Viewer Preset Editor page, tap the **[!UICONTROL Behavior]** tab. Como alternativa, toque ou clique em qualquer elemento visual no visualizador para selecioná-lo para configuração.
1. No menu suspenso **[!UICONTROL Tipo selecionado]**, selecione um componente cujos comportamentos você deseja alterar.

   Muitos componentes no editor visual têm uma descrição detalhada associada. Essas descrições aparecem em caixas azuis quando você expande um componente para revelar seus parâmetros associados.

   Alguns tipos de Visualizador têm componentes que permitem especificar comandos do Servidor de imagens em um campo de texto **[!UICONTROL Comando IS]**. Para obter uma lista de comandos que podem ser usados, consulte a [Referência da API de disponibilização de imagens](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-is-home.html).

   >[!NOTE]
   >
   >**Se você estiver usando um dispositivo de toque, como um telefone ou tablet...**
   >
   >
   >Depois de digitar um valor no campo de texto, toque em outro lugar na interface do usuário para enviar a alteração e fechar o teclado virtual. Se você tocar em Enter, nenhuma ação ocorrerá.

1. Near the upper-right corner of the page, tap **[!UICONTROL Save.]**
1. Publique sua nova predefinição de visualizador. Você deve publicar a predefinição antes de usá-la em seu site.

   See [Publishing Viewer Presets](#publishing-viewer-presets).

### Considerações especiais para a criação de uma predefinição de Visualizador interativo {#special-considerations-for-creating-an-interactive-viewer-preset}

**Sobre modos de exibição para miniaturas de imagens no painel**

When you create or edit an Interactive Video viewer preset, you have the choice of which Display Mode setting to use when you select `InteractiveSwatches` from the **[!UICONTROL Selected Component]** pull-down menu under the **[!UICONTROL Behavior]** tab. O modo de exibição escolhido afeta como e quando as miniaturas aparecem enquanto o vídeo está sendo reproduzido. You can choose either a `segment`display mode (default) or a `continuous` display mode.

<table>
 <tbody>
  <tr>
   <td><strong>Modo de exibição</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>Segmento</td>
   <td><p><code>Segment </code>é o modo de exibição padrão para as predefinições prontas para uso do Visualizador de vídeo interativo <code>Shoppable_Video_light</code> <code>Shoppable_Video_dark</code> e para quaisquer predefinições do Visualizador de vídeo interativo que você mesmo criar.</p> <p>Nesse modo, quando há menos miniaturas atribuídas a um segmento de vídeo do que o número de pontos visíveis no painel de exibição, as miniaturas do subsegmento seguinte ou anterior <i>não são </i>puxadas para preencher nenhum ponto vazio no painel. Ou seja, preserva a exibição de amostras que foram atribuídas ao segmento de vídeo específico.</p> </td>
  </tr>
  <tr>
   <td>Contínuo</td>
   <td><p>No modo de <code>continuous </code>exibição, se o número de miniaturas em um segmento for menor do que o número visível no painel, o visualizador incluirá automaticamente a exibição de miniaturas do próximo segmento ou do anterior, nos casos em que a última miniatura for exibida.</p> <p>O <a href="/help/assets/interactive-videos.md">vídeo neste tópico</a> é um exemplo do modo de <code>continuous </code>exibição.</p> </td>
  </tr>
 </tbody>
</table>

**Sobre o comportamento de rolagem automática no Visualizador de vídeo interativo**

O comportamento de rolagem automática das miniaturas no Visualizador de vídeo interativo funciona independentemente do modo de exibição escolhido.

Ao criar ou editar uma predefinição interativa do visualizador de vídeo, você acessa a opção Rolagem automática na guia Comportamento. Na guia Comportamento, no menu suspenso **[!UICONTROL Componentes selecionados]**, toque em **[!UICONTROL InteractiveSwatches.]** A caixa de seleção Rolagem automática está listada abaixo do campo de texto Comando IS.

Se desativar a opção **[!UICONTROL Rolagem automática]** (desmarcar a caixa de seleção) na predefinição do visualizador, durante a reprodução do vídeo pelo usuário, o painel exibirá apenas a primeira imagem em miniatura em toda a duração do vídeo. Entretanto, um usuário pode rolar manualmente pelas miniaturas usando os ícones de seta para cima e para baixo, se desejar.

Ao ativar (selecionar) a **[!UICONTROL Rolagem automática]** na predefinição do visualizador as imagens em miniatura atribuídas a um segmento de vídeo são roladas para exibição no início de um segmento durante a reprodução do vídeo. Entretanto, há instâncias em que determinadas miniaturas em um segmento são exibidas com duas vezes mais comprimento no início ou no final delas. Esse comportamento ocorre porque a quantidade de miniaturas em um segmento é maior que o número visível no painel e não é divisível uniformemente.

Para ilustrar, suponha que você tenha um segmento de vídeo de 30 segundos. E há um total de nove miniaturas para serem exibidas durante 30 segundos. Seu navegador é dimensionado de forma que haja quatro posições de miniatura visíveis no painel de exibição. O segmento de tempo do vídeo de 30 segundos é dividido em três subsegmentos. A tabela a seguir mostra o detalhamento de quais miniaturas são exibidas para um determinado subsegmento de tempo:

| **Subsegmento de vídeo** | **Tempo de subsegmento em segundos** | **Miniaturas que estão visíveis no painel** |
|---|---|---|
| 1 | 0-10 | 1, 2, 3, 4 |
| 2 | 10-20 | 4, 5, 6, 7 |
| 3 | 20-30 | 6, 7, 8, 9 |

O subsegmento 3 do vídeo não se estende além das miniaturas atribuídas a ele. Observe também que as miniaturas 4, 6 e 7 são visíveis no painel duas vezes mais longas que as outras miniaturas.

A lógica usada pelo visualizador para quantas miniaturas são exibidas no painel com base no número de posições disponíveis é a seguinte:

* Número de subsegmentos = arredondar até o próximo subsegmento (número de miniaturas / número de slots visíveis no painel de miniaturas, com base no tamanho da janela do navegador).
Usando o exemplo na tabela acima, 9 miniaturas / 4 slots = 2,25; a lógica do visualizador arredonda até três subsegmentos.

* Número de miniaturas = arredondar para a próxima miniatura (número de miniaturas / número de subsegmentos de vídeo).
Usando o exemplo na tabela acima, 9 miniaturas / 3 subsegmentos de vídeo = 3 miniaturas.

* Duração do subsegmento = duração total do vídeo / número de subsegmentos do vídeo.
Usando o exemplo na tabela acima, 30 segundos / 3 subsegmentos de vídeo = 10 segundos de exibição de cada subsegmento de vídeo.

#### Considerações especiais para a criação de predefinições do visualizador de banner do carrossel {#special-considerations-for-creating-a-carousel-banner-viewer-preset}

Ao criar predefinições do visualizador de banner do carrossel, a alteração do estilo dos pontos de acesso pode ser acessada da seguinte maneira:

|  | **Descrição** | **Ações** |
|---|---|---|
| **[!UICONTROL Ícone de ponto de acesso]** | Alterar o ícone usado para o ponto de acesso | Para alterar a imagem do ícone do ponto de acesso, na guia **[!UICONTROL Aparência]** , em Componente **** selecionado, toque em **[!UICONTROL ImageMapEffect.]** Em **[!UICONTROL Ícone]**, selecione **[!UICONTROL Plano de fundo]** e, no campo **[!UICONTROL Imagem]**, navegue até a imagem de plano de fundo desejada. |

## Ativar ou desativar as predefinições do visualizador {#activating-or-deactivating-viewer-presets}

As predefinições do visualizador que estão disponíveis na interface do usuário dependem de quais estão ativas no modo Autor. Por padrão, uma predefinição do visualizador é &quot;Ligado&quot; depois que você a cria. Se você alternar a predefinição para desativada, ela não será exibida no modo Autor. Se a predefinição for publicada. será sempre publicada independentemente de ser ativada ou desativada. Talvez você queira desativar as predefinições do visualizador se a lista ficar muito fraca ou se não quiser que uma predefinição do visualizador seja disponibilizada para uso.

**Para ativar ou desativar as predefinições do visualizador**

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Tools]** (hammer icon) > **[!UICONTROL Assets]>[!UICONTROL Viewer Presets.]**
1. Na página Predefinição do visualizador, no cabeçalho da coluna **[!UICONTROL Estado]** , toque na alternância para ativar ou desativar uma predefinição do visualizador.

   As predefinições do visualizador ativadas têm a alternância exibida à direita, dentro de uma caixa azul; as predefinições do visualizador desativado exibem a alternância à esquerda, dentro de uma caixa cinza-clara.

## Predefinições do Visualizador de Publicação {#publishing-viewer-presets}

Ativar (ou ativar) o estado de uma predefinição do visualizador significa que ela está visível no componente Mídia dinâmica, no componente Mídia interativa e sempre que você visualização um ativo.

Entretanto, para fornecer* *um ativo com uma predefinição do visualizador, a predefinição do visualizador também deve ser publicada. Todas as predefinições do visualizador devem ser ativadas *e *publicadas para obter o URL ou código incorporado de um ativo. Ative e publique todas as predefinições do visualizador prontas para uso que acompanham o Dynamic Media. As predefinições do visualizador personalizado criadas e adicionadas são ativadas automaticamente, mas também devem ser publicadas.

Consulte [Ativando ou Desativando predefinições](#activating-or-deactivating-viewer-presets)do visualizador.

Consulte também [Visualizar ativos](/help/assets/previewing-assets.md).

**Para publicar predefinições do visualizador**

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Tools]** (hammer icon) > **[!UICONTROL Assets]>[!UICONTROL Viewer Presets.]**
1. Selecione uma ou mais predefinições do visualizador que deseja publicar.
1. Na barra de ferramentas, toque no ícone **[!UICONTROL Publicar]** .

## Predefinições do visualizador de classificação {#sorting-viewer-presets}

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Tools]** (hammer icon) > **[!UICONTROL Assets]>[!UICONTROL Viewer Presets.]**
1. Clique em **[!UICONTROL Título da predefinição]**, **[!UICONTROL Tipo]**, **[!UICONTROL Publicado]** ou **[!UICONTROL Estado]** para classificar pelo cabeçalho da coluna. Por exemplo, clique em **[!UICONTROL Tipo]** para classificar os tipos de predefinição do visualizador em ordem alfabética ou não.

## Edição de predefinições do visualizador {#editing-viewer-presets}

Observe que a edição de predefinições ** predefinidas e predefinidas do visualizador não é um cenário compatível. Se você editar uma predefinição de visualizador predefinida, será solicitado que ela seja salva com um novo nome.

**Para editar predefinições do visualizador**

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Tools]** (hammer icon) > **[!UICONTROL Asset]>[!UICONTROL Viewer Presets.]**
1. Selecione uma predefinição marcando a caixa à esquerda do título predefinido do visualizador.
1. Na barra de ferramentas, toque em **[!UICONTROL Editar.]**
1. Na página do **[!UICONTROL Editor de predefinições do visualizador]**, faça as alterações desejadas na predefinição do visualizador, usando as opções encontradas nas guias **[!UICONTROL Aparência]** e **[!UICONTROL Comportamento]**.

   Na guia **[!UICONTROL Aparência]**, próximo ao canto superior esquerdo da página Editor de predefinições do visualizador, toque em **[!UICONTROL Desktop]**, **[!UICONTROL Tablet]** ou **[!UICONTROL Telefone]** para alterar o modo de apresentação do ativo.

1. Próximo ao canto superior direito da página, execute um dos procedimentos a seguir:

   * Toque em **[!UICONTROL Salvar]** para salvar as alterações e retornar à página Predefinição do visualizador.
   * Toque em **[!UICONTROL Cancelar]** para anular quaisquer alterações feitas e retornar à página Predefinição do visualizador.

## Excluindo predefinições personalizadas do visualizador {#deleting-custom-viewer-presets}

É possível excluir as predefinições do visualizador que você criou e adicionou ao Dynamic Media.

**Para excluir predefinições do visualizador personalizado**

1. No canto superior esquerdo do AEM, toque no logotipo do AEM e, no painel à esquerda, toque em **[!UICONTROL Ferramentas]** (ícone de martelo) **[!UICONTROL > Ativos > Predefinições do visualizador.]**
1. Na página Predefinições do visualizador, marque um Título predefinido e toque no ícone **[!UICONTROL Lixeira]** .
1. Toque em **[!UICONTROL Excluir.]**

## Aplicar predefinições do visualizador a um ativo {#applying-a-viewer-preset-to-an-asset}

Se já tiver publicado o ativo e o visualizador selecionado, os botões **[!UICONTROL URL]** e **[!UICONTROL Incorporar]** aparecerão depois de selecionar uma predefinição do visualizador.

**Para aplicar uma predefinição do visualizador a um ativo**

1. Abra o ativo e, próximo ao canto superior esquerdo da página, toque no menu suspenso e selecione **[!UICONTROL Visualizadores.]**

   >[!NOTE]
   >
   >Se já tiver publicado o ativo e o visualizador selecionado, os botões **[!UICONTROL URL]** e **[!UICONTROL Incorporar]** aparecerão depois de selecionar uma predefinição do visualizador.

1. Selecione uma predefinição do visualizador no painel esquerdo para aplicá-la ao ativo.

   Você pode [copiar o URL para compartilhar](/help/assets/linking-urls-to-yourwebapplication.md) com outros usuários.

## Fornecer ativos com predefinições do visualizador {#delivering-assets-with-viewer-presets}

Para obter os URLs das predefinições do visualizador, consulte [Vincular URLs à sua Aplicação web](/help/assets/linking-urls-to-yourwebapplication.md). Consulte também [Incorporação do visualizador de vídeo em uma página](/help/assets/embed-code.md)da Web.

Se você estiver usando AEM como seu WCM, poderá adicionar ativos usando as predefinições do visualizador diretamente na página. See [Adding Dynamic Media Assets to Pages](/help/assets/adding-dynamic-media-assets-to-pages.md).
