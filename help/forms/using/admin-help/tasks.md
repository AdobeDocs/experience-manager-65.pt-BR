---
title: Trabalhar com tarefas
seo-title: Trabalhar com tarefas
description: Use a página Pesquisa de tarefas para pesquisar tarefas por nome de usuário ou ID de tarefa. Saiba mais sobre como trabalhar com tarefas.
seo-description: Use a página Pesquisa de tarefas para pesquisar tarefas por nome de usuário ou ID de tarefa. Saiba mais sobre como trabalhar com tarefas.
uuid: 630372d5-255f-4ea8-974d-d4f923108673
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9161c8ca-ef33-4ec9-affc-94b5b3e48a4c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Working with tasks {#working-with-tasks}

Use a página Pesquisa de tarefas para pesquisar tarefas por nome de usuário ou ID de tarefa. Os resultados da pesquisa são exibidos na página Lista de tarefas, onde você pode acessar o histórico de uma tarefa. Você também pode reatribuir uma tarefa se um usuário tiver muitas tarefas ou se um usuário tiver recebido uma atribuição de tarefa por engano.

>[!NOTE]
>
>Executar pesquisas de tarefas não retorna resultados para nomes de usuários que começam com um sinal de número (#). Se possível, evite criar nomes de usuário que comecem com um sinal de número.

## Procurar tarefas associadas a um usuário {#search-for-tasks-associated-with-a-user}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Pesquisa de tarefas.
1. Em Pesquisar por, selecione Nome de usuário. Se você souber parte do nome de usuário que está procurando, digite-o na caixa. Clique em Localizar usuário.
1. A página Localizar usuário é exibida. Você pode refinar ainda mais sua pesquisa pesquisando por nome de usuário ou email. Ao localizar o usuário que você está procurando, selecione o botão de opção ao lado do nome e clique em OK.
1. Por padrão, a pesquisa da tarefa procura tarefas que estão atribuídas ao usuário no momento. Para também procurar tarefas que foram atribuídas anteriormente ao usuário, selecione Mostrar tarefa não atribuída. Para também procurar tarefas que o usuário tenha concluído, selecione Mostrar tarefa concluída.
1. Clique em Pesquisar. A página Lista de tarefas é exibida, listando o resultado da pesquisa.

## Procurar uma tarefa quando você souber a ID da tarefa {#search-for-a-task-when-you-know-its-task-id}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Pesquisa de tarefas.
1. Em Pesquisar por, selecione ID da tarefa e digite a ID da tarefa na caixa.
1. Clique em Pesquisar. A página Lista de tarefas é exibida, listando o resultado da pesquisa.

## Trabalhar com a lista de tarefas {#working-with-the-task-list}

Os resultados de uma pesquisa de tarefa são exibidos na página Lista de Tarefas. Você pode selecionar uma tarefa para abrir a página Histórico de Tarefas. Daí, você pode atribuir a tarefa a outro usuário.

As tarefas são exibidas com as seguintes informações:

**** ID da tarefa: O número inteiro positivo que o fluxo de trabalho do formulário atribui quando a tarefa é instanciada (iniciada por um usuário). É possível usar esse identificador para rastrear a tarefa por meio de seu ciclo de vida. Clique em uma ID de tarefa para exibir detalhes sobre o histórico de tarefas ou reatribuir a tarefa a outro usuário.

**** Status: Atribuída significa que a tarefa está atribuída ao usuário no momento. Não atribuído significa que a tarefa foi atribuída anteriormente ao usuário. O status também pode ser Concluído.

**** Atividade: Mostra o formulário e o nome de uma operação inicial ou a operação de processo que gerou a tarefa.

**** ID do processo: Esse número inteiro positivo que é atribuído pelo fluxo de trabalho dos formulários quando o processo é instanciado (ou seja, quando um usuário ou uma etapa automática inicia um processo). É possível usar esse identificador para rastrear a instância do processo por todo o ciclo de vida.

**** Nome do processo - Versão: O nome do processo, conforme definido no Workbench.

**** Aplicativo: O nome do aplicativo ao qual o processo pertence, conforme definido no Workbench.

**** Data de criação: A data e a hora em que a tarefa foi criada.

## Exibindo histórico de tarefas e reatribuindo tarefas {#viewing-task-history-and-reassigning-tasks}

A página Histórico de tarefas mostra uma lista dos usuários e grupos que foram atribuídos a uma tarefa específica.

Para cada atribuição de tarefa, a lista mostra as seguintes informações:

**** Nome: O nome do usuário.

**** Status: Atribuída significa que a tarefa está atribuída ao usuário no momento. Não atribuído significa que a tarefa foi atribuída anteriormente ao usuário.

**** ID da lista de trabalho: O identificador numérico da fila de usuários à qual a tarefa pertence. Um processo pode ser compartilhado entre vários usuários.

**** Tipo: Indica como a tarefa foi atribuída:

**** Inicial: A tarefa foi atribuída originalmente ao usuário.

**** Avançar: O proprietário da tarefa original atribuiu a tarefa a outro usuário.

**** Rejeitar: Uma tarefa encaminhada foi rejeitada ou uma tarefa foi devolvida a uma lista de trabalho sem ter sido concluída.

**** Reivindicação: O usuário solicitou a tarefa em uma lista de trabalho compartilhada.

**** Escalonamento: Um tempo predeterminado decorrido (conforme definido na ação Usuário no Workbench) sem interação do usuário e outro usuário recebeu a tarefa.

**** Consulta: O proprietário da tarefa encaminhou esta tarefa para outro usuário para consulta que pode abrir o formulário, salvar dados, modificar os anexos e observações, mas não pode concluir a etapa. O usuário deve retornar a tarefa ao proprietário da tarefa que foi consultado com o usuário.

**** Reatribuição do administrador: A tarefa foi reatribuída por um administrador.

**** Data da atribuição: A data e a hora em que a tarefa foi atribuída ao usuário.

### Atribuindo um novo usuário a uma tarefa {#assigning-a-new-user-to-a-task}

A página Atribuir usuário lista os usuários que podem ser atribuídos a uma tarefa. Para acessar a página Atribuir usuário, clique em Atribuir novo usuário na página Histórico de tarefas.

1. Na caixa Procurar na página Atribuir usuário, digite parte ou todo o nome de usuário ou endereço de email necessários.
1. Em Usando, selecione Nome ou Endereço de email e clique em Localizar. Os usuários que correspondem à pesquisa são exibidos.
1. Selecione o usuário na lista e clique em OK. A página Histórico de tarefas é exibida com a nova atribuição de usuário.

