---
title: Entender os conceitos de metadados
description: Saiba mais sobre a necessidade e os tipos de metadados que permitem classificar e organizar facilmente os ativos.
contentOwner: AG
role: User, Admin
feature: Metadados
exl-id: 312fff5f-39c1-48c1-aa99-40feb72c2f59
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '2730'
ht-degree: 6%

---

# Entender os conceitos de metadados {#why-we-need-metadata}

Metadados significa dados sobre dados. Nesse sentido, os dados se referem ao seu ativo digital, digamos uma imagem. Os metadados são essenciais para um gerenciamento eficiente de ativos.

Metadados é a coleção de todos os dados disponíveis para um ativo, mas que não estão necessariamente contidos nessa imagem. Alguns exemplos de metadados são:

* Nome do ativo.
* Hora e data da última modificação.
* Tamanho do ativo como ele foi armazenado no repositório.
* Nome da pasta na qual ele está contido.
* Ativos relacionados ou tags aplicadas.

As informações acima são as propriedades básicas de metadados que [!DNL Experience Manager] pode gerenciar para ativos, o que permite que os usuários vejam todos os ativos. Por exemplo, solicitar ativos pela última data de modificação é útil ao tentar descobrir ativos adicionados recentemente.

Você pode adicionar mais dados de alto nível aos ativos digitais, por exemplo:

* Tipo de ativo (uma imagem, um vídeo, um clipe de áudio ou um documento).
* Proprietário do ativo.
* Título do ativo.
* Descrição do ativo.
* Tags atribuídas a um ativo.

Mais metadados ajudam a categorizar ativos e são úteis à medida que a quantidade de informações digitais aumenta. É possível gerenciar algumas centenas de arquivos com base apenas nos nomes de arquivo. No entanto, essa abordagem não é escalável. Fica aquém do aumento do número de pessoas envolvidas e do número de ativos gerenciados.

Com a adição de metadados, o valor de um ativo digital cresce, porque o ativo se torna,

* Mais acessível - os sistemas e usuários podem encontrá-lo facilmente.
* Mais fácil de gerenciar: é possível encontrar ativos com o mesmo conjunto de propriedades mais facilmente e aplicar alterações a eles.
* Concluído - o ativo carrega mais informações e contexto com mais metadados.

Por esses motivos, [!DNL Assets] fornece o meio certo para criar, gerenciar e trocar metadados para seus ativos digitais.

## Tipos de metadados {#types-of-metadata}

Os dois tipos básicos de metadados são metadados técnicos e descritivos.

Os metadados técnicos são úteis para aplicativos de software que lidam com ativos digitais e não devem ser mantidos manualmente. [!DNL Experience Manager Assets] e outros softwares determinam automaticamente os metadados técnicos e podem mudar quando o ativo é modificado. Os metadados técnicos disponíveis de um ativo dependem principalmente do tipo de arquivo do ativo. Alguns exemplos de metadados técnicos são:

* Tamanho de um arquivo.
* Dimension (altura e largura) de uma imagem.
* Taxa de bits de um arquivo de áudio ou vídeo.
* Resolução (nível de detalhes) de uma imagem.

Os metadados descritivos são metadados relacionados ao domínio do aplicativo, por exemplo, o negócio de onde um ativo vem. Metadados descritivos não podem ser determinados automaticamente. Ele é criado manual ou semiautomaticamente. Por exemplo, uma câmera ativada por GPS pode rastrear automaticamente a latitude e a longitude e adicionar geotag à imagem.

O custo de criar manualmente informações de metadados descritivos é alto. Assim, os padrões são estabelecidos para facilitar a troca de metadados entre sistemas e organizações de software. [!DNL Experience Manager Assets] O suporta todas as normas relevantes para a gestão de metadados.

## Padrões de codificação {#encoding-standards}

Há várias maneiras de incorporar metadados em arquivos. Há suporte para uma seleção de padrões de codificação:

* XMP: usado por [!DNL Assets] para armazenar os metadados extraídos no repositório.
* ID3: para arquivos de áudio e vídeo.
* Exif: para arquivos de imagem.
* Outro/Legado: de [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel] e assim por diante.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) é um padrão aberto usado pelo  [!DNL Experience Manager Assets] para todo o gerenciamento de metadados. O padrão oferece codificação de metadados universais que podem ser incorporados em todos os formatos de arquivo. O Adobe e outras empresas oferecem suporte XMP padrão, pois fornece um modelo de conteúdo avançado. Os usuários XMP padrão e [!DNL Experience Manager Assets] têm uma plataforma poderosa para desenvolver. Para obter mais informações, consulte [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Os dados armazenados nessas tags ID3 são exibidos quando você reproduz um arquivo de áudio digital em seu computador ou em um player MP3 portátil.

As tags ID3 foram projetadas para o formato de arquivo MP3. Informações adicionais sobre formatos:

* As tags ID3 funcionam em arquivos MP3 e mp3PRO.
* O WAV não tem tags.
* O WMA tem tags proprietárias que não permitem implementação de código aberto.
* O Ogg Vorbis usa Comentários Xiph incorporados no contêiner Ogg.
* O AAC usa um formato de marcação proprietário.

### Exif {#exif}

O formato de arquivo de imagem permutável (Exif) é o formato de metadados mais popular usado em fotografia digital. Ele fornece uma maneira de incorporar um vocabulário fixo de propriedades de metadados em muitos formatos de arquivo, como JPEG, TIFF, RIFF e WAV. O Exif armazena metadados como pares de um nome de metadados e um valor de metadados. Esses pares nome-valor-metadados também são chamados de tags , não devem ser confundidos com a marcação em [!DNL Experience Manager]. Câmeras digitais modernas criam metadados Exif e softwares gráficos modernos suportam isso. O formato Exif é o menor denominador comum para o gerenciamento de metadados, especialmente para imagens.

Uma grande limitação do Exif é que alguns formatos de arquivo de imagem populares, como BMP, GIF ou PNG, não são compatíveis.

Os campos de metadados definidos pela Exif normalmente têm natureza técnica e são de uso limitado para o gerenciamento de metadados descritivos. Por esse motivo, [!DNL Experience Manager Assets] oferece mapeamento de propriedades Exif em [esquemas de metadados comuns](metadata-schemas.md) e em [XMP](xmp-writeback.md).

### Outros metadados {#other-metadata}

Outros metadados que podem ser incorporados de arquivos incluem [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], e assim por diante.

## Entender os esquemas de metadados {#metadata-schemata}

Os esquemas de metadados são conjuntos predefinidos de definições de propriedades de metadados que podem ser usadas em vários aplicativos. As propriedades são sempre associadas a um ativo, o que significa que as propriedades são &quot;sobre&quot; o recurso.

Você também pode criar seus próprios esquemas de metadados se não existir nenhum que atenda às suas necessidades. Não duplique as informações existentes. Em uma organização, separar esquemas facilita o compartilhamento de metadados. [!DNL Experience Manager] O fornece uma lista padrão dos esquemas de metadados mais populares. A lista ajuda você a iniciar rapidamente sua estratégia de metadados e escolher rapidamente as propriedades de metadados necessárias.

Os esquemas de metadados compatíveis estão listados abaixo.

### Metadados padrão {#standard-metadata}

* DC - [!DNL Dublin Core] é um conjunto de metadados importante e amplamente usado.
* DICOM - Digital Imaging and Communications in Medicine (Imagem digital e comunicações em medicina).
* `Iptc4xmpCore` e  `iptc4xmpExt` - O International Press Communications Standard contém muitos metadados específicos de assunto.
* RDF - Estrutura de Descrição do Recurso - para metadados semanticos da Web genéricos.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Bilhete básico de trabalho.

### Metadados específicos do aplicativo {#application-specific-metadata}

Os metadados específicos do aplicativo incluem metadados técnicos e descritivos. Se você usar esses metadados, outros aplicativos talvez não consigam usá-los. Por exemplo, um aplicativo de renderização de imagem diferente pode não conseguir acessar metadados [!DNL Adobe Photoshop]. Você pode criar uma etapa de fluxo de trabalho que altera uma propriedade específica do aplicativo para uma propriedade padrão.

* ACDSee - Metadados gerenciados pelo programa [!DNL ACDSee]. Consulte [www.acdsee.com/](https://www.acdsee.com/).
* Álbum - [!DNL Adobe Photoshop Album].
* CQ - Usado por [!DNL Experience Manager Assets].
* DAM - Usado por [!DNL Experience Manager Assets].
* DEX - [Optima SC Description Explorer](http://www.optimasc.com/products/dex/index.html) é uma coleção de ferramentas para metadados e gerenciamento de arquivos para sistemas operacionais Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto e MP - Microsoft Photo.
* PDF e PDF/X.
* Photoshop e psAux - [!DNL Adobe Photoshop].

### Metadados de Digital Rights Management (DRM) {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - [Sistema Universal de Licenciamento de Imagem](https://www.useplus.com).
* PRISM - [Requisitos de publicação para metadados padrão do setor](https://www.idealliance.org/prism-metadata).
* PRL - Linguagem de direitos PRISM.
* PUR - Direitos de uso do PRISM.
* `xmpPlus` - Integração da PLUS com a XMP.

### Metadados específicos da fotografia {#photography-specific-metadata}

* Exif - Informações técnicas da câmera, incluindo a posição GPS.
* CRS - [!DNL Camera Raw] esquema.
* `iptc4xmpCore` e `iptc4xmpExt`.
* TIFF - metadados de imagem (não apenas para imagens TIFF).

### Metadados específicos para impressão {#print-specific-metadata}

* PDF e PDF/X - Adobe PDF e aplicativos de terceiros.
* PRISM - [Requisitos de publicação para metadados padrão do setor](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - XMP metadados para texto paginado.

### Metadados específicos de multimídia {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gerenciamento de mídia.

## Referência de schemas de metadados {#metadata-schemata-reference}

A referência a seguir inclui informações sobre um esquema de metadados específico (em ordem alfabética), bem como uma lista de propriedades e suas definições.

### Dublin Core {#dublin-core}

Os metadados Dublin Core fornecem um conjunto padronizado de convenções para descrever ativos para facilitar a localização. Em [!DNL Assets], o Dublin Core descreve ativos digitais, incluindo vídeo, som, imagens e documentos.

O Conjunto de elementos de metadados principal simples de Dublin (DCMES) contém 15 elementos de metadados, conforme listados na tabela a seguir. Cada elemento Dublin Core é opcional e pode ser repetido. Você pode adicionar ou excluir informações de metadados Dublin Core da mesma maneira que faria para metadados específicos de tipo de mídia.

Além do DCMES, existem outros elementos de metadados criados pela iniciativa Dublin Core. Consulte a [iniciativa Dublin Core](https://dublincore.org/) para obter mais informações.

| Propriedade | Descrição |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| colaborador | A pessoa ou empresa responsável pela contribuição para o conteúdo. |
| cobertura | A localização geográfica ou período que o ativo cobre. |
| criador | A pessoa ou empresa responsável pela criação do conteúdo. |
| date | Data ou período associado ao ativo. |
| descrição | Mais informações sobre o ativo. |
| format | O formato de arquivo, a mídia física ou as dimensões do ativo. [!DNL Experience Manager] O usa  `dc:format` para indicar o tipo MIME do ativo. |
| identifier | Uma referência exclusiva ao ativo. |
| language | O idioma do ativo (por exemplo, `en` para inglês). |
| editor | A pessoa ou empresa responsável pela disponibilização do ativo. |
| relation | Um ativo relacionado. |
| direitos | Informações sobre quem tem os direitos a esse ativo. |
| source | Um ativo relacionado do qual o ativo é derivado. |
| assunto | O tópico do ativo. |
| título | Um nome para o ativo. |
| tipo | A natureza ou o gênero do ativo. |

### IPTC {#iptc}

O International Press Telecommunications Council (IPTC) é um consórcio de agências de notícias em todo o mundo - um de seus objetivos é desenvolver e manter padrões técnicos. O IPTC definiu um conjunto de padrões de metadados de fotos para imagens que são aceitas quase universalmente entre fotógrafos. Esses padrões de metadados faziam parte do padrão mais amplo conhecido como IPTC Information Interchange Model (IIM), criado nos anos 90.

Embora as informações do cabeçalho IPTC tenham sido substituídas principalmente por XMP, um esquema principal IPTC e um esquema de extensão estão disponíveis para XMP. Em programas de imagem, as propriedades XMP e IPTC são sincronizadas.

## Fluxos de trabalho orientados por metadados {#metadata-driven-workflows}

A criação de fluxos de trabalho orientados por metadados ajuda a automatizar alguns processos, o que melhora a eficiência. Em um fluxo de trabalho orientado por metadados, o sistema de gerenciamento de fluxo de trabalho lê o fluxo de trabalho e, como resultado, executa alguma ação predefinida. Por exemplo, algumas das maneiras de usar workflows orientados por metadados:

* O fluxo de trabalho pode verificar se uma imagem tem um título ou não. Caso contrário, o sistema notifica para adicionar um título.
* O workflow pode verificar se um aviso de copyright em um ativo permite distribuição ou não. Assim, o sistema envia o ativo para um servidor ou outro.
* Um workflow pode verificar ativos sem metadados obrigatórios predefinidos ou ativos com metadados *inválidos*.

## Metadados XMP {#xmp-metadata}

XMP (Plataforma de metadados extensível) é o padrão de metadados usado por [!DNL Adobe Experience Manager Assets] para todo o gerenciamento de metadados. O XMP fornece um formato padrão para a criação, o processamento e o intercâmbio de metadados para uma grande variedade de aplicativos.

Além de oferecer a codificação de metadados universais que pode ser incorporada em todos os formatos de arquivo, o XMP fornece um [modelo de conteúdo avançado](#xmp-core-concepts) e é [suportado pelo Adobe](#advantages-of-xmp) e por outras empresas, para que os usuários de XMP em combinação com [!DNL Assets] tenham uma plataforma poderosa para criar.

A [XMP especificação](https://www.adobe.com/devnet/xmp.html) está disponível no Adobe.

### O que é XMP? {#what-is-xmp}

O Adobe introduziu o padrão de XMP como parte do produto de software Adobe Acrobat. Desde então, a norma XMP foi amplamente adotada. [!DNL Assets] suporta nativamente o XMP - a Plataforma de metadados extensível liderada pelo Adobe. XMP é um padrão para processar e armazenar metadados padronizados e proprietários em ativos digitais. O XMP foi projetado para ser o padrão comum que permite que vários aplicativos funcionem com metadados de maneira eficaz.

Os profissionais de produção, por exemplo, usam o suporte XMP integrado nos aplicativos Adobe para transmitir informações em vários formatos de arquivo. [!DNL Assets] O repositório extrai os metadados de XMP e os usa para gerenciar o ciclo de vida do conteúdo e oferece a capacidade de criar workflows de automação.

XMP padroniza como os metadados são definidos, criados e processados fornecendo um modelo de dados, um modelo de armazenamento e esquemas. Todos esses conceitos são abordados nesta seção.

Todos os metadados herdados de EXIF, ID3 ou Microsoft Office são traduzidos automaticamente para XMP, o que pode ser estendido para oferecer suporte ao esquema de metadados específico do cliente, como catálogos de produtos.

Os metadados no XMP consistem em um conjunto de propriedades. Essas propriedades são sempre associadas a um
entidade específica designada por recurso; ou seja, as propriedades são &quot;sobre&quot; o recurso. No caso de XMP, o recurso é sempre o ativo.

### XMP ecossistema {#xmp-ecosystem}

O XMP define um modelo de [metadados](https://pt.wikipedia.org/wiki/Metadados) que pode ser usado com qualquer conjunto definido de itens de metadados. O XMP também define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos de propriedades básicas úteis para gravar o histórico de um recurso à medida que ele passa por várias etapas de processamento, de ser fotografado, [digitalizado](https://pt.wikipedia.org/wiki/Digitalizador) ou criado como texto, até etapas de edição de fotos (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) ou ajuste de cor), para montagem em uma imagem final. O XMP permite que cada programa de software ou dispositivo ao longo do caminho adicione suas próprias informações a um recurso digital, que pode ser retido no arquivo digital final.

O XMP geralmente é serializado e armazenado usando um subconjunto do [W3C](https://pt.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://pt.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que por sua vez é expresso em [XML](https://pt.wikipedia.org/wiki/XML).

### Vantagens do XMP {#advantages-of-xmp}

XMP tem as seguintes vantagens em relação a outros padrões e esquemas de codificação:

* Metadados baseados em XMP são muito avançados e otimizados.
* XMP permite ter vários valores para uma propriedade.
* XMP tem codificação padronizada, que permite a troca fácil de metadados.
* XMP é extensível. É possível adicionar mais informações aos ativos.

O padrão de XMP foi projetado para ser extensível, permitindo adicionar tipos personalizados de metadados aos dados de XMP. Por outro lado, EXIF não - tem uma lista fixa de propriedades que não pode ser estendida.

>[!NOTE]
>
>XMP geralmente não permite que tipos de dados binários sejam incorporados. Para carregar dados binários no XMP, por exemplo, imagens em miniatura, eles devem ser codificados em um formato compatível com XML, como `Base64`.

### XMP conceitos {#xmp-core-concepts}

As seções a seguir descrevem os conceitos principais de XMP, incluindo namespaces e schemas, propriedades e valores e alternativas de idioma.

#### Namespaces e schemata {#namespaces-and-schemata}

Um esquema XMP é um conjunto de nomes de propriedade em um namespace XML comum que inclui
Tipo de dados e informações descritivas. Um esquema de XMP é identificado por seu URI de namespace XML. O uso de namespaces impede conflitos entre propriedades em esquemas diferentes que tenham o mesmo nome, mas um significado diferente.

Por exemplo, a propriedade `Creator` em dois schemas projetados independentemente pode significar a pessoa que criou o ativo ou o aplicativo que criou o ativo (por exemplo, Adobe Photoshop).

#### Propriedades e valores {#properties-and-values}

XMP pode incluir propriedades de um ou mais schemas. Por exemplo, um subconjunto típico usado por muitos aplicativos Adobe pode incluir o seguinte:

* Esquema principal de Dublin: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* XMP esquema básico: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* XMP schema de gerenciamento de direitos: `xmpRights:WebStatement`, `xmpRights:Marked`.
* XMP schema de gerenciamento de mídia: `xmpMM:DocumentID`.

#### Alternativas linguísticas {#language-alternatives}

XMP permite adicionar uma propriedade `xml:lang` às propriedades do texto para especificar o idioma do texto.

## Trabalhar com metadados IPTC {#support-for-iptc-metadata}

Saiba como [!DNL Adobe Experience Manager Assets] suporta os metadados IPTC, as classificações criativas e as palavras-chave adicionadas aos ativos por meio de [!DNL Adobe Bridge] e outros aplicativos [!DNL Adobe Creative Cloud].

[!DNL Adobe Experience Manager Assets] O suporta o padrão de metadados IPTC amplamente usado para descrever ativos. Dessa forma, [!DNL Assets] melhora a aceitação de suas imagens entre vários partidos, incluindo fotógrafos, agências criativas, bibliotecas, museus e assim por diante.

O esquema de metadados padrão para ativos agora incorpora os esquemas de metadados IPTC Core e IPTC Extension para definir propriedades abrangentes de metadados que permitem aos usuários adicionar dados precisos e confiáveis sobre pessoas, locais e produtos mostrados em uma imagem. Também oferece suporte a datas, nomes e identificadores relacionados à criação da imagem e a uma maneira flexível de expressar informações de direitos.

A página Propriedades dos ativos agora inclui guias separadas para exibir os metadados da Extensão IPTC principal e IPTC em campos editáveis.

1. Na interface do usuário [!DNL Assets], selecione uma imagem.
1. Clique em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Clique na guia **[!UICONTROL IPTC]** para exibir os metadados IPTC do ativo.
1. Edite as propriedades de metadados IPTC, conforme necessário.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Clique na guia **[!UICONTROL Extensão IPTC]** para exibir os metadados da Extensão IPTC do ativo.
1. Edite as propriedades de metadados da Extensão IPTC, conforme necessário.
1. Clique em **[!UICONTROL Salvar e fechar]** para salvar as alterações.

### Suporte a classificação criativa {#creative-rating-support}

Além de exibir classificações de usuários individuais e classificações agregadas, a página Propriedades agora exibe as classificações atribuídas aos ativos por meio do Adobe Bridge e de outros aplicativos de criação

Essas classificações estão disponíveis na seção **[!UICONTROL Classificação criativa]**, na guia **[!UICONTROL Avançado]**.

Essa classificação é uma propriedade somente leitura e varia entre 1 e 5. Você pode pesquisar ativos com base em sua Classificação criativa no Painel de pesquisa.

No entanto, essa propriedade não está indexada no momento para evitar qualquer conflito com as alterações personalizadas feitas pelos usuários.

### Suporte a palavras-chave {#keyword-support}

A guia **[!UICONTROL IPTC]** da página [!UICONTROL Propriedades] também exibe as palavras-chave adicionadas aos ativos por meio do Adobe Bridge e de outros aplicativos Adobe Creative Cloud. Também é possível editar essas palavras-chave e adicionar mais palavras-chave na guia **[!UICONTROL IPTC]**.

![keywords](assets/keywords-in-iptc-tab.png)
