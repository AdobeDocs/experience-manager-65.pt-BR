---
title: Acessibilidade no Dynamic Media
description: Saiba mais sobre o suporte de acessibilidade no Dynamic Media e no Dynamic Media Viewers.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
source-git-commit: 01de1d5064f5ebf00acd2fe9f138d852f41f7273
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Acessibilidade em [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

[!DNL Dynamic Media] O suporta o controle de teclado e tecnologias de assistência, como leitores de tela JAWS e NVDA, na interface do usuário de criação.

## Suporte à acessibilidade de teclado no [!DNL Dynamic Media]

Porque [!DNL Dynamic Media] é um plug-in para [!DNL Adobe Experience Manager Assets], a maioria do comportamento de controle do teclado é igual ao comportamento do [!DNL Experience Manager Assets]. Por exemplo, a variável `Cancel` botão em [!DNL Dynamic Media] tem o mesmo realce de foco que em [!DNL Experience Manager Assets]e reage à `Spacebar` como em [!DNL Experience Manager Assets]. Consulte [Atalhos de teclado no Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Traços de chaves suportados por elementos individuais da interface do usuário em [!DNL Dynamic Media] são claros e fáceis de descobrir. Controle de teclado em [!DNL Dynamic Media] é sobre o seguinte:

* Capacidade de usar `Tab` e `Shift+Tab` pressionamentos de teclas para navegar entre elementos interativos na página.
Usando `Tab` avança o foco de entrada para o próximo elemento da interface do usuário na ordem de tabulação; usar `Shift+Tab` traz o foco de entrada de volta ao elemento anterior da interface do usuário.
A travessia de foco segue a localização do elemento da interface de usuário natural na tela e se move de esquerda para direita e de cima para baixo. Além disso, se algum campo tiver um erro, você poderá pressionar `Tab` para mover o foco para ele.
* Capacidade de usar o `Spacebar` e `Enter` tecla para ativar elementos padrão da interface do usuário, como botões e listas suspensas.
* Capacidade de ver o foco do teclado realçar no elemento ativo. O elemento da interface do usuário que tem foco de entrada recebe uma indicação de foco visual como uma borda renderizada em torno do elemento da interface do usuário.
* No editor de ponto de acesso, você pode usar alguns pressionamentos de tecla personalizados, como teclas de seta, para interagir com elementos complexos da interface do usuário e reposicionar pontos de acesso.
* No editor de Vídeo interativo, você pode usar o `Spacebar` para selecionar uma imagem e adicioná-la a um segmento. Além disso, você pode usar o `Backspace` chave para excluir o item selecionado da **[!UICONTROL Conteúdo]** guia . Além disso, pressionar `Tab` conforme desejado para navegar entre elementos interativos na página.
* No editor Recortar de imagem/Recorte inteligente, você pode fazer o seguinte:
   * Use as teclas de seta para recortar o tamanho do quadro ou reposicionar a imagem, ou ambos.
   * O primeiro `Tab` a parada realça todo o quadro da imagem. Você pode usar as teclas de seta no teclado para reposicionar o quadro.
   * Os próximos quatro `Tab` as paradas são os quatro cantos do quadro. Quando o foco é colocado em um canto do quadro, o canto é realçado. Novamente, você pode usar as teclas de seta no teclado para mover o canto focado.
Consulte [Editar o recorte inteligente ou a amostra inteligente de uma única imagem](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Suporte à tecnologia assistiva no [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] os elementos da interface do usuário funcionam com tecnologias de assistência, como leitores de tela. Por exemplo, ele reconhece marcos em uma página ao navegar por marcos usando o atalho do teclado `D` ou regiões que usam atalho do teclado `R`. Ele também narra o cabeçalho ao navegar usando o atalho do teclado do cabeçalho `H`.

## Suporte à acessibilidade de teclado no [!DNL Dynamic Media] visualizadores {#keyboard-accessibility-for-dm-viewers}

Tudo pronto para uso [!DNL Dynamic Media] os componentes do visualizador suportam a acessibilidade do teclado para seus clientes.

Consulte [Acessibilidade e navegação do teclado](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) no Guia de referência de visualizadores do Dynamic Media.

## Suporte à tecnologia assistiva no [!DNL Dynamic Media] visualizadores {#assistive-technology-support-for-dm-viewers}

Todos [!DNL Dynamic Media] os componentes do visualizador suportam funções e atributos ARIA (Accessible Rich Internet Applications) para melhorar a integração com tecnologias assistivas, como leitores de tela.
Consulte a **Suporte à tecnologia assistiva** Tópico de Ajuda em qualquer tópico de personalização do visualizador no Guia de Referência de Visualizadores do Dynamic Media. Por exemplo, consulte [Suporte à tecnologia assistiva](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) para o visualizador de vídeo ou [Suporte à tecnologia assistiva](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) para o visualizador de Imagem interativa .

## Suporte a legendas ocultas no Dynamic Media {#closed-caption-support}

O Dynamic Media oferece suporte para vídeos e conjuntos de vídeos adaptáveis com legendas ocultas. As legendas devem ser exibidas sobre o conteúdo do vídeo.

Consulte [Vídeo no Dynamic Media - Adicionar legendas ou legendas ocultas ao vídeo](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Acessibilidade para soluções Adobe](https://www.adobe.com/accessibility.html)
>* [Acessibilidade em [!DNL Experience Manager Assets]](/help/assets/accessibility.md)

