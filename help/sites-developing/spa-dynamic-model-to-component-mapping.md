---
title: Modelo dinâmico para mapeamento de componentes para SPAs
seo-title: Modelo dinâmico para mapeamento de componentes para SPAs
description: Este artigo descreve como o modelo dinâmico para mapeamento de componentes ocorre no Javascript SPA SDK para AEM.
seo-description: Este artigo descreve como o modelo dinâmico para mapeamento de componentes ocorre no Javascript SPA SDK para AEM.
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# Modelo dinâmico para mapeamento de componentes para SPAs{#dynamic-model-to-component-mapping-for-spas}

Este documento descreve como o modelo dinâmico para mapeamento de componentes ocorre no SDK do Javascript SPA para AEM.

>[!NOTE]
>
>O Editor SPA é a solução recomendada para projetos que exigem renderização do lado do cliente baseada em estrutura SPA (por exemplo, Reagir ou Angular).

## Módulo ComponentMapping {#componentmapping-module}

O `ComponentMapping` módulo é fornecido como um pacote NPM para o projeto front-end. Ele armazena componentes de front-end e fornece uma maneira para o aplicativo de página única mapear componentes de front-end para tipos de recursos do AEM. Isso permite uma resolução dinâmica de componentes ao analisar o modelo JSON do aplicativo.

Cada item presente no modelo contém um `:type` campo que expõe um tipo de recurso AEM. Quando montado, o componente front-end pode se renderizar usando o fragmento do modelo recebido das bibliotecas subjacentes.

Consulte o documento [SPA Blueprint](/help/sites-developing/spa-blueprint.md) para obter mais informações sobre a análise do modelo e o acesso do componente front-end ao modelo.

Consulte também o pacote npm: [https://www.npmjs.com/package/@adobe/cq-spa-component-mapping](https://www.npmjs.com/package/@adobe/cq-spa-component-mapping)

## Aplicativo de página única orientado por modelo {#model-driven-single-page-application}

Aplicativos de página única que usam o Javascript SPA SDK para AEM são orientados por modelo:

1. Os componentes front-end se registram na [Component Mapping Store](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. Em seguida, o [Contêiner](/help/sites-developing/spa-blueprint.md#container), uma vez fornecido com um modelo pelo Provedor [de](/help/sites-developing/spa-blueprint.md#the-model-provider)modelos, repete sobre seu conteúdo de modelo ( `:items`).

1. No caso de uma página, seus filhos ( `:children`) primeiro obtêm uma classe de componente do Mapeamento [de](/help/sites-developing/spa-blueprint.md#componentmapping) componentes e depois a instanciam.

## Inicialização do aplicativo {#app-initialization}

Cada componente é estendido com os recursos do [`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). Por conseguinte, a inicialização assume a seguinte forma geral:

1. Cada provedor de modelo se inicializa e escuta as alterações feitas no modelo que corresponde ao seu componente interno.
1. O [ deve ser inicializado como representado pelo fluxo `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) de [](/help/sites-developing/spa-blueprint.md)inicialização.

1. Depois de armazenado, o gerenciador de modelo de página retorna o modelo completo do aplicativo.
1. Esse modelo é então passado para o componente front-end root [Container](/help/sites-developing/spa-blueprint.md#container) do aplicativo.
1. Partes do modelo são finalmente propagadas para cada componente filho individual.

![app_model_initialization](assets/app_model_initialization.png)

