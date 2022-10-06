---
title: Limitações do editor
seo-title: Editor Limitations
description: O editor na interface habilitada para toque usa as sobreposições para interagir com o conteúdo confinado em um iframe. Essa interação cria algumas limitações no uso do editor e também para desenvolvedores.
seo-description: The editor in the touch-enabled UI makes use of overlays to interact with content confined in an iframe. This interaction creates some limitations in both usage of the editor and also for developers.
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 10%

---

# Limitações do editor{#editor-limitations}

O editor na interface habilitada para toque usa as sobreposições para interagir com o conteúdo confinado em um iframe. Essa interação cria algumas limitações no uso do editor e também para desenvolvedores. Esta página resume essas limitações e fornece soluções ou soluções alternativas, sempre que possível.

## Limitações funcionais {#functional-limitations}

Um autor pode encontrar as seguintes limitações funcionais ao usar o editor para criar páginas.

### Links não ativos {#links-not-active}

When [edição de uma página](/help/sites-authoring/editing-content.md), os links não estão ativos.

* [Mudar para **Visualizar** modo](/help/sites-authoring/editing-content.md#preview-mode) para navegar usando os links no seu conteúdo.

### Páginas da estrutura {#structure-pages}

Páginas não podem ser nomeadas `structure`. Páginas nomeadas `structure` não será editável no editor de páginas.

## Limitações de CSS {#css-limitations}

Um desenvolvedor pode encontrar as seguintes limitações com as interações do editor com o CSS.

### Elementos absolutamente posicionados {#absolutely-positioned-elements}

Elementos totalmente posicionados podem causar problemas na posição de sua sobreposição.

* Se isso acontecer, verifique se as dimensões do elemento absolutamente posicionado estão corretas, pois o editor criará uma sobreposição com as mesmas dimensões.

### unidades vh {#vh-units}

`vh` não há suporte para unidades porque a altura do iframe deve ser ajustada automaticamente pelo AEM.

### Imagens de plano de fundo fixas {#fixed-background-images}

Imagens de plano de fundo fixas podem não ser exibidas como fixas ao rolar devido ao fato de estarem incorporadas a um iframe.

* Selecionar **Exibir página como publicada** nas ações da barra de cabeçalho, a página é exibida corretamente.

### Altura de 100% {#height}

A altura de 100% não é suportada no elemento de corpo de uma página.

* Uma solução alternativa é possível para implementar um corpo de tela cheia &quot;esticando&quot; o elemento do corpo da seguinte maneira:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Redução da Margem {#margin-collapsing}

Problemas de colapso da margem podem ser vistos se o primeiro elemento filho do elemento do corpo tiver uma margem.

* A solução é adicionar uma correção clara no nível do elemento corporal, como a seguir:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
