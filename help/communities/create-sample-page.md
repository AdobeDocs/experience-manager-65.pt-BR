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

Isso inclui um componente parsys para que você possa [habilitar componentes para criação](basics.md#accessing-communities-components).

Outra opção para exploração com componentes de amostra é usar os recursos apresentados no [Guia de Componentes da Comunidade](components-guide.md).

## Criar um site da comunidade {#create-a-community-site}

É semelhante à criação de um site descrito em [Introdução ao AEM Communities](getting-started.md).

A principal diferença é que este tutorial cria um modelo de site de comunidade que contém apenas a [função de Página](functions.md#page-function) para criar um site de comunidade simples. Ele faz isso sem outros recursos (além dos recursos pré-conectados básicos para todos os sites da comunidade).

### Criar novo modelo de site {#create-new-site-template}

Para começar, crie um [modelo de site de comunidade](sites.md) simples.

Na navegação global em uma instância de autor, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Comunidades]** > **[!UICONTROL Modelos de Site]**.

![criar-modelo-site](assets/create-site-template1.png)

* Selecionar `Create button`
* INFORMAÇÕES BÁSICAS

   * `Name`: modelo de página única
   * `Description`: um modelo que consiste em uma única função Page.
   * Selecionar `Enabled`

![editor-modelo-site](assets/site-template-editor.png)

* ESTRUTURA

   * Arraste uma função `Page` para o Construtor de modelos
   * Para Detalhes da Função de Configuração, informe

      * `Title`: Página Simples
      * `URL`: página

![estrutura-editor-modelo-site](assets/site-template-editor1.png)

* Selecionar **`Save`** para a configuração
* Selecione **`Save`** para o modelo de site

### Criar novo site da comunidade {#create-new-community-site}

Agora, crie um site da comunidade com base no modelo de site simples.

Após criar o modelo de site, na navegação global, selecione **[!UICONTROL Comunidades > Sites]**.

![criar-site-comunidade](assets/create-community-site1.png)

* Selecionar ícone de **`Create`**

* Etapa `1 - Site Template`

   * `Title`: Site Simples da Comunidade
   * `Description`: um site da comunidade que consiste em uma única página para experimentação.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: exemplo

      * url = http://localhost:4502/content/sites/sample

      * `Template`: escolher `Single Page Template`

     ![criar-modelo-site-comunidade](assets/create-community-site-template.png)

* Selecionar `Next`
* Etapa `2 - Design`

   * Selecionar qualquer design

* Selecionar `Next`
* Selecionar `Next`

  (Aceitar todas as configurações padrão)

* Selecionar `Create`

  ![criar-site-comunidade](assets/create-community-site.png)

## Publish do site {#publish-the-site}

![publicar-site](assets/publish-site.png)

No [console de sites da comunidade](sites-console.md), selecione o ícone publicar para publicar o site, por padrão, em http://localhost:4503.

## Abrir o site em Autor no Modo de edição {#open-the-site-on-author-in-edit-mode}

![open-site](assets/open-site.png)

Selecione o ícone abrir site para exibir o site no modo de edição.

A URL é [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![site-autor](assets/author-site.png)

Na página inicial simples, é possível ver o que é pré-conectado por meio das funções e modelos da comunidade, além de brincar com a adição e configuração de componentes da comunidade.

## Exibir site no Publish {#view-site-on-publish}

Após a publicação da página, abra a página na [instância de publicação](http://localhost:4503/content/sites/sample/en.html) para experimentar os recursos como um visitante anônimo do site, membro conectado ou administrador. O link Administração visível no ambiente de autor não aparece no ambiente de publicação, a menos que um administrador faça logon.
