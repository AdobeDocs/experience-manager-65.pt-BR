---
title: Desenvolvimento e diff de página
seo-title: Developing and Page Diff
description: Desenvolvimento e diff de página
seo-description: null
uuid: 06f27bc2-f42a-4176-ab94-255e721c6933
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6612f89d-c518-4e5a-8df1-6487cc330a9a
docset: aem65
exl-id: b07134b2-074a-4d52-8d0c-7e7abe51fc3a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 11%

---

# Desenvolvimento e diff de página{#developing-and-page-diff}

## Visão geral dos recursos {#feature-overview}

A criação de conteúdo é um processo iterativo. Criar com eficiência exige poder ver o que mudou de uma iteração para outra. Visualizar uma versão da página e, em seguida, a outra é um processo ineficiente e propenso a erros. Um autor deseja poder comparar a página atual com uma versão anterior lado a lado com as diferenças destacadas.

O diferencial de páginas permite que um usuário compare a página atual com inicializações, versões anteriores etc. Para obter detalhes sobre este recurso do usuário, consulte [Diff da página](/help/sites-authoring/page-diff.md).

## Detalhes da Operação {#operation-details}

Ao comparar versões de uma página, a versão anterior que o usuário deseja comparar é recriada por AEM em segundo plano para facilitar o diferencial. Isso é necessário para poder renderizar o conteúdo [para comparação lado a lado](/help/sites-developing/pagediff.md#operation-details).

Essa operação de recriação é feita por AEM internamente e é transparente para o usuário e não requer intervenção. No entanto, um administrador que visualiza o repositório, por exemplo, no CRX DE Lite, veria essas versões recriadas na estrutura de conteúdo.

Quando o conteúdo é comparado, a árvore inteira até a página a ser comparada é recriada no seguinte local:

`/tmp/versionhistory/`

Uma tarefa de limpeza é executada automaticamente para limpar esse conteúdo temporário.

## Permissões {#permissions}

Anteriormente, na interface do usuário clássica, era necessário considerar o desenvolvimento especial para facilitar a diferenciação AEM (como usar `cq:text` biblioteca de tags ou integração personalizada do `DiffService` Serviço OSGi em componentes). Isso não é mais necessário para o novo recurso de diferencial, pois o recurso de diferencial ocorre no lado do cliente por meio da comparação de DOM.

No entanto, há várias limitações que precisam ser consideradas pelo desenvolvedor.

* Esse recurso usa classes CSS que não são nomeadas espaçadas para o Produto AEM. Se outras classes CSS personalizadas ou classes CSS de terceiros com os mesmos nomes forem incluídas na página, a exibição do diferencial poderá ser afetada.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Como o diferencial é do lado do cliente e é executado no carregamento da página, os ajustes no DOM após a execução do serviço de comparação do lado do cliente não serão contabilizados. Pode afetar

   * Componentes que usam AJAX para incluir conteúdo
   * Aplicativos de página única
   * Componentes baseados em JavaScript que manipulam o DOM na interação do usuário.
