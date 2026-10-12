---
title: Criação de modelos de fragmento de conteúdo - Guia de início rápido do Headless
description: Defina a estrutura do conteúdo que você cria e veicula usando os recursos headless do Adobe Experience Manager (AEM), por meio dos modelos de fragmento de conteúdo.
exl-id: 653e35c9-7b6a-49ae-b55d-af2ec40e257d
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 51%
---
# Criação de modelos de fragmento de conteúdo - Guia de início rápido do Headless {#creating-content-fragment-models}

Defina a estrutura do conteúdo que você cria e veicula usando os recursos headless do Adobe Experience Manager (AEM), por meio dos modelos de fragmento de conteúdo.

## O que são modelos de fragmento de conteúdo? {#what-are-content-fragment-models}

[Agora que você criou uma configuração,](create-configuration.md) é possível usá-la para criar modelos de fragmento de conteúdo.

Os Modelos de fragmento de conteúdo definem a estrutura dos dados e do conteúdo que você irá criar e gerenciar no AEM. Eles servem como uma espécie de andaime para o conteúdo. Ao optar por criar o conteúdo, os autores escolherão entre os Modelos de fragmento de conteúdo definidos, que os orientarão na criação do conteúdo.

## Como criar um modelo de fragmento de conteúdo {#how-to-create-a-content-fragment-model}

Um arquiteto de informações executaria essas tarefas apenas esporadicamente, à medida que novos modelos se tornassem necessários. Para os propósitos deste guia de introdução, você está criando apenas um modelo.

1. Faça logon no AEM e, no menu principal, selecione **Ferramentas > Assets > Modelos de fragmento de conteúdo**.
1. Clique na pasta que foi criada com sua configuração.

   ![A pasta de modelos](assets/models-folder.png)
1. Clique em **Criar**.
1. Forneça um **Título do Modelo**, **Marcas** e **Descrição**. Também é possível marcar/desmarcar a opção **Ativar modelo** para controlar se o modelo é habilitado imediatamente após a criação.

   ![Criar um modelo](assets/models-create.png)
1. Na janela de confirmação, clique em **Abrir** para configurar seu modelo.

   ![Janela de confirmação](assets/models-confirmation.png)
1. Usando o **Editor de modelos de fragmentos de conteúdo**, crie o modelo de fragmento de conteúdo arrastando e soltando campos da coluna **Tipos de dados**.

   ![Arrastar e soltar campos](assets/models-drag-and-drop.png)

1. Depois de colocar um campo, você deve configurar suas propriedades. O editor alterna automaticamente para a guia **Propriedades** do campo adicionado, onde é possível fornecer os campos obrigatórios.

   ![Configurar propriedades](assets/models-configure-properties.png)
1. Quando terminar de criar o modelo, clique em **Salvar**.

1. O modo do modelo recém-criado depende da opção **Habilitar modelo** ter sido selecionada ao criar o modelo:
   * selecionado - o novo modelo já está **Habilitado**
   * não selecionada - o novo modelo será criado em modo de **Rascunho**

1. Se ainda não estiver, o modelo deve ser **habilitado** para ser usado.
   1. Selecione o modelo criado e clique em **Habilitar**.

      ![Habilitação do modelo](assets/models-enable.png)
   1. Confirme a habilitação do modelo tocando ou clicando em **Habilitar** na caixa de diálogo de confirmação.

      ![Caixa de diálogo de confirmação de habilitação](assets/models-enabling.png)
1. O modelo agora está habilitado e pronto para uso.

   ![Modelo habilitado](assets/models-enabled.png)

O **Editor de Modelos de Fragmentos de Conteúdo** oferece suporte a vários tipos de dados diferentes, como campos de texto simples, referências de ativos, referências a outros modelos e dados JSON.

É possível criar vários modelos. Os modelos podem fazer referência a outros fragmentos de conteúdo. Use as [configurações](create-configuration.md) para organizar seus modelos.

## Próximas etapas {#next-steps}

Agora que você definiu as estruturas dos fragmentos de conteúdo criando modelos, poderá seguir para a terceira parte do guia de introdução e [criar pastas onde os fragmentos serão armazenados.](create-assets-folder.md)

>[!TIP]
>
>Para obter detalhes completos sobre os modelos de fragmento de conteúdo, consulte [documentação dos Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md)
