---
title: Compreender conceitos de metadados
description: Saiba mais sobre a necessidade e os tipos de metadados que permitem uma classificação e organização mais fáceis dos ativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: ce43c49f8f7d4509e414554b8f4eba368ff66e95
workflow-type: tm+mt
source-wordcount: '2732'
ht-degree: 6%

---


# Compreender conceitos de metadados {#why-we-need-metadata}

Metadados significa dados sobre dados. Nesse sentido, os dados se referem ao seu ativo digital, digamos uma imagem. Os metadados são essenciais para o gerenciamento eficiente de ativos.

Metadados é a coleta de todos os dados disponíveis para um ativo, mas não necessariamente contidos nessa imagem. Alguns exemplos de metadados são:

* Nome do ativo.
* Hora e data da última modificação.
* Tamanho do ativo conforme ele foi armazenado no repositório.
* Nome da pasta em que está contido.
* Ativos relacionados ou tags aplicadas.

As informações acima são as propriedades básicas de metadados que [!DNL Experience Manager] podem ser gerenciadas para ativos, o que permite que os usuários vejam todos os ativos. Por exemplo, ordenar ativos pela última data de modificação é útil ao tentar descobrir ativos adicionados recentemente.

Você pode adicionar mais dados de alto nível a ativos digitais, por exemplo:

* Tipo de ativo (é uma imagem, um vídeo, um clipe de áudio ou um documento?).
* Proprietário do ativo.
* Título do ativo.
* Descrição do ativo.
* Tags atribuídas a um ativo.

Mais metadados ajudam a categorizar ativos e são úteis à medida que a quantidade de informações digitais cresce. É possível gerenciar algumas centenas de arquivos com base apenas nos nomes dos arquivos. No entanto, essa abordagem não é escalável. Fica aquém quando o número de pessoas envolvidas e o número de ativos gerenciados aumenta.

Com a adição de metadados, o valor de um ativo digital cresce, pois o ativo se torna,

* Mais acessível - os sistemas e usuários podem encontrá-lo facilmente.
* Mais fácil de gerenciar - você pode encontrar ativos com o mesmo conjunto de propriedades mais facilmente e aplicar alterações a eles.
* Concluído - o ativo traz mais informações e contexto com mais metadados.

Por esses motivos, [!DNL Assets] fornece os meios certos de criar, gerenciar e trocar metadados para seus ativos digitais.

## Tipos de metadados {#types-of-metadata}

Os dois tipos básicos de metadados são metadados técnicos e metadados descritivos.

Os metadados técnicos são úteis para aplicativos de software que lidam com ativos digitais e não devem ser mantidos manualmente. [!DNL Experience Manager Assets] e outros softwares determinam automaticamente os metadados técnicos e os metadados podem mudar quando o ativo é modificado. Os metadados técnicos disponíveis de um ativo dependem em grande parte do tipo de arquivo do ativo. Alguns exemplos de metadados técnicos são:

* Tamanho de um arquivo.
* Dimension (altura e largura) de uma imagem.
* Taxa de bits de um arquivo de áudio ou vídeo.
* Resolução (nível de detalhes) de uma imagem.

Metadados descritivos são metadados relacionados ao domínio do aplicativo, por exemplo, o negócio de onde um ativo vem. Metadados descritivos não podem ser determinados automaticamente. É criado manual ou semiautomaticamente. Por exemplo, uma câmera habilitada para GPS pode rastrear automaticamente a latitude e a longitude e adicionar geolocalização da imagem.

O custo da criação manual de informações descritivas de metadados é alto. Assim, os padrões são estabelecidos para facilitar a troca de metadados entre sistemas de software e organizações. [!DNL Experience Manager Assets] oferece suporte a todas as normas relevantes para o gerenciamento de metadados.

## Padrões de codificação {#encoding-standards}

Há várias maneiras de incorporar metadados em arquivos. Há suporte para uma seleção de padrões de codificação:

* XMP: usado por [!DNL Assets] para armazenar os metadados extraídos no repositório.
* ID3: para arquivos de áudio e vídeo.
* Exif: para arquivos de imagem.
* Outro/Legado: de [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]e assim por diante.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) é um padrão aberto usado por [!DNL Experience Manager Assets] todos os gerenciamento de metadados. A codificação padrão de metadados universais do oferta que pode ser incorporada em todos os formatos de arquivo. Adobe e outras empresas oferecem suporte XMP padrão, pois oferecem um modelo de conteúdo avançado. Os usuários XMP padrão e de [!DNL Experience Manager Assets] uma plataforma poderosa para aproveitar. For more information, see [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Os dados armazenados nessas tags ID3 são exibidos quando você reproduz um arquivo de áudio digital em seu computador ou em um player MP3 portátil.

As tags ID3 foram projetadas para o formato de arquivo MP3. Informações adicionais sobre formatos:

* As tags ID3 funcionam em arquivos MP3 e mp3PRO.
* WAV não tem tags.
* O WMA tem tags proprietárias que não permitem a implementação de código aberto.
* Ogg Vorbis usa Comentários Xiph incorporados ao container Ogg.
* O AAC usa um formato de marcação proprietário.

### Exif {#exif}

O formato de arquivo de imagem permutável (Exif) é o formato de metadados mais popular usado na fotografia digital. Ele fornece uma maneira de incorporar um vocabulário fixo de propriedades de metadados em muitos formatos de arquivo, como JPEG, TIFF, RIFF e WAV. O Exif armazena metadados como pares de um nome de metadados e um valor de metadados. Esses pares de nome-valor de metadados também são chamados de tags, para não serem confundidos com a marcação em [!DNL Experience Manager]. As câmeras digitais modernas criam metadados Exif e softwares gráficos modernos suportam isso. O formato Exif é o menor denominador comum para o gerenciamento de metadados, especialmente para imagens.

Uma grande limitação do Exif é que alguns formatos de arquivo de imagem populares, como BMP, GIF ou PNG, não são compatíveis.

Os campos de metadados definidos pela Exif são tipicamente de natureza técnica e têm uso limitado para o gerenciamento descritivo de metadados. Por esse motivo, o [!DNL Experience Manager Assets] oferta mapeia as propriedades Exif em esquemas [de metadados](metadata-schemas.md) comuns e em [XMP](xmp-writeback.md).

### Outros metadados {#other-metadata}

Outros metadados que podem ser incorporados de arquivos incluem [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]etc.

## Entender os esquemas de metadados {#metadata-schemata}

Os schemas de metadados são conjuntos predefinidos de definições de propriedade de metadados que podem ser usados em vários aplicativos. As propriedades estão sempre associadas a um ativo, o que significa que as propriedades são &#39;sobre&#39; o recurso.

Você também pode projetar seus próprios esquemas de metadados se não houver nenhum que atenda às suas necessidades. Não duplicado informações existentes. Em uma organização, a separação de esquemas facilita o compartilhamento de metadados. [!DNL Experience Manager] fornece uma lista padrão dos esquemas de metadados mais populares. A lista ajuda você a iniciar rapidamente sua estratégia de metadados e a escolher rapidamente as propriedades de metadados de que você precisa.

Os esquemas de metadados suportados estão listados abaixo.

### Metadados padronizados {#standard-metadata}

* DC - [!DNL Dublin Core] é um conjunto importante e amplamente utilizado de metadados.
* DICOM - Digital Imaging and Communications in Medicine (Imagem digital e comunicações em medicina).
* `Iptc4xmpCore` e `iptc4xmpExt` - O International Press Communications Standard contém muitos metadados específicos para cada assunto.
* RDF - Estrutura de Descrição do Recurso - para metadados semânticos genéricos da Web.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Ingresso no Serviço Básico.

### Metadados específicos do aplicativo {#application-specific-metadata}

Os metadados específicos do aplicativo incluem metadados técnicos e descritivos. Se você usar esses metadados, outros aplicativos talvez não consigam usá-los. Por exemplo, um aplicativo de renderização de imagem diferente pode não conseguir acessar [!DNL Adobe Photoshop] metadados. Você pode criar uma etapa de fluxo de trabalho que altera uma propriedade específica do aplicativo para uma propriedade padrão.

* ACDSee - Metadados gerenciados pelo [!DNL ACDSee] programa. Consulte [www.acdsee.com/](https://www.acdsee.com/).
* Álbum - [!DNL Adobe Photoshop Album].
* CQ - Usado por [!DNL Experience Manager Assets].
* DAM - Usado por [!DNL Experience Manager Assets].
* DEX - [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html) é uma coleção de ferramentas para gerenciamento de metadados e arquivos para sistemas operacionais Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto e MP - Microsoft Photo.
* PDF e PDF/X.
* Photoshop e psAux - [!DNL Adobe Photoshop].

### Metadados de Digital Rights Management (DRM) {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - Sistema [Universal de Licenciamento de](https://www.useplus.com)Imagens.
* PRISM - Requisitos de [publicação para metadados](https://www.idealliance.org/prism-metadata)padrão do setor.
* PRL - Idioma dos Direitos do PRISM.
* PUR - Direitos de uso do PRISM.
* `xmpPlus` - Integração do PLUS com o XMP.

### Metadados específicos da fotografia {#photography-specific-metadata}

* Exif - Informações técnicas da câmera, incluindo a posição GPS.
* CRS - [!DNL Camera Raw] schema.
* `iptc4xmpCore` e `iptc4xmpExt`.
* TIFF - metadados de imagem (não apenas para imagens TIFF).

### Metadados específicos para impressão {#print-specific-metadata}

* PDF e PDF/X - Adobe PDF e aplicativos de terceiros.
* PRISM - Requisitos de [publicação para metadados](https://www.idealliance.org/prism-metadata)padrão do setor.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - XMP metadados para texto paginado.

### Metadados específicos de multimídia {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gerenciamento de mídia.

## Referência dos esquemas de metadados {#metadata-schemata-reference}

A referência a seguir inclui informações sobre esquemas de metadados específicos (em ordem alfabética), bem como uma lista de propriedades e suas definições.

### Dublin Core {#dublin-core}

Os metadados do Dublin Core fornecem um conjunto padronizado de convenções para descrever ativos para facilitar sua localização. Em [!DNL Assets]Dublin Core descreve os ativos digitais, incluindo vídeo, som, imagens e documentos.

O conjunto simples de elementos de metadados principais de Dublin (DCMES) contém 15 elementos de metadados, conforme listados na tabela a seguir. Cada elemento de Dublin Core é opcional e pode ser repetido. Você pode adicionar ou excluir informações de metadados do Dublin Core como faria para metadados específicos de tipos de mídia.

Além do DCMES, existem outros elementos de metadados criados pela iniciativa Dublin Core. Para mais informações, consultar a iniciativa [](https://dublincore.org/) Dublin Core.

| Propriedade | Descrição |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| contribuinte | A pessoa ou empresa responsável por contribuir para o conteúdo. |
| cobertura | A localização geográfica ou o período de tempo que o ativo cobre. |
| criadora | A pessoa ou empresa responsável pela criação do conteúdo. |
| date | Data ou período associado ao ativo. |
| descrição | Mais informações sobre o ativo. |
| format | O formato de arquivo, a mídia física ou as dimensões do ativo. [!DNL Experience Manager] usa `dc:format` para indicar o tipo MIME do ativo. |
| identifier | Uma referência exclusiva ao ativo. |
| language | O idioma do ativo (por exemplo, en para inglês). |
| editor | A pessoa ou empresa responsável por disponibilizar o ativo. |
| relation | Um ativo relacionado. |
| direitos | Informações sobre quem tem os direitos a este ativo. |
| source | Um ativo relacionado do qual o ativo é derivado. |
| assunto | O tópico do ativo. |
| título | Um nome para o ativo. |
| tipo | A natureza ou o gênero do ativo. |

### IPTC {#iptc}

O International Press Telecommunications Council (IPTC) é um consórcio de agências de notícias ao redor do mundo - um de seus objetivos é desenvolver e manter padrões técnicos. O IPTC definiu um conjunto de padrões de metadados de fotos para imagens que são aceitos quase universalmente pelos fotógrafos. Esses padrões de metadados faziam parte do padrão mais amplo conhecido como IPTC Information Interchange Model (IIM), criado nos anos 90.

Embora as informações do cabeçalho IPTC tenham sido substituídas principalmente por XMP, um schema principal IPTC e um schema de extensão estão disponíveis para XMP. Em programas de imagem, as propriedades XMP e IPTC são sincronizadas.

## Workflows orientados por metadados {#metadata-driven-workflows}

A criação de workflows orientados por metadados ajuda a automatizar alguns processos, o que aumenta a eficiência. Em um fluxo de trabalho controlado por metadados, o sistema de gerenciamento de fluxo de trabalho lê o fluxo de trabalho e, como resultado, executa alguma ação predefinida. Por exemplo, algumas maneiras de usar workflows orientados por metadados:

* O fluxo de trabalho pode verificar se uma imagem tem um título ou não. Caso contrário, o sistema notifica para adicionar um título.
* O fluxo de trabalho pode verificar se um aviso de direitos autorais em um ativo permite distribuição ou não. Portanto, o sistema envia o ativo para um servidor ou outro.
* Um fluxo de trabalho pode verificar ativos sem metadados obrigatórios e predefinidos ou ativos com metadados *inválidos* .

## Metadados XMP {#xmp-metadata}

XMP (Plataforma extensível de metadados) é o padrão de metadados usado por todos [!DNL Adobe Experience Manager Assets] os gerenciamento de metadados. XMP fornece um formato padrão para a criação, o processamento e o intercâmbio de metadados para uma grande variedade de aplicativos.

Além de oferecer codificação de metadados universais que podem ser incorporados em todos os formatos de arquivo, XMP fornece um modelo [de](#xmp-core-concepts) conteúdo avançado e é [suportado pelo Adobe](#advantages-of-xmp) e outras empresas, para que os usuários de XMP em combinação com [!DNL Assets] uma plataforma poderosa para desenvolver.

A especificação [](https://www.adobe.com/devnet/xmp.html) XMP está disponível no Adobe.

### O que é XMP? {#what-is-xmp}

O Adobe introduziu o padrão XMP pela primeira vez como parte do produto de software Adobe Acrobat. Desde então, a norma XMP tem sido amplamente adotada. [!DNL Assets] suporta nativamente o XMP - a Plataforma de Metadados Extensível liderada pelo Adobe. XMP é um padrão para processamento e armazenamento de metadados padronizados e proprietários em ativos digitais. XMP é projetado para ser o padrão comum que permite que vários aplicativos trabalhem com metadados de forma eficaz.

Os profissionais de produção, por exemplo, usam o suporte integrado XMP nos aplicativos Adobe para transmitir informações em vários formatos de arquivo. [!DNL Assets] O repositório extrai os metadados XMP e os usa para gerenciar o ciclo de vida do conteúdo e oferta a capacidade de criar workflows de automação.

XMP padroniza como os metadados são definidos, criados e processados fornecendo um modelo de dados, um modelo de armazenamento e schemas. Todos estes conceitos são abordados nesta seção.

Todos os metadados herdados do EXIF, ID3 ou Microsoft Office são traduzidos automaticamente para XMP, que podem ser estendidos para suportar schemas de metadados específicos do cliente, como catálogos de produtos.

Os metadados no XMP consistem em um conjunto de propriedades. Estas propriedades estão sempre associadas a uma entidade específica, designada por recurso; ou seja, as propriedades são &quot;sobre&quot; o recurso. No caso de XMP, o recurso é sempre o ativo.

### XMP ecossistema {#xmp-ecosystem}

O XMP define um modelo de [metadados](https://pt.wikipedia.org/wiki/Metadados) que pode ser usado com qualquer conjunto definido de itens de metadados. O XMP também define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos de propriedades básicas úteis para gravar o histórico de um recurso à medida que ele passa por várias etapas de processamento, de ser fotografado, [digitalizado](https://pt.wikipedia.org/wiki/Digitalizador) ou criado como texto, até etapas de edição de fotos (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) ou ajuste de cor), para montagem em uma imagem final. O XMP permite que cada programa de software ou dispositivo ao longo do caminho adicione suas próprias informações a um recurso digital, que pode ser retido no arquivo digital final.

O XMP geralmente é serializado e armazenado usando um subconjunto do [W3C](https://pt.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://pt.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que por sua vez é expresso em [XML](https://pt.wikipedia.org/wiki/XML).

### Vantagens do XMP {#advantages-of-xmp}

XMP tem as seguintes vantagens sobre outros padrões e esquemas de codificação:

* Metadados baseados em XMP são muito potentes e de granulação fina.
* XMP permite que você tenha vários valores para uma propriedade.
* XMP tem codificação padronizada, que permite a troca fácil de metadados.
* XMP é extensível. Você pode adicionar informações adicionais aos ativos.

O padrão XMP foi projetado para ser extensível, permitindo que você adicione tipos personalizados de metadados aos dados XMP. O EXIF, por outro lado, não - tem uma lista fixa de propriedades que não podem ser estendidas.

>[!NOTE]
>
>XMP geralmente não permite a incorporação de tipos de dados binários. Para carregar dados binários em XMP, por exemplo, imagens em miniatura, eles devem ser codificados em um formato compatível com XML, como `Base64`.

### XMP conceitos {#xmp-core-concepts}

As seções a seguir descrevem os conceitos principais de XMP, incluindo namespaces e esquemas, propriedades e valores e alternativas de idioma.

#### Namespaces e esquemas {#namespaces-and-schemata}

Um schema XMP é um conjunto de nomes de propriedade em uma namespace XML comum que inclui o tipo de dados e as informações descritivas. Um schema XMP é identificado por seu URI de namespace XML. O uso do namespace evita conflitos entre propriedades em schemas diferentes que tenham o mesmo nome, mas um significado diferente.

Por exemplo, a `Creator` propriedade em dois schemas projetados independentemente pode significar a pessoa que criou o ativo ou pode significar o aplicativo que criou o ativo (por exemplo, Adobe Photoshop).

#### Propriedades e valores {#properties-and-values}

XMP pode incluir propriedades de um ou mais schemas. Por exemplo, um subconjunto típico usado por muitos aplicativos Adobe pode incluir o seguinte:

* Schema principal de Dublin: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* XMP schema básico: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* schema de gerenciamento de direitos XMP: `xmpRights:WebStatement`, `xmpRights:Marked`.
* schema de gerenciamento de mídia XMP: `xmpMM:DocumentID`.

#### Alternativas linguísticas {#language-alternatives}

XMP permite que você adicione uma `xml:lang` propriedade às propriedades de texto para especificar o idioma do texto.

## Trabalhar com metadados IPTC {#support-for-iptc-metadata}

Saiba como [!DNL Adobe Experience Manager Assets] suporta os metadados IPTC, as avaliações criativas e as palavras-chave adicionadas aos ativos por meio [!DNL Adobe Bridge] de outros [!DNL Adobe Creative Cloud] aplicativos.

[!DNL Adobe Experience Manager Assets] suporta o padrão de metadados IPTC amplamente usado para descrever ativos. Dessa forma, [!DNL Assets] aprimora a aceitação de suas imagens entre vários partidos, entre fotógrafos, agências de criação, bibliotecas, museus e assim por diante.

O schema de metadados padrão para ativos agora incorpora os schemas de metadados IPTC Core e IPTC Extension para definir propriedades abrangentes de metadados que permitem que os usuários adicionem dados precisos e confiáveis sobre pessoas, locais e produtos mostrados em uma imagem. Também oferece suporte a datas, nomes e identificadores relacionados à criação da imagem, além de uma maneira flexível de expressar informações de direitos.

A página Propriedades dos ativos agora inclui guias separadas para exibir os metadados IPTC Core e IPTC Extension em campos editáveis.

1. Na interface do [!DNL Assets] usuário, selecione uma imagem.
1. Click **[!UICONTROL Properties]** from the toolbar.
1. Clique na guia **[!UICONTROL IPTC]** para visualização dos metadados IPTC do ativo.
1. Edite as propriedades de metadados IPTC, conforme necessário.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Click the **[!UICONTROL IPTC Extension]** tab to view IPTC Extension metadata for the asset.
1. Edite as propriedades de metadados da extensão IPTC, conforme necessário.
1. Click **[!UICONTROL Save &amp; Close]** to save the changes.

### Suporte a classificação criativa {#creative-rating-support}

Além de exibir classificações individuais de usuários e classificações de agregação, a página Propriedades agora exibe as classificações atribuídas aos ativos por meio do Adobe Bridge e de outros aplicativos criativos

Essas classificações estão disponíveis na seção **[!UICONTROL Classificação criativa]**, na guia **[!UICONTROL Avançado]**.

Essa classificação é uma propriedade somente leitura e varia entre 1 e 5. Você pode pesquisar ativos com base em sua Classificação criativa no Painel de pesquisa.

No entanto, essa propriedade não está indexada no momento para evitar conflitos com as alterações personalizadas feitas pelos usuários.

### Suporte a palavra-chave {#keyword-support}

A guia **[!UICONTROL IPTC]** da página [!UICONTROL Propriedades] também exibe palavras-chave adicionadas aos ativos por meio do Adobe Bridge e de outros aplicativos Adobe Creative Cloud. Você também pode editar essas palavras-chave e adicionar mais palavras-chave na guia **[!UICONTROL IPTC]** .

![keywords](assets/keywords-in-iptc-tab.png)
