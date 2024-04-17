---
title: Modelo dinâmico para mapeamento de componentes para SPA
description: Saiba como o modelo dinâmico para mapeamento de componentes ocorre no SDK SPA JavaScript para Adobe Experience Manager.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Modelo dinâmico para mapeamento de componentes para SPA{#dynamic-model-to-component-mapping-for-spas}

Este documento descreve como o modelo dinâmico para mapeamento de componentes ocorre no SDK SPA JavaScript para Adobe Experience Manager (AEM).

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização no lado do cliente baseada na estrutura SPA (por exemplo, React ou Angular).

## Módulo ComponentMapping {#componentmapping-module}

A variável `ComponentMapping` O módulo é fornecido como um pacote NPM para o projeto de front-end. Ele armazena componentes de front-end e fornece uma maneira para o Aplicativo de página única mapear componentes de front-end para tipos de recursos de AEM. Isso permite uma resolução dinâmica de componentes ao analisar o modelo JSON do aplicativo.

Cada item presente no modelo contém um `:type` campo que expõe um tipo de recurso AEM. Quando montado, o componente de front-end pode ser renderizado usando o fragmento de modelo que recebeu das bibliotecas subjacentes.

Consulte [Blueprint SPA](/help/sites-developing/spa-blueprint.md) para obter mais informações sobre a análise de modelos e o acesso do componente front-end ao modelo.

Consulte também o pacote npm: [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicativo de página única orientado por modelo {#model-driven-single-page-application}

Aplicativos de página única que usam o SDK do SPA do JavaScript para AEM são orientados por modelo:

1. Os componentes de front-end se registram no [Loja de mapeamento de componentes](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. Em seguida, o [Container](/help/sites-developing/spa-blueprint.md#container), uma vez fornecido um modelo pelo [Provedor de modelo](/help/sites-developing/spa-blueprint.md#the-model-provider), repete o conteúdo do seu modelo ( `:items`).

1. Se houver uma página, suas páginas secundárias ( `:children`) primeiro obtenha uma classe de componente do [Mapeamento de componentes](/help/sites-developing/spa-blueprint.md#componentmapping) e, em seguida, instanciá-lo.

## Inicialização do aplicativo {#app-initialization}

Cada componente é estendido com os recursos do [`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). A inicialização assume a seguinte forma geral:

1. Cada provedor de modelo se inicializa e escuta as alterações feitas na parte do modelo que corresponde ao componente interno.
1. A variável [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) deve ser inicializado conforme representado pela variável [fluxo de inicialização](/help/sites-developing/spa-blueprint.md).

1. Depois de armazenado, o gerenciador de modelo de página retorna o modelo completo do aplicativo.
1. Esse modelo é então passado para a raiz do front-end [Container](/help/sites-developing/spa-blueprint.md#container) componente do aplicativo.
1. Partes do modelo são finalmente propagadas para cada componente filho individual.

![app_model_initialization](assets/app_model_initialization.png)
