---
title: Trabalhar com tarefas
description: Utilize a página Pesquisa de Tarefas para procurar tarefas por nome de usuário ou ID de tarefa. Saiba mais sobre como trabalhar com tarefas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 375376d1-60b3-49a4-8893-ba9336e6bf7b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# Trabalhar com tarefas {#working-with-tasks}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Utilize a página Pesquisa de Tarefas para procurar tarefas por nome de usuário ou ID de tarefa. Os resultados da pesquisa são exibidos na página Lista de tarefas, onde você pode acessar o histórico de uma tarefa. Você também pode reatribuir uma tarefa se um usuário tiver muitas tarefas ou se um usuário tiver recebido uma atribuição de tarefa por engano.

>[!NOTE]
>
>A execução de pesquisas de tarefas não retorna nenhum resultado para nomes de usuário que comecem com um sinal numérico (#). Se possível, evite criar nomes de usuário que comecem com um sinal numérico.

## Procurar tarefas associadas a um usuário {#search-for-tasks-associated-with-a-user}

1. No console de administração, clique em Serviços > Fluxo de trabalho de formulários > Pesquisa de tarefa.
1. Em Pesquisar por, selecione Nome do Usuário. Se você souber parte do nome de usuário que está procurando, digite-o na caixa. Clique em Localizar usuário.
1. A página Localizar Usuário é exibida. Você pode refinar sua pesquisa ainda mais, pesquisando por nome de usuário ou email. Quando localizar o usuário que você está procurando, selecione o botão de opção ao lado do nome e clique em OK.
1. Por padrão, a pesquisa de tarefas procura tarefas que estão atribuídas atualmente ao usuário. Para pesquisar também as tarefas que foram atribuídas anteriormente ao usuário, selecione Mostrar tarefa não atribuída. Para pesquisar também as tarefas que o usuário concluiu, selecione Mostrar tarefa concluída.
1. Clique em Pesquisar. A página Lista de tarefas é exibida, listando o resultado da pesquisa.

## Procurar uma tarefa quando souber sua ID {#search-for-a-task-when-you-know-its-task-id}

1. No console de administração, clique em Serviços > Fluxo de trabalho de formulários > Pesquisa de tarefa.
1. Em Pesquisar por, selecione ID de tarefa e digite a ID da tarefa na caixa.
1. Clique em Pesquisar. A página Lista de tarefas é exibida, listando o resultado da pesquisa.

## Trabalhar com a lista de tarefas {#working-with-the-task-list}

Os resultados de uma pesquisa de tarefa são exibidos na página Lista de tarefas. Você pode selecionar uma tarefa para abrir a página Histórico da Tarefa. A partir daí, você pode atribuir a tarefa a outro usuário.

As tarefas são exibidas com as seguintes informações:

**ID da Tarefa:** o número inteiro positivo que o fluxo de trabalho de formulários atribui quando a tarefa é instanciada (iniciada por um usuário). Você pode usar esse identificador para rastrear a tarefa pelo seu ciclo de vida. Clique em um ID de tarefa para exibir detalhes sobre o histórico da tarefa ou para reatribuir a tarefa a outro usuário.

**Status:** Atribuído significa que a tarefa está atualmente atribuída ao usuário. Não atribuída significa que a tarefa foi atribuída anteriormente ao usuário. O status também pode ser Concluído.

**Atividade:** mostra o formulário e o nome de uma operação inicial ou da operação de processo que gerou a tarefa.

**ID do Processo:** Este número inteiro positivo atribuído pelo fluxo de trabalho de formulários quando o processo é instanciado (ou seja, quando um usuário ou uma etapa automatizada inicia um processo). Você pode usar esse identificador para rastrear a instância do processo por meio de seu ciclo de vida.

**Nome do Processo - Versão:** O nome do processo, conforme definido no Workbench.

**Aplicativo:** o nome do aplicativo ao qual o processo pertence, conforme definido no Workbench.

**Data de Criação:** A data e a hora em que a tarefa foi criada.

## Exibição do histórico de tarefas e reatribuição de tarefas {#viewing-task-history-and-reassigning-tasks}

A página Histórico de Tarefas mostra uma lista de usuários e grupos que foram designados a uma tarefa específica.

Para cada atribuição de tarefa, a lista mostra as seguintes informações:

**Nome:** O nome do usuário.

**Status:** Atribuído significa que a tarefa está atualmente atribuída ao usuário. Não atribuída significa que a tarefa foi atribuída anteriormente ao usuário.

**ID da Lista de Trabalho:** O identificador numérico da fila de usuários à qual a tarefa pertence. Um processo pode ser compartilhado entre vários usuários.

**Tipo:** Indica como a tarefa foi atribuída:

**Inicial:** O usuário foi atribuído originalmente à tarefa.

**Encaminhar:** o proprietário original da tarefa atribuiu a tarefa a outro usuário.

**Rejeitar:** uma tarefa encaminhada foi rejeitada ou uma tarefa foi retornada a uma lista de trabalho sem ter sido concluída.

**Declaração:** o usuário solicitou a tarefa em uma lista de trabalho compartilhada.

**Escalonamento:** um tempo predeterminado decorrido (conforme definido na ação Usuário no Workbench) sem interação com o usuário e outro usuário foi atribuído à tarefa.

**Consulta:** o proprietário da tarefa encaminhou esta tarefa para outro usuário para consulta, que pode abrir o formulário, salvar dados, modificar os anexos e as anotações, mas não pode concluir a etapa. O usuário deve retornar a tarefa para o proprietário da tarefa que consultou o usuário.

**Reatribuição de Administrador:** A tarefa foi reatribuída por um administrador.

**Data de atribuição:** a data e a hora em que a tarefa foi atribuída ao usuário.

### Atribuir um novo usuário a uma tarefa {#assigning-a-new-user-to-a-task}

A página Atribuir Usuário lista os usuários que podem ser atribuídos a uma tarefa. Você acessa a página Atribuir usuário clicando em Atribuir novo usuário na página Histórico da tarefa.

1. Na caixa Procurar da página Atribuir usuário, digite parte ou todo o nome de usuário ou endereço de email necessário.
1. Em Uso, selecione Nome ou Endereço de email e clique em Localizar. Os usuários que correspondem à pesquisa são exibidos.
1. Selecione o usuário na lista e clique em OK. A página Histórico da Tarefa é exibida com a nova atribuição do usuário.
