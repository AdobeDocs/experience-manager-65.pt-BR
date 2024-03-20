---
title: Desenvolvimento e diff de página
description: Saiba como desenvolver e utilizar o recurso de comparação de páginas no Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 10%

---

# Desenvolvimento e diff de página{#developing-and-page-diff}

## Visão geral do recurso {#feature-overview}

A criação de conteúdo é um processo iterativo. A criação com eficiência requer a capacidade de ver o que foi alterado de uma iteração para outra. Visualizar uma versão da página e, em seguida, a outra é ineficiente e sujeita a erros. Um autor deseja poder comparar a página atual com uma versão anterior lado a lado com as diferenças destacadas.

A comparação de páginas permite que um usuário compare a página atual com inicializações, versões anteriores e assim por diante. Para obter detalhes sobre esse recurso do usuário, consulte [Diferença de página](/help/sites-authoring/page-diff.md).

## Detalhes da operação {#operation-details}

Ao comparar versões de uma página, a versão anterior que o usuário deseja comparar é recriada pelo AEM em segundo plano para facilitar a comparação. Isso é necessário para renderizar o conteúdo [para comparação lado a lado](/help/sites-developing/pagediff.md#operation-details).

Essa operação de recreação é feita internamente pelo AEM e é transparente para o usuário e não requer nenhuma intervenção. No entanto, um administrador que visualize o repositório, por exemplo, no CRXDE Lite, veria essas versões recriadas na estrutura do conteúdo.

Quando o conteúdo é comparado, a árvore inteira até a página que será comparada é recriada no seguinte local:

`/tmp/versionhistory/`

Uma tarefa de limpeza é executada automaticamente para limpar esse conteúdo temporário.

## Permissões {#permissions}

Anteriormente, na interface clássica, era necessário considerar o desenvolvimento de forma especial para facilitar a difusão do AEM (como o uso de `cq:text` tag lib ou integração personalizada do `DiffService` OSGi em componentes). Isso não é mais necessário para o novo recurso de comparação, pois a comparação ocorre no lado do cliente por meio da comparação de DOM.

No entanto, há algumas limitações que devem ser consideradas pelo desenvolvedor.

* Esse recurso usa classes CSS que não têm namespace para o produto AEM. Se outras classes CSS personalizadas ou classes CSS de terceiros com os mesmos nomes forem incluídas na página, a exibição do diferencial poderá ser afetada.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Como o diferencial é no lado do cliente e é executado no carregamento da página, os ajustes no DOM após a execução do serviço de diferencial do lado do cliente não serão considerados. Isso pode afetar

   * Componentes que usam AJAX para incluir conteúdo
   * Aplicativos de página única
   * Componentes baseados em JavaScript que manipulam o DOM na interação do usuário.

>[!NOTE]
>
>A comparação de diferenças entre páginas funciona somente para os componentes que têm nós cq:editConfig válidos.
