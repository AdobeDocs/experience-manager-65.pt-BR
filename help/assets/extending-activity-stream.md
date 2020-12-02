---
title: Integrar [!DNL Assets] com fluxo de atividade
description: Descreve os recursos de gravação de [!DNL Experience Manager] e como configurá-los para gravar eventos específicos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Integrar [!DNL Assets] ao fluxo de atividade {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] os usuários executam várias ações, como criar, carregar e excluir ativos. Essas ações podem ser registradas para que você possa fornecer um histórico do que foi feito por um usuário. Esta seção descreve os recursos de gravação de [!DNL Experience Manager] e como configurar [!DNL Experience Manager] para gravar eventos específicos.

## Considerações de desempenho e comportamento padrão {#performance-considerations-and-default-behavior}

Essa integração pode ser de CPU e de consumo de espaço em disco, por exemplo, ao fazer a importação em massa. Por esses motivos, a integração [!DNL Assets] com o Fluxo de Atividade está desabilitada por padrão.

## Eventos de ação suportados {#supported-action-events}

Os seguintes eventos podem ser configurados para serem gravados:

* Licença aceita (ACEITE)
* Ativo criado (ASSET_CREATED)
* Ativo movido (ASSET_MOVED)
* Ativo removido (ASSET_REMOVED)
* Licença rejeitada (REJEITADA)
* Ativo baixado (BAIXADO)
* Versão do ativo (VERSÃO)
* Versão do ativo restaurada (RESTAURADA)
* Metadados do ativo atualizados (METADATA_UPDATED)
* Ativo publicado no sistema externo (PUBLISHED_EXTERNAL)
* Atualização original do ativo (ORIGINAL_UPDATED)
* Renderização de ativo atualizada (RENDITION_UPDATED)
* Renderização de ativo removida (RENDITION_REMOVED)
* Subativo atualizado (SUBASSET_UPDATED)
* Subativo removido (SUBASSET_REMOVED)

## Configurar [!DNL Assets] eventos gravando {#configuring-aem-assets-events-recording}

O [console Web](/help/sites-deploying/configuring-osgi.md) fornece acesso ao ajuste do Gravador de Eventos de Ativos. Para configurar o Gravador de Eventos de Ativos, proceda da seguinte maneira:

1. Navegue até **[!UICONTROL Console Web]**

1. Clique em **[!UICONTROL Configuração]**.

1. Clique no duplo **[!UICONTROL Gravador de Evento do Day CQ DAM]**.

1. Marcar **[!UICONTROL Habilita este serviço]**.

1. Verifique quais **[!UICONTROL Tipos de evento]** você deseja que sejam gravados no fluxo de atividade do usuário.

1. Clique em **[!UICONTROL Salvar]**.

## Ler eventos gravados {#reading-recorded-events}

Os eventos gravados são armazenados como atividades. Você pode lê-los de forma programática usando a [API do Activity Manager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
