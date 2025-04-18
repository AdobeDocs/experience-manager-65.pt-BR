---
title: Pesquisar
description: O ambiente de criação do AEM fornece vários mecanismos de pesquisa de conteúdo, dependendo do tipo de recurso.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 1f46a57f-4966-4dd1-8c99-c0740718ae76
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 12%

---

# Pesquisar{#searching}

O ambiente de criação do AEM fornece vários mecanismos de pesquisa de conteúdo, dependendo do tipo de recurso.

>[!NOTE]
>
>Fora do ambiente de criação, outros mecanismos também estão disponíveis para pesquisa, como o [Construtor de consultas](/help/sites-developing/querybuilder-api.md) e o [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## Noções básicas de pesquisa {#search-basics}

Para acessar o painel de pesquisa, clique na guia **Pesquisar** na parte superior do painel à esquerda do console apropriado.

![chlimage_1-101](assets/chlimage_1-101.png)

O painel de pesquisa permite pesquisar em todas as páginas do site. Ele contém campos e widgets para o seguinte:

* **Texto completo**: procure o texto especificado
* **Modificado antes/depois de**: pesquise somente as páginas que foram alteradas entre as datas específicas
* **Modelo**: pesquise somente as páginas baseadas no modelo especificado
* **Marcas**: pesquisar somente as páginas com as marcas especificadas

>[!NOTE]
>
>Quando sua instância está configurada para [Pesquisa Lucene](/help/sites-deploying/queries-and-indexing.md), você pode usar o seguinte em **Texto completo**:
>
>* [Caracteres curinga](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [Operadores booleanos](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)
>
>* [Expressões regulares](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [Agrupamento de campos](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [Aumentando](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)
>

Execute a pesquisa clicando em **Pesquisar** na parte inferior do painel. Clique em **Redefinir** para limpar os critérios de pesquisa.

## Filtro {#filter}

Em vários locais, um filtro pode ser definido (e limpo) para detalhar e refinar sua exibição:

![chlimage_1-102](assets/chlimage_1-102.png)

## Localizar e substituir {#find-and-replace}

No console **Sites**, uma opção de menu **Localizar e Substituir** permite procurar e substituir várias instâncias de uma cadeia de caracteres, em uma seção do site.

1. Selecione a página raiz, ou pasta, onde deseja que a ação localizar e substituir ocorra.
1. Selecione **Ferramentas** e depois **Localizar e Substituir**:

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. A caixa de diálogo **Localizar e Substituir** faz o seguinte:

   * confirma o caminho raiz no qual a ação localizar deve começar
   * define o termo a ser encontrado
   * define o termo que deve substituí-lo
   * indica se a pesquisa deve diferenciar maiúsculas de minúsculas
   * indica se somente palavras inteiras devem ser encontradas (caso contrário, as subsequências de caracteres também serão encontradas)

   Clicar em **Visualizar** lista onde o termo foi encontrado. Você pode selecionar/limpar instâncias específicas a serem substituídas:

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. Clique em **Substituir** para substituir todas as instâncias. Você receberá uma solicitação para confirmar a ação.

O escopo padrão para o servlet localizar e substituir abrange as seguintes propriedades:

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

O escopo pode ser alterado usando o Console de Gerenciamento Web Apache Felix (por exemplo, em `https://localhost:4502/system/console/configMgr`). Selecione `CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)` e configure o escopo conforme necessário.

>[!NOTE]
>
>Em uma instalação padrão do AEM, Localizar e substituir usa Lucene para a funcionalidade de pesquisa.
>
>O Lucene indexa propriedades de sequência de caracteres de até 16k de comprimento. Cadeias de caracteres acima desse valor não serão pesquisadas.
