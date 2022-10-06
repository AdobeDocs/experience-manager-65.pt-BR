---
title: Modelo dinâmico para mapeamento de componentes para SPA
seo-title: Dynamic Model to Component Mapping for SPAs
description: Este artigo descreve como o modelo dinâmico para mapeamento de componentes ocorre no Javascript SPA SDK for AEM.
seo-description: This article describes how the dynamic model to component mapping occurs in the Javascript SPA SDK for AEM.
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Modelo dinâmico para mapeamento de componentes para SPA{#dynamic-model-to-component-mapping-for-spas}

Este documento descreve como o modelo dinâmico para mapeamento de componentes ocorre no Javascript SPA SDK for AEM.

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização do lado do cliente baseada em SPA estrutura (por exemplo, Reagir ou Angular).

## Módulo ComponentMapping {#componentmapping-module}

O `ComponentMapping` é fornecido como um pacote NPM para o projeto front-end. Ele armazena componentes de front-end e fornece uma maneira de o Aplicativo de página única mapear componentes de front-end para AEM tipos de recursos. Isso permite uma resolução dinâmica de componentes ao analisar o modelo JSON do aplicativo.

Cada item presente no modelo contém um `:type` que expõe um tipo de recurso AEM. Quando montado, o componente de front-end pode se renderizar usando o fragmento de modelo recebido das bibliotecas subjacentes.

Consulte a [SPA Blueprint](/help/sites-developing/spa-blueprint.md) documento para obter mais informações sobre a análise do modelo e o acesso do componente de front-end ao modelo.

Consulte também o pacote npm: [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicativo de página única orientado por modelo {#model-driven-single-page-application}

Aplicativos de página única que usam o Javascript SPA SDK para AEM são orientados por modelo:

1. Os componentes de front-end se registram no [Armazenamento de mapeamento de componentes](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. Em seguida, [Contêiner](/help/sites-developing/spa-blueprint.md#container), uma vez fornecido com um modelo pela [Provedor de Modelo](/help/sites-developing/spa-blueprint.md#the-model-provider), repete o conteúdo do modelo ( `:items`).

1. No caso de uma página, seus filhos ( `:children`) primeiro obtenha uma classe de componente do [Mapeamento de componentes](/help/sites-developing/spa-blueprint.md#componentmapping) e depois instancie-o.

## Inicialização do aplicativo {#app-initialization}

Cada componente é estendido com os recursos do [ `ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). Por conseguinte, a inicialização assume a seguinte forma geral:

1. Cada provedor de modelo inicializa-se e escuta alterações feitas no modelo que corresponde ao seu componente interno.
1. O [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) deve ser inicializado, representado pelo [fluxo de inicialização](/help/sites-developing/spa-blueprint.md).

1. Depois de armazenado, o gerenciador de modelo de página retorna o modelo completo do aplicativo.
1. Esse modelo é então passado para a raiz de front-end [Contêiner](/help/sites-developing/spa-blueprint.md#container) componente do aplicativo.
1. Partes do modelo são finalmente propagadas para cada componente filho individual.

![app_model_initialization](assets/app_model_initialization.png)
