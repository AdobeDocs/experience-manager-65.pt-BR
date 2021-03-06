---
title: Desenvolvimento de relatórios
seo-title: Desenvolvimento de relatórios
description: AEM fornece uma seleção de relatórios padrão com base em um quadro de relatórios
seo-description: AEM fornece uma seleção de relatórios padrão com base em um quadro de relatórios
uuid: 1b406d15-bd77-4531-84c0-377dbff5cab2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 50fafc64-d462-4386-93af-ce360588d294
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
source-git-commit: 071bc0e36ed2d8eb4ce7bd0ba46823adc0e43095
workflow-type: tm+mt
source-wordcount: '5252'
ht-degree: 0%

---


# Desenvolvimento de relatórios {#developing-reports}

AEM fornece uma seleção de [relatórios padrão](/help/sites-administering/reporting.md) a maioria dos quais se baseia em uma estrutura de relatórios.

Usando a estrutura, você pode estender esses relatórios padrão ou desenvolver seus próprios, completamente novos, relatórios. A estrutura de relatórios integra-se fortemente aos conceitos e princípios do CQ5 existentes, de modo que os desenvolvedores possam usar seu conhecimento atual do CQ5 como trampolim para desenvolver relatórios.

Para os relatórios padrão entregues com AEM:

* Esses relatórios são baseados na estrutura de relatórios:

   * [Relatório de componentes](/help/sites-administering/reporting.md#component-report)
   * [Relatório de atividades de página](/help/sites-administering/reporting.md#page-activity-report)
   * [Relatório do usuário](/help/sites-administering/reporting.md#user-report)
   * [Relatório de instâncias do fluxo de trabalho](/help/sites-administering/reporting.md#workflow-instance-report)

* Os seguintes relatórios baseiam-se em princípios individuais, pelo que não podem ser alargados:

   * [Uso do disco](/help/sites-administering/reporting.md#disk-usage)
   * [Verificação de integridade](/help/sites-administering/reporting.md#health-check)
   * [Relatório de fluxo de trabalho](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>O tutorial [Criar seu próprio relatório - Um exemplo](#creating-your-own-report-an-example) também mostra quantos dos princípios abaixo podem ser usados.
>
>Você também pode consultar os relatórios padrão para ver outros exemplos de implementação.

>[!NOTE]
>
>Nos exemplos e definições abaixo, a seguinte notação é usada :
>
>* Cada linha define um nó ou uma propriedade em que:
   >  `N:<name> [<nodeType>]` : Descreve um nó com o nome  `<*name*>` e o tipo de nó  `<*nodeType*>`*.*
   >  `P:<name> [<propertyType]` : Descreve uma propriedade com o nome de  `<*name*>` e um tipo de propriedade de  `<*propertyType*>`.
   >  `P:<name> = <value>` : Descreve uma propriedade  `<name>` que deve ser definida com o valor de  `<value>`.
   >
   >
* A Recuo mostra as dependências hierárquicas entre os nós.
>* Itens separados por | indica uma lista de elementos possíveis; por exemplo, tipos ou nomes; por exemplo `String|String[]` significa que a propriedade pode ser String ou String[].

   >
   >
* `[]` representa um array; como [] String ou uma matriz de nós como na Definição de  [Consulta](#query-definition).
>
>
Salvo indicação em contrário, os tipos padrão são:
>
>* Nós - `nt:unstructured`
>* Propriedades - `String`


## Estrutura de relatórios {#reporting-framework}

O quadro de relatórios baseia - se nos seguintes princípios:

* Ele é inteiramente baseado em conjuntos de resultados que são retornados por uma consulta executada pelo QueryBuilder do CQ5.
* O conjunto de resultados define os dados exibidos no relatório. Cada linha no conjunto de resultados corresponde a uma linha na exibição em tabela do relatório.
* As operações disponíveis para execução no conjunto de resultados assemelham-se aos conceitos do RDBMS; primariamente *agrupamento* e *agregação*.

* A maioria da recuperação e do processamento de dados é feita no lado do servidor.
* O cliente é o único responsável pela exibição dos dados pré-processados. Somente tarefas de processamento secundárias (por exemplo, criação de links no conteúdo da célula) são executadas no lado do cliente.

A estrutura de relatórios (ilustrada pela estrutura de um relatório padrão) usa os seguintes blocos fundamentais, alimentados pela fila de processamento:

![chlimage_1-247](assets/chlimage_1-248.png)

### Página Relatório {#report-page}

A página do relatório:

* É uma página CQ5 padrão.
* É baseado em um [modelo CQ5 padrão, configurado para o relatório](#report-template).

### Base de relatórios {#report-base}

O [ `reportbase` componente](#report-base-component) é a base de qualquer relatório da mesma forma que:

* Mantém a definição do [query](#the-query-and-data-retrieval) que fornece o conjunto de dados de resultado subjacente.

* É um sistema de parágrafo adaptado que conterá todas as colunas ( `columnbase`) adicionadas ao relatório.
* Define quais tipos de gráfico estão disponíveis e quais estão ativas no momento.
* Define a caixa de diálogo Editar , que permite ao usuário configurar certos aspectos do relatório.

### Base da coluna {#column-base}

Cada coluna é uma instância do [ `columnbase` componente](#column-base-component) que:

* É um parágrafo, usado pelo parsys ( `reportbase`) do respectivo relatório.
* Define o link para o [conjunto de resultados subjacente](#the-query-and-data-retrieval); ou seja, define os dados específicos referenciados nesse conjunto de resultados e como ele é processado.
* Possui definições adicionais; como agregações e filtros disponíveis, juntamente com quaisquer valores padrão.

### A consulta e a recuperação de dados {#the-query-and-data-retrieval}

O query:

* É definido como parte do componente [ `reportbase`](#report-base).
* É baseado no [CQ QueryBuilder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html).
* Recupera os dados usados como base do relatório. Cada linha do conjunto de resultados (tabela) é vinculada a um nó conforme retornado pelo query. As informações específicas para [colunas individuais](#column-base-component) são então extraídas desse conjunto de dados.

* Normalmente consiste em:

   * Um caminho raiz.

      Especifica a subárvore do repositório a ser pesquisado.

      Para ajudar a minimizar o impacto no desempenho, é aconselhável (tentar) restringir a consulta a uma subárvore específica do repositório. O caminho raiz pode ser predefinido no [modelo de relatório](#report-template) ou definido pelo usuário na caixa de diálogo [Configuração (Editar)](#configuration-dialog).

   * [Um ou mais critérios](#query-definition).

      São impostos para produzir o conjunto de resultados (iniciais); incluem, por exemplo, restrições sobre o tipo de nó ou restrições de propriedade.

**O ponto principal aqui é que cada nó único retornado no conjunto de resultados da query é usado para gerar uma única linha no relatório (portanto, uma relação 1:1).**

O desenvolvedor deve garantir que a consulta definida para um relatório retorne um conjunto de nós apropriado para esse relatório. No entanto, o nó em si não precisa conter todas as informações necessárias, isso também pode ser derivado de nós pai e/ou filho. Por exemplo, a consulta usada para o [Relatório do Usuário](/help/sites-administering/reporting.md#user-report) seleciona nós com base no tipo de nó (neste caso `rep:user`). No entanto, a maioria das colunas neste relatório não obtém seus dados diretamente desses nós, mas dos nós secundários `profile`.

### Fila de processamento {#processing-queue}

O [query](#the-query-and-data-retrieval) retorna um conjunto de dados de resultado a ser exibido como linhas no relatório. Cada linha no conjunto de resultados é processada (no lado do servidor), em [várias fases](#phases-of-the-processing-queue), antes de ser transferida para o cliente para exibição no relatório.

Isso permite:

* Extrair e derivar valores do conjunto de resultados subjacente.

   Por exemplo, permite processar dois valores de propriedade como um único valor, calculando a diferença entre os dois.

* Resolver valores extraídos; isso pode ser feito de várias maneiras.

   Por exemplo, os caminhos podem ser mapeados para um título (como no conteúdo mais legível por humanos da respectiva propriedade *jcr:title*).

* Aplicação de filtros em vários pontos.
* Criação de valores compostos, se necessário.

   Por exemplo, consistindo de um texto exibido ao usuário, um valor a ser usado para a classificação e um URL adicional usado (no lado do cliente) para criar um link.

#### Fluxo de trabalho da fila de processamento {#workflow-of-the-processing-queue}

O seguinte workflow representa a fila de processamento:

![chlimage_1-249](assets/chlimage_1-249.png)

#### Fases da fila de processamento {#phases-of-the-processing-queue}

Onde as etapas e elementos detalhados são:

1. Transforma os resultados retornados pela consulta inicial [(reportbase)](#query-definition) no conjunto de resultados básico usando extratores de valor.

   Os extratores de valores são escolhidos automaticamente dependendo do tipo de coluna [e](#column-specific-definitions). Eles são usados para ler valores da Consulta JCR subjacente e criar um conjunto de resultados a partir deles; após o que pode ser aplicada uma transformação complementar. Por exemplo, para o tipo `diff`, o extrator de valor lê duas propriedades, calcula o valor único que é então adicionado ao conjunto de resultados. Os extratores de valor não podem ser configurados.

1. Para esse conjunto de resultados inicial, contendo dados brutos, [filtragem inicial](#column-specific-definitions) (*fase bruta*) é aplicada.

1. Os valores são [pré-processados](#processing-queue); conforme definido para a fase *apply*.

1. [A filtragem](#column-specific-definitions)  (atribuída à fase  ** pré-processada) é executada nos valores pré-processados.

1. Os valores são resolvidos; de acordo com o [resolvedor definido](#processing-queue).
1. [A filtragem](#column-specific-definitions)  (atribuída à fase  ** resolvida) é executada nos valores resolvidos.

1. Os dados são [agrupados e agregados](#column-specific-definitions).
1. Os dados da matriz são resolvidos convertendo-os em uma lista (baseada em sequência).

   Esta é uma etapa implícita que converte um resultado de vários valores em uma lista que pode ser exibida; é necessário para valores de células (não agregadas) baseados em propriedades JCR de vários valores.

1. Os valores são novamente [pré-processados](#processing-queue); conforme definido para a fase *afterApply*.

1. Os dados são classificados.
1. Os dados processados são transferidos para o cliente.

>[!NOTE]
>
>A consulta inicial que retorna o conjunto de resultados dos dados base é definida no componente `reportbase`.
>
>Outros elementos da fila de processamento são definidos nos componentes `columnbase`.

## Construção e configuração de relatórios {#report-construction-and-configuration}

Os itens a seguir são necessários para construir e configurar um relatório:

* um [local para a definição dos componentes do relatório](#location-of-report-components)
* um [ `reportbase` componente](#report-base-component)
* um, ou mais, [ `columnbase` componente(s)](#column-base-component)
* um [componente de página](#page-component)
* um [design de relatório](#report-design)
* um [modelo de relatório](#report-template)

### Localização dos componentes de relatório {#location-of-report-components}

Os componentes de relatório padrão são mantidos em `/libs/cq/reporting/components`.

No entanto, é altamente recomendável não atualizar esses nós, mas criar seus próprios nós de componente em `/apps/cq/reporting/components` ou se for mais apropriado `/apps/<yourProject>/reports/components`.

Onde (como exemplo):

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

Abaixo, você cria a raiz do seu relatório e, sob isso, o componente base do relatório e os componentes base da coluna:

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### Componente de página {#page-component}

Uma página de relatório deve usar o `sling:resourceType` de `/libs/cq/reporting/components/reportpage`.

Um componente de página personalizada não deve ser necessário (na maioria dos casos).

## Componente base de relatório {#report-base-component}

Cada tipo de relatório requer um componente de contêiner derivado de `/libs/cq/reporting/components/reportbase`.

Esse componente atua como um contêiner para o relatório como um todo e fornece informações para:

* A [definição de consulta](#query-definition).
* Uma caixa de diálogo [(opcional)](#configuration-dialog) para configurar o relatório.
* Qualquer [Gráficos](#chart-definitions) integrado no relatório.

```
N:<reportname> [cq:Component]
    P:sling:resourceSuperType = "cq/reporting/components/reportbase"
    N:charting
    N:dialog [cq:Dialog]
    N:queryBuilder
```

### Definição de Consulta {#query-definition}

```xml
N:queryBuilder
    N:propertyConstraints
    [
        N:<name> // array of nodes (name irrelevant), each with the following properties:
            P:name
            P:value
    ]
    P:nodeTypes [String|String[]]
    P:mandatoryProperties [String|String[]
  ]
```

* `propertyConstraints`

   Pode ser usado para limitar o conjunto de resultados a nós que têm propriedades específicas com valores específicos. Se várias restrições forem especificadas, o nó deverá atender a todas elas (operação AND).

   Por exemplo:

   ```
   N:propertyConstraints
    [
    N:0
    P:sling:resourceType
    P:foundation/components/textimage
    N:1
    P:jcr:modifiedBy
    P:admin
    ]
   ```

   Retornaria todos os `textimage` componentes que foram modificados pela última vez pelo usuário `admin`.

* `nodeTypes`

   Usado para limitar o conjunto de resultados aos tipos de nó especificados. É possível especificar vários tipos de nó.

* `mandatoryProperties`

   Pode ser usado para limitar o conjunto de resultados a nós que têm *all* das propriedades especificadas. O valor das propriedades não é considerado.

Todos são opcionais e podem ser combinados conforme necessário, mas você deve definir pelo menos um deles.

### Definições de gráfico {#chart-definitions}

```xml
N:charting
    N:settings
        N:active [cq:WidgetCollection]
        [
            N:<name> // array of nodes, each with the following property
                P:id   // must match the id of a child node of definitions
        ]
    N:definitions [cq:WidgetCollection]
    [
        N:<name> // array of nodes, each with the following properties
            P:id
            P:type
            // additional, chart type specific configurations
    ]
```

* `settings`

   Mantém definições para os gráficos ativos.

   * `active`

      Como várias configurações podem ser definidas, você pode usar essa opção para definir quais estão ativas no momento. Eles são definidos por uma matriz de nós (não há convenção de nomenclatura obrigatória para esses nós, mas os relatórios padrão geralmente usam `0`, `1`. `x`), cada um com a seguinte propriedade:

      * `id`

         Identificação dos gráficos ativos. Deve corresponder ao ID de um dos gráficos `definitions`.

* `definitions`

   Define os tipos de gráfico que estão potencialmente disponíveis para o relatório. O `definitions` a ser usado será especificado pelas configurações `active`.

   As definições são especificadas usando uma matriz de nós (mais uma vez chamada de `0`, `1`.. `x`), cada um com as seguintes propriedades:

   * `id`

      A identificação do gráfico.

   * `type`

      O tipo de gráfico disponível. Selecione de:

      * `pie`
Gráfico de pizza. Gerado somente a partir dos dados atuais.

      * `lineseries`
Série de linhas (pontos de conexão representando os instantâneos reais). Gerado somente a partir de dados históricos.
   * Propriedades adicionais estão disponíveis, dependendo do tipo de gráfico:

      * para o tipo de gráfico `pie`:

         * `maxRadius` ( `Double/Long`)

            O raio máximo permitido para o gráfico de pizza; portanto, o tamanho máximo permitido para o gráfico (sem legenda). Ignorado se `fixedRadius` estiver definido.

         * `minRadius` (  `Double/Long`)

            O raio mínimo permitido para o gráfico de pizza. Ignorado se `fixedRadius` estiver definido.

         * `fixedRadius` (  `Double/Long`) Define um raio fixo para o gráfico de pizza.
      * para o tipo de gráfico [`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals` (  `Boolean`)

            True se uma linha adicional mostrando o **Total** deve ser mostrada.
default: `false`

         * `series` (  `Long`)

            Número de linhas/séries a serem mostradas.
padrão: `9` (este também é o máximo permitido)

         * `hoverLimit` (  `Long`)

            Número máximo de instantâneos agregados (pontos mostrados em cada linha horizontal, representando valores distintos) para os quais os pop-ups devem ser exibidos, ou seja, quando o usuário passa o mouse sobre um valor distinto ou rótulo correspondente na legenda do gráfico.

            padrão: `35` (ou seja, nenhum pop-up será exibido se mais de 35 valores distintos forem aplicáveis às configurações do gráfico atual).

            Há um limite adicional de 10 pop-ups que podem ser exibidos em paralelo (vários pop-ups podem ser exibidos quando o mouse é passado sobre os textos da legenda).



### Caixa de diálogo Configuração {#configuration-dialog}

Cada relatório pode ter uma caixa de diálogo de configuração, permitindo que o usuário especifique vários parâmetros para o relatório. Essa caixa de diálogo é acessível por meio do botão **Edit** quando a página do relatório está aberta.

Essa caixa de diálogo é um CQ padrão [diálogo](/help/sites-developing/components-basics.md#dialogs) e pode ser configurada como tal (consulte [CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog) para obter mais informações).

Um exemplo de caixa de diálogo pode ter a seguinte aparência:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:Dialog"
    height="{Long}424">
    <items jcr:primaryType="cq:WidgetCollection">
        <props jcr:primaryType="cq:Panel">
            <items jcr:primaryType="cq:WidgetCollection">
                <title
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/title.infinity.json"
                    xtype="cqinclude"/>
                <description
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/description.infinity.json"
                    xtype="cqinclude"/>
                <rootPath
                    jcr:primaryType="cq:Widget"
                    fieldLabel="Root path"
                    name="./report/rootPath"
                    rootPath=""
                    rootTitle="Repository root"
                    xtype="pathfield"/>
                <processing
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/processing.infinity.json"
                    xtype="cqinclude"/>
                <scheduling
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/scheduling.infinity.json"
                    xtype="cqinclude"/>
            </items>
        </props>
    </items>
</jcr:root>
```

São fornecidos vários componentes pré-configurados; eles podem ser referenciados na caixa de diálogo, usando a propriedade `xtype` com um valor `cqinclude`:

* **`title`**

   `/libs/cq/reporting/components/commons/title`

   Campo de texto para definir o título do relatório.

* **`description`**

   `/libs/cq/reporting/components/commons/description`

   Área de texto para definir a descrição do relatório.

* **`processing`**

   `/libs/cq/reporting/components/commons/processing`

   Seletor para o modo de processamento do relatório (carregar dados manualmente/automaticamente).

* **`scheduling`**

   `/libs/cq/reporting/components/commons/scheduling`

   Seletor para programar instantâneos para o gráfico histórico.

>[!NOTE]
>
>Os componentes referenciados devem ser incluídos usando o sufixo `.infinity.json` (veja o exemplo acima).

### Caminho raiz {#root-path}

Além disso, um caminho raiz pode ser definido para o relatório:

* **`rootPath`**

   Isso limita o relatório a uma determinada seção (árvore ou subárvore) do repositório, que é recomendada para otimização de desempenho. O caminho raiz é especificado pela propriedade `rootPath` do nó `report` de cada página de relatório (obtido do modelo ao criar a página).

   Ele pode ser especificado por:

   * o [modelo de relatório](#report-template) (como um valor fixo ou como o valor padrão da caixa de diálogo de configuração).
   * o usuário (usando esse parâmetro)

## Componente base da coluna {#column-base-component}

Cada tipo de coluna requer um componente derivado de `/libs/cq/reporting/components/columnbase`.

Um componente de coluna define uma combinação dos seguintes itens:

* A configuração [Consulta Específica da Coluna](#column-specific-query).
* O [Resolvedores e pré-processamento](#resolvers-and-preprocessing).
* As [Definições Específicas da Coluna](#column-specific-definitions) (como filtros e agregados; `definitions` nó filho).
* [Valores padrão da coluna](#column-default-values).
* O [Filtro de Cliente](#client-filter) para extrair as informações a serem exibidas dos dados retornados pelo servidor.
* Além disso, um componente de coluna deve fornecer uma instância adequada de `cq:editConfig`. para definir os [Eventos e Ações](#events-and-actions) necessários.
* A configuração para [colunas genéricas](#generic-columns).

```
N:<columnname> [cq:Component]
    P:componentGroup
    P:jcr:title
    P:sling:resourceSuperType = "cq/reporting/components/columnbase"
    N:cq:editConfig [cq:EditConfig] // <a href="#events-and-actions">Events and Actions</a>
    N:defaults // <a href="#column-default-values">Column Default Values</a>
    N:definitions
      N:queryBuilder // <a href="#column-specific-query">Column Specific Query</a>
        P:property [String|String[]] // Column Specific Query
        P:subPath // Column Specific Query
        P:secondaryProperty [String|String[]] // Column Specific Query
        P:secondarySubPath // Column Specific Query
      N:data
        P:clientFilter [String] // <a href="#client-filter">Client Filter</a>
        P:resolver // <a href="#resolvers-and-preprocessing">Resolvers and Preprocessing</a>
        N:resolverConfig // Resolvers and Preprocessing
        N:preprocessing // Resolvers and Preprocessing
      P:type // <a href="#column-specific-definitions">Column Specific Definitions</a>
      P:groupable [Boolean] // Column Specific Definitions
      N:filters [cq:WidgetCollection] // Column Specific Definitions
      N:aggregates [cq:WidgetCollection] // Column Specific Definitions
```

Consulte também [Definindo seu novo relatório](#defining-your-new-report).

### Consulta específica da coluna {#column-specific-query}

Isso define a extração de dados específica (do [conjunto de resultados de dados do relatório](#the-query-and-data-retrieval)) para usar na coluna individual.

```xml
N:definitions
    N:queryBuilder
        P:property [String|String[]]
        P:subPath
        P:secondaryProperty [String|String[]]
        P:secondarySubPath
```

* `property`

   Define a propriedade a ser usada para calcular o valor real da célula.

   Se a propriedade estiver definida como String[] várias propriedades serão digitalizadas (em sequência) para localizar o valor real.

   Por exemplo, no caso de:

   `property = [ "jcr:lastModified", "jcr:created" ]`

   O extrator de valor correspondente (que está sob controle aqui) irá:

   * Verifique se há uma propriedade jcr:lastModified disponível e, em caso positivo, use-a.
   * Se nenhuma propriedade jcr:lastModified estiver disponível, o conteúdo de jcr:created será usado.

* `subPath`

   Se o resultado não estiver localizado no nó retornado pelo query, `subPath` define onde a propriedade está realmente localizada.

* `secondaryProperty`

   Define uma segunda propriedade que também deve ser usada para calcular o valor real da célula; isso só será usado para determinados tipos de coluna (diff e sortable).

   Por exemplo, no caso do Relatório de instâncias de fluxo de trabalho, a propriedade especificada é usada para armazenar o valor real da diferença de tempo (em milissegundos) entre as horas de início e de fim.

* `secondarySubPath`

   Semelhante ao subPath, quando `secondaryProperty` é usado.

Na maioria dos casos, somente `property` será usado.

### Filtro do cliente {#client-filter}

O filtro cliente extrai as informações a serem exibidas, dos dados retornados pelo servidor.

>[!NOTE]
>
>Esse filtro é executado no lado do cliente, depois que todo o processamento no lado do servidor for aplicado.

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter` é definida como uma função JavaScript que:

* como entrada, recebe um parâmetro; os dados retornados do servidor (portanto, totalmente pré-processados)
* como saída, retorna o valor filtrado (processado); os dados extraídos ou derivados das informações de entrada

O exemplo a seguir extrai o caminho de página correspondente de um caminho de componente:

```
function(v) {
    var sepPos = v.lastIndexOf('/jcr:content');
    if (sepPos < 0) {
        return v;
    }
    return v.substring(sepPos + '/jcr:content'.length, v.length);
}
```

### Resolvedores e pré-processamento {#resolvers-and-preprocessing}

A [fila de processamento](#processing-queue) define os vários resolvedores e configura o pré-processamento:

```xml
N:definitions
    N:data
        P:resolver
        N:resolverConfig
        N:preprocessing
            N:apply
            N:applyAfter
```

* `resolver`

   Define o resolvedor a ser usado. Os seguintes resolvedores estão disponíveis:

   * `const`

      Mapeia valores para outros valores; por exemplo, isso é usado para resolver constantes como `en` para seu valor equivalente `English`.

   * `default`

      O resolvedor padrão. Este é um resolvedor fictício que na verdade não resolve nada.

   * `page`

      Resolve um valor de caminho para o caminho da página apropriada; com mais precisão, no nó `jcr:content` correspondente. Por exemplo, `/content/.../page/jcr:content/par/xyz` é resolvido para `/content/.../page/jcr:content`.

   * `path`

      Resolve um valor de caminho ao anexar opcionalmente um subcaminho e pegar o valor real de uma propriedade do nó (conforme definido por `resolverConfig`) no caminho resolvido. Por exemplo, um `path` de `/content/.../page/jcr:content` pode ser resolvido para o conteúdo da propriedade `jcr:title`, isso significaria que um caminho de página é resolvido para o título da página.

   * `pathextension`

      Resolve um valor anexando um caminho e obtendo o valor real de uma propriedade do nó no caminho resolvido. Por exemplo, um valor `de` pode ser anexado por um caminho como `/libs/wcm/core/resources/languages`, tomando o valor da propriedade `language`, para resolver o código do país `de` para a descrição do idioma `German`.

* `resolverConfig`

   Fornece definições para o resolvedor; as opções disponíveis dependem do `resolver` selecionado:

   * `const`

      Use as propriedades para especificar as constantes para resolução. O nome da propriedade define a constante a ser resolvida; o valor da propriedade define o valor resolvido.

      Por exemplo, uma propriedade com **Name**= `1` e **Value** `=One` resolverá 1 para Um.

   * `default`

      Nenhuma configuração disponível.

   * `page`

      * `propertyName` (opcional)

         Define o nome da propriedade que deve ser usada para resolver o valor. Se não especificado, é usado o valor padrão de *jcr:title* (o título da página); para o resolvedor `page`, isso significa que primeiro o caminho é resolvido para o caminho da página e depois para o título da página.
   * `path`

      * `propertyName` (opcional)

         Especifica o nome da propriedade que deve ser usada para resolver o valor. Se não especificado, o valor padrão de `jcr:title` é usado.

      * `subPath` (opcional)

         Essa propriedade pode ser usada para especificar um sufixo a ser anexado ao caminho antes que o valor seja resolvido.
   * `pathextension`

      * `path` (mandatory)

         Define o caminho a ser anexado.

      * `propertyName` (obrigatório)

         Define a propriedade no caminho resolvido, onde o valor real está localizado.

      * `i18n` (facultativo; type Boolean)

         Determina se o valor resolvido deve ser *internacionalizado* (ou seja, usando [serviços de internacionalização do CQ5](/help/sites-administering/tc-manage.md)).



* `preprocessing`

   O pré-processamento é opcional e pode ser vinculado (separadamente) às fases de processamento *apply* ou *applyAfter*:

   * `apply`

      A fase de pré-processamento inicial ([etapa 3 na representação da fila de processamento](#processing-queue)).

   * `applyAfter`

      Aplique após o pré-processamento ([etapa 9 na representação da fila de processamento](#processing-queue)).

#### Resolvedores {#resolvers}

Os resolvedores são usados para extrair as informações necessárias. Exemplos dos vários resolvedores são:

**Const**

O seguinte resolverá um valor de conteúdo de `VersionCreated` na string `New version created`.

Consulte `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**Página**

Resolve um valor de caminho para a propriedade jcr:description no nó jcr:content (filho) da página correspondente.

Consulte `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**Caminho**

O seguinte resolve um caminho de `/content/.../page` para o conteúdo da propriedade `jcr:title`, isso significaria que um caminho de página é resolvido para o título da página.

Consulte `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**Extensão do caminho**

O seguinte prepara um valor `de` com a extensão de caminho `/libs/wcm/core/resources/languages`, em seguida, pega o valor da propriedade `language`, para resolver o código do país `de` para a descrição do idioma `German`.

Consulte `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### Pré-processamento {#preprocessing}

A definição `preprocessing` pode ser aplicada a:

* valor original:

   A definição de pré-processamento do valor original é especificada diretamente em `apply` e/ou `applyAfter`.

* no seu estado agregado:

   Se necessário, pode ser apresentada uma definição separada para cada agregação.

   Para especificar o pré-processamento explícito para valores agregados, as definições de pré-processamento têm de residir em um `aggregated` nó filho respectivo ( `apply/aggregated`, `applyAfter/aggregated`). Se o pré-processamento explícito para agregações distintas for necessário, a definição de pré-processamento estará localizada em um nó filho com o nome da respectiva agregação (por exemplo `apply/aggregated/min/max` ou outras agregações).

Você pode especificar um dos seguintes itens a serem usados durante o pré-processamento:

* [localizar e substituir ](#preprocessing-find-and-replace-patterns)
padrões. Quando encontrado, o padrão especificado (que é definido como uma expressão regular) é substituído por outro padrão; por exemplo, isso pode ser usado para extrair uma substring do original.

* [formatadores de tipo de dados](#preprocessing-data-type-formatters)

   Converte um valor numérico em uma string relativa; por exemplo, o valor &quot;representando uma diferença de tempo de 1 hora seria resolvido em uma string como `1:24PM (1 hour ago)`.

Por exemplo:

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply|applyAfter
                P:pattern         // regex
                P:replace         // replacement for regex
                // and/or
                P:format          // data type formatter
```

#### Pré-processamento - localizar e substituir padrões {#preprocessing-find-and-replace-patterns}

Para o pré-processamento, você pode especificar um `pattern` (definido como [expressão regular](https://en.wikipedia.org/wiki/Regular_expression) ou regex) que está localizado e, em seguida, substituído pelo padrão `replace`:

* `pattern`

   A expressão regular usada para localizar uma substring.

* `replace`

   A string, ou representação da string, que será usada como substituição da string original. Geralmente, isso representa uma substring da string localizada pela expressão regular `pattern`.

Um exemplo de substituição pode ser detalhado como:

* Para o nó `definitions/data/preprocessing/apply` com as duas propriedades a seguir:

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`:  `$1`

* Uma string chegando como:

   * `/content/geometrixx/en/services/jcr:content/par/text`

* Serão divididas em quatro seções:

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` -  `(/jcr:content)` -  `/jcr:content`
   * `$3` -  `(/|$)` -  `/`
   * `$4` -  `(.*)` -  `par/text`

* E substituído pela string representada por `$1`:

   * `/content/geometrixx/en/services`

#### Pré-processamento - Tipo de dados para assuntos {#preprocessing-data-type-formatters}

Esses formatadores convertem um valor numérico em uma string relativa.

Por exemplo, isso pode ser usado para uma coluna de tempo que permite agregados `min`, `avg` e `max`. Como `min`/ `avg`/ `max` os agregados são exibidos como uma *diferença de tempo* (por exemplo, `10 days ago`), eles exigem um formatador de dados. Para isso, um formatador `datedelta` é aplicado aos valores agregados `min`/ `avg`/ `max`. Se uma agregação `count` também estiver disponível, isso não precisará de um formatador, nem o valor original.

Atualmente, os formatos de tipo de dados disponíveis são:

* `format`

   Formatador do tipo de dados:

   * `duration`

      Duração é o período entre duas datas definidas. Por exemplo, o início e o fim de uma ação de workflow que levou 1 hora, começando em 13/02/11 11:23 e terminando uma hora depois em 13/02/11 12:23.

      Ele converte um valor numérico (interpretado como milissegundos) em uma string de duração; por exemplo, `30000` é formatado como * `30s`.*

   * `datedelta`

      Dados são o período entre uma data no passado e &quot;agora&quot; (portanto, terá um resultado diferente se o relatório for visualizado em um ponto no tempo posterior).

      Ele converte o valor numérico (interpretado como uma diferença de tempo em dias) em uma string de data relativa. Por exemplo, 1 é formatado como um dia atrás.

O exemplo a seguir define `datedelta` formatação para `min` e `max` agregações:

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply
                N:aggregated
                    N:min
                        P:format = "datedelta"
                    N:max
                        P:format = "datedelta"
```

### Definições específicas da coluna {#column-specific-definitions}

As definições específicas da coluna definem os filtros e agregações disponíveis para essa coluna.

```xml
N:definitions
    P:type
    P:groupable [Boolean]
    N:filters [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:filterType
            P:id
            P:phase
    ]
    N:aggregates [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:text
            P:type
    ]
```

* `type`

   As opções a seguir estão disponíveis como opções padrão:

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

      É usado para extrair partes de uma data necessária para agregação (por exemplo, grupo por ano para obter dados agregados para cada ano).

   * `sortable`

      É usado para valores que usam valores diferentes (obtidos de propriedades diferentes) para classificação e exibição.
   Além disso. qualquer um destes valores pode ser definido como valor múltiplo; por exemplo, `string[]` define uma matriz de sequências de caracteres.

   O extrator de valor é escolhido pelo tipo de coluna. Se um extrator de valor estiver disponível para um tipo de coluna, esse extrator será usado. Caso contrário, o extrator do valor padrão será usado.

   Um tipo pode (opcionalmente) tomar um parâmetro. Por exemplo, `timeslot:year` extrai o ano de um campo de data. Tipos com seus parâmetros:

   * `timeslot` - Os valores são comparáveis às constantes correspondentes de  `java.utils.Calendar`.

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` -  `Calendar.MONTH`
      * `timeslot:week-of-year` -  `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` -  `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` -  `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` -  `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` -  `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` -  `Calendar.MINUTE`


* `groupable`

   Define se o relatório pode ser agrupado por essa coluna.

* `filters`

   Definições de filtro.

   * `filterType`

      Os filtros disponíveis são:

      * `string`

         Um filtro baseado em string.
   * `id`

      Identificador de filtro.

   * `phase`

      Fases disponíveis:

      * `raw`

         O filtro é aplicado aos dados brutos.

      * `preprocessed`

         O filtro é aplicado aos dados pré-processados.

      * `resolved`

         O filtro é aplicado aos dados resolvidos.


* `aggregates`

   Definições agregadas.

   * `text`

      Nome textual da agregação. Se `text` não for especificado, ele terá a descrição padrão da agregação; por exemplo, `minimum` será usado para a agregação `min`.

   * `type`

      Tipo agregado. Os agregados disponíveis são:

      * `count`

         Conta o número de linhas.

      * `count-nonempty`

         Conta o número de linhas não vazias.

      * `min`

         Fornece o valor mínimo.

      * `max`

         Fornece o valor máximo.

      * `average`

         Fornece o valor médio.

      * `sum`

         Fornece a soma de todos os valores.

      * `median`

         Fornece o valor mediano.

      * `percentile95`

         Obtém o 95º percentil de todos os valores.

### Valores padrão da coluna {#column-default-values}

Isso é usado para definir valores padrão para a coluna:

```xml
N:defaults
    P:aggregate
```

* `aggregate`

   Os valores válidos de `aggregate` são iguais aos de `type` em `aggregates` (consulte [Definições específicas de coluna (definições - filtros/agregações)](#column-specific-definitions) ).

### Eventos e ações {#events-and-actions}

Editar configuração define os eventos necessários para os ouvintes detectarem e as ações a serem aplicadas após esses eventos. Consulte a [introdução ao desenvolvimento de componentes](/help/sites-developing/components.md) para obter informações de fundo.

Os seguintes valores devem ser definidos para garantir que todas as ações necessárias sejam atendidas:

```xml
N:cq:editConfig [cq:EditConfig]
    P:cq:actions [String[]] = "insert", "delete"
    P:cq:dialogMode = "floating"
    P:cq:layout = "auto"
    N:cq:listeners [cq:EditListenersConfig]
        P:aftercreate = "REFRESH_INSERTED"
        P:afterdelete = "REFRESH_SELF"
        P:afteredit = "REFRESH_SELF"
        P:afterinsert = "REFRESH_INSERTED"
        P:aftermove = "REFRESH_SELF"
        P:afterremove = "REFRESH_SELF"
```

### Colunas Genéricas {#generic-columns}

Colunas genéricas são uma extensão em que (a maioria das) as definições da coluna são armazenadas na instância do nó da coluna (em vez do nó do componente).

Eles usam uma caixa de diálogo (padrão), que você personaliza, para o componente genérico individual. Essa caixa de diálogo permite que o usuário do relatório defina as propriedades da coluna de uma coluna genérica na página do relatório (usando a opção de menu **Column properties...**).

Um exemplo é a coluna **Generic** do **Relatório do Usuário**; consulte `/libs/cq/reporting/components/userreport/genericcol`.

Para tornar uma coluna genérica:

* Defina a propriedade `type` do nó `definition` da coluna para `generic`.

   Consulte `/libs/cq/reporting/components/userreport/genericcol/definitions`

* Especifique uma definição de diálogo (padrão) no nó `definition` da coluna.

   Consulte `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * Os campos da caixa de diálogo devem se referir aos mesmos nomes da propriedade de componente correspondente (incluindo seu caminho).

      Por exemplo, se você quiser tornar o tipo da coluna genérica configurável por meio da caixa de diálogo, use um campo com o nome `./definitions/type`.

   * As propriedades definidas usando a interface/caixa de diálogo têm prioridade sobre as definidas no componente `columnbase`.

* Defina a Configuração de edição.

   Consulte `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* Use metodologias de AEM padrão para definir propriedades de coluna (adicionais).

   Observe que para propriedades definidas nas instâncias de componente e coluna, o valor na instância da coluna tem prioridade.

   As propriedades disponíveis para uma coluna genérica são:

   * `jcr:title` - nome da coluna
   * `definitions/aggregates` - agregados
   * `definitions/filters` - filtros
   * `definitions/type`- o tipo da coluna (isso deve ser definido na caixa de diálogo, usando um seletor/caixa de combinação ou um campo oculto)
   * `definitions/data/resolver` e  `definitions/data/resolverConfig` (mas não  `definitions/data/preprocessing` ou  `.../clientFilter`) - o resolvedor e a configuração
   * `definitions/queryBuilder` - a configuração do construtor de consultas
   * `defaults/aggregate` - o agregado padrão

   No caso de uma nova instância da coluna genérica no **Relatório do usuário** as propriedades definidas com a caixa de diálogo são persistentes em:

   `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## Design do relatório {#report-design}

O design define quais tipos de coluna estão disponíveis para criar um relatório. Também define o sistema de parágrafo ao qual as colunas são adicionadas.

É altamente recomendável criar um design individual para cada relatório. Isso garante total flexibilidade. Consulte também [Definindo seu novo relatório](#defining-your-new-report).

Os componentes de relatório padrão são mantidos em `/etc/designs/reports`.

A localização dos relatórios pode depender de onde você localizou seus componentes:

* `/etc/designs/reports/<yourReport>` é adequado se o relatório estiver localizado abaixo de  `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` para relatórios que usam o  `/apps/<yourProject>/reports` padrão

As propriedades de design necessárias são registradas em `jcr:content/reportpage/report/columns` (por exemplo, `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`):

* `components`

   Quaisquer componentes e/ou grupos de componentes permitidos no relatório.

* `sling:resourceType`

   Propriedade com valor `cq/reporting/components/repparsys`.

Um trecho de design de exemplo (retirado do design do relatório de componente) é:

```xml
<!-- ... -->
    <jcr:content
        jcr:primaryType="nt:unstructured"
        jcr:title="Component Report"
        sling:resourceType="wcm/core/components/designer">
        <reportpage jcr:primaryType="nt:unstructured">
            <report jcr:primaryType="nt:unstructured">
                <columns
                    jcr:primaryType="nt:unstructured"
                    sling:resourceType="cq/reporting/components/repparsys"
                    components="group:Component Report"/>
            </report>
        </reportpage>
    </jcr:content>
<!-- ... -->
```

Não é necessário especificar designs para colunas individuais. As colunas disponíveis podem ser definidas no modo de design.

>[!NOTE]
>
>É recomendável não fazer alterações nos designs de relatório padrão. Isso garante que você não perca nenhuma alteração ao atualizar ou instalar hotfixes.
>
>Copie o relatório e seu design se desejar personalizar um relatório padrão.

>[!NOTE]
>
>Colunas padrão podem ser criadas automaticamente quando um relatório é criado. Eles são especificados no template.

## Modelo de relatório {#report-template}

Cada tipo de relatório deve fornecer um template. Esses são os [Modelos CQ](/help/sites-developing/templates.md) padrão e podem ser configurados como tal.

O modelo deve:

* defina `sling:resourceType` para `cq/reporting/components/reportpage`

* indicar o projeto a utilizar
* crie um nó filho `report` que faça referência ao componente do contêiner ( `reportbase`) por meio da propriedade `sling:resourceType`

Um trecho de modelo de exemplo (retirado do modelo de relatório de componente) é:

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/compreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

Um trecho de modelo de exemplo, mostrando a definição do caminho raiz (retirado do modelo de relatório do usuário), é:

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/userreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            rootPath="/home/users"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

Os modelos de relatório padrão são mantidos em `/libs/cq/reporting/templates`.

No entanto, é altamente recomendável não atualizar esses nós, mas criar seus próprios nós de componente em `/apps/cq/reporting/templates` ou se for mais apropriado `/apps/<yourProject>/reports/templates`.

Onde, como exemplo (consulte também [Localização dos componentes do relatório](#location-of-report-components)):

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

Abaixo, você cria a raiz do modelo:

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## Criar Seu Próprio Relatório - Um Exemplo {#creating-your-own-report-an-example}

### Definição De Seu Novo Relatório {#defining-your-new-report}

Para definir um novo relatório, você deve criar e configurar:

1. A raiz dos componentes do relatório.
1. O componente básico do relatório.
1. Um ou mais componentes de base de coluna.
1. O design do relatório.
1. A raiz do seu modelo de relatório.
1. O modelo de relatório.

Para ilustrar essas etapas, o exemplo a seguir define um relatório que lista todas as configurações OSGi no repositório; ou seja, todas as instâncias do nó `sling:OsgiConfig`.

>[!NOTE]
>
>Copiar um relatório existente e, em seguida, personalizar a nova versão é um método alternativo.

1. Crie o nó raiz do novo relatório.

   Por exemplo, em `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. Defina sua base de relatórios. Por exemplo `osgireport[cq:Component]` em `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:osgireport [sling:Folder]
       N:osgireport [cq:Component]
           P:sling:resourceSuperType [String] = "cq/reporting/components/reportbase"
           N:charting [nt:unstructured]
               N:settings [nt:unstructured]
                   N:active [cq:WidgetCollection]
                       N:0 [nt:unstructured]
                           P:id [String] = "pie"
                       N:1 [nt:unstructured]
                           P:id [String] = "lineseries"
               N:definitions [cq:WidgetCollections]
                   N:0 [nt:unstructured]
                       P:id [String] = "pie"
                       P:maxRadius [Long] = 180
                       P:type [String] = "pie"
                   N:1 [nt:unstructured]
                       P:id [String] = "lineseries"
                       P:type [String] = "lineseries"
           N:dialog [cq:Dialog]
               P:height [Long] = 424
               N:items [cq:WidgetCollection]
                   N:props [cq:Panel]
                       N:items [cq:WidgetCollection]
                           N:title [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/title.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:description [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/description.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:rootPath [cq:Widget]
                               P:fieldLabel [String] = "Root path"
                               P:name [String] = "./report/rootPath"
                               P:xtype [String] = "pathfield"
                           N:processing [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/processing.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:scheduling [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/scheduling.infinity.json"
                               P:xtype [String] = "cqinclude"
           N:queryBuilder [nt:unstructured]
               P:nodeTypes [String[]] = "sling:OsgiConfig"
   ```

   Isso define um componente de base de relatório que:

   * procura por todos os nós do tipo `sling:OsgiConfig`
   * exibe os gráficos `pie` e `lineseries`
   * fornece uma caixa de diálogo para o usuário configurar o relatório

1. Defina o componente da primeira coluna (columnbase). Por exemplo `bundlecol[cq:Component]` em `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:osgireport [sling:Folder]
       N:bundlecol [cq:Component]
           P:componentGroup [String] = "OSGi Report"
           P:jcr:title = "Bundle"
           P:sling:resourceSuperType [String] = "cq/reporting/components/columnbase"
           N:cq:editConfig [cq:EditConfig]
               P:cq:actions [String[]] = "insert", "delete"
               P:cq:dialogMode [String] = "floating"
               P:cq:layout [String] = "auto"
               N:cq:listeners [cq:EditListenersConfig]
                   P:aftercreate [String] "REFRESH_INSERTED"
                   P:afterdelete [String] "REFRESH_SELF"
                   P:afteredit [String] "REFRESH_SELF"
                   P:afterinsert [String] "REFRESH_INSERTED"
                   P:aftermove [String] "REFRESH_SELF"
                   P:afterremove [String] "REFRESH_SELF"
           N:defaults [nt:unstructured]
               P:aggregate [String] = "count"
           N:definitions [nt:unstructured]
               P:groupable [Boolean] = false
               P:type [String] = "string"
               N:queryBuilder [nt:unstructured]
                   P:property [String] = "jcr:path"
   ```

   Isso define um componente base de coluna que:

   * pesquisa e retorna o valor recebido do servidor; nesse caso, a propriedade `jcr:path` para cada nó `sling:OsgiConfig`
   * fornece a agregação `count`
   * não é agrupável
   * tem o título `Bundle` (título da coluna dentro da tabela)
   * está no grupo de sidekick `OSGi Report`
   * é atualizado em eventos especificados

   >[!NOTE]
   >
   >Neste exemplo, não há definições de `N:data` e `P:clientFilter`. Isso ocorre porque o valor recebido do servidor é retornado em uma base 1:1 - que é o comportamento padrão.
   >
   >É o mesmo que as definições:
   >
   >
   ```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >Onde a função simplesmente retorna o valor recebido.

1. Defina o design do relatório. Por exemplo `osgireport[cq:Page]` em `/etc/designs/reports`.

   ```xml
   N:osgireport [cq:Page]
       N:jcr:content [nt:unstructured]
           P:jcr:title [String] = "OSGi report"
           P:sling:resourceType [String] = "wcm/core/components/designer"
           N:reportpage [nt:unstructured]
               N:report [nt:unstructured]
                   N:columns [nt:unstructured]
                       P:components [String] = "group:OSGi Report"
                       P:sling:resourceType [String] = "cq/reporting/components/repparsys"
   ```

1. Crie o nó raiz do novo modelo de relatório.

   Por exemplo, em `/apps/cq/reporting/templates/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. Defina seu template de relatório. Por exemplo `osgireport[cq:Template]` em `/apps/cq/reporting/templates`.

   ```xml
   N:osgireport [cq:Template]
       P:allowedPaths [String[]] = "/etc/reports(/.*)?"
       P:jcr:description [String] = "Use this report generator to create a new OSGi report."
       P:jcr:title [String] = "OSGi Report Template"
       P:ranking [Long] = 100
       P:shortTitle [String] = "OSGi Report"
       N:jcr:content [cq:PageContent]
           P:cq:designPath [String] = "/etc/designs/reports/osgireport"
           P:sling:resourceType [String] = "cq/reporting/components/reportpage"
           N:report [nt:unstructured]
               P:rootPath [String] = "/"
               P:sling:resourceType [String] = "cq/reporting/components/osgireport/osgireport"
       N:thumbnail.png [nt:file]
   ```

   Isso define um modelo que:

   * define o `allowedPaths` para os relatórios resultantes - no caso acima, em qualquer lugar em `/etc/reports`
   * fornece títulos e descrições para o modelo
   * O fornece uma imagem em miniatura para uso na lista de modelos (a definição completa desse nó não está listada acima - é mais fácil copiar uma instância de thumbnail.png de um relatório existente).

### Criação de uma instância do seu novo relatório {#creating-an-instance-of-your-new-report}

Uma instância do novo relatório pode ser criada:

1. Abra o console **Ferramentas**.

1. Selecione **Relatórios** no painel esquerdo.
1. Em seguida **Novo...** na barra de ferramentas. Defina um **Título** e **Nome**, selecione o novo tipo de relatório (o **Modelo de Relatório OSGi**) na lista de modelos e clique em **Criar**.
1. A nova instância do relatório será exibida na lista. Clique duas vezes para abrir.
1. Arraste um componente (por exemplo, **Pacote** no grupo **Relatório OSGi**) do sidekick para criar a primeira coluna e [iniciar a definição do relatório](/help/sites-administering/reporting.md#the-basics-of-report-customization).

   >[!NOTE]
   >
   >Como este exemplo não tem nenhuma coluna agrupável, os gráficos não estarão disponíveis. Para ver gráficos, defina `groupable` para `true`:
   >
   >
   ```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```

## Configuração dos serviços de estrutura de relatórios {#configuring-the-report-framework-services}

Esta seção descreve opções de configuração avançadas para os serviços OSGi que implementam a estrutura do relatório.

Elas podem ser visualizadas usando o menu Configuração do console da Web (disponível, por exemplo, em `http://localhost:4502/system/console/configMgr`). Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

### Serviço básico (Configuração de relatórios Day CQ) {#basic-service-day-cq-reporting-configuration}

* **** O fuso horário define os dados históricos do fuso horário que são criados. Isso garante que o gráfico histórico exiba os mesmos dados para cada usuário em todo o mundo.
* **** Localedefine o local a ser usado em conjunto com o  **** Fuso horário dos dados históricos. A localidade é usada para determinar algumas configurações específicas de localidade do calendário (por exemplo, se o primeiro dia de uma semana é domingo ou segunda).

* **Os** caminhos de instantâneo definem o caminho raiz onde os instantâneos dos gráficos históricos são armazenados.
* **Caminho para** relatórios define o caminho onde os relatórios estão localizados. Isso é usado pelo serviço de instantâneos para determinar os relatórios para os quais os instantâneos serão realmente capturados.
* **Os** instantâneos diários definem a hora de cada dia em que os instantâneos diários são tirados. A hora especificada está no fuso horário local do servidor.
* **Os** instantâneos por hora definem o minuto de cada hora em que os instantâneos por hora são tirados.
* **As linhas (máx.)** definem o número máximo de linhas armazenadas para cada instantâneo. Este valor deve ser razoavelmente escolhido; se for muito alto, isso afetará o tamanho do repositório, se for muito baixo, os dados podem não ser precisos devido à maneira como os dados históricos são tratados.
* **Os dados** falsos, se ativados, podem ser criados usando o  `fakedata` seletor; se estiver desativado, o uso do  `fakedata` seletor lançará uma exceção.

   Como os dados são falsos, eles devem *somente* ser usados para fins de teste e depuração.

   Usar o seletor `fakedata` concluirá o relatório implicitamente, de modo que todos os dados existentes serão perdidos; Os dados podem ser restaurados manualmente, mas esse pode ser um processo demorado.

* **O** usuário de instantâneo define um usuário opcional que pode ser usado para captura de instantâneos.

   Basicamente, os instantâneos são tirados para o usuário que concluiu o relatório. Pode haver situações (por exemplo, em um sistema de publicação, em que esse usuário não existe, pois sua conta não foi replicada) em que você deseja especificar um usuário de fallback que é usado.

   Além disso, especificar um usuário pode impor um risco à segurança.

* **Impor usuário** de snapshot, se ativado, todos os snapshots serão capturados com o usuário especificado em Usuário  *de Snapshot*. Isso pode ter graves impactos na segurança se não for tratado corretamente.

### Configurações de cache (Cache de relatório Day CQ) {#cache-settings-day-cq-reporting-cache}

* **** Habilitar permite habilitar ou desabilitar o armazenamento em cache de dados de relatórios. Ativar o cache de relatório manterá os dados do relatório na memória durante várias solicitações. Isso pode aumentar o desempenho, mas resultará em maior consumo de memória e, em circunstâncias extremas, pode levar a situações de falta de memória.
* **** O TTL define o tempo (em segundos) para o qual os dados do relatório são armazenados em cache. Um número maior aumentará o desempenho, mas também poderá retornar dados imprecisos se os dados forem alterados dentro do período de tempo.
* **Máximo de** entradas define o número máximo de relatórios que serão armazenados em cache de uma vez.

>[!NOTE]
>
>Os dados do relatório podem ser diferentes para cada usuário e idioma. Portanto, os dados do relatório são armazenados em cache por relatório, usuário e idioma. Isso significa que um valor **Máximo de entradas** de `2` realmente armazena dados em cache para:
>
>* um relatório para dois usuários com configurações de idioma diferentes
>* um usuário e dois relatórios

>


