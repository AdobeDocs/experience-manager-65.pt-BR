---
title: Painéis
seo-title: Dashboards
description: Saiba como criar, configurar e desenvolver novos painéis de AEM.
seo-description: Learn how to create, configure and develop new AEM dashboards.
uuid: 3eadbba2-0ce1-41be-a9f8-e6cafa109893
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 40560e06-2508-45a4-a648-39629ed54f28
exl-id: 5b934e3a-f554-46ec-a913-8d570abb1503
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 3%

---

# Painéis{#dashboards}

Ao usar o AEM, você é capaz de gerenciar muito conteúdo de diferentes tipos (por exemplo, páginas, ativos). Os painéis de AEM fornecem uma maneira fácil de usar e personalizável de definir páginas que exibem dados consolidados.

>[!NOTE]
>
>Painéis AEM são criados com base no usuário, de modo que um usuário só pode acessar seu próprio painel.
>
>No entanto, [Modelos de painel](#creating-a-dashboard-template) pode ser usado para compartilhar configurações comuns e layout do Painel de controle.

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## Administração de painéis {#administering-dashboards}

### Criar Um Painel De Controle {#creating-a-dashboard}

Para criar um novo Painel de Controle, proceda da seguinte maneira:

1. No **Ferramentas** clique em **Console de configuração**.
1. Na árvore, clique duas vezes em **Painel**.
1. Clique em **Novo painel**.
1. Digite o **Título** (por exemplo, Meu painel) e a variável **Nome**.
1. Clique em **Criar**.

### Clonagem De Um Painel {#cloning-a-dashboard}

Talvez você queira ter vários painéis para ver rapidamente as informações sobre seu conteúdo de diferentes visualizações. Para ajudá-lo a criar um novo Painel de Controle, o AEM fornece um recurso de clone que você pode usar para duplicar um Painel de Controle existente. Para clonar um painel, proceda da seguinte maneira:

1. No **Ferramentas** clique em **Console de configuração**.

1. Na árvore, clique em **Painel**.
1. Clique no painel que deseja clonar.

1. Clique em **Clonar**.

1. Digite o **Nome** do novo painel.

### Remover Um Painel {#removing-a-dashboard}

1. No **Ferramentas** clique em **Console de configuração**.

1. Na árvore, clique em **Painel**.
1. Clique no painel que deseja excluir.

1. Clique em **Remover**.

1. Clique em **Sim** para confirmar.

## Componentes do painel {#dashboard-components}

### Visão geral {#overview}

Os componentes do painel não são nada mais do que comuns [Componentes do AEM](/help/sites-developing/developing-components-samples.md). Esta seção descreve os componentes de relatórios enviados com o AEM.

### Componentes de relatórios do Web Analytics {#web-analytics-reporting-components}

O AEM vem com um conjunto de componentes que renderizam várias métricas do [SiteCatalyst](/help/sites-administering/adobeanalytics.md) dados. Esses componentes estão listados na Sidekick sob o **Painel** seção.

Cada componente de relatório fornece pelo menos três guias:

* **Básico**: contém a configuração principal.

* **Relatório:** contém a configuração específica de cada relatório.
* **Estilo**: contém configuração de estilo, como tamanho e margem do gráfico.

Os componentes de relatórios são inicializados com uma configuração padrão que ajuda a configurar rapidamente seu painel.

#### Configuração básica {#basic-configuration}

A variável **Básico** fornece acesso às seguintes entradas de configuração:

**Título** O título exibido no painel.

**Tipo de solicitação** A forma como os dados são solicitados.

**Configuração do SiteCatalyst (opcional)** A configuração que você deseja usar para se conectar ao SiteCatalyst. Se não for fornecida, presume-se que a configuração esteja definida na página Painel (por meio das propriedades da página).

**ID do conjunto de relatórios (opcional)** O conjunto de relatórios SiteCatalyst que você deseja usar para gerar o gráfico.

#### Configuração do relatório {#report-configuration}

Para exibir estatísticas da Web, você precisa definir o intervalo de datas dos dados que deseja obter. A variável **Relatório** fornece dois campos para definir esse intervalo.

>[!NOTE]
>
>Definir um intervalo de datas grande pode diminuir a capacidade de resposta do painel.

**Data - De** Data absoluta ou relativa a partir da qual os dados são obtidos.

**Data - Até** Data absoluta ou relativa para a qual os dados são obtidos.

Cada componente também define configurações específicas.

#### Relatório de horas extras {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**Granularidade de data** Unidade de tempo do eixo X (por exemplo, dia, hora).

**Métricas** A lista de eventos que você deseja exibir.

**Elementos** A lista de elementos que detalha os dados de métricas no gráfico.

#### Relatório da lista classificada {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**Elementos** O elemento que detalha os dados de métricas no gráfico.

**Métricas** O evento que você deseja exibir.

**Não. dos principais itens** Número de itens exibidos pelo relatório.

#### Relatório classificado {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**Métricas** O evento que você deseja exibir.

**Elementos** O elemento que detalha os dados de métricas no gráfico.

#### Relatório principal da seção do site {#top-site-section-report}

Este componente exibe um gráfico mostrando a seção mais visitada de um site de acordo com a configuração a seguir.

![chlimage_1-29](assets/chlimage_1-29a.png)

**Não. dos principais itens** Número de seções exibidas por no relatório.

#### Relatório de tendências {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**Granularidade de data** Unidade de tempo do eixo X (por exemplo, dia, hora).

**Métricas** O evento que você deseja exibir.

**Elementos** O elemento que detalha os dados de métricas no gráfico.

## Extensão do painel {#extending-dashboard}

### Visão geral {#overview-1}

Os painéis são páginas normais ( `cq:Page`), portanto, quaisquer componentes podem ser usados para montar Painéis.

Há um grupo de componentes padrão `Dashboard` contendo componentes de relatórios do analytics que estão habilitados no modelo por padrão.

### Criação De Um Modelo De Painel De Controle {#creating-a-dashboard-template}

Um template define o conteúdo padrão de um novo Painel. Você pode usar vários modelos para criar diferentes tipos de painéis.

Os modelos de painéis são criados como outros modelos de página, exceto pelo fato de serem armazenados em `/libs/cq/dashboards/templates/`. Consulte a [Criação do modelo Contentpage](/help/sites-developing/website.md#creating-the-contentpage-template) seção.

>[!NOTE]
>
>Os modelos de painel são compartilhados entre usuários.

### Desenvolver um componente do painel {#developing-a-dashboard-component}

O desenvolvimento de um componente do Painel consiste na criação de um componente AEM comum. Esta seção descreve um exemplo de um componente que exibe os 10 principais colaboradores.

![chlimage_1-31](assets/chlimage_1-31a.png)

Os componentes principais do autor são armazenados no repositório em `/apps/geometrixx-outdoors/components/reporting` e é composto por:

1. a `jsp` arquivo que lê os dados jcr e define o `html` espaço reservado.

1. uma biblioteca do lado do cliente contendo um `js` arquivo que busca e solicita os dados e, em seguida, preenche o `html` espaço reservado.

![chlimage_1-32](assets/chlimage_1-32a.png)

O seguinte arquivo JavaScript é definido na variável `geout.reporting.topauthors` [Biblioteca do cliente](/help/sites-developing/clientlibs.md) como filho do próprio componente.

A variável [QueryBuilder](/help/sites-developing/querybuilder-api.md) é usado para consultar o repositório para ler `cq:AuditEvent` nós. O resultado da consulta é um objeto JSON do qual as contribuições do autor são extraídas.

#### top_author.js {#top-authors-js}

```
$.ajax({
  url: "/bin/querybuilder.json",
  cache: false,
  data: {
       "orderby": "cq:time",
       "orderby.sort": "desc",
       "p.hits": "full",
       "p.limit": 100,
       "path": "/var/audit/com.day.cq.wcm.core.page/",
       "type": "cq:AuditEvent"
   },
  dataType: "json"
}).done(function( res ) {
    var authors = {};
    // from JSON to Object
    for(var r in res.hits) {
        var userId = res.hits[r].userId;
        if(userId == undefined) {
            continue;
        }
        var auth = authors[userId] || {userId : userId};
        auth.contrib = (auth.contrib || 0) +1;

        authors[userId] = auth;
    }

    // order by contribution
    var orderedByContrib = [];
    for(var a in authors) {
        orderedByContrib.push(authors[a]);
    }
    orderedByContrib.sort(function(a,b){return b.contrib - a.contrib});

    // produce the list
    for (var i=0, tot=orderedByContrib.length; i < tot; i++) {
        var current = orderedByContrib[i];
        $("<div> #" + (i + 1) +" "+ current.userId + " (" + current.contrib +" contrib.)</div>").appendTo("#authors-list");

    }
});
```

A variável `JSP` inclui ambos `global.jsp` e `clientlib`.

#### top_author.jsp {#top-authors-jsp}

```java
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%
%><%@include file="/libs/foundation/global.jsp" %><%
%>
<ui:includeClientLib categories="geout.reporting.topauthors" />
<%
String reportletTitle = properties.get("title", "Top Authors");
%>
<html>
     <h3><%=xssAPI.encodeForHTML(reportletTitle) %></h3>
     <div id="authors-list"></div>
</html>
```
