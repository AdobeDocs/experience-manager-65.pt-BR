---
title: Criação de uma página para dispositivos móveis
seo-title: Criação de uma página para dispositivos móveis
description: Ao criar uma página para dispositivos móveis, a página é exibida de uma maneira que emula o dispositivo móvel. Ao criar a página, você pode alternar entre vários emuladores para ver o que o usuário final vê ao acessar a página.
seo-description: Ao criar uma página para dispositivos móveis, a página é exibida de uma maneira que emula o dispositivo móvel. Ao criar a página, você pode alternar entre vários emuladores para ver o que o usuário final vê ao acessar a página.
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
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
>Os desenvolvedores do AEM podem criar novos grupos de dispositivos. (See [Creating Device Group Filters.](/help/sites-developing/groupfilters.md))

Use o procedimento a seguir para criar uma página para dispositivos móveis:

1. In your browser, go to the **Siteadmin** console.
1. Open the **Products** page below **Websites** >> **Geometrixx Mobile Demo Site** >> **English**.

1. Mude para um emulador diferente. Para fazer isso, você pode:

   * Clicar no ícone do dispositivo na parte superior da página.
   * Click the **Edit** button in the **Sidekick** and select the device in the drop-down menu.

1. Drag and drop the **Text &amp; Image** component from the Mobile tab of the Sidekick to the page.
1. Editar o componente e adicionar texto. Clique em **OK** para salvar as alterações.

A página tem uma aparência semelhante à seguinte:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Os emuladores são desativados quando uma página na instância de autor é solicitada em um dispositivo móvel. A criação pode ser feita usando a interface habilitada para toque.

