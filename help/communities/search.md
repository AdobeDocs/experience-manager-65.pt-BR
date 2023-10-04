---
title: Recurso de pesquisa
description: Adicionando e configurando a Pesquisa em um site de Comunidades
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 2%

---

# Recurso de pesquisa {#search-feature}

O recurso de pesquisa funciona com vários outros recursos, como fóruns, para fornecer a capacidade de pesquisar conteúdo.

Ao adicionar a capacidade de pesquisar publicações inseridas por membros da comunidade, chamadas de conteúdo gerado pelo usuário (UGC), há dois componentes: [Pesquisar](#search) e [Resultados da pesquisa](#search-results).

A página que inclui a variável `Search Results` O componente oferece suporte à pesquisa e à exibição de resultados.

A página que inclui a variável `Search` componente fornece um local para iniciar uma pesquisa com resultados que aparecem na `Search Results` página.

O recurso de pesquisa pode ser usado com qualquer outro recurso que permita que visitantes e membros do site visualizem conteúdo.

## Pesquisar {#search-features}

### Adicionar pesquisa a uma página {#add-search-to-a-page}

Para adicionar um `Search` para uma página no modo de autor, use o navegador de componentes para localizar `Communities / Search` e arraste-o para o local em uma página. Uso do `Search` O requer uma segunda página para o `Search Results.`

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando a biblioteca do lado do cliente for necessária, `cq.social.hbs.search`, está incluído, é assim que a variável `Search` será exibido.

![adicionar-pesquisar](assets/add-search.png)

### Configurar a pesquisa adicionada {#configure-the-added-search}

Selecione o colocado `Search` para acessar e selecionar a variável `Configure` ícone que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

No **[!UICONTROL Configurações de pesquisa]** especifique quais caminhos são pesquisados quando uma consulta é inserida por um visitante.

![search-settings](assets/search-settings.png)

* **[!UICONTROL Caminhos de pesquisa]**
Ao adicionar caminhos de pesquisa usando o botão Adicionar item, a pesquisa de conteúdo é limitada. Como exemplo, para limitar a pesquisa a um fórum específico, selecione um componente do fórum que será colocado em uma página:

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Página de resultado]**
Os resultados aparecerão em uma página separada especificada usando o navegador para selecionar uma página contendo os `Search Results` componente.

## Resultados da pesquisa {#search-results}

### Adicionar resultados da pesquisa a uma página {#add-search-results-to-a-page}

Para adicionar um `Search Results` para uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Search Results`

e arraste-o para o local em uma página. Diferentemente do componente de Pesquisa, nenhuma segunda página é necessária, pois os resultados serão exibidos na mesma página.

Se estiver usando a Pesquisa em outro lugar no site, esta página com `Search Results` pode ser configurado para ser o `Result Page` para qualquer uma ou todas as instâncias de `Search`.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando a biblioteca do lado do cliente for necessária, `cq.social.hbs.search`, está incluído, é assim que a variável `Search Result` componente aparecerá:

![resultado da pesquisa](assets/search-result1.png)

### Configurar o resultado de pesquisa adicionado {#configure-the-added-search-result}

Selecione o colocado `Search Results` para acessar e selecionar a variável `Configure` ícone que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

No **[!UICONTROL Configurações dos resultados de pesquisa]** é possível especificar quais caminhos são incluídos na pesquisa quando um query é inserido por um visitante.

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL Resultados de busca por página]**

  Defina o número de tópicos/postagens exibidos por página. O padrão é 10.

* **[!UICONTROL Caminhos de pesquisa]**

  Ao adicionar caminhos de pesquisa usando o botão Adicionar item, a pesquisa de conteúdo é limitada.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Search Essentials](search-implementation.md) página para desenvolvedores.
