---
title: Criação de um Guia de início rápido sem cabeçalho de configuração
description: Crie uma configuração como uma primeira etapa para começar a usar o headless no AEM 6.5.
exl-id: f1df97a1-164f-4ed4-bb63-34caf35ae27c
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 69%

---

# Criação de um Guia de início rápido sem cabeçalho de configuração {#creating-configuration}

Como primeiro passo para começar a usar o headless no AEM 6.5, é necessário criar uma configuração.

## O que é uma configuração? {#what-is-a-configuration}

O Navegador de configuração fornece uma API de configuração genérica, uma estrutura de conteúdo e um mecanismo de resolução para configurações no AEM.

No contexto do gerenciamento de conteúdo headless no AEM, considere uma configuração como um local de trabalho dentro do AEM onde é possível criar modelos de conteúdo, que definem a estrutura do conteúdo futuro e dos fragmentos de conteúdo. É possível ter várias configurações para separar esses modelos.

>[!NOTE]
>
>Se você estiver familiarizado com os [modelos de página em uma implementação de pilha completa do AEM,](/help/sites-authoring/templates.md) o uso de configurações para o gerenciamento de modelos de conteúdo é semelhante.

## Como criar uma configuração {#how-to-create-a-configuration}

Um administrador só precisaria criar uma configuração uma vez ou, muito raramente, quando um novo espaço de trabalho fosse necessário para organizar seus modelos de conteúdo. Para os propósitos deste guia de introdução, precisamos criar apenas uma configuração.

1. Faça logon em AEM e, no menu principal, selecione **Ferramentas -> Geral -> Navegador de configuração**.
1. Forneça uma **Título** para sua configuração.
   * Um nome será gerado automaticamente com base no título e ajustado de acordo com [AEM convenções de nomenclatura.](/help/sites-developing/naming-conventions.md). Ele se tornará o nome do nó no repositório.
1. Verifique as seguintes opções:
   * **Modelos de fragmentos do conteúdo**
   * **Consultas persistentes de GraphQL**

   ![Criar configuração](../assets/create-configuration.png)

1. Toque ou clique em **Criar**

É possível criar várias configurações, se necessário. As configurações também podem ser aninhadas.

>[!NOTE]
>
>Outras opções de configuração além de **Modelos de fragmento do conteúdo** e **Consultas persistentes de GraphQL** podem ser necessárias, dependendo de seus requisitos de implementação.

## Próximas etapas {#next-steps}

Usando essa configuração, agora é possível seguir para a segunda parte do guia de introdução e [criar modelos de fragmento de conteúdo.](create-content-model.md)

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
