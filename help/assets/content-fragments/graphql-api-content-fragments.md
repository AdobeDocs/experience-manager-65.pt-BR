---
title: AEM API GraphQL para uso com Fragmentos de conteúdo
description: Saiba como usar Fragmentos de conteúdo no Adobe Experience Manager (AEM) com a API GraphQL AEM para entrega de conteúdo sem interface.
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: b5cf18d8e83786a23005aadf8aafe43d006a2e67
workflow-type: tm+mt
source-wordcount: '3919'
ht-degree: 1%

---

# AEM API GraphQL para uso com Fragmentos de conteúdo {#graphql-api-for-use-with-content-fragments}

Saiba como usar Fragmentos de conteúdo no Adobe Experience Manager (AEM) com a API GraphQL AEM para entrega de conteúdo sem interface.

AEM API GraphQL usada com Fragmentos de conteúdo é altamente baseada na API GraphQL de código aberto padrão.

Usar a API GraphQL no AEM permite a entrega eficiente dos Fragmentos de conteúdo aos clientes JavaScript em implementações CMS sem periféricos:

* Evitar solicitações de API iterativas como com REST,
* Garantir que a entrega se limite aos requisitos específicos,
* Permite a entrega em massa do exatamente o que é necessário para renderização como resposta a uma única consulta de API.

>[!NOTE]
>
>O GraphQL é usado atualmente em dois cenários (separados) no Adobe Experience Manager (AEM):
>
>* [O AEM Commerce consome dados de uma plataforma do Commerce via GraphQL](/help/commerce/cif/integrating/magento.md).
>* AEM Fragmentos de conteúdo trabalham com a API GraphQL AEM (uma implementação personalizada, com base no GraphQL padrão), para fornecer conteúdo estruturado para uso em seus aplicativos.


## A API GraphQL {#graphql-api}

GraphQL é:

* &quot;*...um idioma de consulta para APIs e um tempo de execução para realizar essas consultas com seus dados existentes. O GraphQL fornece uma descrição completa e compreensível dos dados em sua API, fornece aos clientes o poder de solicitar exatamente o que precisam e nada mais, facilita a evolução das APIs ao longo do tempo e permite ferramentas poderosas de desenvolvedor.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

* &quot;*...uma especificação aberta para uma camada de API flexível. Coloque GraphQL sobre seus back-end existentes para criar produtos mais rápido do que nunca....*&quot;.

   Consulte [Explorar GraphQL](https://www.graphql.com).

* *&quot;...uma linguagem de consulta de dados e especificação desenvolvidas internamente pela Facebook em 2012 antes de serem disponibilizadas publicamente em 2015. Ele oferece uma alternativa às arquiteturas baseadas em REST com o objetivo de aumentar a produtividade do desenvolvedor e minimizar as quantidades de dados transferidos. GraphQL é usado na produção por centenas de organizações de todos os tamanhos...&quot;*

   Consulte [Base GraphQL](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Para obter mais informações sobre a API GraphQL, consulte as seguintes seções (entre muitos outros recursos):

* Em [grafql.org](https://graphql.org):

   * [Introdução ao GraphQL](https://graphql.org/learn)

   * [A especificação GraphQL](http://spec.graphql.org/)

* Em [grafql.com](https://graphql.com):

   * [Guias](https://www.graphql.com/guides/)

   * [Tutoriais](https://www.graphql.com/tutorials/)

   * [Estudos de caso](https://www.graphql.com/case-studies/)

A implementação de GraphQL para AEM é baseada na Biblioteca GraphQL Java padrão. Consulte:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [Java GraphQL no GitHub](https://github.com/graphql-java)

### Terminologia GraphQL {#graphql-terminology}

GraphQL usa o seguinte:

* **[Queries](https://graphql.org/learn/queries/)**

* **[Esquemas e tipos](https://graphql.org/learn/schema/)**:

   * Os esquemas são gerados por AEM com base nos Modelos de fragmento de conteúdo.
   * Usando seus esquemas, GraphQL apresenta os tipos e as operações permitidas para GraphQL para AEM implementação.

* **[Campos](https://graphql.org/learn/queries/#fields)**

* **[Endpoint GraphQL](#graphql-aem-endpoint)**
   * O caminho no AEM que responde a consultas GraphQL e fornece acesso aos esquemas GraphQL.

   * Consulte [Ativar o Ponto de Extremidade GraphQL](#enabling-graphql-endpoint) para obter mais detalhes.

Consulte a [(GraphQL.org) Introdução ao GraphQL](https://graphql.org/learn/) para obter detalhes abrangentes, incluindo as [Práticas recomendadas](https://graphql.org/learn/best-practices/).

### Tipos de consulta GraphQL {#graphql-query-types}

Com GraphQL, você pode executar consultas para retornar:

* Uma **entrada única**

* Uma **[lista de entradas](https://graphql.org/learn/schema/#lists-and-non-null)**

Também é possível executar:

* [Consultas Persistentes, que estão em cache](#persisted-queries-caching)

>[!NOTE]
>Você pode testar e depurar consultas GraphQL usando o [GraphiQL IDE](#graphiql-interface).

## GraphQL para AEM Endpoint {#graphql-aem-endpoint}

O endpoint é o caminho usado para acessar GraphQL para AEM. Usando esse caminho você (ou seu aplicativo) pode:

* acesse o esquema GraphQL,
* enviar suas consultas GraphQL,
* receba as respostas (para suas consultas GraphQL).

Há dois tipos de endpoints no AEM:

* Global
   * Disponível para uso por todos os sites.
   * Esse terminal pode usar todos os Modelos de fragmento de conteúdo de todas as configurações de Sites (definidas no [Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
   * Se houver Modelos de fragmento de conteúdo que devem ser compartilhados entre configurações de Sites, eles devem ser criados nas configurações globais de Sites.
* Configurações de sites:
   * Corresponde a uma configuração de Sites, conforme definido no [Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * Específico de um site/projeto especificado.
   * Um endpoint específico de configuração de Sites usará os Modelos de fragmento de conteúdo da configuração de Sites específica junto com aqueles da configuração de Sites global.

>[!CAUTION]
>
>O Editor de fragmento de conteúdo pode permitir que um Fragmento de conteúdo de uma configuração de Sites faça referência a um Fragmento de conteúdo de outra configuração de Sites (por meio de políticas).
>
>Nesse caso, nem todo o conteúdo poderá ser recuperado usando um endpoint específico da configuração de Sites .
>
>O autor de conteúdo deve controlar esse cenário; por exemplo, pode ser útil considerar colocar Modelos de fragmento de conteúdo compartilhados na configuração de Sites globais.

O caminho do repositório do GraphQL para AEM endpoint global é:

`/content/cq:graphql/global/endpoint`

Para o qual seu aplicativo pode usar o seguinte caminho no URL da solicitação:

`/content/_cq_graphql/global/endpoint.json`

Para ativar um terminal para GraphQL para AEM, é necessário:

* [Ativar o terminal GraphQL](#enabling-graphql-endpoint)
* [Publicar seu terminal GraphQL](#publishing-graphql-endpoint)

### Ativação do terminal GraphQL {#enabling-graphql-endpoint}

Para ativar um Endpoint GraphQL, primeiro é necessário ter uma configuração apropriada. Consulte [Fragmentos de conteúdo - Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Se o [uso de modelos de fragmento de conteúdo não tiver sido ativado](/help/assets/content-fragments/content-fragments-configuration-browser.md), a opção **Criar** não estará disponível.

Para ativar o endpoint correspondente:

1. Navegue até **Ferramentas**, **Ativos**, em seguida selecione **GraphQL**.
1. Selecione **Criar**.
1. A caixa de diálogo **Criar novo Ponto de Extremidade GraphQL** será aberta. Aqui você pode especificar:
   * **Nome**: nome do ponto final; você pode inserir qualquer texto.
   * **Use o esquema GraphQL fornecido por**: use a lista suspensa para selecionar o site/projeto necessário.

   >[!NOTE]
   >
   >O seguinte aviso é mostrado na caixa de diálogo:
   >
   >* *Os pontos de extremidade do GraphQL podem causar problemas de segurança e desempenho de dados se não forem gerenciados com cuidado. Defina as permissões apropriadas após criar um ponto de extremidade.*


1. Confirme com **Create**.
1. A caixa de diálogo **Próximas etapas** fornecerá um link direto para o console Segurança para que você possa garantir que o endpoint recém-criado tenha as permissões adequadas.

   >[!CAUTION]
   >
   >O endpoint é acessível a todos. Isso pode - especialmente em instâncias de publicação - causar uma preocupação de segurança, já que as consultas GraphQL podem impor uma carga pesada no servidor.
   >
   >Você pode configurar ACLs, apropriadas ao seu caso de uso, no terminal.

### Publicar seu ponto de extremidade GraphQL {#publishing-graphql-endpoint}

Selecione o novo terminal e **Publish** para torná-lo totalmente disponível em todos os ambientes.

>[!CAUTION]
>
>O endpoint é acessível a todos.
>
>Em instâncias de publicação, isso pode causar uma preocupação de segurança, já que as consultas GraphQL podem impor uma carga pesada no servidor.
>
>Você deve configurar as ACLs apropriadas ao seu caso de uso no terminal.

## Interface GraphiQL {#graphiql-interface}

Uma implementação da interface [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) padrão está disponível para uso com AEM GraphQL. Pode ser [instalado com AEM](#installing-graphiql-interface).

>[!NOTE]
>
>O GraphiQL está vinculado ao endpoint global (e não funciona com outros endpoints para configurações específicas do Sites).

Essa interface permite que você insira e teste diretamente consultas.

Por exemplo:

* `http://localhost:4502/content/graphiql.html`

Isso fornece recursos como realce de sintaxe, preenchimento automático, sugestão automática, juntamente com um histórico e documentação online:

![Interface GraphiQL ](assets/cfm-graphiql-interface.png "InterfaceInterface GraphiQL")

### Instalação da interface GraphiQL AEM {#installing-graphiql-interface}

<!-- 6.5.10.0??? -->

A interface do usuário GraphiQL pode ser instalada no AEM com um pacote dedicado: o pacote [Pacote de Conteúdo GraphiQL v0.0.6 (2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip).

>[!NOTE]
>
>O pacote disponível é totalmente compatível com AEM 6.5.10.0 e AEM como Cloud Service.

## Casos de uso para ambientes de autor e publicação {#use-cases-author-publish-environments}

Os casos de uso podem depender do tipo de ambiente de AEM:

* Ambiente de publicação; usado para:
   * Dados de consulta para aplicativo JS (caso de uso padrão)

* Ambiente de criação; usado para:
   * Consultar dados para &quot;fins de gerenciamento de conteúdo&quot;:
      * GraphQL no AEM é uma API somente leitura no momento.
      * A REST API pode ser usada para operações de CR(u)D.

## Permissões {#permission}

As permissões são as necessárias para acessar o Assets.

## Geração de esquema {#schema-generation}

GraphQL é uma API altamente digitada, o que significa que os dados devem ser estruturados e organizados claramente por tipo.

A especificação GraphQL fornece uma série de diretrizes sobre como criar uma API robusta para interrogar dados em uma determinada instância. Para fazer isso, um cliente precisa buscar o [Schema](#schema-generation), que contém todos os tipos necessários para um query.

Para Fragmentos de conteúdo, os esquemas GraphQL (estrutura e tipos) são baseados em **Ativado** [Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) e seus tipos de dados.

>[!CAUTION]
>
>Todos os esquemas GraphQL (derivados dos Modelos de fragmento de conteúdo que foram **Enabled**) podem ser lidos pelo ponto de extremidade GraphQL.
>
>Isso significa que você precisa garantir que não haja dados confidenciais disponíveis, pois eles poderiam ser vazados dessa forma; por exemplo, isso inclui informações que podem estar presentes como nomes de campo na definição do modelo.

Por exemplo, se um usuário criou um Modelo de fragmento de conteúdo chamado `Article`, AEM gera o objeto `article` que é do tipo `ArticleModel`. Os campos desse tipo correspondem aos campos e tipos de dados definidos no modelo.

1. Um modelo de fragmento de conteúdo:

   ![Modelo de fragmento de conteúdo para uso com o ](assets/cfm-graphqlapi-01.png "GraphQLContent Fragment Model para uso com GraphQL")

1. O esquema GraphQL correspondente (saída da documentação automática GraphiQL):
   ![Esquema GraphQL com base no ](assets/cfm-graphqlapi-02.png "modelo de fragmento de conteúdoGraphQL com base no modelo de fragmento de conteúdo")

   Isso mostra que o tipo gerado `ArticleModel` contém vários [campos](#fields).

   * Três delas foram controladas pelo usuário: `author`, `main` e `referencearticle`.

   * Os outros campos foram adicionados automaticamente por AEM e representam métodos úteis para fornecer informações sobre um determinado Fragmento de conteúdo; neste exemplo, `_path`, `_metadata`, `_variations`. Esses [campos auxiliares](#helper-fields) são marcados com um `_` anterior para distinguir entre o que foi definido pelo usuário e o que foi gerado automaticamente.

1. Depois que um usuário cria um Fragmento de conteúdo com base no modelo de Artigo, ele pode ser interrogado por meio de GraphQL. Para obter exemplos, consulte as [Consultas de amostra](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries) (com base em uma [estrutura de fragmento de conteúdo de amostra para usar com GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).

No GraphQL para AEM, o esquema é flexível. Isso significa que ele é gerado automaticamente cada vez que um Modelo de fragmento de conteúdo é criado, atualizado ou excluído. Os caches de esquema de dados também são atualizados quando você atualiza um Modelo de fragmento de conteúdo.

O serviço GraphQL do Sites escuta (em segundo plano) quaisquer modificações feitas em um Modelo de fragmento de conteúdo. Quando as atualizações são detectadas, somente essa parte do esquema é regenerada. Essa otimização economiza tempo e oferece estabilidade.

Por exemplo, se você:

1. Instale um pacote contendo `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. Os tipos GraphQL para `Model-1` e `Model-2` serão gerados.

1. Em seguida, modifique `Content-Fragment-Model-2`:

   1. Somente o tipo GraphQL `Model-2` será atualizado.

   1. Enquanto `Model-1` permanecerá o mesmo.

>[!NOTE]
>
>Isso é importante observar caso queira fazer atualizações em massa nos Modelos de fragmento de conteúdo por meio da api REST ou de outra forma.

O esquema é distribuído por meio do mesmo terminal que as consultas GraphQL, com o cliente lidando com o fato de que o esquema é chamado com a extensão `GQLschema`. Por exemplo, executar uma solicitação `GET` simples em `/content/cq:graphql/global/endpoint.GQLschema` resultará na saída do schema com o Tipo de conteúdo: `text/x-graphql-schema;charset=iso-8859-1`.

### Geração de esquema - Modelos não publicados {#schema-generation-unpublished-models}

Quando os Fragmentos de conteúdo são aninhados, pode acontecer que um Modelo de fragmento de conteúdo principal seja publicado, mas um modelo referenciado não é.

>[!NOTE]
>
>A interface do usuário do AEM impede que isso aconteça, mas se a publicação for feita de forma programática ou com pacotes de conteúdo, ela poderá ocorrer.

Quando isso acontece, o AEM gera um esquema *incompleto* para o modelo de fragmento de conteúdo pai. Isso significa que a Referência do fragmento, que depende do modelo não publicado, é removida do esquema.

## Fields {#fields}

Dentro do schema há campos individuais, de duas categorias básicas:

* Campos gerados.

   Uma seleção de [Tipos de campo](#field-types) é usada para criar campos com base em como você configura o Modelo de fragmento de conteúdo. Os nomes de campo são obtidos do campo **Nome da propriedade** do **Tipo de dados**.

   * Também há a propriedade **Renderizar como** a ser levada em consideração, pois os usuários podem configurar determinados tipos de dados; por exemplo, como um texto de linha única ou um multicampo.

* GraphQL para AEM também gera vários [campos auxiliares](#helper-fields).

   Eles são usados para identificar um Fragmento de conteúdo ou para obter mais informações sobre um fragmento de conteúdo.

### Tipos de campos {#field-types}

GraphQL para AEM oferece suporte a uma lista de tipos. Todos os tipos de dados do modelo de fragmento de conteúdo suportados e os tipos GraphQL correspondentes são representados:

| Modelo de fragmento de conteúdo - Tipo de dados | Tipo GraphQL | Descrição |
|--- |--- |--- |
| Texto de linha única | String, [String] |  Usado para strings simples, como nomes de autor, nomes de localização etc. |
| Texto de várias linhas | Sequência de caracteres |  Usado para saída de texto, como o corpo de um artigo |
| Número |  Flutuante, [Flutuante] | Usado para exibir números de ponto flutuante e números regulares |
| Booleano |  Booleano |  Usado para exibir caixas de seleção → declarações simples verdadeiras/falsas |
| Data E Hora | Calendário |  Usado para exibir data e hora em um formato ISO 8086. Dependendo do tipo selecionado, há três opções disponíveis para uso em GraphQL AEM: `onlyDate`, `onlyTime`, `dateTime` |
| Enumeração |  Sequência de caracteres |  Usado para exibir uma opção de uma lista de opções definidas na criação do modelo |
|  Tags |  [Sequência de caracteres] |  Usado para exibir uma lista de strings que representam tags usadas em AEM |
| Referência de conteúdo |  Sequência de caracteres |  Usado para exibir o caminho para outro ativo no AEM |
| Referência do fragmento |  *Um tipo de modelo* |  Usado para fazer referência a outro Fragmento de conteúdo de um determinado Tipo de modelo, definido quando o modelo foi criado |

### Campos de ajuda {#helper-fields}

Além dos tipos de dados para campos gerados pelo usuário, o GraphQL para AEM também gera vários campos *helper* para ajudar a identificar um Fragmento de conteúdo ou para fornecer informações adicionais sobre um Fragmento de conteúdo.

#### Caminho {#path}

O campo de caminho é usado como um identificador em GraphQL. Ele representa o caminho do ativo Fragmento de conteúdo dentro do repositório de AEM. Optamos por isso como o identificador de um fragmento de conteúdo, pois ele:

* é único no AEM,
* podem ser buscadas facilmente.

O código a seguir exibirá os caminhos de todos os Fragmentos de conteúdo que foram criados com base no Modelo do Fragmento de conteúdo `Person`.

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

Para recuperar um único Fragmento de conteúdo de um tipo específico, também é necessário determinar seu caminho primeiro. por exemplo:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

Consulte [Exemplo de consulta - Um único fragmento de cidade específico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

#### Metadados {#metadata}

Por meio do GraphQL, o AEM também expõe os metadados de um Fragmento de conteúdo. Metadados são as informações que descrevem um fragmento de conteúdo, como o título de um fragmento de conteúdo, o caminho de miniatura, a descrição de um Fragmento de conteúdo, a data de criação, entre outros.

Como os metadados são gerados por meio do Editor de esquemas e, como tal, não têm uma estrutura específica, o tipo GraphQL `TypedMetaData` foi implementado para expor os metadados de um Fragmento de conteúdo. `TypedMetaData` expõe as informações agrupadas pelos seguintes tipos escalares:

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

Cada tipo escalar representa um único par de nome-valor ou uma matriz de pares de nome-valor, onde o valor desse par é do tipo em que foi agrupado.

Por exemplo, se você quiser recuperar o título de um Fragmento de conteúdo, sabemos que essa propriedade é uma propriedade de String, portanto, consultaríamos todos os Metadados de String:

Para consultar metadados:

```xml
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

Você pode exibir todos os tipos de metadados GraphQL se exibir o esquema GraphQL gerado. Todos os tipos de modelo têm o mesmo `TypedMetaData`.

>[!NOTE]
>
>**Diferença entre metadados normais e de matriz**
>Lembre-se de que `StringMetadata` e `StringArrayMetadata` ambos se referem ao que é armazenado no repositório, não como você os recupera.
>
>Assim, por exemplo, ao chamar o campo `stringMetadata`, você receberia uma matriz de todos os metadados que foram armazenados no repositório como um `String` , e se chamar `stringArrayMetadata` você receberia uma matriz de todos os metadados que foram armazenados no repositório como `String[]`.

Consulte [Exemplo de consulta para metadados - Liste os metadados para prêmios denominados GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

#### Variações {#variations}

O campo `_variations` foi implementado para simplificar a consulta das variações que um Fragmento de conteúdo tem. Por exemplo:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

Consulte [Exemplo de consulta - Todas as cidades com uma variável nomeada](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## Variáveis GraphQL {#graphql-variables}

GraphQL permite que as variáveis sejam colocadas no query. Para obter mais informações, consulte a [documentação GraphQL para Variáveis](https://graphql.org/learn/queries/#variables).

Por exemplo, para obter todos os Fragmentos de conteúdo do tipo `Article` que têm uma variação específica, você pode especificar a variável `variation` em GraphiQL.

![Variáveis GraphQL ](assets/cfm-graphqlapi-03.png "Variáveis GraphQL")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## Diretivas GraphQL {#graphql-directives}

No GraphQL há uma possibilidade de alterar o query com base em variáveis, chamadas de Diretivas GraphQL.

Por exemplo, é possível incluir o campo `adventurePrice` em uma consulta para todos os `AdventureModels`, com base em uma variável `includePrice`.

![Diretivas GraphQL ](assets/cfm-graphqlapi-04.png "Diretivas GraphQL")

```xml
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

Você também pode usar a filtragem em consultas GraphQL para retornar dados específicos.

A filtragem usa uma sintaxe baseada em operadores lógicos e expressões.

Por exemplo, a consulta a seguir (básica) filtra todas as pessoas que têm um nome `Jobs` ou `Smith`:

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

Para obter mais exemplos, consulte:

* detalhes do [GraphQL para extensões de AEM](#graphql-extensions)

* [Consultas de exemplo usando este conteúdo e estrutura de amostra](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * E o [Conteúdo e estrutura de amostra](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) preparado para uso em consultas de amostra

* [Consultas de exemplo com base no projeto WKND](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL para AEM - Resumo das extensões {#graphql-extensions}

A operação básica de consultas com GraphQL para AEM adere à especificação GraphQL padrão. Para consultas GraphQL com AEM, há algumas extensões:

* Se você precisar de um único resultado:
   * Utilizar o nome do modelo; cidade eg

* Se você espera uma lista de resultados:
   * adicionar `List` ao nome do modelo; por exemplo, `cityList`
   * Consulte [Exemplo de consulta - Todas as informações sobre todas as cidades](#sample-all-information-all-cities)

* Se quiser usar um OR lógico:
   * use ` _logOp: OR`
   * Consulte [Exemplo de Consulta - Todas as Pessoas que têm o nome de &quot;Trabalhos&quot; ou &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* AND lógico também existe, mas está (muitas vezes) implícito

* Você pode consultar nomes de campos que correspondem aos campos no Modelo de fragmento de conteúdo
   * Consulte [Exemplo de consulta - Detalhes completos do CEO e funcionários de uma empresa](#sample-full-details-company-ceos-employees)

* Além dos campos do modelo, há alguns campos gerados pelo sistema (precedidos pelo sublinhado ):

   * Para conteúdo:

      * `_locale` : Revelar a língua; com base no Gerenciador de idiomas
         * Consulte [Exemplo de consulta para vários fragmentos de conteúdo de uma determinada localidade](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : para revelar metadados para o fragmento
         * Consulte [Exemplo de consulta para metadados - Liste os metadados para prêmios denominados GB](#sample-metadata-awards-gb)
      * `_model` : permitir consulta para um Modelo de fragmento de conteúdo (caminho e título)
         * Consulte [Exemplo de consulta para um modelo de fragmento de conteúdo de um modelo](#sample-wknd-content-fragment-model-from-model)
      * `_path` : o caminho para o Fragmento do conteúdo no repositório
         * Consulte [Exemplo de consulta - Um único fragmento de cidade específico](#sample-single-specific-city-fragment)
      * `_reference` : revelar referências; incluindo referências em linha no Editor de Rich Text
         * Consulte [Exemplo de consulta para vários fragmentos de conteúdo com referências pré-buscadas](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : para revelar variações específicas no Fragmento de conteúdo
         * Consulte [Exemplo de consulta - Todas as cidades com uma variável nomeada](#sample-cities-named-variation)
   * E operações:

      * `_operator` : Aplicar operadores específicos;  `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`,  `STARTS_WITH`
         * Consulte [Consulta de Amostra - Todas as Pessoas que não têm um nome &quot;Trabalhos&quot;](#sample-all-persons-not-jobs)
         * Consulte [Exemplo de consulta - Todas as empresas onde o `_path` começa com um prefixo específico](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : Aplicar condições específicas; por exemplo,   `AT_LEAST_ONCE`
         * Consulte [Exemplo de consulta - Filtrar em uma matriz com um item que deve ocorrer pelo menos uma vez](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : para ignorar o caso ao consultar
         * Consulte [Exemplo de consulta - Todas as cidades com SAN no nome, independentemente do caso](#sample-all-cities-san-ignore-case)









* Os tipos de união GraphQL são suportados:

   * use `... on`
      * Consulte [Exemplo de consulta para um fragmento de conteúdo de um modelo específico com uma referência de conteúdo](#sample-wknd-fragment-specific-model-content-reference)

## Consultas Persistentes (Cache) {#persisted-queries-caching}

Após preparar uma consulta com uma solicitação POST, ela pode ser executada com uma solicitação GET que pode ser armazenada em cache por caches HTTP ou um CDN.

Isso é necessário, pois as consultas do POST geralmente não são armazenadas em cache e, se estiver usando o GET com o query como parâmetro, há um risco significativo de o parâmetro se tornar muito grande para serviços HTTP e intermediários.

As consultas persistentes devem sempre usar o terminal relacionado ao [configuração apropriada do Sites](#graphql-aem-endpoint); para que possam usar ou ambos:

* A configuração global e o terminal
O query tem acesso a todos os Modelos de fragmento de conteúdo.
* Configuração(ões) de sites específicos e endpoint(s)
A criação de uma consulta persistente para uma configuração de Sites específica requer um endpoint específico de configuração de Sites correspondente (para fornecer acesso aos Modelos de fragmento de conteúdo relacionados).
Por exemplo, para criar uma consulta persistente especificamente para a configuração de Sites WKND, uma configuração de Sites específica de WKND correspondente e um endpoint específico de WKND devem ser criados antecipadamente.

>[!NOTE]
>
>Consulte [Ativar a funcionalidade de fragmento de conteúdo no Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) para obter mais detalhes.
>
>As **Consultas de Persistência GraphQL** precisam ser ativadas para a configuração apropriada do Sites.

Por exemplo, se houver uma consulta específica chamada `my-query`, que usa um modelo `my-model` da configuração de Sites `my-conf`:

* Você pode criar uma consulta usando o terminal específico `my-conf` e, em seguida, a consulta será salva da seguinte maneira:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Você pode criar a mesma consulta usando o ponto de extremidade `global`, mas a consulta será salva da seguinte maneira:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Essas são duas consultas diferentes - salvas em caminhos diferentes.
>
>Acontece que eles apenas usam o mesmo modelo - mas por diferentes endpoints.


Estas são as etapas necessárias para persistir uma determinada query:

1. Prepare a query colocando-a no novo URL de ponto de extremidade `/graphql/persist.json/<config>/<persisted-label>`.

   Por exemplo, crie uma consulta persistente:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. Neste ponto, verifique a resposta.

   Por exemplo, verifique se há sucesso:

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. Em seguida, você pode repetir a consulta persistente usando GETo URL `/graphql/execute.json/<shortPath>`.

   Por exemplo, use a consulta persistente:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Atualize uma consulta persistente do POSTing para um caminho de consulta já existente.

   Por exemplo, use a consulta persistente:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Crie uma consulta simples encapsulada.

   Por exemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Crie uma consulta simples encapsulada com controle de cache.

   Por exemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Crie uma consulta persistente com parâmetros:

   Por exemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. Execução de uma consulta com parâmetros.

   Por exemplo:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. Para executar o query na publicação, a árvore persistente relacionada precisa ser replicada

   * Usando um POST para replicação:

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * Uso de um pacote:
      1. Crie uma nova definição de pacote.
      1. Inclua a configuração (por exemplo, `/conf/wknd/settings/graphql/persistentQueries`).
      1. Crie o pacote.
      1. Replicar o pacote.
   * Uso da ferramenta de replicação/distribuição.
      1. Vá para a ferramenta Distribution .
      1. Selecione ativação em árvore para a configuração (por exemplo, `/conf/wknd/settings/graphql/persistentQueries`).
   * Uso de um workflow (por meio da configuração do iniciador do workflow):
      1. Defina uma regra do iniciador do workflow para executar um modelo de workflow que replicaria a configuração em eventos diferentes (por exemplo, criar, modificar, entre outros).



1. Quando a configuração do query estiver em publicação, os mesmos princípios se aplicarão, apenas usando o endpoint de publicação.

   >[!NOTE]
   >
   >Para acesso anônimo, o sistema assume que a ACL permite que &quot;todos&quot; tenham acesso à configuração da consulta.
   >
   >Se esse não for o caso, não será possível executar.

   >[!NOTE]
   >
   >Qualquer ponto e vírgula (&quot;;&quot;) nos URLs precisa ser codificado.
   >
   >Por exemplo, como na solicitação para executar uma consulta mantida:
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## Consultando o ponto de extremidade GraphQL de um site externo {#query-graphql-endpoint-from-external-website}

Para acessar o ponto de extremidade GraphQL de um site externo, é necessário configurar o:

* [Filtro CORS](#cors-filter)
* [Filtro referenciador](#referrer-filter)

### Filtro CORS {#cors-filter}

>[!NOTE]
>
>Para obter uma visão geral detalhada da política de compartilhamento de recursos do CORS em AEM consulte [Entender o compartilhamento de recursos entre origens (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors)).

Para acessar o ponto de extremidade GraphQL, uma política CORS deve ser configurada no repositório Git do cliente. Isso é feito adicionando um arquivo de configuração de CORS OSGi apropriado para os endpoints desejados.

Essa configuração deve especificar uma origem de site confiável `alloworigin` ou `alloworiginregexp` para a qual o acesso deve ser concedido.

Por exemplo, para conceder acesso ao ponto de extremidade GraphQL e ao ponto de extremidade de consultas persistentes para `https://my.domain` é possível usar:

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

Se você tiver configurado um caminho personalizado para o endpoint, também poderá usá-lo em `allowedpaths`.

### Filtro referenciador {#referrer-filter}

Além da configuração do CORS, um filtro Referenciador deve ser configurado para permitir acesso de hosts de terceiros.

Isso é feito adicionando um arquivo de configuração do Filtro de referenciador OSGi apropriado que:

* especifica um nome de host de site confiável; `allow.hosts` ou `allow.hosts.regexp`,
* concede acesso a esse nome de host.

Por exemplo, para conceder acesso a solicitações com o Referenciador `my.domain` você pode:

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
>* certifique-se de que nenhuma informação sensível seja exposta
>* não use uma sintaxe curinga [*]; isso desativará o acesso autenticado ao ponto de extremidade GraphQL e também o exporá ao mundo inteiro.


>[!CAUTION]
>
>Todos os esquemas GraphQL [](#schema-generation) (derivados dos Modelos de Fragmento de Conteúdo que foram **Ativado**) podem ser lidos pelo ponto de extremidade GraphQL.
>
>Isso significa que você precisa garantir que não haja dados confidenciais disponíveis, pois eles poderiam ser vazados dessa forma; por exemplo, isso inclui informações que podem estar presentes como nomes de campo na definição do modelo.

## Autenticação {#authentication}

Consulte [Autenticação para consultas GraphQL de AEM Remotas em Fragmentos de Conteúdo](/help/assets/content-fragments/graphql-authentication-content-fragments.md).

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## Perguntas frequentes {#faqs}

Questões que surgiram:

1. **P**: &quot;*Como a API GraphQL para AEM diferente da API do Query Builder?*&quot;

   * **A**: &quot;*A API GraphQL da AEM oferece controle total sobre a saída JSON e é um padrão do setor para consulta de conteúdo.
A partir de agora, AEM planeja investir na API GraphQL AEM.*&quot;

## Tutorial - Introdução ao AEM Headless e GraphQL {#tutorial}

Procurando um tutorial prático? Confira o [Introdução ao AEM Headless e o tutorial GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) completo ilustrando como criar e expor conteúdo usando as APIs GraphQL da AEM e consumidas por um aplicativo externo, em um cenário de CMS sem periféricos.
