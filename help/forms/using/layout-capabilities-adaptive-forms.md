---
title: Recursos de layout de formulários adaptáveis
seo-title: Recursos de layout de formulários adaptáveis
description: O layout e as aparências de formulários adaptáveis em vários dispositivos são controlados pelas configurações de layout. Entenda os vários layouts e como aplicá-los.
seo-description: O layout e as aparências de formulários adaptáveis em vários dispositivos são controlados pelas configurações de layout. Entenda os vários layouts e como aplicá-los.
uuid: 79022ac2-1aa3-47c5-b094-cbe83334ea62
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9459c414-eac9-4bd9-a773-cceaeb736c56
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 1%

---


# Recursos de layout de formulários adaptáveis{#layout-capabilities-of-adaptive-forms}

O Adobe Experience Manager (AEM) permite criar formulários adaptáveis fáceis de usar que oferecem experiências dinâmicas para os usuários finais. O layout do formulário controla como os itens ou componentes são exibidos em um formulário adaptável.

## Conhecimento pré-requisito {#prerequisite-knowledge}

Antes de saber mais sobre os diferentes recursos de layout de formulários adaptáveis, leia os artigos a seguir para saber mais sobre formulários adaptáveis.

[Introdução ao AEM Forms](../../forms/using/introduction-aem-forms.md)

[Introdução à criação de formulários](../../forms/using/introduction-forms-authoring.md)

## Tipos de layouts {#types-of-layouts}

Um formulário adaptável fornece os seguintes tipos de layouts:

**** Layout do painelControla como os itens ou componentes dentro de um painel são exibidos em um dispositivo.

**Layout** móvel Controla a navegação de um formulário em um dispositivo móvel. Se a largura do dispositivo for de 768 pixels ou mais, o layout será considerado um layout móvel e otimizado para um dispositivo móvel.

**Layout da barra de ferramentas** Controla a posição dos botões de Ação na barra de ferramentas ou no painel em um formulário.

Todos esses layouts de painel são definidos no seguinte local:

`/libs/fd/af/layouts`.

>[!NOTE]
>
>Para alterar o layout de um formulário adaptável, use o Modo de criação no AEM.

![Localização dos layouts no repositório CRX](assets/layouts_location_in_crx.png)

## Layout do painel {#panel-layout}

Um autor de formulário pode associar um layout a cada painel de um formulário adaptável, incluindo o painel raiz.

Os layouts do Painel estão disponíveis no local `/libs/fd/af/layouts/panel`.

![Lista de layouts de painel para o painel raiz de um formulário adaptável](assets/layouts.png)

Lista de layouts de painel em formulários adaptáveis

### Responsivo - tudo em uma página sem navegação {#responsive-everything-on-one-page-without-navigation-br}

Use este layout de painel para criar um layout responsivo que se ajuste ao tamanho da tela do seu dispositivo sem precisar de navegação especializada.

Usando esse layout, você pode colocar vários componentes **[!UICONTROL Painel adaptáveis de formulário]** um após o outro dentro do painel.

![Um formulário usando um layout responsivo, como visto em uma tela pequena](assets/responsive_layout_seen_on_small_screen.png)

Um formulário usando um layout responsivo, como visto em uma tela pequena

![Um formulário usando um layout responsivo, como visto em uma tela grande](assets/responsive_layout_seen_on_large_screen.png)

Um formulário usando um layout responsivo, como visto em uma tela grande

### Assistente - um formulário de várias etapas que mostra uma etapa de cada vez {#wizard-a-multi-step-form-showing-one-step-at-a-time}

Use esse layout de painel para fornecer a navegação guiada dentro de um formulário. Por exemplo, use esse layout quando desejar capturar informações obrigatórias em um formulário, ao mesmo tempo em que orienta os usuários passo a passo.

Use o componente `Panel adaptive form` para fornecer a navegação passo a passo dentro de um painel. Quando você usa esse layout, um usuário move para a próxima etapa somente após a conclusão da etapa atual

```javascript
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![Expressão de conclusão de etapa no layout do Assistente para um formulário de várias etapas](assets/layout-sidebar.png)

Expressão de conclusão de etapa no layout do Assistente para um formulário de várias etapas

![Um formulário usando o layout do assistente](assets/wizard-layout.png)

Um formulário usando o Assistente

### Layout para design de acordeão {#layout-for-accordion-design}

Usando esse layout, você pode colocar o componente `Panel adaptive form` em um painel com navegação no estilo acordeão. Com esse layout, também é possível criar painéis repetitivos. Painéis repetitivos permitem adicionar ou remover dinamicamente painéis, conforme necessário. Você pode definir o número mínimo e máximo de vezes que um painel se repete. Além disso, o título do painel pode ser determinado dinamicamente, com base nas informações fornecidas nos itens do painel.

A expressão Summary pode ser usada para mostrar os valores fornecidos pelo usuário final no título do painel minimizado.

![Painéis repetíveis usando o layout Acordeão em formulários adaptáveis](assets/repeatable_panels_using_accordion_layout.png)

Painéis repetitivos criados com o layout Acordeão

### Layout com guias - as guias são exibidas à esquerda {#tabbed-layout-tabs-appear-on-the-left}

Com esse layout, é possível colocar o componente `Panel adaptive form` em um painel com a navegação por guias. As guias são colocadas à esquerda do conteúdo do painel.

![No layout Tabbed , as guias são exibidas à esquerda](assets/tabbed_layout_left.png)

Guias que aparecem à esquerda de um painel

### Layout com guias - as guias são exibidas na parte superior {#tabbed-layout-tabs-appear-on-the-top}

Com esse layout, é possível colocar o componente `Panel adaptive form` em um painel com a navegação por guias. As guias são colocadas sobre o conteúdo do painel.

![Layout com guias em formulários adaptáveis com guias na parte superior](assets/tabbed_layout_top.png)

Guias que aparecem na parte superior de um painel

## Layouts móveis {#mobile-layouts}

Os layouts móveis permitem uma navegação simples nos dispositivos móveis com telas relativamente menores. Os layouts móveis usam estilos de guias ou de assistente para navegação de formulários. Aplicar um layout móvel fornece um único layout para todo o formulário.

Esse layout controla a navegação usando uma barra de navegação e um menu de navegação. A barra de navegação mostra o ícone **&lt;** e **** para indicar **próximo** e **etapas de navegação anteriores** no formulário.

Os Layouts móveis estão disponíveis no local `/libs/fd/af/layouts/mobile/`. Os seguintes layouts para dispositivos móveis estão disponíveis em formulários adaptáveis, por padrão.

![Lista de layouts para dispositivos móveis em formulários adaptáveis](assets/mobile-navigation.png)

Lista de layouts para dispositivos móveis em formulários adaptáveis

Ao usar um layout móvel, o menu de formulário, para acessar vários painéis de formulário, está disponível ao tocar no ícone ![aem6forms_form_menu](assets/aem6forms_form_menu.png) .

### Layout com títulos de painel no cabeçalho do formulário {#layout-with-panel-titles-in-the-form-header}

Esse layout, como o nome sugere, mostra os títulos do painel junto com o menu de navegação e a barra de navegação. Esse layout também fornece ícones Próximo e Anterior para navegação.

![Layouts para dispositivos móveis com títulos de painéis nos cabeçalhos do formulário](assets/mobile_layout_with.png)

Layouts para dispositivos móveis com títulos de painéis nos cabeçalhos do formulário

### Layout sem títulos de painel no cabeçalho do formulário {#layout-without-panel-titles-in-the-form-header}

Esse layout, como o nome sugere, mostra somente o menu de navegação e a barra de navegação sem títulos de painel. Esse layout também fornece ícones Próximo e Anterior para navegação.

![Layouts para dispositivos móveis sem títulos de painéis nos cabeçalhos do formulário](assets/mobile_layout_without.png)

Layouts para dispositivos móveis sem títulos de painéis nos cabeçalhos do formulário

## Layouts da barra de ferramentas {#toolbar-layouts}

Um Layout da barra de ferramentas controla o posicionamento e a exibição de todos os botões de ação adicionados aos formulários adaptáveis. O layout pode ser adicionado em um nível de formulário ou em um painel.

![Uma lista de Layouts da barra de ferramentas em formulários adaptáveis para controlar o layout de botões](assets/toolbar-layouts.png)

Uma lista de Layouts da barra de ferramentas em formulários adaptáveis

Os layouts da barra de ferramentas estão disponíveis no local `/libs/fd/af/layouts/toolbar`. por padrão, os formulários adaptáveis fornecem os seguintes Layouts da barra de ferramentas.

### Layout padrão da barra de ferramentas {#default-layout-for-toolbar}

Esse layout é selecionado como o layout padrão quando você adiciona botões de ação em um formulário adaptável. Selecionar esse layout exibe o mesmo layout para dispositivos móveis e de desktop.

Além disso, é possível adicionar várias barras de ferramentas contendo botões de ação configurados com esse layout. Um botão de ação está associado a um controle de formulário. É possível configurar as barras de ferramentas para serem anteriores ou posteriores a um painel.

![Exibição padrão da barra de ferramentas](assets/toolbar_layout_default.png)

Exibição padrão da barra de ferramentas

### Layout móvel fixo para a barra de ferramentas {#mobile-fixed-layout-for-toolbar}

Selecione este layout para fornecer layouts alternativos para dispositivos móveis e desktop.

Para o layout da área de trabalho, é possível adicionar botões de ação usando alguns rótulos específicos. Somente uma barra de ferramentas pode ser configurada com esse layout. Se mais de uma barra de ferramentas estiver configurada com esse layout, há uma sobreposição para dispositivos móveis e apenas uma barra de ferramentas estará visível. Por exemplo, é possível ter uma barra de ferramentas na parte inferior ou superior do formulário ou, depois ou antes dos painéis no formulário.

Para o layout móvel, é possível adicionar botões de ação usando ícones.

![Layout móvel fixo para a barra de ferramentas](assets/toolbar_layout_mobile_fixed.png)

Layout móvel fixo para a barra de ferramentas

