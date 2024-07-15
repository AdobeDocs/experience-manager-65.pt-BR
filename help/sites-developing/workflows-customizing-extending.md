---
title: Ampliação da funcionalidade do fluxo de trabalho
description: Saiba como estender a funcionalidade de fluxo de trabalho do Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 9e205912-50a6-414a-b8d4-a0865269d0e0
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3499'
ht-degree: 1%

---

# Ampliação da funcionalidade do fluxo de trabalho{#extending-workflow-functionality}

Este tópico descreve como desenvolver componentes de etapa personalizados para seus workflows e, em seguida, como interagir programaticamente com workflows.

A criação de uma etapa de fluxo de trabalho personalizada envolve as seguintes atividades:

* Desenvolva o componente da etapa do fluxo de trabalho.
* Implemente a funcionalidade da etapa como um serviço OSGi ou um script ECMA.

Você também pode [interagir com seus fluxos de trabalho a partir de seus programas e scripts](/help/sites-developing/workflows-program-interaction.md).

## Componentes da etapa do fluxo de trabalho - Noções básicas {#workflow-step-components-the-basics}

Um componente da etapa do fluxo de trabalho define a aparência e o comportamento da etapa ao criar modelos de fluxo de trabalho:

* A categoria e o nome da etapa no sidekick do fluxo de trabalho.
* A aparência da etapa em modelos de fluxo de trabalho.
* A caixa de diálogo de edição para configurar propriedades do componente.
* O serviço ou script que é executado no tempo de execução.

Assim como em [todos os componentes](/help/sites-developing/components.md), os componentes da etapa do fluxo de trabalho herdam do componente especificado para a propriedade `sling:resourceSuperType`. O diagrama a seguir mostra a hierarquia dos nós `cq:component` que formam a base de todos os componentes da etapa do fluxo de trabalho. O diagrama também inclui os componentes da **Etapa do processo**, da **Etapa de participante** e da **Etapa de participante dinâmica**, pois esses são os pontos de partida mais comuns (e básicos) para o desenvolvimento de componentes de etapa personalizados.

![aem_wf_componentinherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>Você ***deve*** não alterar nada no caminho `/libs`.
>
>Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recrie o item necessário (isto é, como ele existe em `/libs` em `/apps`
>2. Fazer alterações em `/apps`

O componente `/libs/cq/workflow/components/model/step` é o ancestral comum mais próximo das **Etapa de Processo**, **Etapa de Participante** e **Etapa de Participante Dinâmica**, que herdam os seguintes itens:

* `step.jsp`

  O script `step.jsp` renderiza o título do componente da etapa quando ele é adicionado a um modelo.

  ![wf-22-1](assets/wf-22-1.png)

* [cq:dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

  Uma caixa de diálogo com as seguintes guias:

   * **Comum**: para editar o título e a descrição.
   * **Avançado**: para editar propriedades de notificação por email.

  ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

  >[!NOTE]
  >
  >Quando as guias da caixa de diálogo de edição de um componente da etapa não corresponderem a essa aparência padrão, o componente da etapa terá scripts definidos, propriedades do nó ou guias de caixa de diálogo que substituem essas guias herdadas.

### Scripts ECMA {#ecma-scripts}

Os seguintes objetos estão disponíveis (dependendo do tipo de etapa) nos scripts ECMA:

* [ItemDeTrabalho](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html)
* [WorkflowSession](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) workflowSession
* [DadosFluxoDeTrabalho](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) DadosFluxoDeTrabalho
* `args`: matriz com os argumentos do processo.

* `sling`: para acessar outros serviços osgi.
* `jcrSession`

### MetaDataMaps {#metadatamaps}

Você pode usar metadados de fluxo de trabalho para manter as informações necessárias durante a vida útil do fluxo de trabalho. Um requisito comum de etapas do fluxo de trabalho é criar dados persistentes para uso futuro no fluxo de trabalho ou recuperar os dados persistentes.

Há três tipos de objetos MetaDataMap - para objetos `Workflow`, `WorkflowData` e `WorkItem`. Todos têm a mesma finalidade: armazenar metadados.

Um item de trabalho tem seu próprio MetaDataMap que só pode ser usado enquanto esse item de trabalho (por exemplo, etapa ) estiver em execução.

Os mapeamentos de metadados `Workflow` e `WorkflowData` são compartilhados em todo o fluxo de trabalho. Nesses casos, é recomendável usar apenas o mapa de metadados `WorkflowData`.

## Criação de componentes de etapa de fluxo de trabalho personalizados {#creating-custom-workflow-step-components}

Os componentes da etapa do fluxo de trabalho podem ser [criados da mesma maneira que qualquer outro componente](/help/sites-developing/components.md).

Para herdar de um dos componentes da etapa base (existentes), adicione a seguinte propriedade ao nó `cq:Component`:

* Nome: `sling:resourceSuperType`
* Tipo: `String`
* Valor: um dos seguintes caminhos que são resolvidos para um componente base:

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### Especificando o Título e a Descrição Default para Instâncias da Etapa {#specifying-the-default-title-and-description-for-step-instances}

Use o procedimento a seguir para especificar valores padrão para os campos **Título** e **Descrição** na guia **Comum**.

>[!NOTE]
>
>Os valores de campo são exibidos na instância da etapa quando ambos os requisitos a seguir são atendidos:
>
>* A caixa de diálogo de edição da etapa armazena o título e a descrição nos seguintes locais: >
>* `./jcr:title`
>* `./jcr:description` locais
>
>  Esse requisito é atendido quando a caixa de diálogo de edição usa a guia Comum que o componente `/libs/cq/flow/components/step/step` implementa.
>
>* O componente de etapa ou um ancestral do componente não substitui o script `step.jsp` que o componente `/libs/cq/flow/components/step/step` implementa.

1. Abaixo do nó `cq:Component`, adicione o seguinte nó:

   * Nome: `cq:editConfig`
   * Tipo: `cq:EditConfig`

   >[!NOTE]
   >
   >Para obter mais informações sobre o nó cq:editConfig, consulte [Configurando o Comportamento de Edição de um Componente](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. Abaixo do nó `cq:EditConfig`, adicione o seguinte nó:

   * Nome: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Adicionar propriedades `String` dos seguintes nomes ao nó `cq:formParameters`:

   * `jcr:title`: O valor preenche o campo **Título** da guia **Comum**.
   * `jcr:description`: O valor preenche o campo **Descrição** da guia **Comum**.

### Salvar valores de propriedade nos metadados de fluxo de trabalho {#saving-property-values-in-workflow-metadata}

>[!NOTE]
>
>Consulte [Persistindo e Acessando Dados](#persisting-and-accessing-data). Especificamente, para obter informações sobre como acessar o valor da propriedade em tempo de execução, consulte [Acessando Valores da Propriedade da Caixa de Diálogo em Tempo de Execução](#accessing-dialog-property-values-at-runtime).

A propriedade name de `cq:Widget` itens especifica o nó JCR que armazena o valor do widget. Quando os widgets na caixa de diálogo dos componentes da etapa do fluxo de trabalho armazenam valores abaixo do nó `./metaData`, o valor é adicionado ao fluxo de trabalho `MetaDataMap`.

Por exemplo, um campo de texto em uma caixa de diálogo é um nó `cq:Widget` que tem as seguintes propriedades:

| Nome | Tipo | Valor |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

O valor especificado neste campo de texto é adicionado ao objeto ` [MetaDataMap](#metadatamaps)` da instância de fluxo de trabalho e está associado à chave `subject`.

>[!NOTE]
>
>Quando a chave é `PROCESS_ARGS`, o valor está prontamente disponível nas implementações de script ECMA por meio da variável `args`. Nesse caso, o valor da propriedade de nome é `./metaData/PROCESS_ARGS.`

### Substituição da implementação da etapa {#overriding-the-step-implementation}

Cada componente da etapa base permite que os desenvolvedores de modelo de fluxo de trabalho configurem os seguintes recursos principais em tempo de design:

* Etapa do Processo: O serviço ou script ECMA a ser executado no tempo de execução.
* Etapa do participante: a ID do usuário ao qual foi atribuído o item de trabalho gerado.
* Etapa dinâmica do participante: o serviço ou script ECMA que seleciona o ID do usuário atribuído ao item de trabalho.

Para focalizar o componente para uso em um cenário de fluxo de trabalho específico, configure o recurso principal no design e remova a capacidade dos desenvolvedores de modelo de alterá-lo.

1. Abaixo do nó cq:component, adicione o seguinte nó:

   * Nome: `cq:editConfig`
   * Tipo: `cq:EditConfig`

   Para obter mais informações sobre o nó cq:editConfig, consulte [Configurando o Comportamento de Edição de um Componente](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. Abaixo do nó cq:EditConfig, adicione o seguinte nó:

   * Nome: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Adicione uma propriedade `String` ao nó `cq:formParameters`. O supertipo de componente determina o nome da propriedade:

   * Etapa do processo: `PROCESS`
   * Etapa do participante: `PARTICIPANT`
   * Etapa dinâmica do participante: `DYNAMIC_PARTICIPANT`

1. Especifique o valor da propriedade:

   * `PROCESS`: O caminho para o script ECMA ou o PID do serviço que implementa o comportamento da etapa.
   * `PARTICIPANT`: a identificação do usuário ao qual o item de trabalho foi atribuído.
   * `DYNAMIC_PARTICIPANT`: o caminho para o script ECMA ou o PID do serviço que seleciona o usuário para atribuir o item de trabalho.

1. Para remover a capacidade dos desenvolvedores de modelo de alterar os valores de propriedade, substitua a caixa de diálogo do supertipo de componente.

### Adicionar Forms e caixas de diálogo às etapas do participante {#adding-forms-and-dialogs-to-participant-steps}

Personalize o componente da etapa do participante para fornecer recursos encontrados nos componentes da [Etapa de participante do formulário](/help/sites-developing/workflows-step-ref.md#form-participant-step) e da [Etapa de participante da caixa de diálogo](/help/sites-developing/workflows-step-ref.md#dialog-participant-step):

* Apresente um formulário ao usuário quando ele abrir o item de trabalho gerado.
* Apresentar uma caixa de diálogo personalizada ao usuário quando ele concluir o item de trabalho gerado.

Execute o seguinte procedimento no novo componente (consulte [Criação de Componentes de Etapa de Fluxo de Trabalho Personalizado](#creating-custom-workflow-step-components)):

1. Abaixo do nó `cq:Component`, adicione o seguinte nó:

   * Nome: `cq:editConfig`
   * Tipo: `cq:EditConfig`

   Para obter mais informações sobre o nó cq:editConfig, consulte [Configurando o Comportamento de Edição de um Componente](/help/sites-developing/components-basics.md#edit-behavior).

1. Abaixo do nó cq:EditConfig, adicione o seguinte nó:

   * Nome: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Para apresentar um formulário quando o usuário abrir o item de trabalho, adicione a seguinte propriedade ao nó `cq:formParameters`:

   * Nome: `FORM_PATH`
   * Tipo: `String`
   * Valor: o caminho que é resolvido para o formulário

1. Para apresentar uma caixa de diálogo personalizada quando o usuário concluir o item de trabalho, adicione a seguinte propriedade ao nó `cq:formParameters`

   * Nome: `DIALOG_PATH`
   * Tipo: `String`
   * Valor: o caminho que é resolvido para a caixa de diálogo

### Configurar o comportamento do tempo de execução da etapa do fluxo de trabalho {#configuring-the-workflow-step-runtime-behavior}

Abaixo do nó `cq:Component`, adicione um nó `cq:EditConfig`. Abaixo, adicione um nó `nt:unstructured` (deve se chamar `cq:formParameters`) e, a esse nó, adicione as seguintes propriedades:

* Nome: `PROCESS_AUTO_ADVANCE`

   * Tipo: `Boolean`
   * Valor:

      * quando definido como `true`, o fluxo de trabalho executará essa etapa e continuará. isso é padrão e também é recomendado
      * quando `false`, o fluxo de trabalho será executado e interrompido; isso requer manipulação extra; portanto, `true` é recomendado

* Nome: `DO_NOTIFY`

   * Tipo: `Boolean`
   * Value: indica se as notificações por email devem ser enviadas para as etapas de participação do usuário (e presume que o servidor de email esteja configurado corretamente)

## Persistência e acesso a dados {#persisting-and-accessing-data}

### Dados persistentes para etapas de fluxo de trabalho subsequentes {#persisting-data-for-subsequent-workflow-steps}

Você pode usar metadados de fluxo de trabalho para manter as informações necessárias durante a vida útil do fluxo de trabalho - e entre etapas. Um requisito comum de etapas do fluxo de trabalho é criar dados persistentes para uso futuro ou recuperar os dados persistentes de etapas anteriores.

Os metadados do fluxo de trabalho são armazenados em um objeto [`MetaDataMap`](#metadatamaps). A API Java fornece o método [`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html) para retornar um objeto [`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) que forneça o objeto `MetaDataMap` apropriado. Este objeto `WorkflowData` `MetaDataMap` está disponível para o serviço OSGi ou script ECMA de um componente de etapa.

#### Java {#java}

O método execute da implementação `WorkflowProcess` recebeu o objeto `WorkItem`. Use este objeto para obter o objeto `WorkflowData` para a instância de fluxo de trabalho atual. O exemplo a seguir adiciona um item ao objeto de fluxo de trabalho `MetaDataMap` e registra cada item. O item (&quot;mykey&quot;, &quot;My Step Value&quot;) está disponível para etapas subsequentes no workflow.

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {

    MetaDataMap wfd = item.getWorkflow().getWorkflowData().getMetaDataMap();

    wfd.put("mykey", "My Step Value");

    Set<String> keyset = wfd.keySet();
    Iterator<String> i = keyset.iterator();
    while (i.hasNext()){
     Object key = i.next();
     log.info("The workflow medata includes key {} and value {}",key.toString(),wfd.get(key).toString());
    }
}
```

#### Script ECMA {#ecma-script}

A variável `graniteWorkItem` é a representação de script ECMA do objeto Java `WorkItem` atual. Portanto, você pode usar a variável `graniteWorkItem` para obter os metadados do fluxo de trabalho. O script ECMA a seguir pode ser usado para implementar uma **Etapa do Processo** para adicionar um item ao objeto de fluxo de trabalho `MetaDataMap` e registrar cada item. Esses itens ficam disponíveis nas etapas subsequentes do fluxo de trabalho.

>[!NOTE]
>
>A variável `metaData` que está imediatamente disponível para o script de etapa são os metadados da etapa. Os metadados da etapa são diferentes dos metadados do fluxo de trabalho.

```
var currentDateInMillis = new Date().getTime();

graniteWorkItem.getWorkflowData().getMetaDataMap().put("hardcodedKey","theKey");

graniteWorkItem.getWorkflowData().getMetaDataMap().put("currentDateInMillisKey",currentDateInMillis);

var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
```

### Acessando Valores de Propriedade da Caixa de Diálogo no Tempo de Execução {#accessing-dialog-property-values-at-runtime}

O objeto `MetaDataMap` de instâncias de fluxo de trabalho é útil para armazenar e recuperar dados durante toda a vida útil do fluxo de trabalho. Para implementações de componentes de etapa de fluxo de trabalho, o `MetaDataMap` é especialmente útil para recuperar valores de propriedade de componente em tempo de execução.

>[!NOTE]
>
>Para obter informações sobre como configurar a caixa de diálogo do componente para armazenar propriedades como metadados de fluxo de trabalho, consulte [Salvando Valores de Propriedade nos Metadados de Fluxo de Trabalho](#saving-property-values-in-workflow-metadata).

O fluxo de trabalho `MetaDataMap` está disponível para implementações de processo de script Java e ECMA:

* Em implementações Java da interface WorkflowProcess, o parâmetro `args` é o objeto `MetaDataMap` do fluxo de trabalho.

* Em implementações de script ECMA, o valor está disponível usando as variáveis `args` e `metadata`.

### Exemplo: Recuperação de Argumentos do Componente de Etapa do Processo {#example-retrieving-the-arguments-of-the-process-step-component}

A caixa de diálogo de edição do componente **Etapa do Processo** inclui a propriedade **Argumentos**. O valor da propriedade **Arguments** é armazenado nos metadados do fluxo de trabalho e está associado à chave `PROCESS_ARGS`.

No diagrama a seguir, o valor da propriedade **Arguments** é `argument1, argument2`:

![wf-24](assets/wf-24.png)

#### Java {#java-1}

O código Java a seguir é o método `execute` para uma implementação `WorkflowProcess`. O método registra o valor no `args` `MetaDataMap` que está associado à chave `PROCESS_ARGS`.

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

Quando uma etapa do processo que usa essa implementação Java é executada, o log contém a seguinte entrada:

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### Script ECMA {#ecma-script-1}

O seguinte script ECMA é usado como o processo para a **Etapa do processo**. Ele registra o número de argumentos e os valores do argumento:

```
var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
log.info("hardcodedKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("hardcodedKey"));
log.info("currentDateInMillisKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("currentDateInMillisKey"));
```

>[!NOTE]
>
>Esta seção descreve como trabalhar com argumentos para etapas do processo. As informações também se aplicam aos seletores de participantes dinâmicos.

>[!NOTE]
>Para obter outro exemplo de armazenamento de propriedades do componente nos metadados do fluxo de trabalho, consulte Exemplo: criar uma etapa do fluxo de trabalho do agente de log. Este exemplo apresenta uma caixa de diálogo que associa o valor dos metadados a uma chave diferente de PROCESS_ARGS.

### Scripts e Argumentos do Processo {#scripts-and-process-arguments}

Em um script para um componente **Etapa do processo**, os argumentos estão disponíveis por meio do objeto `args`.

Ao criar um componente de etapa personalizado, o objeto `metaData` está disponível em um script. Esse objeto é limitado a um único argumento de string.

## Desenvolvimento de implementações de etapas do processo {#developing-process-step-implementations}

Quando as etapas do processo são iniciadas durante o processo de um workflow, as etapas enviam uma solicitação para um serviço OSGi ou executam um script ECMA. Desenvolva o serviço ou script ECMA que executa as ações exigidas pelo seu fluxo de trabalho.

>[!NOTE]
>
>Para obter informações sobre como associar o componente Etapa do Processo ao serviço ou script, consulte [Etapa do Processo](/help/sites-developing/workflows-step-ref.md#process-step) ou [Substituição da Implementação da Etapa](#overriding-the-step-implementation).

### Implementando uma etapa do processo com uma classe Java {#implementing-a-process-step-with-a-java-class}

Para definir uma etapa do processo como um componente de serviço OSGI (pacote Java):

1. Crie o pacote e implante-o no contêiner OSGI. Consulte a documentação sobre a criação de um pacote com [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) ou [Eclipse](/help/sites-developing/howto-projects-eclipse.md).

   >[!NOTE]
   >
   >O componente OSGI precisa implementar a interface `WorkflowProcess` com seu método `execute()`. Consulte o código de exemplo abaixo.

   >[!NOTE]
   >
   >O nome do pacote precisa ser adicionado à seção `<*Private-Package*>` da configuração `maven-bundle-plugin`.

1. Adicione a propriedade SCR `process.label` e defina o valor conforme necessário. Esse será o nome com o qual a etapa do processo será listada ao usar o componente genérico **Etapa do processo**. Veja o exemplo abaixo.
1. No editor **Modelos**, adicione a etapa do processo ao fluxo de trabalho usando o componente genérico **Etapa do processo**.
1. Na caixa de diálogo de edição (da **Etapa do processo**), vá para a guia **Processo** e selecione a implementação do processo.
1. Se você usar argumentos em seu código, defina os **Argumentos do processo**. Por exemplo: falso.
1. Salve as alterações para a etapa e o modelo de fluxo de trabalho (canto superior esquerdo do editor de modelo).

Os métodos java, respectivamente, as classes que implementam o método Java executável são registrados como serviços OSGI, permitindo que você adicione métodos a qualquer momento durante o tempo de execução.

O seguinte componente OSGI adiciona a propriedade `approved` ao nó de conteúdo da página quando a carga é uma página:

```java
package com.adobe.example.workflow.impl.process;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.exec.WorkflowProcess;
import com.adobe.granite.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import org.osgi.framework.Constants;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

/**
 * Sample workflow process that sets an <code>approve</code> property to the payload based on the process argument value.
 */
@Component
@Service
public class MyProcess implements WorkflowProcess {

 @Property(value = "An example workflow process implementation.")
 static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
 @Property(value = "Adobe")
 static final String VENDOR = Constants.SERVICE_VENDOR;
 @Property(value = "My Sample Workflow Process")
 static final String LABEL="process.label";

 private static final String TYPE_JCR_PATH = "JCR_PATH";

 public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
  WorkflowData workflowData = item.getWorkflowData();
  if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
   String path = workflowData.getPayload().toString() + "/jcr:content";
   try {
    Session jcrSession = session.adaptTo(Session.class);
    Node node = (Node) jcrSession.getItem(path);
    if (node != null) {
     node.setProperty("approved", readArgument(args));
     jcrSession.save();
    }
   } catch (RepositoryException e) {
    throw new WorkflowException(e.getMessage(), e);
   }
  }
 }

 private boolean readArgument(MetaDataMap args) {
  String argument = args.get("PROCESS_ARGS", "false");
  return argument.equalsIgnoreCase("true");
 }
}
```

>[!NOTE]
>
>Se o processo falhar três vezes seguidas, um item será colocado na Caixa de entrada do administrador do fluxo de trabalho.

### Utilização do ECMAScript {#using-ecmascript}

Os scripts ECMA permitem que os desenvolvedores de script implementem etapas de processo. Os scripts estão no repositório JCR e são executados nele.

A tabela a seguir lista as variáveis que estão imediatamente disponíveis para processar scripts, fornecendo acesso aos objetos da API Java do workflow.

| Classe Java | Nome da variável de script | Descrição |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | A instância da etapa atual. |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | A sessão de fluxo de trabalho da instância da etapa atual. |
| `String[]` (contém argumentos de processo) | `args` | Os argumentos da etapa. |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | Os metadados da instância de etapa atual. |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | Fornece acesso ao ambiente de tempo de execução do Sling. |

O exemplo de script a seguir demonstra como acessar o nó JCR que representa a carga do fluxo de trabalho. A variável `graniteWorkflowSession` é adaptada a uma variável de sessão JCR, que é usada para obter o nó do caminho da carga.

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getNode(path);
    if (node.hasProperty("approved")){
     node.setProperty("approved", args[0] == "true" ? true : false);
     node.save();
 }
}
```

O script a seguir verifica se a carga é uma imagem (arquivo `.png`), cria uma imagem em preto-e-branco dela e a salva como um nó irmão.

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getRootNode().getNode(path.substring(1));
     if (node.isNodeType("nt:file") && node.getProperty("jcr:content/jcr:mimeType").getString().indexOf("image/") == 0) {
        var is = node.getProperty("jcr:content/jcr:data").getStream();
        var layer = new Packages.com.day.image.Layer(is);
        layer.grayscale();
                var parent = node.getParent();
                var gn = parent.addNode("grey" + node.getName(), "nt:file");
        var content = gn.addNode("jcr:content", "nt:resource");
                content.setProperty("jcr:mimeType","image/png");
                var cal = Packages.java.util.Calendar.getInstance();
                content.setProperty("jcr:lastModified",cal);
                var f = Packages.java.io.File.createTempFile("test",".png");
        var tout = new Packages.java.io.FileOutputStream(f);
        layer.write("image/png", 1.0, tout);
        var fis = new Packages.java.io.FileInputStream(f);
                content.setProperty("jcr:data", fis);
                parent.save();
        tout.close();
        fis.close();
        is.close();
        f.deleteOnExit();
    }
}
```

Para usar o script:

1. Crie o script (por exemplo, com CRXDE Lite) e salve-o no repositório abaixo de `//apps/workflow/scripts/`
1. Para especificar um título que identifique o script na caixa de diálogo de edição **Etapa do processo**, adicione as seguintes propriedades ao nó `jcr:content` do script:

   | Nome | Tipo | Valor |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | O nome a ser exibido na caixa de diálogo de edição. |

1. Edite a instância **Etapa do Processo** e especifique o script a ser usado.

## Desenvolvendo seletores de participantes {#developing-participant-choosers}

Você pode desenvolver seletores de participantes para **componentes da Etapa dinâmica de participantes**.

Quando um componente **Etapa dinâmica de participante** é iniciado durante um fluxo de trabalho, a etapa precisa determinar o participante ao qual o item de trabalho gerado pode ser atribuído. Para fazer isso, siga um destes procedimentos:

* envia uma solicitação a um serviço OSGi
* executa um script ECMA para selecionar o participante

Você pode desenvolver um serviço ou script ECMA que selecione o participante de acordo com os requisitos do seu fluxo de trabalho.

>[!NOTE]
>
>Para obter informações sobre como associar o componente **Etapa dinâmica de participante** ao serviço ou script, consulte [Etapa dinâmica de participante](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) ou [Substituição da implementação da etapa](#persisting-and-accessing-data).

### Desenvolvendo um seletor de participantes usando uma classe Java {#developing-a-participant-chooser-using-a-java-class}

Para definir uma etapa do participante como um componente de serviço OSGI (classe Java):

1. O componente OSGI precisa implementar a interface `ParticipantStepChooser` com seu método `getParticipant()`. Consulte o código de exemplo abaixo.

   Crie o pacote e implante-o no contêiner OSGI.

1. Adicione a propriedade SCR `chooser.label` e defina o valor conforme necessário. Esse será o nome com que seu seletor de participantes será listado, usando o componente **Etapa dinâmica de participante**. Veja o exemplo:

   ```java
   package com.adobe.example.workflow.impl.process;
   
   import com.adobe.granite.workflow.WorkflowException;
   import com.adobe.granite.workflow.WorkflowSession;
   import com.adobe.granite.workflow.exec.ParticipantStepChooser;
   import com.adobe.granite.workflow.exec.WorkItem;
   import com.adobe.granite.workflow.exec.WorkflowData;
   import com.adobe.granite.workflow.metadata.MetaDataMap;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   
   import org.osgi.framework.Constants;
   
   /**
    * Sample dynamic participant step that determines the participant based on a path given as argument.
    */
   @Component
   @Service
   
   public class MyDynamicParticipant implements ParticipantStepChooser {
   
    @Property(value = "An example implementation of a dynamic participant chooser.")
    static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
       @Property(value = "Adobe")
       static final String VENDOR = Constants.SERVICE_VENDOR;
       @Property(value = "Dynamic Participant Chooser Process")
       static final String LABEL=ParticipantStepChooser.SERVICE_PROPERTY_LABEL;
   
       private static final String TYPE_JCR_PATH = "JCR_PATH";
   
       public String getParticipant(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
           WorkflowData workflowData = workItem.getWorkflowData();
           if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
               String path = workflowData.getPayload().toString();
               String pathFromArgument = args.get("PROCESS_ARGS", String.class);
               if (pathFromArgument != null && path.startsWith(pathFromArgument)) {
                   return "admin";
               }
           }
           return "administrators";
       }
   }
   ```

1. No editor **Modelos**, adicione a etapa de participante dinâmico ao fluxo de trabalho usando o componente genérico **Etapa de participante dinâmico**.
1. Na caixa de diálogo de edição, selecione a guia **Seletor de participantes** e selecione a implementação do seletor.
1. Se você usar argumentos no código, defina os **Argumentos do processo**. Para este exemplo: `/content/we-retail/de`.
1. Salve as alterações para a etapa e o modelo de fluxo de trabalho.

### Desenvolvendo um seletor de participantes usando um script ECMA {#developing-a-participant-chooser-using-an-ecma-script}

Você pode criar um script ECMA que selecione o usuário atribuído ao item de trabalho gerado pela **Etapa de participante**. O script deve incluir uma função chamada `getParticipant` que não requer argumentos e retorna um `String` que contém a ID de um usuário ou grupo.

Os scripts estão no repositório JCR e são executados nele.

A tabela a seguir lista as variáveis que fornecem acesso imediato aos objetos Java do workflow nos scripts.

| Classe Java | Nome da variável de script |
|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` |
| `String[]` (contém argumentos de processo) | `args` |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` |

```
function getParticipant() {
    var workflowData = graniteWorkItem.getWorkflowData();
    if (workflowData.getPayloadType() == "JCR_PATH") {
        var path = workflowData.getPayload().toString();
        if (path.indexOf("/content/we-retail/de") == 0) {
            return "admin";
        } else {
            return "administrators";
        }
    }
}
```

1. Crie o script (por exemplo, com CRXDE Lite) e salve-o no repositório abaixo de `//apps/workflow/scripts`
1. Para especificar um título que identifique o script na caixa de diálogo de edição **Etapa do processo**, adicione as seguintes propriedades ao nó `jcr:content` do script:

   | Nome | Tipo | Valor |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | O nome a ser exibido na caixa de diálogo de edição. |

1. Edite a instância [Etapa dinâmica de participante](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) e especifique o script a ser usado.

## Lidar com pacotes de fluxo de trabalho {#handling-workflow-packages}

[Pacotes de fluxo de trabalho](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) podem ser passados para um fluxo de trabalho para processamento. Os pacotes de fluxo de trabalho contêm referências a recursos como páginas e ativos.

>[!NOTE]
>
>As seguintes etapas do processo de fluxo de trabalho aceitam pacotes de fluxo de trabalho para ativação de página em massa:
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)
>

Você pode desenvolver etapas de fluxo de trabalho que obtêm os recursos do pacote e os processam. Os seguintes membros do pacote `com.day.cq.workflow.collection` fornecem acesso aos pacotes de fluxo de trabalho:

* `ResourceCollection`: classe do pacote de fluxo de trabalho.
* `ResourceCollectionUtil`: use para recuperar objetos ResourceCollection.
* `ResourceCollectionManager`: cria e recupera coleções. Uma implementação é implantada como um serviço OSGi.

O exemplo de classe Java a seguir demonstra como obter recursos de pacote:

```java
package com.adobe.example;

import java.util.ArrayList;
import java.util.List;

import com.day.cq.workflow.WorkflowException;
import com.day.cq.workflow.WorkflowSession;
import com.day.cq.workflow.collection.ResourceCollection;
import com.day.cq.workflow.collection.ResourceCollectionManager;
import com.day.cq.workflow.collection.ResourceCollectionUtil;
import com.day.cq.workflow.exec.WorkItem;
import com.day.cq.workflow.exec.WorkflowData;
import com.day.cq.workflow.exec.WorkflowProcess;
import com.day.cq.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.osgi.framework.Constants;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Node;
import javax.jcr.PathNotFoundException;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

@Component
@Service
public class LaunchBulkActivate implements WorkflowProcess {

 private static final Logger log = LoggerFactory.getLogger(LaunchBulkActivate.class);

 @Property(value="Bulk Activate for Launches")
  static final String PROCESS_NAME ="process.label";
 @Property(value="A sample workflow process step to support Launches bulk activation of pages")
 static final String SERVICE_DESCRIPTION = Constants.SERVICE_DESCRIPTION;

 @Reference
 private ResourceCollectionManager rcManager;
public void execute(WorkItem workItem, WorkflowSession workflowSession) throws Exception {
    Session session = workflowSession.getSession();
    WorkflowData data = workItem.getWorkflowData();
    String path = null;
    String type = data.getPayloadType();
    if (type.equals(TYPE_JCR_PATH) && data.getPayload() != null) {
        String payloadData = (String) data.getPayload();
        if (session.itemExists(payloadData)) {
            path = payloadData;
        }
    } else if (data.getPayload() != null && type.equals(TYPE_JCR_UUID)) {
        Node node = session.getNodeByUUID((String) data.getPayload());
        path = node.getPath();
    }

    // CUSTOMIZED CODE IF REQUIRED....

    if (path != null) {
        // check for resource collection
        ResourceCollection rcCollection = ResourceCollectionUtil.getResourceCollection((Node)session.getItem(path), rcManager);
        // get list of paths to replicate (no resource collection: size == 1
        // otherwise size >= 1
        List<String> paths = getPaths(path, rcCollection);
        for (String aPath: paths) {

            // CUSTOMIZED CODE....

        }
    } else {
        log.warn("Cannot process because path is null for this " + "workitem: " + workItem.toString());
    }
}

/**
 * helper
 */
private List<String> getPaths(String path, ResourceCollection rcCollection) {
    List<String> paths = new ArrayList<String>();
    if (rcCollection == null) {
        paths.add(path);
    } else {
        log.debug("ResourceCollection detected " + rcCollection.getPath());
        // this is a resource collection. the collection itself is not
        // replicated. only its members
        try {
            List<Node> members = rcCollection.list(new String[]{"cq:Page", "dam:Asset"});
            for (Node member: members) {
                String mPath = member.getPath();
                paths.add(mPath);
            }
        } catch(RepositoryException re) {
            log.error("Cannot build path list out of the resource collection " + rcCollection.getPath());
        }
    }
    return paths;
}
}
```

## Exemplo: Criação de uma etapa personalizada {#example-creating-a-custom-step}

Uma maneira fácil de começar a criar sua própria etapa personalizada é copiar uma etapa existente do:

`/libs/cq/workflow/components/model`

### Criação da etapa básica {#creating-the-basic-step}

1. Recrie o caminho em /apps; por exemplo:

   `/apps/cq/workflow/components/model`

   As novas pastas são do tipo `nt:folder`:

   ```xml
   - apps
     - cq
       - workflow (nt:folder)
         - components (nt:folder)
           - model (nt:folder)
   ```

   >[!NOTE]
   >
   >Esta etapa não se aplica ao editor de modelo de interface clássica.

1. Em seguida, coloque a etapa copiada na pasta /apps; por exemplo, como:

   `/apps/cq/workflow/components/model/myCustomStep`

   Este é o resultado de nosso exemplo de etapa personalizada:

   ![wf-34](assets/wf-34.png)

   >[!CAUTION]
   >
   >Como na interface do usuário padrão, somente o título e não os detalhes não são exibidos no cartão, `details.jsp` não é necessário, pois era para o editor de interface do usuário clássico.

1. Aplique as seguintes propriedades ao nó:

   `/apps/cq/workflow/components/model/myCustomStep`

   **Propriedades de interesse:**

   * `sling:resourceSuperType`

     Deve herdar de uma etapa existente.

     Neste exemplo, estamos herdando da etapa base em `cq/workflow/components/model/step`, mas você pode usar outros supertipos como `participant`, `process` e assim por diante.

   * `jcr:title`

     É o título exibido quando o componente é listado no navegador de etapas (painel lateral esquerdo do editor de modelo de fluxo de trabalho).

   * `cq:icon`

     Usado para especificar um [ícone Coral](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) para a etapa.

   * `componentGroup`

     Deve ser um dos seguintes:

      * Fluxo de trabalho de colaboração
      * Fluxo de trabalho DAM
      * Fluxo de trabalho dos formulários
      * Projetos
      * WCM fluxo de trabalho
      * Fluxo de trabalho

   ![wf-35](assets/wf-35.png)

1. Agora é possível abrir um modelo de fluxo de trabalho para edição. No navegador de etapas, você pode filtrar para ver **Minha Etapa Personalizada**:

   ![wf-36](assets/wf-36.png)

   Arrastar **Minha etapa personalizada** para o modelo exibe o cartão:

   ![wf-37](assets/wf-37.png)

   Se nenhum `cq:icon` tiver sido definido para a etapa, um ícone padrão será renderizado usando as duas primeiras letras do título. Por exemplo:

   ![wf-38](assets/wf-38.png)

#### Definir a caixa de diálogo Configurar etapa {#defining-the-step-configure-dialog}

Depois de [Criar a Etapa Básica](#creating-the-basic-step), defina a caixa de diálogo **Configurar** da seguinte maneira:

1. Configure as propriedades no nó `cq:editConfig` da seguinte maneira:

   **Propriedades de interesse:**

   * `cq:inherit`

     Quando definido como `true`, seu componente de etapa herdará propriedades da etapa especificada em `sling:resourceSuperType`.

   * `cq:disableTargeting`

     Defina conforme necessário.

   ![wf-39](assets/wf-39.png)

1. Configure as propriedades no nó `cq:formsParameter` da seguinte maneira:

   **Propriedades de interesse:**

   * `jcr:title`

     Define o título padrão no cartão de etapas no mapa de modelos e no campo **Título** da caixa de diálogo de configuração **Meu Personalizado - Propriedades da Etapa**.

   * Você também pode definir suas próprias propriedades personalizadas.

   ![wf-40](assets/wf-40.png)

1. Configure as propriedades no nó `cq:listeners`.

   O nó `cq:listener` e suas propriedades permitem definir manipuladores de eventos que reagem a eventos no editor de modelo de interface habilitada para toque; como arrastar uma etapa para uma página de modelo ou editar propriedades de uma etapa.

   **Propriedades de interesse:**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`

   Essa configuração é essencial para o funcionamento adequado do editor. Na maioria dos casos, essa configuração não deve ser alterada.

   No entanto, definir `cq:inherit` como verdadeiro (no nó `cq:editConfig`, veja acima) permite que você herde essa configuração, sem precisar incluí-la explicitamente na definição da etapa. Se nenhuma herança estiver em vigor, será necessário adicionar esse nó com as seguintes propriedades e valores.

   Neste exemplo, a herança foi ativada para que pudéssemos remover o nó `cq:listeners` e a etapa ainda funcionará corretamente.

   ![wf-41](assets/wf-41.png)

1. Agora é possível adicionar uma instância da etapa a um modelo de fluxo de trabalho. Quando você **Configurar** a etapa, verá a caixa de diálogo:

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### Exemplo de marcação usada neste exemplo {#sample-markup-used-in-this-example}

A marcação para uma etapa personalizada será representada no `.content.xml` do nó raiz do componente. A amostra `.content.xml` usada para este exemplo:

`/apps/cq/workflow/components/model/myCustomStep/.content.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:icon="bell"
    jcr:primaryType="cq:Component"
    jcr:title="My Custom Step"
    sling:resourceSuperType="cq/workflow/components/model/process"
    allowedParents="[*/parsys]"
    componentGroup="Workflow"/>
```

A amostra `_cq_editConfig.xml` usada neste exemplo:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:disableTargeting="{Boolean}true"
    cq:inherit="{Boolean}true"
    jcr:primaryType="cq:EditConfig">
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        jcr:title="My Custom Step Card"
        SAMPLE_PROPERY="sample value"/>
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="CQ.workflow.flow.Step.afterDelete"
        afteredit="CQ.workflow.flow.Step.afterEdit"
        afterinsert="CQ.workflow.flow.Step.afterInsert"
        afterMove="REFRESH_PAGE"/>
</jcr:root>
```

A amostra `_cq_dialog/.content.xml` usada neste exemplo:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    jcr:title="My Custom - Step Properties"
    sling:resourceType="cq/gui/components/authoring/dialog">
    <content
        jcr:primaryType="nt:unstructured"
        sling:resourceType="granite/ui/components/coral/foundation/tabs">
        <items jcr:primaryType="nt:unstructured">
            <common
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <process
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Process"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <mycommon
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <title
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                fieldLabel="Title"
                                name="./jcr:title"/>
                            <description
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textarea"
                                fieldLabel="Description"
                                name="./jcr:description"/>
                        </items>
                    </columns>
                </items>
            </mycommon>
            <advanced
                jcr:primaryType="nt:unstructured"
                jcr:title="Advanced"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <email
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/checkbox"
                                fieldDescription="Notify user via email."
                                fieldLabel="Email"
                                name="./metaData/PROCESS_AUTO_ADVANCE"
                                text="Notify user via email."
                                value="true"/>
                        </items>
                    </columns>
                </items>
            </advanced>
        </items>
    </content>
</jcr:root>
```

>[!NOTE]
>
>Observe os nós comum e de processo na definição da caixa de diálogo. Eles são herdados da etapa do processo que usamos como supertipo para nossa etapa personalizada:
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>As caixas de diálogo do editor de modelo de interface clássica ainda funcionarão com o editor de interface habilitado para toque padrão.
>
>Embora o AEM tenha [ferramentas de modernização](/help/sites-developing/modernization-tools.md), se você quiser atualizar as caixas de diálogo de etapa da interface clássica para as caixas de diálogo da interface padrão. Após a conversão, ainda há algumas melhorias manuais que podem ser feitas na caixa de diálogo para determinados casos.
>
>* Nos casos em que uma caixa de diálogo atualizada está vazia, você pode ver caixas de diálogo no `/libs` que tenham funcionalidade semelhante a exemplos de como fornecer uma solução. Por exemplo:
>
>* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`
>
>  Não edite nada em `/libs`, apenas use-os como exemplos. Se quiser usar qualquer uma das etapas existentes, copie-as para `/apps` e edite-as lá.
