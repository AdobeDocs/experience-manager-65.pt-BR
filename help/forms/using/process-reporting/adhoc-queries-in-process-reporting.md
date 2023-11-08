---
title: Consultas ad-hoc em relatórios do processo
description: Criar consultas personalizadas para pesquisar por detalhes do processo e da tarefa do AEM Forms no JEE em Relatórios do Processo
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: a096eea0-b2fb-4d86-b729-ca47611135b2
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1672'
ht-degree: 0%

---

# Consultas ad-hoc em relatórios do processo{#ad-hoc-queries-in-process-reporting}

## Consultas ad-hoc em Relatórios do processo {#ad-hoc-queries-in-process-reporting-1}

As consultas ad-hoc no Process Reporting permitem criar consultas personalizadas que você pode usar para procurar detalhes de processos e tarefas das instâncias de processos AEM Forms definidas no ambiente AEM Forms.

Além disso, as consultas ad hoc podem ser definidas usando filtros de propriedade de processo e tarefa. Esses filtros podem ser salvos e usados para executar os relatórios posteriormente.

[**Pesquisa de processos**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p): pesquise instâncias de processo com um filtro de pesquisa definido pelo usuário com base em atributos de processo.

[**Detalhes do processo**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p): visualize os detalhes de uma instância do processo especificando a ID do processo.

**Pesquisa de tarefa**: procure instâncias de tarefas com um filtro de pesquisa definido pelo usuário com base em atributos de tarefas.

**Detalhes da tarefa**: visualize os detalhes de uma instância de tarefa especificando a ID da tarefa.

### Processos e tarefas {#processes-and-tasks}

As etapas seguidas para criar filtros e executar consultas para detalhes do processo são as mesmas das tarefas.

Isso significa que as interfaces de usuário para a Pesquisa de processos e a Pesquisa de tarefas diferem apenas nos campos pelos quais é possível pesquisar e nos campos retornados nos resultados da pesquisa. Isso ocorre simplesmente porque, embora muitos dos campos sejam idênticos, determinados campos são específicos de processos e determinados campos são específicos de tarefas.

Este artigo detalha as descrições das seções Pesquisa de Processo/Tarefa e Detalhes de Processo/Tarefa. Em locais apropriados, quaisquer diferenças específicas serão chamadas especificamente.

## Pesquisa de Processo/Tarefa {#process-task-search}

Use a Pesquisa de processos/tarefas para definir filtros para consultar instâncias de processos/tarefas.

### Para criar uma consulta de Pesquisa de Processo/Tarefa {#to-create-a-process-task-search-query}

1. Para exibir as consultas salvas de Pesquisa de Processo/Tarefa ou criar uma consulta, clique em **Consultas adhoc** e clique em **Pesquisa de Processo/Tarefa**.

   ![search_nodes](assets/search_nodes.png)

   A variável **Meus filtros** é exibido à direita da exibição em árvore.

   No **Meus filtros** você pode criar novas consultas ad-hoc e clicar em para executar as consultas salvas anteriormente.

   ![my_filters_panel](assets/my_filters_panel.png)

1. Para executar uma consulta existente, basta clicar na consulta na **Meus filtros** painel.
1. Para criar uma consulta, clique em **Adicionar** (+).

   A variável **Criar filtro** é exibido.

   ![create_filter_panel](assets/create_filter_panel.png)

   Uma consulta consiste em um ou mais filtros de consulta. Para criar um filtro, adicione uma linha de filtro à query. Por padrão, uma linha de filtro é adicionada à query.

   **Para definir um filtro**

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

Após criar uma query, use as opções no canto superior direito da **Criar filtro** para:

* **Cancelar**: Cancele as alterações e volte para a guia **Meus filtros** painel.
* **Executar**: execute a consulta atual para ver e/ou verificar os resultados. Nesse caso, não é necessário salvar a query antes de executá-la. Você pode verificar os resultados, fazer alterações se necessário e salvar a consulta quando estiver satisfeito com a saída.
* **Salvar**: Salve o filtro. O filtro pode ser exibido e executado no **Meus filtros** painel.

### Opções no painel Meus filtros {#options-in-my-filters-panel}

Use as opções no **Meus filtros** painel para **Adicionar** ![lc_pr_add_filter](assets/lc_pr_add_filter.png), **Editar** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png)ou **Excluir** ![lc_pr_edit_filter](assets/lc_pr_edit_filter.png)uma consulta ad-hoc.

![my_filters_options](assets/my_filters_options.png)

### Para executar uma consulta de Pesquisa {#to-execute-a-search-query}

1. Para executar uma consulta, clique no filtro na **Meus filtros** ou clique no botão **Executar** botão se estiver criando ou editando um filtro.
1. Os resultados da query são exibidos na variável **Relatório** painel da **Relatório do processo** janela.

   ![process_search_result](assets/process_search_result.png)

   Você pode paginar os resultados da pesquisa com a ajuda do painel de paginação exibido na parte inferior do relatório.

   ![process_result_pgn](assets/process_result_pgn.png)

   No **Exibir** escolha o número de resultados a serem exibidos por página.

   No **Página** , insira um número de página para ir diretamente para essa página.

1. Os seguintes campos são exibidos em um resultado de Pesquisa de processo:

   * **ID do processo**: a ID do processo. O campo está com hiperlink. Se você clicar em uma ID de processo neste campo, será redirecionado para a **[!UICONTROL Detalhes do processo]** painel do processo.
   * **Iniciador**: o usuário do AEM Forms que iniciou a instância do processo
   * **Hora de criação**: a data e a hora em que a instância do processo foi iniciada
   * **Hora de conclusão**: a data e a hora em que a instância do processo foi concluída
   * **Duração**: a duração do início à conclusão da instância do processo
   * **Status**: o status atual da instância do processo.

   Por padrão, o resultado é classificado pela ID do processo. No entanto, para classificar o resultado por qualquer um dos campos, clique no título do campo.

   Como a classificação é uma operação de alternância, clique em um cabeçalho de coluna para classificar o resultado em ordem crescente e clique nele novamente para classificar em ordem decrescente.

   Da mesma forma, os seguintes campos são exibidos em um resultado de Pesquisa de tarefa:

   * **ID da tarefa**: A ID da tarefa. O campo está com hiperlink. Se clicar em uma ID de tarefa neste campo, você será redirecionado para a **[!UICONTROL Detalhes da tarefa]** painel da tarefa.
   * **Iniciador**: o usuário do AEM Forms que iniciou a instância do processo
   * **Hora de criação**: a data e a hora em que a instância do processo foi iniciada
   * **Hora de conclusão**: a data e a hora em que a instância do processo foi concluída
   * **Duração**: a duração do início à conclusão da instância do processo
   * **Status**: o status atual da instância do processo.

   Por padrão, o resultado é classificado pela ID da tarefa. No entanto, para classificar o resultado por qualquer um dos campos, clique no título do campo. O resultado é classificado pela coluna indicada por uma seta escurecida ao lado do cabeçalho da coluna.

   Como a classificação é uma operação de alternância, clique em um cabeçalho de campo para classificar o resultado em ordem crescente e clique nele novamente para classificar em ordem decrescente. A ordem de classificação atual (crescente / decrescente) é indicada pela direção da seta escurecida ao lado do cabeçalho da coluna.

   ![task_search_result](assets/task_search_result.png)

1. Clique no botão do painel ![lc_pr_rail_button](assets/lc_pr_rail_button.png) na parte superior esquerda para recolher o **Meus filtros** e expande o espaço disponível para o **Relatório** painel.
1. Use as opções no canto superior direito do painel **Relatório** para executar operações no resultado da consulta.

   * **Atualizar**: atualiza o relatório com os dados mais recentes armazenados no armazenamento

   * **Exportar para CSV**: exporte os dados do relatório para um arquivo separado por vírgulas.

   >[!NOTE]
   >
   >Ao exportar um relatório, todo o resultado da pesquisa é exportado para um arquivo CSV e não apenas para a página atual

## Detalhes de Processo/Tarefa {#process-task-details}

Você usa o **Detalhes do processo** para exibir os detalhes de um processo específico.

Da mesma forma, você usa o **Detalhes da tarefa** para exibir os detalhes de uma tarefa específica.

### Para exibir Detalhes de Processos/Tarefas {#to-view-process-task-details}

Você pode exibir os detalhes de um processo/tarefa específico do AEM Forms:

* **De um resultado de Pesquisa de Processo/Tarefa**
* **Ao inserir o ID de processo/tarefa no painel Detalhes de processo/tarefa**

#### De um resultado de Pesquisa de Processo/Tarefa {#from-a-process-task-search-result}

1. Executar uma pesquisa de processo/tarefa. Para obter detalhes, consulte [Para executar uma consulta de Pesquisa de Processo](#to-execute-a-search-query).

   Observe que as IDs do processo exibidas, retornadas no resultado, estão com um hiperlink.

   ![process_id_list](assets/process_id_list.png)

1. Clique em uma ID de processo na lista para exibir os detalhes desse processo na **Detalhes do processo** painel.

   A variável **Detalhes de Processo/Tarefa** o resultado da consulta exibe detalhes das tarefas/formulários contidos no processo/tarefa.

   Por padrão, o resultado é classificado por ID de tarefa/formulário. No entanto, para classificar o resultado por qualquer um dos campos, clique no título do campo. A coluna pela qual o resultado é classificado é indicada por uma seta escurecida ao lado do cabeçalho da coluna.

   Como a classificação é uma operação de alternância, clique em um cabeçalho de campo para classificar o resultado em ordem crescente e clique nele novamente para classificar em ordem decrescente. A ordem de classificação atual (crescente / decrescente) é indicada pela direção da seta escurecida ao lado do cabeçalho da coluna.

   **Resultado dos Detalhes do Processo**

   ![process_details](assets/process_details.png)

   **Painel esquerdo:** Exibe os seguintes detalhes do processo selecionado:

   * Nome do processo
   * Data e hora de criação do processo
   * Data e hora de conclusão do processo
   * Duração do processo
   * Status do processo
   * Iniciador do processo

   **Painel superior direito:** Exibe os seguintes detalhes das tarefas que compõem o processo selecionado:

   * ID da tarefa
   * Nome da tarefa
   * Proprietário da tarefa
   * Data e hora de criação da tarefa
   * Data e hora de atualização da tarefa
   * Data e hora de conclusão da tarefa
   * Duração da tarefa
   * Status da tarefa

   **Painel inferior direito:** Exibe os seguintes detalhes do histórico do processo selecionado:

   * Nome do processo
   * Iniciador do processo
   * Processar data e hora de atualização
   * Data e hora de conclusão do processo
   * Status do processo

   **Resultado da tarefa Detalhes**

   ![task_details](assets/task_details.png)

   **Painel esquerdo:** Exibe os seguintes detalhes da tarefa selecionada:

   * Nome da tarefa
   * ID do processo ao qual esta tarefa pertence
   * Descrição da tarefa
   * Data e hora de criação da tarefa
   * Data e hora de conclusão da tarefa
   * Duração da tarefa
   * Status da tarefa
   * Rota selecionada da tarefa

   **Painel superior direito:** Exibe os seguintes detalhes dos formulários que compõem a tarefa selecionada:

   * ID do formulário
   * Data e hora de criação do formulário
   * Data e hora de atualização do formulário
   * URL do modelo de formulário

   **Painel inferior direito:** Exibe os seguintes detalhes do histórico do processo da tarefa selecionada:

   * Tipo de atribuição de tarefa
   * Proprietário da tarefa
   * Data e hora de criação da atribuição de tarefa
   * Data e hora de atualização da tarefa

1. Clique em **Voltar para Pesquisa de Processo/Tarefa** para voltar ao resultado da pesquisa a partir do qual os detalhes do processo/tarefa foram detalhados.

   ![back_to_search](assets/back_to_search.png)

   No entanto, se os detalhes do processo/tarefa foram encontrados ao inserir um ID de processo/tarefa específico, clicar em Voltar para a Pesquisa de Processo/Tarefa o redirecionará para **Pesquisa de Processo/Tarefa**, sem exibir nenhum resultado de pesquisa.

#### Ao inserir o ID de processo/tarefa no painel Detalhes de processo/tarefa {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. Vá para a **Detalhes de Processo/Tarefa** painel.

   ![details_nodes](assets/details_nodes.png)

1. Na caixa de texto ID de Processo/Tarefa, informe o ID de processo/tarefa.

   ![process_details-1](assets/process_details-1.png)

   Os campos no **Detalhes de Processo/Tarefa** os resultados da consulta são campos específicos de um processo/tarefa do AEM Forms.

   Para um processo, o resultado da consulta exibe os detalhes das tarefas contidas no processo.

   Para uma tarefa, o resultado da consulta exibe os detalhes dos formulários contidos na tarefa.
