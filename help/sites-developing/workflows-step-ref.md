---
title: Referência da Etapa do fluxo de trabalho
seo-title: Workflow Step Reference
description: Referência da Etapa do fluxo de trabalho
seo-description: null
uuid: 88bf6997-73a1-4639-82aa-5dff08d3ef86
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e3afffd0-d90c-4bd0-b814-f7aeac6ceb6d
docset: aem65
exl-id: 8de78bde-2fcb-4221-873e-59e347ff2d74
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3284'
ht-degree: 2%

---

# Referência da Etapa do fluxo de trabalho {#workflow-step-reference}

Os modelos de fluxo de trabalho consistem em uma série de etapas de vários tipos. De acordo com o tipo , essas etapas podem ser configuradas e estendidas com parâmetros e scripts para fornecer a funcionalidade e o controle necessários.

>[!NOTE]
>
>Esta seção aborda as etapas padrão do fluxo de trabalho.
>
>Para ver as etapas específicas do módulo, consulte também:
>
>* [Referência em etapas do fluxo de trabalho do AEM Forms](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [Processamento de ativos usando manipuladores de mídia e fluxos de trabalho](/help/assets/media-handlers.md)
>


## Propriedades da etapa {#step-properties}

Cada componente de etapa tem uma **Propriedades da etapa** que permite definir e editar as propriedades necessárias.

### Propriedades da etapa - guia Comum {#step-properties-common-tab}

Uma combinação das seguintes propriedades está disponível para a maioria dos componentes da etapa do fluxo de trabalho, no **Frequentes** da caixa de diálogo de propriedades:

* **Título**
O título da etapa.

* **Descrição**
Uma descrição da etapa.

* **Estágio do fluxo de trabalho**

   Um seletor suspenso para aplicar um [Fase](/help/sites-developing/workflows.md#workflow-stages) para a etapa .

* **Tempo limite**

   O período após o qual a etapa será &quot;atingida&quot;.
Você pode selecionar entre: **Desligado**, **Imediato**, **1h**, **6h**, **12h**, **24 h**.

* **Tempo limite do Handler**

   O manipulador que controlará o fluxo de trabalho quando a etapa expirar; por exemplo:
   `Auto Advancer`

* **Handler avançado**

   Selecione essa opção para avançar automaticamente o workflow para a próxima etapa após a execução. Se não estiver selecionado, o script de implementação deve lidar com a evolução do fluxo de trabalho.

### Propriedades da etapa - guia Usuário/grupo {#step-properties-user-group-tab}

As seguintes propriedades estão disponíveis para vários componentes de etapa do fluxo de trabalho, na variável **Usuário/Grupo** da caixa de diálogo de propriedades:

* **Notificar usuário via e-mail**

   * Você pode notificar o(s) participante(s) enviando um email quando o workflow atingir a etapa .
   * Se ativado, um email será enviado para o usuário definido pela propriedade **Usuário/Grupo** ou a cada membro do grupo, se um grupo estiver definido.

* **Usuário/Grupo**

   * Uma caixa de seleção suspensa permitirá que você navegue e selecione um usuário ou grupo.
   * Se você atribuir a etapa a um usuário específico, somente esse usuário poderá realizar uma ação na etapa .
   * Se você atribuir a etapa a um grupo inteiro, quando o fluxo de trabalho atingir essa etapa, todos os usuários desse grupo terão a ação em seus **Caixa de entrada do fluxo de trabalho**.
   * Consulte [Participar de fluxos de trabalho](/help/sites-authoring/workflows-participating.md) para obter mais informações.

## E dividir {#and-split}

O **E dividir** O cria uma divisão no fluxo de trabalho, depois disso as duas ramificações estarão ativas. Adicione etapas de fluxo de trabalho a cada ramificação, conforme necessário. Essa etapa permite introduzir vários caminhos de processamento no fluxo de trabalho. Por exemplo, você pode permitir que determinadas etapas de revisão ocorram em paralelo, economizando tempo.

![wf-26](assets/wf-26.png)

### AND Split - Configuração {#and-split-configuration}

Para configurar a divisão:

* Edite o **E Dividir Propriedades**:

   * **Nome da divisão**: atribuir um nome para fins explicativos
   * Selecione o número de ramificações necessárias; 2, 3, 4 ou 5.

* Adicione etapas de fluxo de trabalho às ramificações, conforme necessário.

   ![wf-27](assets/wf-27.png)

## Etapa do contêiner {#container-step}

Uma etapa do contêiner inicia outro modelo de fluxo de trabalho executado como um fluxo de trabalho filho.

Esse contêiner pode permitir que você reutilize modelos de fluxo de trabalho para implementar sequências de etapas comuns. Por exemplo, um modelo de fluxo de trabalho de tradução pode ser usado em vários fluxos de trabalho de edição.

![wf-28](assets/wf-28.png)

### Etapa do contêiner - Configuração {#container-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* **Container**

   * **Sub-fluxo de trabalho**: Selecione o workflow a ser iniciado.

## Etapa Ir para {#goto-step}

O **Etapa Ir para** permite especificar a próxima etapa a ser executada no modelo de fluxo de trabalho. Você pode especificar uma definição de regra, um script externo ou um script ECMA como a expressão de roteamento para avaliar a próxima etapa do modelo de workflow.

* Se a condição especificada for verdadeira, a variável **Etapa Ir para** O é concluído e o mecanismo de workflow executa a etapa especificada.
* Se a condição especificada não for verdadeira, a variável **Etapa Ir para** é concluída e a lógica normal de roteamento determina a próxima etapa a ser executada.

O **Etapa Ir para** O permite implementar estruturas avançadas de roteamento em seus modelos de workflow. Por exemplo, para implementar um loop, a variável **Etapa Ir para** pode ser definido para executar uma etapa anterior no fluxo de trabalho, com a expressão de roteamento avaliando uma condição de loop.

### Etapa Ir - Configuração {#goto-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* **Processo**

   * **Etapa do Target**: Selecione a etapa a ser executada após avaliar a condição da expressão de roteamento.
   * **Expressão de Roteamento**: Selecione Definição de regra, Script externo ou um script ECMA que determine se a execução do **Etapa do Target**.

      * **Definição de regra:** Use o [editor de expressão](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) para definir a regra.
      * **Script externo:** O caminho do script externo.
      * **Script ECMA**: O script que determina se o **Etapa Ir para**.

#### Simulação de um loop for {#simulating-a-for-loop}

A simulação de um loop for requer que você mantenha uma contagem do número de iterações de loop que ocorreram:

* A contagem geralmente representa um índice de itens que são ativados no fluxo de trabalho.
* A contagem é avaliada como o critério de saída do loop.

Por exemplo, para implementar um workflow que executa uma ação em vários nós JCR, você pode usar um contador de loop como um índice para os nós. Para manter a contagem, armazene um `integer` no mapa de dados da instância do workflow. Use o script do **Etapa Ir para** para incrementar a contagem e comparar a contagem com os critérios de saída.

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

Também é possível simular um loop for usando a Definição de regra como a expressão de roteamento. [Crie um **count** variável](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) do tipo de dados Long. Use **Expressão** como o modo de mapeamento no **[Definir variável](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** para definir o valor da variável **count** para **contagem + 1** em cada execução do **Definir variável** etapa.

![Simulação de um loop for](assets/variable_use_case_count_new.png)

No **Etapa Ir para**, use **Definir variável** como **Etapa do Target** e **contagem &lt; 5** como a expressão de roteamento.

![Condição para simular um loop for](assets/variable_use_case_count1_new.png)

O **Definir variável** a etapa é executada repetidamente, aumentando o valor de **count** em 1 em cada execução até o valor atingir 5.

## OU dividir {#or-split}

O **OU Dividir** cria uma divisão no fluxo de trabalho, depois disso apenas uma ramificação estará ativa. Essa etapa permite introduzir caminhos de processamento condicional no fluxo de trabalho. Adicione etapas de fluxo de trabalho a cada ramificação, conforme necessário.

>[!NOTE]
>
>Para obter informações adicionais sobre como criar uma divisão OU, consulte: [https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html](https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html)

![Ramificação usando OU Dividir](assets/variables_orsplit_new.png)

### OU Dividir - Configuração {#or-split-configuration}

Para configurar a divisão:

* Edite o **OU Dividir propriedades**:

   * **Comum**

      * Especifique o nome da divisão.
   * **Ramificações (*x)***

      * **Adicionar Ramificação:** Adicione mais ramificações à etapa .
      * **Selecionar Expressão de Roteamento**: Selecione a expressão de roteamento para avaliar a ramificação ativa. Os valores possíveis incluem: Definição de regra, script externo e script ECMA.
      * **Clique para adicionar expressão**: Adicionar expressão para avaliar a ramificação ativa se você selecionar **Definição de regra** como a expressão de roteamento.
      * **Caminho do script**: O caminho para um arquivo que contém o script para avaliar a ramificação ativa se você selecionar **Script externo** como a expressão de roteamento.
      * **Script**: Adicione o script na caixa para avaliar a ramificação ativa se você selecionar **Script ECMA** como a expressão de roteamento.
      * **Rota padrão**: A ramificação padrão é seguida no caso de várias ramificações. Você pode especificar apenas uma ramificação como padrão.

   >[!NOTE]
   >
   >    * Uma ramificação é avaliada de cada vez com base na expressão de roteamento.
   >    * As ramificações são avaliadas de cima para baixo.
   >    * O primeiro script que resulta em true é executado.
   >    * Se nenhuma ramificação for avaliada como true, o workflow não será adiantado.


   >[!NOTE]
   >
   >Consulte [Definição de uma regra para uma divisão OR](/help/sites-developing/workflows-models.md#defineruleecmascript).

* Adicione etapas de fluxo de trabalho às ramificações, conforme necessário.

## Etapas e seletores do participante {#participant-steps-and-choosers}

### Etapa do participante {#participant-step}

A **Etapa do participante** permite atribuir a propriedade de uma ação específica. O fluxo de trabalho só continuará quando o usuário tiver confirmado manualmente a etapa. Isso é usado quando você deseja que alguém execute uma ação no fluxo de trabalho; por exemplo, uma etapa de revisão.

Embora não esteja diretamente relacionada, a autorização do utilizador deve ser considerada ao atribuir uma ação; o usuário deve ter acesso à página que é a carga do fluxo de trabalho.

#### Etapa do participante - Configuração {#participant-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* [Usuário/Grupo](#step-properties-user-group-tab)

>[!NOTE]
>
>O iniciador do workflow é sempre notificado quando:
>
>* O fluxo de trabalho é concluído (concluído).
>* O workflow é abortado (encerrado).
>


>[!NOTE]
>
>Algumas propriedades precisam ser configuradas para ativar as notificações por email. Você também pode personalizar o modelo de email ou adicionar um modelo de email para um novo idioma. Consulte [Configuração de notificação por email](/help/sites-administering/notification.md#configuringemailnotification) para configurar notificações por email no AEM.

### Etapa do participante do diálogo {#dialog-participant-step}

Use um **Etapa da caixa de diálogo do participante** para coletar informações do usuário que recebe o item de trabalho. Essa etapa é útil para coletar pequenas quantidades de dados usadas posteriormente no workflow.

Ao concluir a etapa, o **Item de Trabalho Concluído** contém os campos definidos na caixa de diálogo. Os dados coletados nos campos são armazenados em nós da carga do workflow. As etapas de fluxo de trabalho subsequentes podem ler o valor do repositório.

Para configurar a etapa, especifique o grupo ou usuário ao qual o item de trabalho será atribuído e o caminho para a caixa de diálogo.

#### Etapa da caixa de diálogo do participante - Configuração {#dialog-participant-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* [Usuário/Grupo](#step-properties-user-group-tab)
* **Caixa de diálogo**

   * **Caminho da caixa de diálogo**: O caminho para o nó de diálogo do [diálogo que você criar](#dialog-participant-step-creating-a-dialog).

#### Etapa da caixa de diálogo do participante - Criação de uma caixa de diálogo {#dialog-participant-step-creating-a-dialog}

Para criar uma caixa de diálogo, é necessário criar a caixa de diálogo:

* Decida onde os dados resultantes serão [armazenado na carga](#dialog-participant-step-storing-data-in-the-payload).
* [Definir a caixa de diálogo; isso inclui a definição dos campos usados para coletar (e salvar) os dados](#dialog-participant-step-dialog-definition).

#### Etapa da caixa de diálogo do participante - Armazenamento de dados na carga {#dialog-participant-step-storing-data-in-the-payload}

Você pode armazenar dados de widget na carga do fluxo de trabalho ou nos metadados do item de trabalho. O formato do `name` a propriedade do nó widget determina onde os dados são armazenados.

* **Armazenar dados com a carga**

   * Para armazenar dados de widget como uma propriedade do payload do workflow, use o seguinte formato para o valor da propriedade name do nó do widget:
      `./jcr:content/nodename`

   * Os dados são armazenados no `nodename` propriedade do nó de carga. Se o nó não contiver essa propriedade, a propriedade será criada.
   * Quando armazenados com a carga, os usos subsequentes da caixa de diálogo com a mesma carga substitui o valor da propriedade.

* **Armazenar dados com o item de trabalho**

   * Para armazenar dados de widget como uma propriedade dos metadados do item de trabalho, use o seguinte formato para o valor da propriedade name :
      `nodename`

   * Os dados são armazenados no `nodename` propriedade do item de trabalho `metadata`. Os dados são preservados se a caixa de diálogo for posteriormente usada com a mesma carga útil.

#### Etapa da caixa de diálogo do participante - Definição da caixa de diálogo {#dialog-participant-step-dialog-definition}

1. **Estrutura de diálogo**

   As caixas de diálogo para Etapas do participante na caixa de diálogo são semelhantes às caixas de diálogo criadas para os componentes da criação. São armazenadas em:

   `/apps/myapp/workflow/dialogs`

   As caixas de diálogo da interface de usuário padrão e habilitada para toque têm a seguinte estrutura de nó:

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
   >Para obter mais informações, consulte [Criação e configuração de uma caixa de diálogo](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog).

1. **Propriedade do caminho de diálogo**

   O **Etapa da caixa de diálogo do participante** tem **Caminho da caixa de diálogo** (junto com as propriedades de um [Etapa do participante](#participant-step)). O valor da variável **Caminho da caixa de diálogo** propriedade é o caminho para a variável `dialog` nó da caixa de diálogo.

   Por exemplo, a caixa de diálogo está contida em um componente chamado `EmailWatch` que é armazenado no nó :

   `/apps/myapp/workflows/dialogs`

   Para a interface habilitada para toque, o seguinte valor é usado para a variável **Caminho da caixa de diálogo** propriedade:

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **Exemplo de definição de caixa de diálogo**

   O trecho de código XML a seguir representa uma caixa de diálogo que armazena um `String` na variável `watchEmail` nó do conteúdo da carga útil. O nó title representa o [TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) componente:

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

   Esse exemplo, no caso da interface habilitada para toque, resultará em uma caixa de diálogo, como:

   ![chlimage_1-70](assets/chlimage_1-70.png)

### Etapa dinâmica do participante {#dynamic-participant-step}

O **Etapa dinâmica do participante** é semelhante a **[Etapa do participante](#participant-step)** com a diferença de que o participante é selecionado automaticamente em tempo de execução.

Para configurar a etapa, selecione um **Seletor de participante** que identifica o participante ao qual atribuir o item de trabalho, junto com uma caixa de diálogo.

#### Etapa dinâmica do participante - Configuração {#dynamic-participant-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* **Seletor de participantes**

   * **Seletor de participante**: O nome do [selecionador de participantes que você criar](#developingtheparticipantchooser).
   * **Argumentos**: Qualquer argumento necessário.
   * **Email**: Se uma notificação por email deve ser enviada ao usuário.

* **Caixa de diálogo**

   * **Caminho da caixa de diálogo**: O caminho para o nó de diálogo do [da caixa de diálogo criada (como com o **Etapa da caixa de diálogo do participante**)](#dialog-participant-step-creating-a-dialog).

#### Etapa dinâmica do participante - Desenvolvimento do seletor de participantes {#dynamic-participant-step-developing-the-participant-chooser}

Crie o seletor de participantes. Portanto, você pode usar qualquer lógica ou critério de seleção. Por exemplo, o seletor de participantes pode selecionar o usuário (em um grupo) que tem menos itens de trabalho. Você pode criar qualquer número de opções de participantes para usar com diferentes instâncias do **Etapa dinâmica do participante** em seus modelos de fluxo de trabalho.

Crie um serviço OSGi ou um ECMAScript que selecione um usuário para atribuir o item de trabalho.

* **ECMAscript**

   Os scripts devem incluir uma função chamada getParticipant que retorna uma ID de usuário como um `String` valor. Armazene seus scripts personalizados na, por exemplo, a variável `/apps/myapp/workflow/scripts` ou uma subpasta.

   Um script de amostra é incluído em uma instância de AEM padrão:

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >Você ***must*** não altere nada no `/libs` caminho.
   >
   >
   >Isso ocorre porque o conteúdo da variável `/libs` O é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).

   Este script seleciona o iniciador do workflow como o participante:

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >O **Seletor de Participante Iniciador de Fluxo de Trabalho** estende o **Etapa dinâmica do participante** e usa esse script como a implementação da etapa.

* **Serviço OSGi**

   Os serviços devem implementar o [com.day.cq.workflow.exec.ParticipantStepChooser](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) interface. A interface define os seguintes membros:

   * `SERVICE_PROPERTY_LABEL` campo : Use este campo para especificar o nome do seletor de participantes. O nome aparece em uma lista de seletores de participantes disponíveis no **Etapa dinâmica do participante** propriedades.

   * `getParticipant` método : Retorna o ID Principal resolvido dinamicamente como um `String` valor.
   >[!CAUTION]
   >
   >O `getParticipant` O método retorna o Principal id resolvido dinamicamente. Pode ser uma id de grupo ou uma id de usuário.
   >
   >
   >No entanto, uma id de grupo só pode ser usada para um **Etapa do participante**, quando uma lista de participantes é retornada. Para um **Etapa dinâmica do participante** uma lista vazia é retornada e não pode ser usada para delegação.

   Para disponibilizar a implementação para **Etapa dinâmica do participante** componentes, adicione sua classe Java a um pacote OSGi que exporte o serviço e implante o pacote no servidor AEM.

   >[!NOTE]
   >
   >**Seletor de participante aleatório** é um serviço de exemplo que seleciona um usuário aleatório ( `com.day.cq.workflow.impl.process.RandomParticipantChooser`). O **Escolha um participante aleatório** A amostra do componente da etapa r estende a **Etapa dinâmica do participante** e usa esse serviço como a implementação da etapa .

#### Etapa dinâmica do participante - Exemplo de serviço de escolha do participante {#dynamic-participant-step-example-participant-chooser-service}

A seguinte classe Java implementa o `ParticipantStepChooser` interface. A classe retorna o nome do participante que iniciou o fluxo de trabalho. O código usa a mesma lógica do script de amostra (`initiator-participant-chooser.ecma`).

O `@Property` a anotação define o valor da variável `SERVICE_PROPERTY_LABEL` campo para `Workflow Initiator Participant Chooser`.

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

No **Etapa dinâmica do participante** caixa de diálogo de propriedades, a **Seletor de participante** lista inclui o item `Workflow Initiator Participant Chooser (script)`, que representa esse serviço.

Quando o modelo de fluxo de trabalho é iniciado, o log indica a ID do usuário que iniciou o fluxo de trabalho e a quem foi atribuído o item de trabalho. Neste exemplo, a variável `admin` usuário iniciou o fluxo de trabalho.

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### Etapa de participante do formulário {#form-participant-step}

O **Etapa do participante do formulário** apresenta um formulário quando o item de trabalho é aberto. Quando o usuário preenche e envia o formulário, os dados do campo são armazenados nos nós da carga útil do workflow.

Para configurar a etapa, especifique o grupo ou usuário ao qual o item de trabalho será atribuído e o caminho para o formulário.

>[!CAUTION]
>
>Esta seção trata do [Seção Forms de componentes básicos para criação de página](/help/sites-authoring/default-components-foundation.md#form).

#### Etapa do participante do formulário - Configuração {#form-participant-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* [Usuário/Grupo](#step-properties-user-group-tab)
* **Formulário**

   * **Caminho do formulário**: O caminho para o [formulário que você criar](#form-participant-step-creating-the-form).

#### Etapa do participante do formulário - Criação do formulário {#form-participant-step-creating-the-form}

Crie um formulário para uso com um **Etapa do participante do formulário** normalmente. No entanto, os formulários para uma etapa do participante do formulário devem ter as seguintes configurações:

* O **Início do formulário** o componente deve ter o **Tipo de ação** propriedade definida como `Edit Workflow Controlled Resource(s)`.
* O **Início do formulário** O componente deve ter um valor para a variável `Form Identifier` propriedade.
* Os componentes do formulário devem ter a variável **Nome do elemento** propriedade definida para o caminho do nó onde os dados do campo são armazenados. O caminho deve localizar um nó no conteúdo do payload do workflow. O valor usa o seguinte formato:

   `./jcr:content/path_to_node`

* O formulário deve incluir um **Botão(s) de envio de fluxo de trabalho** componente. Você não configura nenhuma propriedade do componente.

Os requisitos do fluxo de trabalho determinam onde você deve armazenar dados de campo. Por exemplo, os dados de campo podem ser usados para configurar as propriedades do conteúdo da página. O seguinte valor de um **Nome do elemento** A propriedade armazena dados de campo como o valor da variável `redirectTarget` da `jcr:content` nó:

`./jcr:content/redirectTarget`

No exemplo a seguir, os dados do campo são usados como o conteúdo de um **Texto** componente na página de carga útil:

`./jcr:content/par/text_3/text`

O primeiro exemplo pode ser usado para qualquer página que a variável `cq:Page` renderizadores de componentes. O segundo exemplo só pode ser usado quando a página de carga inclui um **Texto** componente que tem uma ID de `text_3`.

O formulário pode ser localizado em qualquer lugar no repositório, no entanto, os usuários do workflow devem estar autorizados a ler o formulário.

### Seletor de participante aleatório {#random-participant-chooser}

O **Seletor de participante aleatório** etapa é um seletor de participante que atribui o item de trabalho gerado a um usuário que é selecionado aleatoriamente em uma lista.

![wf-31](assets/wf-31.png)

#### Seletor de participante aleatório - Configuração {#random-participant-chooser-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* **Argumentos**

   * **Participantes**: Especifica a lista de usuários disponíveis para seleção. Para adicionar um usuário à lista, clique em **Adicionar item** e digite o caminho inicial do nó do usuário ou a ID do usuário. A ordem dos usuários não afeta a probabilidade de receber um item de trabalho.

### Seletor do participante iniciador do fluxo de trabalho {#workflow-initiator-participant-chooser}

O **Seletor de Participante Iniciador de Fluxo de Trabalho** etapa é um seletor de participante que atribui o item de trabalho gerado ao usuário que iniciou o fluxo de trabalho. Não há outras propriedades a serem configuradas além do **Frequentes** propriedades.

#### Seletor de Participante Iniciador do Fluxo de Trabalho - Configuração {#workflow-initiator-participant-chooser-configuration}

Para configurar a etapa, edite usando as seguintes guias:

* [Comum](#step-properties-common-tab)

## Etapa do processo {#process-step}

A **Etapa do processo** O executa um ECMAScript ou chama um serviço OSGi para executar processamento automático.

![wf-32](assets/wf-32.png)

### Etapa do processo - Configuração {#process-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* **Processo**

   * **Processo**: A implementação do processo a ser executada. Use o menu suspenso para selecionar o serviço ECMAScript ou OSGi. Para obter informações sobre:

      * Os serviços ECMAScripts e OSGi padrão, consulte [Processos incorporados para etapas do processo](/help/sites-developing/workflows-process-ref.md).
      * Criando ECMAScripts para uma etapa do Processo, consulte [Implementando uma etapa do processo com um ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * Criando serviços OSGi para uma etapa do Processo, consulte [Implementar uma etapa do processo com uma classe Java](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class).
   * **Avanço do Manipulador**: Selecione essa opção para avançar automaticamente o workflow para a próxima etapa após a execução. Se não estiver selecionado, o script de implementação deve lidar com a evolução do fluxo de trabalho.
   * **Argumentos**: Argumentos a serem passados para o processo.


## Definir variável {#set-variable}

A etapa Definir variável permite definir o valor de uma variável e a ordem em que os valores são definidos. A variável é definida na ordem em que os mapeamentos de variável são listados na etapa Definir variável .

![Adicionar mapeamento para definir uma variável](assets/set_variable_addmappingnew.png)

### Definir variável - Configuração {#setvariable}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **Mapeamento**

   * **Selecionar variável:** Use essa opção para selecionar uma variável para definir seu valor.
   * **Selecione o Modo de Mapeamento:** Selecione um modo de mapeamento para definir o valor da variável. Dependendo do tipo de dados da variável, você pode usar as seguintes opções para definir o valor de uma variável:

      * **Literal:** Use a opção quando souber o valor exato a ser especificado.
      * **Expressão:** Use a opção quando o valor a ser usado for calculado com base em uma expressão. A expressão é criada no editor de expressão fornecido.
      * **Notação de ponto JSON:** Use a opção para recuperar um valor de uma variável do tipo JSON ou FDM.
      * **XPATH:** Use a opção para recuperar um valor de uma variável do tipo XML.
      * **Em relação à carga:** Use a opção quando o valor a ser salvo na variável estiver disponível em um caminho relativo à carga útil.
      * **Caminho absoluto:** Use a opção quando o valor a ser salvo na variável estiver disponível em um caminho absoluto.
   * **Especificar valor:** Especifique um valor para mapear para a variável. O valor especificado nesse campo depende do modo de mapeamento.
   * **Adicionar mapeamento:** Use esta opção para adicionar mais mapeamentos para definir um valor para a variável.
