---
title: Trabalhar com operações e ramificações paralisadas
seo-title: Working with stalled operations and branches
description: A página Operações paralisadas e a página Ramificações paralisadas mostram os processos que pararam.
seo-description: The Stalled Operations page and the Stalled Branches page show the processes that have stalled.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# Trabalhar com operações e ramificações paralisadas {#working-with-stalled-operations-and-branches}

A página Operações paralisadas e a página Ramificações paralisadas mostram os processos que pararam. Um processo pode ser interrompido quando ocorrer um erro durante ou após a execução de uma operação ou devido a uma operação de paralisação deliberada no processo:

* As operações podem parar devido a um erro imprevisto. No entanto, uma operação Stall Branch em um processo interrompe deliberadamente a execução de um processo e requer a intervenção do administrador.
* As ramificações podem ficar entre operações durante uma avaliação de regra.

Quando um processo é interrompido, nenhuma outra operação é executada até que o problema seja corrigido e a operação ou ramificação seja reiniciada.

Para cada item parado, a lista mostra as seguintes informações:

**Nome da Operação ou Nome da Ramificação:** O nome da operação ou ramificação.

**Status:** Sempre PARADO para itens parados.

**Erro:** Uma breve descrição do problema.

**ID do processo:** O número inteiro positivo que o fluxo de trabalho do Forms atribui quando o processo é instanciado (ou seja, quando um usuário ou uma etapa automatizada inicia um processo). Você pode usar esse identificador para rastrear a instância do processo por meio de seu ciclo de vida.

**Nome do processo - Versão:** O nome do processo atribuído no Workbench.

**Data de paralisação:** A data e a hora em que a operação ou ramificação parou.

Você pode executar as seguintes tarefas na página Operações paralisadas ou Ramificações paralisadas :

* Selecione um erro para exibir detalhes. Quando você seleciona um erro, a página Detalhes do erro é exibida.
* Encerre ou tente novamente as operações paralisadas ou tente ramificações paralisadas.

## Terminando ou repetindo operações ou ramificações paralisadas {#terminating-or-retrying-stalled-operations-or-branches}

Na página Operações paralisadas, você pode encerrar as instâncias de processo exibidas.

Quando você encerra uma instância de processo, ela para de ser executada e nenhuma outra operação acontece. Normalmente, você encerra um processo somente se ele se tornar bloqueado ou inutilizável devido a um erro e não pode ser corrigido e reiniciado.

Na página Operações paralisadas ou na página Ramificações paralisadas, é possível repetir a operação ou ramificação.

Quando você tenta uma operação novamente, o workflow do Forms é enviado com uma solicitação para reiniciar a operação. Se o erro que causou a paralisação do processo tiver sido corrigido e a solicitação de nova tentativa for bem-sucedida, o processo começará a ser executado novamente a partir do ponto em que havia parado e seu status será alterado para EXECUTANDO. Se a operação não puder ser reiniciada, ela permanecerá PARADA e talvez seja necessário encerrá-la.

### Encerrar uma operação paralisada {#terminate-a-stalled-operation}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Erros de operações paralisadas.
1. Na página Operações paralisadas , selecione o item que deseja encerrar e clique em Encerrar.

### Repetir uma operação ou ramificação paralisada {#retry-a-stalled-operation-or-branch}

1. No console de administração, clique em Services > forms workflow e, em seguida, clique em Stalled Operations Errors ou Stalled Branch Errors.
1. Na página Operações paralisadas ou Ramificações paralisadas , selecione o item que deseja repetir e clique em Repetir.

## Exibição de detalhes do erro sobre operações ou ramificações paralisadas {#viewing-error-details-about-stalled-operations-or-branches}

Se você selecionar um erro na lista de itens paralisados na página Operações ou Ramificações Paralisadas, a página Detalhes do Erro será exibida, mostrando detalhes sobre o erro que podem ajudar você a solucionar o problema.

A caixa na parte inferior da página contém as informações do erro.

Você também pode encerrar ou tentar novamente as operações paralisadas e tentar novamente ramificações paralisadas na página Detalhes do erro .

## O processo não é interrompido quando o usuário de escalonamento não existe {#process-does-not-stall-when-escalation-user-does-not-exist}

Ocorrem erros quando a operação Atribuir tarefa nos formulários AEM do serviço Usuário está configurada para encaminhar a tarefa a outro usuário após um período específico e o usuário de escalonamento é excluído depois que a operação Atribuir tarefa é executada, mas antes que o escalonamento ocorra.

Quando essa situação ocorre, o estado do processo e da tarefa não é alterado no momento do escalonamento configurado e o escalonamento não ocorre, mas o processo não é interrompido. A seguinte mensagem é exibida no log do servidor:

&quot;O principal especificado para escalonamento não é válido, para taskID: *número*, fila especificada: *número*.&quot;

Se o usuário de escalonamento for excluído antes que a tarefa seja gerada (antes da execução da operação Atribuir Tarefa), o processo será interrompido ou o evento de exceção InvalidPrincipal será lançado.

Para evitar esse problema, ao excluir um usuário, procure por tarefas pertencentes a esse usuário e gerencie-as adequadamente. (Consulte [Trabalhar com tarefas](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
