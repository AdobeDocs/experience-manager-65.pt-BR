---
title: Desenvolvimento e extensão de workflows
seo-title: Developing and Extending Workflows
description: O AEM fornece várias ferramentas e recursos para criar modelos de fluxo de trabalho, desenvolver etapas de fluxo de trabalho e interagir programaticamente com fluxos de trabalho
seo-description: AEM provides several tools and resources for creating workflow models, developing workflow steps, and for programmatically interacting with workflows
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
source-git-commit: 82b9b852fa3134f140f8de0bad229282979c8a30
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 3%

---


# Desenvolvimento e extensão de workflows{#developing-and-extending-workflows}

O AEM fornece várias ferramentas e recursos para criar modelos de fluxo de trabalho, desenvolver etapas de fluxo de trabalho e interagir programaticamente com fluxos de trabalho.

Os workflows permitem automatizar processos para gerenciar recursos e publicar conteúdo no ambiente de AEM. Os workflows são compostos de uma série de etapas, com cada etapa realizando uma tarefa discreta. Você pode usar dados de lógica e tempo de execução para tomar decisões sobre quando um processo pode continuar e selecionar a próxima etapa de uma das várias etapas possíveis.

Por exemplo, os processos de negócios para criar e publicar páginas da Web incluem tarefas de aprovação e aprovação por vários participantes. Esses processos podem ser modelados usando fluxos de trabalho AEM e aplicados a conteúdo específico.

Os principais aspectos são abordados abaixo, enquanto as seguintes páginas cobrem mais detalhes:

* [Criação de modelos de fluxo de trabalho](/help/sites-developing/workflows-models.md)
* [Ampliação da funcionalidade do fluxo de trabalho](/help/sites-developing/workflows-customizing-extending.md)
* [Interação com fluxos de trabalho programaticamente](/help/sites-developing/workflows-program-interaction.md)
* [Referência da Etapa do fluxo de trabalho](/help/sites-developing/workflows-step-ref.md)
* [Referência do processo de fluxo de trabalho](/help/sites-developing/workflows-process-ref.md)
* [Práticas recomendadas do workflow](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Para obter informações sobre:
>
>* Participar de fluxos de trabalho, consulte [Usar fluxos de trabalho](/help/sites-authoring/workflows.md).
>* Administrando workflows e instâncias de workflow, consulte [Administrando Workflows](/help/sites-administering/workflows.md).
>* Para obter um artigo completo da Comunidade, consulte [Modificar ativos digitais usando fluxos de trabalho do Adobe Experience Manager.](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* Consulte o [Webinar Fale com os especialistas do AEM em workflows](https://bit.ly/ATACE218).
>* Para obter um artigo completo da Comunidade, consulte [Criação de uma etapa personalizada do Adobe Experience Manager 6.3 Dynamic Participant](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html).
>* As alterações nos locais das informações podem ser consultadas [Reestruturação do Repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md) e [Práticas recomendadas do fluxo de trabalho - Localizações](/help/sites-developing/workflows-best-practices.md#locations).

>


## Modelo {#model}

Um `WorkflowModel` representa uma definição (modelo) de um fluxo de trabalho. Ele é feito de `WorkflowNodes` e `WorkflowTransitions`. As transições conectam os nós e definem o *fluxo*. O Modelo sempre tem um nó inicial e um nó final.

### Modelo de tempo de execução {#runtime-model}

Os modelos de fluxo de trabalho têm controle de versão. Ao executar uma instância de workflow, ele usará (e manterá) o modelo de tempo de execução do workflow (conforme disponível no momento em que o workflow foi iniciado).

Um modelo de tempo de execução é [gerado quando **Sync** é acionado no editor de modelo de fluxo de trabalho](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

Edições no modelo de fluxo de trabalho que ocorrem e/ou modelos de tempo de execução gerados, *after* a instância específica foi iniciada não será aplicada a essa instância.

>[!CAUTION]
>
>As etapas executadas são as definidas pelo [modelo de tempo de execução](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model); isso é gerado no momento em que a ação **Sync** é acionada no editor de modelo de fluxo de trabalho.
>
>Se o modelo de workflow for alterado após esse ponto no tempo (sem **Sync** ser acionado), a instância de tempo de execução não refletirá essas alterações. Somente os modelos de tempo de execução gerados após a atualização refletirão as alterações. As exceções são os scripts ECMA subjacentes, que são mantidos apenas uma vez, de modo que as alterações a eles são feitas.

### Etapa {#step}

Cada etapa realiza uma tarefa discreta. Existem diferentes tipos de etapas do fluxo de trabalho:

* Participante (Usuário/Grupo): Essas etapas geram um item de trabalho e o atribuem a um usuário ou grupo. Um usuário deve concluir o item de trabalho para avançar o fluxo de trabalho.
* Processo (Script, chamada do método Java): Essas etapas são executadas automaticamente pelo sistema. Um script ECMA ou classe Java implementa a etapa. Os serviços podem ser desenvolvidos para acompanhar eventos especiais de fluxo de trabalho e executar tarefas de acordo com a lógica comercial.
* Container (Sub Workflow): Esse tipo de etapa inicia outro modelo de fluxo de trabalho.
* OU Dividir/Associar: Use a lógica para decidir qual etapa executar em seguida no fluxo de trabalho.
* AND Split/Join: Permite que várias etapas sejam executadas simultaneamente.

Todas as etapas compartilham as seguintes propriedades comuns: Alertas `Autoadvance` e `Timeout` (com script).

### Transição {#transition}

Um `WorkflowTransition` representa uma transição entre dois `WorkflowNodes` de um `WorkflowModel`.

* Ele define o link entre duas etapas consecutivas.
* É possível aplicar regras.

### Item de trabalho {#workitem}

Um `WorkItem` é a unidade que é passada por uma instância `Workflow` de um `WorkflowModel`. Ela contém o `WorkflowData` em que a instância atua e uma referência para o `WorkflowNode` que descreve a etapa do fluxo de trabalho subjacente.

* Ele é usado para identificar a tarefa e é colocado na respectiva caixa de entrada.
* Uma instância de workflow pode ter um ou vários `WorkItems` ao mesmo tempo (dependendo do modelo de workflow).
* O `WorkItem` faz referência à instância do workflow.
* No repositório, o `WorkItem` é armazenado abaixo da instância de workflow.

### Carga {#payload}

Faz referência ao recurso que deve ser avançado por meio de um workflow.

A implementação de carga faz referência a um recurso no repositório (por caminho, UUID ou URL) ou por um objeto java serializado. A referência a um recurso no repositório é muito flexível e em conjunto com o sling muito produtivo; por exemplo, o nó referenciado pode ser renderizado como um formulário.

### Vida útil {#lifecycle}

É criado ao iniciar um novo workflow (escolhendo o respectivo modelo de workflow e definindo a carga) e termina quando o nó final é processado.

As seguintes ações são possíveis em uma instância de workflow:

* Finalizar
* Suspender
* Retomar
* Reiniciar

As instâncias concluídas e terminadas são arquivadas.

### Caixa de entrada {#inbox}

Cada conta de usuário tem sua própria caixa de entrada de workflow na qual os `WorkItems` atribuídos são acessíveis.

Os `WorkItems` são atribuídos à conta de usuário diretamente ou ao grupo ao qual pertencem.

### Tipos de fluxo de trabalho {#workflow-types}

Há vários tipos de fluxo de trabalho, conforme indicado no console Modelos de fluxo de trabalho :

![wf-upgrade-03](assets/wf-upgraded-03.png)

* **Padrão**

   Esses são os workflows prontos incluídos em uma instância de AEM padrão.

* Fluxos de trabalho personalizados (nenhum indicador no console)

   Esses são workflows que foram criados como novos ou de workflows prontos que foram sobrepostos com personalizações.

* **Legado**

   Fluxos de trabalho criados em uma versão anterior do AEM. Elas podem ser retidas durante uma atualização ou exportadas como um pacote de fluxo de trabalho da versão anterior e, em seguida, importadas para a nova versão.

### Workflows transitórios {#transient-workflows}

Os workflows padrão salvam informações de tempo de execução (histórico) durante a execução. Você também pode definir um modelo de workflow como **Transient** para evitar que esse histórico seja persistente. Isso é usado para ajuste de desempenho, pois salva/evita o tempo/recursos usados para persistir as informações.

Fluxos de trabalho transitórios podem ser usados para qualquer fluxo de trabalho que:

* são executados com frequência.
* não precisam do histórico do workflow.

Fluxos de trabalho transitórios foram introduzidos para carregar um grande número de ativos, onde as informações do ativo são importantes, mas não o histórico de tempo de execução do fluxo de trabalho.

>[!NOTE]
>
>Consulte [Criação de um fluxo de trabalho transitório](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) para obter mais detalhes.

>[!CAUTION]
>
>Quando um modelo de fluxo de trabalho é sinalizado como Transitório, há alguns cenários em que as informações de tempo de execução ainda serão mantidas:
>
>* O tipo de carga (por exemplo, vídeo) requer etapas externas para processamento; nesses casos, o histórico do tempo de execução é necessário para a confirmação do status.
>* O workflow insere um **AND Split**; nesses casos, o histórico do tempo de execução é necessário para a confirmação do status.
>* Quando o fluxo de trabalho transitório entra em uma etapa do participante, ele muda o modo (no tempo de execução) para não transitório; como a tarefa está sendo passada para uma pessoa, o histórico precisa ser mantido

>


>[!CAUTION]
>
>Em um fluxo de trabalho transitório, você não deve usar **Ir para a etapa**.
>
>Isso ocorre quando a **Etapa Ir para** cria um trabalho de sling para continuar o workflow no ponto `goto`. Isso elimina a finalidade de tornar o workflow transitório e gera um erro no arquivo de log.
>
>Para tomar decisões em um workflow transitório, você pode usar o **OU Split**.

>[!NOTE]
>
>Consulte [Práticas recomendadas do Assets](/help/assets/performance-tuning-guidelines.md#transient-workflows) para obter mais informações sobre como os Fluxos de trabalho transitórios afetam o desempenho do Ativo.

### Suporte a vários recursos {#multi-resource-support}

Ativar **Suporte a vários recursos** para seu modelo de fluxo de trabalho significa que uma única instância de fluxo de trabalho será iniciada mesmo quando você selecionar vários recursos; eles serão anexados como um pacote.

Se **Suporte a vários recursos** não estiver ativado para seu modelo de fluxo de trabalho e vários recursos forem selecionados, uma instância de fluxo de trabalho individual será iniciada para cada recurso.

>[!NOTE]
>
>Consulte [Configuração de um fluxo de trabalho para suporte a vários recursos](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) para obter mais detalhes.

### Estágios do Fluxo de Trabalho {#workflow-stages}

As Etapas do fluxo de trabalho ajudam a visualizar o progresso de um fluxo de trabalho ao manipular tarefas. Eles podem ser usados para fornecer uma visão geral de até que ponto o fluxo de trabalho está por meio do processamento, como quando o fluxo de trabalho é executado, o usuário pode visualizar o progresso descrito por **Stage** (em vez de uma etapa individual).

Como os nomes de etapas individuais podem ser específicos e técnicos, os nomes de etapas podem ser definidos para fornecer uma visão conceitual do progresso do fluxo de trabalho.

Por exemplo, para um fluxo de trabalho com seis etapas e quatro etapas:

1. Você pode [configurar os Estágios do Fluxo de Trabalho (que mostram o Progresso do Fluxo de Trabalho) e, em seguida, atribuir o estágio apropriado a cada etapa do fluxo de trabalho](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * Vários nomes de palco podem ser criados.
   * Em seguida, um nome de estágio individual é atribuído a cada etapa (um nome de estágio pode ser atribuído a uma ou mais etapas).

   | **Nome da etapa** | **Estágio (atribuído à etapa)** |
   |---|---|
   | Etapa 1 | Criar |
   | Etapa 2 | Criar |
   | Etapa 3 | Análise |
   | Etapa 4 | Aprovar |
   | Etapa 5 | Concluir |
   | Etapa 6 | Concluir |

1. Quando o fluxo de trabalho é executado, o usuário pode visualizar o progresso de acordo com os nomes do Palco (em vez dos nomes das etapas). O progresso do workflow será exibido na guia [INFORMAÇÕES DO WORKFLOW da janela de detalhes da tarefa do item de trabalho](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) listado na [Caixa de entrada](/help/sites-authoring/inbox.md).

### Fluxos de trabalho e Forms {#workflows-and-forms}

Normalmente, os workflows são usados para processar envios de formulários no AEM. Isso pode ser feito com os [componentes principais de formulário](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) disponíveis em uma instância padrão do AEM ou com a [solução AEM Forms](/help/forms/using/aem-forms-workflow.md).

Ao criar um novo formulário, o envio do formulário pode ser facilmente associado a um modelo de fluxo de trabalho; por exemplo, para armazenar o conteúdo em um local específico do repositório ou notificar um usuário sobre o envio do formulário e seu conteúdo.

### Fluxos de trabalho e tradução {#workflows-and-translation}

Os workflows também são parte integrante do processo [Translation](/help/sites-administering/translation.md).
