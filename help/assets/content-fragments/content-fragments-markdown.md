---
title: Markdown
seo-title: Markdown
description: Durante a criação, o editor de fragmentos de conteúdo usa a sintaxe de markdown para permitir que você escreva conteúdo facilmente.
seo-description: Durante a criação, o editor de fragmentos de conteúdo usa a sintaxe de markdown para permitir que você escreva conteúdo facilmente.
uuid: afcbf82f-3a75-4491-9172-706188db65bb
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: b193f28c-46c2-4eab-bbb8-578530f80ba5
docset: aem65
translation-type: tm+mt
source-git-commit: afed13a2f832b91d0df825d1075852cc84443646
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 4%

---


# Markdown{#markdown}

Quando você está [criando](content-fragments-variations.md#authoring-your-content), o editor de fragmentos de conteúdo usa a sintaxe de *markdown* para permitir que você escreva conteúdo facilmente:

![editor de marcação](/help/assets/content-fragments/assets/cfm-6420-08.png)

Você pode definir:

* [Notação do cabeçalho](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [Quebras de parágrafos e linhas](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [Links](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [Imagens](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [Bloquear aspas](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [Listas](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [Ênfase](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [Blocos de código](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [A barra invertida escapa](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## Notação do cabeçalho {#heading-notation}

Para criar um cabeçalho, insira uma tag hash (#) na frente do cabeçalho. Uma hash tag (#) é usada para H1, duas hash tags (##) para H2 etc. Você pode usar até 6 hashtags. Por exemplo:

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

Como opção, você pode criar um H1 ao sublinhar o texto em sinais iguais e criar um H2 ao sublinhar o texto em sinais de menos. Por exemplo:

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## Quebras de parágrafos e linhas {#paragraphs-and-line-breaks}

Um parágrafo é simplesmente uma ou mais linhas consecutivas de texto, separadas por uma ou mais linhas em branco. Uma linha em branco é uma linha que só contém espaços ou guias. Os parágrafos normais não devem ser recuados com espaços ou tabulações.

Uma quebra de linha é criada terminando uma linha com dois ou mais espaços e depois um retorno.

## Links {#links}

Você pode criar links em linha e de referência.

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

A sintaxe das imagens é semelhante aos links. É possível criar imagens em linha e referenciadas.

Por exemplo, uma imagem em linha tem a seguinte sintaxe:

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

A sintaxe inclui:

* Um ponto de exclamação: !;
* seguido de um conjunto de colchetes, que contém o texto alternativo do atributo da imagem;
* seguido por um conjunto de parênteses, contendo o URL ou o caminho para a imagem, e um atributo de título opcional incluído entre duplos ou aspas simples.

Uma imagem de estilo de referência tem a seguinte sintaxe:

    `![Alt text][id]`

Onde &quot;id&quot; é o nome de uma referência de imagem definida. As referências de imagem são definidas usando sintaxe idêntica a referências de link:

    `[id]: url/to/image "Optional title attribute"`

## Bloquear aspas {#block-quotes}

É possível citar o texto adicionando o símbolo > antes do texto. Por exemplo:

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

Para adicionar itálico, faça o seguinte:

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

Você pode negrito como segue:

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

Para indicar uma extensão de código, vincule-o com aspas invertidas (`). Ao contrário de um bloco de código pré-formatado, uma extensão de código indica o código dentro de um parágrafo normal.

Por exemplo:

    ``Use the `printf()` function.``

## Blocos de código {#code-blocks}

Blocos de código geralmente são usados para ilustrar o código-fonte. É possível criar blocos de código recuando o código usando uma guia ou no mínimo 4 espaços. Por exemplo:

    `This is a normal paragraph.`

        `This is a code block.`

## A barra invertida escapa {#backslash-escapes}

Você pode usar escape de barra invertida para gerar caracteres literais que têm um significado especial na formatação da sintaxe. Por exemplo, se você quiser circundar uma palavra com asteriscos literais (em vez de uma tag HTML &lt;em>), você pode usar barras invertidas antes dos asteriscos, como em:

    `\\*literal asterisks\\*`

As escapadas de barra invertida estão disponíveis para os seguintes caracteres:

    `\ backslash`

    &#39;backtick&#39;

    `* asterisk`

    `_ underscore`

    `{} curly braces`

    `[] square brackets`

    `() parentheses`

    `# hash mark`

    `+ plus sign`

    `- minus sign (hyphen)`

    `. dot`
