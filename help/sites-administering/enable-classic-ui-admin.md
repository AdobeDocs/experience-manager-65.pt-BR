---
title: Admin Console
description: Saiba como usar o Admin Console disponível no Adobe Experience Manager.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%
---

# Admin Console{#admin-consoles}

Por padrão, a capacidade de alternar para a interface clássica por meio dos consoles de Administração está desativada. Portanto, os ícones pop-up que eram vistos ao passar o mouse sobre determinados ícones do console, permitindo acesso à interface clássica, não são mais exibidos.

Todo console que tenha uma versão da interface clássica no `/libs/cq/core/content/nav` pode ser reabilitado individualmente para que a opção **Interface clássica** apareça novamente sobre o ícone do console quando for posicionada com o mouse.

Neste exemplo, você está reativando a interface clássica para o console Sites.

1. Usando o CRXDE Lite, localize o nó correspondente ao Admin Console para o qual você deseja reativar a interface clássica. Eles são encontrados em:

   `/libs/cq/core/content/nav`

   Por exemplo

   [`https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Selecione o nó correspondente ao console para o qual você deseja reativar a interface clássica. Neste exemplo, você está reativando a interface clássica para o console Sites.

   `/libs/cq/core/content/nav/sites`

1. Crie uma sobreposição usando a opção **Sobrepor Nó**; por exemplo:

   * **Caminho**: `/apps/cq/core/content/nav/sites`
   * **Local de Sobreposição**: `/apps/`
   * **Corresponder Tipos de Nó**: ativo (marque a caixa de seleção)

1. Adicione a seguinte propriedade booleana ao nó sobreposto:

   `enableDesktopOnly = {Boolean}true`

1. A opção **Interface Clássica** está novamente disponível como uma opção de pop-over no Admin Console.

   ![opção de popover da interface clássica](assets/syui-01-2019-02-27-15-16-55.png)

Repita essas etapas para cada console para o qual deseja reativar o acesso à versão da interface clássica.
