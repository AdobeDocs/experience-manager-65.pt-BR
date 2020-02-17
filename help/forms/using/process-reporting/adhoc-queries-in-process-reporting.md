---
title: Consultas Ad-hoc em Relatório de Processo
seo-title: Consultas Ad-hoc em Relatório de Processo
description: Crie consultas personalizadas para pesquisar por AEM Forms em detalhes de processos e tarefas do JEE no Process Reporting
seo-description: Crie consultas personalizadas para pesquisar por AEM Forms em detalhes de processos e tarefas do JEE no Process Reporting
uuid: db0c5c28-b213-4582-a6ed-df127e570a4e
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b0a544e2-2ce4-48e2-a721-82f481d36004
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# Consultas Ad-hoc em Relatório de Processo{#ad-hoc-queries-in-process-reporting}

## Consultas ad-hoc no Process Reporting {#ad-hoc-queries-in-process-reporting-1}

As consultas ad-hoc no Process Reporting permitem que você crie consultas personalizadas que podem ser usadas para pesquisar detalhes de processos e tarefas das instâncias de processo do AEM Forms definidas no ambiente do AEM Forms.

Além disso, as consultas ad hoc podem ser definidas usando filtros de propriedade de processo e tarefa. Esses filtros podem ser salvos e usados para executar os relatórios posteriormente.

[**Pesquisa **](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p)de processos: Procure instâncias de processo com um filtro de pesquisa definido pelo usuário com base em atributos de processo.

[**Detalhes **](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p)do processo: Visualize detalhes de uma instância do processo especificando a ID do processo.

**Pesquisa** de tarefas: Procure instâncias de tarefa com um filtro de pesquisa definido pelo usuário com base em atributos de tarefa.

**Detalhes** da tarefa: Visualize detalhes de uma instância de tarefa especificando a ID da tarefa.

### Processos e tarefas {#processes-and-tasks}

As etapas que você segue para criar filtros e executar consultas para detalhes do processo são as mesmas que para tarefas.

Isso significa que as interfaces do usuário para Pesquisa de processos e Pesquisa de tarefas diferem somente nos campos pelos quais você pode pesquisar e nos campos retornados nos resultados da pesquisa. Isso ocorre simplesmente porque, embora muitos dos campos sejam idênticos, determinados campos são específicos de processos e determinados campos são específicos de tarefas.

Este artigo detalha as descrições das seções Pesquisa de Processo/Tarefa e Detalhes de Processo/Tarefa. Em locais apropriados, quaisquer diferenças específicas serão especificamente destacadas.

## Pesquisa de Processo/Tarefa {#process-task-search}

Use a Pesquisa de Processo/Tarefa para definir filtros para consultar instâncias de processo/tarefa.

### Para criar uma consulta de Pesquisa de Processo/Tarefa {#to-create-a-process-task-search-query}

1. Para exibir as consultas salvas de Pesquisa de Processo/Tarefa ou para criar uma consulta, clique em Consultas **** Ad-hoc e clique em Pesquisa **de** Processo/Tarefa.

   ![search_nodes](assets/search_nodes.png)

   O painel **Meus filtros** é exibido à direita da visualização em árvore.

   No painel **Meus filtros** , você pode criar novas consultas ad-hoc e clicar para executar consultas salvas anteriormente.

   ![my_filter_panel](assets/my_filters_panel.png)

1. Para executar uma consulta existente, basta clicar na consulta no painel **Meus filtros** .
1. Para criar uma consulta, clique em **Adicionar** (+).

   O painel **Criar filtro** é exibido.

   ![create_filter_panel](assets/create_filter_panel.png)

   Uma consulta consiste em um ou mais filtros de consulta. Para criar um filtro, adicione uma linha de filtro à consulta. Por padrão, uma linha de filtro é adicionada à consulta.

   **Definição de um filtro**

   1. Selecione um campo.

      ![filter_field](assets/filter_field.png)

      >[!NOTE]
      >
      >A lista de campos contém os campos específicos do processo/tarefa do AEM Forms.

   1. Selecione uma condição.

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >As condições listadas dependem do atributo selecionado para filtragem.

   1. Insira um valor.

      ![filter_value](assets/filter_value.png)

   1. Para adicionar outro filtro à consulta, clique em **Adicionar (+)** à direita da linha de filtro.

      Para remover um filtro da consulta, clique em **Excluir (-)** à direita da linha de filtro.

      ![filter_add_del](assets/filter_add_del.png)

Depois de criar uma consulta, use as opções no canto superior direito do painel **Criar filtro** para:

* **Cancelar**: Cancele as alterações e volte ao painel **Meus filtros** .
* **Executar**: Execute a consulta atual para ver e/ou verificar os resultados. Nesse caso, não é necessário salvar a consulta antes de executá-la. Você pode verificar os resultados, fazer alterações se necessário e salvar a consulta quando estiver satisfeito com a saída.
* **Salvar**:Salve o filtro. O filtro pode ser exibido e executado a partir do painel **Meus filtros** .

### Opções no painel Meus filtros {#options-in-my-filters-panel}

Use as opções no painel **Meus filtros** para **Adicionar** ![lc_pr_add_filter](assets/lc_pr_add_filter.png), **Editar** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png)**** ![](assets/lc_pr_edit_filter.png)ou Excluirlc_pr_edit_filteran consulta ad-hoc.

![my_filter_options](assets/my_filters_options.png)

### Para executar uma consulta de pesquisa {#to-execute-a-search-query}

1. Para executar uma consulta, clique no filtro no painel **Meus filtros** ou clique no botão **Executar** se você estiver criando ou editando um filtro.
1. Os resultados da consulta são exibidos no painel **Relatório** da janela Relatório de **Processo** .

   ![process_search_result](assets/process_search_result.png)

   Você pode paginar os resultados da pesquisa com a ajuda do painel de paginação exibido na parte inferior do relatório.

   ![process_result_pgn](assets/process_result_pgn.png)

   Na lista suspensa **Exibir** , escolha o número de resultados a serem exibidos por página.

   Na caixa de texto **Página** , digite um número de página para ir diretamente para essa página.

1. Os seguintes campos são exibidos em um resultado de Pesquisa de Processo:

   * **ID** do processo: A ID do processo. O campo está hipervinculado. Se você clicar em uma ID de processo nesse campo, será redirecionado para o painel Detalhes **[!UICONTROL do]** processo.
   * **Iniciador**: O usuário do AEM Forms que iniciou a instância do processo
   * **Hora** de criação: A data e a hora em que a instância do processo começou
   * **Hora** de conclusão: A data e a hora em que a instância do processo foi concluída
   * **Duração**: A duração do início até a conclusão da instância do processo
   * **Status**: O status atual da instância do processo.
   Por padrão, o resultado é classificado pela ID do processo. Entretanto, para classificar o resultado por qualquer um dos campos, clique no título do campo.

   Como a classificação é uma operação de alternância, clique em um cabeçalho de coluna para classificar o resultado em ordem crescente e clique nele novamente para classificar em ordem decrescente.

   Da mesma forma, os seguintes campos são exibidos em um resultado de Pesquisa de tarefa:

   * **ID** da tarefa: A ID da tarefa. O campo está hipervinculado. Se você clicar em uma ID de tarefa nesse campo, será redirecionado para o painel Detalhes **[!UICONTROL da]** tarefa da tarefa.
   * **Iniciador**: O usuário do AEM Forms que iniciou a instância do processo
   * **Hora** de criação: A data e a hora em que a instância do processo começou
   * **Hora** de conclusão: A data e a hora em que a instância do processo foi concluída
   * **Duração**: A duração do início até a conclusão da instância do processo
   * **Status**: O status atual da instância do processo.
   Por padrão, o resultado é classificado pela ID da tarefa. Entretanto, para classificar o resultado por qualquer um dos campos, clique no título do campo. O resultado é classificado pela coluna que é indicada por uma seta escurecida ao lado do cabeçalho da coluna.

   Como a classificação é uma operação de alternância, clique em um cabeçalho de campo para classificar o resultado em ordem crescente e clique nele novamente para classificar em ordem decrescente. A ordem de classificação atual (crescente/decrescente) é indicada pela direção da seta escurecida ao lado do cabeçalho da coluna.

   ![task_search_result](assets/task_search_result.png)

1. Clique no botão do painel ![lc_pr_Rail_button](assets/lc_pr_rail_button.png) no canto superior esquerdo para recolher o painel **Meus filtros** e expandir o espaço disponível para o painel **Relatório** .
1. Use as opções no canto superior direito do painel **Relatório **para executar operações no resultado da consulta.

   * **Atualizar**: Atualiza o relatório com os dados mais recentes no armazenamento

   * **Exportar para CSV**: Exporte os dados do relatório para um arquivo separado por vírgulas.
   >[!NOTE]
   >
   >Quando você exporta um relatório, todo o resultado da pesquisa é exportado para um arquivo CSV e não apenas para a página atual

## Detalhes do processo/tarefa {#process-task-details}

Use o painel Detalhes **do** processo para exibir os detalhes de um processo específico.

Da mesma forma, use o painel Detalhes **da** tarefa para exibir os detalhes de uma tarefa específica.

### Para exibir Detalhes do Processo/Tarefa {#to-view-process-task-details}

Você pode exibir os detalhes de um processo/tarefa específica do AEM Forms:

* **De um resultado de Pesquisa de Processo/Tarefa**
* **Inserindo a ID Processo/Tarefa no painel Detalhes do Processo/Tarefa**

#### De um resultado de Pesquisa de Processo/Tarefa {#from-a-process-task-search-result}

1. Executar uma pesquisa de processo/tarefa. Para obter detalhes, consulte [Para executar uma consulta](#to-execute-a-search-query)de Pesquisa de Processo.

   Observe que as IDs de processo exibidas retornadas no resultado são hipervinculadas.

   ![process_id_list](assets/process_id_list.png)

1. Clique em uma ID de processo na lista para exibir os detalhes desse processo no painel Detalhes **do** processo.

   O resultado da consulta Detalhes **do** Processo/Tarefa exibe detalhes das tarefas/formulários contidos no processo/tarefa.

   Por padrão, o resultado é classificado pela ID da tarefa/do formulário. Entretanto, para classificar o resultado por qualquer um dos campos, clique no título do campo. A coluna pela qual o resultado é classificado é indicada por uma seta escurecida ao lado do cabeçalho da coluna.

   Como a classificação é uma operação de alternância, clique em um cabeçalho de campo para classificar o resultado em ordem crescente e clique nele novamente para classificar em ordem decrescente. A ordem de classificação atual (crescente/decrescente) é indicada pela direção da seta escurecida ao lado do cabeçalho da coluna.

   **Resultado de Detalhes do Processo**

   ![process_details](assets/process_details.png)

   **** Painel esquerdo: Exibe os seguintes detalhes do processo selecionado:

   * Nome do processo
   * Hora da data de criação do processo
   * Hora de conclusão do processo
   * Duração do processo
   * Status do processo
   * Iniciador do processo
   **** Painel Superior direito: Exibe os seguintes detalhes das tarefas que compõem o processo selecionado:

   * ID da tarefa
   * Nome da tarefa
   * Proprietário da tarefa
   * Data e hora de criação da tarefa
   * Hora da data de atualização da tarefa
   * Hora de conclusão da tarefa
   * Duração da tarefa
   * Status da tarefa
   **** Painel inferior direito: Exibe os seguintes detalhes do histórico do processo selecionado:

   * Nome do processo
   * Iniciador do processo
   * Hora da data de atualização do processo
   * Hora de conclusão do processo
   * Status do processo
   **Resultado Detalhes da Tarefa**

   ![task_details](assets/task_details.png)

   **** Painel esquerdo: Exibe os seguintes detalhes da tarefa selecionada:

   * Nome da tarefa
   * ID do processo ao qual esta tarefa pertence
   * Descrição da tarefa
   * Data e hora de criação da tarefa
   * Hora de conclusão da tarefa
   * Duração da tarefa
   * Status da tarefa
   * Rota de tarefa selecionada
   **** Painel Superior direito: Exibe os seguintes detalhes dos formulários que compõem a tarefa selecionada:

   * ID do formulário
   * Data e hora de criação do formulário
   * Hora de atualização do formulário
   * URL do modelo de formulário
   **** Painel inferior direito: Exibe os seguintes detalhes do histórico do processo da tarefa selecionada:

   * Tipo de atribuição da tarefa
   * Proprietário da tarefa
   * Hora da data de criação da atribuição da tarefa
   * Hora da data de atualização da tarefa






1. Clique em **Voltar para Processar/Pesquisar** tarefa para voltar ao resultado da pesquisa a partir do qual os detalhes do processo/tarefa foram detalhados.

   ![back_to_search](assets/back_to_search.png)

   Entretanto, se os detalhes do processo/tarefa forem encontrados inserindo uma ID de processo/tarefa específica, clicar em Voltar para Processo/Pesquisa de tarefa o levará de volta para Pesquisa **de** Processo/Tarefa, sem exibir nenhum resultado de pesquisa.

#### Inserindo a ID Processo/Tarefa no painel Detalhes do Processo/Tarefa {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. Vá para o painel Detalhes **do** processo/tarefa.

   ![details_nodes](assets/details_nodes.png)

1. Na caixa de texto ID Processo/Tarefa, informe a ID do processo/tarefa.

   ![process_details-1](assets/process_details-1.png)

   Os campos no resultado da consulta Detalhes **do** processo/tarefa são campos específicos de um processo/tarefa do AEM Forms.

   Para um processo, o resultado da consulta exibe os detalhes das tarefas contidas no processo.

   Para uma tarefa, o resultado da consulta exibe os detalhes dos formulários contidos na tarefa.

[Contate o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
