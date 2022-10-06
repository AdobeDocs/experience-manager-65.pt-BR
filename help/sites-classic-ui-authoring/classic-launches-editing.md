---
title: Edição de inicializações
seo-title: Editing Launches
description: Quando um lançamento foi criado para uma página (ou um conjunto de páginas), é possível editar o conteúdo na cópia de lançamento da(s) página(s).
seo-description: When a launch has been created for a page (or set of pages) you can edit the content in the launch copy of the page(s).
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 99%

---

# Edição de inicializações{#editing-launches}

## Edição de páginas de lançamento {#editing-launch-pages}

Quando um lançamento foi criado para uma página (ou um conjunto de páginas), é possível editar o conteúdo na cópia de lançamento da(s) página(s).

1. Abra a página para edição.
1. No Sidekick, selecione a guia **Controle de versão** e, em seguida, expanda o grupo **Lançamentos**. O título do lançamento que está sendo editado usa uma fonte em negrito.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. Selecione o lançamento em que você deseja trabalhar e clique em **Alternar**.
1. Comece a editar.

   >[!NOTE]
   >
   >Você pode usar a guia **Página** do sidekick para realizar ações como **Criar página secundária**, entre outras.

## Edição de configuração de lançamento {#editing-a-launch-configuration}

Depois de criar um lançamento, você pode alterar seu nome e sua data. Também é possível especificar uma imagem que será associada ao lançamento.

1. Abra a página de administração de lançamentos ([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html)).

1. Selecione o lançamento necessário e clique em **Editar** para abrir a caixa de diálogo:

   * Na guia **Geral**, você pode editar:

      * **Título**
      * **Data de ativação**: equivalente à data de lançamento
      * **Pronto para produção**

      Consulte [Lançamentos - a ordem de eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obter informações sobre o propósito e a interação desses campos.

   * Na guia **Imagem**, você pode fazer upload de um arquivo de imagem.


1. Clique em **Salvar**.

## Descoberta do status de lançamento de uma página {#discovering-the-launch-status-of-a-page}

Quando você está editando um lançamento de uma página, as informações sobre esse lançamento aparecem na parte inferior da guia **Controle de versão** do Sidekick:

* O nome do lançamento.
* O tempo desde a última alteração.
* O usuário que fez a última alteração.
* O status do sinalizador de **Pronto para produção** (laranja = não definido; verde = definido).

![chlimage_1-186](assets/chlimage_1-186.png)
