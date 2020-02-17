---
title: Publicar páginas
seo-title: Publicar páginas
description: Após criar e revisar seu conteúdo no ambiente de criação, o objetivo é que ele seja disponibilizado no seu site público.
seo-description: Após criar e revisar seu conteúdo no ambiente de criação, o objetivo é que ele seja disponibilizado no seu site público.
uuid: ab5ffc59-1c41-46fe-904e-9fc67d7ead04
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 46d6bde0-8645-4cff-b79c-8e1615ba4ed4
docset: aem65
translation-type: tm+mt
source-git-commit: bcb1840d23ae538c183eecb0678b6a75d346aa50

---


# Publicar páginas{#publishing-pages}

Depois de criar (e revisar) seu conteúdo no ambiente de criação, o objetivo é disponibilizá-lo em seu site público (seu ambiente de publicação).

Isso é referido como a publicação de uma página. Quando você deseja remover uma página do ambiente de publicação, este é o processo de desfazer publicação. Ao publicar e desfazer a publicação, a página permanece disponível no ambiente de criação para modificações adicionais até que você a exclua.

Você também pode publicar/desfazer a publicação de uma página imediatamente ou em uma data/hora predefinida posteriormente.

>[!NOTE]
>
>Certos termos relacionados à publicação podem ser confundidos:
>
>* **Publicar / Não publicar**
   >  Esses são os termos principais das ações que tornam o conteúdo publicamente disponível no ambiente de publicação (ou não).
   >
   >
* **Ativar / Desativar**
   >  Esses termos são sinônimos de publicar/desfazer a publicação.
   >
   >
* **Replicar / Replicação**
   >  Esses são os termos técnicos que descrevem a movimentação de dados (por exemplo, conteúdo da página, arquivos, código, comentários do usuário) de um ambiente para outro, como ao publicar ou reverter a replicação de comentários do usuário.
>



>[!NOTE]
>
>Caso não tenha os privilégios necessários para a publicação de uma página específica:
>
>* Um fluxo de trabalho será acionado para notificar a pessoa adequada sobre a sua solicitação para publicação.
>* Uma mensagem será exibida (por um curto período) para notificá-lo sobre isso.
>



## Publicar uma página {#publishing-a-page}

Existem dois métodos para a ativação de uma página:

* [do console Sites](#activating-a-page-from-the-websites-console)
* [do sidekick na própria página](#activating-a-page-from-sidekick)

>[!NOTE]
>
>Também é possível ativar uma subárvore de várias páginas usando a opção [Ativar árvore](#howtoactivateacompletesectiontreeofyourwebsite) no console Ferramentas.

### Activating a Page from the Websites Console {#activating-a-page-from-the-websites-console}

É possível ativar as páginas no console Sites. Após ter aberto uma página e modificado o conteúdo, volte ao console Sites:

1. No console Sites, selecione a página que deseja ativar.
1. Selecione **Ativar**, no menu superior ou no suspenso, no item da página selecionada.

   Para ativar o conteúdo da página e todas as suas subpáginas, use o [** console Ferramentas **](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#howtoactivateacompletesectiontreeofyourwebsite).

   ![screen_shot_2012-02-08at13817pm](assets/screen_shot_2012-02-08at13817pm.png)

   >[!NOTE]
   >
   >Se necessário, o AEM solicita que você ative ou ative novamente quaisquer ativos relacionadas com a página. É possível selecionar ou desmarcar as caixas de seleção para ativar esses ativos.

1. Se necessário, o AEM solicita que você ative ou ative novamente quaisquer ativos relacionadas com a página. É possível selecionar ou desmarcar as caixas de seleção para ativar esses ativos.

   ![chlimage_1-100](assets/chlimage_1-100.png)

1. O AEM WCM ativa o conteúdo selecionado. A página ou páginas publicadas aparecem no console [Sites](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) (marcado em verde) com as informações sobre quem ativou o conteúdo, bem como a data e a hora da ativação.

   ![screen_shot_2012-02-08at14335pm](assets/screen_shot_2012-02-08at14335pm.png)

### Activating a Page from Sidekick {#activating-a-page-from-sidekick}

Também é possível ativar uma página quando estiver aberta para edição.

Após ter aberto a página e o conteúdo modificado:

1. Selecione a guia **Página** no Sidekick.
1. Clique em **Ativar página**. Uma mensagem é exibida no canto superior direito da janela, confirmando que a página foi ativada.

## Desfazer publicação de uma página {#unpublishing-a-page}

Para remover uma página do ambiente de publicação é necessário desativar o conteúdo.

Para desativar uma página:

1. No console Sites, selecione a página que deseja desativar.
1. Selecione **Desativar**, no menu superior ou no suspenso, no item da página selecionada. Será solicitado que você confirme a exclusão.

   ![screen_shot_2012-02-08at14859pm](assets/screen_shot_2012-02-08at14859pm.png)

1. Atualize o console [Sites](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) e o conteúdo é marcado em vermelho, indicando que não está mais publicado.

   ![screen_shot_2012-02-08at15018pm](assets/screen_shot_2012-02-08at15018pm.png)

## Ativar/desativar posteriormente {#activate-deactivate-later}

### Ativar mais tarde {#activate-later}

Para agendar a ativação para um momento posterior:

1. No console Sites, vá para o menu **Ativar** e selecione **Ativar mais tarde**.
1. In the dialog that opens you provide the date and time for activation and click **OK**. This creates a version of the page that is activated at the specified time.

   ![screen_shot_2012-02-08at14751pm](assets/screen_shot_2012-02-08at14751pm.png)

Ao ativar mais tarde, um fluxo de trabalho é iniciado para ativar esta versão de página na hora especificada. Por outro lado, a desativação mais tarde inicia um fluxo de trabalho para desativar esta versão de página em uma hora específica.

Caso deseje cancelar essa ativação/desativação, acesse o console [Fluxo de trabalho ](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) para encerrar o fluxo de trabalho correspondente.

### Desativar mais tarde {#deactivate-later}

Para agendar a desativação para um momento posterior:

1. In the Website console, go to the **Deactivate** menu, and select **Deactivate later**.

1. In the dialog that opens you provide the date and time for deactivation and click **OK**.

   ![screen_shot_2012-02-08at15129pm](assets/screen_shot_2012-02-08at15129pm.png)

**Ao desativar mais tarde,** um fluxo de trabalho é iniciado para desativar esta versão de página na hora específica.

Caso deseje cancelar essa desativação, acesse o console [Fluxo de trabalho ](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) para encerrar o fluxo de trabalho correspondente.

## Ativação/Desativação agendada (Tempo desligado/ligado) {#scheduled-activation-deactivation-on-off-time}

Você pode agendar horários para publicar/desfazer a publicação de uma página usando o **Tempo ligado** e **Tempo desligado** que podem ser definidos nas [Propriedades da página](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

### Determinar o status de publicação da página {#determining-page-publication-status-classic-ui}

O status pode ser visualizado no [console Sites](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console). As cores indicam o status da publicação.

## Ativar uma seção completa (árvore) do seu site {#activating-a-complete-section-tree-of-your-website}

Na guia **Sites** é possível ativar as páginas individuais. Ao entrar ou atualizar um número considerável de páginas de conteúdo - todos residentes na mesma página raiz - pode ser mais fácil ativar toda a árvore em uma ação. Também é possível a execução de prática para emular uma ativação e destacar quais as páginas foram ativadas.

1. Open the **Tools** console by selecting it from the **Welcome** page and then double-click **Replication** to open the console ( `https://localhost:4502/etc/replication.html`).

   ![screen_shot_2012-02-08at125033pm](assets/screen_shot_2012-02-08at125033pm.png)

1. No console **Replicação**, clique na **árvore Activate**.

   The following window ( `https://localhost:4502/etc/replication/treeactivation.html`) will be displayed.

   ![screen_shot_2012-02-08at125033pm-1](assets/screen_shot_2012-02-08at125033pm-1.png)

1. Enter the **Start Path**. This specifies the path to the root of the section you want to activate (publish). This page and all pages underneath are considered for activation (or used in the emulation if a Dry Run is selected).
1. Ative os critérios de seleção conforme necessário:

   * **Somente modificados**: ativar apenas as páginas que foram modificadas.
   * **Somente ativados**: somente ativar páginas que (já) foram ativadas. Atua como uma forma de reativação.
   * **Ignorar desativados**: ignorar todas as páginas que foram desativadas.

1. Selecione a ação que deseja executar:

   1. Select **Dry Run** if you want to check which pages *would* be activated. This is only an emulation, no pages will be activated.

   1. Select **Activate** if you want to activate the pages.
