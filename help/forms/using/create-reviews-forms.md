---
title: Criação e gerenciamento de revisões de ativos em formulários
seo-title: Criação e gerenciamento de revisões de ativos em formulários
description: 'Uma revisão é um mecanismo que permite que um ou mais revisores comentem sobre um ativo disponível em um formulário. '
seo-description: 'Uma revisão é um mecanismo que permite que um ou mais revisores comentem sobre um ativo disponível em um formulário. '
uuid: 45c7ff56-3fa8-4a0f-8597-05404e547282
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: d8c1c507-a6c4-44f5-be01-ee902bc28410
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---


# Criação e gerenciamento de revisões de ativos em formulários{#creating-and-managing-reviews-for-assets-in-forms}

## Análise {#review}

Uma revisão é um mecanismo que permite que um ou mais revisores comentem sobre um ativo disponível em um formulário.

## Configuração de uma revisão {#setting-up-a-review}

1. Navegue até a guia Forms e selecione um formulário.
1. Se o ativo não tiver uma revisão em andamento, um ícone Revisão de Start ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) será exibido na barra de Ação. Clique no ícone Revisão do Start ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png).
1. Digite as seguintes informações:

   * Nome da revisão: Obrigatório, pode conter caracteres alfanuméricos, hífen ou sublinhado.
   * Descrição da análise: Opcional, descrição da finalidade/conteúdo para análise.
   * Prazo de revisão: Opcional, a data em que a revisão termina. Quando ultrapassado o prazo, a tarefa aparece como &quot;Vencida&quot;.
   * Revisores: Um mínimo de um é obrigatório. Use a caixa de combinação para adicionar revisores. Digitar um nome lista todos os nomes correspondentes; selecione um nome e clique em Adicionar.

1. Preencha todos os detalhes restantes e clique em Start.

### Ações que ocorrem quando uma revisão é configurada {#actions-that-occur-when-a-review-is-set-up}

Esta seção descreve o que acontece quando uma revisão é criada ou configurada.

1. Uma nova tarefa de revisão é criada e atribuída ao iniciador da revisão.
1. Todos os revisores recebem uma tarefa de revisão. A tarefa é exibida na seção Notificações. Um revisor pode clicar em uma notificação ou ir para a Caixa de entrada para visualização da tarefa. Um revisor pode clicar para abrir a tarefa de revisão, para visualização do formulário e para adicionar comentários ao start.

   ![Alerta de notificação do revisor](assets/noti.png)

   Alerta de notificação do revisor

1. A caixa de comentários está disponível para o iniciador e os revisores do ativo. Outros podem visualização os comentários, mas não podem escrever comentários.

## Gerenciar uma revisão {#managing-a-review}

>[!NOTE]
>
>Somente as revisões em andamento podem ser modificadas. As revisões concluídas não podem ser modificadas.

1. Navegue até a guia Forms e selecione um formulário.

1. Se um ativo tiver uma revisão em andamento e você for o iniciador da revisão, um ícone Gerenciar revisão ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) será exibido na barra de Ação. Somente o iniciador de revisão pode gerenciar (atualizar/encerrar) a revisão.

   Clique no ícone Gerenciar revisão ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png).

   Para outro usuário que não seja iniciador, o ícone Gerenciar revisão está desativado.

1. Você obtém uma tela que exibe informações:

   * **Nome** da revisão: Não é possível editar.

   * **Descrição** da revisão: Disponível para edição.

   * **Prazo** de revisão: Disponível para edição. É possível modificar o prazo para qualquer data e hora além da data e hora atuais.

   * **Revisores**: Disponível para edição. Você pode adicionar ou remover revisores. Se uma tarefa estiver atrasada, você poderá adicionar revisores somente depois de estender o prazo para além da data atual.

1. Edite os campos necessários e clique em Atualizar.

   ![Revisar estado atualizado no Gerenciador de Tarefas](assets/tskmgr.png)

   Revisar estado atualizado no Gerenciador de Tarefas

1. Para encerrar a revisão, clique em Encerrar.

### Ações que ocorrem quando uma revisão é modificada {#actions-that-occur-when-a-review-is-modified}

Esta seção descreve o que acontece no final/modificação da revisão:

1. Se a descrição de Revisão for modificada, a tarefa correspondente de revisores e o iniciador será atualizada.
1. Se o prazo de revisão for modificado, a tarefa correspondente para os revisores será atualizada com a nova data.

1. Se um revisor for removido:

   ![Remoção de um revisor](assets/removeduser.png)

   Remoção de um revisor

   1. Se estiver incompleta, a tarefa atribuída será encerrada.
   1. O revisor não pode mais comentar o ativo.

1. Se um revisor for adicionado:

   ![Adicionar um revisor](assets/addedreviewer.png)

   Adicionar um revisor

   1. Uma tarefa de revisão é criada e atribuída ao revisor recém-adicionado.
   1. O revisor recém-adicionado pode adicionar comentários para o ativo.

1. Quando uma revisão terminar:

   1. **Revisores**: Para cada revisor, a tarefa incompleta relacionada com o reexame é encerrada. A tarefa não aparece mais como &quot;Pendente&quot; na seção Notificações do revisor.
   1. **Iniciador**: A tarefa atribuída ao iniciador da revisão está marcada como concluída. A tarefa é removida da seção Notificação do iniciador da revisão.
   1. **Todos**: A revisão é exibida na seção Análises anteriores. Não podem ser acrescentadas outras observações.

