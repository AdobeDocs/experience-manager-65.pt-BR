---
title: Administração de Workflows
seo-title: Administração de Workflows
description: Saiba como administrar workflows em AEM.
seo-description: Saiba como administrar workflows em AEM.
uuid: d000a13c-97cb-4b1b-809e-6c3eb0d675e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4b09cd44-434e-4834-bc0d-c9c082a4ba5a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# Administração de Workflows{#administering-workflows}

Os workflows permitem que você automatize as atividades Adobe Experience Manager (AEM). Fluxos de trabalhos:

* Consiste de uma série de etapas executadas em uma ordem específica.

   * Cada etapa executa uma atividade distinta; como aguardar a entrada do usuário, ativar uma página ou enviar uma mensagem de email.

* Pode interagir com ativos no repositório, contas de usuário e serviços de AEM.
* Pode coordenar atividades complicadas que envolvem qualquer aspecto da AEM.

Os processos de negócios que sua organização estabeleceu podem ser representados como workflows. Por exemplo, o processo de publicação de conteúdo do site normalmente inclui etapas como aprovação e aprovação por vários participantes. Esses processos podem ser implementados como workflows AEM e aplicados a páginas de conteúdo e ativos.

* [Iniciando Workflows](/help/sites-administering/workflows-starting.md)
* [Administração de instâncias de fluxo de trabalho](/help/sites-administering/workflows-administering.md)
* [Gerenciamento do acesso a Workflows](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* Aplicação e participação em workflows: [Trabalhando com Workflows](/help/sites-authoring/workflows.md).
>* Criação de modelos de fluxo de trabalho e extensão da funcionalidade do fluxo de trabalho: [Desenvolvimento e extensão de Workflows](/help/sites-developing/workflows.md).
>* Melhorando o desempenho de workflows que usam recursos significativos do servidor: [Processamento de Fluxo de Trabalho Simultâneo](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).

>



## Modelos e instâncias de fluxo de trabalho {#workflow-models-and-instances}

[Os ](/help/sites-developing/workflows.md#model) modelos de fluxo de trabalho em AEM são a representação e implementação de processos de negócios:

* Normalmente, eles agem em páginas ou ativos para obter um resultado específico.
* Essas páginas e/ou ativos são chamados de carga do fluxo de trabalho.
* Os modelos de fluxo de trabalho consistem em uma série de etapas que executam uma tarefa específica.
* A carga é passada de etapa para etapa à medida que o fluxo de trabalho avança.

Quando um modelo de fluxo de trabalho é iniciado (executado), uma instância de fluxo de trabalho é criada. Um modelo de fluxo de trabalho pode ser iniciado várias vezes, sempre gerando uma instância de fluxo de trabalho distinta. Para cada instância, as etapas definidas pelo modelo de fluxo de trabalho são executadas.

>[!CAUTION]
>
>As etapas executadas são as definidas pelo modelo de fluxo de trabalho *no momento em que a instância é gerada*. Consulte [Desenvolvimento de Workflows](/help/sites-developing/workflows.md#model) para obter mais detalhes.

As instâncias de fluxo de trabalho avançam pelo seguinte ciclo de vida:

1. O modelo de fluxo de trabalho é iniciado e uma instância de fluxo de trabalho é criada e executada.

   1. A carga da instância do fluxo de trabalho é identificada quando o modelo é iniciado.
   1. A instância é efetivamente uma cópia do modelo (como no momento da criação).
   1. AEM autores, administradores ou serviços podem criar modelos de fluxo de trabalho de start.

1. A primeira etapa do modelo de fluxo de trabalho é executada.
1. A etapa é concluída e o motor de workflow usa o modelo para determinar a próxima etapa a ser executada.
1. As etapas subsequentes no modelo de fluxo de trabalho são executadas e concluídas.
1. Quando a etapa final é concluída, a instância do fluxo de trabalho é concluída e, portanto, arquivada.

Muitos modelos úteis de fluxo de trabalho são fornecidos com AEM. Além disso, os desenvolvedores em sua organização podem criar modelos de fluxo de trabalho personalizados, adaptados às necessidades específicas de seus processos de negócios.

## Etapas do fluxo de trabalho {#workflow-steps}

Quando as etapas do fluxo de trabalho são executadas, elas são associadas a uma instância do fluxo de trabalho. O histórico de uma instância de fluxo de trabalho inclui informações sobre cada etapa executada para a instância. Essas informações são úteis para investigar problemas que ocorrem durante a execução.

Um usuário ou serviço executa etapas de fluxo de trabalho, dependendo do tipo de etapa:

* Quando um usuário executa uma etapa, ele recebe um item de trabalho que é colocado em sua Caixa de entrada. O usuário é responsável por concluir manualmente a etapa para que a instância do fluxo de trabalho avance.
* Quando um serviço executa uma etapa, após a conclusão, a instância do fluxo de trabalho avança automaticamente para a próxima etapa.

>[!NOTE]
>
>Se ocorrer um erro, a implementação de serviço/etapa deve lidar com o comportamento de um cenário de erro. O próprio motor de workflow tentará novamente o trabalho, registrará um erro e interromperá a instância.

## Status e ações do fluxo de trabalho {#workflow-status-and-actions}

Um fluxo de trabalho pode ter um dos seguintes status:

* **EM EXECUÇÃO**: A instância do fluxo de trabalho está em execução.
* **CONCLUÍDO**: A instância do fluxo de trabalho foi encerrada com êxito.

* **SUSPENSA**: A instância do fluxo de trabalho foi suspensa.
* **ABORTADO**: A instância do fluxo de trabalho foi encerrada.
* **ESCALA**: A progressão da instância do fluxo de trabalho requer que um trabalho em segundo plano seja executado, no entanto, o trabalho não pode ser encontrado no sistema. Essa situação pode ocorrer quando ocorre um erro ao executar o fluxo de trabalho.

>[!NOTE]
>
>Quando a execução de uma Etapa do processo resulta em erros, a etapa é exibida na Caixa de entrada do administrador e o status do fluxo de trabalho é **EXECUTANDO**.

Dependendo do status atual, você pode executar ações em executar instâncias de fluxo de trabalho quando precisar intervir na progressão normal de uma instância de fluxo de trabalho:

* **Suspender**: Interrompe temporariamente a execução do fluxo de trabalho. A suspensão é útil em casos excepcionais quando você não deseja que o fluxo de trabalho continue, por exemplo, para manutenção. A suspensão altera o estado do fluxo de trabalho para Suspenso.
* **Retomar**: Reinicie um fluxo de trabalho suspenso no mesmo ponto de execução em que ele foi suspenso, usando a mesma configuração.
* **Terminar**: Termina a execução do fluxo de trabalho e altera o estado para  **ABORTED**. Uma instância de fluxo de trabalho abortada não pode ser reiniciada.

