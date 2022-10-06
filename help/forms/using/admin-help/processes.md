---
title: Gerenciamento de processos
seo-title: Managing Processes
description: A página Lista de Processos mostra os processos que um usuário iniciou ou que foram iniciados automaticamente. Saiba mais sobre como gerenciar os processos.
seo-description: The Process List page shows the processes that a user has initiated or that were started automatically. Learn more about managing the processes.
uuid: 4cd17400-681a-4e40-996c-7dda57ce449a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 37e702c2-8716-4360-a3eb-d9877b28cc86
exl-id: 21a2317d-3542-4ccb-98db-3cedf20c89ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 0%

---

# Gerenciamento de processos {#managing-processes}

A página Lista de Processos mostra os processos que um usuário iniciou ou que foram iniciados automaticamente.

1. No console de administração, clique em Services > Forms workflow > Forms workflow. A Lista de Processos mostra as seguintes informações:

   **Nome do processo - Versão:** O nome do processo, conforme definido no Workbench.

   **Aplicativo:** O aplicativo ao qual o processo pertence, conforme definido no Workbench.

   **Status:** Ativo significa que o processo é ativado para a versão do processo. Inativo significa que o processo é uma versão antiga que ainda tem instâncias de processo.

   **Data de criação:** A data e a hora em que o processo foi implantado.

1. Clique em um nome de processo para exibir suas instâncias de processo na página Instância de processo .

## Trabalhar com instâncias de processo {#working-with-process-instances}

Se você acessar a página Instância do Processo na página Lista de Processos, todas as instâncias do processo que você selecionou serão listadas. Se você acessar a página Instância do processo depois de realizar uma pesquisa, somente as instâncias do processo encontradas serão listadas.

Para cada instância do processo, a lista mostra as seguintes informações:

**ID do processo:** O identificador que o fluxo de trabalho de formulários atribui quando o processo é instanciado (ou seja, quando um usuário ou uma etapa automatizada inicia um processo). Você pode usar esse identificador para rastrear a instância do processo por meio de seu ciclo de vida.

**Nome do processo - Versão:** O nome do processo, conforme definido no Workbench.

**Status:** Indica se a instância do processo está em execução normalmente, alterando o estado ou parou. (Consulte Sobre status da instância do processo.)

**Data de criação:** A data e a hora em que a instância do processo foi criada.

**Data de atualização:** A data e a hora em que o status da instância do processo foi alterado pela última vez.

Você pode realizar as seguintes tarefas na página Instância do Processo:

* Selecione uma instância do processo para exibir detalhes, como operações e subprocessos. Quando você seleciona uma instância de processo, a página Detalhes da Instância de Processo é exibida.
* Suspender, remover a suspensão ou encerrar instâncias do processo.
* Procure por uma instância de processo. Para iniciar uma pesquisa, clique em Pesquisar.

### Sobre status da instância do processo {#about-process-instance-statuses}

Uma instância do processo, incluindo subprocessos, pode ter os seguintes status:

**CONCLUIR:** Todas as ramificações e operações na instância do processo foram concluídas. COMPLETE é o status final de uma instância de processo.

**CONCLUINDO:** O status da instância do processo está prestes a ser alterado para COMPLETE.

**INICIADO:** A instância do processo foi criada, mas ainda não está em execução. INITIATED é o primeiro status de uma instância de processo.

**EM EXECUÇÃO:** A instância do processo está sendo executada normalmente. Uma etapa automatizada pode estar em andamento ou a instância do processo pode estar recebendo entrada do usuário ou aguardando a interação do usuário.

**SUSPENSA:** A instância do processo foi suspensa por um administrador ou por uma etapa do processo. Nenhuma outra operação ocorrerá até que o status seja alterado.

**SUSPENSÃO:** O status está prestes a mudar para SUSPENDER. Se uma operação tiver sido projetada para ignorar solicitações de suspensão e ainda não tiver sido concluída, essa operação deverá ser concluída antes que a instância do processo seja suspensa.

**TERMINADO:** A instância do processo foi finalizada por um administrador.

**TERMINANDO:** O status está prestes a mudar para TERMINADO. Se uma operação tiver sido projetada para ignorar solicitações de finalização e ainda não tiver sido concluída, essa operação deverá ser concluída antes que a instância do processo seja encerrada.

**SUSPENSÃO:** O status está prestes a mudar para EXECUÇÃO depois de SUSPENDER.

>[!NOTE]
>
>Quando uma solicitação é feita para alterar o status de uma instância do processo (como suspender ou encerrar), a solicitação insere a fila de comandos para o fluxo de trabalho de formulários. Dependendo do tamanho da fila e da velocidade geral de processamento, o status exibido pode não ser alterado até que a página seja recarregada uma ou mais vezes.

### Suspender ou remover a suspensão das instâncias do processo {#suspend-or-unsuspend-process-instances}

Se você precisar solucionar um problema ou se souber que uma instância de processo encontrará um problema em uma etapa posterior devido a alguma condição externa, poderá suspender temporariamente a instância do processo.

Você pode suspender instâncias de processo com status EXECUTANDO.

Após suspender uma instância do processo, seu status será alterado para SUSPENDER, SUSPENDER e o processo será pausado em sua operação atual. A instância do processo permanece nesse status até que o status seja alterado para UNSUSPENDED.

Somente instâncias de processo com status SUSPENDER podem ser alteradas para NÃO SUSPENDER.

Quando você remove a suspensão de uma instância do processo, seu status muda para RUNNING e continua com a operação em que ela foi suspensa.

Quando você suspende uma instância de processo que tenha chamado outros processos (processos filhos) usando sua operação invoke, os processos filho também serão suspensos.

1. No console de administração, clique em Services > Forms workflow > Forms workflow.
1. Na página Instância do processo , selecione o processo e clique em Suspender ou Remover a suspensão.

### Encerrar instâncias de processo {#terminate-a-process-instances}

Se uma operação de uma instância de processo tiver parado ou encontrado alguma outra condição de erro, ou se for necessário forçar uma instância de processo a parar de ser executada, você poderá encerrar a instância de processo.

Você pode encerrar instâncias de processo que tenham qualquer status.

Quando você encerra uma instância do processo, seu status muda para TERMINANDO, depois TERMINADO e o processo para em sua operação atual. Nenhuma outra operação é executada e todas as operações e tarefas associadas são encerradas.

1. No console de administração, clique em Services > Forms workflow > Forms workflow.
1. Na página Instância do processo , selecione o processo e clique em Encerrar.

## Trabalhar com detalhes da instância de processo {#working-with-process-instance-details}

A página Detalhes da instância do processo mostra o histórico de uma instância do processo.

A área Resumo mostra informações básicas sobre a instância do processo.

Na guia Operations , cada operação da instância do processo é mostrada em ordem de conclusão da primeira à última com as seguintes informações:

**Nome da Operação:** O nome da operação, conforme definido no Workbench.

**Status:** Indica se a operação está sendo executada normalmente ou foi interrompida. (Consulte Sobre status da instância do processo.)

**Nome da ramificação:** O nome da ramificação, conforme definido no Workbench.

**Data de início:** A data e a hora em que a operação foi iniciada.

**Data de Conclusão:** A data e a hora em que a operação foi concluída.

Um subprocesso é uma instância de processo iniciada por outro processo e executada independentemente desse outro processo. Os subprocessos são exibidos somente se tiverem sido projetados como parte do processo no Workbench. Na guia Subprocessos , cada subprocesso é mostrado com as seguintes informações:

**ID do processo:** Esse número inteiro positivo que o fluxo de trabalho do Forms atribui quando o processo é instanciado (ou seja, quando um usuário ou uma etapa automatizada inicia o processo). Você pode usar esse identificador para rastrear a instância do processo por meio de seu ciclo de vida.

**Nome do processo - Versão:** O nome do processo, conforme definido no Designer.

**Status:** Indica se a instância do processo está sendo executada normalmente, alterando o estado ou interrompida. (Consulte Sobre status da instância do processo.)

**Data de criação:** A data e a hora em que o subprocesso foi criado.

**Data de atualização:** A data e a hora em que o status do subprocesso foi alterado pela última vez.

Você pode realizar as seguintes tarefas na página Detalhes da instância do processo :

* Selecione uma operação para exibir detalhes sobre ela. Quando você seleciona uma operação, a página Detalhes da Operação é exibida.
* Selecione um subprocesso para exibir detalhes. Quando você seleciona um subprocesso, a página Detalhes da instância do processo é exibida.
* Encerrar ou repetir operações ou subprocessos, dependendo de seu status.

### Sobre status de operação {#about-operation-statuses}

Uma operação (uma etapa em um processo) pode ter os seguintes status:

**CONCLUIR:** A operação foi concluída.

**EM EXECUÇÃO:** A operação está sendo executada normalmente. Ele pode estar recebendo entrada do usuário ou aguardando interação do usuário, ou uma etapa automatizada pode estar em andamento.

**PARADO:** Ocorreu um problema durante o processamento da operação. Verifique o erro ou a exceção na página de operações paralisadas.

**TERMINADO:** A operação foi finalizada por um administrador.

### Encerrar operações ou subprocessos {#terminate-operations-or-subprocesses}

Se uma operação ou subprocesso tiver parado ou encontrado alguma outra condição de erro, ou se for necessário forçar uma operação ou subprocesso a parar de ser executado, você poderá finalizá-lo.

É possível encerrar uma operação em EXECUÇÃO.

Quando você encerra uma operação, seu status muda para TERMINADO. A operação não é concluída e a instância do processo para de ser executada.

Você pode encerrar um subprocesso que tenha qualquer status.

Quando você encerra um subprocesso, seu status muda para TERMINANDO, depois TERMINADO e a instância do processo para em suas operações atuais. Nenhuma outra operação é executada no subprocesso, embora a instância do processo pai continue a ser executada.

Não é possível encerrar processos que têm elementos de gateway no diagrama de processos. Se você tentar encerrar esses tipos de processos, as operações dentro dos elementos do gateway não serão afetadas. Para encerrar as operações que estão dentro de um elemento de gateway, você deve encerrar as operações diretamente.

1. Na página Detalhes da instância do processo , clique na guia Operações ou na guia Subprocessos .
1. Selecione a operação ou subprocesso e clique em Encerrar.

### Repetir uma operação {#retry-an-operation}

Você pode repetir a operação que tem um status STALLED.

Quando você tenta uma operação novamente, o workflow do Forms é enviado com uma solicitação para reiniciar a operação. Se a solicitação for bem-sucedida, o status será alterado para EXECUTANDO. Se a operação não puder ser reiniciada, ela permanecerá PARADA e talvez seja necessário encerrá-la.

1. Na página Detalhes da instância do processo , clique na guia Operações.
1. Selecione a operação e clique em Repetir.

## Trabalhar com operações {#working-with-operations}

A página Detalhes da Operação mostra um resumo de uma operação em um processo e suas atribuições de usuário atuais.

1. No console de administração, clique em Services > Forms workflow > Forms workflow.
1. Clique em um nome de processo para exibir suas instâncias de processo. Clique em uma instância do processo para exibir a página Detalhes da Instância do Processo e selecione uma operação para exibir a página Detalhes da Operação.

   Para cada tarefa, a lista mostra as seguintes informações:

   **Nome do processo - Versão:** O nome do processo, conforme definido no Workbench.

   **Aplicativo:** O aplicativo ao qual o processo pertence, conforme definido no Workbench.

   **Status:** Ativo significa que o processo é ativado para a versão do processo. Inativo significa que o processo é uma versão antiga que ainda tem instâncias de processo.

   **Data de criação:** A data e a hora em que o processo foi implantado.
