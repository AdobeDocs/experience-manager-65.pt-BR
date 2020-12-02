---
title: Desenvolvimento e extensão de Workflows
seo-title: Desenvolvimento e extensão de Workflows
description: AEM fornece várias ferramentas e recursos para criar modelos de fluxo de trabalho, desenvolver etapas de fluxo de trabalho e interagir programaticamente com workflows
seo-description: AEM fornece várias ferramentas e recursos para criar modelos de fluxo de trabalho, desenvolver etapas de fluxo de trabalho e interagir programaticamente com workflows
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 1%

---


# Desenvolvimento e extensão de Workflows{#developing-and-extending-workflows}

AEM fornece várias ferramentas e recursos para criar modelos de fluxo de trabalho, desenvolver etapas do fluxo de trabalho e interagir programaticamente com workflows.

Os workflows permitem que você automatize processos para gerenciar recursos e publicar conteúdo no seu ambiente AEM. Os workflows são compostos de uma série de etapas, com cada etapa realizando uma tarefa discreta. Você pode usar dados de lógica e tempo de execução para tomar decisões sobre quando um processo pode continuar e selecionar a próxima etapa de uma de várias etapas possíveis.

Por exemplo, os processos de negócios para criação e publicação de páginas da Web incluem tarefas de aprovação e aprovação por vários participantes. Esses processos podem ser modelados usando workflows AEM e aplicados a conteúdo específico.

Os principais aspectos são abordados abaixo, enquanto as páginas a seguir abordam mais detalhes:

* [Criação de modelos de fluxo de trabalho](/help/sites-developing/workflows-models.md)
* [Ampliação da funcionalidade do fluxo de trabalho](/help/sites-developing/workflows-customizing-extending.md)
* [Interação programática com Workflows](/help/sites-developing/workflows-program-interaction.md)
* [Referência da Etapa do Fluxo de Trabalho](/help/sites-developing/workflows-step-ref.md)
* [Referência do processo de fluxo de trabalho](/help/sites-developing/workflows-process-ref.md)
* [Práticas recomendadas do fluxo de trabalho](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Para obter informações sobre:
>
>* Participando de workflows, consulte [Usando Workflows](/help/sites-authoring/workflows.md).
>* Administrando workflows e instâncias de fluxo de trabalho, consulte [Administrando Workflows](/help/sites-administering/workflows.md).
>* Para obter um artigo completo da Comunidade, consulte [Modificando ativos digitais usando Workflows Adobe Experience Manager.](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* Consulte o [Webinar Fale com os especialistas do AEM em Workflows](https://bit.ly/ATACE218).
>* Para obter um artigo completo da Comunidade, consulte [Criando uma etapa personalizada do Adobe Experience Manager 6.3 Dynamic Participant](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html).
>* Alterações nos locais das informações consulte [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md) e [Práticas recomendadas do fluxo de trabalho - Locais](/help/sites-developing/workflows-best-practices.md#locations).

>



## Modelo {#model}

Um `WorkflowModel` representa uma definição (modelo) de um fluxo de trabalho. É feito de `WorkflowNodes` e `WorkflowTransitions`. O transição conecta os nós e define o *fluxo*. O Modelo sempre tem um nó de start e um nó final.

### Modelo de tempo de execução {#runtime-model}

Os modelos de fluxo de trabalho têm controle de versão. Ao executar uma instância de fluxo de trabalho, ele usará (e manterá) o modelo de tempo de execução do fluxo de trabalho (conforme disponível no momento em que o fluxo de trabalho foi iniciado).

Um modelo de tempo de execução é [gerado quando **Sincronizar** é acionado no editor de modelo de fluxo de trabalho](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

As edições no modelo de fluxo de trabalho que ocorrem e/ou nos modelos de tempo de execução que são gerados, *depois de* a instância específica que foi iniciada não serão aplicadas a essa instância.

>[!CAUTION]
>
>As etapas executadas são as definidas pelo [modelo de tempo de execução](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model); isso é gerado no momento em que a ação **Sincronizar** é acionada no editor do modelo de fluxo de trabalho.
>
>Se o modelo de fluxo de trabalho for alterado após esse ponto no tempo (sem **Sincronizar** ser acionado), a instância do tempo de execução não refletirá essas alterações. Somente os modelos de tempo de execução gerados após a atualização refletirão as alterações. As exceções são os scripts ECMA subjacentes, que são mantidos somente uma vez, portanto, as alterações são feitas.

### Etapa {#step}

Cada etapa realiza uma tarefa discreta. Existem diferentes tipos de etapas do fluxo de trabalho:

* Participante (usuário/grupo): Essas etapas geram um item de trabalho e o atribuem a um usuário ou grupo. Um usuário deve concluir o item de trabalho para avançar no fluxo de trabalho.
* Processo (Script, chamada de método Java): Essas etapas são executadas automaticamente pelo sistema. Um script ECMA ou uma classe Java implementa a etapa. Os serviços podem ser desenvolvidos para acompanhar eventos de fluxo de trabalho especiais e executar tarefas de acordo com a lógica comercial.
* Container (Sub fluxo de trabalho): Esse tipo de etapa start outro modelo de fluxo de trabalho.
* OU Dividir/Ingressar: Use a lógica para decidir qual etapa executar em seguida no fluxo de trabalho.
* E dividir/unir: Permite que várias etapas sejam executadas simultaneamente.

Todas as etapas compartilham as seguintes propriedades comuns: Alertas `Autoadvance` e `Timeout` (com script).

### Transição {#transition}

Um `WorkflowTransition` representa uma transição entre dois `WorkflowNodes` de um `WorkflowModel`.

* Ela define o link entre duas etapas consecutivas.
* É possível aplicar regras.

### Item de trabalho {#workitem}

Uma `WorkItem` é a unidade transmitida por uma instância `Workflow` de uma `WorkflowModel`. Ele contém o `WorkflowData` em que a instância atua e uma referência para o `WorkflowNode` que descreve a etapa de fluxo de trabalho subjacente.

* É usado para identificar a tarefa e é colocado na respectiva caixa de entrada.
* Uma instância de fluxo de trabalho pode ter um ou vários `WorkItems` ao mesmo tempo (dependendo do modelo de fluxo de trabalho).
* O `WorkItem` faz referência à instância do fluxo de trabalho.
* No repositório, `WorkItem` é armazenado abaixo da instância do fluxo de trabalho.

### Carga {#payload}

Faz referência ao recurso que deve ser avançado por meio de um fluxo de trabalho.

A implementação da carga faz referência a um recurso no repositório (por caminho, UUID ou URL) ou por um objeto java serializado. A referência a um recurso no repositório é muito flexível e em conjunção com lingas muito produtivas; por exemplo, o nó referenciado poderia ser renderizado como um formulário.

### Ciclo de vida {#lifecycle}

É criado ao iniciar um novo fluxo de trabalho (escolhendo o respectivo modelo de fluxo de trabalho e definindo a carga) e termina quando o nó final é processado.

As seguintes ações são possíveis em uma instância do fluxo de trabalho:

* Finalizar
* Suspender
* Retomar
* Reiniciar

As instâncias concluídas e terminadas são arquivadas.

### Caixa de entrada {#inbox}

Cada conta de usuário tem sua própria caixa de entrada de fluxo de trabalho na qual os `WorkItems` atribuídos estão acessíveis.

Os `WorkItems` são atribuídos à conta de usuário diretamente ou ao grupo ao qual pertencem.

### Tipos de Fluxo de Trabalho {#workflow-types}

Há vários tipos de fluxo de trabalho, conforme indicado no console Modelos de fluxo de trabalho:

![wf-upgrade-03](assets/wf-upgraded-03.png)

* **Padrão**

   Esses são os workflows prontos para uso incluídos em uma instância AEM padrão.

* Workflows personalizados (nenhum indicador no console)

   Esses são workflows que foram criados como novos ou de workflows prontos para uso que foram sobrepostos com personalizações.

* **Legado**

   Workflows criados em uma versão anterior do AEM. Eles podem ser retidos durante uma atualização ou exportados como um pacote de fluxo de trabalho da versão anterior e, em seguida, importados para a nova versão.

### Workflows transitórios {#transient-workflows}

Workflows padrão salvam informações de tempo de execução (histórico) durante sua execução. Você também pode definir um modelo de fluxo de trabalho como **Transitório** para evitar que esse histórico seja persistente. Isso é usado para ajuste de desempenho, pois economiza/evita o tempo/recursos usados para persistir nas informações.

Workflows transitórios podem ser usados para qualquer workflows que:

* são executados com frequência.
* não precisa do histórico de fluxo de trabalho.

Foram introduzidos workflows transitórios para carregar um grande número de ativos, onde as informações do ativo são importantes, mas não o histórico de tempo de execução do fluxo de trabalho.

>[!NOTE]
>
>Consulte [Criando um fluxo de trabalho temporário](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) para obter mais detalhes.

>[!CAUTION]
>
>Quando um modelo de fluxo de trabalho é sinalizado como Transitório, há alguns cenários em que as informações do tempo de execução ainda serão mantidas:
>
>* O tipo de carga (por exemplo, vídeo) requer etapas externas para processamento. nesses casos, o histórico do tempo de execução é necessário para a confirmação do status.
>* O fluxo de trabalho entra em **AND Split**; nesses casos, o histórico do tempo de execução é necessário para a confirmação do status.
>* Quando o fluxo de trabalho temporário entra em uma etapa do participante, ele muda de modo (no tempo de execução) para não transitório; como a tarefa está sendo passada para uma pessoa, a história precisa ser persistente

>



>[!CAUTION]
>
>Em um fluxo de trabalho temporário, você não deve usar **Etapa Ir para**.
>
>Isso ocorre quando **Ir para a Etapa** cria um trabalho de sling para continuar o fluxo de trabalho no ponto `goto`. Isso derrota a finalidade de tornar o fluxo de trabalho temporário e gera um erro no arquivo de log.
>
>Para tomar decisões em um fluxo de trabalho temporário, você pode usar **OU Dividir**.

>[!NOTE]
>
>Consulte [Práticas recomendadas para os ativos](/help/assets/performance-tuning-guidelines.md#transient-workflows) para obter mais informações sobre como os Workflows transitórios afetam o desempenho dos ativos.

### Suporte a vários recursos {#multi-resource-support}

Ativar **Suporte a vários recursos** para o modelo de fluxo de trabalho significa que uma única instância de fluxo de trabalho será iniciada mesmo quando você selecionar vários recursos; estes serão anexados como um pacote.

Se **Suporte a vários recursos** não estiver ativado para o seu modelo de fluxo de trabalho e vários recursos estiverem selecionados, uma instância de fluxo de trabalho individual será iniciada para cada recurso.

>[!NOTE]
>
>Consulte [Configurando um fluxo de trabalho para suporte a vários recursos](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) para obter mais detalhes.

### Etapas do fluxo de trabalho {#workflow-stages}

As Etapas do fluxo de trabalho ajudam a visualizar o progresso de um fluxo de trabalho ao manipular tarefas. Eles podem ser usados para fornecer uma visão geral de até onde o fluxo de trabalho está por meio do processamento, pois quando o fluxo de trabalho é executado, o usuário pode visualização o progresso descrito por **Stage** (em vez de uma etapa individual).

Como os nomes de etapas individuais podem ser específicos e técnicos, os nomes de etapas podem ser definidos para fornecer uma visualização conceitual do progresso do fluxo de trabalho.

Por exemplo, para um fluxo de trabalho com seis etapas e quatro etapas:

1. Você pode [configurar as Etapas do Fluxo de Trabalho (que mostram o Progresso do Fluxo de Trabalho) e, em seguida, atribuir a etapa apropriada a cada etapa do seu fluxo de trabalho](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

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

1. Quando o fluxo de trabalho é executado, o usuário pode visualização o progresso de acordo com os nomes do Palco (em vez dos nomes das etapas). O andamento do fluxo de trabalho será exibido na guia [INFORMAÇÕES DO FLUXO DE TRABALHO da janela de detalhes da tarefa do item de trabalho](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) listado na [Caixa de entrada](/help/sites-authoring/inbox.md).

### Workflows e Forms {#workflows-and-forms}

Normalmente, os workflows são usados para processar envios de formulário em AEM. Isso pode ser feito com os [componentes principais de formulário](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) disponíveis em uma instância AEM padrão, ou com a [solução AEM Forms](/help/forms/using/aem-forms-workflow.md).

Ao criar um novo formulário, o envio do formulário pode ser facilmente associado a um modelo de fluxo de trabalho; por exemplo, para armazenar o conteúdo em um local específico do repositório ou notificar um usuário sobre o envio do formulário e seu conteúdo.

### Workflows e tradução {#workflows-and-translation}

Workflows também são parte integrante do processo [Translation](/help/sites-administering/translation.md).
