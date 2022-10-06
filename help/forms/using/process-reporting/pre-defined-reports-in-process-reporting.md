---
title: Relatórios predefinidos em Relatório de Processo
seo-title: Pre-defined reports in Process Reporting
description: Consulte AEM Forms nos dados do processo JEE para criar relatórios em processos de longa execução, duração do processo e volume de fluxo de trabalho
seo-description: Query for AEM Forms on JEE process data to create reports on long running processes, Process duration, and Workflow volume
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# Relatórios predefinidos em Relatório de Processo {#pre-defined-reports-in-process-reporting}

## Relatórios predefinidos em andamento {#pre-defined-reports-in-process-reporting-1}

O AEM Forms Process Reporting é enviado com o seguinte *pronto para uso* relatórios:

* **[Processos de Longa Execução](#long-running-processes)**: Um relatório de todos os processos do AEM Forms que levaram mais de um tempo especificado para serem concluídos
* **[Gráfico de Duração do Processo](#process-duration-report)**: Um relatório de um processo AEM Forms especificado por duração
* **[Volume do fluxo de trabalho](#workflow-volume-report)**: Um relatório das instâncias em execução e concluídas do processo especificado por data

## Processos de Longa Execução {#long-running-processes}

O relatório Long Running Processes exibe os processos do AEM Forms que levaram mais de um tempo especificado para serem concluídos.

### Para executar um relatório de Processo de Execução Longa {#to-execute-a-long-running-process-report}

1. Para exibir a lista de relatórios predefinidos em Relatórios do Processo, no **Relatório de processos** exibição em árvore, clique no botão **Relatórios** nó .
1. Clique no botão **Processos de Longa Execução** nó do relatório.

   ![long_running_node](assets/long_running_node.png)

   Ao selecionar um relatório, a variável **Parâmetros do relatório** é exibido à direita da visualização em árvore.

   ![painel de parâmetros de relatório de processos de execução longa](assets/report_parameters_panel.png)

   Parâmetros:

   * **Duração** (*mandatory*): Especifique uma duração e uma unidade de tempo. Exibe todos os processos do AEM Forms que foram executados por mais do que a duração especificada.
   * **Iniciado após** (*opcional*): Selecione uma data. Filtre o relatório para exibir instâncias de processo que começaram após a data especificada.
   * **Iniciado antes** (*opcional*): Selecione uma data. Filtre o relatório para exibir instâncias de processo que iniciaram antes da data especificada.

1. Clique em **Ir** para executar o relatório.

   O relatório é exibido na **Relatório** à direita do **Relatório de processos** janela.

   ![long_running_processes](assets/long_running_processes.png)

   Use as opções no canto superior direito do **Relatório** para executar as seguintes operações no relatório.

   * **Atualizar**: Atualiza o relatório com os dados mais recentes no armazenamento
   * **Alterar cor da legenda**: Selecionar e alterar a cor da legenda do relatório
   * **Exportar para CSV**: Exportar e baixar os dados do relatório para um arquivo separado por vírgulas

## Relatório de duração do processo  {#process-duration-report}

O relatório Duração do processo exibe o número de instâncias de um processo do Forms por número de dias que cada instância foi executada.

### Para executar um relatório de Duração do processo {#to-execute-a-process-duration-report}

1. Para exibir os relatórios predefinidos no Relatório do Processo, no **Relatório de processos** exibição em árvore, clique no botão **Relatórios** nó .
1. Clique no botão **Duração dos processos** nó do relatório.

   ![process_duration_node](assets/process_duration_node.png)

   Ao selecionar um relatório, a variável **Parâmetros do relatório** é exibido à direita da visualização em árvore.

   ![painel de parâmetros de relatório de processos de execução longa](assets/process_duration_params.png)

   Parâmetros:

   * **Selecionar processo** (*mandatory*): Selecione um processo do AEM Forms.

1. Clique em **Ir** para executar o relatório.

   O relatório é exibido na **Relatório** painel à direita da janela Relatório de Processos.

   ![process_duration_report](assets/process_duration_report.png)

   Use as opções no canto superior direito do **Relatório** para executar as seguintes operações no relatório.

   * **Atualizar**: Atualiza o relatório com os dados mais recentes no armazenamento
   * **Alterar cor da legenda**: Selecionar e alterar a cor da legenda do relatório
   * **Exportar para CSV**: Exportar e baixar os dados do relatório para um arquivo separado por vírgulas

## Relatório de volume de fluxo de trabalho {#workflow-volume-report}

O relatório de Volume de fluxo de trabalho exibe o número de instâncias em execução e concluídas no momento de um processo do AEM Forms por dia do calendário.

### Para executar um relatório de Volume de fluxo de trabalho {#to-execute-a-workflow-volume-report}

1. Para exibir os relatórios predefinidos no Relatório do Processo, no **Relatório de processos** exibição em árvore, clique no botão **Relatórios** nó .
1. Clique no botão **Volume do fluxo de trabalho** nó do relatório.

   ![workflow_volume_node](assets/workflow_volume_node.png)

   Ao selecionar um relatório, a variável **Parâmetros do relatório** é exibido à direita da visualização em árvore.

   ![painel de parâmetros de relatório de processos de execução longa](assets/workflow_volume_params.png)

   Parâmetros:

   * **Selecionar processo** (*mandatory*): Selecione um processo do AEM Forms.

   * **Iniciado após** (*opcional*): Selecione uma data. Filtra o relatório para exibir instâncias de processo que começaram após a data especificada.

   * **Iniciado antes** (*opcional*): Selecione uma data. Filtra o relatório para exibir instâncias de processo que iniciaram antes da data especificada.

1. Clique em **Ir** para executar o relatório.

   O relatório é exibido na **Relatório** à direita do **Relatório de processos** janela.

   ![workflow_volume_report](assets/workflow_volume_report.png)

   Use as opções no canto superior direito do **Relatório** para executar as seguintes operações no relatório.

   * **Atualizar**: Atualiza o relatório com os dados mais recentes no armazenamento
   * **Alterar cor da legenda**: Selecionar e alterar a cor da legenda do relatório
   * **Exportar para CSV**: Exportar e baixar os dados do relatório para um arquivo separado por vírgulas
