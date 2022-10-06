---
title: Trabalhar com o Dynamic Media
description: Saiba como usar o Dynamic Media para fornecer ativos para consumo na Web, em dispositivos móveis e em sites sociais.
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaboration,Asset Management
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 13%

---

# Trabalhar com o Dynamic Media {#working-with-dynamic-media}

O [Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) ajuda a fornecer ativos de marketing e merchandising visual por demanda, automaticamente dimensionados para o consumo na Web, em dispositivos móveis e sites sociais. Usando um conjunto de ativos de origem primária, a Dynamic Media gera e fornece várias variações de conteúdo rico em tempo real por meio de sua rede global, escalável e otimizada para desempenho.

O Dynamic Media fornece experiências de visualização interativas, incluindo zoom, rotação de 360 graus e vídeo. O Dynamic Media incorpora exclusivamente os fluxos de trabalho da solução de gerenciamento de ativos digitais (Assets) da Adobe Experience Manager para simplificar e simplificar o processo de gerenciamento de campanhas digitais.

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## O que você pode fazer com o Dynamic Media {#what-you-can-do-with-dynamic-media}

O Dynamic Media permite gerenciar seus ativos antes de publicá-los. Como trabalhar com ativos em geral é abordado detalhadamente em [Trabalhar com ativos digitais](manage-assets.md). Os tópicos gerais incluem upload, download, edição e publicação de ativos; visualizar e editar propriedades e procurar ativos.

Os recursos exclusivos ao Dynamic Media incluem o seguinte:

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
>Para entender as diferenças entre usar o Dynamic Media e integrar o Dynamic Media Classic ao Adobe Experience Manager, consulte [Integração do Dynamic Media Classic versus Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamic Media ativado versus Dynamic Media desativado {#dynamic-media-on-versus-dynamic-media-off}

É possível saber se o Dynamic Media está ativado (ativado) pelas seguintes características:

* As representações dinâmicas estão disponíveis ao baixar ou visualizar ativos.
* Conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista estão disponíveis.
* As representações PTIFF são criadas.

Quando você seleciona um ativo de imagem, a exibição do ativo é diferente com a Dynamic Media [ativado](config-dynamic.md#enabling-dynamic-media). O Dynamic Media usa os visualizadores HTML5 sob demanda.

### Representações dinâmicas {#dynamic-renditions}

Representações dinâmicas, como predefinições de imagem e do visualizador (em **[!UICONTROL Dinâmico]**) estão disponíveis quando o Dynamic Media está ativado.

![chlimage_1-358](assets/chlimage_1-358.png)

### Conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista {#image-sets-spins-sets-mixed-media-sets}

Conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista estarão disponíveis se o Dynamic Media estiver ativado.

![chlimage_1-359](assets/chlimage_1-359.png)

### Representações PTIFF {#ptiff-renditions}

Os ativos habilitados para a Dynamic Media incluem `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Alteração nas exibições de ativos {#asset-views-change}

Com o Dynamic Media ativado, é possível ampliar e diminuir o zoom clicando no botão `+` e `-` botões. Também é possível clicar/tocar para ampliar determinadas áreas. Reverter o traz para a versão original e você pode fazer a imagem em tela cheia clicando nas setas diagonais. O Dynamic Media ativado tem esta aparência:

![chlimage_1-361](assets/chlimage_1-361.png)

Com o Dynamic Media desativado, é possível ampliar e diminuir o zoom e reverter para o tamanho original:

![chlimage_1-362](assets/chlimage_1-362.png)
