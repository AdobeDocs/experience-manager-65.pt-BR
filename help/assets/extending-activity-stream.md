---
title: Integrar ativos ao fluxo de atividade
description: Descreve os recursos de gravação do AEM e como configurar o AEM para gravar eventos específicos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Integrar ativos ao fluxo de atividade {#integrating-assets-with-activity-stream}

Os usuários do Adobe Experience Manager (AEM) Assets executam várias ações, como criar, carregar e excluir ativos. Essas ações podem ser registradas para que você possa fornecer um histórico do que foi feito por um usuário. Esta seção descreve os recursos de gravação do AEM e como configurar o AEM para gravar eventos específicos.

## Considerações de desempenho e comportamento padrão {#performance-considerations-and-default-behavior}

Essa integração pode ser de CPU e de consumo de espaço em disco, por exemplo, ao fazer a importação em massa. Por esses motivos, a integração dos ativos AEM com o fluxo de atividade é desativada por padrão.

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

## Configurar a gravação de eventos do AEM Assets {#configuring-aem-assets-events-recording}

O console [da](/help/sites-deploying/configuring-osgi.md) Web fornece acesso ao ajuste do Gravador de eventos dos ativos AEM. Para configurar o Gravador de eventos do AEM Assets, proceda da seguinte maneira:

1. Navegue até o Console **[!UICONTROL da Web]**

1. Clique em **[!UICONTROL Configuração]**.

1. Clique duas vezes em Gravador **[!UICONTROL de eventos CQ DAM do]** dia.

1. Marcar **[!UICONTROL Ativa este serviço]**.

1. Verifique quais tipos **[!UICONTROL de]** evento você deseja que sejam registrados no fluxo de atividade do usuário.

1. Clique em **[!UICONTROL Salvar]**.

## Ler eventos gravados {#reading-recorded-events}

Os eventos gravados são armazenados como atividades. Você pode lê-los de forma programática usando a API [do](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html)Activity Manager.
