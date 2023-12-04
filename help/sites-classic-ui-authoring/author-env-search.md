---
title: Pesquisar
description: O ambiente de criação do AEM fornece vários mecanismos de pesquisa de conteúdo, dependendo do tipo de recurso.
uuid: 6dd3df4d-6040-4230-8373-fc028687b675
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8d32960c-47c3-4e92-b02e-ad4d8fea7b2d
docset: aem65
exl-id: 1f46a57f-4966-4dd1-8c99-c0740718ae76
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 11%

---

# Pesquisar{#searching}

O ambiente de criação do AEM fornece vários mecanismos de pesquisa de conteúdo, dependendo do tipo de recurso.

>[!NOTE]
>
>Fora do ambiente de criação, outros mecanismos também estão disponíveis para pesquisa, como o [Construtor de consulta](/help/sites-developing/querybuilder-api.md) e [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## Noções básicas de pesquisa {#search-basics}

Para acessar o painel de pesquisa, clique no link **Pesquisar** na parte superior do painel esquerdo do console apropriado.

![chlimage_1-101](assets/chlimage_1-101.png)

O painel de pesquisa permite pesquisar em todas as páginas do site. Ele contém campos e widgets para o seguinte:

* **Texto completo**: Procure o texto especificado
* **Modificado antes/depois**: Pesquise somente as páginas que foram alteradas entre as datas específicas
* **Modelo**: Pesquise somente as páginas com base no modelo especificado
* **Tags**: pesquisa somente nas páginas com as tags especificadas

>[!NOTE]
>
>Quando sua instância é configurada para [Pesquisa Lucene](/help/sites-deploying/queries-and-indexing.md) você pode usar o seguinte no **Texto completo**:
>
>* [Curingas](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Wildcard_Searches)
>* [Operadores booleanos](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boolean_operators)
>
>* [Expressões regulares](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Regexp_Searches)
>* [Agrupamento de campos](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Field_Grouping)
>* [Impulsionando](https://lucene.apache.org/core/5_3_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Boosting_a_Term)
>

Execute a pesquisa clicando em **Pesquisar** na parte inferior do painel. Clique em **Redefinir** para limpar os critérios de pesquisa.

## Filtro {#filter}

Em vários locais, um filtro pode ser definido (e limpo) para detalhar e refinar sua exibição:

![chlimage_1-102](assets/chlimage_1-102.png)

## Localizar e substituir {#find-and-replace}

No **Sites** console a **Localizar e substituir** A opção de menu permite pesquisar e substituir várias instâncias de uma cadeia de caracteres em uma seção do site.

1. Selecione a página raiz, ou pasta, onde deseja que a ação localizar e substituir ocorra.
1. Selecionar **Ferramentas** depois **Localizar e substituir**:

   ![screen_shot_2012-02-15at120346pm](assets/screen_shot_2012-02-15at120346pm.png)

1. A variável **Localizar e substituir** faz o seguinte:

   * confirma o caminho raiz no qual a ação localizar deve começar
   * define o termo a ser encontrado
   * define o termo que deve substituí-lo
   * indica se a pesquisa deve diferenciar maiúsculas de minúsculas
   * indica se somente palavras inteiras devem ser encontradas (caso contrário, as subsequências de caracteres também serão encontradas)

   Clicando **Visualizar** listas em que o termo foi encontrado. Você pode selecionar/limpar instâncias específicas a serem substituídas:

   ![screen_shot_2012-02-15at120719pm](assets/screen_shot_2012-02-15at120719pm.png)

1. Clique em **Substituir** para substituir todas as instâncias. Você receberá uma solicitação para confirmar a ação.

O escopo padrão para o servlet localizar e substituir abrange as seguintes propriedades:

* `jcr:title`
* `jcr:description`
* `jcr:text`
* `text`

O escopo pode ser alterado usando o Console de gerenciamento Web Apache Felix (por exemplo, em `https://localhost:4502/system/console/configMgr`). Selecionar `CQ WCM Find Replace Servlet (com.day.cq.wcm.core.impl.servlets.FindReplaceServlet)` e configure o escopo conforme necessário.

>[!NOTE]
>
>Em uma instalação padrão do AEM, Localizar e substituir usa Lucene para a funcionalidade de pesquisa.
>
>O Lucene indexa propriedades de sequência de caracteres de até 16k de comprimento. Cadeias de caracteres acima desse valor não serão pesquisadas.
