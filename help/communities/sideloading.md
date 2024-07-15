---
title: Sideload do componente
description: O sideload do componente Communities é útil quando uma página da Web é projetada como um aplicativo simples de página única que altera dinamicamente o que é exibido, dependendo do que é selecionado pelo visitante do site
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Sideload do componente {#component-sideloading}

## Visão geral {#overview}

O sideload do componente Communities é útil quando uma página da Web é projetada como um aplicativo simples de página única que altera dinamicamente o que é exibido, dependendo do que é selecionado pelo visitante do site.

Isso é feito quando os componentes das Comunidades não existem no modelo de página, mas são adicionados dinamicamente após a seleção de um visitante do site.

Como a estrutura do componente social (SCF) tem uma presença leve, somente os componentes SCF existentes no momento do carregamento da página inicial são registrados. Para que um componente SCF adicionado dinamicamente seja registrado após o carregamento da página, o SCF deve ser chamado para &quot;sideload&quot; do componente.

Quando uma página é projetada para fazer o sideload de componentes do Communities, é possível armazenar a página inteira em cache.

As etapas para adicionar componentes SCF dinamicamente são:

1. [Adicionar o componente ao DOM](#dynamically-add-component-to-dom)

1. [Faça Sideload do componente](#sideload-by-invoking-scf) usando um dos dois métodos a seguir:

* [Inclusão dinâmica](#dynamic-inclusion)
   * Inicializar todos os componentes adicionados dinamicamente
* [Carregamento dinâmico](#dynamic-loading)
   * Adicionar um componente específico sob demanda

>[!NOTE]
>
>Não há suporte para sideload de [recursos não existentes](scf.md#add-or-include-a-communities-component).

## Adicionar dinamicamente o componente ao DOM {#dynamically-add-component-to-dom}

Se o componente for incluído dinamicamente ou carregado dinamicamente, ele deverá ser adicionado primeiro ao DOM.

Ao adicionar o componente SCF, a tag mais comum a ser usada é a tag DIV, mas outras tags também podem ser usadas. Como o SCF só examina o DOM quando a página é carregada inicialmente, essa adição ao DOM passará despercebida até que o SCF seja chamado explicitamente.

Independentemente da tag usada, no mínimo, o elemento deve estar em conformidade com o padrão normal do elemento raiz do SCF, contendo estes dois atributos:

* **id do componente de dados**

  O caminho efetivo para o componente adicionado.

* **componente-scf-dados**

  O resourceType do componente.

Veja a seguir um exemplo de um componente de comentários adicionado:

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## Sideload chamando o SCF {#sideload-by-invoking-scf}

### Inclusão dinâmica {#dynamic-inclusion}

A inclusão dinâmica usa uma solicitação de inicialização que resulta no exame do DOM pelo SCF e na inicialização de todos os componentes do SCF encontrados na página.

Para inicializar componentes SCF a qualquer momento após o carregamento da página, basta acionar um evento JQuery como este:

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### Carregamento dinâmico {#dynamic-loading}

O carregamento dinâmico fornece controle sobre o carregamento de componentes SCF.

Em vez de inicializar todos os componentes SCF encontrados no DOM, é possível especificar um componente SCF específico para carregar usando este método JavaScript:

`SCF.addComponent(document.getElementById(*someId*));`

Onde `someId` é o valor do atributo `data-component-id`.
