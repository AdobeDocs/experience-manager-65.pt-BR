---
title: Desenvolvimento de componentes do AEM
seo-title: Desenvolvimento de componentes do AEM
description: Os componentes do AEM são usados para manter, formatar e renderizar o conteúdo disponibilizado em suas páginas da Web.
seo-description: Os componentes do AEM são usados para manter, formatar e renderizar o conteúdo disponibilizado em suas páginas da Web.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '3452'
ht-degree: 1%

---


# Desenvolvimento de componentes do AEM{#developing-aem-components}

Os componentes do AEM são usados para manter, formatar e renderizar o conteúdo disponibilizado em suas páginas da Web.

* Ao [criar páginas](/help/sites-authoring/default-components.md), os componentes permitem que os autores editem e configurem o conteúdo.

   * Ao construir um site de [Comércio](/help/sites-administering/ecommerce.md) , os componentes podem, por exemplo, coletar e renderizar informações do catálogo.
See [Developing eCommerce](/help/sites-developing/ecommerce.md) for more information.

   * Ao construir um site [Communities](/help/communities/author-communities.md) , os componentes podem fornecer informações e coletar informações de seus visitantes.
See [Developing Communities](/help/communities/communities.md) for more information.

* Na instância de publicação, os componentes renderizam o conteúdo, apresentando-o conforme necessário aos visitantes do site.

>[!NOTE]
>
>Esta página é uma continuação do documento [AEM Components - The Basics](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>Os componentes abaixo `/libs/cq/gui/components/authoring/dialog` devem ser usados somente no Editor (caixas de diálogo de componentes em Criação). Se forem usados em outro lugar (como em uma caixa de diálogo do assistente, por exemplo), eles podem não se comportar como esperado.

## Amostras de código {#code-samples}

Esta página fornece a documentação de referência (ou links para a documentação de referência) necessária para desenvolver novos componentes para o AEM. Consulte [Desenvolvimento de componentes AEM - Exemplos](/help/sites-developing/developing-components-samples.md) de código para obter alguns exemplos práticos.

## Estrutura {#structure}

A estrutura básica de um componente é abordada na página Componentes do [AEM - Noções básicas](/help/sites-developing/components-basics.md#structure). Esse documento abrange as interfaces de usuário habilitadas para toque e clássica. Mesmo que você não precise usar as configurações clássicas em seu novo componente, pode ajudar a conhecê-las ao herdar dos componentes existentes.

## Extensão de componentes e caixas de diálogo existentes {#extending-existing-components-and-dialogs}

Dependendo do componente que você deseja implementar, talvez seja possível estender ou personalizar uma instância existente, em vez de definir e desenvolver toda a [estrutura](#structure) do zero.

Ao estender ou personalizar um componente ou uma caixa de diálogo existente, é possível copiar ou replicar toda a estrutura ou a estrutura necessária para a caixa de diálogo antes de fazer as alterações.

### Extensão de um componente existente {#extending-an-existing-component}

A extensão de um componente existente pode ser alcançada com a Hierarquia [de Tipo de](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) Recurso e os mecanismos de herança relacionados.

>[!NOTE]
>
>Os componentes também podem ser redefinidos com uma sobreposição baseada na lógica do caminho de pesquisa. No entanto, nesse caso, a fusão [de recursos de](/help/sites-developing/sling-resource-merger.md) Sling não será acionada e `/apps` deverá definir a cobertura total.

>[!NOTE]
>
>O componente [do fragmento do](/help/sites-developing/customizing-content-fragments.md) conteúdo também pode ser personalizado e estendido, embora a estrutura completa e os relacionamentos com os Ativos devam ser considerados.

### Personalizar uma caixa de diálogo de componente existente {#customizing-a-existing-component-dialog}

Também é possível substituir uma caixa de diálogo *de* componente usando a Fusão [de Recursos de](/help/sites-developing/sling-resource-merger.md) Sling e definindo a propriedade `sling:resourceSuperType`.

Isso significa que você só precisa redefinir as diferenças necessárias, em vez de redefinir toda a caixa de diálogo (usando `sling:resourceSuperType`). Esse método agora é recomendado para estender uma caixa de diálogo de componente

Consulte a [Sling Resource Fusão](/help/sites-developing/sling-resource-merger.md) para obter mais detalhes.

## Definição da marcação {#defining-the-markup}

Seu componente será renderizado com [HTML](https://www.w3schools.com/htmL/html_intro.asp). Seu componente precisa definir o HTML necessário para pegar o conteúdo necessário e, em seguida, renderizá-lo conforme necessário, nos ambientes de autor e publicação.

### Usar o idioma do modelo HTML {#using-the-html-template-language}

The [HTML Templating Language (HTL)](https://docs.adobe.com/content/help/br/experience-manager-htl/using/overview.html), introduced with AEM 6.0, takes the place of JSP (JavaServer Pages) as the preferred and recommended server-side template system for HTML. Para desenvolvedores da Web que precisam criar sites corporativos robustos, o HTL ajuda a aumentar a segurança e a eficiência do desenvolvimento.

>[!NOTE]
>
>Embora o HTL e o JSP possam ser usados para desenvolver componentes, ilustraremos o desenvolvimento com o HTL nesta página, já que é a linguagem de script recomendada para o AEM.

## Desenvolver a lógica do conteúdo {#developing-the-content-logic}

Essa lógica opcional seleciona e/ou calcula o conteúdo a ser renderizado. Ele é chamado das expressões HTL com o padrão Use-API apropriado.

O mecanismo para separar a lógica da aparência ajuda a esclarecer o que é chamado para uma determinada visualização. Também permite lógica diferente para visualizações diferentes do mesmo recurso.

### Uso do Java {#using-java}

[A HTL Java Use-API permite que um arquivo HTL acesse métodos auxiliares em uma classe](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html)Java personalizada. Isso permite usar o código Java para implementar a lógica de seleção e configuração do conteúdo do componente.

### Como usar o JavaScript {#using-javascript}

[A API de uso do JavaScript HTL permite que um arquivo HTL acesse o código auxiliar escrito em JavaScript](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html). Isso permite usar o código JavaScript para implementar a lógica de seleção e configuração do conteúdo do componente.

### Usando bibliotecas HTML do lado do cliente {#using-client-side-html-libraries}

Sites modernos dependem muito do processamento no cliente, conduzido por códigos complexos de JavaScript e CSS. Organizar e otimizar a entrega desse código pode ser um problema complicado.

Para ajudar a lidar com esse problema, o AEM fornece Pastas **de biblioteca do lado do** cliente, que permitem armazenar o código do lado do cliente no repositório, organizá-lo no categoria e definir quando e como cada categoria de código deve ser fornecida ao cliente. O sistema de biblioteca do lado do cliente cuida de produzir os links corretos em sua página da Web final para carregar o código correto.

Leia [Usando bibliotecas](/help/sites-developing/clientlibs.md) HTML do lado do cliente para obter mais informações.

## Configuração do comportamento de edição {#configuring-the-edit-behavior}

Você pode configurar o comportamento de edição de um componente incluindo atributos, como ações disponíveis para o componente, características do editor local e os ouvintes relacionados aos eventos no componente. A configuração é comum à interface habilitada para toque e clássica, embora com certas diferenças específicas.

O comportamento de [edição de um componente é configurado](/help/sites-developing/components-basics.md#edit-behavior) adicionando um `cq:editConfig` nó do tipo `cq:EditConfig` abaixo do nó do componente (do tipo `cq:Component`) e adicionando propriedades específicas e nós secundários.

## Configuração do comportamento de Pré-visualização {#configuring-the-preview-behavior}

O cookie [WCM Mode](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) é definido ao alternar para o modo **Pré-visualização** mesmo quando a página não é atualizada.

Para componentes com uma renderização que são sensíveis ao Modo WCM, eles precisam ser definidos para se atualizarem especificamente e, em seguida, dependem do valor do cookie.

>[!NOTE]
>
>Na interface habilitada para toque, somente os valores `EDIT` e `PREVIEW` são usados para o cookie do Modo [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) WCM.

## Criando e Configurando uma Caixa de Diálogo {#creating-and-configuring-a-dialog}

As caixas de diálogo são usadas para permitir que o autor interaja com o componente. O uso de uma caixa de diálogo permite que autores e/ou administradores editem conteúdo, configurem o componente ou definam parâmetros de design (usando uma caixa de diálogo [de](#creating-and-configuring-a-design-dialog)design)

### IU do Coral e IU do Granite {#coral-ui-and-granite-ui}

[A interface do usuário](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) do Coral e a interface do usuário [do](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) Granite definem a aparência moderna do AEM.

[A interface do usuário do Granite fornece uma grande variedade dos componentes básicos (widgets)](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) necessários para criar sua caixa de diálogo no ambiente de criação. Quando necessário, você pode estender essa seleção e [criar seu próprio widget](#creatinganewwidget).

Para obter mais informações sobre como desenvolver componentes usando os tipos de recursos Coral e Granite, consulte: [Criação de componentes de Experience Manager usando os tipos](https://helpx.adobe.com/experience-manager/using/aem64_coral_resourcetypes.html)de recursos Coral/Granite.

Para obter detalhes completos, consulte:

* Interface do usuário do Coral

   * Fornece uma interface de usuário consistente em todas as soluções de nuvem
   * [Conceitos da interface de usuário habilitada para toque do AEM - IU coral](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Guia da interface do usuário do Coral](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Interface do usuário Granite

   * Fornece marcação da interface do usuário Coral encapsulada em componentes Sling para criar consoles e diálogos da interface do usuário
   * [Conceitos da interface de usuário habilitada para toque do AEM - IU do Granite](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Documentação da interface do usuário do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>Devido à natureza dos componentes da interface do usuário Granite (e diferenças nos widgets ExtJS), há algumas diferenças entre a forma como os componentes interagem com a interface do usuário habilitada para toque e a interface do usuário [](/help/sites-developing/developing-components-classic.md)clássica.

### Creating a New Dialog {#creating-a-new-dialog}

Caixas de diálogo para a interface habilitada para toque:

* são nomeados `cq:dialog`.
* são definidos como um `nt:unstructured` nó com o conjunto de `sling:resourceType` propriedades.

* estão localizados sob o `cq:Component` nó e ao lado da definição do componente.
* são renderizados no lado do servidor (como componentes Sling), com base em sua estrutura de conteúdo e na `sling:resourceType` propriedade.
* use a estrutura da interface do usuário do Granite.
* contém uma estrutura de nó que descreve os campos na caixa de diálogo.

   * esses nós estão `nt:unstructured` com a propriedade necessária `sling:resourceType` .

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

A personalização de uma caixa de diálogo é semelhante ao desenvolvimento de um componente, já que a caixa de diálogo é um componente (isto é, uma marcação renderizada por um script de componente junto com o comportamento/estilo fornecido por uma biblioteca de cliente).

Para obter exemplos, consulte:

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>Se um componente não tiver uma caixa de diálogo definida para a interface habilitada para toque, a caixa de diálogo clássica da interface do usuário será usada como um fallback dentro de uma camada de compatibilidade. Para personalizar essa caixa de diálogo, é necessário personalizar a caixa de diálogo da interface clássica. Consulte Componentes do [AEM para a interface clássica](/help/sites-developing/developing-components-classic.md).

### Personalização de campos de diálogo {#customizing-dialog-fields}

>[!NOTE]
>
>Consulte:
>
>* a sessão AEM Gems em [Personalizar campos](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)de diálogo.
>* o código de amostra relacionado abordado em Amostra de [código - Como personalizar campos](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)de diálogo.

>



#### Creating a New Field {#creating-a-new-field}

Os widgets da interface habilitada para toque são implementados como componentes da interface de usuário Granite.

Para criar um novo widget para uso em uma caixa de diálogo de componente para a interface do usuário habilitada para toque, é necessário [criar um novo componente](/help/sites-developing/granite-ui-component.md)de campo da interface do usuário do Granite.

>[!NOTE]
>
>Para obter detalhes completos sobre a interface do usuário do Granite, consulte a documentação [da interface do usuário do](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)Granite.

Se você considerar sua caixa de diálogo como um container simples para um elemento de formulário, também poderá ver o conteúdo principal do conteúdo da caixa de diálogo como campos de formulário. A criação de um novo campo de formulário requer a criação de um tipo de recurso; isso equivale a criar um novo componente. Para ajudá-lo nessa tarefa, a interface do usuário do Granite oferta um componente de campo genérico do qual herdar (usando `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

Mais especificamente, a interface do usuário do Granite fornece uma variedade de componentes de campo adequados para uso em diálogos (ou, de modo mais geral, em [formulários](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Isso difere da interface clássica, onde os widgets são representados por `cq:Widgets` nós, cada um com um particular `xtype` para estabelecer a relação com seu widget ExtJS correspondente. Do ponto de vista da implementação, esses widgets foram renderizados no lado do cliente pela estrutura ExtJS.

Depois de criar seu tipo de recurso, você pode instanciar seu campo adicionando um novo nó na caixa de diálogo, com a propriedade `sling:resourceType` referente ao tipo de recurso que você acabou de apresentar.

#### Criar uma biblioteca de clientes para estilo e comportamento {#creating-a-client-library-for-style-and-behavior}

Se quiser definir o estilo e o comportamento do seu componente, você pode criar uma biblioteca [de](/help/sites-developing/clientlibs.md) cliente dedicada que defina seu CSS/LESS e JS personalizados.

Para que a biblioteca do cliente seja carregada exclusivamente para a caixa de diálogo do seu componente (isto é, ela não será carregada para outro componente), é necessário definir a propriedade `extraClientlibs`** **da sua caixa de diálogo com o nome da categoria da biblioteca do cliente que você acabou de criar. Isso é aconselhável se a biblioteca do cliente for muito grande e/ou seu campo for específico dessa caixa de diálogo e não for necessário em outras caixas de diálogo.

Para que a biblioteca do cliente seja carregada para todas as caixas de diálogo, defina a propriedade de categoria da biblioteca do cliente como `cq.authoring.dialog`. Esse é o nome da categoria da biblioteca do cliente que é incluída por padrão ao renderizar todas as caixas de diálogo. Você deseja fazer isso se a biblioteca do cliente for pequena e/ou seu campo for genérico e puder ser reutilizado em outras caixas de diálogo.

Para ver um exemplo, consulte:

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * fornecido pela amostra [de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Estender (Herdar de) um campo {#extending-inheriting-from-a-field}

Dependendo dos seus requisitos, você pode:

* Estender um determinado campo da interface do usuário do Granite por herança de componente ( `sling:resourceSuperType`)
* Estenda um determinado widget da biblioteca de widgets subjacente (no caso da interface do usuário Granite, esta é a interface do usuário Coral), seguindo a API da biblioteca de widgets (herança JS/CSS)

#### Acesso aos campos de diálogo {#access-to-dialog-fields}

Você também pode usar as condições de renderização ( `rendercondition`) para controlar quem tem acesso a guias/campos específicos na caixa de diálogo; por exemplo:

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Tratamento de Eventos de campo {#handling-field-events}

O método de manipulação de eventos em campos de diálogo agora é feito com [ouvintes em uma biblioteca](#listeners-in-a-custom-client-library)personalizada do cliente. Essa é uma alteração do método mais antigo de ter [ouvintes na estrutura](#listenersinthecontentstructureclassicui)do conteúdo.

#### Ouvintes em uma biblioteca de clientes personalizada {#listeners-in-a-custom-client-library}

Para injetar lógica no seu campo, deve:

1. Tenha seu campo marcado com uma determinada classe CSS (o *gancho*).
1. Defina, na biblioteca do cliente, um ouvinte JS vinculado ao nome da classe CSS (isso garante que a lógica personalizada tenha escopo somente para o campo e não afete outros campos do mesmo tipo).

Para isso, é necessário saber mais sobre a biblioteca de widgets subjacente com a qual você deseja interagir. Consulte a documentação [da interface do usuário do](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) Coral para identificar a qual evento você deseja reagir. Isso é muito semelhante ao processo que você tinha que executar com ExtJS no passado: localize a página de documentação de um determinado widget e verifique os detalhes de sua API de evento.

Para ver um exemplo, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * fornecido pela amostra [de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Ouvintes na estrutura do conteúdo {#listeners-in-the-content-structure}

Na interface clássica com ExtJS, era comum ter ouvintes para um determinado widget na estrutura de conteúdo. Alcançar o mesmo na interface habilitada para toque é diferente do código de ouvinte JS (ou qualquer código) não é mais definido no conteúdo.

A estrutura do conteúdo descreve a estrutura semântica; não deve (deve) implicar a natureza do widget subjacente. Ao não ter o código JS na estrutura de conteúdo, você pode alterar os detalhes da implementação sem precisar alterar a estrutura de conteúdo. Em outras palavras, é possível alterar a biblioteca de widgets sem precisar tocar na estrutura de conteúdo.

### Validação de campo {#field-validation}

#### Campo obrigatório {#mandatory-field}

Para marcar um determinado campo como obrigatório, defina a seguinte propriedade no nó de conteúdo do seu campo:

* Nome: `required`
* Tipo: `Boolean`

Para ver um exemplo, consulte:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### Validação de campo (IU Granite) {#field-validation-granite-ui}

A validação de campo na interface do usuário do Granite e nos Componentes da interface do usuário do Granite (equivalente aos widgets) é feita usando a `foundation-validation` API. [Consulte a documentação do `foundation-valdiation` Granite para obter detalhes.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Para obter exemplos, consulte:

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * fornecido pela amostra [de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Criando e Configurando uma Caixa de Diálogo de Design {#creating-and-configuring-a-design-dialog}

A caixa de diálogo Design é fornecida quando um componente tem detalhes de design que podem ser editados no Modo [de](/help/sites-authoring/default-components-designmode.md)Design.

A definição é muito semelhante à de uma [caixa de diálogo usada para editar conteúdo](#creating-a-new-dialog), com a diferença de que é definida como um nó:

* Node name: `cq:design_dialog`
* Tipo: `nt:unstructured`

## Criação e configuração de um editor local {#creating-and-configuring-an-inplace-editor}

Um editor local permite que o usuário edite o conteúdo diretamente no fluxo de parágrafo, sem a necessidade de abrir uma caixa de diálogo. Por exemplo, os componentes padrão Texto e Título têm um editor local.

Um editor local não é necessário/significativo para cada tipo de componente.

Consulte [Extensão da criação de páginas - Adicionar novo editor](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) local para obter mais informações.

## Personalização da barra de ferramentas do componente {#customizing-the-component-toolbar}

A barra de ferramentas [do](/help/sites-developing/touch-ui-structure.md#component-toolbar) componente fornece ao usuário acesso a uma variedade de ações para o componente, como editar, configurar, copiar e excluir.

Consulte [Extensão da criação de páginas - Adicionar nova ação a uma barra de ferramentas](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) de componentes para obter mais informações.

## Configuração de um componente para o painel Referências (Emprestado/Emprestado) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Se o novo componente fizer referência ao conteúdo de outras páginas, você poderá considerar se deseja que ele afete as seções Conteúdo **** emprestado e Conteúdo **** emprestado do painel [**Referências **](/help/sites-authoring/basic-handling.md#references).

O AEM predefinido verifica somente o componente de referência. Para adicionar seu componente, é necessário configurar a Configuração **de referência de conteúdo de criação do pacote OSGi** WCM.

Crie uma nova entrada na definição, especificando seu componente, junto com a propriedade a ser verificada. Por exemplo:

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>When working with AEM there are several methods of managing the configuration settings for such services. See [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

## Ativação e adição do componente ao sistema de parágrafo {#enabling-and-adding-your-component-to-the-paragraph-system}

Depois que o componente é desenvolvido, ele precisa ser habilitado para uso em um sistema de parágrafo apropriado, para que possa ser usado nas páginas necessárias.

Isso pode ser feito:

* uso do modo [](/help/sites-authoring/default-components-designmode.md) Design ao editar uma página específica.
* [definição da `components` propriedade no sistema de parágrafo de um modelo](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

O AEM oferta a possibilidade de configurar um sistema de parágrafo em sua página para que [uma instância do novo componente seja criada automaticamente quando um usuário arrasta um ativo (apropriado) para uma instância dessa página](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (em vez de sempre ter que arrastar um componente vazio para a página).

Este comportamento e a relação entre ativos e componentes necessária podem ser configurados:

1. Na definição de parágrafo do design da página. Por exemplo:

   * `/etc/designs/<myApp>/page/par`

   Criar um novo nó:

   * Nome: `cq:authoring`
   * Tipo: `nt:unstructured`


1. Sob isso, crie um novo nó para manter todos os mapeamentos ativo-componente:

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
      * Valor: público alvo; por exemplo, `image`
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

* [Abrir projeto aem-project-archetype no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>A criação automática de instâncias de componentes agora pode ser configurada facilmente na interface do usuário ao usar os Componentes [](https://docs.adobe.com/content/help/br/experience-manager-core-components/using/introduction.html) principais e os Modelos editáveis. Consulte [Criação de modelos](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) de página para obter mais informações sobre como definir quais componentes são associados automaticamente a determinados tipos de mídia.

## Uso da extensão de colchetes AEM {#using-the-aem-brackets-extension}

A extensão [de suportes](/help/sites-developing/aem-brackets.md) AEM fornece um fluxo de trabalho suave para editar componentes AEM e bibliotecas clientes. Ele é baseado no editor de código [do Brackets](https://brackets.io/) .

A extensão:

* Facilita a sincronização (sem necessidade de Maven ou File Vault) para ajudar a aumentar a eficiência do desenvolvedor e também ajuda os desenvolvedores de front-end com conhecimento limitado de AEM a participar de projetos.
* Fornece suporte a [HTL](https://docs.adobe.com/content/help/br/experience-manager-htl/using/overview.html) , a linguagem de modelo projetada para simplificar o desenvolvimento de componentes e aumentar a segurança.

>[!NOTE]
>
>Os suportes são o mecanismo recomendado para a criação de componentes. Substitui a funcionalidade CRXDE Lite - Criar componente, projetada para a interface clássica.

## Migração de um componente clássico {#migrating-from-a-classic-component}

Ao migrar um componente projetado para uso com a interface clássica para um componente que pode ser usado com a interface habilitada para toque (individual ou conjuntamente), os seguintes problemas devem ser considerados:

* HTL

   * O uso de [HTL](https://docs.adobe.com/content/help/br/experience-manager-htl/using/overview.html) não é obrigatório, mas se o componente precisar de atualização, então é o momento ideal para [migrar do JSP para o HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Componentes

   * Migrar [ `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) código que usa funções específicas de interface clássica
   * Plug-in RTE, para obter mais informações, consulte [Configuração do Editor](/help/sites-administering/rich-text-editor.md)de Rich Text.
   * [Migre o `cq:listener` código](#migrating-cq-listener-code) que usa funções específicas para a interface clássica

* Caixas de diálogo

   * Será necessário criar uma nova caixa de diálogo para usar na interface habilitada para toque. No entanto, para fins de compatibilidade, a interface habilitada para toque pode usar a definição de uma caixa de diálogo de interface clássica, quando nenhuma caixa de diálogo tiver sido definida para a interface habilitada para toque.
   * A Ferramenta [de conversão de](/help/sites-developing/dialog-conversion.md) caixa de diálogo é fornecida para ajudá-lo a estender os componentes existentes.
   * [O mapeamento de componentes](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) ExtJS para a interface de usuário Granite fornece uma visão geral conveniente dos tipos de nó e xtypes ExtJS com os tipos de recursos equivalentes da interface de usuário Granite.
   * Para obter mais informações, consulte a sessão Gems do AEM sobre como [personalizar campos](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)de diálogo.
   * Migrar de vtypes para validação de interface do usuário [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Usando ouvintes JS, para obter mais informações, consulte [Manuseio de Eventos](#handling-field-events) de campo e a sessão Gems AEM sobre [personalização de campos](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)de diálogo.

### Migração de cq:código do listener {#migrating-cq-listener-code}

Se você estiver migrando um projeto projetado para a interface clássica, o `cq:listener` código (e clientlibs relacionados a componentes) poderá usar funções específicas para a interface clássica (como `CQ.wcm.*`). Para a migração, você deve atualizar esse código usando os objetos/funções equivalentes na interface habilitada para toque.

Se o seu projeto estiver sendo completamente migrado para a interface habilitada para toque, é necessário substituir esse código para usar os objetos e as funções relevantes para a interface habilitada para toque.

No entanto, se o projeto precisar atender tanto à interface clássica quanto à interface habilitada para toque durante o período de migração (o cenário normal), será necessário implementar uma opção para diferenciar o código separado que faz referência aos objetos apropriados.

Este mecanismo de comutação pode ser implementado como:

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## Documentação do seu componente {#documenting-your-component}

Como desenvolvedor, você quer acesso fácil à documentação do componente para que você possa entender rapidamente:

* Descrição
* Utilização prevista
* Estrutura e propriedades do conteúdo
* APIs e pontos de extensão expostos
* Etc.

Por essa razão, é muito fácil disponibilizar qualquer marcação de documentação existente no próprio componente.

Tudo o que você precisa fazer é colocar um `README.md` arquivo na estrutura do componente. Essa marcação será exibida no console [do](/help/sites-authoring/default-components-console.md)componente.

![chlimage_1-7](assets/chlimage_1-7.png)

A marcação suportada é a mesma para fragmentos [de](/help/assets/content-fragments/content-fragments-markdown.md)conteúdo.
