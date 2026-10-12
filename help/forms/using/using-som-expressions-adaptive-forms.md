---
title: Uso de expressões SOM em formulários adaptáveis
description: Saiba como extrair expressões SOM de um painel de um formulário adaptável.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms,Foundation Components
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
exl-id: 6a158e18-b7d0-45fb-b4fc-4770e66982b4
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
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%
---
# Uso de expressões SOM em formulários adaptáveis{#using-som-expressions-in-adaptive-forms}

Os formulários adaptáveis são modelados como uma página do AEM, que é representada como estrutura de conteúdo JCR no repositório do AEM. O elemento principal da estrutura de conteúdo é o nó guideContainer. Abaixo de guideContainer, há rootPanel que pode conter painéis e campos aninhados.

Você pode usar um modelo de objeto de script (SOM) para fazer referência a valores, propriedades e métodos em um modelo de objeto de documento (DOM) específico. Um DOM organiza os objetos de memória e as propriedades em uma hierarquia de árvore. Uma expressão SOM faz referência a campos/desenha elementos e painéis.

A imagem a seguir descreve uma estrutura de nó para a qual um formulário adaptável é traduzido quando você adiciona componentes a um formulário. Por exemplo, você pode adicionar um painel ao painel raiz e um botão de opção no painel que é transformado em DOM no tempo de execução. A Expressão SOM do campo de botão de opção em um formulário adaptável está especificada como `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`.

![árvore DOM](assets/hierarchy.png)

Árvore DOM

Uma expressão SOM para qualquer elemento em um formulário adaptável tem o prefixo `guide[0].guide1[0]`. A posição de um componente na hierarquia de estrutura de nó é usada para derivar sua expressão SOM.

![Árvore DOM com dois botões de opção](assets/hierarchy_radio_button.png)

Árvore DOM com dois botões de opção

A expressão SOM muda quando você altera a posição dos botões de opção no formulário adaptável. No modo de criação, é possível exibir a expressão SOM de um campo ou elemento no AEM Forms usando a opção Exibir expressão SOM. A opção é exibida no painel e quando você clica com o botão direito do mouse no campo ou elemento.

![Extraindo Expressões SOM em um formulário adaptável](assets/som-expressions.png)

Extração de expressões SOM em um formulário adaptável

Nos painéis, você pode acessar o recurso na barra de ferramentas do painel. O recurso facilita a criação de scripts por autores de formulários adaptáveis.

![Extraindo expressões SOM usando a barra de ferramentas do painel](assets/som-expression.png)

Extração de expressões SOM usando a barra de ferramentas do painel

Algumas APIs listadas no [GuideBridge](https://helpx.adobe.com/br/aem-forms/6/javascript-api/GuideBridge.html) usam a expressão SOM de um elemento. Por exemplo, para focalizar um campo específico em um formulário adaptável, passe a expressão SOM correspondente para a API `getFocus` em `guideBridge`.
