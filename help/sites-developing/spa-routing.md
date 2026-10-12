---
title: Roteamento de modelo SPA
description: Para aplicativos de página única no AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo de encaminhamento, o contrato e as opções disponíveis.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: eaef65ec-2e4d-490f-8158-d48d738e3409
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
source-wordcount: '479'
ht-degree: 0%
---

# Roteamento de modelo SPA{#spa-model-routing}

Para aplicativos de página única no AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo de encaminhamento, o contrato e as opções disponíveis.

{{ue-over-spa}}

## Roteamento do projeto {#project-routing}

O aplicativo é o proprietário do roteamento e é implementado pelos desenvolvedores de front-end do projeto. Este documento descreve o roteamento específico para o modelo retornado pelo servidor do AEM. A estrutura de dados do modelo de página expõe o URL do recurso subjacente. O projeto de front-end pode usar qualquer biblioteca personalizada ou de terceiros fornecendo funcionalidades de roteamento. Quando uma rota espera um fragmento de modelo, é possível fazer uma chamada para a função `PageModelManager.getData()`. Quando uma rota de modelo é alterada, um evento deve ser acionado para avisar as bibliotecas de escuta, como o Editor de páginas.

## Arquitetura {#architecture}

Para obter uma descrição detalhada, consulte a seção [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) do documento do SPA Blueprint.

## RoteadorModelo {#modelrouter}

O `ModelRouter`, quando habilitado, encapsula as funções `pushState` e `replaceState` da API do Histórico do HTML5 para garantir que determinado fragmento de modelo seja buscado previamente e esteja acessível. Em seguida, notifica o componente de front-end registrado de que o modelo foi modificado.

## Roteiro de Modelo Manual vs. Automático {#manual-vs-automatic-model-routing}

O `ModelRouter` automatiza a busca de fragmentos do modelo. Mas, como qualquer ferramenta automatizada, há limitações. Quando necessário, o `ModelRouter` pode ser desabilitado ou configurado para ignorar caminhos usando metapropriedades (Consulte a seção Propriedades do Meta do [Componente de página do SPA](/help/sites-developing/spa-page-component.md) documento). Os desenvolvedores de front-end podem então implementar sua própria camada de roteamento de modelo, solicitando que `PageModelManager` carregue qualquer fragmento de modelo fornecido usando a função `getData()`.

>[!NOTE]
>
>O projeto React de amostra do [We.Retail](https://github.com/adobe/aem-sample-we-retail-journal) ilustra a abordagem automatizada, enquanto o projeto Angular ilustra a manual. Uma abordagem semiautomatizada também seria um caso de uso válido.

>[!CAUTION]
>
>A versão atual do `ModelRouter` dá suporte apenas ao uso de URLs que apontam para o caminho de recurso real dos pontos de entrada do Modelo Sling. Ele não é compatível com o uso de URLs ou aliases personalizados.

## Contrato de Encaminhamento {#routing-contract}

A implementação atual é baseada no pressuposto de que o projeto de SPA usa a API de histórico do HTML5 para roteamento para diferentes páginas de aplicativos.

### Configuração {#configuration}

O `ModelRouter` dá suporte ao conceito de roteamento de modelo, pois escuta as chamadas `pushState` e `replaceState` para buscar previamente fragmentos de modelo. Internamente, ele aciona `PageModelManager` para carregar o modelo que corresponde a determinada URL e aciona um evento `cq-pagemodel-route-changed` que outros módulos podem ouvir.

Por padrão, esse comportamento é ativado automaticamente. Para desativá-lo, o SPA deve renderizar a seguinte metapropriedade:

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

Observe que cada rota do SPA deve corresponder a um recurso acessível no AEM (por exemplo, &quot; `/content/mysite/mypage"`), pois o `PageModelManager` tentará automaticamente carregar o modelo de página correspondente depois que a rota for selecionada. Embora, se necessário, o SPA também possa definir uma &quot;lista de bloqueios&quot; de rotas que devem ser ignoradas pelo `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
