---
title: Saiba como usar GraphQL com AEM - Conteúdo de amostra e consultas
description: Saiba como usar o GraphQL com AEM para fornecer conteúdo headless, explorando conteúdo de amostra e consultas.
feature: Content Fragments,GraphQL API
exl-id: 91c5f61c-9c15-4d72-9b9b-0c23f31e7cdc
source-git-commit: 1a3d5a6b3b4f7af67d6a62cdaab484daa536cb63
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Saiba como usar GraphQL com AEM - Conteúdo de amostra e consultas {#learn-graphql-with-aem-sample-content-queries}

Saiba como usar o GraphQL com AEM para fornecer conteúdo headless, explorando conteúdo de amostra e consultas.

>[!NOTE]
>
>Esta página deve ser lida junto com:
>
>* [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
>* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
>* [AEM API GraphQL para uso com Fragmentos de conteúdo](/help/assets/content-fragments/graphql-api-content-fragments.md)


Para começar a usar consultas GraphQL e como elas funcionam com AEM Fragmentos do conteúdo, é útil ver alguns exemplos práticos.

Para ajudar com isso, consulte:

* A [estrutura do fragmento de conteúdo de amostra](#content-fragment-structure-graphql)

* E alguns [exemplo de consultas GraphQL](#graphql-sample-queries), com base na estrutura do fragmento de conteúdo de amostra (Modelos de fragmento de conteúdo e Fragmentos de conteúdo relacionados).


## GraphQL - Consultas de exemplo usando a estrutura do fragmento de conteúdo de amostra {#graphql-sample-queries-sample-content-fragment-structure}

Consulte essas consultas de amostra para obter ilustrações de criação de consultas, junto com resultados de amostra.

>[!NOTE]
>
>Dependendo do seu caso, você pode acessar diretamente o [Interface GraphiQL incluída na API GraphQL AEM](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) para enviar e testar consultas.
>
>Por exemplo: `http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>As consultas de amostra são baseadas na variável [Estrutura de fragmento de conteúdo de amostra para uso com GraphQL](#content-fragment-structure-graphql)

### Consulta de exemplo - Todos os esquemas e tipos de dados disponíveis {#sample-all-schemes-datatypes}

Isso retornará tudo `types` para todos os schemas disponíveis.

**Exemplo de consulta**

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

**Resultado da amostra**

```xml
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### Consulta de exemplo - Todas as informações sobre todas as cidades {#sample-all-information-all-cities}

Para recuperar todas as informações sobre todas as cidades, você pode usar a query muito básica:
**Exemplo de consulta**

```xml
{
  cityList {
    items
  }
}
```

Quando executado, o sistema expandirá automaticamente a consulta para incluir todos os campos:

```xml
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### Consulta de exemplo - Nomes de todas as cidades {#sample-names-all-cities}

Esta é uma consulta simples para retornar a variável `name`de todas as entradas no `city`esquema.

**Exemplo de consulta**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### Exemplo de consulta - Um único fragmento de cidade específico {#sample-single-specific-city-fragment}

Esta é uma consulta para retornar os detalhes de uma única entrada de fragmento em um local específico no repositório.

**Exemplo de consulta**

```xml
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### Consulta de exemplo - Todas as cidades com uma variável nomeada {#sample-cities-named-variation}

Se você criar uma nova variação, chamada &quot;Centro de Berlim&quot; (`berlin_centre`), para o `city` Berlim, então você pode usar uma query para retornar detalhes da variação.

**Exemplo de consulta**

```xml
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### Exemplo de consulta - Detalhes completos do CEO e funcionários de uma empresa {#sample-full-details-company-ceos-employees}

Usando a estrutura dos fragmentos aninhados, esse query retorna os detalhes completos do CEO de uma empresa e de todos os seus funcionários.

**Exemplo de consulta**

```xml
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### Consulta de amostra - Todas as pessoas com o nome de &quot;Trabalhos&quot; ou &quot;Smith&quot; {#sample-all-persons-jobs-smith}

Isso filtrará tudo `persons` para qualquer que tenha o nome `Jobs`ou `Smith`.

**Exemplo de consulta**

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### Consulta de Amostra - Todas as Pessoas que não têm um nome de &quot;Trabalhos&quot; {#sample-all-persons-not-jobs}

Isso filtrará tudo `persons` para qualquer que tenha o nome `Jobs`ou `Smith`.

**Exemplo de consulta**

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### Consulta de Amostra - Todas as Aventuras `_path` está começando com um prefixo específico {#sample-wknd-all-adventures-cycling-path-filter}

Todos `adventures` em que `_path` começa com um prefixo específico (`/content/dam/wknd/en/adventures/cycling`).

**Exemplo de consulta**

```xml
query {
  adventureList(
    filter: {
      _path: {
        _expressions: [
        {
          value: "/content/dam/wknd/en/adventures/cycling"
         _operator: STARTS_WITH
        }]
       }
    })
    {
    items {
      _path
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-southern-utah/cycling-southern-utah"
        },
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-tuscany/cycling-tuscany"
        }
      ]
    }
  }
}
```

### Exemplo de consulta - Todas as cidades localizadas na Alemanha ou na Suíça com uma população entre 400000 e 999999 {#sample-all-cities-d-ch-population}

Aqui, uma combinação de campos é filtrada. Um `AND` (implícito) é usado para selecionar a variável `population`intervalo, enquanto um `OR` (explícito) é usado para selecionar as cidades necessárias.

**Exemplo de consulta**

```xml
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### Consulta de exemplo - Todas as cidades com SAN no nome, independentemente do caso {#sample-all-cities-san-ignore-case}

Esta consulta interroga todas as cidades que têm `SAN` no nome, independentemente do caso.

**Exemplo de consulta**

```xml
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### Consulta de amostra - Filtrar em uma matriz com um item que deve ocorrer pelo menos uma vez {#sample-array-item-occur-at-least-once}

Essa consulta filtra em uma matriz com um item (`city:na`) que deve ocorrer pelo menos uma vez.

**Exemplo de consulta**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Consulta de exemplo - Filtrar em um valor de matriz exato {#sample-array-exact-value}

Essa consulta filtra em um valor de matriz exato.

**Exemplo de consulta**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Exemplo de consulta para fragmentos de conteúdo aninhados - Todas as empresas que têm pelo menos um funcionário com o nome &quot;Smith&quot; {#sample-companies-employee-smith}

Esta consulta ilustra a filtragem de qualquer `person` de `name` &quot;Smith&quot;, retornando informações de dois fragmentos aninhados - `company` e `employee`.

**Exemplo de consulta**

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### Exemplo de consulta para fragmentos de conteúdo aninhados - Todas as empresas nas quais todos os funcionários ganharam o prêmio &quot;Gamestar&quot; {#sample-all-companies-employee-gamestar-award}

Esta consulta ilustra a filtragem em três fragmentos aninhados - `company`, `employee`e `award`.

**Exemplo de consulta**

```xml
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
        awards {
          id
          title
        }
      }
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### Exemplo de consulta para metadados - Lista os metadados para prêmios denominados GB {#sample-metadata-awards-gb}

Esta consulta ilustra a filtragem em três fragmentos aninhados - `company`, `employee`e `award`.

**Exemplo de consulta**

```xml
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## Exemplos de consultas usando o projeto WKND {#sample-queries-using-wknd-project}

Essas consultas de amostra são baseadas no projeto WKND. Isso tem:

* Modelos de fragmentos do conteúdo disponíveis em:
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Fragmentos de conteúdo (e outro conteúdo) disponíveis em:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>Como os resultados podem ser extensos, eles não são reproduzidos aqui.

### Consulta de amostra para todos os Fragmentos de conteúdo de um determinado modelo com as propriedades especificadas {#sample-wknd-all-model-properties}

Este exemplo de consulta interroga:

* para todos os Fragmentos de conteúdo do tipo `article`
* com o `path`e `author` propriedades.

**Exemplo de consulta**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### Exemplo de consulta para metadados {#sample-wknd-metadata}

Esta consulta interroga:

* para todos os Fragmentos de conteúdo do tipo `adventure`
* metadados

**Exemplo de consulta**

```xml
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### Exemplo de consulta para um único fragmento de conteúdo de um determinado modelo {#sample-wknd-single-content-fragment-of-given-model}

Este exemplo de consulta interroga:

* para um único Fragmento de conteúdo do tipo `article` em um caminho específico
   * dentro desse conteúdo, todos os formatos de conteúdo:
      * HTML
      * Markdown
      * Texto sem formatação
      * JSON

**Exemplo de consulta**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### Exemplo de consulta para um modelo de fragmento de conteúdo de um modelo {#sample-wknd-content-fragment-model-from-model}

Este exemplo de consulta interroga:

* para um único Fragmento de conteúdo
   * detalhes do modelo de fragmento de conteúdo subjacente

**Exemplo de consulta**

```xml
{
  adventureByPath(_path: "/content/dam/wknd/en/adventures/riverside-camping-australia/riverside-camping-australia") {
    item {
      _path
      adventureTitle
      _model {
        _path
        title
      }
    }
  }
}
```

### Exemplo de consulta para um fragmento de conteúdo aninhado - Tipo de modelo único{#sample-wknd-nested-fragment-single-model}

Esta consulta interroga:

* para um único Fragmento de conteúdo do tipo `article` em um caminho específico
   * dentro disso, o caminho e o autor do fragmento referenciado (aninhado)

>[!NOTE]
>
>O campo `referencearticle` tem o tipo de dados `fragment-reference`.

**Exemplo de consulta**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### Exemplo de consulta para um fragmento de conteúdo aninhado - Tipo de modelo múltiplo{#sample-wknd-nested-fragment-multiple-model}

Esta consulta interroga:

* para vários Fragmentos de conteúdo do tipo `bookmark`
   * com referências de fragmento a outros fragmentos dos tipos de modelo específicos `article` e `adventure`

>[!NOTE]
>
>O campo `fragments` tem o tipo de dados `fragment-reference`, com os modelos `Article`, `Adventure` selecionado.

```xml
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### Consulta de amostra para um fragmento de conteúdo de um modelo específico com referências de conteúdo{#sample-wknd-fragment-specific-model-content-reference}

Há dois sabores deste query:

1. Para retornar todas as referências de conteúdo.
1. Para retornar as referências de conteúdo específicas do tipo `attachments`.

Essas consultas interrogam:

* para vários Fragmentos de conteúdo do tipo `bookmark`
   * com referências de conteúdo a outros fragmentos

#### Exemplo de consulta para vários fragmentos de conteúdo com referências previamente buscadas {#sample-wknd-multiple-fragments-prefetched-references}

A consulta a seguir retorna todas as referências de conteúdo usando `_references`:

```xml
{
  bookmarkList {
     _references {
         ... on ImageRef {
          _path
          type
          height
        }
        ... on MultimediaRef {
          _path
          type
          size
        }
        ... on DocumentRef {
          _path
          type
          author
        }
        ... on ArchiveRef {
          _path
          type
          format
        }
    }
    items {
        _path
    }
  }
}
```

#### Exemplo de consulta para vários fragmentos de conteúdo com anexos {#sample-wknd-multiple-fragments-attachments}

A consulta a seguir retorna todos `attachments` - um campo específico (subgrupo) de tipo `content-reference`:

>[!NOTE]
>
>O campo `attachments` tem o tipo de dados `content-reference`, com vários formulários selecionados.

```xml
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### Exemplo de consulta para um único fragmento de conteúdo com referência em linha do RTE {#sample-wknd-single-fragment-rte-inline-reference}

Esta consulta interroga:

* para um único Fragmento de conteúdo do tipo `bookmark` em um caminho específico
   * dentro disso, referências em linha do RTE

>[!NOTE]
>
>As referências em linha do RTE são hidratadas em `_references`.

**Exemplo de consulta**

```xml
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### Consulta de amostra para uma única variação do Fragmento de conteúdo de um determinado modelo {#sample-wknd-single-fragment-given-model}

Esta consulta interroga:

* para um único Fragmento de conteúdo do tipo `article` em um caminho específico
   * nesse contexto, os dados relativos à variação: `variation1`

**Exemplo de consulta**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Exemplo de consulta para uma variação nomeada de vários fragmentos de conteúdo de um determinado modelo {#sample-wknd-variation-multiple-fragment-given-model}

Esta consulta interroga:

* para Fragmentos de conteúdo do tipo `article` com uma variação específica: `variation1`

**Exemplo de consulta**

```xml
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Consulta de amostra para vários Fragmentos de conteúdo de uma determinada localidade {#sample-wknd-multiple-fragments-given-locale}

Esta consulta interroga:

* para Fragmentos de conteúdo do tipo `article` no `fr` locale

**Exemplo de consulta**

```xml
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

## A estrutura do fragmento de conteúdo de amostra (usada com GraphQL) {#content-fragment-structure-graphql}

As consultas de amostra são baseadas na seguinte estrutura, que usa:

* Uma ou mais, [Modelos de fragmento do conteúdo de amostra](#sample-content-fragment-models-schemas) - servir de base para os esquemas GraphQL

* [Fragmentos de conteúdo de amostra](#sample-content-fragments) com base nos modelos acima referidos

### Modelos de fragmento do conteúdo de amostra (esquemas) {#sample-content-fragment-models-schemas}

Para consultas de amostra, usaremos os seguintes Modelos de conteúdo e suas interrelações (referências ->):

* [Empresa](#model-company)
-> [Pessoa](#model-person)
    -> [Prêmio](#model-award)

* [Cidade](#model-city)

#### Empresa {#model-company}

Os campos básicos que definem a empresa são:

| Nome do campo | Tipo de dados | Referência |
|--- |--- |--- |
| Nome da empresa | Texto em linha única |  |
| CEO | Referência do fragmento (único) | [Person](#model-person) |
| Empregados | Referência do fragmento (vários campos) | [Pessoa](#model-person) |

#### Person {#model-person}

Os campos que definem uma pessoa, que também pode ser um funcionário:

| Nome do campo | Tipo de dados | Referência |
|--- |--- |--- |
| Nome | Texto em linha única |  |
| Nome | Texto em linha única |  |
| Prêmios | Referência do fragmento (vários campos) | [Prêmio](#model-award) |

#### Prêmio {#model-award}

Os campos que definem um prêmio são:

| Nome do campo | Tipo de dados | Referência |
|--- |--- |--- |
| Atalho/ID | Texto em linha única |  |
| Título | Texto em linha única |  |

#### Cidade {#model-city}

Os campos para definir uma cidade são:

| Nome do campo | Tipo de dados | Referência |
|--- |--- |--- |
| Nome | Texto em linha única |  |
| País | Texto em linha única |  |
| População | Número |  |
| Categorias | Tags |  |

### Fragmentos de conteúdo de amostra {#sample-content-fragments}

Os fragmentos a seguir são usados para o modelo apropriado.

#### Empresa {#fragment-company}

| Nome da empresa | CEO | Empregados |
|--- |--- |--- |
| Apple | Steve Jobs | Duke Marsh<br>Max Caulfield |
|  Little Pony Inc. | Adam Smith | Lara Croft<br>Deslizamento do Cortador |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### Pessoa {#fragment-person}

| Nome | Nome | Prêmios |
|--- |--- |--- |
| Lincoln |  Abe |  |
| Smith | Adam |   |
| Barra |  Cortador |  Gameblitz<br>Gamestar |
| Marsh |  Duke |   |   |
|  Smith |  Joe |   |
| Corte |  Lara | Gamestar |
| Caulfield |  Máximo |  Gameblitz |
|  Tarefas |  Steve |   |

#### Prêmio {#fragment-award}

| Atalho/ID | Título |
|--- |--- |
| GB | Gameblitz |
|  GS | Gamestar |
|  OSC | Oscar |

#### Cidade {#fragment-city}

| Nome | País | População | Categorias |
|--- |--- |--- |--- |
| Basileia | Suíça | 172258 | cidade:emea |
| Berlim | Alemanha | 3669491 | cidade:capital<br>cidade:emea |
| Bucareste | Romênia | 1821000 |  cidade:capital<br>cidade:emea |
| São Francisco |  EUA |  883306 |  cidade:praia<br>cidade:na |
| San Jose |  EUA |  102635 |  cidade:na |
| Stuttgart |  Alemanha |  634830 |  cidade:emea |
|  Zurique |  Suíça |  415367 |  cidade:capital<br>cidade:emea |
