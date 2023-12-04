---
title: Publicar páginas
description: Depois de criar e revisar seu conteúdo no ambiente de criação, disponibilize-o em seu site público.
uuid: ab5ffc59-1c41-46fe-904e-9fc67d7ead04
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 46d6bde0-8645-4cff-b79c-8e1615ba4ed4
docset: aem65
exl-id: 3f6aa06e-b5fd-4ab0-9ecc-14250cb3f55e
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 9%

---

# Publicar páginas{#publishing-pages}

Depois de criar e revisar seu conteúdo no ambiente de criação, disponibilize-o em seu site público (seu ambiente de publicação).

Isso é chamado de publicação de uma página. Quando você deseja remover uma página do ambiente de publicação, este é o processo de desfazer a publicação. Ao publicar ou desfazer a publicação, a página permanecerá disponível no ambiente do autor para mais alterações até ser excluída.

Você também pode publicar/desfazer a publicação de uma página imediatamente ou em uma data/hora predefinida posteriormente.

>[!NOTE]
>
>Alguns termos relacionados à publicação podem ser confundidos:
>
>* **Publicar/Desfazer a publicação**
>  Esses são os termos principais para as ações que tornam o conteúdo publicamente disponível no ambiente de publicação (ou não).
>
>* **Ativar / Desativar**
>  Estes termos são sinônimos de publicar/desfazer a publicação.
>
>* **Replicar / Replicação**
>  Esses são os termos técnicos que descrevem a movimentação de dados (por exemplo, conteúdo da página, arquivos, código, comentários do usuário) de um ambiente para outro, como ao publicar ou reverter a replicação de comentários do usuário.
>

>[!NOTE]
>
>Se você não tiver os privilégios necessários para publicar uma página específica:
>
>* Um fluxo de trabalho será acionado para notificar a pessoa apropriada sobre sua solicitação de publicação.
>* Uma mensagem será exibida (por um curto período de tempo) para notificá-lo sobre isso.
>

## Publicar uma página {#publishing-a-page}

Há dois métodos para ativar uma página:

* [no console Sites](#activating-a-page-from-the-websites-console)
* [do sidekick na própria página](#activating-a-page-from-sidekick)

>[!NOTE]
>
>Também é possível ativar uma subárvore de várias páginas usando [Ativar árvore](#howtoactivateacompletesectiontreeofyourwebsite) no console Ferramentas.

### Ativar uma página no console Sites {#activating-a-page-from-the-websites-console}

Você pode ativar páginas no console Sites. Depois de abrir uma página e modificar seu conteúdo, você retorna ao console Sites:

1. No console Sites, selecione a página que deseja ativar.
1. Selecionar **Ativar**, no menu superior ou no menu suspenso do item de página selecionado.

   Para ativar o conteúdo da página e todas as suas subpáginas, use o [**Ferramentas** console](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#howtoactivateacompletesectiontreeofyourwebsite).

   ![screen_shot_2012-02-08at13817pm](assets/screen_shot_2012-02-08at13817pm.png)

   >[!NOTE]
   >
   >Se necessário, o AEM solicita que você ative ou reative quaisquer ativos vinculados à página. Você pode marcar ou desmarcar as caixas de seleção para ativar esses ativos.
   >
   >

1. Se necessário, o AEM solicita que você ative ou reative quaisquer ativos vinculados à página. Você pode marcar ou desmarcar as caixas de seleção para ativar esses ativos.

   ![chlimage_1-100](assets/chlimage_1-100.png)

1. O WCM do AEM ativa o conteúdo selecionado. As páginas publicadas aparecem no [Console de sites](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) (marcado em verde) com informações sobre quem ativou o conteúdo e a data e hora da ativação.

   ![screen_shot_2012-02-08at14335pm](assets/screen_shot_2012-02-08at14335pm.png)

### Ativar uma página do Sidekick {#activating-a-page-from-sidekick}

Você também pode ativar uma página quando ela estiver aberta para edição.

Depois de abrir a página e modificar seu conteúdo, você:

1. Selecione o **Página** no Sidekick.
1. Clique em **Ativar página**.
Uma mensagem é exibida na parte superior direita da janela confirmando que a página foi ativada.

## Desfazer a publicação de uma página {#unpublishing-a-page}

Para remover uma página do ambiente de publicação, você desativa o conteúdo.

Para desativar uma página:

1. No console Sites, selecione a página que deseja desativar.
1. Selecionar **Desativar**, no menu superior ou no menu suspenso do item de página selecionado. Você será solicitado a confirmar a exclusão.

   ![screen_shot_2012-02-08at14859pm](assets/screen_shot_2012-02-08at14859pm.png)

1. Atualize o [Console de sites](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) e o conteúdo é marcado em vermelho, indicando que não é mais publicado.

   ![screen_shot_2012-02-08at15018pm](assets/screen_shot_2012-02-08at15018pm.png)

## Ativar/desativar mais tarde {#activate-deactivate-later}

### Ativar mais tarde {#activate-later}

Para agendar sua ativação para um horário posterior:

1. No console Sites, acesse o **Ativar** e selecione **Ativar mais tarde**.
1. Na caixa de diálogo aberta, forneça a data e a hora para ativação e clique em **OK**. Isso cria uma versão da página que é ativada no horário especificado.

   ![screen_shot_2012-02-08at14751pm](assets/screen_shot_2012-02-08at14751pm.png)

Ativar mais tarde inicia um fluxo de trabalho para ativar essa versão da página no horário especificado. Por outro lado, a desativação posterior inicia um fluxo de trabalho para desativar essa versão de página em um momento específico.

Se quiser cancelar essa ativação/desativação, acesse o [Console de fluxo de trabalho](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) para encerrar o workflow correspondente.

### Desativar mais tarde {#deactivate-later}

Para programar a desativação para um momento posterior:

1. No console do Site, acesse o **Desativar** e selecione **Desativar mais tarde**.

1. Na caixa de diálogo aberta, forneça a data e a hora para a desativação e clique em **OK**.

   ![screen_shot_2012-02-08at15129pm](assets/screen_shot_2012-02-08at15129pm.png)

**Desativando depois** r inicia um fluxo de trabalho para desativar essa versão de página em um horário específico.

Se quiser cancelar essa desativação, acesse o [Console de fluxo de trabalho](/help/sites-administering/workflows-administering.md#main-pars_title_3-yjqslz-refd) para encerrar o workflow correspondente.

## Ativação/Desativação Programada (Hora de Ativação/Desativação) {#scheduled-activation-deactivation-on-off-time}

É possível agendar os horários de publicação/despublicação de uma página usando o **No Prazo** e **Tempo desligado** que pode ser definido na variável [Propriedades da página](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md).

### Determinação do status de publicação da página {#determining-page-publication-status-classic-ui}

O status pode ser visto no campo [Console de sites](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console). As cores indicam o status da publicação.

## Ativar uma seção completa (árvore) do site {#activating-a-complete-section-tree-of-your-website}

No **Sites** guia, é possível ativar as páginas individuais. Quando você tiver inserido ou atualizado um número considerável de páginas de conteúdo, todas as quais residem na mesma página raiz, pode ser mais fácil ativar toda a árvore em uma ação. Também é possível executar um Dry Run para emular uma ativação e realçar quais páginas seriam ativadas.

1. Abra o **Ferramentas** ao selecioná-lo na lista suspensa **Bem-vindo** e clique duas vezes em **Replicação** para abrir o console ( `https://localhost:4502/etc/replication.html`).

   ![screen_shot_2012-02-08at125033pm](assets/screen_shot_2012-02-08at125033pm.png)

1. No **Replicação** , clique em **Ativar árvore**.

   A janela a seguir ( `https://localhost:4502/etc/replication/treeactivation.html`) será exibida.

   ![screen_shot_2012-02-08at125033pm-1](assets/screen_shot_2012-02-08at125033pm-1.png)

1. Insira o **Caminho inicial**. Especifica o caminho para a raiz da seção que você deseja ativar (publicar). Esta página e todas as páginas abaixo dela são consideradas para ativação (ou usadas na emulação se um Dry Run estiver selecionado).
1. Ative os critérios de seleção conforme necessário:

   * **Somente modificados**: ativar somente as páginas que foram modificadas.
   * **Somente ativado**: ativar somente as páginas que (já) foram ativadas. Atua como uma forma de reativação.
   * **Ignorar desativados**: ignore todas as páginas que foram desativadas.

1. Selecione a ação que deseja executar:

   1. Selecionar **Dry Run** se quiser verificar quais páginas *seria* ser ativados. Isso é apenas uma emulação, nenhuma página será ativada.

   1. Selecionar **Ativar** se desejar ativar as páginas.
