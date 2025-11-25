---
title: Formatos de arquivo e tipos MIME compatíveis
description: Formatos de arquivo e tipos MIME com suporte do  [!DNL Assets] and [!DNL Dynamic Media] e os recursos com suporte para cada formato.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Asset Management,Renditions
exl-id: a4bcf67b-54f4-4681-9e42-fd4753acde1a
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 12%

---

# Formatos com suporte no [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

O [!DNL Experience Manager Assets] oferece suporte a uma grande variedade de formatos de arquivo e cada funcionalidade oferece suporte para diferentes tipos MIME. Para integrar o [!DNL Assets] a outras soluções de gerenciamento de ativos digitais (DAM) e software de desktop compatíveis com os padrões, use o [!DNL Extensible Metadata Platform] (XMP) da Adobe.

Use a legenda para entender o nível de compatibilidade.

| Nível de compatibilidade | Descrição |
| :-----------: | ------------------------------ |
| ✓ | Compatível |
| &#42; | Compatível com recursos complementares |
| − | Não aplicável |

## Formatos de imagem rasterizada com suporte em [!DNL Experience Manager] {#supported-raster-image-formats}

Os formatos de imagem rasterizada com suporte em [!DNL Assets] são:

| Formato | Armazenamento | Gerenciamento de metadados | Extração de metadados | Geração de miniaturas | Edição | Writeback de metadados | Insights |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PNM | ✓ | ✓ | − | − | − | − | ✓ |
| PGM | ✓ | ✓ | − | − | − | − | ✓ |
| PBM | ✓ | ✓ | − | − | − | − | ✓ |
| PPM | ✓ | ✓ | − | − | − | − | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | − | ✓ | − |
| PICT | − | − | − | − | − | − | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | − | − | − |

‡ A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada pelo Adobe Photoshop e incluída no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

Além das informações acima, considere o seguinte:

* O suporte para arquivos EPS se aplica somente a imagens rasterizadas. Por exemplo, a geração de miniaturas para imagens vetoriais do EPS não é compatível por padrão. Para adicionar suporte, [configure o ImageMagick](best-practices-for-imagemagick.md). Para integrar ferramentas de terceiros para habilitar recursos adicionais, consulte [Manipulador de mídia baseado em linha de comando](media-handlers.md#command-line-based-media-handler).

* O write-back de metadados funciona para o formato de arquivo PSB quando ele é adicionado ao manipulador `NComm`.

* Para arquivos EPS, o write-back de metadados é compatível com a PostScript Document Structuring Convention (PS-Adobe) versão 3.0 ou posterior.

## Formatos 3D compatíveis {#support-3d-formats}

A seguinte lista de formatos 3D é compatível.

Consulte também [Trabalhar com ativos 3D no Dynamic Media.](/help/assets/assets-3d.md)

| Formato | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Visualização da miniatura | Visualização 3D | Entrega do Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ | | ✓ | ✓ | − | − |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ | | ✓ | − | ✓ | − |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | − | − | ✓ |

## Biblioteca PDF Rasterizer compatível {#supported-pdf-rasterizer-library}

A biblioteca do Adobe PDF Rasterizer gera miniaturas e visualizações de alta qualidade para arquivos [!DNL Adobe Illustrator] e PDF grandes e de conteúdo intensivo. A Adobe recomenda usar a biblioteca PDF Rasterizer para o seguinte:

* Arquivos AI/PDF de conteúdo intensivo que exigem muitos recursos para serem processados.
* Arquivos AI/PDF, para os quais as miniaturas não são geradas por padrão.
* Arquivos AI com cores do Sistema de correspondência Pantone (PMS).

Consulte [Uso do PDF Rasterizer](aem-pdf-rasterizer.md).

## Biblioteca de transcodificação de imagens suportada {#supported-image-transcoding-library}

A biblioteca de transcodificação de imagens do Adobe é uma solução de processamento de imagens que executa funções principais de tratamento de imagens, como codificação, transcodificação, reamostragem e redimensionamento.

A biblioteca Transcodificação de imagens é compatível com JPG/JPEG, PNG (8 e 16 bits), GIF, BMP, TIFF/Compressed TIFF (exceto arquivos TIFF de 32 bits e arquivos PTIFF), ICO e ICN tipos MIME.

Consulte [Biblioteca de Transcodificação de Imagens](imaging-transcoding-library.md).

## Camera Raw compatível {#supported-camera-raw}

A biblioteca [!DNL Adobe Camera Raw] permite que [!DNL Assets] assimile imagens brutas. Consulte o [suporte da Camera Raw](camera-raw.md).

## [!DNL Assets] formatos de documento com suporte {#supported-document-formats}

Os formatos de documento compatíveis com recursos de gerenciamento de ativos são os seguintes:

| Formato | Armazenamento | [Gerenciamento de metadados](metadata.md) | Extração de texto completo <br> | [Extração de metadados](metadata.md) | Geração de miniatura<br> | [Extração de subativos](managing-linked-subassets.md) | [Writeback de metadados](xmp-writeback.md) | [Connected Assets](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [IA](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| DOC | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| RTF | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| TXT | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLS | ✓ | ✓ | ✓ | − | − | − | − | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | − | − | − | ✓ |
| ODS | ✓ | ✓ | ✓ | − | − | − | − | − |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | − | ✓ |
| ODP | ✓ | ✓ | ✓ | − | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | − | ✓ | ✓ | ✓ | ✓ | − |
| PS | ✓ | ✓ | − | − | − | − | − | − |
| QXP | ✓ | ✓ | − | − | − | − | − | − |
| EPUB | ✓ | ✓ | − | ✓ | ✓ | − | − | − |

## Formatos multimídia compatíveis {#supported-multimedia-formats}

| | Armazenamento | Gerenciamento de metadados | Extração de metadados | Geração de miniaturas | Transcodificação de FFmpeg |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | − | − | &#42; |
| MIDI | ✓ | ✓ | − | − | &#42; |
| 3GP | ✓ | ✓ | − | − | &#42; |
| MP3 | ✓ | ✓ | ✓ | − | &#42; |
| MPG | ✓ | ✓ | − | − | &#42; |
| OGA | ✓ | ✓ | − | − | &#42; |
| OGG | ✓ | ✓ | − | − | &#42; |
| RA | ✓ | ✓ | − | − | &#42; |
| WAV | ✓ | ✓ | − | − | &#42; |
| WMA | ✓ | ✓ | − | − | &#42; |
| DVI | ✓ | ✓ | − | &#42; | &#42; |
| FLV | ✓ | ✓ | − | &#42; | &#42; |
| M4V | ✓ | ✓ | − | &#42; | &#42; |
| MPEG | ✓ | ✓ | − | &#42; | &#42; |
| OGV | ✓ | ✓ | − | &#42; | &#42; |
| MOV | ✓ | ✓ | − | &#42; | &#42; |
| WMV | ✓ | ✓ | − | &#42; | &#42; |
| SWF | ✓ | ✓ | − | − | − |

## Formatos de arquivo não suportados {#supported-archive-formats}

Os formatos de arquivo compatíveis e a aplicabilidade dos fluxos de trabalho comuns do DAM são abordados na tabela a seguir.

| Formatos | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Distribuição do Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Outros formatos compatíveis {#other-supported-formats}

A aplicabilidade das funcionalidades comuns do DAM para alguns formatos de arquivo específicos é descrita abaixo.

| Formatos | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Distribuição do Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript (quando configurado com seu próprio domínio de delivery) | − | − | − | − | − | ✓ |

>[!NOTE]
>
>O upload e a distribuição de arquivos JavaScript podem ou não ser seguros. Se necessário, você pode usar sobreposições para impedir que os usuários façam upload de arquivos JS.

## Tipos MIME suportados {#supported-mime-types}

Por padrão, o [!DNL Experience Manager] detecta o tipo de arquivo usando a extensão. O [!DNL Experience Manager] pode detectá-lo a partir do conteúdo dos arquivos. Para o último, selecione a opção [!UICONTROL Detectar MIME do conteúdo] no [!UICONTROL Day CQ DAM Mime Type Service] no Console da Web [!DNL Experience Manager].

Uma lista de tipos MIME suportados está disponível no CRXDE Lite em `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

| Extensão de arquivo | Tipo de MIME/ tipo de mídia da Internet | Valor padrão de jobParam | Valor jobParam permitido |
|---|---|---|---|
| Imagem | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | O jobParam padrão se aplica a todos os ativos de tipo MIME da imagem.<ul><li>[OpçõesDePlanoDeFundoNocaute](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-knockout-background-options)</li><li>[manualCropOptions](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-manual-crop-options)</li><li>[autoColorCropOptions](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-color-crop-options)</li><li>[autoTransparentCropOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-transparent-crop-options.html)</li><li>[colorManagementOptions](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-color-management-options)</li><li>[autoSetCreationOptions](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-auto-set-creation-options)</li><li>[configuraçãoEmail](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/sting-constants/r-email-settings)</li><li>[xmpKeywords](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-xmp-keywords)</li><li>[unsharpMaskOptions](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-unsharp-mask-options)</li></ul> |
| 3G2 | video/3gpp2 | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| 3GP | video/3gpp | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| AAC | audio/x-aac | | |
| AFM | application/x-font-type1 | | |
| IA | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options)</li><li> [OpçõesDoIlustrador](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options)</li></ul> |
| AIFF | audio/x-aiff | | |
| AVI | video/x-msvideo | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| BMP | image/bmp | | |
| CSS | texto/css | | |
| DOC | application/msword | | |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> | | |
| F4V | video/x-f4v | | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash | | |
| FLV | video/x-flv | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| FPX | image/vnd.fpx | | |
| GIF | image/gif | | |
| ICC | application/vnd.iccprofile | | |
| ICM | application/vnd.iccprofile | | |
| INDD | application/x-indesign | | |
| JPEG | image/jpeg | | |
| JPG | image/jpeg | | |
| M2V | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| M4V | video/x-m4v | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| MOV | video/quicktime | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| MP3 | audio/mpeg | | |
| MP4 | video/mp4 | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| MPEG | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| MPG | video/mpeg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| MTS | model/vnd.mts | | |
| OGV | video/ogg | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| OTF | application/x-font-otf | | |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [OpçõesPDF](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-pdf-options) |
| PFB | application/x-font-type1 | | |
| PFM | application/x-font-type1 | | |
| PICT | image/x-pict | | |
| PNG | image/png | | |
| PPT | application/vnd.ms-powerpoint | | |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options)</li><li>[illustratorOptions](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-options)</li><li>[photoshopLayerOptions](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/data-types/r-photoshop-layer-options)</li></ul> |
| RTF | application/rtf | | |
| SVG | image/svg+xml | | |
| SWF | application/x-shockwave-flash | | |
| TAR | application/x-tar | | |
| TIF/TIFF | image/tiff | | |
| TTC | application/x-font-ttf | | |
| TTF | application/x-font-ttf | | |
| VOB | video/dvd | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| VTT | text/vtt | | |
| WAV | audio/x-wav | | |
| WEBM | video/webm | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| WMA | audio/x-ms-wma | | |
| WMV | video/x-ms-wmv | | [ExcludeMasterVideoFromAVS](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-production-api/c-deprecated-calls) |
| XLS | application/vnd.ms-excel | | |
| ZIP | application/zip | | |

## Dynamic Media - Formatos de vídeo de entrada compatíveis com transcodificação {#supported-input-video-formats-for-dynamic-media-transcoding}

| Extensão do arquivo de vídeo | Contêiner | Codecs de vídeo recomendados | Codecs de vídeo não suportados |
|---|---|---|---|
| AVI | Intercalação A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft® Video 1 (MS-CRAM) |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (arquivos de animação de vetor) |
| M4V | Apple iTunes | H264/AVC | − |
| MKV | Matroska | H264/AVC | − |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 e HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Animação do Apple |
| MP4 | MPEG-4 | H264/AVC (todos os perfis) | − |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | − |
| MXF ‡ | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | − |
| OGV, OGG | Ogg | Theora, VP3, Dirac | − |
| WebM | WebM | Google VP8 | − |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Tela Microsoft® (MSS2), História de foto Microsoft® (WVP2) |

‡ Este formato de vídeo ainda não é suportado para uso com Vídeos interativos no Dynamic Media ou para uso com Anotação no Experience Manager Assets.

## Dynamic Media - Formatos de documento compatíveis {#supported-document-formats-dynamic-media}

| Formato | Carregar <br> (Formato de entrada) | Criar<br> imagem<br> predefinição<br> (Formato de saída) | Visualizar representação<br> dinâmica<br> | Entregar <br> representação <br> dinâmica | Baixar representação <br> dinâmica<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| [IA](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | − | − | − | − |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | − | − | − | − |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) (Veja a Observação abaixo) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>Para PDFs seguros, somente o Upload é suportado.

Além da funcionalidade acima, considere o seguinte:

* Para usar o Dynamic Media para gerar representações dinâmicas para arquivos PDF, consulte os formatos de arquivo do [Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para usar o Dynamic Media para visualizar e gerar representações dinâmicas para arquivos AI, consulte os formatos de arquivo do [Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para usar o Dynamic Media para gerar representações dinâmicas para arquivos INDD, consulte [formato de arquivo InDesign (INDD)](../assets/managing-image-presets.md#indesign-indd-file-format).

## Dynamic Media - Formatos de imagem rasterizada compatíveis {#supported-raster-image-formats-dynamic-media}

| Formato | Upload (formato de entrada) | Criar predefinição de imagem (Formato de saída) | Visualizar representação dinâmica | Entregar representação dinâmica | Baixar representação dinâmica | Definir tipos que oferecem suporte a este formato |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| AVIF | − | − | − | ✓ | − | − |
| BMP | ✓ | − | − | − | − | [Imagem](/help/assets/image-sets.md), [Mídia mista](/help/assets/mixed-media-sets.md) e [Rotação](/help/assets/spin-sets.md) |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | − |
| HEIC | − | − | − | ✓ | − | − |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagem](/help/assets/image-sets.md), [Mídia mista](/help/assets/mixed-media-sets.md) e [Rotação](/help/assets/spin-sets.md) |
| PICT | ✓ | − | − | − | − | − |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagem](/help/assets/image-sets.md), [Mídia mista](/help/assets/mixed-media-sets.md) e [Rotação](/help/assets/spin-sets.md) |
| PSD ‡ | ✓ | − | − | − | − | − |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagem](/help/assets/image-sets.md), [Mídia mista](/help/assets/mixed-media-sets.md) e [Rotação](/help/assets/spin-sets.md) |
| WEBP | − | − | − | ✓ | − | − |

<!-- AVIF, HEIC, and WebP added to table above on March 4, 2024 based on CQDOC-21294 -->

‡ A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada pelo Adobe Photoshop e incluída no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

* O suporte para arquivos EPS se aplica somente a imagens rasterizadas. Por exemplo, a geração de miniaturas para imagens vetoriais do EPS não é compatível por padrão. Para adicionar suporte, [configure o ImageMagick](best-practices-for-imagemagick.md). Para integrar ferramentas de terceiros para habilitar recursos adicionais, consulte [Manipulador de mídia baseado em linha de comando](media-handlers.md#command-line-based-media-handler).

* Para usar o [!DNL Dynamic Media] para visualizar e gerar representações dinâmicas para arquivos do EPS, consulte os formatos de arquivo do [Adobe Illustrator (AI), Postscript (EPS) e PDF.](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para arquivos EPS, o write-back de metadados é compatível com a PostScript Document Structuring Convention (PS-Adobe) versão 3.0 ou posterior.

## Dynamic Media - Formatos de imagem rasterizada não aceitos {#unsupported-image-formats-dynamic-media}

A lista a seguir descreve os subtipos de formatos de arquivo de imagem rasterizada que *não* são suportados pelo Dynamic Media.

* Arquivos PNG com tamanho de bloco IDAT maior que 100 MB.
* Arquivos PSB.
* Arquivos PSD com um espaço de cor diferente de CMYK, RGB, Tons de cinza ou Bitmap não são compatíveis. Espaços de cores DuoTone, Lab e Indexado não são compatíveis.
* Arquivos PSD com profundidade de bits superior a 16.
* Arquivos TIFF com dados de ponto flutuante.
* Arquivos TIFF com espaço de cores Lab.

<!-- Topic commented out for now as of March 31, 2020. The topic may still need adjustment so it can be published live, or it may be moved into a KB article instead. Just waiting on feedback in CQDOC-15657. - Rick
## Unsupported raster image formats in Dynamic Media (#unsupported-image-formats-dynamic-media)

The following table describes the sub-types of raster image formats that are *not* supported in Dynamic Media. The table also describes suggested methods you can use to detect such files.

| Format | What is unsupported? | Suggested detection method |
|---|---|---|
| JPEG  | Files where the initial three bytes is incorrect. | To identify a JPEG file, its initial three bytes must be `ff d8 ff`. If they are anything else, then it is not classified as a JPEG.<br>&bull; There is no software tool that can help with this issue.<br>&bull; A small C++/java program which reads the initial three bytes of a file should be able to detect these types of files.<br>&bull; It may be better to track the source of such files and look at the tool generating the file. |
| PNG |  Files that have an IDAT chunk size greater than 100 MB. | You can detect this issue using [libpng](https://www.libpng.org/pub/png/libpng.html) in C++. |
| PSB |  | Use exiftool if the file type is PSB.<br>Example in an ExifTool log:<br>1. File type: `PSB` |
| PSD | Files with a color space other than CMYK, RGB, Grayscale, or Bitmap are not supported.<br>DuoTone, Lab, and Indexed color spaces are not supported. | Use ExifTool if Color mode is Duotone.<br>Example in an ExifTool log:<br>1. Color mode: `Duotone` |
|  | Files with abrupt endings. | Adobe is unable to detect this condition. Also, such files cannot be opened with Adobe PhotoShop. Adobe suggests you examine the tool that was used to create such a file and troubleshoot at the source. |
|  | Files that have a bit depth greater than 16. | Use ExifTool if the bit depth is greater than 16.<br>Example in an ExifTool log:<br>1. Bit depth: `32` |
|  | File that have Lab color space. | Use exiftool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
| TIFF | Files that have floating point data. That is, a TIFF file with 32-bit depth is not supported. | Use ExifTool if the MIME type is `image/tiff` and the SampleFormat has `Float` in its value. Example in an ExifTool log:<br>1. MIME type: `image/tiff`<br>Sample format: `Float #`<br>2. MIME type: `image/tiff`<br>Sample format: `Float; Float; Float; Float` |
|  | Files that have Lab color space. | Use ExifTool if the color mode is Lab.<br>Example in an ExifTool log:<br>1. Color mode: `Lab` |
-->

## Dynamic Media - Formatos 3D compatíveis {#supported-three-d-file-formats-in-dm}

O Dynamic Media é compatível com os seguintes formatos 3D.

Consulte também [Trabalhar com ativos 3D no Dynamic Media](/help/assets/assets-3d.md).

| Extensão de arquivo 3D | Formato do arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão GL Binária | model/gltf-binary | Inclui os materiais e texturas como um único ativo. |
| OBJ | Arquivo de objeto 3D do WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Arquivo Zip de Descrição de Cena Universal | model/vnd.usdz+zip | *Suporte somente para assimilação; não há visualização ou interação disponíveis.O* USDZ é um formato 3D proprietário que pode ser visualizado nativamente por dispositivos Safari e iOS. |

>[!MORELIKETHIS]
>
>* [Habilitar suporte a parâmetro de trabalho de carregamento do Dynamic Media Classic e do Assets baseado em tipo MIME](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [Configurar baseado em tipo MIME para suporte a parâmetros de trabalho de carregamento](config-dynamic.md).
