---
title: Renderização adaptável do modelo
description: Saiba mais sobre a renderização de modelo adaptável no Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Renderização adaptável do modelo{#adaptive-template-rendering}

A renderização do modelo adaptável fornece uma maneira de gerenciar uma página com variações. Originalmente útil para fornecer várias saídas de HTML para dispositivos móveis (por exemplo, telefone de recurso versus smartphone), esse recurso é útil quando as experiências precisam ser entregues a vários dispositivos que precisam de diferentes saídas de marcação ou HTML.

## Visão geral {#overview}

Os modelos são criados em torno de uma grade responsiva, e as páginas criadas com base nesses modelos são totalmente responsivas, ajustando-se automaticamente para a janela de visualização do dispositivo cliente. Usando a barra de ferramentas do Emulador no editor de páginas, os autores podem direcionar layouts para dispositivos específicos.

Também é possível configurar modelos para suportar a renderização adaptável. Quando os grupos de dispositivos são configurados corretamente, a página é renderizada com um seletor diferente no URL ao selecionar um dispositivo no modo emulador. Usando um seletor, uma renderização de página específica pode ser chamada diretamente pelo URL.

Lembre-se ao configurar seus grupos de dispositivos:

* Cada dispositivo deve estar em pelo menos um grupo de dispositivos.
* Um dispositivo pode estar em vários grupos de dispositivos.
* Como os dispositivos podem estar em vários grupos de dispositivos, os seletores podem ser combinados.
* A combinação de seletores é avaliada de cima para baixo, pois eles são mantidos no repositório.

>[!NOTE]
>
>O grupo de dispositivos **Dispositivos responsivos nunca têm um seletor porque presume-se que os dispositivos reconhecidos como compatíveis com design responsivo não precisem de um layout adaptável

## Configuração {#configuration}

Os seletores de renderização adaptativa podem ser configurados para grupos de dispositivos existentes ou para [grupos que você mesmo criou.](/help/sites-developing/mobile.md#device-groups)

Neste exemplo, você configurará o grupo de dispositivos existente **Smartphones** para ter um seletor de renderização adaptável como parte da **Página da experiência** modelo no We.Retail.

1. Editar o grupo de dispositivos que requer um seletor adaptável em `http://localhost:4502/miscadmin#/etc/mobile/groups`

   Definir a opção **Desativar emulador** e salve.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. O seletor está disponível para o **BlackBerry®** e **IPHONE 4** forneceu o grupo de dispositivos **Telefone inteligente** é adicionado ao modelo e às estruturas de página nas etapas a seguir.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Usando o CRXDE Lite, permita que o grupo de dispositivos seja usado em seu modelo, adicionando-o à propriedade de cadeia de caracteres de vários valores `cq:deviceGroups` na estrutura do modelo.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Por exemplo, se você quiser adicionar o grupo de dispositivos Telefone Inteligente:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Usando o CRXDE Lite, permita que o grupo de dispositivos seja usado em seu site, adicionando-o à propriedade de cadeia de caracteres de vários valores `cq:deviceGroups` na estrutura do site.

   `/content/<your-site>/jcr:content`

   Por exemplo, se você deseja permitir a variável **Telefone inteligente** grupo de dispositivos:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

Agora, ao usar o [emulador](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) no editor de páginas (como quando [modificação do layout](/help/sites-authoring/responsive-layout.md)) e você escolher um dispositivo do grupo de dispositivos configurado, a página será renderizada com um seletor como parte do URL.

Neste exemplo, ao editar uma página com base no **Página da experiência** e ao escolher iPhone 4 no emulador, a página é renderizada incluindo o seletor como `arctic-surfing-in-lofoten.smart.html` em vez de `arctic-surfing-in-lofoten.html`

A página também pode ser chamada diretamente usando esse seletor.

![chlimage_1-161](assets/chlimage_1-161.png)
