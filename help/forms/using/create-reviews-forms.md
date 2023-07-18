---
title: Criar e gerenciar revisões em formulários
seo-title: Creating and managing reviews in forms
description: Uma Revisão é um mecanismo que permite que um ou mais revisores comente em um formulário.
seo-description: A Review is a mechanism that allows one or more reviewers to comment on a form.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
feature: Adaptive Forms
exl-id: 9ca4fcd6-3eb0-4fc1-a09c-e4ad532bbed0
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 2%

---

# Criar e gerenciar revisões em formulários{#creating-and-managing-reviews-to-forms}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms.html?lang=pt-br) |
| AEM 6.5 | Este artigo |

## Análise {#review}

Uma revisão é um mecanismo que permite que um ou mais revisores comentem formulários.

## Configurar uma revisão {#setting-up-a-review}

1. Navegue até o navegador de formulários e selecione um formulário para revisão.
1. Se o Formulário não tiver uma revisão em andamento, uma solicitação **Iniciar revisão** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) aparece na barra de Ações. Clique em **Iniciar revisão** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) ícone.
1. Insira as seguintes informações:

   * **Título**: obrigatório, pode conter caracteres alfanuméricos, hífen e sublinhado.
   * **Descrição**: opcional, descrição da finalidade/conteúdo para revisão.
   * **Prazo**: opcional, a data em que a revisão termina. Quando ultrapassado o prazo, a tarefa aparece como &#39;Vencida&#39;.
   * **Nome do Revisor**: no mínimo um é obrigatório. use a caixa de combinação para adicionar revisores, digitando uma lista de nomes com todos os nomes correspondentes; selecione um nome e clique em **Adicionar**. Na próxima seção do **Revisores** mostra o nome de todos os revisores.

1. Clique em **Início** para iniciar uma revisão.

   >[!NOTE]
   >
   >* O administrador pode acessar qualquer grupo associado aos usuários do formulário.
   >* O grupo Usuários de Serviço não está disponível para seleção para revisão.

### Ações que ocorrem quando uma revisão é configurada {#actions-that-occur-when-a-review-is-set-up}

Esta seção descreve o que acontece quando uma revisão é criada ou configurada.

1. Uma nova tarefa de revisão é criada e atribuída ao revisor selecionado.
1. Todos os revisores recebem uma tarefa de revisão. A tarefa é exibida na seção Notificações. Um revisor pode clicar em uma notificação ou ir para a Caixa de entrada para exibir a tarefa. Um revisor pode clicar em para abrir a tarefa de revisão, exibir o formulário e começar a adicionar comentários.

   ![Alerta de notificação do revisor](assets/review-notification-img.png)

   Alerta de notificação do revisor

1. A caixa comment está disponível para os revisores do formulário. Outras pessoas podem ler os comentários, mas não podem adicionar os seus próprios.

## Gerenciamento de uma revisão {#managing-a-review}

>[!NOTE]
>
>* Somente as revisões em andamento podem ser modificadas.
>* As revisões concluídas não podem ser modificadas.

1. Navegue até a guia formulários e selecione um formulário.

1. Se um formulário tiver uma revisão em andamento e você for o iniciador da revisão, uma solicitação **Gerenciar revisão** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) ícones são exibidos na barra de Ações. Somente o iniciador da revisão pode gerenciar (Atualizar/Encerrar) a revisão.

   Clique em **Gerenciar revisão** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)ícone.

   Para usuários diferentes do iniciador, o ícone Gerenciar revisão está desativado.

1. Agora você obtém uma tela que exibe informações:

   * **Nome da revisão**: não pode ser editado.

   * **Descrição da revisão**: disponível para edição.

   * **Prazo da revisão**: disponível para edição. É possível modificar o prazo para qualquer data e hora além da data e hora atuais.

   * **Revisores**: disponível para edição. É possível adicionar ou remover revisores. Se uma tarefa estiver vencida, você poderá adicionar revisores somente depois de estender o prazo além da data atual.

1. Para encerrar a revisão, clique em **Fim**.

### Ações que ocorrem quando uma revisão é modificada {#actions-that-occur-when-a-review-is-modified}

Esta seção descreve o que acontece em **Atualização/Fim da Revisão**:

1. Se a descrição da revisão for modificada, a tarefa correspondente dos revisores e do iniciador será atualizada.
1. Se o prazo da revisão for modificado, a tarefa correspondente para os revisores será atualizada com a nova data.

1. Se um revisor for removido:

   ![Remover um revisor](assets/removeduser.png)

   Remover um revisor

   1. Se estiver incompleta, a tarefa atribuída será encerrada.
   1. O revisor não pode mais comentar no formulário.

1. Se um revisor for adicionado:

   ![Adicionar um revisor](assets/addedreviewer.png)

   Adicionar um revisor

   1. Uma tarefa de revisão é criada e atribuída ao revisor recém-adicionado.
   1. O revisor recém-adicionado pode adicionar comentários sobre o formulário.

1. Quando uma revisão termina:

   1. **Revisores**: Para cada revisor, a tarefa incompleta relacionada à revisão é encerrada. A tarefa não aparece mais como &#39;Pendente&#39; na seção Notificações do revisor.
   1. **Iniciador**: a tarefa atribuída ao iniciador da revisão está marcada como concluída. A tarefa é removida da seção Notificação do iniciador da revisão.
   1. **Todos**: a revisão aparece na seção Análises anteriores. Nenhum comentário adicional pode ser adicionado.

   ![revisão concluída](assets/review-complete-imgg.png)
