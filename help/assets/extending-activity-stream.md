---
title: Integrar [!DNL Assets] com fluxo de atividade
description: Descreve os recursos de gravação de [!DNL Experience Manager] e como configurá-lo para registrar eventos específicos.
contentOwner: AG
role: Developer
feature: Asset Management
exl-id: 2a08a7c1-8be9-42d1-9983-f9c8b12ea4e8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Integrar [!DNL Assets] com fluxo de atividade {#integrating-assets-with-activity-stream}

[!DNL Adobe Experience Manager Assets] Os usuários do executam muitas ações, como criar, fazer upload e excluir ativos. Essas ações podem ser registradas para que você possa fornecer um histórico do que foi feito por um usuário. Esta seção descreve os recursos de gravação de [!DNL Experience Manager] e como configurar [!DNL Experience Manager] para registrar eventos específicos.

## Considerações sobre o desempenho e comportamento padrão {#performance-considerations-and-default-behavior}

Essa integração pode consumir CPU e espaço em disco, por exemplo, ao fazer uma importação em massa. Por estes motivos, a [!DNL Assets] a integração com o Fluxo de atividades é desabilitada por padrão.

## Eventos de ação compatíveis {#supported-action-events}

Os seguintes eventos podem ser configurados para serem gravados:

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

## Configurar [!DNL Assets] gravação de eventos {#configuring-aem-assets-events-recording}

A variável [Console da Web](/help/sites-deploying/configuring-osgi.md) O fornece acesso ao ajuste do Gravador de eventos do Assets. Para configurar o Gravador de eventos do Assets, proceda da seguinte maneira:

1. Navegue até a **[!UICONTROL Console da Web]**

1. Clique em **[!UICONTROL Configuração]**.

1. Clique duas vezes **[!UICONTROL Gravador de eventos DAM CQ do dia]**.

1. Marcar **[!UICONTROL Habilita este serviço]**.

1. Verificar qual **[!UICONTROL Tipos de evento]** você deseja ser registrado no fluxo de atividade do usuário.

1. Clique em **[!UICONTROL Salvar]**.

## Ler eventos gravados {#reading-recorded-events}

Os eventos registrados são armazenados como atividades. Você pode lê-los programaticamente usando o [API do ActivityManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/activitystreams/ActivityManager.html).
