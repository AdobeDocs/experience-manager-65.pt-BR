---
title: Gerenciar metadados para ativos digitais
description: Saiba mais sobre os tipos de metadados e como os ativos AEM ajudam a gerenciar metadados de ativos para facilitar a categorização e a organização de ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Manage metadata for digital assets {#managing-metadata-for-digital-assets}

O Adobe Experience Manager (AEM) Assets mantém metadados para cada ativo. Isso permite uma classificação e organização mais fáceis de ativos e ajuda as pessoas que estão procurando um ativo específico. Com a capacidade de extrair metadados de arquivos carregados para ativos AEM, o gerenciamento de metadados se integra ao fluxo de trabalho criativo. Com a capacidade de manter e gerenciar metadados arbitrários com seus ativos, os ativos AEM permitem organizar e processar automaticamente ativos com base em seus metadados.

* [Metadados XMP](xmp.md)
* [Como editar ou adicionar metadados](meta-edit.md)
* [Referência dos esquemas de metadados](meta-ref.md)

## Por que precisamos de metadados {#why-we-need-metadata}

Metadados significa dados sobre dados. Nesse sentido, os dados se referem ao ativo que você está lidando, por exemplo, uma imagem. Os metadados são importantes porque permitem que os usuários gerenciem ativos com mais eficiência.

Metadados é a coleção de todos os dados disponíveis para esta imagem, mas isso não está necessariamente contido nessa imagem, por exemplo:

* o nome do ativo
* a data e hora da última modificação
* o tamanho da imagem conforme ela foi armazenada no repositório
* o nome da pasta em que está contido

Essas são as propriedades básicas de metadados que o AEM pode gerenciar para ativos, o que permite que os usuários vejam todos os ativos, por exemplo, solicitados pela última data de modificação - úteis ao tentar descobrir quais ativos foram adicionados recentemente ao repositório.

Você pode adicionar mais dados de alto nível a ativos digitais, por exemplo:

* o tipo de ativo (é uma imagem, um vídeo, um clipe de áudio ou um documento?)
* o proprietário do ativo
* o título do ativo
* a descrição do ativo
* as tags que foram atribuídas a um ativo

Mais metadados ajudam a categorizar ativos e são úteis à medida que a quantidade de informações digitais cresce. Embora seja possível para uma única pessoa gerenciar uma lista de algumas centenas de arquivos simplesmente com base em seus nomes de arquivo, essa abordagem fica aquém do número de pessoas envolvidas e o número de ativos gerenciados cresce.

À medida que os metadados são adicionados aos ativos, o valor do ativo cresce, pois o ativo se torna

* mais acessível - as pessoas podem achar muito mais fácil
* fácil de gerenciar - você pode encontrar ativos com o mesmo conjunto de propriedades mais facilmente e aplicar alterações a eles
* mais complexo - quanto mais metadados forem adicionados a um ativo, mais importantes serão os metadados de gerenciamento

Por esses motivos, o AEM Assets fornece os meios certos para criar, gerenciar e trocar metadados para seus ativos digitais.

## Noções básicas sobre metadados {#metadata-basics}

Os metadados são extraídos dos ativos quando são importados (assimilados). Além disso, adicionar metadados ajuda a categorizar ativos ainda mais.

Esta seção aborda os tipos de metadados e padrões de codificação.

### Tipos de metadados {#types-of-metadata}

Há dois tipos básicos de metadados:

* metadados técnicos
* metadados descritivos

#### Metadados técnicos {#technical-metadata}

Os metadados técnicos são úteis para aplicativos de software que lidam com ativos digitais e não devem ser mantidos manualmente. Os metadados técnicos podem ser determinados automaticamente pelos ativos AEM e outros softwares e podem mudar quando o ativo é modificado. Os metadados técnicos disponíveis de um ativo dependem em grande parte do tipo de arquivo do ativo. Os exemplos de metadados técnicos são os seguintes:

* o tamanho de um arquivo
* as dimensões (altura e largura) de uma imagem
* a taxa de bits de um arquivo de áudio ou vídeo
* a resolução (nível de detalhes) de uma imagem

#### Metadados descritivos {#descriptive-metadata}

Metadados descritivos são metadados relacionados ao domínio do aplicativo, por exemplo, o negócio de onde um ativo vem. Metadados descritivos não podem ser determinados automaticamente. Ela deve ser criada manual ou semiautomaticamente. Por exemplo, uma câmera habilitada para GPS pode rastrear automaticamente a latitude e a longitude de uma imagem capturada e adicionar essas informações aos metadados da imagem.

Devido ao alto custo do esforço manual necessário para criar informações descritivas de metadados, foram estabelecidos padrões para facilitar a troca de metadados entre sistemas de software e organizações.

O AEM Assets suporta todos os padrões relevantes para o gerenciamento de metadados.

Devido à importância dos metadados e ao alto envolvimento manual necessário para criar metadados, foram estabelecidas normas que facilitam o intercâmbio.

### Padrões de codificação {#encoding-standards}

Há várias maneiras de incorporar metadados aos arquivos. Há suporte para uma seleção de padrões de codificação:

* XMP: usado pelo AEM Assets para armazenar os metadados extraídos no repositório.
* ID3: para arquivos de áudio e vídeo.
* EXIF: para arquivos de imagem.
* Outro/Legado: do Microsoft Word, PowerPoint, Excel e assim por diante.

#### XMP {#xmp}

XMP significa Plataforma de metadados extensível e é o padrão de metadados usado pelo AEM Assets para todo o gerenciamento de metadados. Além de oferecer codificação de metadados universais que podem ser incorporados em todos os formatos de arquivo, o XMP fornece um modelo de conteúdo avançado e é suportado pela Adobe e por outras empresas, de modo que os usuários do XMP em combinação com os ativos AEM tenham uma plataforma poderosa para desenvolver.

#### ID3 {#id}

Os dados armazenados nessas tags ID3 são exibidos quando você reproduz um arquivo de áudio digital em seu computador ou em um player MP3 portátil.

As tags ID3 foram projetadas para o formato de arquivo MP3. Informações adicionais sobre formatos:

* As tags ID3 funcionam em arquivos MP3 e MP3pro.
* WAV não tem tags.
* O WMA tem tags proprietárias que não permitem a implementação de código aberto.
* Ogg Vorbis usa Comentários Xiph incorporados no contêiner Ogg.
* O AAC usa um formato de marcação proprietário.

#### EXIF {#exif}

EXIF significa o formato de arquivo de imagem permutável e é o formato de metadados mais popular usado na fotografia digital. Ele fornece uma maneira de incorporar um vocabulário fixo de propriedades de metadados em vários formatos de arquivo, como JPEG, TIFF, RIFF e WAV.

Uma grande limitação do EXIF é que ele não é suportado por outros formatos de arquivo de imagem populares, como BMP, GIF ou PNG.

O EXIF armazena metadados como pares de um nome de metadados e um valor de metadados. Esses pares de nome-valor de metadados também são chamados de tags, não devem ser confundidos com a marcação no AEM.

Como o EXIF é criado automaticamente por câmeras digitais modernas e suportado por software de gráficos modernos, ele pode ser visto como o menor denominador comum para o gerenciamento de metadados.

A maioria dos campos de metadados definidos pelo EXIF são de natureza altamente técnica e de uso limitado para o gerenciamento descritivo de metadados. Por esse motivo, o AEM Assets oferece o mapeamento de propriedades EXIF em esquemas [de metadados](metadata-schemas.md) comuns e em [XMP](xmp-writeback.md), o formato de metadados avançado que o AEM Assets usa para gerenciamento de metadados.

#### Outros metadados {#other-metadata}

Outros metadados que podem ser incorporados de arquivos incluem Microsoft Word, PowerPoint, Excel e assim por diante.

## Esquema de metadados {#metadata-schemata}

Os esquemas de metadados são conjuntos predefinidos de definições de propriedade de metadados que podem ser usados em diversos aplicativos. As propriedades estão sempre associadas a um ativo, o que significa que as propriedades são sobre o recurso.

Você também pode projetar seus próprios esquemas de metadados se não houver nenhum que atenda às suas necessidades (tenha cuidado, no entanto, para não duplicar algo que já existe). Em uma organização, a separação de esquemas facilita o compartilhamento de metadados entre organizações.

O AEM fornece uma lista pronta dos esquemas de metadados mais populares, permitindo que você inicie rapidamente sua estratégia de metadados e escolha as propriedades de metadados de que você precisa em um esquema já definido.

Os esquemas de metadados suportados estão listados na seção a seguir.

### Metadados padrão {#standard-metadata}

* dc - Dublin Core - o conjunto de metadados mais importante e amplamente utilizado
* DICOM - Imagens digitais e comunicações na medicina
* Iptc4xmpCore &amp; iptc4xmpExt - International Press Communications Standard - muitos metadados específicos do assunto
* rdf - Estrutura de Descrição de Recurso - para metadados web semânticos genéricos
* xmp - Plataforma extensível de metadados
* xmpBJ - Ingresso no serviço básico

### Metadados específicos do aplicativo {#application-specific-metadata}

>[!NOTE]
>
>Metadados específicos do aplicativo incluem metadados técnicos e descritivos. Se você os usar, outros aplicativos talvez não consigam usar os metadados. Por exemplo, se você tiver um ativo com metadados do Adobe Photoshop e outro aplicativo de renderização de imagem tentar acessar os metadados, talvez ele não consiga.
>
>Se você descobrir que tem muitos metadados específicos do aplicativo em seus ativos, poderá criar uma etapa de fluxo de trabalho que altera a propriedade específica do aplicativo para uma padrão.

* acdsee - metadados gerenciados pelo programa ACDSee [www.acdsee.com/](https://www.acdsee.com/)
* álbum - Adobe Photoshop Album
* cq - usado pelo AEM Assets
* dam - usado pelo AEM Assets
* dex - Optima SC Description Explorer
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - IView MediaPro
* MicrosoftPhoto e MP - Microsoft Photo
* pdf amd pdfx
* photoshop &amp; psAux - Adobe Photoshop

### Metadados do gerenciamento de direitos digitais {#digital-rights-management-metadata}

* cc - creative commons
* xmpRights
* mais - Sistema Universal de Licenciamento de Imagens - https://www.useplus.com/
* prisma - https://www.idealliance.org/prism-metadata de publicação da DPS para metadados padrão do setor
* prl - Idioma dos Direitos da Prisma
* pur - Direitos de uso de prisioneiros
* xmpPlus - integração de PLUS com XMP

### Metadados específicos para fotografia {#photography-specific-metadata}

* exif - muitas informações técnicas da câmera, incluindo a posição GPS
* crs - Photoshop camera raw
* Iptc4xmpCore e iptc4xmpExt
* TIFF - metadados de imagem (não apenas para imagens TIFF)

### Metadados específicos para impressão {#print-specific-metadata}

* pdf e pdfx - Adobe PDF e aplicativos de terceiros
* prisma - [www.prismstandard.org](https://www.prismstandard.org) de publicação da DPS para metadados padrão do setor
* xmp
* xmpPG - xmp para texto paginado

### Metadados específicos de multimídia {#multimedia-specific-metadata}

* xmpDM - Dynamic Media
* xmpMM - Gerenciamento de mídia

## Fluxos de trabalho orientados por metadados {#metadata-driven-workflows}

A criação de fluxos de trabalho orientados por metadados ajuda a automatizar alguns processos, o que aumenta a eficiência. Em um fluxo de trabalho controlado por metadados, o sistema de gerenciamento de fluxo de trabalho lê o fluxo de trabalho e, como resultado, executa alguma ação predefinida.

Por exemplo, algumas maneiras de usar fluxos de trabalho orientados por metadados:

* O fluxo de trabalho pode verificar se uma imagem tem um título. Caso contrário, o sistema notifica um usuário específico para adicionar um título.
* O fluxo de trabalho pode verificar se um aviso de direitos autorais em um ativo permite a distribuição. Se isso ocorrer, o sistema enviará o ativo para um servidor. Caso contrário, o sistema enviará o ativo para outro servidor.
