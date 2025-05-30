---
title: Desenvolvimento e extensão de workflows
description: O AEM fornece várias ferramentas e recursos para criar modelos de fluxo de trabalho, desenvolver etapas de fluxo de trabalho e interagir programaticamente com fluxos de trabalho
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1460'
ht-degree: 3%

---


# Desenvolvimento e extensão de workflows{#developing-and-extending-workflows}

O AEM fornece várias ferramentas e recursos para criar modelos de fluxo de trabalho, desenvolver etapas de fluxo de trabalho e interagir programaticamente com fluxos de trabalho.

Os workflows permitem automatizar processos para gerenciar recursos e publicar conteúdo no ambiente do AEM. Os workflows são compostos por uma série de etapas, com cada etapa realizando uma tarefa distinta. Você pode usar a lógica e os dados de tempo de execução para decidir quando um processo pode continuar e selecionar a próxima etapa a partir de uma das várias etapas possíveis.

Por exemplo, os processos comerciais para criar e publicar páginas da Web incluem tarefas de aprovação e aprovação por vários participantes. Esses processos podem ser modelados usando fluxos de trabalho de AEM e aplicados a conteúdo específico.

Os principais aspectos são abordados abaixo, enquanto as seguintes páginas abordam mais detalhes:

* [Criação de modelos de fluxo de trabalho](/help/sites-developing/workflows-models.md)
* [Ampliação da funcionalidade do fluxo de trabalho](/help/sites-developing/workflows-customizing-extending.md)
* [Interação programática com fluxos de trabalho](/help/sites-developing/workflows-program-interaction.md)
* [Referência da Etapa do fluxo de trabalho](/help/sites-developing/workflows-step-ref.md)
* [Referência do processo de fluxo de trabalho](/help/sites-developing/workflows-process-ref.md)
* [Práticas recomendadas de workflow](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Para obter informações sobre:
>
>* Participando de fluxos de trabalho, consulte [Usando Fluxos de Trabalho](/help/sites-authoring/workflows.md).
>* Administrando fluxos de trabalho e instâncias de fluxo de trabalho, consulte [Administração de Fluxos de Trabalho](/help/sites-administering/workflows.md).
>* Para obter um Artigo completo sobre a Comunidade, consulte [Modificação de Assets digital usando fluxos de trabalho do Adobe Experience Manager.](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html?lang=pt-BR)
>* Consulte o [Webinário do Pergunte a um especialista em AEM sobre fluxos de trabalho](https://communities.adobeconnect.com/p5s33iburd54/).
>* Mudanças nos locais das informações: consulte [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md) e [Práticas recomendadas de fluxo de trabalho - Locais](/help/sites-developing/workflows-best-practices.md#locations).
>

## Modelo {#model}

Um `WorkflowModel` representa uma definição (modelo) de um fluxo de trabalho. Ele é feito de `WorkflowNodes` e `WorkflowTransitions`. As transições conectam os nós e definem o *fluxo*. O modelo sempre tem um nó inicial e um nó final.

### Modelo de tempo de execução {#runtime-model}

Os modelos de fluxo de trabalho têm controle de versão. Quando você executa uma instância de fluxo de trabalho, ela usa e mantém o modelo de tempo de execução do fluxo de trabalho, conforme disponível no momento em que o fluxo de trabalho foi iniciado.

Um modelo de tempo de execução é [gerado quando a **Sincronização** é acionada no editor de modelo de fluxo de trabalho](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

Edições no modelo de fluxo de trabalho que ocorrem, ou modelos de tempo de execução que são gerados, ou ambos, *após* a instância específica foi iniciada não são aplicadas a essa instância.

>[!CAUTION]
>
>As etapas executadas são definidas pelo [modelo de tempo de execução](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model), gerado no momento em que a ação **Sincronizar** é acionada no editor de modelo de fluxo de trabalho.
>
>Se o modelo de fluxo de trabalho for alterado após esse ponto no tempo (sem a **Sincronização** ser acionada), a instância de tempo de execução não refletirá essas alterações. Somente os modelos em tempo de execução gerados após a atualização refletem as alterações. As exceções são os scripts ECMA subjacentes, que são mantidos apenas uma vez para que essas alterações sejam feitas.

### Etapa {#step}

Cada etapa realiza uma tarefa distinta. Há diferentes tipos de etapas de fluxo de trabalho:

* Participante (Usuário/Grupo): Essas etapas geram um item de trabalho e o atribuem a um usuário ou grupo. Um usuário deve concluir o item de trabalho para avançar o fluxo de trabalho.
* Processo (Script, chamada de método Java™): essas etapas são executadas automaticamente pelo sistema. Um script ECMA ou classe Java™ implementa a etapa. Os serviços podem ser desenvolvidos para acompanhar eventos especiais de fluxo de trabalho e executar tarefas de acordo com a lógica de negócios.
* Contêiner (subfluxo de trabalho): esse tipo de etapa inicia outro modelo de fluxo de trabalho.
* OU Split/Join: use a lógica para decidir qual etapa executar em seguida no fluxo de trabalho.
* AND Split/Join: permite que várias etapas sejam executadas simultaneamente.

Todas as etapas compartilham as seguintes propriedades comuns: `Autoadvance` e `Timeout` alertas (com script).

### Transição {#transition}

Um `WorkflowTransition` representa uma transição entre dois `WorkflowNodes` de um `WorkflowModel`.

* Ele define o vínculo entre duas etapas consecutivas.
* É possível aplicar regras.

### Item de trabalho {#workitem}

`WorkItem` é a unidade passada por uma instância `Workflow` de `WorkflowModel`. Ele contém o `WorkflowData` no qual a instância atua e uma referência ao `WorkflowNode` que descreve a etapa do fluxo de trabalho subjacente.

* É usada para identificar a tarefa e é colocada na respectiva caixa de entrada.
* Uma instância de fluxo de trabalho pode ter um ou vários `WorkItems` ao mesmo tempo (dependendo do modelo de fluxo de trabalho).
* O `WorkItem` faz referência à instância do fluxo de trabalho.
* No repositório, o `WorkItem` é armazenado abaixo da instância do fluxo de trabalho.

### Carga útil {#payload}

Faz referência ao recurso que deve ser avançado por meio de um workflow.

A implementação de carga referencia um recurso no repositório (por caminho, UUID ou URL) ou por um objeto Java™ serializado. A referência a um recurso no repositório é flexível e simples, com o sling produtivo. Por exemplo, o nó referenciado pode ser renderizado como um formulário.

### Ciclo de vida {#lifecycle}

É criado ao iniciar um novo workflow (escolhendo o respectivo modelo de workflow e definindo a carga) e termina quando o nó final é processado.

As seguintes ações são possíveis em uma instância de workflow:

* Finalizar
* Suspender
* Retomar
* Reiniciar

As instâncias concluídas e encerradas são arquivadas.

### Caixa de entrada {#inbox}

Cada conta de usuário tem sua própria caixa de entrada de fluxo de trabalho na qual o `WorkItems` atribuído está acessível.

Os `WorkItems` são atribuídos diretamente à conta de usuário ou ao grupo ao qual pertencem.

### Tipos de fluxo de trabalho {#workflow-types}

Há vários tipos de fluxo de trabalho, conforme indicado no console Modelos de fluxo de trabalho:

![wf-updated-03](assets/wf-upgraded-03.png)

* **Padrão**

  Esses tipos são os workflows prontos para uso incluídos em uma instância padrão do AEM.

* Fluxos de trabalho personalizados (nenhum indicador no console)

  Esses workflows foram criados como novos ou a partir de workflows prontos para uso que foram sobrepostos com personalizações.

* **Herdados**

  Fluxos de trabalho criados em uma versão anterior do AEM. Esses workflows podem ser retidos durante uma atualização ou exportados como um pacote de workflow da versão anterior e, em seguida, importados para a nova versão.

### Workflows transitórios {#transient-workflows}

Os workflows padrão salvam as informações de tempo de execução (histórico) durante a execução. Você também pode definir um modelo de fluxo de trabalho como **Temporário** para evitar que esse histórico seja mantido. Esse workflow é usado para ajuste de desempenho porque economiza tempo e recursos usados para a persistência das informações.

Os workflows transitórios podem ser usados para qualquer workflow que:

* são executados com frequência.
* não precisam do histórico do workflow.

Foram introduzidos fluxos de trabalho transitórios para carregar muitos ativos, nos quais as informações do ativo são importantes, mas não o histórico do tempo de execução do fluxo de trabalho.

>[!NOTE]
>
>Consulte [Criando um Fluxo de Trabalho Transitório](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) para obter mais detalhes.

>[!CAUTION]
>
>Quando um modelo de fluxo de trabalho é sinalizado como Temporário, há alguns cenários em que as informações de tempo de execução ainda devem ser mantidas:
>
>* O tipo de conteúdo (por exemplo, vídeo) requer etapas externas para o processamento; nesses casos, o histórico do tempo de execução é necessário para a confirmação do status.
>* O fluxo de trabalho entra em uma **AND Split**. Nesses casos, o histórico do tempo de execução é necessário para a confirmação do status.
>* Quando o fluxo de trabalho temporário entra em uma etapa do participante, ele muda o modo, no tempo de execução, para não transitório. Como a tarefa está sendo passada para uma pessoa, o histórico deve ser mantido.
>

>[!CAUTION]
>
>Em um fluxo de trabalho transitório, você não deve usar uma **Etapa Ir para**.
>
>O motivo é porque a **Etapa Ir** cria um trabalho do sling para continuar o fluxo de trabalho no ponto `goto`. Ele anula a finalidade de tornar o fluxo de trabalho transitório e gera um erro no arquivo de log.
>
>Use **OU Split** para fazer escolhas em um fluxo de trabalho temporário.

>[!NOTE]
>
>Consulte [Práticas recomendadas para o Assets](/help/assets/performance-tuning-guidelines.md#transient-workflows) para obter mais informações sobre como os fluxos de trabalho transitórios afetam o desempenho dos ativos.

### Suporte a vários recursos {#multi-resource-support}

Ativar o **Suporte a vários recursos** para o seu modelo de fluxo de trabalho significa que uma única instância de fluxo de trabalho é iniciada mesmo quando você seleciona vários recursos. Cada uma está anexada como um pacote.

Se o **Suporte a Vários Recursos** não for ativado para o seu modelo de fluxo de trabalho e vários recursos forem selecionados, uma instância de fluxo de trabalho individual será iniciada para cada recurso.

>[!NOTE]
>
>Consulte [Configuração de um Fluxo de Trabalho para Suporte a Vários Recursos](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) para obter mais detalhes.

### Estágios do fluxo de trabalho {#workflow-stages}

Estágios do fluxo de trabalho ajudam a visualizar o progresso de um fluxo de trabalho ao manipular tarefas. Eles podem ser usados para fornecer uma visão geral de até que ponto o fluxo de trabalho está por meio do processamento. Quando o fluxo de trabalho é executado, o usuário pode exibir o progresso descrito por **Estágio** (em vez de etapa individual).

Como os nomes de etapa individuais podem ser específicos e técnicos, os nomes de estágio podem ser definidos para fornecer uma visualização conceitual do progresso do fluxo de trabalho.

Por exemplo, para um fluxo de trabalho com seis etapas e quatro estágios:

1. Você pode [configurar Estágios do Fluxo de Trabalho (que mostram o Progresso do Fluxo de Trabalho) e atribuir o estágio apropriado a cada etapa do fluxo de trabalho](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * Vários nomes de estágio podem ser criados.
   * Em seguida, um nome de estágio individual é atribuído a cada etapa (um nome de estágio pode ser atribuído a uma ou mais etapas).

   | **Nome da Etapa** | **Estágio (atribuído à etapa)** |
   |---|---|
   | Etapa 1 | Criar |
   | Etapa 2 | Criar |
   | Etapa 3 | Revisar |
   | Etapa 4 | Aprovar |
   | Etapa 5 | Concluído |
   | Etapa 6 | Concluído |

1. Quando o fluxo de trabalho é executado, o usuário pode visualizar o progresso de acordo com os Nomes dos estágios (em vez dos nomes das etapas). O andamento do fluxo de trabalho é exibido na guia [INFORMAÇÕES DO FLUXO DE TRABALHO da janela de detalhes da tarefa do item do fluxo de trabalho](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) listado na [Caixa de Entrada](/help/sites-authoring/inbox.md).

### Workflows e Forms {#workflows-and-forms}

Normalmente, os fluxos de trabalho são usados para processar envios de formulários no AEM. Pode ser com os [componentes de formulário principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html?lang=pt-BR) disponíveis em uma instância AEM padrão ou com a [solução AEM Forms](/help/forms/using/aem-forms-workflow.md).

Ao criar um formulário, o envio dele pode ser facilmente associado a um modelo de fluxo de trabalho. Por exemplo, para armazenar o conteúdo em um local específico do repositório ou notificar um usuário sobre o envio do formulário e seu conteúdo.

### Fluxos de trabalho e tradução {#workflows-and-translation}

Os fluxos de trabalho também fazem parte do processo [Tradução](/help/sites-administering/translation.md).
