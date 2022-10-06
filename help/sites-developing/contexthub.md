---
title: ContextHub
seo-title: ContextHub
description: O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto
seo-description: ContextHub is a framework for storing, manipulating, and presenting context data
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 1%

---

# ContextHub{#contexthub}

O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto. A API Javascript do lado do cliente permite acessar os dados para personalizar o conteúdo.

>[!NOTE]
>
>O [Implementação de referência We.Retail](/help/sites-developing/we-retail.md) O implementa o ContextHub e pode servir como referência à medida que você integra o ContextHub ao seu próprio projeto.

>[!CAUTION]
>
>O caminho que contém a configuração de amostra do ContextHub usada pela variável [Implementação de referência We.Retail](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) só deve ser usada como referência para criar sua própria configuração.
>
>Ela não deve ser usada em um projeto como sua própria configuração do ContextHub.

## Persistência {#persistence}

O ContextHub armazena dados de contexto persistentes no cliente. A API Javascript do ContextHub permite acessar armazenamentos para criar, atualizar e excluir dados, conforme necessário. Dessa forma, o ContextHub representa uma camada de dados nas páginas.

Cada armazenamento do ContextHub é uma instância de um tipo de armazenamento predefinido:

* O ContextHub fornece vários [tipos de armazenamento de exemplo](/help/sites-developing/ch-samplestores.md).
* Use AEM consoles para [criar lojas](ch-configuring.md#creating-a-contexthub-store).
* Os desenvolvedores podem [criar tipos de loja personalizada](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Os desenvolvedores podem [acessar dados do armazenamento](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) via Javascript.

## Segmentação {#segmentation}

O ContextHub inclui um mecanismo de segmentação que gerencia segmentos e determina quais segmentos são resolvidos para o contexto atual. Vários segmentos são definidos. Você pode usar a API do Javascript para [determinar segmentos resolvidos](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Apresentação {#presentation}

O [Barra de ferramentas do ContextHub](/help/sites-authoring/ch-previewing.md) permite que profissionais de marketing e autores vejam e manipulem dados de armazenamento para simular a experiência do usuário ao criar páginas. A barra de ferramentas consiste em grupos de módulos de interface que fornecem acesso aos armazenamentos do ContextHub.

Cada módulo do ContextHub UI é uma instância de um tipo de módulo predefinido:

* O ContextHub fornece vários [tipos de módulos de amostra](/help/sites-developing/ch-samplemodules.md).
* Use AEM consoles para [adicionar módulos de interface](ch-configuring.md#adding-a-ui-module)e para [agrupá-los em modos de interface do usuário](ch-configuring.md#adding-a-ui-mode).

* Os desenvolvedores podem [criar tipos de módulo personalizados](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Os desenvolvedores precisam [adicionar o componente ContextHub à página](/help/sites-developing/ch-adding.md).
