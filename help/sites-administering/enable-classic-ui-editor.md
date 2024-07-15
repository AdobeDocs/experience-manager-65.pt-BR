---
title: Editor
description: Saiba como alternar de volta para o Editor de interface clássica.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---


# Editor{#editor}

Por padrão, a capacidade de alternar para a interface clássica do editor foi desativada.

Para habilitar novamente a opção **Abrir na Interface Clássica** no menu **Informações da Página**, siga estas etapas.

1. Usando o CRXDE Lite, localize o seguinte nó:

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   Por exemplo

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. Crie uma sobreposição usando a opção **Sobrepor Nó**; por exemplo:

   * **Caminho**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **Local de Sobreposição**: `/apps/`
   * **Corresponder Tipos de Nó**: ativo (marque a caixa de seleção)

1. Adicione a seguinte propriedade de texto de vários valores ao nó sobreposto:

   `sling:hideProperties = ["granite:hidden"]`

1. A opção **Abrir na Interface Clássica** está novamente disponível no menu **Informações da Página** ao editar páginas.

   ![abrir na opção da interface clássica a partir de informações da página](assets/syui-03-2019-02-27-15-19-48.png)
