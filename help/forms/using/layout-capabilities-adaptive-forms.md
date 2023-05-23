---
title: Recursos de layout de formulários adaptáveis
seo-title: Layout capabilities of adaptive forms
description: O layout e as aparências dos formulários adaptáveis em vários dispositivos são regidos pelas configurações de layout. Entenda os vários layouts e como aplicá-los.
seo-description: Layout and appearances of adaptive forms on various devices are governed by the layout settings. Understand the various layouts and how to apply them.
uuid: 79022ac2-1aa3-47c5-b094-cbe83334ea62
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9459c414-eac9-4bd9-a773-cceaeb736c56
docset: aem65
feature: Adaptive Forms
exl-id: 3db623a4-f1ad-4b7f-97e8-0be138aa8b26
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 1%

---

# Recursos de layout de formulários adaptáveis{#layout-capabilities-of-adaptive-forms}

O Adobe Experience Manager (AEM) permite criar formulários adaptáveis fáceis de usar que oferecem experiências dinâmicas para os usuários finais. O layout de formulário controla como os itens ou componentes são exibidos em um formulário adaptável.

## Conhecimento de pré-requisito {#prerequisite-knowledge}

Antes de saber mais sobre os diferentes recursos de layout dos formulários adaptáveis, leia os seguintes artigos para saber mais sobre formulários adaptáveis.

[Introdução ao AEM Forms](../../forms/using/introduction-aem-forms.md)

[Introdução à criação de formulários](../../forms/using/introduction-forms-authoring.md)

## Tipos de layouts {#types-of-layouts}

Um formulário adaptável fornece os seguintes tipos de layouts:

**Layout do painel** Controla como os itens ou componentes dentro de um painel são exibidos em um dispositivo.

**Layout de dispositivo móvel** Controla a navegação de um formulário em um dispositivo móvel. Se a largura do dispositivo for de 768 pixels ou mais, o layout é considerado um layout móvel e otimizado para um dispositivo móvel.

**Layout da barra de ferramentas** Controla a colocação dos botões de Ação na barra de ferramentas ou na barra de ferramentas do painel em um formulário.

Todos esses layouts de painel são definidos no seguinte local:

`/libs/fd/af/layouts`.

>[!NOTE]
>
>Para alterar o layout de um formulário adaptável, use o Modo de criação no AEM.

![Local dos layouts no repositório CRX](assets/layouts_location_in_crx.png)

## Layout do painel {#panel-layout}

Um autor de formulário pode associar um layout a cada painel de um formulário adaptável, incluindo o painel raiz.

Os layouts do painel estão disponíveis em `/libs/fd/af/layouts/panel` localização.

![Lista de layouts de painel para o painel raiz de um formulário adaptável](assets/layouts.png)

Lista de layouts de painel em formulários adaptáveis

### Responsivo - tudo em uma página sem navegação {#responsive-everything-on-one-page-without-navigation-br}

Use este layout de painel para criar um layout responsivo que se ajuste ao tamanho da tela do seu dispositivo sem qualquer necessidade de navegação especializada.

Usando este layout, você pode colocar vários **[!UICONTROL Formulário adaptável do painel]** componentes um após o outro, dentro do painel.

![Um formulário usando layout responsivo como visto em uma tela pequena](assets/responsive_layout_seen_on_small_screen.png)

Um formulário usando layout responsivo como visto em uma tela pequena

![Um formulário usando layout responsivo como visto em uma tela grande](assets/responsive_layout_seen_on_large_screen.png)

Um formulário usando layout responsivo como visto em uma tela grande

### Assistente - um formulário de várias etapas que mostra uma etapa de cada vez {#wizard-a-multi-step-form-showing-one-step-at-a-time}

Use esse layout de painel para fornecer navegação guiada dentro de um formulário. Por exemplo, use esse layout quando quiser capturar informações obrigatórias em um formulário enquanto guia os usuários passo a passo.

Use o `Panel adaptive form` para fornecer navegação passo a passo dentro de um painel. Quando você usa esse layout, um usuário passa para a próxima etapa somente após a etapa atual ser concluída

```javascript
window.guideBridge.validate([], this.panel.navigationContext.currentItem.somExpression)
```

![Expressão de conclusão de etapa no layout Assistente para um formulário de várias etapas](assets/layout-sidebar.png)

Expressão de conclusão de etapa no layout Assistente para um formulário de várias etapas

![Um formulário usando o layout do assistente](assets/wizard-layout.png)

Um formulário usando o Assistente

### Layout para design do Accordion {#layout-for-accordion-design}

Usando esse layout, você pode colocar o `Panel adaptive form` em um painel com navegação de estilo Accordion. Usando esse layout, você também pode criar painéis repetíveis. Os painéis repetíveis permitem adicionar ou remover painéis dinamicamente, conforme necessário. Você pode definir o número mínimo e máximo de vezes que um painel é repetido. Além disso, o título do painel pode ser determinado dinamicamente, com base nas informações fornecidas nos itens do painel.

A expressão de resumo pode ser usada para mostrar os valores fornecidos pelo usuário final no título do painel minimizado.

![Painéis repetíveis usando o layout Acordeão em formulários adaptáveis](assets/repeatable_panels_using_accordion_layout.png)

Painéis repetíveis criados com o layout Acordeão

### Layout com guias - as guias são exibidas à esquerda {#tabbed-layout-tabs-appear-on-the-left}

Usando esse layout, você pode colocar o `Panel adaptive form` em um painel com navegação por guias. As guias são colocadas à esquerda do conteúdo do painel.

![No layout com guias, as guias são exibidas à esquerda](assets/tabbed_layout_left.png)

Guias que aparecem à esquerda de um painel

### Layout com guias - guias são exibidas na parte superior {#tabbed-layout-tabs-appear-on-the-top}

Usando esse layout, você pode colocar o `Panel adaptive form` Componente em um painel com navegação por guias. As guias são colocadas em cima do conteúdo do painel.

![Layout com guias em formulários adaptáveis com guias na parte superior](assets/tabbed_layout_top.png)

Guias que aparecem na parte superior de um painel

## Layouts móveis {#mobile-layouts}

Os layouts móveis permitem uma navegação fácil nos dispositivos móveis com telas relativamente menores. Os layouts móveis usam estilos com guias ou de assistente para navegação de formulário. A aplicação de um layout móvel fornece um único layout para todo o formulário.

Esse layout controla a navegação usando uma barra de navegação e um menu de navegação. A barra de navegação mostra **&lt;** e **>** ícone para indicar **próximo** e **anterior** etapas de navegação no formulário.

Os Layouts móveis estão disponíveis em `/libs/fd/af/layouts/mobile/` localização. Os seguintes layouts móveis estão disponíveis em formulários adaptáveis, por padrão.

![Lista de layouts móveis em formulários adaptáveis](assets/mobile-navigation.png)

Lista de layouts móveis em formulários adaptáveis

Ao usar um layout móvel, o menu de formulário, para acessar vários painéis de formulário, está disponível ao tocar em ![aem6forms_form_menu](assets/aem6forms_form_menu.png) ícone.

### Layout com títulos de painel no cabeçalho do formulário {#layout-with-panel-titles-in-the-form-header}

Esse layout, como o nome sugere, mostra títulos de painel junto com o menu de navegação e a barra de navegação. Esse layout também fornece ícones Próximo e Anterior para navegação.

![Layouts móveis com títulos de painel nos cabeçalhos do formulário](assets/mobile_layout_with.png)

Layouts móveis com títulos de painel nos cabeçalhos do formulário

### Layout sem títulos de painel no cabeçalho do formulário {#layout-without-panel-titles-in-the-form-header}

Esse layout, como o nome sugere, mostra apenas o menu de navegação e a barra de navegação sem títulos de painel. Esse layout também fornece ícones Próximo e Anterior para navegação.

![Layouts móveis sem títulos de painel nos cabeçalhos do formulário](assets/mobile_layout_without.png)

Layouts móveis sem títulos de painel nos cabeçalhos do formulário

## Layouts da barra de ferramentas {#toolbar-layouts}

Um Layout da barra de ferramentas controla o posicionamento e a exibição de qualquer botão de ação adicionado aos formulários adaptáveis. O layout pode ser adicionado no nível do formulário ou do painel.

![Uma lista de Layouts de Barra de Ferramentas em formulários adaptáveis para controlar o layout dos botões](assets/toolbar-layouts.png)

Uma lista de Layouts de Barra de Ferramentas em formulários adaptáveis

Os layouts da barra de ferramentas estão disponíveis em `/libs/fd/af/layouts/toolbar` localização. por padrão, os formulários adaptáveis fornecem os seguintes Layouts de barra de ferramentas.

### Layout padrão da barra de ferramentas {#default-layout-for-toolbar}

Esse layout é selecionado como o layout padrão ao adicionar botões de ação em um formulário adaptável. A seleção desse layout exibe o mesmo layout para dispositivos móveis e desktop.

Além disso, é possível adicionar várias barras de ferramentas contendo botões de ação configurados com esse layout. Um botão de ação está associado a um controle de formulário. Você pode configurar as barras de ferramentas como antes ou depois de um painel.

![Exibição padrão da barra de ferramentas](assets/toolbar_layout_default.png)

Exibição padrão da barra de ferramentas

### Layout móvel fixo para a barra de ferramentas {#mobile-fixed-layout-for-toolbar}

Selecione este layout para fornecer layouts alternativos para dispositivos móveis e desktop.

Para o layout da área de trabalho, você pode adicionar botões de Ação usando alguns rótulos específicos. Somente uma barra de ferramentas pode ser configurada com este layout. Se mais de uma barra de ferramentas estiver configurada com esse layout, haverá uma sobreposição para dispositivos móveis e apenas uma barra de ferramentas estará visível. Por exemplo, você pode ter uma barra de ferramentas na parte inferior ou superior do formulário ou depois ou antes dos painéis no formulário.

Para o layout móvel, é possível adicionar botões de ação usando ícones.

![Layout móvel fixo para a barra de ferramentas](assets/toolbar_layout_mobile_fixed.png)

Layout móvel fixo para a barra de ferramentas
