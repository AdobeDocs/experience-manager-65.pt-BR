---
title: Formatos de arquivo suportados e tipos MIME
description: Formatos de arquivo e tipos MIME suportados por [!DNL Assets] and [!DNL Dynamic Media] e os recursos suportados para cada formato.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Gerenciamento de ativos,Representações
exl-id: a4bcf67b-54f4-4681-9e42-fd4753acde1a
source-git-commit: f0a0ea53675afa16463a3cf863257020ba5374d3
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 10%

---

# Formatos suportados em [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] O suporta uma grande variedade de formatos de arquivo e cada funcionalidade tem suporte variado para diferentes tipos MIME. Para integrar [!DNL Assets] a outras soluções de gerenciamento de ativos digitais (DAM) compatíveis com os padrões e software de desktop, use Adobe [!DNL Extensible Metadata Platform] (XMP).

Use a legenda para entender o nível de suporte.

| Nível de suporte | Descrição |
| :-----------: | ------------------------------ |
| Instantâneo | Compatível |
| * | Suportado com recursos complementares |
| - | Não aplicável |

## Formatos de imagem rasterizada compatíveis em [!DNL Experience Manager] {#supported-raster-image-formats}

Os formatos de imagem rasterizada compatíveis em [!DNL Assets] são:

| Formato | Armazenamento | Gerenciamento de metadados | Extração de metadados | Geração de miniaturas | Edição | Write-back de metadados | Insights |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| GIF | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo |
| TIFF | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo | Instantâneo |
| JPEG | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| BMP | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo |
| PNM | Instantâneo | Instantâneo | - | - | - | - | Instantâneo |
| PGM | Instantâneo | Instantâneo | - | - | - | - | Instantâneo |
| PBM | Instantâneo | Instantâneo | - | - | - | - | Instantâneo |
| PPM | Instantâneo | Instantâneo | - | - | - | - | Instantâneo |
| PSD ‡ | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | - | Instantâneo |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo | - |
| PICT | - | - | - | - | - | - | Instantâneo |
| PSB | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | - | - |

‡ A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada pela Adobe Photoshop e incluída no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

Os formatos de imagem rasterizada compatíveis em [!DNL Dynamic Media] são:

| Formato | Upload<br> (Formato de entrada) | Criar<br> imagem<br> predefinição<br> (Formato de saída) | Visualizar<br> representação dinâmica<br> | Entregar<br> representação dinâmica<br> | Baixar<br> representação dinâmica<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| GIF | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| TIFF | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| JPEG | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| BMP | Instantâneo | - | - | - | - |
| PSD ‡ | Instantâneo | - | - | - | - |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| PICT | Instantâneo | - | - | - | - |

‡ A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada pela Adobe Photoshop e incluída no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

Além das informações acima, considere o seguinte:

* O suporte para arquivos EPS se aplica somente a imagens raster. Por exemplo, a geração de miniaturas para imagens vetoriais EPS não é compatível por padrão. Para adicionar suporte, [configure ImageMagick](best-practices-for-imagemagick.md). Para integrar ferramentas de terceiros para ativar recursos adicionais, consulte [Manipulador de mídia baseado na linha de comando](media-handlers.md#command-line-based-media-handler).

* O write-back de metadados funciona para o formato de arquivo PSB quando é adicionado ao manipulador `NComm`.

* Para usar [!DNL Dynamic Media] para visualizar e gerar representações dinâmicas para arquivos EPS, consulte [Adobe Illustrator (AI), Postscript (EPS) e formatos de arquivo PDF.](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para arquivos EPS, o write-back de metadados é compatível com a versão 3.0 ou posterior da Convenção de Estrutura de Documentos PostScript (PS-Adobe).

## Formatos 3D suportados {#support-3d-formats}

A seguinte lista de formatos 3D é suportada.

Consulte também [Trabalhar com ativos 3D no Dynamic Media.](/help/assets/assets-3d.md)

| Formato | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Visualização de miniatura | Visualização 3D | Delivery Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | Instantâneo | Instantâneo | Instantâneo |  | Instantâneo | Instantâneo | - | - |
| gLB | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo | Instantâneo |
| gLTF | Instantâneo | Instantâneo | Instantâneo |  | Instantâneo | - | Instantâneo | - |
| OBJ | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo | Instantâneo |
| STL | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo | Instantâneo |
| USDz | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | - | Instantâneo |

## Formatos de imagem rasterizada não aceitos no Dynamic Media {#unsupported-image-formats-dynamic-media}

A lista a seguir descreve os subtipos de formatos de arquivo de imagem rasterizada que são *not* suportados no Dynamic Media.

Consulte também [Detectar formatos de arquivo não suportados para Dynamic Media](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html).

* Arquivos PNG com um tamanho de bloco IDAT superior a 100 MB.
* Arquivos PSB.
* Arquivos PSD com um espaço de cor diferente de CMYK, RGB, Escala de cinza ou Bitmap não são compatíveis. Não há suporte para espaços de cores DuoTone, Lab e Indexado.
* Arquivos PSD com uma profundidade de bits superior a 16.
* Arquivos TIFF com dados de ponto flutuante.
* Arquivos TIFF com espaço de cor Lab.

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](http://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Biblioteca PDF rasterizer suportada {#supported-pdf-rasterizer-library}

A biblioteca Adobe PDF Rasterizer gera miniaturas e visualizações de alta qualidade para arquivos PDF e [!DNL Adobe Illustrator] grandes e com uso intenso de conteúdo. O Adobe recomenda usar a biblioteca Rasterizer de PDF para o seguinte:

* Arquivos AI/PDF com uso intenso de conteúdo que consomem muitos recursos para serem processados.
* Arquivos AI/PDF, para os quais as miniaturas não são geradas por padrão.
* Arquivos AI com cores Pantone Matching System (PMS).

Consulte [Usando o PDF Rasterizer](aem-pdf-rasterizer.md).

## Biblioteca de transcodificação de imagem suportada {#supported-image-transcoding-library}

A biblioteca de transcodificação de imagem do Adobe é uma solução de processamento de imagens que executa funções essenciais de manipulação de imagens, como codificação, transcodificação, redefinição de amostra e redimensionamento.

A biblioteca de transcodificação de imagens oferece suporte a JPG/JPEG, PNG (8 e 16 bits), GIF, BMP, TIFF/Compressed TIFF (exceto arquivos TIFF de 32 bits e arquivos PTIFF), ICO e ICN MIME.

Consulte [Biblioteca de transcodificação de imagem](imaging-transcoding-library.md).

## Camera Raw suportado {#supported-camera-raw}

A biblioteca [!DNL Adobe Camera Raw] permite [!DNL Assets] assimilar imagens brutas. Consulte [Suporte Camera Raw](camera-raw.md).

## Formatos de documento [!DNL Assets] suportados {#supported-document-formats}

Os formatos de documento compatíveis com os recursos de gerenciamento de ativos são os seguintes:

| Formato | Armazenamento | [Gerenciamento de metadados](metadata.md) | Extração de texto completo<br> | [Extração de metadados](metadata.md) | Geração de miniatura<br> | [Extração de subconjunto](managing-linked-subassets.md) | [Write-back de metadados](xmp-writeback.md) | [Connected Assets](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | Instantâneo | Instantâneo | - | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - |
| DOC | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | - | - | Instantâneo |
| DOCX | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | - | - | Instantâneo |
| ODT | Instantâneo | Instantâneo | Instantâneo | - | - | - | - | Instantâneo |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| HTML | Instantâneo | Instantâneo | Instantâneo | - | - | - | - | Instantâneo |
| RTF | Instantâneo | Instantâneo | Instantâneo | - | - | - | - | Instantâneo |
| TXT | Instantâneo | Instantâneo | Instantâneo | - | - | - | - | Instantâneo |
| XLS | Instantâneo | Instantâneo | Instantâneo | - | - | - | - | Instantâneo |
| XLSX | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | - | - | Instantâneo |
| ODS | Instantâneo | Instantâneo | Instantâneo | - | - | - | - | - |
| PPT | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo |
| PPTX | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - | Instantâneo |
| ODP | Instantâneo | Instantâneo | Instantâneo | - | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | Instantâneo | Instantâneo | - | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - |
| PS | Instantâneo | Instantâneo | - | - | - | - | - | - |
| QXP | Instantâneo | Instantâneo | - | - | - | - | - | - |
| EPUB | Instantâneo | Instantâneo | - | Instantâneo | Instantâneo | - | - | - |

## Formatos de documento compatíveis no Dynamic Media {#supported-document-formats-dynamic-media}

| Formato | Upload<br> (Formato de entrada) | Criar<br> imagem<br> predefinição<br> (Formato de saída) | Visualizar<br> representação dinâmica<br> | Entregar<br> representação dinâmica<br> | Baixar<br> representação dinâmica<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | Instantâneo | - | - | - | - |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | Instantâneo | - | - | - | - |

Além da funcionalidade acima, considere o seguinte:

* Para usar o Dynamic Media para gerar representações dinâmicas para arquivos PDF, consulte [Adobe Illustrator (AI), Postscript (EPS) e formatos de arquivo PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para usar o Dynamic Media para visualizar e gerar representações dinâmicas para arquivos AI, consulte [Adobe Illustrator (AI), Postscript (EPS) e formatos de arquivo PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para usar o Dynamic Media para gerar representações dinâmicas para arquivos INDD, consulte [InDesign (INDD) file format](../assets/managing-image-presets.md#indesign-indd-file-format).

## Formatos multimídia compatíveis {#supported-multimedia-formats}

|  | Armazenamento | Gerenciamento de metadados | Extração de metadados | Geração de miniaturas | Transcodificação de FFmpeg |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | Instantâneo | Instantâneo | - | - | * |
| MIDI | Instantâneo | Instantâneo | - | - | * |
| 3GP | Instantâneo | Instantâneo | - | - | * |
| MP3 | Instantâneo | Instantâneo | Instantâneo | - | * |
| MPG | Instantâneo | Instantâneo | - | - | * |
| OGA | Instantâneo | Instantâneo | - | - | * |
| OGG | Instantâneo | Instantâneo | - | - | * |
| ARM | Instantâneo | Instantâneo | - | - | * |
| WAV | Instantâneo | Instantâneo | - | - | * |
| WMA | Instantâneo | Instantâneo | - | - | * |
| DVI | Instantâneo | Instantâneo | - | * | * |
| FLV | Instantâneo | Instantâneo | - | * | * |
| M4V | Instantâneo | Instantâneo | - | * | * |
| MPEG | Instantâneo | Instantâneo | - | * | * |
| OGV | Instantâneo | Instantâneo | - | * | * |
| MOV | Instantâneo | Instantâneo | - | * | * |
| WMV | Instantâneo | Instantâneo | - | * | * |
| SWF | Instantâneo | Instantâneo | - | - | - |

## Formatos de vídeo de entrada suportados no Dynamic Media para transcodificação {#supported-input-video-formats-for-dynamic-media-transcoding}

| Extensão de arquivo de vídeo | Container | Codecs de vídeo recomendados | Codecs de vídeo não suportados |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC (todos os perfis) | - |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediário, Animação da Apple |
| FLV, F4V | Flash Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (arquivos de animação vetorial) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft® Screen (MSS2), Microsoft® Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | - |
| M4V | Apple iTunes | H264/AVC | - |
| AVI | Intercalação A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft® Video 1 (MS-CRAM) |
| WebM | WebM | VP8 do Google | - |
| OGV, OGG | Ogg | Theora, VP3, Dirac | - |
| MKV | Matroska | H264/AVC | - |
| RAM, RM | RealVideo | Não suportado | G2 real (RV20), Real 8 (RV30), Real 10 (RV40) |
| MJ2 | Motion JPEG 2000 | Codec Motion JPEG 2000 | - |

## Formatos de arquivo compatíveis {#supported-archive-formats}

Os formatos de arquivamento compatíveis e a aplicabilidade dos workflows comuns do DAM são abordados na tabela a seguir.

| Formatos | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Entrega do Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - |
| JAR | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - |
| RAR | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - |
| TAR | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - |
| ZIP | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |

## Outros formatos compatíveis {#other-supported-formats}

A aplicabilidade das funcionalidades usuais do DAM para alguns formatos de arquivo específicos está descrita abaixo.

| Formatos | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Entrega do Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - |
| CSS | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| VTT | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| XML | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo | Instantâneo |
| JavaScript (quando configurado com o próprio domínio de delivery) | - | - | - | - | - | Instantâneo |

>[!NOTE]
>
>O upload e a distribuição de arquivos JavaScript podem ou não ser seguros. Se necessário, é possível usar as sobreposições para impedir que os usuários carreguem arquivos JS.

## Tipos MIME suportados {#supported-mime-types}

Por padrão, [!DNL Experience Manager] detecta o tipo de arquivo usando a extensão de arquivo. [!DNL Experience Manager] O pode detectá-lo do conteúdo dos arquivos. Para o último, selecione a opção [!UICONTROL Detectar MIME do conteúdo] em [!UICONTROL Day CQ DAM Mime Type Service] no [!DNL Experience Manager] Console da Web.

Uma lista de tipos MIME suportados está disponível no CRXDE Lite em `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| Extensão de arquivo | Tipo MIME/tipo de mídia da Internet | Valor padrão de jobParam | Valor jobParam permitido |
|---|---|---|---|
| Imagem | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | O jobParam padrão se aplica a todos os ativos de tipo MIME de imagem.<ul><li>[nockoutBackgroundOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options.html)</li><li>[manualCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options.html)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options.html)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options.html)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options.html)</li><li>[emailSetting](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings.html)</li><li>[xmpKeywords](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords.html)</li><li>[unsharMaskOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options.html)</li></ul> |
| 3G2 | vídeo/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| 3GP | vídeo/3gpp |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li> [ilustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
| AIFF | áudio/x-aiff |  |  |
| AVI | vídeo/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| M4V | vídeo/x-m4v |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPEG | vídeo/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MPG | vídeo/mpeg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options.html) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[ilustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options.html)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | vídeo/dvd |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-exclude-master-video-from-avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [Habilite o suporte](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support) a parâmetros de trabalho de upload do Dynamic Media Classic e ativos baseados em tipo MIME.
>* [Configure o tipo MIME baseado no suporte para carregar parâmetros de trabalho](config-dynamic.md).

