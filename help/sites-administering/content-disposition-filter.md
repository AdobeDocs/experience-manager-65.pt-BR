---
title: Filtro de Disposição de Conteúdo
seo-title: Filtro de Disposição de Conteúdo
description: Saiba como usar o Filtro de descarte de conteúdo para evitar ataques de XSS.
seo-description: Saiba como usar o Filtro de descarte de conteúdo para evitar ataques de XSS.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
translation-type: tm+mt
source-git-commit: bb50e530f0d015c0e7d06650157e3e3994082483
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Filtro de Disposição de Conteúdo{#content-disposition-filter}

O filtro de disposição de conteúdo é um recurso de segurança contra ataques XSS em arquivos SVG.

Depois de instalado, o filtro bloqueia o acesso a todos os ativos. Por exemplo, não foi possível visualização um PDF online. Esta seção descreve como configurar o filtro de acordo com suas necessidades.

## Configurar filtro de descarte de conteúdo {#configure-content-disposition-filter}

Você pode visualização o filtro de [Apache Sling Content Disposition no GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

As opções de Filtro de descarte de conteúdo fornecem a seguinte funcionalidade:

* Caminhos de descarte do conteúdo: uma lista de caminhos onde o filtro será aplicado seguido por uma lista de tipos MIME a serem excluídos nesse caminho. Esse caminho deve ser um caminho absoluto e pode conter um curinga (&#39;&amp;ast;&#39;) no final, para corresponder cada caminho de recurso ao prefixo de caminho especificado. Por exemplo: /content/&amp;ast;:image/jpeg,image/svg+xml &quot; aplicará o filtro a todos os nós em /content, exceto imagens jpg e svg

* Caminhos de recursos excluídos: uma lista de recursos excluídos, cada caminho de recurso deve ser fornecido como caminho absoluto e totalmente qualificado. Correspondência de prefixo/curingas não são suportados.

* Ativar Para Todos Os Caminhos De Recurso: esse sinalizador controla se esse filtro deve ser ativado para todos os caminhos, exceto para os caminhos excluídos definidos pelos Caminhos de recursos excluídos. Definir isso como &quot;true&quot; leva a ignorar os Caminhos de Disposição de Conteúdo. Independentemente da configuração, somente os caminhos de recursos são abordados que contêm uma propriedade chamada &#39;jcr:data&#39; ou &#39;jcr:content/jcr:data&#39;.
