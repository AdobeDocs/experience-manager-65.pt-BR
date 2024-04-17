---
title: Gerenciamento de acesso a workflows
description: Saiba como configurar Listas de controle de acesso de acordo com contas de usuário para permitir (ou desativar) a inicialização e a participação em fluxos de trabalho.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: cc54d637-d66c-49d2-99ee-00d96f1a74e0
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 2%

---

# Gerenciamento de acesso a workflows{#managing-access-to-workflows}

Configure ACLs de acordo com as contas de usuário para permitir (ou desativar) a inicialização e a participação em workflows.

## Permissões de usuário necessárias para fluxos de trabalho {#required-user-permissions-for-workflows}

As ações relativas aos fluxos de trabalho podem ser realizadas se:

* você está trabalhando com o `admin` account
* a conta foi atribuída ao grupo padrão `workflow-users`:

   * esse grupo mantém todos os privilégios necessários para que seus usuários executem ações de workflow.
   * quando a conta está nesse grupo, ela só tem acesso aos workflows iniciados.

* a conta foi atribuída ao grupo padrão `workflow-administrators`:

   * esse grupo tem todos os privilégios necessários para que seus usuários privilegiados monitorem e administrem workflows.
   * quando a conta está nesse grupo, ela tem acesso a todos os workflows.

>[!NOTE]
>
>Estes são os requisitos mínimos. Sua conta também deve ser o participante atribuído ou um membro do grupo atribuído para executar etapas específicas.

## Configuração do acesso aos fluxos de trabalho {#configuring-access-to-workflows}

Os modelos de workflow herdam uma lista de controle de acesso (ACL) padrão para controlar como os usuários podem interagir com workflows. Para personalizar o acesso do usuário a um workflow, modifique a ACL (Access Control List, lista de controle de acesso) no repositório da pasta que contém o nó do modelo de workflow:

* [Aplicar uma ACL para o modelo de fluxo de trabalho específico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [Crie uma subpasta em /var/workflow/models e aplique a ACL a ela](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>Para obter informações sobre o uso do CRXDE Lite para configurar ACLs, consulte [Gerenciamento de direitos de acesso](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### Aplicar uma ACL para o modelo de fluxo de trabalho específico a /var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

Se o modelo de fluxo de trabalho for armazenado em `/var/workflow/models`, é possível atribuir uma ACL específica, relevante somente para esse fluxo de trabalho, na pasta:

1. Abra o CRXDE Lite no navegador da Web (por exemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Na árvore do nó, selecione o nó da pasta de modelos de fluxo de trabalho:

   `/var/workflow/models`

1. Clique em **Controle de acesso** guia.
1. No **Políticas do controle de acesso local** (**Lista de controle de acesso**), clique no ícone de adição para **Adicionar entrada**.
1. No **Adicionar nova entrada** adicione uma ACE com as seguintes propriedades:

   * **Principal**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilégios**: `jcr:read`
   * **representante:glob**: referência ao workflow específico

   ![wf-108](assets/wf-108.png)

   A variável **Lista de controle de acesso** A tabela agora inclui a restrição para `content-authors` no `prototype-wfm-01` modelo de fluxo de trabalho.

   ![wf-109](assets/wf-109.png)

1. Clique em **Salvar tudo**.

   A variável `prototype-wfm-01` o fluxo de trabalho não está mais disponível para os membros do `content-authors` grupo.

### Crie uma subpasta em /var/workflow/models e aplique a ACL a ela {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

Seu [a equipe de desenvolvimento pode criar os workflows em uma subpasta](/help/sites-developing/workflows-models.md#creating-a-new-workflow) de

`/var/workflow/models`

Comparável aos fluxos de trabalho do DAM armazenados em

`/var/workflow/models/dam/`

Em seguida, você pode adicionar uma ACL à própria pasta.

1. Abra o CRXDE Lite no navegador da Web (por exemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Na árvore de nós, selecione o nó da pasta individual na pasta de modelos de fluxo de trabalho; por exemplo:

   `/var/workflow/models/prototypes`

1. Clique em **Controle de acesso** guia.
1. No **Política do controle de acesso aplicável** clique no ícone de adição para **Adicionar** uma entrada.
1. No **Políticas do controle de acesso local** (**Lista de controle de acesso**), clique no ícone de adição para **Adicionar entrada**.
1. No **Adicionar nova entrada** adicione uma ACE com as seguintes propriedades:

   * **Principal**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilégios**: `jcr:read`

   >[!NOTE]
   >
   >Assim como com [Aplicar uma ACL para o modelo de fluxo de trabalho específico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) você pode incluir um rep:glob para limitar o acesso a um workflow específico.

   ![wf-110](assets/wf-110.png)

   A variável **Lista de controle de acesso** A tabela agora inclui a restrição para `content-authors` no `prototypes` pasta.

   ![wf-111](assets/wf-111.png)

1. Clique em **Salvar tudo**.

   Os modelos na `prototypes` as pastas não estão mais disponíveis para os membros da `content-authors` grupo.
