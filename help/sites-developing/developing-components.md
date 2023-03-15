---
title: Desenvolvimento de componentes de AEM
seo-title: Developing AEM Components
description: AEM componentes são usados para manter, formatar e renderizar o conteúdo disponibilizado nas suas páginas da Web.
seo-description: AEM components are used to hold, format, and render the content made available on your webpages.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '3477'
ht-degree: 2%

---

# Desenvolvimento de componentes de AEM{#developing-aem-components}

AEM componentes são usados para manter, formatar e renderizar o conteúdo disponibilizado nas suas páginas da Web.

* When [criação de páginas](/help/sites-authoring/default-components.md), os componentes permitem que os autores editem e configurem o conteúdo.

   * Ao construir um [Comércio](/help/commerce/cif-classic/administering/ecommerce.md) site em que os componentes podem, por exemplo, coletar e renderizar informações do catálogo.
Consulte [Desenvolvimento do comércio eletrônico](/help/commerce/cif-classic/developing/ecommerce.md) para obter mais informações.

   * Ao construir um [Comunidades](/help/communities/author-communities.md) no site, os componentes podem fornecer informações e coletar informações de seus visitantes.
Consulte [Desenvolvimento de comunidades](/help/communities/communities.md) para obter mais informações.

* Na instância de publicação, os componentes renderizam o conteúdo, apresentando-o como você precisa para os visitantes do site.

>[!NOTE]
>
>Esta página é uma continuação do documento [Componentes AEM - Noções básicas](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>Componentes abaixo `/libs/cq/gui/components/authoring/dialog` devem ser usadas somente no Editor (caixas de diálogo de componentes em Criação). Se forem usados em outro local (como em uma caixa de diálogo do assistente, por exemplo), talvez não se comportem conforme esperado.

## Amostras de código {#code-samples}

Esta página fornece a documentação de referência (ou links para a documentação de referência) necessária para desenvolver novos componentes para o AEM. Consulte [Desenvolvimento de componentes de AEM - Amostras de código](/help/sites-developing/developing-components-samples.md) para obter alguns exemplos práticos.

## Estrutura {#structure}

A estrutura básica de um componente é abordada na página [Componentes AEM - Noções básicas](/help/sites-developing/components-basics.md#structure). Esse documento abrange as interfaces de usuário habilitadas para toque e clássica. Mesmo que você não precise usar as configurações clássicas em seu novo componente, isso pode ajudar a conhecê-las ao herdar dos componentes existentes.

## Extensão de componentes e caixas de diálogo existentes {#extending-existing-components-and-dialogs}

Dependendo do componente que você deseja implementar, pode ser possível estender ou personalizar uma instância existente, em vez de definir e desenvolver o [estrutura](#structure) do zero.

Ao estender ou personalizar um componente ou caixa de diálogo existente, você pode copiar ou replicar toda a estrutura ou a estrutura necessária para a caixa de diálogo antes de fazer suas alterações.

### Extensão de um componente existente {#extending-an-existing-component}

A extensão de um componente existente pode ser alcançada com [Hierarquia do Tipo de Recurso](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) e os mecanismos de herança relacionados.

>[!NOTE]
>
>Os componentes também podem ser redefinidos com uma sobreposição baseada na lógica do caminho de pesquisa. No entanto, nesse caso, o [Fusão de Recursos Sling](/help/sites-developing/sling-resource-merger.md) não será acionado e `/apps` deve definir a sobreposição inteira.

>[!NOTE]
>
>O [componente do fragmento de conteúdo](/help/sites-developing/customizing-content-fragments.md) também pode ser personalizado e estendido, embora a estrutura completa e os relacionamentos com o Assets devam ser considerados.

### Personalização de uma caixa de diálogo de componente existente {#customizing-a-existing-component-dialog}

Também é possível substituir um *caixa de diálogo do componente* usando o [Fusão de Recursos Sling](/help/sites-developing/sling-resource-merger.md) e definição da propriedade `sling:resourceSuperType`.

Isso significa que você só precisa redefinir as diferenças necessárias, em vez de redefinir toda a caixa de diálogo (usando `sling:resourceSuperType`). Esse agora é um método recomendado para estender uma caixa de diálogo de componentes

Consulte a [Fusão de Recursos Sling](/help/sites-developing/sling-resource-merger.md) para obter mais detalhes.

## Como definir a marcação {#defining-the-markup}

Seu componente será renderizado com [HTML](https://www.w3schools.com/htmL/html_intro.asp). Seu componente precisa definir o HTML necessário para obter o conteúdo necessário e, em seguida, renderizá-lo conforme necessário, nos ambientes de autor e publicação.

### Utilização da Linguagem de Modelo do HTML {#using-the-html-template-language}

O [Linguagem de modelo de HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html), introduzido com o AEM 6.0, substitui o JSP (JavaServer Pages) como o sistema de modelo preferencial e recomendado do lado do servidor para o HTML. Para desenvolvedores da Web que precisam criar sites corporativos robustos, o HTL ajuda a aumentar a segurança e a eficiência do desenvolvimento.

>[!NOTE]
>
>Embora o HTL e o JSP possam ser usados para desenvolver componentes, ilustraremos o desenvolvimento com o HTL nesta página, pois é a linguagem de script recomendada para o AEM.

## Desenvolvimento da lógica de conteúdo {#developing-the-content-logic}

Essa lógica opcional seleciona e/ou calcula o conteúdo a ser renderizado. É chamado de expressões HTL com o padrão Use-API apropriado.

O mecanismo para separar a lógica da aparência ajuda a esclarecer o que é chamado para uma determinada exibição. Também permite lógica diferente para diferentes exibições do mesmo recurso.

### Uso do Java {#using-java}

[A API de uso do Java do HTL permite que um arquivo HTL acesse métodos de ajuda em uma classe Java personalizada](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html). Isso permite usar o código Java para implementar a lógica de seleção e configuração do conteúdo do componente.

### Como usar o JavaScript {#using-javascript}

[A API de uso do JavaScript do HTL permite que um arquivo HTL acesse o código de ajuda gravado em JavaScript](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html). Isso permite usar o código JavaScript para implementar a lógica de seleção e configuração do conteúdo do componente.

### Usar bibliotecas HTML do lado do cliente {#using-client-side-html-libraries}

Sites modernos dependem muito de processamento no lado do cliente impulsionado por códigos complexos de JavaScript e CSS. Organizar e otimizar a veiculação desse código pode ser um problema complicado.

Para ajudar a lidar com esse problema, AEM fornece **Pastas de bibliotecas do lado do cliente**, que permitem armazenar o código do lado do cliente no repositório, organizá-lo em categorias e definir quando e como cada categoria de código deve ser apresentada ao cliente. O sistema de bibliotecas do lado do cliente cuida da produção dos links corretos na página da Web final para carregar o código correto.

Ler [Usar bibliotecas HTML do lado do cliente](/help/sites-developing/clientlibs.md) para obter mais informações.

## Configurar o comportamento de edição {#configuring-the-edit-behavior}

É possível configurar o comportamento de edição de um componente, incluindo atributos, como ações disponíveis para o componente, características do editor local e ouvintes relacionados a eventos no componente. A configuração é comum à interface habilitada para toque e clássica, embora com determinadas diferenças específicas.

O [editar o comportamento de um componente está configurado](/help/sites-developing/components-basics.md#edit-behavior) adicionando uma `cq:editConfig` nó do tipo `cq:EditConfig` abaixo do nó do componente (do tipo `cq:Component`) e adicionando propriedades específicas e nós secundários.

## Configuração do comportamento de visualização {#configuring-the-preview-behavior}

O [Modo WCM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) cookie é definido ao alternar para **Visualizar** mesmo quando a página não é atualizada.

Para componentes com uma renderização que são sensíveis ao modo WCM, eles precisam ser definidos para serem atualizados especificamente e, em seguida, dependem do valor do cookie.

>[!NOTE]
>
>Na interface habilitada para toque, somente os valores `EDIT` e `PREVIEW` são usados para [Modo WCM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) cookie.

## Criação e configuração de uma caixa de diálogo {#creating-and-configuring-a-dialog}

As caixas de diálogo são usadas para permitir que o autor interaja com o componente. Usar uma caixa de diálogo permite que autores e/ou administradores editem o conteúdo, configurem o componente ou definam parâmetros de design (usando um [Caixa de diálogo Design](#creating-and-configuring-a-design-dialog))

### Interface do usuário do Coral e do Granite {#coral-ui-and-granite-ui}

[Interface do usuário do Coral](https://helpx.adobe.com/br/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) e [Interface do usuário do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) defina a aparência moderna do AEM.

[A interface do usuário do Granite fornece uma grande variedade de componentes básicos (widgets)](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) necessário para criar sua caixa de diálogo no ambiente de criação. Quando necessário, é possível estender essa seleção e [criar seu próprio widget](#creatinganewwidget).

Para obter detalhes completos, consulte:

* Interface do usuário do Coral

   * Fornece uma interface do usuário consistente em todas as soluções de nuvem
   * [Conceitos da interface de usuário habilitada para toque do AEM - Interface do usuário do Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Guia da interface do usuário do Coral](https://helpx.adobe.com/br/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Interface do usuário do Granite

   * Fornece marcação Coral UI encapsulada em componentes Sling para criar consoles e caixas de diálogo da interface do usuário
   * [Conceitos da interface habilitada para toque do AEM - Interface do usuário do Granite](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Documentação da interface de usuário do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>Devido à natureza dos componentes da interface do usuário do Granite (e diferenças nos widgets ExtJS), há algumas diferenças entre a forma como os componentes interagem com a interface do usuário habilitada para toque e a [interface clássica](/help/sites-developing/developing-components-classic.md).

### Criação de uma nova caixa de diálogo {#creating-a-new-dialog}

Caixas de diálogo da interface habilitada para toque:

* são nomeadas `cq:dialog`.
* são definidos como um `nt:unstructured` com o `sling:resourceType` conjunto de propriedades.

* estejam localizadas sob a sua `cq:Component` e ao lado da definição do componente.
* são renderizados no lado do servidor (como componentes do Sling), com base em sua estrutura de conteúdo e na variável `sling:resourceType` propriedade.
* use a estrutura da interface do usuário do Granite.
* contém uma estrutura de nó que descreve os campos na caixa de diálogo.

   * esses nós são `nt:unstructured` com o `sling:resourceType` propriedade.

Uma estrutura de nó de exemplo pode ser:

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

A personalização de uma caixa de diálogo é semelhante ao desenvolvimento de um componente, já que a caixa de diálogo é um componente (ou seja, uma marcação renderizada por um script de componente junto com o comportamento/estilo fornecido por uma biblioteca do cliente).

Para obter exemplos, consulte:

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>Se um componente não tiver uma caixa de diálogo definida para a interface habilitada para toque, a caixa de diálogo da interface clássica será usada como um fallback dentro de uma camada de compatibilidade. Para personalizar essa caixa de diálogo, é necessário personalizar a caixa de diálogo da interface clássica. Consulte [Componentes do AEM para a interface clássica](/help/sites-developing/developing-components-classic.md).

### Personalização de campos de diálogo {#customizing-dialog-fields}

>[!NOTE]
>
>Consulte:
>
>* a sessão AEM Gems em [Personalização de campos de diálogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
>* o código de amostra correspondente abrangido pelo [Amostra de código - Como personalizar campos de diálogo](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>


#### Criação de um novo campo {#creating-a-new-field}

Os widgets da interface de usuário habilitada para toque são implementados como componentes da interface de usuário do Granite.

Para criar um novo widget para uso em uma caixa de diálogo de componentes para a interface habilitada para toque, é necessário [criar um novo componente de campo da interface do usuário do Granite](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Para obter detalhes completos sobre a interface do usuário do Granite, consulte o [Documentação da interface do usuário do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Se sua caixa de diálogo for considerada um contêiner simples para um elemento de formulário, você também poderá ver o conteúdo principal do conteúdo da caixa de diálogo como campos de formulário. A criação de um novo campo de formulário requer a criação de um tipo de recurso; isso equivale a criar um novo componente. Para ajudar você nessa tarefa, a interface do usuário do Granite oferece um componente de campo genérico do qual herdar (usando `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Mais especificamente, a interface do usuário do Granite fornece uma variedade de componentes de campo adequados para uso em caixas de diálogo (ou, de modo mais geral, em [formulários](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Isso é diferente da interface clássica, onde os widgets são representados por `cq:Widgets` nós, cada um com um `xtype` para estabelecer a relação com o widget ExtJS correspondente. Do ponto de vista da implementação, esses widgets foram renderizados no lado do cliente pela estrutura ExtJS.

Depois de criar o tipo de recurso, é possível instanciar o campo adicionando um novo nó na caixa de diálogo, com a propriedade `sling:resourceType` referência ao tipo de recurso que acabou de apresentar.

#### Criação de uma biblioteca do cliente para estilo e comportamento {#creating-a-client-library-for-style-and-behavior}

Se quiser definir o estilo e o comportamento do seu componente, é possível criar um [biblioteca do cliente](/help/sites-developing/clientlibs.md) que define o CSS/LESS e o JS personalizados.

Para carregar a biblioteca do cliente apenas para a caixa de diálogo do componente (ou seja, ela não será carregada para outro componente), é necessário definir a propriedade `extraClientlibs`** **da caixa de diálogo para o nome da categoria da biblioteca do cliente que você acabou de criar. Isso é aconselhável se a biblioteca do cliente for muito grande e/ou se o campo for específico dessa caixa de diálogo e não for necessário em outras caixas de diálogo.

Para carregar sua biblioteca do cliente para todas as caixas de diálogo, defina a propriedade category da biblioteca do cliente como `cq.authoring.dialog`. Esse é o nome da categoria da biblioteca do cliente incluída por padrão ao renderizar todas as caixas de diálogo. Você deseja fazer isso se a biblioteca do cliente for pequena e/ou se o campo for genérico e puder ser reutilizado em outras caixas de diálogo.

Para ver um exemplo, consulte:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * do [Amostra de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Estender (Herdar de) um campo {#extending-inheriting-from-a-field}

Dependendo dos seus requisitos, você pode:

* Estender um determinado campo da interface do usuário do Granite por herança de componente ( `sling:resourceSuperType`)
* Estender um determinado widget a partir da biblioteca de widgets subjacente (no caso da interface do usuário do Granite, essa é a interface do usuário Coral), seguindo a API da biblioteca de widgets (herança JS/CSS)

#### Acesso aos campos de diálogo {#access-to-dialog-fields}

Também é possível usar condições de renderização ( `rendercondition`) para controlar quem tem acesso a guias/campos específicos na caixa de diálogo; por exemplo:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Tratamento de eventos de campo {#handling-field-events}

O método de tratamento de eventos em campos de diálogo agora é feito com [ouvintes em uma biblioteca cliente personalizada](#listeners-in-a-custom-client-library). Isso é uma mudança no método antigo de ter [ouvintes na estrutura do conteúdo](#listenersinthecontentstructureclassicui).

#### Ouvintes em uma biblioteca personalizada do cliente {#listeners-in-a-custom-client-library}

Para inserir lógica em seu campo, você deve:

1. Tenha seu campo marcado com uma determinada classe CSS (a variável *gancho*).
1. Defina, na biblioteca do cliente, um ouvinte JS vinculado ao nome da classe CSS (isso garante que a lógica personalizada tenha escopo somente para o campo e não afete outros campos do mesmo tipo).

Para isso, você precisa saber sobre a biblioteca de widgets subjacente com a qual deseja interagir. Consulte a [Documentação da interface do usuário do Coral](https://helpx.adobe.com/br/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) para identificar a qual evento você deseja reagir. Isso é muito semelhante ao processo que você tinha que executar com ExtJS no passado: encontre a página de documentação de um determinado widget e verifique os detalhes de sua API de evento.

Para ver um exemplo, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * do [Amostra de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Ouvintes na estrutura do conteúdo {#listeners-in-the-content-structure}

Na interface clássica com ExtJS, era normal ter ouvintes de um determinado widget na estrutura de conteúdo. Alcançar o mesmo na interface habilitada para toque é diferente do código de ouvinte JS (ou qualquer código) não é mais definido no conteúdo.

A estrutura de conteúdo descreve a estrutura semântica; não deve (deve) implicar a natureza do widget subjacente. Não tendo o código JS na estrutura de conteúdo, você pode alterar os detalhes da implementação sem precisar alterar a estrutura do conteúdo. Em outras palavras, você pode alterar a biblioteca de widgets sem precisar tocar na estrutura do conteúdo.

#### Detectando Disponibilidade da Caixa de Diálogo {#dialog-ready}

Se você tiver um JavaScript personalizado que precisa ser executado somente quando a caixa de diálogo estiver disponível e pronta, você deve ouvir a `dialog-ready` evento.

Esse evento é acionado sempre que a caixa de diálogo é carregada (ou recarregada) e está pronta para uso, o que significa que sempre que há uma alteração (criar/atualizar) no DOM da caixa de diálogo.

`dialog-ready` pode ser usada para conectar o código personalizado JavaScript que executa personalizações nos campos dentro de uma caixa de diálogo ou tarefas semelhantes.

### Validação de campo {#field-validation}

#### Campo Obrigatório {#mandatory-field}

Para marcar um determinado campo como obrigatório, defina a seguinte propriedade no nó de conteúdo do campo:

* Nome: `required`
* Tipo: `Boolean`

Para ver um exemplo, consulte:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### Validação de campo (interface do usuário do Granite) {#field-validation-granite-ui}

A validação de campo na interface do usuário do Granite e nos Componentes da interface do usuário do Granite (equivalente aos widgets) é feita usando o `foundation-validation` API. [Consulte a `foundation-valdiation` Documentação do Granite para obter detalhes.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Para obter exemplos, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * do [Amostra de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Criação e configuração de uma caixa de diálogo de design {#creating-and-configuring-a-design-dialog}

A caixa de diálogo Design é fornecida quando um componente tem detalhes de design que podem ser editados em [Modo Design](/help/sites-authoring/default-components-designmode.md).

A definição é muito semelhante à de um [caixa de diálogo usada para editar conteúdo](#creating-a-new-dialog), com a diferença de que é definido como um nó:

* Nome do nó: `cq:design_dialog`
* Tipo: `nt:unstructured`

## Criação e configuração de um editor no local {#creating-and-configuring-an-inplace-editor}

Um editor local permite que o usuário edite conteúdo diretamente no fluxo de parágrafo, sem a necessidade de abrir uma caixa de diálogo. Por exemplo, os componentes padrão Texto e Título têm um editor local.

Um editor local não é necessário/significativo para cada tipo de componente.

Consulte [Extensão da criação de página - Adicionar novo editor local](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) para obter mais informações.

## Personalização da barra de ferramentas do componente {#customizing-the-component-toolbar}

O [Barra de ferramentas do componente](/help/sites-developing/touch-ui-structure.md#component-toolbar) dá ao usuário acesso a uma variedade de ações para o componente, como editar, configurar, copiar e excluir.

Consulte [Extensão da criação de páginas - Adicionar nova ação a uma barra de ferramentas de componentes](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) para obter mais informações.

## Configurar um componente para o painel de referências (emprestado/concedido) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Se o novo componente fizer referência ao conteúdo de outras páginas, você poderá considerar se deseja que afete a variável **Conteúdo emprestado** e **Conteúdo emprestado** seções da [**Referências**](/help/sites-authoring/basic-handling.md#references) Trilho.

O AEM pronto para uso verifica apenas o componente de referência. Para adicionar seu componente é necessário configurar o pacote OSGi **Configuração de Referência de Conteúdo de Criação do WCM**.

Crie uma nova entrada na definição, especificando seu componente, junto com a propriedade a ser verificada. Por exemplo:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>Ao trabalhar com o AEM há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas

## Ativar e adicionar seu componente ao sistema de parágrafos {#enabling-and-adding-your-component-to-the-paragraph-system}

Depois que o componente tiver sido desenvolvido, ele precisará ser ativado para uso em um sistema de parágrafo apropriado, para que possa ser usado nas páginas necessárias.

Isso pode ser feito:

* usar [Modo de design](/help/sites-authoring/default-components-designmode.md) ao editar uma página específica.
* [definição da `components` propriedade no sistema de parágrafo de um modelo](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## Configurar um sistema de parágrafo para que a arrastar um ativo crie uma instância de componente {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

O AEM oferece a possibilidade de configurar um sistema de parágrafo na página para que [uma instância do novo componente é criada automaticamente quando um usuário arrasta um ativo (apropriado) para uma instância dessa página](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (em vez de sempre ter que arrastar um componente vazio para a página).

Esse comportamento e o relacionamento ativo-componente necessário podem ser configurados:

1. Na definição de parágrafo do design da página. Por exemplo:

   * `/etc/designs/<myApp>/page/par`

   Crie um novo nó:

   * Nome: `cq:authoring`
   * Tipo: `nt:unstructured`


1. Em seguida, crie um novo nó para manter todos os mapeamentos de ativo para componente:

   * Nome: `assetToComponentMapping`
   * Tipo: `nt:unstructured`

1. Para cada mapeamento de ativo para componente, crie um nó:

   * Nome: texto; recomenda-se que o nome indique o tipo de ativo e componente relacionado; por exemplo, imagem
   * Tipo: `nt:unstructured`

   Cada um com as seguintes propriedades:

   * `assetGroup`:

      * Tipo: `String`
      * Valor: o grupo ao qual o ativo relacionado pertence; por exemplo, `media`
   * `assetMimetype`:

      * Tipo: `String`
      * Valor: o tipo MIME do ativo relacionado; por exemplo `image/*`
   * `droptarget`:

      * Tipo: `String`
      * Valor: o objetivo de queda; por exemplo, `image`
   * `resourceType`:

      * Tipo: `String`
      * Valor: o recurso componente relacionado; por exemplo, `foundation/components/image`
   * `type`:

      * Tipo: `String`
      * Valor: o tipo , por exemplo, `Images`






Por exemplo, consulte:

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-project-archetype no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>A criação automática de instâncias de componente agora pode ser configurada facilmente na interface do usuário ao usar [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) Modelos e modelos editáveis. Consulte [Criação de modelos de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) para obter mais informações sobre como definir quais componentes são associados automaticamente a determinados tipos de mídia.

## Uso da extensão AEM Brackets {#using-the-aem-brackets-extension}

O [Extensão de colchetes AEM](/help/sites-developing/aem-brackets.md) O fornece um fluxo de trabalho suave para editar componentes AEM e bibliotecas de clientes. É baseado no [Colchetes](https://brackets.io/) editor de código.

A extensão:

* Facilita a sincronização (sem necessidade de Maven ou File Vault) para ajudar a aumentar a eficiência do desenvolvedor e também ajuda desenvolvedores de front-end com conhecimento de AEM limitado a participar de projetos.
* Fornece alguns [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) suporte, a linguagem de modelo criada para simplificar o desenvolvimento de componentes e aumentar a segurança.

>[!NOTE]
>
>Brackets é o mecanismo recomendado para criar componentes. Substitui a funcionalidade CRXDE Lite - Criar componente, que foi criada para a interface clássica.

## Migração de um componente clássico {#migrating-from-a-classic-component}

Ao migrar um componente projetado para uso com a interface clássica para um componente que pode ser usado com a interface habilitada para toque (individual ou conjuntamente), os seguintes problemas devem ser considerados:

* HTL

   * Utilização de [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) não é obrigatório, mas se seu componente precisar de atualização, é o momento ideal para considerar [migração de JSP para HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Componentes

   * Migrar [ `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) código que usa funções específicas da interface clássica
   * Plug-in do RTE, para obter mais informações, consulte [Configuração do editor de rich text](/help/sites-administering/rich-text-editor.md).
   * [Migrar `cq:listener` código](#migrating-cq-listener-code) que usa funções específicas da interface clássica

* Caixas de diálogo

   * Você precisará criar uma nova caixa de diálogo para usar na interface do usuário habilitada para toque. No entanto, para fins de compatibilidade, a interface habilitada para toque pode usar a definição de uma caixa de diálogo da interface clássica, quando nenhuma caixa de diálogo tiver sido definida para a interface habilitada para toque.
   * O [Ferramentas de Modernização AEM](/help/sites-developing/modernization-tools.md) são fornecidas para ajudá-lo a estender os componentes existentes.
   * [Mapeamento de ExtJS para componentes da interface de usuário do Granite](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) O fornece uma visão geral conveniente dos xtypes e tipos de nó do ExtJS com seus tipos equivalentes de recursos da interface do usuário do Granite.
   * Personalização de campos, para obter mais informações, consulte a sessão AEM Gems em [Personalização de campos de diálogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
   * Migrar de vtypes para [Validação da interface do usuário do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Uso de ouvintes JS, para obter mais informações, consulte [Tratamento de eventos de campo](#handling-field-events) e a sessão AEM Gems em [Personalização de campos de diálogo](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).

### Migração do cq:listener Code {#migrating-cq-listener-code}

Se você estiver migrando um projeto que foi criado para a interface clássica, então a variável `cq:listener` código (e clientlibs relacionadas a componentes) pode usar funções específicas para a interface clássica (como `CQ.wcm.*`). Para a migração, você deve atualizar esse código usando os objetos/funções equivalentes na interface do usuário habilitada para toque.

Se o seu projeto estiver sendo totalmente migrado para a interface habilitada para toque, é necessário substituir esse código para usar os objetos e as funções relevantes para a interface do usuário habilitada para toque.

No entanto, se o projeto precisar atender tanto à interface clássica quanto à interface habilitada para toque durante o período de migração (o cenário normal), será necessário implementar um switch para diferenciar o código separado que faz referência aos objetos apropriados.

Esse mecanismo de switch pode ser implementado como:

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## Documentação do seu componente {#documenting-your-component}

Como desenvolvedor, você deseja obter acesso fácil à documentação do componente, para que possa entender rapidamente:

* Descrição
* Utilização prevista
* Estrutura e propriedades do conteúdo
* APIs e pontos de extensão expostos
* Etc.

Por isso, é muito fácil tornar qualquer marcação de documentação existente disponível no próprio componente.

Tudo o que você precisa fazer é colocar um `README.md` na estrutura do componente. Essa marcação será exibida no [console de componentes](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

O Markdown suportado é igual ao do [fragmentos de conteúdo](/help/assets/content-fragments/content-fragments-markdown.md).
