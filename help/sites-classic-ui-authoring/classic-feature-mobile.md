---
title: 'Criação de uma página para dispositivos móveis  '
seo-title: 'Criação de uma página para dispositivos móveis  '
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
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 77%

---


# Criação de uma página para dispositivos móveis   {#authoring-a-page-for-mobile-devices}

Ao criar uma página para dispositivos móveis, a página é exibida de uma maneira que emula o dispositivo móvel. Ao criar a página, você pode alternar entre vários emuladores para ver o que o usuário final vê ao acessar a página.

Os dispositivos são agrupados nas categorias Recurso, Inteligente e Toque, de acordo com as capacidades dos dispositivos de renderizar uma página. Quando o usuário final acessa uma página para dispositivos móveis, o AEM detecta o dispositivo e envia a representação que corresponde ao seu grupo de dispositivos.

>[!NOTE]
>
>Para criar um site móvel com base em um site padrão existente, crie uma live copy do site padrão. (Consulte [Criação de uma Live Copy para Canais Diferentes](/help/sites-administering/msm-livecopy.md).)
>
>Os desenvolvedores do AEM podem criar novos grupos de dispositivos. (Consulte [Criando Filtros de Grupos de Dispositivos.](/help/sites-developing/groupfilters.md))

Use o procedimento a seguir para criar uma página para dispositivos móveis:

1. No seu navegador, vá para o console **Siteadmin**.
1. Abra a página **Produtos** abaixo de **Sites** >> **Site de demonstração do Geometrixx Mobile** >> **Inglês**.

1. Mude para um emulador diferente. Para fazer isso, você pode:

   * Clicar no ícone do dispositivo na parte superior da página.
   * Clique no botão **Editar** no **Sidekick** e selecione o dispositivo no menu suspenso.

1. Arraste e solte o componente **Texto e imagem** da guia Móvel do Sidekick para a página.
1. Editar o componente e adicionar texto. Clique em **OK** para salvar as alterações.

A página tem uma aparência semelhante à seguinte:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Os emuladores são desativados quando uma página na instância de autor é solicitada em um dispositivo móvel. A criação pode ser feita usando a interface habilitada para toque.

