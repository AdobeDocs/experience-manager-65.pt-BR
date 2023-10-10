---
title: Otimização de consultas de GraphQL
description: Saiba como otimizar suas consultas do GraphQL ao filtrar, paginar e classificar os fragmentos de conteúdo no Adobe Experience Manager as a Cloud Service para entrega de conteúdo headless.
exl-id: 47d0570b-224e-4109-b94e-ccc369d7ac5f
source-git-commit: c0570d6c0d624d950ddbb5c0d2ce38ff7c3756a4
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 60%

---

# Otimização de consultas de GraphQL {#optimizing-graphql-queries}

>[!NOTE]
>
>Antes de aplicar essas recomendações de otimização, considere [Atualização dos fragmentos de conteúdo para paginação e classificação na filtragem do GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) para obter o melhor desempenho.

Essas diretrizes são fornecidas para ajudar a evitar problemas de desempenho com as consultas do GraphQL.

## Lista de verificação do GraphQL {#graphql-checklist}

A lista de verificação a seguir tem como objetivo ajudar você a otimizar a configuração e o uso do GraphQL no Adobe Experience Manager (AEM) as a Cloud Service.

### Primeiros princípios {#first-principles}

#### Usar consultas persistentes do GraphQL {#use-persisted-graphql-queries}

**Recomendação**

O uso de consultas persistentes do GraphQL é altamente recomendado.

As consultas persistentes do GraphQL ajudam a reduzir o desempenho da execução da consulta utilizando a Rede de entrega de conteúdo (CDN). Os aplicativos clientes solicitam consultas persistentes com solicitações GET para execução habilitada para fast edge.

**Referência adicional**

Consulte:

* [Consultas persistentes de GraphQL](/help/sites-developing/headless/graphql-api/persisted-queries.md).
* [Saiba como usar o GraphQL com o AEM - Exemplos de conteúdo e consultas](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md)

#### Instalar o pacote de índice do GraphQL {#install-graphql-index-package}

**Recomendação**

Clientes que usam o GraphQL *deve* instale o Fragmento de conteúdo do Experience Manager com o pacote de indexação do GraphQL. Isso permite adicionar a definição de índice necessária com base nos recursos que eles realmente usam. A falha na instalação deste pacote pode resultar em consultas lentas ou com falha do GraphQL.

Consulte as Notas de versão da versão apropriada para seu Service Pack. Por exemplo, para obter o Service Pack mais recente, consulte [Instalar pacote de índice do GraphQL para fragmentos de conteúdo do Experience Manager](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package) .

>[!NOTE]
>
>Instale esse pacote apenas uma vez por instância; ele não precisa ser reinstalado com cada Service Pack.

**Referência adicional**
Consulte:

* [Instalar pacote de índice do GraphQL para fragmentos de conteúdo do Experience Manager](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package)

### Estratégia de cache {#cache-strategy}

Vários métodos de armazenamento em cache também podem ser usados para otimização.

#### Ativar o armazenamento em cache do AEM Dispatcher {#enable-aem-dispatcher-caching}

**Recomendação**

[Dispatcher AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) é o cache de primeiro nível no serviço AEM, antes do cache CDN.

**Referência adicional**

Consulte:

* [Consultas persistentes do GraphQL - ativação do armazenamento em cache no Dispatcher](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphql-persisted-queries-enabling-caching-dispatcher)

#### Usar uma rede de entrega de conteúdo (CDN) {#use-cdn}

**Recomendação**

As consultas do GraphQL e suas respostas JSON podem ser armazenadas em cache se direcionadas como `GET` solicitações ao usar um CDN. Por outro lado, as solicitações não armazenadas em cache podem ser muito caras (recursos) e de processamento lento, com potencial para efeitos prejudiciais adicionais nos recursos da origem.

**Referência adicional**

Consulte:

* [Uso da CDN no AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR#using-dispatcher-with-a-cdn)

#### Definir cabeçalhos de controle de cache HTTP {#set-http-cache-control-headers}

**Recomendação**

Ao usar consultas persistentes do GraphQL com um CDN, é recomendável definir cabeçalhos de controle de cache HTTP apropriados.

Cada consulta persistente pode ter seu próprio conjunto específico de cabeçalhos de controle de cache. Os cabeçalhos podem ser definidos no [API do GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md).

<!-- or the [AEM GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache). 
-->

**Referência adicional**

Consulte:

* [Armazenamento em cache de consultas persistentes](/help/sites-developing/headless/graphql-api/persisted-queries.md#caching-persisted-queries)
<!--
* [Managing cache for your persisted queries](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache)
-->

<!--
#### Use AEM GraphQL pre-caching {#use-aem-graphql-pre-caching}

**Recommendation**

This capability allows AEM to further cache content within the scope of GraphQL queries that can then be assembled as blocks in JSON output rather than line by line. 

**Further Reference**

Please contact Adobe to enable this capability for your AEM Cloud Service program and environments. 
-->

### Otimização de consulta do GraphQL {#graphql-query-optimization}

Em uma instância do AEM com um alto número de fragmentos de conteúdo que compartilham o mesmo modelo, as consultas de lista de GraphQL podem se tornar caras (em termos de recursos).

Isso ocorre porque *todos* os fragmentos que compartilham um modelo que está sendo usado na consulta de GraphQL devem ser carregados na memória. Isso consome tempo e memória. A filtragem, que pode reduzir o número de itens no conjunto de resultados (final), só pode ser aplicada **após** carregar todo o conjunto de resultados na memória.

Isso pode causar a impressão de que até mesmo pequenos conjuntos de resultados podem resultar em baixo desempenho. No entanto, na realidade, a lentidão é causada pelo tamanho do conjunto de resultados inicial, pois ele deve ser manipulado internamente antes que a filtragem possa ser aplicada.

Para reduzir os problemas de desempenho e memória, esse conjunto de resultados inicial deve ser mantido o menor possível.

O AEM fornece duas abordagens para a otimização de consultas de GraphQL:

* [Filtragem híbrida](#use-aem-graphql-hybrid-filtering)
* [Paginação](#use-aem-graphql-pagination)

   * A [Classificação](#use-graphql-sorting) não está diretamente relacionada à otimização, mas à paginação

Cada abordagem tem seus próprios casos de uso e limitações. Esta seção fornece informações sobre Filtragem e Paginação Híbrida, juntamente com alguns dos [práticas recomendadas](#best-practices) para uso na otimização de consultas do GraphQL.

#### Usar filtragem híbrida do AEM GraphQL {#use-aem-graphql-hybrid-filtering}

**Recomendação**

A filtragem híbrida combina a filtragem do JCR com a filtragem do AEM.

Ela aplica um filtro do JCR (na forma de uma restrição de consulta) antes de carregar o conjunto de resultados na memória para a filtragem do AEM. O objetivo é reduzir o conjunto de resultados carregado na memória, pois o filtro do JCR remove os resultados supérfluos.

>[!NOTE]
>
>Por motivos técnicos (por exemplo, flexibilidade e aninhamento de fragmentos), o AEM não pode delegar toda a filtragem ao JCR.

Essa técnica mantém a flexibilidade que os filtros de GraphQL oferecem e delega o máximo possível da filtragem para o JCR.

>[!NOTE]
>
>A filtragem híbrida de AEM requer a atualização dos fragmentos de conteúdo existentes

**Referência adicional**

Consulte:

* [Atualização dos fragmentos de conteúdo para paginação e classificação na filtragem do GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md)
* [Exemplo de consulta com filtragem por ID de _tags, excluindo variações](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

#### Usar paginação do GraphQL {#use-aem-graphql-pagination}

**Recomendação**

O tempo de resposta de consultas complexas, com grandes conjuntos de resultados, pode ser melhorado ao segmentar respostas em partes usando paginação, um padrão do GraphQL.

O GraphQL no AEM é compatível com dois tipos de paginação:

* [paginação baseada em limite/deslocamento](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
Isso é usado para consultas de lista; elas terminam com `List`; por exemplo, `articleList`.
Para usá-la, é preciso fornecer a posição do primeiro item a ser retornado (o `offset`) e o número de itens a serem retornados (o `limit` ou o tamanho da página).

* [paginação baseada em cursor](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after) (representada por `first` e `after`)
Ela fornece uma ID exclusiva para cada item; também conhecida como o cursor.
Na consulta, você especifica o cursor do último item da página anterior, além do tamanho da página (o número máximo de itens a serem retornados).

  Como a paginação baseada em cursor não se encaixa nas estruturas de dados das consultas baseadas em lista, o AEM introduziu o tipo de consulta `Paginated`; por exemplo, `articlePaginated`. As estruturas de dados e os parâmetros utilizados seguem a [Especificação de conexão de cursores do GraphQL](https://relay.dev/graphql/connections.htm).

  >[!NOTE]
  >
  >Atualmente, o AEM é compatível com a paginação para a frente (usando os parâmetros `after`/`first`).
  >
  >A paginação para trás (usando os parâmetros `before`/`last`) não é compatível.

**Referência adicional**

Consulte:

* [Exemplo de consulta de paginação usando primeiro e depois](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-pagination-first-after)

#### Usar classificação do GraphQL {#use-graphql-sorting}

**Recomendação**

Além de ser um padrão do GraphQL, a classificação permite que os clientes recebam conteúdo JSON em ordem de classificação. Isso pode reduzir a necessidade de processamento adicional no cliente.

A classificação só poderá ser eficiente se todos os critérios de classificação estiverem relacionados a fragmentos de nível superior.

Se a ordem de classificação incluir um ou mais campos localizados em um fragmento aninhado, todos os fragmentos que compartilham o modelo de nível superior deverão ser carregados na memória. Isso causa um impacto negativo no desempenho.

>[!NOTE]
>
>A classificação em campos de nível superior também tem um impacto (embora pequeno) no desempenho.

**Referência adicional**

Consulte:

* [Exemplo de consulta com filtragem por ID de _tags e exclusão de variações e classificação por nome](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

## Práticas recomendadas {#best-practices}

O principal objetivo de todas as recomendações de otimização é reduzir o conjunto de resultados inicial. As práticas recomendadas listadas aqui fornecem maneiras de se fazer isso. Elas podem (e devem) ser combinadas.

### Filtrar somente nas propriedades de nível superior {#filter-top-level-properties-only}

Atualmente, a filtragem no nível do JCR funciona somente para fragmentos de nível superior.

Se um filtro aborda os campos de um fragmento aninhado, o AEM precisa recorrer ao carregamento (na memória) de todos os fragmentos que compartilham o modelo subjacente.

Você ainda pode otimizar essas consultas de GraphQL combinando expressões de filtro em campos de fragmentos de nível superior, bem como aquelas em campos de fragmentos aninhados com o [operador AND](#logical-operations-in-filter-expressions).

### Usar a estrutura de conteúdo {#use-content-structure}

No AEM, geralmente é considerada uma boa prática usar a estrutura do repositório para restringir o escopo do conteúdo a ser processado.

Essa abordagem também deve ser aplicada às consultas de GraphQL.

Isso pode ser feito aplicando um filtro no campo `_path` do fragmento de nível superior:

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

Se você filtrar ou classificar fragmentos aninhados, as consultas paginadas ainda poderão ser lentas, pois é provável que o AEM ainda precisará carregar quantidades maiores de fragmentos na memória. Portanto, se você combinar filtragem e paginação, considere as regras de filtragem (conforme mencionado acima).

Para a paginação, a classificação é igualmente importante, pois os resultados paginados são sempre classificados, seja de forma explícita ou implícita.

Se você estiver interessado principalmente em recuperar apenas as primeiras páginas, não há diferença significativa entre o uso das consultas `...List` ou `...Paginated`. No entanto, se o aplicativo estiver interessado em ler mais de uma ou duas páginas, considere usar a consulta `...Paginated`, pois ela tem um desempenho consideravelmente melhor com as páginas posteriores.

### Operações lógicas em expressões de filtro {#logical-operations-in-filter-expressions}

Se estiver filtrando em fragmentos aninhados, você ainda poderá aplicar a filtragem do JCR fornecendo um filtro de acompanhamento em um campo de nível superior, o qual é combinado usando o operador `AND`.

Um caso de uso típico seria restringir o escopo da consulta usando um filtro no campo `_path` do fragmento de nível superior e, em seguida, filtrar por campos adicionais que podem estar no nível superior ou em um fragmento aninhado.

Nesse caso, as diferentes expressões de filtro seriam combinadas com `AND`. Portanto, o filtro no campo `_path` pode limitar efetivamente o conjunto de resultados inicial. Todos os outros filtros em campos de nível superior também podem ajudar a reduzir o conjunto de resultados inicial, desde que sejam combinados com `AND`.

Expressões de filtro combinadas com `OR` não podem ser otimizadas se fragmentos aninhados estiverem envolvidos. Expressões `OR` só podem ser otimizadas se *nenhum* fragmento aninhado estiver envolvido.

### Evite filtrar em campos de texto multilinha {#avoid-filtering-multiline-textfields}

Os campos de um texto multilinha (HTML, markdown, texto simples, JSON) não podem ser filtrados por uma consulta do JCR, pois o conteúdo desses campos deve ser calculado dinamicamente.

Se ainda precisar filtrar em um campo de texto multilinha, considere limitar o tamanho do conjunto de resultados inicial adicionando expressões de filtro adicionais e combinando-as com `AND`. Limitar o escopo filtrando no campo `_path` também é uma boa abordagem.

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

* Filtrar expressões em um valor `Calendar`, `Date` ou `Time` que usa o operador `NOT_AT`.

### Minimizar aninhamento de fragmento de conteúdo {#minimize-content-fragment-nesting}

O aninhamento de fragmentos de conteúdo é uma ótima maneira de modelar estruturas de conteúdo personalizadas. Você pode até ter um fragmento com um fragmento aninhado, que tenha um fragmento aninhado, que tenha... e assim por diante.

No entanto, criar uma estrutura com muitos níveis pode aumentar os tempos de processamento de uma consulta do GraphQL, pois o GraphQL precisa percorrer toda a hierarquia de todos os fragmentos de conteúdo aninhados.

O aninhamento profundo também pode ter efeitos adversos na governança de conteúdo. Em geral, é recomendável limitar o aninhamento do Fragmento de conteúdo a menos de cinco ou seis níveis.

### Não produzir todos os formatos (elementos de texto multilinha) {#do-not-output-all-formats}

O AEM GraphQL pode retornar texto, criado no **[Texto multilinha](/help/assets/content-fragments/content-fragments-models.md#data-types)** tipo de dados, em vários formatos: Rich Text, Texto simples e Markdown.

A saída de todos os três formatos aumenta o tamanho da saída de texto em JSON por um fator de três. Isso, combinado com conjuntos de resultados geralmente grandes de consultas muito amplas, pode produzir respostas JSON muito grandes que, portanto, levam muito tempo para serem computadas. É melhor limitar a saída somente aos formatos de texto necessários para renderizar o conteúdo.

### Modificação de fragmentos de conteúdo {#modifying-content-fragments}

Modifique somente os Fragmentos de conteúdo e seus recursos, usando a interface do usuário ou as APIs do AEM. Não faça modificações diretamente no JCR.

### Testar suas consultas {#test-your-queries}

O processamento de consultas do GraphQL GET é semelhante ao processamento de consultas de pesquisa, e é significativamente mais complexo do que as simples solicitações de API de conteúdo completo.

Planejar, testar e otimizar cuidadosamente suas consultas em um ambiente controlado não relacionado à produção é fundamental para o sucesso posterior, quando usado na produção.
