---
title: Práticas recomendadas para processar os formatos de arquivo compatíveis
description: Práticas recomendadas para processar os vários tipos de arquivo com suporte usando [!DNL Experience Manager Assets].
contentOwner: AG
role: Administrator
feature: Asset Management,Developer Tools
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# Práticas recomendadas de formato de arquivo de ativos {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] O suporta muitas bibliotecas de formatos de arquivo proprietárias e de terceiros para atender a diversos requisitos de suporte de arquivos dos usuários. As bibliotecas Adobe compatíveis incluem, [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer e [!DNL Adobe InDesign Server]. Além disso, [!DNL Experience Manager Assets] suporta bibliotecas de terceiros, incluindo [!DNL ImageMagick], [!DNL TwelveMonkeys] e assim por diante.

Para os formatos de arquivo compatíveis, consulte [Formatos compatíveis com ativos](/help/assets/assets-formats.md).

>[!TIP]
>
>Se estiver usando [!DNL Experience Manager] no Adobe Managed Services (AMS), entre em contato com o Atendimento ao cliente do Adobe se planeja processar muitos arquivos grandes de PSD ou PSB. Trabalhe com o representante do Atendimento ao cliente do Adobe para implementar essas práticas recomendadas para a implantação do AMS e escolher as melhores ferramentas e modelos possíveis para os formatos proprietários do Adobe. [!DNL Experience Manager] pode não processar arquivos PSB de alta resolução que tenham mais de 30000 x 23000 pixels.

## [!DNL Adobe Camera Raw] biblioteca  {#adobe-camera-raw-library}

Para obter o melhor desempenho, o Adobe recomenda usar a biblioteca [!DNL Adobe Camera Raw] para arquivos RAW e DNG.

[!DNL Adobe Camera Raw] A biblioteca oferece suporte ao perfil de cores CMYK como entrada. No entanto, ele gera a saída no espaço de cores RGB e suporta a saída somente no formato JPEG. Ele não retém o espaço de cores do arquivo de origem (por exemplo, CMYK) nas miniaturas.

Para obter mais informações, consulte [Suporte Camera Raw](/help/assets/camera-raw.md).

## Biblioteca do Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Para obter melhores resultados, o Adobe recomenda usar a biblioteca Adobe PDF Rasterizer para os seguintes arquivos:

* Arquivos PDF pesados e com uso intenso de conteúdo
* Arquivos AI com miniaturas não gerados imediatamente
* Para arquivos AI com cores SPOT (PMS)

Miniaturas e visualizações geradas usando o PDF Rasterizer têm melhor qualidade em comparação à saída rasterizada predefinida. A biblioteca Adobe PDF Rasterizer não oferece suporte a nenhuma conversão de espaço de cores. Independentemente do espaço de cores do arquivo PDF de origem, o Adobe PDF Rasterizer gera somente saída RGB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

O Adobe recomenda usar [!DNL Adobe InDesign Server] para extrair renderizações específicas de [!DNL Adobe InDesign], como IDML e HTML. Para obter mais informações, consulte [Adicionar ativos Experience Manager como referências no Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] O gera e oferece várias variações de conteúdo rico em tempo real por meio de sua rede global, escalável e otimizada para desempenho. Ele fornece experiências de visualização interativas e simplifica o processo de gerenciamento de campanhas digitais. Para obter detalhes sobre como habilitar [!DNL Dynamic Media], consulte [Configuração do Dynamic Media](/help/assets/config-dynamic.md).

Atualmente, [!DNL Dynamic Media] pode oferecer suporte a vídeos de até 15 GB de conteúdo por arquivo.

## Biblioteca ImageMagick {#imagemagick-library}

O Adobe recomenda usar a biblioteca ImageMagick nos seguintes cenários:

* Para gerar representações em miniatura de arquivos EPS.
* Para preservar as informações do perfil da imagem.
* Preservar transparência.
* Para processar arquivos PSD e PSB.

Para saber como configurar a biblioteca [!DNL ImageMagick] em [!DNL Experience Manager], consulte [Usando o ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Para obter um uso ideal, consulte [Práticas recomendadas para configurar o ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Biblioteca de transcodificação de imagem {#image-transcoding-library}

A Adobe Imaging Transcoding Library é uma solução de processamento de imagens que executa funções essenciais de manipulação de imagens, incluindo codificação de imagens, transcodificação, re-amostragem, redimensionamento e assim por diante.

A Biblioteca de transcodificação de imagens oferece suporte aos seguintes tipos MIME:

* JPG/JPEG
* PNG (8 bits e 16 bits)
* GIF
* BMP
* TIFF/TIFF compactado (exceto os Tiffs de 32 bits e os PTiffs).
* ICO
* ICN

Para obter detalhes, consulte [Biblioteca de transcodificação de imagem](/help/assets/imaging-transcoding-library.md).
