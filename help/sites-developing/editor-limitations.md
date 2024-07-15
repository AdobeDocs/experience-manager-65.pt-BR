---
title: Limitações do editor
description: O editor na interface habilitada para toque usa sobreposições para interagir com o conteúdo confinado em um iframe. Essa interação cria algumas limitações no uso do editor e também para desenvolvedores.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 6%

---

# Limitações do editor{#editor-limitations}

O editor na interface habilitada para toque usa sobreposições para interagir com o conteúdo confinado em um iframe. Essa interação cria algumas limitações no uso do editor e também para desenvolvedores. Esta página resume essas limitações e fornece soluções ou soluções alternativas, quando possível.

## Limitações funcionais {#functional-limitations}

Um autor pode encontrar as seguintes limitações funcionais ao usar o editor para criar páginas.

### Links não ativos {#links-not-active}

Ao [editar uma página](/help/sites-authoring/editing-content.md), os links não ficam ativos.

* [Alterne para o **modo de Visualização**](/help/sites-authoring/editing-content.md#preview-mode) para navegar usando os links no seu conteúdo.

### Páginas de estrutura {#structure-pages}

Páginas não podem ser nomeadas como `structure`. As páginas com o nome `structure` não são editáveis no editor de páginas.

## Limitações de CSS {#css-limitations}

Um desenvolvedor pode encontrar as seguintes limitações nas interações do editor com o CSS.

### Elementos posicionados de forma absoluta {#absolutely-positioned-elements}

Elementos posicionados de forma absoluta podem causar problemas na posição da sobreposição.

* Se isso acontecer, verifique se as dimensões do elemento absolutamente posicionado estão corretas porque o editor cria uma sobreposição com exatamente as mesmas dimensões.

### Unidades de vh {#vh-units}

Não há suporte para `vh` unidades porque a altura do iframe deve ser ajustada automaticamente pelo Adobe Experience Manager (AEM).

### Imagens de fundo fixas {#fixed-background-images}

Imagens de fundo fixas não podem ser exibidas como fixas ao rolar a tela porque estão incorporadas em um iframe.

* Selecionar **Exibir página como publicada** nas ações da barra de cabeçalho exibe a página corretamente.

### Altura de 100% {#height}

Não há suporte para 100% de altura no elemento de corpo de uma página.

* Uma solução alternativa é possível implementar um corpo de tela cheia &quot;esticando&quot; o elemento do corpo da seguinte maneira:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Recolhimento de margem {#margin-collapsing}

Problemas de recolhimento de margem podem ser vistos se o primeiro elemento filho do elemento body tiver uma margem.

* A solução é adicionar uma correção clara no nível do elemento do corpo, como a seguir:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
