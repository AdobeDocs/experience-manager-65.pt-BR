---
title: Uso do SOM expressão em formulários adaptáveis
seo-title: Uso do SOM expressão em formulários adaptáveis
description: Saiba como extrair expressões SOM de um painel de um formulário adaptável.
seo-description: Saiba como extrair expressões SOM de um painel de um formulário adaptável.
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
translation-type: tm+mt
source-git-commit: 6b4bc58efd72900c54cb245878239e345d72ae3e
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Uso do SOM expressão em formulários adaptáveis{#using-som-expressions-in-adaptive-forms}

Os formulários adaptáveis são modelados como página AEM, que é representada como estrutura de conteúdo JCR no repositório AEM. O elemento principal da estrutura de conteúdo é o nó guideContainer. Abaixo de guideContainer, há um rootPanel que pode conter campos e painel aninhados.

Você pode usar um SOM (Modelo de objeto de script) para fazer referência a valores, propriedades e métodos em um DOM (Modelo de objeto de documento) específico. Um DOM organiza os objetos de memória e as propriedades em uma hierarquia de árvore. Uma expressão SOM faz referência aos elementos Campos/Desenhar e painéis.

A imagem a seguir descreve uma estrutura de nó à qual um formulário adaptável se traduz ao adicionar componentes a um formulário. Por exemplo, você pode adicionar um painel ao painel raiz e um botão de opção no painel que é transformado em DOM no tempo de execução. A Expressão SOM do campo de botão de opção em forma adaptável é especificada como `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`.

![árvore DOM](assets/hierarchy.png)

árvore DOM

Uma expressão SOM para qualquer elemento em um formulário adaptável recebe o prefixo `guide[0].guide1[0]`. A posição de um componente na hierarquia da estrutura do nó é usada para derivar sua expressão SOM.

![Árvore DOM com dois botões de opção](assets/hierarchy_radio_button.png)

Árvore DOM com dois botões de opção

A expressão SOM muda quando você altera a posição dos botões de opção na forma adaptativa. No modo de criação, é possível visualização a expressão SOM de um campo ou elemento no AEM Forms usando a opção Visualização SOM. A opção é exibida no painel e quando você clica com o botão direito do mouse no campo ou elemento.

![Extrair Expressões SOM em um formulário adaptável](assets/som-expressions.png)

Extrair Expressões SOM em um formulário adaptável

Dentro dos painéis, você pode acessar o recurso na barra de ferramentas do painel. O recurso facilita a criação de scripts por autores de formulários adaptativos.

![Extrair Expressões SOM usando a barra de ferramentas do painel](assets/som-expression.png)

Extrair Expressões SOM usando a barra de ferramentas do painel

Algumas APIs listadas no [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) usam a expressão SOM de um elemento. Por exemplo, para trazer o foco para um campo específico em um formulário adaptável, passe a expressão SOM correspondente para a `getFocus`API em `guideBridge`.

