---
title: Estilo em linha de componentes de formulário adaptáveis
description: Embora você possa aplicar estilos personalizados em um formulário adaptável, também pode aplicar propriedades CSS em linha a componentes individuais de um formulário adaptável.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 67cfecb8-c31d-4192-904d-7bfaa1a31ea5
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 4%

---

# Estilo em linha de componentes de formulário adaptáveis {#inline-styling-of-adaptive-form-components}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/inline-style-adaptive-forms.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

Você pode definir a aparência geral e o estilo de um formulário adaptável especificando estilos com o [editor de temas](../../forms/using/themes.md). Além disso, você pode aplicar estilos CSS em linha a componentes de formulário adaptáveis individuais e visualizar as alterações em tempo real. Os estilos embutidos substituem o estilo fornecido no tema.

## Aplicar propriedades CSS em linha {#apply-inline-css-properties}

Para adicionar estilos em linha a um componente:

1. Abra o formulário no editor de formulários e altere o modo para o modo de estilo. Para alterar o modo para o modo de estilo, na barra de ferramentas da página, selecione ![tela suspensa](assets/canvas-drop-down.png) > **Estilo**.
1. Selecione um componente na página e selecione o botão de edição ![botão de edição](assets/edit-button.png). As propriedades de estilo são abertas na barra lateral.

   Você também pode selecionar componentes da árvore de hierarquia de formulários na barra lateral. A árvore de hierarquia de formulários está disponível como Objetos de formulário na barra lateral.

   Você também pode selecionar um componente na barra lateral. No modo Estilo, você pode ver os componentes listados em Objetos de formulário. No entanto, a lista Objetos de formulário na barra lateral lista componentes como campos e painéis. Campos e painéis são componentes genéricos que podem conter componentes como caixa de texto e botões de opção.

   Ao selecionar um componente na barra lateral, você verá todos os subcomponentes listados e as propriedades do componente selecionado. É possível selecionar um subcomponente específico e estilizá-lo.

1. Clique em uma guia na barra lateral para especificar as propriedades de CSS. É possível especificar propriedades como:

   * Dimension e Posição (configuração de exibição, preenchimento, altura, largura, margem, posição, índice z, flutuação, limpar, estouro)
   * Texto (Família da fonte, peso, cor, tamanho, altura da linha e alinhamento)
   * Plano de fundo (imagem e gradiente, cor do plano de fundo)
   * Borda (largura, estilo, cor, raio)
   * Efeitos (sombra, opacidade)
   * Avançado (permite escrever CSS personalizado para o componente)

1. Da mesma forma, é possível aplicar estilos a outras partes de um componente, como Widget, Legenda e Ajuda.
1. Selecione **Concluído** para confirmar as alterações ou **Cancelar** para descartar as alterações.

## Exemplo: estilos em linha para um componente de campo {#example-inline-styles-for-a-field-component}

As imagens a seguir representam um campo de texto antes e depois que estilos em linha são aplicados a ele.

![Componente de caixa de texto antes da aplicação do estilo embutido](assets/no-style.png)

Componente Caixa de texto antes de aplicar propriedades de estilo em linha

Observe a alteração no estilo da caixa de texto, como mostrado na imagem a seguir, após aplicar as seguintes propriedades CSS.

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
   <td><p>borda</p> </td>
   <td><p>Largura da borda =2px</p> <p>Estilo da borda=Sólido</p> <p>Cor da borda=#1111</p> </td>
   <td><p>Cria uma borda preta com 2 px de largura em torno do campo</p> </td>
  </tr>
  <tr>
   <td><p>Caixa de texto</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Altera a cor de fundo para CornflowerBlue (#6495ED)</p> <p>Observação: você pode especificar um nome de cor ou seu código hexadecimal no campo de valor.</p> </td>
  </tr>
  <tr>
   <td><p>Rótulo</p> </td>
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
   <td><p>centro</p> </td>
   <td><p>Alinha a descrição longa da ajuda para centralizar</p> </td>
  </tr>
 </tbody>
</table>

![Estilo da caixa de texto após a aplicação do estilo incorporado](assets/applied-style.png)

Componente Caixa de texto após aplicar propriedades de estilo em linha

Seguindo as etapas acima, você pode selecionar e estilizar outros componentes, como painéis, botões de envio e botões de opção.

>[!NOTE]
>
>As propriedades de estilo variam de acordo com o componente selecionado.
