---
title: Criação de estilos CSS para formulários HTML5
seo-title: Creating CSS styles for HTML5 forms
description: Saiba como alterar a aparência dos formulários HTML5 modificando a classe CSS associada ao elemento de formulário HTML.
seo-description: Learn how to change the appearance of HTML5 forms by modifying the CSS class associated with the HTML form element.
uuid: 43c689b4-243c-43de-a8be-1eef10d75295
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
feature: Mobile Forms
exl-id: 8cc90ff7-284e-41cd-bfda-7fa09371e270
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 4%

---

# Criação de estilos CSS para formulários HTML5 {#creating-css-styles-for-html-forms}

A representação de HTML5 de um template de formulário baseado em XFA consiste em vários elementos de HTML. Esses elementos são organizados em ordem. Cada elemento tem classes CSS bem definidas. Você pode usar essa classe CSS para selecionar e alterar a aparência de um elemento.

>[!NOTE]
>
>Nas classes CSS, não altere o valor da largura, altura, espessura da borda, parte superior, esquerda, direita, parte inferior, preenchimento, margem e outros atributos de posição e tamanho. Qualquer alteração na posição e nos atributos de tamanho traz alterações ao layout do formulário.

## Classes CSS para elementos  {#css-classes-nbsp-for-elements-nbsp}

Cada elemento contém classes CSS bem definidas. Você pode modificar essas classes para alterar a aparência de um elemento. Cada elemento, exceto os elementos field e draw , tem duas classes CSS - classe Type e classe Name .

* O **Classe de tipo** representa o tipo do campo XFA. Você pode substituir o `type` classe para modificar os estilos de todos os elementos de um tipo específico.

* O **Classe de nome** corresponde ao nome do campo XFA. Você pode substituir o `name` classe para modificar e aplicar estilo personalizado a um elemento.

>[!NOTE]
>
>Alguns elementos XFA não têm um nome. Para alterar os estilos desses componentes, modifique todos os componentes desse tipo específico.

Para as páginas não nomeadas no AEM Forms Designer, as páginas em um formulário HTML5 são nomeadas na ordem crescente de seu número. Por exemplo, para um formulário HTML5 com duas páginas, as páginas são nomeadas Página1, Página2.

## Elemento de campo {#field-element}

O elemento field contém dois elementos aninhados: widget e legenda.

**Elemento de widget**

O elemento de widget contém o elemento da interface do usuário para interação com usuários. Ele tem três classes CSS:

* **Widget**: Todo widget tem essa classe.
* **name**: Todos os widgets enviados com AEM contêm a classe de nome de widget. Para widgets personalizados, o desenvolvedor do widget fornece a classe de nome do widget.
* **type**: Cada widget tem um elemento da interface do usuário. Essa classe define o tipo do elemento da interface do usuário.

```xml
<!--field with caption-->
<div class="field numericfield NumericField3 ">
     <div class="caption">
        caption content
     </div>
     <div class="widget numericfieldwidget numericInput">
       widget content
     </div>
</div>

<!--field without caption-->
<div class="widget numericfieldwidget numericInput">
   widget content
</div>
```

Além do tipo e da classe de nome, o componente de campo também contém uma classe CSS adicional chamada **subtipo**. Um subtipo identifica qual tipo de campo é, por exemplo, NumericField, DateField, TextField. É possível substituir a classe do subtipo para modificar o estilo de todos os campos do tipo , do subtipo .

## Classes CSS para diferentes componentes {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>Componente</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Nome</strong></td>
  </tr>
  <tr>
   <td>Página</td>
   <td>page</td>
   <td>Nome definido pelo usuário<br /> ou<br /> Página&lt;pagenumber&gt; (padrão)</td>
  </tr>
  <tr>
   <td>Área de conteúdo</td>
   <td>contentarea</td>
   <td>Nome definido pelo usuário</td>
  </tr>
  <tr>
   <td>Subformulário</td>
   <td>subformulário</td>
   <td>Nome definido pelo usuário</td>
  </tr>
  <tr>
   <td>Grupo de exclusão</td>
   <td>exclgroup</td>
   <td>Nome definido pelo usuário</td>
  </tr>
  <tr>
   <td>Draw</td>
   <td>draw</td>
   <td>Nome definido pelo usuário</td>
  </tr>
  <tr>
   <td>Texto</td>
   <td>campo</td>
   <td>Nome definido pelo usuário</td>
  </tr>
  <tr>
   <td>Legenda</td>
   <td>caption</td>
   <td>ND</td>
  </tr>
  <tr>
   <td>Widget</td>
   <td>widget</td>
   <td>O desenvolvedor do widget o define (para widgets definidos pelo usuário, consulte a tabela na seção a seguir)</td>
  </tr>
 </tbody>
</table>

## Classes CSS para diferentes campos {#css-classes-for-different-fields}

O AEM Forms Designer oferece suporte a diferentes tipos de campos em um formulário como NumericField, DecimalField e Date Field. Todos esses campos no HTML contêm as classes CSS mencionadas acima. Eles também contêm algumas classes extras, dependendo do tipo de campo.

Cada campo tem um widget associado que representa o elemento da interface do usuário. As classes de cada campo e os widgets associados a cada campo são listados abaixo.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de campo</strong></td>
   <td><strong>Subtipo</strong></td>
   <td><strong>Nome do widget</strong></td>
   <td><strong>Tipo de widget</strong></td>
   <td><strong>Tag da interface do usuário do HTML</strong></td>
  </tr>
  <tr>
   <td>Botão<br type="_moz" /> </td>
   <td>ND</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttonfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=botão<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=caixa de seleção<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateField<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateTimeField<br type="_moz" /> </td>
   <td>campo de texto<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DropDown<br type="_moz" /> </td>
   <td>choicelista<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>select</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>choicelista<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>NumericField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>PasswordField<br type="_moz" /> </td>
   <td>passwordfield<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>passwordfieldwidget<br type="_moz" /> </td>
   <td>input type=password<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>RadioButton<br type="_moz" /> </td>
   <td>radiocampo<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>radiofieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=rádio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TextField<br type="_moz" /> </td>
   <td>campo de texto<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>campo de texto<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Classes CSS para diferentes Elementos de Desenho {#css-classes-for-different-draw-elements}

É possível inserir elementos de desenho estático, como texto e imagens, usando o AEM Forms Designer. Para cada elemento draw , uma classe CSS separada é associada a esse elemento. A lista de classes CSS para elementos draw está listada abaixo. Cada elemento draw tem uma classe draw associada a ele.

| **Tipo de desenho** | **Classe CSS** |
|---|---|
| Texto | text |
| Imagem | imagem |
| Retângulo | rectangle |
| Linha | linha |

## Estilo de outras partes do formulário {#styling-other-parts-of-the-form}

Além da aparência dos componentes da interface do usuário no formulário HTML, você pode alterar o estilo de elementos como Erros em linha, Avisos em linha e campos com erros de validação.

`Styling Inline Errors`

Quando a validação de um campo resulta em um erro, um erro em linha é exibido quando o campo está ativo. Para alterar o estilo dos erros em linha, substitua a ID do CSS **error-msg**.

`Styling Inline Warnings`

Quando a validação de um campo resulta em um aviso, um aviso em linha é exibido quando o campo está ativo. Para alterar o estilo desses avisos em linha, substitua a ID de CSS **warning-msg**.

`Styling Fields with Validation Errors`

Quando a validação de um campo falha, o estilo do widget muda. Essa alteração de estilo é feita pela aplicação de uma classe CSS **widgetError** no componente de widget. Para modificar o estilo padrão, substitua o **widgetError** classe .
