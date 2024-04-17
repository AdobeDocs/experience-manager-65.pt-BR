---
title: ContextHub
description: O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# ContextHub{#contexthub}

O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto. A API JavaScript do lado do cliente permite acessar os dados para personalizar o conteúdo.

>[!NOTE]
>
>A variável [Implementação de referência do We.Retail](/help/sites-developing/we-retail.md) O implementa o ContextHub e pode servir como referência à medida que você integra o ContextHub em seu próprio projeto.

>[!CAUTION]
>
>O caminho que contém a amostra de configuração do ContextHub usada pelo [Implementação de referência do We.Retail](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`) só deve ser usada como referência para criar sua própria configuração.
>
>Não use em um projeto como sua própria configuração do ContextHub.

## Persistência {#persistence}

O ContextHub armazena dados de contexto persistentes no cliente. A API do JavaScript do ContextHub permite acessar armazenamentos para criar, atualizar e excluir dados conforme necessário. Dessa forma, o ContextHub representa uma camada de dados em suas páginas.

Cada armazenamento do ContextHub é uma instância de um tipo de armazenamento predefinido:

* O ContextHub fornece vários [tipos de loja de amostra](/help/sites-developing/ch-samplestores.md).
* Use os consoles AEM para [criar lojas](ch-configuring.md#creating-a-contexthub-store).
* Os desenvolvedores podem [criar tipos de loja personalizados](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).
* Os desenvolvedores podem [acessar dados da loja](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) via JavaScript.

## Segmentação {#segmentation}

O ContextHub inclui um mecanismo de segmentação que gerencia segmentos e determina quais segmentos são resolvidos para o contexto atual. Vários segmentos estão definidos. Você pode usar a API do JavaScript para [determinar segmentos resolvidos](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments).

## Apresentação {#presentation}

A variável [Barra de ferramentas do ContextHub](/help/sites-authoring/ch-previewing.md) O permite que profissionais de marketing e autores vejam e manipulem dados da loja para simular a experiência do usuário ao criar páginas. A barra de ferramentas consiste em grupos de módulos de interface do usuário que fornecem acesso aos armazenamentos do ContextHub.

Cada módulo da interface do usuário do ContextHub é uma instância de um tipo de módulo predefinido:

* O ContextHub fornece vários [tipos de módulo de amostra](/help/sites-developing/ch-samplemodules.md).
* Use os consoles AEM para [adicionar módulos de interface](ch-configuring.md#adding-a-ui-module), e para [agrupá-los nos modos da interface](ch-configuring.md#adding-a-ui-mode).

* Os desenvolvedores podem [criar tipos de módulo personalizados](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

Os desenvolvedores precisam [adicionar o componente ContextHub à página](/help/sites-developing/ch-adding.md).
