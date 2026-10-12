---
title: Integrar [!DNL Assets] ao fluxo de atividade
description: Descreve os recursos de gravação de [!DNL Experience Manager] e como configurá-los para gravar eventos específicos.
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%
---
# Integrar [!DNL Assets] ao fluxo de atividade {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] usuários executam muitas ações, como criar, carregar e excluir o Assets. Essas ações podem ser registradas para que você possa fornecer um histórico do que foi feito por um usuário. Esta seção descreve os recursos de gravação de [!DNL Experience Manager] e como configurar [!DNL Experience Manager] para gravar eventos específicos.

## Considerações sobre o desempenho e comportamento padrão {#performance-considerations-and-default-behavior}

Essa integração pode consumir espaço em disco e CPU, por exemplo, ao fazer uma importação em massa. Por esses motivos, a integração [!DNL Assets] com o Fluxo de atividades é desabilitada por padrão.

## Eventos de ação compatíveis {#supported-action-events}

Você pode configurar os seguintes eventos a serem gravados:

* Licença aceita (ACEITA)
* Ativo criado (ASSET_CREATED)
* Ativo movido (ASSET_MOVED)
* Ativo removido (ASSET_REMOVED)
* Licença rejeitada (REJEITADA)
* Ativo baixado (BAIXADO)
* Versão do ativo (VERSIONED)
* Versão do ativo restaurada (RESTAURADA)
* Metadados de ativos atualizados (METADATA_UPDATED)
* Ativo publicado no sistema externo (PUBLISHED_EXTERNAL)
* Original do ativo atualizado (ORIGINAL_UPDATED)
* Representação de ativo atualizada (RENDITION_UPDATED)
* Representação de ativo removida (RENDITION_REMOVED)
* Subativo atualizado (SUBASSET_UPDATED)
* Subativo removido (SUBASSET_REMOVED)

## Configurar a gravação de eventos do [!DNL Assets] {#configuring-aem-assets-events-recording}

O [console da Web](/help/sites-deploying/configuring-osgi.md) fornece acesso ao ajuste do Gravador de Eventos do Assets. Para configurar o Gravador de eventos do Assets, proceda da seguinte maneira:

1. Navegue até o **[!UICONTROL Console da Web]**

1. Clique em **[!UICONTROL Configuração]**.

1. Clique duas vezes em **[!UICONTROL Gravador de eventos DAM do Day CQ]**.

1. Verificar **[!UICONTROL Habilita este serviço]**.

1. Verifique quais **[!UICONTROL Tipos de Evento]** você deseja registrar no fluxo de atividades do usuário.

1. Clique em **[!UICONTROL Salvar]**.

## Ler eventos gravados {#reading-recorded-events}

Os eventos registrados são armazenados como atividades. Você pode lê-las programaticamente usando a [API do ActivityManager](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
