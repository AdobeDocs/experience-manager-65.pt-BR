---
title: API GraphQL do AEM para uso com Fragmentos de conteúdo
description: Saiba como usar Fragmentos de conteúdo no Adobe Experience Manager (AEM) com a API do AEM GraphQL para entrega de conteúdo headless.
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: 452813cf50110b515c181dba1ecbde4527808cfb
workflow-type: tm+mt
source-wordcount: '4796'
ht-degree: 52%

---

# API GraphQL do AEM para uso com Fragmentos de conteúdo {#graphql-api-for-use-with-content-fragments}

Saiba como usar Fragmentos de conteúdo no Adobe Experience Manager (AEM) com a API do AEM GraphQL para entrega de conteúdo headless.

A API do GraphQL do AEM usada com Fragmentos de conteúdo é altamente baseada na API padrão de código aberto do GraphQL.

Usar a API GraphQL no AEM permite a entrega eficiente dos Fragmentos de conteúdo aos clientes JavaScript em implementações CMS headless:

* Evitando solicitações de API iterativas como com REST,
* Garantindo que a entrega se limite aos requisitos específicos,
* Permitindo a entrega em massa exatamente daquilo que é necessário para a renderização, como resposta a uma única consulta de API.

>[!NOTE]
>
>O GraphQL é usado em dois cenários (separados) no Adobe Experience Manager (AEM):
>
>* [O AEM Commerce consome dados de uma plataforma do Commerce por meio do GraphQL](/help/commerce/cif/integrating/magento.md).
>* Fragmentos de conteúdo do AEM trabalham em conjunto com a API GraphQL do AEM (uma implementação personalizada, com base no GraphQL padrão), para fornecer conteúdo estruturado para uso em seus aplicativos.

## Pré-requisitos {#prerequisites}

Os clientes que usam o GraphQL devem instalar o AEM Content Fragment with GraphQL Index Package 1.0.5. Consulte a [Notas de versão](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package) para obter mais detalhes.

## A API GraphQL {#graphql-api}

O GraphQL é:

* &quot;*...um idioma de consulta para APIs e um tempo de execução para realizar essas consultas com seus dados existentes. O GraphQL fornece uma descrição completa e compreensível dos dados em sua API. Ele dá aos clientes o poder de solicitar exatamente o que precisam e nada mais, facilita a evolução das APIs ao longo do tempo e habilita ferramentas avançadas de desenvolvedor.*&quot;.

  Consulte [GraphQL.org](https://graphql.org)

* &quot;*...uma especificação aberta para uma camada de API flexível. Coloque o GraphQL sobre seus back-end existentes para que você possa criar produtos mais rápido do que nunca....*&quot;.

  Consulte [Explorar GraphQL](https://graphql.com/).

* *&quot;...uma linguagem de consulta de dados e especificação desenvolvidas internamente pela Facebook em 2012, antes de serem disponibilizadas publicamente em 2015. Ele oferece uma alternativa às arquiteturas baseadas em REST, com o objetivo de aumentar a produtividade do desenvolvedor e minimizar as quantidades de dados transferidos. O GraphQL é usado na produção por centenas de organizações de todos os tamanhos...&quot;*

  Consulte [Fundação GraphQL](https://graphql.org/foundation).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all the tools they need to understand and adopt GraphQL.*". 
-->

Para obter mais informações sobre a API do GraphQL, consulte as seguintes seções (entre muitos outros recursos):

* Em [graphql.org](https://graphql.org):

   * [Introdução ao GraphQL](https://graphql.org/learn)

   * [A especificação GraphQL](https://spec.graphql.org/)

* Em [graphql.com](https://graphql.com):

   * [Tutoriais](https://graphql.com/tutorials/)


A implementação do GraphQL para AEM é baseada na Biblioteca GraphQL Java™ padrão. Consulte:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java™ no GitHub](https://github.com/graphql-java)

### Terminologia de GraphQL {#graphql-terminology}

O GraphQL usa o seguinte:

* **[Consultas](https://graphql.org/learn/queries/)**

* **[Esquemas e Tipos](https://graphql.org/learn/schema/)**:

   * Os esquemas são gerados pelo AEM com base nos modelos de fragmento de conteúdo.
   * Usando seus esquemas, o GraphQL apresenta os tipos e as operações permitidas no GraphQL para implementação no AEM.

* **[Campos](https://graphql.org/learn/queries/#fields)**

* **[Endpoint de GraphQL](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#graphql-aem-endpoint)**
   * O caminho no AEM que responde a consultas de GraphQL e fornece acesso aos esquemas de GraphQL.

   * Consulte [Habilitação do endpoint de GraphQL](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint) para obter mais detalhes.

Consulte a [Introdução ao GraphQL (GraphQL.org)](https://graphql.org/learn/) para obter detalhes abrangentes, incluindo as [Práticas recomendadas](https://graphql.org/learn/best-practices/).

### Tipos de consulta de GraphQL {#graphql-query-types}

Com o GraphQL, é possível executar consultas para retornar:

* Uma **entrada única**

* Uma **[lista de entradas](https://graphql.org/learn/schema/#lists-and-non-null)**

O AEM fornece recursos para converter consultas (ambos os tipos) em [Consultas persistentes](/help/sites-developing/headless/graphql-api/persisted-queries.md) que são armazenados em cache pelo Dispatcher e pelo CDN.

### Práticas recomendadas de consulta GraphQL (Dispatcher e CDN) {#graphql-query-best-practices}

[Consultas persistentes](/help/sites-developing/headless/graphql-api/persisted-queries.md) são o método recomendado para ser usado em instâncias de publicação como:

* são armazenadas em cache
* eles são gerenciados centralmente pelo AEM

<!-- is this fully accurate? -->
>[!NOTE]
>
>Normalmente, não há dispatcher/CDN no autor, portanto, não há ganho de desempenho ao usar consultas persistentes lá; além de testá-las.

As consultas GraphQL que utilizam solicitações POST não são recomendadas, pois não são armazenadas em cache. Portanto, em uma instância padrão, o Dispatcher é configurado para bloquear essas consultas.

Embora o GraphQL também seja compatível com solicitações GET, essas solicitações podem atingir limites (por exemplo, o comprimento do URL) que podem ser evitados usando consultas persistentes.

Consulte [Habilitar armazenamento em cache de consultas persistentes](#enable-caching-persisted-queries) para obter mais detalhes.

>[!NOTE]
>
>A capacidade de realizar consultas diretas pode se tornar obsoleta em algum momento no futuro.

## Interface GraphiQL {#graphiql-interface}

Uma implementação da norma [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) A interface do está disponível para uso com o AEM GraphQL.

>[!NOTE]
>
>O GraphiQL é incluído em todos os ambientes de AEM (mas só é acessível/visível quando você configura os endpoints).
>
>Em versões anteriores, você precisava de um pacote para instalar o GraphiQL IDE. Se você tiver esse pacote instalado, ele poderá ser removido.

Essa interface permite inserir e testar diretamente consultas.

Por exemplo:

* `http://localhost:4502/content/graphiql.html`

Ele fornece recursos como realce de sintaxe, preenchimento automático e sugestão automática, juntamente com um histórico e uma documentação online:

![Interface GraphiQL](assets/cfm-graphiql-interface.png "Interface GraphiQL")

>[!NOTE]
>
>Consulte [Uso do GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md).

## Casos de uso para ambientes de Autor e Publicação {#use-cases-author-publish-environments}

Os casos de uso podem depender do tipo de ambiente AEM:

* Ambiente de publicação; usado para:
   * Consultar dados para o aplicativo JS (caso de uso padrão)

* Ambiente de autor; usado para:
   * Consultar dados para “fins de gerenciamento de conteúdo”:
      * O GraphQL no AEM é uma API somente leitura.
      * A API REST pode ser usada para operações de CR(u)D.

## Permissões {#permission}

As permissões são necessárias para acessar o Assets.

As consultas do GraphQL são executadas com a permissão do usuário AEM da solicitação subjacente. Se o usuário não tiver acesso de leitura a alguns fragmentos (armazenados como Ativos), eles não se tornarão parte do conjunto de resultados.

Além disso, o usuário deve ter acesso a um endpoint do GraphQL para executar consultas do GraphQL.

## Geração de esquemas {#schema-generation}

O GraphQL é uma API tipificada, o que significa que os dados devem ser estruturados e organizados claramente por tipo.

A especificação GraphQL fornece uma série de diretrizes sobre como criar uma API robusta para interrogar dados em uma determinada instância. Para concluir essas diretrizes, um cliente deve buscar o [Esquema](#schema-generation), que contém todos os tipos necessários para uma query.

Para fragmentos de conteúdo, os esquemas de GraphQL (estrutura e tipos) são baseados em [modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) **habilitados** e seus tipos de dados.

>[!CAUTION]
>
>Todos os esquemas de GraphQL (derivados dos modelos de fragmento de conteúdo que foram **Habilitados**) são legíveis por meio do endpoint do GraphQL.
>
>Essa capacidade significa que você deve garantir que não haja dados confidenciais disponíveis, pois eles podem ser vazados dessa maneira. Por exemplo, inclui informações que podem estar presentes como nomes de campo na definição do modelo.

Por exemplo, se um usuário criar um modelo de fragmento de conteúdo chamado `Article`, o AEM gerará um `ArticleModel` do tipo GraphQL. Os campos desse tipo correspondem aos campos e tipos de dados definidos no modelo. Além disso, ele cria alguns pontos de entrada para as consultas que operam nesse tipo, como `articleByPath` ou `articleList`.

1. Um modelo de fragmento de conteúdo:

   ![Modelo de fragmento de conteúdo para uso com GraphQL](assets/cfm-graphqlapi-01.png "Modelo de fragmento de conteúdo para uso com GraphQL")

1. O esquema de GraphQL correspondente (saída da documentação automática do GraphiQL):
   ![Esquema de GraphQL com base no modelo de fragmento de conteúdo](assets/cfm-graphqlapi-02.png "Esquema de GraphQL com base no modelo de fragmento de conteúdo")

   Esta imagem mostra que o tipo gerado `ArticleModel` contém vários [campos](#fields).

   * Três deles foram controlados pelo usuário: `author`, `main`, e `referencearticle`.

   * Os outros campos foram adicionados automaticamente pelo AEM e representam métodos úteis para fornecer informações sobre um determinado fragmento de conteúdo. Neste exemplo, (a variável [campos auxiliares](#helper-fields)) `_path`, `_metadata`, `_variations`.

1. Depois que um usuário cria um fragmento de conteúdo com base no modelo de Artigo, ele pode ser interrogado por meio do GraphQL. Para obter exemplos, consulte [Exemplos de consulta](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#graphql-sample-queries) (baseado em uma [amostra da estrutura do fragmento de conteúdo para uso com GraphQL](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).

No GraphQL para AEM, o esquema é flexível. Essa flexibilidade significa que ela é gerada automaticamente sempre que um modelo de fragmento de conteúdo é criado, atualizado ou excluído. Os caches do esquema de dados também são atualizados quando você atualiza um modelo de fragmento de conteúdo.

O serviço GraphQL do Sites acompanha (em segundo plano) quaisquer modificações feitas em um modelo de fragmento de conteúdo. Quando as atualizações são detectadas, somente essa parte do esquema é gerada novamente. Essa otimização economiza tempo e oferece estabilidade.

Por exemplo, se você:

1. Instalar um pacote contendo `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. Tipos de GraphQL para `Model-1` e `Model-2` são gerados.

1. Em seguida, o `Content-Fragment-Model-2` é modificado:

   1. Somente o `Model-2` O tipo de GraphQL é atualizado.

   1. Considerando `Model-1` continua a mesma.

>[!NOTE]
>
>É importante observar esses detalhes caso queira fazer atualizações em massa nos modelos de fragmento de conteúdo por meio da API REST ou de outra maneira.

O esquema é distribuído por meio do mesmo endpoint das consultas de GraphQL, com o cliente lidando com o fato de que o esquema é chamado com a extensão `GQLschema`. Por exemplo, executar uma `GET` solicitação em `/content/cq:graphql/global/endpoint.GQLschema` resulta na saída do schema com o tipo de conteúdo: `text/x-graphql-schema;charset=iso-8859-1`.

### Geração de esquema - Modelos não publicados {#schema-generation-unpublished-models}

Quando os fragmentos de conteúdo são aninhados, pode acontecer que um modelo de fragmento de conteúdo principal seja publicado, mas um modelo referenciado não.

>[!NOTE]
>
>A interface de usuário do AEM impede que isso aconteça, mas se a publicação for feita de forma programática ou com pacotes de conteúdo, isso poderá ocorrer.

Quando isso acontece, o AEM gera um *incompleto* Esquema para o modelo de fragmento de conteúdo principal. Isso significa que a referência do fragmento, que depende do modelo não publicado, é removida do esquema.

## Campos {#fields}

Dentro do esquema, há campos individuais de duas categorias básicas:

* Campos gerados.

  Uma seleção de [Tipos de dados](#data-types) é usada para criar campos com base em como você configura o modelo de fragmento de conteúdo. Os nomes de campo são retirados do campo **Nome da propriedade** do **Tipo de dados**.

   * Há também a **Renderizar como** configuração a ser considerada, pois os usuários podem configurar determinados tipos de dados. Por exemplo, um campo de texto de linha única pode ser configurado para conter vários textos de linha única, escolhendo `multifield` na lista suspensa.

* O GraphQL para AEM também gera vários [campos auxiliares](#helper-fields).

  Esses campos são usados para identificar um fragmento de conteúdo ou obter mais informações sobre ele.

### Tipos de dados {#data-types}

O GraphQL do AEM oferece suporte a uma lista de tipos. Todos os tipos de dados do modelo de fragmento de conteúdo compatíveis e os tipos de GraphQL correspondentes são representados:

| Modelo de fragmento de conteúdo - Tipo de dados | Tipo de GraphQL | Descrição |
|--- |--- |--- |
| Texto em linha única | `String`, `[String]` |  Usado para sequências de caracteres simples, como nomes de autor e nomes de localização. |
| Texto multilinha | `String` |  Usado para saída de texto, como o corpo de um artigo |
| Número |  `Float`, `[Float]` | Usado para exibir números de ponto flutuantes e números regulares |
| Booleano |  `Boolean` |  Usado para exibir caixas de seleção → declarações simples de verdadeiro/falso |
| Data e hora | `Calendar` |  Usado para exibir data e hora em um formato ISO 8086. Dependendo do tipo selecionado, há três opções disponíveis para uso no GraphQL do AEM: `onlyDate`, `onlyTime` e `dateTime` |
| Enumeração |  `String` |  Usado para exibir uma opção de uma lista de opções definidas na criação do modelo |
|  Tags |  `[String]` |  Usado para exibir uma lista de sequências de caracteres que representam tags usadas no AEM |
| Referência de conteúdo |  `String` |  Usado para exibir o caminho para outro ativo no AEM |
| Referência do fragmento |  *Um tipo de modelo* <br><br>Campo único: `Model` - Tipo de modelo, referenciado diretamente <br><br>Vários campos, com um tipo referenciado: `[Model]` - Matriz de tipo `Model`, referenciado diretamente do array <br><br>Vários campos, com vários tipos referenciados: `[AllFragmentModels]` - Matriz de todos os tipos de modelo, referenciada da matriz com tipo de união |  Usado para fazer referência a um ou mais Fragmentos de conteúdo de determinados Tipos de modelo, definidos quando o modelo foi criado |

{style="table-layout:auto"}

### Campos auxiliares {#helper-fields}

Além dos tipos de dados para campos gerados pelo usuário, o GraphQL para AEM também gera vários *auxiliar* campos para ajudar a identificar um fragmento de conteúdo ou para fornecer informações adicionais sobre um fragmento de conteúdo.

Esses [campos auxiliares](#helper-fields) estão marcados com um `_` precedente, para distinguir entre o que foi definido pelo usuário e o que foi gerado automaticamente.

#### Caminho {#path}

O campo de caminho é usado como um identificador no GraphQL do AEM. Ele representa o caminho do ativo Fragmento de conteúdo dentro do repositório do AEM. Esse caminho é escolhido como o identificador de um fragmento de conteúdo, pois ele:

* é exclusivo dentro do AEM,
* pode ser buscado facilmente.

O código a seguir exibe os caminhos de todos os fragmentos de conteúdo que foram criados com base no modelo de fragmento de conteúdo `Person`.

```graphql
{
  personList {
    items {
      _path
    }
  }
}
```

Para recuperar um único Fragmento de conteúdo de um tipo específico, você também deve determinar seu caminho primeiro. Por exemplo:

```graphql
{
  authorByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

Consulte [Exemplo de consulta - um único fragmento específico de cidade](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

#### Metadados {#metadata}

Por meio do GraphQL, o AEM também expõe os metadados de um Fragmento de conteúdo. Os metadados são as informações que descrevem um fragmento de conteúdo, como o seguinte:

* o título de um fragmento de conteúdo
* o caminho da miniatura
* a descrição de um fragmento de conteúdo
* e a data de criação, entre outras.

Como os metadados são gerados por meio do Editor de esquemas e, como tal, não têm uma estrutura específica, o GraphQL tipo `TypedMetaData` foi implementado para expor os metadados de um Fragmento de conteúdo. A variável `TypedMetaData` expõe as informações agrupadas pelos seguintes tipos escalares:

| Texto |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

Cada tipo escalar representa um único par de nome-valor ou uma matriz de pares de nome-valor, em que o valor desse par é do tipo em que foi agrupado.

Por exemplo, se você quiser recuperar o título de um fragmento de conteúdo, essa propriedade será uma propriedade de sequência; portanto, consulte todos os metadados de sequência:

Para consultar metadados:

```graphql
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

É possível exibir todos os tipos de metadados GraphQL, se você exibir o esquema GraphQL gerado. Todos os tipos de modelo têm o mesmo `TypedMetaData`.

>[!NOTE]
>
>**Diferença entre metadados normais e de matriz**
>Lembre-se que `StringMetadata` e `StringArrayMetadata` se referem ao que é armazenado no repositório, não a como você os recupera.
>
>Por exemplo, ao chamar a variável `stringMetadata` recebe uma matriz de todos os metadados armazenados no repositório como um `String`. E se você chamar `stringArrayMetadata`, você receberá uma matriz de todos os metadados armazenados no repositório como `String[]`.

Consulte [Exemplo de consulta para metadados - listar os metadados para prêmios denominados GB](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

#### Variações {#variations}

O campo `_variations` foi implementado para simplificar a consulta das variações que um Fragmento de conteúdo possui. Por exemplo:

```graphql
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

>[!NOTE]
>
>A variável `_variations` o campo não contém um `master` variação, uma vez que tecnicamente os dados originais (referenciados *Principal* na interface) não é considerada uma variação explícita.

Consulte [Exemplo de consulta - todas as cidades com uma variável nomeada](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-cities-named-variation).

>[!NOTE]
>
>Se a variação fornecida não existir para um fragmento de conteúdo, os dados originais (também conhecidos como variação principal) serão retornados como um padrão (fallback).

<!--
## Security Considerations {#security-considerations}
-->

## Variáveis GraphQL {#graphql-variables}

O GraphQL permite que as variáveis sejam colocadas na consulta. Para obter mais informações, consulte [Documentação do GraphQL para variáveis](https://graphql.org/learn/queries/#variables).

Por exemplo, para obter todos os Fragmentos de conteúdo do tipo `Article` que tenham uma variação específica, é possível especificar a variável `variation` no GraphiQL.

![Variáveis GraphQL](assets/cfm-graphqlapi-03.png "Variáveis GraphQL")

```graphql
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
            _variations
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## Diretivas GraphQL {#graphql-directives}

No GraphQL, há uma possibilidade de alterar o query com base em variáveis, chamadas de Diretivas do GraphQL.

Por exemplo, é possível incluir o campo `adventurePrice` em uma consulta para todos os `AdventureModels`, com base em uma variável `includePrice`.

![Diretivas do GraphQL](assets/cfm-graphqlapi-04.png "Diretivas do GraphQL")

```graphql
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## Filtragem {#filtering}

Também é possível usar a filtragem em consultas de GraphQL para retornar dados específicos.

A filtragem usa uma sintaxe baseada em operadores lógicos e expressões.

A menor parte é uma expressão única que pode ser aplicada ao conteúdo de um determinado campo. Ela compara o conteúdo do campo com um determinado valor constante.

Por exemplo, a expressão a seguir compararia o conteúdo do campo com o valor `some text`e terão êxito se o conteúdo for igual ao valor. Caso contrário, a expressão falhará.:

```graphql
{
  value: "some text"
  _op: EQUALS
}
```

Os operadores a seguir podem ser usados para comparar campos com um determinado valor:

| Operador | Tipos | A expressão será bem-sucedida se... |
|--- |--- |--- |
| `EQUALS` | `String`, `ID`, `Boolean` | ... o valor é igual ao conteúdo do campo |
| `EQUALS_NOT` | `String`, `ID` | ...o valor *não* for igual ao conteúdo do campo |
| `CONTAINS` | `String` | ... o conteúdo do campo contém o valor (`{ value: "mas", _op: CONTAINS }` corresponde a `Christmas`, `Xmas`, `master`, ...) |
| `CONTAINS_NOT` | `String` | ...o conteúdo do campo *não* contiver o valor |
| `STARTS_WITH` | `ID` | ... a ID começa com um determinado valor (`{ value: "/content/dam/", _op: STARTS_WITH` corresponde a `/content/dam/path/to/fragment`, mas não `/namespace/content/dam/something` |
| `EQUAL` | `Int`, `Float` | ... o valor é igual ao conteúdo do campo |
| `UNEQUAL` | `Int`, `Float` | ...o valor *não* for igual ao conteúdo do campo |
| `GREATER` | `Int`, `Float` | ...o conteúdo do campo for maior que o valor |
| `GREATER_EQUAL` | `Int`, `Float` | ...o conteúdo do campo for maior ou igual ao valor |
| `LOWER` | `Int`, `Float` | ...o conteúdo do campo for menor que o valor |
| `LOWER_EQUAL` | `Int`, `Float` | ...o conteúdo do campo for menor ou igual ao valor |
| `AT` | `Calendar`, `Date`, `Time` | ... o conteúdo do campo é o mesmo que o valor (incluindo a configuração de fuso horário) |
| `NOT_AT` | `Calendar`, `Date`, `Time` | ...o conteúdo do campo *não* for igual ao valor |
| `BEFORE` | `Calendar`, `Date`, `Time` | ...o ponto no tempo indicado pelo valor for anterior ao ponto no tempo indicado pelo conteúdo do campo |
| `AT_OR_BEFORE` | `Calendar`, `Date`, `Time` | ...o ponto no tempo indicado pelo valor for anterior ou igual ao ponto no tempo indicado pelo conteúdo do campo |
| `AFTER` | `Calendar`, `Date`, `Time` | ...o ponto no tempo indicado pelo valor for posterior ao ponto no tempo indicado pelo conteúdo do campo |
| `AT_OR_AFTER` | `Calendar`, `Date`, `Time` | ...o ponto no tempo indicado pelo valor for posterior ou igual ao ponto no tempo indicado pelo conteúdo do campo |

Alguns tipos também permitem especificar opções adicionais que modificam como uma expressão é avaliada:

| Opção | Tipos | Descrição |
|--- |--- |--- |
| `_ignoreCase` | `String` | Ignora a capitalização de uma cadeia de caracteres, por exemplo, um valor de `time` corresponde a `TIME`, `time`, `tImE`, ... |
| `_sensitiveness` | `Float` | Permite uma certa margem para que valores `float` sejam considerados iguais (para contornar limitações técnicas devido à representação interna de valores `float`; deve ser evitada, pois essa opção pode ter um impacto negativo no desempenho |

As expressões podem ser combinadas a um conjunto com a ajuda de um operador lógico (`_logOp`):

* `OR` - o conjunto de expressões terá êxito se pelo menos uma expressão tiver êxito
* `AND` - o conjunto de expressões terá êxito se todas as expressões tiverem êxito (padrão)

Cada campo pode ser filtrado por seu próprio conjunto de expressões. Os conjuntos de expressões de todos os campos mencionados no argumento de filtro são eventualmente combinados por seu próprio operador lógico.

Uma definição de filtro (transmitida como o argumento `filter` para uma consulta) contém:

* Uma subdefinição para cada campo (o campo pode ser acessado por meio de seu nome; por exemplo, há uma `lastName` no filtro para o `lastName` no Tipo de dados (campo)
* Cada subdefinição contém a variável `_expressions` , fornecendo o conjunto de expressões e a variável `_logOp` campo que define o operador lógico com o qual as expressões devem ser combinadas
* Cada expressão é definida pelo valor (campo `value`) e o operador (campo `_operator`) com o qual o conteúdo de um campo deve ser comparado

Você pode omitir `_logOp` se quiser combinar itens com `AND` e `_operator` se quiser verificar a igualdade, pois esses valores são padrões.

O exemplo a seguir demonstra uma consulta completa que filtra todas as pessoas que têm um `lastName` igual a `Provo` ou que contêm `sjö`, independentemente do caso:

```graphql
{
  authorList(filter: {
    lastname: {
      _logOp: OR
      _expressions: [
        {
          value: "sjö",
          _operator: CONTAINS,
          _ignoreCase: true
        },
        {
          value: "Provo"
        }
      ]
    }
  }) {
    items {
      lastName
      firstName
    }
  }
}
```

Ao executar uma consulta GraphQL usando variáveis opcionais, se um valor específico for **não** fornecida para a variável opcional, então a variável será ignorada na avaliação do filtro. Isso significa que os resultados da consulta conterão todos os valores, ambos `null` e não `null`, para a propriedade relacionada à variável de filtro.

>[!NOTE]
>
>Se um `null` o valor é *explicitamente* especificado para essa variável, o filtro só corresponderá `null` valores para a propriedade correspondente.

Por exemplo, na consulta abaixo, onde nenhum valor é especificado para a propriedade `lastName`:

```graphql
query getAuthorsFilteredByLastName($authorLastName: String) {
  authorList(filter:
    {
      lastName: {_expressions: {value: $authorLastName}
      }}) {
    items {
      lastName
    }
  }
}
```

Todos os autores serão retornados:

```graphql
{
  "data": {
    "authorList": {
      "items": [
        {
          "lastName": "Hammer"
        },
        {
          "lastName": "Provo"
        },
        {
          "lastName": "Wester"
        },
        {
          "lastName": null
        },
         ...
      ]
    }
  }
}
```

Embora também seja possível filtrar em campos aninhados, isso não é recomendado, pois pode causar problemas de desempenho.

Para obter mais exemplos, consulte:

* detalhes da [GraphQL para extensões do AEM](#graphql-extensions)

* [Exemplos de consulta usando esta amostra de conteúdo e estrutura](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * E a [amostra de conteúdo e estrutura](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql) preparada para uso em consultas de exemplo

* [Exemplos de consulta com base no projeto WKND](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## Classificação {#sorting}

>[!NOTE]
>
>Para obter o melhor desempenho, considere [Atualização dos fragmentos de conteúdo para paginação e classificação na filtragem do GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md).

Esse recurso permite classificar os resultados da consulta de acordo com um campo especificado.

Os critérios de classificação são:

* é uma lista de valores separados por vírgulas que representa o caminho do campo
   * o primeiro campo na lista define a ordem de classificação principal
      * o segundo campo é usado se dois valores do critério de classificação principal forem iguais
      * o terceiro campo é usado se os dois primeiros critérios forem iguais e assim por diante.
   * notação pontilhada, ou seja, `field1.subfield.subfield`e assim por diante.
* com uma direção de ordem opcional
   * ASC (crescente) ou DESC (decrescente); como padrão, ASC é aplicado
   * a direção pode ser especificada por campo; essa capacidade significa que você pode classificar um campo em ordem crescente, outro em ordem decrescente (nome, nome DESC)

Por exemplo:

```graphql
query {
  authorList(sort: "lastName, firstName") {
    items {
      firstName
      lastName
    }
  }
}
```

E também:

```graphql
{
  authorList(sort: "lastName DESC, firstName DESC") {
    items {
        lastName
        firstName
    }
  }
}
```

Também é possível classificar um campo dentro de um fragmento aninhado, usando o formato de `nestedFragmentname.fieldname`.

>[!NOTE]
>
>Este formato pode ter um impacto negativo no desempenho.

Por exemplo:

```graphql
query {
  articleList(sort: "authorFragment.lastName")  {
    items {
      title
      authorFragment {
        firstName
        lastName
        birthDay
      }
      slug
    }
  }
}
```

## Paginação {#paging}

>[!NOTE]
>
>Para obter o melhor desempenho, considere [Atualização dos fragmentos de conteúdo para paginação e classificação na filtragem do GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md).

Esse recurso permite executar a paginação em tipos de consulta que retornam uma lista. Dois métodos são fornecidos:

* `offset` e `limit` em uma consulta `List`
* `first` e `after` em uma consulta `Paginated`

### Consulta de lista - offset e limit {#list-offset-limit}

Em uma consulta de `...List` você pode usar `offset` e `limit` para retornar um subconjunto específico de resultados:

* `offset`: especifica o primeiro conjunto de dados a ser retornado
* `limit`: especifica o número máximo de conjuntos de dados a serem retornados

Por exemplo, para exibir uma página de resultados que contém até cinco artigos, começando do quinto artigo da lista de resultados *completa*:

```graphql
query {
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        lastName
        firstName
      }
    }
  }
}
```

<!-- When available link to BP and replace "JCR query level" with a more neutral term. -->

<!-- When available link to BP and replace "JCR query result set" with a more neutral term. -->

>[!NOTE]
>
>* A paginação exige uma ordem de classificação estável para funcionar corretamente em várias consultas que solicitam páginas diferentes do mesmo conjunto de resultados. Por padrão, ele usa o caminho do repositório de cada item do conjunto de resultados para garantir que a ordem seja sempre a mesma. Se uma ordem de classificação diferente for usada e se essa classificação não puder ser feita no nível de consulta JCR, haverá um impacto negativo no desempenho. O motivo é que todo o conjunto de resultados deve ser carregado na memória antes que as páginas sejam determinadas.
>
>* Quanto maior o deslocamento, mais tempo leva para ignorar os itens do conjunto completo de resultados da consulta JCR. Uma solução alternativa para grandes conjuntos de resultados é usar a consulta paginada com os métodos `first` e `after`.

### Consulta paginada - first e after {#paginated-first-after}

O tipo de consulta `...Paginated` reutiliza a maioria dos recursos do tipo de consulta `...List` (filtragem, classificação), mas, em vez de usar os argumentos `offset`/`limit`, ele usa os argumentos `first`/`after`, definidos pela [Especificação de conexões do cursor GraphQL](https://relay.dev/graphql/connections.htm). Você pode encontrar uma introdução mais simplificada na [Introdução ao GraphQL](https://graphql.org/learn/pagination/#pagination-and-edges).

* `first`: os primeiros `n` itens a serem retornados.
O padrão é `50`.
O máximo é `100`.
* `after`: o cursor que determina o início da página solicitada. O item representado pelo cursor não está incluído no conjunto de resultados. O cursor de um item é determinado pela variável `cursor` do campo `edges` estrutura.

Por exemplo, exibe uma página de resultados contendo até cinco aventuras, começando pelo item de cursor especificado na lista de resultados *completa*:

```graphql
query {
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            title
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

<!-- When available link to BP -->
<!-- Due to internal technical constraints, performance will degrade if sorting and filtering is applied on nested fields. Therefore it is recommended to use filter/sort fields stored at root level. For more information, see the [Best Practices document](link). -->

>[!NOTE]
>
>* Por padrão, a paginação usa a UUID do nó do repositório que representa o fragmento para ordenação, garantindo que a ordem dos resultados seja sempre a mesma. Quando `sort` é usado, o UUID será usado implicitamente para garantir uma ordem de classificação exclusiva, mesmo para dois itens com chaves de classificação idênticas.
>
>* Devido a restrições técnicas internas, o desempenho será reduzido se a classificação e a filtragem forem aplicadas em campos aninhados. Portanto, use os campos de filtro/classificação armazenados no nível raiz. Essa técnica também é a maneira recomendada se você quiser consultar grandes conjuntos de resultados paginados.

## Consultas persistentes do GraphQL - ativação do armazenamento em cache no Dispatcher {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>Se o armazenamento em cache no Dispatcher estiver ativado, a variável [Filtro CORS](#cors-filter) não é necessária e, portanto, essa seção pode ser ignorada.

O armazenamento em cache de consultas persistentes não é ativado por padrão no Dispatcher. A ativação padrão não é possível, pois os clientes que usam CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens) precisam revisar e possivelmente atualizar a configuração do Dispatcher.

>[!NOTE]
>
>O Dispatcher não armazena em cache os `Vary` cabeçalho.
>
>O armazenamento em cache de outros cabeçalhos relacionados ao CORS pode ser habilitado no Dispatcher, mas pode ser insuficiente quando há várias origens do CORS.

### Habilitar armazenamento em cache de consultas persistentes {#enable-caching-persisted-queries}

Para habilitar o armazenamento em cache de consultas persistentes, as seguintes atualizações para os arquivos de configuração do Dispatcher são necessárias:

* `<conf.d/rewrites/base_rewrite.rules>`

  ```xml
  # Allow the dispatcher to be able to cache persisted queries - they need an extension for the cache file
  RewriteCond %{REQUEST_URI} ^/graphql/execute.json
  RewriteRule ^/(.*)$ /$1;.json [PT] 
  ```

  >[!NOTE]
  >
  >O Dispatcher adiciona o sufixo `.json` para todos os URLS de consulta persistentes, para que o resultado possa ser armazenado em cache.
  >
  >Isso garante que a consulta esteja em conformidade com os requisitos do Dispatcher para documentos que podem ser armazenados em cache. Para obter mais detalhes, consulte [Como o Dispatcher retorna documentos?](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html#how-does-the-dispatcher-return-documents%3F)

* `<conf.dispatcher.d/filters/ams_publish_filters.any>`

  ```xml
  # Allow GraphQL Persisted Queries & preflight requests
  /0110 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
  ```

### Configuração do CORS no Dispatcher {#cors-configuration-in-dispatcher}

Clientes que usam solicitações do CORS podem precisar revisar e atualizar sua configuração do CORS no Dispatcher.

* A variável `Origin` O cabeçalho não deve ser transmitido para a publicação do AEM por meio do Dispatcher:
   * Verifique a `clientheaders.any` arquivo.
* Em vez disso, as solicitações do CORS devem ser avaliadas para as origens permitidas no nível do Dispatcher. Essa abordagem também garante que os cabeçalhos relacionados ao CORS sejam definidos corretamente, em um local, em todos os casos.
   * Essa configuração deve ser adicionada à variável `vhost` arquivo. Um exemplo de configuração é fornecido abaixo; para simplificar, somente a parte relacionada ao CORS foi fornecida. Você pode adaptá-la aos seus casos de uso específicos.

  ```xml
  <VirtualHost *:80>
     ServerName "publish"
  
     # ...
  
     <IfModule mod_headers.c>
         Header add X-Vhost "publish"
  
          ################## Start of the CORS specific configuration ##################
  
          SetEnvIfExpr "req_novary('Origin') == ''"  CORSType=none CORSProcessing=false
          SetEnvIfExpr "req_novary('Origin') != ''"  CORSType=cors CORSProcessing=true CORSTrusted=false
  
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') == '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=invalidpreflight CORSProcessing=false
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') != '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=preflight CORSProcessing=true CORSTrusted=false
          SetEnvIfExpr "req_novary('Origin') -strcmatch 'https://%{HTTP_HOST}*'"  CORSType=samedomain CORSProcessing=false
  
          # For requests that require CORS processing, check if the Origin can be trusted
          SetEnvIfExpr "%{HTTP_HOST} =~ /(.*)/ " ParsedHost=$1
  
          ################## Adapt the regex to match CORS origin for your environment
          SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*.your-domain.tld(:\d+)?$)#" CORSTrusted=true
  
          # Extract the Origin header 
          SetEnvIfNoCase ^Origin$ ^https://(.*)$ CORSTrustedOrigin=https://$1
  
          # Flush If already set
          Header unset Access-Control-Allow-Origin
          Header unset Access-Control-Allow-Credentials
  
          # Trusted
          Header always set Access-Control-Allow-Credentials "true" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Origin "%{CORSTrustedOrigin}e" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Methods "GET" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Max-Age 1800 "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Headers "Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers" "expr=reqenv('CORSTrusted') == 'true'"
  
          # Non-CORS or Not Trusted
          Header unset Access-Control-Allow-Credentials "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Origin "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Methods "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Max-Age "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
  
          # Always vary on origin, even if its not there.
          Header merge Vary Origin
  
          # CORS - send 204 for CORS requests which are not trusted
          RewriteCond expr "reqenv('CORSProcessing') == 'true' && reqenv('CORSTrusted') == 'false'"
          RewriteRule "^(.*)" - [R=204,L]
  
          ################## End of the CORS specific configuration ##################
  
     </IfModule>
  
     <Directory />
  
         # ...
  
     </Directory>
  
     # ...
  
  </VirtualHost>
  ```

## GraphQL para AEM - resumo das extensões {#graphql-extensions}

A operação básica de consultas com o GraphQL para AEM adere à especificação GraphQL padrão. Para consultas do GraphQL com AEM, há algumas extensões:

* Se você precisar de um único resultado:
   * use o nome do modelo; por exemplo, cidade

* Se você espera uma lista de resultados:
   * adicione `List` ao nome do modelo; por exemplo, `cityList`
   * Consulte [Exemplo de consulta - Todas as informações sobre todas as cidades](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-information-all-cities)

  É possível:

   * [Classificar os resultados](#sorting)

      * `ASC`: crescente
      * `DESC`: decrescente

   * Retorna uma página de resultados usando uma dessas duas opções:

      * [Uma consulta de lista com “offset” e “limit”](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#list-offset-limit)
      * [Uma consulta paginada com “first” e “after”](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#paginated-first-after)
   * Consulte [Exemplo de consulta - Todas as informações sobre todas as cidades](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-information-all-cities)

* O filtro `includeVariations` está incluído na variável `List` tipo de consulta. Para recuperar as Variações do fragmento de conteúdo nos resultados da consulta, a variável `includeVariations` o filtro deve ser definido como `true`.

  >[!CAUTION]
  >O filtro `includeVariations` não pode ser usado junto com o campo gerado pelo sistema `_variation`.

* Se quiser usar um operador OR lógico:
   * use ` _logOp: OR`
   * Consulte [Exemplo de consulta - Todas as pessoas cujo nome é “Jobs” ou “Smith”](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-persons-jobs-smith)

* O operador AND lógico também existe, mas está (muitas vezes) implícito

* Você pode consultar nos nomes de campos que correspondem aos campos no modelo de fragmento de conteúdo
   * Consulte [Exemplo de consulta - Detalhes completos do CEO e dos funcionários de uma empresa](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-full-details-company-ceos-employees)

* Além dos campos do modelo, há alguns campos gerados pelo sistema (precedidos por um sublinhado):

   * Para conteúdo:

      * `_locale` : para revelar a língua; com base no Gerenciador de idiomas
         * Consulte [Exemplo de consulta para vários fragmentos de conteúdo de uma determinada localidade](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-given-locale)

      * `_metadata` : para revelar metadados do fragmento
         * Consulte [Exemplo de consulta para metadados - Listar os metadados para prêmios denominados como GB](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-metadata-awards-gb)

      * `_model` : permite a consulta para um modelo de fragmento de conteúdo (caminho e título)
         * Consulte [Exemplo de consulta para um modelo de fragmento de conteúdo de um modelo](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-content-fragment-model-from-model)

      * `_path` : o caminho para o fragmento de conteúdo no repositório
         * Consulte [Exemplo de consulta - Um único fragmento de cidade específico](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)

      * `_reference` : para revelar referências; incluindo referências em linha no Editor de Rich Text
         * Consulte [Exemplo de consulta para vários fragmentos de conteúdo com referências previamente buscadas](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-prefetched-references)

      * `_variation` : para revelar variações específicas no fragmento de conteúdo

        >[!NOTE]
        >
        >Se a variação especificada não existir para um Fragmento de conteúdo, a variação principal será retornada como padrão (fallback).

        >[!CAUTION]
        >O campo `_variation` gerado pelo sistema não pode ser usado junto com o filtro `includeVariations`.

         * Consulte [Exemplo de consulta - Todas as cidades com uma variação nomeada](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-cities-named-variation)

      * `_tags` : para revelar as IDs dos Fragmentos de conteúdo ou Variações que contêm tags; esta lista é uma matriz de `cq:tags` identificadores.

         * Consulte [Exemplo de consulta - Nomes de todas as cidades marcadas como Cidades para passeio](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-names-all-cities-tagged-city-breaks)
         * Consulte [Exemplo de consulta para variações de fragmento de conteúdo de um determinado modelo que tem uma tag específica anexada](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-fragment-variations-given-model-specific-tag)

        >[!NOTE]
        >
        >As tags também podem ser consultadas listando os metadados de um fragmento de conteúdo.

   * E operações:

      * `_operator` : aplica operadores específicos; `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS` e `STARTS_WITH`
         * Consulte [Exemplo de consulta - Todas as pessoas cujo nome não é “Jobs”](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-persons-not-jobs)
         * Consulte [Exemplo de consulta - Todas as aventuras em que o `_path` começa com um prefixo específico](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-all-adventures-cycling-path-filter)

      * `_apply` : para aplicar condições específicas; por exemplo, `AT_LEAST_ONCE`
         * Consulte [Exemplo de consulta - Filtrar em uma matriz com um item que deve ocorrer pelo menos uma vez](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-array-item-occur-at-least-once)

      * `_ignoreCase` : para ignorar se os caracteres são maiúsculos ou minúsculos ao consultar
         * Consulte [Exemplo de consulta - Todas as cidades com SAN no nome, independentemente de caracteres maiúsculos ou minúsculos](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-all-cities-san-ignore-case)

* Os tipos de união GraphQL são compatíveis:

   * use `... on`
      * Consulte [Exemplo de consulta para um fragmento de conteúdo de um modelo específico com uma referência de conteúdo](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-wknd-fragment-specific-model-content-reference)

* Fazer o fallback ao consultar fragmentos aninhados:

   * Se a variação solicitada não existir em um fragmento aninhado, a variável **Principal** a variação é retornada.

### Filtro CORS {#cors-filter}

>[!CAUTION]
>
>Se [o armazenamento em cache no Dispatcher foi ativado](#graphql-persisted-queries-enabling-caching-dispatcher) então, o filtro CORS não é necessário e, portanto, esta seção pode ser ignorada.

>[!NOTE]
>
>Para obter uma visão geral detalhada da política de compartilhamento de recursos do CORS no AEM, consulte [Entenda o CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=pt-BR#understand-cross-origin-resource-sharing-(cors)).

Para acessar o endpoint do GraphQL, configure uma política do CORS no repositório Git do cliente. Essa configuração é feita adicionando um arquivo de configuração OSGi CORS apropriado para um ou mais endpoints desejados.

Esta configuração deve especificar uma origem de site confiável `alloworigin` ou `alloworiginregexp` acesso deve ser concedido.

Por exemplo, para conceder acesso ao endpoint do GraphQL e ao endpoint de consultas persistentes para `https://my.domain` você pode usar:

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

Se você tiver configurado um caminho personalizado para o endpoint, também poderá usá-lo no `allowedpaths`.

### Filtro de referenciador {#referrer-filter}

Além da configuração do CORS, um filtro Referenciador deve ser configurado para permitir acesso de hosts de terceiros.

Esse filtro é feito adicionando um arquivo de configuração de Filtro referenciador OSGi apropriado que:

* especifica um nome de host de site confiável; `allow.hosts` ou `allow.hosts.regexp`
* concede acesso a esse nome de host.

Por exemplo, para conceder acesso a solicitações com o referenciador `my.domain`, é possível:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Continua a ser responsabilidade do cliente:
>
>* conceder acesso somente a domínios confiáveis
>* certificar-se de que nenhuma informação sensível seja exposta
>* não usar um curinga [*] sintaxe; essa funcionalidade desativa o acesso autenticado ao endpoint do GraphQL e também o expõe ao mundo inteiro.

>[!CAUTION]
>
>Toda os [esquemas](#schema-generation) de GraphQL (derivados de modelos de fragmento de conteúdo que foram **Habilitados**) são legíveis por meio do endpoint do GraphQL.
>
>Essa funcionalidade significa que você deve garantir que não haja dados confidenciais disponíveis, pois eles podem ser vazados dessa maneira. Por exemplo, inclui informações que podem estar presentes como nomes de campo na definição do modelo.

## Autenticação {#authentication}

Consulte [Autenticação para consultas de GraphQL remotas do AEM sobre fragmentos de conteúdo](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md).

## Perguntas frequentes {#faqs}

Perguntas que surgiram:

1. **P**: “*Qual a diferença entre a API GraphQL do AEM e a API do Construtor de consultas?*”

   * **R**: “*A API GraphQL do AEM oferece controle total sobre a saída em JSON e é um padrão do setor para consulta de conteúdo.
No futuro, o AEM planeja investir na API AEM GraphQL.*&quot;

## Tutorial - Introdução ao AEM Headless e GraphQL {#tutorial}

Procurando um tutorial prático? Veja o tutorial completo de [Introdução ao AEM Headless e GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=pt-BR) que ilustra como criar e expor conteúdo usando as APIs GraphQL do AEM e consumi-lo por meio de um aplicativo externo, em um cenário de CMS headless.
