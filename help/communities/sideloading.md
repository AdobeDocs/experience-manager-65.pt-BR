---
title: Sideload de Componente
seo-title: Component Sideloading
description: O sideload do componente Comunidades é útil quando uma página da Web é projetada como um aplicativo de página simples que altera dinamicamente o que é exibido, dependendo do que é selecionado pelo visitante do site
seo-description: Communities component sideloading is useful when a web page is designed as a simple, single page app that dynamically alters what is displayed depending on what is selected by the site visitor
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Sideload de Componente {#component-sideloading}

## Visão geral {#overview}

O sideload do componente Comunidades é útil quando uma página da Web é projetada como um aplicativo de página simples que altera dinamicamente o que é exibido, dependendo do que é selecionado pelo visitante do site.

Isso é feito quando os componentes Comunidades não existem no modelo da página, mas são adicionados dinamicamente após a seleção de um visitante do site.

Como a estrutura de componentes sociais (SCF) tem uma presença leve, somente os componentes SCF existentes no momento do carregamento da página inicial são registrados. Para que um componente SCF adicionado dinamicamente seja registrado após o carregamento da página, o SCF deve ser chamado para &quot;sideload&quot; do componente.

Quando uma página é projetada para fazer o sideload dos componentes do Communities, é possível fazer o cache de toda a página.

As etapas para adicionar dinamicamente componentes SCF são:

1. [Adicione o componente ao DOM](#dynamically-add-component-to-dom)

1. [Carregar o componente de maneira secundária](#sideload-by-invoking-scf) usando um dos dois métodos:

* [Inclusão dinâmica](#dynamic-inclusion)
   * Inicialize todos os componentes adicionados dinamicamente
* [Carregamento dinâmico](#dynamic-loading)
   * Adicionar um componente específico sob demanda

>[!NOTE]
>
>Sideload de [recursos não existentes](scf.md#add-or-include-a-communities-component) não é suportado.

## Adicionar componente dinamicamente ao DOM {#dynamically-add-component-to-dom}

Independentemente de o componente ser incluído dinamicamente ou carregado dinamicamente, ele deve primeiro ser adicionado ao DOM.

Ao adicionar o componente SCF, a tag mais comum a ser usada é a tag DIV, mas outras tags também podem ser usadas. Como o SCF examina apenas o DOM quando a página é carregada inicialmente, essa adição ao DOM passa despercebida até que o SCF seja chamado explicitamente.

Qualquer tag usada, no mínimo, o elemento deve estar em conformidade com o padrão normal do elemento raiz SCF contendo esses dois atributos:

* **data-component-id**

   O caminho efetivo para o componente adicionado.

* **data-scf-component**

   O resourceType do componente.

Veja a seguir um exemplo de um componente de comentários adicionados:

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## Sideload chamando SCF {#sideload-by-invoking-scf}

### Inclusão dinâmica {#dynamic-inclusion}

A inclusão dinâmica usa uma solicitação de reforço que resulta na análise do SCF no DOM e na inicialização de todos os componentes do SCF encontrados na página.

Para inicializar componentes SCF a qualquer momento após o carregamento da página, basta disparar um evento JQuery como este:

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### Carregamento dinâmico {#dynamic-loading}

O carregamento dinâmico fornece controle sobre o carregamento de componentes SCF.

Em vez de bootstrapping de todos os componentes SCF encontrados no DOM, é possível especificar um componente SCF específico para carregar usando este método JavaScript:

`SCF.addComponent(document.getElementById(*someId*));`

Onde `someId` é o valor da variável `data-component-id` atributo.
