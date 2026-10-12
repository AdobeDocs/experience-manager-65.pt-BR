---
title: Criação de fragmentos de conteúdo do Guia de início rápido do Headless
description: Saiba como usar fragmentos de conteúdo do AEM para projetar, criar, preparar e usar conteúdo independente de página para entrega headless.
exl-id: 5787204d-bcce-447e-b98c-2bc1c0d744c3
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
source-wordcount: '378'
ht-degree: 73%
---
# Criação de fragmentos de conteúdo do Guia de início rápido do Headless {#creating-content-fragments}

Saiba como usar fragmentos de conteúdo do AEM para projetar, criar, preparar e usar conteúdo independente de página para entrega headless.

## O que são fragmentos de conteúdo? {#what-are-content-fragments}

[Agora que você criou uma pasta de ativos](create-assets-folder.md) onde você pode armazenar os fragmentos de conteúdo, é possível criar os fragmentos.

Os fragmentos de conteúdo permitem projetar, criar, preparar e publicar conteúdo independente de página. Eles permitem preparar conteúdo pronto para uso em vários locais e em vários canais.

Fragmentos de conteúdo contêm conteúdo estruturado e podem ser entregues no formato JSON.

## Como criar um fragmento de conteúdo {#how-to-create-a-content-fragment}

Os autores de conteúdo criarão qualquer quantidade de fragmentos de conteúdo para representar o conteúdo que eles criam. Esta será a principal tarefa deles no AEM. Para os propósitos deste guia de introdução, só será necessário criar um.

1. Faça logon no AEM e, no menu principal, selecione **Navegação > Assets**.
1. Navegue até a [pasta criada anteriormente.](create-assets-folder.md)
1. Clique em **Criar > Fragmento de conteúdo**.
1. A criação de um fragmento de conteúdo é apresentada como um assistente de duas etapas. Primeiro, selecione qual modelo deseja usar para criar o fragmento de conteúdo e clique em **Próximo**.
   * Os modelos disponíveis dependem da [**Configuração na nuvem** que foi definida para a pasta de ativos](create-assets-folder.md) na qual você está criando o fragmento de conteúdo.
   * Se você receber a mensagem `We could not find any models`, verifique a configuração da pasta de ativos.

   ![Selecionar modelo de fragmento de conteúdo](assets/content-fragment-model-select.png)
1. Forneça o **Título**, **Descrição** e **Marcas** conforme necessário e clique em **Criar**.

   ![Criar fragmento de conteúdo](assets/content-fragment-create.png)
1. Clique em **Abrir** na janela de confirmação.

   ![Confirmação da criação do fragmento de conteúdo](assets/content-fragment-confirmation.png)
1. Forneça os detalhes do fragmento de conteúdo no Editor de fragmento de conteúdo.

   ![Editor de fragmento de conteúdo](assets/content-fragment-edit.png)
1. Clique em **Salvar** ou **Salvar e fechar**.

Os fragmentos de conteúdo podem fazer referência a outros fragmentos de conteúdo, permitindo uma estrutura de conteúdo aninhada, se necessário.

Fragmentos de conteúdo também podem fazer referência a outros ativos no AEM. [Esses ativos precisam estar armazenados no AEM](/help/assets/manage-assets.md) antes da criação de um fragmento de conteúdo de referência.

## Próximas etapas {#next-steps}

Agora que você criou um fragmento de conteúdo, poderá seguir para a parte final do guia de introdução e [criar solicitações de API para acessar e entregar fragmentos de conteúdo.](create-api-request.md)

>[!TIP]
>
>Para obter detalhes completos sobre o gerenciamento de fragmentos de conteúdo, consulte a [documentação dos Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
