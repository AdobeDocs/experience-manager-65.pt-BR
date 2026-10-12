---
title: Modelo dinâmico para mapeamento de componentes para SPAs
description: Saiba como o modelo dinâmico para mapeamento de componentes ocorre no JavaScript SPA SDK for Adobe Experience Manager.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: a9f7d31e-bbe1-4475-966a-5f213546fcd9
    internal-label: SPA Editor
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%
---

# Modelo dinâmico para mapeamento de componentes para SPAs{#dynamic-model-to-component-mapping-for-spas}

Este documento descreve como o modelo dinâmico para mapeamento de componentes ocorre no JavaScript SPA SDK for Adobe Experience Manager (AEM).

{{ue-over-spa}}

## Módulo ComponentMapping {#componentmapping-module}

O módulo `ComponentMapping` é fornecido como um pacote NPM para o projeto front-end. Ele armazena componentes de front-end e fornece uma maneira para o Aplicativo de página única mapear componentes de front-end para tipos de recursos do AEM. Isso permite uma resolução dinâmica de componentes ao analisar o modelo JSON do aplicativo.

Cada item presente no modelo contém um campo `:type` que expõe um tipo de recurso AEM. Quando montado, o componente de front-end pode ser renderizado usando o fragmento de modelo que recebeu das bibliotecas subjacentes.

Consulte [Blueprint do SPA](/help/sites-developing/spa-blueprint.md) para obter mais informações sobre análise de modelo e acesso do componente front-end ao modelo.

Consulte também o pacote npm: [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicativo de página única orientado por modelo {#model-driven-single-page-application}

Os aplicativos de página única que usam o JavaScript SPA SDK para AEM são orientados por modelo:

1. Os componentes front-end se registram no [Repositório de Mapeamentos de Componentes](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. Em seguida, o [Contêiner](/help/sites-developing/spa-blueprint.md#container), uma vez fornecido com um modelo pelo [Provedor de Modelos](/help/sites-developing/spa-blueprint.md#the-model-provider), itera sobre seu conteúdo de modelo ( `:items`).

1. Se houver uma página, seus filhos ( `:children`) obterão primeiro uma classe de componente do [Mapeamento de Componentes](/help/sites-developing/spa-blueprint.md#componentmapping) e a instanciarão.

## Inicialização do aplicativo {#app-initialization}

Cada componente é estendido com os recursos do [`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). A inicialização assume a seguinte forma geral:

1. Cada provedor de modelo se inicializa e escuta as alterações feitas na parte do modelo que corresponde ao componente interno.
1. O [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) deve ser inicializado como representado pelo [fluxo de inicialização](/help/sites-developing/spa-blueprint.md).

1. Depois de armazenado, o gerenciador de modelo de página retorna o modelo completo do aplicativo.
1. Este modelo é então passado para o componente raiz de front-end [Container](/help/sites-developing/spa-blueprint.md#container) do aplicativo.
1. Partes do modelo são finalmente propagadas para cada componente filho individual.

![app_model_initialization](assets/app_model_initialization.png)
