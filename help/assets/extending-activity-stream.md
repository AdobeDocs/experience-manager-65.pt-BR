---
title: Integrar [!DNL Assets] ao fluxo de atividade.
description: Descreve os recursos [!DNL Experience Manager] de gravação de e como configurá-los para gravar eventos específicos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Integrar [!DNL Assets] ao fluxo de atividade {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] os usuários executam várias ações, como criar, carregar e excluir ativos. Essas ações podem ser registradas para que você possa fornecer um histórico do que foi feito por um usuário. Esta seção descreve os recursos de gravação de [!DNL Experience Manager] e como configurar [!DNL Experience Manager] para gravar eventos específicos.

## Considerações de desempenho e comportamento padrão {#performance-considerations-and-default-behavior}

Essa integração pode ser de CPU e de consumo de espaço em disco, por exemplo, ao fazer a importação em massa. Por esses motivos, a integração [!DNL Assets] com o Fluxo de Atividade é desativada por padrão.

## eventos de ação suportados {#supported-action-events}

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

## Configurar gravação de [!DNL Assets] eventos {#configuring-aem-assets-events-recording}

O console [da](/help/sites-deploying/configuring-osgi.md) Web fornece acesso ao ajuste do Gravador do Evento Assets. Para configurar o Gravador de Eventos de Ativos, proceda da seguinte maneira:

1. Navegue até o Console **[!UICONTROL da Web]**

1. Clique em **[!UICONTROL Configuração]**.

1. Duplo clique em Gravador **[!UICONTROL do Evento]** Day CQ DAM.

1. Marcar **[!UICONTROL Ativa este serviço]**.

1. Verifique quais **[!UICONTROL Tipos de evento]** você deseja que sejam registrados no fluxo de atividade do usuário.

1. Clique em **[!UICONTROL Salvar]**.

## Ler eventos gravados {#reading-recorded-events}

Os eventos gravados são armazenados como atividades. Você pode lê-los de forma programática usando a API [do](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)Activity Manager.
