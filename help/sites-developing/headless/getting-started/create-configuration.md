---
title: Criação de um guia de início rápido do headless de configuração
description: Crie uma configuração como uma primeira etapa para começar a usar o headless no AEM 6.5.
exl-id: f1df97a1-164f-4ed4-bb63-34caf35ae27c
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
source-wordcount: '296'
ht-degree: 66%
---
# Criação de um guia de início rápido do headless de configuração {#creating-configuration}

Como primeira etapa para começar a usar o headless no AEM 6.5, é necessário criar uma configuração.

## O que é uma configuração? {#what-is-a-configuration}

O Navegador de configuração fornece uma API de configuração genérica, uma estrutura de conteúdo e um mecanismo de resolução para configurações no AEM.

No contexto do gerenciamento de conteúdo headless no AEM, considere uma configuração como um local de trabalho dentro do AEM onde é possível criar modelos de conteúdo, que definem a estrutura do conteúdo futuro e dos fragmentos de conteúdo. É possível ter várias configurações para separar esses modelos.

>[!NOTE]
>
>Se você estiver familiarizado com os [modelos de página em uma implementação de pilha completa do AEM,](/help/sites-authoring/templates.md) o uso de configurações para o gerenciamento de modelos de conteúdo é semelhante.

## Como criar uma configuração {#how-to-create-a-configuration}

Um administrador só precisaria criar uma configuração uma vez ou, muito raramente, quando um novo espaço de trabalho fosse necessário para organizar seus modelos de conteúdo. Para os propósitos deste guia de introdução, precisamos criar apenas uma configuração.

1. Faça logon no AEM e, no menu principal, selecione **Ferramentas > Geral > Navegador de configuração**.
1. Forneça um **Título** para sua configuração.
   * Um nome será gerado automaticamente com base no título e ajustado de acordo com as [convenções de nomenclatura do AEM.](/help/sites-developing/naming-conventions.md). Ele se tornará o nome do nó no repositório.
1. Verifique as seguintes opções:
   * **Modelos de fragmentos de conteúdo**
   * **Consultas persistentes de GraphQL**

   ![Criar configuração](assets/create-configuration.png)

1. Clique em **Criar**

Você pode criar várias configurações, se necessário. As configurações também podem ser aninhadas.

>[!NOTE]
>
>Outras opções de configuração além de **Modelos de fragmento de conteúdo** e **Consultas persistentes de GraphQL** podem ser necessárias, dependendo de seus requisitos de implementação.

## Próximas etapas {#next-steps}

Usando essa configuração, agora é possível seguir para a segunda parte do guia de introdução e [criar modelos de fragmento de conteúdo.](create-content-model.md)

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
