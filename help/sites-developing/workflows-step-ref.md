---
title: Referência da etapa do fluxo de trabalho
seo-title: Referência da etapa do fluxo de trabalho
description: 'null'
seo-description: 'null'
uuid: 88bf6997-73a1-4639-82aa-5dff08d3ef86
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e3afffd0-d90c-4bd0-b814-f7aeac6ceb6d
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Referência da etapa do fluxo de trabalho {#workflow-step-reference}

Os modelos de fluxo de trabalho consistem em uma série de etapas de vários tipos. De acordo com o tipo, essas etapas podem ser configuradas e estendidas com parâmetros e scripts para fornecer a funcionalidade e o controle necessários.

>[!NOTE]
>
>Esta seção aborda as etapas padrão do Fluxo de trabalho.
>
>Para ver as etapas específicas do módulo, consulte também:
>
>* [Referência da etapa do fluxo de trabalho do AEM Forms](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [Processando ativos usando manipuladores de mídia e fluxos de trabalho](/help/assets/media-handlers.md)
>



## Propriedades da etapa {#step-properties}

Cada componente de etapa tem uma caixa de diálogo Propriedades **da** etapa que permite definir e editar as propriedades necessárias.

### Propriedades da etapa - guia Comum {#step-properties-common-tab}

Uma combinação das seguintes propriedades está disponível para a maioria dos componentes da etapa do fluxo de trabalho, na guia **Comum** da caixa de diálogo de propriedades:

* **Título** O título da etapa.

* **Descrição** Uma descrição da etapa.

* **Estágio do fluxo de trabalho**

   Um seletor suspenso para aplicar um [Palco](/help/sites-developing/workflows.md#workflow-stages) à etapa.

* **Tempo limite**

   O período após o qual a etapa será &quot;atingida&quot;.
Você pode selecionar entre: **Desligado**, **Imediato**, **1h**, **6h**, **12h******, 24h.

* **Tempo limite do Handler**

   O manipulador que controlará o fluxo de trabalho quando a etapa expirar; por exemplo:
   `Auto Advancer`

* **Handler avançado**

   Selecione essa opção para avançar automaticamente o fluxo de trabalho para a próxima etapa após a execução. Se não estiver selecionado, o script de implementação deve lidar com a evolução do fluxo de trabalho.

### Propriedades da etapa - guia Usuário/grupo {#step-properties-user-group-tab}

As seguintes propriedades estão disponíveis para vários componentes de etapa do fluxo de trabalho, na guia **Usuário/Grupo** da caixa de diálogo de propriedades:

* **Notificar usuário via e-mail**

   * Você pode notificar os participantes enviando-lhes um email quando o fluxo de trabalho chegar à etapa.
   * Se ativado, um email será enviado para o usuário definido pela propriedade **Usuário/Grupo** ou para cada membro do grupo, se um grupo for definido.

* **Usuário/Grupo**

   * Uma caixa de seleção suspensa permitirá que você navegue e selecione um usuário ou grupo.
   * Se você atribuir a etapa a um usuário específico, somente esse usuário poderá executar uma ação na etapa.
   * Se você atribuir a etapa a um grupo inteiro, então quando o fluxo de trabalho atingir essa etapa, todos os usuários desse grupo terão a ação em sua Caixa de entrada **de fluxo de trabalho**.
   * Consulte [Participação em fluxos de trabalho](/help/sites-authoring/workflows-participating.md) para obter mais informações.

## E dividir {#and-split}

A divisão **AND** cria uma divisão no fluxo de trabalho, após a qual ambas as ramificações estarão ativas. Você adiciona etapas de fluxo de trabalho a cada ramificação, conforme necessário. Essa etapa permite que você introduza vários caminhos de processamento no fluxo de trabalho. Por exemplo, você pode permitir que determinadas etapas de revisão ocorram em paralelo, economizando tempo.

![wf-26](assets/wf-26.png)

### E dividir - Configuração {#and-split-configuration}

Para configurar a divisão:

* Edite as propriedades **de divisão** E:

   * **Nome** da divisão: atribuir um nome para fins explicativos
   * Selecionar o número de ramificações necessárias; 2, 3, 4 ou 5.

* Adicione etapas de fluxo de trabalho às ramificações, conforme necessário.

   ![wf-27](assets/wf-27.png)

## Etapa do contêiner {#container-step}

Uma etapa de contêiner inicia outro modelo de fluxo de trabalho que é executado como um fluxo de trabalho filho.

Esse contêiner pode permitir que você reutilize modelos de fluxo de trabalho para implementar sequências comuns de etapas. Por exemplo, um modelo de fluxo de trabalho de tradução poderia ser usado em vários fluxos de trabalho de edição.

![wf-28](assets/wf-28.png)

### Etapa do contêiner - Configuração {#container-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* **Container**

   * **Sub fluxo de trabalho**: Selecione o fluxo de trabalho para iniciar.

## Etapa Ir para {#goto-step}

A Etapa **** Ir para permite especificar a próxima etapa a ser executada no modelo de fluxo de trabalho. Você pode especificar uma definição de regra, um script externo ou um script ECMA como a expressão de roteamento para avaliar a próxima etapa do modelo de fluxo de trabalho.

* Se a condição especificada for verdadeira, a Etapa **** Ir para será concluída e o mecanismo de fluxo de trabalho executará a etapa especificada.
* Se a condição especificada não for verdadeira, a Etapa **Ir para** será concluída e a lógica normal de roteamento determinará a próxima etapa a ser executada.

A Etapa **Ir para** permite implementar estruturas avançadas de roteamento nos modelos de fluxo de trabalho. Por exemplo, para implementar um loop, a Etapa **** Ir para pode ser definida para executar uma etapa anterior no fluxo de trabalho, com a expressão de roteamento avaliando uma condição de loop.

### Etapa Ir para - Configuração {#goto-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* **Processo**

   * **Etapa** de destino: Selecione a etapa a ser executada após avaliar a condição da expressão de roteamento.
   * **Expressão** de roteamento: Selecione Definição de regra, Script externo ou um script ECMA que determina se a Etapa **** de destino deve ser executada.

      * **** Definição de regra: Use o editor [de](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) expressões para definir a regra.
      * **** Script externo: O caminho do script externo.
      * **Script** ECMA: O script que determina se a Etapa **Ir para será executada**.

#### Simulação de um Loop for {#simulating-a-for-loop}

A simulação de um loop for requer a manutenção de uma contagem do número de iterações de loop que ocorreram:

* A contagem geralmente representa um índice de itens que são acionados no fluxo de trabalho.
* A contagem é avaliada como o critério de saída do loop.

Por exemplo, para implementar um fluxo de trabalho que executa uma ação em vários nós JCR, você pode usar um contador de loop como índice para os nós. Para persistir na contagem, armazene um `integer` valor no mapa de dados da instância do fluxo de trabalho. Use o script da Etapa **** Ir para incrementar a contagem, bem como para comparar a contagem com os critérios de saída.

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

Também é possível simular um loop for usando a Definição de regra como a expressão de roteamento. [Crie uma variável **de** contagem](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) do tipo de dados Longo. Use a **Expressão** como modo de mapeamento na etapa **[Definir variável](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)**para definir o valor da variável de **contagem**para **contar + 1**em cada execução da etapa **Definir variável**.

![Simulação de um loop for](assets/variable_use_case_count_new.png)

Na Etapa **** Ir para, use **Definir variável** como a Etapa **** de destino e **conte &lt; 5** como a expressão de roteamento.

![Condição para simular um loop For](assets/variable_use_case_count1_new.png)

A etapa **Definir variável** é executada repetidamente, aumentando o valor da variável de **contagem** em 1 em cada execução até que o valor atinja 5.

## OU dividir {#or-split}

A divisão **OU** cria uma divisão no fluxo de trabalho, após a qual apenas uma ramificação estará ativa. Esta etapa permite que você introduza caminhos de processamento condicional no seu fluxo de trabalho. Você adiciona etapas de fluxo de trabalho a cada ramificação, conforme necessário.

>[!NOTE]
>
>Para obter informações adicionais sobre como criar uma divisão OR, consulte: [https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html](https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html)

![Ramificação usando OU Dividir](assets/variables_orsplit_new.png)

### OU Dividir - Configuração {#or-split-configuration}

Para configurar a divisão:

* Edite as propriedades **OU dividir**:

   * **Comum**

      * Especifique o nome da divisão.
   * **Ramificações (*x)***

      * **** Adicionar Ramificação: Adicione mais ramificações à etapa.
      * **Selecione Expressão** de Roteamento: Selecione a expressão de roteamento para avaliar a ramificação ativa. Os valores possíveis incluem: Definição de regra, Script externo e script ECMA.
      * **Clique para Adicionar expressão**: Adicione uma expressão para avaliar a ramificação ativa se você selecionar Definição **de** regra como a expressão de roteamento.
      * **Caminho** do script: O caminho para um arquivo que contém o script para avaliar a ramificação ativa se você selecionar Script **** externo como a expressão de roteamento.
      * **Script**: Adicione o script na caixa para avaliar a ramificação ativa se você selecionar Script **** ECMA como a expressão de roteamento.
      * **Rota** padrão: A ramificação padrão é seguida no caso de várias ramificações. Você pode especificar somente uma ramificação como padrão.
   >[!NOTE]
   >
   >    * Uma ramificação é avaliada de cada vez com base na expressão de roteamento.
   >    * As ramificações são avaliadas de cima para baixo.
   >    * O primeiro script avaliado como true é executado.
   >    * Se nenhuma ramificação for avaliada como true, o fluxo de trabalho não avançará.


   >[!NOTE]
   >
   >Consulte [Definindo uma regra para uma divisão](/help/sites-developing/workflows-models.md#defineruleecmascript)OR.

* Adicione etapas de fluxo de trabalho às ramificações, conforme necessário.

## Etapas e opções do participante {#participant-steps-and-choosers}

### Etapa do participante {#participant-step}

Uma Etapa **de** participante permite que você atribua propriedade para uma ação específica. O fluxo de trabalho só continuará quando o usuário tiver confirmado manualmente a etapa. Isso é usado quando você deseja que alguém execute uma ação no fluxo de trabalho; por exemplo, uma etapa de revisão.

Embora não esteja diretamente relacionada, a autorização do utilizador deve ser considerada ao atribuir uma ação; o usuário deve ter acesso à página que é a carga do fluxo de trabalho.

#### Etapa do participante - Configuração {#participant-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* [Usuário/Grupo](#step-properties-user-group-tab)

>[!NOTE]
>
>O iniciador do fluxo de trabalho é sempre notificado quando:
>
>* O fluxo de trabalho está concluído (concluído).
>* O fluxo de trabalho é abortado (encerrado).
>



>[!NOTE]
>
>Algumas propriedades precisam ser configuradas para habilitar notificações por email. Você também pode personalizar o modelo de email ou adicionar um modelo de email para um novo idioma. See [Configuring Email Notification](/help/sites-administering/notification.md#configuringemailnotification) to configure email notifications in AEM.

### Etapa do participante do diálogo {#dialog-participant-step}

Use uma Etapa **Participante da** caixa de diálogo para coletar informações do usuário ao qual o item de trabalho foi atribuído. Essa etapa é útil para coletar pequenas quantidades de dados que são usadas posteriormente no fluxo de trabalho.

Ao concluir a etapa, a caixa de diálogo **Concluir item** de trabalho contém os campos que você define na caixa de diálogo. Os dados coletados nos campos são armazenados nos nós da carga do fluxo de trabalho. As etapas subsequentes do fluxo de trabalho podem ler o valor do repositório.

Para configurar a etapa, especifique o grupo ou usuário ao qual o item de trabalho será atribuído e o caminho para a caixa de diálogo.

#### Etapa do participante da caixa de diálogo - Configuração {#dialog-participant-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* [Usuário/Grupo](#step-properties-user-group-tab)
* **Caixa de diálogo**

   * **Caminho** da caixa de diálogo: O caminho para o nó de diálogo da [caixa de diálogo criada](#dialog-participant-step-creating-a-dialog).

#### Etapa do participante da caixa de diálogo - Criar uma caixa de diálogo {#dialog-participant-step-creating-a-dialog}

Para criar uma caixa de diálogo, é necessário criar a caixa de diálogo:

* Decida onde os dados resultantes serão [armazenados na carga](#dialog-participant-step-storing-data-in-the-payload).
* [Definir a caixa de diálogo; isso inclui a definição dos campos usados para coletar (e salvar) os dados](#dialog-participant-step-dialog-definition).

#### Etapa do participante da caixa de diálogo - Armazenamento de dados na carga {#dialog-participant-step-storing-data-in-the-payload}

Você pode armazenar dados de widget na carga do fluxo de trabalho ou nos metadados do item de trabalho. O formato da `name` propriedade do nó do widget determina onde os dados são armazenados.

* **Armazenar dados com a carga**

   * Para armazenar dados de widget como uma propriedade da carga do fluxo de trabalho, use o seguinte formato para o valor da propriedade name do nó do widget:
      `./jcr:content/nodename`

   * Os dados são armazenados na `nodename` propriedade do nó de carga. Se o nó não contiver essa propriedade, a propriedade será criada.
   * Quando armazenado com a carga, os usos subsequentes da caixa de diálogo com a mesma carga sobrescreve o valor da propriedade.

* **Armazenar dados com o item de trabalho**

   * Para armazenar dados de widget como uma propriedade dos metadados de item de trabalho, use o seguinte formato para o valor da propriedade name:
      `nodename`

   * Os dados são armazenados na `nodename` propriedade do item de trabalho `metadata`. Os dados são preservados se a caixa de diálogo for usada subsequentemente com a mesma carga.

#### Etapa do participante da caixa de diálogo - Definição da caixa de diálogo {#dialog-participant-step-dialog-definition}

1. **Estrutura de diálogo**

   As caixas de diálogo para Etapas do participante da caixa de diálogo são semelhantes às caixas de diálogo criadas para componentes de criação. São armazenados em:

   `/apps/myapp/workflow/dialogs`

   As caixas de diálogo para a interface de usuário padrão e habilitada para toque têm a seguinte estrutura de nó:

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

   A Etapa **Participante da** caixa de diálogo tem a propriedade Caminho **da** caixa de diálogo (juntamente com as propriedades de uma Etapa [](#participant-step)Participante). O valor da propriedade Caminho **da** caixa de diálogo é o caminho para o `dialog` nó da caixa de diálogo.

   Por exemplo, a caixa de diálogo está contida em um componente chamado `EmailWatch` que está armazenado no nó:

   `/apps/myapp/workflows/dialogs`

   Para a interface habilitada para toque, o seguinte valor é usado para a propriedade Caminho **da** caixa de diálogo:

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **Exemplo de definição de caixa de diálogo**

   O trecho de código XML a seguir representa uma caixa de diálogo que armazena um `String` valor no `watchEmail` nó do conteúdo da carga. O nó de título representa o componente [TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) :

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

   Esse exemplo resultará em uma caixa de diálogo, como:

   ![chlimage_1-70](assets/chlimage_1-70.png)

### Etapa dinâmica do participante {#dynamic-participant-step}

O componente Etapa **dinâmica do participante é semelhante à Etapa** do **[](#participant-step)**participante com a diferença de que o participante é selecionado automaticamente em tempo de execução.

Para configurar a etapa, selecione um Seletor **de** participantes que identifique o participante ao qual atribuir o item de trabalho, juntamente com uma caixa de diálogo.

#### Etapa dinâmica do participante - Configuração {#dynamic-participant-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* **Seletor de participantes**

   * **Seletor** de participantes: O nome do seletor de [participantes criado](#developingtheparticipantchooser).
   * **Argumentos**: Quaisquer argumentos necessários.
   * **Email**: Se uma notificação por email deve ser enviada ao usuário.

* **Caixa de diálogo**

   * **Caminho** da caixa de diálogo: O caminho para o nó de diálogo da [caixa de diálogo criada (como na Etapa **Participante da** caixa de diálogo)](#dialog-participant-step-creating-a-dialog).

#### Etapa dinâmica do participante - Desenvolvimento do seletor de participantes {#dynamic-participant-step-developing-the-participant-chooser}

Crie o seletor de participantes. Portanto, você pode usar qualquer lógica ou critério de seleção. Por exemplo, o selecionador de participantes pode selecionar o usuário (dentro de um grupo) que tem menos itens de trabalho. Você pode criar qualquer número de selecionadores de participantes para usar com diferentes instâncias do componente Etapa **do participante** dinâmico em seus modelos de fluxo de trabalho.

Crie um serviço OSGi ou um ECMAScript que selecione um usuário ao qual atribuir o item de trabalho.

* **ECMAscript**

   Os scripts devem incluir uma função chamada getParticipant que retorna uma ID de usuário como um `String` valor. Armazene scripts personalizados em, por exemplo, a `/apps/myapp/workflow/scripts` pasta ou uma subpasta.

   Um script de amostra é incluído em uma instância padrão do AEM:

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >Você não ***deve*** alterar nada no `/libs` caminho.
   >
   >
   >Isso ocorre porque o conteúdo do é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar uma correção ou um pacote de recursos). `/libs`

   Este script seleciona o iniciador do fluxo de trabalho como participante:

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >O componente Seletor **de Participantes do Iniciador de** Fluxo de Trabalho estende a Etapa **de Participante** Dinâmico e usa esse script como a implementação da etapa.

* **Serviço OSGi**

   Os serviços devem implementar a interface [com.day.cq.workflow.exec.ParticipantStepChooser](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) . A interface define os seguintes membros:

   * `SERVICE_PROPERTY_LABEL` campo: Use esse campo para especificar o nome do seletor de participantes. O nome aparece em uma lista de selecionadores de participantes disponíveis nas propriedades Etapa **** dinâmica do participante.

   * `getParticipant` método: Retorna a ID Principal dinamicamente resolvida como um `String` valor.
   >[!CAUTION]
   >
   >O `getParticipant` método retorna a ID Principal dinamicamente resolvida. Isso pode ser uma ID de grupo ou de usuário.
   >
   >
   >No entanto, uma ID de grupo só pode ser usada para uma Etapa **de** participante quando uma lista de participantes for retornada. Para uma Etapa **de participante** dinâmico, uma lista vazia é retornada e não pode ser usada para delegação.

   Para disponibilizar sua implementação para os componentes Etapa **do participante** dinâmico, adicione sua classe Java a um pacote OSGi que exporta o serviço e implante o pacote no servidor AEM.

   >[!NOTE]
   >
   >**O Seletor** de Participantes Aleatórios é um serviço de exemplo que seleciona um usuário aleatório ( `com.day.cq.workflow.impl.process.RandomParticipantChooser`). A amostra do componente **Random Participant** Chooser estende a Etapa **** Dinâmica do Participante e usa esse serviço como a implementação da etapa.

#### Etapa dinâmica do participante - Exemplo de serviço do seletor de participantes {#dynamic-participant-step-example-participant-chooser-service}

A classe Java a seguir implementa a `ParticipantStepChooser` interface. A classe retorna o nome do participante que iniciou o fluxo de trabalho. O código usa a mesma lógica que o script de amostra (`initiator-participant-chooser.ecma`) usa.

A `@Property` anotação define o valor do `SERVICE_PROPERTY_LABEL` campo como `Workflow Initiator Participant Chooser`.

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

Na caixa de diálogo de propriedades Etapa **dinâmica do participante, a lista Seletor** de **participantes inclui o item** `Workflow Initiator Participant Chooser (script)`, que representa esse serviço.

Quando o modelo de fluxo de trabalho é iniciado, o log indica a ID do usuário que iniciou o fluxo de trabalho e quem recebeu o item de trabalho. Neste exemplo, o `admin` usuário iniciou o fluxo de trabalho.

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### Etapa de participante do formulário {#form-participant-step}

A Etapa **Participante do** formulário apresenta um formulário quando o item de trabalho é aberto. Quando o usuário preenche e envia o formulário, os dados do campo são armazenados nos nós da carga do fluxo de trabalho.

Para configurar a etapa, especifique o grupo ou usuário ao qual o item de trabalho será atribuído e o caminho para o formulário.

>[!CAUTION]
>
>Esta seção trata da seção [Formulários dos Componentes do Foundation para a Criação](/help/sites-authoring/default-components-foundation.md#form)de Página.

#### Etapa do participante do formulário - Configuração {#form-participant-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* [Usuário/Grupo](#step-properties-user-group-tab)
* **Formulário**

   * **Caminho** do formulário: O caminho para o [formulário criado](#form-participant-step-creating-the-form).

#### Etapa do participante do formulário - Criação do formulário {#form-participant-step-creating-the-form}

Crie um formulário para uso com uma Etapa **de participante de** formulário como normal. No entanto, os formulários para uma Etapa do participante do formulário devem ter as seguintes configurações:

* O componente **Início do formulário** deve ter a propriedade Tipo **de** ação definida como `Edit Workflow Controlled Resource(s)`.
* O componente **Início do formulário** deve ter um valor para a `Form Identifier` propriedade.
* Os componentes do formulário devem ter a propriedade Nome **do** elemento definida como o caminho do nó onde os dados do campo são armazenados. O caminho deve localizar um nó no conteúdo de carga do fluxo de trabalho. O valor usa o seguinte formato:

   `./jcr:content/path_to_node`

* O formulário deve incluir um componente Botões de envio de **fluxo de trabalho** . Você não configura nenhuma propriedade do componente.

Os requisitos do seu fluxo de trabalho determinam onde você deve armazenar dados de campo. Por exemplo, dados de campo podem ser usados para configurar as propriedades do conteúdo da página. O seguinte valor de uma propriedade Nome **de** elemento armazena dados de campo como o valor da `redirectTarget` propriedade do `jcr:content` nó:

`./jcr:content/redirectTarget`

No exemplo a seguir, os dados de campo são usados como conteúdo de um componente de **Texto** na página de carga:

`./jcr:content/par/text_3/text`

O primeiro exemplo pode ser usado para qualquer página que o `cq:Page` componente renderizar. O segundo exemplo só pode ser usado quando a página de carga inclui um componente de **Texto** com uma ID de `text_3`.

O formulário pode ser localizado em qualquer lugar no repositório, no entanto, os usuários do fluxo de trabalho devem estar autorizados a ler o formulário.

### Seletor de participante aleatório {#random-participant-chooser}

A etapa Seletor de participantes **aleatórios** é um seletor de participantes que atribui o item de trabalho gerado a um usuário que é selecionado aleatoriamente em uma lista.

![wf-31](assets/wf-31.png)

#### Seletor de participantes aleatórios - Configuração {#random-participant-chooser-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* **Argumentos**

   * **Participantes**: Especifica a lista de usuários disponíveis para seleção. Para adicionar um usuário à lista, clique em **Adicionar item** e digite o caminho inicial do nó do usuário ou a ID do usuário. A ordem dos usuários não afeta a probabilidade de serem atribuídos a um item de trabalho.

### Seletor do participante iniciador do fluxo de trabalho {#workflow-initiator-participant-chooser}

A etapa do Seletor **de Participantes do Iniciador de** Fluxo de Trabalho é um selecionador de participantes que atribui o item de trabalho gerado ao usuário que iniciou o fluxo de trabalho. Não há propriedades para configurar além das propriedades **Comuns** .

#### Workflow Initiator Participant Chooser - Configuration {#workflow-initiator-participant-chooser-configuration}

Para configurar a etapa, edite usando as seguintes guias:

* [Comum](#step-properties-common-tab)

## Etapa do processo {#process-step}

Uma Etapa **do** processo executa um ECMAScript ou chama um serviço OSGi para executar processamento automático.

![wf-32](assets/wf-32.png)

### Etapa do processo - Configuração {#process-step-configuration}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](#step-properties-common-tab)
* **Processo**

   * **Processo**: A implementação do processo a ser executada. Use o menu suspenso para selecionar o serviço ECMAScript ou OSGi. Para obter informações sobre:

      * Os serviços ECMAScripts e OSGi padrão, consulte Processos [incorporados para etapas](/help/sites-developing/workflows-process-ref.md)do processo.
      * Criando ECMAScripts para uma etapa do Processo, consulte [Implementação de uma Etapa do Processo com um ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * Criando serviços OSGi para uma etapa do Processo, consulte [Implementação de uma Etapa do Processo com uma Classe](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class)Java.
   * **Avanço** do manipulador:Selecione essa opção para avançar automaticamente o fluxo de trabalho para a próxima etapa após a execução. Se não estiver selecionado, o script de implementação deve lidar com a evolução do fluxo de trabalho.
   * **Argumentos**: Argumentos a serem passados ao processo.


## Definir variável {#set-variable}

A etapa Definir variável permite definir o valor de uma variável e definir a ordem na qual os valores são definidos. A variável é definida na ordem em que os mapeamentos da variável são listados na etapa Definir variável.

![Adicionar mapeamento para definir uma variável](assets/set_variable_addmappingnew.png)

### Definir variável - Configuração {#setvariable}

Para configurar a etapa, edite e use as seguintes guias:

* [Comum](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **Mapeamento**

   * **** Selecionar variável: Use essa opção para selecionar uma variável para definir seu valor.
   * **** Selecione o modo de mapeamento: Selecione um modo de mapeamento para definir o valor da variável. Dependendo do tipo de dados da variável, você pode usar as seguintes opções para definir o valor de uma variável:

      * **** Literal: Use a opção quando souber o valor exato a ser especificado.
      * **** Expressão: Use a opção quando o valor a ser usado for calculado com base em uma expressão. A expressão é criada no editor de expressões fornecido.
      * **** Notação de ponto JSON: Use a opção para recuperar um valor de uma variável do tipo JSON ou FDM.
      * **** XPATH: Use a opção para recuperar um valor de uma variável de tipo XML.
      * **** Em relação à carga: Use a opção quando o valor a ser salvo na variável estiver disponível em um caminho relativo à carga.
      * **** Caminho absoluto: Use a opção quando o valor a ser salvo na variável estiver disponível em um caminho absoluto.
   * **** Especificar valor: Especifique um valor para mapear para a variável. O valor especificado nesse campo depende do modo de mapeamento.
   * **** Adicionar mapeamento: Use essa opção para adicionar mais mapeamentos para definir um valor para a variável.
