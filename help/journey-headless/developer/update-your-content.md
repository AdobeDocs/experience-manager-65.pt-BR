---
title: Como atualizar seu conteúdo por meio das APIs do AEM Assets
description: Nesta parte da Jornada do desenvolvedor sem cabeçalho AEM, saiba como usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo.
source-git-commit: 7f43d9d6b631b26f7b9293aa109498d0c8040436
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 2%

---

# Como atualizar seu conteúdo por meio das APIs do AEM Assets {#update-your-content}

Nesta parte do [AEM Jornada de desenvolvedor sem periféricos,](overview.md) saiba como usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo.

## A História Até Agora {#story-so-far}

No documento anterior da jornada sem cabeçalho AEM, [Como acessar seu conteúdo por meio AEM APIs de entrega](access-your-content.md) você aprendeu a acessar seu conteúdo headless no AEM por meio da API GraphQL AEM e agora deve:

* Ter um alto nível de compreensão do GraphQL.
* Entenda como a API GraphQL AEM funciona.
* Entenda algumas consultas práticas de amostra.

Este artigo se baseia nesses fundamentos para que você entenda como atualizar o conteúdo headless existente no AEM por meio da REST API.

## Objetivo {#objective}

* **Público**: Avançado
* **Objetivo**: Saiba como usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo:
   * Apresente a API HTTP do AEM Assets.
   * Apresente e discuta o suporte ao Fragmento de conteúdo na API.
   * Ilustre detalhes da API.

<!--
  * Look at sample code to see how things work in practice.
-->

## Por que você precisa da API HTTP de ativos para o fragmento de conteúdo {#why-http-api}

No estágio anterior da Jornada Sem cabeçalho, você aprendeu a usar a API GraphQL da AEM para recuperar o conteúdo usando consultas.

Então, por que outra API é necessária?

A API HTTP de ativos permite **Ler** seu conteúdo, mas também permite que você **Criar**, **Atualizar** e **Excluir** conteúdo - ações que não são possíveis com a API GraphQL.

A API REST de ativos está disponível em cada instalação pronta para uso de uma versão recente do Adobe Experience Manager.

## API HTTP de ativos {#assets-http-api}

A API HTTP de ativos abrange:

* API REST de ativos
* incluindo suporte para Fragmentos de conteúdo

A implementação atual da API HTTP de ativos é baseada no **REST** estilo de arquitetura e permite que você acesse o conteúdo (armazenado em AEM) por meio de **CRUD** operações (Criar, Ler, Atualizar, Excluir).

Com essa operação, a API permite operar o Adobe Experience Manager como um CMS (Content Management System) sem periféricos fornecendo serviços de conteúdo a um aplicativo front-end JavaScript. Ou qualquer outro aplicativo que possa executar solicitações HTTP e manipular respostas JSON. Por exemplo, Aplicativos de página única (SPA), baseados em estrutura ou personalizados, exigem conteúdo fornecido por meio de uma API, geralmente no formato JSON.

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

Fragmentos de conteúdo são usados para entrega sem cabeçalho, e um Fragmento de conteúdo é um tipo especial de ativo. Eles são usados para acessar dados estruturados, como textos, números, datas, entre outros.

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

A API REST de ativos usa o `/api/assets` endpoint e requer o caminho do ativo para acessá-lo (sem a `/content/dam`).

* Isso significa que para acessar o ativo em:
   * `/content/dam/path/to/asset`
* Você precisa solicitar:
   * `/api/assets/path/to/asset`

Por exemplo, para acessar `/content/dam/wknd/en/adventures/cycling-tuscany`, solicitação `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Acesso ao:
>
>* `/api/assets` **não** a utilização da `.model` seletor.
>* `/content/path/to/page` **does** exigir a utilização da `.model` seletor.


### Operação {#operation}

O método HTTP determina a operação a ser executada:

* **GET** - para recuperar uma representação JSON de um ativo ou uma pasta
* **POST** - para criar novos ativos ou pastas
* **PUT** - para atualizar as propriedades de um ativo ou pasta
* **DELETE** - para excluir um ativo ou pasta

>[!NOTE]
>
>O corpo da solicitação e/ou os parâmetros de URL podem ser usados para configurar algumas dessas operações; por exemplo, defina que uma pasta ou um ativo deve ser criado por um **POST** solicitação.

O formato exato das solicitações compatíveis é definido na documentação de Referência da API.

O uso pode ser diferente dependendo se você está usando um autor ou um ambiente de publicação AEM, juntamente com seu caso de uso específico.

* É altamente recomendável que a criação seja vinculada a uma instância do autor (e atualmente não há como replicar um fragmento para publicar usando essa API).
* A entrega é possível de ambos, pois AEM serve o conteúdo solicitado somente no formato JSON.

   * O armazenamento e o delivery de uma instância de autor de AEM devem ser suficientes para aplicativos de biblioteca de mídia por trás do firewall.

   * Para entrega na Web ao vivo, recomenda-se uma instância de publicação de AEM.

>[!CAUTION]
>
>A configuração do dispatcher em instâncias AEM pode bloquear o acesso a `/api`.

>[!NOTE]
>
>Para obter mais detalhes, consulte a Referência da API. Em especial, [API Adobe Experience Manager Assets - Fragmentos de conteúdo](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html).

### Leitura/entrega {#read-delivery}

O uso é via:

`GET /{cfParentPath}/{cfName}.json`

Por exemplo:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

A resposta é JSON serializado com o conteúdo estruturado como no fragmento de conteúdo. As referências são fornecidas como URLs de referência.

Dois tipos de operações de leitura são possíveis:

* Ao ler um fragmento de conteúdo específico por caminho, a representação JSON do fragmento de conteúdo é retornada.
* Leitura de uma pasta de fragmentos de conteúdo por caminho: isso retorna as representações JSON de todos os fragmentos de conteúdo dentro da pasta.

### Criar {#create}

O uso é via:

`POST /{cfParentPath}/{cfName}`

O corpo deve conter uma representação JSON do fragmento de conteúdo a ser criado, incluindo qualquer conteúdo inicial que deve ser definido nos elementos do fragmento de conteúdo. É obrigatório definir a variável `cq:model` e deve apontar para um modelo de fragmento de conteúdo válido. Se isso não for feito, haverá um erro. Também é necessário adicionar um cabeçalho `Content-Type` que está definida como `application/json`.

### Atualizar {#update}

O uso é via

`PUT /{cfParentPath}/{cfName}`

O corpo deve conter uma representação JSON do que deve ser atualizado para o fragmento de conteúdo especificado.

Pode ser simplesmente o título ou a descrição de um fragmento de conteúdo, um único elemento ou todos os valores e/ou metadados do elemento.

### Excluir {#delete}

O uso é via:

`DELETE /{cfParentPath}/{cfName}`

Para obter mais detalhes sobre o uso da API REST do AEM Assets, consulte:

* API HTTP do Adobe Experience Manager Assets (Recursos adicionais)
* Suporte a fragmentos de conteúdo na API HTTP do AEM Assets (Recursos adicionais)

## O que vem a seguir {#whats-next}

Agora que você concluiu esta parte da Jornada de Desenvolvedores sem Cabeça da AEM, você deve:

* Entenda as noções básicas da API HTTP do AEM Assets.
* Entenda como os Fragmentos de conteúdo são compatíveis com essa API.

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page isn't going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

Você deve continuar sua jornada sem periféricos de AEM revisando o documento em seguida [Como ativar seu aplicativo sem periféricos](go-live.md) onde você leva seu AEM projeto Headless ao vivo!

## Recursos adicionais {#additional-resources}

* [API HTTP de ativos](/help/assets/mac-api-assets.md)
* [API REST de fragmentos de conteúdo](/help/assets/assets-api-content-fragments.md)
   * [Referência da API](/help/assets/assets-api-content-fragments.md#api-reference)
* [API Adobe Experience Manager Assets - Fragmentos de conteúdo](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)
* [Trabalho com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
* [Componentes principais do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)
* [Explicação do CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [Vídeo - Desenvolvimento do CORS com AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
