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
source-git-commit: 0985ba24f7430381fccc40faf3a316d3abd85a30
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 69%

---


# Sistema de estilos{#style-system}

O Sistema de estilos permite ao autor do modelo definir classes de estilo na política de conteúdo de um componente, de modo que o autor de conteúdo possa selecioná-los ao editar o componente em uma página. Esses estilos podem ser variações visuais alternativas de um componente, tornando o componente mais flexível.

Isso elimina a necessidade de desenvolver um componente personalizado para cada estilo ou personalizar a caixa de diálogo do componente para permitir essa funcionalidade de estilo. Isso resulta em componentes mais reutilizáveis, que podem ser adaptados de forma rápida e fácil às necessidades dos autores de conteúdo, sem exigir uma implantação de back-end no AEM.

## Caso de uso   {#use-case}

Os autores de modelos precisam ter a capacidade de configurar a forma como os componentes funcionam para os autores de conteúdo, bem como configurar algumas variações visuais alternativas de um componente.

Da mesma forma, os autores de conteúdo precisam ter a capacidade de estruturar e organizar o conteúdo, além de selecionar a maneira como ele é apresentado visualmente.

O Sistema de estilo fornece uma solução unificada para os requisitos do autor do modelo e do autor do conteúdo:

* Os autores de modelos podem definir classes de estilo na política de conteúdo de componentes.
* Os autores de conteúdo podem selecionar essas classes em uma lista suspensa ao editar o componente em uma página para aplicar os estilos correspondentes.

A classe de estilo é inserida no elemento wrapper de decoração do componente para que o desenvolvedor do componente não precise se preocupar com a manipulação de estilos além de fornecer as regras de CSS.

## Visão geral {#overview}

O uso do Sistema de estilo geralmente assume o seguinte formato.

1. O web designer cria diferentes variações visuais de um componente.

1. O desenvolvedor de HTML recebe a saída dos componentes em HTML e as variações visuais desejadas para implementar.

1. O desenvolvedor de HTML define as classes CSS que correspondem a cada variação visual e que devem ser inseridas no elemento que envolve os componentes.

1. O desenvolvedor de HTML implementa o código CSS correspondente (e, opcionalmente, o código JS) para cada uma das variações visuais, de modo a serem exibidas conforme a definição.

1. O desenvolvedor do AEM coloca o CSS fornecido (e o JS opcional) em uma [Biblioteca do cliente](/help/sites-developing/clientlibs.md) e a implanta.

1. O desenvolvedor do AEM ou o autor do modelo define os modelos de página e edita a política de cada componente estilizado, adicionando as classes CSS definidas, fornecendo nomes amigáveis a cada estilo e indicando quais estilos podem ser combinados.

1. O autor da página do AEM pode escolher os estilos criados no editor de páginas no menu de estilo da barra de ferramentas do componente.

Observe que somente as três últimas etapas são realmente realizadas no AEM. Isso significa que todo o desenvolvimento dos códigos CSS e Javascript necessários pode ser feito sem o AEM.

A aplicação real dos estilos requer apenas a implantação no AEM e a seleção nos componentes dos modelos desejados.

O diagrama a seguir ilustra a arquitetura do Sistema de estilo.

![aem-style-system](assets/aem-style-system.png)

## Uso {#use}

Para demonstrar o recurso, usaremos a implementação do [WKND](https://docs.adobe.com/content/help/br/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)do componente [de](https://www.adobe.com/go/aem_cmp_title_v2) título do componente principal como exemplo.

The following sections [As a Content Author](#as-a-content-author) and [As a Template Author](#as-a-template-author) describe how to test the functionality of the Style System using the Style System of WKND.

Se você quiser usar o Sistema de estilo para seus próprios componentes, faça o seguinte:

1. Instale o CSS como bibliotecas de cliente, conforme descrito na seção [Visão geral](#overview).
1. Configure as classes CSS que deseja disponibilizar para os autores de conteúdo, conforme descrito na seção [Como um autor de modelo](#as-a-template-author).
1. Os autores de conteúdo podem usar os estilos conforme descrito na seção [Como um autor de conteúdo](#as-a-content-author).

### Como um autor de conteúdo   {#as-a-content-author}

1. Após instalar o projeto WKND, navegue até o home page mestre do idioma inglês da WKND em `http://<host>:<port>/sites.html/content/wknd/language-masters/en` e edite a página.
1. Selecione um componente de **Título** mais abaixo da página

   ![Sistema de estilo do autor](assets/style-system-author.png)

1. Toque ou clique no botão **Estilos** na barra de ferramentas do componente **Lista** para abrir o menu de estilos e alterar a aparência do componente.

   ![Seleção de estilos](assets/style-system-author2.png)

   >[!NOTE]
   >
   >Neste exemplo, os estilos de **Cores** (**Preto**, **Branco** e **Cinza**) são mutuamente exclusivos, enquanto as opções de **Estilo**************(Sublinhado, , SpacingMini) podem ser combinadas. Isso pode ser [configurado no modelo como o autor do modelo](#as-a-template-author).

### Como um autor de modelo   {#as-a-template-author}

1. While editing WKND&#39;s English language master home page at `http://<host>:<port>/sites.html/content/wknd/language-masters/en`, edit the template of the page via **Page Information -> Edit Template**.

   ![Editar modelo](assets/style-system-edit-template.png)

1. Edit the policy of the **Title** component by tapping or clicking the **Policy** button of the component.

   ![Editar política](assets/style-system-edit-policy.png)

1. Na guia Estilos das propriedades, é possível ver como os estilos foram configurados.

   ![Editar propriedades](assets/style-system-properties.png)

   * **Nome do grupo:** os estilos podem ser agrupados no menu de estilos que o autor de conteúdo verá ao configurar o estilo do componente.
   * **Estilos podem ser combinados:** permite a seleção simultânea de vários estilos desse grupo.
   * **Nome do estilo:** a descrição do estilo que será exibida para o autor do conteúdo ao configurar o estilo do componente.
   * **Classes de CSS:** o nome real da classe CSS associada ao estilo.
   Use as alças de arrastar para organizar a ordem dos grupos e dos estilos nos grupos. Use os ícones Adicionar ou Excluir para adicionar ou remover grupos ou estilos nos grupos.

>[!CAUTION]
>
>The CSS classes (as well as any necessary Javascript) configured as style properties of a component&#39;s policy must be deployed as [Client Libraries](/help/sites-developing/clientlibs.md) in order to work.

## Configurar {#setup}

Os Componentes principais versão 2 e posteriores estão habilitados para se beneficiarem do Sistema de estilo e não exigem configuração adicional.

As etapas a seguir são necessárias apenas para ativar o Sistema de estilo para seus próprios componentes personalizados ou para [ativar a guia Estilos opcional na caixa de diálogo Editar.](#enable-styles-tab-edit)

### Ativar guia Estilo na caixa de diálogo Design {#enable-styles-tab-design}

Para que um componente funcione com o Sistema de estilo do AEM e mostre a guia de estilo em sua caixa de diálogo de design, o desenvolvedor do componente deve incluir a guia de estilo com as seguintes configurações no componente:

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

Com o componente configurado, os estilos configurados pelos autores da página serão inseridos automaticamente pelo AEM no elemento de decoração que o AEM adiciona ao redor de cada componente editável. O componente não precisa fazer mais nada para que isso ocorra.

### Ativar guia Estilos na caixa de diálogo Editar {#enable-styles-tab-edit}

A partir do AEM versão 6.5.3.0, uma guia Estilos opcional na caixa de diálogo Editar está disponível. Diferentemente da guia Caixa de diálogo de design, a guia na caixa de diálogo Editar não é essencial para o funcionamento do Sistema de estilo, mas é uma interface alternativa opcional para um autor de conteúdo definir estilos.

A guia da caixa de diálogo de edição pode ser incluída de maneira semelhante à guia da caixa de diálogo de design:

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>
>A guia Estilos na caixa de diálogo Editar não está ativada por padrão.

### Estilos com nomes de elemento   {#styles-with-element-names}

Um desenvolvedor também pode configurar uma lista de nomes de elementos permitidos para os estilos no componente por meio da propriedade de matriz da sequência `cq:styleElements`. Na guia Estilos da política na caixa de diálogo de design, o autor do modelo também pode escolher um nome de elemento para definir cada estilo. Isso definirá o nome de elemento do wrapper.

Essa propriedade é definida no nó `cq:Component`. Por exemplo:

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>Evite definir nomes de elemento para os estilos que podem ser combinados. Quando vários nomes de elemento são definidos, a ordem de prioridade é:
>
>1. HTL tem precedência sobre tudo: `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. Entre os vários estilos ativos, o primeiro estilo na lista de estilos configurados na política do componente é aplicado.
>1. Por fim, a `cq:tagName`/ `cq:htmlTag` do componente será considerada como um valor de fallback.
>



Essa capacidade de definir nomes de estilo é útil para componentes muito genéricos, como o Contêiner de layout ou o componente de Fragmento do conteúdo, para oferecer-lhes significado adicional.

Por exemplo, permite que um Contêiner de layout receba uma semântica como `<main>`, `<aside>`, `<nav>`, etc.
