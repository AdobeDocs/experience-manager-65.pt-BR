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
source-git-commit: 6d961456e0e1f7a26121da9be493308a62c53e04
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# Roteamento de modelo SPA{#spa-model-routing}

Para aplicativos de página única no AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo de encaminhamento, o contrato e as opções disponíveis.

{{ue-over-spa}}

## Roteamento do projeto {#project-routing}

O aplicativo é o proprietário do roteamento e é implementado pelos desenvolvedores de front-end do projeto. Este documento descreve o roteamento específico para o modelo retornado pelo servidor AEM. A estrutura de dados do modelo de página expõe o URL do recurso subjacente. O projeto de front-end pode usar qualquer biblioteca personalizada ou de terceiros fornecendo funcionalidades de roteamento. Quando uma rota espera um fragmento de modelo, é possível fazer uma chamada para a função `PageModelManager.getData()`. Quando uma rota de modelo é alterada, um evento deve ser acionado para avisar as bibliotecas de escuta, como o Editor de páginas.

## Arquitetura {#architecture}

Para obter uma descrição detalhada, consulte a seção [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) do documento Blueprint do SPA.

## RoteadorModelo {#modelrouter}

O `ModelRouter`, quando habilitado, encapsula as funções `pushState` e `replaceState` da API do Histórico de HTML5 para garantir que determinado fragmento de modelo seja buscado previamente e esteja acessível. Em seguida, notifica o componente de front-end registrado de que o modelo foi modificado.

## Roteiro de Modelo Manual vs. Automático {#manual-vs-automatic-model-routing}

O `ModelRouter` automatiza a busca de fragmentos do modelo. Mas, como qualquer ferramenta automatizada, há limitações. Quando necessário, o `ModelRouter` pode ser desabilitado ou configurado para ignorar caminhos usando metapropriedades (Consulte a seção Metapropriedades do [Componente de página do SPA](/help/sites-developing/spa-page-component.md)). Os desenvolvedores de front-end podem então implementar sua própria camada de roteamento de modelo, solicitando que `PageModelManager` carregue qualquer fragmento de modelo fornecido usando a função `getData()`.

>[!NOTE]
>
>O projeto React de amostra do [We.Retail](https://github.com/adobe/aem-sample-we-retail-journal) ilustra a abordagem automatizada, enquanto o projeto do Angular ilustra a manual. Uma abordagem semiautomatizada também seria um caso de uso válido.

>[!CAUTION]
>
>A versão atual do `ModelRouter` dá suporte apenas ao uso de URLs que apontam para o caminho de recurso real dos pontos de entrada do Modelo Sling. Ele não é compatível com o uso de URLs ou aliases personalizados.

## Contrato de Encaminhamento {#routing-contract}

A implementação atual baseia-se no pressuposto de que o projeto SPA usa a API de Histórico HTML5 para roteamento para as diferentes páginas de aplicativos.

### Configuração {#configuration}

O `ModelRouter` dá suporte ao conceito de roteamento de modelo, pois escuta as chamadas `pushState` e `replaceState` para buscar previamente fragmentos de modelo. Internamente, ele aciona `PageModelManager` para carregar o modelo que corresponde a determinada URL e aciona um evento `cq-pagemodel-route-changed` que outros módulos podem ouvir.

Por padrão, esse comportamento é ativado automaticamente. Para desativá-lo, o SPA deve renderizar a seguinte metapropriedade:

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

Observe que cada rota do SPA deve corresponder a um recurso acessível no AEM (por exemplo, &quot; `/content/mysite/mypage"`), já que o `PageModelManager` tentará automaticamente carregar o modelo de página correspondente quando a rota for selecionada. Embora, se necessário, o SPA também possa definir uma &quot;lista de bloqueios&quot; de rotas que devem ser ignoradas pelo `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
