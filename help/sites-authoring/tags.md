---
title: 'Uso de tags  '
seo-title: 'Uso de tags  '
description: Tags são um método rápido e fácil de classificar o conteúdo em um site
seo-description: Tags são um método rápido e fácil de classificar o conteúdo em um site
uuid: 5d922443-f924-426e-acf4-27dffd1053f6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9fb6d603-eb17-4192-bfa6-6c316f14ac7d
docset: aem65
translation-type: tm+mt
source-git-commit: 52cb99353ae33c8097b6b5bd29f6c040df30b42d
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 84%

---


# Uso de tags  {#using-tags}

Tags são um método rápido e fácil de classificar o conteúdo em um site. Tags podem ser consideradas palavras-chave ou rótulos que podem ser anexados a uma página, ativo ou outro conteúdo para permitir que as pesquisas encontrem esse conteúdo e todo o conteúdo relacionado.

* See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.
* See [Tagging for Developers](/help/sites-developing/tags.md) for information about the tagging framework as well as including and extending tags in custom applications.

## Dez razões para usar marcação {#ten-reasons-to-use-tagging}

1. **Organização do conteúdo** - a marcação facilita a vida dos autores, pois eles podem organizar rapidamente o conteúdo com pouco esforço.
1. **Organização de tags** - enquanto tags organizam conteúdo, taxonomias/espaços de nome hierárquicos organizam tags.
1. **Tags profundamente organizadas** - com a capacidade de criar tags e subtags, é possível expressar sistemas taxonômicos inteiros, abrangendo termos, subtermos e seus relacionamentos. É possível criar uma segunda (ou terceira) hierarquia de conteúdo em paralelo à oficial.
1. **Marcação controlada** - a marcação pode ser controlada com a aplicação de permissões a tags e/ou espaços de nome para controlar a criação e a aplicação de tags.
1. **Marcação flexível** - tags têm muitos nomes e faces: tags, termos de taxonomia, categorias, rótulos e muito mais. Elas são flexíveis em seu modelo de conteúdo e na maneira como podem ser usadas. Por exemplo, ao estruturar dados demográficos de direcionamento, categorizar e classificar conteúdo ou criar uma hierarquia de conteúdo secundário.
1. **Pesquisas aprimoradas** - o componente de pesquisa padrão no AEM inclui amplamente tags criadas e tags aplicadas, às quais é possível aplicar filtros para restringir os resultados apenas àqueles que são relevantes.
1. **Habilitação de SEO** - aplicadas como propriedades de página aparecerão automaticamente nas metatags da página, tornando-a visível para os mecanismos de pesquisa.
1. **Sofisticação simples** - tags podem ser criadas simplesmente a partir de uma palavra e com o toque de um botão. Posteriormente, um título, uma descrição e um número ilimitado de etiquetas podem ser adicionadas para fornecer mais semântica à tag.
1. **Consistência básica** - o sistema de marcação é um componente central do AEM e é usado por todos os recursos do AEM para categorizar o conteúdo. Além disso, a API de marcação está disponível para os desenvolvedores criarem aplicativos ativados para marcação com acesso às mesmas taxonomias.
1. **Combina estrutura e flexibilidade** - AEM é ideal para trabalhar com informações estruturadas, devido ao aninhamento de páginas e caminhos. Ele é igualmente eficiente quando se trabalha com informações não estruturadas, devido à pesquisa de texto completo integrada. A marcação combina os pontos fortes de estrutura e flexibilidade.

Ao projetar a estrutura de conteúdo de um site e o esquema de metadados para ativos, considere a abordagem leve e acessível de tags.

## Aplicação de tags   {#applying-tags}

No ambiente de criação, os autores podem aplicar tags acessando as propriedades da página e digitando uma ou mais tags no campo **Tags/Palavras-chave**.

To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window. A guia **Tags padrão** é o namespace padrão, o que significa que não há `namespace-string:` prefixado à taxonomia.

![Janela Selecionar tags; use o botão X para desmarcar as tags atualmente selecionadas](assets/chlimage_1-41.png)

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
