---
title: Componente separador em formulários adaptáveis
seo-title: Separator component in adaptive forms
description: Você pode usar o componente separador para segregar visualmente seções de um formulário.
seo-description: You can use the separator component to visually segregate sections of a form.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: Adaptive Forms
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 1%

---

# Componente separador em formulários adaptáveis{#separator-component-in-adaptive-forms}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-br) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

Você pode usar o componente separador para segregar visualmente os painéis de um formulário. Você pode definir a aparência geral e o estilo de um componente separador especificando as seguintes propriedades do componente separador:

* **Nome do elemento:** Especifica o nome do componente. As expressões SOM abordam o componente com o valor especificado no campo Nome do elemento.
* **Espessura:** Especifica a espessura do componente separador em pixels.

* **Classe CSS:** Especifica a classe CSS personalizada para o componente separador

* **Estilos em linha:** Com o AEM Forms, agora é possível aplicar estilos CSS em linha a componentes de formulário adaptáveis individuais e visualizar as alterações em tempo real.

Você pode usar o modo Layout para definir o número de colunas ao qual o componente separador se estende. Para obter mais informações, consulte [Usar o modo Layout para redimensionar componentes](../../forms/using/resize-using-layout-mode.md).

Para especificar propriedades de um componente separador:

1. Selecione um componente separador e toque em ![cmppr](assets/cmppr.png). As propriedades são abertas na barra lateral.
1. Clique em uma guia na seção Propriedades CSS em linha para especificar propriedades CSS. Por exemplo: a. Na guia Campo, clique em **Adicionar item**. Uma linha com dois campos é adicionada.
1. No primeiro campo a partir da esquerda, especifique uma propriedade CSS3 que deseja aplicar. Por exemplo, **borda**. Você também pode selecionar uma propriedade clicando no botão de seta para baixo. A lista suspensa não é exaustiva e você pode especificar qualquer nome de propriedade CSS3 compatível nesse campo.
1. No campo adjacente, especifique um valor válido para a propriedade CSS3 especificada. Por exemplo, **3px preto sólido**.
1. Clique em **Adicionar item** para especificar outra propriedade e seu valor.
1. Clique em **Visualizar** para visualizar as alterações no formulário.
1. Clique em **OK** para confirmar as alterações ou **Cancelar** para sair da caixa de diálogo sem alterações.
