---
title: Administração de fluxos de trabalho
seo-title: Administering Workflows
description: Saiba como administrar workflows no AEM.
seo-description: Learn how to administer workflows in AEM.
uuid: d000a13c-97cb-4b1b-809e-6c3eb0d675e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4b09cd44-434e-4834-bc0d-c9c082a4ba5a
exl-id: 10eecfb8-d43d-4f01-9778-87c752dee64c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# Administração de fluxos de trabalho{#administering-workflows}

Os workflows permitem automatizar as atividades do Adobe Experience Manager (AEM). Fluxos de trabalhos:

* Consiste em uma série de etapas que são executadas em uma ordem específica.

   * Cada etapa executa uma atividade distinta; como aguardar a entrada do usuário, ativar uma página ou enviar uma mensagem de email.

* Pode interagir com ativos no repositório, contas de usuário e serviços de AEM.
* Pode coordenar atividades complicadas que envolvem qualquer aspecto da AEM.

Os processos de negócios que sua organização estabeleceu podem ser representados como fluxos de trabalho. Por exemplo, o processo de publicação de conteúdo do site normalmente inclui etapas como aprovação e aprovação por vários participantes. Esses processos podem ser implementados como fluxos de trabalho AEM e aplicados a páginas e ativos de conteúdo.

* [Inicialização de workflows](/help/sites-administering/workflows-starting.md)
* [Administração de instâncias do fluxo de trabalho](/help/sites-administering/workflows-administering.md)
* [Gerenciamento de acesso a workflows](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* Aplicar e participar de fluxos de trabalho: [Trabalhar com fluxos de trabalho](/help/sites-authoring/workflows.md).
>* Criação de modelos de workflow e extensão da funcionalidade do workflow: [Desenvolvimento e extensão de fluxos de trabalho](/help/sites-developing/workflows.md).
>* Melhorando o desempenho dos workflows que usam recursos significativos do servidor: [Processamento de fluxo de trabalho simultâneo](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).
>


## Modelos e instâncias de fluxo de trabalho {#workflow-models-and-instances}

[Modelos de workflow](/help/sites-developing/workflows.md#model) em AEM estão a representação e implementação de processos de negócios:

* Normalmente, elas agem em páginas ou ativos para obter um resultado específico.
* Essas páginas e/ou ativos são chamados de carga do fluxo de trabalho.
* Os modelos de fluxo de trabalho consistem em uma série de etapas que executam uma tarefa específica.
* A carga é passada de etapa para etapa à medida que o fluxo de trabalho avança.

Quando um modelo de workflow é iniciado (executado), uma instância de workflow é criada. Um modelo de workflow pode ser iniciado várias vezes, cada vez gerando uma instância de workflow distinta. Para cada instância, as etapas que o modelo de fluxo de trabalho define são executadas.

>[!CAUTION]
>
>As etapas executadas são as definidas pelo modelo de workflow *no momento em que a instância é gerada*. Consulte [Desenvolvimento de fluxos de trabalho](/help/sites-developing/workflows.md#model) para obter mais detalhes.

As instâncias de fluxo de trabalho avançam pelo seguinte ciclo de vida:

1. O modelo de workflow é iniciado e uma instância de workflow é criada e executada.

   1. A carga da instância do workflow é identificada quando o modelo é iniciado.
   1. A instância é efetivamente uma cópia do modelo (como no momento da criação).
   1. AEM autores, administradores ou serviços podem iniciar modelos de fluxo de trabalho.

1. A primeira etapa do modelo de fluxo de trabalho é executada.
1. A etapa é concluída e o mecanismo de fluxo de trabalho usa o modelo para determinar a próxima etapa a ser executada.
1. As etapas subsequentes no modelo de fluxo de trabalho são executadas e concluídas.
1. Quando a etapa final é concluída, a instância do workflow é concluída e, portanto, arquivada.

Muitos modelos de fluxo de trabalho úteis são fornecidos com AEM. Além disso, os desenvolvedores em sua organização podem criar modelos de fluxo de trabalho personalizados, adaptados às necessidades específicas de seus processos comerciais.

## Etapas do fluxo de trabalho {#workflow-steps}

Quando as etapas do fluxo de trabalho são executadas, elas são associadas a uma instância de fluxo de trabalho. O histórico de uma instância de workflow inclui informações sobre cada etapa que foi executada para a instância. Essas informações são úteis para investigar problemas que ocorrem durante a execução.

Um usuário ou um serviço realiza etapas do fluxo de trabalho, dependendo do tipo de etapa:

* Quando um usuário executa uma etapa, ele recebe um item de trabalho que é colocado em sua Caixa de entrada. O usuário é responsável por concluir manualmente a etapa para que a instância do fluxo de trabalho avance.
* Quando um serviço executa uma etapa, após a conclusão, a instância do workflow avança automaticamente para a próxima etapa.

>[!NOTE]
>
>Se ocorrer um erro, a implementação de serviço/etapa deve lidar com o comportamento de um cenário de erro. O próprio motor de workflow tentará novamente o trabalho, registrará um erro e interromperá a instância.

## Status e ações do fluxo de trabalho {#workflow-status-and-actions}

Um workflow pode ter um dos seguintes status:

* **EM EXECUÇÃO**: A instância do workflow está em execução.
* **CONCLUÍDO**: A instância do workflow foi encerrada com êxito.

* **SUSPENSA**: Marca o workflow como suspenso. No entanto, consulte a Nota de precaução abaixo sobre um problema conhecido com este estado.
* **ABORTADO**: A instância do workflow foi encerrada.
* **STALE**: A progressão da instância do workflow requer que um trabalho em segundo plano seja executado, no entanto, o trabalho não pode ser encontrado no sistema. Essa situação pode ocorrer quando ocorre um erro ao executar o workflow.

>[!NOTE]
>
>Quando a execução de uma Etapa do processo resulta em erros, a etapa aparece na Caixa de entrada do administrador e o status do fluxo de trabalho é **EM EXECUÇÃO**.

Dependendo do status atual, você pode executar ações em executar instâncias de fluxo de trabalho quando precisar intervir na progressão normal de uma instância de fluxo de trabalho:

* **Suspender**: A suspensão altera o estado do fluxo de trabalho para Suspenso. Consulte Cuidado abaixo:

>[!CAUTION]
>
>Marcar um estado de workflow como &quot;Suspender&quot; tem um problema conhecido. Nesse estado, é possível realizar ações em itens de fluxo de trabalho suspensos em uma Caixa de entrada.

* **Retomar**: Reinicia um workflow suspenso no mesmo ponto de execução em que ele foi suspenso, usando a mesma configuração.
* **Encerrar**: Termina a execução do workflow e altera o estado para **ABORTADO**. Não é possível reiniciar uma instância de fluxo de trabalho abortada.
