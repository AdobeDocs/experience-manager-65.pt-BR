---
title: Inicialização de workflows
description: Saiba como administrar workflows no Adobe Experience Manager para iniciá-los usando vários métodos, manual ou automaticamente.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 84a1964c-4121-4763-b946-9eee6093747d
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%

---

# Inicialização de workflows{#starting-workflows}

Ao administrar workflows, você pode iniciá-los usando vários métodos:

* Manualmente:

   * De um [Modelo de Fluxo de Trabalho](#workflow-models).
   * Usando um pacote de fluxo de trabalho para [processamento em lote](#workflow-packages-for-batch-processing).

* Automaticamente:

   * Em resposta às alterações de nó; [usando um Iniciador](#workflows-launchers).

>[!NOTE]
>
>Outros métodos também estão disponíveis para os autores; para obter detalhes completos, consulte:
>
>* [Aplicando Fluxos de Trabalho a Páginas](/help/sites-authoring/workflows-applying.md)
>* [Como aplicar fluxos de trabalho a ativos do DAM](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/br/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [Projetos de tradução](/help/sites-administering/tc-manage.md)
>

## Modelos do fluxo de trabalho {#workflow-models}

Você pode iniciar um fluxo de trabalho [ com base em um dos modelos](/help/sites-administering/workflows.md#workflow-models-and-instances) listados no console Modelos de Fluxo de Trabalho. As únicas informações obrigatórias são o conteúdo, embora um título e/ou comentário também possa ser adicionado.

## Iniciadores de fluxos de trabalho {#workflows-launchers}

O Iniciador do fluxo de trabalho monitora as alterações no repositório de conteúdo para iniciar fluxos de trabalho dependendo da localização e do tipo de recurso do nó alterado.

Usando o **Iniciador**, você pode:

* Consulte os workflows já iniciados para nós específicos.
* Selecione um workflow a ser iniciado quando um determinado nó/tipo de nó for criado/modificado/removido.
* Remover uma relação existente entre fluxo de trabalho e nó.

Um inicializador pode ser criado para qualquer nó. No entanto, as alterações em determinados nós não iniciam workflows. As alterações nos nós abaixo dos seguintes caminhos não fazem com que os fluxos de trabalho sejam inicializados:

* `/var/workflow/instances`
* Qualquer nó da caixa de entrada de fluxo de trabalho localizado em qualquer lugar na ramificação `/home/users`
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * Exceção: as alterações nos nós abaixo de `/var/statistics/tracking` *do* fazem com que os fluxos de trabalho sejam inicializados.

Várias definições estão incluídas na instalação padrão. Eles são usados para tarefas de gerenciamento de ativos digitais e colaboração social:

![wf-100](assets/wf-100.png)

## Pacotes de fluxo de trabalho para processamento em lote {#workflow-packages-for-batch-processing}

Pacotes de fluxo de trabalho são pacotes que podem ser passados para um fluxo de trabalho como carga útil para processamento, permitindo que vários recursos sejam processados.

Um pacote de workflow:

* contém links para um conjunto de recursos (como páginas, ativos).
* O armazena informações do pacote, como a data de criação, o usuário que criou o pacote e uma breve descrição.
* é definido usando um modelo de página especializado; essas páginas permitem que o usuário especifique os recursos no pacote.
* pode ser usado várias vezes.
* pode ser alterado pelo usuário (adicionar ou remover recursos) enquanto a instância do fluxo de trabalho está em execução.

## Iniciar um fluxo de trabalho a partir do console Modelos {#starting-a-workflow-from-the-models-console}

1. Navegue até o console **Modelos** usando **Ferramentas**, **Fluxo de trabalho** e **Modelos**.
1. Selecione o fluxo de trabalho (de acordo com a exibição do console); também é possível usar Pesquisar (parte superior esquerda), se necessário:

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >O indicador **[Transient](/help/sites-developing/workflows.md#transient-workflows)** mostra fluxos de trabalho para os quais o histórico de fluxo de trabalho não é persistente.

1. Selecione **Iniciar Fluxo de Trabalho** na barra de ferramentas.
1. A caixa de diálogo Executar fluxo de trabalho é aberta, permitindo especificar:

   * **Carga**

     Pode ser uma página, nó, ativo, pacote, entre outros recursos.

   * **Título**

     Um título opcional para ajudar a identificar esta instância.

   * **Comentário**

     Um comentário opcional para ajudar a indicar detalhes desta instância.

   ![wf-104](assets/wf-104.png)

## Criação de uma configuração do iniciador {#creating-a-launcher-configuration}

1. Navegue até o console **Iniciadores de Fluxo de Trabalho** usando **Ferramentas**, **Fluxo de Trabalho** e **Iniciadores**.
1. Selecione **Criar**, depois **Adicionar Inicializador** para abrir a caixa de diálogo:

   ![wf-105](assets/wf-105.png)

   * **Tipo de evento**

     O tipo de evento que inicia o fluxo de trabalho:

      * Criado
      * Modificado
      * Removido

   * **Nodetype**

     O tipo de nó ao qual o inicializador do fluxo de trabalho se aplica.

   * **Caminho**

     O caminho ao qual o inicializador do fluxo de trabalho se aplica.

   * **Modo(s) de Execução**

     O tipo de servidor ao qual o inicializador do fluxo de trabalho se aplica. Selecione **Author**, **Publish** ou **Author &amp; Publish**.

   * **Condições**

     Uma lista de condições para valores de nó que, quando avaliados, determinam se o workflow é iniciado. Por exemplo, a seguinte condição faz com que o fluxo de trabalho seja iniciado quando o nó tem um nome de propriedade com o valor User:

     name==Usuário

   * **Recursos**

     Uma lista de recursos a serem habilitados. Selecione os recursos necessários usando o seletor suspenso.

   * **Recursos Desabilitados**

   Uma lista de recursos a serem desabilitados. Selecione os recursos necessários usando o seletor suspenso.

   * **Modelo de Fluxo de Trabalho**

     O fluxo de trabalho a ser iniciado quando o Tipo de evento ocorrer no Tipo de nó e/ou Caminho na Condição definida.

   * **Descrição**

     Seu próprio texto para descrever e identificar a configuração do iniciador.

   * **Ativar**

     Controla se o inicializador do fluxo de trabalho está ativado:

      * Selecione **Habilitar** para iniciar fluxos de trabalho quando as propriedades de configuração forem satisfeitas.
      * Selecione **Desabilitar** quando o fluxo de trabalho não deve ser executado (nem mesmo quando as propriedades de configuração forem satisfeitas).

   * **Lista de exclusões**

     Isso especifica todos os eventos JCR a serem excluídos (ou seja, ignorados) ao determinar se um fluxo de trabalho deve ser acionado.

     Esta propriedade do inicializador é uma lista de itens separados por vírgulas: &quot;

      * `property-name` ignorar qualquer evento `jcr` disparado no nome de propriedade especificado. &quot;
      * `event-user-data:<*someValue*>` ignora qualquer evento que contenha `*<someValue*`> `user-data` definido por meio da API [`ObservationManager` ] (https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String).

     Por exemplo:

     `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

     Esse recurso pode ser usado para ignorar qualquer alteração acionada por outro processo de fluxo de trabalho adicionando o item de exclusão:

     `event-user-data:changedByWorkflowProcess`

1. Selecione **Criar** para criar o inicializador e retornar ao console.

   Quando o evento apropriado ocorre, o inicializador é acionado e o fluxo de trabalho é iniciado.

## Gerenciamento de uma configuração do iniciador {#managing-a-launcher-configuration}

Depois de criar a configuração do inicializador, você pode usar o mesmo console para selecionar a instância e **Exibir Propriedades** (e editá-las) ou **Excluir**.
