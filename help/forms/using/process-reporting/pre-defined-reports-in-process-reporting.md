---
title: Relatórios predefinidos em relatórios de processo
description: Consultar dados de processo do AEM Forms no JEE para criar relatórios sobre processos de longa execução, duração do processo e volume do fluxo de trabalho
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%
---
# Relatórios predefinidos em relatórios de processo {#pre-defined-reports-in-process-reporting}

## Relatórios predefinidos em relatórios de processo {#pre-defined-reports-in-process-reporting-1}

O AEM Forms Process Reporting vem com os seguintes *relatórios prontos para uso*:

* **[Processos de Longa Execução](#long-running-processes)**: Um relatório de todos os processos do AEM Forms que levaram mais tempo do que o especificado para serem concluídos
* **[Gráfico de Duração do Processo](#process-duration-report)**: Um relatório de um processo do AEM Forms especificado por duração
* **[Volume do Fluxo de Trabalho](#workflow-volume-report)**: um relatório das instâncias em execução e concluídas do processo especificado por data

## Processos de longa execução {#long-running-processes}

O relatório Processos de Longa Execução exibe os processos do AEM Forms que levaram mais de um tempo especificado para serem concluídos.

### Para executar um relatório de Processo de Longa Execução {#to-execute-a-long-running-process-report}

1. Para exibir a lista de relatórios predefinidos em Relatórios de Processo, no modo de exibição de árvore **Relatórios de Processo**, clique no nó **Relatórios**.
1. Clique no nó de relatório **Processos de Longa Execução**.

   ![nó_de_execução_longo](assets/long_running_node.png)

   Quando você seleciona um relatório, o painel **Parâmetros do relatório** é exibido à direita do modo de exibição em árvore.

   ![painel de parâmetros de relatório de processos de longa execução](assets/report_parameters_panel.png)

   Parâmetros:

   * **Duração** (*obrigatório*): especifique uma duração e uma unidade de tempo. Exibir todos os processos do AEM Forms que foram executados por mais do que a duração especificada.
   * **Iniciado após** (*opcional*): selecione uma data. Filtre o relatório para exibir instâncias de processo iniciadas após a data especificada.
   * **Iniciado antes** (*opcional*): selecione uma data. Filtre o relatório para exibir instâncias de processo iniciadas antes da data especificada.

1. Clique em **Ir** para executar o relatório.

   O relatório é exibido no painel **Relatório** à direita da janela **Relatórios do Processo**.

   ![long_running_processes](assets/long_running_processes.png)

   Use as opções no canto superior direito do painel **Relatório** para executar as seguintes operações no relatório.

   * **Atualizar**: atualiza o relatório com os dados mais recentes contidos no armazenamento
   * **Alterar cor da legenda**: selecione e altere a cor da legenda do relatório
   * **Exportar para CSV**: exporte e baixe os dados do relatório para um arquivo separado por vírgulas

## Relatório de duração do processo  {#process-duration-report}

O relatório Duração do processo exibe o número de instâncias de um processo do Forms por número de dias que cada instância foi executada.

### Para executar um relatório de Duração do processo {#to-execute-a-process-duration-report}

1. Para exibir os relatórios predefinidos em Relatórios de Processo, na exibição em árvore **Relatórios de Processo**, clique no nó **Relatórios**.
1. Clique no nó de relatório **Duração dos processos**.

   ![process_duration_node](assets/process_duration_node.png)

   Quando você seleciona um relatório, o painel **Parâmetros do relatório** é exibido à direita do modo de exibição em árvore.

   ![painel de parâmetros de relatório de processos de longa execução](assets/process_duration_params.png)

   Parâmetros:

   * **Selecionar Processo** (*obrigatório*): Selecione um processo do AEM Forms.

1. Clique em **Ir** para executar o relatório.

   O relatório é exibido no painel **Relatório**, à direita da janela Relatórios do Processo.

   ![process_duration_report](assets/process_duration_report.png)

   Use as opções no canto superior direito do painel **Relatório** para executar as seguintes operações no relatório.

   * **Atualizar**: atualiza o relatório com os dados mais recentes contidos no armazenamento
   * **Alterar cor da legenda**: selecione e altere a cor da legenda do relatório
   * **Exportar para CSV**: exporte e baixe os dados do relatório para um arquivo separado por vírgulas

## Relatório de volume do fluxo de trabalho {#workflow-volume-report}

O relatório Volume do fluxo de trabalho exibe o número de instâncias atualmente em execução e concluídas de um processo do AEM Forms por dia do calendário.

### Para executar um relatório de Volume de Workflow {#to-execute-a-workflow-volume-report}

1. Para exibir os relatórios predefinidos em Relatórios de Processo, na exibição em árvore **Relatórios de Processo**, clique no nó **Relatórios**.
1. Clique no nó de relatório **Volume do Fluxo de Trabalho**.

   ![workflow_volume_node](assets/workflow_volume_node.png)

   Quando você seleciona um relatório, o painel **Parâmetros do relatório** é exibido à direita do modo de exibição em árvore.

   ![painel de parâmetros de relatório de processos de longa execução](assets/workflow_volume_params.png)

   Parâmetros:

   * **Selecionar Processo** (*obrigatório*): Selecione um processo do AEM Forms.

   * **Iniciado após** (*opcional*): selecione uma data. Filtra o relatório para exibir instâncias de processo iniciadas após a data especificada.

   * **Iniciado antes** (*opcional*): selecione uma data. Filtra o relatório para exibir instâncias de processo iniciadas antes da data especificada.

1. Clique em **Ir** para executar o relatório.

   O relatório é exibido no painel **Relatório** à direita da janela **Relatórios do Processo**.

   ![relatório_de_volume_de_fluxo_de_trabalho](assets/workflow_volume_report.png)

   Use as opções no canto superior direito do painel **Relatório** para executar as seguintes operações no relatório.

   * **Atualizar**: atualiza o relatório com os dados mais recentes contidos no armazenamento
   * **Alterar cor da legenda**: selecione e altere a cor da legenda do relatório
   * **Exportar para CSV**: exporte e baixe os dados do relatório para um arquivo separado por vírgulas
