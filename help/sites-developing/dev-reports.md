---
title: Desenvolvimento de relatórios
description: O Adobe Experience Manager (AEM) fornece uma seleção de relatórios padrão com base em uma estrutura de relatórios
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '5177'
ht-degree: 0%

---


# Desenvolvimento de relatórios {#developing-reports}

O Adobe Experience Manager (AEM) fornece uma seleção de [relatórios padrão](/help/sites-administering/reporting.md), a maioria dos quais com base em uma estrutura de relatórios.

Usando a estrutura, você pode estender esses relatórios padrão ou desenvolver seus próprios novos relatórios. A estrutura de relatórios integra-se perfeitamente aos conceitos e princípios existentes do CQ5 para que os desenvolvedores possam usar seu conhecimento existente sobre o CQ5 como um trampolim para o desenvolvimento de relatórios.

Para os relatórios padrão entregues com AEM:

* Esses relatórios se baseiam na estrutura de relatórios:

   * [Relatório do componente](/help/sites-administering/reporting.md#component-report)
   * [Relatório de atividades de página](/help/sites-administering/reporting.md#page-activity-report)
   * [Relatório do usuário](/help/sites-administering/reporting.md#user-report)
   * [Relatório de instâncias do fluxo de trabalho](/help/sites-administering/reporting.md#workflow-instance-report)

* Os seguintes relatórios baseiam-se em princípios individuais e, por conseguinte, não podem ser alargados:

   * [Uso do disco](/help/sites-administering/reporting.md#disk-usage)
   * [Verificação de integridade](/help/sites-administering/reporting.md#health-check)
   * [Relatório de fluxo de trabalho](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>O tutorial [Criando Seu Próprio Relatório - Um Exemplo](#creating-your-own-report-an-example) também mostra quantos dos princípios abaixo podem ser usados.
>
>Você também pode consultar os relatórios padrão para ver outros exemplos de implementação.

>[!NOTE]
>
>Nos exemplos e definições abaixo, a seguinte notação é usada:
>
>* Cada linha define um nó ou uma propriedade em que:
>  `N:<name> [<nodeType>]` : descreve um nó com o nome de `<*name*>` e o tipo de nó de `<*nodeType*>`*.*
>  `P:<name> [<propertyType]` : descreve uma propriedade com o nome de `<*name*>` e um tipo de propriedade de `<*propertyType*>`.
>  `P:<name> = <value>` : descreve uma propriedade `<name>` que deve ser definida como o valor de `<value>`.
>
>* Recuo mostra as dependências hierárquicas entre os nós.
>* Itens separados por | indica uma lista de itens possíveis; por exemplo, tipos ou nomes; por exemplo, `String|String[]` significa que a propriedade pode ser String ou String[].
>
>* `[]` descreve uma matriz; como Cadeia de Caracteres[] ou uma matriz de nós como na [Definição de Consulta](#query-definition).
>
>Salvo indicação em contrário, os tipos padrão são:
>
>* Nós - `nt:unstructured`
>* Propriedades - `String`

## Estrutura de relatórios {#reporting-framework}

O quadro de comunicação de informações assenta nos seguintes princípios:

* É totalmente baseada em conjuntos de resultados que são retornados por uma consulta executada pelo QueryBuilder do CQ5.
* O conjunto de resultados define os dados exibidos no relatório. Cada linha no conjunto de resultados corresponde a uma linha na exibição tabular do relatório.
* As operações disponíveis para execução no conjunto de resultados assemelham-se aos conceitos de RDBMS; principalmente *agrupamento* e *agregação*.

* A maioria da recuperação e do processamento de dados é feita no lado do servidor.
* O cliente é o único responsável pela exibição dos dados pré-processados. Somente tarefas de processamento secundárias (por exemplo, criar links no conteúdo da célula) são executadas no lado do cliente.

A estrutura de relatórios (ilustrada pela estrutura de um relatório padrão) usa os seguintes blocos fundamentais, alimentados pela fila de processamento:

![chlimage_1-248](assets/chlimage_1-248.png)

### Página do relatório {#report-page}

A página do relatório é:

* Uma página CQ5 padrão.
* Com base em um [modelo CQ5 padrão, configurado para o relatório](#report-template).

### Base de Relatório {#report-base}

O componente [`reportbase` ](#report-base-component) forma a base de qualquer relatório porque ele:

* Preserva a definição da [consulta](#the-query-and-data-retrieval) que fornece o conjunto de resultados subjacente de dados.

* É um sistema de parágrafo adaptado que contém todas as colunas ( `columnbase`) adicionadas ao relatório.
* Define quais tipos de gráfico estão disponíveis e quais estão ativos no momento.
* Define a caixa de diálogo Editar, que permite ao usuário configurar determinados aspectos do relatório.

### Base da coluna {#column-base}

Cada coluna é uma instância do [`columnbase` componente](#column-base-component) que:

* É um parágrafo, usado pelo parsys ( `reportbase`) do respectivo relatório.
* Define o link para o [conjunto de resultados subjacente](#the-query-and-data-retrieval). Ou seja, define os dados específicos referenciados nesse conjunto de resultados e como ele é processado.
* Mantém definições adicionais; como as agregações e os filtros disponíveis, juntamente com quaisquer valores padrão.

### O Query e a Recuperação de Dados {#the-query-and-data-retrieval}

A consulta:

* É definido como parte do componente [`reportbase`](#report-base).
* É baseado no [QueryBuilder](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/QueryBuilder.html) do CQ.
* Recupera os dados usados como base do relatório. Cada linha do conjunto de resultados (tabela) está vinculada a um nó, conforme retornado pela consulta. As informações específicas de [colunas individuais](#column-base-component) são então extraídas deste conjunto de dados.

* Geralmente consiste em:

   * Um caminho raiz.

     Especifica a subárvore do repositório a ser pesquisado.

     Para ajudar a minimizar o impacto no desempenho, é aconselhável (tentar) restringir a consulta a uma subárvore específica do repositório. O caminho raiz pode ser predefinido no [modelo de relatório](#report-template) ou definido pelo usuário na [caixa de diálogo Configuração (Editar)](#configuration-dialog).

   * [Um ou mais critérios](#query-definition).

     Elas são impostas para produzir o conjunto de resultados (inicial); incluem, por exemplo, restrições no tipo de nó ou restrições de propriedade.

**O ponto principal aqui é que cada único nó retornado no conjunto de resultados da consulta é usado para gerar uma única linha no relatório (portanto, uma relação 1:1).**

O desenvolvedor deve garantir que a consulta definida para um relatório retorne um conjunto de nós apropriado para esse relatório. No entanto, o nó em si não precisa manter todas as informações necessárias, isso também pode ser derivado de nós principais e/ou secundários. Por exemplo, a consulta usada para o [Relatório de Usuário](/help/sites-administering/reporting.md#user-report) seleciona nós com base no tipo de nó (neste caso, `rep:user`). No entanto, a maioria das colunas neste relatório não obtém seus dados diretamente desses nós, mas dos nós filhos `profile`.

### Fila de processamento {#processing-queue}

A [consulta](#the-query-and-data-retrieval) retorna um conjunto de resultados de dados a serem exibidos como linhas no relatório. Cada linha do conjunto de resultados é processada (no lado do servidor), em [várias fases](#phases-of-the-processing-queue), antes de ser transferida para o cliente para exibição no relatório.

Isso permite:

* Extrair e derivar valores do conjunto de resultados subjacente.

  Por exemplo, permite processar dois valores de propriedade como um único valor, calculando a diferença entre os dois.

* Resolução de valores extraídos; isso pode ser feito de várias maneiras.

  Por exemplo, caminhos podem ser mapeados para um título (como no conteúdo mais legível da respectiva propriedade *jcr:title*).

* Aplicação de filtros em vários pontos.
* Criação de valores compostos, se necessário.

  Por exemplo, consistindo em um texto que é exibido ao usuário, um valor a ser usado para classificação e um URL adicional que é usado (no lado do cliente) para criar um link.

#### Fluxo de trabalho da fila de processamento {#workflow-of-the-processing-queue}

O fluxo de trabalho a seguir representa a fila de processamento:

![chlimage_1-249](assets/chlimage_1-249.png)

#### Fases da fila de processamento {#phases-of-the-processing-queue}

Onde as etapas e os elementos detalhados são:

1. Transforma os resultados retornados pela [consulta inicial (reportbase)](#query-definition) no conjunto de resultados básico usando extratores de valor.

   Extratores de valor são escolhidos automaticamente dependendo do [tipo de coluna](#column-specific-definitions). Eles são usados para ler valores da Consulta JCR subjacente e criar um conjunto de resultados a partir deles; depois disso, o processamento adicional pode ser aplicado. Por exemplo, para o tipo `diff`, o extrator de valor lê duas propriedades, calcula o valor único que é então adicionado ao conjunto de resultados. Não é possível configurar os extratores de valor.

1. Para esse conjunto de resultados inicial, contendo dados brutos, a [filtragem inicial](#column-specific-definitions) (*fase raw*) é aplicada.

1. Os valores são [pré-processados](#processing-queue); conforme definido para a fase *apply*.

1. A [Filtragem](#column-specific-definitions) (atribuída à fase *pré-processada*) é executada nos valores pré-processados.

1. Os valores são resolvidos; de acordo com o [resolvedor definido](#processing-queue).
1. A [Filtragem](#column-specific-definitions) (atribuída à fase *resolvida*) é executada nos valores resolvidos.

1. Os dados estão [agrupados e agregados](#column-specific-definitions).
1. Os dados da matriz são resolvidos convertendo-os em uma lista (baseada em sequência de caracteres).

   Esta é uma etapa implícita que converte um resultado de vários valores em uma lista que pode ser exibida; é necessária para valores de célula (não agregados) que se baseiam em propriedades JCR de vários valores.

1. Os valores são novamente [pré-processados](#processing-queue); conforme definido para a fase *afterApply*.

1. Os dados são classificados.
1. Os dados processados são transferidos para o cliente.

>[!NOTE]
>
>A consulta inicial que retorna o conjunto de resultados de dados base está definida no componente `reportbase`.
>
>Outros elementos da fila de processamento são definidos nos componentes `columnbase`.

## Construção e configuração do relatório {#report-construction-and-configuration}

Os itens a seguir são necessários para criar e configurar um relatório:

* um [local para a definição dos componentes do relatório](#location-of-report-components)
* um componente [`reportbase`](#report-base-component)
* um ou mais, [`columnbase` componentes](#column-base-component)
* um [componente de página](#page-component)
* um [design de relatório](#report-design)
* um [modelo de relatório](#report-template)

### Local dos componentes do relatório {#location-of-report-components}

Os componentes de relatórios padrão são mantidos em `/libs/cq/reporting/components`.

No entanto, é recomendável não atualizar esses nós, mas criar seus próprios nós de componente em `/apps/cq/reporting/components` ou, se mais apropriado, `/apps/<yourProject>/reports/components`.

Onde (como exemplo):

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

Sob isso, você cria a raiz para seu relatório e, sob esse, o componente base de relatório e os componentes base da coluna:

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### Componente de Página  {#page-component}

Uma página de relatório deve usar o `sling:resourceType` de `/libs/cq/reporting/components/reportpage`.

Um componente de página personalizado não deve ser necessário (geralmente).

## Componente base do relatório {#report-base-component}

Cada tipo de relatório requer um componente de contêiner derivado de `/libs/cq/reporting/components/reportbase`.

Este componente atua como um contêiner para o relatório como um todo e fornece informações para:

* A [definição de consulta](#query-definition).
* Uma [(opcional) caixa de diálogo](#configuration-dialog) para configurar o relatório.
* Quaisquer [Gráficos](#chart-definitions) integrados ao relatório.

```
N:<reportname> [cq:Component]
    P:sling:resourceSuperType = "cq/reporting/components/reportbase"
    N:charting
    N:dialog [cq:Dialog]
    N:queryBuilder
```

### Definição da consulta {#query-definition}

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

  Limita o conjunto de resultados a nós que têm propriedades específicas com valores específicos. Se várias restrições forem especificadas, o nó deverá atender a todas elas (operação AND).

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

  Retornaria todos os componentes `textimage` que foram modificados pela última vez pelo usuário `admin`.

* `nodeTypes`

  Usado para limitar o conjunto de resultados aos tipos de nó especificados. Vários tipos de nó podem ser especificados.

* `mandatoryProperties`

  Limita o conjunto de resultados a nós que têm *todos* as propriedades especificadas. O valor das propriedades não é considerado.

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

     Como várias configurações podem ser definidas, você pode usá-las para definir quais estão ativas no momento. Eles são definidos por uma matriz de nós (não há convenção de nomenclatura obrigatória para esses nós, mas os relatórios padrão geralmente usam `0`, `1`. `x`), cada um com a seguinte propriedade:

      * `id`

        Identificação dos gráficos ativos. Deve corresponder à identificação de um dos gráficos `definitions`.

* `definitions`

  Define os tipos de gráfico que estão potencialmente disponíveis para o relatório. O `definitions` a ser usado é especificado pelas configurações de `active`.

  As definições são especificadas usando uma matriz de nós (mais uma vez frequentemente nomeados como `0`, `1`. `x`), cada um com as seguintes propriedades:

   * `id`

     A identificação do gráfico.

   * `type`

     O tipo de gráfico disponível. Selecionar de:

      * `pie`
Gráfico de pizza. Gerado somente a partir dos dados atuais.

      * `lineseries`
Séries de linhas (pontos de conexão que representam os instantâneos reais). Gerado somente a partir de dados históricos.

   * Propriedades adicionais estão disponíveis, dependendo do tipo de gráfico:

      * para o tipo de gráfico `pie`:

         * `maxRadius` ( `Double/Long`)

           O raio máximo permitido para o gráfico de pizza; portanto, o tamanho máximo permitido para o gráfico (sem legenda). Ignorado se `fixedRadius` estiver definido.

         * `minRadius` ( `Double/Long`)

           O raio mínimo permitido para o gráfico de pizza. Ignorado se `fixedRadius` estiver definido.

         * `fixedRadius` ( `Double/Long`)
Define um raio fixo para o gráfico de pizza.

      * para o tipo de gráfico [`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals` ( `Boolean`)

           Verdadeiro se uma linha adicional mostrando o **Total** deve ser mostrada.
padrão: `false`

         * `series` ( `Long`)

           Número de linhas/séries a serem exibidas.
padrão: `9` (este também é o máximo permitido)

         * `hoverLimit` ( `Long`)

           Número máximo de instantâneos agregados (pontos mostrados em cada linha horizontal, representando valores distintos) para os quais os pop-ups serão exibidos. Ou seja, quando o usuário passa o mouse sobre um valor distinto ou rótulo correspondente na legenda do gráfico.

           padrão: `35` (isto é, nenhum pop-up será exibido se mais de 35 valores distintos forem aplicáveis às configurações atuais do gráfico).

           Há um limite adicional de dez pop-ups que podem ser exibidos em paralelo (vários pop-ups podem ser exibidos quando o mouse sobre os textos da legenda é feito).

### Caixa de diálogo Configuração {#configuration-dialog}

Cada relatório pode ter uma caixa de diálogo de configuração, permitindo que o usuário especifique vários parâmetros para o relatório. Esta caixa de diálogo pode ser acessada por meio do botão **Editar** quando a página do relatório estiver aberta.

Esta caixa de diálogo é uma [caixa de diálogo](/help/sites-developing/components-basics.md#dialogs) padrão do CQ e pode ser configurada como tal (consulte [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Dialog) para obter mais informações).

Uma caixa de diálogo de exemplo pode ter esta aparência:

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

Vários componentes pré-configurados são fornecidos; eles podem ser referenciados na caixa de diálogo, usando a propriedade `xtype` com um valor de `cqinclude`:

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

  Seletor para agendamento de instantâneos para o gráfico histórico.

>[!NOTE]
>
>Os componentes referenciados devem ser incluídos usando o sufixo `.infinity.json` (veja o exemplo acima).

### Caminho raiz {#root-path}

Além disso, um caminho raiz pode ser definido para o relatório:

* **`rootPath`**

  Isso limita o relatório a uma determinada seção (árvore ou subárvore) do repositório, recomendada para otimização de desempenho. O caminho raiz é especificado pela propriedade `rootPath` do nó `report` de cada página do relatório (retirada do modelo após a criação da página).

  Ele pode ser especificado por:

   * o [modelo de relatório](#report-template) (como valor fixo ou como valor padrão para a caixa de diálogo de configuração).
   * o usuário (usando este parâmetro)

## Componente de base da coluna {#column-base-component}

Cada tipo de coluna requer um componente derivado de `/libs/cq/reporting/components/columnbase`.

Um componente de coluna define uma combinação do seguinte:

* A configuração da [Consulta Específica de Coluna](#column-specific-query).
* Os [Resolvedores e Pré-Processamento](#resolvers-and-preprocessing).
* As [Definições Específicas de Coluna](#column-specific-definitions) (como filtros e agregações; nó filho `definitions`).
* [Valores Padrão de Coluna](#column-default-values).
* O [Filtro de Cliente](#client-filter) para extrair as informações para exibição dos dados retornados pelo servidor.
* Além disso, um componente de coluna deve fornecer uma instância adequada de `cq:editConfig`. para definir os [Eventos e Ações](#events-and-actions) necessários.
* A configuração de [colunas genéricas](#generic-columns).

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

Consulte também [Definindo seu Novo Relatório](#defining-your-new-report).

### Consulta Específica de Coluna {#column-specific-query}

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

  Se uma propriedade estiver definida como Cadeia de Caracteres [], várias propriedades serão verificadas (em sequência) para localizar o valor real.

  Por exemplo, se houver:

  `property = [ "jcr:lastModified", "jcr:created" ]`

  O extrator de valor correspondente (que está no controle aqui):

   * Verifica se há uma propriedade jcr:lastModified disponível e, em caso afirmativo, a usa.
   * Se nenhuma propriedade jcr:lastModified estiver disponível, o conteúdo de jcr:created será usado em seu lugar.

* `subPath`

  Se o resultado não estiver no nó retornado pela consulta, `subPath` definirá onde a propriedade está localizada.

* `secondaryProperty`

  Uma segunda propriedade que deve ser usada para calcular o valor real da célula. Essa definição só é usada para determinados tipos de coluna (diferente e classificável).

  Por exemplo, se houver o Relatório de instâncias de fluxo de trabalho, a propriedade especificada será usada para armazenar o valor real da diferença de tempo (em milissegundos) entre as horas de início e término.

* `secondarySubPath`

  Semelhante a subPath, quando `secondaryProperty` é usado.

Normalmente, somente `property` é usado.

### Filtro do cliente {#client-filter}

O filtro do cliente extrai as informações a serem exibidas dos dados retornados pelo servidor.

>[!NOTE]
>
>Esse filtro é executado no lado do cliente, depois que todo o processamento do lado do servidor foi aplicado.

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

O `clientFilter` é uma função JavaScript que:

* como entrada, recebe um parâmetro; os dados retornados do servidor (pré-processados)
* como saída, retorna o valor filtrado (processado); os dados extraídos ou derivados das informações de entrada

O exemplo a seguir extrai o caminho da página correspondente de um caminho de componente:

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

     Resolve um valor de caminho para o caminho da página apropriada; mais precisamente, para o nó `jcr:content` correspondente. Por exemplo, `/content/.../page/jcr:content/par/xyz` é resolvido como `/content/.../page/jcr:content`.

   * `path`

     Resolve um valor de caminho anexando opcionalmente um subcaminho e obtendo o valor real de uma propriedade do nó (conforme definido por `resolverConfig`) no caminho resolvido. Por exemplo, um `path` de `/content/.../page/jcr:content` pode ser resolvido para o conteúdo da propriedade `jcr:title`. Isso significa que um caminho de página é resolvido para o título da página.

   * `pathextension`

     Resolve um valor ao preceder um caminho e obter o valor real de uma propriedade do nó no caminho resolvido. Por exemplo, um valor `de` pode ser precedido por um caminho como `/libs/wcm/core/resources/languages`, pegando o valor da propriedade `language`, para resolver o código do país `de` para a descrição do idioma `German`.

* `resolverConfig`

  Fornece definições para o resolvedor. As opções disponíveis dependem do `resolver` selecionado:

   * `const`

     Use propriedades para especificar as constantes para resolução. O nome da propriedade define a constante a ser resolvida; o valor da propriedade define o valor resolvido.

     Por exemplo, uma propriedade com **Nome**= `1` e **Valor** `=One` resolve 1 para Um.

   * `default`

     Nenhuma configuração disponível.

   * `page`

      * `propertyName` (opcional)

        Define o nome da propriedade que deve ser usada para resolver o valor. Se não especificado, o valor padrão de *jcr:title* (o título da página) é usado; para o resolvedor `page`, isso significa que primeiro o caminho é resolvido para o caminho da página e, em seguida, resolvido para o título da página.

   * `path`

      * `propertyName` (opcional)

        Especifica o nome da propriedade que deve ser usada para resolver o valor. Se não for especificado, o valor padrão de `jcr:title` será usado.

      * `subPath` (opcional)

        Essa propriedade pode ser usada para especificar um sufixo a ser anexado ao caminho antes que o valor seja resolvido.

   * `pathextension`

      * `path` (obrigatório)

        Define o caminho que será anexado.

      * `propertyName` (obrigatório)

        Define a propriedade no caminho resolvido em que o valor real está localizado.

      * `i18n` (opcional; tipo Booleano)

        Determina se o valor resolvido deve ser *internacionalizado* (ou seja, usando os [serviços de internacionalização do CQ5](/help/sites-administering/tc-manage.md)).

* `preprocessing`

  O pré-processamento é opcional e pode ser associado (separadamente) às fases de processamento *apply* ou *applyAfter*:

   * `apply`

     A fase inicial de pré-processamento ([etapa 3 na representação da fila de processamento](#processing-queue)).

   * `applyAfter`

     Aplicar após o pré-processamento ([etapa 9 na representação da fila de processamento](#processing-queue)).

#### Resolvedores {#resolvers}

Os resolvedores são usados para extrair as informações necessárias. Exemplos dos vários resolvedores são:

**Const**

O valor a seguir resolve um valor constante de `VersionCreated` para a cadeia de caracteres `New version created`.

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

O item a seguir resolve um caminho de `/content/.../page` para o conteúdo da propriedade `jcr:title`. Isso significa que um caminho de página é resolvido para o título da página.

Consulte `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**Extensão do Caminho**

O código a seguir anexa um valor `de` com a extensão de caminho `/libs/wcm/core/resources/languages`, em seguida, usa o valor da propriedade `language` para resolver o código do país `de` para a descrição de idioma `German`.

Consulte `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### Pré-processando {#preprocessing}

A definição `preprocessing` pode ser aplicada a:

* valor original:

  A definição de pré-processamento do valor original está especificada diretamente em `apply` e/ou `applyAfter`.

* no seu estado agregado:

  Se necessário, pode ser fornecida uma definição separada para cada agregação.

  Para especificar o pré-processamento explícito para valores agregados, as definições de pré-processamento devem residir em um respectivo nó filho `aggregated` ( `apply/aggregated`, `applyAfter/aggregated`). Se o pré-processamento explícito para agregações distintas for necessário, a definição de pré-processamento estará em um nó filho com o nome da respectiva agregação (por exemplo, `apply/aggregated/min/max` ou outras agregações).

Você pode especificar qualquer um dos seguintes itens a serem usados durante o pré-processamento:

* [localizar e substituir padrões](#preprocessing-find-and-replace-patterns)
Quando encontrado, o padrão especificado (que é definido como uma expressão regular) é substituído por outro padrão; por exemplo, isso pode ser usado para extrair uma substring do original.

* [formatadores de tipo de dados](#preprocessing-data-type-formatters)

  Converte um valor numérico em uma cadeia de caracteres relativa; por exemplo, o valor &quot;representando uma diferença de tempo de uma hora seria resolvido como uma cadeia de caracteres como `1:24PM (1 hour ago)`.

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

#### Pré-processamento - Localizar e substituir padrões {#preprocessing-find-and-replace-patterns}

Para pré-processamento, você pode especificar um `pattern` (definido como uma [expressão regular](https://en.wikipedia.org/wiki/Regular_expression) ou regex) que esteja localizado e substituído pelo padrão `replace`:

* `pattern`

  A expressão regular usada para localizar uma subsequência de caracteres.

* `replace`

  A sequência, ou representação da sequência, que é usada como substituição da sequência original. Geralmente representa uma subcadeia de caracteres da cadeia localizada pela expressão regular `pattern`.

Um exemplo de substituição pode ser detalhado como:

* Para o nó `definitions/data/preprocessing/apply` com estas duas propriedades:

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`: `$1`

* Uma string que chega como:

   * `/content/geometrixx/en/services/jcr:content/par/text`

* Dividido em quatro seções:

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` - `(/jcr:content)` - `/jcr:content`
   * `$3` - `(/|$)` - `/`
   * `$4` - `(.*)` - `par/text`

* E substituída pela cadeia de caracteres representada por `$1`:

   * `/content/geometrixx/en/services`

#### Pré-processamento - Formatos de tipo de dados {#preprocessing-data-type-formatters}

Esses formatadores convertem um valor numérico em uma sequência de caracteres relativa.

Por exemplo, isso pode ser usado para uma coluna de tempo que permite agregações de `min`, `avg` e `max`. Como as agregações `min`/ `avg`/ `max` são exibidas como *diferença de tempo* (por exemplo, `10 days ago`), elas exigem um formatador de dados. Para isso, um formatador `datedelta` é aplicado aos valores agregados `min`/ `avg`/ `max`. Se uma agregação `count` também estiver disponível, ela não precisará de um formatador, nem o valor original.

Atualmente, os formatadores de tipo de dados disponíveis são:

* `format`

  Formatador de tipo de dados:

   * `duration`

     Duração é o intervalo de tempo entre duas datas definidas. Por exemplo, o início e o fim de uma ação de fluxo de trabalho que levou uma hora, começando em 13/02/11 às 11:23h e terminando uma hora depois às 12:23h de 13/02/11.

     Ele converte um valor numérico (interpretado como milissegundos) em uma cadeia de caracteres de duração; por exemplo, `30000` é formatado como * `30s`.*

   * `datedelta`

     Datadelta é o intervalo de tempo entre uma data no passado e &quot;agora&quot; (portanto, tem um resultado diferente se o relatório for visualizado em um momento posterior).

     Ele converte o valor numérico (interpretado como uma diferença de tempo em dias) em uma string de data relativa. Por exemplo, 1 é formatado como um dia atrás.

O exemplo a seguir define a formatação `datedelta` para agregações `min` e `max`:

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

### Definições específicas de coluna {#column-specific-definitions}

As definições específicas de coluna definem os filtros e agregações disponíveis para essa coluna.

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

  Os itens a seguir estão disponíveis como opções padrão:

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

     Usado para extrair partes de uma data necessária para agregação (por exemplo, agrupar por ano para obter dados agregados para cada ano).

   * `sortable`

     Usado para valores que usam valores diferentes (conforme obtidos de propriedades diferentes) para classificação e exibição.

  Além disso, qualquer uma das opções acima pode ser definida como vários valores; por exemplo, `string[]` define uma matriz de cadeias de caracteres.

  O extrator de valor é escolhido pelo tipo de coluna. Se um extrator de valor estiver disponível para um tipo de coluna, esse extrator será usado. Caso contrário, o extrator de valor padrão será usado.

  Um tipo pode (opcionalmente) receber um parâmetro. Por exemplo, `timeslot:year` extrai o ano de um campo de data. Tipos com seus parâmetros:

   * `timeslot` - Os valores são comparáveis às constantes correspondentes de `java.utils.Calendar`.

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` - `Calendar.MONTH`
      * `timeslot:week-of-year` - `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` - `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` - `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` - `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` - `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` - `Calendar.MINUTE`

* `groupable`

  Define se o relatório pode ser agrupado por esta coluna.

* `filters`

  Definições de filtro.

   * `filterType`

     Filtros disponíveis:

      * `string`

        Um filtro baseado em sequência de caracteres.

   * `id`

     Identificador do filtro.

   * `phase`

     Fases disponíveis:

      * `raw`

        O filtro é aplicado em dados brutos.

      * `preprocessed`

        O filtro é aplicado aos dados pré-processados.

      * `resolved`

        O filtro é aplicado aos dados resolvidos.

* `aggregates`

  Definições de agregação.

   * `text`

     Nome textual da agregação. Se `text` não for especificado, será usada a descrição padrão da agregação. Por exemplo, `minimum` é usado para a agregação `min`.

   * `type`

     Tipo de agregação. As agregações disponíveis são:

      * `count`

        Conta o número de linhas.

      * `count-nonempty`

        Conta o número de linhas não vazias.

      * `min`

        Ele fornece o valor mínimo.

      * `max`

        Ele fornece o valor máximo.

      * `average`

        Ele fornece o valor médio.

      * `sum`

        Ela fornece a soma de todos os valores.

      * `median`

        Ele fornece o valor mediano.

      * `percentile95`

        Usa o 95º percentil de todos os valores.

### Valores Padrão da Coluna {#column-default-values}

Define os valores padrão para a coluna:

```xml
N:defaults
    P:aggregate
```

* `aggregate`

  Os valores válidos de `aggregate` são iguais aos de `type` em `aggregates` (consulte [Definições Específicas de Coluna (definições - filtros / agregações)](#column-specific-definitions) ).

### Eventos e ações {#events-and-actions}

Editar configuração define os eventos necessários para os ouvintes detectarem e as ações a serem aplicadas após a ocorrência desses eventos. Consulte a [introdução ao desenvolvimento de componentes](/help/sites-developing/components.md) para obter informações sobre o plano de fundo.

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

### Colunas genéricas {#generic-columns}

Colunas genéricas são uma extensão em que (a maioria das) definições de coluna são armazenadas na instância do nó da coluna (em vez do nó do componente ).

Eles usam uma caixa de diálogo (padrão) que pode ser personalizada para o componente genérico individual. Esta caixa de diálogo permite que o usuário do relatório defina as propriedades de coluna de uma coluna genérica na página do relatório (usando a opção de menu **Propriedades da coluna...**).

Um exemplo é a coluna **Genérica** do **Relatório de Usuário**. Consulte `/libs/cq/reporting/components/userreport/genericcol`.

Para tornar uma coluna genérica:

* Defina a propriedade `type` do nó `definition` da coluna como `generic`.

  Ver `/libs/cq/reporting/components/userreport/genericcol/definitions`

* Especifique uma definição de caixa de diálogo (padrão) no nó `definition` da coluna.

  Ver `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * Os campos da caixa de diálogo devem se referir aos mesmos nomes que a propriedade do componente correspondente, incluindo seu caminho.

     Por exemplo, se você quiser que o tipo de coluna genérica seja configurável por meio da caixa de diálogo, use um campo com o nome de `./definitions/type`.

   * As propriedades definidas usando a interface do usuário/caixa de diálogo têm precedência sobre as definidas no componente `columnbase`.

* Defina a Editar configuração.

  Ver `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* Use metodologias padrão de AEM para definir propriedades de coluna (adicionais).

  Para propriedades definidas nas instâncias de componente e coluna, o valor na instância de coluna tem prioridade.

  As propriedades disponíveis para uma coluna genérica são:

   * `jcr:title` - nome da coluna
   * `definitions/aggregates` - agregações
   * `definitions/filters` - filtros
   * `definitions/type`- o tipo da coluna (deve ser definido na caixa de diálogo, usando um seletor/caixa de combinação ou um campo oculto)
   * `definitions/data/resolver` e `definitions/data/resolverConfig` (mas não `definitions/data/preprocessing` ou `.../clientFilter`) - o resolvedor e a configuração
   * `definitions/queryBuilder` - a configuração do construtor de consultas
   * `defaults/aggregate` - a agregação padrão

  Se houver uma nova instância da coluna genérica no **Relatório de Usuário**, as propriedades definidas com a caixa de diálogo serão mantidas em:

  `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## Design do relatório {#report-design}

O design define quais tipos de coluna estão disponíveis para criar um relatório. Também define o sistema de parágrafo ao qual as colunas são adicionadas.

A Adobe recomenda criar um design individual para cada relatório. Isso garante total flexibilidade. Consulte [Definindo Seu Novo Relatório](#defining-your-new-report).

Os componentes de relatórios padrão são mantidos em `/etc/designs/reports`.

O local dos relatórios pode depender de onde seus componentes estão localizados:

* `/etc/designs/reports/<yourReport>` é adequado se o relatório estiver em `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` para relatórios usando o padrão `/apps/<yourProject>/reports`

As propriedades de design necessárias estão registradas em `jcr:content/reportpage/report/columns` (por exemplo, `/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`):

* `components`

  Quaisquer componentes e/ou grupos de componentes permitidos no relatório.

* `sling:resourceType`

  Propriedade com valor `cq/reporting/components/repparsys`.

Um exemplo de trecho de design (retirado do design do relatório de componentes) é:

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
>A Adobe recomenda que você não altere os designs de relatórios padrão. Isso garante que você não perca nenhuma alteração ao atualizar ou instalar hotfixes.
>
>Copie o relatório e seu design se quiser personalizar um relatório padrão.

>[!NOTE]
>
>As colunas padrão podem ser criadas automaticamente quando um relatório é criado. Eles são especificados no template.

## Modelo de relatório {#report-template}

Cada tipo de relatório deve fornecer um modelo. Estes são os [Modelos CQ](/help/sites-developing/templates.md) padrão e podem ser configurados como tal.

O template deve:

* definir o `sling:resourceType` como `cq/reporting/components/reportpage`

* indicar o modelo a utilizar
* criar um nó filho `report` que faça referência ao componente do contêiner ( `reportbase`) com a propriedade `sling:resourceType`

Um exemplo de trecho de modelo (retirado do modelo de relatório do componente) é:

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

Um exemplo de trecho de modelo, mostrando a definição do caminho raiz (retirado do modelo de relatório do usuário), é:

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

Os modelos de relatórios padrão são mantidos em `/libs/cq/reporting/templates`.

No entanto, o Adobe recomenda que você não atualize esses nós. Em vez disso, crie seus próprios nós de componente em `/apps/cq/reporting/templates` ou, se mais apropriado, `/apps/<yourProject>/reports/templates`.

Onde, como exemplo (consulte também [Local dos Componentes de Relatório](#location-of-report-components)):

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

Em, crie a raiz para seu modelo:

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## Criar Seu Próprio Relatório - Um Exemplo {#creating-your-own-report-an-example}

### Definição do novo relatório {#defining-your-new-report}

Para definir um relatório, crie e configure:

1. A raiz dos componentes do relatório.
1. O componente da base de relatório.
1. Um ou mais componentes de base da coluna.
1. O design do relatório.
1. A raiz do seu modelo de relatório.
1. O template do relatório.

Para ilustrar essas etapas, o exemplo a seguir define um relatório que lista todas as configurações de OSGi no repositório. Ou seja, todas as instâncias do nó `sling:OsgiConfig`.

>[!NOTE]
>
>Copiar um relatório existente e, em seguida, personalizar a nova versão é um método alternativo.

1. Crie o nó raiz para o novo relatório.

   Por exemplo, em `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. Defina sua base de relatórios. Por exemplo, `osgireport[cq:Component]` em `/apps/cq/reporting/components/osgireport`.

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

   Isso define um componente da base de relatórios que:

   * procura todos os nós do tipo `sling:OsgiConfig`
   * exibe os gráficos `pie` e `lineseries`
   * fornece uma caixa de diálogo para o usuário configurar o relatório

1. Defina seu primeiro componente de coluna (columnbase). Por exemplo, `bundlecol[cq:Component]` em `/apps/cq/reporting/components/osgireport`.

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

   Isso define um componente columnbase que:

   * procura e retorna o valor que recebe do servidor; nesse caso, a propriedade `jcr:path` para cada nó `sling:OsgiConfig`
   * fornece a agregação `count`
   * não é agrupável
   * tem o título `Bundle` (título de coluna dentro da tabela)
   * está no grupo sidekick `OSGi Report`
   * atualiza em eventos especificados

   >[!NOTE]
   >
   >Neste exemplo, não há definições de `N:data` e `P:clientFilter`. Isso ocorre porque o valor recebido do servidor é retornado com base em 1:1, que é o comportamento padrão.
   >
   >É igual às definições:
   >
   >```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >Onde a função simplesmente retorna o valor recebido.

1. Defina o design do relatório. Por exemplo, `osgireport[cq:Page]` em `/etc/designs/reports`.

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

1. Crie o nó raiz para o novo modelo de relatório.

   Por exemplo, em `/apps/cq/reporting/templates/osgireport`.

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. Defina seu modelo de relatório. Por exemplo, `osgireport[cq:Template]` em `/apps/cq/reporting/templates`.

   ```xml
   N:osgireport [cq:Template]
       P:allowedPaths [String[]] = "/etc/reports(/.*)?"
       P:jcr:description [String] = "Use this report generator to create an OSGi report."
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
   * O fornece uma imagem em miniatura para uso na lista de modelos (a definição completa desse nó não está listada acima; é mais fácil copiar uma instância de thumbnail.png de um relatório existente).

### Criação de uma instância do novo relatório {#creating-an-instance-of-your-new-report}

Uma instância do novo relatório agora pode ser criada:

1. Abra o console **Ferramentas**.

1. Selecione **Relatórios** no painel esquerdo.
1. Em seguida, **Novo...** da barra de ferramentas. Defina um **Título** e um **Nome**, selecione seu novo tipo de relatório (o **Modelo de Relatório OSGi**) na lista de modelos e clique em **Criar**.
1. A nova instância do relatório aparece na lista. Clique duas vezes para abrir.
1. Arraste um componente (para este exemplo, **Pacote** no grupo **Relatório OSGi**) do sidekick para criar a primeira coluna e [iniciar a definição de relatório](/help/sites-administering/reporting.md#the-basics-of-report-customization).

   >[!NOTE]
   >
   >Como este exemplo não tem nenhuma coluna agrupável, os gráficos não estão disponíveis. Para ver gráficos, defina `groupable` como `true`:
   >
   >```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```
   >

## Configuração dos serviços da estrutura de relatório {#configuring-the-report-framework-services}

Esta seção descreve opções avançadas de configuração para os serviços OSGi que implementam a estrutura de relatório.

Elas podem ser visualizadas usando o menu Configuração do console da Web (disponível em `http://localhost:4502/system/console/configMgr`, por exemplo). Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

### Serviço básico (Configuração de relatório do Day CQ) {#basic-service-day-cq-reporting-configuration}

* **Timezone** define os dados do histórico do fuso horário que são criados para. Isso garante que o gráfico histórico exiba os mesmos dados para cada usuário em todo o mundo.
* **Locale** define a localidade a ser usada com **Timezone** para dados de histórico. O local é usado para determinar algumas configurações de calendário específicas do local (por exemplo, se o primeiro dia de uma semana é domingo ou segunda-feira).

* **Caminho de instantâneo** define o caminho raiz onde os instantâneos de gráficos históricos são armazenados.
* **Caminho para relatórios** define o caminho onde os relatórios estão localizados. Isso é usado pelo serviço de instantâneo para determinar os relatórios para os quais são feitos instantâneos.
* **Instantâneos diários** define a hora de cada dia em que os instantâneos diários são tirados. A hora especificada está no fuso horário local do servidor.
* **Instantâneos por hora** define o minuto de cada hora em que instantâneos por hora são tirados.
* **Linhas (máx.)** define o número máximo de linhas armazenadas para cada instantâneo. Esse valor deve ser escolhido de forma razoável. Se for muito alto, isso afetará o tamanho do repositório. Se for muito baixo, os dados podem não ser precisos por causa da maneira como os dados do histórico são tratados.
* **Dados falsos**, se estiverem habilitados, dados de histórico falsos poderão ser criados com o seletor `fakedata`; se estiverem desabilitados, o uso do seletor `fakedata` acionará uma exceção.

  Como os dados são falsos, eles devem *somente* ser usados para fins de teste e depuração.

  O uso do seletor `fakedata` finaliza o relatório implicitamente, portanto, todos os dados existentes são perdidos. Os dados podem ser restaurados manualmente, mas isso pode ser um processo demorado.

* O **usuário do instantâneo** define um usuário opcional que pode ser usado para tirar instantâneos.

  Basicamente, instantâneos são tirados para o usuário que concluiu o relatório. Pode haver situações (por exemplo, em um sistema de publicação, em que esse usuário não exista, pois sua conta não foi replicada) em que você deseje especificar um usuário de fallback que será usado.

  Além disso, especificar um usuário pode impor um risco de segurança.

* **Impor usuário de instantâneo**, se habilitado, todos os instantâneos serão tirados com o usuário especificado em *Usuário de instantâneo*. Isso pode ter um sério impacto na segurança se não for tratado corretamente.

### Configurações de cache (Cache de relatórios do Day CQ) {#cache-settings-day-cq-reporting-cache}

* **Habilitar** permite habilitar ou desabilitar o cache de dados de relatório. A ativação do cache de relatórios mantém os dados do relatório na memória durante várias solicitações. Isso pode aumentar o desempenho, mas leva a um maior consumo de memória e pode, em circunstâncias extremas, levar a situações de falta de memória.
* **TTL** define o tempo (em segundos) durante o qual os dados de relatório são armazenados em cache. Um número mais alto aumenta o desempenho, mas também pode retornar dados imprecisos se os dados forem alterados dentro do período.
* **Máximo de entradas** define o número máximo de relatórios a serem armazenados em cache a qualquer momento.

>[!NOTE]
>
>Os dados do relatório podem ser diferentes para cada usuário e idioma. Portanto, os dados de relatório são armazenados em cache por relatório, usuário e idioma. Isso significa que um valor de **Máx. de entradas** de `2` realmente armazena dados em cache para:
>
>* um relatório para dois usuários com configurações de idioma diferentes
>* um usuário e dois relatórios
>
