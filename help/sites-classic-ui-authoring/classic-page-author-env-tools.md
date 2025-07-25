---
title: Criação - o ambiente e as ferramentas
description: O console Sites permite gerenciar e navegar no site. Usando dois painéis, a estrutura do site pode ser expandida e as ações podem ser executadas nos elementos necessários.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: 5d7b6b2e-d1d8-4efe-b9ff-c9542b4e67d7
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 25bf0d64b6839afec0112ea8c9fde0510e56ccf4
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 5%

---

# Criação - o ambiente e as ferramentas {#authoring-the-environment-and-tools}

O ambiente de criação do AEM fornece vários mecanismos para organização e edição de conteúdo. As ferramentas fornecidas são acessadas de vários consoles e editores de página.

## Administração do site {#site-administration}

O console **Sites** permite gerenciar e navegar no site. Usando os dois painéis, a estrutura do site pode ser expandida e as ações podem ser executadas no elemento necessário:

![chlimage_1-108](assets/chlimage_1-108.png)

## Editar seu conteúdo da página {#editing-your-page-content}

Há um editor de página separado com a interface clássica, usando o localizador de conteúdo e o sidekick:

`https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

![chlimage_1-109](assets/chlimage_1-109.png)

## Acessar ajuda   {#accessing-help}

Vários recursos da **Ajuda** podem ser acessados diretamente de dentro do AEM:

Além de acessar a [ajuda das barras de ferramentas do console](/help/sites-classic-ui-authoring/author-env-basic-handling.md#accessing-help), você também pode acessar a ajuda do sidekick (usando o ? ícone) ao editar uma página:

![Sidekick Recolhido](do-not-localize/sidekick-collapsed-2.png)

Ou usando o botão **Ajuda** na caixa de diálogo de edição de componentes específicos; isso mostrará a ajuda sensível ao contexto.

## Sidekick {#sidekick}

A guia **Componentes** do sidekick permite navegar pelos componentes disponíveis para serem adicionados à página atual. O grupo desejado pode ser expandido e, em seguida, um componente arrastado para o local desejado na página.

![chlimage_1-110](assets/chlimage_1-110.png)

## O Localizador de conteúdo {#the-content-finder}

O Localizador de conteúdo é uma maneira rápida e fácil de encontrar ativos e/ou conteúdo no repositório ao editar uma página.

Você pode usar o localizador de conteúdo para localizar um intervalo de recursos. Quando apropriado, você pode arrastar um item e soltá-lo em um parágrafo na sua página:

* [Imagens](#finding-images)
* [Documentos](#finding-documents)
* [Filmes](#finding-movies)
* [Navegador do Dynamic Media](/help/sites-administering/scene7.md#scene7contentbrowser)
* [Páginas](#finding-pages)

* [Parágrafos](#referencing-paragraphs-from-other-pages)
* [Produtos](#products)
* Ou para [navegar no site por estrutura de repositório](#the-content-finder)

Com todas as opções você pode [procurar itens específicos](#the-content-finder).

### Localizando imagens {#finding-images}

Essa guia lista todas as imagens no repositório.

Depois de criar um parágrafo Imagem na página, você pode arrastar um item e soltá-lo no parágrafo.

![chlimage_1-111](assets/chlimage_1-111.png)

### Localizando documentos {#finding-documents}

Essa guia lista todos os documentos no repositório.

Depois de criar um parágrafo Download na página, você pode arrastar um item e soltá-lo no parágrafo.

![chlimage_1-112](assets/chlimage_1-112.png)

### Encontrar filmes {#finding-movies}

Essa guia lista todos os filmes (por exemplo, itens de Flash) no repositório.

Depois de criar um parágrafo apropriado (por exemplo, Flash) na página, você pode arrastar um item e soltá-lo no parágrafo.

![chlimage_1-113](assets/chlimage_1-113.png)

### Produtos {#products}

Essa guia lista todos os produtos. Depois de criar um parágrafo apropriado (por exemplo, Produto) na página, você pode arrastar um item e soltá-lo no parágrafo.

![chlimage_1-114](assets/chlimage_1-114.png)

### Encontrar páginas {#finding-pages}

Esta guia mostra todas as páginas. Clique duas vezes em qualquer página para abri-la para edição.

![chlimage_1-115](assets/chlimage_1-115.png)

### Referência de parágrafos de outras páginas {#referencing-paragraphs-from-other-pages}

Esta guia permite procurar outra página. Todos os parágrafos dessa página serão listados. Você pode arrastar um parágrafo para a página atual, isso criará uma referência ao parágrafo original.

![chlimage_1-116](assets/chlimage_1-116.png)

### Usando a View Repositório Completo {#using-the-full-repository-view}

Esta guia mostra todos os recursos no repositório.

![chlimage_1-117](assets/chlimage_1-117.png)

### Utilização da pesquisa com o navegador de conteúdo {#using-search-with-the-content-browser}

Em todas as opções, é possível pesquisar por itens específicos. Todas as tags e recursos que correspondem ao padrão de pesquisa são listados:

![screen_shot_2012-02-08at100746am](assets/screen_shot_2012-02-08at100746am.png)

Também é possível usar curingas para a pesquisa. Os curingas aceitos são:

* `*`
corresponde a uma sequência de zero ou mais caracteres.

* `?`
corresponde a um único caractere.

>[!NOTE]
>
>Há uma pseudo propriedade &quot;name&quot; que deve ser usada para executar uma pesquisa curinga.

Por exemplo, se houver uma imagem disponível com o nome:

`ad-nmvtis.jpg`

os seguintes padrões de pesquisa o encontrarão (e quaisquer outras imagens que correspondam ao padrão):

* `name:*nmv*`
* `name:AD*`
a correspondência de caracteres *não* diferencia maiúsculas de minúsculas.

* `name:ad?nm??is.*`
você pode usar qualquer número de curingas em uma query.

>[!NOTE]
>
>Você também pode usar a pesquisa do [SQL2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/commons/query/sql2/package-summary.html).

## Mostrando referências {#showing-references}

O AEM permite visualizar quais páginas estão vinculadas à página em que você está trabalhando no momento.

Para mostrar referências de página:

1. No sidekick, selecione o ícone de guia **Página**.

   ![screen_shot_2012-02-16at83127pm](assets/screen_shot_2012-02-16at83127pm.png)

1. Selecionar **Mostrar referências...** O AEM abre a janela Referências e exibe quais páginas se referem à página selecionada, incluindo seus caminhos.

   ![screen_shot_2012-02-16at83311pm](assets/screen_shot_2012-02-16at83311pm.png)

O AEM mostra todas as páginas que fazem referência direta à página selecionada, bem como qualquer referência indireta. É útil compreender todos os links que serão atualizados se você precisar mover ou excluir a página.

## Ações adicionais do Sidekick {#additional-actions}

Em determinadas situações, outras ações estão disponíveis no Sidekick, incluindo:

* [Lançamentos](/help/sites-classic-ui-authoring/classic-launches.md)
* [Live Copies](/help/sites-administering/msm.md)

* [Blueprint](/help/sites-administering/msm-best-practices.md)

Outras [relações entre páginas podem ser vistas no console Sites](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console).

## Log de auditoria {#audit-log}

O **Log de Auditoria** pode ser acessado a partir da guia **Informações** do sidekick. Ela lista as ações recentes tomadas na página atual; por exemplo:

![chlimage_1-118](assets/chlimage_1-118.png)

## Informações da página {#page-information}

O console do Site também [fornece informações sobre o status atual da página](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console), como publicação, modificação, bloqueado, livecopy etc.

## Modos de página   {#page-modes}

Ao editar uma página com a interface clássica, existem vários modos que podem ser acessados usando os ícones na parte inferior do sidekick:

![Modos de Página](do-not-localize/chlimage_1-12.png)

A linha de ícones na parte inferior do Sidekick é usada para alternar modos para trabalhar com as páginas:

* [Editar](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)
Esse é o modo padrão e permite editar a página, adicionar ou excluir componentes e fazer outras alterações.

* [Visualizar](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#previewing-pages)
Esse modo permite que você visualize a página como se ela estivesse aparecendo em seu site em sua forma final.

* [Design](/help/sites-classic-ui-authoring/classic-page-author-design-mode.md#main-pars-procedure-0)
Nesse modo, é possível editar o design da página configurando os componentes acessíveis.

>[!NOTE]
>
>Outras opções também estão disponíveis:
>
>* [Andaime](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md)
>* [Contexto do Cliente](/help/sites-administering/client-context.md)
>* Sites - abre o console Sites.
>* Recarregar - atualizará a página.

## Atalhos de teclado {#keyboard-shortcuts}

Vários [atalhos de teclado](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) estão disponíveis.
