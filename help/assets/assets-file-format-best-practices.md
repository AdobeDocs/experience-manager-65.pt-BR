---
title: Práticas recomendadas para processar os vários formatos de arquivo suportados usando o [!DNL Adobe Experience Manager Assets].
description: Práticas recomendadas para processar os vários tipos de arquivos suportados usando o [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5f67b4e5ccd5d7e982732e449050123e917c9914

---


# Assets file format best practices {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] oferece suporte a várias bibliotecas proprietárias e de arquivos de terceiros para atender aos diversos requisitos de suporte de arquivos dos usuários. As bibliotecas da Adobe suportadas incluem, [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer e [!DNL Adobe InDesign Server]. Além disso, [!DNL Experience Manager Assets] suporta bibliotecas de terceiros, incluindo [!DNL ImageMagick], [!DNL TwelveMonkeys]etc.

For the supported file formats, see [Assets supported formats](/help/assets/assets-formats.md).

>[!TIP]
>
>Se você estiver usando [!DNL Experience Manager] o Adobe Managed Services (AMS), entre em contato com o Atendimento ao cliente da Adobe se planeja processar muitos arquivos grandes PSD ou PSB. Entre em contato com o representante do Atendimento ao cliente da Adobe para implementar essas práticas recomendadas para sua implantação do AMS e escolher as melhores ferramentas e modelos possíveis para os formatos proprietários da Adobe. [!DNL Experience Manager] pode não processar arquivos PSB de alta resolução com mais de 30000 x 23000 pixels.

## [!DNL Adobe Camera Raw] biblioteca {#adobe-camera-raw-library}

Para obter o melhor desempenho, a Adobe recomenda usar a [!DNL Adobe Camera Raw] biblioteca para arquivos RAW e DNG.

[!DNL Adobe Camera Raw] biblioteca suporta perfil de cores CMYK como entrada. No entanto, ele gera a saída no espaço de cores RGB e suporta a saída somente no formato JPEG. Ele não retém o espaço de cores do arquivo de origem (por exemplo, CMYK) nas miniaturas.

Para obter mais informações, consulte Suporte ao [Camera Raw](/help/assets/camera-raw.md).

## Biblioteca do Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Para obter melhores resultados, a Adobe recomenda usar a biblioteca do Adobe PDF Rasterizer para os seguintes arquivos:

* Arquivos PDF pesados e com conteúdo intenso
* Arquivos AI com miniaturas não gerados na caixa
* Para arquivos AI com cores SPOT (PMS)

As miniaturas e pré-visualizações geradas usando o PDF Rasterizer têm melhor qualidade em comparação à saída rasterizada predefinida. A biblioteca do Adobe PDF Rasterizer não suporta nenhuma conversão de espaço de cores. Independentemente do espaço de cores do arquivo PDF de origem, o Adobe PDF Rasterizer gera apenas saída RGB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

A Adobe recomenda usar [!DNL Adobe InDesign Server] para extrair execuções [!DNL Adobe InDesign]específicas, como IDML e HTML. Para obter mais informações, consulte [Adicionar ativos do Experience Manager como referências no Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media]  {#dynamic-media}

[!DNL Dynamic Media] gera e oferece várias variações de conteúdo rico em tempo real por meio de sua rede global, escalável e otimizada para desempenho. Ele proporciona experiências de visualização interativas e simplifica o processo de gestão de campanha digital. Para obter detalhes sobre a ativação, consulte [!DNL Dynamic Media]Configuração do Dynamic Media [](/help/assets/config-dynamic.md).

Atualmente, [!DNL Dynamic Media] é possível oferecer suporte a vídeos com até 15 GB de conteúdo por arquivo.

## Biblioteca ImageMagick {#imagemagick-library}

A Adobe recomenda usar a biblioteca ImageMagick nos seguintes cenários:

* Para gerar renderizações em miniatura para arquivos EPS.
* Para preservar as informações do perfil da imagem.
* Para preservar a transparência.
* Para processar arquivos PSD e PSB.

Para saber como configurar a [!DNL ImageMagick] biblioteca em [!DNL Experience Manager], consulte [Uso do ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Para obter o uso ideal, consulte Práticas [recomendadas para configurar o ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Biblioteca de transcodificação de imagens {#image-transcoding-library}

A Biblioteca de transcodificação de imagens da Adobe é uma solução de processamento de imagens que executa funções essenciais de manipulação de imagens, incluindo codificação de imagens, transcodificação, nova amostragem, redimensionamento e assim por diante.

A Biblioteca de transcodificação de imagens suporta os seguintes tipos MIME:

* JPG/JPEG
* PNG (8 bits e 16 bits)
* GIF
* BMP
* TIFF/TIFF compactado (exceto Tiffs de 32 bits e PTiffs).
* ICO
* ICN

Para obter detalhes, consulte Biblioteca [de transcodificação de](/help/assets/imaging-transcoding-library.md)imagens.
