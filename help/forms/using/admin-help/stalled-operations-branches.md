---
title: Trabalhar com operações e ramificações paralisadas
description: As páginas Operações Paralisadas e Ramificações Paralisadas mostram os processos que foram paralisados.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---

# Trabalhar com operações e ramificações paralisadas {#working-with-stalled-operations-and-branches}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

As páginas Operações Paralisadas e Ramificações Paralisadas mostram os processos que foram paralisados. Um processo pode ser paralisado quando ocorre um erro durante ou após a execução de uma operação ou devido a uma operação de paralisação deliberada no processo:

* As operações podem parar devido a um erro imprevisto. No entanto, uma operação de Stall Branch em um processo impede deliberadamente que um processo seja executado ainda mais e requer a intervenção do administrador.
* As ramificações podem travar entre operações durante uma avaliação de regra.

Quando um processo é interrompido, nenhuma outra operação é executada até que o problema seja corrigido e a operação ou ramificação seja reiniciada.

Para cada item paralisado, a lista mostra as seguintes informações:

**Nome da Operação ou da Ramificação:** O nome da operação ou ramificação.

**Status:** Sempre PARADO para itens paralisados.

**Erro:** Uma breve descrição do problema.

**ID do Processo:** O número inteiro positivo que o fluxo de trabalho de formulários atribui quando o processo é instanciado (ou seja, quando um usuário ou uma etapa automatizada inicia um processo). Você pode usar esse identificador para rastrear a instância do processo por meio de seu ciclo de vida.

**Nome do Processo - Versão:** O nome do processo atribuído no Workbench.

**Data de Paralisação:** A data e a hora em que a operação ou ramificação foi paralisada.

Você pode executar as seguintes tarefas na página Operações interrompidas ou Ramificações interrompidas:

* Selecione um erro para exibir detalhes sobre ele. Quando você seleciona um erro, a página Detalhes do Erro é exibida.
* Encerre ou repita operações interrompidas ou repita ramificações interrompidas.

## Encerrando ou repetindo operações ou ramificações paralisadas {#terminating-or-retrying-stalled-operations-or-branches}

Na página Operações Paralisadas, é possível encerrar as instâncias do processo exibidas.

Quando você encerra uma instância de processo, ela para de ser executada e não ocorre mais nenhuma operação. Normalmente, você encerra um processo somente se ele se tornar bloqueado ou inutilizável devido a um erro e não puder ser corrigido e reiniciado.

Na página Operações interrompidas ou na página Ramificações interrompidas, você pode repetir a operação ou ramificação.

Quando você repete uma operação, o fluxo de trabalho do Forms recebe uma solicitação para reiniciar a operação. Se o erro que causou a paralisação do processo for corrigido e a solicitação de repetição for bem-sucedida, o processo começará a ser executado novamente a partir do ponto em que foi interrompido e seu status será alterado para RUNNING. Se a operação não puder ser reiniciada, ela permanecerá STALLED e talvez seja necessário encerrá-la.

### Encerrar uma operação paralisada {#terminate-a-stalled-operation}

1. No console de administração, clique em Serviços > Fluxo de trabalho de formulários > Erros de operações paralisadas.
1. Na página Operações Paralisadas, selecione o item que deseja encerrar e clique em Encerrar.

### Tentar novamente uma operação ou ramificação paralisada {#retry-a-stalled-operation-or-branch}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários e, em seguida, clique em Erros de operações interrompidas ou Erros de ramificação interrompida.
1. Na página Operações interrompidas ou Ramificações interrompidas, selecione o item que deseja repetir e clique em Repetir.

## Exibir detalhes de erros sobre operações ou ramificações paralisadas {#viewing-error-details-about-stalled-operations-or-branches}

Se você selecionar um erro na lista de itens paralisados na página Operações Paralisadas ou Ramificações Paralisadas, a página Detalhes do Erro será exibida, mostrando detalhes sobre o erro que podem ajudá-lo a solucionar o problema.

A caixa na parte inferior da página contém as informações do erro.

Você também pode encerrar ou repetir operações interrompidas e repetir ramificações interrompidas na página Detalhes do Erro.

## O processo não pára quando o usuário de escalonamento não existe {#process-does-not-stall-when-escalation-user-does-not-exist}

Erros ocorrem quando a operação Atribuir Tarefa no serviço de Usuário de forms AEM é configurada para escalar a tarefa para outro usuário após um período específico e o usuário de escalação é deletado após a execução da operação Atribuir Tarefa, mas antes do escalonamento ocorrer.

Quando essa situação ocorre, o estado do processo e da tarefa não é alterado no tempo de escalação configurado e o escalonamento não ocorre, mas o processo não é interrompido. A seguinte mensagem é exibida no registro do servidor:

&quot;O principal especificado para escalonamento não é válido, para taskID: *number*, fila especificada: *number*.&quot;

Se o usuário de escalonamento for excluído antes que a tarefa seja gerada (antes que a operação Atribuir Tarefa seja executada), o processo será interrompido ou o evento de exceção InvalidPrincipal será lançado.

Para evitar esse problema, ao excluir um usuário, procure tarefas pertencentes a esse usuário e lide com elas de acordo. (Consulte [Trabalhar com tarefas](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
