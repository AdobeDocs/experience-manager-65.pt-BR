---
title: Roteamento do Modelo de SPA
seo-title: SPA Model Routing
description: Para aplicativos de página única no AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo de roteamento, o contrato e as opções disponíveis.
seo-description: For single page applications in AEM, the app is responsible for the routing. This document describes the routing mechanism, the contract, and options available.
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
exl-id: eaef65ec-2e4d-490f-8158-d48d738e3409
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Roteamento do Modelo de SPA{#spa-model-routing}

Para aplicativos de página única no AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo de roteamento, o contrato e as opções disponíveis.

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização do lado do cliente baseada em SPA estrutura (por exemplo, Reagir ou Angular).

## Roteamento do projeto {#project-routing}

O aplicativo é proprietário do roteamento e é implementado pelos desenvolvedores de front-end do projeto. Este documento descreve o roteamento específico para o modelo retornado pelo servidor AEM. A estrutura de dados do modelo de página expõe o URL do recurso subjacente. O projeto front-end pode usar qualquer biblioteca personalizada ou de terceiros que forneça funcionalidades de roteamento. Quando uma rota espera um fragmento de modelo, uma chamada para a variável `PageModelManager.getData()` pode ser feita. Quando uma rota de modelo é alterada, um evento deve ser acionado para avisar as bibliotecas de escuta, como o Editor de páginas.

## Arquitetura {#architecture}

Para obter uma descrição detalhada, consulte o [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) seção do documento Blueprint SPA.

## ModelRouter {#modelrouter}

O `ModelRouter` - quando ativado - encapsula as funções da API do Histórico do HTML5 `pushState` e `replaceState` para garantir que um determinado fragmento do modelo seja buscado e acessível previamente. Em seguida, notifica o componente front-end registrado de que o modelo foi modificado.

## Roteamento Manual vs Automático de Modelo {#manual-vs-automatic-model-routing}

O `ModelRouter` automatiza a busca de fragmentos do modelo. Mas como qualquer ferramenta automatizada, ela tem limitações. Quando necessário `ModelRouter` pode ser desativado ou configurado para ignorar caminhos usando propriedades meta (consulte a seção Propriedades Meta do [Componente Página SPA](/help/sites-developing/spa-page-component.md) documento). Os desenvolvedores de front-end podem implementar sua própria camada de roteamento de modelo, solicitando a `PageModelManager` para carregar qualquer fragmento específico do modelo usando o `getData()` .

>[!NOTE]
>
>Atualmente, o projeto React da amostra de diário We.Retail ilustra a abordagem automatizada, enquanto o projeto do Angular ilustra a abordagem manual. Uma abordagem semiautomatizada seria também um caso de uso válido.

>[!CAUTION]
>
>A versão atual do `ModelRouter` suporta apenas o uso de URLs que apontem para o caminho de recurso real dos pontos de entrada do Modelo do Sling. Não é compatível com o uso de URLs ou aliases personalizados.

## Contrato de Roteamento {#routing-contract}

A implementação atual baseia-se na hipótese de que o projeto de SPA usa a API do Histórico do HTML5 para rotear para as diferentes páginas do aplicativo.

### Configuração {#configuration}

O `ModelRouter` suporta o conceito de roteamento de modelo como ele escuta `pushState` e `replaceState` chamadas para buscar fragmentos de modelo previamente. Internamente, ele dispara a função `PageModelManager` para carregar o modelo que corresponde a um determinado URL e dispara um `cq-pagemodel-route-changed` evento que outros módulos podem ouvir.

Por padrão, esse comportamento é ativado automaticamente. Para desativá-lo, o SPA deve renderizar a seguinte meta propriedade:

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Observe que cada rota do SPA deve corresponder a um recurso acessível em AEM (por exemplo, &quot; `/content/mysite/mypage"`) desde a `PageModelManager` O tentará carregar automaticamente o modelo de página correspondente depois que a rota for selecionada. Embora, se necessário, o SPA também possa definir uma &quot;lista de bloqueios&quot; de rotas que devem ser ignoradas pelo `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
