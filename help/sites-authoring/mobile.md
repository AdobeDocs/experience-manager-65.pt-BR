---
title: Criação de uma página para dispositivos móveis
seo-title: Criação de uma página para dispositivos móveis
description: Ao criar em dispositivos móveis, você pode alternar entre vários emuladores para ver o que o usuário final vê
seo-description: Ao criar em dispositivos móveis, você pode alternar entre vários emuladores para ver o que o usuário final vê
uuid: a7a1ba68-d608-4819-88d1-0dab5955d3f4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9554cdb3-b604-4d50-9760-89b9e7a7755f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Criação de uma página para dispositivos móveis{#authoring-a-page-for-mobile-devices}

Ao criar uma página para dispositivos móveis, a página é exibida de uma maneira que emula o dispositivo móvel. Ao criar a página, você pode alternar entre vários emuladores para ver o que o usuário final vê ao acessar a página.

Os dispositivos são agrupados nas categorias Recurso, Inteligente e Toque, de acordo com as capacidades dos dispositivos de renderizar uma página. Quando o usuário final acessa uma página para dispositivos móveis, o AEM detecta o dispositivo e envia a representação que corresponde ao seu grupo de dispositivos.

>[!NOTE]
>
>Para criar um site móvel com base em um site padrão existente, crie uma live copy do site padrão. (See [Creating a Live Copy for Different Channels](/help/sites-administering/msm-livecopy.md).)
>
>Os desenvolvedores do AEM podem criar novos grupos de dispositivos. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)

Use o procedimento a seguir para criar uma página para dispositivos móveis:

1. From global navigation open the **Sites** console.
1. Open the page **We.Retail** -> **United States** -> **English**.

1. Switch to **Preview** mode.
1. Alterne para o emulador desejado, clicando no ícone de dispositivo na parte superior da página.
1. Arraste e solte componentes do navegador de componentes na página.

A página é semelhante ao seguinte:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Os emuladores são desativados quando uma página na instância de autor é solicitada em um dispositivo móvel.

