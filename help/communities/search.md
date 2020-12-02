---
title: Recurso de pesquisa
seo-title: Recurso de pesquisa
description: Adicionar e configurar a Pesquisa em um site das Comunidades
seo-description: Adicionar e configurar a Pesquisa em um site das Comunidades
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
translation-type: tm+mt
source-git-commit: 6ab91667ad668abf80ccf1710966169b3a187928
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 2%

---


# Recurso de pesquisa {#search-feature}

O recurso de pesquisa funciona com vários outros recursos, como fóruns, para fornecer a capacidade de pesquisar conteúdo.

Ao adicionar a capacidade de pesquisar postagens inseridas por membros da comunidade, chamado de conteúdo gerado pelo usuário (UGC), há dois componentes: [Pesquisar](#search) e [Resultados da Pesquisa](#search-results).

A página que inclui o componente `Search Results` oferece suporte à pesquisa e à exibição de resultados.

A página que inclui o componente `Search` fornece um local para iniciar uma pesquisa com os resultados que aparecem na página `Search Results`.

O recurso de pesquisa pode ser usado com qualquer outro recurso que permita aos visitantes e membros do site visualizações conteúdo.

## Pesquisar {#search-features}

### Adicionar Pesquisa a uma Página {#add-search-to-a-page}

Para adicionar um componente `Search` a uma página no modo de autor, use o navegador de componentes para localizar `Communities / Search` e arraste-o para o lugar em uma página. O uso de `Search` requer uma segunda página para `Search Results.`

Para obter as informações necessárias, visite [Informações básicas sobre componentes das comunidades](basics.md).

Quando a biblioteca necessária do lado do cliente, `cq.social.hbs.search`, for incluída, será assim que o componente `Search` aparecerá.

![add-search](assets/add-search.png)

### Configurar a pesquisa adicionada {#configure-the-added-search}

Selecione o componente `Search` inserido para acessar e selecione o ícone `Configure` que abre a caixa de diálogo de edição.

![configue](assets/configure-new.png)

Na guia **[!UICONTROL Configurações de pesquisa]**, especifique como os caminhos são pesquisa quando um query é inserido por um visitante.

![definições de pesquisa](assets/search-settings.png)

* **[!UICONTROL Procurar]**
caminhosAo adicionar caminhos de pesquisa usando o botão Adicionar item, a pesquisa de conteúdo é limitada. Como exemplo, para limitar a pesquisa a um fórum específico, selecione um componente de fórum inserido em uma página:

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Página]**
de resultadoOs resultados aparecerão em uma página separada especificada usando o navegador para selecionar uma página que contém a variável 
`Search Results` componente.

## Resultados da pesquisa {#search-results}

### Adicionar resultados de pesquisa a uma página {#add-search-results-to-a-page}

Para adicionar um componente `Search Results` a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Search Results`

e arraste-o para o lugar em uma página. Ao contrário do componente de Pesquisa, nenhuma segunda página é necessária, pois os resultados serão exibidos na mesma página.

Se estiver usando Pesquisar em outro lugar do site, essa única página com `Search Results` pode ser configurada para ser `Result Page` para qualquer instância ou todas as instâncias de `Search`.

Para obter as informações necessárias, visite [Informações básicas sobre componentes das comunidades](basics.md).

Quando a biblioteca do lado do cliente, `cq.social.hbs.search`, for incluída, o componente `Search Result` aparecerá desta forma:

![resultado da pesquisa](assets/search-result1.png)

### Configurar o resultado de pesquisa adicionado {#configure-the-added-search-result}

Selecione o componente `Search Results` inserido para acessar e selecione o ícone `Configure` que abre a caixa de diálogo de edição.

![configure](assets/configure-new.png)

Na guia **[!UICONTROL Configurações do resultado da pesquisa]**, é possível especificar quais caminhos estão incluídos na pesquisa quando um query é inserido por um visitante.

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL Resultados de busca por página]**

   Defina o número de tópicos/postagens exibidos por página. O padrão é 10.

* **[!UICONTROL Caminhos de pesquisa]**

   Ao adicionar caminhos de pesquisa usando o botão Adicionar item, a pesquisa de conteúdo é limitada.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Search Essentials](search-implementation.md) para desenvolvedores.
