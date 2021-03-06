---
title: Formatos de arquivo suportados e tipos MIME
description: Formatos de arquivo e tipos MIME suportados por [!DNL Assets] e [!DNL Dynamic Media] e os recursos compatíveis com cada formato.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Asset Management,Renditions
exl-id: a4bcf67b-54f4-4681-9e42-fd4753acde1a
source-git-commit: fcbfd8b378282d908b68c61ab235e9b80fd6644c
workflow-type: tm+mt
source-wordcount: '1751'
ht-degree: 10%

---

# Formatos compatíveis com o [!DNL Adobe Experience Manager Assets] {#assets-supported-formats}

[!DNL Experience Manager Assets] O suporta uma grande variedade de formatos de arquivo e cada funcionalidade tem suporte variado para diferentes tipos MIME. Para integrar [!DNL Assets] com outras soluções de gerenciamento de ativos digitais (DAM) compatíveis com os padrões, use o Adobe e [!DNL Extensible Metadata Platform] (XMP).

Use a legenda para entender o nível de compatibilidade.

| Nível de compatibilidade | Descrição |
| :-----------: | ------------------------------ |
| ✓ | Compatível |
| &#42; | Suportado com recursos complementares |
| − | Não aplicável |

## Formatos de imagem raster suportados em [!DNL Experience Manager] {#supported-raster-image-formats}

Os formatos de imagem rasterizada aceitos em [!DNL Assets] são:

| Formato | Armazenamento | Gerenciamento de metadados | Extração de metadados | Geração de miniaturas | Edição | Write-back de metadados | Insights |
| ------------ | :------: | :-----------------: | :-----------------: | :------------------: | :------: | :----------------: | :------: |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| PNM | ✓ | ✓ | - | - | - | - | ✓ |
| PGM | ✓ | ✓ | - | - | - | - | ✓ |
| PBM | ✓ | ✓ | - | - | - | - | ✓ |
| PPM | ✓ | ✓ | - | - | - | - | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | - | ✓ | - |
| PICT | - | - | - | - | - | - | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ | - | - | - |

‡ A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada pelo Adobe Photoshop e incluída no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

Além das informações acima, considere o seguinte:

* O suporte para arquivos EPS se aplica somente a imagens raster. Por exemplo, a geração de miniaturas de imagens vetoriais do EPS não é compatível por padrão. Para adicionar suporte, [configurar o ImageMagick](best-practices-for-imagemagick.md). Para integrar ferramentas de terceiros e ativar recursos adicionais, consulte [Manipulador de mídia baseado em linha de comando](media-handlers.md#command-line-based-media-handler).

* O write-back de metadados funciona para o formato de arquivo PSB quando é adicionado ao `NComm` manipulador.

* Para arquivos EPS, o write-back de metadados é compatível com a versão 3.0 ou posterior da Convenção de Estrutura de Documentos PostScript (PS-Adobe).

## Formatos 3D suportados {#support-3d-formats}

A seguinte lista de formatos 3D é suportada.

Consulte também [Trabalhar com ativos 3D no Dynamic Media.](/help/assets/assets-3d.md)

| Formato | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Visualização de miniatura | Visualização 3D | Delivery Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DN | ✓ | ✓ | ✓ |  | ✓ | ✓ | - | - |
| gLB | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| gLTF | ✓ | ✓ | ✓ |  | ✓ | - | ✓ | - |
| OBJ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| STL | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ | ✓ |
| USDz | ✓ | ✓ | ✓ | ✓ | ✓ | - | - | ✓ |

## Biblioteca PDF Rasterizer suportada {#supported-pdf-rasterizer-library}

A biblioteca do Adobe PDF Rasterizer gera miniaturas e visualizações de alta qualidade para grandes e com uso intenso de conteúdo [!DNL Adobe Illustrator] e arquivos PDF. O Adobe recomenda usar a biblioteca PDF Rasterizer para o seguinte:

* Arquivos IA/PDF com uso intenso de conteúdo que consomem muitos recursos para serem processados.
* Arquivos AI/PDF, para os quais as miniaturas não são geradas por padrão.
* Arquivos AI com cores do Pantone Matching System (PMS).

Consulte [Usando PDF Rasterizer](aem-pdf-rasterizer.md).

## Biblioteca de transcodificação de imagem suportada {#supported-image-transcoding-library}

A biblioteca de transcodificação de imagem do Adobe é uma solução de processamento de imagens que executa funções essenciais de manipulação de imagens, como codificação, transcodificação, redefinição de amostra e redimensionamento.

A biblioteca de transcodificação de imagens oferece suporte a JPG/JPEG, PNG (8 bits e 16 bits), GIF, BMP, TIFF/TIFF compactado (além dos arquivos TIFF de 32 bits e PTIFF), ICO e ICN MIME.

Consulte [Biblioteca de transcodificação de imagens](imaging-transcoding-library.md).

## Camera Raw suportado {#supported-camera-raw}

O [!DNL Adobe Camera Raw] habilitação da biblioteca [!DNL Assets] para assimilar imagens brutas. Consulte [Suporte Camera Raw](camera-raw.md).

## Suportado [!DNL Assets] formatos de documento {#supported-document-formats}

Os formatos de documento compatíveis com os recursos de gerenciamento de ativos são os seguintes:

| Formato | Armazenamento | [Gerenciamento de metadados](metadata.md) | Texto completo<br> extração | [Extração de metadados](metadata.md) | Miniatura<br> geração | [Extração de subconjunto](managing-linked-subassets.md) | [Write-back de metadados](xmp-writeback.md) | [Connected Assets](use-assets-across-connected-assets-instances.md) |
|---|---|---|---|---|---|---|---|---|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | - |
| DOC | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| ODT | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| RTF | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| TXT | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| XLS | ✓ | ✓ | ✓ | - | - | - | - | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ | - | - | - | ✓ |
| ODS | ✓ | ✓ | ✓ | - | - | - | - | - |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | - | ✓ |
| ODP | ✓ | ✓ | ✓ | - | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ | - | ✓ | ✓ | ✓ | ✓ | - |
| PS | ✓ | ✓ | - | - | - | - | - | - |
| QXP | ✓ | ✓ | - | - | - | - | - | - |
| ePub | ✓ | ✓ | - | ✓ | ✓ | - | - | - |

## Formatos multimídia compatíveis {#supported-multimedia-formats}

|  | Armazenamento | Gerenciamento de metadados | Extração de metadados | Geração de miniaturas | Transcodificação de FFmpeg |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ | - | - | &#42; |
| MIDI | ✓ | ✓ | - | - | &#42; |
| 3GP | ✓ | ✓ | - | - | &#42; |
| MP3 | ✓ | ✓ | ✓ | - | &#42; |
| MPG | ✓ | ✓ | - | - | &#42; |
| OGA | ✓ | ✓ | - | - | &#42; |
| OGG | ✓ | ✓ | - | - | &#42; |
| ARM | ✓ | ✓ | - | - | &#42; |
| WAV | ✓ | ✓ | - | - | &#42; |
| WMA | ✓ | ✓ | - | - | &#42; |
| DVI | ✓ | ✓ | - | &#42; | &#42; |
| FLV | ✓ | ✓ | - | &#42; | &#42; |
| M4V | ✓ | ✓ | - | &#42; | &#42; |
| MPEG | ✓ | ✓ | - | &#42; | &#42; |
| OGV | ✓ | ✓ | - | &#42; | &#42; |
| MOV | ✓ | ✓ | - | &#42; | &#42; |
| WMV | ✓ | ✓ | - | &#42; | &#42; |
| SWF | ✓ | ✓ | - | - | - |

## Formatos de arquivo compatíveis {#supported-archive-formats}

Os formatos de arquivamento compatíveis e a aplicabilidade dos workflows comuns do DAM são abordados na tabela a seguir.

| Formatos | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Entrega do Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Outros formatos compatíveis {#other-supported-formats}

A aplicabilidade das funcionalidades usuais do DAM para alguns formatos de arquivo específicos está descrita abaixo.

| Formatos | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Entrega do Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript (quando configurado com o próprio domínio de delivery) | - | - | - | - | - | ✓ |

>[!NOTE]
>
>O upload e a distribuição de arquivos JavaScript podem ou não ser seguros. Se necessário, é possível usar as sobreposições para impedir que os usuários carreguem arquivos JS.

## Tipos MIME suportados {#supported-mime-types}

Por padrão, [!DNL Experience Manager] O detecta o tipo de arquivo usando a extensão de arquivo . [!DNL Experience Manager] O pode detectá-lo do conteúdo dos arquivos. Para o último, selecione [!UICONTROL Detectar MIME do conteúdo] em [!UICONTROL Serviço de Tipo Mime Day CQ DAM] no [!DNL Experience Manager] Console da Web.

Uma lista de tipos MIME suportados está disponível no CRXDE Lite at `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

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
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-post-script-options.html)</li><li>[ilustratorOptions](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-illustrator-options.html)</li></ul> |
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

## Dynamic Media - Formatos de vídeo de entrada compatíveis com transcodificação {#supported-input-video-formats-for-dynamic-media-transcoding}

| Extensão de arquivo de vídeo | Contêiner | Codecs de vídeo recomendados | Codecs de vídeo não suportados |
|---|---|---|---|
| AVI | Intercalação A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft® Video 1 (MS-CRAM) |
| FLV, F4V | Flash Adobe | H264/AVC, Flix VP6, H263, Sorenson | SWF (arquivos de animação vetorial) |
| M4V | Apple iTunes | H264/AVC | - |
| MKV | Matroska | H264/AVC | - |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediário, Animação do Apple |
| MP4 | MPEG-4 | H264/AVC (todos os perfis) | - |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 | - |
| MXF ‡ | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro | - |
| OGV, OGG | Ogg | Theora, VP3, Dirac | - |
| WebM | WebM | VP8 do Google | - |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Tela Microsoft® (MSS2), Microsoft® Photo Story (WVP2) |

‡ Este formato de vídeo ainda não é suportado para o uso com Vídeos interativos no Dynamic Media ou para o uso com Anotações no Experience Manager Assets.

## Dynamic Media - Formatos de documento compatíveis {#supported-document-formats-dynamic-media}

| Formato | Upload<br> (Formato de entrada) | Criar<br> imagem<br> predefinição<br> (Formato de saída) | Visualizar<br> dinâmico<br> representação | Delivery<br> dinâmico<br> representação | Baixar<br> dinâmico<br> representação |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | - | - | - | - |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | - | - | - | - |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) (Consulte a Observação abaixo) | ✓ | ✓ | ✓ | ✓ | ✓ |

>[!NOTE]
>
>Para PDF seguros, somente Upload é suportado.

Além da funcionalidade acima, considere o seguinte:

* Para usar o Dynamic Media para gerar representações dinâmicas para arquivos PDF, consulte [Formatos de arquivo Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para usar o Dynamic Media para visualizar e gerar representações dinâmicas para arquivos AI, consulte [Formatos de arquivo Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para usar o Dynamic Media para gerar representações dinâmicas para arquivos INDD, consulte [Formato de arquivo INDD (InDesign)](../assets/managing-image-presets.md#indesign-indd-file-format).

## Dynamic Media - Formatos de imagem rasterizada compatíveis {#supported-raster-image-formats-dynamic-media}

| Formato | Upload<br> (Formato de entrada) | Criar<br> imagem<br> predefinição<br> (Formato de saída) | Visualizar<br> dinâmico<br> representação | Delivery<br> dinâmico<br> representação | Baixar<br> dinâmico<br> representação | Definir tipos que suportam este formato |
|---|:---:|:---:|:---:|:---:|:---:| --- |
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagem](/help/assets/image-sets.md), [Mídia mista](/help/assets/mixed-media-sets.md)e [Rotação](/help/assets/spin-sets.md) |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagem](/help/assets/image-sets.md), [Mídia mista](/help/assets/mixed-media-sets.md)e [Rotação](/help/assets/spin-sets.md) |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | [Imagem](/help/assets/image-sets.md), [Mídia mista](/help/assets/mixed-media-sets.md)e [Rotação](/help/assets/spin-sets.md) |
| BMP | ✓ | - | - | - | - | [Imagem](/help/assets/image-sets.md), [Mídia mista](/help/assets/mixed-media-sets.md)e [Rotação](/help/assets/spin-sets.md) |
| PSD ‡ | ✓ | - | - | - | - | - |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | - |
| PICT | ✓ | - | - | - | - | - |

‡ A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada pelo Adobe Photoshop e incluída no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

* O suporte para arquivos EPS se aplica somente a imagens raster. Por exemplo, a geração de miniaturas de imagens vetoriais do EPS não é compatível por padrão. Para adicionar suporte, [configurar o ImageMagick](best-practices-for-imagemagick.md). Para integrar ferramentas de terceiros e ativar recursos adicionais, consulte [Manipulador de mídia baseado em linha de comando](media-handlers.md#command-line-based-media-handler).

* Para usar [!DNL Dynamic Media] para visualizar e gerar representações dinâmicas para arquivos EPS, consulte [Formatos de arquivo Adobe Illustrator (AI), Postscript (EPS) e PDF.](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para arquivos EPS, o write-back de metadados é compatível com a versão 3.0 ou posterior da Convenção de Estrutura de Documentos PostScript (PS-Adobe).

## Dynamic Media - Formatos de imagem rasterizada não aceitos {#unsupported-image-formats-dynamic-media}

A lista a seguir descreve os subtipos de formatos de arquivo de imagem rasterizada que são *not* compatível com o Dynamic Media.

Consulte também [Detectar formatos de arquivo não suportados para o Dynamic Media](https://helpx.adobe.com/experience-manager/kb/detect-unsupported-assets-for-dynamic-media.html) Artigo da Base de conhecimento.

* Arquivos PNG com um tamanho de bloco IDAT superior a 100 MB.
* Arquivos PSB.
* Arquivos PSD com um espaço de cores diferente de CMYK, RGB, Escala de cinza ou Bitmap não são compatíveis. Não há suporte para espaços de cores DuoTone, Lab e Indexado.
* Arquivos PSD com profundidade de bits superior a 16.
* Arquivos TIFF com dados de ponto flutuante.
* Arquivos TIFF com espaço de cores Lab.

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

## Dynamic Media - Formatos 3D compatíveis {#supported-three-d-file-formats-in-dm}

O Dynamic Media é compatível com os seguintes formatos 3D.

Consulte também [Trabalhar com ativos 3D no Dynamic Media](/help/assets/assets-3d.md).

| extensão de arquivo 3D | Formato de arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão binária GL | modelo/gltf-binário | Inclui os materiais e as texturas como um único ativo. |
| OBJ | Arquivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Arquivo Zip de descrição da cena universal | model/vnd.usdz+zip | *Suporte apenas para ingestão; nenhuma visualização ou interação está disponível.* USDZ é um formato 3D proprietário que pode ser visualizado originalmente por dispositivos Safari e iOS. |

>[!MORELIKETHIS]
>
>* [Habilitar o suporte ao parâmetro de trabalho de upload do Dynamic Media Classic e ativos baseados em tipo MIME](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).
>* [Configurar o tipo MIME baseado no suporte para carregar parâmetros de trabalho](config-dynamic.md).

