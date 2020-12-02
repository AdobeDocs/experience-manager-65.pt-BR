---
title: Gerenciamento do acesso a Workflows
seo-title: Gerenciamento do acesso a Workflows
description: Saiba como gerenciar o acesso aos Workflows.
seo-description: Saiba como gerenciar o acesso aos Workflows.
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 1%

---


# Gerenciando o acesso a Workflows{#managing-access-to-workflows}

Configure as ACLs de acordo com as contas de usuário para permitir (ou desativar) o início e a participação em workflows.

## Permissões de usuário necessárias para Workflows {#required-user-permissions-for-workflows}

As ações relativas aos workflows podem ser realizadas se:

* você está trabalhando com a conta `admin`
* a conta foi atribuída ao grupo padrão `workflow-users`:

   * esse grupo mantém todos os privilégios necessários para que seus usuários executem ações de fluxo de trabalho.
   * quando a conta está nesse grupo, ela só tem acesso aos workflows que iniciou.

* a conta foi atribuída ao grupo padrão `workflow-administrators`:

   * esse grupo possui todos os privilégios necessários para que seus usuários privilegiados monitorem e administrem workflows.
   * quando a conta está nesse grupo, ela tem acesso a todos os workflows.

>[!NOTE]
>
>Estes são os requisitos mínimos. Sua conta também deve ser o participante atribuído ou um membro do grupo atribuído para executar etapas específicas.

## Configurando o acesso a Workflows {#configuring-access-to-workflows}

Os modelos de fluxo de trabalho herdam uma ACL (controle de acesso padrão) para controlar como os usuários podem interagir com workflows. Para personalizar o acesso do usuário para um fluxo de trabalho, modifique a ACL (Lista de Controle de acesso) no repositório para a pasta que contém o nó do modelo de fluxo de trabalho:

* [Aplicar uma ACL para o modelo de fluxo de trabalho específico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [Crie uma subpasta em /var/workflow/models e aplique a ACL a essa](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>Para obter informações sobre como usar o CRXDE Lite para configurar ACLs, consulte [Gerenciamento de direitos de acesso](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### Aplicar uma ACL para o modelo de fluxo de trabalho específico a /var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

Se o modelo de fluxo de trabalho for armazenado em `/var/workflow/models`, você poderá atribuir uma ACL específica, relevante apenas para esse fluxo de trabalho, na pasta:

1. Abra o CRXDE Lite no navegador da Web (por exemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Na árvore de nós, selecione o nó da pasta de modelos de fluxo de trabalho:

   `/var/workflow/models`

1. Clique na guia **Controle de acesso**.
1. Na tabela **Políticas de Controle de acesso Local** (**Lista de Controle de acesso**), clique no ícone de mais para **Adicionar entrada**.
1. Na caixa de diálogo **Adicionar nova entrada** adicione uma nova ECA com as seguintes propriedades:

   * **Principal**:  `content-authors`
   * **Tipo**: `Deny`
   * **Privilégios**:  `jcr:read`
   * **rep:global**: referência ao fluxo de trabalho específico

   ![wf-108](assets/wf-108.png)

   A tabela **Lista do Controle de acesso** agora inclui a restrição para `content-authors` no modelo de fluxo de trabalho `prototype-wfm-01`.

   ![wf-109](assets/wf-109.png)

1. Clique em **Salvar tudo**.

   O fluxo de trabalho `prototype-wfm-01` não está mais disponível para membros do grupo `content-authors`.

### Crie uma subpasta em /var/workflow/models e aplique a ACL a essa {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

Sua equipe de desenvolvimento [pode criar os workflows em uma subpasta](/help/sites-developing/workflows-models.md#creating-a-new-workflow) de

`/var/workflow/models`

Comparável aos workflows DAM armazenados em

`/var/workflow/models/dam/`

Em seguida, é possível adicionar uma ACL à própria pasta.

1. Abra o CRXDE Lite no navegador da Web (por exemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Na árvore do nó, selecione o nó para a pasta individual na pasta de modelos de fluxo de trabalho; por exemplo:

   `/var/workflow/models/prototypes`

1. Clique na guia **Controle de acesso**.
1. Na tabela **Política de Controle de acesso aplicável**, clique no ícone de mais para **Adicionar** uma entrada.
1. Na tabela **Políticas de Controle de acesso Local** (**Lista de Controle de acesso**), clique no ícone de mais para **Adicionar entrada**.
1. Na caixa de diálogo **Adicionar nova entrada** adicione uma nova ECA com as seguintes propriedades:

   * **Principal**:  `content-authors`
   * **Tipo**: `Deny`
   * **Privilégios**:  `jcr:read`

   >[!NOTE]
   >
   >Assim como com [Aplique uma ACL para o modelo de fluxo de trabalho específico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models), você pode incluir um rep:globo para limitar o acesso a um fluxo de trabalho específico.

   ![wf-110](assets/wf-110.png)

   A tabela **Lista do Controle de acesso** agora inclui a restrição para `content-authors` na pasta `prototypes`.

   ![wf-111](assets/wf-111.png)

1. Clique em **Salvar tudo**.

   Os modelos na pasta `prototypes` não estão mais disponíveis para membros do grupo `content-authors`.

