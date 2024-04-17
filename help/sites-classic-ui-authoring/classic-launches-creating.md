---
title: Criação de inicializações
description: Crie um lançamento para permitir a atualização de uma nova versão de páginas da Web para ativação futura. Ao criar uma inicialização, especifique um título e a página de origem.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 8ab21067-c19a-4faa-8bf0-cd9f21f6df70
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 54%

---

# Criação de inicializações{#creating-launches}

Crie um lançamento para permitir a atualização de uma nova versão de páginas da Web para ativação futura. Ao criar a inicialização, especifique um título e a página de origem:

* O título aparece na tag **Sidekick**, de onde os autores podem acessá-los para trabalhar neles.
* As páginas secundárias da página de origem são incluídas no lançamento por padrão. Você pode usar somente a página de origem, se desejar.
* Por padrão, [Live Copy](/help/sites-administering/msm.md) atualiza automaticamente as páginas de lançamento à medida que as páginas de origem são alteradas. É possível especificar que uma cópia estática seja criada para impedir alterações automáticas.

Como opção, especifique a **Data de inicialização** (e a hora) para definir quando as páginas de inicialização devem ser promovidas e ativadas. No entanto, a **Data de inicialização** só funciona em combinação com o sinalizador **Pronto para produção** (consulte [Editar uma configuração de inicialização](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration)); para que as ações realmente ocorram automaticamente, ambas devem ser definidas.

## Criação de um lançamento {#creating-a-launch}

O procedimento a seguir cria um lançamento.

1. Abra a página Administração do site ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin)).
1. Clique em **Novo...** depois **Novo lançamento...**.
1. No **Criar lançamento** especifique valores para as seguintes propriedades:

   * **Título do lançamento**: o nome do lançamento. O nome deve ser significativo para os autores.
   * **Página de origem**: o caminho para a página para a qual criar a inicialização. Por padrão, todas as páginas secundárias são incluídas.
   * **Excluir subpáginas**: selecione essa opção para criar a inicialização somente para a página de origem e não para as páginas secundárias. Por padrão, essa opção não está selecionada.
   * **Manter em Sincronia**: selecione essa opção para atualizar automaticamente o conteúdo das páginas de inicialização quando as páginas de origem forem alteradas. Isso é feito tornando o lançamento um [live copy](/help/sites-administering/msm.md).
   * **Data da inicialização**: a data e a hora em que a cópia de inicialização deve ser ativada (dependendo do sinalizador de **Pronto para produção**; consulte [Inicializações - a ordem dos eventos](/help/sites-authoring/launches.md#launches-the-order-of-events)).

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. Clique em **Criar**.

## Exclusão de um lançamento {#deleting-a-launch}

Você também pode excluir um lançamento.

1. No [inicia o console](/help/sites-classic-ui-authoring/classic-launches.md), selecione a inicialização necessária.
1. Clique em **Excluir** - é necessária uma confirmação:

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >Ao excluir inicializações aninhadas, você deve excluir os níveis mais baixos primeiro.
