---
title: Recurso de pesquisa
description: Adicionando e configurando a Pesquisa em um site de Comunidades
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---

# Recurso de pesquisa {#search-feature}

O recurso de pesquisa funciona com vários outros recursos, como fóruns, para fornecer a capacidade de pesquisar conteúdo.

Ao adicionar a capacidade de pesquisar postagens inseridas por membros da comunidade, chamadas de conteúdo gerado pelo usuário (UGC), há dois componentes: [Pesquisa](#search) e [Resultados da Pesquisa](#search-results).

A página que inclui o componente `Search Results` oferece suporte à pesquisa e à exibição de resultados.

A página que inclui o componente `Search` fornece um local para iniciar uma pesquisa com resultados que aparecem na página `Search Results`.

O recurso de pesquisa pode ser usado com qualquer outro recurso que permita que visitantes e membros do site visualizem conteúdo.

## Pesquisar {#search-features}

### Adicionar pesquisa a uma página {#add-search-to-a-page}

Para adicionar um componente `Search` a uma página no modo de autor, use o navegador de componentes para localizar `Communities / Search` e arrastá-lo para o local em uma página. O uso de `Search` requer uma segunda página para `Search Results.`

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando a biblioteca necessária do lado do cliente, `cq.social.hbs.search`, for incluída, é assim que o componente `Search` aparecerá.

![adicionar-pesquisa](assets/add-search.png)

### Configurar a pesquisa adicionada {#configure-the-added-search}

Selecione o componente `Search` inserido para acessar e selecione o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

Na guia **[!UICONTROL Configurações de pesquisa]**, especifique quais caminhos são pesquisados quando uma consulta é inserida por um visitante.

![configurações-de-pesquisa](assets/search-settings.png)

* **[!UICONTROL Caminhos de Pesquisa]**
Ao adicionar caminhos de pesquisa usando o botão Adicionar item, a pesquisa de conteúdo é limitada. Como exemplo, para limitar a pesquisa a um fórum específico, selecione um componente do fórum que será colocado em uma página:

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Página de resultado]**
Os resultados aparecerão em uma página separada especificada usando o navegador para selecionar uma página contendo o componente `Search Results`.

## Resultados da pesquisa {#search-results}

### Adicionar resultados da pesquisa a uma página {#add-search-results-to-a-page}

Para adicionar um componente `Search Results` a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Search Results`

e arraste-o para o local em uma página. Diferentemente do componente de Pesquisa, nenhuma segunda página é necessária, pois os resultados serão exibidos na mesma página.

Se estiver usando a Pesquisa em outro lugar no site, esta página com `Search Results` poderá ser configurada como `Result Page` para qualquer uma ou todas as instâncias de `Search`.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando a biblioteca do lado do cliente necessária, `cq.social.hbs.search`, for incluída, o componente `Search Result` será mostrado da seguinte forma:

![resultado-da-pesquisa](assets/search-result1.png)

### Configurar o resultado de pesquisa adicionado {#configure-the-added-search-result}

Selecione o componente `Search Results` inserido para acessar e selecione o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

Na guia **[!UICONTROL Configurações de resultado de pesquisa]**, é possível especificar quais caminhos são incluídos na pesquisa quando uma consulta é inserida por um visitante.

![configurações-resultado-pesquisa](assets/search-result-settings.png)

* **[!UICONTROL Resultados de Pesquisa por Página]**

  Defina o número de tópicos/postagens exibidos por página. O padrão é 10.

* **[!UICONTROL Caminhos de Pesquisa]**

  Ao adicionar caminhos de pesquisa usando o botão Adicionar item, a pesquisa de conteúdo é limitada.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página do [Search Essentials](search-implementation.md) para desenvolvedores.
