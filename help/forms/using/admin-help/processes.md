---
title: Gerenciar processos
seo-title: Managing Processes
description: A página Lista de processos mostra os processos que um usuário iniciou ou que foram iniciados automaticamente. Saiba mais sobre como gerenciar os processos.
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

# Gerenciar processos {#managing-processes}

A página Lista de processos mostra os processos que um usuário iniciou ou que foram iniciados automaticamente.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Fluxo de trabalho do Forms. A Lista de Processos mostra as seguintes informações:

   **Nome do processo - Versão:** O nome do processo, conforme definido na Bancada.

   **Aplicativo:** O aplicativo ao qual o processo pertence, conforme definido no Workbench.

   **Status:** Ativo significa que é o processo ativado para a versão do processo. Inativo significa que o processo é uma versão antiga que ainda tem instâncias de processo.

   **Data de criação:** A data e a hora em que o processo foi implantado.

1. Clique em um nome de processo para exibir suas instâncias na página Instância do processo.

## Trabalhar com instâncias de processo {#working-with-process-instances}

Se você acessar a página Instância do processo a partir da página Lista de processos, todas as instâncias do processo selecionado serão listadas. Se você acessar a página Instância do Processo após executar uma pesquisa, somente as instâncias do processo encontradas serão listadas.

Para cada instância do processo, a lista mostra as seguintes informações:

**ID do processo:** O identificador que o fluxo de trabalho de formulários atribui quando o processo é instanciado (ou seja, quando um usuário ou uma etapa automatizada inicia um processo). Você pode usar esse identificador para rastrear a instância do processo por meio de seu ciclo de vida.

**Nome do processo - Versão:** O nome do processo, conforme definido na Bancada.

**Status:** Indica se a instância do processo está sendo executada normalmente, mudando de estado ou se foi interrompida. (Consulte Sobre status de instância de processo.)

**Data de criação:** A data e a hora em que a instância do processo foi criada.

**Data de atualização:** A data e a hora em que o status da instância do processo foi alterado pela última vez.

Você pode executar as seguintes tarefas na página Instância do Processo:

* Selecione uma instância de processo para exibir detalhes sobre ela, como operações e subprocessos. Quando você seleciona uma instância de processo, a página Detalhes da Instância de Processo é exibida.
* Suspender, cancelar suspensão ou encerrar instâncias de processo.
* Procure uma instância de processo. Para iniciar uma pesquisa, clique em Pesquisar.

### Sobre status de instância de processo {#about-process-instance-statuses}

Uma instância de processo, incluindo subprocessos, pode ter os seguintes status:

**CONCLUÍDO:** Todas as ramificações e operações na instância do processo foram concluídas. CONCLUÍDO é o status final de uma instância do processo.

**CONCLUINDO:** O status da instância do processo está prestes a ser alterado para COMPLETE.

**INICIADO:** A instância do processo foi criada, mas ainda não está em execução. INITIATED é o primeiro status de uma instância do processo.

**EM EXECUÇÃO:** A instância do processo está sendo executada normalmente. Uma etapa automatizada pode estar em andamento ou a instância do processo pode estar recebendo entrada do usuário ou aguardando a interação do usuário.

**SUSPENSO:** A instância do processo foi suspensa por um administrador ou por uma etapa do processo. Nenhuma outra operação ocorrerá até que o status seja alterado.

**SUSPENDENDO:** O status está prestes a mudar para SUSPENDED. Se uma operação tiver sido projetada para ignorar solicitações suspensas e ainda não tiver sido concluída, essa operação deverá ser concluída antes que a instância do processo seja suspensa.

**ENCERRADO:** A instância do processo foi encerrada por um administrador.

**ENCERRANDO:** O status está prestes a mudar para TERMINADO. Se uma operação tiver sido projetada para ignorar solicitações de encerramento e ainda não tiver sido concluída, essa operação deverá ser concluída antes que a instância do processo seja encerrada.

**CANCELANDO SUSPENSÃO:** O status está prestes a mudar para RUNNING após ter sido SUSPENDED.

>[!NOTE]
>
>Quando é feita uma solicitação para alterar o status de uma instância de processo (como suspender ou encerrar), a solicitação entra na fila de comandos para o fluxo de trabalho de formulários. Dependendo do tamanho da fila e da velocidade geral de processamento, o status exibido pode não ser alterado até que a página seja recarregada uma ou mais vezes.

### Suspender ou cancelar a suspensão de instâncias de processos {#suspend-or-unsuspend-process-instances}

Se você precisar solucionar um problema ou se souber que uma instância do processo encontrará um problema em uma etapa posterior devido a alguma condição externa, suspenda a instância do processo temporariamente.

Você pode suspender instâncias de processo com status de EM EXECUÇÃO.

Depois de suspender uma instância do processo, seu status será alterado para SUSPENDING e, em seguida, SUSPENDED, e o processo será pausado em sua operação atual. A instância do processo permanece nesse status até que o status seja alterado para UNSUSPENDED.

Somente as instâncias de processo com status SUSPENSO podem ser alteradas para UNSUSPENDED.

Quando você cancela a suspensão de uma instância do processo, seu status é alterado para RUNNING e ela continua com a operação em que foi suspensa.

Quando você suspende uma instância de processo que chamou outros processos (processos filhos) usando a operação de chamada, os processos filhos também são suspensos.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Fluxo de trabalho do Forms.
1. Na página Instância do Processo, selecione o processo e clique em Suspender ou Cancelar Suspensão.

### Encerrar instâncias de processos {#terminate-a-process-instances}

Se uma operação de uma instância de processo tiver sido paralisada ou se encontrar outra condição de erro, ou se você precisar forçar uma instância de processo a parar de ser executada, poderá encerrar a instância de processo.

Você pode encerrar instâncias de processo que tenham qualquer status.

Quando você encerra uma instância do processo, seu status muda para TERMINANDO, em seguida, TERMINADO e o processo é interrompido em sua operação atual. Nenhuma outra operação será executada e todas as operações e tarefas associadas serão encerradas.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Fluxo de trabalho do Forms.
1. Na página Instância do processo, selecione o processo e clique em Encerrar.

## Trabalhar com detalhes de instância de processo {#working-with-process-instance-details}

A página Detalhes da instância do processo mostra o histórico de uma instância do processo.

A área Resumo mostra informações básicas sobre a instância do processo.

Na guia Operações, cada operação da instância do processo é mostrada em ordem de conclusão, da primeira até a última, com as seguintes informações:

**Nome da operação:** O nome da operação, conforme definido na Bancada.

**Status:** Indica se a operação está sendo executada normalmente ou se parou. (Consulte Sobre status de instância de processo.)

**Nome da filial:** O nome da filial, conforme definido na Bancada.

**Data de início:** A data e a hora em que a operação foi iniciada.

**Data de conclusão:** A data e a hora em que a operação foi concluída.

Um subprocesso é uma instância de processo iniciada por outro processo e executada independentemente desse outro processo. Os subprocessos são exibidos somente se tiverem sido projetados como parte do processo no Workbench. Na guia Subprocessos, cada subprocesso é mostrado com as seguintes informações:

**ID do processo:** Esse número inteiro positivo que o workflow de formulários atribui quando o processo é instanciado (ou seja, quando um usuário ou uma etapa automatizada inicia o processo). Você pode usar esse identificador para rastrear a instância do processo por meio de seu ciclo de vida.

**Nome do processo - Versão:** O nome do processo, conforme definido no Designer.

**Status:** Indica se a instância do processo está sendo executada normalmente, mudando de estado ou parada. (Consulte Sobre status de instância de processo.)

**Data de criação:** A data e a hora em que o subprocesso foi criado.

**Data de atualização:** A data e a hora em que o status do subprocesso foi alterado pela última vez.

Você pode executar as seguintes tarefas na página Detalhes da instância do processo:

* Selecione uma operação para exibir detalhes sobre ela. Quando você seleciona uma operação, a página Detalhes da Operação é exibida.
* Selecione um subprocesso para exibir detalhes sobre ele. Quando você seleciona um subprocesso, a página Detalhes da instância do processo é exibida.
* Encerrar ou repetir operações ou subprocessos, dependendo de seu status.

### Sobre status de operação {#about-operation-statuses}

Uma operação (uma etapa em um processo) pode ter os seguintes status:

**CONCLUÍDO:** A operação foi concluída.

**EM EXECUÇÃO:** A operação está sendo executada normalmente. Ele pode estar recebendo entrada do usuário ou esperando a interação do usuário, ou uma etapa automatizada pode estar em andamento.

**PARALISADO:** Ocorreu um problema enquanto a operação estava sendo processada. Verifique o erro ou a exceção na página Operações Paralisadas.

**ENCERRADO:** A operação foi encerrada por um administrador.

### Encerrar operações ou subprocessos {#terminate-operations-or-subprocesses}

Se uma operação ou um subprocesso tiver sido interrompido ou encontrado alguma outra condição de erro, ou se você precisar forçar uma operação ou um subprocesso a parar de ser executado, poderá encerrá-lo.

Você pode encerrar uma operação que esteja em EXECUÇÃO.

Quando você encerra uma operação, seu status muda para ENCERRADO. A operação não é concluída e a instância do processo para de ser executada.

Você pode finalizar um subprocesso que tenha qualquer status.

Quando você encerra um subprocesso, seu status é alterado para TERMINANDO, em seguida, TERMINADO, e a instância do processo é interrompida em suas operações atuais. Nenhuma outra operação é executada no subprocesso, embora a instância do processo pai continue a ser executada.

Não é possível encerrar processos que tenham elementos de gateway no diagrama de processos. Se você tentar encerrar esses tipos de processos, as operações nos elementos do gateway não serão afetadas. Para encerrar operações que estão dentro de um elemento de gateway, você deve encerrar as operações diretamente.

1. Na página Detalhes da Instância do Processo, clique na guia Operações ou na guia Subprocessos.
1. Selecione a operação ou o subprocesso e clique em Encerrar.

### Tentar novamente uma operação {#retry-an-operation}

Você pode repetir uma operação que tenha o status STALLED.

Quando você repete uma operação, o fluxo de trabalho do Forms recebe uma solicitação para reiniciar a operação. Se a solicitação for bem-sucedida, o status será alterado para RUNNING. Se a operação não puder ser reiniciada, ela permanecerá INATIVA e talvez seja necessário encerrá-la.

1. Na página Detalhes da Instância do Processo, clique na guia Operações.
1. Selecione a operação e clique em Repetir.

## Trabalhar com operações {#working-with-operations}

A página Detalhes da Operação mostra um resumo de uma operação em um processo e suas atribuições de usuário atuais.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Fluxo de trabalho do Forms.
1. Clique em um nome de processo para exibir suas instâncias de processo. Clique em uma instância do processo para exibir a página Detalhes da Instância do Processo e selecione uma operação para exibir a página Detalhes da Operação.

   Para cada tarefa, a lista mostra as seguintes informações:

   **Nome do processo - Versão:** O nome do processo, conforme definido na Bancada.

   **Aplicativo:** O aplicativo ao qual o processo pertence, conforme definido no Workbench.

   **Status:** Ativo significa que é o processo ativado para a versão do processo. Inativo significa que o processo é uma versão antiga que ainda tem instâncias de processo.

   **Data de criação:** A data e a hora em que o processo foi implantado.
