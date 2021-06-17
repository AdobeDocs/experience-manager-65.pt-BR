---
title: Markdown
seo-title: Markdown
description: Durante a criação, o editor de fragmento de conteúdo usa a sintaxe de marcação para permitir que você grave conteúdo com facilidade.
seo-description: Durante a criação, o editor de fragmento de conteúdo usa a sintaxe de marcação para permitir que você grave conteúdo com facilidade.
uuid: afcbf82f-3a75-4491-9172-706188db65bb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: b193f28c-46c2-4eab-bbb8-578530f80ba5
docset: aem65
feature: Fragmentos de conteúdo
role: Business Practitioner, Administrator
exl-id: 28e1052f-62b5-47bc-9bc8-f2d92f0254f6
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 4%

---

# Markdown{#markdown}

Quando você está [criando](content-fragments-variations.md#authoring-your-content), o editor de fragmento de conteúdo usa a sintaxe *markdown* para permitir que você grave facilmente o conteúdo:

![editor de marcação](/help/assets/content-fragments/assets/cfm-6420-08.png)

Você pode definir:

* [Notação de cabeçalho](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [Parágrafos e quebras de linha](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [Links](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [Imagens](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [Bloquear aspas](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [Listas](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [Ênfase](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [Blocos de código](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [Escovas da barra invertida](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## Notação de cabeçalho {#heading-notation}

Para criar um cabeçalho, coloque uma hash tag (#) na frente do cabeçalho. Uma hash tag (#) é usada para H1, duas hash tags (##) para H2 etc. Você pode usar até 6 hashtags. Por exemplo:

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

Como opção, você pode criar um H1 ao sublinhar o texto em sinais iguais e criar um H2 ao sublinhar o texto em sinais de menos. Por exemplo:

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## Parágrafos e quebras de linha {#paragraphs-and-line-breaks}

Um parágrafo é simplesmente uma ou mais linhas consecutivas de texto, separadas por uma ou mais linhas em branco. Uma linha em branco é uma linha que contém apenas espaços ou guias. Os parágrafos normais não devem ser recuados com espaços ou tabulações.

Uma quebra de linha é criada ao terminar uma linha com dois ou mais espaços e depois um retorno.

## Links {#links}

Você pode criar links integrados e de referência.

Em ambos os estilos, o texto do link é delimitado por colchetes `[]`.

Estes são exemplos de links em linha:

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

Um link de referência tem a seguinte sintaxe:

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## Imagens {#images}

A sintaxe das imagens é semelhante aos links. Você pode criar imagens embutidas e referenciadas.

Por exemplo, uma imagem em linha tem a seguinte sintaxe:

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

A sintaxe inclui:

* Um ponto de exclamação: !;
* seguido por um conjunto de colchetes, contendo o texto alternativo do atributo para a imagem;
* seguido por um conjunto de parênteses, contendo o URL ou o caminho para a imagem, e um atributo de título opcional entre aspas duplas ou simples.

Uma imagem do estilo de referência tem a seguinte sintaxe:

    `![Alt text][id]`

Onde &quot;id&quot; é o nome de uma referência de imagem definida. As referências de imagem são definidas usando a sintaxe idêntica às referências de link:

    `[id]: url/to/image "Optional title attribute"`

## Bloquear aspas {#block-quotes}

É possível fazer aspas de texto adicionando o símbolo > antes do texto. Por exemplo:

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

Você pode ter aspas de bloco aninhadas. Por exemplo:

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## Listas {#lists}

Você pode criar listas ordenadas e não ordenadas.

Para criar uma lista não ordenada, use o &amp;ast; antes dos itens na lista. Por exemplo:

    `* item in list`

    `* item in list`

    `* item in list`

Para criar uma lista ordenada, adicione os números, seguidos de um ponto, antes de cada item na lista. Por exemplo:

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## Ênfase {#emphasis}

É possível adicionar um estilo em itálico ou negrito ao texto.

Para adicionar itálico da seguinte maneira:

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

Você pode negrito como segue:

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

Para indicar uma extensão de código, vincule-a com aspas invertidas (&amp;grave;). Ao contrário de um bloco de código pré-formatado, uma extensão de código indica código dentro de um parágrafo normal.

Por exemplo:

    ``Use the `printf()` function.``

## Blocos de código {#code-blocks}

Os blocos de código geralmente são usados para ilustrar o código-fonte. Você pode criar blocos de código recuando o código usando uma guia ou um mínimo de 4 espaços. Por exemplo:

    `This is a normal paragraph.`

        `This is a code block.`

## A barra invertida evita {#backslash-escapes}

Você pode usar escape de barra invertida para gerar caracteres literais que têm significado especial na formatação da sintaxe. Por exemplo, se você deseja rodar uma palavra com asteriscos literais (em vez de uma tag HTML &lt;em> ), é possível usar barras invertidas antes dos asteriscos, desta forma:

    `\\*literal asterisks\\*`

Os escape de barra invertida estão disponíveis para os seguintes caracteres:

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`
