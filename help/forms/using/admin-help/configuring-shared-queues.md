---
title: Configuração de filas compartilhadas
seo-title: Configuração de filas compartilhadas
description: As Filas compartilhadas permitem que você configure e gerencie as filas de usuários de forma eficaz. Saiba como configurar filas compartilhadas.
seo-description: As Filas compartilhadas permitem que você configure e gerencie as filas de usuários de forma eficaz. Saiba como configurar filas compartilhadas.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# Configuração de filas compartilhadas{#configuring-shared-queues}

As Filas compartilhadas permitem que você configure e gerencie as filas de usuários de forma eficaz. Uma fila de usuários é simplesmente todas as tarefas atribuídas a um usuário, consulte [Listas de tarefas ](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) para obter mais informações. Você pode atribuir, cancelar a atribuição e reatribuir filas de usuário, dependendo de suas necessidades organizacionais. Você pode gerenciar Filas compartilhadas de duas formas:

**Gerenciar Acesso A Um Usuário**

Você pode gerenciar o acesso a uma fila de usuários selecionada usando essa opção.

**Gerenciar Acesso Por Um Usuário**

Você pode gerenciar filas compartilhadas atribuídas a um usuário selecionado usando essa opção.

## Gerenciando o acesso a uma fila de usuários selecionada {#managing-access-to-a-selected-user-queue}

A funcionalidade Gerenciar acesso a um usuário permite gerenciar o acesso a uma fila de usuários selecionada. Você pode conceder ou revogar o acesso a uma fila de usuários selecionada para outros usuários em sua organização. Por exemplo, Kara Bowman está fora do escritório. Usando a funcionalidade Gerenciar acesso a um usuário, sua fila pode ser compartilhada com Akira Tanaka e John Jacobs para conclusão. Mais tarde, quando Kara Bowman voltar ao escritório, você pode revogar o acesso à sua fila de Akira Tanaka e John Jacobs.

Depois de compartilhadas, essas tarefas podem ser concluídas pelo usuário, com acesso à fila, usando o Workspace.

>[!NOTE]
>
>O Flex Workspace está obsoleto para AEM versão de formulários.

### Configurar acesso a uma fila de usuários selecionada {#configuring-access-to-a-selected-user-queue}

1. Faça logon no console de administração usando uma conta de administrador.
1. Selecione **Serviços** > **fluxo de trabalho de formulários** > **Fila compartilhada**.

1. Na guia Gerenciar acesso a um usuário, localize e selecione o usuário cuja fila você deseja compartilhar. A qualquer momento, o painel inferior direito exibe a lista dos usuários com acesso à fila de usuários selecionada.
1. No painel inferior esquerdo, localize e selecione o usuário. Clique em Compartilhar.
1. Clique em Salvar para concluir.

### Revogando o acesso a uma fila de usuários selecionada {#revoking-access-to-a-selected-user-queue}

1. Faça logon no console de administração usando uma conta de administrador.
1. Selecione **Serviços** > **fluxo de trabalho de formulários** > **Fila compartilhada**.

1. Na guia Gerenciar acesso a um usuário, localize e selecione o usuário cuja fila você deseja gerenciar.
1. O painel inferior direito exibe a lista dos usuários com acesso à fila de usuários selecionada. Selecione o usuário e clique em Revogar.
1. Clique em Salvar para concluir.

## Gerenciando filas atribuídas a um usuário {#managing-queues-assigned-to-a-user}

A funcionalidade Gerenciar acesso por usuário permite gerenciar filas atribuídas a um usuário selecionado. Você pode conceder ou revogar o acesso às filas do usuário a um usuário selecionado individualmente. Por exemplo, você deseja atribuir filas de usuário de Akira Tanaka e John Jacobs a Kara Bowman. Usando a funcionalidade Gerenciar acesso por um usuário, você pode pesquisar por Kara Bowman e conceder acesso às tarefas atribuídas a Akira Tanaka e John Jacobs. Posteriormente, você poderá revogar o acesso de Kara Bowman a essas filas de usuários.

Depois de atribuídas, essas tarefas podem ser concluídas pelo usuário usando o Workspace.

>[!NOTE]
>
>O Flex Workspace está obsoleto para AEM versão de formulários.

### Conceder acesso a uma fila de usuários selecionada {#granting-access-to-a-selected-user-queue}

1. Faça logon no console de administração usando uma conta de administrador.
1. Selecione **Serviços** > **fluxo de trabalho de formulários** > **Fila compartilhada**.

1. Na guia Gerenciar acesso a um usuário, localize e selecione o usuário cuja fila você deseja compartilhar. A qualquer momento, o painel inferior direito exibe a lista dos usuários com acesso à fila de usuários selecionada.
1. No painel inferior esquerdo, localize e selecione as filas de usuário que deseja compartilhar com o usuário selecionado. Clique em Compartilhar.
1. Clique em Salvar para concluir.

### Revogando o acesso a uma fila de usuários selecionada {#revoking_access_to_a_selected_user_queue-1}

1. Faça logon no console de administração usando uma conta de administrador.
1. Selecione **Serviços** > **fluxo de trabalho de formulários** > **Fila compartilhada**.

1. Na guia Gerenciar acesso por usuário, localize e selecione o usuário cuja fila você deseja gerenciar.
1. O painel inferior direito exibe a lista das filas de usuário atribuídas ao usuário selecionado. Selecione a fila de usuários e clique em Revogar.
1. Clique em Salvar para concluir.

