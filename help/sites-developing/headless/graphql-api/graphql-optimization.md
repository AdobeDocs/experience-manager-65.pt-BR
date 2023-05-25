---
title: Otimização de consultas de GraphQL
description: Saiba como otimizar suas consultas do GraphQL ao filtrar, paginar e classificar os fragmentos de conteúdo no Adobe Experience Manager as a Cloud Service para entrega de conteúdo headless.
source-git-commit: 1481d613783089046b44d4652d38f7b4b16acc4d
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 58%

---


# Otimização de consultas de GraphQL {#optimizing-graphql-queries}

>[!NOTE]
>
>Antes de aplicar essas recomendações de otimização, considere [Atualização dos fragmentos de conteúdo para paginação e classificação na filtragem do GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) para obter o melhor desempenho.

Em uma instância do AEM com um alto número de fragmentos de conteúdo compartilhados pelo mesmo modelo, as consultas de lista do GraphQL podem se tornar caras (em termos de recursos).

O motivo é porque *all* os fragmentos que compartilham um modelo em uso na consulta do GraphQL devem ser carregados na memória. Isso consome tempo e memória. A filtragem, que pode reduzir o número de itens no conjunto de resultados (final), só pode ser aplicada **após** carregar todo o conjunto de resultados na memória.

Esse processo pode levar à impressão de que mesmo conjuntos de resultados pequenos (podem) resultam em mau desempenho. No entanto, na realidade, a lentidão é causada pelo tamanho do conjunto de resultados inicial, pois ele deve ser manipulado internamente antes que a filtragem possa ser aplicada.

Para reduzir os problemas de desempenho e memória, esse conjunto de resultados inicial deve ser mantido o menor possível.

O AEM fornece duas abordagens para a otimização de consultas de GraphQL:

* [Filtragem híbrida](#hybrid-filtering)
* [Paginação](#paging)

   * A [Classificação](#sorting) não está diretamente relacionada à otimização, mas à paginação

Cada abordagem tem seus próprios casos de uso e limitações. Este documento fornece informações sobre filtragem híbrida e paginação e contém algumas [práticas recomendadas](#best-practices) para otimizar as consultas de GraphQL.

## Filtragem híbrida {#hybrid-filtering}

A filtragem híbrida combina a filtragem do JCR com a filtragem do AEM.

Ela aplica um filtro do JCR (na forma de uma restrição de consulta) antes de carregar o conjunto de resultados na memória para a filtragem do AEM. Esse processo reduz o conjunto de resultados carregado na memória, pois o filtro JCR remove resultados supérfluos antecipadamente.

>[!NOTE]
>
>Por motivos técnicos (por exemplo, flexibilidade, aninhamento de fragmentos), o AEM não pode delegar toda a filtragem ao JCR.

Essa técnica mantém a flexibilidade que os filtros de GraphQL oferecem e delega o máximo possível da filtragem para o JCR.

## Paginação {#paging}

O GraphQL no AEM suporta dois tipos de paginação:

* [paginação baseada em limite/deslocamento](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
Esse tipo de paginação é usado para consultas de lista; essas consultas terminam com 
`List`; por exemplo, `articleList`.
Para usá-la, é preciso fornecer a posição do primeiro item a ser retornado (o `offset`) e o número de itens a serem retornados (o `limit` ou o tamanho da página).

* [paginação baseada em cursor](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after) (representante: `first`e `after`) Esse tipo de paginação fornece um identificador exclusivo para cada item; também conhecido como cursor.
Na consulta, você especifica o cursor do último item da página anterior, além do tamanho da página (o número máximo de itens a serem retornados).

   Como a paginação baseada em cursor não se encaixa nas estruturas de dados das consultas baseadas em lista, o AEM introduziu o tipo de consulta `Paginated`; por exemplo, `articlePaginated`. As estruturas de dados e os parâmetros utilizados seguem a [Especificação de conexão de cursores do GraphQL](https://relay.dev/graphql/connections.htm).

   >[!NOTE]
   >
   >Atualmente, o AEM é compatível com a paginação para a frente (usando os parâmetros `after`/`first`).
   >
   >A paginação para trás (usando os parâmetros `before`/`last`) não é compatível.

## Classificação {#sorting}

A classificação só poderá ser eficiente se todos os critérios de classificação estiverem relacionados a fragmentos de nível superior.

Se a ordem de classificação incluir um ou mais campos que estão em um fragmento aninhado, todos os fragmentos que compartilham o modelo de nível superior deverão ser carregados na memória. Esse fluxo causa um impacto negativo no desempenho.

>[!NOTE]
>
>A classificação em campos de nível superior também tem um impacto (embora pequeno) no desempenho.

## Práticas recomendadas     {#best-practices}

O principal objetivo de todas as otimizações é reduzir o conjunto de resultados inicial. As práticas recomendadas listadas aqui fornecem maneiras de se fazer isso. Elas podem (e devem) ser combinadas.

### Filtrar somente nas propriedades de nível superior {#filter-top-level-properties-only}

Atualmente, a filtragem no nível do JCR funciona somente para fragmentos de nível superior.

Se um filtro aborda os campos de um fragmento aninhado, o AEM precisa recorrer ao carregamento (na memória) de todos os fragmentos que compartilham o modelo subjacente.

Você ainda pode otimizar essas consultas do GraphQL combinando expressões de filtro em campos de fragmentos de nível superior e em campos de fragmentos aninhados com o [Operador AND](#logical-operations-in-filter-expressions).

### Usar a estrutura de conteúdo {#use-content-structure}

No AEM, é considerada uma boa prática usar a estrutura do repositório para restringir o escopo do conteúdo a ser processado.

Aplique essa abordagem a consultas do GraphQL aplicando um filtro no `_path` campo do fragmento de nível superior:

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>O `/` à direita de `value` é necessário para obter o melhor desempenho.

### Usar paginação {#use-paging}

Também é possível usar a paginação para reduzir o conjunto de resultados inicial, especialmente se suas solicitações não usarem filtragem e classificação.

Se você filtrar ou classificar fragmentos aninhados, as consultas paginadas ainda poderão ficar lentas, pois o AEM ainda deverá carregar quantidades maiores de fragmentos na memória. Portanto, se você combinar filtragem e paginação, considere as regras de filtragem (conforme mencionado acima).

Para a paginação, a classificação é igualmente importante, pois os resultados paginados são sempre classificados, seja de forma explícita ou implícita.

Se você estiver interessado principalmente em recuperar apenas as primeiras páginas, não há diferença significativa entre o uso das consultas `...List` ou `...Paginated`. No entanto, se o aplicativo estiver interessado em ler mais de uma ou duas páginas, considere usar a consulta `...Paginated`, pois ela tem um desempenho consideravelmente melhor com as páginas posteriores.

### Operações lógicas em expressões de filtro {#logical-operations-in-filter-expressions}

Se você estiver filtrando em fragmentos aninhados, ainda será possível aplicar a filtragem JCR fornecendo um filtro de acompanhamento em um campo de nível superior combinado usando o `AND` operador.

Um caso de uso típico é a restrição do escopo da consulta usando um filtro no `_path` do fragmento de nível superior. Em seguida, filtre por campos adicionais que podem estar no nível superior ou em um fragmento aninhado.

Nesse caso, as diferentes expressões de filtro seriam combinadas com `AND`. Portanto, o filtro no campo `_path` pode limitar efetivamente o conjunto de resultados inicial. Todos os outros filtros em campos de nível superior também podem ajudar a reduzir o conjunto de resultados inicial, desde que sejam combinados com `AND`.

Expressões de filtro combinadas com `OR` não podem ser otimizadas se fragmentos aninhados estiverem envolvidos. Tais `OR` expressões só podem ser otimizadas se *não* fragmentos aninhados estão envolvidos.

### Evite filtrar em campos de texto multilinha {#avoid-filtering-multiline-textfields}

Os campos de um campo de texto multilinha (html, markdown, texto simples, json) não podem ser filtrados por uma consulta JCR, pois o conteúdo desses campos deve ser calculado dinamicamente.

Se você ainda precisar filtrar em um campo de texto de várias linhas, considere limitar o tamanho do conjunto de resultados inicial adicionando expressões de filtro adicionais e combinando-as com `AND`. Limitar o escopo filtrando no campo `_path` também é uma boa abordagem.

### Evite filtrar em campos virtuais {#avoid-filtering-virtual-fields}

Os campos virtuais (a maioria dos campos que começam com `_`) são calculados enquanto uma consulta de GraphQL é executada e, portanto, estão fora do escopo da filtragem baseada em JCR.

Uma exceção importante é o campo `_path`, que pode ser usado efetivamente para reduzir o tamanho do conjunto de resultados inicial, se o conteúdo for estruturado de acordo (consulte [Usar a estrutura de conteúdo](#use-content-structure)).

### Filtragem: exclusões {#filtering-exclusions}

Há várias outras situações em que uma expressão de filtro não pode ser avaliada no nível do JCR (e, portanto, deve ser evitada para se obter o melhor desempenho):

* Filtrar expressões em um valor `Float` que usa a opção de filtro `_sensitiveness`, no qual `_sensitiveness` está definido como um valor diferente de `0.0`.

* Filtrar expressões em um valor `String` usando a opção de filtro `_ignoreCase`.

* Filtrar em valores `null`.

* Filtrar em matrizes com `_apply: ALL_OR_EMPTY`.

* Filtrar em matrizes com `_apply: INSTANCES` e `_instances: 0`.

* Filtrar expressões usando o operador `CONTAINS_NOT`.

* Filtrar expressões em um `Calendar`, `Date`ou `Time` valor que usa o `NOT_AT` operador.
