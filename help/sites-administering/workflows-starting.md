---
title: Iniciando Workflows
seo-title: Iniciando Workflows
description: Saiba como start Workflows em AEM.
seo-description: Saiba como start Workflows em AEM.
uuid: 0648d335-ecce-459d-95fd-3d4d76181b32
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: e9ab4796-a050-40de-b073-af7d33cff009
translation-type: tm+mt
source-git-commit: 967018907e32e5916df72ff16dfc7bc06f8dbed8
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 5%

---


# Iniciando Workflows{#starting-workflows}

Ao administrar workflows, você pode start-los usando uma variedade de métodos:

* Manualmente:

   * De um [Modelo de Fluxo de Trabalho](#workflow-models).
   * Usando um pacote de fluxo de trabalho para [processamento em lote](#workflow-packages-for-batch-processing).

* Automaticamente:

   * Em resposta a alterações de nó; [utilizando um Iniciador](#workflows-launchers).

>[!NOTE]
>
>Os autores também dispõem de outros métodos; para obter detalhes completos, consulte:
>
>* [Aplicação de fluxos de trabalho às páginas](/help/sites-authoring/workflows-applying.md)
>* [Como aplicar fluxos de trabalho a ativos do DAM](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [Projetos de tradução](/help/sites-administering/tc-manage.md)

>



## Modelos do fluxo de trabalho {#workflow-models}

Você pode start um fluxo de trabalho [com base em um dos modelos](/help/sites-administering/workflows.md#workflow-models-and-instances) listados no console Modelos de fluxo de trabalho. A única informação obrigatória é a carga, embora um título e/ou comentário também possa ser adicionado.

## Iniciadores de workflows {#workflows-launchers}

O Workflow Launcher monitora as alterações no repositório de conteúdo para iniciar workflows dependendo do local e do tipo de recurso do nó alterado.

Usando o **Iniciador** você pode:

* Consulte os workflows já iniciados para nós específicos.
* Selecione um fluxo de trabalho a ser iniciado quando determinado nó/tipo de nó tiver sido criado/modificado/removido.
* Remova uma relação fluxo de trabalho para nó existente.

Um iniciador pode ser criado para qualquer nó. No entanto, as alterações em determinados nós não iniciam workflows. As alterações nos nós abaixo dos seguintes caminhos não fazem com que os workflows sejam iniciados:

* `/var/workflow/instances`
* Qualquer nó de caixa de entrada de fluxo de trabalho localizado em qualquer lugar na ramificação `/home/users`
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * Exceção: As alterações nos nós abaixo de `/var/statistics/tracking` *do* fazem com que os workflows sejam iniciados.

Várias definições estão incluídas na instalação padrão. Eles são usados para tarefas de gerenciamento de ativos digitais e colaboração social:

![wf-100](assets/wf-100.png)

## Pacotes de fluxo de trabalho para processamento em lote {#workflow-packages-for-batch-processing}

Os pacotes de fluxo de trabalho são pacotes que podem ser enviados para um fluxo de trabalho como carga para processamento, permitindo que vários recursos sejam processados.

Um pacote de fluxo de trabalho:

* contém links para um conjunto de recursos (como páginas, ativos).
* contém informações do pacote, como a data de criação, o usuário que criou o pacote e uma breve descrição.
* é definido usando um modelo de página especializado; essas páginas permitem que o usuário especifique os recursos no pacote.
* pode ser usado várias vezes.
* pode ser alterado pelo usuário (adicionar ou remover recursos) enquanto a instância do fluxo de trabalho estiver em execução.

## Iniciando um fluxo de trabalho a partir do console Modelos {#starting-a-workflow-from-the-models-console}

1. Navegue até o console **Modelos** usando **Ferramentas**, **Fluxo de trabalho** e, em seguida, **Modelos**.
1. Selecione o fluxo de trabalho (de acordo com a visualização do console); você também pode usar Pesquisar (parte superior esquerda) se necessário:

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >O indicador **[Transitório](/help/sites-developing/workflows.md#transient-workflows)** mostra workflows cujo histórico de fluxo de trabalho não será persistente.

1. Selecione **Fluxo de trabalho do Start** na barra de ferramentas.
1. A caixa de diálogo Executar fluxo de trabalho será aberta, permitindo que você especifique:

   * **Carga**

      Pode ser uma página, nó, ativo, pacote, entre outros recursos.

   * **Título**

      Um título opcional para ajudar a identificar essa instância.

   * **Comentário**

      Um comentário opcional para ajudar a indicar detalhes desta instância.
   ![wf-104](assets/wf-104.png)

## Criando uma Configuração do Iniciador {#creating-a-launcher-configuration}

1. Navegue até o console **Inicializações de fluxo de trabalho** usando **Ferramentas**, **Fluxo de trabalho** e, em seguida, **Iniciadores**.
1. Selecione **Criar** e **Adicionar Iniciador** para abrir a caixa de diálogo:

   ![wf-105](assets/wf-105.png)

   * **Tipo de evento**

      O tipo de evento que iniciará o fluxo de trabalho:

      * Criado
      * Modificado
      * Removido
   * **Nodetype**

      O tipo de nó ao qual o iniciador do fluxo de trabalho se aplica.

   * **Caminho**

      O caminho ao qual o iniciador do fluxo de trabalho se aplica.

   * **Modo(s) de execução**

      O tipo de servidor ao qual o iniciador do fluxo de trabalho se aplica. Selecione **Autor**, **Publicar** ou **Autor e publicação**.

   * **Condições**

      Uma lista de condições para valores de nó que, quando avaliados, determinam se o fluxo de trabalho é iniciado. Por exemplo, a seguinte condição faz com que o fluxo de trabalho seja iniciado quando o nó tiver um nome de propriedade com o valor Usuário:

      name==Usuário

   * **Recursos**

      Uma lista de recursos a serem ativados. Selecione os recursos necessários usando o seletor suspenso.

   * **Recursos desativados**

   Uma lista de recursos a serem desativados. Selecione os recursos necessários usando o seletor suspenso.

   * **Modelo de fluxo de trabalho**

      O fluxo de trabalho a ser iniciado quando o Tipo de evento ocorrer no Tipo de nó e/ou Caminho sob a Condição definida.

   * **Descrição**

      Seu próprio texto para descrever e identificar a configuração do iniciador.

   * **Ativar**

      Controla se o inicializador de fluxo de trabalho está ativado:

      * Selecione **Ativar** para iniciar workflows quando as propriedades de configuração forem satisfeitas.
      * Selecione **Desativar** quando o fluxo de trabalho não deve ser executado (nem mesmo quando as propriedades de configuração forem satisfeitas).
   * **Excluir lista**

      Isso especifica quaisquer eventos JCR a serem excluídos (ou seja, ignorar) ao determinar se um fluxo de trabalho deve ser acionado.

      Esta propriedade de iniciador é uma lista de itens separada por vírgulas: &quot;

      * `property-name` ignorar qualquer  `jcr` evento que tenha sido acionado no nome da propriedade especificada. &quot;
      * `event-user-data:<*someValue*>` ignora qualquer evento que contenha o  `*<someValue*`>  `user-data` definido pela  [ `ObservationManager` API](https://docs.adobe.com/content/docs/en/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String).

      Por exemplo:

      `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

      Este recurso pode ser usado para ignorar quaisquer alterações acionadas por outro processo de fluxo de trabalho ao adicionar o item excluído:

      `event-user-data:changedByWorkflowProcess`





1. Selecione **Criar** para criar o iniciador e voltar ao console.

   Quando o evento apropriado ocorrer, o iniciador será acionado e o fluxo de trabalho será iniciado.

## Gerenciando uma Configuração do Iniciador {#managing-a-launcher-configuration}

Depois de criar a configuração do iniciador, você pode usar o mesmo console para selecionar a instância e, em seguida, **Propriedades da Visualização** (e editá-las) ou **Excluir**.
