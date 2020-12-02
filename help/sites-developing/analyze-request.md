---
title: Script de Análise de solicitação
seo-title: Script de Análise de solicitação
description: O script de análise de solicitação é feito para facilitar a análise dos arquivos access.log, produzindo um relatório legível para processamento posterior
seo-description: O script de análise de solicitação é feito para facilitar a análise dos arquivos access.log, produzindo um relatório legível para processamento posterior
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 1%

---


# Script de Análise de solicitação{#request-analysis-script}

## Download {#download}

Esse script é feito para facilitar a análise dos arquivos `access.log` que produzem um relatório legível para processamento posterior.

[Obter arquivo](assets/analyse-access.sh)

## Descrição {#description}

Esse script é feito para facilitar a análise dos arquivos `access.log` que produzem um relatório legível para processamento posterior.

Produz o número geral de solicitações, GET vs POST, distribuição de solicitações ao longo do tempo e muito mais.

A saída está na sintaxe de Marcação, portanto, será mais fácil convertê-la em PDFs com ferramentas como pandoc ou exibi-la em um navegador com plug-ins como o Visualizador de Marcação.

Ele pode analisar um caminho personalizado fornecido na linha de comando.

Retirando do comentário dentro do arquivo que informa como executá-lo:

Analise o CQ `access.log` extrapolando várias informações e produzindo uma saída de Markdown em `stdout`.

## Uso {#usage}

`./analyse-access.sh access.log.2013-&ast;`

você pode fornecer caminhos personalizados adicionais para analisar na linha de comando

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

é possível salvar a saída por uma simples tubulação

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
