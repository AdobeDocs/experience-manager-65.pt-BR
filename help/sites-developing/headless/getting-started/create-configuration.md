---
title: Criação de um Guia de início rápido sem cabeçalho de configuração
description: Crie uma configuração como uma primeira etapa para começar a usar o headless no AEM 6.5.
exl-id: 48801599-f279-4e55-8033-9c418d2af5bb
source-git-commit: 8ab774b8d21dd16e4873cd39ef0175ead3f2da23
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 3%

---

# Criação de um Guia de início rápido sem cabeçalho de configuração {#creating-configuration}

Como primeiro passo para começar a usar o headless no AEM 6.5, é necessário criar uma configuração.

## O que é uma configuração? {#what-is-a-configuration}

O Navegador de configuração fornece uma API de configuração genérica, estrutura de conteúdo, mecanismo de resolução para configurações no AEM.

No contexto do gerenciamento de conteúdo sem periféricos no AEM, considere uma configuração como um local de trabalho no AEM onde você pode criar os Modelos de conteúdo, que definem a estrutura do conteúdo futuro e os Fragmentos de conteúdo. É possível ter várias configurações para separar esses modelos.

>[!NOTE]
>
>Se você estiver familiarizado com [modelos de página em uma implementação de AEM de pilha completa,](/help/sites-authoring/templates.md) o uso de configurações para o gerenciamento de Modelos de conteúdo é semelhante.

## Como criar uma configuração {#how-to-create-a-configuration}

Um administrador só precisaria criar uma configuração uma vez ou muito automaticamente quando um novo espaço de trabalho for necessário para organizar seus Modelos de conteúdo. Para o objetivo deste guia de introdução, precisamos apenas criar uma configuração.

1. Faça logon em AEM e, no menu principal, selecione **Ferramentas -> Geral -> Navegador de configuração**.
1. Forneça uma **Título** para sua configuração.
   * Um nome será gerado automaticamente com base no título e ajustado de acordo com [AEM convenções de nomenclatura.](/help/sites-developing/naming-conventions.md). Ele se tornará o nome do nó no repositório.
1. Verifique as seguintes opções:
   * **Modelos de fragmentos do conteúdo**
   * **Consultas Persistentes GraphQL**

   ![Criar configuração](../assets/create-configuration.png)

1. Toque ou clique em **Criar**

É possível criar várias configurações, se necessário. As configurações também podem ser aninhadas.

>[!NOTE]
>
>Opções de configuração além de **Modelos de fragmentos do conteúdo** e **Consultas Persistentes GraphQL** pode ser necessário, dependendo de seus requisitos de implementação.

## Próximas etapas {#next-steps}

Usando essa configuração, agora você pode seguir para a segunda parte do guia de introdução e [criar Modelos de fragmentos do conteúdo.](create-content-model.md)

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
