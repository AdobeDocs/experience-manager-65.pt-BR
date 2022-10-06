---
title: Consultas ad-hoc em relatórios de processo
seo-title: Ad-hoc Queries in Process Reporting
description: Crie consultas personalizadas para pesquisar o AEM Forms nos detalhes do processo e da tarefa do JEE no Process Reporting
seo-description: Create custom queries to search for AEM Forms on JEE  process and task details in Process Reporting
uuid: db0c5c28-b213-4582-a6ed-df127e570a4e
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b0a544e2-2ce4-48e2-a721-82f481d36004
docset: aem65
exl-id: a096eea0-b2fb-4d86-b729-ca47611135b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# Consultas ad-hoc em relatórios de processo{#ad-hoc-queries-in-process-reporting}

## Consultas ad-hoc no Process Reporting {#ad-hoc-queries-in-process-reporting-1}

As consultas ad-hoc no Process Reporting permitem criar consultas personalizadas que você pode usar para pesquisar detalhes de processos e tarefas das instâncias de processo do AEM Forms definidas no seu ambiente AEM Forms.

Além disso, as consultas ad hoc podem ser definidas usando filtros de propriedades de processo e tarefa. Esses filtros podem ser salvos e usados para executar os relatórios posteriormente.

[**Pesquisa de processos**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p): Procure por instâncias de processo com um filtro de pesquisa definido pelo usuário com base em atributos de processo.

[**Detalhes do processo**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p): Visualize detalhes de uma instância do processo especificando a ID do processo.

**Pesquisa de tarefa**: Procure por instâncias de tarefa com um filtro de pesquisa definido pelo usuário com base em atributos de tarefa.

**Detalhes da tarefa**: Visualize detalhes de uma instância de tarefa especificando a ID da tarefa.

### Processos e tarefas {#processes-and-tasks}

As etapas a seguir para criar filtros e executar consultas para detalhes do processo são as mesmas das tarefas.

Isso significa que a interface do usuário para a Pesquisa de Processo e Pesquisa de Tarefa é diferente apenas nos campos que você pode pesquisar e nos campos retornados nos resultados da pesquisa. Isso ocorre porque, embora muitos dos campos sejam idênticos, determinados campos são específicos dos processos e determinados campos são específicos das tarefas.

Este artigo detalha as descrições das seções Pesquisa de Processo/Tarefa e Detalhes de Processo/Tarefa. Em locais apropriados, quaisquer diferenças específicas serão especificamente eliminadas.

## Pesquisa de Processo/Tarefa {#process-task-search}

Use Pesquisa de Processo/Tarefa para definir filtros para consultar instâncias de processo/tarefa.

### Para criar uma consulta de Pesquisa de Processo/Tarefa {#to-create-a-process-task-search-query}

1. Para exibir as consultas de Pesquisa de Processo/Tarefa salvas ou para criar uma consulta, clique em **Consultas adhoc** e, em seguida, clique em **Pesquisa de Processo/Tarefa**.

   ![search_nodes](assets/search_nodes.png)

   O **Meus filtros** é exibido à direita da visualização em árvore.

   No **Meus filtros** , você pode criar novas consultas ad-hoc e clicar em para executar consultas salvas anteriormente.

   ![my_filters_panel](assets/my_filters_panel.png)

1. Para executar uma query existente, basta clicar na query no **Meus filtros** painel.
1. Para criar um query, clique em **Adicionar** (+).

   O **Criar filtro** será exibido.

   ![create_filter_panel](assets/create_filter_panel.png)

   Uma consulta consiste em um ou mais filtros de consulta. Para criar um filtro, adicione uma linha de filtro à query. Por padrão, uma linha de filtro é adicionada ao query.

   **Definição de um filtro**

   1. Selecione um campo.

      ![filter_field](assets/filter_field.png)

      >[!NOTE]
      >
      >A lista de campos contém os campos específicos para processo/tarefa do AEM Forms.

   1. Selecione uma condição.

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >As condições listadas dependem do atributo selecionado para filtragem.

   1. Insira um valor.

      ![filter_value](assets/filter_value.png)

   1. Para adicionar outro filtro à query, clique em **Adicionar (+)** à direita da linha de filtro.

      Para remover um filtro da consulta, clique em **Excluir (-)** à direita da linha de filtro.

      ![filter_add_del](assets/filter_add_del.png)

Após criar uma query, use as opções no canto superior direito da variável **Criar filtro** painel para:

* **Cancelar**: Cancele as alterações e retorne ao **Meus filtros** painel.
* **Executar**: Execute a consulta atual para ver e/ou verificar os resultados. Nesse caso, não é necessário salvar a query antes de executar a query. Você pode verificar os resultados, fazer alterações se necessário e salvar a query quando estiver satisfeito com a saída.
* **Salvar**: Salve o filtro. O filtro pode ser visualizado e executado do **Meus filtros** painel.

### Opções no painel Meus filtros {#options-in-my-filters-panel}

Use as opções na **Meus filtros** painel para **Adicionar** ![lc_pr_add_filter](assets/lc_pr_add_filter.png), **Editar** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png)ou **Excluir** ![lc_pr_edit_filter](assets/lc_pr_edit_filter.png)uma consulta ad-hoc.

![my_filters_options](assets/my_filters_options.png)

### Para executar uma consulta de pesquisa {#to-execute-a-search-query}

1. Para executar uma query, clique no filtro na **Meus filtros** ou clique no botão **Executar** se estiver criando ou editando um filtro.
1. Os resultados da query são exibidos na **Relatório** painel do **Relatório de processos** janela.

   ![process_search_result](assets/process_search_result.png)

   Você pode paginar os resultados da pesquisa com a ajuda do painel de paginação exibido na parte inferior do relatório.

   ![process_result_pgn](assets/process_result_pgn.png)

   No **Exibir** na lista suspensa, escolha o número de resultados a serem exibidos por página.

   No **Página** , insira um número de página para ir diretamente para essa página.

1. Os seguintes campos são exibidos em um resultado de Pesquisa de processo:

   * **ID do processo**: A ID do processo. O campo é hipervinculado. Se você clicar em uma ID de processo neste campo, será redirecionado para a função **[!UICONTROL Detalhes do processo]** painel para o processo.
   * **Iniciador**: O usuário do AEM Forms que iniciou a instância do processo
   * **Hora de criação**: A data e a hora em que a instância do processo começou
   * **Hora de Conclusão**: A data e a hora em que a instância do processo foi concluída
   * **Duração**: A duração do início até a conclusão da instância do processo
   * **Status**: O status atual da instância do processo.

   Por padrão, o resultado é classificado por ID do processo. No entanto, para classificar o resultado por qualquer um dos campos, clique no título do campo.

   Como a classificação é uma operação de alternância, clique em um cabeçalho de coluna para classificar o resultado em ordem crescente e clique nele novamente para classificar em ordem decrescente.

   Da mesma forma, os seguintes campos são exibidos em um resultado Pesquisa de tarefa:

   * **ID da tarefa**: A ID da tarefa. O campo é hipervinculado. Se você clicar em uma ID de tarefa nesse campo, será redirecionado para a função **[!UICONTROL Detalhes da tarefa]** para a tarefa.
   * **Iniciador**: O usuário do AEM Forms que iniciou a instância do processo
   * **Hora de criação**: A data e a hora em que a instância do processo começou
   * **Hora de Conclusão**: A data e a hora em que a instância do processo foi concluída
   * **Duração**: A duração do início até a conclusão da instância do processo
   * **Status**: O status atual da instância do processo.

   Por padrão, o resultado é classificado pela ID da tarefa. No entanto, para classificar o resultado por qualquer um dos campos, clique no título do campo. O resultado é classificado pela coluna que é indicada por uma seta escura ao lado do cabeçalho da coluna.

   Como a classificação é uma operação de alternância, clique em um cabeçalho de campo para classificar o resultado em ordem crescente e clique nele novamente para classificar em ordem decrescente. A ordem de classificação atual (crescente/decrescente) é indicada pela direção da seta escura ao lado do cabeçalho da coluna.

   ![task_search_result](assets/task_search_result.png)

1. Clique no botão do painel ![lc_pr_Rail_button](assets/lc_pr_rail_button.png) no canto superior esquerdo para recolher o **Meus filtros** e expande o espaço disponível para o **Relatório** painel.
1. Use as opções no canto superior direito do painel **Relatório **para executar operações no resultado da consulta.

   * **Atualizar**: Atualiza o relatório com os dados mais recentes no armazenamento

   * **Exportar para CSV**: Exporte os dados do relatório para um arquivo separado por vírgulas.
   >[!NOTE]
   >
   >Quando você exporta um relatório, todo o resultado da pesquisa é exportado para um arquivo CSV e não apenas para a página atual

## Detalhes do Processo/Tarefa {#process-task-details}

Você usa a variável **Detalhes do processo** para exibir os detalhes de um processo específico.

Da mesma forma, use a variável **Detalhes da tarefa** para exibir os detalhes de uma tarefa específica.

### Para exibir Detalhes do Processo/Tarefa {#to-view-process-task-details}

Você pode visualizar os detalhes de um processo/tarefa específico do AEM Forms:

* **De um resultado de Pesquisa de Processo/Tarefa**
* **Inserindo a ID Processo/Tarefa no painel Detalhes do Processo/Tarefa**

#### De um resultado de Pesquisa de Processo/Tarefa {#from-a-process-task-search-result}

1. Execute uma pesquisa de processo/tarefa. Para obter detalhes, consulte [Para executar uma consulta de Pesquisa de Processo](#to-execute-a-search-query).

   Observe que as IDs do processo exibidas no resultado são hipervinculadas.

   ![process_id_list](assets/process_id_list.png)

1. Clique em uma ID de processo na lista para exibir os detalhes desse processo na **Detalhes do processo** painel.

   O **Detalhes do Processo/Tarefa** o resultado da consulta exibe detalhes das tarefas/formulários contidos no processo/tarefa.

   Por padrão, o resultado é classificado por Tarefa/ID do formulário. No entanto, para classificar o resultado por qualquer um dos campos, clique no título do campo. A coluna pela qual o resultado é classificado é indicada por uma seta escura ao lado do cabeçalho da coluna.

   Como a classificação é uma operação de alternância, clique em um cabeçalho de campo para classificar o resultado em ordem crescente e clique nele novamente para classificar em ordem decrescente. A ordem de classificação atual (crescente/decrescente) é indicada pela direção da seta escura ao lado do cabeçalho da coluna.

   **Resultado dos Detalhes do Processo**

   ![process_details](assets/process_details.png)

   **Painel esquerdo:** Exibe os seguintes detalhes do processo selecionado:

   * Nome do processo
   * Hora de criação do processo
   * Hora de conclusão do processo
   * Duração do processo
   * Status do processo
   * Iniciador do processo

   **Painel Superior direito:** Exibe os seguintes detalhes das tarefas que compõem o processo selecionado:

   * ID da tarefa
   * Nome da tarefa
   * Proprietário da tarefa
   * Data de criação da tarefa
   * Hora da atualização da tarefa
   * Hora de conclusão da tarefa
   * Duração da tarefa
   * Status da tarefa

   **Painel inferior direito:** Exibe os seguintes detalhes do histórico do processo selecionado:

   * Nome do processo
   * Iniciador do processo
   * Hora da data de atualização do processo
   * Hora de conclusão do processo
   * Status do processo

   **Resultado dos Detalhes da tarefa**

   ![task_details](assets/task_details.png)

   **Painel esquerdo:** Exibe os seguintes detalhes da tarefa selecionada:

   * Nome da tarefa
   * ID do processo ao qual esta tarefa pertence
   * Descrição da tarefa
   * Data de criação da tarefa
   * Hora de conclusão da tarefa
   * Duração da tarefa
   * Status da tarefa
   * Rota de tarefa selecionada

   **Painel Superior direito:** Exibe os seguintes detalhes dos formulários que compõem a tarefa selecionada:

   * ID do formulário
   * Data de criação do formulário
   * Data de atualização do formulário
   * Url do modelo de formulário

   **Painel inferior direito:** Exibe os seguintes detalhes do histórico de processos da tarefa selecionada:

   * Tipo de atribuição da tarefa
   * Proprietário da tarefa
   * Hora de criação da atribuição da tarefa
   * Hora da atualização da tarefa






1. Clique em **Voltar para Pesquisa de Processo/Tarefa** voltar ao resultado da pesquisa do qual os detalhes do processo/tarefa foram detalhados.

   ![back_to_search](assets/back_to_search.png)

   No entanto, se os detalhes do processo/tarefa foram encontrados inserindo uma ID de processo/tarefa específica, clicar em Voltar para Processar/Pesquisa de tarefa o redirecionará para **Pesquisa de Processo/Tarefa**, sem exibir nenhum resultado de pesquisa.

#### Inserindo a ID Processo/Tarefa no painel Detalhes do Processo/Tarefa {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. Vá para o **Detalhes do Processo/Tarefa** painel.

   ![details_nodes](assets/details_nodes.png)

1. Na caixa de texto Process/Task ID , digite a ID do processo/tarefa.

   ![process_details-1](assets/process_details-1.png)

   Os campos no **Detalhes do Processo/Tarefa** o resultado da query são campos específicos de um processo/tarefa do AEM Forms.

   Para um processo, o resultado da consulta exibe os detalhes das tarefas contidas no processo.

   Para uma tarefa, o resultado da query exibe os detalhes dos formulários contidos na tarefa.
