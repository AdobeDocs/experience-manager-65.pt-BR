---
title: Estilo em linha de componentes de formulário adaptáveis
seo-title: Propriedades CSS embutidas para componentes de formulário adaptáveis
description: Embora seja possível aplicar estilos personalizados em um formulário adaptável, também é possível aplicar propriedades de CSS em linha em componentes individuais de um formulário adaptável.
seo-description: Embora seja possível aplicar estilos personalizados em um formulário adaptável, também é possível aplicar propriedades de CSS em linha em componentes individuais de um formulário adaptável.
uuid: e863780e-2250-4bea-9569-22be5638d54e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 21dec713-c76d-408b-baea-fc585377b429
docset: aem65
feature: Formulários adaptáveis
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 3%

---


# Estilo em linha de componentes de formulário adaptáveis {#inline-styling-of-adaptive-form-components}

Você pode definir a aparência e o estilo gerais de um formulário adaptável especificando estilos usando o [editor de temas](../../forms/using/themes.md). Além disso, você pode aplicar estilos CSS em linha a componentes de formulário adaptáveis individuais e visualizar as alterações dinamicamente. Os estilos em linha substituem o estilo fornecido no tema.

## Aplicar propriedades CSS em linha {#apply-inline-css-properties}

Para adicionar estilos em linha a um componente:

1. Abra o formulário no editor de formulário e altere o modo para o modo de estilo. Para alterar o modo para o modo de estilo, na barra de ferramentas da página, toque em ![tela suspensa](assets/canvas-drop-down.png) > **Estilo**.
1. Selecione um componente na página e toque no botão de edição ![edit-button](assets/edit-button.png). Propriedades de estilo abertas na barra lateral.

   Você também pode selecionar componentes da árvore de hierarquia do formulário na barra lateral. A árvore da hierarquia do formulário está disponível como Objetos de formulário na barra lateral.

   Você também pode selecionar um componente na barra lateral. No modo Estilo , é possível ver os componentes listados em Objetos de formulário. No entanto, a lista Objetos de formulário na barra lateral lista componentes como campos e painéis. Campos e painéis são componentes genéricos que podem conter componentes, como caixa de texto e botões de opção.

   Ao selecionar um componente na barra lateral, você verá todos os subcomponentes listados e as propriedades do componente selecionado. Você pode selecionar um subcomponente específico e estilizá-lo.

1. Clique em uma guia na barra lateral para especificar as propriedades de CSS. É possível especificar propriedades, como:

   * Dimension &amp; Posição (Configuração de exibição, preenchimento, altura, largura, margem, posição, índice z, flutuante, limpar, sobrefluxo)
   * Texto (família da fonte, peso, cor, tamanho, altura da linha e alinhamento)
   * Plano de fundo (Imagem e gradiente, cor do plano de fundo)
   * Borda (Largura, estilo, cor, raio)
   * Efeitos (sombra, opacidade)
   * Avançado (Permite gravar CSS personalizado para o componente)

1. Da mesma forma, é possível aplicar estilos para outras partes de um componente, como Widget, Legenda e Ajuda.
1. Toque em **Concluído** para confirmar as alterações ou em **Cancelar** para descartar as alterações.

## Exemplo: estilos em linha para um componente de campo {#example-inline-styles-for-a-field-component}

As imagens a seguir representam um campo de texto antes e depois da aplicação dos estilos em linha.

![Componente de caixa de texto antes da aplicação do estilo em linha](assets/no-style.png)

Componente de caixa de texto antes de aplicar as propriedades de estilo em linha

Observe a alteração no estilo da caixa de texto, como mostrado na imagem a seguir, após aplicar as seguintes propriedades de CSS.

<table>
 <tbody>
  <tr>
   <td><p>Seletor</p> </td>
   <td><p>Propriedade CSS</p> </td>
   <td><p>Valor</p> </td>
   <td><p>Efeito</p> </td>
  </tr>
  <tr>
   <td><p>Texto</p> </td>
   <td><p>border</p> </td>
   <td><p>Largura da borda =2px</p> <p>Estilo da borda=Sólido</p> <p>Cor da borda=#1111</p> </td>
   <td><p>Cria uma borda larga de 2px preta em torno do campo</p> </td>
  </tr>
  <tr>
   <td><p>Caixa de texto</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Altera a cor de fundo para CornflorBlue (#6495ED)</p> <p>Observação: Você pode especificar um nome de cor ou seu código hexadecimal no campo de valor.</p> </td>
  </tr>
  <tr>
   <td><p>Etiqueta</p> </td>
   <td><p>Dimensões e posição &gt; largura</p> </td>
   <td><p>100px</p> </td>
   <td><p>Corrige a largura como 100px para o rótulo</p> </td>
  </tr>
  <tr>
   <td>Ícone da ajuda do campo</td>
   <td>Texto &gt; Cor da fonte</td>
   <td>#2ECC40</td>
   <td>Altera a cor da face do ícone de ajuda.</td>
  </tr>
  <tr>
   <td><p>Descrição longa</p> </td>
   <td><p>text-align</p> </td>
   <td><p>center</p> </td>
   <td><p>Alinha a descrição longa para a ajuda do centro</p> </td>
  </tr>
 </tbody>
</table>

![Estilo da caixa de texto após a aplicação do estilo em linha](assets/applied-style.png)

Componente de caixa de texto após aplicar as propriedades de estilo em linha

Após as etapas acima, você pode selecionar e criar um estilo para outros componentes, como painéis, botões Enviar e botões de opção.

>[!NOTE]
>
>As propriedades de estilo variam de acordo com o componente selecionado.

