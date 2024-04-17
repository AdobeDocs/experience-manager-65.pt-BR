---
title: Desenvolvimento de componentes do AEM
description: Os componentes do AEM são usados para reter, formatar e renderizar o conteúdo disponibilizado em suas páginas da Web.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3246'
ht-degree: 0%

---

# Desenvolvimento de componentes do AEM{#developing-aem-components}

Os componentes do AEM são usados para reter, formatar e renderizar o conteúdo disponibilizado em suas páginas da Web.

* Quando [criação de páginas](/help/sites-authoring/default-components.md), os componentes permitem que os autores editem e configurem o conteúdo.

   * Ao construir um [Commerce](/help/commerce/cif-classic/administering/ecommerce.md) site, os componentes podem, por exemplo, coletar e renderizar informações do catálogo.
Consulte [Desenvolvimento do comércio eletrônico](/help/commerce/cif-classic/developing/ecommerce.md) para obter mais informações.

   * Ao construir um [Communities](/help/communities/author-communities.md) site, os componentes podem fornecer informações e coletar informações de seus visitantes.
Consulte [Comunidades de desenvolvimento](/help/communities/communities.md) para obter mais informações.

* Na instância de publicação, os componentes renderizam o conteúdo, apresentando-o conforme necessário aos visitantes do site.

>[!NOTE]
>
>Esta página é uma continuação do documento [Componentes do AEM - Noções básicas](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>Componentes abaixo `/libs/cq/gui/components/authoring/dialog` devem ser usados somente no Editor (caixas de diálogo de componentes na Criação). Se forem usados em outro lugar (como em uma caixa de diálogo de assistente, por exemplo), talvez eles não se comportem conforme esperado.

## Amostras de código {#code-samples}

Esta página fornece a documentação de referência (ou links para a documentação de referência) necessária para desenvolver novos componentes para AEM. Consulte [Desenvolvimento de componentes do AEM - Amostras de código](/help/sites-developing/developing-components-samples.md) para obter alguns exemplos práticos.

## Estrutura {#structure}

A estrutura básica de um componente é abordada na página [Componentes do AEM - Noções básicas](/help/sites-developing/components-basics.md#structure). Esse documento abrange as interfaces habilitadas para toque e as interfaces clássicas. Mesmo que você não precise usar as configurações clássicas no novo componente, pode ser útil estar ciente delas ao herdar de componentes existentes.

## Extensão de componentes e caixas de diálogo existentes {#extending-existing-components-and-dialogs}

Dependendo do componente que você deseja implementar, talvez seja possível estender ou personalizar uma instância existente, em vez de definir e desenvolver a instância inteira [estrutura](#structure) do zero.

Ao estender ou personalizar um componente ou caixa de diálogo existente, você pode copiar ou replicar toda a estrutura ou a estrutura necessária para a caixa de diálogo antes de fazer as alterações.

### Extensão de um componente existente {#extending-an-existing-component}

A extensão de um componente existente pode ser obtida com [Hierarquia de tipo de recurso](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) e os mecanismos de herança relacionados.

>[!NOTE]
>
>Os componentes também podem ser redefinidos com uma sobreposição com base na lógica do caminho de pesquisa. No entanto, nesse caso, a [Fusão de recursos do Sling](/help/sites-developing/sling-resource-merger.md) não é acionado e `/apps` deve definir toda a sobreposição.

>[!NOTE]
>
>A variável [componente do fragmento de conteúdo](/help/sites-developing/customizing-content-fragments.md) O também pode ser personalizado e estendido, embora a estrutura completa e os relacionamentos com o Assets devam ser considerados.

### Personalização de uma caixa de diálogo Componente existente {#customizing-a-existing-component-dialog}

Também é possível substituir um *caixa de diálogo componente* usando o [Fusão de recursos do Sling](/help/sites-developing/sling-resource-merger.md) e definição da propriedade `sling:resourceSuperType`.

Isso significa que você só precisa redefinir as diferenças necessárias, em vez de redefinir toda a caixa de diálogo (usando `sling:resourceSuperType`). Este método agora é recomendado para estender uma caixa de diálogo de componente

Consulte a [Fusão de recursos do Sling](/help/sites-developing/sling-resource-merger.md) para obter mais detalhes.

## Definição da marcação {#defining-the-markup}

Seu componente será renderizado com [HTML](https://www.w3schools.com/htmL/html_intro.asp). Seu componente precisa definir o HTML necessário para obter o conteúdo necessário e, em seguida, renderizá-lo conforme necessário nos ambientes do autor e de publicação.

### Uso da Linguagem de modelo do HTML {#using-the-html-template-language}

A variável [Linguagem de modelo HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR), introduzido com o AEM 6.0, substitui o JSP (JavaServer Pages) como o sistema de modelo preferencial e recomendado do lado do servidor para o HTML. Para desenvolvedores da Web que precisam criar sites corporativos robustos, o HTL ajuda a aumentar a segurança e a eficiência do desenvolvimento.

>[!NOTE]
>
>Embora HTL e JSP possam ser usados para desenvolver componentes, ilustraremos o desenvolvimento com HTL nesta página, pois é a linguagem de script recomendada para AEM.

## Desenvolvimento da lógica do conteúdo {#developing-the-content-logic}

Essa lógica opcional seleciona e/ou calcula o conteúdo a ser renderizado. É chamado a partir de expressões HTL com o padrão Use-API apropriado.

O mecanismo para separar a lógica da aparência ajuda a esclarecer o que é necessário para uma determinada visualização. Também permite lógicas diferentes para visualizações diferentes do mesmo recurso.

### Uso do Java {#using-java}

[A API de uso Java do HTL permite que um arquivo HTL acesse métodos de ajuda em uma classe Java personalizada](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html). Isso permite usar o código Java para implementar a lógica de seleção e configuração do conteúdo do componente.

### Utilização do JavaScript {#using-javascript}

[A API de uso do JavaScript do HTL permite que um arquivo HTL acesse o código de ajuda gravado em JavaScript](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html). Isso permite usar o código JavaScript para implementar a lógica de seleção e configuração do conteúdo do componente.

### Uso de bibliotecas de HTML do lado do cliente {#using-client-side-html-libraries}

Sites modernos dependem muito do processamento do lado do cliente orientado por códigos JavaScript e CSS complexos. Organizar e otimizar a veiculação desse código pode ser um problema complicado.

Para ajudar a lidar com esse problema, o AEM fornece **Pastas de biblioteca do lado cliente**, que permitem armazenar o código do lado do cliente no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser entregue ao cliente. O sistema de biblioteca do lado do cliente cuida de produzir os links corretos na página final da Web para carregar o código correto.

Ler [Uso de bibliotecas de HTML do lado do cliente](/help/sites-developing/clientlibs.md) para obter mais informações.

## Configuração do comportamento de edição {#configuring-the-edit-behavior}

É possível configurar o comportamento de edição de um componente, incluindo atributos como ações disponíveis para o componente, características do editor local e os ouvintes relacionados aos eventos no componente. A configuração é comum à interface habilitada para toque e à interface clássica, embora com determinadas diferenças específicas.

A variável [editar comportamento de um componente está configurado](/help/sites-developing/components-basics.md#edit-behavior) adicionando um `cq:editConfig` nó do tipo `cq:EditConfig` abaixo do nó do componente (do tipo `cq:Component`) e adicionando propriedades específicas e nós filhos.

## Configuração do comportamento de visualização {#configuring-the-preview-behavior}

A variável [Modo WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) o cookie é definido ao alternar para **Visualizar** mesmo quando a página não é atualizada.

Para componentes com uma renderização sensível ao Modo WCM, eles precisam ser definidos para se atualizarem especificamente e, em seguida, confiar no valor do cookie.

>[!NOTE]
>
>Na interface habilitada para toque, somente os valores `EDIT` e `PREVIEW` são usados para o [Modo WCM](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) cookie.

## Criando e configurando uma caixa de diálogo {#creating-and-configuring-a-dialog}

As caixas de diálogo são usadas para permitir que o autor interaja com o componente. Usar uma caixa de diálogo permite que autores e/ou administradores editem conteúdo, configurem o componente ou definam parâmetros de design (usando um [Caixa de diálogo Design](#creating-and-configuring-a-design-dialog))

### Interface do usuário do Coral e do Granite {#coral-ui-and-granite-ui}

[Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) e [Interface do Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) definir a aparência moderna do AEM.

[A interface do usuário do Granite fornece uma grande variedade de componentes básicos (widgets)](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) necessário para criar sua caixa de diálogo no ambiente de criação. Quando necessário, é possível estender essa seleção e [criar seu próprio widget](#creatinganewwidget).

Para obter detalhes completos, consulte:

* Coral UI

   * Fornece uma interface consistente em todas as soluções em nuvem
   * [Conceitos da interface habilitada para toque por AEM - interface do Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Guia da interface de usuário do Coral](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html)

* Interface do Granite

   * Fornece marcação da interface Coral encapsulada em componentes Sling para construir consoles e caixas de diálogo da interface
   * [Conceitos da interface habilitada para toque por AEM - Interface do usuário do Granite](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Documentação da interface de usuário do Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)

>[!NOTE]
>
>Devido à natureza dos componentes da interface do Granite (e às diferenças dos widgets ExtJS), há algumas diferenças entre a forma como os componentes interagem com a interface habilitada para toque e a [IU clássica](/help/sites-developing/developing-components-classic.md).

### Criando uma nova caixa de diálogo {#creating-a-new-dialog}

Caixas de diálogo para a interface habilitada para toque:

* são nomeados `cq:dialog`.
* são definidos como um `nt:unstructured` com o nó `sling:resourceType` conjunto de propriedades.

* estão localizados sob sua `cq:Component` e ao lado da definição do componente.
* são renderizados no lado do servidor (como componentes do Sling), com base em sua estrutura de conteúdo e na `sling:resourceType` propriedade.
* usar a estrutura da interface de usuário do Granite.
* contém uma estrutura de nó que descreve os campos na caixa de diálogo.

   * esses nós são `nt:unstructured` com o necessário `sling:resourceType` propriedade.

Um exemplo de estrutura de nó pode ser:

```xml
newComponent (cq:Component)
  cq:dialog (nt:unstructured)
    content
      layout
      items
        column
          items
            file
            description
```

A personalização de uma caixa de diálogo é semelhante ao desenvolvimento de um componente, pois a caixa de diálogo é, em si, um componente (ou seja, uma marcação renderizada por um script de componente juntamente com o comportamento/estilo fornecido por uma biblioteca do cliente).

Para obter exemplos, consulte:

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>Se um componente não tiver uma caixa de diálogo definida para a interface habilitada para toque, a caixa de diálogo da interface clássica será usada como um fallback dentro de uma camada de compatibilidade. Para personalizar essa caixa de diálogo, é necessário personalizar a caixa de diálogo da interface clássica. Consulte [Componentes do AEM para a interface clássica](/help/sites-developing/developing-components-classic.md).

### Personalizar campos de diálogo {#customizing-dialog-fields}

>[!NOTE]
>
>Consulte:
>
>* a sessão AEM Gems em [Personalizar campos de diálogo](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html).
>* o código de amostra relacionado abrangido pelo [Amostra de código - Como personalizar campos de diálogo](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>

#### Criação de um novo campo {#creating-a-new-field}

Os dispositivos para a interface habilitada para toque são implementados como componentes de interface do Granite.

Para criar um widget para usar em uma caixa de diálogo de componente para a interface habilitada para toque, é necessário [criar um componente de campo da interface de usuário do Granite](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Para obter detalhes completos sobre a interface do Granite, consulte a [Documentação da interface de usuário do Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

Se você considerar sua caixa de diálogo como um contêiner simples para um elemento de formulário, também poderá ver o conteúdo principal do seu conteúdo da caixa de diálogo como campos de formulário. A criação de um campo de formulário requer a criação de um tipo de recurso; é equivalente à criação de um componente. Para ajudá-lo nessa tarefa, a interface do usuário do Granite oferece um componente de campo genérico do qual herdar (usando `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Mais especificamente, o Granite UI fornece uma variedade de componentes de campo adequados para uso em diálogos (ou, de forma mais geral, em [formulários](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Isso é diferente da interface clássica, onde os widgets são representados por `cq:Widgets` nós, cada um com um determinado `xtype` para estabelecer a relação com o widget ExtJS correspondente. Do ponto de vista da implementação, esses widgets foram renderizados no lado do cliente pela estrutura ExtJS.

Depois de criar o tipo de recurso, é possível instanciar o campo adicionando um novo nó na caixa de diálogo, com a propriedade `sling:resourceType` referindo-se ao tipo de recurso que acabou de introduzir.

#### Criação de uma biblioteca do cliente para estilo e comportamento {#creating-a-client-library-for-style-and-behavior}

Se quiser definir o estilo e o comportamento do componente, você poderá criar um [biblioteca do cliente](/help/sites-developing/clientlibs.md) que define seus CSS/LESS e JS personalizados.

Para carregar a biblioteca do cliente exclusivamente para a caixa de diálogo do componente (ou seja, ela não será carregada para outro componente), é necessário definir a propriedade `extraClientlibs` da caixa de diálogo para o nome da categoria da biblioteca do cliente que você criou. Isso é aconselhável se a biblioteca do cliente for muito grande e/ou se o campo for específico para essa caixa de diálogo e não for necessário em outras caixas de diálogo.

Para carregar a biblioteca do cliente para todas as caixas de diálogo, defina a propriedade category da biblioteca do cliente como `cq.authoring.dialog`. Esse é o nome da categoria da biblioteca do cliente que é incluído por padrão ao renderizar todas as caixas de diálogo. Você deseja fazer isso se a biblioteca do cliente for pequena e/ou seu campo for genérico e puder ser reutilizado em outras caixas de diálogo.

Para ver um exemplo, consulte:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * fornecido pelo [Amostra de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Estender (herdar de) um campo {#extending-inheriting-from-a-field}

Dependendo das suas necessidades, você pode:

* Estender um determinado campo da interface do usuário do Granite por herança de componente ( `sling:resourceSuperType`)
* Estender um determinado widget da biblioteca de widgets subjacente (se houver uma interface de usuário do Granite, essa é a Coral UI), seguindo a API da biblioteca de widgets (herança JS/CSS)

#### Acesso aos campos da caixa de diálogo {#access-to-dialog-fields}

Também é possível usar as condições de renderização ( `rendercondition`) para controlar quem tem acesso a guias/campos específicos na caixa de diálogo; por exemplo:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Manipulação de eventos de campo {#handling-field-events}

O método de manipulação de eventos em campos de diálogo agora é feito com [ouvintes em uma biblioteca de cliente personalizada](#listeners-in-a-custom-client-library). Essa é uma alteração do método mais antigo de ter [ouvintes na estrutura de conteúdo](#listenersinthecontentstructureclassicui).

#### Ouvintes em uma biblioteca de cliente personalizada {#listeners-in-a-custom-client-library}

Para inserir lógica no campo, você deve:

1. Marque o campo com uma determinada classe CSS (a variável *gancho*).
1. Defina, na biblioteca do cliente, um ouvinte JS conectado a esse nome de classe CSS (isso garante que a lógica personalizada tenha escopo somente para o campo e não afete outros campos do mesmo tipo).

Para fazer isso, você precisa saber sobre a biblioteca de widgets subjacente com a qual deseja interagir. Consulte a [Documentação da interface do Coral](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) para identificar a qual evento você deseja reagir. Isso é muito semelhante ao processo que você teve que executar com ExtJS no passado: localize a página de documentação de um determinado widget e, em seguida, verifique os detalhes da API de evento.

Para ver um exemplo, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * fornecido pelo [Amostra de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Ouvintes na estrutura de conteúdo {#listeners-in-the-content-structure}

Na interface clássica com ExtJS, era comum ter ouvintes de um determinado widget na estrutura do conteúdo. Fazer o mesmo na interface habilitada para toque é diferente, pois o código de ouvinte JS (ou qualquer código) não é mais definido no conteúdo.

A estrutura de conteúdo descreve a estrutura semântica; ela não deve (deve) implicar a natureza do widget subjacente. Ao não ter o código JS na estrutura do conteúdo, é possível alterar os detalhes da implementação sem precisar alterar a estrutura do conteúdo. Em outras palavras, você pode alterar a biblioteca de widgets sem precisar tocar na estrutura de conteúdo.

#### Detectando Disponibilidade da Caixa de Diálogo {#dialog-ready}

Se você tiver um JavaScript personalizado que precisa ser executado somente quando a caixa de diálogo estiver disponível e pronta, você deve ouvir o `dialog-ready` evento.

Esse evento é acionado sempre que a caixa de diálogo é carregada (ou recarregada) e está pronta para uso, o que significa que sempre que há uma alteração (criar/atualizar) no DOM da caixa de diálogo.

`dialog-ready` O pode ser usado para conectar o código personalizado JavaScript que executa personalizações nos campos dentro de uma caixa de diálogo ou tarefas semelhantes.

### Validação de campo {#field-validation}

#### Campo obrigatório {#mandatory-field}

Para marcar um determinado campo como obrigatório, defina a seguinte propriedade no nó de conteúdo do campo:

* Nome: `required`
* Tipo: `Boolean`

Para ver um exemplo, consulte:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### Validação de campo (interface do usuário do Granite) {#field-validation-granite-ui}

A validação de campo na interface do usuário do Granite e nos componentes da interface do usuário do Granite (equivalente a widgets) é feita usando `foundation-validation` API. [Consulte a `foundation-valdiation` Documentação do Granite para obter detalhes.](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Para obter exemplos, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * fornecido pelo [Amostra de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Criando e configurando uma caixa de diálogo de design {#creating-and-configuring-a-design-dialog}

A caixa de diálogo Design é fornecida quando um componente tem detalhes de design que podem ser editados no [Modo Design](/help/sites-authoring/default-components-designmode.md).

A definição é muito semelhante à de um [caixa de diálogo usada para editar conteúdo](#creating-a-new-dialog), com a diferença de que é definido como um nó:

* Nome do nó: `cq:design_dialog`
* Tipo: `nt:unstructured`

## Criação e configuração de um editor local {#creating-and-configuring-an-inplace-editor}

Um editor local permite que o usuário edite o conteúdo diretamente no fluxo de parágrafo, sem a necessidade de abrir uma caixa de diálogo. Por exemplo, os componentes Texto e Título padrão têm um editor local.

Um editor local não é necessário/significativo para cada tipo de componente.

Consulte [Extensão da criação de páginas - Adicionar novo editor de local](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) para obter mais informações.

## Personalização da barra de ferramentas do componente {#customizing-the-component-toolbar}

A variável [Component Toolbar](/help/sites-developing/touch-ui-structure.md#component-toolbar) fornece ao usuário acesso a uma variedade de ações para o componente, como editar, configurar, copiar e excluir.

Consulte [Extensão de criação de página - Adicionar nova ação a uma barra de ferramentas do componente](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) para obter mais informações.

## Configurar um componente para o painel de referências (emprestado/concedido) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Se o novo componente fizer referência ao conteúdo de outras páginas, você poderá considerar se deseja que ele afete a **Conteúdo Emprestado** e **Conteúdo concedido** seções do [**Referências**](/help/sites-authoring/basic-handling.md#references) Ferroviário.

O AEM pronto para uso verifica apenas o componente de Referência. Para adicionar seu componente, é necessário configurar o pacote OSGi **Configuração de referência de conteúdo de criação do WCM**.

Crie uma entrada na definição, especificando seu componente, juntamente com a propriedade a ser verificada. Por exemplo:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>Ao trabalhar com o AEM, há vários métodos de gerenciamento das definições de configuração desses serviços. Consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

## Ativação e adição do componente ao sistema de parágrafos {#enabling-and-adding-your-component-to-the-paragraph-system}

Depois que o componente tiver sido desenvolvido, ele precisará ser ativado para uso em um sistema de parágrafo apropriado, para que possa ser usado nas páginas necessárias.

Isso pode ser feito:

* usar [Modo de design](/help/sites-authoring/default-components-designmode.md) ao editar uma página específica.
* [definição do `components` propriedade no sistema de parágrafo de um modelo](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## Configurar um sistema de parágrafo para que arrastar um ativo crie uma instância de componente {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

O AEM oferece a possibilidade de configurar um sistema de parágrafos em sua página para que [uma instância do novo componente é criada automaticamente quando um usuário arrasta um ativo (apropriado) para uma instância dessa página](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (em vez de sempre ter que arrastar um componente vazio para a página).

Esse comportamento e a relação necessária entre ativo e componente podem ser configurados:

1. Na definição de parágrafo do design da página. Por exemplo:

   * `/etc/designs/<myApp>/page/par`

   Criar um nó:

   * Nome: `cq:authoring`
   * Tipo: `nt:unstructured`

1. Em, crie um nó para manter todos os mapeamentos de ativo para componente:

   * Nome: `assetToComponentMapping`
   * Tipo: `nt:unstructured`

1. Para cada mapeamento de ativo para componente, crie um nó:

   * Nome: texto; recomenda-se que o nome indique o ativo e o tipo de componente relacionado; por exemplo, imagem
   * Tipo: `nt:unstructured`

   Cada um com as seguintes propriedades:

   * `assetGroup`:

      * Tipo: `String`
      * Valor: o grupo ao qual o ativo relacionado pertence; por exemplo, `media`

   * `assetMimetype`:

      * Tipo: `String`
      * Valor: o tipo MIME do ativo relacionado; por exemplo, `image/*`

   * `droptarget`:

      * Tipo: `String`
      * Valor: o alvo de liberação; por exemplo, `image`

   * `resourceType`:

      * Tipo: `String`
      * Valor: o recurso componente relacionado; por exemplo, `foundation/components/image`

   * `type`:

      * Tipo: `String`
      * Valor: o tipo, por exemplo, `Images`

Para obter exemplos, consulte:

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir projeto aem-project-archetype no GitHub](https://github.com/adobe/aem-project-archetype)
* Baixar o projeto como [um arquivo ZIP](https://github.com/adobe/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>A criação automática de instâncias de componentes agora pode ser configurada facilmente na interface ao usar [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) e modelos editáveis. Consulte [Criação de modelos de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) para obter mais informações sobre como definir quais componentes são associados automaticamente a determinados tipos de mídia.

## Uso da extensão AEM Brackets {#using-the-aem-brackets-extension}

A variável [Extensão de Colchetes AEM](/help/sites-developing/aem-brackets.md) O fornece um fluxo de trabalho suave para editar componentes do AEM e bibliotecas de clientes. Baseia-se no [Colchetes](https://brackets.io/) editor de código.

A extensão:

* Facilita a sincronização (sem a necessidade de Maven ou File Vault) para ajudar a aumentar a eficiência do desenvolvedor e também ajuda desenvolvedores de front-end com conhecimento limitado em AEM a participar de projetos.
* Fornece alguns [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR) suporte, a linguagem de modelo criada para simplificar o desenvolvimento de componentes e aumentar a segurança.

>[!NOTE]
>
>Colchetes é o mecanismo recomendado para criar componentes. Ele substitui a funcionalidade CRXDE Lite - Criar componente, projetada para a interface clássica.

## Migração de um componente clássico {#migrating-from-a-classic-component}

Ao migrar um componente projetado para uso com a interface clássica para um componente que pode ser usado com a interface habilitada para toque (exclusiva ou conjuntamente), os seguintes problemas devem ser considerados:

* HTL

   * Uso do [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR) não é obrigatório, mas se o componente precisar ser atualizado, é o momento ideal para considerar [migração de JSP para HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Componentes

   * Migrar [`cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) código que usa funções específicas da interface clássica
   * Plug-in RTE. Para obter mais informações, consulte [Configuração do editor de rich text](/help/sites-administering/rich-text-editor.md).
   * [Migrar `cq:listener` código](#migrating-cq-listener-code) que usa funções específicas para a interface clássica

* Caixas de diálogo

   * Crie uma caixa de diálogo para usar na interface habilitada para toque. No entanto, para fins de compatibilidade, a interface habilitada para toque pode usar a definição de uma caixa de diálogo da interface clássica, quando nenhuma caixa de diálogo foi definida para a interface habilitada para toque.
   * A variável [Ferramentas de modernização do AEM](/help/sites-developing/modernization-tools.md) são fornecidos para ajudar a estender os componentes existentes.
   * [Mapeamento de ExtJS para componentes de interface do usuário do Granite](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) O fornece uma visão geral conveniente dos tipos xtypes ExtJS e tipos de nós com seus tipos de recursos equivalentes da interface do usuário do Granite.
   * Personalização de campos, para obter mais informações, consulte a sessão Gems do AEM em [Personalizar campos de diálogo](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html).
   * Migrar de vtypes para [Validação da interface do usuário do Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Usando ouvintes JS, para obter mais informações, consulte [Manipulação de eventos de campo](#handling-field-events) e a sessão AEM Gems em [Personalizar campos de diálogo](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html).

### Migrando o código cq:listener {#migrating-cq-listener-code}

Se você estiver migrando um projeto criado para a interface clássica, a variável `cq:listener` o código (e clientlibs relacionadas ao componente) pode usar funções específicas para a interface clássica (como `CQ.wcm.*`). Para a migração, você deve atualizar esse código usando os objetos/funções equivalentes na interface habilitada para toque.

Se o projeto estiver sendo completamente migrado para a interface habilitada para toque, será necessário substituir esse código para usar os objetos e funções relevantes para a interface habilitada para toque.

No entanto, se o seu projeto precisar atender à interface clássica e à interface habilitada para toque durante o período de migração (o cenário normal), você deverá implementar uma opção para diferenciar o código separado que faz referência aos objetos apropriados.

Esse mecanismo de switch pode ser implementado como:

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## Documentação do componente {#documenting-your-component}

Como desenvolvedor, você deseja obter acesso fácil à documentação de componentes para compreender rapidamente:

* Descrição
* Uso previsto
* Estrutura de conteúdo e propriedades
* APIs e pontos de extensão expostos
* E assim por diante

Por isso, é fácil criar qualquer marcação de documentação existente disponível no próprio componente.

Colocar um `README.md` na estrutura do componente. Essa marcação é exibida no campo [console do componente](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

A marcação compatível é a mesma para [fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-markdown.md).
