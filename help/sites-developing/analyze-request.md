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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 2%
---
# Script de análise de solicitação{#request-analysis-script}

## Download {#download}

Este script é feito para facilitar a análise dos arquivos `access.log`, produzindo um relatório legível para processamento posterior.

[Obter arquivo](assets/analyse-access.sh)

## Descrição {#description}

Este script é feito para facilitar a análise dos arquivos `access.log`, produzindo um relatório legível para processamento posterior.

Ele produz o número geral de solicitações, GET vs POST, Distribuição de solicitações ao longo do tempo e muito mais.

A saída está na sintaxe do Markdown, portanto, será mais fácil convertê-la em PDFs com ferramentas como o pandoc ou mostrá-la em um navegador com plug-ins como o visualizador do Markdown.

Ele pode analisar um caminho personalizado fornecido na linha de comando.

A partir do comentário dentro do arquivo que informa como executá-lo:

Analisar CQ `access.log` extrapolando várias informações e produzindo uma saída do Markdown em `stdout`.

## Uso {#usage}

`./analyse-access.sh access.log.2013-&ast;`

você pode fornecer caminhos personalizados adicionais para analisar na linha de comando

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

você pode salvar a saída usando um encanamento simples

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
