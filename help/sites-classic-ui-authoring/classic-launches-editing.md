---
title: Edição de inicializações
description: Quando uma inicialização é criada para uma página (ou conjunto de páginas), é possível editar o conteúdo na cópia de inicialização das páginas.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 9%

---

# Edição de inicializações{#editing-launches}

## Editar páginas de lançamento {#editing-launch-pages}

Quando uma inicialização é criada para uma página (ou conjunto de páginas), é possível editar o conteúdo na cópia de inicialização das páginas.

1. Abra a página para edição.
1. No Sidekick, selecione a variável **Controle de versão** e expanda a guia **Lançamentos** grupo. O título do lançamento que está sendo editado no momento usa uma fonte em negrito.

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. Selecione o lançamento que deseja trabalhar e clique em **Alternar**.
1. Comece a editar.

   >[!NOTE]
   >
   >Você pode usar o **Página** guia do sidekick para executar ações como **Criar página secundária**, entre outros.

## Editar uma configuração de lançamento {#editing-a-launch-configuration}

Depois de criar um lançamento, é possível alterar o nome do lançamento e a data do lançamento. Você também pode especificar uma imagem para associar ao lançamento.

1. Abra a página de administração de inicializações ([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html)).

1. Selecione a inicialização necessária e clique em **Editar** para abrir a caixa de diálogo:

   * No **Geral** é possível editar:

      * **Título**
      * **Data de ativação**: é equivalente à data de lançamento
      * **Pronto para produção**

     Consulte [Inicializações - a ordem dos eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obter informações sobre a finalidade e interação desses campos.

   * No **Imagem** é possível fazer upload de um arquivo de imagem.

1. Clique em **Salvar**.

## Descobrir o status de lançamento de uma página {#discovering-the-launch-status-of-a-page}

Quando você está editando uma inicialização de uma página, as informações sobre a inicialização são exibidas na parte inferior da **Controle de versão** guia do Sidekick:

* O nome da inicialização.
* O tempo desde a última alteração.
* O usuário que executou a última alteração.
* O status do **Pronto para produção** sinalizador (laranja=não definido; verde=definido).

![chlimage_1-186](assets/chlimage_1-186.png)
