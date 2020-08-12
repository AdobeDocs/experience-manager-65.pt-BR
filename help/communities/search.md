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

Ao adicionar a capacidade de pesquisar postagens inseridas por membros da comunidade, chamado de conteúdo gerado pelo usuário (UGC), há dois componentes: [Resultados](#search) de pesquisa e [pesquisa](#search-results).

A página que inclui o `Search Results` componente oferece suporte à pesquisa e à exibição de resultados.

A página que inclui o `Search` componente fornece um local para iniciar uma pesquisa com os resultados que aparecem na `Search Results` página.

O recurso de pesquisa pode ser usado com qualquer outro recurso que permita aos visitantes e membros do site visualizações conteúdo.

## Pesquisar {#search-features}

### Adicionar pesquisa a uma página {#add-search-to-a-page}

Para adicionar um `Search` componente a uma página no modo de autor, use o navegador de componentes para localizá-lo `Communities / Search` e arrastá-lo para um local em uma página. O uso de `Search` requer uma segunda página para a variável `Search Results.`

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](basics.md).

Quando a biblioteca do lado do cliente necessária, `cq.social.hbs.search`, estiver incluída, é assim que o `Search` componente será exibido.

![add-search](assets/add-search.png)

### Configurar a pesquisa adicionada {#configure-the-added-search}

Selecione o componente inserido a ser acessado e selecione o `Search` `Configure` ícone que abre a caixa de diálogo de edição.

![configue](assets/configure-new.png)

Na guia Configurações **[!UICONTROL de]** pesquisa, especifique como os caminhos são pesquisa quando um query é inserido por um visitante.

![definições de pesquisa](assets/search-settings.png)

* **[!UICONTROL Caminhos de pesquisa]** Ao adicionar caminhos de pesquisa usando o botão Adicionar item, a pesquisa de conteúdo é limitada. Como exemplo, para limitar a pesquisa a um fórum específico, selecione um componente de fórum inserido em uma página:

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Página]** de resultados Os resultados serão exibidos em uma página separada especificada usando o navegador para selecionar uma página que contenha a variável 
`Search Results` componente.

## Resultados da pesquisa {#search-results}

### Adicionar resultados de pesquisa a uma página {#add-search-results-to-a-page}

Para adicionar um `Search Results` componente a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Search Results`

e arraste-o para o lugar em uma página. Ao contrário do componente de Pesquisa, nenhuma segunda página é necessária, pois os resultados serão exibidos na mesma página.

Se você estiver usando Pesquisar em outro lugar do site, essa página com `Search Results` pode ser configurada para ser a `Result Page` para qualquer instância ou para todas as instâncias de `Search`.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](basics.md).

Quando a biblioteca do lado do cliente necessária, `cq.social.hbs.search`, estiver incluída, será assim que o `Search Result` componente será exibido:

![resultado da pesquisa](assets/search-result1.png)

### Configurar o resultado de pesquisa adicionado {#configure-the-added-search-result}

Selecione o componente inserido a ser acessado e selecione o `Search Results` `Configure` ícone que abre a caixa de diálogo de edição.

![configure](assets/configure-new.png)

Na guia Configurações **[!UICONTROL de resultado da]** pesquisa, é possível especificar quais caminhos são incluídos na pesquisa quando um query é inserido por um visitante.

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL Resultados de busca por página]**

   Defina o número de tópicos/postagens exibidos por página. O padrão é 10.

* **[!UICONTROL Caminhos de pesquisa]**

   Ao adicionar caminhos de pesquisa usando o botão Adicionar item, a pesquisa de conteúdo é limitada.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Search Essentials](search-implementation.md) para desenvolvedores.
