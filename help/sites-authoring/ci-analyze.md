---
title: Análise do desempenho da página
description: Use a página Content Insight para analisar o desempenho da página que você está criando
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: 14484a90-4e44-4c85-9411-b78ed11dc70d
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Análise do desempenho da página{#analyzing-page-performance}

Abra o [Content Insight](/help/sites-authoring/content-insights.md) página para analisar o desempenho da página que você está criando. Configure o período do relatório para focalizar sua análise.

## Abrir o Analytics e o Recommendations em uma página {#opening-analytics-and-recommendations-for-a-page}

Use o procedimento a seguir para ver o Analytics e o Recommendations de uma página:

1. Navegue até a página que deseja analisar.
1. Na barra de ferramentas, clique em **Analytics e Recommendations**.

   >[!NOTE]
   >
   >O Analytics e o Recommendations para uma página somente serão exibidos se você tiver configurado o AEM para [integrar ao Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md).

   ![screen-shot_2019-03-05at115319](assets/screen-shot_2019-03-05at115319.png)

### Alteração do Período de Geração de Relatórios {#changing-the-reporting-period}

Altere os seguintes aspectos relacionados ao tempo dos relatórios de análise:

* O período no qual o relatório será gerado.
* A granularidade dos dados.

As ferramentas para alterar os aspectos relacionados ao tempo dos relatórios aparecem na parte superior da página Content Insight. ![chlimage_1-126](assets/chlimage_1-126.png)

#### Alteração do Período de Geração de Relatórios {#changing-the-reporting-period-1}

Altere o período de geração de relatório da página Content Insight para focalizar sua análise da atividade da página em um período específico. Quando você altera o período do relatório, os relatórios são atualizados automaticamente. A área sombreada no período representa o período do relatório. As datas no período aumentam da esquerda para a direita.

![chlimage_1-127](assets/chlimage_1-127.png)

Para alterar o período de geração de relatório de uma página de Content Insight:

1. Se o período de tempo não for exibido na parte superior da página, clique no ícone Alternar período de tempo.

   ![Alternar intervalo de tempo](do-not-localize/chlimage_1-22.png)

1. Para alterar a data de início do período do relatório, arraste o círculo que aparece no lado esquerdo da área sombreada para a data de início desejada.

   Se você não conseguir ver o lado esquerdo da área sombreada, use a barra de rolagem para exibi-la.

1. Para alterar a data final do período do relatório, arraste o círculo que aparece no lado direito da área sombreada para a data final desejada.

#### Alteração da Granularidade do Período de Geração de Relatórios {#changing-the-granularity-of-the-reporting-period}

Alterar o tempo que cada ponto de dados passa em um relatório. Por exemplo, quando a granularidade Semana é selecionada, cada ponto de dados no relatório Exibições representa o número de exibições para uma semana.

![screen_shot_2017-11-29at141001](assets/screen_shot_2017-11-29at141001.png)

A granularidade afeta os relatórios que plotam dados em relação ao tempo, como os relatórios Exibições e Média de páginas em minutos. A granularidade também afeta a escala do período.

1. Se o controle de granularidade não for exibido, clique no ícone Alternar granularidade.

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. Clique na granularidade desejada. Depois de selecionado, o relatório é atualizado automaticamente para refletir a granularidade.

### Atribuição de tarefas para SEO Recommendations {#assigning-tasks-for-seo-recommendations}

Use o relatório SEO Recommendations para criar tarefas a fim de melhorar a visibilidade da página para mecanismos de pesquisa. Para cada recomendação no relatório que não tem uma marca de seleção, você pode criar uma tarefa atribuída a um usuário para executar o trabalho necessário.

![chlimage_1-129](assets/chlimage_1-129.png)

O status da recomendação da SEO indica quando a tarefa foi criada, mas ainda não foi concluída.

![chlimage_1-130](assets/chlimage_1-130.png)

Quando criada, a tarefa aparece na lista Tarefas do usuário. Para obter informações sobre tarefas, consulte [Trabalhar com tarefas](/help/sites-authoring/task-content.md).

Use o procedimento a seguir para criar uma tarefa para uma recomendação da SEO.

1. Clique no ícone de informações da recomendação da SEO.

   ![Ícone de informação](do-not-localize/chlimage_1-23.png)

1. Clique no ícone de triângulo delimitado que aparece ao lado do ícone de informações.

   ![chlimage_1-131](assets/chlimage_1-131.png)

1. Preencha os campos de formulário exibidos e selecione Criar:

   * Projeto: Selecione o projeto no qual criar a tarefa.
   * Nome: o nome que identifica a tarefa. O nome padrão é o título da recomendação da SEO.
   * Atribuir a: selecione o usuário ao qual a tarefa será atribuída. Comece a digitar o nome do usuário para filtrar a lista.
   * Descrição: Uma descrição da atividade necessária para concluir a tarefa. A descrição padrão são as informações que acompanham a recomendação da SEO.
   * Prioridade da tarefa: a prioridade da tarefa.
   * Data de Vencimento: A data até a qual a tarefa deve ser concluída.

   **Nota:** A tarefa criada também inclui o caminho para a página à qual a recomendação de SEO se aplica.

1. Clique em Concluído para fechar a mensagem Tarefa criada.
