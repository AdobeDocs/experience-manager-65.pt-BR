---
title: Criação de uma página para dispositivos móveis
description: Ao criar uma página móvel, a página é exibida de uma forma que emula o dispositivo móvel. Ao criar a página, você pode alternar entre vários emuladores para ver o que o usuário final vê ao acessar a página.
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 13%

---

# Criação de uma página para dispositivos móveis  {#authoring-a-page-for-mobile-devices}

Ao criar uma página móvel, a página é exibida de uma forma que emula o dispositivo móvel. Ao criar a página, você pode alternar entre vários emuladores para ver o que o usuário final vê ao acessar a página.

Os dispositivos são agrupados no recurso de categorias, inteligente e por toque de acordo com os recursos dos dispositivos para renderizar uma página. Quando o usuário final acessa uma página móvel, o AEM detecta o dispositivo e envia a representação que corresponde ao seu grupo de dispositivos.

>[!NOTE]
>
>Para criar um site móvel com base em um site padrão existente, crie uma live copy do site padrão. (Consulte [Criação de uma Live Copy para diferentes canais](/help/sites-administering/msm-livecopy.md).)
>
>Os desenvolvedores do AEM podem criar novos grupos de dispositivos. (Consulte [Criando Filtros de Grupos de Dispositivos.](/help/sites-developing/groupfilters.md))

Use o procedimento a seguir para criar uma página para dispositivos móveis:

1. No navegador, acesse o menu **Siteadmin** console.
1. Abra o **Produtos** página abaixo **Sites** >> **Site de demonstração do Geometrixx Mobile** >> **Inglês**.

1. Alternar para um emulador diferente. Para fazer isso, é possível:

   * Clique no ícone do dispositivo na parte superior da página.
   * Clique em **Editar** botão na caixa **Sidekick** e selecione o dispositivo no menu suspenso.

1. Arraste e solte a **Texto e imagem** da guia Dispositivo móvel do Sidekick para a página.
1. Edite o componente e adicione texto. Clique em **OK** para salvar as alterações.

A página tem a mesma aparência do seguinte:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Os emuladores são desativados quando uma página na instância de autor é solicitada em um dispositivo móvel. A criação pode ser feita usando a interface habilitada para toque.
