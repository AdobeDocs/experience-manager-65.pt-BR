---
title: Entender os conceitos de metadados
description: Saiba mais sobre a necessidade de e os tipos de metadados que permitem categorização e organização mais fáceis de ativos.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 312fff5f-39c1-48c1-aa99-40feb72c2f59
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2718'
ht-degree: 9%

---

# Entender os conceitos de metadados {#why-we-need-metadata}

Metadados são dados sobre dados. A este respeito, os dados se referem ao seu ativo digital, digamos uma imagem. Os metadados são essenciais para um gerenciamento eficiente de ativos.

Os metadados são a coleção de todos os dados disponíveis para um ativo, mas que não estão necessariamente contidos nessa imagem. Alguns exemplos de metadados são:

* Nome do ativo.
* Hora e data da última modificação.
* Tamanho do ativo conforme foi armazenado no repositório.
* Nome da pasta na qual ele está contido.
* Ativos relacionados ou tags aplicadas.

As propriedades de metadados básicas acima que [!DNL Experience Manager] O pode gerenciar para ativos, o que permite que os usuários vejam todos os ativos. Por exemplo, solicitar ativos pela última data de modificação é útil ao tentar descobrir ativos adicionados recentemente.

Você pode adicionar mais dados de alto nível aos ativos digitais, por exemplo:

* Tipo de ativo (uma imagem, vídeo, clipe de áudio ou documento).
* Proprietário do ativo.
* Título do ativo.
* Descrição do ativo.
* Tags atribuídas a um ativo.

Mais metadados ajudam a categorizar os ativos e são úteis à medida que a quantidade de informações digitais cresce. É possível gerenciar algumas centenas de arquivos com base apenas nos nomes de arquivo. No entanto, essa abordagem não é escalável. Ela é limitada quando o número de pessoas envolvidas e o número de ativos gerenciados aumentam.

Com a adição de metadados, o valor de um ativo digital cresce, porque o ativo se torna,

* Mais acessível — os sistemas e usuários podem encontrá-lo facilmente.
* Mais fácil de gerenciar — é possível encontrar ativos com o mesmo conjunto de propriedades mais facilmente e realizar alterações neles.
* Completo — o ativo carrega mais informações e contexto com mais metadados.

Por estas razões, [!DNL Assets] O oferece o meio certo de criar, gerenciar e trocar metadados para seus ativos digitais.

## Tipos de metadados {#types-of-metadata}

Os dois tipos básicos de metadados são os técnicos e os descritivos.

Os metadados técnicos são úteis para aplicativos de software que lidam com ativos digitais e não devem ser mantidos manualmente. [!DNL Experience Manager Assets] O e outros softwares determinam automaticamente os metadados técnicos e eles podem mudar quando o ativo for modificado. Os metadados técnicos disponíveis de um ativo dependem em grande parte do tipo de arquivo do ativo. Alguns exemplos de metadados técnicos são:

* Tamanho de um arquivo.
* Dimension (altura e largura) de uma imagem.
* Taxa de bits de um arquivo de áudio ou vídeo.
* Resolução (nível de detalhe) de uma imagem.

Metadados descritivos são metadados relacionados ao domínio do aplicativo, por exemplo, o negócio de onde um ativo vem. Os metadados descritivos não podem ser determinados automaticamente. Ele é criado manual ou semiautomaticamente. Por exemplo, uma câmera habilitada para GPS pode rastrear automaticamente a latitude e a longitude e adicionar uma marca de localização geográfica à imagem.

O custo de criar manualmente as informações de metadados descritivos é alto. Assim, os padrões são estabelecidos para facilitar a troca de metadados entre sistemas e organizações de software. [!DNL Experience Manager Assets] O suporta todos os padrões relevantes para o gerenciamento de metadados.

## Padrões de codificação {#encoding-standards}

Há várias maneiras de incorporar metadados em arquivos. Uma seleção de padrões de codificação é compatível:

* XMP: usado por [!DNL Assets] para armazenar os metadados extraídos no repositório.
* ID3: para arquivos de áudio e vídeo.
* Exif: para arquivos de imagem.
* Outro/herdado: de [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]e assim por diante.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) é um padrão aberto usado pelo [!DNL Experience Manager Assets] para todo o gerenciamento de metadados. O padrão oferece codificação de metadados universais que pode ser incorporada em todos os formatos de arquivo. O Adobe e outras empresas apoiam o padrão XMP, pois ele fornece um modelo de conteúdo avançado. Usuários do padrão XMP e de [!DNL Experience Manager Assets] ter uma plataforma poderosa para utilizar. Para obter mais informações, consulte [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Os dados armazenados nessas tags de ID3 são exibidos ao reproduzir um arquivo de áudio digital no computador ou em um MP3 player portátil.

As tags ID3 foram criadas para o formato de arquivo MP3. Informações adicionais sobre formatos:

* As tags ID3 funcionam em arquivos MP3 e mp3PRO.
* O WAV não tem tags.
* O WMA tem tags proprietárias que não permitem a implementação de código aberto.
* Ogg Vorbis usa comentários Xiph incorporados no contêiner Ogg.
* A AAC usa um formato de marcação proprietário.

### Exif {#exif}

O formato de arquivo de imagem intercambiável (Exif) é o formato de metadados mais popular usado em fotografias digitais. Ele fornece uma maneira de incorporar um vocabulário fixo de propriedades de metadados em muitos formatos de arquivo, como JPEG, TIFF, RIFF e WAV. O Exif armazena metadados como pares de um nome de metadados e um valor de metadados. Esses pares de nome-valor dos metadados também são chamados de tags, para não serem confundidos com a marcação em [!DNL Experience Manager]. Câmeras digitais modernas criam metadados Exif e software de gráficos modernos suportam isso. O formato Exif é o menor denominador comum para o gerenciamento de metadados, especialmente para imagens.

Uma limitação importante do Exif é que alguns formatos populares de arquivos de imagem, como BMP, GIF ou PNG, não são compatíveis.

Os campos de metadados definidos pelo Exif são normalmente de natureza técnica e de uso limitado para a gestão de metadados descritivos. Por esse motivo, [!DNL Experience Manager Assets] oferece mapeamento de propriedades Exif em [esquema de metadados comum](metadata-schemas.md) e em [XMP](xmp-writeback.md).

### Outros metadados {#other-metadata}

Outros metadados que podem ser incorporados de arquivos incluem [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]e assim por diante.

## Entender o esquema de metadados {#metadata-schemata}

Os esquemas de metadados são conjuntos predefinidos de definições de propriedades de metadados que podem ser usadas em vários aplicativos. As propriedades são sempre associadas a um ativo, o que significa que as propriedades são &quot;sobre&quot; o recurso.

Você também pode projetar seu próprio esquema de metadados se não houver nenhum que atenda às suas necessidades. Não duplique as informações existentes. Em uma organização, a separação de esquemas facilita o compartilhamento de metadados. [!DNL Experience Manager] O fornece uma lista padrão dos esquemas de metadados mais populares. A lista ajuda você a iniciar rapidamente sua estratégia de metadados e escolher rapidamente as propriedades de metadados necessárias.

Os esquemas de metadados compatíveis estão listados abaixo.

### Metadados padrão {#standard-metadata}

* DC - [!DNL Dublin Core] O é um conjunto de metadados importante e amplamente usado.
* DICOM - Imagem Digital e Comunicações em Medicina.
* `Iptc4xmpCore` e `iptc4xmpExt` - O International Press Communications Standard contém muitos metadados específicos para cada assunto.
* RDF - Estrutura de descrição do recurso - para metadados web semânticos genéricos.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Emissão de tíquetes de trabalho básicos.

### Metadados específicos do aplicativo {#application-specific-metadata}

Os metadados específicos do aplicativo incluem metadados técnicos e descritivos. Se você usar esses metadados, outros aplicativos talvez não consigam usá-los. Por exemplo, um aplicativo de renderização de imagem diferente pode não conseguir acessar [!DNL Adobe Photoshop] metadados. Você pode criar uma etapa de fluxo de trabalho que altere uma propriedade específica do aplicativo para uma propriedade padrão.

* ACDSee - Metadados gerenciados pelo [!DNL ACDSee] programa. Consulte [www.acdsee.com/](https://www.acdsee.com/).
* Álbum - [!DNL Adobe Photoshop Album].
* CQ - Usado por [!DNL Experience Manager Assets].
* DAM - Usado por [!DNL Experience Manager Assets].
* DEX - [!DNL Optima SC Description explorer] O é uma coleção de ferramentas para gerenciamento de metadados e arquivos de sistemas operacionais Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto e MP - Microsoft Photo.
* PDF e PDF/X.
* Photoshop e psAux - [!DNL Adobe Photoshop].

### Digital Rights Management metadados (DRM) {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* MAIS - [Sistema Universal de Licenciamento de Imagem](https://www.useplus.com).
* PRISM - [Requisitos de publicação para metadados padrão do setor](https://www.idealliance.org/prism-metadata).
* PRL - Idioma de direitos PRISM.
* PUR - Direitos de Uso do PRISM.
* `xmpPlus` - Integração do PLUS com o XMP.

### Metadados específicos de fotografia {#photography-specific-metadata}

* Exif - Informações técnicas da câmera, incluindo a posição GPS.
* CRS - [!DNL Camera Raw] esquema.
* `iptc4xmpCore` e `iptc4xmpExt`.
* TIFF - metadados de imagem (não apenas para imagens TIFF).

### Metadados específicos de impressão {#print-specific-metadata}

* PDF e PDF/X - Adobe PDF e aplicativos de terceiros.
* PRISM - [Requisitos de publicação para metadados padrão do setor](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - Metadados de XMP para texto paginado.

### Metadados específicos de multimídia {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gerenciamento de mídia.

## Referência do esquema de metadados {#metadata-schemata-reference}

A referência a seguir inclui informações sobre um esquema de metadados específico (em ordem alfabética) e uma lista de propriedades e suas definições.

### Dublin Core {#dublin-core}

Os metadados principais de Dublin fornecem um conjunto padronizado de convenções para descrever ativos para facilitar a localização. Entrada [!DNL Assets], o Dublin Core descreve ativos digitais incluindo vídeo, som, imagens e documentos.

O conjunto simples de elementos de metadados principais (DCMES) de Dublin contém 15 elementos de metadados, conforme listados na tabela a seguir. Cada elemento principal de Dublin é opcional e pode ser repetido. Você pode adicionar ou excluir as informações dos metadados principais de Dublin da mesma maneira que faria com os metadados específicos do tipo de mídia.

Além do DCMES, existem outros elementos de metadados criados pela Iniciativa principal de Dublim. Consulte a [Iniciativa principal de Dublin](https://dublincore.org/) para obter mais informações.

| Propriedade | Descrição |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| colaborador | A pessoa ou empresa responsável por fazer contribuições ao conteúdo. |
| cobertura | A localização geográfica ou o período abrangido pelo ativo. |
| criador | A pessoa ou empresa responsável pela criação do conteúdo. |
| data | Data ou período associado ao ativo. |
| descrição | Mais informações sobre o ativo. |
| formato | O formato do arquivo, a mídia física ou as dimensões do ativo. [!DNL Experience Manager] usos `dc:format` para indicar o tipo MIME do ativo. |
| identificador | Uma referência exclusiva ao ativo. |
| idioma | O idioma do ativo (por exemplo, `en` para inglês). |
| editor | A pessoa ou empresa responsável por disponibilizar o ativo. |
| relação | Um ativo relacionado. |
| direitos | Informações sobre quem tem os direitos a este ativo. |
| source | Um ativo relacionado do qual o ativo é derivado. |
| assunto | O tópico do ativo. |
| título | Um nome para o ativo. |
| tipo | A natureza ou gênero do ativo. |

### IPTC {#iptc}

O International Press Telecommunications Council (IPTC) é um consórcio de agências de notícias em todo o mundo - um de seus objetivos é desenvolver e manter padrões técnicos. O IPTC definiu um conjunto de padrões de metadados fotográficos para imagens que é quase universalmente aceito entre os fotógrafos. Esses padrões de metadados faziam parte de um padrão mais amplo conhecido como Modelo de Intercâmbio de Informações IPTC (IIM), criado na década de 1990.

Embora as informações do cabeçalho IPTC tenham sido substituídas principalmente pelo XMP, um esquema principal IPTC e um esquema de extensão estão disponíveis para o XMP. Nos programas de imagem, as propriedades XMP e IPTC são sincronizadas.

## Fluxos de trabalho orientados por metadados {#metadata-driven-workflows}

A criação de workflows orientados por metadados ajuda você a automatizar alguns processos, o que melhora a eficiência. Em um fluxo de trabalho orientado por metadados, o sistema de gerenciamento de fluxos de trabalho lê o fluxo de trabalho e, como resultado, executa alguma ação predefinida. Por exemplo, algumas das maneiras de usar workflows orientados por metadados:

* O fluxo de trabalho pode verificar se uma imagem tem ou não um título. Caso contrário, o sistema notificará a adição de um título.
* O fluxo de trabalho pode verificar se um aviso de copyright em um ativo permite a distribuição ou não. Assim, o sistema envia o ativo para um servidor ou para o outro.
* Um fluxo de trabalho pode verificar ativos sem metadados ou ativos obrigatórios predefinidos com *inválido* metadados.

## Metadados XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) é o padrão de metadados usado pelo [!DNL Adobe Experience Manager Assets] para todo o gerenciamento de metadados. O XMP fornece um formato padrão para a criação, processamento e intercâmbio de metadados para uma grande variedade de aplicativos.

Além de oferecer codificação de metadados universal que pode ser incorporada em todos os formatos de arquivo, o XMP fornece uma [modelo de conteúdo](#xmp-core-concepts) e está [suportado pelo Adobe](#advantages-of-xmp) e outras empresas, de modo que os utilizadores de XMP em combinação com [!DNL Assets] ter uma plataforma poderosa para utilizar.

A variável [Especificação XMP](https://www.adobe.com/devnet/xmp.html) está disponível no Adobe.

### O que é XMP? {#what-is-xmp}

O Adobe introduziu pela primeira vez o padrão XMP como parte do produto de software Adobe Acrobat. Desde então, o padrão XMP tem sido amplamente adotado. [!DNL Assets] suporta nativamente o XMP - a plataforma de metadados extensíveis liderada pelo Adobe. O XMP é um padrão para processar e armazenar metadados padronizados e proprietários em ativos digitais. O XMP foi projetado para ser o padrão comum que permite que vários aplicativos funcionem efetivamente com metadados.

Os profissionais de produção, por exemplo, usam o suporte integrado para XMP em vários aplicativos Adobe para transmitir informações entre vários formatos de arquivo. [!DNL Assets] O repositório extrai os metadados XMP e os usa para gerenciar o ciclo de vida do conteúdo e oferece a capacidade de criar workflows de automação.

O XMP padroniza como os metadados são definidos, criados e processados fornecendo um modelo de dados, um modelo de armazenamento e esquemas. Todos esses conceitos são abordados nesta seção.

Todos os metadados herdados do EXIF, ID3 ou do Microsoft Office são traduzidos automaticamente para XMP, que pode ser estendido para oferecer suporte ao esquema de metadados específico do cliente, como catálogos de produtos.

Os metadados no XMP consistem em um conjunto de propriedades. Essas propriedades são sempre associadas a uma entidade específica chamada de recurso; ou seja, as propriedades são &quot;sobre&quot; o recurso. No caso do XMP, o recurso é sempre o ativo.

### ecosistema XMP {#xmp-ecosystem}

O XMP define um modelo de [metadados](https://pt.wikipedia.org/wiki/Metadados) que pode ser usado com qualquer conjunto definido de itens de metadados. O XMP também define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos de propriedades básicas úteis para gravar o histórico de um recurso à medida que ele passa por várias etapas de processamento, de ser fotografado, [digitalizado](https://pt.wikipedia.org/wiki/Digitalizador) ou criado como texto, até etapas de edição de fotos (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) ou ajuste de cor), para montagem em uma imagem final. O XMP permite que cada programa de software ou dispositivo ao longo do caminho adicione suas próprias informações a um recurso digital, que pode ser retido no arquivo digital final.

O XMP geralmente é serializado e armazenado usando um subconjunto do [W3C](https://pt.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://pt.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que por sua vez é expresso em [XML](https://pt.wikipedia.org/wiki/XML).

### Vantagens do XMP {#advantages-of-xmp}

O XMP tem as seguintes vantagens em relação a outros padrões e esquemas de codificação:

* Os metadados com base em XMP são muito poderosos e refinados.
* O XMP permite que você tenha vários valores para uma propriedade.
* O XMP tem codificação padronizada, que permite a fácil troca de metadados.
* O XMP é extensível. Você pode adicionar mais informações aos seus ativos.

O padrão XMP é projetado para ser extensível, permitindo adicionar tipos personalizados de metadados aos dados XMP. O EXIF, por outro lado, não - ele tem uma lista fixa de propriedades que não podem ser estendidas.

>[!NOTE]
>
>O XMP geralmente não permite que tipos de dados binários sejam incorporados. Para transportar dados binários no XMP, por exemplo, imagens em miniatura, eles devem ser codificados em um formato compatível com XML, como `Base64`.

### Conceitos de XMP {#xmp-core-concepts}

As seções a seguir descrevem os principais conceitos do XMP, incluindo namespaces e esquemas, propriedades e valores e alternativas de idioma.

#### Namespaces e esquemas {#namespaces-and-schemata}

Um esquema XMP é um conjunto de nomes de propriedades em um namespace XML comum que inclui o tipo de dados e as informações descritivas. Um esquema XMP é identificado por seu URI de namespace XML. O uso de namespaces impede conflitos entre propriedades em esquemas diferentes que têm o mesmo nome, mas um significado diferente.

Por exemplo, a variável `Creator` propriedade em dois esquemas criados de forma independente pode significar a pessoa que criou o ativo ou pode significar o aplicativo que criou o ativo (por exemplo, Adobe Photoshop).

#### Propriedades e valores {#properties-and-values}

O XMP pode incluir propriedades de um ou mais esquemas. Por exemplo, um subconjunto típico usado por muitos aplicativos Adobe pode incluir o seguinte:

* Esquema principal de Dublin: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* Esquema básico do XMP: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* Esquema de gestão de direitos de XMP: `xmpRights:WebStatement`, `xmpRights:Marked`.
* Esquema de gerenciamento de mídia XMP: `xmpMM:DocumentID`.

#### Alternativas de idioma {#language-alternatives}

XMP permite adicionar um `xml:lang` para propriedades de texto para especificar o idioma do texto.

## Trabalhar com metadados IPTC {#support-for-iptc-metadata}

Saiba como [!DNL Adobe Experience Manager Assets] O é compatível com metadados IPTC, classificações criativas e palavras-chave adicionadas aos ativos por meio do [!DNL Adobe Bridge] e outros [!DNL Adobe Creative Cloud] aplicativos.

[!DNL Adobe Experience Manager Assets] O é compatível com o padrão de metadados IPTC, amplamente usado para descrever ativos. Por aqui, [!DNL Assets] aumenta a aceitação de suas imagens entre várias partes, incluindo fotógrafos, agências de criação, bibliotecas, museus e assim por diante.

O esquema de metadados padrão para ativos agora incorpora os esquemas de metadados Principal IPTC e Extensão IPTC para definir propriedades abrangentes de metadados que permitem aos usuários adicionar dados precisos e confiáveis sobre pessoas, locais e produtos mostrados em uma imagem. Também aceita datas, nomes e identificadores relacionados à criação da imagem, e uma maneira flexível de expressar informações de direitos.

A página Propriedades dos ativos agora inclui guias separadas para exibir os metadados do Núcleo IPTC e da Extensão IPTC nos campos editáveis.

1. No [!DNL Assets] selecione uma imagem.
1. Clique em **[!UICONTROL Propriedades]** na barra de ferramentas.
1. Clique em **[!UICONTROL IPTC]** para exibir os metadados IPTC do ativo.
1. Edite as propriedades dos metadados IPTC, conforme necessário.

   ![iptc_tab](assets/keywords-in-iptc-tab.png)

1. Clique em **[!UICONTROL Extensão IPTC]** para exibir os metadados da Extensão IPTC do ativo.
1. Edite as propriedades dos metadados da extensão IPTC, conforme necessário.
1. Clique em **[!UICONTROL Salvar e fechar]** para salvar as alterações.

### Suporte de classificação criativa {#creative-rating-support}

Além de exibir classificações de usuário individuais e classificações agregadas, a página Propriedades agora exibe as classificações atribuídas aos ativos por meio do Adobe Bridge e de outros aplicativos criativos

Essas classificações estão disponíveis na seção **[!UICONTROL Classificação criativa]**, na guia **[!UICONTROL Avançado]**.

Essa classificação é uma propriedade somente leitura e varia de 1 a 5. Você pode pesquisar ativos com base na sua Classificação criativa no painel Pesquisar.

No entanto, essa propriedade não está indexada no momento para evitar conflitos com as alterações personalizadas feitas pelos usuários.

### Suporte a palavras-chave {#keyword-support}

A variável **[!UICONTROL IPTC]** guia do [!UICONTROL Propriedades] A página também exibe palavras-chave adicionadas a ativos por meio do Adobe Bridge e de outros aplicativos da Adobe Creative Cloud. Também é possível editar essas palavras-chave e adicionar mais palavras-chave na **[!UICONTROL IPTC]** guia.

![palavras-chave](assets/keywords-in-iptc-tab.png)
