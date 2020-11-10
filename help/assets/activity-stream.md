---
title: Atividade de ativos digitais na visualização da linha do tempo
description: Este artigo descreve como exibir registros de atividades para ativos na linha do tempo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 23%

---


# Atividade na linha do tempo {#activity-stream-in-timeline}

Este recurso exibe registros de atividades para ativos na linha do tempo. Se você executar qualquer uma das seguintes operações relacionadas a ativos em [!DNL Adobe Experience Manager Assets], o recurso de fluxo de atividade atualizará a linha do tempo para refletir a atividade.

As seguintes operações são registradas no fluxo de atividade:

* Criar
* Excluir
* Download (incluindo execuções)
* Publicação
* Desfazer publicação
* Aprovar
* Rejeitar
* Mover

Os registros de atividades a serem exibidos na linha do tempo são obtidos do local `/var/audit/com.day.cq.dam/content/dam` no CRX, onde os arquivos de registro são armazenados. In addition, timeline activity is logged when new assets are uploaded or existing asses are modified and checked into [!DNL Experience Manager] via [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) or [Experience Manager desktop app](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>Workflows transitórios não são exibidos na linha do tempo, pois nenhuma informação de histórico é salva para esses workflows.

Para visualização do fluxo de atividade, execute uma ou mais operações no ativo, selecione o ativo e escolha **[!UICONTROL Linha]** do tempo na lista GlobalNav.

![linha do tempo 2](assets/timeline-2.png)

A linha do tempo exibe o fluxo de atividade para as operações que você executa nos ativos.

![atividade_stream](assets/activity_stream.png)

>[!NOTE]
>
>O local de armazenamento de log padrão das tarefas **[!UICONTROL Publicar]** e **[!UICONTROL Cancelar publicação]** é `/var/audit/com.day.cq.replication/content`. Para tarefas **[!UICONTROL Mover]**, o local padrão é `/var/audit/com.day.cq.wcm.core.page`.
