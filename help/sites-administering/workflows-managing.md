---
title: Gerenciamento de acesso a workflows
seo-title: Managing Access to Workflows
description: Saiba como gerenciar o acesso aos Workflows.
seo-description: Learn how to manage access to Workflows.
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
exl-id: cc54d637-d66c-49d2-99ee-00d96f1a74e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 3%

---

# Gerenciamento de acesso a workflows{#managing-access-to-workflows}

Configure as ACLs de acordo com as contas de usuário para permitir (ou desativar) o início e a participação em workflows.

## Permissões de usuário necessárias para fluxos de trabalho {#required-user-permissions-for-workflows}

As ações relativas aos fluxos de trabalho podem ser realizadas se:

* você está trabalhando com o `admin` account
* a conta foi atribuída ao grupo padrão `workflow-users`:

   * esse grupo mantém todos os privilégios necessários para que seus usuários executem ações de workflow.
   * quando a conta está nesse grupo, ela só tem acesso aos workflows que iniciou.

* a conta foi atribuída ao grupo padrão `workflow-administrators`:

   * esse grupo mantém todos os privilégios necessários para que seus usuários privilegiados monitorem e administrem workflows.
   * quando a conta está nesse grupo, ela tem acesso a todos os workflows.

>[!NOTE]
>
>Estes são os requisitos mínimos. Sua conta também deve ser o participante atribuído ou um membro do grupo atribuído para tomar etapas específicas.

## Configuração do acesso aos fluxos de trabalho {#configuring-access-to-workflows}

Os modelos de workflow herdam uma ACL (lista de controle de acesso) padrão para controlar como os usuários podem interagir com workflows. Para personalizar o acesso do usuário para um workflow, modifique a Lista de Controle de Acesso (ACL) no repositório para a pasta que contém o nó do modelo de workflow:

* [Aplique uma ACL para o modelo de fluxo de trabalho específico para /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [Crie uma subpasta em /var/workflow/models e aplique a ACL a ela](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>Para obter informações sobre como usar o CRXDE Lite para configurar ACLs, consulte [Gerenciamento de direitos de acesso](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### Aplique uma ACL para o modelo de fluxo de trabalho específico para /var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

Se o modelo de fluxo de trabalho for armazenado em `/var/workflow/models` em seguida, é possível atribuir uma ACL específica, relevante somente para esse workflow, na pasta :

1. Abra o CRXDE Lite no navegador da Web (por exemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Na árvore de nós, selecione o nó da pasta de modelos de fluxo de trabalho:

   `/var/workflow/models`

1. Clique no botão **Controle de acesso** guia .
1. No **Políticas de Controle de Acesso Local** (**Lista de Controle de Acesso**), clique no ícone de adição para **Adicionar entrada**.
1. No **Adicionar nova entrada** adicione uma nova ACE com as seguintes propriedades:

   * **Principal**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilégios**: `jcr:read`
   * **rep:glob**: referência ao fluxo de trabalho específico

   ![wf-108](assets/wf-108.png)

   O **Lista de Controle de Acesso** agora inclui a restrição para `content-authors` no `prototype-wfm-01` modelo de fluxo de trabalho.

   ![wf-109](assets/wf-109.png)

1. Clique em **Salvar tudo**.

   O `prototype-wfm-01` O fluxo de trabalho não está mais disponível para os membros do `content-authors` grupo.

### Crie uma subpasta em /var/workflow/models e aplique a ACL a ela {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

Seu [a equipe de desenvolvimento pode criar os workflows em uma subpasta](/help/sites-developing/workflows-models.md#creating-a-new-workflow) de

`/var/workflow/models`

Comparável aos workflows do DAM armazenados em

`/var/workflow/models/dam/`

Em seguida, você pode adicionar uma ACL à própria pasta.

1. Abra o CRXDE Lite no navegador da Web (por exemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Na árvore de nós, selecione o nó da pasta individual na pasta de modelos de fluxo de trabalho; por exemplo:

   `/var/workflow/models/prototypes`

1. Clique no botão **Controle de acesso** guia .
1. No **Política de Controle de Acesso Aplicável** clique no ícone de adição para **Adicionar** uma entrada.
1. No **Políticas de Controle de Acesso Local** (**Lista de Controle de Acesso**), clique no ícone de adição para **Adicionar entrada**.
1. No **Adicionar nova entrada** adicione uma nova ACE com as seguintes propriedades:

   * **Principal**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilégios**: `jcr:read`

   >[!NOTE]
   >
   >Como com [Aplique uma ACL para o modelo de fluxo de trabalho específico para /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) é possível incluir um rep:glob para limitar o acesso a um workflow específico.

   ![wf-110](assets/wf-110.png)

   O **Lista de Controle de Acesso** agora inclui a restrição para `content-authors` no `prototypes` pasta.

   ![wf-111](assets/wf-111.png)

1. Clique em **Salvar tudo**.

   Os modelos na `prototypes` não estão mais disponíveis para membros do `content-authors` grupo.
