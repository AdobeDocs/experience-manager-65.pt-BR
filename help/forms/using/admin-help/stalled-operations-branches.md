---
title: Trabalhar com operações e ramificações paralisadas
seo-title: Trabalhar com operações e ramificações paralisadas
description: As páginas Operações paradas e Ramificações paradas mostram os processos que pararam.
seo-description: As páginas Operações paradas e Ramificações paradas mostram os processos que pararam.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 0%

---


# Trabalhar com operações e ramificações paradas {#working-with-stalled-operations-and-branches}

As páginas Operações paradas e Ramificações paradas mostram os processos que pararam. Um processo pode parar quando ocorrer um erro durante ou após a execução de uma operação ou devido a uma operação deliberada de parada no processo:

* As operações podem parar devido a um erro imprevisto. No entanto, uma operação de Parar Ramificação em um processo interrompe deliberadamente a execução de um processo e requer a intervenção do administrador.
* As ramificações podem parar entre operações durante uma avaliação de regra.

Quando um processo é interrompido, nenhuma outra operação é executada até que o problema seja corrigido e a operação ou ramificação seja reiniciada.

Para cada item parado, a lista mostra as seguintes informações:

**Nome da Operação ou Nome da Ramificação:** O nome da operação ou ramificação.

**Status:** sempre parado para itens parados.

**Erro:** uma breve descrição do problema.

**ID do processo:** o número inteiro positivo que o fluxo de trabalho do formulário atribui quando o processo é instanciado (ou seja, quando um usuário ou uma etapa automática inicia um processo). É possível usar esse identificador para rastrear a instância do processo por todo o ciclo de vida.

**Nome do Processo - Versão:** O nome do processo atribuído no Workbench.

**Data de parada:** A data e a hora em que a operação ou ramificação parou.

Você pode fazer as seguintes tarefas na página Operações paradas ou Ramificações paradas:

* Selecione um erro para visualização de detalhes sobre ele. Quando você seleciona um erro, a página Detalhes do erro é exibida.
* Encerre ou tente novamente operações paradas ou tente novamente ramificações paradas.

## Terminando ou repetindo operações ou ramificações paradas {#terminating-or-retrying-stalled-operations-or-branches}

Na página Operações paradas, você pode encerrar as instâncias de processo exibidas.

Quando você encerra uma instância do processo, ela para de ser executada e nenhuma outra operação acontece. Normalmente, você encerra um processo somente se ele se tornar bloqueado ou inutilizável devido a um erro e não puder ser corrigido e reiniciado.

Na página Operações paradas ou na página Ramificações paradas, você pode repetir a operação ou ramificação.

Quando você tenta uma operação novamente, o fluxo de trabalho da Forms recebe uma solicitação para reiniciar a operação. Se o erro que causou a paralisação do processo tiver sido corrigido e a solicitação de nova tentativa for bem-sucedida, o processo começará a ser executado novamente a partir do ponto em que havia parado e seu status mudará para EXECUÇÃO. Se a operação não puder ser reiniciada, ela permanecerá PARADA e talvez seja necessário encerrá-la.

### Encerrar uma operação parada {#terminate-a-stalled-operation}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Erros de operações instaladas.
1. Na página Operações paradas, selecione o item que deseja encerrar e clique em Encerrar.

### Repita uma operação ou ramificação parada {#retry-a-stalled-operation-or-branch}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários e, em seguida, clique em Erros de operações paradas ou Erros de ramificação parados.
1. Na página Operações paradas ou Ramificações paradas, selecione o item que deseja repetir e clique em Repetir.

## Exibindo detalhes do erro sobre operações ou ramificações paradas {#viewing-error-details-about-stalled-operations-or-branches}

Se você selecionar um erro na lista de itens parados na página Operações paradas ou Ramificações paradas, a página Detalhes do erro será exibida, mostrando detalhes sobre o erro que pode ajudá-lo a solucionar o problema.

A caixa na parte inferior da página contém as informações do erro.

Você também pode encerrar ou tentar novamente operações paradas e tentar novamente ramificações paradas, na página Detalhes do erro.

## O processo não é parado quando o usuário de escalonamento não existe {#process-does-not-stall-when-escalation-user-does-not-exist}

Erros ocorrem quando a operação Atribuir Tarefa nos formulários AEM serviço Usuário está configurada para escalonar a tarefa a outro usuário após um período de tempo específico, e o usuário de escalonamento é excluído depois que a operação Atribuir Tarefa é executada, mas antes que o escalonamento ocorra.

Quando essa situação ocorre, o estado do processo e a tarefa não são alterados no tempo de escalonamento configurado, e o escalonamento não ocorre, mas o processo não é interrompido. A seguinte mensagem é exibida no log do servidor:

&quot;O principal especificado para escalonamento não é válido, para taskID: *number*, fila especificada: *number*.&quot;

Se o usuário de escalonamento for excluído antes da geração da tarefa (antes da execução da operação Atribuir Tarefa), o processo será interrompido ou o evento de exceção InvalidPrincipal será lançado.

Para evitar esse problema, ao excluir um usuário, procure tarefas pertencentes a esse usuário e trate-as de acordo. (Consulte [Trabalhar com tarefa](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
