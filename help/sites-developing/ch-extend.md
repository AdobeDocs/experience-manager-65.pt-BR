---
title: Extensão do ContextHub
seo-title: Extending ContextHub
description: Defina novos tipos de armazenamentos e módulos do ContextHub quando os fornecidos não atenderem aos requisitos da solução
seo-description: Define new types of ContextHub stores and modules when the ones provided do not meet your solution requirements
uuid: 1d80c01d-ec5d-4e76-849d-bec0e1c3941a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 13a908ae-6965-4438-96d0-93516b500884
exl-id: 41898fa7-a369-4c63-8ccb-69eb3fa146a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---

# Extensão do ContextHub{#extending-contexthub}

Defina novos tipos de armazenamentos e módulos do ContextHub quando os fornecidos não atenderem aos requisitos da solução.

## Criação de Candidatos de Loja Personalizada {#creating-custom-store-candidates}

As lojas ContextHub são criadas a partir de candidatos a lojas registradas. Para criar uma loja personalizada, você precisa criar e registrar um candidato de loja.

O arquivo javascript que inclui o código que cria e registra o candidato da loja deve ser incluído em um [pasta da biblioteca do cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). A categoria da pasta deve corresponder ao seguinte padrão:

```xml
contexthub.store.[storeType]
```

O `[storeType]` parte da categoria é `storeType` com o qual o candidato da loja está registrado. (Consulte [Registrando um candidato a armazenamento do ContextHub](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). Por exemplo, para o storeType de `contexthub.mystore`, a categoria da pasta da biblioteca do cliente deve ser `contexthub.store.contexthub.mystore`.

### Criando um candidato a armazenamento do ContextHub {#creating-a-contexthub-store-candidate}

Para criar um candidato de loja, use a variável [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) para estender um dos armazenamentos base:

* [&quot;ContextHub.Store.PersistedStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [&quot;ContextHub.Store.SessionStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [&quot;ContextHub.Store.JSONPStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [&quot;ContextHub.Store.PersistedJSONPStore&quot;](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

Observe que cada loja base estende a variável [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core) armazenar.

O exemplo a seguir cria a extensão mais simples do `ContextHub.Store.PersistedStore` candidato à loja:

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

Realisticamente, os candidatos a loja personalizada definirão funções adicionais ou substituirão a configuração inicial da loja. Vários [candidatos à loja de amostras](/help/sites-developing/ch-samplestores.md) são instalados no repositório abaixo `/libs/granite/contexthub/components/stores`. Para aprender com essas amostras, use o CRXDE Lite para abrir os arquivos javascript.

### Registrando um candidato a armazenamento do ContextHub {#registering-a-contexthub-store-candidate}

Registre um candidato a loja para integrá-lo à estrutura do ContextHub e permitir que as lojas sejam criadas a partir dele. Para registrar um candidato de loja, use a variável [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) da `ContextHub.Utils.storeCandidates` classe .

Ao registrar um candidato de loja, forneça um nome para o tipo de loja. Ao criar uma loja do candidato, você usa o tipo de loja para identificar o candidato em que se baseia.

Ao registrar um candidato a loja, você indica sua prioridade. Quando um candidato de loja é registrado usando o mesmo tipo de loja que um candidato de loja já registrado, o candidato com prioridade mais alta é usado. Portanto, você pode substituir candidatos de loja existentes por novas implementações.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Na maioria dos casos, só é necessário um candidato e a prioridade pode ser definida como `0`, mas se você estiver interessado, poderá saber mais sobre [registros mais avançados,](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) O que permite que uma das poucas implementações da loja seja escolhida com base na condição de javascript (`applies`) e a prioridade do candidato.

## Criação de tipos de módulos da interface do usuário do ContextHub {#creating-contexthub-ui-module-types}

Criar tipos de módulo de interface de usuário personalizada quando os [instalado com o ContextHub](/help/sites-developing/ch-samplemodules.md) não atenda aos seus requisitos. Para criar um tipo de módulo de interface do usuário, crie um novo renderizador de módulo de interface do usuário estendendo o `ContextHub.UI.BaseModuleRenderer` e registrá-la com `ContextHub.UI`.

Para criar um renderizador de módulo de interface do usuário, crie um `Class` objeto que contém a lógica que renderiza o módulo da interface do usuário. No mínimo, sua classe deve executar as seguintes ações:

* Estender o `ContextHub.UI.BaseModuleRenderer` classe . Essa classe é a implementação básica para todos os renderizadores de módulo da interface do usuário. O `Class` objeto define uma propriedade chamada `extend` que você usa para nomear essa classe como aquela que está sendo estendida.

* Forneça uma configuração padrão. Crie um `defaultConfig` propriedade. Essa propriedade é um objeto que inclui as propriedades definidas para a variável [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) Módulo de interface do usuário e quaisquer outras propriedades necessárias.

A fonte para `ContextHub.UI.BaseModuleRenderer` está localizado em /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js.  Para registrar o renderizador, use o [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) do método `ContextHub.UI` classe . É necessário fornecer um nome para o tipo de módulo. Quando os administradores criam um módulo de interface com base nesse renderizador, eles especificam esse nome.

Crie e registre a classe renderer em uma função anônima de execução automática. O exemplo a seguir é baseado no código-fonte do módulo da interface do usuário contexthub.browserinfo . Este módulo de interface é uma extensão simples do `ContextHub.UI.BaseModuleRenderer` classe .

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

O arquivo javascript que inclui o código que cria e registra o renderizador deve ser incluído em um [pasta da biblioteca do cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). A categoria da pasta deve corresponder ao seguinte padrão:

```xml
contexthub.module.[moduleType]
```

O `[moduleType]` parte da categoria é `moduleType` com o qual o renderizador de módulo é registrado. Por exemplo, para a variável `moduleType` de `contexthub.browserinfo`, a categoria da pasta da biblioteca do cliente deve ser `contexthub.module.contexthub.browserinfo`.
