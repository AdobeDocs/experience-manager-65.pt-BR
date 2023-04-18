---
title: Editar inicializações
description: Depois de criar um lançamento para sua página (ou conjunto de páginas), você pode editar o conteúdo na cópia de lançamento das páginas.
uuid: 1f2c2e53-73a3-4bd7-b2c7-425491bc0118
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 30aa3177-bcf4-4260-8f64-e73bc907942a
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 2d441820-b394-47c8-b4ca-a8aede590937
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 38%

---

# Edição de inicializações{#editing-launches}

## Editar páginas de lançamento {#editing-launch-pages}

Quando um lançamento é criado para uma página (ou um conjunto de páginas), é possível editar o conteúdo na cópia de lançamento da(s) página(s).

1. Acesse [Inicialização a partir de Referências (console Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console) para mostrar as ações disponíveis.
1. Selecionar **Ir para a página** para abrir a página para edição.

>[!NOTE]
>
>Você não tem permissão para mover uma página em um lançamento. Tentar esta ação acionará uma mensagem de aviso:
>
>* Aviso: esta página é a origem de um lançamento. Não é permitido mover a página.


### Edição de páginas de lançamento sujeitas a uma live copy {#editing-launch-pages-subject-to-a-live-copy}

Se o lançamento se basear em um [live copy](/help/sites-administering/msm.md) em seguida, você:

* consulte símbolos de bloqueio (pequenos cadeados) ao editar um componente (conteúdo e/ou propriedades).
* consulte o **Live Copy** em **Propriedades da página**

Uma livecopy é usada para sincronizar o conteúdo da *ramificação de origem* para a *ramificação de inicialização* (para manter a inicialização atualizada com as alterações feitas na origem).

Você pode fazer alterações da mesma maneira que pode editar uma live copy padrão; por exemplo:

* Clicar em um cadeado fechado quebrará essa sincronização e permitirá que você faça novas atualizações no conteúdo no seu lançamento. Depois de desbloqueadas (cadeado aberto), as alterações não serão substituídas por alterações feitas no mesmo local na ramificação de origem.
* **Suspender** (e **Retomar**) herança de uma página específica.

Consulte [Alterar conteúdo da Live Copy](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) para obter mais informações.

## Comparação de uma página de lançamento a sua página de origem {#comparing-a-launch-page-to-its-source-page}

Para rastrear as alterações feitas, é possível exibir a inicialização em **Referências** e comparar a página de inicialização com a página de origem:

1. No **Sites** console, [navegue até a página de origem do seu lançamento e selecione-a](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources).
1. Abra o **[Referências](/help/sites-authoring/basic-handling.md#references)** e selecione **Lançamentos**.
1. Selecione seu lançamento específico e **Comparar à Origem**:

   ![screen-shot_2019-03-05at121952](assets/screen-shot_2019-03-05at121952.png)

1. As duas páginas (lançamento e origem) serão abertas lado a lado.

   Para obter informações completas sobre como usar esse recurso, consulte [Diff da página](/help/sites-authoring/page-diff.md).

## Alterar as páginas de origem usadas {#changing-the-source-pages-used}

A qualquer momento, você pode adicionar ou remover páginas ao/do intervalo de páginas de origem para um lançamento:

1. Acesse e selecione o lançamento a partir do seguinte:

   * o [Console Lançamentos](/help/sites-authoring/launches.md#the-launches-console):

      * Selecione **Editar**.
   * [Referências (console Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console) para mostrar as ações disponíveis:

      * Selecione **Editar lançamento**.

   As páginas de origem serão exibidas.

1. Faça as alterações necessárias e confirme com **Salvar**.

   >[!NOTE]
   >
   >Para adicionar páginas a um lançamento, elas devem estar abaixo de uma raiz de idioma comum; ou seja, em um único site.

## Editar uma configuração do Launch {#editing-a-launch-configuration}

A qualquer momento, você pode editar as propriedades de um lançamento:

1. Acesse e selecione o lançamento a partir do seguinte:

   * o [Console Lançamentos](/help/sites-authoring/launches.md#the-launches-console):

      * Selecionar **Propriedades**.
   * [Referências (console Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console) para mostrar as ações disponíveis:

      * Selecione **Editar propriedades**.

   Os detalhes serão mostrados.

1. Faça as alterações necessárias e confirme com **Salvar**.

   Consulte [Inicializações - a Ordem dos eventos](/help/sites-authoring/launches.md#launches-the-order-of-events) para obter informações sobre a finalidade e interação dos campos **Data de inicialização** e **Pronto para produção**.

## Descobrindo o status de lançamento de uma página {#discovering-the-launch-status-of-a-page}

O status é mostrado quando você seleciona um lançamento específico na guia Referências (consulte [Lançamentos em Referências (console Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console)).

![screen-shot_2019-03-05at121901](assets/screen-shot_2019-03-05at121901.png)
