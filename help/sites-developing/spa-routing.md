---
title: roteamento Modelo SPA
seo-title: roteamento Modelo SPA
description: Para aplicativos de página única em AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo do roteamento, o contrato e as opções disponíveis.
seo-description: Para aplicativos de página única em AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo do roteamento, o contrato e as opções disponíveis.
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
translation-type: tm+mt
source-git-commit: 4ea1bad1fb76142be7f6d564ecf30ed85a6da694
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---


# roteamento do modelo SPA{#spa-model-routing}

Para aplicativos de página única em AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo do roteamento, o contrato e as opções disponíveis.

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização do cliente baseada em SPA estrutura (por exemplo, Reagir ou Angular).

## Roteamento do projeto {#project-routing}

O aplicativo é proprietário do roteamento e é implementado pelos desenvolvedores front-end do projeto. Este documento descreve o roteamento específico para o modelo retornado pelo servidor AEM. A estrutura de dados do modelo de página expõe o URL do recurso subjacente. O projeto front-end pode usar qualquer biblioteca personalizada ou de terceiros que ofereça funcionalidades de roteamento. Quando uma rota espera um fragmento de modelo, uma chamada para a função `PageModelManager.getData()` pode ser feita. Quando uma rota de modelo é alterada, um evento deve ser acionado para avisar bibliotecas de escuta, como o Editor de páginas.

## Arquitetura {#architecture}

Para obter uma descrição detalhada, consulte a seção [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) do documento Blueprint SPA.

## ModelRouter {#modelrouter}

O `ModelRouter` - quando ativado - encapsula as funções da API do histórico HTML5 `pushState` e `replaceState` para garantir que um determinado fragmento de modelo seja obtido previamente e acessível. Em seguida, notifica o componente de front-end registrado de que o modelo foi modificado.

## Roteamento de Modelo Manual vs Automático {#manual-vs-automatic-model-routing}

O `ModelRouter` automatiza a busca de fragmentos do modelo. Mas como qualquer ferramenta automática, ela traz limitações. Quando necessário, `ModelRouter` pode ser desabilitado ou configurado para ignorar caminhos usando metapropriedades (consulte a seção Metopropriedades do documento [SPA Componente de página](/help/sites-developing/spa-page-component.md)). Os desenvolvedores front-end podem implementar sua própria camada de roteamento de modelo, solicitando que `PageModelManager` carregue qualquer fragmento específico do modelo usando a função `getData()`.

>[!NOTE]
>
>Atualmente, o projeto React da amostra de Journal We.Retail ilustra a abordagem automatizada, enquanto o projeto Angular ilustra a abordagem manual. Uma abordagem semiautomatizada seria também um caso de utilização válido.

>[!CAUTION]
>
>A versão atual do `ModelRouter` suporta apenas o uso de URLs que apontam para o caminho de recurso real dos pontos de entrada do Modelo Sling. Ele não suporta o uso de URLs ou aliases personalizados.

## Contrato de roteamento {#routing-contract}

A implementação atual baseia-se na premissa de que o projeto SPA usa a API do histórico HTML5 para roteamento para as diferentes páginas do aplicativo.

### Configuração {#configuration}

O `ModelRouter` oferece suporte ao conceito de roteamento de modelo, pois ele escuta as chamadas `pushState` e `replaceState` para realizar a busca prévia de fragmentos de modelo. Internamente, aciona `PageModelManager` para carregar o modelo que corresponde a um determinado URL e aciona um evento `cq-pagemodel-route-changed` que outros módulos podem ouvir.

Por padrão, esse comportamento é ativado automaticamente. Para desativá-la, o SPA deve renderizar a seguinte propriedade meta:

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Observe que cada rota do SPA deve corresponder a um recurso acessível no AEM (por exemplo, &quot; `/content/mysite/mypage"`), já que `PageModelManager` tentará carregar automaticamente o modelo de página correspondente depois que a rota for selecionada. Embora, se necessário, o SPA também possa definir uma &quot;lista de bloqueios&quot; de rotas que devem ser ignoradas pelo `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
