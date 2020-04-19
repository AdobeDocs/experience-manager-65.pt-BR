---
title: Gerenciamento de processos
seo-title: Gerenciamento de processos
description: A página Lista do processo mostra os processos que um usuário iniciou ou que foram iniciados automaticamente. Saiba mais sobre como gerenciar os processos.
seo-description: A página Lista do processo mostra os processos que um usuário iniciou ou que foram iniciados automaticamente. Saiba mais sobre como gerenciar os processos.
uuid: 4cd17400-681a-4e40-996c-7dda57ce449a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 37e702c2-8716-4360-a3eb-d9877b28cc86
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Gerenciamento de processos {#managing-processes}

A página Lista do processo mostra os processos que um usuário iniciou ou que foram iniciados automaticamente.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Fluxo de trabalho do Forms. A Lista Process mostra as seguintes informações:

   **Nome do processo - Versão:** O nome do processo, conforme definido no Workbench.

   **Aplicativo:** O aplicativo ao qual o processo pertence, conforme definido no Workbench.

   **Status:** Ativo significa que o processo é ativado para a versão do processo. Inativo significa que o processo é uma versão antiga que ainda tem instâncias de processo.

   **Data de criação:** A data e a hora em que o processo foi implantado.

1. Clique em um nome de processo para visualização suas instâncias de processo na página Instância de processo.

## Trabalhar com instâncias de processo {#working-with-process-instances}

Se você acessar a página Instância do processo na página Lista do processo, todas as instâncias do processo selecionadas serão listadas. Se você acessar a página Instância do processo depois de executar uma pesquisa, somente as instâncias do processo encontradas serão listadas.

Para cada instância do processo, a lista mostra as seguintes informações:

**ID do processo:** O identificador que o fluxo de trabalho dos formulários atribui quando o processo é instanciado (ou seja, quando um usuário ou uma etapa automática inicia um processo). É possível usar esse identificador para rastrear a instância do processo por todo o ciclo de vida.

**Nome do processo - Versão:** O nome do processo, conforme definido no Workbench.

**Status:** Indica se a instância do processo está sendo executada normalmente, alterando o estado ou se foi interrompida. (Consulte Sobre os status da instância do processo.)

**Data de criação:** A data e a hora em que a instância do processo foi criada.

**Data de atualização:** A data e a hora em que o status da instância do processo foi alterado pela última vez.

Você pode fazer as seguintes tarefas na página Instância do Processo:

* Selecione uma instância do processo para visualização de detalhes sobre ela, como suas operações e subprocessos. Quando você seleciona uma instância do processo, a página Detalhes da instância do processo é exibida.
* Suspender, cancelar a suspensão ou encerrar instâncias do processo.
* Procure uma instância do processo. Para iniciar uma pesquisa, clique em Pesquisar.

### Sobre os status da instância do processo {#about-process-instance-statuses}

Uma instância do processo, incluindo subprocessos, pode ter os seguintes status:

**CONCLUÍDO:** Todas as ramificações e operações na instância do processo foram concluídas. COMPLETE é o status final de uma instância do processo.

**CONCLUINDO:** O status da instância do processo está prestes a mudar para COMPLETE.

**INICIADO:** A instância do processo foi criada, mas ainda não está em execução. INITIATED é o primeiro status de uma instância do processo.

**EM EXECUÇÃO:** A instância do processo está sendo executada normalmente. Uma etapa automática pode estar em andamento ou a instância do processo pode estar recebendo entrada do usuário ou aguardando interação do usuário.

**SUSPENSA:** A instância do processo foi suspensa por um administrador ou por uma etapa do processo. Nenhuma outra operação ocorrerá até que o status seja alterado.

**SUSPENSÃO:** O status está prestes a mudar para SUSPENDER. Se uma operação tiver sido projetada para ignorar solicitações de suspensão e ainda não tiver sido concluída, essa operação deverá ser concluída antes que a instância do processo seja suspensa.

**TERMINADO:** A instância do processo foi encerrada por um administrador.

**TERMINANDO:** O status está prestes a mudar para TERMINADO. Se uma operação tiver sido projetada para ignorar solicitações de encerramento e ainda não tiver sido concluída, ela deverá ser concluída antes que a instância do processo seja encerrada.

**SUSPENSÃO:** O status está prestes a mudar para RUNNING depois de SUSPENDER.

>[!NOTE]
>
>Quando uma solicitação é feita para alterar o status de uma instância do processo (como suspender ou encerrar), ela entra na fila de comandos para o fluxo de trabalho dos formulários. Dependendo do tamanho da fila e da velocidade geral de processamento, o status exibido pode não ser alterado até que a página seja recarregada uma ou mais vezes.

### Suspender ou remover a suspensão de instâncias de processo {#suspend-or-unsuspend-process-instances}

Se você precisar solucionar um problema ou se souber que uma instância do processo encontrará um problema posteriormente devido a alguma condição externa, poderá suspender a instância do processo temporariamente.

É possível suspender instâncias de processo com status de EXECUÇÃO.

Após suspender uma instância do processo, seu status é alterado para SUSPENDER, SUSPENDER e o processo é pausado na operação atual. A instância do processo permanece nesse status até que o status seja alterado para UNSUSPENDED.

Somente instâncias de processo com status SUSPENDER podem ser alteradas para UNSUSPENDED.

Quando você remove a suspensão de uma instância do processo, seu status muda para EXECUÇÃO e continua com a operação na qual ela foi suspensa.

Quando você suspende uma instância de processo que tenha chamado outros processos (processos filhos) usando sua operação de chamada, os processos filhos também são suspensos.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Fluxo de trabalho do Forms.
1. Na página Instância do processo, selecione o processo e clique em Suspender ou Cancelar suspensão.

### Encerrar instâncias de um processo {#terminate-a-process-instances}

Se uma operação de uma instância de processo tiver parado ou encontrado alguma outra condição de erro, ou se for necessário forçar uma instância de processo a parar de ser executada, você poderá encerrar a instância de processo.

É possível encerrar instâncias de processo que tenham qualquer status.

Quando você encerra uma instância do processo, seu status muda para TERMINANDO, TERMINADO e o processo para na operação atual. Nenhuma outra operação é executada e todas as operações e tarefas associadas são encerradas.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Fluxo de trabalho do Forms.
1. Na página Instância do processo, selecione o processo e clique em Terminar.

## Trabalhar com detalhes da instância do processo {#working-with-process-instance-details}

A página Detalhes da instância do processo mostra o histórico de uma instância do processo.

A área Resumo mostra informações básicas sobre a instância do processo.

Na guia Operações, cada operação para a instância do processo é mostrada na ordem de conclusão da primeira para a última com as seguintes informações:

**Nome da Operação:** O nome da operação, conforme definido no Workbench.

**Status:** Indica se a operação está sendo executada normalmente ou se foi interrompida. (Consulte Sobre os status da instância do processo.)

**Nome da ramificação:** O nome da ramificação, conforme definido no Workbench.

**Data do Start:** A data e a hora em que a operação foi iniciada.

**Data de conclusão:** A data e a hora em que a operação foi concluída.

Um subprocesso é uma instância de processo iniciada por outro processo e executada independentemente desse outro processo. Os subprocessos são exibidos somente se tiverem sido projetados como parte do processo no Workbench. Na guia Subprocessos, cada subprocesso é exibido com as seguintes informações:

**ID do processo:** Esse número inteiro positivo que forma o fluxo de trabalho atribui quando o processo é instanciado (ou seja, quando um usuário ou uma etapa automática inicia o processo). É possível usar esse identificador para rastrear a instância do processo por meio de seu ciclo de vida.

**Nome do processo - Versão:** O nome do processo, conforme definido no Designer.

**Status:** Indica se a instância do processo está sendo executada normalmente, alterando o estado ou parada. (Consulte Sobre os status da instância do processo.)

**Data de criação:** A data e a hora em que o subprocesso foi criado.

**Data de atualização:** A data e a hora em que o status do subprocesso foi alterado pela última vez.

Você pode fazer as seguintes tarefas na página Detalhes da instância do processo:

* Selecione uma operação para visualização de detalhes sobre ela. Quando você seleciona uma operação, a página Detalhes da operação é exibida.
* Selecione um subprocesso para visualização de detalhes sobre ele. Quando você seleciona um subprocesso, a página Detalhes da instância do processo é exibida.
* Encerrar ou repetir operações ou subprocessos, dependendo de seu status.

### Sobre status de operações {#about-operation-statuses}

Uma operação (uma etapa em um processo) pode ter os seguintes status:

**CONCLUÍDO:** A operação foi concluída.

**EM EXECUÇÃO:** A operação está sendo executada normalmente. Pode estar recebendo entrada do usuário ou aguardando interação do usuário, ou uma etapa automática pode estar em andamento.

**PARADO:** Ocorreu um problema durante o processamento da operação. Verifique o erro ou a exceção na página Operações paradas.

**TERMINADO:** A operação foi terminada por um administrador.

### Encerrar operações ou subprocessos {#terminate-operations-or-subprocesses}

Se uma operação ou subprocesso tiver parado ou encontrado alguma outra condição de erro, ou se for necessário forçar uma operação ou subprocesso a parar de ser executado, você poderá finalizá-lo.

Você pode encerrar uma operação em andamento.

Quando você encerra uma operação, seu status muda para TERMINADO. A operação não é concluída e a instância do processo para de ser executada.

É possível encerrar um subprocesso que tenha qualquer status.

Quando você encerra um subprocesso, seu status muda para TERMINANDO, TERMINADO e a instância do processo para em suas operações atuais. Nenhuma outra operação é executada no subprocesso, embora a instância do processo pai continue em execução.

Não é possível encerrar processos que tenham elementos de gateway no diagrama de processos. Se você tentar encerrar esses tipos de processos, as operações dentro dos elementos do gateway não serão afetadas. Para encerrar operações que estão dentro de um elemento de gateway, você deve encerrar as operações diretamente.

1. Na página Detalhes da instância do processo, clique na guia Operações ou na guia Subprocessos.
1. Selecione a operação ou o subprocesso e clique em Terminar.

### Repetir uma operação {#retry-an-operation}

Você pode repetir a operação com um status STALLED.

Quando você tenta uma operação novamente, o fluxo de trabalho do Forms recebe uma solicitação para reiniciar a operação. Se a solicitação for bem-sucedida, o status mudará para EXECUÇÃO. Se a operação não puder ser reiniciada, ela permanecerá PARADA e talvez seja necessário encerrá-la.

1. Na página Detalhes da instância do processo, clique na guia Operações.
1. Selecione a operação e clique em Repetir.

## Trabalhar com operações {#working-with-operations}

A página Detalhes da Operação mostra um resumo de uma operação em um processo e suas atribuições de usuário atuais.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Fluxo de trabalho do Forms.
1. Clique em um nome de processo para exibir suas instâncias de processo. Clique em uma instância do processo para exibir a página Detalhes da Instância do Processo e selecione uma operação para exibir a página Detalhes da Operação.

   Para cada tarefa, a lista mostra as seguintes informações:

   **Nome do processo - Versão:** O nome do processo, conforme definido no Workbench.

   **Aplicativo:** O aplicativo ao qual o processo pertence, conforme definido no Workbench.

   **Status:** Ativo significa que o processo é ativado para a versão do processo. Inativo significa que o processo é uma versão antiga que ainda tem instâncias de processo.

   **Data de criação:** A data e a hora em que o processo foi implantado.

