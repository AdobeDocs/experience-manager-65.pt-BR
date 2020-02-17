---
title: Gerenciamento do acesso aos fluxos de trabalho
seo-title: Gerenciamento do acesso aos fluxos de trabalho
description: Saiba como gerenciar o acesso aos fluxos de trabalho.
seo-description: Saiba como gerenciar o acesso aos fluxos de trabalho.
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Gerenciamento do acesso aos fluxos de trabalho{#managing-access-to-workflows}

Configure as ACLs de acordo com as contas de usuário para permitir (ou desativar) o início e a participação em fluxos de trabalho.

## Permissões de usuário necessárias para fluxos de trabalho {#required-user-permissions-for-workflows}

Podem ser empreendidas ações em matéria de fluxos de trabalho se:

* você está trabalhando com a `admin` conta
* a conta foi atribuída ao grupo padrão `workflow-users`:

   * esse grupo mantém todos os privilégios necessários para que seus usuários executem ações de fluxo de trabalho.
   * quando a conta está nesse grupo, ela só tem acesso aos fluxos de trabalho que iniciou.

* a conta foi atribuída ao grupo padrão `workflow-administrators`:

   * esse grupo possui todos os privilégios necessários para que seus usuários privilegiados monitorem e administrem fluxos de trabalho.
   * quando a conta está nesse grupo, ela tem acesso a todos os fluxos de trabalho.

>[!NOTE]
>
>Estes são os requisitos mínimos. Sua conta também deve ser o participante atribuído ou um membro do grupo atribuído para executar etapas específicas.

## Configuração do acesso aos fluxos de trabalho {#configuring-access-to-workflows}

Os modelos de fluxo de trabalho herdam uma ACL (lista de controle de acesso) padrão para controlar como os usuários podem interagir com fluxos de trabalho. Para personalizar o acesso do usuário para um fluxo de trabalho, modifique a ACL (Access Control List, lista de controle de acesso) no repositório da pasta que contém o nó do modelo de fluxo de trabalho:

* [Aplicar uma ACL para o modelo de fluxo de trabalho específico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [Crie uma subpasta em /var/workflow/models e aplique a ACL a essa](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>Para obter informações sobre como usar o CRXDE Lite para configurar ACLs, consulte Gerenciamento [de direitos de](/help/sites-administering/user-group-ac-admin.md#access-right-management)acesso.

### Aplicar uma ACL para o modelo de fluxo de trabalho específico a /var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

Se o modelo de fluxo de trabalho estiver armazenado dentro `/var/workflow/models` , você poderá atribuir uma ACL específica, relevante somente para esse fluxo de trabalho, na pasta:

1. Abra o CRXDE Lite no navegador da Web (por exemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Na árvore de nós, selecione o nó da pasta de modelos de fluxo de trabalho:

   `/var/workflow/models`

1. Clique na guia Controle **de** acesso.
1. Na tabela Políticas **de controle de acesso** local (Lista **de controle de** acesso), clique no ícone de adição para **Adicionar entrada**.
1. Na caixa de diálogo **Adicionar nova entrada** , adicione um novo ACE com as seguintes propriedades:

   * **Principal**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilégios**: `jcr:read`
   * **rep:global**: referência ao fluxo de trabalho específico
   ![wf-108](assets/wf-108.png)

   A tabela Lista **de controle de** acesso agora inclui a restrição para `content-authors` no modelo de `prototype-wfm-01` fluxo de trabalho.

   ![wf-109](assets/wf-109.png)

1. Clique em **Salvar tudo**.

   O `prototype-wfm-01` fluxo de trabalho não está mais disponível para os membros do `content-authors` grupo.

### Crie uma subpasta em /var/workflow/models e aplique a ACL a essa {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

Sua equipe [de desenvolvimento pode criar os fluxos de trabalho em uma subpasta](/help/sites-developing/workflows-models.md#creating-a-new-workflow) de

`/var/workflow/models`

Comparável aos fluxos de trabalho DAM armazenados em

`/var/workflow/models/dam/`

Em seguida, é possível adicionar uma ACL à própria pasta.

1. Abra o CRXDE Lite no navegador da Web (por exemplo, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Na árvore do nó, selecione o nó da pasta individual na pasta de modelos de fluxo de trabalho; por exemplo:

   `/var/workflow/models/prototypes`

1. Clique na guia Controle **de** acesso.
1. Na tabela Política **de controle de acesso** aplicável, clique no ícone de adição para **Adicionar** uma entrada.
1. Na tabela Políticas **de controle de acesso** local (Lista **de controle de** acesso), clique no ícone de adição para **Adicionar entrada**.
1. Na caixa de diálogo **Adicionar nova entrada** , adicione um novo ACE com as seguintes propriedades:

   * **Principal**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilégios**: `jcr:read`
   >[!NOTE]
   >
   >Assim como em [Aplicar uma ACL para o modelo de fluxo de trabalho específico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) , você pode incluir uma rep:globo para limitar o acesso a um fluxo de trabalho específico.

   ![wf-110](assets/wf-110.png)

   A tabela Lista **de controle de** acesso agora inclui a restrição para `content-authors` na `prototypes` pasta.

   ![wf-111](assets/wf-111.png)

1. Clique em **Salvar tudo**.

   Os modelos na `prototypes` pasta não estão mais disponíveis para os membros do `content-authors` grupo.

