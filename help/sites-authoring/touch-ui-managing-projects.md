---
title: Gerenciamento de projetos
description: O console de Projetos permite organizar o projeto, agrupando os recursos em uma única entidade que pode ser acessada e gerenciada no próprio console
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
exl-id: 62586c8e-dab4-4be9-a44a-2c072effe3c0
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 18%

---


# Gerenciamento de projetos {#managing-projects}

No console **Projetos**, você acessa e gerencia seus projetos.

![O console de projetos](assets/projects-console.png)

Usando o console, você pode criar um projeto, associar recursos ao projeto e também excluir um projeto ou links de recursos.

## Requisitos de acesso {#access-requirements}

Projeta um recurso padrão do AEM e não requer configuração adicional.

No entanto, para que os usuários em projetos possam ver outros usuários/grupos enquanto usam Projetos, como ao criar projetos, criar tarefas/fluxos de trabalho ou exibir e gerenciar a equipe, eles precisam ter acesso de leitura a `/home/users` e `/home/groups`.

A maneira mais fácil de fazer isso é conceder ao grupo **projetos-usuários** acesso de leitura a `/home/users` e `/home/groups`.

## Criação de um projeto {#creating-a-project}

Siga estas etapas para criar um projeto.

1. No console **Projetos**, clique em **Criar** para abrir o assistente **Criar Projeto**.
1. Selecione um modelo e clique em **Próximo**. Você pode saber mais sobre os modelos de projeto padrão [aqui.](/help/sites-authoring/projects.md#project-templates)

   ![Assistente para criação de projeto](assets/create-project-wizard.png)

1. Defina o **Título** e a **Descrição** e adicione uma imagem de **Miniatura**, se necessário. Também é possível adicionar ou excluir usuários e a qual grupo eles pertencem.

   ![Etapa de propriedades do assistente](assets/create-project-wizard-properties.png)

1. Clique em **Criar**. Você é solicitado(a) a confirmar se deseja abrir o novo projeto ou retornar ao console.

O procedimento para criar um projeto é o mesmo para todos os modelos de projeto. A diferença entre os tipos de projetos está relacionada às [funções de usuário](/help/sites-authoring/projects.md) e [fluxos de trabalho.](/help/sites-authoring/projects-with-workflows.md) disponíveis

### Associando recursos ao seu projeto {#associating-resources-with-your-project}

Os projetos permitem agrupar recursos em uma entidade para gerenciá-los como um todo. Portanto, é necessário associar recursos ao projeto. Estes recursos estão agrupados no projeto como **Blocos**. Os tipos de recursos que você pode adicionar estão descritos em [Blocos de projeto](/help/sites-authoring/projects.md#project-tiles).

Para associar recursos ao projeto:

1. Abra o projeto no console **Projetos**.
1. Clique em **Adicionar bloco** e selecione o bloco que deseja vincular ao seu projeto. É possível selecionar vários tipos de mosaicos.

   ![Adicionar mosaico](assets/project-add-tile.png)

1. Clique em **Criar**. O recurso é vinculado ao seu projeto e a partir de agora é possível acessá-lo do próprio projeto.

### Adicionar itens a um bloco {#adding-items-to-a-tile}

Talvez você queira adicionar mais de um item em alguns blocos. Por exemplo, você pode ter mais de um fluxo de trabalho em execução ao mesmo tempo ou mais de uma experiência.

Para adicionar itens a um bloco:

1. Em **Projetos**, navegue até o projeto e clique no ícone de divisa para baixo na parte superior direita do bloco ao qual deseja adicionar um item e selecione a opção apropriada.

   * A opção depende do tipo de bloco. Por exemplo, pode ser **Criar Tarefa** para o bloco **Tarefas** ou **Iniciar Fluxo de Trabalho** para o bloco **Fluxos de Trabalho**.

   ![Divisa do bloco](assets/project-tile-create-task.png)

1. Adicione o item ao bloco da mesma maneira que você faria ao criar um bloco. Os mosaicos do projeto estão descritos [aqui.](/help/sites-authoring/projects.md#project-tiles)

## Exibindo Informações do Projeto {#viewing-project-info}

O principal objetivo dos projetos é agrupar informações associadas em um local para torná-las mais acessíveis e acionáveis. Há várias maneiras de acessar essas informações.

### Abrir um bloco {#opening-a-tile}

Você pode querer ver quais itens estão incluídos no bloco atual, ou modificar e excluir itens no bloco.

Para abrir um bloco e visualizar ou modificar itens:

1. Clique no ícone de reticências na parte inferior direita do bloco.

   ![Bloco de tarefas](assets/project-tile-tasks.png)

1. O AEM abre o console para os tipos de itens associados ao bloco e filtros com base no projeto selecionado.

   ![Tarefas do projeto](assets/project-tasks.png)

### Visualizar uma linha do tempo do projeto {#viewing-a-project-timeline}

A linha do tempo do projeto fornece informações sobre quando os ativos do projeto foram usados pela última vez. Para exibir a linha do tempo do projeto, siga estas etapas.

1. No console **Projetos**, clique em **Linha do tempo** no seletor do painel na parte superior esquerda do console.
   ![Selecionando o modo de linha de tempo](assets/projects-timeline-rail.png)
2. No console, selecione o projeto para o qual deseja exibir sua linha do tempo.
   ![Exibição da linha do tempo do projeto](assets/project-timeline-view.png)

O Assets é exibido no painel. Use o seletor de painéis para retornar à exibição normal quando terminar.

### Visualizando projetos inativos {#viewing-active-inactive-projects}

Para alternar entre os projetos ativos e [inativos](#making-projects-inactive-or-active), no console **Projetos**, clique no ícone **Alternar projetos ativos**, na barra de ferramentas.

![Alternar ícone de projetos ativos](assets/projects-toggle-active.png)

Por padrão, o console mostra os projetos ativos. Clique no ícone **Alternar projetos ativos** uma vez para alternar para a exibição de projetos inativos. Clique nele novamente para voltar para projetos ativos.

## Organização de projetos {#organizing-projects}

Há várias opções disponíveis para ajudar a organizar seus projetos para manter o console de **Projetos** gerenciável.

### Pastas de Projeto {#project-folders}

Você pode criar pastas no console **Projetos** para agrupar e organizar projetos semelhantes.

1. No console **Projetos**, clique em **Criar** e em **Criar Pasta**.

   ![Criar pasta](assets/project-create-folder.png)

1. Dê um título à sua pasta e clique em **Criar**.

1. A pasta é adicionada ao console.

Agora você pode criar projetos dentro da pasta. É possível criar várias pastas e também aninhar pastas.

### Desativação de projetos {#making-projects-inactive-or-active}

Você pode marcar um projeto como inativo se ele for concluído, mas ainda assim manter as informações sobre ele. [Os projetos inativos agora mostram](#viewing-active-inactive-projects) por padrão no console **Projetos**.

Para tornar um projeto inativo, siga estas etapas.

1. Abra a janela **Propriedades do projeto** do projeto.
   * Você pode fazer isso no console selecionando o projeto ou no projeto por meio do bloco **Informações do projeto**.
1. Na janela **Propriedades do Projeto**, altere o controle deslizante **Status do Projeto** de **Ativo** para **Inativo**.

   ![Seletor de status de projeto na janela de propriedades](assets/project-status.png)

1. Clique em **Salvar e fechar** para salvar suas alterações.

### Exclusão de projetos {#deleting-a-project}

Siga estas etapas para excluir um projeto.

1. Navegue até o nível superior do console **Projetos**.
1. Selecionar o projeto no console.
1. Clique em **Excluir** na barra de ferramentas.
1. O AEM pode remover/modificar dados de projeto associados ao excluir o projeto. Selecione quais opções são necessárias na caixa de diálogo **Excluir projeto**.
   * Remover os grupos e as funções do projeto
   * Excluir a pasta do Assets do projeto
   * Encerrar fluxos de trabalho do projeto

   ![Opções de exclusão do projeto](assets/project-delete-options.png)
1. Clique em **Excluir** para excluir o projeto com as opções selecionadas.

Para saber mais sobre os grupos criados automaticamente pelos projetos, consulte [Criação automática de grupos](/help/sites-authoring/projects.md#auto-group-creation) para obter detalhes.
