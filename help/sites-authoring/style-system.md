---
title: Sistema de estilos
seo-title: Style System
description: O sistema de estilos permite ao autor do modelo definir classes de estilo na política de conteúdo de um componente para que autores de conteúdo possam selecioná-las ao editarem o componente em uma página. Esses estilos podem ser variações visuais alternativas de um componente, tornando-o mais flexível.
seo-description: The Style System allows a template author to define style classes in the content policy of a component so that a content author is able to select them when editing the component on a page. These styles can be alternative visual variations of a component, making it more flexible.
uuid: 0d857650-8738-49e6-b431-f69c088be74f
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: e3ccddb6-be5e-4e5f-a017-0eed263555ce
exl-id: 1772368a-f5c9-440c-a92a-0f1d34cc4bf8
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 98%

---

# Sistema de estilos{#style-system}

O sistema de estilos permite ao autor do modelo definir classes de estilo na política de conteúdo de um componente para que autores de conteúdo possam selecioná-las ao editarem o componente em uma página. Esses estilos podem ser variações visuais alternativas de um componente, tornando esse componente mais flexível.

Isso elimina a necessidade de desenvolver um componente personalizado para cada estilo ou personalizar a caixa de diálogo do componente para permitir essa funcionalidade de estilo. Isso resulta em componentes mais reutilizáveis, que podem ser adaptados de forma rápida e fácil às necessidades dos autores de conteúdo, sem exigir uma implantação de back-end no AEM.

## Caso de uso  {#use-case}

Os autores de modelos precisam ter a capacidade de configurar a forma como os componentes funcionam para os autores de conteúdo, bem como configurar algumas variações visuais alternativas de um componente.

Da mesma forma, os autores de conteúdo precisam ter a capacidade de estruturar e organizar o conteúdo, além de selecionar a maneira como ele é apresentado visualmente.

O Sistema de estilos fornece uma solução unificada para os requisitos do autor de modelo e do autor de conteúdo:

* Os autores de modelos podem definir classes de estilo na política de conteúdo de componentes.
* Os autores de conteúdo podem selecionar essas classes em uma lista suspensa ao editar o componente em uma página para aplicar os estilos correspondentes.

A classe de estilo é inserida no elemento wrapper de decoração do componente para que o desenvolvedor do componente não precise se preocupar com a manipulação de estilos além de fornecer as regras de CSS.

## Visão geral {#overview}

O uso do Sistema de estilos geralmente funciona da seguinte maneira.

1. O web designer cria diferentes variações visuais de um componente.

1. O desenvolvedor de HTML recebe a saída dos componentes em HTML e as variações visuais desejadas para implementar.

1. O desenvolvedor de HTML define as classes CSS que correspondem a cada variação visual e que devem ser inseridas no elemento que envolve os componentes.

1. O desenvolvedor de HTML implementa o código CSS correspondente (e, opcionalmente, o código JS) para cada uma das variações visuais, de modo a serem exibidas conforme a definição.

1. O desenvolvedor do AEM coloca o CSS fornecido (e o JS opcional) em uma [Biblioteca do cliente](/help/sites-developing/clientlibs.md) e a implanta.

1. O desenvolvedor do AEM ou o autor do modelo define os modelos de página e edita a política de cada componente estilizado, adicionando as classes CSS definidas, fornecendo nomes amigáveis a cada estilo e indicando quais estilos podem ser combinados.

1. O autor da página do AEM pode escolher os estilos criados no editor de páginas no menu de estilo da barra de ferramentas do componente.

Observe que somente as três últimas etapas são realmente realizadas no AEM. Isso significa que todo o desenvolvimento dos códigos CSS e Javascript necessários pode ser feito sem o AEM.

A aplicação real dos estilos requer apenas a implantação no AEM e a seleção nos componentes dos modelos desejados.

O diagrama a seguir ilustra a arquitetura do Sistema de estilos.

![aem-style-system](assets/aem-style-system.png)

## Utilização {#use}

Para demonstrar o recurso, usaremos como exemplo a implementação da [WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR) do [componente de título](https://www.adobe.com/go/aem_cmp_title_v2_br) do componente principal.

As seções a seguir, [Como um autor de conteúdo](#as-a-content-author) e [Como um autor de modelo](#as-a-template-author) descrevem como testar a funcionalidade do Sistema de estilos usando o Sistema de estilos da WKND.

Se você desejar usar o Sistema de estilos em seus próprios componentes, faça o seguinte:

1. Instale o CSS como bibliotecas de cliente, conforme descrito na seção [Visão geral](#overview).
1. Configure as classes CSS que deseja disponibilizar para os autores de conteúdo, conforme descrito na seção [Como um autor de modelo](#as-a-template-author).
1. Os autores de conteúdo podem usar os estilos conforme descrito na seção [Como um autor de conteúdo](#as-a-content-author).

### Como autor de conteúdo  {#as-a-content-author}

1. Depois de instalar o projeto WKND, navegue até a página inicial principal no idioma inglês da WKND em `http://<host>:<port>/sites.html/content/wknd/language-masters/en` e edite a página.
1. Selecione um componente de **Título** mais abaixo da página

   ![Sistema de estilos do autor](assets/style-system-author.png)

1. Toque ou clique no botão **Estilos** na barra de ferramentas do componente **Lista** para abrir o menu de estilos e alterar a aparência do componente.

   ![Seleção de estilos](assets/style-system-author2.png)

   >[!NOTE]
   >
   >Neste exemplo, os estilos de **Cores** (**Preto**, **Branco** e **Cinza**) são mutuamente exclusivos, enquanto as opções de **Estilo** (**Sublinhado**, **Alinhar à direita** e **Miniespaçamento**) podem ser combinadas. Isso pode ser [configurado no modelo como o autor do modelo](#as-a-template-author).

### Como autor de modelo  {#as-a-template-author}

1. Ao editar a página inicial mestre em inglês do WKND em `http://<host>:<port>/sites.html/content/wknd/language-masters/en`, edite o modelo da página em **Informações da página -> Editar modelo**.

   ![Editar modelo](assets/style-system-edit-template.png)

1. Edite a política do componente de **Título** tocando ou clicando no botão **Política** do componente.

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
>As classes CSS (bem como qualquer Javascript necessário) configuradas como propriedades de estilo da política de um componente devem ser implantadas como [Bibliotecas do cliente](/help/sites-developing/clientlibs.md) para funcionarem.

## Configurar {#setup}

Os Componentes principais versão 2 e posteriores estão habilitados para se beneficiarem do Sistema de estilos e não exigem configuração adicional.

As etapas a seguir são necessárias apenas para ativar o Sistema de estilos para os seus próprios componentes personalizados ou para [habilitar a guia Estilos opcional na caixa de diálogo Editar.](#enable-styles-tab-edit)

### Habilitar guia Estilo na caixa de diálogo Design {#enable-styles-tab-design}

Para que um componente funcione com o Sistema de estilos do AEM e mostre a guia Estilo na caixa de diálogo Design, o desenvolvedor do componente deve incluir essa guia com as seguintes configurações no componente:

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

Com o componente configurado, os estilos configurados pelos autores da página serão inseridos automaticamente pelo AEM no elemento de decoração que o AEM adiciona ao redor de cada componente editável. O componente não precisa fazer mais nada para que isso ocorra.

### Habilitar a guia Estilos na caixa de diálogo Editar {#enable-styles-tab-edit}

Desde AEM versão 6.5.3.0, uma guia Estilos opcional na caixa de diálogo Editar agora está disponível. Diferentemente da guia da caixa de diálogo Design, a guia na caixa de diálogo Editar não é essencial para o funcionamento do Sistema de estilos, mas é uma interface alternativa opcional para um autor de conteúdo definir estilos.

A guia da caixa de diálogo Editar pode ser incluída de maneira semelhante na guia da caixa de diálogo Design:

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>
>A guia Estilos na caixa de diálogo Editar não está habilitada por padrão.

### Estilos com nomes de elemento  {#styles-with-element-names}

Um desenvolvedor também pode configurar uma lista de nomes de elementos permitidos para os estilos no componente por meio da propriedade de matriz da sequência `cq:styleElements`. Na guia Estilos da política na caixa de diálogo de design, o autor do modelo também pode escolher um nome de elemento para definir cada estilo. Isso definirá o nome de elemento do wrapper.

Essa propriedade é definida no nó `cq:Component`. Por exemplo:

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>Evite definir nomes de elemento para os estilos que podem ser combinados. Quando vários nomes de elemento são definidos, a ordem de prioridade é:
>
>1. HTL tem precedência sobre tudo: `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. Entre os vários estilos ativos, o primeiro estilo na lista de estilos configurados na política do componente é aplicado.
>1. Por fim, a `cq:htmlTag`/ `cq:tagName` do componente será considerada um valor de fallback.

>


Essa capacidade de definir nomes de estilo é útil para componentes muito genéricos, como o Contêiner de layout ou o componente de Fragmento de conteúdo, para oferecer-lhes significado adicional.

Por exemplo, permite que um Contêiner de layout receba uma semântica como `<main>`, `<aside>`, `<nav>`, etc.
