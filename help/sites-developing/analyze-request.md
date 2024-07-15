---
title: Script de análise de solicitação
description: O script de análise de solicitação é feito para facilitar a análise dos arquivos access.log, produzindo um relatório legível para processamento posterior
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# Script de análise de solicitação{#request-analysis-script}

## Download {#download}

Este script é feito para facilitar a análise dos arquivos `access.log`, produzindo um relatório legível para processamento posterior.

[Obter arquivo](assets/analyse-access.sh)

## Descrição {#description}

Este script é feito para facilitar a análise dos arquivos `access.log`, produzindo um relatório legível para processamento posterior.

Ele produz o número geral de solicitações, GET vs. POST, a distribuição de Solicitações ao longo do tempo e muito mais.

A saída está na sintaxe do Markdown, portanto, será mais fácil convertê-la em PDF com ferramentas como pandoc ou mostrá-la em um navegador com plug-ins como o visualizador do Markdown.

Ele pode analisar um caminho personalizado fornecido na linha de comando.

A partir do comentário dentro do arquivo que informa como executá-lo:

Analisar CQ `access.log` extrapolando várias informações e produzindo uma saída do Markdown em `stdout`.

## Uso {#usage}

`./analyse-access.sh access.log.2013-&ast;`

você pode fornecer caminhos personalizados adicionais para analisar na linha de comando

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

você pode salvar a saída usando um encanamento simples

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
