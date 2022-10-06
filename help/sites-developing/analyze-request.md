---
title: Script de análise de solicitação
seo-title: Request Analysis Script
description: O script de análise de solicitação é feito para facilitar a análise dos arquivos access.log produzindo um relatório legível para processamento posterior
seo-description: The request analysis script is made to ease the analysis of the access.log files producing a readable report for later processing
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# Script de análise de solicitação{#request-analysis-script}

## Download {#download}

Esse script é feito para facilitar a análise da variável `access.log` arquivos que geram um relatório legível para processamento posterior.

[Obter arquivo](assets/analyse-access.sh)

## Descrição {#description}

Esse script é feito para facilitar a análise da variável `access.log` arquivos que geram um relatório legível para processamento posterior.

Ele produz o número geral de solicitações, o GET vs POST, a distribuição de solicitações ao longo do tempo e muito mais.

A saída está na sintaxe do Markdown, portanto, será mais fácil convertê-la em PDF com ferramentas como pandoc ou exibi-la em um navegador com plug-ins como o visualizador do Markdown.

Ele pode analisar um caminho personalizado fornecido na linha de comando.

Retirando do comentário dentro do arquivo que informa como executá-lo:

Analisar CQ `access.log` extrapolação de várias informações e produção de uma saída do Markdown em `stdout`.

## Uso {#usage}

`./analyse-access.sh access.log.2013-&ast;`

você pode fornecer caminhos personalizados adicionais para analisar na linha de comando

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

você pode salvar a saída por uma simples tubulação

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
