---
title: Integrar [!DNL Assets] com o fluxo de atividade
description: Descreve os recursos de gravação de [!DNL Experience Manager] e como configurá-la para registrar eventos específicos.
contentOwner: AG
role: Developer
feature: Asset Management
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---


# Integre [!DNL Assets] ao fluxo de atividade {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] Os usuários executam muitas ações, como criar, carregar e excluir ativos. Essas ações podem ser registradas para que você possa fornecer um histórico do que foi feito por um usuário. Esta seção descreve os recursos de gravação de [!DNL Experience Manager] e como configurar [!DNL Experience Manager] para registrar eventos específicos.

## Considerações de desempenho e comportamento padrão {#performance-considerations-and-default-behavior}

Essa integração pode consumir CPU e espaço em disco, por exemplo, ao fazer importação em massa. Por esses motivos, a integração [!DNL Assets] com o fluxo de atividade é desabilitada por padrão.

## Eventos de ação compatíveis {#supported-action-events}

Os seguintes eventos podem ser configurados para serem registrados:

* Licença aceita (ACEITE)
* Ativo criado (ASSET_CREATED)
* Ativo movido (ASSET_MOVED)
* Ativo removido (ASSET_REMOVED)
* Licença rejeitada (REJEITADA)
* Ativo baixado (BAIXADO)
* Versão do ativo (VERSIONED)
* Versão do ativo restaurada (RESTAURADA)
* Metadados de ativos atualizados (METADATA_UPDATED)
* Ativo publicado no sistema externo (PUBLISHED_EXTERNAL)
* Atualização original do ativo (ORIGINAL_UPDATED)
* Representação de ativo atualizada (RENDITION_UPDATED)
* Representação de ativo removida (RENDITION_REMOVED)
* Subativo atualizado (SUBASSET_UPDATED)
* Subativo removido (SUBASSET_REMOVED)

## Configurar [!DNL Assets] eventos que registram {#configuring-aem-assets-events-recording}

O [console da Web](/help/sites-deploying/configuring-osgi.md) fornece acesso ao ajuste do Gravador de eventos de ativos. Para configurar o Gravador de eventos do Assets, proceda da seguinte maneira:

1. Navegue até **[!UICONTROL Console da Web]**

1. Clique em **[!UICONTROL Configuração]**.

1. Clique duas vezes em **[!UICONTROL Day CQ DAM Event Recorder]**.

1. Marque **[!UICONTROL Habilita este serviço]**.

1. Verifique quais **[!UICONTROL Tipos de evento]** você deseja registrar no fluxo de atividade do usuário.

1. Clique em **[!UICONTROL Salvar]**.

## Ler eventos gravados {#reading-recorded-events}

Os eventos gravados são armazenados como atividades. Você pode lê-las programaticamente usando a [API do ActivityManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
