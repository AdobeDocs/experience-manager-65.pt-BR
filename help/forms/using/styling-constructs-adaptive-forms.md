---
title: Construção de estilo para formulários adaptáveis
seo-title: Construção de estilo para formulários adaptáveis
description: Use a estrutura MENOS para personalizar a aparência de formulários adaptáveis.
seo-description: Use a estrutura MENOS para personalizar a aparência de formulários adaptáveis.
uuid: d2e45ad9-7322-43ce-a1dd-ad97e2eea742
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ed50fa70-a8dd-4cc6-82a9-d59de0fa417d
docset: aem65
feature: Formulários adaptáveis
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2324'
ht-degree: 3%

---


# Construção de estilo para formulários adaptáveis{#styling-constructs-for-adaptive-forms}

## Pré-requisitos {#prerequisites}

Conhecimento do CSS e da estrutura LESS.

## O que pode ser personalizado {#what-can-be-customized}

O artigo lista as classes css de formulários adaptáveis disponíveis publicamente. Você pode aproveitar essas classes para criar um estilo em vários componentes de um formulário adaptável. O estilo de componentes de criação, como caixas de diálogo e barras de status que exibem avisos, está além do escopo deste artigo. Use essas construções de estilo para criar estilos (usando CSS ou Menos) somente quando não for possível criar estilo de componentes usando o [editor de temas](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html).

## Personalização de estilos em formulários adaptáveis {#customizing-styles-in-adaptive-forms}

A estrutura MENOS simplifica o caso de uso para personalizar estilos em formulários adaptáveis. A estrutura permite definir estilos usando um conjunto de variáveis e funções (mixins). A estrutura LESS ajuda a reduzir o tamanho do código empacotado e aumenta sua capacidade de reutilização.

Você pode personalizar estilos de formulário adaptáveis das seguintes maneiras:

* Alterar o tema
* Alterar o estilo do componente

## Alterar tema {#changing-theme}

É possível alterar o tema de um formulário adaptável para garantir que sua aparência seja consistente com as páginas da Web em que o formulário adaptável está incorporado.

As alterações na aparência geral do formulário adaptável usando propriedades de CSS normalmente fazem parte de alterações de tema. Alterações importantes no lo &quot;ok e comportamento do formulário adaptável, como alterações no layout e no posicionamento dos componentes, não são consideradas alterações de tema.

Com base no bootstrap, o seguinte conjunto de propriedades de CSS define o tema de uma página da Web:

* Cor do plano de fundo
* Borda (tipo, cor, espessura)
* Cor da fonte
* Preenchimento
* Imagem
* Tamanho da Fonte
* LineHeight

Atualmente, as variáveis MENOS são definidas apenas para essas propriedades dos vários elementos em um formulário adaptável.

## Alteração do estilo do componente {#changing-component-style}

Você pode fazer alterações na aparência, layout, posicionamento e visibilidade dos elementos. Para realizar essa tarefa, crie ou atualize seus arquivos .css personalizados para incluir as construções de estilo listadas neste artigo.

Para aplicar um estilo a um formulário adaptável, abra o formulário adaptável no para edição, abra as propriedades do contêiner de formulário adaptável e especifique o caminho do arquivo CSS personalizado na guia básica. O estilo padrão é construído do formulário adaptável e substituído pelas construções listadas no arquivo .css personalizado.

## Componentes {#components}

Os componentes discutidos neste artigo têm classes CSS predefinidas. É possível editar as variáveis para modificar os estilos nas classes CSS. Como alternativa, você pode reescrever a classe inteira. Esta seção descreve as classes nos componentes e estilos que você pode modificar usando variáveis.

## Estilo do contêiner {#container-styling}

Um contêiner é o componente de nível superior. Outros painéis e campos estão no componente do contêiner.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideContainerNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Descrição das variáveis</strong></p> </td>
   <td><p><strong>Descrição das variáveis</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>container-bgColor</code></p> </td>
   <td><p>Cor do plano de fundo do contêiner</p> </td>
  </tr>
  <tr>
   <td><p><code>container-padding</code></p> </td>
   <td><p>Preenchimento do contêiner</p> </td>
  </tr>
  <tr>
   <td><p><code>container-margin</code></p> </td>
   <td><p>Margem do contêiner</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>Cor da fonte do contêiner</p> </td>
  </tr>
 </tbody>
</table>

## Estilo de campo {#field-styling}

Os formulários adaptáveis incluem vários tipos de campos. Cada campo tem um nome de classe exclusivo, que é o nome do campo. O campo também tem um nome de classe comum `guideFieldNode`.

Os campos incluem rótulos, widgets, descrição da Ajuda (descrição longa e curta) e ícones de Ajuda do campo (ponto de interrogação).

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideFieldNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>field-padding</code><strong></strong></p> </td>
   <td><p>Preenchimento do campo</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-color</code></p> </td>
   <td><p>Cor da fonte da mensagem de erro do campo</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>Tamanho da fonte da mensagem de erro do campo</p> </td>
  </tr>
 </tbody>
</table>

## Estilo do rótulo {#label-styling}

O elemento HTML **label** usado para o campo inclui as classes **left** ou **top**, dependendo se o rótulo está na parte superior ou à esquerda.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideFieldLabel</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-color</code></p> </td>
   <td><p>Cor da fonte para o rótulo do campo</p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-size</code></p> </td>
   <td><p>Tamanho da fonte para o rótulo do campo</p> </td>
  </tr>
  <tr>
   <td><p><code>label-line-height</code></p> </td>
   <td>Propriedade CSS line height para rótulo de campo </td>
  </tr>
  <tr>
   <td><p><code>label-font-weight</code></p> </td>
   <td>Propriedade de peso da fonte CSS para o rótulo do campo </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>Margem para o rótulo do campo</p> </td>
  </tr>
 </tbody>
</table>

As regras de CSS para o rótulo são aplicadas usando o rótulo **guideFieldLabel**. Se você for um autor, substitua essa regra para tornar suas alterações personalizadas visíveis.

## Estilo de widgets {#widgets-styling}

Dependendo do tipo, os widgets também incluem classes. Geralmente, os widgets incluem a classe `guideFieldWidget`. Os widgets fornecidos com HTML normalmente usam a entrada de elemento HTML padrão e selecionam. O estilo é feito adequadamente. Não é possível criar um estilo de widget personalizado alterando as variáveis.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideFieldWidget</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis <code></code></strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-bg-color</code></p> </td>
   <td>Cor do plano de fundo dos widgets (Não funciona para a caixa de seleção e o botão de opção)</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>Cor da borda dos widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>Tamanho da borda dos widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>Raio da borda dos widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>Tipo de borda dos widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>Tipo de foco para bordas de widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>Estilo de borda consolidado de widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>Cor do texto dentro do widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>Tamanho do texto dentro do widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>Propriedade CSS lineheight para widget </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>Propriedade de preenchimento CSS para o widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>Cor da borda quando o widget está em foco</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-border-color</code></p> </td>
   <td><p>Cor da borda do widget para os campos obrigatórios</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo do widget para os campos obrigatórios</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo do widget quando o campo está desativado</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>Cor da fonte do widget quando o campo está desativado</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>Cor da Borda do widget quando o campo está desativado</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>Altura do widget (não funciona para a caixa de seleção e o botão de opção)</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>Altura para caixa de seleção e botão de opção.</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>Altura máxima para uma lista suspensa de várias seleções</p> </td>
  </tr>
 </tbody>
</table>

### Limitações no estilo de widget {#limitations-in-widget-styling}

O estilo de campos focados, obrigatórios e desativados é restrito com o uso de variáveis. No entanto, é possível alterá-la substituindo os estilos. A restrição que usa variáveis é fornecida principalmente para manter o número de variáveis sob controle. A restrição pode ser relaxada se a aparência de um campo mudar drasticamente porque está em qualquer um dos estados discutidos anteriormente.

## Descrição da Ajuda {#help-description}

Um autor pode especificar o conteúdo da Ajuda nos campos usando componentes de Descrição curta e longa. Ambos os componentes têm uma classe comum `.guideHelpDescription` e outra classe `.long`/ `.short`, dependendo do tipo de descrição. O conteúdo da Ajuda é incluído em um elemento de parágrafo para substituir o estilo da descrição. A descrição da Ajuda (longa e curta) é modificada usando variáveis que começam com widgetshelp, como mencionado na tabela a seguir:

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo da longa Ajuda dos widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>Cor da borda da longa Ajuda dos widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>Cor da borda do indicador esquerdo da longa Ajuda dos widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo da Ajuda curta dos widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>Cor da fonte da Ajuda curta dos widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>Cor do fundo da Ajuda da dica de ferramenta curta dos widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>Cor da fonte da ajuda da dica de ferramenta curta dos widgets</p> </td>
  </tr>
 </tbody>
</table>

## Termos e condições {#terms-and-conditions}

O widget Termos e condições (TnC `` ``) permite que você especifique termos e condições. Você pode personalizar o widget usando as variáveis descritas na tabela a seguir.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><code>tnc-unvisited</code></td>
   <td>Cor da fonte do link tnc não visitado.</td>
  </tr>
  <tr>
   <td><code>tnc-visited</code></td>
   <td>Cor da fonte do link tnc visitado.</td>
  </tr>
 </tbody>
</table>

## Botão {#button}

Os botões também são widgets. No entanto, o estilo é um pouco diferente dos widgets. Em formulários adaptáveis, qualquer um dos itens a seguir constitui um botão:

* input[type = text]
* botão
* elemento com class .button

Código HTML do botão:

`<button type="button" >`

`<span class="iconButtonicon"></`

`span>`

`<span class="iconButtonlabel"></`

`span>`

`</button>`

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-icon</code></p> </td>
   <td><p>Fornece ícones para o botão</p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-label</code></p> </td>
   <td><p>Rótulo/legenda do botão Estilos</p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis <code></code></strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-size</code></p> </td>
   <td><p>Tamanho da borda dos botões</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-type</code></p> </td>
   <td><p>Tipo de borda</p> </td>
  </tr>
  <tr>
   <td><p><code>button-padding</code></p> </td>
   <td><p>Propriedade de preenchimento CSS do botão</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-size</code></p> </td>
   <td><p>Tamanho da fonte para o botão</p> </td>
  </tr>
  <tr>
   <td><p><code>button-background-color</code></p> </td>
   <td><p>Cor do plano de fundo do botão</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-color</code></p> </td>
   <td><p>Cor da fonte do botão</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-color</code></p> </td>
   <td><p>Cor da borda do botão</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-padding</code></p> </td>
   <td><p>Preenchimento dos botões grandes (botões com classe .buttonlarge)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>Tamanho da fonte para botões grandes</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>Preenchimento dos botões pequenos (botões com classe .buttonsmall)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>Tamanho da fonte para botões pequenos</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>Cor do plano de fundo para botões informativos (botões com classe .buttoninformative)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>Cor da fonte para botões informativos</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>Cor da borda para botões informativos</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>Cor do plano de fundo para botões com estilo de aviso (botões com classe .buttonwarning)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>Cor da fonte para botões com estilo de aviso</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>Cor da borda para botões com estilo de aviso</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>Cor do plano de fundo para botões de alerta (botões com classe .buttonalert)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-font-color</code></p> </td>
   <td><p>Cor da fonte para botões de alerta</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-border-color</code></p> </td>
   <td><p>Cor da borda para botões de alerta</p> </td>
  </tr>
 </tbody>
</table>

## Ponto de interrogação {#question-mark}

Para os widgets, um ponto de interrogação é exibido quando um autor adiciona uma descrição longa no conteúdo da Ajuda. O ícone padrão fornecido no bootstrap é usado. Para usar um ícone personalizado, você pode personalizar os ícones do bootstrap.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideHelpQuestionMark</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-font-color</code></p> </td>
   <td><p>Cor do ícone</p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-hover-font-color</code></p> </td>
   <td><p>Cor do ícone quando o mouse está sobre ele</p> </td>
  </tr>
 </tbody>
</table>

## Table {#table}

Você pode alterar o tema de cor para linhas de cabeçalho e de corpo em uma tabela usando as seguintes variáveis.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>table-header-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo da linha de cabeçalho. O valor padrão é <code>#333</code>.<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>table-odd-row-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo para a linha de corpo ímpar. O valor padrão é <code>rgb(255, 255, 255)</code>.</p> </td>
  </tr>
  <tr>
   <td><p><code>table-even-row-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo para a linha de corpo par. O valor padrão é <code>#eee</code>.</p> </td>
  </tr>
 </tbody>
</table>

## Anexo de arquivo {#file-attachment}

O widget Anexo de arquivo de formulários adaptáveis permite carregar arquivos. Também é possível personalizar o widget usando as variáveis.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>Preenchimento dos arquivos exibidos no widget</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBackground</code></p> </td>
   <td><p>Cor do plano de fundo do item de arquivo</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>Cor da borda da borda superior</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemColor</code></p> </td>
   <td><p>Cor da fonte para o item de arquivo</p> </td>
  </tr>
  <tr>
   <td><p><code>filePreviewIconColor</code></p> </td>
   <td><p>Cor do ícone de Visualização (ícone de Bootstrap) no widget</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>Altura do comentário para o item de arquivo</p> </td>
  </tr>
 </tbody>
</table>

## Estilos do Navegador {#navigator-styles}

Há quatro tipos de guias de navegador. Isso inclui guias à esquerda, na parte superior, no assistente e na opção . Cada navegador tem uma classe diferente.

<table>
 <tbody>
  <tr>
   <td><p><strong>Naviagador</strong></p> </td>
   <td><p><strong>Classe CSS</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.acordion-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab-navigators-vertical</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.wizard-navigators</p> </td>
  </tr>
 </tbody>
</table>

Este é o código HTML para o elemento do navegador de guias (semelhante às guias do bootstrap):

`<li>`

`<a>tab title</a>`

`</li>`

`Accordion navigator is an exception, it has following barebone`

`structure:`

`<div class="accordion.navigators">`

`<div>`

`<div class = "guideHeader">`

`<a>`

`<span class = "guideSummary" ></code>`

`........................... repeatable buttons, if the repeatable configuration is set ................................`

`<div class = "repeatableButtons">`

`<button name="Add" class="Add"/>`

`<button name="Remove" class="Remove"/>`

`</div>`

`</a>`

`</div>`

`................................ panel content ..................................`

`</div>`

`</div>`

Você pode alterar o estilo do navegador usando regras CSS que selecionam os elementos usando seletores **descendente**. Por exemplo, para adicionar um estilo de decoração de texto à tag de âncora:

Navegador de guias na parte superior:

`.tab-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

`Tab navigator on left:`

`.tab-navigators-vertical`

`li a {`

`text-decoration:`

`underline;`

`}`

`Accordion navigator:`

`.accordion-navigators .guideHeader a .guideSummary {`

`text-decoration:`

`underline;`

`}`

`Wizard navigator:`

`.wizard-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

Além disso, há classes para navegadores de guias de estilo (esquerda e superior) com base em se eles têm navegadores aninhados/filhos/subnavegadores.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>Navegadores de guias (à esquerda e à parte superior) com navegadores aninhados/filhos/subnavegadores</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>Navegadores de guias (esquerda e superior) que não têm navegadores aninhados/filhos/subnavegadores</p> </td>
  </tr>
 </tbody>
</table>

A classe guideNavigationIcon fornece um ícone padrão para navegadores de tabulação (esquerda e superior) e navegadores de assistente.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideNavIcon</code></p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Você pode alterar o ícone de um determinado navegador fornecendo uma classe CSS no painel em criação, no exemplo de formulário &lt;CLASS_NAME>. Você adiciona um **&lt;CLASS_NAME>_nav** para o ícone do navegador.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>Navegadores de guias</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>navigator-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo do navegador da guia inteira</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo da guia</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-color</code></p> </td>
   <td><p>Cor da fonte da guia</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo da guia ao passar o mouse</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-font-color</code></p> </td>
   <td><p>Cor da fonte da guia ao passar o mouse</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo quando o painel está em foco (ativo)</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-font-color</code></p> </td>
   <td><p>Cor da fonte quando o painel está em foco</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo quando a expressão de conclusão do painel retorna true</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>Cor da fonte quando a expressão de conclusão do painel retorna true</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>Cor do plano de fundo quando o painel estava em foco uma vez, mas a expressão de conclusão retorna false </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>Cor da fonte quando o painel está em foco uma vez, mas a expressão de conclusão retorna false </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>Cor da borda da guia</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>Tamanho da fonte da guia</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>Preenchimento da guia</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>Margem para a guia</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-vertical-margin</code></p> </td>
   <td><p>Margem para as guias verticais</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-thickness</code></p> </td>
   <td><p>Tamanho da borda das guias</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-min-height</code></p> </td>
   <td><p>Altura mínima das guias</p> </td>
  </tr>
  <tr>
   <td><p><code>heirarichal-indent</code></p> </td>
   <td><p>Recuo para as guias aninhadas</p> </td>
  </tr>
  <tr>
   <td><p><strong>Navegadores do Assistente</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-navigator-bg-color</code></p> </td>
   <td>Cor do plano de fundo para todo o navegador do assistente</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-bg-color</code></p> </td>
   <td><p>Cor do fundo do assistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-color</code></p> </td>
   <td><p>Cor da fonte do assistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo quando o painel está em foco (ativo)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-font-color</code></p> </td>
   <td><p>Cor da fonte quando o painel está em foco (focalizado)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo quando a expressão de conclusão do painel retorna true</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>Cor da fonte quando a expressão de conclusão do painel retorna true</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>Cor do plano de fundo quando o painel estava em foco uma vez, mas a expressão de conclusão retorna falso</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>Cor da fonte quando o painel é focado uma vez, mas a expressão de conclusão retorna false</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>Cor do assistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>Tamanho da fonte do assistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-padding</code></p> </td>
   <td><p>Preenchimento do assistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>Tamanho da borda do assistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>Cor da borda do marcador do navegador do assistente (prefixo da legenda/rótulo)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo da barra de progresso do navegador do assistente</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>Cor de preenchimento da barra de progresso</p> </td>
  </tr>
  <tr>
   <td><p><strong>Navegadores acordeão</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>Preenchimento para opção de acordeão</p> </td>
  </tr>
 </tbody>
</table>

## Estilo do painel {#panel-styling}

Um Painel inclui uma barra de ferramentas opcional e seu conteúdo.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guidePanelNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>panel-background-color</code></p> </td>
   <td><p>Cor do plano de fundo do painel</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-size</code></p> </td>
   <td><p>Tamanho da fonte para o texto do painel</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-color</code></p> </td>
   <td><p>Cor da fonte para o texto do painel<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>panel-padding</code></p> </td>
   <td><p>Preenchimento dentro do painel</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>Tamanho da fonte da descrição do painel</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-padding</code></p> </td>
   <td><p>Preenchimento da descrição do painel</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo para a ajuda do painel</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-border-indicator-color</code></p> </td>
   <td><p>Cor da borda do indicador para a ajuda do painel</p> </td>
  </tr>
 </tbody>
</table>

O nó do painel é dividido em navegadores e conteúdo. `` `` não há um componente de estilo separado para o conteúdo. As variáveis descritas são aplicadas no navegador e também no conteúdo.

O painel mais superior (RootPanel) não tem essa classe.

## Estilo móvel {#mobile-styling}

## Barra de cabeçalho {#header-bar}

Essas variáveis influenciam a barra de cabeçalho visível em um dispositivo móvel ou em dispositivos de tela pequena que contêm o título do painel e navegadores ao lado e ao verso.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guide-header-bar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-background-color</code></p> </td>
   <td><p>Cor do plano de fundo da barra de cabeçalho</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-font-color</code></p> </td>
   <td><p>Cor da fonte do texto dentro da barra de cabeçalho</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>Preenchimento da barra de cabeçalho</p> </td>
  </tr>
 </tbody>
</table>

## Indicador de rolagem {#scroll-indicator}

Essas variáveis influenciam o indicador de Rolagem, que é uma seta laranja que aparece em um dispositivo móvel ou em dispositivos de tela pequena. Um indicador de Rolagem indica que há conteúdo além da parte visível da tela. Você pode rolar para baixo para vê-lo. Quando você atinge o fim do conteúdo, a seta desaparece.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>mobileScrollIndicator</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorBottom</code></p> </td>
   <td><p>Posição fixa do indicador de rolagem na parte inferior</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>Posição fixa do indicador de rolagem à direita</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>Largura do indicador de rolagem</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>Altura do indicador de rolagem</p> </td>
  </tr>
 </tbody>
</table>

## Variáveis específicas do layout da barra de ferramentas fixa para dispositivos móveis {#mobile-fixed-toolbar-layout-specific-variables}

Essas variáveis na tabela a seguir influenciam o layout da barra de ferramentas fixa para dispositivos móveis.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>mobileToolbar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarBottom</code></p> </td>
   <td><p>Posição fixa da barra de ferramentas, no dispositivo móvel, na parte inferior</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>Posição fixa da barra de ferramentas, no dispositivo móvel, na parte superior</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>Posição fixa da barra de ferramentas, no dispositivo móvel, à esquerda</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>Posição fixa da barra de ferramentas, no dispositivo móvel, à direita</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>Posição fixa do ícone dos botões da barra de ferramentas, na parte superior</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconWidth</code></p> </td>
   <td><p>Largura do ícone dos botões da barra de ferramentas no dispositivo móvel</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconHeight</code></p> </td>
   <td><p>Altura do ícone dos botões da barra de ferramentas no dispositivo móvel</p> </td>
  </tr>
  <tr>
   <td><p><code>mobilefixedtoolbarbgcolor</code></p> </td>
   <td><p>Cor do plano de fundo da barra de ferramentas no dispositivo móvel</p> </td>
  </tr>
 </tbody>
</table>

## Variável específica do tema {#theme-specific-variable}

O tema **Simple enrollment** em /etc/clientlibs/fd/af/guidetheme/simpleEnrollment e a categoria `guide.theme.simpleEnrollment` também apresentam algumas variáveis. Se quiser criar um tema que aprimore a inscrição simples, você pode usar as seguintes &quot;variáveis extras:

<table>
 <tbody>
  <tr>
   <td><p><strong>Variáveis </strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-focus-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo do botão em foco</p> </td>
  </tr>
  <tr>
   <td><p><code>button-hover-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo do botão ao passar o mouse</p> </td>
  </tr>
  <tr>
   <td><p><code>button-radius</code></p> </td>
   <td><p>Raio do botão</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo para botões de navegação (voltar/próximo)</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>Cor do plano de fundo para botões de navegação (voltar/próximo) ao passar o mouse</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>Cor do plano de fundo para navegadores do assistente e barra de progresso correspondente, quando renderizados pela primeira vez.</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>Cor do plano de fundo do navegador atual / ativo do assistente e barra de progresso correspondente </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>Cor do plano de fundo para navegadores do assistente e barra de progresso correspondente, que foram visitados.</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>Contêiner de bifurcação de cores da borda em navegadores e painéis</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>Guias separadoras de cores da borda inferior para guias à esquerda (navegadores de guias).</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>Cor do plano de fundo para navegadores aninhados/filhos/subnavegadores</p> </td>
  </tr>
 </tbody>
</table>

