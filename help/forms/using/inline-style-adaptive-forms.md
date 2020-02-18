---
title: Estilo em linha de componentes de formulário adaptáveis
seo-title: Propriedades de CSS em linha para componentes de formulário adaptáveis
description: Embora seja possível aplicar estilos personalizados em um formulário adaptável, também é possível aplicar propriedades CSS em linha em componentes individuais de um formulário adaptável.
seo-description: Embora seja possível aplicar estilos personalizados em um formulário adaptável, também é possível aplicar propriedades CSS em linha em componentes individuais de um formulário adaptável.
uuid: e863780e-2250-4bea-9569-22be5638d54e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 21dec713-c76d-408b-baea-fc585377b429
docset: aem65
translation-type: tm+mt
source-git-commit: 33f73225fbb2c48353c1f34db3339c0bb79d4236

---


# Estilo em linha de componentes de formulário adaptáveis {#inline-styling-of-adaptive-form-components}

É possível definir a aparência geral e o estilo de um formulário adaptável especificando estilos usando o editor [de](../../forms/using/themes.md)temas. Além disso, é possível aplicar estilos CSS em linha a componentes de formulário adaptáveis individuais e visualizar as alterações dinamicamente. Os estilos incorporados substituem o estilo fornecido no tema.

## Aplicar propriedades CSS em linha {#apply-inline-css-properties}

Para adicionar estilos incorporados a um componente:

1. Abra o formulário no editor de formulários e altere o modo para o modo de estilização. Para alterar o modo para o modo de estilização, na barra de ferramentas da página, toque em ![tela suspensa](assets/canvas-drop-down.png) > **Estilo**.
1. Selecione um componente na página e toque no botão editar, botão ![editar, botão](assets/edit-button.png). As propriedades de estilo são abertas na barra lateral.

   Também é possível selecionar componentes da árvore de hierarquia do formulário na barra lateral. A árvore da hierarquia do formulário está disponível como Objetos de formulário na barra lateral.

   Você também pode selecionar um componente na barra lateral. No modo Estilo, é possível ver os componentes listados em Objetos de formulário. Entretanto, a lista Objetos de formulário na barra lateral lista componentes como campos e painéis. Campos e painéis são componentes genéricos que podem conter componentes como caixa de texto e botões de opção.

   Ao selecionar um componente na barra lateral, você verá todos os subcomponentes listados e as propriedades do componente selecionado. Você pode selecionar um subcomponente específico e estilizá-lo.

1. Clique em uma guia na barra lateral para especificar as propriedades CSS. Você pode especificar propriedades como:

   * Dimensões e posição (configuração de exibição, preenchimento, altura, largura, margem, posição, índice z, flutuante, claro, sobrefluxo)
   * Texto (família da fonte, peso, cor, tamanho, altura da linha e alinhamento)
   * Plano de fundo (imagem e gradiente, cor do plano de fundo)
   * Borda (Largura, estilo, cor, raio)
   * Efeitos (sombra, opacidade)
   * Avançado (permite gravar CSS personalizado para o componente)

1. Da mesma forma, você pode aplicar estilos para outras partes de um componente, como Widget, Legenda e Ajuda.
1. Toque em **Concluído** para confirmar as alterações ou em **Cancelar** para descartar as alterações.

## Exemplo: estilos incorporados para um componente de campo {#example-inline-styles-for-a-field-component}

As imagens a seguir representam um campo de texto antes e depois da aplicação de estilos incorporados a ele.

![Componente de caixa de texto antes da aplicação do estilo incorporado](assets/no-style.png)

Componente da caixa de texto antes de aplicar propriedades de estilo em linha

Observe a alteração no estilo da caixa de texto como mostrado na imagem a seguir após aplicar as seguintes propriedades de CSS.

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
   <td><p>Largura da borda = 2px</p> <p>Estilo de borda=Sólido</p> <p>Cor da borda=#1111</p> </td>
   <td><p>Cria uma borda preta com largura de 2x ao redor do campo</p> </td>
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
   <td><p>Alinha a descrição longa da ajuda ao centro</p> </td>
  </tr>
 </tbody>
</table>

![Estilo da caixa de texto após a aplicação do estilo incorporado](assets/applied-style.png)

Componente da caixa de texto após aplicar propriedades de estilo em linha

Siga as etapas acima para selecionar e criar um estilo para outros componentes, como painéis, botões de envio e botões de opção.

>[!NOTE]
>
>As propriedades de estilo variam com base no componente selecionado.

