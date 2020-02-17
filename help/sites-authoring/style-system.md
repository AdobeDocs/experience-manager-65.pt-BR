---
title: Sistema de estilos
seo-title: Sistema de estilos
description: O Sistema de estilos permite ao autor do modelo definir classes de estilo na política de conteúdo de um componente, de modo que o autor de conteúdo possa selecioná-los ao editar o componente em uma página. Esses estilos podem ser variações visuais alternativas de um componente, tornando-o mais flexível.
seo-description: O Sistema de estilos permite ao autor do modelo definir classes de estilo na política de conteúdo de um componente, de modo que o autor de conteúdo possa selecioná-los ao editar o componente em uma página. Esses estilos podem ser variações visuais alternativas de um componente, tornando-o mais flexível.
uuid: 0d857650-8738-49e6-b431-f69c088be74f
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: e3ccddb6-be5e-4e5f-a017-0eed263555ce
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Sistema de estilos{#style-system}

O Sistema de estilos permite ao autor do modelo definir classes de estilo na política de conteúdo de um componente, de modo que o autor de conteúdo possa selecioná-los ao editar o componente em uma página. Esses estilos podem ser variações visuais alternativas de um componente, tornando-o mais flexível.

Isso elimina a necessidade de desenvolver um componente personalizado para cada estilo ou personalizar a caixa de diálogo do componente para permitir essa funcionalidade de estilo. Isso resulta em componentes mais reutilizáveis, que podem ser adaptados de forma rápida e fácil às necessidades dos autores de conteúdo, sem exigir uma implantação de back-end no AEM.

## Caso de uso {#use-case}

Os autores de modelos precisam ter a capacidade de configurar a forma como os componentes funcionam para os autores de conteúdo, bem como configurar algumas variações visuais alternativas de um componente.

Da mesma forma, os autores de conteúdo precisam ter a capacidade de estruturar e organizar o conteúdo, além de selecionar a maneira como ele é apresentado visualmente.

O sistema de estilos fornece uma solução unificada para os requisitos do autor de modelo e do autor de conteúdo:

* Os autores de modelos podem definir classes de estilo na política de conteúdo de componentes.
* Os autores de conteúdo podem selecionar essas classes em uma lista suspensa ao editar o componente em uma página para aplicar os estilos correspondentes.

A classe de estilo é inserida no elemento wrapper de decoração do componente para que o desenvolvedor do componente não precise se preocupar com a manipulação de estilos além de fornecer as regras de CSS.

## Visão geral {#overview}

O uso do sistema de estilos geralmente funciona da seguinte maneira.

1. O web designer cria diferentes variações visuais de um componente.

1. O desenvolvedor de HTML recebe a saída dos componentes em HTML e as variações visuais desejadas para implementar.

1. O desenvolvedor HTML define as classes CSS que correspondem a cada variação visual e que devem ser inseridas no elemento que envolve os componentes.

1. O desenvolvedor de HTML implementa o código CSS correspondente (e opcionalmente o código JS) para cada uma das variações visuais para que elas pareçam definidas.

1. O desenvolvedor do AEM coloca o CSS fornecido (e o JS opcional) em uma [Biblioteca do cliente](/help/sites-developing/clientlibs.md) e a implanta.

1. O desenvolvedor ou autor do modelo do AEM configura os modelos de página e edita a política de cada componente estilizado, adicionando as classes CSS definidas, dando nomes amigáveis a cada estilo e indicando quais estilos podem ser combinados.

1. O autor da página do AEM pode escolher os estilos criados no editor de páginas no menu de estilo da barra de ferramentas do componente.

Observe que somente as três últimas etapas são realmente realizadas no AEM. Isso significa que todo o desenvolvimento dos códigos CSS e Javascript necessários pode ser feito sem o AEM.

A aplicação real dos estilos requer apenas a implantação no AEM e a seleção nos componentes dos modelos desejados.

O diagrama a seguir ilustra a arquitetura do sistema de estilos.

![aem-style-system](assets/aem-style-system.png)

## Use {#use}

Para demonstrar o recurso, estilos precisam ser criados para um componente. Usando a implementação do [We.Retail](/help/sites-developing/we-retail.md) do [componente de lista](https://helpx.adobe.com/experience-manager/core-components/using/list.html) do componente principal como base, é possível instalar o pacote anexado que contém os estilos para explorar a funcionalidade do recurso.

Download do pacote de demonstração do sistema [style](assets/package_-_style_systemdemo.zip)

>[!NOTE]
>
>O pacote de demonstração tem o objetivo de mostrar como o sistema de estilos pode ser usado por autores, mas não é uma referência da melhor forma de implementá-lo.
>
>Esse pacote será necessário somente até que o We.Retail forneça um exemplo integrado de implementação e melhores práticas.

As seções [Como um autor de conteúdo](/help/sites-authoring/style-system.md#as-a-content-author) e [Como um autor de modelo](/help/sites-authoring/style-system.md#as-a-template-author) descrevem como testar a funcionalidade do sistema de estilos usando o pacote de demonstração do sistema de estilos no We.Retail.

Se você desejar usar o sistema de estilos em seus próprios componentes, faça o seguinte:

1. Instale o CSS como bibliotecas de cliente, conforme descrito na seção [Visão geral](/help/sites-authoring/style-system.md#overview).
1. Configure as classes CSS que deseja disponibilizar para os autores de conteúdo, conforme descrito na seção [Como um autor de modelo](/help/sites-authoring/style-system.md#as-a-template-author).
1. Os autores de conteúdo podem usar os estilos conforme descrito na seção [Como um autor de conteúdo](/help/sites-authoring/style-system.md#as-a-content-author).

### Como um autor de conteúdo {#as-a-content-author}

1. After installing the style system demo package, navigate to We.Retail&#39;s English language master home page at `http://localhost:4502/sites.html/content/we-retail/language-masters/en` and edit the page.
1. Selecione o componente **Lista** na parte inferior ou superior do parsys. Do not confuse it with the **Articles List** component.

   ![screen_shot_2017-11-15at162032](assets/screen_shot_2017-11-15at162032.png)

1. Toque ou clique no botão **Estilos** na barra de ferramentas do componente **Lista** para abrir o menu de estilos e alterar a aparência do componente.

   ![screen_shot_2017-11-15at162358](assets/screen_shot_2017-11-15at162358.png)

   >[!NOTE]
   >
   >In this example, the **Layout** styles (**Block** and **Grid**) are mutually exclusive, while the **Display** options (**Image** or **Date**) can be combined. Isso pode [ser configurado no modelo como autor do modelo](/help/sites-authoring/style-system.md#as-a-template-author).

### Como um autor de modelo {#as-a-template-author}

1. While editing We.Retail&#39;s English language master home page at `http://localhost:4502/sites.html/content/we-retail/language-masters/en`, edit the template of the page via **Page Information -> Edit Template**.

   ![screen_shot_2017-11-15at162922](assets/screen_shot_2017-11-15at162922.png)

1. Edite a política do componente de **Lista** tocando ou clicando no botão **Política** do componente. Não confunda isso com o componente **Lista de artigos**.

   ![screen_shot_2017-11-15at163133](assets/screen_shot_2017-11-15at163133.png)

1. Na guia Estilos das propriedades, é possível ver como os estilos foram configurados.

   ![screen_shot_2017-12-15at101404](assets/screen_shot_2017-12-15at101404.png)

   * **Nome do grupo:** os estilos podem ser agrupados no menu de estilos que o autor de conteúdo verá ao configurar o estilo do componente.
   * **Estilos podem ser combinados:** permite a seleção simultânea de vários estilos desse grupo.
   * **Nome do estilo:** a descrição do estilo que será exibida para o autor do conteúdo ao configurar o estilo do componente.
   * **Classes de CSS:** o nome real da classe CSS associada ao estilo.
   Use as alças de arrastar para organizar a ordem dos grupos e dos estilos nos grupos. Use os ícones Adicionar ou Excluir para adicionar ou remover grupos ou estilos nos grupos.

>[!CAUTION]
>
>The CSS classes (as well as any necessary Javascript) configured as style properties of a component&#39;s policy must be deployed as [Client Libraries](/help/sites-developing/clientlibs.md) in order to work.

## Configurar {#setup}

>[!NOTE]
>
>A versão 2 dos componentes principais é completamente habilitada para usufruir do sistema de estilos e não exige configuração adicional.
>
>Siga as próximas etapas para habilitar o sistema de estilos para seus próprios componentes personalizados ou para estender os componentes principais da versão 1 para usar o recurso.

Para que um componente funcione com o sistema de estilos do AEM e mostre a guia Estilo na caixa de diálogo de design, o desenvolvedor do componente deve incluir a guia do produto com as seguintes configurações no componente:

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

Com o componente configurado, os estilos configurados pelos autores da página serão inseridos automaticamente pelo AEM no elemento de decoração que o AEM adiciona ao redor de cada componente editável. O componente não precisa fazer mais nada para que isso ocorra.

### Estilos com nomes de elemento {#styles-with-element-names}

Um desenvolvedor também pode configurar uma lista de nomes de elementos permitidos para os estilos no componente por meio da propriedade de matriz da sequência `cq:styleElements`. Na guia Estilos da política na caixa de diálogo de design, o autor do modelo também pode escolher um nome de elemento para definir cada estilo. Isso definirá o nome de elemento do wrapper.

This property is set on the `cq:Component` node. Por exemplo:

* `/apps/weretail/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>Evite definir nomes de elemento para os estilos que podem ser combinados. Quando vários nomes de elemento são definidos, a ordem de prioridade é:
>
>1. HTL tem precedência sobre tudo: `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. Entre os vários estilos ativos, o primeiro estilo na lista de estilos configurados na política do componente é aplicado.
>1. Finally, the component&#39;s `cq:htmlTag`/ `cq:tagName` will be considered as a fallback value.
>



Essa capacidade de definir nomes de estilo é útil para componentes muito genéricos, como o Contêiner de layout ou o componente de Fragmento do conteúdo, para oferecer-lhes significado adicional.

For instance it allows a Layout Container to be given semantics like `<main>`, `<aside>`, `<nav>`, etc.
