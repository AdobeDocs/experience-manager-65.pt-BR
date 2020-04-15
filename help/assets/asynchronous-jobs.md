---
title: Operações assíncronas
description: O AEM Assets otimiza o desempenho ao concluir de forma assíncrona algumas tarefas que consomem muitos recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Operações assíncronas {#asynchronous-operations}

Para reduzir o impacto negativo no desempenho, o Adobe Experience Manager (AEM) Assets processa de modo assíncrono determinadas operações de ativos de longa duração e com uso intenso de recursos.

Essas operações incluem:

* Excluindo muitos ativos
* Movimentação de muitos ativos ou ativos com muitas referências
* Exportar/importar metadados de ativos em massa.
* Buscando ativos, que estão acima do limite definido, de uma implantação remota do AEM.

O processamento assíncrono envolve enfileiramento de várias tarefas e, eventualmente, sua execução em série, dependendo da disponibilidade dos recursos do sistema.

Você pode visualização o status de trabalhos assíncronos na página Status **[!UICONTROL do trabalho]** assíncrono.

>[!NOTE]
>
>Por padrão, os trabalhos no AEM Assets são executados em paralelo. Se N for o número de núcleos da CPU, os trabalhos N/2 poderão ser executados em paralelo, por padrão. Para usar configurações personalizadas para a fila de trabalhos, modifique a configuração da Fila **[!UICONTROL padrão de operação]** assíncrona do console da Web. Para obter mais informações, consulte configurações [de](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)fila.

## Monitore o status das operações assíncronas {#monitoring-the-status-of-asynchronous-operations}

Sempre que o AEM Assets processa uma operação de forma assíncrona, você recebe uma notificação na sua caixa de entrada e por email.

Para visualização o status das operações assíncronas em detalhes, navegue até a página Status **[!UICONTROL do trabalho]** assíncrono.

1. Na interface do Experience Manager, clique em **[!UICONTROL Operações]** > **[!UICONTROL Tarefas]**.

1. Na página Status **[!UICONTROL do trabalho]** assíncrono, reveja os detalhes das operações.

   ![Status e detalhes das operações assíncronas](assets/AsyncOperation-status.png)

   Para verificar o progresso de uma operação específica, consulte o valor na coluna **[!UICONTROL Status]** . Dependendo do progresso, um dos seguintes status é exibido:

   * **[!UICONTROL Ativo]**: A operação está sendo processada

   * **[!UICONTROL Sucesso]**: A operação está concluída

   * **[!UICONTROL Falha]** ou **[!UICONTROL erro]**: não foi possível processar a operação

   * **[!UICONTROL Agendado]**: A operação está programada para processamento posterior

1. Para interromper uma operação ativa, selecione-a na lista e clique em **[!UICONTROL Parar]** na barra de ferramentas.

   ![stop_icon](assets/stop_icon.png)

1. Para visualização de detalhes adicionais, por exemplo, descrição e registros, selecione a operação e clique em **[!UICONTROL Abrir]** na barra de ferramentas.

   ![open_icon](assets/open_icon.png)

   A página de detalhes da tarefa é exibida.

   ![job_details](assets/job_details.png)

1. Para excluir a operação da lista, selecione **[!UICONTROL Excluir]** na barra de ferramentas. Para baixar os detalhes em um arquivo CSV, clique em **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >Não é possível excluir um trabalho se seu status estiver ativo ou na fila.

## Expurgar trabalhos concluídos {#purging-completed-jobs}

Os ativos AEM executam um trabalho de limpeza todos os dias às 13:00 da manhã para excluir trabalhos assíncronos concluídos que têm mais de um dia.

Você pode modificar a programação para a ordem de produção de expurgação e a duração para a qual os detalhes das ordens de produção concluídas são retidos antes de serem deletados. Você também pode configurar o número máximo de trabalhos concluídos para os quais os detalhes são retidos a qualquer momento.

1. Na interface do Experience Manager, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da]** Web.
1. Abra o trabalho **[!UICONTROL Adobe CQ DAM Async Jobs para Expurgar agendado]** .
1. Especifique o número limite de dias após o qual as tarefas concluídas são excluídas e o número máximo de trabalhos para os quais os detalhes são mantidos no histórico.

   ![Configuração para agendar a remoção de trabalhos assíncronos](assets/configmgr_purge_asyncjobs.png)

1. Salve as alterações.

## Configurar limites para processamento assíncrono {#configuring-thresholds-for-asynchronous-processing}

Você pode configurar o número limite de ativos ou referências para que os ativos AEM processem uma determinada operação de forma assíncrona.

### Configurar limites para operações de exclusão assíncronas {#configuring-thresholds-for-asynchronous-delete-operations}

Se o número de ativos ou pastas a serem excluídos exceder o número limite, a operação de exclusão será executada de forma assíncrona.

1. Na interface do Experience Manager, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da]** Web.
1. No console da Web, abra a configuração **[!UICONTROL Async Delete Operation Job Processing]** .
1. Na caixa Número **[!UICONTROL limite de ativos]** , especifique o número limite de ativos/pastas para o processamento assíncrono de operações de exclusão.

   ![delete_limit](assets/delete_threshold.png)

1. Salve as alterações.

### Configurar limites para operações de movimentação assíncronas {#configuring-thresholds-for-asynchronous-move-operations}

Se o número de ativos/pastas ou referências a serem movidos exceder o número limite, a operação de movimentação será executada de forma assíncrona.

1. Na interface do Experience Manager, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > Console **[!UICONTROL da]** Web.
1. No console da Web, abra a configuração Processamento **[!UICONTROL de Trabalho da Operação de Movimentação]** Assíncrona.
1. Na caixa Número **[!UICONTROL limite de ativos/referências]** , especifique o número limite de ativos/pastas ou referências para o processamento assíncrono de operações de movimentação.

   ![move_limit](assets/move_threshold.png)

1. Salve as alterações.
