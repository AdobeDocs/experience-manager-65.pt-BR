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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 2%
---
# Componente separador em formulários adaptáveis{#separator-component-in-adaptive-forms}

A Adobe <span class="preview"> recomenda usar os [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve uma abordagem mais antiga para a criação do Forms adaptável usando componentes de base. </span>

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
