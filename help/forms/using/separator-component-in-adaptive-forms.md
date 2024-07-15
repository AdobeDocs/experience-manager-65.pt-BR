---
title: Componente separador em formulários adaptáveis
description: Você pode usar o componente separador para segregar visualmente seções de um formulário.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Componente separador em formulários adaptáveis{#separator-component-in-adaptive-forms}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve uma abordagem mais antiga para a criação do Forms adaptável usando componentes de base. </span>

Você pode usar o componente separador para segregar visualmente os painéis de um formulário. Você pode definir a aparência geral e o estilo de um componente separador especificando as seguintes propriedades do componente separador:

* **Nome do Elemento:** Especifica o nome do componente. As expressões SOM endereçam o componente com um valor especificado no campo Nome do elemento.
* **Espessura:** Especifica a espessura do componente separador em pixels.

* **Classe CSS:** Especifica a classe CSS personalizada para o componente separador

* **Estilos em linha:** com o AEM Forms, agora é possível aplicar estilos CSS em linha a componentes de formulário adaptáveis individuais e visualizar as alterações em tempo real.

Você pode usar o modo Layout para definir o número de colunas ao qual o componente separador se estende. Para obter mais informações, consulte [Usar o modo de layout para redimensionar componentes](../../forms/using/resize-using-layout-mode.md).

Para especificar as propriedades de um componente separador:

1. Selecione um componente separador e selecione ![cmppr](assets/cmppr.png). As propriedades são abertas na barra lateral.
1. Clique em uma guia na seção Propriedades CSS em linha para especificar propriedades CSS. Por exemplo: a. Na guia Field, clique em **Add Item**. Uma linha com dois campos é adicionada.
1. No primeiro campo à esquerda, especifique uma propriedade CSS3 que deseja aplicar. Por exemplo, **borda**. Você também pode selecionar uma propriedade clicando no botão de seta para baixo. A lista suspensa não é exaustiva e você pode especificar qualquer nome de propriedade CSS3 compatível nesse campo.
1. No campo adjacente, especifique um valor válido para a propriedade CSS3 especificada. Por exemplo, **3-px preto sólido**.
1. Clique em **Adicionar Item** para especificar outra propriedade e seu valor.
1. Clique em **Visualizar** para que você possa visualizar as alterações no formulário.
1. Clique em **OK** se desejar confirmar as alterações ou em **Cancelar** para sair da caixa de diálogo sem alterações.
