---
title: Trabalhar com registros
seo-title: Trabalhar com registros
description: Saiba como solucionar problemas de AEM trabalhando com registros.
seo-description: Saiba como solucionar problemas de AEM trabalhando com registros.
uuid: af8b7f50-c8d4-4760-9f00-3feb0b79ee4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: da92d751-6f14-4512-9d77-7ecf098bd58e
docset: aem65
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 3%

---


# Trabalhar com Logs{#working-with-logs}

Esta seção inclui informações detalhadas sobre registros disponíveis para ajudá-lo a solucionar problemas.

O CRX registra registros detalhados. Depois de desempacotar e start Quickstart, você pode encontrar registros nos seguintes locais:

* crx-quickstart/launch/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## Ativando o nível de log DEBUG {#activating-the-debug-log-level}

O nível de log padrão é INFO, ou seja, as mensagens DEBUG não são registradas.

Para ativar o nível de log DEBUG, use o explorador CRX para definir a variável

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

propriedade para depurar. Não deixe o log no nível de log DEBUG mais tempo do que o necessário, pois ele gera muitos logs.

Uma linha no arquivo de depuração geralmente é start com DEBUG e, em seguida, fornece o nível de log, a ação do instalador e a mensagem de log. Por exemplo:

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Os níveis de log são os seguintes:

| 0 | Erro fatal | A ação falhou e o instalador não pode continuar. |
|---|---|---|
| 1 | Erro | A ação falhou. A instalação continua, mas uma parte do CRX não foi instalada corretamente e não funcionará. |
| 2 | Aviso | A ação foi bem-sucedida, mas encontrou problemas. O CRX pode ou não funcionar corretamente. |
| 3 | Info | A ação foi bem sucedida. |

## Opção detalhada usada para solucionar problemas {#verbose-option-used-for-troubleshooting}

Ao start do CRX, você pode adicionar a opção -v (verbose) à linha de comando como em:

` java -jar crx-<*version*>-<*edition*>.jar -v`

Use a opção detalhada para solução de problemas, pois essa opção exibe algumas das saídas do log de início rápido no console.