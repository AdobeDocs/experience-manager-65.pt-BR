---
title: Trabalhar com o Dynamic Media
description: Saiba como usar o Dynamic Media para fornecer ativos para consumo na Web, em dispositivos móveis e em sites sociais.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaboration,Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 7%

---

# Trabalhar com o Dynamic Media {#working-with-dynamic-media}

O [Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) ajuda a fornecer ativos avançados de marketing e merchandising visual sob demanda, dimensionados automaticamente para consumo em sites da Web, móveis e sociais. Usando um conjunto de ativos de origem primária, a Dynamic Media gera e fornece várias variações de conteúdo avançado em tempo real por meio de sua rede global, dimensionável e com desempenho otimizado.

O Dynamic Media oferece experiências de visualização interativa, incluindo zoom, rotação de 360 graus e vídeo. A Dynamic Media incorpora exclusivamente os fluxos de trabalho da solução Adobe Experience Manager digital asset management (Assets) para simplificar e simplificar o processo de gerenciamento de campanhas digitais.

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## O que você pode fazer com o Dynamic Media {#what-you-can-do-with-dynamic-media}

O Dynamic Media permite gerenciar os ativos antes de publicá-los. Como trabalhar com ativos em geral é abordado em detalhes em [Trabalhar com ativos digitais](manage-assets.md). Os tópicos gerais incluem upload, download, edição e publicação de ativos, visualização e edição de propriedades e pesquisa de ativos.

Os recursos exclusivos do Dynamic Media incluem o seguinte:

* [Banners em carrossel](carousel-banners.md)
* [Conjuntos de imagem](image-sets.md)
* [Imagens interativas](interactive-images.md)
* [Vídeos interativos](interactive-videos.md)
* [Conjuntos de mídia mista](mixed-media-sets.md)
* [Imagens panorâmicas](panoramic-images.md)

* [Conjuntos de rotação](spin-sets.md)
* [Vídeo](video.md)
* [Entregar ativos do Dynamic Media](delivering-dynamic-media-assets.md)
* [Gerenciar ativos](managing-assets.md)
* [Criar pop-ups personalizados usando o Quickview](custom-pop-ups.md)

Consulte também [Configurar Dynamic Media](administering-dynamic-media.md).

>[!NOTE]
>
>Para entender as diferenças entre usar o Dynamic Media e integrar o Dynamic Media Classic com o Adobe Experience Manager, consulte [integração do Dynamic Media Classic versus o Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamic Media ativado versus Dynamic Media desativado {#dynamic-media-on-versus-dynamic-media-off}

Você pode saber se o Dynamic Media está ativado pelas seguintes características:

* As representações dinâmicas estão disponíveis ao baixar ou visualizar ativos.
* Conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista estão disponíveis.
* As representações PTIFF são criadas.

Ao selecionar um ativo de imagem, a exibição do ativo é diferente com o Dynamic Media [habilitado](config-dynamic.md#enabling-dynamic-media). O Dynamic Media usa visualizadores HTML5 sob demanda.

### Representações dinâmicas {#dynamic-renditions}

Representações dinâmicas, como imagens e predefinições do visualizador (em **[!UICONTROL Dynamic]**), estarão disponíveis quando o Dynamic Media for habilitado.

![chlimage_1-358](assets/chlimage_1-358.png)

### Conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista {#image-sets-spins-sets-mixed-media-sets}

Conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista estarão disponíveis se o Dynamic Media estiver ativado.

![chlimage_1-359](assets/chlimage_1-359.png)

### Representações PTIFF {#ptiff-renditions}

Os ativos habilitados para Dynamic Media incluem `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Exibições de ativos alteradas {#asset-views-change}

Com o Dynamic Media habilitado, você pode ampliar e reduzir clicando nos botões `+` e `-`. Você também pode clicar em para aplicar zoom em determinada área. Reverter leva à versão original e você pode tornar a imagem em tela cheia clicando nas setas diagonais. Dynamic Media habilitado tem esta aparência:

![chlimage_1-361](assets/chlimage_1-361.png)

Com o Dynamic Media desativado, você pode aumentar ou diminuir o zoom e reverter para o tamanho original:

![chlimage_1-362](assets/chlimage_1-362.png)
