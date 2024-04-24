---
title: Criar uma página de exemplo
description: Saiba como criar um modelo de site da comunidade que contenha apenas a função Página, que pode ajudá-lo a criar um site da comunidade simples.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Criar uma página de exemplo {#create-a-sample-page}

A partir do AEM 6.1 Communities, a maneira mais fácil de criar uma página de exemplo é criar um site de comunidade simples, que consiste simplesmente em uma função Página.

Isso inclui um componente parsys para que você possa [ativar componentes para criação](basics.md#accessing-communities-components).

Outra opção para exploração com componentes de amostra é usar os recursos apresentados na [Guia de componentes da comunidade](components-guide.md).

## Criar um site da comunidade {#create-a-community-site}

É semelhante à criação de um site descrito em [Introdução ao AEM Communities](getting-started.md).

A principal diferença é que este tutorial cria um modelo de site da comunidade que contém somente o [Função Page](functions.md#page-function) para criar um site de comunidade simples. Ele faz isso sem outros recursos (além dos recursos pré-conectados básicos para todos os sites da comunidade).

### Criar novo modelo de site {#create-new-site-template}

Para começar, crie um [modelo do site da comunidade](sites.md).

Na navegação global em uma instância do autor, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Communities]** > **[!UICONTROL Modelos de site]**.

![create-site-template](assets/create-site-template1.png)

* Selecionar `Create button`
* INFORMAÇÕES BÁSICAS

   * `Name`: modelo de página única
   * `Description`: um modelo que consiste em uma única função Page.
   * Selecionar `Enabled`

![site-template-editor](assets/site-template-editor.png)

* ESTRUTURA

   * Arraste um `Page` para o Construtor de modelos
   * Para Detalhes da Função de Configuração, informe

      * `Title`: Página única
      * `URL`: página

![site-template-editor-structure](assets/site-template-editor1.png)

* Selecionar **`Save`** para a configuração
* Selecionar **`Save`** para o modelo de site

### Criar novo site da comunidade {#create-new-community-site}

Agora, crie um site da comunidade com base no modelo de site simples.

Depois de criar o modelo de site, na navegação global, selecione **[!UICONTROL Comunidades > Sites]**.

![create-community-site](assets/create-community-site1.png)

* Selecionar **`Create`** ícone

* Etapa `1 - Site Template`

   * `Title`: Site simples da comunidade
   * `Description`: um site da comunidade que consiste em uma única página para experimentação.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: exemplo

      * url = http://localhost:4502/content/sites/sample

      * `Template`: escolher `Single Page Template`

     ![create-community-site-template](assets/create-community-site-template.png)

* Selecionar `Next`
* Etapa `2 - Design`

   * Selecionar qualquer design

* Selecionar `Next`
* Selecionar `Next`

  (Aceitar todas as configurações padrão)

* Selecionar `Create`

  ![create-community-site](assets/create-community-site.png)

## Publicar o site {#publish-the-site}

![site de publicação](assets/publish-site.png)

No [console de sites da comunidade](sites-console.md), selecione o ícone publicar para publicar o site, por padrão http://localhost:4503.

## Abrir o site em Autor no Modo de edição {#open-the-site-on-author-in-edit-mode}

![open-site](assets/open-site.png)

Selecione o ícone abrir site para exibir o site no modo de edição.

O URL é [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![author-site](assets/author-site.png)

Na página inicial simples, é possível ver o que é pré-conectado por meio das funções e modelos da comunidade, além de brincar com a adição e configuração de componentes da comunidade.

## Exibir Site na Publicação {#view-site-on-publish}

Após publicar a página, abra a página no [instância de publicação](http://localhost:4503/content/sites/sample/en.html) para experimentar os recursos como um visitante anônimo do site, membro conectado ou administrador. O link Administração visível no ambiente de autor não aparece no ambiente de publicação, a menos que um administrador faça logon.
