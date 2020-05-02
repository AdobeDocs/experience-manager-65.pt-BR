---
title: Gerencie metadados de seus ativos digitais no [!DNL Adobe Experience Manager].
description: Saiba mais sobre os tipos de metadados e como o [!DNL Adobe Experience Manager Assets] ajuda a gerenciar metadados de ativos para facilitar a categorização e a organização de ativos. O [!DNL Experience Manager] permite organizar e processar ativos automaticamente com base em seus metadados.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f21e9dbb81f18e07a691b2470c1c5b1569876b17

---


# Gerenciar metadados de seus ativos digitais {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] mantém metadados para cada ativo. Isso facilita a categorização e organização de ativos e ajuda as pessoas que estão procurando um ativo específico. Com a capacidade de extrair metadados de arquivos carregados para [!DNL Experience Manager Assets], o gerenciamento de metadados se integra ao fluxo de trabalho criativo. Com a capacidade de manter e gerenciar metadados com seus ativos, [!DNL Experience Manager Assets] torna possível organizar e processar automaticamente ativos com base em seus metadados.

* [Metadados XMP](xmp.md).
* [Como editar ou adicionar metadados](meta-edit.md).
* [Referência](meta-ref.md)de esquemas de metadados.

## Por que precisamos de metadados {#why-we-need-metadata}

Metadados significa dados sobre dados. Nesse sentido, os dados se referem ao seu ativo digital, digamos uma imagem. Os metadados são essenciais para o gerenciamento eficiente de ativos.

Metadados é a coleta de todos os dados disponíveis para um ativo, mas não necessariamente contidos nessa imagem. Alguns exemplos de metadados são:

* Nome do ativo.
* Hora e data da última modificação.
* Tamanho do ativo conforme ele foi armazenado no repositório.
* Nome da pasta em que está contido.
* Ativos relacionados ou tags aplicadas.

Essas são as propriedades básicas de metadados que [!DNL Experience Manager] podem ser gerenciadas para ativos, o que permite que os usuários vejam todos os ativos, por exemplo, ordenados por sua última data de modificação - úteis ao tentar descobrir quais ativos foram adicionados recentemente ao repositório.

Você pode adicionar mais dados de alto nível a ativos digitais, por exemplo:

* Tipo de ativo (é uma imagem, um vídeo, um clipe de áudio ou um documento?).
* Proprietário do ativo.
* Título do ativo.
* Descrição do ativo.
* Tags atribuídas a um ativo.

Mais metadados ajudam a categorizar ativos e são úteis à medida que a quantidade de informações digitais cresce. É possível gerenciar algumas centenas de arquivos com base apenas nos nomes dos arquivos. No entanto, essa abordagem não é escalável e rapidamente fica aquém do número de pessoas envolvidas e o número de ativos gerenciados aumenta.

Com a adição de metadados, o valor de um ativo digital cresce, pois o ativo se torna,

* Mais acessível - os sistemas e usuários podem encontrá-lo facilmente.
* Mais fácil de gerenciar - você pode encontrar ativos com o mesmo conjunto de propriedades mais facilmente e aplicar alterações a eles.
* Mais completo: quanto mais metadados você adicionar a um ativo, mais informações e contexto serão exibidos.

Por esses motivos, [!DNL Assets] fornece os meios certos de criar, gerenciar e trocar metadados para seus ativos digitais.

## Tipos de metadados {#types-of-metadata}

Os dois tipos básicos de metadados são metadados técnicos e metadados descritivos.

Os metadados técnicos são úteis para aplicativos de software que lidam com ativos digitais e não devem ser mantidos manualmente. [!DNL Experience Manager Assets] e outros softwares determinam automaticamente os metadados técnicos e os metadados podem mudar quando o ativo é modificado. Os metadados técnicos disponíveis de um ativo dependem em grande parte do tipo de arquivo do ativo. Alguns exemplos de metadados técnicos são:

* Tamanho de um arquivo.
* Dimensões (altura e largura) de uma imagem.
* Taxa de bits de um arquivo de áudio ou vídeo.
* Resolução (nível de detalhes) de uma imagem.

Metadados descritivos são metadados relacionados ao domínio do aplicativo, por exemplo, o negócio de onde um ativo vem. Metadados descritivos não podem ser determinados automaticamente. É criado manual ou semiautomaticamente. Por exemplo, uma câmera habilitada para GPS pode rastrear automaticamente a latitude e a longitude e adicionar geolocalização da imagem.

Devido ao alto custo do esforço manual necessário para criar informações descritivas de metadados, foram estabelecidos padrões para facilitar a troca de metadados entre sistemas de software e organizações.

[!DNL Experience Manager Assets] oferece suporte a todas as normas relevantes para o gerenciamento de metadados.

Devido à importância dos metadados e ao alto envolvimento manual necessário para criar metadados, foram estabelecidas normas que facilitam o intercâmbio.

## Padrões de codificação {#encoding-standards}

Há várias maneiras de incorporar metadados em arquivos. Há suporte para uma seleção de padrões de codificação:

* XMP: usado por [!DNL Assets] para armazenar os metadados extraídos no repositório.
* ID3: para arquivos de áudio e vídeo.
* Exif: para arquivos de imagem.
* Outro/Legado: de [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]e assim por diante.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) é um padrão aberto usado por todos [!DNL Experience Manager Assets] o gerenciamento de metadados. A codificação padrão de metadados universais do oferta que pode ser incorporada em todos os formatos de arquivo. A Adobe e outras empresas oferecem suporte ao padrão XMP, pois fornece um modelo de conteúdo avançado. Os usuários do padrão XMP e do [!DNL Experience Manager Assets] têm uma plataforma poderosa para desenvolver. For more information, see [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Os dados armazenados nessas tags ID3 são exibidos quando você reproduz um arquivo de áudio digital em seu computador ou em um player MP3 portátil.

As tags ID3 foram projetadas para o formato de arquivo MP3. Informações adicionais sobre formatos:

* As tags ID3 funcionam em arquivos MP3 e mp3PRO.
* WAV não tem tags.
* O WMA tem tags proprietárias que não permitem a implementação de código aberto.
* Ogg Vorbis usa Comentários Xiph incorporados ao container Ogg.
* O AAC usa um formato de marcação proprietário.

### Exif {#exif}

O formato de arquivo de imagem permutável (Exif) é o formato de metadados mais popular usado na fotografia digital. Ele fornece uma maneira de incorporar um vocabulário fixo de propriedades de metadados em muitos formatos de arquivo, como JPEG, TIFF, RIFF e WAV. O Exif armazena metadados como pares de um nome de metadados e um valor de metadados. Esses pares de nome-valor de metadados também são chamados de tags, para não serem confundidos com a marcação em [!DNL Experience Manager]. Como a Exif é criada automaticamente por câmeras digitais modernas e é suportada por software de gráficos modernos, ela pode ser vista como o menor denominador comum para o gerenciamento de metadados.

Uma grande limitação do Exif é que alguns formatos de arquivo de imagem populares, como BMP, GIF ou PNG, não são compatíveis.

Os campos de metadados normalmente definidos pela Exif são de natureza técnica e são de uso limitado para o gerenciamento descritivo de metadados. Por esse motivo, o [!DNL Experience Manager Assets] oferta mapeia as propriedades Exif em esquemas [de metadados](metadata-schemas.md) comuns e em [XMP](xmp-writeback.md).

### Outros metadados {#other-metadata}

Outros metadados que podem ser incorporados de arquivos incluem Microsoft Word, PowerPoint, Excel e assim por diante.

## Esquemas de metadados {#metadata-schemata}

Os schemas de metadados são conjuntos predefinidos de definições de propriedade de metadados que podem ser usados em vários aplicativos. As propriedades estão sempre associadas a um ativo, o que significa que as propriedades são &#39;sobre&#39; o recurso.

Você também pode projetar seus próprios esquemas de metadados se não houver nenhum que atenda às suas necessidades. Não duplicado informações existentes. Em uma organização, a separação de esquemas facilita o compartilhamento de metadados. [!DNL Experience Manager] fornece uma lista padrão dos esquemas de metadados mais populares. A lista ajuda você a iniciar rapidamente sua estratégia de metadados e a escolher rapidamente as propriedades de metadados de que você precisa.

Os esquemas de metadados suportados estão listados abaixo.

### Metadados padronizados {#standard-metadata}

* DC - [!DNL Dublin Core] é um conjunto importante e amplamente utilizado de metadados.
* DICOM - Digital Imaging and Communications in Medicine (Imagem digital e comunicações em medicina).
* Iptc4xmpCore &amp; iptc4xmpExt - International Press Communications Standard contém muitos metadados específicos para cada assunto.
* rdf - Estrutura de Descrição do Recurso - para metadados semânticos genéricos da Web.
* xmp - [!DNL Extensible Metadata Platform].
* xmpBJ - Ingresso no serviço básico.

### Metadados específicos do aplicativo {#application-specific-metadata}

Os metadados específicos do aplicativo incluem metadados técnicos e descritivos. Se você os usar, outros aplicativos talvez não consigam usar os metadados. Por exemplo, se você tiver um ativo com [!DNL Adobe Photoshop] metadados e outro aplicativo de renderização de imagem tentar acessar os metadados, talvez ele não consiga acessar os metadados. Se você descobrir que tem muitos metadados específicos do aplicativo em seus ativos, poderá criar uma etapa de fluxo de trabalho que altera uma propriedade específica do aplicativo para uma propriedade padrão.

* ACDSee - Metadados gerenciados pelo [!DNL ACDSee] programa. Consulte [www.acdsee.com/](https://www.acdsee.com/).
* Álbum - [!DNL Adobe Photoshop Album].
* CQ - Usado por [!DNL Experience Manager Assets].
* DAM - Usado por [!DNL Experience Manager Assets].
* DEX - [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html) é uma coleção de ferramentas para gerenciamento de metadados e arquivos para sistemas operacionais Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto &amp; MP - Microsoft Photo.
* PDF e PDF/X.
* Photoshop e psAux - [!DNL Adobe Photoshop].

### Metadados do Gerenciamento de direitos digitais {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - Sistema [Universal de Licenciamento de](https://www.useplus.com)Imagens.
* PRISM - Requisitos de [publicação para metadados](https://www.idealliance.org/prism-metadata)padrão do setor.
* PRL - Idioma dos Direitos do PRISM.
* PUR - Direitos de uso do PRISM.
* `xmpPlus` - Integração da PLUS com a XMP.

### Metadados específicos da fotografia {#photography-specific-metadata}

* Exif - Informações técnicas da câmera, incluindo a posição GPS.
* CRS - [!DNL Camera Raw] schema.
* `iptc4xmpCore` e `iptc4xmpExt`.
* TIFF - metadados de imagem (não apenas para imagens TIFF).

### Metadados específicos para impressão {#print-specific-metadata}

* PDF e PDF/X - Adobe PDF e aplicativos de terceiros.
* PRISM - [www.prismstandard.org](https://www.prismstandard.org) de publicação da DPS para metadados padrão do setor.
* XMP.
* `xmpPG` - Metadados XMP para texto paginado.

### Metadados específicos de multimídia {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gerenciamento de mídia.

## workflows orientados por metadados {#metadata-driven-workflows}

A criação de workflows orientados por metadados ajuda a automatizar alguns processos, o que aumenta a eficiência. Em um fluxo de trabalho controlado por metadados, o sistema de gerenciamento de fluxo de trabalho lê o fluxo de trabalho e, como resultado, executa alguma ação predefinida. Por exemplo, algumas maneiras de usar workflows orientados por metadados:

* O fluxo de trabalho pode verificar se uma imagem tem um título ou não. Caso contrário, o sistema notifica para adicionar um título.
* O fluxo de trabalho pode verificar se um aviso de direitos autorais em um ativo permite distribuição ou não. Assim, o sistema envia o ativo para um servidor ou outro.
* Um fluxo de trabalho pode verificar ativos sem metadados obrigatórios e predefinidos ou ativos com metadados *inválidos* .
