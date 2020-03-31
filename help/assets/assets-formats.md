---
title: Formatos compatíveis de ativos
description: Lista de formatos de arquivo suportados pelo AEM Assets e pelo Dynamic Media e recursos compatíveis com cada formato.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 593c1e1954a1c8e0355ede9889caed05ff72f3f9

---


# Formatos de ativos suportados {#assets-supported-formats}

O AEM Assets oferece suporte para diversos formatos de arquivo e cada funcionalidade tem suporte variado para diferentes tipos de MIME.

Para integrar os ativos AEM a outras soluções de gerenciamento de ativos digitais (DAM) compatíveis com padrões e software de desktop, use a Plataforma extensível de metadados (XMP) da Adobe.

Use a legenda para entender o nível de suporte.

| Nível de suporte | Descrição |
|:---:|---|
| ✓ | Compatível |
| * | Suportado com recursos complementares |
| − | Não aplicável |

## Formatos de imagem de rasterização suportados nos ativos AEM {#supported-raster-image-formats}

| Formato | Armazenamento | Gerenciamento de metadados | Extração de metadados | Geração de miniaturas | Edição interativa | Writeback de metadados | Insights |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PNM | ✓ | ✓ |  |  |  |  | ✓ |
| PFM | ✓ | ✓ |  |  |  |  | ✓ |
| PBM | ✓ | ✓ |  |  |  |  | ✓ |
| PPM | ✓ | ✓ |  |  |  |  | ✓ |
| PSD ‡ | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ |  | ✓ |  |
| PICT |  |  |  |  |  |  | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ |  |  |  |

‡ A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada pelo Adobe Photoshop e incluída no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

## Formatos de imagem rasterizada suportados no Dynamic Media (#supported-raster-image-format-dynamic-media)

| Formato | Carregar<br> (formato de entrada) | Criar<br> predefinição<br><br> de imagem (formato de saída) | Execução dinâmica<br> de Pré-visualização<br> | Fornecer<br> representação dinâmica<br> | Baixar<br> representação dinâmica<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ |  |  |  |  |
| PSD **‡** | ✓ |  |  |  |  |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ |  |  |  |  |

**‡** A imagem mesclada é extraída do arquivo PSD. É uma imagem gerada pelo Adobe Photoshop e incluída no arquivo PSD. Dependendo das configurações, a imagem mesclada pode ou não ser a imagem real.

Além das informações acima, considere o seguinte:

* O suporte para arquivos EPS se aplica somente a imagens rasterizadas. Por exemplo, a geração de miniaturas para imagens vetoriais EPS não é suportada por padrão. Para adicionar suporte, [configure o ImageMagick](best-practices-for-imagemagick.md). Para integrar ferramentas de terceiros para ativar recursos adicionais, consulte Manipulador [de mídia baseado na linha](media-handlers.md#command-line-based-media-handler)de comando.

* A gravação de metadados funciona no formato de arquivo PSB quando é adicionada ao manipulador `NComm` .

* Para usar o Dynamic Media para pré-visualização e gerar renderizações dinâmicas para arquivos EPS, consulte os formatos de arquivo [Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para arquivos EPS, o write-back de metadados é compatível com a versão 3.0 ou posterior da Convenção de estruturação de Documentos PostScript (PS-Adobe).

## Formatos de imagem rasterizada não suportados no Dynamic Media (#unsupported-image-format-dynamic-media)

A tabela a seguir descreve os subtipos de formatos de imagem rasterizada que *não* são suportados no Dynamic Media. A tabela também descreve os métodos sugeridos que você pode usar para detectar esses arquivos.

| Formato | O que não é suportado? | Método de detecção sugerido |
|---|---|---|
| JPEG | Arquivos nos quais os três bytes iniciais estão incorretos. | Para identificar um arquivo JPEF, os três bytes iniciais devem ser `ff d8 ff`. Se forem mais alguma coisa, então não é classificado como um JPEG.<br>・ Não há nenhuma ferramenta de software que possa ajudar neste problema.<br>・ Um pequeno programa C++/java que lê os três bytes iniciais de um arquivo deve ser capaz de detectar esses tipos de arquivos.<br>・ Pode ser melhor rastrear a fonte desses arquivos e observar a ferramenta que gera o arquivo. |
| PNG | Arquivos com um tamanho de bloco IDAT maior que 100 MB. | Você pode detectar esse problema usando o [libpng](http://www.libpng.org/pub/png/libpng.html) no C++. |
| PSB |  | Use exiftool se o tipo de arquivo for PSB.<br>Exemplo em um log ExifTool:<br>1. Tipo de arquivo: `PSB` |
| PSD | Arquivos com um espaço de cor diferente de CMYK, RGB, Escala de cinza ou Bitmap não são suportados.<br>Espaços de cores Indexadas, Lab e DuoTone não são suportados. | Use ExifTool se o modo Cor for Duotônico.<br>Exemplo em um log ExifTool:<br>1. Modo de cores: `Duotone` |
|  | Arquivos com terminações abruptas. | A Adobe não consegue detectar essa condição. Além disso, esses arquivos não podem ser abertos com o Adobe PhotoShop. A Adobe sugere que você examine a ferramenta usada para criar tal arquivo e solucionar problemas na fonte. |
|  | Arquivos com uma profundidade de bits maior que 16. | Use ExifTool se a profundidade de bits for maior que 16.<br>Exemplo em um log ExifTool:<br>1. Profundidade de bits: `32` |
|  | Arquivo com espaço de cor Lab. | Use exiftool se o modo de cor for Lab.<br>Exemplo em um log ExifTool:<br>1. Modo de cores: `Lab` |
| TIFF | Arquivos com dados de ponto flutuante. Ou seja, um arquivo TIFF com profundidade de 32 bits não é suportado. | Use ExifTool se o tipo MIME for `image/tiff` e SampleFormat tiver `Float` o valor. Exemplo em um log ExifTool:<br>1. Tipo MIME: Formato `image/tiff`<br>de amostra: `Float #`<br>2. Tipo MIME: Formato `image/tiff`<br>de amostra: `Float; Float; Float; Float` |
|  | Arquivos com espaço de cor Lab. | Use ExifTool se o modo de cor for Lab.<br>Exemplo em um log ExifTool:<br>1. Modo de cores: `Lab` |

## Biblioteca PDF Rasterizer compatível {#supported-pdf-rasterizer-library}

A biblioteca do Adobe PDF Rasterizer gera miniaturas e pré-visualizações de alta qualidade para arquivos Adobe Illustrator e PDF grandes e com grande quantidade de conteúdo. A Adobe recomenda usar a biblioteca do PDF Rasterizer para o seguinte:

* Arquivos AI/PDF com uso intenso de conteúdo que consomem muitos recursos para serem processados.
* Arquivos AI/PDF, para os quais as miniaturas não são geradas por padrão.
* Arquivos AI com cores Pantone Matching System (PMS).

See [Using PDF Rasterizer](aem-pdf-rasterizer.md).

## Biblioteca de transcodificação de imagem suportada {#supported-image-transcoding-library}

A biblioteca Adobe Imaging Transcoding é uma solução de processamento de imagem que executa funções essenciais de manipulação de imagens, como codificação, transcodificação, redefinição de resolução e redimensionamento.

A biblioteca de transcodificação de imagens suporta JPG/JPEG, PNG (8 bits e 16 bits), GIF, BMP, TIFF/Compressed TIFF (exceto arquivos TIFF de 32 bits e arquivos PTIFF), ICO e ICN MIME.

Consulte Biblioteca [de transcodificação de](imaging-transcoding-library.md)imagens.

## Camera bruta suportada {#supported-camera-raw}

A biblioteca do Adobe Camera Raw permite que os ativos AEM assimilem imagens brutas. See [Camera Raw support](camera-raw.md).

## Formatos de documento de ativos suportados {#supported-document-formats}

Os formatos de Documento suportados para recursos de gerenciamento de ativos são os seguintes:

| Formato | Armazenamento | Gerenciamento de metadados<br> | Metadata<br> extraction | Geração de miniaturas<br> | Edição interativa<br> | Writeback de metadados<br> | [Insights](touch-ui-asset-insights.md) | [Connected Assets](use-assets-across-connected-assets-instances.md) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| DOC | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| RTF | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| TXT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLS | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODS | ✓ | ✓ | ✓ |  |  |  |  |  |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| ODP | ✓ | ✓ | ✓ |  |  |  |  |  |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| PS | ✓ | ✓ |  |  |  |  |  |  |
| QXP | ✓ | ✓ |  |  |  |  |  |  |
| EPUB | ✓ | ✓ |  | ✓ | ✓ |  |  |  |

## Formatos de documento suportados no Dynamic Media (#supported-documento-format-dynamic-media)

| Formato | Carregar<br> (formato de entrada) | Criar<br> predefinição<br><br> de imagem (formato de saída) | Execução dinâmica<br> de Pré-visualização<br> | Fornecer<br> representação dinâmica<br> | Baixar<br> representação dinâmica<br> |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ |  |  |  |  |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ |  |  |  |  |

Além da funcionalidade acima, considere o seguinte:

* Para usar o Dynamic Media para gerar renderizações dinâmicas para arquivos PDF, consulte [Adobe Illustrator (AI), Postscript (EPS) e formatos de arquivo PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para usar o Dynamic Media para pré-visualização e gerar renderizações dinâmicas para arquivos AI, consulte os formatos de arquivo [Adobe Illustrator (AI), Postscript (EPS) e PDF.](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* Para usar o Dynamic Media para gerar execuções dinâmicas para arquivos INDD, consulte o formato [de arquivo](../assets/managing-image-presets.md#indesign-indd-file-format)InDesign (INDD).

## Formatos de multimídia suportados {#supported-multimedia-formats}

|  | Armazenamento | Gerenciamento de metadados | Extração de metadados | Geração de miniaturas | Transcodificação FMPEG |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ |  | − | * |
| MIDI | ✓ | ✓ |  | − | * |
| 3GP | ✓ | ✓ |  | − | * |
| MP3 | ✓ | ✓ | ✓ | − | * |
| MPG | ✓ | ✓ |  | − | * |
| OGA | ✓ | ✓ |  | − | * |
| OGG | ✓ | ✓ |  | − | * |
| RA | ✓ | ✓ |  | − | * |
| WAV | ✓ | ✓ |  | − | * |
| WMA | ✓ | ✓ |  | − | * |
| DVI | ✓ | ✓ |  | * | * |
| FLV | ✓ | ✓ |  | * | * |
| M4V | ✓ | ✓ |  | * | * |
| MPEG | ✓ | ✓ |  | * | * |
| OGV | ✓ | ✓ |  | * | * |
| MOV | ✓ | ✓ |  | * | * |
| WMV | ✓ | ✓ |  | * | * |
| SWF | ✓ | ✓ |  |  |  |

## Formatos de vídeo de entrada suportados no Dynamic Media para transcodificação {#supported-input-video-formats-for-dynamic-media-transcoding}

| Extensão do arquivo de vídeo | Container | Codecs de vídeo recomendados | Codecs de vídeo não suportados |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC (todos os perfis) |  |
| MOV, QT | Apple QuickTime | H264/AVC, Apple ProRes422 &amp; HQ, Sony XDCAM, Sony DVCAM, HDV, Panasonic DVCPro, Apple DV (DV25), Apple PhotoJPEG, Sorenson, Avid DNxHD, Avid AVR | Apple Intermediate, Animação da Apple |
| FLV, F4V | Adobe Flash | H264/AVC, Flix VP6, H263, Sorenson | SWF (arquivos de animação vetorial) |
| WMV | Windows Media 9 | WMV3 (v9), WMV2 (v8), WMV1 (v7), GoToMeeting (G2M2, G2M3, G2M4) | Microsoft Screen (MSS2), Microsoft Photo Story (WVP2) |
| MPG, VOB, M2V, MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | Intercalação A/V | XVID, DIVX, HDV, MiniDV (DV25), Techsmith Camtasia, Huffyuv, Fraps, Panasonic DVCPro | Indeo3 (IV30), MJPEG, Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | VP8 do Google |  |
| OGV, OGG | Ogg | Theora, VP3, Dirac |  |
| MXF | MXF | Sony XDCAM, MPEG-2, MPEG-4, Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D, RM | Vídeo vermelho bruto | MJPEG 2000 |  |
| RAM, RM | RealVideo | Não suportado | Real G2 (RV20), Real 8 (RV30), Real 10 (RV40) |
| FLAC | Flash nativo | Codec de áudio sem perda gratuito |  |
| MJ2 | Motion JPEG 2000 | Codec Motion JPEG 2000 |  |

## Formatos de arquivo suportados {#supported-archive-formats}

Os formatos de arquivamento suportados e a aplicabilidade dos workflows DAM comuns são abordados na tabela a seguir.

| Formatos | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Delivery Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Outros formatos suportados {#other-supported-formats}

A aplicabilidade de workflows DAM comuns para alguns outros formatos de arquivo está descrita na tabela abaixo. A funcionalidade comum do DAM, como armazenamento, controle de versão, ACL, fluxo de trabalho, publicação e gerenciamento de metadados, exceto o Delivery de Mídia dinâmica, é compatível com todos os arquivos.

| Formatos | Armazenamento | Versões | Fluxo de trabalho | Publicação | Controle de acesso | Delivery Dynamic Media |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript (quando configurado com o próprio domínio do delivery) |  |  |  |  |  | ✓ |

## Supported MIME types {#supported-mime-types}

Por padrão, o AEM detecta o tipo de arquivo usando a extensão de arquivo. O AEM pode detectá-lo do conteúdo dos arquivos. Para o último, selecione a opção [!UICONTROL Detectar MIME do conteúdo] no [!UICONTROL Dia CQ DAM Mime Type Service] no console da Web do AEM.

Uma lista de tipos MIME suportados está disponível no CRXDE Lite em `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`.

Consulte [Configuração baseada em tipo MIME para suporte](config-dynamic.md)a parâmetros de trabalho de upload.

Consulte também [Habilitando o suporte](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)a parâmetros de trabalho de upload de ativos/Scene7 baseados em tipos MIME.

| Extensão de arquivo | Tipo MIME/tipo de mídia da Internet | Valor de jobParam padrão | Valor jobParam permitido |
|---|---|---|---|
| Imagem | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | O jobParam padrão se aplica a todos os ativos do tipo mime de imagem.<ul><li>[knockoutBackgroundOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_knockout_background_options.html)</li><li>manualCropOptions</li><li>[autoColorCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_auto_color_crop_options)</li><li>[autoTransparentCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_auto_transparent_crop_options)</li><li>[colorManagementOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_color_management_options.html)</li><li>[autoSetCreationOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_auto_set_creation_options.html)</li><li>[emailSetting](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/string_constants/index.html?f=r_email_settings)</li><li>[xmpKeywords](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_xmp_keywords)</li><li>[unsharMaskOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_unsharp_mask_options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| 3GP | video/3gpp |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_exclude_master_video_from_avs) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_post_script_options.html)</li><li> [illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_illustrator_options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| BMP | image/bmp |  |  |
| CSS | text/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcluirVídeoMestreDeAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| M4V | video/x-m4v |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MOV | video/quicktime |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPEG | video/mpeg |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPG | video/mpeg |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdfOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_pdf_options) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_post_script_options)</li><li>[illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_illustrator_options)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_photoshop_options)</li><li>[photoshopLayerOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_photoshop_layer_options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcluirVídeoMestreDeAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [Habilite o suporte](../sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)ao parâmetro de trabalho de upload do tipo MIME Assets/Scene7.

