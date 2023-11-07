---
title: Práticas recomendadas para processar os formatos de arquivo compatíveis
description: Práticas recomendadas para processar os vários tipos de arquivos compatíveis usando o [!DNL Experience Manager Assets].
contentOwner: AG
role: Admin
feature: Asset Management,Developer Tools
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 3%

---

# Práticas recomendadas de formato de arquivo de ativos {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] O oferece suporte a muitas bibliotecas de formato de arquivo proprietárias e de terceiros para atender aos diversos requisitos de suporte de arquivos dos usuários. As bibliotecas de Adobe compatíveis incluem, [!DNL Adobe Camera Raw], Gibson, Adobe PDF Rasterizer e [!DNL Adobe InDesign Server]. Além disso, [!DNL Experience Manager Assets] O é compatível com bibliotecas de terceiros, incluindo [!DNL ImageMagick], [!DNL TwelveMonkeys]e assim por diante.

Para obter os formatos de arquivo compatíveis, consulte [Formatos de ativos compatíveis](/help/assets/assets-formats.md).

>[!TIP]
>
>Se você estiver usando [!DNL Experience Manager] no Adobe Managed Services (AMS), entre em contato com o Suporte ao cliente do Adobe se planejar processar muitos arquivos PSD ou PSB grandes. Trabalhe com o representante do Suporte ao cliente da Adobe para implementar essas práticas recomendadas para a implantação do AMS e escolher as melhores ferramentas e modelos possíveis para os formatos proprietários do Adobe. [!DNL Experience Manager]O pode não processar arquivos PSB de resolução muito alta com mais de 30.000 x 23.000 pixels. 

## [!DNL Adobe Camera Raw] biblioteca {#adobe-camera-raw-library}

Para obter o desempenho ideal, o Adobe recomenda o uso de [!DNL Adobe Camera Raw] para arquivos RAW e DNG.

[!DNL Adobe Camera Raw] A biblioteca é compatível com o perfil de cores CMYK como entrada. No entanto, gera a saída no espaço de cores RGB e suporta a saída apenas no formato JPEG. Ele não retém o espaço de cores do arquivo de origem (por exemplo, CMYK) nas miniaturas.

Para obter mais informações, consulte [Suporte Camera Raw](/help/assets/camera-raw.md).

## Biblioteca do Adobe PDF Rasterizer {#adobe-pdf-rasterizer-library}

Para obter melhores resultados, a Adobe recomenda o uso da biblioteca Adobe PDF Rasterizer para os seguintes arquivos:

* Arquivos PDF pesados e de conteúdo intenso
* Arquivos de IA com miniaturas não gerados imediatamente
* Para arquivos AI com cores SPOT (PMS)

Miniaturas e visualizações geradas usando o PDF Rasterizer têm melhor qualidade em comparação à saída de rasterização pronta para uso. A biblioteca do Adobe PDF Rasterizer não suporta nenhuma conversão de espaço de cores. Independentemente do espaço de cores do arquivo de PDF de origem, o Adobe PDF Rasterizer gera apenas a saída de RGB.

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

O Adobe recomenda usar [!DNL Adobe InDesign Server] para extrair [!DNL Adobe InDesign]representações específicas do, como IDML e HTML. Para obter mais informações, consulte [Adicionar ativos Experience Manager como referências no Adobe InDesign](/help/assets/managing-linked-subassets.md#refai).

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] gera e fornece várias variações de conteúdo avançado em tempo real por meio de sua rede global, dimensionável e otimizada para desempenho. Ele fornece experiências de visualização interativa e simplifica o processo de gerenciamento de campanhas digitais. Para obter detalhes sobre como ativar [!DNL Dynamic Media], consulte [Configuração do Dynamic Media](/help/assets/config-dynamic.md).

Atualmente, [!DNL Dynamic Media] O pode aceitar vídeos com até 15 GB de conteúdo por arquivo.

## Biblioteca ImageMagick {#imagemagick-library}

A Adobe recomenda usar a biblioteca ImageMagick nos seguintes cenários:

* Para gerar representações em miniatura de arquivos do EPS.
* Para preservar as informações do perfil de imagem.
* Para preservar a transparência.
* Para processar arquivos PSD e PSB.

Para saber como configurar o [!DNL ImageMagick] biblioteca em [!DNL Experience Manager], consulte [Utilização do ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick). Para obter o uso ideal, consulte [Práticas recomendadas para a configuração do ImageMagick](/help/assets/best-practices-for-imagemagick.md).

## Biblioteca de transcodificação de imagens {#image-transcoding-library}

A Biblioteca de transcodificação de imagens do Adobe é uma solução de processamento de imagens que executa funções principais de tratamento de imagens, incluindo codificação de imagens, transcodificação, reamostragem, redimensionamento e assim por diante.

A Biblioteca de Transcodificação de Imagens é compatível com os seguintes tipos MIME:

* JPG/JPEG
* PNG (8 e 16 bits)
* GIF
* BMP
* TIFF/TIFF compactado (exceto Tiffs de 32 bits e PTiffs).
* ICO
* ICN

Para obter detalhes, consulte [Biblioteca de transcodificação de imagem](/help/assets/imaging-transcoding-library.md).
