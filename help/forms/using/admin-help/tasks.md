---
title: Trabalhar com tarefas
seo-title: Working with tasks
description: Use a página Pesquisa de tarefa para procurar tarefas por nome de usuário ou ID de tarefa. Saiba mais sobre como trabalhar com tarefas.
seo-description: Use the Task Search page to search for tasks by user name or task ID. Learn more about working with tasks.
uuid: 630372d5-255f-4ea8-974d-d4f923108673
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9161c8ca-ef33-4ec9-affc-94b5b3e48a4c
exl-id: 375376d1-60b3-49a4-8893-ba9336e6bf7b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Trabalhar com tarefas {#working-with-tasks}

Use a página Pesquisa de tarefa para procurar tarefas por nome de usuário ou ID de tarefa. Os resultados da pesquisa são exibidos na página Lista de tarefas , onde você pode acessar o histórico de uma tarefa. Você também pode reatribuir uma tarefa se um usuário tiver muitas tarefas ou se um usuário tiver recebido uma atribuição de tarefa com erro.

>[!NOTE]
>
>Realizar pesquisas de tarefa não retorna resultados para nomes de usuário que comecem com um sinal de número (#). Se possível, evite criar nomes de usuário que comecem com um sinal de número.

## Pesquisar tarefas associadas a um usuário {#search-for-tasks-associated-with-a-user}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Pesquisa de tarefas.
1. Em Pesquisar por, selecione Nome de usuário. Se você souber parte do nome de usuário que está procurando, digite-o na caixa . Clique em Localizar Usuário.
1. A página Localizar Usuário é exibida. Você pode refinar sua pesquisa pesquisando ainda mais por nome de usuário ou email. Ao localizar o usuário que você está procurando, selecione o botão de opção ao lado do nome e clique em OK.
1. Por padrão, a pesquisa de tarefa procura tarefas que estão atribuídas ao usuário no momento. Para também procurar tarefas que foram atribuídas anteriormente ao usuário, selecione Mostrar tarefa não atribuída. Para também procurar tarefas que o usuário concluiu, selecione Mostrar tarefa concluída.
1. Clique em Pesquisar. A página Lista de tarefas é exibida, listando o resultado da pesquisa.

## Procurar uma tarefa quando souber a ID da tarefa {#search-for-a-task-when-you-know-its-task-id}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Pesquisa de tarefas.
1. Em Pesquisar por, selecione ID da tarefa e digite a ID da tarefa na caixa.
1. Clique em Pesquisar. A página Lista de tarefas é exibida, listando o resultado da pesquisa.

## Trabalhar com a lista de tarefas {#working-with-the-task-list}

Os resultados de uma pesquisa de tarefa são exibidos na página Lista de tarefas . Você pode selecionar uma tarefa para abrir a página Histórico de Tarefas . A partir daí, é possível atribuir a tarefa a outro usuário.

As tarefas são exibidas com as seguintes informações:

**ID da tarefa:** O número inteiro positivo que o fluxo de trabalho do Forms atribui quando a tarefa é instanciada (iniciada por um usuário). Você pode usar esse identificador para rastrear a tarefa por meio de seu ciclo de vida. Clique em uma ID de tarefa para exibir detalhes sobre o histórico de tarefas ou reatribuir a tarefa a outro usuário.

**Status:** Atribuída significa que a tarefa está atualmente atribuída ao usuário. Não atribuído significa que a tarefa foi atribuída anteriormente ao usuário. O status também pode ser Completed.

**Atividade:** Mostra o formulário e o nome de uma operação inicial ou da operação de processo que gerou a tarefa.

**ID do processo:** Esse número inteiro positivo atribuído pelo fluxo de trabalho de formulários quando o processo é instanciado (ou seja, quando um usuário ou uma etapa automatizada inicia um processo). Você pode usar esse identificador para rastrear a instância do processo por meio de seu ciclo de vida.

**Nome do processo - Versão:** O nome do processo, conforme definido no Workbench.

**Aplicativo:** O nome do aplicativo ao qual o processo pertence, conforme definido no Workbench.

**Data de criação:** A data e a hora em que a tarefa foi criada.

## Exibindo o histórico de tarefas e reatribuindo tarefas {#viewing-task-history-and-reassigning-tasks}

A página Histórico de tarefas mostra uma lista de usuários e grupos que foram atribuídos a uma tarefa específica.

Para cada atribuição de tarefa, a lista mostra as seguintes informações:

**Nome:** O nome do usuário.

**Status:** Atribuído significa que a tarefa está atualmente atribuída ao usuário. Não atribuído significa que a tarefa foi atribuída anteriormente ao usuário.

**ID da lista de trabalho:** O identificador numérico da fila de usuários à qual a tarefa pertence. Um processo pode ser compartilhado entre vários usuários.

**Tipo:** Indica como a tarefa foi atribuída:

**Inicial:** A tarefa foi atribuída originalmente ao usuário.

**Avançar:** O proprietário da tarefa original atribuiu a tarefa a outro usuário.

**Rejeitar:** Uma tarefa encaminhada foi rejeitada ou uma tarefa foi devolvida a uma lista de trabalho sem ter sido concluída.

**Reivindicação:** O usuário reivindicou a tarefa em uma lista de trabalho compartilhada.

**Escalonamento:** Um tempo predeterminado decorrido (como definido na ação Usuário no Workbench) sem interação do usuário e outro usuário foi atribuído à tarefa.

**Consultar:** O proprietário da tarefa encaminhou esta tarefa para outro usuário para consulta que pode abrir o formulário, salvar dados, modificar os anexos e notas, mas não pode concluir a etapa. O usuário deve retornar a tarefa ao proprietário da tarefa que foi consultado com o usuário.

**Reatribuição do administrador:** A tarefa foi reatribuída por um administrador.

**Data da Atribuição:** A data e a hora em que a tarefa foi atribuída ao usuário.

### Atribuição de um novo usuário a uma tarefa {#assigning-a-new-user-to-a-task}

A página Atribuir usuário lista os usuários que podem ser atribuídos a uma tarefa. Você acessa a página Atribuir usuário clicando em Atribuir novo usuário na página Histórico de tarefas .

1. Na caixa Pesquisar por na página Atribuir usuário , digite parte ou todo o nome de usuário ou endereço de email necessário.
1. Em Usar, selecione Nome ou Endereço de email e clique em Localizar. Os usuários que correspondem à pesquisa são exibidos.
1. Selecione o usuário na lista e clique em OK. A página Histórico de tarefas é exibida com a nova atribuição de usuário.
