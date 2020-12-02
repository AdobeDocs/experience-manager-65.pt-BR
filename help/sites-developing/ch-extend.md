---
title: Extensão do ContextHub
seo-title: Extensão do ContextHub
description: Definir novos tipos de armazenamentos e módulos do ContextHub quando os fornecidos não atenderem aos requisitos da solução
seo-description: Definir novos tipos de armazenamentos e módulos do ContextHub quando os fornecidos não atenderem aos requisitos da solução
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
translation-type: tm+mt
source-git-commit: ed34f2200f4ff4f407f7b92165685af390f5f7e3
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Extensão do ContextHub{#extending-contexthub}

Defina novos tipos de armazenamentos e módulos do ContextHub quando os fornecidos não atenderem aos requisitos da solução.

## Criando Candidatos à Loja Personalizada {#creating-custom-store-candidates}

As lojas do ContextHub são criadas de candidatos a lojas registradas. Para criar uma loja personalizada, é necessário criar e registrar um candidato de loja.

O arquivo javascript que inclui o código que cria e registra o candidato da loja deve ser incluído em uma [pasta da biblioteca do cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). A categoria da pasta deve corresponder ao seguinte padrão:

```xml
contexthub.store.[storeType]
```

A parte `[storeType]` da categoria é a `storeType` com a qual o candidato da loja está registrado. (Consulte [Registrando um Candidato à Loja do ContextHub](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). Por exemplo, para o storeType de `contexthub.mystore`, a categoria da pasta da biblioteca do cliente deve ser `contexthub.store.contexthub.mystore`.

### Criando um candidato de armazenamento do ContextHub {#creating-a-contexthub-store-candidate}

Para criar um candidato de loja, use a função [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) para estender um dos armazenamentos base:

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

Observe que cada armazenamento base estende a loja [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core).

O exemplo a seguir cria a extensão mais simples do candidato de armazenamento `ContextHub.Store.PersistedStore`:

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

Realisticamente, seus candidatos à loja personalizada definirão funções adicionais ou substituirão a configuração inicial da loja. Vários [candidatos de armazenamento de amostra](/help/sites-developing/ch-samplestores.md) estão instalados no repositório abaixo de `/libs/granite/contexthub/components/stores`. Para aprender com essas amostras, use o CRXDE Lite para abrir os arquivos javascript.

### Registrando um candidato da loja do ContextHub {#registering-a-contexthub-store-candidate}

Registre um candidato de loja para integrá-lo à estrutura do ContextHub e permitir que as lojas sejam criadas a partir dela. Para registrar um candidato de loja, use a função [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) da classe `ContextHub.Utils.storeCandidates`.

Ao registrar um candidato de loja, forneça um nome para o tipo de loja. Ao criar uma loja a partir do candidato, use o tipo de loja para identificar o candidato no qual ela se baseia.

Ao registrar um candidato a loja, você indica sua prioridade. Quando um candidato de loja é registrado usando o mesmo tipo de loja que um candidato de loja já registrado, o candidato com prioridade mais alta é usado. Portanto, você pode substituir os candidatos de armazenamento existentes por novas implementações.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Na maioria dos casos, apenas um candidato é necessário e a prioridade pode ser definida como `0`, mas se você estiver interessado, você pode saber mais sobre [registros mais avançados,](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) o que permite que uma das poucas implementações de armazenamento seja escolhida com base na condição javascript (`applies`) e na prioridade do candidato.

## Criando tipos de módulo de interface do usuário do ContextHub {#creating-contexthub-ui-module-types}

Crie tipos de módulo de interface de usuário personalizados quando os que estão [instalados com o ContextHub](/help/sites-developing/ch-samplemodules.md) não atenderem aos seus requisitos. Para criar um tipo de módulo de interface, crie um novo renderizador de módulo de interface estendendo a classe `ContextHub.UI.BaseModuleRenderer` e, em seguida, registrando-o com `ContextHub.UI`.

Para criar um renderizador de modulador de interface, crie um objeto `Class` que contenha a lógica que renderiza o módulo de interface. No mínimo, sua classe deve executar as seguintes ações:

* Estende a classe `ContextHub.UI.BaseModuleRenderer`. Essa classe é a implementação básica para todos os renderizadores de módulo de interface. O objeto `Class` define uma propriedade chamada `extend` que você usa para nomear essa classe como aquela que está sendo estendida.

* Forneça uma configuração padrão. Crie uma propriedade `defaultConfig`. Esta propriedade é um objeto que inclui as propriedades definidas para o módulo [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) da interface do usuário e quaisquer outras propriedades necessárias.

A fonte para `ContextHub.UI.BaseModuleRenderer` está localizada em /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js.  Para registrar o renderizador, use o método [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) da classe `ContextHub.UI`. É necessário fornecer um nome para o tipo de módulo. Quando os administradores criam um módulo de interface com base nesse renderizador, eles especificam esse nome.

Crie e registre a classe renderizadora em uma função anônima autoexecutável. O exemplo a seguir é baseado no código fonte do módulo de interface do usuário context.browserinfo. Este módulo de interface é uma extensão simples da classe `ContextHub.UI.BaseModuleRenderer`.

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

O arquivo javascript que inclui o código que cria e registra o renderizador deve ser incluído em uma [pasta da biblioteca do cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). A categoria da pasta deve corresponder ao seguinte padrão:

```xml
contexthub.module.[moduleType]
```

A parte `[moduleType]` da categoria é a `moduleType` com a qual o renderizador de módulo está registrado. Por exemplo, para `moduleType` de `contexthub.browserinfo`, a categoria da pasta da biblioteca do cliente deve ser `contexthub.module.contexthub.browserinfo`.
