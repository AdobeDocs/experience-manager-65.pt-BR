---
title: Blueprint do SPA
seo-title: Blueprint do SPA
description: Este documento descreve o contrato geral e independente de estrutura que qualquer estrutura de SPA deve cumprir para implementar componentes de SPA editáveis dentro do AEM.
seo-description: Este documento descreve o contrato geral e independente de estrutura que qualquer estrutura de SPA deve cumprir para implementar componentes de SPA editáveis dentro do AEM.
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 0%

---


# Blueprint do SPA{#spa-blueprint}

Para permitir que o autor use o Editor SPA AEM para editar o conteúdo de um SPA, há requisitos que o SPA deve atender, descritos neste documento.

>[!NOTE]
>
>O Editor SPA é a solução recomendada para projetos que exigem renderização do lado do cliente baseada em estrutura SPA (por exemplo, Reagir ou Angular).

## Introdução {#introduction}

Este documento descreve o contrato geral que qualquer estrutura SPA deve cumprir (isto é, o tipo de camada de suporte AEM) para implementar componentes SPA editáveis dentro da AEM.

>[!NOTE]
>
>Os seguintes requisitos são independentes da estrutura. Se esses requisitos forem cumpridos, poderá ser fornecida uma camada específica da estrutura composta por módulos, componentes e serviços.
>
>**Estes requisitos já são cumpridos para os quadros React e Angular em AEM.** Os requisitos neste plano só são relevantes se você quiser implementar outra estrutura para uso com o AEM.

>[!CAUTION]
>
>Embora os recursos de SPA do AEM sejam independentes da estrutura, atualmente, apenas os frameworks React e Angular são suportados.

Para permitir que o autor use o Editor de páginas AEM para editar os dados expostos por uma estrutura de aplicativo de página única, um projeto deve ser capaz de interpretar a estrutura do modelo que representa a semântica dos dados armazenados para um aplicativo no repositório AEM. Para atingir esse objetivo, são fornecidas duas bibliotecas agnósticas de estrutura: o `PageModelManager` e o `ComponentMapping`.

### PageModelManager {#pagemodelmanager}

A `PageModelManager` biblioteca é fornecida como um pacote NPM a ser usado por um projeto SPA. Ele acompanha o SPA e atua como um gerenciador de modelo de dados.

Em nome da ZPE, abstrai a recuperação e a gestão da estrutura JSON que representa a estrutura real do conteúdo. Também é responsável por sincronizar com o SPA para informá-lo quando ele precisa renderizar novamente seus componentes.

Consulte o pacote NPM [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

Ao inicializar o aplicativo, `PageModelManager`a biblioteca primeiro carrega o modelo raiz fornecido do aplicativo (por meio de parâmetro, meta propriedade ou URL atual). Se a biblioteca identificar que o modelo da página atual não faz parte do modelo raiz, ele o busca e o inclui como o modelo de uma página secundária.

![page_model_Consolidation](assets/page_model_consolidation.png)

### ComponentMapping {#componentmapping}

O `ComponentMapping` módulo é fornecido como um pacote NPM para o projeto front-end. Ele armazena componentes de front-end e fornece uma maneira para o SPA mapear componentes de front-end para tipos de recursos AEM. Isso permite uma resolução dinâmica de componentes ao analisar o modelo JSON do aplicativo.

Cada item presente no modelo contém um `:type` campo que expõe um tipo de recurso AEM. Quando montado, o componente front-end pode se renderizar usando o fragmento do modelo recebido das bibliotecas subjacentes.

#### Modelo dinâmico para mapeamento de componentes {#dynamic-model-to-component-mapping}

Para obter detalhes sobre como o modelo dinâmico para mapeamento de componentes ocorre no SDK do Javascript SPA para AEM, consulte o artigo Modelo [dinâmico para mapeamento de componentes para SPAs](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

### Camada específica da estrutura {#framework-specific-layer}

Deve ser implementada uma terceira camada para cada estrutura de front-end. Esta terceira biblioteca é responsável por interagir com as bibliotecas subjacentes e fornece uma série de pontos de entrada bem integrados e fáceis de usar para interagir com o modelo de dados.

O restante deste documento descreve os requisitos desta camada específica do quadro intermediário e aspira a ser independente da estrutura. Respeitando os requisitos a seguir, pode ser fornecida uma camada específica para a estrutura, para que os componentes do projeto interajam com as bibliotecas subjacentes responsáveis pelo gerenciamento do modelo de dados.

## Conceitos gerais {#general-concepts}

### Modelo de página {#page-model}

A estrutura de conteúdo da página é armazenada em AEM. O modelo da página é usado para mapear e instanciar componentes do SPA. Os desenvolvedores do SPA criam componentes do SPA que mapeiam para AEM componentes. Para fazer isso, eles usam o tipo de recurso (ou caminho para o componente AEM) como uma chave exclusiva.

Os componentes do SPA devem estar em sincronia com o modelo de página e ser atualizados com quaisquer alterações em seu conteúdo de acordo. Um padrão que potencialize componentes dinâmicos deve ser usado para instanciar componentes dinamicamente após a estrutura do modelo de página fornecida.

### Campos de meta {#meta-fields}

O modelo de página aproveita o Exportador do Modelo JSON, que é baseado na API do Modelo [](https://sling.apache.org/documentation/bundles/models.html) Sling. Os modelos de sling exportáveis expõem a seguinte lista de campos para permitir que as bibliotecas subjacentes interpretem o modelo de dados:

* `:type`: Tipo do recurso AEM (padrão = tipo de recurso)
* `:children`: Filhos hierárquicos do recurso atual. Os filhos não fazem parte do conteúdo interno do recurso atual (pode ser encontrado em itens que representam uma página)
* `:hierarchyType`: Tipo hierárquico de um recurso. O `PageModelManager` atualmente suporta o tipo de página

* `:items`: Recursos de conteúdo filho do recurso atual (estrutura aninhada, presente apenas em container)
* `:itemsOrder`: Lista ordenada das crianças. O objeto de mapa JSON não garante a ordem de seus campos. Com o mapa e o array atual, o consumidor da API tem os benefícios de ambas as estruturas
* `:path`: Caminho do conteúdo de um item (presente em itens que representam uma página)

Consulte também [Introdução ao AEM Content Services.](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### Módulo específico da estrutura {#framework-specific-module}

A separação de preocupações ajuda a facilitar a implementação do projeto. Por conseguinte, deve ser fornecido um pacote específico para as npm. Este pacote é responsável por agregar e expor os módulos, serviços e componentes básicos. Esses componentes devem encapsular a lógica de gerenciamento do modelo de dados e fornecer acesso aos dados que o componente do projeto espera. O módulo também é responsável por expor transitoriamente pontos de entrada úteis das bibliotecas subjacentes.

Para facilitar a interoperabilidade das bibliotecas, o Adobe aconselha o módulo específico da estrutura a agrupar as seguintes bibliotecas. Se necessário, a camada pode encapsular e adaptar as APIs subjacentes antes de expô-las ao projeto.

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### Implementações {#implementations}

#### Reagir {#react}

módulo npm: [@adobe/aem-response-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angular {#angular}

módulo npm: em breve

## Principais serviços e componentes {#main-services-and-components}

As seguintes entidades devem ser implementadas em conformidade com as orientações específicas de cada quadro. Com base na arquitetura-quadro, a implementação pode variar bastante, mas as funcionalidades descritas devem ser fornecidas.

### O provedor de modelo {#the-model-provider}

Os componentes do projeto devem delegar acesso aos fragmentos de um modelo a um Provedor de modelos. O Provedor de modelos é responsável por acompanhar as alterações feitas no fragmento especificado do modelo e retornar o modelo atualizado ao componente de delegação.

Para fazer isso, o Provedor de modelos deve se registrar no ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`. Em seguida, quando uma alteração ocorre, ele recebe e transmite os dados atualizados para o componente de delegação. Por convenção, a propriedade disponibilizada ao componente de delegação que carregará o fragmento do modelo é nomeada `cqModel`. A implementação é gratuita para fornecer essa propriedade ao componente, mas deve considerar aspectos como a integração com a arquitetura da estrutura, a descoberta e a facilidade de uso.

### O Decorador HTML do componente {#the-component-html-decorator}

O Decorador de componentes é responsável por decorar o HTML externo do elemento de cada instância de componente com uma série de atributos de dados e nomes de classe esperados pelo Editor de páginas.

#### Declaração de componente {#component-declaration}

Os metadados a seguir devem ser adicionados ao elemento HTML externo produzido pelo componente do projeto. Eles permitem que o Editor de páginas recupere a configuração de edição correspondente.

* `data-cq-data-path`: Caminho para o recurso relativo ao `jcr:content`

#### Declaração de capacidade de edição e espaço reservado {#editing-capability-declaration-and-placeholder}

Os metadados e nomes de classe a seguir devem ser adicionados ao elemento HTML externo produzido pelo componente do projeto. Eles permitem que o Editor de páginas oferta funcionalidades relacionadas.

* `cq-placeholder`: Nome da classe que identifica o espaço reservado para um componente vazio
* `data-emptytext`: Rótulo a ser exibido pela sobreposição quando uma instância do componente estiver vazia

**Espaço reservado para componentes vazios**

Cada componente deve ser estendido com uma funcionalidade que decorará o elemento HTML externo com atributos de dados e nomes de classe específicos para espaços reservados e sobreposições relacionadas quando o componente for identificado como vazio.

**Sobre o vazio de um componente**

* O componente está logicamente vazio?
* Qual deve ser o rótulo exibido pela sobreposição quando o componente está vazio?

### Container {#container}

Um container é um componente destinado a conter e renderizar componentes filhos. Para isso, o container repete as `:itemsOrder`propriedades, `:items` e `:children` propriedades de seu modelo.

O container obtém dinamicamente os componentes filho da loja da ` [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)` biblioteca. O container estende o componente filho com os recursos do Provedor de modelos e, por fim, instanciá-lo.

### Página {#page}

O `Page` componente estende o `Container` componente. Um container é um componente destinado a conter e renderizar componentes filhos, incluindo páginas secundárias. Para fazer isso, o container repete as propriedades `:itemsOrder`, `:items`e `:children` propriedades de seu modelo. O `Page` componente obtém dinamicamente os componentes filho da loja da biblioteca [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping) . O `Page` é responsável pela instanciação de componentes filhos.

### Grade responsiva {#responsive-grid}

O componente Grade responsiva é um container. Ele contém uma variante específica do Provedor de modelos que representa suas colunas. A Grade responsiva e suas colunas são responsáveis por decorar o elemento HTML externo do componente do projeto com os nomes de classe específicos contidos no modelo.

O componente de Grade responsiva deve vir pré-mapeado para sua AEM contrapartida, pois esse componente é complexo e raramente personalizado.

#### Campos de modelo específicos {#specific-model-fields}

* `gridClassNames:` Nomes de classe fornecidos para a grade responsiva
* `columnClassNames:` Nomes de classe fornecidos para a coluna responsiva

Consulte também o recurso npm [@adobe/aem-response-editable-components#srccomponentsresponsivegridjsx](https://www.npmjs.com/package/@adobe/aem-react-editable-components#srccomponentsresponsivegridjsx)

#### Espaço reservado da grade responsiva {#placeholder-of-the-reponsive-grid}

O componente SPA é mapeado para um container gráfico, como a Grade responsiva, e deve adicionar um espaço reservado para filho virtual quando o conteúdo está sendo criado. Quando o conteúdo do SPA está sendo criado pelo Editor de páginas, esse conteúdo é incorporado ao editor usando um iframe e o `data-cq-editor` atributo é adicionado ao nó do documento desse conteúdo. Quando o `data-cq-editor` atributo está presente, o container deve incluir um HTMLElement para representar a área com a qual o autor interage ao inserir um novo componente na página.

Por exemplo:

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>Os nomes de classe usados no exemplo são exigidos atualmente pelo editor de página.
>
>* `"new section"`: Indica que o elemento atual é o espaço reservado do container
>* `"aem-Grid-newComponent"`: Normaliza o componente para a criação de layout

>



#### Component Mapping {#component-mapping}

A [`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping) biblioteca subjacente e sua `MapTo` função podem ser encapsuladas e estendidas para fornecer as funcionalidades relativas à configuração de edição fornecida ao lado da classe de componente atual.

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

Na implementação acima, o componente do projeto é estendido com a funcionalidade vazia antes de ser realmente registrado na loja Mapeamento [de](/help/sites-developing/spa-blueprint.md#componentmapping) componentes. Isso é feito encapsulando e estendendo a [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) biblioteca para introduzir o suporte do objeto de `EditConfig` configuração:

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

## Contrato com o editor de página {#contract-with-the-page-editor}

Os componentes do projeto devem gerar no mínimo os seguintes atributos de dados para permitir que o editor interaja com eles.

* `data-cq-data-path`: Caminho relativo do componente conforme fornecido pelo `PageModel` (por exemplo, `"root/responsivegrid/image"`). Este atributo não deve ser adicionado às páginas.

Em resumo, para ser interpretado pelo editor de página como editável, um componente de projeto deve respeitar o seguinte contrato:

* Forneça os atributos esperados para associar uma instância de componente front-end a um recurso AEM.
* Forneça a série esperada de atributos e nomes de classe que permitem a criação de espaços reservados vazios.
* Forneça os nomes de classe esperados, permitindo a ação de arrastar e soltar ativos.

### Estrutura típica do elemento HTML {#typical-html-element-structure}

O fragmento a seguir ilustra a representação HTML típica de uma estrutura de conteúdo de página. Estes são alguns pontos importantes:

* O elemento de grade responsivo contém nomes de classe prefixados com `aem-Grid--`
* O elemento de coluna responsiva contém nomes de classe prefixados com `aem-GridColumn--`
* Uma grade responsiva que também é a coluna de uma grade pai está encapsulada, como os dois prefixos anteriores não aparecem no mesmo elemento
* Os elementos correspondentes a recursos editáveis possuem uma `data-cq-data-path` propriedade. Consulte a seção [Contrato com o Editor](#contract-wtih-the-page-editor) de páginas deste documento.

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

O aplicativo é o proprietário do roteamento. Primeiro, o desenvolvedor front-end precisa implementar um componente de Navegação (mapeado para um componente de navegação AEM). Esse componente renderizaria links de URL a serem usados em conjunto com uma série de rotas que exibirão ou ocultarão fragmentos de conteúdo.

A [ biblioteca subjacente `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) e seu ` [ModelRouter](/help/sites-developing/spa-routing.md)` módulo (ativado por padrão) são responsáveis pela busca prévia e pelo acesso ao modelo associado a um determinado caminho de recurso.

As duas entidades se relacionam à noção de roteamento, mas o ` [ModelRouter](/help/sites-developing/spa-routing.md)` é responsável apenas por ter o ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` carregado com um modelo de dados estruturado em sincronia com o estado atual do aplicativo.

Consulte o artigo [SPA Model Roteamento](/help/sites-developing/spa-routing.md) para obter mais informações.

## SPA em ação {#spa-in-action}

Veja como um simples SPA funciona e experimente com um SPA você mesmo, continuando com o documento [Introdução aos SPAs no AEM](/help/sites-developing/spa-getting-started-react.md).

## Leitura adicional {#further-reading}

Para obter mais informações sobre SPAs em AEM, consulte os seguintes documentos:

* [Visão geral](/help/sites-developing/spa-overview.md) de criação do SPA para obter uma visão geral dos SPAs no AEM e no modelo de comunicação
* [Introdução aos SPAs em AEM](/help/sites-developing/spa-getting-started-react.md) para obter um guia para um SPA simples e como ele funciona
