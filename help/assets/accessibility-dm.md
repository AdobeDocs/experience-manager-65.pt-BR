---
title: Acessibilidade no Dynamic Media
description: Saiba mais sobre o suporte de acessibilidade no Dynamic Media e em Visualizadores do Dynamic Media.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: User, Admin
exl-id: bbdb800c-b6f8-4506-b8ac-daf64edcd6c0
solution: Experience Manager, Experience Manager Assets
autotag-review: '2026-05-18T18:39:42.457Z'
TQID: 'https://experienceleague.adobe.com/f9-0rO4QHX7kbx7xwptmuOW1W7WzduM3tOlL2YgHXxI'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: cc72dcf1-72e1-48cc-b434-e7c27d62d67c
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 647
ht-degree: 0%

---

# Acessibilidade em [!DNL Dynamic Media] {#working-with-three-d-assets-dm}

O [!DNL Dynamic Media] oferece suporte ao controle de teclado e às tecnologias assistivas, como leitores de tela JAWS e NVDA, na interface do usuário de criação.

## Suporte para acessibilidade do teclado no [!DNL Dynamic Media]

Como [!DNL Dynamic Media] é um plug-in para [!DNL Adobe Experience Manager Assets], a maioria do comportamento de controle do teclado é igual ao de [!DNL Experience Manager Assets]. Por exemplo, o botão `Cancel` em [!DNL Dynamic Media] tem o mesmo destaque de foco que em [!DNL Experience Manager Assets] e reage à tecla `Spacebar` como em [!DNL Experience Manager Assets]. Consulte [Atalhos de teclado no Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Os pressionamentos de tecla suportados por elementos individuais da interface do usuário no [!DNL Dynamic Media] são claros e fáceis de descobrir. O controle do teclado em [!DNL Dynamic Media] é sobre o seguinte:

* Capacidade de usar as teclas `Tab` e `Shift+Tab` para navegar entre elementos interativos na página.
O uso de `Tab` avança o foco de entrada para o próximo elemento da interface do usuário na ordem de tabulação; o uso de `Shift+Tab` traz o foco de entrada de volta para o elemento da interface do usuário anterior.
O percurso do foco segue o local natural do elemento da interface do usuário na tela e se move da esquerda para a direita e de cima para baixo. Além disso, se qualquer campo tiver um erro, você pode pressionar `Tab` para mover o foco para ele.
* Capacidade de usar as teclas `Spacebar` e `Enter` para ativar elementos padrão da interface do usuário, como botões e listas suspensas.
* Capacidade de ver o foco do teclado destacado no elemento ativo. O elemento da interface do usuário que tem foco de entrada recebe uma indicação de foco visual como uma borda renderizada ao redor do elemento da interface do usuário.
* No editor de ponto de acesso, é possível usar alguns pressionamentos de tecla personalizados, como teclas de seta, para interagir com elementos complexos da interface do usuário e reposicionar pontos de acesso.
* No editor de Vídeo Interativo, você pode usar o `Spacebar` para selecionar uma imagem e adicioná-la a um segmento. Além disso, você pode usar a chave `Backspace` para excluir o item selecionado da guia **[!UICONTROL Conteúdo]**. Além disso, pressionar `Tab` funções conforme desejado para navegar entre elementos interativos na página.
* No editor de Recorte de imagem/Recorte inteligente, você pode fazer o seguinte:
   * Use as teclas de seta para recortar o tamanho do quadro ou reposicionar a imagem, ou ambos.
   * A primeira parada de `Tab` realça o quadro de imagem inteiro. Em seguida, é possível usar as teclas de seta no teclado para reposicionar o quadro.
   * As próximas quatro `Tab` paradas são os quatro cantos do quadro. Quando o foco é colocado em um canto do quadro, o canto é realçado. Novamente, você pode usar as teclas de seta no teclado para mover o canto focalizado.
Consulte [Editar o recorte inteligente ou a amostra inteligente de uma única imagem](/help/assets/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Suporte de tecnologia assistiva no [!DNL Dynamic Media] {#assistive-technology-support-for-dm}

[!DNL Dynamic Media] elementos da interface de usuário funcionam com tecnologias assistivas, como leitores de tela. Por exemplo, ela reconhece pontos de referência em uma página quando você navega em pontos de referência usando o atalho de teclado `D` ou regiões usando o atalho de teclado `R`. Ele também narra o cabeçalho ao navegar usando o atalho de teclado de cabeçalho `H`.

## Suporte para acessibilidade do teclado em [!DNL Dynamic Media] visualizadores {#keyboard-accessibility-for-dm-viewers}

Todos os componentes de visualizadores do [!DNL Dynamic Media] prontos para uso oferecem suporte à acessibilidade do teclado para seus clientes.

Consulte [Acessibilidade e navegação do teclado](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html?lang=pt-BR) no Guia de Referência de Visualizadores do Dynamic Media.

## Suporte de tecnologia assistiva em [!DNL Dynamic Media] visualizadores {#assistive-technology-support-for-dm-viewers}

Todos os componentes do visualizador [!DNL Dynamic Media] oferecem suporte a funções e atributos ARIA (Accessible Rich Internet Applications) para melhorar a integração com tecnologias assistivas, como leitores de tela.
Consulte o tópico de Ajuda **Suporte à tecnologia assistiva** em qualquer tópico de personalização do visualizador no Guia de referência do visualizador do Dynamic Media. Por exemplo, consulte o [Suporte de tecnologia assistiva](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html?lang=pt-BR) para o visualizador de vídeo ou o [Suporte de tecnologia assistiva](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=pt-BR#viewers-for-aem-assets-only) para o visualizador de imagem interativa.

## Suporte a legendas ocultas no Dynamic Media {#closed-caption-support}

O Dynamic Media é compatível com a entrega de vídeos e conjuntos de vídeos adaptáveis com legendas ocultas. As legendas devem ser exibidas sobre o conteúdo do vídeo.

Consulte [Vídeo no Dynamic Media - Adicionar legendas ocultas ao vídeo](/help/assets/video.md#adding-captions-to-video).

>[!MORELIKETHIS]
>
>* [Acessibilidade para soluções da Adobe](https://www.adobe.com/accessibility.html)
>* [Acessibilidade em [!DNL Experience Manager Assets]](/help/assets/accessibility.md)
