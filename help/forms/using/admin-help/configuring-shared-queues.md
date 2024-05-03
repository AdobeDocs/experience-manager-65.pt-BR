---
title: Configurando Filas Compartilhadas
description: As Filas compartilhadas permitem configurar e gerenciar as filas de usuários com eficiência. Saiba como configurar filas compartilhadas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# Configurando Filas Compartilhadas{#configuring-shared-queues}

As Filas compartilhadas permitem configurar e gerenciar as filas de usuários com eficiência. Uma fila de usuários é simplesmente todas as tarefas atribuídas a um usuário, consulte [Listas de Tarefas Pendentes](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) para obter mais informações. É possível atribuir, cancelar atribuições e reatribuir filas de usuários dependendo das necessidades organizacionais. Você pode gerenciar Filas compartilhadas de duas maneiras:

**Gerenciar Acesso A Um Usuário**

Você pode gerenciar o acesso a uma fila de usuários selecionada usando essa opção.

**Gerenciar Acesso Por Um Usuário**

É possível gerenciar filas compartilhadas atribuídas a um usuário selecionado usando essa opção.

## Gerenciar o acesso a uma fila de usuários selecionada {#managing-access-to-a-selected-user-queue}

A funcionalidade Gerenciar acesso a um usuário permite gerenciar o acesso a uma fila de usuários selecionada. Você pode conceder ou revogar o acesso a uma fila de usuários selecionada para outros usuários em sua organização. Por exemplo, Kara Bowman está fora do cargo. Usando a funcionalidade Gerenciar acesso a um usuário, a fila do Kara pode ser compartilhada com Akira Tanaka e John Jacobs para conclusão. Em um ponto posterior, quando Kara retorna ao escritório, você pode revogar o acesso a sua fila de Akira Tanaka e John Jacobs.

Depois de compartilhadas, essas tarefas podem ser concluídas pelo usuário, com acesso à fila, usando o Espaço de trabalho.

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão do AEM forms.

### Configurar o acesso a uma fila de usuários selecionada {#configuring-access-to-a-selected-user-queue}

1. Faça logon no console de administração usando uma conta de Administrador.
1. Selecionar **Serviços** > **Forms Workflow** > **Fila compartilhada**.

1. Na guia Gerenciar acesso a um usuário, localize e selecione o usuário cuja fila você deseja compartilhar. A qualquer momento, o painel inferior direito exibe a lista de usuários com acesso à fila de usuários selecionada.
1. No painel inferior esquerdo, localize e selecione o usuário. Clique em Compartilhar.
1. Clique em Salvar para concluir.

### Revogação do acesso a uma fila de usuários selecionada {#revoking-access-to-a-selected-user-queue}

1. Faça logon no console de administração usando uma conta de Administrador.
1. Selecionar **Serviços** > **Forms Workflow** > **Fila compartilhada**.

1. Na guia Gerenciar acesso a um usuário, localize e selecione o usuário cuja fila você deseja gerenciar.
1. O painel inferior direito exibe a lista de usuários com acesso à fila de usuários selecionada. Selecione o usuário e clique em Revogar.
1. Clique em Salvar para concluir.

## Gerenciamento de filas atribuídas a um usuário {#managing-queues-assigned-to-a-user}

A funcionalidade Gerenciar acesso por um usuário permite gerenciar filas atribuídas a um usuário selecionado. Você pode conceder ou revogar acesso às filas de usuários para um usuário selecionado individualmente. Por exemplo, você deseja atribuir as filas de usuário Akira Tanaka e John Jacobs a Kara Bowman. Usando a funcionalidade Gerenciar acesso por um usuário, você pode pesquisar por Kara Bowman e conceder acesso às tarefas atribuídas a Akira Tanaka e John Jacobs. Em um ponto posterior, você pode revogar o acesso de Kara Bowman a essas filas de usuários.

Depois de atribuídas, essas tarefas podem ser concluídas pelo usuário usando o Espaço de trabalho.

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão do AEM forms.

### Concedendo acesso a uma fila de usuários selecionada {#granting-access-to-a-selected-user-queue}

1. Faça logon no console de administração usando uma conta de Administrador.
1. Selecionar **Serviços** > **Forms Workflow** > **Fila compartilhada**.

1. Na guia Gerenciar acesso a um usuário, localize e selecione o usuário cuja fila você deseja compartilhar. A qualquer momento, o painel inferior direito exibe a lista de usuários com acesso à fila de usuários selecionada.
1. No painel inferior esquerdo, localize e selecione as filas de usuários que deseja compartilhar com o usuário selecionado. Clique em Compartilhar.
1. Clique em Salvar para concluir.

### Revogação do acesso a uma fila de usuários selecionada {#revoking_access_to_a_selected_user_queue-1}

1. Faça logon no console de administração usando uma conta de Administrador.
1. Selecionar **Serviços** > **Forms Workflow** > **Fila compartilhada**.

1. Na guia Gerenciar acesso por um usuário, localize e selecione o usuário cuja fila você deseja gerenciar.
1. O painel inferior direito exibe a lista de filas de usuários atribuídas ao usuário selecionado. Selecione a fila de usuários e clique em Revogar.
1. Clique em Salvar para concluir.
