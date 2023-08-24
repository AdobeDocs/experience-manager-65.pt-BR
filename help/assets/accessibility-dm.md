---
title: Acessibilidade no Dynamic Media
description: Saiba mais sobre o suporte à acessibilidade no Dynamic Media e Dynamic Media Viewers.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
source-git-commit: 29fb61f9fdcb72864068662d935bc01779b9e451
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 1%

---

# Acessibilidade no [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] O suporta controle de teclado e tecnologias assistivas, como leitores de tela JAWS e NVDA, na interface do usuário de criação.

## Suporte para acessibilidade do teclado no [!DNL Dynamic Media]

Porque [!DNL Dynamic Media] é um plug-in para [!DNL Adobe Experience Manager Assets], a maior parte do comportamento de controle do teclado é igual ao de [!DNL Experience Manager Assets]. Por exemplo, a variável `Cancel` botão em [!DNL Dynamic Media] tem o mesmo destaque que em [!DNL Experience Manager Assets], e reage à `Spacebar` chave como em [!DNL Experience Manager Assets]. Consulte [Atalhos de teclado no Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Pressionamentos de tecla suportados por elementos individuais da interface do usuário no [!DNL Dynamic Media] são claras e fáceis de descobrir. Controle de teclado em [!DNL Dynamic Media] O é sobre o seguinte:

* Capacidade de usar `Tab` e `Shift+Tab` pressionamentos de teclas para navegar entre elementos interativos na página.
Usar `Tab` avança o foco de entrada para o próximo elemento da interface do usuário na ordem de tabulação; usando `Shift+Tab` O traz o foco de entrada de volta para o elemento anterior da interface do usuário.
O percurso do foco segue o local natural do elemento da interface do usuário na tela e se move da esquerda para a direita e de cima para baixo. Além disso, se algum campo tiver um erro, você poderá pressionar `Tab` para mover o foco para ele.
* Capacidade de usar o `Spacebar` e `Enter` tecla para ativar elementos padrão da interface do usuário, como botões e listas suspensas.
* Capacidade de ver o foco do teclado destacado no elemento ativo. O elemento da interface do usuário que tem foco de entrada recebe uma indicação de foco visual como uma borda renderizada ao redor do elemento da interface do usuário.
* No editor de ponto de acesso, é possível usar alguns pressionamentos de tecla personalizados, como teclas de seta, para interagir com elementos complexos da interface do usuário e reposicionar pontos de acesso.
* No editor de Vídeo interativo, é possível usar a variável `Spacebar` para selecionar uma imagem e adicioná-la a um segmento. Além disso, você pode usar a variável `Backspace` para excluir o item selecionado da lista **[!UICONTROL Conteúdo]** guia. Além disso, pressionando `Tab` funciona conforme desejado para navegar entre elementos interativos na página.
* No editor de Recorte de imagem/Recorte inteligente, você pode fazer o seguinte:
   * Use as teclas de seta para recortar o tamanho do quadro ou reposicionar a imagem, ou ambos.
   * O primeiro `Tab` parar realça o quadro de imagem inteiro. Em seguida, é possível usar as teclas de seta no teclado para reposicionar o quadro.
   * Os próximos quatro `Tab` as paradas são os quatro cantos do quadro. Quando o foco é colocado em um canto do quadro, o canto é realçado. Novamente, você pode usar as teclas de seta no teclado para mover o canto focalizado.
Consulte [Editar o recorte inteligente ou a amostra inteligente de uma única imagem](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Suporte de tecnologia assistiva no [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] os elementos da interface do usuário funcionam com tecnologias assistivas, como leitores de tela. Por exemplo, ela reconhece pontos de referência em uma página quando você navega por pontos de referência usando o atalho de teclado `D` ou regiões usando o atalho de teclado `R`. Ele também narra o cabeçalho ao navegar usando o atalho de teclado do cabeçalho `H`.

## Suporte para acessibilidade do teclado no [!DNL Dynamic Media] visualizador {#keyboard-accessibility-for-dm-viewers}

Tudo pronto para uso [!DNL Dynamic Media] os componentes de visualizadores suportam a acessibilidade do teclado para os clientes.

Consulte [Acessibilidade e navegação pelo teclado](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) no Guia de referência de visualizadores do Dynamic Media.

## Suporte de tecnologia assistiva no [!DNL Dynamic Media] visualizador {#assistive-technology-support-for-dm-viewers}

Todos [!DNL Dynamic Media] Os componentes do visualizador são compatíveis com funções e atributos ARIA (Accessible Rich Internet Applications) para melhorar a integração com tecnologias assistivas, como leitores de tela.
Consulte a **Suporte de tecnologia assistiva** Tópico de ajuda em qualquer tópico de personalização do visualizador no Guia de referência do Dynamic Media Viewers. Por exemplo, consulte [Suporte de tecnologia assistiva](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) para o visualizador de vídeo ou [Suporte de tecnologia assistiva](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) para o visualizador de imagem interativa.

## Suporte a legendas ocultas no Dynamic Media {#closed-caption-support}

O Dynamic Media é compatível com a entrega de vídeos e conjuntos de vídeos adaptáveis com legendas ocultas. As legendas devem ser exibidas sobre o conteúdo do vídeo.

Consulte [Vídeo no Dynamic Media - Adicionar legendas ocultas ou legendas ao vídeo](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Acessibilidade para soluções Adobe](https://www.adobe.com/accessibility.html)
>* [Acessibilidade no  [!DNL Experience Manager Assets]](/help/assets/accessibility.md)
