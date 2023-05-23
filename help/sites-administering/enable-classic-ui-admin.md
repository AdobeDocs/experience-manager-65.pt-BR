---
title: Admin Console
seo-title: Admin Consoles
description: Saiba como usar os Admin Console disponíveis no AEM.
seo-description: Lear how to use the Admin Consoles available in AEM.
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 2%

---

# Admin Console{#admin-consoles}

Por padrão, a capacidade de alternar para a interface clássica por meio dos consoles de administração foi desativada. Portanto, os ícones pop-up que eram vistos ao passar o mouse sobre determinados ícones do console, permitindo acesso à interface clássica, não são mais exibidos.

Todo console que tenha uma versão da interface clássica no `/libs/cq/core/content/nav` podem ser reativados individualmente para que a variável **Interface clássica** A opção aparece novamente sobre o ícone do console quando é tocada com o mouse.

Neste exemplo, estamos reativando a IU Clássica para o console Sites.

1. Usando o CRXDE Lite, localize o nó correspondente ao Admin Console para o qual você deseja reativar a interface clássica. Eles são encontrados em:

   `/libs/cq/core/content/nav`

   Por exemplo

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. Selecione o nó correspondente ao console para o qual você deseja reativar a interface clássica. Para nosso exemplo, reativaremos a interface clássica para o console Sites.

   `/libs/cq/core/content/nav/sites`

1. Criar uma sobreposição usando o **Sobrepor nó** opção; por exemplo:

   * **Caminho**: `/apps/cq/core/content/nav/sites`
   * **Local de sobreposição**: `/apps/`
   * **Corresponder tipos de nós**: ativo (marque a caixa de seleção)

1. Adicione a seguinte propriedade booleana ao nó sobreposto:

   `enableDesktopOnly = {Boolean}true`

1. A variável **Interface clássica** A opção está disponível novamente como uma opção de popover no admin console.

   ![](assets/syui-01-2019-02-27-15-16-55.png)

Repita essas etapas para cada console para o qual deseja reativar o acesso à versão da interface clássica.
