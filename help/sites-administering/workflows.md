---
title: Administração de fluxos de trabalho
description: Saiba como automatizar atividades do Adobe Experience Manager usando workflows.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 10eecfb8-d43d-4f01-9778-87c752dee64c
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# Administração de fluxos de trabalho{#administering-workflows}

Os workflows permitem automatizar as atividades do Adobe Experience Manager (AEM). Fluxos de trabalhos:

* Consiste em uma série de etapas executadas em uma ordem específica.

   * Cada etapa executa uma atividade distinta; como aguardar a entrada do usuário, ativar uma página ou enviar uma mensagem de email.

* Pode interagir com ativos no repositório, contas de usuário e serviços AEM.
* Pode coordenar atividades complicadas que envolvem qualquer aspecto do AEM.

Os processos de negócios que sua organização estabeleceu podem ser representados como workflows. Por exemplo, o processo de publicação do conteúdo do site normalmente inclui etapas como aprovação e aprovação por vários participantes. Esses processos podem ser implementados como fluxos de trabalho de AEM e aplicados a páginas de conteúdo e ativos.

* [Inicialização de workflows](/help/sites-administering/workflows-starting.md)
* [Administração de instâncias do fluxo de trabalho](/help/sites-administering/workflows-administering.md)
* [Gerenciamento de acesso a workflows](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* Aplicar e participar de fluxos de trabalho: [Trabalhar com fluxos de trabalho](/help/sites-authoring/workflows.md).
>* Criação de modelos de workflow e extensão da funcionalidade do workflow: [Desenvolvimento e extensão de workflows](/help/sites-developing/workflows.md).
>* Melhorar o desempenho de workflows que usam recursos significativos do servidor: [Processamento de fluxo de trabalho simultâneo](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).
>

## Modelos e instâncias de fluxo de trabalho {#workflow-models-and-instances}

[Modelos de fluxo de trabalho](/help/sites-developing/workflows.md#model) no AEM são a representação e a implementação de processos comerciais:

* Normalmente, eles agem em páginas ou ativos para alcançar um resultado específico.
* Essas páginas e/ou ativos são chamados de carga de fluxo de trabalho.
* Os modelos de fluxo de trabalho consistem em uma série de etapas que executam uma tarefa específica.
* A carga é transmitida de etapa a etapa à medida que o fluxo de trabalho avança.

Quando um modelo de fluxo de trabalho é iniciado (executado), uma instância de fluxo de trabalho é criada. Um modelo de fluxo de trabalho pode ser iniciado várias vezes, cada vez gerando uma instância de fluxo de trabalho distinta. Para cada instância, as etapas definidas pelo modelo de fluxo de trabalho são executadas.

>[!CAUTION]
>
>As etapas executadas são aquelas definidas pelo modelo de fluxo de trabalho *no momento em que a instância é gerada*. Consulte [Desenvolvimento de fluxos de trabalho](/help/sites-developing/workflows.md#model) para obter mais detalhes.

As instâncias de fluxo de trabalho avançam pelo seguinte ciclo de vida:

1. O modelo de fluxo de trabalho é iniciado e uma instância de fluxo de trabalho é criada e executada.

   1. A carga da instância do fluxo de trabalho é identificada quando o modelo é iniciado.
   1. A instância é efetivamente uma cópia do modelo (como no momento da criação).
   1. Autores, administradores ou serviços de AEM podem iniciar modelos de fluxo de trabalho.

1. A primeira etapa do modelo de fluxo de trabalho é executada.
1. A etapa é concluída e o motor de workflow usa o modelo para determinar a próxima etapa a ser executada.
1. As etapas subsequentes do modelo de fluxo de trabalho são executadas e concluídas.
1. Quando a etapa final é concluída, a instância do workflow é concluída e, portanto, arquivada.

Muitos modelos úteis de fluxo de trabalho são fornecidos com AEM. Além disso, os desenvolvedores em sua organização podem criar modelos de fluxo de trabalho personalizados, adaptados às necessidades específicas de seus processos comerciais.

## Etapas do fluxo de trabalho {#workflow-steps}

Quando as etapas de fluxo de trabalho são executadas, elas são associadas a uma instância de fluxo de trabalho. O histórico de uma instância de fluxo de trabalho inclui informações sobre cada etapa executada para a instância. Essas informações são úteis para investigar problemas que ocorrem durante a execução.

Um usuário ou serviço executa etapas de fluxo de trabalho, dependendo do tipo de etapa:

* Quando um usuário executa uma etapa, ele recebe um item de trabalho que é colocado em sua Caixa de entrada. O usuário é responsável por concluir manualmente a etapa para que a instância do workflow avance.
* Quando um serviço executa uma etapa, após a conclusão, a instância do fluxo de trabalho avança automaticamente para a próxima etapa.

>[!NOTE]
>
>Se ocorrer um erro, a implementação de serviço/etapa deve lidar com o comportamento de um cenário de erro. O próprio motor de workflow tenta a tarefa novamente, registra um erro e interrompe a instância.

## Status e ações do fluxo de trabalho {#workflow-status-and-actions}

Um workflow pode ter um dos seguintes status:

* **EM EXECUÇÃO**: a instância do workflow está em execução.
* **CONCLUÍDO**: a instância do fluxo de trabalho foi encerrada com êxito.

* **SUSPENSO**: marca o workflow como suspenso. No entanto, consulte a Nota de advertência abaixo sobre um problema conhecido nesse estado.
* **ANULADO**: a instância do workflow foi encerrada.
* **OBSOLETO**: a progressão da instância de fluxo de trabalho exige que um trabalho em segundo plano seja executado, no entanto, o trabalho não pode ser encontrado no sistema. Essa situação pode ocorrer quando ocorre um erro ao executar o workflow.

>[!NOTE]
>
>Quando a execução de uma Etapa do processo resulta em erros, a etapa é exibida na Caixa de entrada do administrador e o status do fluxo de trabalho é **EM EXECUÇÃO**.

Dependendo do status, você pode executar ações em instâncias de fluxo de trabalho em execução quando é necessário intervir no progresso normal de uma instância de fluxo de trabalho:

* **Suspender**: a suspensão altera o estado do workflow para Suspenso. Consulte Cuidado abaixo:

>[!CAUTION]
>
>Marcar um estado de workflow como &quot;Suspender&quot; tem um problema conhecido. Nesse estado, é possível agir em itens de fluxo de trabalho suspensos em uma Caixa de entrada.

* **Retomar**: reinicia um workflow suspenso no mesmo ponto de execução em que ele foi suspenso, usando a mesma configuração.
* **Encerrar**: encerra a execução do workflow e altera o estado para **ANULADO**. Uma instância de fluxo de trabalho anulada não pode ser reiniciada.
