---
title: Roteamento de modelo SPA
seo-title: SPA Model Routing
description: Para aplicativos de página única no AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo de encaminhamento, o contrato e as opções disponíveis.
seo-description: For single page applications in AEM, the app is responsible for the routing. This document describes the routing mechanism, the contract, and options available.
uuid: 93b4f85a-a240-42d4-95e2-e8b790df7723
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: d9f1e24e-51a9-4f28-b2cd-2e97aed63a24
exl-id: eaef65ec-2e4d-490f-8158-d48d738e3409
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Roteamento de modelo SPA{#spa-model-routing}

Para aplicativos de página única no AEM, o aplicativo é responsável pelo roteamento. Este documento descreve o mecanismo de encaminhamento, o contrato e as opções disponíveis.

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização no lado do cliente baseada na estrutura SPA (por exemplo, React ou Angular).

## Roteamento do projeto {#project-routing}

O aplicativo é o proprietário do roteamento e é implementado pelos desenvolvedores de front-end do projeto. Este documento descreve o roteamento específico para o modelo retornado pelo servidor AEM. A estrutura de dados do modelo de página expõe o URL do recurso subjacente. O projeto de front-end pode usar qualquer biblioteca personalizada ou de terceiros fornecendo funcionalidades de roteamento. Quando uma rota espera um fragmento de modelo, uma chamada para o `PageModelManager.getData()` função pode ser feita. Quando uma rota de modelo é alterada, um evento deve ser acionado para avisar as bibliotecas de escuta, como o Editor de páginas.

## Arquitetura {#architecture}

Para obter uma descrição detalhada, consulte o [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager) seção do documento Blueprint SPA.

## RoteadorModelo {#modelrouter}

A variável `ModelRouter` - quando ativado - encapsula as funções da API do histórico do HTML5 `pushState` e `replaceState` para garantir que determinado fragmento de modelo seja buscado previamente e acessível. Em seguida, notifica o componente de front-end registrado de que o modelo foi modificado.

## Roteiro de Modelo Manual vs. Automático {#manual-vs-automatic-model-routing}

A variável `ModelRouter` O automatiza a busca de fragmentos do modelo. Mas, como qualquer ferramenta automatizada, há limitações. Quando necessário, a variável `ModelRouter` podem ser desativadas ou configuradas para ignorar caminhos usando metapropriedades (Consulte a seção Metapropriedades do [Componente de página do SPA](/help/sites-developing/spa-page-component.md) documento). Os desenvolvedores de front-end podem então implementar sua própria camada de roteamento de modelo, solicitando a `PageModelManager` para carregar um determinado fragmento de modelo usando o `getData()` função.

>[!NOTE]
>
>A variável [Diário do We.Retail](https://github.com/adobe/aem-sample-we-retail-journal) exemplo O projeto React ilustra a abordagem automatizada, enquanto o projeto Angular ilustra a manual. Uma abordagem semiautomatizada também seria um caso de uso válido.

>[!CAUTION]
>
>A versão atual do `ModelRouter` suportam apenas o uso de URLs que apontam para o caminho real do recurso dos pontos de entrada do Modelo Sling. Ele não é compatível com o uso de URLs ou aliases personalizados.

## Contrato de Encaminhamento {#routing-contract}

A implementação atual baseia-se no pressuposto de que o projeto SPA usa a API de Histórico HTML5 para roteamento para as diferentes páginas de aplicativos.

### Configuração {#configuration}

A variável `ModelRouter` O suporta o conceito de roteamento de modelo conforme ele escuta `pushState` e `replaceState` chamadas para buscar previamente fragmentos do modelo. Internamente, ele aciona o `PageModelManager` para carregar o modelo que corresponde a um determinado URL e acionar um `cq-pagemodel-route-changed` evento que outros módulos podem ouvir.

Por padrão, esse comportamento é ativado automaticamente. Para desativá-lo, o SPA deve renderizar a seguinte metapropriedade:

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

Observe que cada rota do SPA deve corresponder a um recurso acessível no AEM (por exemplo, &quot; `/content/mysite/mypage"`), uma vez que `PageModelManager` O tentará carregar automaticamente o modelo de página correspondente quando a rota for selecionada. Embora, se necessário, o SPA também possa definir uma &quot;lista de bloqueios&quot; de rotas que devem ser ignoradas pelo `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
