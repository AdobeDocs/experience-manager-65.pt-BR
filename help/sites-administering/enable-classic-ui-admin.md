---
title: Admin Console
seo-title: Admin Console
description: Saiba como usar os Admin Console disponíveis no AEM.
seo-description: Saiba como usar os Admin Console disponíveis no AEM.
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
translation-type: tm+mt
source-git-commit: 954c1d5b06b54d59f523483ce5c1af36c2083a76
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 2%

---


# Admin Console{#admin-consoles}

Por padrão, a capacidade de alternar para a interface clássica por meio dos consoles admin foi desativada. Portanto, os ícones de pop-up que foram vistos ao passar o mouse sobre certos ícones de console, permitindo o acesso à interface clássica, não são mais exibidos.

Cada console que tem uma versão de interface clássica em `/libs/cq/core/content/nav` pode ser reativado individualmente para que a opção **Interface clássica** volte a aparecer no ícone do console quando o mouse for passado.

Neste exemplo, estamos reativando a interface clássica para o console Sites.

1. Usando o CRXDE Lite, localize o nó correspondente ao console de administração para o qual você deseja reativar a interface clássica. Encontram-se em:

   `/libs/cq/core/content/nav`

   Por exemplo

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Selecione o nó correspondente ao console para o qual você deseja reativar a interface clássica. Para nosso exemplo, reativaremos a interface clássica para o console Sites.

   `/libs/cq/core/content/nav/sites`

1. Crie uma sobreposição usando a opção **Sobrepor nó**; por exemplo:

   * **Caminho**: `/apps/cq/core/content/nav/sites`
   * **Local de sobreposição**: `/apps/`
   * **Corresponder tipos** de nós: ativo (marque a caixa de seleção)

1. Adicione a seguinte propriedade booleana ao nó sobreposto:

   `enableDesktopOnly = {Boolean}true`

1. A opção **Interface clássica** está novamente disponível como uma opção de entrega no console de administração.

   ![](assets/syui-01-2019-02-27-15-16-55.png)

Repita essas etapas para cada console para o qual você deseja reativar o acesso à versão da interface clássica.