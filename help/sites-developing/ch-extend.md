---
title: Extensão do ContextHub
description: Definir novos tipos de armazenamentos e módulos do ContextHub quando os fornecidos não atenderem aos requisitos da solução
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# Extensão do ContextHub{#extending-contexthub}

Defina novos tipos de armazenamentos e módulos do ContextHub quando os fornecidos não atenderem aos requisitos da solução.

## Criação de candidatos à loja personalizada {#creating-custom-store-candidates}

Os armazenamentos do ContextHub são criados de candidatos de armazenamento registrados. Para criar um armazenamento personalizado, crie e registre um candidato do armazenamento.

O arquivo JavaScript que inclui o código que cria e registra o candidato do armazenamento deve ser incluído em um [pasta da biblioteca do cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). A categoria da pasta deve corresponder ao seguinte padrão:

```xml
contexthub.store.[storeType]
```

A variável `[storeType]` parte da categoria é a `storeType` com o qual o candidato da loja está registrado. (Consulte [Registrando um candidato de armazenamento do ContextHub](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). Por exemplo, para o storeType de `contexthub.mystore`, a categoria da pasta da biblioteca do cliente deve ser `contexthub.store.contexthub.mystore`.

### Criação de um candidato de armazenamento do ContextHub {#creating-a-contexthub-store-candidate}

Para criar um candidato de armazenamento, use o [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) função para estender um dos armazenamentos base:

* [&quot;ContextHub.Store.PersistedStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [&quot;ContextHub.Store.SessionStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [&quot;ContextHub.Store.JSONPStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [&quot;ContextHub.Store.PersistedJSONPStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

Cada armazenamento básico estende o [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) armazenamento.

O exemplo a seguir cria a extensão mais simples do `ContextHub.Store.PersistedStore` candidato a armazenamento:

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

Na realidade, seus candidatos de armazenamento personalizados definem funções adicionais ou substituem a configuração inicial do armazenamento. Vários [exemplos de candidatos à loja](/help/sites-developing/ch-samplestores.md) estão instalados no repositório abaixo `/libs/granite/contexthub/components/stores`. Para aprender com esses exemplos, use o CRXDE Lite para abrir os arquivos JavaScript.

### Registrando um candidato de armazenamento do ContextHub {#registering-a-contexthub-store-candidate}

Registre um candidato de armazenamento para integrá-lo à estrutura do ContextHub e permitir que os armazenamentos sejam criados a partir dele. Para registrar um candidato de armazenamento, use o [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) função da `ContextHub.Utils.storeCandidates` classe.

Ao registrar um candidato de armazenamento, forneça um nome para o tipo de armazenamento. Ao criar um armazenamento a partir do candidato, use o tipo de armazenamento para identificar o candidato no qual ele se baseia.

Ao registrar um candidato de armazenamento, você indica sua prioridade. Quando um candidato de armazenamento é registrado usando o mesmo tipo de armazenamento que um candidato de armazenamento já registrado, o candidato com a prioridade mais alta é usado. Portanto, você pode substituir candidatos de armazenamento existentes por novas implementações.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Normalmente, apenas um candidato é necessário e a prioridade pode ser definida como `0`. Mas se você estiver interessado, você pode aprender sobre [registros mais avançados,](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) que permite que uma das poucas implementações de armazenamento seja escolhida com base na condição do JavaScript (`applies`) e a prioridade do candidato.

## Criação de tipos de módulo da interface do usuário do ContextHub {#creating-contexthub-ui-module-types}

Criar tipos de módulo de interface personalizada quando os que estão [instalado com o ContextHub](/help/sites-developing/ch-samplemodules.md) não atendem aos seus requisitos. Para criar um tipo de módulo de interface do usuário, crie um renderizador de módulo de interface do usuário estendendo o `ContextHub.UI.BaseModuleRenderer` e, em seguida, registrando-a com `ContextHub.UI`.

Para criar um renderizador de módulo de interface do usuário, crie um `Class` objeto que contém a lógica que renderiza o módulo da interface do usuário. No mínimo, sua classe deve executar as seguintes ações:

* Estenda o `ContextHub.UI.BaseModuleRenderer` classe. Essa classe é a implementação base para todos os renderizadores de módulo de interface do usuário. A variável `Class` O objeto define uma propriedade chamada `extend` que você usa para nomear essa classe como aquela que está sendo estendida.

* Forneça uma configuração padrão. Criar um `defaultConfig` propriedade. Essa propriedade é um objeto que inclui as propriedades definidas para o [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) Módulo de interface do usuário e quaisquer outras propriedades necessárias.

A fonte para `ContextHub.UI.BaseModuleRenderer` O está em /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js. Para registrar o renderizador, use o [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) método do `ContextHub.UI` classe. Forneça um nome para o tipo de módulo. Quando os administradores criam um módulo de interface do usuário com base nesse renderizador, eles especificam esse nome.

Crie e registre a classe do renderizador em uma função anônima autoexecutável. O exemplo a seguir é baseado no código-fonte para o módulo de interface do usuário contexthub.browserinfo. Esse módulo de interface do usuário é uma extensão simples do `ContextHub.UI.BaseModuleRenderer` classe.

```xml
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

O arquivo JavaScript que inclui o código que cria e registra o renderizador deve ser incluído em um [pasta da biblioteca do cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). A categoria da pasta deve corresponder ao seguinte padrão:

```xml
contexthub.module.[moduleType]
```

A variável `[moduleType]` parte da categoria é a `moduleType` com o qual o renderizador do módulo está registrado. Por exemplo, para o `moduleType` de `contexthub.browserinfo`, a categoria da pasta da biblioteca do cliente deve ser `contexthub.module.contexthub.browserinfo`.
