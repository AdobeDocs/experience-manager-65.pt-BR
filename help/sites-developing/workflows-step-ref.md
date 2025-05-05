---
title: Referência da Etapa do fluxo de trabalho
description: Consulte esta referência de etapa para fluxos de trabalho no Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 8de78bde-2fcb-4221-873e-59e347ff2d74
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3227'
ht-degree: 2%

---

# Referência da Etapa do fluxo de trabalho {#workflow-step-reference}

Os modelos de fluxo de trabalho consistem em uma série de etapas de vários tipos. De acordo com o tipo, essas etapas podem ser configuradas e estendidas com parâmetros e scripts para fornecer a funcionalidade e o controle necessários.

>[!NOTE]
>
>Esta seção aborda as etapas padrão do fluxo de trabalho.
>
>Para obter etapas específicas do módulo, consulte o seguinte:
>
>* [Referência da etapa do fluxo de trabalho do AEM Forms](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [Processando o Assets com Manipuladores e Fluxos de Trabalho de Mídia](/help/assets/media-handlers.md)
>

## Propriedades da etapa {#step-properties}

Cada componente da etapa tem uma caixa de diálogo **Propriedades da Etapa** que permite definir e editar as propriedades necessárias.

### Propriedades da etapa - Guia Comum {#step-properties-common-tab}

Uma combinação das seguintes propriedades está disponível para a maioria dos componentes da etapa do fluxo de trabalho, na guia **Comum** da caixa de diálogo de propriedades:

* **Título**
O título da etapa.

* **Descrição**
Uma descrição da etapa.

* **Estágio do fluxo de trabalho**

  Um seletor suspenso para aplicar um [Estágio](/help/sites-developing/workflows.md#workflow-stages) à etapa.

* **Tempo limite**

  O período após o qual a etapa &quot;expira&quot;.
Você pode selecionar entre: **Desligado**, **Imediato**, **1h**, **6h**, **12h**, **24h**.

* **Manipulador de tempo limite**

  O manipulador que controla o fluxo de trabalho quando a etapa expira. Por exemplo, `Auto Advancer`

* **Avanço do manipulador**

  Selecione essa opção para avançar automaticamente o fluxo de trabalho para a próxima etapa após a execução. Se não for selecionada, o script de implementação deverá lidar com o avanço do fluxo de trabalho.

### Propriedades da etapa - guia Usuário/Grupo {#step-properties-user-group-tab}

As seguintes propriedades estão disponíveis para muitos componentes da etapa do fluxo de trabalho, na guia **Usuário/Grupo** da caixa de diálogo de propriedades:

* **Notificar usuário via email**

   * Notifique os participantes enviando um email quando o fluxo de trabalho atingir a etapa.
   * Se habilitado, um email será enviado ao usuário definido pela propriedade **User/Group**, ou a cada membro do grupo, se um grupo estiver definido.

* **Usuário/Grupo**

   * Uma caixa de seleção suspensa permite navegar até um usuário ou grupo e selecioná-lo.
   * Se você atribuir a etapa a um usuário específico, somente esse usuário poderá agir na etapa.
   * Se você atribuir a etapa a um grupo inteiro, quando o fluxo de trabalho atingir essa etapa, todos os usuários nesse grupo terão a ação em sua **Caixa de Entrada do Fluxo de Trabalho**.
   * Consulte [Participando de fluxos de trabalho](/help/sites-authoring/workflows-participating.md) para obter mais informações.

## Divisão E {#and-split}

A **AND Split** cria uma divisão no fluxo de trabalho, depois da qual ambas as ramificações estão ativas. Adicione etapas do fluxo de trabalho a cada ramificação, conforme necessário. Essa etapa permite introduzir vários caminhos de processamento no fluxo de trabalho. Por exemplo, é possível permitir que determinadas etapas de revisão ocorram em paralelo, economizando tempo.

![wf-26](assets/wf-26.png)

### E Dividir - Configuração {#and-split-configuration}

Para configurar a divisão:

* Editar as **E Dividir as Propriedades**:

   * **Dividir Nome**: atribuir um nome para fins explicativos
   * Selecione o número de ramificações necessárias: 2, 3, 4 ou 5.

* Adicione etapas do fluxo de trabalho às ramificações, conforme necessário.

  ![wf-27](assets/wf-27.png)

## Etapa do contêiner {#container-step}

Uma etapa do contêiner inicia outro modelo de fluxo de trabalho que é executado como um fluxo de trabalho secundário.

Esse contêiner pode permitir que você reutilize modelos de fluxo de trabalho para implementar sequências comuns de etapas. Por exemplo, um modelo de fluxo de trabalho de tradução pode ser usado em vários fluxos de trabalho de edição.

![wf-28](assets/wf-28.png)

### Etapa do contêiner - Configuração {#container-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Valores comuns de](#step-properties-common-tab)
* **Container**

   * **Subfluxo de trabalho**: selecione o fluxo de trabalho a ser iniciado.

## Etapa Ir para {#goto-step}

A **Etapa Ir para** permite que você especifique a próxima etapa a ser executada no modelo de fluxo de trabalho. Você pode especificar uma definição de regra, um script externo ou um script ECMA como a expressão de roteamento para avaliar a próxima etapa do modelo de workflow.

* Se a condição especificada for verdadeira, a **Etapa Ir** será concluída e o mecanismo de fluxo de trabalho executará a etapa especificada.
* Se a condição especificada não for verdadeira, a **Etapa Ir** será concluída e a lógica de roteamento normal determinará a próxima etapa a ser executada.

A **Etapa Ir para** permite implementar estruturas avançadas de roteamento em seus modelos de fluxo de trabalho. Por exemplo, para implementar um loop, a **Etapa Ir para** pode ser definida para executar uma etapa anterior no fluxo de trabalho, com a expressão de roteamento avaliando uma condição de loop.

### Etapa Ir para - Configuração {#goto-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Valores comuns de](#step-properties-common-tab)
* **Processo**

   * **Etapa de destino**: selecione a etapa a ser executada após avaliar a condição da expressão de roteamento.
   * **Expressão de Roteamento**: Selecione Definição de Regra, Script Externo ou um script ECMA que determine se a **Etapa de Destino** deverá ser executada.

      * **Definição de Regra:** Use o [editor de expressão](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) para definir a regra.
      * **Script Externo:** O caminho do script externo.
      * **Script ECMA**: o script que determina se a **Etapa Ir** deve ser executada.

#### Simulação de um loop for {#simulating-a-for-loop}

A simulação de um &quot;loop for&quot; requer que você mantenha uma contagem do número de iterações de loop que ocorreram:

* A contagem normalmente representa um índice de itens que são acionados no fluxo de trabalho.
* A contagem é avaliada como o critério de saída do loop.

Por exemplo, para implementar um fluxo de trabalho que execute uma ação em vários nós JCR, você pode usar um contador de loop como um índice para os nós. Para manter a contagem, armazene um valor `integer` no mapa de dados da instância de fluxo de trabalho. Para incrementar a contagem e comparar a contagem aos critérios de saída, use o script da **Etapa Ir para**.

```
function check(){
   var count=0;
   var keyname="loopcount"
   try{
      if (workflowData.getMetaDataMap().containsKey(keyname)){
        log.info("goto script: found loopcount key");
        count= parseInt(workflowData.getMetaDataMap().get(keyname))+1;
      }

     workflowData.getMetaDataMap().put(keyname,count);

     }catch(err) {
         log.info(err.message);
         return false;
    }
   if (parseInt(count) <7){
       return true;
   } else {
      return false;
   }
}
```

### Simulação de um loop for usando a Definição de regra {#simulateforloop}

Você também pode simular um loop for usando a Definição de Regra como a expressão de roteamento. [Crie uma variável **count**](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) do tipo de dados Long. Use **Expression** como modo de mapeamento na etapa **[Set Variable](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** para definir o valor da variável **count** como **count + 1** em cada execução da etapa **Set Variable**.

![Simulando um loop for](assets/variable_use_case_count_new.png)

Na **Etapa Ir para**, use **Set Variable** como a **Etapa de Destino** e **count &lt; 5** como a expressão de roteamento.

![Condição para simular um loop for](assets/variable_use_case_count1_new.png)

A etapa **Definir Variável** é executada repetidamente, incrementando o valor da variável **count** em 1 em cada execução até que o valor atinja 5.

## OU dividir {#or-split}

A **OU Split** cria uma divisão no fluxo de trabalho, depois da qual apenas uma ramificação fica ativa. Essa etapa permite introduzir caminhos de processamento condicional no fluxo de trabalho. Adicione etapas do fluxo de trabalho a cada ramificação, conforme necessário.

>[!NOTE]
>
>Consulte [OU Split step](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/using-variables-in-aem-workflows.html?lang=pt-BR#use-a-variable)

![Ramificação usando OU Split](assets/variables_orsplit_new.png)

### OU Split - Configuração {#or-split-configuration}

Para configurar a divisão:

* Edite as **OU Divida as Propriedades**:

   * **Comum**

      * Especifique o nome da divisão.

   * **Ramificações (*x)***

      * **Adicionar ramificação:** Adicione mais ramificações à etapa.
      * **Selecionar expressão de roteamento**: para avaliar a ramificação ativa, selecione a expressão de roteamento. Os valores possíveis incluem: Definição de regra, Script externo e script ECMA.
      * **Clique para Adicionar Expressão**: adicione a expressão para avaliar a ramificação ativa se você selecionar **Definição de Regra** como a expressão de roteamento.
      * **Caminho do Script**: o caminho para um arquivo que contém o script para avaliar a ramificação ativa se você selecionar **Script Externo** como expressão de roteamento.
      * **Script**: adicione o script na caixa para avaliar a ramificação ativa se você selecionar **Script ECMA** como expressão de roteamento.
      * **Rota Padrão**: a ramificação padrão será seguida se houver várias ramificações. Você pode especificar apenas uma ramificação como padrão.

  >[!NOTE]
  >
  >    * Uma ramificação é avaliada de cada vez com base na expressão de roteamento.
  >    * As ramificações são avaliadas de cima para baixo.
  >    * O primeiro script que é avaliado como true é executado.
  >    * Se nenhuma ramificação for avaliada como verdadeira, o fluxo de trabalho não avançará.
  >
  >

  >[!NOTE]
  >
  >Consulte [Definindo uma Regra para uma Divisão OR](/help/sites-developing/workflows-models.md#defineruleecmascript).

* Adicione etapas do fluxo de trabalho às ramificações, conforme necessário.

## Etapas e seletores do participante {#participant-steps-and-choosers}

### Etapa do participante {#participant-step}

Uma **Etapa de participante** permite que você atribua a propriedade de uma ação específica. O fluxo de trabalho continua somente quando o usuário confirma manualmente a etapa. Esse workflow é usado quando você deseja que alguém atue no workflow. Por exemplo, uma etapa de revisão.

Embora não esteja diretamente relacionada, a autorização do usuário deve ser considerada ao atribuir uma ação; o usuário deve ter acesso à página que é a carga do fluxo de trabalho.

#### Etapa do participante - Configuração {#participant-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Valores comuns de](#step-properties-common-tab)
* [Usuário/Grupo](#step-properties-user-group-tab)

>[!NOTE]
>
>O iniciador do fluxo de trabalho é sempre notificado quando:
>
>* O fluxo de trabalho foi concluído (concluído).
>* O fluxo de trabalho é interrompido (encerrado).
>

>[!NOTE]
>
>Algumas propriedades devem ser configuradas para habilitar notificações por email. Você também pode personalizar o modelo de email ou adicionar um modelo de email para um novo idioma. Para configurar notificações por email no AEM, consulte [Configurando Notificação por Email](/help/sites-administering/notification.md#configuringemailnotification).

### Etapa do participante do diálogo {#dialog-participant-step}

Use uma **Etapa do participante da caixa de diálogo** para coletar informações do usuário ao qual foi atribuído o item de trabalho. Essa etapa é útil para coletar pequenas quantidades de dados que são usados posteriormente no fluxo de trabalho.

Ao concluir a etapa, a caixa de diálogo **Concluir Item de Trabalho** contém os campos que você define na caixa de diálogo. Os dados coletados nos campos são armazenados em nós da carga do fluxo de trabalho. As etapas subsequentes do fluxo de trabalho podem ler o valor no repositório.

Para configurar a etapa, especifique o grupo ou usuário ao qual atribuir o item de trabalho e o caminho para a caixa de diálogo.

#### Etapa do participante da caixa de diálogo - Configuração {#dialog-participant-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Valores comuns de](#step-properties-common-tab)
* [Usuário/Grupo](#step-properties-user-group-tab)
* **Caixa de diálogo**

   * **Caminho da caixa de diálogo**: o caminho para o nó da caixa de diálogo [que você cria](#dialog-participant-step-creating-a-dialog).

#### Etapa do participante da caixa de diálogo - Criação de uma caixa de diálogo {#dialog-participant-step-creating-a-dialog}

Para criar uma caixa de diálogo, você deve criar a caixa de diálogo:

* Decida onde os dados resultantes são [armazenados na carga](#dialog-participant-step-storing-data-in-the-payload).
* [Definir a caixa de diálogo; inclui a definição dos campos usados para coletar e salvar os dados](#dialog-participant-step-dialog-definition).

#### Etapa do participante do diálogo - Armazenamento de dados na carga {#dialog-participant-step-storing-data-in-the-payload}

Você pode armazenar dados do widget na carga do fluxo de trabalho ou nos metadados do item de trabalho. O formato da propriedade `name` do nó do widget determina onde os dados são armazenados.

* **Armazenar dados com a carga**

   * Para armazenar dados do widget como uma propriedade da carga do fluxo de trabalho, use o seguinte formato para o valor da propriedade name do nó do widget:

     `./jcr:content/nodename`

   * Os dados são armazenados na propriedade `nodename` do nó de carga. Se o nó não contiver essa propriedade, a propriedade será criada.
   * Quando armazenado com a carga, os usos subsequentes da caixa de diálogo com a mesma carga substituem o valor da propriedade.

* **Armazenar dados com o item de trabalho**

   * Para armazenar dados do widget como uma propriedade dos metadados do item de trabalho, use o seguinte formato para o valor da propriedade name:

     `nodename`

   * Os dados são armazenados na propriedade `nodename` do item de trabalho `metadata`. Os dados são preservados se a caixa de diálogo for usada posteriormente com a mesma carga.

#### Etapa do participante do diálogo - Definição do diálogo {#dialog-participant-step-dialog-definition}

1. **Estrutura de diálogo**

   As caixas de diálogo das Etapas do participante da caixa de diálogo são semelhantes às caixas de diálogo criadas para a criação de componentes. Eles são armazenados em:

   `/apps/myapp/workflow/dialogs`

   As caixas de diálogo da interface do usuário padrão habilitada para toque têm a seguinte estrutura de nó:

   ```xml
   newComponent (cq:Component)
     |- cq:dialog (nt:unstructured)
       |- content
         |- layout
           |- items
             |- column
               |- items
                 |- component0
                 |- component1
                 |- ...
   ```

   >[!NOTE]
   >
   >Consulte [Criando e Configurando uma Caixa de Diálogo](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog).

1. **Propriedade do Caminho da Caixa de Diálogo**

   A **Etapa do Participante da Caixa de Diálogo** tem a propriedade **Caminho da Caixa de Diálogo** (juntamente com as propriedades de uma [Etapa do Participante](#participant-step)). O valor da propriedade **Caminho da Caixa de Diálogo** é o caminho para o nó `dialog` da caixa de diálogo.

   Por exemplo, a caixa de diálogo está contida em um componente chamado `EmailWatch` que está armazenado no nó:

   `/apps/myapp/workflows/dialogs`

   Para a interface habilitada para toque, o seguinte valor é usado para a propriedade **Caminho da Caixa de Diálogo**:

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **Definição de Caixa de Diálogo de Exemplo**

   O trecho de código XML a seguir representa uma caixa de diálogo que armazena um valor `String` no nó `watchEmail` do conteúdo da carga. O nó de título representa o componente [TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html):

   ```xml
   jcr:primaryType="nt:unstructured"
       jcr:title="Watcher Email Address Dialog"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/foundation/container">
           <layout jcr:primaryType="nt:unstructured"
               margin="false"
               sling:resourceType="granite/ui/components/foundation/layouts/fixedcolumns"
           />
           <items jcr:primaryType="nt:unstructured">
               <column jcr:primaryType="nt:unstructured"
                   sling:resourceType="granite/ui/components/foundation/container">
                   <items jcr:primaryType="nt:unstructured">
                       <title jcr:primaryType="nt:unstructured"
                           fieldLabel="Notification Email Address"
                           name="./jcr:content/watchEmails"
                           sling:resourceType="granite/ui/components/foundation/form/textfield"
                       />
                   </items>
               </column>
           </items>
       </content>
   </cq:dialog>
   ```

   Na interface habilitada para toque, esse exemplo resulta em uma caixa de diálogo como a seguinte:

   ![chlimage_1-70](assets/chlimage_1-70.png)

### Etapa dinâmica do participante {#dynamic-participant-step}

O componente **Etapa Dinâmica de Participante** é semelhante à **[Etapa de Participante](#participant-step)**, com a diferença de que o participante é selecionado automaticamente em tempo de execução.

Para configurar a etapa, selecione um **Seletor de Participantes** que identifique o participante ao qual atribuir o item de trabalho, juntamente com uma caixa de diálogo.

#### Etapa dinâmica do participante - Configuração {#dynamic-participant-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Valores comuns de](#step-properties-common-tab)
* **Seletor de participantes**

   * **Seletor de Participantes**: o nome do [seletor de participantes que você cria](#developingtheparticipantchooser).
   * **Argumentos**: qualquer argumento necessário.
   * **Email**: se uma notificação por email deve ser enviada ao usuário.

* **Caixa de diálogo**

   * **Caminho da Caixa de Diálogo**: O caminho para o nó da caixa de diálogo da [caixa de diálogo que você cria (como com a **Etapa de Participante da Caixa de Diálogo**)](#dialog-participant-step-creating-a-dialog).

#### Etapa dinâmica do participante - Desenvolvendo o seletor de participantes {#dynamic-participant-step-developing-the-participant-chooser}

Você cria o seletor de participantes. Portanto, é possível usar qualquer lógica ou critério de seleção. Por exemplo, seu seletor de participantes pode selecionar o usuário (dentro de um grupo) que tem menos itens de trabalho. Você pode criar qualquer número de seletores de participantes para usar com instâncias diferentes do componente **Etapa dinâmica de participante** em seus modelos de fluxo de trabalho.

Crie um serviço OSGi ou um ECMAScript que selecione um usuário ao qual atribuir o item de trabalho.

* **ECMAscript**

  Os scripts devem incluir uma função chamada getParticipant que retorne uma ID de usuário como um valor `String`. Armazene seus scripts personalizados, por exemplo, na pasta `/apps/myapp/workflow/scripts` ou em uma subpasta.

  Um exemplo de script é incluído em uma instância AEM padrão:

  `/libs/workflow/scripts/initiator-participant-chooser.ecma`

  >[!CAUTION]
  >
  >Não altere nada no caminho `/libs`.
  >
  >
  >O motivo é que o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).

  Este script seleciona o iniciador do fluxo de trabalho como o participante:

  ```
  function getParticipant() {
      return workItem.getWorkflow().getInitiator();
  }
  ```

  >[!NOTE]
  >
  >O componente **Seletor de Participante Iniciador do Fluxo de Trabalho** estende a **Etapa de Participante Dinâmica** e usa esse script como a implementação da etapa.

* **Serviço OSGi**

  Os serviços devem implementar a interface [com.day.cq.workflow.exec.ParticipantStepChooser](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html). A interface define os seguintes membros:

   * Campo `SERVICE_PROPERTY_LABEL`: use este campo para especificar o nome do seletor de participantes. O nome aparece em uma lista de seletores de participantes disponíveis nas propriedades da **Etapa dinâmica de participante**.

   * Método `getParticipant`: retorna a ID da Entidade de Segurança resolvida dinamicamente como um valor `String`.

  >[!CAUTION]
  >
  >O método `getParticipant` retorna a ID Principal resolvida dinamicamente. Essa ID pode ser uma ID de grupo ou de usuário.
  >
  >
  >No entanto, uma ID de grupo só pode ser usada para uma **Etapa do participante**, quando uma lista de participantes é retornada. Para uma **Etapa dinâmica de participante**, uma lista vazia é retornada e não pode ser usada para delegação.

  Para disponibilizar sua implementação para componentes da **Etapa dinâmica de participante**, adicione sua classe Java™ a um pacote OSGi que exporte o serviço e implante o pacote no servidor AEM.

  >[!NOTE]
  >
  >**Seletor de Participante Aleatório** é um serviço de exemplo que seleciona um usuário aleatório ( `com.day.cq.workflow.impl.process.RandomParticipantChooser`). A amostra do componente de etapa **Escolher Participante Aleatório** r estende a **Etapa de Participante Dinâmico** e usa esse serviço como a implementação da etapa.

#### Etapa dinâmica do participante - Exemplo de serviço do seletor de participantes {#dynamic-participant-step-example-participant-chooser-service}

A seguinte classe Java™ implementa a interface `ParticipantStepChooser`. A classe retorna o nome do participante que iniciou o workflow. O código usa a mesma lógica que o script de exemplo (`initiator-participant-chooser.ecma`) usa.

A anotação `@Property` define o valor do campo `SERVICE_PROPERTY_LABEL` como `Workflow Initiator Participant Chooser`.

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.osgi.framework.Constants;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.ParticipantStepChooser;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;

@Component
@Service
@Properties({
        @Property(name = Constants.SERVICE_DESCRIPTION, value = "An example implementation of a dynamic participant chooser."),
        @Property(name = ParticipantStepChooser.SERVICE_PROPERTY_LABEL, value = "Workflow Initiator Participant Chooser (service)") })
public class InitiatorParticipantChooser implements ParticipantStepChooser {

 private Logger logger = LoggerFactory.getLogger(this.getClass());

 public String getParticipant(WorkItem arg0, WorkflowSession arg1,
   MetaDataMap arg2) throws WorkflowException {

  String initiator = arg0.getWorkflow().getInitiator();
  logger.info("Assigning Dynamic Participant Step work item to {}",initiator);

  return initiator;
 }
}
```

Na caixa de diálogo de propriedades **Etapa Dinâmica de Participante**, a lista **Seletor de Participante** inclui o item `Workflow Initiator Participant Chooser (script)`, que representa este serviço.

Quando o modelo de fluxo de trabalho é iniciado, o log indica a ID do usuário que iniciou o fluxo de trabalho e a quem foi atribuído o item de trabalho. Neste exemplo, o usuário `admin` iniciou o fluxo de trabalho.

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### Etapa de participante do formulário {#form-participant-step}

A **Etapa de participante do formulário** apresenta um formulário quando o item de trabalho é aberto. Quando o usuário preenche e envia o formulário, os dados do campo são armazenados nos nós da carga do fluxo de trabalho.

Para configurar a etapa, especifique o grupo ou usuário ao qual atribuir o item de trabalho e o caminho para o formulário.

>[!CAUTION]
>
>Esta seção trata da [seção Forms dos Componentes de Base para Criação de Página](/help/sites-authoring/default-components-foundation.md#form).

#### Etapa de participante do formulário - Configuração {#form-participant-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Valores comuns de](#step-properties-common-tab)
* [Usuário/Grupo](#step-properties-user-group-tab)
* **Formulário**

   * **Caminho do Formulário**: O caminho para o [formulário que você criar](#form-participant-step-creating-the-form).

#### Etapa de participante do formulário - Criação do formulário {#form-participant-step-creating-the-form}

Crie um formulário para usar com uma **Etapa de participante do formulário** como de costume. No entanto, os formulários para uma Etapa de participante do formulário devem ter as seguintes configurações:

* O componente **Início do Formulário** deve ter a propriedade **Tipo de Ação** definida como `Edit Workflow Controlled Resource(s)`.
* O componente **Início do Formulário** deve ter um valor para a propriedade `Form Identifier`.
* Os componentes de formulário devem ter a propriedade **Nome do Elemento** definida como o caminho do nó onde os dados do campo estão armazenados. O caminho deve localizar um nó no conteúdo de carga do fluxo de trabalho. O valor usa o seguinte formato:

  `./jcr:content/path_to_node`

* O formulário deve incluir um componente **Botão de Envio do Fluxo de Trabalho**. Você não configura nenhuma propriedade do componente.

Os requisitos do fluxo de trabalho determinam onde você deve armazenar os dados de campo. Por exemplo, dados de campo podem ser usados para configurar as propriedades do conteúdo da página. O seguinte valor de uma propriedade **Nome do Elemento** armazena dados de campo como o valor da propriedade `redirectTarget` do nó `jcr:content`:

`./jcr:content/redirectTarget`

No exemplo a seguir, os dados do campo são usados como conteúdo de um componente **Texto** na página de carga:

`./jcr:content/par/text_3/text`

O primeiro exemplo pode ser usado para qualquer página que o componente `cq:Page` renderize. O segundo exemplo só pode ser usado quando a página de carga inclui um componente **Texto** com ID `text_3`.

O formulário pode estar localizado em qualquer lugar no repositório, no entanto, os usuários do fluxo de trabalho devem estar autorizados a ler o formulário.

### Seletor de participante aleatório {#random-participant-chooser}

A etapa **Seletor de Participante Aleatório** é um seletor de participante que atribui o item de trabalho gerado a um usuário selecionado aleatoriamente de uma lista.

![wf-31](assets/wf-31.png)

#### Seletor de participante aleatório - Configuração {#random-participant-chooser-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Valores comuns de](#step-properties-common-tab)
* **Argumentos**

   * **Participantes**: especifica a lista de usuários disponíveis para seleção. Para adicionar um usuário à lista, clique em **Adicionar item** e digite o caminho inicial do nó do usuário ou da ID do usuário. A ordem dos usuários não afeta a probabilidade de receber um item de trabalho.

### Seletor do participante iniciador do fluxo de trabalho  {#workflow-initiator-participant-chooser}

A etapa **Seletor de Participante Iniciador do Fluxo de Trabalho** é um seletor de participantes que atribui o item de trabalho gerado ao usuário que iniciou o fluxo de trabalho. Não há propriedades a serem configuradas diferentes das propriedades **Common**.

#### Seletor do participante iniciador do fluxo de trabalho - Configuração {#workflow-initiator-participant-chooser-configuration}

Para configurar a etapa, edite usando as seguintes guias:

* [Valores comuns de](#step-properties-common-tab)

## Etapa do processo {#process-step}

Uma **Etapa do processo** executa um ECMAScript ou chama um serviço OSGi para executar o processamento automático.

![wf-32](assets/wf-32.png)

### Etapa do processo - Configuração {#process-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Valores comuns de](#step-properties-common-tab)
* **Processo**

   * **Processo**: a implementação do processo a ser executada. Use o menu suspenso para selecionar o serviço ECMAScript ou OSGi. Para obter informações sobre:

      * Os ECMAScripts padrão e os serviços OSGi, consulte [Processos internos para etapas do processo](/help/sites-developing/workflows-process-ref.md).
      * Criando ECMAScripts para uma etapa do Processo, consulte [Implementando uma Etapa do Processo com um ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * Criando serviços OSGi para uma etapa do Processo, consulte [Implementando uma Etapa do Processo com uma Classe Java™](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class).

   * **Avanço do manipulador**: selecione essa opção para avançar automaticamente o fluxo de trabalho para a próxima etapa após a execução. Se não for selecionada, o script de implementação deverá lidar com o avanço do fluxo de trabalho.
   * **Argumentos**: argumentos a serem passados para o processo.

## Definir variável {#set-variable}

A etapa Definir variável permite definir o valor de uma variável e a ordem na qual os valores são definidos. A variável é definida na ordem em que os mapeamentos de variável são listados na etapa Definir variável.

![Adicionar mapeamento para definir uma variável](assets/set_variable_addmappingnew.png)

### Definir variável - Configuração {#setvariable}

Para configurar a etapa, edite e use as seguintes guias:

* [Valores comuns de](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **Mapeamento**

   * **Selecionar variável:** use esta opção para selecionar uma variável para definir seu valor.
   * **Selecionar Modo de Mapeamento:** Para definir o valor da variável, selecione um modo de mapeamento. Dependendo do tipo de dados da variável, você pode usar as seguintes opções para definir o valor de uma variável:

      * **Literal:** Use a opção quando você souber o valor exato a ser especificado.
      * **Expressão:** use a opção quando o valor a ser usado for calculado com base em uma expressão. A expressão é criada no editor de expressão fornecido.
      * **Anotação JSON Dot:** Use a opção para recuperar um valor de uma variável do tipo JSON ou FDM.
      * **XPATH:** Use a opção para recuperar um valor de uma variável do tipo XML.
      * **Relativo à carga:** use a opção quando o valor a ser salvo na variável estiver disponível em um caminho relativo à carga.
      * **Caminho absoluto:** Use a opção quando o valor a ser salvo na variável estiver disponível em um caminho absoluto.

   * **Especificar Valor:** Para mapear para a variável, especifique um valor. O valor especificado neste campo depende do modo de mapeamento.
   * **Adicionar mapeamento:** use esta opção para adicionar mais mapeamentos para definir um valor para a variável.
