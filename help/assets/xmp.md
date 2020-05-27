---
title: Suporte para metadados XMP nos ativos Adobe Experience Manager.
description: Saiba mais sobre o padrão de metadados XMP (Extensible Metadata Platform) usado pelos ativos do Experience Manager para o gerenciamento de metadados. O XMP fornece um formato padrão para a criação, o processamento e o intercâmbio de metadados para uma grande variedade de aplicativos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 19%

---


# Metadados XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) é o padrão de metadados usado pelos ativos Adobe Experience Manager para todo o gerenciamento de metadados. O XMP fornece um formato padrão para a criação, o processamento e o intercâmbio de metadados para uma grande variedade de aplicativos.

Além de oferecer codificação de metadados universais que podem ser incorporados em todos os formatos de arquivo, o XMP fornece um modelo [de](xmp.md#xmp-core-concepts) conteúdo avançado e é [suportado pela Adobe](xmp.md#advantages-of-xmp) e outras empresas, para que os usuários do XMP em combinação com o Assets tenham uma plataforma poderosa para desenvolver.

A especificação [](https://www.adobe.com/devnet/xmp.html) XMP está disponível na Adobe.

## O que é o XMP? {#what-is-xmp}

O Assets suporta nativamente o XMP - a Plataforma de metadados extensível liderada pela Adobe. O XMP é um padrão para processamento e armazenamento de metadados padronizados e proprietários em ativos digitais. O XMP é projetado para ser o padrão comum que permite que vários aplicativos funcionem com metadados de forma eficaz.

Os profissionais de produção, por exemplo, usam o suporte XMP integrado nos aplicativos da Adobe para transmitir informações em vários formatos de arquivo. O repositório de ativos extrai os metadados XMP e os usa para gerenciar o ciclo de vida do conteúdo e oferta a capacidade de criar workflows de automação.

O XMP padroniza como os metadados são definidos, criados e processados fornecendo um modelo de dados, um modelo de armazenamento e schemas. Todos estes conceitos são abordados nesta seção.

Todos os metadados herdados do EXIF, ID3 ou Microsoft Office são automaticamente traduzidos para XMP, que pode ser estendido para suportar schemas de metadados específicos do cliente, como catálogos de produtos.

Os metadados no XMP consistem em um conjunto de propriedades. Estas propriedades estão sempre associadas a uma entidade específica, designada por recurso; ou seja, as propriedades são &quot;sobre&quot; o recurso. No caso do XMP, o recurso é sempre o ativo.

### Adobe {#adobe}

A Adobe introduziu o padrão XMP pela primeira vez como parte do produto de software Adobe Acrobat. Desde então, a norma XMP tem sido amplamente adotada.

### ecossistema XMP {#xmp-ecosystem}

O XMP define um modelo de [metadados](https://pt.wikipedia.org/wiki/Metadados) que pode ser usado com qualquer conjunto definido de itens de metadados. O XMP também define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos de propriedades básicas úteis para gravar o histórico de um recurso à medida que ele passa por várias etapas de processamento, de ser fotografado, [digitalizado](https://pt.wikipedia.org/wiki/Digitalizador) ou criado como texto, até etapas de edição de fotos (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) ou ajuste de cor), para montagem em uma imagem final. O XMP permite que cada programa de software ou dispositivo ao longo do caminho adicione suas próprias informações a um recurso digital, que pode ser retido no arquivo digital final.

O XMP geralmente é serializado e armazenado usando um subconjunto do [W3C](https://pt.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://pt.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que por sua vez é expresso em [XML](https://pt.wikipedia.org/wiki/XML).

## Vantagens do XMP {#advantages-of-xmp}

O XMP tem as seguintes vantagens em relação a outros padrões e esquemas de codificação:

* Metadados baseados em XMP são muito potentes e de granulação fina.
* O XMP permite que você tenha vários valores para uma propriedade.
* O XMP tem codificação padronizada, que permite a troca fácil de metadados.
* XMP é extensível. Você pode adicionar informações adicionais aos ativos.

### Extensíveis {#extensible}

O padrão XMP foi projetado para ser extensível, permitindo que você adicione tipos personalizados de metadados aos dados XMP. O EXIF, por outro lado, não - tem uma lista fixa de propriedades que não podem ser estendidas.

>[!NOTE]
>
>O XMP geralmente não permite a incorporação de tipos de dados binários. Para carregar dados binários no XMP, por exemplo, imagens em miniatura, eles devem ser codificados em um formato compatível com XML, como `Base64`.

## Conceitos principais XMP {#xmp-core-concepts}

As seções a seguir descrevem os conceitos principais do XMP, incluindo namespaces e esquemas, propriedades e valores e alternativas de idioma.

### Namespace e Schemata {#namespaces-and-schemata}

Um schema XMP é um conjunto de nomes de propriedade em uma namespace XML comum que inclui o tipo de dados e as informações descritivas. Um schema XMP é identificado pelo URI da namespace XML. O uso do namespace evita conflitos entre propriedades em schemas diferentes que tenham o mesmo nome, mas um significado diferente.

Por exemplo, a `Creator` propriedade em dois schemas projetados de forma independente pode significar a pessoa que criou o ativo ou pode significar o aplicativo que criou o ativo (por exemplo, Adobe Photoshop).

### Propriedades e valores {#properties-and-values}

XMP pode incluir propriedades de um ou mais schemas.

Por exemplo, um subconjunto típico usado por muitos aplicativos Adobe pode incluir o seguinte:

* schema principal de Dublin: dc:title, dc:creator, dc:subject, dc:format, dc:rights
* schema básico XMP: xmp:CreateDate, xmp:CreatorTool, xmp:ModifyDate, xmp:metadataDate
* schema de gerenciamento de direitos XMP: xmpRights:WebStatement, xmpRights:Marked
* schema de gerenciamento de mídia XMP: xmpMM:DocumentID

### Alternativas de idioma {#language-alternatives}

O XMP oferta a capacidade de adicionar uma `xml:lang` propriedade às propriedades do texto para especificar o idioma do texto.
