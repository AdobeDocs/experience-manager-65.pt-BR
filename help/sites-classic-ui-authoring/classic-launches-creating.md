---
title: Criação de lançamentos
seo-title: Criação de lançamentos
description: Crie um lançamento para permitir a atualização de uma nova versão de páginas da web existentes para ativação futura. Ao criar o Lançamento, especifique um título e a página de origem.
seo-description: Crie um lançamento para permitir a atualização de uma nova versão de páginas da web existentes para ativação futura. Ao criar o Lançamento, especifique um título e a página de origem.
uuid: e67608a9-e6c9-42f3-bd1d-63a5fa87ae18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 48826f03-6731-49c5-a6c5-6e2fb718f912
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# Criação de lançamentos{#creating-launches}

Crie um lançamento para permitir a atualização de uma nova versão de páginas da web existentes para ativação futura. Ao criar o Lançamento, especifique um título e a página de origem:

* The title appears in the **Sidekick**, from where authors can access them to work on them.
* As páginas secundárias da página de origem são incluídas no lançamento por padrão. Você pode usar apenas a página de origem, se desejar.
* Por padrão, a [Live Copy](/help/sites-administering/msm.md) atualiza automaticamente as páginas de lançamento conforme as páginas de origem são alteradas. Você pode especificar que uma cópia estática seja criada para evitar alterações automáticas.

Opcionalmente, é possível especificar a **Data de lançamento** (e a hora) para definir quando as páginas de lançamento devem ser promovidas e ativadas. However the **Launch Date** only operates in combination with the **Production Ready** flag (see [Editing a Launch Configuration](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration)); for the actions to actually occur automatically, both must be set.

## Criação de um lançamento {#creating-a-launch}

O procedimento a seguir cria um lançamento.

1. Abra a página de administração do Site ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin)).
1. Clique em **Novo...** e depois em **Novo lançamento...**.
1. Na caixa de diálogo **Criar lançamento**, especifique valores para as seguintes propriedades:

   * **Título do lançamento**: o nome do lançamento. O nome deve ser significativo para os autores.
   * **Página de origem**: o caminho da página para a qual criar o lançamento. Por padrão, todas as páginas filho são incluídas.
   * **Excluir subpáginas**: selecione essa opção para criar o lançamento somente para a página de origem, e não para as páginas filho. Por padrão, essa opção não está selecionada.
   * **Manter em sincronia**: selecione essa opção para atualizar automaticamente o conteúdo das páginas de lançamento quando as páginas de origem forem alteradas. Isso é feito transformando o lançamento em uma [live copy](/help/sites-administering/msm.md).
   * **Data de lançamento**: a data e a hora em que a cópia de lançamento deve ser ativada (dependendo do sinalizador de **Pronto para produção**; consulte [Lançamentos - a ordem dos eventos](/help/sites-authoring/launches.md#launches-the-order-of-events)).
   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. Clique em **Criar**.

## Exclusão de um lançamento {#deleting-a-launch}

Você também pode excluir um lançamento.

1. No console [Lançamentos](/help/sites-classic-ui-authoring/classic-launches.md), selecione o lançamento necessário.
1. Clique em **Excluir** - uma confirmação é necessária:

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >Ao excluir lançamentos aninhados, você deve excluir os níveis inferiores primeiro.

