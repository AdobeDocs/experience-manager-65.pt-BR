---
title: Fluxo de atividade na linha do tempo
description: Este artigo descreve como exibir registros de atividades para ativos na linha do tempo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Fluxo de atividade na linha do tempo {#activity-stream-in-timeline}

Este recurso exibe os registros de atividades dos ativos na linha do tempo. Se você executar qualquer uma das seguintes operações relacionadas a ativos nos ativos Adobe Experience Manager (AEM), o recurso de fluxo de atividades atualizará a linha do tempo para refletir a atividade.

As seguintes operações são registradas no fluxo de atividades:

* Criar
* Excluir
* Download (incluindo execuções)
* Publicação
* Cancelar publicação
* Aprovar
* Rejeitar
* Mover

Os registros de atividades a serem exibidos na linha do tempo são obtidos do local `/var/audit/com.day.cq.dam/content/dam` no CRX, onde os arquivos de log são armazenados.  Além disso, a atividade da linha do tempo é registrada quando novos ativos são carregados ou os ativos existentes são modificados e verificados no AEM por meio do [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) ou do aplicativo [de desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)AEM.

>[!NOTE]
>
>Fluxos de trabalho transitórios não são exibidos na linha do tempo, pois nenhuma informação de histórico é salva para esses fluxos de trabalho.

Para exibir o fluxo de atividade, execute uma ou mais operações no ativo, selecione o ativo e escolha **[!UICONTROL Linha do tempo]** na lista GlobalNav.

![linha do tempo 2](assets/timeline-2.png)

A linha do tempo exibe o fluxo de atividade para as operações que você executa nos ativos.

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>O local de armazenamento de log padrão para as tarefas **[!UICONTROL Publicar]** e **[!UICONTROL Cancelar publicação]** é `/var/audit/com.day.cq.replication/content`. Para tarefas **[!UICONTROL Mover]** , o local padrão é `/var/audit/com.day.cq.wcm.core.page`.
