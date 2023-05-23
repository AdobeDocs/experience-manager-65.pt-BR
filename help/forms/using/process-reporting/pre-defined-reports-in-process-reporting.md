---
title: Relatórios predefinidos em relatórios de processo
seo-title: Pre-defined reports in Process Reporting
description: Consultar dados de processo do AEM Forms no JEE para criar relatórios sobre processos de longa execução, duração do processo e volume do fluxo de trabalho
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

# Relatórios predefinidos em relatórios de processo {#pre-defined-reports-in-process-reporting}

## Relatórios predefinidos em relatórios de processo {#pre-defined-reports-in-process-reporting-1}

O AEM Forms Process Reporting inclui o seguinte *pronto para uso* relatórios:

* **[Processos de longa execução](#long-running-processes)**: um relatório de todos os processos do AEM Forms que levaram mais tempo do que o especificado para serem concluídos
* **[Gráfico de Duração do Processo](#process-duration-report)**: um relatório de um processo do AEM Forms especificado por duração
* **[Volume do fluxo de trabalho](#workflow-volume-report)**: um relatório das instâncias em execução e concluídas do processo especificado por data

## Processos de longa execução {#long-running-processes}

O relatório Processos de Longa Execução exibe os processos do AEM Forms que levaram mais de um tempo especificado para serem concluídos.

### Para executar um relatório de Processo de Longa Execução {#to-execute-a-long-running-process-report}

1. Para exibir a lista de relatórios predefinidos em Relatórios de Processo, no campo **Relatório do processo** exibição em árvore, clique no link **Relatórios** nó.
1. Clique em **Processos de longa execução** nó do relatório.

   ![long_running_node](assets/long_running_node.png)

   Ao selecionar um relatório, a variável **Parâmetros do relatório** é exibido à direita da exibição em árvore.

   ![painel parâmetros de relatório de processos de longa duração](assets/report_parameters_panel.png)

   Parâmetros:

   * **Duração** (*obrigatório*): especifique uma duração e uma unidade de tempo. Exibir todos os processos do AEM Forms que foram executados por mais do que a duração especificada.
   * **Iniciado após** (*opcional*): Selecione uma data. Filtre o relatório para exibir instâncias de processo iniciadas após a data especificada.
   * **Iniciado antes** (*opcional*): Selecione uma data. Filtre o relatório para exibir instâncias de processo iniciadas antes da data especificada.

1. Clique em **Ir** para executar o relatório.

   O relatório é exibido na **Relatório** à direita do painel **Relatório do processo** janela.

   ![long_running_processes](assets/long_running_processes.png)

   Use as opções no canto superior direito do **Relatório** para executar as seguintes operações no relatório.

   * **Atualizar**: atualiza o relatório com os dados mais recentes armazenados no armazenamento
   * **Alterar cor da legenda**: selecionar e alterar a cor da legenda do relatório
   * **Exportar para CSV**: exporte e baixe os dados do relatório para um arquivo separado por vírgulas

## Relatório de duração do processo  {#process-duration-report}

O relatório Duração do processo exibe o número de instâncias de um processo do Forms por número de dias que cada instância foi executada.

### Para executar um relatório de Duração do processo {#to-execute-a-process-duration-report}

1. Para exibir os relatórios predefinidos em Emissão de Relatórios do Processo, no campo **Relatório do processo** exibição em árvore, clique no link **Relatórios** nó.
1. Clique em **Duração dos processos** nó do relatório.

   ![process_duration_node](assets/process_duration_node.png)

   Ao selecionar um relatório, a variável **Parâmetros do relatório** é exibido à direita da exibição em árvore.

   ![painel parâmetros de relatório de processos de longa duração](assets/process_duration_params.png)

   Parâmetros:

   * **Selecionar processo** (*obrigatório*): selecione um processo AEM Forms.

1. Clique em **Ir** para executar o relatório.

   O relatório é exibido na **Relatório** à direita da janela Relatórios do processo.

   ![process_duration_report](assets/process_duration_report.png)

   Use as opções no canto superior direito do **Relatório** para executar as seguintes operações no relatório.

   * **Atualizar**: atualiza o relatório com os dados mais recentes armazenados no armazenamento
   * **Alterar cor da legenda**: selecionar e alterar a cor da legenda do relatório
   * **Exportar para CSV**: exporte e baixe os dados do relatório para um arquivo separado por vírgulas

## Relatório de volume do fluxo de trabalho {#workflow-volume-report}

O relatório Volume do fluxo de trabalho exibe o número de instâncias atualmente em execução e concluídas de um processo do AEM Forms por dia do calendário.

### Para executar um relatório de Volume de Workflow {#to-execute-a-workflow-volume-report}

1. Para exibir os relatórios predefinidos em Emissão de Relatórios do Processo, no campo **Relatório do processo** exibição em árvore, clique no link **Relatórios** nó.
1. Clique em **Volume do fluxo de trabalho** nó do relatório.

   ![workflow_volume_node](assets/workflow_volume_node.png)

   Ao selecionar um relatório, a variável **Parâmetros do relatório** é exibido à direita da exibição em árvore.

   ![painel parâmetros de relatório de processos de longa duração](assets/workflow_volume_params.png)

   Parâmetros:

   * **Selecionar processo** (*obrigatório*): selecione um processo AEM Forms.

   * **Iniciado após** (*opcional*): Selecione uma data. Filtra o relatório para exibir instâncias de processo iniciadas após a data especificada.

   * **Iniciado antes** (*opcional*): Selecione uma data. Filtra o relatório para exibir instâncias de processo iniciadas antes da data especificada.

1. Clique em **Ir** para executar o relatório.

   O relatório é exibido na **Relatório** à direita do painel **Relatório do processo** janela.

   ![workflow_volume_report](assets/workflow_volume_report.png)

   Use as opções no canto superior direito do **Relatório** para executar as seguintes operações no relatório.

   * **Atualizar**: atualiza o relatório com os dados mais recentes armazenados no armazenamento
   * **Alterar cor da legenda**: selecionar e alterar a cor da legenda do relatório
   * **Exportar para CSV**: exporte e baixe os dados do relatório para um arquivo separado por vírgulas
