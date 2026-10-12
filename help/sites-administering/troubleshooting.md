---
title: Trabalhar com logs
description: Saiba como solucionar problemas do AEM trabalhando com logs.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: ab4fc41f-e0e9-4577-aab2-f0b4298f9a59
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%
---
# Trabalhar com logs{#working-with-logs}

Esta seção inclui informações detalhadas sobre logs disponíveis para ajudar a solucionar problemas.

>[!NOTE]
>
>Para obter mais informações sobre logs, consulte:
>
>* [Manutenção do Log de Auditoria no AEM](/help/sites-administering/operations-audit-log.md)
>* [Trabalhando com Registros de Auditoria e Arquivos de Log](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)

O CRX registra logs detalhados. Depois de descompactar e iniciar o Quickstart, você pode encontrar logs nos seguintes locais:

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## Ativando o Nível de Log DEBUG {#activating-the-debug-log-level}

O nível de log padrão é INFO, ou seja, as mensagens DEBUG não são registradas.

Para ativar o nível de log DEBUG, use o explorador do CRX para definir o

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

propriedade a ser depurada. Não deixe o log no nível de log DEBUG mais tempo do que o necessário, pois ele gera vários logs.

Uma linha no arquivo de depuração geralmente começa com DEBUG e, em seguida, fornece o nível de log, a ação do instalador e a mensagem de log. Por exemplo:

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Os níveis de log são os seguintes:

| 0 | Erro fatal | A ação falhou e o instalador não pode continuar. |
|---|---|---|
| 1 | Erro | Falha na ação. A instalação continua, mas uma parte do CRX não foi instalada corretamente e não funcionará. |
| 2 | Aviso | A ação foi bem-sucedida, mas encontrou problemas. O CRX pode ou não funcionar corretamente. |
| 3 | Informações | A ação foi bem-sucedida. |

## Opção detalhada usada para solução de problemas {#verbose-option-used-for-troubleshooting}

Ao iniciar o CRX, você pode adicionar a opção -v (detalhada) à linha de comando como em:

` java -jar crx-<*version*>-<*edition*>.jar -v`

Use a opção detalhada para solução de problemas, pois essa opção exibe parte da saída de registro de início rápido no console.
