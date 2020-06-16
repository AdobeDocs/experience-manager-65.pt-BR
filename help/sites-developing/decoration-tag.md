---
title: Tag de decoração
description: Quando um componente em uma página da Web é renderizado, um elemento HTML pode ser gerado, vinculando o componente renderizado dentro dele mesmo. Para desenvolvedores, a lógica clara e simples do AEM oferta controla as marcas de decoração que envolvem os componentes incluídos.
translation-type: tm+mt
source-git-commit: be1c0e21216b1014a36f88d13557f6e1d7a87c0a
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 1%

---


# Tag de decoração{#decoration-tag}

Quando um componente em uma página da Web é renderizado, um elemento HTML pode ser gerado, vinculando o componente renderizado dentro dele mesmo. Isto serve principalmente dois objetivos:

* Um componente só pode ser editado quando estiver envolvido com um elemento HTML.
* O elemento de vinculação é usado para aplicar classes HTML que fornecem:

   * informações de layout
   * informações de estilo

Para desenvolvedores, a lógica clara e simples do AEM oferta controla as marcas de decoração que envolvem os componentes incluídos. Se e como a tag de decoração é renderizada é definida pela combinação de dois fatores, que esta página dividirá em:

* O próprio componente pode configurar sua tag de decoração com um conjunto de propriedades.
* Os scripts que incluem componentes (HTL, JSP, dispatcher etc.) podem definir os aspectos da tag de decoração com parâmetros de inclusão.

## Recomendações {#recommendations}

Estas são algumas recomendações gerais de quando incluir o elemento wrapper que deve ajudar a evitar problemas inesperados:

* A presença do elemento wrapper não deve diferir entre WCMModes (modo de edição ou pré-visualização), instâncias (autor ou publicação) ou ambientes (armazenamento temporário ou produção), de modo que o CSS e o JavaScripts da página funcionem de forma idêntica em todos os casos.
* O elemento wrapper deve ser adicionado a todos os componentes editáveis, para que o editor de páginas possa inicializá-los e atualizá-los corretamente.
* Para componentes não editáveis, o elemento wrapper pode ser evitado se não servir a função específica, de modo que a marcação resultante não fique inchada desnecessariamente.

## Controles de componentes {#component-controls}

As seguintes propriedades e nós podem ser aplicados aos componentes para controlar o comportamento de sua tag de decoração:

* **`cq:noDecoration {boolean}`:**Essa propriedade pode ser adicionada a um componente e um valor real faz com que o AEM não gere elementos de invólucro sobre o componente.

* **`cq:htmlTag`nó :**Esse nó pode ser adicionado em um componente e pode ter as seguintes propriedades:

   * **`cq:tagName {String}`:**Isso pode ser usado para especificar uma tag HTML personalizada a ser usada para vincular os componentes em vez do elemento DIV padrão.
   * **`class {String}`:**Isso pode ser usado para especificar nomes de classe css a serem adicionados ao invólucro.
   * Outros nomes de propriedade serão adicionados como atributos HTML com o mesmo valor String fornecido.

## Controles de script {#script-controls}

O comportamento do invólucro difere, no entanto, dependendo se [HTL](/help/sites-developing/decoration-tag.md#htl) ou [JSP](/help/sites-developing/decoration-tag.md#jsp) for usado para incluir o elemento.

### HTL {#htl}

Em geral, o comportamento do invólucro em HTL pode ser resumido da seguinte forma:

* Nenhum DIV de invólucro é renderizado por padrão (apenas ao fazer `data-sly-resource="foo"`).
* Todos os modos de wcm (desativados, pré-visualizações, editar no autor e publicar) são renderizados de forma idêntica.

O comportamento do invólucro também pode ser totalmente controlado.

* O script HTL tem controle total sobre o comportamento resultante da tag wrapper.
* As propriedades do componente (como `cq:noDecoration` e `cq:tagName`) também podem definir a tag do invólucro.

É possível controlar totalmente o comportamento das tags de wrapper dos scripts HTL e sua lógica associada.

Para obter mais informações sobre o desenvolvimento em HTL, consulte a documentação [](https://docs.adobe.com/content/help/br/experience-manager-htl/using/overview.html)HTL.

#### Árvore de decisão {#decision-tree}

Essa árvore decisória resume a lógica que determina o comportamento das tags de invólucro.

![chlimage_1-75](assets/chlimage_1-75a.png)

#### Use Cases {#use-cases}

Os três casos de uso a seguir fornecem exemplos de como as tags de invólucro são manipuladas e também ilustram como é simples controlar o comportamento desejado das tags de invólucro.

Todos os exemplos a seguir pressupõem a seguinte estrutura de conteúdo e componentes:

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### Caso de uso 1: Incluir um componente para reutilização de código {#use-case-include-a-component-for-code-reuse}

O caso de uso mais comum é quando um componente inclui outro componente por motivos de reutilização do código. Nesse caso, o componente incluído não é desejado para ser editável com sua própria barra de ferramentas e caixa de diálogo, portanto, nenhum invólucro é necessário e o componente `cq:htmlTag` será ignorado. Isso pode ser considerado o comportamento padrão.

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

Saída resultante em `/content/test.html`:

**`Hello World!`**

Um exemplo seria um componente que inclui um componente de imagem principal para exibir uma imagem, normalmente nesse caso usando um recurso sintético, que consiste em incluir um componente filho virtual transmitindo para o recurso inteligente de dados um objeto de mapa que representa todas as propriedades que o componente teria.

#### Caso de uso 2: Incluir um componente editável {#use-case-include-an-editable-component}

Outro caso de uso comum é quando os componentes do container incluem componentes filhos editáveis, como um Container de layout. Nesse caso, cada filho incluído precisa imperativamente de um invólucro para que o editor funcione (a menos que explicitamente desabilitado com a `cq:noDecoration` propriedade).

Como o componente incluído é, nesse caso, um componente independente, ele precisa de um elemento de invólucro para que o editor funcione e defina seu layout e estilo para aplicar. Para acionar esse comportamento, há a `decoration=true` opção.

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

Saída resultante em `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### Caso de uso 3: Comportamento personalizado {#use-case-custom-behavior}

Pode haver vários casos complexos, que podem ser facilmente alcançados através da possibilidade de HTL fornecer explicitamente:

* **`decorationTagName='ELEMENT_NAME'`** Para definir o nome do elemento do invólucro.
* **`cssClassName='CLASS_NAME'`** Para definir os nomes de classe CSS a serem definidos.

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

Saída resultante `/content/test.html`:

**`<aside class="child">Hello World!</aside>`**

## JSP {#jsp}

Ao incluir um componente usando `cq:includ`e ou `sling:include`, o comportamento padrão no AEM é usar um DIV para vincular o elemento. No entanto, essa vinculação pode ser personalizada de duas formas:

* Diga explicitamente ao AEM para não envolver o componente usando `cq:noDecoration`.
* Use uma tag HTML personalizada para vincular o componente usando `cq:htmlTag`/ `cq:tagName` ou `decorationTagName`.

### Árvore de decisão {#decision-tree-1}

A árvore decisória a seguir ilustra como `cq:noDecoration`, `cq:htmlTag`, `cq:tagName`e `decorationTagName` afeta o comportamento do invólucro.

![chlimage_1-3](assets/chlimage_1-3a.jpeg)

