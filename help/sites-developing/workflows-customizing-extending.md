---
title: Ampliação da funcionalidade do fluxo de trabalho
seo-title: Extending Workflow Functionality
description: Ampliação da funcionalidade do fluxo de trabalho
seo-description: null
uuid: 9f4ea2a8-8b21-4e7c-ac73-dd37d9ada111
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f23408c3-6b37-4047-9cce-0cab97bb6c5c
exl-id: 9e205912-50a6-414a-b8d4-a0865269d0e0
source-git-commit: 13f15bee38b6b4af4cd59376849810a788f0c467
workflow-type: tm+mt
source-wordcount: '3583'
ht-degree: 2%

---

# Ampliação da funcionalidade do fluxo de trabalho{#extending-workflow-functionality}

Este tópico descreve como desenvolver componentes de etapa personalizados para seus fluxos de trabalho e, em seguida, como interagir programaticamente com fluxos de trabalho.

A criação de uma etapa de fluxo de trabalho personalizada envolve as seguintes atividades:

* Desenvolva o componente de etapa do fluxo de trabalho.
* Implemente a funcionalidade da etapa como um serviço OSGi ou um script ECMA.

Você também pode [interagir com seus workflows a partir de seus programas e scripts](/help/sites-developing/workflows-program-interaction.md).

## Componentes da etapa do fluxo de trabalho - Noções básicas {#workflow-step-components-the-basics}

Um componente de etapa do fluxo de trabalho define a aparência e o comportamento da etapa ao criar modelos de fluxo de trabalho:

* A categoria e o nome da etapa no sidekick do fluxo de trabalho.
* A aparência da etapa em modelos de fluxo de trabalho.
* A caixa de diálogo Editar para configurar as propriedades do componente.
* O serviço ou script que é executado em tempo de execução.

Como com [todos os componentes](/help/sites-developing/components.md), os componentes da etapa do fluxo de trabalho herdam do componente especificado para o `sling:resourceSuperType` propriedade. O diagrama a seguir mostra a hierarquia de `cq:component` nós que formam a base de todos os componentes de etapa do fluxo de trabalho. O diagrama também inclui a variável **Etapa do processo**, **Etapa do participante** e **Etapa dinâmica do participante** componentes, pois esses são os pontos de partida mais comuns (e básicos) para o desenvolvimento de componentes de etapa personalizados.

![aem_wf_componentherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>Você ***must*** não altere nada no `/libs` caminho.
>
>Isso ocorre porque o conteúdo da variável `/libs` O é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recrie o item necessário (ou seja, como ele existe em `/libs` under `/apps`
>2. Faça quaisquer alterações no `/apps`


O `/libs/cq/workflow/components/model/step` é o ancestral comum mais próximo da **Etapa do processo**, **Etapa do participante** e **Etapa dinâmica do participante**, que herdam os seguintes itens:

* `step.jsp`

   O `step.jsp` script renderiza o título do componente da etapa quando ele é adicionado a um modelo.

   ![wf-22-1](assets/wf-22-1.png)

* [cq:dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

   Uma caixa de diálogo com as seguintes guias:

   * **Frequentes**: para editar o título e a descrição.
   * **Avançado**: para editar as propriedades de notificação de email.

   ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

   >[!NOTE]
   >
   >Quando as guias da caixa de diálogo de edição de um componente de etapa não correspondem a essa aparência padrão, o componente de etapa tem scripts definidos, propriedades de nó ou guias de diálogo que substituem essas guias herdadas.

### Scripts ECMA {#ecma-scripts}

Os seguintes objetos estão disponíveis (dependendo do tipo de etapa) nos scripts ECMA:

* [WorkItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) workItem
* [WorkflowSession](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) workflowSession
* [WorkflowData](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) workflowData
* `args`: com os argumentos do processo.

* `sling`: para acessar outros serviços osgi.
* `jcrSession`

### MetaDataMaps {#metadatamaps}

Você pode usar metadados de workflow para manter as informações necessárias durante a vida útil do workflow. Um requisito comum de etapas do fluxo de trabalho é a persistência de dados para uso futuro no fluxo de trabalho ou a recuperação dos dados persistentes.

Existem três tipos de objetos MetaDataMap - para `Workflow`, `WorkflowData` e `WorkItem` objetos. Todos têm o mesmo objetivo pretendido - armazenar metadados.

Um WorkItem tem seu próprio MetaDataMap que só pode ser usado enquanto esse item de trabalho (por exemplo, etapa) está em execução.

Ambos `Workflow` e `WorkflowData` os metadados são compartilhados em todo o fluxo de trabalho. Nesses casos, é recomendável usar somente a variável `WorkflowData` mapa de metadados.

## Criação de componentes de etapa de fluxo de trabalho personalizados {#creating-custom-workflow-step-components}

Os componentes da etapa do fluxo de trabalho podem ser [criado da mesma forma que qualquer outro componente](/help/sites-developing/components.md).

Para herdar de um dos componentes da etapa base (existente), adicione a seguinte propriedade ao `cq:Component` nó:

* Nome: `sling:resourceSuperType`
* Tipo: `String`
* Valor: Um dos seguintes caminhos que são resolvidos para um componente básico:

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### Especificação do título e da descrição padrão para instâncias de etapa {#specifying-the-default-title-and-description-for-step-instances}

Use o procedimento a seguir para especificar valores padrão para a variável **Título** e **Descrição** nos campos **Frequentes** guia .

>[!NOTE]
>
>Os valores de campo aparecem na instância da etapa quando ambos os requisitos a seguir são cumpridos:
>
>* A caixa de diálogo de edição da etapa armazena o título e a descrição nos seguintes locais: >
>* `./jcr:title`
>* `./jcr:description` locais
>
>  Esse requisito é atendido quando a caixa de diálogo de edição usa a guia Comum de que a variável `/libs/cq/flow/components/step/step` implementações de componente.
>
>* O componente de etapa ou um ancestral do componente não substitui o `step.jsp` script que `/libs/cq/flow/components/step/step` implementações de componente.


1. Abaixo do `cq:Component` , adicione o seguinte nó:

   * Nome: `cq:editConfig`
   * Tipo: `cq:EditConfig`

   >[!NOTE]
   >
   >Para obter mais informações sobre o nó cq:editConfig , consulte [Configurar o comportamento de edição de um componente](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. Abaixo do `cq:EditConfig` , adicione o seguinte nó:

   * Nome: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Adicionar `String` propriedades dos seguintes nomes para a `cq:formParameters` nó:

   * `jcr:title`: O valor preenche a variável **Título** do **Frequentes** guia .
   * `jcr:description`: O valor preenche a variável **Descrição** do **Frequentes** guia .

### Salvar valores de propriedade nos metadados do fluxo de trabalho {#saving-property-values-in-workflow-metadata}

>[!NOTE]
>
>Consulte [Persistência e acesso a dados](#persisting-and-accessing-data). Especificamente, para obter informações sobre como acessar o valor da propriedade no tempo de execução, consulte [Acessar valores de propriedade da caixa de diálogo no tempo de execução](#accessing-dialog-property-values-at-runtime).

A propriedade name de `cq:Widget` itens especifica o nó JCR que armazena o valor do widget. Quando os widgets na caixa de diálogo dos componentes da etapa do fluxo de trabalho armazenam valores abaixo de `./metaData` , o valor é adicionado ao workflow `MetaDataMap`.

Por exemplo, um campo de texto em uma caixa de diálogo é um `cq:Widget` nó que tem as seguintes propriedades:

| Nome | Tipo | Valor |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

O valor especificado nesse campo de texto é adicionado ao da instância do fluxo de trabalho ` [MetaDataMap](#metadatamaps)` e está associado à variável `subject` chave.

>[!NOTE]
>
>Quando a tecla `PROCESS_ARGS`, o valor está prontamente disponível nas implementações do script ECMA por meio do `args` variável. Nesse caso, o valor da propriedade name é `./metaData/PROCESS_ARGS.`

### Substituição da implementação da etapa {#overriding-the-step-implementation}

Cada componente básico de etapa permite que os desenvolvedores do modelo de fluxo de trabalho configurem os seguintes recursos principais no momento do design:

* Etapa do processo: O serviço ou script ECMA a ser executado no tempo de execução.
* Etapa do participante: A ID do usuário que recebe o item de trabalho gerado.
* Etapa dinâmica do participante: O serviço ou script ECMA que seleciona a ID do usuário que recebe o item de trabalho.

Para focalizar o componente para uso em um cenário de fluxo de trabalho específico, configure o recurso principal no design e remova a capacidade dos desenvolvedores de modelo alterá-lo.

1. Abaixo do nó cq:component , adicione o seguinte nó:

   * Nome: `cq:editConfig`
   * Tipo: `cq:EditConfig`

   Para obter mais informações sobre o nó cq:editConfig , consulte [Configurar o comportamento de edição de um componente](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. Abaixo do nó cq:EditConfig , adicione o seguinte nó:

   * Nome: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Adicione um `String` para a `cq:formParameters` nó . O supertipo de componente determina o nome da propriedade:

   * Etapa do processo: `PROCESS`
   * Etapa do participante: `PARTICIPANT`
   * Etapa dinâmica do participante: `DYNAMIC_PARTICIPANT`

1. Especifique o valor da propriedade:

   * `PROCESS`: O caminho para o script ECMA ou o PID do serviço que implementa o comportamento da etapa.
   * `PARTICIPANT`: A ID do usuário que recebe o item de trabalho.
   * `DYNAMIC_PARTICIPANT`: O caminho para o script ECMA ou o PID do serviço que seleciona o usuário para atribuir o item de trabalho.

1. Para remover a capacidade dos desenvolvedores de modelo de alterarem seus valores de propriedade, substitua a caixa de diálogo do supertipo de componente.

### Adicionar Forms e caixas de diálogo às etapas do participante {#adding-forms-and-dialogs-to-participant-steps}

Personalize o componente da etapa do participante para fornecer os recursos encontrados no [Etapa do participante do formulário](/help/sites-developing/workflows-step-ref.md#form-participant-step) e [Etapa da caixa de diálogo do participante](/help/sites-developing/workflows-step-ref.md#dialog-participant-step) componentes:

* Apresentar um formulário ao usuário quando ele abrir o item de trabalho gerado.
* Apresentar uma caixa de diálogo personalizada ao usuário quando ele concluir o item de trabalho gerado.

Execute o procedimento a seguir no novo componente (consulte [Criação de componentes de etapa de fluxo de trabalho personalizados](#creating-custom-workflow-step-components)):

1. Abaixo do `cq:Component` , adicione o seguinte nó:

   * Nome: `cq:editConfig`
   * Tipo: `cq:EditConfig`

   Para obter mais informações sobre o nó cq:editConfig , consulte [Configurar o comportamento de edição de um componente](/help/sites-developing/components-basics.md#edit-behavior).

1. Abaixo do nó cq:EditConfig , adicione o seguinte nó:

   * Nome: `cq:formParameters`
   * Tipo: `nt:unstructured`

1. Para apresentar um formulário quando o usuário abrir o item de trabalho, adicione a seguinte propriedade ao `cq:formParameters` nó:

   * Nome: `FORM_PATH`
   * Tipo: `String`
   * Valor: O caminho que é resolvido para o formulário

1. Para apresentar uma caixa de diálogo personalizada quando o usuário concluir o item de trabalho, adicione a seguinte propriedade ao `cq:formParameters` nó

   * Nome: `DIALOG_PATH`
   * Tipo: `String`
   * Valor: O caminho que resolve a caixa de diálogo

### Configurar o comportamento do tempo de execução da etapa do fluxo de trabalho {#configuring-the-workflow-step-runtime-behavior}

Abaixo do `cq:Component` nó , adicione um `cq:EditConfig` nó . Abaixo que adiciona uma `nt:unstructured` nó (deve ser nomeado `cq:formParameters`) e, nesse nó, adicione as seguintes propriedades:

* Nome: `PROCESS_AUTO_ADVANCE`

   * Tipo: `Boolean`
   * Valor:

      * quando definido como `true` o fluxo de trabalho executará essa etapa e continuará - isso é padrão e também recomendado
      * when `false`, o fluxo de trabalho será executado e interrompido; isso precisa de um tratamento extra, portanto `true` é recomendado

* Nome: `DO_NOTIFY`

   * Tipo: `Boolean`
   * Valor: indica se as notificações por email devem ser enviadas para etapas de participação do usuário (e assume que o servidor de email está configurado corretamente)

## Persistência e acesso a dados {#persisting-and-accessing-data}

### Dados Persistentes para Etapas Subsequentes do Fluxo de Trabalho {#persisting-data-for-subsequent-workflow-steps}

Você pode usar metadados de workflow para manter as informações necessárias durante a vida útil do workflow - e entre etapas. Um requisito comum de etapas do fluxo de trabalho é a persistência de dados para uso futuro ou a recuperação dos dados persistentes de etapas anteriores.

Os metadados do fluxo de trabalho são armazenados em um [`MetaDataMap`](#metadatamaps) objeto. A API do Java fornece a variável [`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html) método para retornar um [`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) que fornece o `MetaDataMap` objeto. Essa `WorkflowData` `MetaDataMap` O objeto está disponível para o serviço OSGi ou o script ECMA de um componente de etapa.

#### Java {#java}

O método execute do `WorkflowProcess` a implementação é aprovada `WorkItem` objeto. Use esse objeto para obter a variável `WorkflowData` objeto para a instância de fluxo de trabalho atual. O exemplo a seguir adiciona um item ao workflow `MetaDataMap` e, em seguida, registra cada item. O item (&quot;mykey&quot;, &quot;My Step Value&quot;) está disponível para as etapas subsequentes no fluxo de trabalho.

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

O `graniteWorkItem` é a representação do script ECMA da variável atual `WorkItem` Objeto Java. Portanto, você pode usar a variável `graniteWorkItem` para obter os metadados do workflow. O script ECMA a seguir pode ser usado para implementar um **Etapa do processo** para adicionar um item ao fluxo de trabalho `MetaDataMap` e, em seguida, registre cada item. Esses itens ficam disponíveis para as etapas subsequentes no fluxo de trabalho.

>[!NOTE]
>
>O `metaData` que está imediatamente disponível para o script da etapa são os metadados da etapa. Os metadados da etapa são diferentes dos metadados do fluxo de trabalho.

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

### Acessar valores de propriedade da caixa de diálogo no tempo de execução {#accessing-dialog-property-values-at-runtime}

O `MetaDataMap` O objeto de instâncias de fluxo de trabalho é útil para armazenar e recuperar dados durante toda a vida do fluxo de trabalho. Para implementações de componentes de etapa do fluxo de trabalho, a variável `MetaDataMap` é útil para recuperar valores de propriedade de componente no tempo de execução.

>[!NOTE]
>
>Para obter informações sobre como configurar a caixa de diálogo do componente para armazenar propriedades como metadados de fluxo de trabalho, consulte [Salvar valores de propriedade nos metadados do fluxo de trabalho](#saving-property-values-in-workflow-metadata).

O fluxo de trabalho `MetaDataMap` O está disponível para implementações de processos de script Java e ECMA:

* Em implementações Java da interface WorkflowProcess , a variável `args` é o parâmetro `MetaDataMap` para o fluxo de trabalho.

* Em implementações de script ECMA, o valor está disponível usando a variável `args` e `metadata` variáveis.

### Exemplo: Recuperação dos Argumentos do Componente Etapa do Processo {#example-retrieving-the-arguments-of-the-process-step-component}

A caixa de diálogo Editar da **Etapa do processo** inclui o **Argumentos** propriedade. O valor da variável **Argumentos** é armazenada nos metadados do fluxo de trabalho e está associada à variável `PROCESS_ARGS` chave.

No diagrama a seguir, o valor da variável **Argumentos** a propriedade é `argument1, argument2`:

![wf-24](assets/wf-24.png)

#### Java {#java-1}

O código Java a seguir é o `execute` método para um `WorkflowProcess` implementação. O método registra o valor na variável `args` `MetaDataMap` que está associada ao `PROCESS_ARGS` chave.

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

Quando uma etapa do processo que usa essa implementação do Java é executada, o log contém a seguinte entrada:

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### Script ECMA {#ecma-script-1}

O script ECMA a seguir é usado como o processo para o **Etapa do processo**. Ele registra o número de argumentos e os valores do argumento:

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
>Esta seção descreve como trabalhar com argumentos para etapas do processo. A informação também se aplica a choosers dinâmicos para participantes.

>[!NOTE]
>Para obter outro exemplo de armazenamento de propriedades do componente em metadados do fluxo de trabalho, consulte Exemplo: Criar uma etapa do fluxo de trabalho do logger. Este exemplo apresenta uma caixa de diálogo que associa o valor de metadados a uma chave diferente de PROCESS_ARGS.

### Scripts e Argumentos de Processo {#scripts-and-process-arguments}

Dentro de um script para um **Etapa do processo** , os argumentos estão disponíveis por meio do `args` objeto.

Ao criar um componente de etapa personalizado, o objeto `metaData` está disponível em um script. Esse objeto é limitado a um único argumento de string.

## Implementações em etapas do processo de desenvolvimento {#developing-process-step-implementations}

Quando as etapas do processo são iniciadas durante o processo de um workflow, as etapas enviam uma solicitação para um serviço OSGi ou executam um script ECMA. Desenvolva o serviço ou o script ECMA que executa as ações necessárias ao seu fluxo de trabalho.

>[!NOTE]
>
>Para obter informações sobre como associar o componente Etapa do processo ao serviço ou script, consulte [Etapa do processo](/help/sites-developing/workflows-step-ref.md#process-step) ou [Substituição da implementação da etapa](#overriding-the-step-implementation).

### Implementar uma etapa do processo com uma classe Java {#implementing-a-process-step-with-a-java-class}

Para definir uma etapa do processo como um componente de serviço OSGI (pacote Java):

1. Crie o pacote e implante-o no contêiner OSGI. Consulte a documentação sobre como criar um pacote com [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) ou [Eclipse](/help/sites-developing/howto-projects-eclipse.md).

   >[!NOTE]
   >
   >O componente OSGI precisa implementar o `WorkflowProcess` com sua `execute()` método . Consulte o código de exemplo abaixo.

   >[!NOTE]
   >
   >O nome do pacote precisa ser adicionado ao `<*Private-Package*>` da seção `maven-bundle-plugin` configuração.

1. Adicionar a propriedade SCR `process.label`  e defina o valor conforme necessário. Esse será o nome que sua etapa do processo será listada ao usar o **Etapa do processo** componente. Veja o exemplo abaixo.
1. No **Modelos** , adicione a etapa do processo ao workflow usando o **Etapa do processo** componente.
1. Na caixa de diálogo de edição (do **Etapa do processo**), acesse o **Processo** e selecione a implementação do processo.
1. Se você usar argumentos em seu código, defina a variável **Argumentos do processo**. Por exemplo: falso.
1. Salve as alterações, tanto para a etapa quanto para o modelo de fluxo de trabalho (canto superior esquerdo do editor de modelo).

Os métodos java, respectivamente, as classes que implementam o método Java executável são registradas como serviços OSGI, permitindo que você adicione métodos a qualquer momento durante o tempo de execução.

O componente OSGI a seguir adiciona a propriedade `approved` para o nó de conteúdo da página quando a carga for uma página:

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
>Se o processo falhar três vezes seguidas, um item é colocado na Caixa de entrada do administrador do fluxo de trabalho.

### Uso de ECMAScript {#using-ecmascript}

Os scripts ECMA permitem que os desenvolvedores de script implementem as etapas do processo. Os scripts estão localizados no repositório JCR e são executados a partir daí.

A tabela a seguir lista as variáveis imediatamente disponíveis para processar scripts, fornecendo acesso a objetos da API Java do workflow.

| Classe Java | Nome da variável de script | Descrição |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | A instância da etapa atual. |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | A sessão de fluxo de trabalho da instância da etapa atual. |
| `String[]` (contém argumentos de processo) | `args` | Os argumentos da etapa. |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | Os metadados da instância da etapa atual. |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | Fornece acesso ao ambiente de tempo de execução do Sling. |

O script de exemplo a seguir demonstra como acessar o nó JCR que representa a carga do fluxo de trabalho. O `graniteWorkflowSession` é adaptada a uma variável de sessão JCR, que é usada para obter o nó do caminho de carga.

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

O script a seguir verifica se a carga é uma imagem ( `.png` arquivo ), cria uma imagem em preto-e-branco a partir dela e a salva como um nó irmão.

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

1. Crie o script (por exemplo, com o CRXDE Lite) e salve-o no repositório abaixo `//apps/workflow/scripts/`
1. Especificação de um título que identifique o script no **Etapa do processo** editar , adicione as seguintes propriedades ao `jcr:content` nó do script:

   | Nome | Tipo | Valor |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | O nome a ser exibido na caixa de diálogo de edição. |

1. Edite o **Etapa do processo** e especifique o script a ser usado.

## Desenvolvendo seletores de participantes {#developing-participant-choosers}

Você pode desenvolver seletores de participantes para **Etapa dinâmica do participante** componentes.

Quando uma **Etapa dinâmica do participante** for iniciado durante um fluxo de trabalho, a etapa precisa determinar o participante ao qual o item de trabalho gerado pode ser atribuído. Para fazer isso, siga um destes procedimentos:

* envia uma solicitação para um serviço OSGi
* executa um ECMA script para selecionar o participante

Você pode desenvolver um serviço ou um ECMA script que selecione o participante de acordo com os requisitos do seu fluxo de trabalho.

>[!NOTE]
>
>Para obter informações sobre como associar **Etapa dinâmica do participante** com o serviço ou script, consulte [Etapa dinâmica do participante](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) ou [Substituição da implementação da etapa](#persisting-and-accessing-data).

### Desenvolvimento de um seletor de participante usando uma classe Java {#developing-a-participant-chooser-using-a-java-class}

Para definir uma etapa do participante como um componente de serviço OSGI (classe Java):

1. O componente OSGI precisa implementar o `ParticipantStepChooser` com sua `getParticipant()` método . Consulte o código de exemplo abaixo.

   Crie o pacote e implante-o no contêiner OSGI.

1. Adicionar a propriedade SCR `chooser.label` e defina o valor conforme necessário. Esse será o nome listado no seletor de participantes, usando a variável **Etapa dinâmica do participante** componente. Veja o exemplo:

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

1. No **Modelos** , adicione a etapa do participante dinâmico ao fluxo de trabalho usando o **Etapa dinâmica do participante** componente.
1. Na caixa de diálogo de edição, selecione o **Seletor de participante** e selecione a implementação do seletor.
1. Se você usar argumentos em seu código, defina a variável **Argumentos do processo**. Neste exemplo: `/content/we-retail/de`.
1. Salve as alterações, tanto para a etapa quanto para o modelo de fluxo de trabalho.

### Desenvolvimento de um seletor de participante usando um script ECMA {#developing-a-participant-chooser-using-an-ecma-script}

Você pode criar um script ECMA que selecione o usuário que recebe o item de trabalho que a **Etapa do participante** gera. O script deve incluir uma função chamada `getParticipant` que não requer argumentos e retorna um `String` que contém a ID de um usuário ou grupo.

Os scripts estão localizados no repositório JCR e são executados a partir daí.

A tabela a seguir lista as variáveis que fornecem acesso imediato a objetos Java de fluxo de trabalho em seus scripts.

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

1. Crie o script (por exemplo, com o CRXDE Lite) e salve-o no repositório abaixo `//apps/workflow/scripts`
1. Especificação de um título que identifique o script no **Etapa do processo** editar , adicione as seguintes propriedades ao `jcr:content` nó do script:

   | Nome | Tipo | Valor |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | O nome a ser exibido na caixa de diálogo de edição. |

1. Edite o [Etapa dinâmica do participante](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) e especifique o script a ser usado.

## Manuseio de pacotes de fluxo de trabalho {#handling-workflow-packages}

[Pacotes de workflow](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) pode ser passado para um workflow para processamento. Os pacotes de fluxo de trabalho contêm referências a recursos como páginas e ativos.

>[!NOTE]
>
>As etapas do processo de fluxo de trabalho a seguir aceitam pacotes de fluxo de trabalho para ativação de página em massa:
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)
>


Você pode desenvolver etapas de fluxo de trabalho que obtêm os recursos do pacote e processá-los. Os seguintes membros da `com.day.cq.workflow.collection` O pacote fornece acesso aos pacotes de fluxo de trabalho:

* `ResourceCollection`: Classe de pacote de fluxo de trabalho.
* `ResourceCollectionUtil`: Use para recuperar objetos ResourceCollection.
* `ResourceCollectionManager`: Cria e recupera coleções. Uma implementação é implantada como um serviço OSGi.

O exemplo de classe Java a seguir demonstra como obter recursos do pacote:

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

Uma maneira fácil de começar a criar sua própria etapa personalizada é copiar uma etapa existente de:

`/libs/cq/workflow/components/model`

### Criando a etapa básica {#creating-the-basic-step}

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

   Este é o resultado do nosso exemplo de etapa personalizada:

   ![wf-34](assets/wf-34.png)

   >[!CAUTION]
   >
   >Como na interface de usuário padrão, somente o título e não os detalhes não são exibidos no cartão, `details.jsp` não é necessária, pois era para o editor de interface clássica.

1. Aplique as seguintes propriedades ao nó :

   `/apps/cq/workflow/components/model/myCustomStep`

   **Propriedades de interesse:**

   * `sling:resourceSuperType`

      Deve herdar de uma etapa existente.

      Neste exemplo, estamos herdando da etapa base em `cq/workflow/components/model/step`, mas você pode usar outros supertipos como `participant`, `process`, etc.

   * `jcr:title`

      É o título exibido quando o componente é listado no navegador de etapas (painel do lado esquerdo do editor de modelo de fluxo de trabalho).

   * `cq:icon`

      Usado para especificar uma [Ícone Coral](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) para a etapa .

   * `componentGroup`

      Deve ser um dos seguintes:

      * Fluxo de trabalho de colaboração
      * Fluxo de trabalho DAM
      * Fluxo de trabalho dos formulários
      * Projetos
      * Fluxo de trabalho WCM
      * Fluxo de trabalho

   ![wf-35](assets/wf-35.png)

1. Agora é possível abrir um modelo de fluxo de trabalho para edição. No navegador de etapas, você pode filtrar para ver **Minha etapa personalizada**:

   ![wf-36](assets/wf-36.png)

   Arrastar **Minha etapa personalizada** no modelo, o exibe o cartão :

   ![wf-37](assets/wf-37.png)

   Se não `cq:icon` tiver sido definido para a etapa, um ícone padrão será renderizado usando as duas primeiras letras do título. Por exemplo:

   ![wf-38](assets/wf-38.png)

#### Definir a caixa de diálogo Configurar etapa {#defining-the-step-configure-dialog}

Depois [Criando a etapa básica](#creating-the-basic-step), defina a etapa **Configurar** como segue:

1. Configure as propriedades no nó `cq:editConfig` como se segue:

   **Propriedades de interesse:**

   * `cq:inherit`

      Quando definido como `true`, o componente da etapa herdará as propriedades da etapa especificada em `sling:resourceSuperType`.

   * `cq:disableTargeting`

      Defina como necessário.
   ![wf-39](assets/wf-39.png)

1. Configure as propriedades no nó `cq:formsParameter` como se segue:

   **Propriedades de interesse:**

   * `jcr:title`

      Define o título padrão no cartão de etapas no mapa de modelo e no **Título** do **Meu personalizado - Propriedades da etapa** caixa de diálogo de configuração.

   * Também é possível definir suas próprias propriedades personalizadas.

   ![wf-40](assets/wf-40.png)

1. Configure as propriedades no nó `cq:listeners`.

   O `cq:listener` O nó e suas propriedades permitem definir manipuladores de eventos que reagem a eventos no editor de modelo de interface do usuário habilitado para toque; como arrastar uma etapa para uma página de modelo ou editar uma propriedade de etapa.

   **Propriedades de interesse:**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`

   Essa configuração é essencial para o funcionamento correto do editor. Na maioria dos casos, essa configuração não deve ser alterada.

   No entanto, defina `cq:inherit` como true (no `cq:editConfig` , veja acima) permite herdar essa configuração, sem precisar incluí-la explicitamente na definição da etapa. Se nenhuma herança estiver em vigor, será necessário adicionar esse nó com as seguintes propriedades e valores.

   Neste exemplo, a herança foi ativada para que pudéssemos remover o `cq:listeners` e a etapa ainda funcionará corretamente.

   ![wf-41](assets/wf-41.png)

1. Agora é possível adicionar uma instância da etapa a um modelo de fluxo de trabalho. Quando você **Configurar** na etapa que você verá a caixa de diálogo:

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### Marcação de exemplo usada neste exemplo {#sample-markup-used-in-this-example}

A marcação para uma etapa personalizada é representada na variável `.content.xml` do nó raiz do componente. A amostra `.content.xml` usado para este exemplo:

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

O `_cq_editConfig.xml` exemplo usado neste exemplo:

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

O `_cq_dialog/.content.xml` exemplo usado neste exemplo:

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
>Observe os nós comuns e de processo na definição da caixa de diálogo. Eles são herdados da etapa do processo que usamos como supertipo para nossa etapa personalizada:
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>As caixas de diálogo do editor de modelo da interface clássica ainda funcionarão com o editor de interface de usuário padrão habilitado para toque.
>
>Embora AEM tenha [ferramentas de modernização](/help/sites-developing/modernization-tools.md) se você quiser atualizar as caixas de diálogo das etapas da interface clássica para caixas de diálogo padrão da interface do usuário. Após a conversão, ainda há algumas melhorias manuais que podem ser feitas no diálogo em determinados casos.
>
>* Nos casos em que uma caixa de diálogo atualizada está vazia, você pode visualizar as caixas de diálogo em `/libs` que tenham funcionalidade semelhante a exemplos de como fornecer uma solução. Por exemplo:
>
>* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`
>
>  Você não deve modificar nada em `/libs`, use-os como exemplos. Caso deseje aproveitar qualquer uma das etapas existentes, copie-as para `/apps` e modificá-las lá.
