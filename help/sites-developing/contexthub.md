---
title: ContextHub
seo-title: ContextHub
description: O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto
seo-description: O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---


# ContextHub{#contexthub}

O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto. A API Javascript do cliente permite acessar os dados para personalizar o conteúdo.

>[!NOTE]
>
>A [implementação de referência We.Retail](/help/sites-developing/we-retail.md) implementa o ContextHub e pode servir como referência à medida que você integra o ContextHub ao seu próprio projeto.

>[!CAUTION]
>
>O caminho que contém a amostra da configuração do ContextHub usada pela [implementação de referência We.Retail](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) só deve ser usado como referência para criar sua própria configuração.
>
>Ele não deve ser usado em um projeto como sua própria configuração do ContextHub.

## Persistência {#persistence}

O ContextHub armazena dados de contexto persistentes no cliente. A API Javascript do ContextHub permite acessar lojas para criar, atualizar e excluir dados, conforme necessário. Dessa forma, o ContextHub representa uma camada de dados em suas páginas.

Cada armazenamento ContextHub é uma instância de um tipo de armazenamento predefinido:

* O ContextHub fornece vários [tipos de armazenamento de amostra](/help/sites-developing/ch-samplestores.md).
* Use AEM consoles para [criar armazenamentos](ch-configuring.md#creating-a-contexthub-store).
* Os desenvolvedores podem [criar tipos de armazenamento personalizados](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Os desenvolvedores podem [acessar dados do armazenamento](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) por meio do Javascript.

## Segmentação {#segmentation}

O ContextHub inclui um mecanismo de segmentação que gerencia segmentos e determina quais segmentos são resolvidos para o contexto atual. Vários segmentos são definidos. Você pode usar a API Javascript para [determinar segmentos resolvidos](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Apresentação {#presentation}

A [barra de ferramentas do ContextHub](/help/sites-authoring/ch-previewing.md) permite que comerciantes e autores vejam e manipulem dados de armazenamento para simular a experiência do usuário ao criar páginas. A barra de ferramentas consiste em grupos de módulos de interface que fornecem acesso às lojas do ContextHub.

Cada módulo de interface do usuário do ContextHub é uma instância de um tipo de módulo predefinido:

* O ContextHub fornece vários [tipos de módulo de amostra](/help/sites-developing/ch-samplemodules.md).
* Use AEM consoles para [adicionar módulos de interface de usuário](ch-configuring.md#adding-a-ui-module) e para [agrupá-los em modos de interface de usuário](ch-configuring.md#adding-a-ui-mode).

* Os desenvolvedores podem [criar tipos de módulo personalizados](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Os desenvolvedores precisam [adicionar o componente ContextHub à página](/help/sites-developing/ch-adding.md).
