---
title: Blueprint do SPA
seo-title: SPA Blueprint
description: Este documento descreve o contrato geral, independente de estrutura, que qualquer estrutura de SPA deve cumprir para implementar componentes SPA editáveis no AEM.
seo-description: This document describes the general, framework-independent contract that any SPA framework should fulfill in order to implement editable SPA components within AEM.
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
exl-id: 383f84fd-455c-49a4-9e2b-1c4757cc188b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 1%

---

# Blueprint do SPA{#spa-blueprint}

Para permitir que o autor use o Editor de SPA de AEM para editar o conteúdo de um SPA, há requisitos que o SPA deve atender, que estão descritos neste documento.

>[!NOTE]
>
>O Editor de SPA é a solução recomendada para projetos que exigem renderização do lado do cliente baseada em SPA estrutura (por exemplo, Reagir ou Angular).

## Introdução {#introduction}

Este documento descreve o contrato geral que qualquer estrutura de SPA deve cumprir (ou seja, o tipo de camada de suporte AEM) para implementar componentes SPA editáveis dentro do AEM.

>[!NOTE]
>
>Os seguintes requisitos são independentes de estrutura. Se esses requisitos forem cumpridos, poderá ser fornecida uma camada específica de estrutura composta por módulos, componentes e serviços.
>
>**Esses requisitos já são atendidos para os quadros React e Angular em AEM.** Os requisitos neste blueprint só são relevantes se você quiser implementar outra estrutura para uso com o AEM.

>[!CAUTION]
>
>Embora os recursos de SPA do AEM sejam independentes de estrutura, atualmente, apenas os quadros React e Angular são compatíveis.

Para permitir que o autor use o Editor de páginas AEM para editar os dados expostos por uma estrutura de Aplicativo de página única, um projeto deve ser capaz de interpretar a estrutura do modelo que representa a semântica dos dados armazenados para um aplicativo dentro do repositório AEM. Para atingir esse objetivo, duas bibliotecas agnósticas de estrutura são fornecidas: o `PageModelManager` e `ComponentMapping`.

### PageModelManager {#pagemodelmanager}

O `PageModelManager` A biblioteca é fornecida como um pacote NPM a ser usado por um projeto SPA. Ela acompanha o SPA e serve como um gerenciador de modelo de dados.

Em nome do SPA, ele abstrai a recuperação e o gerenciamento da estrutura JSON que representa a estrutura de conteúdo real. Também é responsável pela sincronização com o SPA para informá-lo quando deve renderizar novamente seus componentes.

Consulte o pacote NPM [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

Ao inicializar o `PageModelManager`, a biblioteca primeiro carrega o modelo raiz fornecido do aplicativo (por meio do parâmetro , da meta propriedade ou do URL atual). Se a biblioteca identificar que o modelo da página atual não faz parte do modelo raiz, ele é buscado e inclui-o como o modelo de uma página secundária.

![page_model_Consolidation](assets/page_model_consolidation.png)

### ComponentMapping {#componentmapping}

O `ComponentMapping` é fornecido como um pacote NPM para o projeto front-end. Ele armazena componentes de front-end e fornece uma maneira de o SPA mapear componentes de front-end para AEM tipos de recursos. Isso permite uma resolução dinâmica de componentes ao analisar o modelo JSON do aplicativo.

Cada item presente no modelo contém um `:type` que expõe um tipo de recurso AEM. Quando montado, o componente de front-end pode se renderizar usando o fragmento de modelo recebido das bibliotecas subjacentes.

#### Modelo dinâmico para mapeamento de componentes {#dynamic-model-to-component-mapping}

Para obter detalhes sobre como o modelo dinâmico para mapeamento de componentes ocorre no Javascript SPA SDK para AEM, consulte o artigo [Modelo dinâmico para mapeamento de componentes para SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

### Camada específica da estrutura {#framework-specific-layer}

Uma terceira camada deve ser implementada para cada estrutura de front-end. Essa terceira biblioteca é responsável por interagir com as bibliotecas subjacentes e fornecer uma série de pontos de entrada bem integrados e fáceis de usar para interagir com o modelo de dados.

O restante deste documento descreve os requisitos dessa camada específica da estrutura intermediária e aspira a ser independente da estrutura. Respeitando os requisitos a seguir, pode ser fornecida uma camada específica para a estrutura para que os componentes do projeto interajam com as bibliotecas subjacentes responsáveis pelo gerenciamento do modelo de dados.

## Conceitos gerais {#general-concepts}

### Modelo de página {#page-model}

A estrutura de conteúdo da página é armazenada em AEM. O modelo da página é usado para mapear e instanciar componentes SPA. Os desenvolvedores de SPA criam componentes SPA que mapeiam para AEM componentes. Para fazer isso, eles usam o tipo de recurso (ou o caminho para o componente de AEM) como uma chave exclusiva.

Os componentes do SPA devem estar sincronizados com o modelo da página e ser atualizados com qualquer alteração no conteúdo de acordo. Um padrão que aproveite componentes dinâmicos deve ser usado para instanciar os componentes dinamicamente de acordo com a estrutura do modelo de página fornecida.

### Campos Meta {#meta-fields}

O modelo de página aproveita o Exportador de Modelo JSON, que se baseia no [Modelo Sling](https://sling.apache.org/documentation/bundles/models.html) API. Os modelos de sling exportáveis expõem a seguinte lista de campos para permitir que as bibliotecas subjacentes interpretem o modelo de dados:

* `:type`: Tipo do recurso AEM (padrão = tipo de recurso)
* `:children`: Filhos hierárquicos do recurso atual. Os filhos não fazem parte do conteúdo interno do recurso atual (pode ser encontrado em itens que representam uma página)
* `:hierarchyType`: Tipo hierárquico de um recurso. O `PageModelManager` atualmente suporta o tipo de página

* `:items`: Recursos de conteúdo filho do recurso atual (estrutura aninhada, presente somente em contêineres)
* `:itemsOrder`: Lista ordenada dos filhos. O objeto de mapa JSON não garante a ordem de seus campos. Com o mapa e o array atual, o consumidor da API tem os benefícios de ambas as estruturas
* `:path`: Caminho do conteúdo de um item (presente nos itens que representam uma página)

Consulte também [Introdução aos AEM Content Services.](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### Módulo específico da estrutura {#framework-specific-module}

A separação de preocupações ajuda a facilitar a implementação do projeto. Por conseguinte, deve ser fornecido um pacote específico para as npm. Esse pacote é responsável pela agregação e exposição dos módulos, serviços e componentes básicos. Esses componentes devem encapsular a lógica de gerenciamento do modelo de dados e fornecer acesso aos dados que o componente do projeto espera. O módulo também é responsável por expor transitoriamente pontos de entrada úteis das bibliotecas subjacentes.

Para facilitar a interoperabilidade das bibliotecas, o Adobe aconselha o módulo específico da estrutura a agrupar as seguintes bibliotecas. Se necessário, a camada pode encapsular e adaptar as APIs subjacentes antes de expô-las ao projeto.

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### Implementações {#implementations}

#### Reagir {#react}

módulo npm: [@adobe/aem-response-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angular {#angular}

módulo npm: em breve

## Principais serviços e componentes {#main-services-and-components}

As seguintes entidades devem ser implementadas em conformidade com as orientações específicas de cada quadro. Com base na arquitetura da estrutura, a implementação pode variar amplamente, mas as funcionalidades descritas devem ser fornecidas.

### O Provedor de Modelo {#the-model-provider}

Os componentes do projeto devem delegar acesso aos fragmentos de um modelo em um Provedor de Modelo. O Provedor de Modelo é responsável por acompanhar as alterações feitas no fragmento especificado do modelo e retornar o modelo atualizado ao componente delegado.

Para fazer isso, o Provedor de Modelo deve se registrar no ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`. Em seguida, quando ocorrer uma alteração, ele receberá e transmitirá os dados atualizados ao componente de delegação. Por convenção, a propriedade disponibilizada ao componente delegado que carregará o fragmento do modelo é nomeada `cqModel`. A implementação é gratuita para fornecer essa propriedade ao componente, mas deve considerar aspectos como a integração com a arquitetura da estrutura, a descoberta e a facilidade de uso.

### O HTML do componente {#the-component-html-decorator}

O Component Decorator é responsável por decorar a HTML externa do elemento de cada instância de componente com uma série de atributos de dados e nomes de classe esperados pelo Editor de páginas.

#### Declaração de componente {#component-declaration}

Os metadados a seguir devem ser adicionados ao elemento HTML externo produzido pelo componente do projeto. Eles permitem que o Editor de páginas recupere a configuração de edição correspondente.

* `data-cq-data-path`: Caminho para o recurso relativo ao `jcr:content`

#### Editar declaração de capacidade e espaço reservado {#editing-capability-declaration-and-placeholder}

Os metadados e nomes de classe a seguir devem ser adicionados ao elemento HTML externo produzido pelo componente do projeto. Eles permitem que o Editor de páginas ofereça funcionalidades relacionadas.

* `cq-placeholder`: Nome da classe que identifica o espaço reservado de um componente vazio
* `data-emptytext`: Rótulo a ser exibido pela sobreposição quando uma instância de componente estiver vazia

**Espaço reservado para componentes vazios**

Cada componente deve ser estendido com uma funcionalidade que decorará o elemento HTML externo com atributos de dados e nomes de classe específicos para espaços reservados e sobreposições relacionadas quando o componente for identificado como vazio.

**Sobre o vazamento de um componente**

* O componente está logicamente vazio?
* Qual deve ser o rótulo exibido pela sobreposição quando o componente está vazio?

### Contêiner {#container}

Um contêiner é um componente destinado a conter e renderizar componentes filhos. Para fazer isso, o contêiner repete a `:itemsOrder`, `:items` e `:children` propriedades do modelo.

O contêiner obtém dinamicamente os componentes filhos do armazenamento do ` [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)` biblioteca. Em seguida, o contêiner estende o componente filho com os recursos do Provedor de modelo e, por fim, instanciá-lo.

### Página {#page}

O `Page` estende o `Container` componente. Um contêiner é um componente destinado a conter e renderizar componentes filhos, incluindo páginas filhas. Para fazer isso, o contêiner repete a `:itemsOrder`, `:items`e `:children` propriedades do modelo. O `Page` O componente obtém dinamicamente os componentes filhos do armazenamento do [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping) biblioteca. O `Page` é responsável pela instanciação de componentes filhos.

### Grade responsiva {#responsive-grid}

O componente Grade responsiva é um contêiner. Ela contém uma variante específica do Provedor de Modelo que representa suas colunas. A Grade Responsiva e suas colunas são responsáveis por decorar o elemento HTML externo do componente do projeto com os nomes de classe específicos contidos no modelo.

O componente Grade responsiva deve vir pré-mapeado para sua AEM contraparte, pois esse componente é complexo e raramente personalizado.

#### Campos de modelo específicos {#specific-model-fields}

* `gridClassNames:` Nomes de classe fornecidos para a grade responsiva
* `columnClassNames:` Nomes de classe fornecidos para a coluna responsiva

Veja também o recurso npm [@adobe/aem-response-editable-components#srccomponentsresponsivegridjsx](https://www.npmjs.com/package/@adobe/aem-react-editable-components#srccomponentsresponsivegridjsx)

#### Espaço reservado da grade responsiva {#placeholder-of-the-reponsive-grid}

O componente de SPA é mapeado para um contêiner gráfico, como a Grade Responsiva, e deve adicionar um espaço reservado para filho virtual quando o conteúdo estiver sendo criado. Quando o conteúdo do SPA é criado pelo Editor de páginas, ele é incorporado ao editor usando um iframe e o `data-cq-editor` é adicionado ao nó do documento desse conteúdo. Quando a variável `data-cq-editor` estiver presente, o contêiner deverá incluir um HTMLElement para representar a área com a qual o autor interage ao inserir um novo componente na página.

Por exemplo:

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>Os nomes de classe usados no exemplo são atualmente exigidos pelo editor de páginas.
>
>* `"new section"`: Indica que o elemento atual é o espaço reservado do contêiner
>* `"aem-Grid-newComponent"`: Normaliza o componente para a criação de layout
>


#### Mapeamento de componentes {#component-mapping}

O [`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping) biblioteca e sua `MapTo` pode ser encapsulada e estendida para fornecer as funcionalidades relativas à configuração de edição fornecida ao lado da classe de componente atual.

```
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

Na implementação acima, o componente do projeto é estendido com a funcionalidade vazia antes de ser realmente registrado na [Mapeamento de componentes](/help/sites-developing/spa-blueprint.md#componentmapping) armazenar. Isso é feito encapsulando e estendendo o [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) para introduzir o suporte da `EditConfig` objeto de configuração:

```
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data will be decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## Contrato com o Editor de páginas {#contract-with-the-page-editor}

Os componentes do projeto devem gerar no mínimo os seguintes atributos de dados para permitir que o editor interaja com eles.

* `data-cq-data-path`: O caminho relativo do componente, conforme fornecido pelo `PageModel` (por exemplo, `"root/responsivegrid/image"`). Esse atributo não deve ser adicionado às páginas.

Em resumo, para ser interpretado pelo editor de páginas como editável, um componente de projeto deve respeitar o seguinte contrato:

* Forneça os atributos esperados para associar uma instância do componente front-end a um recurso AEM.
* Forneça a série esperada de atributos e nomes de classe que permite a criação de espaços reservados vazios.
* Forneça os nomes de classe esperados, permitindo o arrastar e soltar dos ativos.

### Estrutura típica do elemento HTML {#typical-html-element-structure}

O fragmento a seguir ilustra a representação HTML típica de uma estrutura de conteúdo da página. Aqui estão alguns pontos importantes:

* O elemento de grade responsiva contém nomes de classe prefixados com `aem-Grid--`
* O elemento de coluna responsiva tem nomes de classe prefixados com `aem-GridColumn--`
* Uma grade responsiva que também é a coluna de uma grade pai é encapsulada, como os dois prefixos anteriores, não aparecem no mesmo elemento
* Os elementos correspondentes aos recursos editáveis carregam uma `data-cq-data-path` propriedade. Consulte a [Contrato com o editor de páginas](#contract-wtih-the-page-editor) seção deste documento.

```
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## Navegação e Roteamento {#navigation-and-routing}

O aplicativo é o proprietário do roteamento. O desenvolvedor de front-end precisa primeiro implementar um componente de Navegação (mapeado para um componente de navegação de AEM). Esse componente renderizaria links de URL a serem usados junto com uma série de rotas que exibirão ou ocultarão fragmentos de conteúdo.

O [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) biblioteca e sua ` [ModelRouter](/help/sites-developing/spa-routing.md)` módulo (habilitado por padrão) são responsáveis pela pré-busca e pelo fornecimento de acesso ao modelo associado a um determinado caminho de recurso.

As duas entidades estão relacionadas com a noção de encaminhamento, mas a ` [ModelRouter](/help/sites-developing/spa-routing.md)` é responsável apenas por ter a ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` carregado com um modelo de dados estruturado em sincronia com o estado atual do aplicativo.

Veja o artigo [Roteamento do Modelo de SPA](/help/sites-developing/spa-routing.md) para obter mais informações.

## SPA em ação {#spa-in-action}

Veja como um SPA simples funciona e experimente um SPA você mesmo continuando com o documento [Introdução ao SPA no AEM](/help/sites-developing/spa-getting-started-react.md).

## Leitura adicional {#further-reading}

Para obter mais informações sobre SPA no AEM, consulte os seguintes documentos:

* [Visão geral da criação de SPA](/help/sites-developing/spa-overview.md) para uma visão geral das SPA no AEM e no modelo de comunicação
* [Introdução ao SPA no AEM](/help/sites-developing/spa-getting-started-react.md) para obter um guia sobre um SPA simples e como ele funciona
