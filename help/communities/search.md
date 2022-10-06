---
title: Recurso de pesquisa
seo-title: Search Feature
description: Adicionar e configurar a Pesquisa em um site do Communities
seo-description: Adding and configuring Search to a Communities site
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 2%

---

# Recurso de pesquisa {#search-feature}

O recurso de pesquisa funciona com vários outros recursos, como fóruns, para fornecer a capacidade de pesquisar conteúdo.

Ao adicionar a capacidade de pesquisar postagens inseridas por membros da comunidade, conhecidas como conteúdo gerado pelo usuário (UGC), há dois componentes: [Pesquisar](#search) e [Resultados da pesquisa](#search-results).

A página que inclui a variável `Search Results` O componente suporta pesquisa e a exibição de resultados.

A página que inclui a variável `Search` fornece um local para iniciar uma pesquisa com os resultados que aparecem no `Search Results` página.

O recurso de pesquisa pode ser usado com qualquer outro recurso que permita que visitantes e membros do site visualizem o conteúdo.

## Pesquisar {#search-features}

### Adicionar Pesquisa a uma Página {#add-search-to-a-page}

Para adicionar uma `Search` para uma página no modo autor, use o navegador de componentes para localizar `Communities / Search` e arraste-a para o local em uma página. Utilização de `Search` O requer uma segunda página para o `Search Results.`

Para obter as informações necessárias, visite [Noções básicas sobre componentes do Communities](basics.md).

Quando a biblioteca do lado do cliente necessária, `cq.social.hbs.search`, está incluído, é assim que a função `Search` será exibido.

![adicionar pesquisa](assets/add-search.png)

### Configure a pesquisa adicionada {#configure-the-added-search}

Selecione o `Search` para acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![config](assets/configure-new.png)

Em **[!UICONTROL Configurações de pesquisa]** , especifique como são os caminhos de pesquisa quando uma consulta é inserida por um visitante.

![configurações de pesquisa](assets/search-settings.png)

* **[!UICONTROL Caminhos de pesquisa]**
Ao adicionar caminhos de pesquisa usando o botão Adicionar item, a pesquisa de conteúdo é limitada. Como exemplo, para limitar a pesquisa a um fórum específico, selecione um componente de fórum inserido em uma página:

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Página de resultados]**
Os resultados serão exibidos em uma página separada especificada usando o navegador para selecionar uma página contendo o 
`Search Results` componente.

## Resultados da pesquisa {#search-results}

### Adicionar resultados de pesquisa a uma página {#add-search-results-to-a-page}

Para adicionar uma `Search Results` para uma página no modo autor, use o navegador de componentes para localizar

* `Communities / Search Results`

e arraste-a para o local em uma página. Diferentemente do componente de Pesquisa, nenhuma segunda página é necessária, pois os resultados serão exibidos na mesma página.

Se estiver usando Pesquisar em outro lugar do site, esta página terá `Search Results` pode ser configurado para ser `Result Page` para qualquer ou todas as instâncias de `Search`.

Para obter as informações necessárias, visite [Noções básicas sobre componentes do Communities](basics.md).

Quando a biblioteca do lado do cliente necessária, `cq.social.hbs.search`, está incluído, é assim que a função `Search Result` componente será exibido:

![resultado da pesquisa](assets/search-result1.png)

### Configurar o resultado da pesquisa adicionada {#configure-the-added-search-result}

Selecione o `Search Results` para acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure](assets/configure-new.png)

Em **[!UICONTROL Configurações do Resultado da Pesquisa]** , é possível especificar quais caminhos estão incluídos na pesquisa quando um query é inserido por um visitante.

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL Resultados de busca por página]**

   Defina o número de tópicos/postagens exibidos por página. O padrão é 10.

* **[!UICONTROL Caminhos de pesquisa]**

   Ao adicionar caminhos de pesquisa usando o botão Adicionar item, a pesquisa de conteúdo é limitada.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos da pesquisa](search-implementation.md) página para desenvolvedores.
