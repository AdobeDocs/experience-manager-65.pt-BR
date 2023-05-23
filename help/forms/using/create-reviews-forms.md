---
title: Criação e gerenciamento de revisões para ativos em formulários
seo-title: Creating and managing reviews for assets in forms
description: Uma Revisão é um mecanismo que permite que um ou mais revisores comentem sobre um ativo que está disponível em um formulário.
seo-description: A Review is a mechanism that allows one or more reviewers to comment on an asset that is available in a form.
uuid: 45c7ff56-3fa8-4a0f-8597-05404e547282
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: d8c1c507-a6c4-44f5-be01-ee902bc28410
docset: aem65
feature: Adaptive Forms
exl-id: 9ca4fcd6-3eb0-4fc1-a09c-e4ad532bbed0
source-git-commit: 4edfc51227607b4fb3ee4b97443d2040015b6a65
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Criação e gerenciamento de revisões para ativos em formulários{#creating-and-managing-reviews-for-assets-in-forms}

## Análise {#review}

Uma Revisão é um mecanismo que permite que um ou mais revisores comentem sobre um ativo que está disponível em um formulário.

## Configurar uma revisão {#setting-up-a-review}

1. Navegue até a guia Forms e selecione um formulário.
1. Se o ativo não tiver uma revisão em andamento, inicie uma revisão ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) aparece na barra de Ações. Clique em Iniciar revisão ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) ícone.
1. Insira as seguintes informações:

   * Nome da revisão: obrigatório, pode conter caracteres alfanuméricos, hífen ou sublinhado.
   * Descrição da revisão: opcional, descrição da finalidade/conteúdo para revisão.
   * Prazo da revisão: opcional, a data em que a revisão termina. Quando ultrapassado o prazo, a tarefa aparece como &#39;Vencida&#39;.
   * Revisores: é obrigatório no mínimo um. Use a caixa de combinação para adicionar revisores. Digitar um nome lista todos os nomes correspondentes; selecione um nome e clique em Adicionar.

1. Preencha todos os detalhes restantes e clique em Start.

### Ações que ocorrem quando uma revisão é configurada {#actions-that-occur-when-a-review-is-set-up}

Esta seção descreve o que acontece quando uma revisão é criada ou configurada.

1. Uma nova tarefa de revisão é criada e atribuída ao iniciador da revisão.
1. Todos os revisores recebem uma tarefa de revisão. A tarefa é exibida na seção Notificações. Um revisor pode clicar em uma notificação ou ir para a Caixa de entrada para exibir a tarefa. Um revisor pode clicar em para abrir a tarefa de revisão, exibir o formulário e começar a adicionar comentários.

   ![Alerta de notificação do revisor](assets/noti.png)

   Alerta de notificação do revisor

1. A caixa de comentário está disponível para o iniciador e revisores do ativo. Outras pessoas podem exibir os comentários, mas não podem escrevê-los.

## Gerenciamento de uma revisão {#managing-a-review}

>[!NOTE]
>
>Somente as revisões em andamento podem ser modificadas. As revisões concluídas não podem ser modificadas.

1. Navegue até a guia Forms e selecione um formulário.

1. Se um ativo tiver uma revisão em andamento e você for o iniciador da revisão, uma opção Gerenciar revisão ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) ícones são exibidos na barra de Ações. Somente o iniciador da revisão pode gerenciar (atualizar/encerrar) a revisão.

   Clique em Gerenciar revisão ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)ícone.

   Para usuários diferentes do iniciador, o ícone Gerenciar revisão está desativado.

1. Você obtém uma tela que exibe informações:

   * **Nome da revisão**: não pode ser editado.

   * **Descrição da revisão**: disponível para edição.

   * **Prazo da revisão**: disponível para edição. É possível modificar o prazo para qualquer data e hora além da data e hora atuais.

   * **Revisores**: disponível para edição. É possível adicionar ou remover revisores. Se uma tarefa estiver vencida, você poderá adicionar revisores somente depois de estender o prazo além da data atual.

1. Para encerrar a revisão, clique em Encerrar.

### Ações que ocorrem quando uma revisão é modificada {#actions-that-occur-when-a-review-is-modified}

Esta seção descreve o que acontece no final/modificação da revisão:

1. Se a Descrição da revisão for modificada, a tarefa correspondente dos revisores e do iniciador será atualizada.
1. Se o Prazo de revisão for modificado, a tarefa correspondente para os revisores será atualizada com a nova data.

1. Se um revisor for removido:

   ![Remover um revisor](assets/removeduser.png)

   Remover um revisor

   1. Se estiver incompleta, a tarefa atribuída será encerrada.
   1. O revisor não pode mais comentar no ativo.

1. Se um revisor for adicionado:

   ![Adicionar um revisor](assets/addedreviewer.png)

   Adicionar um revisor

   1. Uma tarefa de revisão é criada e atribuída ao revisor recém-adicionado.
   1. O revisor recém-adicionado pode adicionar comentários ao ativo.

1. Quando uma revisão termina:

   1. **Revisores**: Para cada revisor, a tarefa incompleta relacionada à revisão é encerrada. A tarefa não aparece mais como &#39;Pendente&#39; na seção Notificações do revisor.
   1. **Iniciador**: a tarefa atribuída ao iniciador da revisão está marcada como concluída. A tarefa é removida da seção Notificação do iniciador da revisão.
   1. **Todos**: a revisão aparece na seção Análises anteriores. Nenhum comentário adicional pode ser adicionado.
