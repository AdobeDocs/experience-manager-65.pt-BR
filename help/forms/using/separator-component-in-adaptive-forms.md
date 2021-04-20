---
title: Componente separador em formulários adaptáveis
seo-title: Componente separador em formulários adaptáveis
description: Você pode usar o componente separador para separar visualmente seções de um formulário.
seo-description: Você pode usar o componente separador para separar visualmente seções de um formulário.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Componente separador em formulários adaptáveis{#separator-component-in-adaptive-forms}

Você pode usar o componente separador para segregar visualmente os painéis de um formulário. Você pode definir a aparência e o estilo gerais de um componente separador especificando as seguintes propriedades do componente separador:

* **Nome do elemento:** Especifica o nome do componente. As expressões SOM endereçam o componente com o valor especificado no campo Nome do elemento .
* **Espessura:** Especifica a espessura do componente separador em pixels.

* **Classe CSS:** Especifica a classe CSS personalizada para o componente separador

* **Estilos em linha:** com o AEM Forms, agora é possível aplicar estilos de CSS em linha a componentes de formulário adaptáveis individuais e visualizar as alterações em tempo real.

Você pode usar o modo Layout para definir o número de colunas nas quais o componente separador se expande. Para obter mais informações, consulte [Usar o modo Layout para redimensionar componentes](../../forms/using/resize-using-layout-mode.md).

Para especificar as propriedades de um componente separador:

1. Selecione um componente separador e toque em ![cmppr](assets/cmppr.png). As propriedades são abertas na barra lateral.
1. Clique em uma guia na seção Propriedades de CSS em linha para especificar as propriedades de CSS. Por exemplo: a. Na guia Campo, clique em **Adicionar item**. Uma linha com dois campos é adicionada.
1. No primeiro campo à esquerda, especifique uma propriedade CSS3 que deseja aplicar. Por exemplo, **border**. Você também pode selecionar uma propriedade clicando no botão de seta para baixo. A lista suspensa não é exaustiva e você pode especificar qualquer nome de propriedade CSS3 compatível nesse campo.
1. No campo adjacente, especifique um valor válido para a propriedade CSS3 especificada. Por exemplo, **3px preto sólido**.
1. Clique em **Adicionar Item** para especificar outra propriedade e seu valor.
1. Clique em **Preview** para visualizar as alterações no formulário.
1. Clique em **OK** para confirmar as alterações ou em **Cancelar** para sair da caixa de diálogo sem alterações.

