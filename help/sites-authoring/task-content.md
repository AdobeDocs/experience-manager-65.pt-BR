---
title: Trabalhar com tarefas
description: As tarefas representam itens de trabalho a serem realizados no conteúdo e são usadas nos projetos para determinar a percentagem de conclusão das tarefas atuais
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
exl-id: a0719745-8d67-44bc-92ba-9ab07f31f8d2
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 41%

---


# Trabalhar com tarefas {#working-with-tasks}

As tarefas representam itens de trabalho a serem executados em relação ao conteúdo. Quando uma tarefa é atribuída, ela aparece na Caixa de entrada do fluxo de trabalho. Os itens da tarefa podem ser diferenciados dos itens do fluxo de trabalho pelo valor que **Tipo** coluna.

As tarefas também são usadas em projetos para determinar o nível de integridade do projeto.

## Monitoramento do progresso do projeto {#tracking-project-progress}

É possível acompanhar o progresso do projeto observando as tarefas ativas/concluídas dentro de um projeto representado pelo bloco de **Tarefas**. O progresso do projeto pode ser determinado por:

* **Mosaico de tarefas:** Um progresso geral do projeto é representado no bloco de tarefas, disponível na página de detalhes do projeto.

* **Lista de tarefas:** Ao clicar no bloco de tarefas, uma lista de tarefas é exibida. Essa lista contém informações detalhadas sobre todas as tarefas relacionadas ao projeto.

Ambas as opções listam tarefas de fluxo de trabalho e tarefas que você cria diretamente no bloco de tarefas.

### Bloco de tarefas {#task-tile}

Se um projeto tiver tarefas relacionadas, um bloco de tarefas será exibido dentro do projeto. O bloco de tarefas mostra o status atual do projeto. Isso se baseia em tarefas já existentes dentro do fluxo de trabalho e não inclui nenhuma tarefa que será gerada no futuro à medida que o fluxo de trabalho continua. As seguintes informações estão visíveis no bloco de tarefas:

* Porcentagem de tarefas concluídas
* Porcentagem de tarefas ativas
* Porcentagem de tarefas atrasadas

![Mosaico de tarefas](assets/project-tile-tasks.png)

### Visualização ou modificação das tarefas em um projeto {#viewing-or-modifying-the-tasks-in-a-project}

Além de monitorar o progresso, é possível exibir mais informações sobre o projeto ou modificá-lo.

#### Lista de tarefas {#task-list}

Clique no botão de reticências no canto inferior direito do bloco tarefas para exibir sua caixa de entrada filtrada nas tarefas relacionadas ao projeto. Os detalhes da tarefa são exibidos juntamente com metadados como prazo, responsável, prioridade e status.

![Caixa de entrada de tarefas do projeto](assets/project-tasks.png)

#### Detalhes da tarefa {#task-details}

Para obter mais informações sobre uma tarefa específica, na caixa de entrada, clique na tarefa para selecioná-la e clique em **Abertura** na barra de ferramentas.

![Detalhes da tarefa](assets/project-task-detail.png)

É possível exibir, editar ou adicionar detalhes à tarefa por meio de guias diferentes.

* **Tarefa** - Informações gerais sobre a tarefa
* **Informações do projeto** - Resumo do projeto ao qual a tarefa está associada
* **Informações do fluxo de trabalho** - Resumo do fluxo de trabalho ao qual a tarefa está associada (se aplicável)
* **Comentários** - Comentários gerais sobre a tarefa propriamente dita

### Adição de tarefas {#adding-tasks}

É possível adicionar novas tarefas a projetos. Essas tarefas são exibidas no bloco tarefas e estão disponíveis na caixa de entrada de notificações para que você esteja ciente de suas tarefas pendentes.

Para adicionar uma tarefa:

1. No projeto, localize o **Tarefas** bloco
1. Clique na divisa para baixo na parte superior direita do bloco e selecione **Criar tarefa**.
1. No **Adicionar tarefa** , forneça os detalhes da tarefa, como prioridade, destinatário e data de vencimento.

   ![Adicionar uma tarefa](assets/project-add-task.png)

1. Clique em **Enviar**.

## Trabalhando com tarefas na caixa de entrada {#working-with-tasks-in-the-inbox}

Em vez de acessar as tarefas do projeto diretamente do projeto, você pode acessá-las diretamente na caixa de entrada. Sua caixa de entrada fornece uma visão geral das tarefas entre projetos para que você possa entender todo o seu fluxo de trabalho.

Na caixa de entrada, é possível abrir as tarefas e definir o status da tarefa. As tarefas também aparecem na sua caixa de entrada quando são atribuídas a um grupo de usuários ao qual você pertence. Nesse caso, qualquer membro do grupo pode executar o trabalho e concluir a tarefa.

![Caixa de entrada](assets/project-inbox.png)

Para concluir uma tarefa, selecione-a e clique em **Concluído** na barra de ferramentas. Adicione informações à tarefa e clique em **Concluído**. Consulte [Sua Caixa de entrada](/help/sites-authoring/inbox.md) para obter mais informações.
