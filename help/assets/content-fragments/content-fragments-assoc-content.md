---
title: Conteúdo associado
description: Entenda como o recurso de conteúdo associado do AEM fornece a conexão para que os ativos possam ser usados opcionalmente com o fragmento quando ele for adicionado a uma página de conteúdo, adicionando flexibilidade adicional à entrega de conteúdo headless.
feature: Content Fragments
role: User
exl-id: 8b93fd6e-47d1-46fd-901b-621caa25be7b
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: a45b1e7f-e65f-4cd3-be86-5cec5d9449ef
    internal-label: Content management
subfeature_v2:
  - id: b7f5d1e0-aa2f-4a55-83f4-c2b35a8bd3a7
    internal-label: Content fragments
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 49%
---
# Conteúdo associado{#associated-content}

O recurso de conteúdo associado do AEM fornece a conexão para que os ativos possam (opcionalmente) ser usados com o fragmento quando ele for adicionado a uma página de conteúdo. Isso proporciona flexibilidade para a entrega de conteúdo headless [fornecendo um intervalo de ativos para acessar ao usar o fragmento de conteúdo em uma página](/help/sites-authoring/content-fragments.md#using-associated-content), além de ajudar a reduzir o tempo necessário para pesquisar o ativo apropriado. Qualquer conteúdo associado pode ser configurado usando o editor de Fragmento de conteúdo.

## Adicionar conteúdo associado {#adding-associated-content}

>[!NOTE]
>
>Existem vários métodos de adicionar [ativos visuais (por exemplo, imagens)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) ao fragmento e/ou página.

Para fazer a associação, primeiro você precisa [adicionar seus ativos de mídia a uma coleção](/help/assets/manage-collections.md). Depois disso, você pode:

1. Abrir o fragmento e selecionar **Conteúdo associado** no painel lateral.

   ![Conteúdo associado](assets/cfm-assoc-content-01.png)

1. Dependendo de alguma coleção já ter sido associada ou não, selecione:

   * **Associar conteúdo** — esta será a primeira coleção associada
   * **Associar Coleção** - coleções associadas que já estão configuradas

1. Selecione a coleção necessária.

   Opcionalmente, é possível adicionar o próprio fragmento à coleção selecionada; isso auxilia no rastreamento.

   ![Selecionar coleção](assets/cfm-assoc-content-02.png)

1. Confirmar (com **Selecionar**). A coleção será listada como associada.

   ![cfm-6420-05](assets/cfm-assoc-content-03.png)

## Editar conteúdo associado {#editing-associated-content}

Depois de associar uma coleção, você pode:

* **Remover** a associação.
* **Adicionar ativos** à coleção.
* Selecionar um ativo para realizar mais ações.
* Editar o ativo.
