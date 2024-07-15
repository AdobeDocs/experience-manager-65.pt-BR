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

O arquivo JavaScript que inclui o código que cria e registra o candidato de armazenamento deve ser incluído em uma [pasta da biblioteca do cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). A categoria da pasta deve corresponder ao seguinte padrão:

```xml
contexthub.store.[storeType]
```

A parte `[storeType]` da categoria é o `storeType` com o qual o candidato a armazenamento está registrado. (Consulte [Registrando um candidato de armazenamento do ContextHub](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). Por exemplo, para o storeType de `contexthub.mystore`, a categoria da pasta da biblioteca do cliente deve ser `contexthub.store.contexthub.mystore`.

### Criação de um candidato de armazenamento do ContextHub {#creating-a-contexthub-store-candidate}

Para criar um candidato de armazenamento, use a função [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) para estender um dos armazenamentos base:

* [&quot;ContextHub.Store.PersistedStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [&quot;ContextHub.Store.SessionStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [&quot;ContextHub.Store.JSONPStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [&quot;ContextHub.Store.PersistedJSONPStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

Cada armazenamento base estende o armazenamento [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core).

O exemplo a seguir cria a extensão mais simples do candidato a armazenamento `ContextHub.Store.PersistedStore`:

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

Na realidade, seus candidatos de armazenamento personalizados definem funções adicionais ou substituem a configuração inicial do armazenamento. Vários [candidatos de armazenamento de exemplo](/help/sites-developing/ch-samplestores.md) estão instalados no repositório abaixo de `/libs/granite/contexthub/components/stores`. Para aprender com esses exemplos, use o CRXDE Lite para abrir os arquivos JavaScript.

### Registrando um candidato de armazenamento do ContextHub {#registering-a-contexthub-store-candidate}

Registre um candidato de armazenamento para integrá-lo à estrutura do ContextHub e permitir que os armazenamentos sejam criados a partir dele. Para registrar um candidato de armazenamento, use a função [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) da classe `ContextHub.Utils.storeCandidates`.

Ao registrar um candidato de armazenamento, forneça um nome para o tipo de armazenamento. Ao criar um armazenamento a partir do candidato, use o tipo de armazenamento para identificar o candidato no qual ele se baseia.

Ao registrar um candidato de armazenamento, você indica sua prioridade. Quando um candidato de armazenamento é registrado usando o mesmo tipo de armazenamento que um candidato de armazenamento já registrado, o candidato com a prioridade mais alta é usado. Portanto, você pode substituir candidatos de armazenamento existentes por novas implementações.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Normalmente, apenas um candidato é necessário e a prioridade pode ser definida como `0`. Mas, se estiver interessado, você poderá saber mais sobre [registros mais avançados](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies), que permitem que uma das poucas implementações de loja seja escolhida com base na condição do JavaScript (`applies`) e na prioridade do candidato.

## Criação de tipos de módulo da interface do usuário do ContextHub {#creating-contexthub-ui-module-types}

Crie tipos de módulo de interface personalizada quando os que estão [instalados com o ContextHub](/help/sites-developing/ch-samplemodules.md) não atenderem aos seus requisitos. Para criar um tipo de módulo de interface do usuário, crie um renderizador de módulo de interface estendendo a classe `ContextHub.UI.BaseModuleRenderer` e depois registrando-a com `ContextHub.UI`.

Para criar um renderizador de módulo de interface do usuário, crie um objeto `Class` que contenha a lógica que renderiza o módulo de interface do usuário. No mínimo, sua classe deve executar as seguintes ações:

* Estender a classe `ContextHub.UI.BaseModuleRenderer`. Essa classe é a implementação base para todos os renderizadores de módulo de interface do usuário. O objeto `Class` define uma propriedade chamada `extend` que você usa para nomear essa classe como aquela que está sendo estendida.

* Forneça uma configuração padrão. Criar uma propriedade `defaultConfig`. Esta propriedade é um objeto que inclui as propriedades definidas para o módulo de interface do usuário [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) e quaisquer outras propriedades necessárias.

A origem de `ContextHub.UI.BaseModuleRenderer` está em /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js. Para registrar o renderizador, use o método [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) da classe `ContextHub.UI`. Forneça um nome para o tipo de módulo. Quando os administradores criam um módulo de interface do usuário com base nesse renderizador, eles especificam esse nome.

Crie e registre a classe do renderizador em uma função anônima autoexecutável. O exemplo a seguir é baseado no código-fonte para o módulo de interface do usuário contexthub.browserinfo. Este módulo de interface é uma extensão simples da classe `ContextHub.UI.BaseModuleRenderer`.

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

O arquivo JavaScript que inclui o código que cria e registra o renderizador deve ser incluído em uma [pasta da biblioteca do cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). A categoria da pasta deve corresponder ao seguinte padrão:

```xml
contexthub.module.[moduleType]
```

A parte `[moduleType]` da categoria é o `moduleType` com o qual o renderizador de módulo está registrado. Por exemplo, para o `moduleType` de `contexthub.browserinfo`, a categoria da pasta da biblioteca do cliente deve ser `contexthub.module.contexthub.browserinfo`.
