---
title: Uso de tags
seo-title: Uso de tags
description: Tags são um método rápido e fácil de classificar o conteúdo em um site. Tags podem ser consideradas palavras-chave ou rótulos que podem ser anexados a uma página, ativo ou outro conteúdo para permitir que as pesquisas encontrem esse conteúdo e todo o conteúdo relacionado.
seo-description: Tags são um método rápido e fácil de classificar o conteúdo em um site. Tags podem ser consideradas palavras-chave ou rótulos que podem ser anexados a uma página, ativo ou outro conteúdo para permitir que as pesquisas encontrem esse conteúdo e todo o conteúdo relacionado.
uuid: 9799131f-4043-4022-a401-af8be93a1bf6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: c117b9d1-e4ae-403f-8619-6e48d424a761
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# Uso de tags{#using-tags}

Tags são um método rápido e fácil de classificar o conteúdo em um site. Tags podem ser consideradas palavras-chave ou rótulos que podem ser anexados a uma página, ativo ou outro conteúdo para permitir que as pesquisas encontrem esse conteúdo e todo o conteúdo relacionado.

* See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.
* See [Tagging for Developers](/help/sites-developing/tags.md) for information about the tagging framework as well as including and extending tags in custom applications.

## Dez razões para usar marcação {#ten-reasons-to-use-tagging}

1. Organização do conteúdo: a marcação facilita a vida dos autores, pois eles podem organizar rapidamente o conteúdo com pouco esforço.
1. Organização de tags: enquanto tags organizam conteúdo, taxonomias/espaços de nome hierárquicos organizam tags.
1. Tags profundamente organizadas: com a capacidade de criar tags e subtags, é possível expressar sistemas taxonômicos inteiros, abrangendo termos, subtermos e seus relacionamentos. É possível criar uma segunda (ou terceira) hierarquia de conteúdo em paralelo à oficial.
1. Marcação controlada: a marcação pode ser controlada com a aplicação de permissões a tags e/ou espaços de nome para controlar a criação e a aplicação de tags.
1. Marcação flexível: tags têm muitos nomes e faces: tags, termos de taxonomia, categorias, rótulos e muito mais. Elas são flexíveis em seu modelo de conteúdo e na maneira como podem ser usadas. Por exemplo, ao estruturar dados demográficos de direcionamento, categorizar e classificar conteúdo ou criar uma hierarquia de conteúdo secundário.
1. Pesquisas aprimoradas: o componente de pesquisa padrão no AEM inclui amplamente tags criadas e tags aplicadas, às quais é possível aplicar filtros para restringir os resultados apenas àqueles que são relevantes.
1. Habilitação de SEO: tags aplicadas como propriedades de página aparecerão automaticamente nas metatags da página, tornando-a visível para os mecanismos de pesquisa.
1. Sofisticação simples: tags podem ser criadas simplesmente a partir de uma palavra e com o toque de um botão. Posteriormente, um título, uma descrição e um número ilimitado de etiquetas podem ser adicionadas para fornecer mais semântica à tag.
1. Consistência básica: o sistema de marcação é um componente central do AEM e é usado por todos os recursos do AEM para categorizar o conteúdo. Além disso, a API de marcação está disponível para os desenvolvedores criarem aplicativos ativados para marcação com acesso às mesmas taxonomias.
1. Combina estrutura e flexibilidade: o AEM é ideal para trabalhar com informações estruturadas, devido ao aninhamento de páginas e caminhos. Ele é igualmente eficiente quando se trabalha com informações não estruturadas, devido à pesquisa de texto completo integrada. A marcação combina os pontos fortes de estrutura e flexibilidade.

Ao projetar a estrutura de conteúdo de um site e o esquema de metadados para ativos, considere a abordagem leve e acessível de tags.

## Aplicação de tags {#applying-tags}

In the author environment, authors may apply tags by accessing the page properties and entering one or more tags in the **Tags/Keywords** field.

To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the `Tags/Keywords` field pull-down to select from the list of tags permitted for the page. Tthe **Standard Tags** tab is the default namespace, which means there is no `namespace-string:` prefixed to the taxonomy.

![chlimage_1-2](assets/chlimage_1-2a.png)

### Publicação de tags {#publishing-tags}

Assim como com as páginas, você pode fazer o seguinte em tags e espaços de nome:

**Ativar**

* Ativar tags individuais.

   Assim como com as páginas, tags recém-criadas precisam ser ativadas antes de serem disponibilizadas no ambiente de publicação.

>[!NOTE]
>
>Quando você ativa uma página, uma caixa de diálogo é aberta automaticamente e permite ativar tags inativadas pertencentes à página.

**Desativar**

* Desativar as tags selecionadas.

## Nuvens de tags {#tag-clouds}

Nuvens de tags mostram uma nuvem de tags, seja para a página atual, o site inteiro ou as tags mais acessadas. Nuvens de tags são um meio de destacar os problemas que são (ou foram) de interesse do usuário. O tamanho do texto usado para exibir a tag varia em relação ao seu uso.

O componente [Nuvem de tags](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#tag-cloud) (grupo de componentes Geral) é usado para adicionar uma nuvem de tags a uma página.

## Pesquisa em tags {#searching-on-tags}

Você pode procurar tags nos ambiente de autor e publicação.

### Uso do componente de pesquisa {#using-search-component}

Adding a [Search component](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md#search) to a page provides a search capability which includes tags and can be used in both the author and publish environments.

![chlimage_1-3](assets/chlimage_1-3a.png)

