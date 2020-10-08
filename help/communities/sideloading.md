---
title: Sideload do componente
seo-title: Sideload do componente
description: O sideload de componentes das Comunidades é útil quando uma página da Web é projetada como um aplicativo de página simples que altera dinamicamente o que é exibido, dependendo do que for selecionado pelo visitante do site
seo-description: O sideload de componentes das Comunidades é útil quando uma página da Web é projetada como um aplicativo de página simples que altera dinamicamente o que é exibido, dependendo do que for selecionado pelo visitante do site
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Sideload do componente {#component-sideloading}

## Visão geral {#overview}

O sideload de componentes das Comunidades é útil quando uma página da Web é projetada como um aplicativo de página simples que altera dinamicamente o que é exibido, dependendo do que for selecionado pelo visitante do site.

Isso é realizado quando os componentes Comunidades não existem no modelo de página, mas são adicionados dinamicamente após a seleção do visitante do site.

Como o SCF (Social Component Framework) tem uma presença leve, somente os componentes do SCF que existem no momento do carregamento da página inicial são registrados. Para que um componente SCF adicionado dinamicamente seja registrado após o carregamento da página, o SCF deve ser chamado para &quot;sideload&quot; do componente.

Quando uma página é projetada para fazer sideload dos componentes das Comunidades, é possível fazer o cache de toda a página.

As etapas para adicionar dinamicamente componentes SCF são:

1. [Adicionar o componente ao DOM](#dynamically-add-component-to-dom)

1. [Carregue o componente](#sideload-by-invoking-scf) de maneira auxiliar usando um dos dois métodos:

* [Inclusão dinâmica](#dynamic-inclusion)
   * Boostrap de todos os componentes adicionados dinamicamente
* [Carregamento dinâmico](#dynamic-loading)
   * Adicionar um componente específico sob demanda

>[!NOTE]
>
>Não há suporte para o sideload de recursos [não](scf.md#add-or-include-a-communities-component) existentes.

## Adicionar componente dinamicamente ao DOM {#dynamically-add-component-to-dom}

Independentemente de o componente ser incluído dinamicamente ou carregado dinamicamente, ele deve primeiro ser adicionado ao DOM.

Ao adicionar o componente SCF, a tag mais comum a ser usada é a tag DIV, mas outras tags também podem ser usadas. Como o SCF examina somente o DOM quando a página é carregada inicialmente, essa adição ao DOM passará despercebida até que o SCF seja explicitamente chamado.

Seja qual for a tag usada, no mínimo, o elemento deve estar em conformidade com o padrão normal do elemento raiz SCF, contendo estes dois atributos:

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

A inclusão dinâmica usa uma solicitação de inicialização que resulta em SCF examinando o DOM e inicializando todos os componentes do SCF encontrados na página.

Para inicializar componentes SCF a qualquer momento após o carregamento da página, basta disparar um evento JQuery como este:

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### Carregamento dinâmico {#dynamic-loading}

O carregamento dinâmico fornece controle sobre o carregamento de componentes SCF.

Em vez de fazer o carregamento de todos os componentes SCF encontrados no DOM, é possível especificar um componente SCF específico para carregar usando este método JavaScript:

`SCF.addComponent(document.getElementById(*someId*));`

Onde `someId` é o valor do `data-component-id` atributo.
