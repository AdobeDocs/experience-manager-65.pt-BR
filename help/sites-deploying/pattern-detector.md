---
title: Avaliação da complexidade da atualização com o detector de padrões
seo-title: Avaliação da complexidade da atualização com o detector de padrões
description: Saiba como usar o Detector de padrão para avaliar a complexidade da atualização.
seo-description: Saiba como usar o Detector de padrão para avaliar a complexidade da atualização.
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
translation-type: tm+mt
source-git-commit: d510decba9b2af23bab54c78779f98a36a6172d4
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 1%

---


# Avaliação da complexidade da atualização com o detector de padrões

## Visão geral {#overview}

Este recurso permite verificar as instâncias AEM existentes quanto à sua capacidade de atualização, detectando padrões em uso que:

1. Violar certas regras e são feitas em áreas que serão afetadas ou substituídas pela atualização
1. Use um recurso AEM 6.x ou uma API que não seja compatível com versões anteriores no AEM 6.5 e que possa ser interrompida após a atualização.

Tal poderia servir de avaliação do esforço de desenvolvimento que está envolvido na atualização para a AEM 6.5.

## Como configurar {#how-to-set-up}

O Detector de padrão é lançado separadamente como um [único pacote](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/pd-all-aem65) que funciona em qualquer versão de AEM de origem da 6.1 para a 6.5, visando AEM atualização 6.5. Ele pode ser instalado usando o Gerenciador [de pacotes](/help/sites-administering/package-manager.md).

## Como usar {#how-to-use}

>[!NOTE]
>
>O Detector de padrão pode ser executado em qualquer ambiente, incluindo instâncias de desenvolvimento local. No entanto, para:
>
>* aumentar a taxa de detecção
>* evitar qualquer lentidão em instâncias críticas para os negócios

>
>
ao mesmo tempo, é recomendável executá-lo **em ambientes** de preparo que estejam o mais próximos possível dos de produção nas áreas de aplicativos, conteúdo e configurações do usuário.

Você pode usar vários métodos para verificar a saída do Detector de padrão:

* **Através do console Inventário Felix:**

1. Vá para o Console da Web AEM navegando até *https://serveraddress:serverport/system/console/configMgr*
1. Selecionar **status - Detector** de padrão, conforme mostrado na imagem abaixo:

   ![screenshot-2018-2-5detector de padrões](assets/screenshot-2018-2-5pattern-detector.png)

* **Por meio de uma interface JSON comum ou baseada em texto reativo**
* **Por meio de uma interface de linhas JSON reativa, **que gera um documento JSON separado em cada linha.

Ambos os métodos estão detalhados abaixo:

## Interface reativa {#reactive-interface}

A interface reativa permite o processamento do relatório de violação assim que uma suspeita é detectada.

A saída está disponível atualmente em 2 URLs:

1. Interface de texto sem formatação
1. Interface JSON

## Manuseio da interface de texto simples {#handling-the-plain-text-interface}

As informações na saída são formatadas como uma série de entradas de evento. Há dois canais - um para violações de publicação e o segundo para publicar o progresso atual.

Eles podem ser obtidos usando os seguintes comandos:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

A saída será parecida com esta:

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

O progresso pode ser filtrado usando o `grep` comando:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

O que resulta na seguinte saída:

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## Manuseio da interface JSON {#handling-the-json-interface}

Da mesma forma, o JSON pode ser processado usando a ferramenta [](https://stedolan.github.io/jq/) jq assim que for publicado.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

Com a saída:

```
{
  "timestamp": "2018-02-13T14:20:18.894+01:00",
  "suspicion": true,
  "pattern": {
    "code": "ECU",
    "type": "extraneous.content.usage",
    "detective": "ContentAccessDetector",
    "moreInfo": "https://www.adobe.com/go/aem6_ECU"
  },
  "item": {
    "id": "a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f",
    "message": "Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid"
  }
}
```

O progresso é relatado a cada 5 segundos e pode ser obtido excluindo outras mensagens além daquelas marcadas como suspeitas:

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

Com a saída:

```
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:17.279+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 57209,
    "itemsAnalysedSize": "26 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT5.003S",
    "elapsedTimeMilliseconds": 5003,
    "itemsPerSecond": 36965
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:22.276+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 113194,
    "itemsAnalysedSize": "46 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT10S",
    "elapsedTimeMilliseconds": 10000,
    "itemsPerSecond": 24092
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:25.762+01:00",
  "type": "FINISHED",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 140744,
    "itemsAnalysedSize": "63 MB",
    "suspicionsFound": 1
  },
  "progress": {
    "elapsedTime": "PT13.486S",
    "elapsedTimeMilliseconds": 13486,
    "itemsPerSecond": 19907
  }
}
{
  "suspicion": false,
  "type": "SUMMARY",
  "suspicionsFound": 1,
  "totalTime": "PT13.487S"
}
```

>[!NOTE]
>
>A abordagem recomendada é salvar toda a saída do ondulado no arquivo e, em seguida, processá-la por meio `jq` ou `grep` para filtrar o tipo de informação.

## Âmbito de detecção {#scope}

Atualmente, o Detector de padrão permite verificar:

* Incompatibilidade entre exportações e importações de pacotes OSGi
* Como soltar tipos de recursos e supertipos (com sobreposições de conteúdo de caminho de pesquisa)
* definições de índices Oak (compatibilidade)
* Embalagens VLT (utilização excessiva)
* rep:compatibilidade de nós do usuário (no contexto da configuração OAuth)

>[!NOTE]
>
>Observe que o Detector de padrão tenta prever com precisão os avisos para atualização. No entanto, pode gerar falsos positivos em alguns cenários.
