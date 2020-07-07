---
title: Configure operações assíncronas [!DNL Adobe Experience Manager].
description: Conclua de forma assíncrona algumas tarefas que consomem muitos recursos para otimizar o desempenho [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 2%

---


# Operações assíncronas {#asynchronous-operations}

Para reduzir o impacto adverso no desempenho, [!DNL Adobe Experience Manger Assets] processa de forma assíncrona determinadas operações de ativos de longa duração e de uso intensivo de recursos. O processamento assíncrono envolve enfileirar várias tarefas e, eventualmente, executá-las de forma serial, dependendo da disponibilidade de recursos do sistema. Essas operações incluem:

* Excluindo muitos ativos.
* Movimentação de muitos ativos ou ativos com muitas referências.
* Exportar e importar metadados de ativos em massa.
* Buscando ativos de uma [!DNL Experience Manager] implantação remota, que são mais do que um limite definido. O limite está no número de ativos.

Você pode visualização o status de tarefas assíncronas na página Status **[!UICONTROL do trabalho]** assíncrono.

>[!NOTE]
>
>Por padrão, as [!DNL Assets] tarefas são executadas em paralelo. Se `N` for o número de núcleos da CPU, o `N/2` tarefa pode executar simultaneamente, por padrão. Para usar configurações personalizadas para a fila de tarefas, modifique a configuração da Fila **[!UICONTROL padrão de operação]** assíncrona do console [!UICONTROL da]Web. Para obter mais informações, consulte configurações [de](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)fila.

## Monitore o status das operações assíncronas {#monitoring-the-status-of-asynchronous-operations}

Sempre que [!DNL Assets] processar uma operação de forma assíncrona, você receberá uma notificação em sua [!DNL Experience Manager] Caixa de [entrada](/help/sites-authoring/inbox.md) e por email. Para visualização o status das operações assíncronas em detalhes, navegue até a página Status **[!UICONTROL do trabalho]** assíncrono.

1. Na [!DNL Experience Manager] interface, clique em **[!UICONTROL Operações]** > **[!UICONTROL Tarefas]**.

1. Na página Status **[!UICONTROL do trabalho]** assíncrono, reveja os detalhes das operações.

   ![Status e detalhes das operações assíncronas](assets/AsyncOperation-status.png)

   Para verificar o progresso de uma operação, consulte a coluna **[!UICONTROL Status]** . Dependendo do progresso, um dos seguintes status é exibido:

   * **[!UICONTROL Ativo]**: A operação está sendo processada.
   * **[!UICONTROL Sucesso]**: A operação está concluída.
   * **[!UICONTROL Falha]** ou **[!UICONTROL erro]**: não foi possível processar a operação.
   * **[!UICONTROL Agendado]**: A operação está programada para processamento posterior.

1. Para interromper uma operação ativa, selecione-a na lista e clique no ícone **[!UICONTROL Parar]** ![parar](assets/do-not-localize/stop_icon.svg) na barra de ferramentas.

1. Para visualização de detalhes adicionais, por exemplo, descrição e registros, selecione a operação e clique em **[!UICONTROL Abrir]** ![open_icon](assets/do-not-localize/edit_icon.svg) na barra de ferramentas. A página de detalhes da tarefa é exibida.

   ![Detalhes de uma tarefa de importação de metadados](assets/job_details.png)

1. Para excluir a operação da lista, selecione **[!UICONTROL Excluir]** na barra de ferramentas. Para baixar os detalhes em um arquivo CSV, clique em **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >Não é possível excluir uma tarefa se seu status estiver ativo ou na fila.

## Limpar tarefas concluídas {#purge-completed-tasks}

[!DNL Experience Manager Assets] executa uma tarefa de expurgação todos os dias às 100 horas para excluir tarefas assíncronas concluídas com mais de um dia de idade.

<!-- TBD: Find out from the engineering team and mention the time zone of this 1:00 am task.
-->

Você pode modificar a programação para a tarefa de expurgação e a duração para a qual os detalhes das tarefas concluídas são retidos antes de serem excluídas. Você também pode configurar o número máximo de tarefas concluídas para as quais os detalhes são retidos a qualquer momento.

1. Na [!DNL Experience Manager] interface, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da Web]**.
1. Abra a tarefa Programada **[!UICONTROL de Expurgação de tarefas assíncronas do]** Adobe CQ DAM.
1. Especifique o número limite de dias após os quais as tarefas concluídas são excluídas e o número máximo de tarefas para as quais os detalhes são mantidos no histórico. Salve as alterações.

   ![Configuração para agendar a remoção de tarefas assíncronas](assets/configmgr_purge_asyncjobs.png)

## Configurar limite para operações de exclusão assíncronas {#configure-thresholds-for-asynchronous-delete-operations}

Se o número de ativos ou pastas a serem excluídos exceder o número limite definido, a operação de exclusão será executada de forma assíncrona.

1. Na [!DNL Experience Manager] interface, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da Web]**.
1. No Console [!UICONTROL da]Web, abra a configuração Processamento **[!UICONTROL de Trabalho da Operação de Exclusão]** Assíncrona.
1. Na caixa Número **[!UICONTROL limite de ativos]** , especifique os números limite para excluir ativos, pastas ou referências de forma assíncrona. Salve as alterações.

   ![Definir o limite para a tarefa excluir ativos](assets/delete_threshold.png)

## Configurar limite para operações de movimentação assíncronas {#configure-thresholds-for-asynchronous-move-operations}

Se o número de ativos, pastas ou referências a serem movidos exceder o número limite definido, a operação de movimentação será executada de forma assíncrona.

1. Na [!DNL Experience Manager] interface, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da Web]**.
1. No Console Web, abra a configuração Processamento **[!UICONTROL de Trabalho da Operação de Movimentação]** Assíncrona.
1. Na caixa Número **[!UICONTROL limite de ativos/referências]** , especifique os números limite para mover ativos, pastas ou referências de forma assíncrona. Salve as alterações.

   ![Definir o limite de tarefa para mover ativos](assets/move_threshold.png)

>[!MORELIKETHIS]
>
>* [Configure e-mail no Experience Manager](/help/sites-administering/notification.md).
>* [Importe e exporte metadados de ativos em massa](/help/assets/metadata-import-export.md).
>* [Use Ativos conectados para compartilhar ativos DAM de implantações](/help/assets/use-assets-across-connected-assets-instances.md)remotas.

