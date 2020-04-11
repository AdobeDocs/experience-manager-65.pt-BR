---
title: Criação de estilos CSS para formulários HTML5
seo-title: Criação de estilos CSS para formulários HTML5
description: Saiba como alterar a aparência de formulários HTML5 modificando a classe CSS associada ao elemento de formulário HTML.
seo-description: Saiba como alterar a aparência de formulários HTML5 modificando a classe CSS associada ao elemento de formulário HTML.
uuid: 43c689b4-243c-43de-a8be-1eef10d75295
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Criação de estilos CSS para formulários HTML5 {#creating-css-styles-for-html-forms}

A execução HTML5 de um modelo de formulário baseado em XFA consiste em vários elementos HTML. Esses elementos são organizados em uma ordem. Cada elemento tem classes CSS bem definidas. Você pode usar essa classe CSS para selecionar e alterar a aparência de um elemento.

>[!NOTE]
>
>Nas classes CSS, não altere o valor da largura, altura, espessura da borda, superior, esquerda, direita, inferior, preenchimento, margem e outros atributos de posição e tamanho. Qualquer alteração nos atributos de posição e tamanho traz alterações ao layout do formulário.

## Classes CSS para elementos {#css-classes-nbsp-for-elements-nbsp}

Cada elemento contém classes CSS bem definidas. É possível modificar essas classes para alterar a aparência de um elemento. Cada elemento, exceto os elementos field e draw, tem duas classes CSS - classe Type e classe Name.

* A classe **** Type representa o tipo do campo XFA. Você pode substituir a `type` classe para modificar os estilos de todos os elementos de um tipo específico.

* A classe **** Name corresponde ao nome do campo XFA. Você pode substituir a `name` classe para modificar e aplicar um estilo personalizado a um elemento.

>[!NOTE]
>
>Alguns elementos XFA não têm um nome. Para alterar os estilos desses componentes, modifique todos os componentes desse tipo específico.

Para as páginas não nomeadas no AEM Forms Designer, as páginas em um formulário HTML5 são nomeadas na ordem crescente de seu número. Por exemplo, para um formulário HTML5 com duas páginas, as páginas são nomeadas Página1, Página2.

## Elemento de campo {#field-element}

O elemento field contém dois elementos aninhados: widget e legenda.

**Elemento de widget**

O elemento do widget contém o elemento da interface do usuário para interação com os usuários. Ele tem três classes de CSS:

* **Widget**: Todo widget tem essa classe.
* **name**: Todos os widgets enviados com o AEM contêm a classe de nome do widget. Para widgets personalizados, o desenvolvedor do widget fornece a classe de nome do Widget.
* **tipo**: Todo widget tem um elemento de interface do usuário. Essa classe define o tipo do elemento da interface do usuário.

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

Além da classe type e name, o componente field também contém uma classe CSS adicional chamada **subtype**. Um subtipo identifica qual tipo de campo é, por exemplo, NumericField, DateField, TextField. É possível substituir a classe de subtipo para modificar o estilo de todos os campos do tipo, subtipo.

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
   <td>Nome<br /> definido pelo usuário ou<br /> Page&lt;pageNumber&gt; (padrão)</td>
  </tr>
  <tr>
   <td>Área de conteúdo</td>
   <td>área de conteúdo</td>
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

O AEM Forms Designer oferece suporte a diferentes tipos de campos em um formulário como NumericField, DecimalField e Data Field. Todos esses campos em HTML contêm as classes CSS mencionadas acima. Eles também contêm algumas classes adicionais dependendo do tipo de campo.

Cada campo tem um widget associado que representa o elemento da interface do usuário. As classes de cada campo e os widgets associados a cada campo são listados abaixo.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de campo</strong></td>
   <td><strong>Subtipo</strong></td>
   <td><strong>Nome do widget</strong></td>
   <td><strong>Tipo de Widget</strong></td>
   <td><strong>Tag da interface do usuário HTML</strong></td>
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
   <td>checkbox<br /> </td>
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
   <td>textfield<br type="_moz" /> </td>
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
   <td>choicelist<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>select</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
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
   <td>tipo de entrada=senha<br type="_moz" /> </td>
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
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>tipo de entrada=texto<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Classes CSS para diferentes Elementos de desenho {#css-classes-for-different-draw-elements}

É possível inserir elementos de desenho estáticos, como texto e imagens, usando o AEM Forms Designer. Para cada elemento draw, uma classe CSS separada é associada a esse elemento. A lista das classes CSS para elementos draw está listada abaixo. Cada elemento draw tem uma classe draw associada a ele.

| **Tipo de desenho** | **Classe CSS** |
|---|---|
| Texto | texto |
| Imagem | imagem |
| Retângulo | rectangle |
| Linha | line |

## Estilo de outras partes do formulário {#styling-other-parts-of-the-form}

Além da aparência dos componentes da interface no formulário HTML, é possível alterar o estilo de elementos como Erros em linha, Avisos em linha e campos com erros de validação.

`Styling Inline Errors`

Quando a validação de um campo resulta em um erro, um erro em linha é exibido quando o campo está ativo. Para alterar o estilo dos erros em linha, substitua a ID CSS **error-msg**.

`Styling Inline Warnings`

Quando a validação de um campo resulta em um aviso, um aviso em linha é exibido quando o campo está ativo. Para alterar o estilo desses avisos embutidos, substitua o **warning-msg** da ID CSS.

`Styling Fields with Validation Errors`

Quando a validação de um campo falha, o estilo do widget muda. Essa alteração de estilo é feita aplicando um **widgetError** de classe CSS no componente do widget. Para modificar o estilo padrão, substitua a classe **widgetError** .
