---
title: Acessibilidade no Dynamic Media
description: Saiba mais sobre a acessibilidade no Dynamic Media e no Dynamic Media Viewers
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 696aaa54007e4a78fe6b07d8ba65660595286dca
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# Acessibilidade em [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] suporta o controle de teclado e tecnologias de assistência, como leitores de tela JAWS e NVDA, na interface do usuário de criação.

## Suporte à acessibilidade do teclado em [!DNL Dynamic Media]

Como [!DNL Dynamic Media] é um plug-in para [!DNL Adobe Experience Manager Assets], a maioria do comportamento de controle do teclado é exatamente o mesmo que ocorre no teclado [!DNL Experience Manager Assets]. Por exemplo, o `Cancel` botão em [!DNL Dynamic Media] tem o mesmo realce de foco [!DNL Experience Manager Assets]e reage à `Spacebar` chave como em [!DNL Experience Manager Assets]. Consulte Atalhos de [teclado em Ativos](/help/assets/accessibility.md#keyboard-shortcuts).

Os pressionamentos de teclas suportados por elementos individuais da interface do usuário na maioria dos casos [!DNL Dynamic Media] são óbvios e fáceis de descobrir. O controle de teclado em [!DNL Dynamic Media] é aproximadamente o seguinte:

* Capacidade de usar `Tab` e `Shift+Tab` pressionar teclas para navegar entre elementos interativos na página.
O uso `Tab` avança o foco de entrada para o próximo elemento da interface do usuário na ordem de tabulação; o uso `Shift+Tab` traz o foco de entrada de volta ao elemento anterior da interface do usuário.
O foco transversal segue a localização do elemento natural da interface do usuário na tela e se move de esquerda para direita e de cima para baixo. Além disso, se algum campo apresentar um erro, pressione `Tab` para mover o foco para ele.
* Capacidade de usar a tecla `Spacebar` e `Enter` para ativar elementos padrão da interface do usuário, como botões, lista suspensa e assim por diante.
* A capacidade de ver o foco do teclado é realçada no elemento ativo. O elemento da interface do usuário que tem foco de entrada pode receber uma indicação de foco visual como uma borda renderizada ao redor do elemento da interface do usuário.
* No editor do Hotspot, você pode usar alguns pressionamentos de teclas personalizados, como teclas de seta, para interagir com elementos complexos da interface do usuário para reposicionar pontos de conexão.
* No editor de Vídeo interativo, é possível usar o para selecionar uma imagem e adicioná-la `Spacebar` a um segmento. Além disso, você pode usar a `Backspace` tecla para excluir o item selecionado da guia **[!UICONTROL Conteúdo]** . Além disso, pressione `Tab` as funções conforme desejado para navegar entre os elementos interativos na página.
* No editor de recorte de imagem/recorte inteligente, você pode fazer o seguinte:
   * Use as teclas de seta para recortar o tamanho do quadro, reposicionar a imagem ou ambas.
   * A primeira `Tab` parada realça todo o quadro da imagem. Você pode usar as teclas de seta no teclado para reposicionar o quadro.
   * As quatro `Tab` paradas seguintes são os quatro cantos do quadro. Quando o foco é colocado em um canto do quadro, o canto é realçado. Novamente, você pode usar as teclas de seta no teclado para mover o canto focalizado.
Consulte [Editar o recorte inteligente ou a amostra inteligente de uma única imagem](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Suporte a tecnologia assistiva em [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] os elementos da interface do usuário funcionam com tecnologias de assistência, como leitores de tela. Por exemplo, ele reconhece marcos em uma página quando você navega por marcos usando atalhos do teclado `D` ou regiões usando atalhos do teclado `R`. Ele também narrará o cabeçalho ao navegar usando o atalho do teclado de cabeçalho `H`.

## Suporte de acessibilidade de teclado nos [!DNL Dynamic Media] visualizadores {#keyboard-accessibility-for-dm-viewers}

Todos os componentes de visualizadores prontos para uso [!DNL Dynamic Media] suportam a acessibilidade do teclado para seus clientes.

Consulte Acessibilidade e navegação [do](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) teclado no Guia de Referência do Visualizador de Mídia Dinâmica.

## Suporte a tecnologia assistiva em [!DNL Dynamic Media] visualizadores {#assistive-technology-support-for-dm-viewers}

Todos os componentes do [!DNL Dynamic Media] visualizador suportam funções e atributos ARIA (Accessible Rich Internet Applications) para melhorar a integração com tecnologias de assistência, como leitores de tela.
Consulte o tópico Ajuda para suporte **à tecnologia** Assistive em qualquer tópico do visualizador personalizado no Guia de Referência do Visualizador de Mídia Dinâmica. Por exemplo, consulte Suporte [à tecnologia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) Assistive para o Visualizador de vídeo ou Suporte [à tecnologia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) Assistive para o Visualizador de Imagem interativa.

>[!MORELIKETHIS]
>
>* [Acessibilidade para soluções de Adobe](https://www.adobe.com/accessibility.html)
>* [Acessibilidade em [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

