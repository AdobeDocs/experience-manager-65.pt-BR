---
title: Como atualizar seu conteúdo por meio das APIs do AEM Assets
description: Nesta parte da jornada do desenvolvedor headless do AEM, saiba como usar a API REST para acessar e atualizar o conteúdo dos seus fragmentos de conteúdo.
exl-id: af29cb77-0210-4fc4-8d86-2a833d19b49f
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 92%

---

# Como atualizar seu conteúdo por meio das APIs do AEM Assets {#update-your-content}

Nesta parte da [jornada do desenvolvedor headless do AEM,](overview.md) saiba como usar a API REST para acessar e atualizar o conteúdo dos seus fragmentos de conteúdo.

## A história até agora {#story-so-far}

No documento anterior da jornada headless do AEM, [Como acessar seu conteúdo por meio das APIs de entrega do AEM](access-your-content.md), você aprendeu a acessar o conteúdo headless no AEM por meio da API GraphQL do AEM; agora você deve:

* Ter um alto nível de compreensão sobre GraphQL.
* Entender como a API GraphQL do AEM funciona.
* Conhecer alguns exemplos de consultas práticas.

Este artigo se baseia nesses fundamentos para que você entenda como atualizar o seu conteúdo headless existente no AEM por meio da API REST.

## Objetivo {#objective}

* **Público-alvo**: avançado
* **Objetivo**: aprender a usar a API REST para acessar e atualizar o conteúdo dos seus fragmentos de conteúdo:
   * Introdução à API HTTP do AEM Assets.
   * Apresentação e discussão sobre o suporte de fragmento de conteúdo da API.
   * Ilustração de detalhes da API.

<!--
  * Look at sample code to see how things work in practice.
-->

## Por que você precisa da API HTTP de ativos para fragmentos de conteúdo {#why-http-api}

No estágio anterior da jornada headless, você aprendeu como usar a API GraphQL do AEM para recuperar o conteúdo usando consultas.

Então, por que é necessária outra API?

A API HTTP de ativos permite **ler** seu conteúdo, mas também permite **criar**, **atualizar** e **excluir** conteúdo, ações que não são possíveis com a API GraphQL.

A API REST de ativos está disponível em cada instalação pronta para uso de versões recentes do Adobe Experience Manager 

## API HTTP de ativos {#assets-http-api}

A API HTTP de ativos abrange:

* API REST de ativos
* incluindo suporte para fragmentos de conteúdo

A implementação atual da API HTTP de ativos é baseada no estilo de arquitetura **REST** e permite que você acesse o conteúdo (armazenado no AEM) por meio de operações **CRUD** (criar, ler, atualizar, excluir).

Com essa operação, a API permite operar o Adobe Experience Manager como um CMS (Content Management System) sem periféricos fornecendo serviços de conteúdo a um aplicativo front-end JavaScript. Ou qualquer outro aplicativo que possa executar solicitações HTTP e manipular respostas JSON. Por exemplo, aplicativos de página única (SPA) baseados em estrutura ou personalizados exigem conteúdo fornecido por meio de uma API, geralmente no formato JSON.

<!--
>[!NOTE]
>
>It is not possible to customize JSON output from the Assets REST API. 

The Assets REST API:

* follows the HATEOAS principle
* implements the SIREN format

## Key Concepts {#key-concepts}

The Assets REST API offers REST-style access to assets stored within an AEM instance. 

It uses the `/api/assets` endpoint and requires the path of the asset to access it (without the leading `/content/dam`). 

* This means that to access the asset at:
  * `/content/dam/path/to/asset`
* You need to request:
  * `/api/assets/path/to/asset` 

For example, to access `/content/dam/wknd/en/adventures/cycling-tuscany`, request `/api/assets/wknd/en/adventures/cycling-tuscany.json` 

>[!NOTE]
>Access over:
>
>* `/api/assets` **does not** need the use of the `.model` selector.
>* `/content/path/to/page` **does** require the use of the `.model` selector.

The HTTP method determines the operation to be executed:

* **GET** - to retrieve a JSON representation of an asset or a folder
* **POST** - to create new assets or folders
* **PUT** - to update the properties of an asset or folder
* **DELETE** - to delete an asset or folder

>[!NOTE]
>
>The request body and/or URL parameters can be used to configure some of these operations; for example, define that a folder or an asset should be created by a **POST** request.

The exact format of supported requests is defined in the API Reference documentation. 

### Transactional Behavior {#transactional-behavior}

All requests are atomic.

This means that subsequent (`write`) requests cannot be combined into a single transaction that could succeed or fail as a single entity.

### Security {#security}

If the Assets REST API is used within an environment without specific authentication requirements, AEM's CORS filter needs to be configured correctly.

>[!NOTE]
>
>For further information see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For further information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (i.e. folders or assets with renditions), as it relates to the children of the requested entity.

#### Example: Paging {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Entity Types {#entity-types}

### Folders {#folders}

Folders act as containers for assets and other folders. They reflect the structure of the AEM content repository.

The Assets REST API exposes access to the properties of a folder; for example its name, title, etc. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## API HTTP de ativos e fragmentos de conteúdo {#assets-http-api-content-fragments}

Os fragmentos de conteúdo são usados para entrega headless e são um tipo especial de ativo. Eles são usados para acessar dados estruturados, como textos, números, datas, entre outros.

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, i.e. the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, etc. are part of the definition.

To create a new content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## Uso da API REST de ativos {#using-aem-assets-rest-api}

### Acesso {#access}

A API REST de ativos usa o ponto de acesso `/api/assets` e necessita do caminho do ativo para acessá-lo (sem o `/content/dam` inicial).

* Isso significa que para acessar o ativo em:
   * `/content/dam/path/to/asset`
* Você precisa solicitar:
   * `/api/assets/path/to/asset`

Por exemplo, para acessar `/content/dam/wknd/en/adventures/cycling-tuscany`, solicite `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>O acesso por:
>
>* `/api/assets` **não** precisa da utilização do seletor `.model`.
>* `/content/path/to/page` **precisa** da utilização do seletor `.model`.


### Operação {#operation}

O método HTTP determina a operação a ser executada:

* **GET**: para recuperar uma representação JSON de um ativo ou uma pasta
* **POST**: para criar novos ativos ou pastas
* **PUT**: para atualizar as propriedades de um ativo ou pasta
* **DELETE**: para excluir um ativo ou pasta

>[!NOTE]
>
>O corpo da solicitação e/ou os parâmetros de URL podem ser usados para configurar algumas dessas operações; por exemplo, definir que uma pasta ou um ativo deve ser criado por uma solicitação **POST**.

O formato exato das solicitações compatíveis é definido na documentação de Referência da API.

O uso pode ser diferente dependendo se você está usando um ambiente de autor ou de publicação no AEM, juntamente com seu caso de uso específico.

* É altamente recomendável que a criação seja vinculada a uma instância de autor (e atualmente não há meios de replicar um fragmento para publicação usando essa API).
* A entrega é possível de ambos os ambientes, pois o AEM apresenta o conteúdo solicitado somente no formato JSON.

   * Armazenar e entregar a partir de uma instância de autor do AEM deve ser o suficiente para aplicativos de biblioteca de mídia por trás do firewall.

   * Para entrega em tempo real na web, recomenda-se uma instância de publicação do AEM.

>[!CAUTION]
>
>A configuração do dispatcher em instâncias AEM pode bloquear o acesso a `/api`.

>[!NOTE]
>
>Para obter mais detalhes, consulte a Referência da API. Em especial, a seção [API do Adobe Experience Manager Assets - Fragmentos de conteúdo](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html).

### Leitura/entrega {#read-delivery}

O uso é feito via:

`GET /{cfParentPath}/{cfName}.json`

Por exemplo:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

A resposta é em JSON serializado e o conteúdo é estruturado de acordo com o fragmento de conteúdo. As referências são fornecidas como URLs de referência.

Dois tipos de operações de leitura são possíveis:

* Ao ler um fragmento de conteúdo específico por caminho, a representação JSON do fragmento de conteúdo é retornada.
* Leitura de uma pasta de fragmentos de conteúdo por caminho: retorna as representações JSON de todos os fragmentos de conteúdo contidos na pasta.

### Criar {#create}

O uso é feito via:

`POST /{cfParentPath}/{cfName}`

O corpo deve conter uma representação JSON do fragmento de conteúdo a ser criado, incluindo qualquer conteúdo inicial que deve ser definido nos elementos do fragmento de conteúdo. É obrigatório definir a propriedade `cq:model` e ela deve apontar para um modelo de fragmento de conteúdo válido. Se isso não for feito, haverá um erro. Também é necessário adicionar um cabeçalho `Content-Type` definido como `application/json`.

### Atualizar o {#update}

O uso é feito via

`PUT /{cfParentPath}/{cfName}`

O corpo deve conter uma representação JSON referente ao que deve ser atualizado para o fragmento de conteúdo especificado.

Isso pode ser simplesmente o título ou a descrição de um fragmento de conteúdo, um único elemento ou todos os valores e/ou metadados do elemento.

### Excluir {#delete}

O uso é feito via:

`DELETE /{cfParentPath}/{cfName}`

Para obter mais detalhes sobre o uso da API REST do AEM Assets, consulte:

* API HTTP do Adobe Experience Manager Assets (recursos adicionais)
* Compatibilidade com fragmentos de conteúdo na API HTTP do AEM Assets (recursos adicionais)

## O que vem a seguir {#whats-next}

Agora que concluiu esta parte da jornada de desenvolvedores headless do AEM, você deve:

* Entender as noções básicas sobre a API HTTP do AEM Assets.
* Entender como os fragmentos de conteúdo são compatíveis com essa API.

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page isn't going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

Você deve continuar sua jornada sem periféricos de AEM revisando o documento em seguida [Como ativar seu aplicativo sem periféricos](go-live.md) onde você leva seu AEM projeto Headless ao vivo!

## Recursos adicionais {#additional-resources}

* [API HTTP de ativos](/help/assets/mac-api-assets.md)
* [API REST de fragmentos de conteúdo](/help/assets/assets-api-content-fragments.md)
   * [Referência da API ](/help/assets/assets-api-content-fragments.md#api-reference)
* [API do Adobe Experience Manager Assets - Fragmentos de conteúdo](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)
* [Trabalho com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
* [Componentes principais do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)
* [Explicação sobre o CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html?lang=pt-BR)
* [Vídeo - Desenvolvimento do CORS com o AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html?lang=pt-BR)
