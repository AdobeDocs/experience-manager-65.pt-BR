---
title: Desenvolvendo e comparação de páginas
seo-title: Desenvolvendo e comparação de páginas
description: 'null'
seo-description: 'null'
uuid: 06f27bc2-f42a-4176-ab94-255e721c6933
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6612f89d-c518-4e5a-8df1-6487cc330a9a
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Desenvolvendo e comparação de páginas{#developing-and-page-diff}

## Visão geral do recurso {#feature-overview}

A criação de conteúdo é um processo iterativo. Criar com eficiência exige poder ver o que mudou de uma iteração para outra. Visualizar uma versão da página e, em seguida, a outra é um processo ineficiente e propenso a erros. Um autor deseja comparar a página atual com uma versão anterior lado a lado com as diferenças destacadas.

O diff da página permite que um usuário compare a página atual com inicializações, versões anteriores etc. Para obter detalhes sobre esse recurso do usuário, consulte Diferença de [página](/help/sites-authoring/page-diff.md).

## Detalhes da operação {#operation-details}

Ao comparar versões de uma página, a versão anterior que o usuário deseja comparar é recriada pelo AEM em segundo plano para facilitar a diferença. Isso é necessário para que o conteúdo seja renderizado [para comparação](/help/sites-developing/pagediff.md#operation-details)lado a lado.

Essa operação de recriação é feita pelo AEM internamente e é transparente para o usuário e não requer intervenção. No entanto, um administrador que visualiza o repositório, por exemplo, no CRX DE Lite, veria essas versões recriadas na estrutura de conteúdo.

Quando o conteúdo é comparado, a árvore inteira até a página a ser comparada é recriada no seguinte local:

`/tmp/versionhistory/`

Uma tarefa de limpeza é executada automaticamente para limpar esse conteúdo temporário.

## Permissões {#permissions}

Anteriormente, na interface clássica, era necessário considerar um desenvolvimento especial para facilitar a difusão do AEM (como o uso da `cq:text` `DiffService` tag lib ou a integração personalizada do serviço OSGi nos componentes). Isso não é mais necessário para o novo recurso diff, pois o diff ocorre no cliente por meio da comparação DOM.

No entanto, há várias limitações que precisam ser consideradas pelo desenvolvedor.

* Esse recurso usa classes CSS que não têm o nome espaçado para o produto AEM. Se outras classes CSS personalizadas ou classes CSS de terceiros com os mesmos nomes forem incluídas na página, a exibição do diff poderá ser afetada.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Como o diff é do lado do cliente e é executado no carregamento da página, todos os ajustes no DOM após a execução do serviço de comparação do lado do cliente não serão contabilizados. Este fato pode afetar

   * Componentes que usam AJAX para incluir conteúdo
   * Aplicativos de página única
   * Componentes baseados em JavaScript que manipulam o DOM na interação do usuário.
