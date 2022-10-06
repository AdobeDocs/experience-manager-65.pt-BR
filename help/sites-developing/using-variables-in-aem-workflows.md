---
title: Variáveis em workflows AEM
seo-title: Variables in AEM Workflows
description: Crie uma variável, defina um valor para a variável e use-a em OU Dividir e Ir para AEM etapas do fluxo de trabalho.
seo-description: Create a variable, set a value for the variable, and use it in OR Split and  Goto AEM workflow steps.
uuid: cc62ff11-51d4-4db4-9c6d-5dc2caa1da52
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: bbb9936e-ecd2-44b3-b4ae-dd62a3160641
docset: aem65
exl-id: c8aeceec-860c-49ee-b681-d7107e52020d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 0%

---

# Variáveis em workflows AEM{#variables-in-aem-workflows}

Uma variável em um modelo de fluxo de trabalho é uma maneira de armazenar um valor com base em seu tipo de dados. Em seguida, você pode usar o nome da variável em qualquer etapa do fluxo de trabalho para recuperar o valor armazenado na variável . Também é possível usar nomes de variáveis para definir expressões para tomar decisões de roteamento.

Em AEM modelos de fluxo de trabalho, você pode:

* [Criar uma variável](/help/sites-developing/using-variables-in-aem-workflows.md#create-a-variable) de um tipo de dados com base no tipo de informação que você deseja armazenar nele.
* [Defina um valor para a variável](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable) usando a etapa de fluxo de trabalho Definir variável .
* [Usar a variável](/help/sites-developing/using-variables-in-aem-workflows.md#use-a-variable) em OR Split e Goto AEM etapas do fluxo de trabalho para definir uma expressão para tomar decisões de roteamento. Também é possível usar variáveis em todas as etapas do fluxo de trabalho do AEM Forms.

O vídeo a seguir demonstra como você pode criar, definir e usar variáveis em AEM modelos de fluxo de trabalho:

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/usevariables_example.mp4)

As variáveis são uma extensão do [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) interface. Você pode usar [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) no ECMAScript para acessar metadados salvos usando variáveis.

## Criar uma variável {#create-a-variable}

Você cria variáveis usando a seção Variáveis disponível no sidekick do modelo de fluxo de trabalho. AEM variáveis de fluxo de trabalho são compatíveis com os seguintes tipos de dados:

* **Tipos de dados primitivos**: Longo, duplo, booleano, data e string
* **Tipos de dados complexos**: [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html) e [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)

>[!NOTE]
>
>Os fluxos de trabalho suportam apenas o formato ISO8601 para variáveis do tipo Data .

Para obter tipos de dados complexos adicionais disponíveis nos fluxos de trabalho do AEM Forms, consulte [Variáveis em workflows do AEM Forms](/help/forms/using/variable-in-aem-workflows.md).  Use o tipo de dados ArrayList para criar coleções de variáveis. É possível criar uma variável ArrayList para todos os tipos de dados primitivos e complexos. Por exemplo, crie uma variável ArrayList e selecione String como subtipo para armazenar vários valores de string usando a variável .

Execute as seguintes etapas para criar uma variável:

1. Em uma instância AEM, navegue até Ferramentas > Fluxo de trabalho > Modelos.
1. Toque **[!UICONTROL Criar]** e especifique o título e um nome opcional para o modelo de fluxo de trabalho. Selecione o modelo e toque em **[!UICONTROL Editar]**.
1. Toque no ícone de variáveis disponíveis no sidekick do modelo de fluxo de trabalho e toque em **[!UICONTROL Adicionar variável]**.

   ![Adicionar variável](assets/variables_add_variable_new.png)

1. Na caixa de diálogo Adicionar variável , especifique o nome e selecione o tipo da variável.
1. Selecione o tipo de dados no **[!UICONTROL Tipo]** e especifique os seguintes valores:

   * Tipo de dados primitivos - Especifique um valor padrão opcional para a variável.
   * JSON ou XML - especifique um caminho de esquema JSON ou XML opcional. O sistema valida o caminho do esquema ao mapear e armazenar as propriedades disponíveis nesse esquema para outra variável.
   * Modelo de dados de formulário - Especifique um caminho de Modelo de dados de formulário.
   * ArrayList - especifique um subtipo para a coleção.

1. Especifique uma descrição opcional para a variável e toque em ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) para salvar as alterações. A variável é exibida na lista disponível no painel esquerdo.

Ao criar variáveis, considere as seguintes práticas:

* Crie quantas variáveis forem necessárias para um fluxo de trabalho. No entanto, para conservar os recursos do banco de dados, use o número mínimo de variáveis necessárias e reutilize variáveis quando possível.
* As variáveis fazem distinção entre maiúsculas e minúsculas. Certifique-se de fazer referência às variáveis usando as mesmas letras maiúsculas e minúsculas no fluxo de trabalho.
* Evite usar caracteres especiais no nome da variável

## Definir uma variável {#set-a-variable}

Você pode usar a etapa Definir variável para definir o valor de uma variável e a ordem em que os valores são definidos. A variável é definida na ordem em que os mapeamentos de variável são listados na etapa Definir variável .

As alterações nos valores da variável afetam apenas a instância do processo em que a alteração ocorre. Por exemplo, quando um workflow é iniciado e os dados variáveis são alterados, as alterações afetam somente essa instância do workflow. As alterações não afetam outras instâncias do fluxo de trabalho que foram iniciadas anteriormente ou são iniciadas subsequentemente.

Dependendo do tipo de dados da variável, você pode usar as seguintes opções para definir o valor de uma variável:

* **Literal:** Use a opção quando souber o valor exato a ser especificado.
* **Expressão:** Use a opção quando o valor a ser usado for calculado com base em uma expressão. A expressão é criada no editor de expressão fornecido.
* **Notação de ponto JSON:** Use a opção para recuperar um valor de uma variável do tipo JSON ou FDM.
* **XPATH:** Use a opção para recuperar um valor de uma variável do tipo XML.
* **Em relação à carga:** Use a opção quando o valor a ser salvo na variável estiver disponível em um caminho relativo à carga útil.
* **Caminho absoluto:** Use a opção quando o valor a ser salvo na variável estiver disponível em um caminho absoluto.

Você também pode atualizar elementos específicos de uma variável do tipo JSON ou XML usando notação JSON DOT ou notação XPATH.

### Adicionar mapeamento entre variáveis {#add-mapping-between-variables}

Execute as seguintes etapas para adicionar o mapeamento entre as variáveis:

1. Na página de edição do fluxo de trabalho, toque no ícone Etapas disponível no sidekick do modelo de fluxo de trabalho.
1. Arraste e solte a **Definir variável** para acessar o editor de fluxo de trabalho, toque na etapa e selecione ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) (Configurar).
1. Na caixa de diálogo Definir variável , selecione **[!UICONTROL Mapeamento]** > **[!UICONTROL Adicionar mapeamento]**.
1. No **Variável de mapa** selecione a variável para armazenar dados, selecione o modo de mapeamento e especifique um valor a ser armazenado na variável . Os modos de mapeamento variam de acordo com o tipo de variável.
1. Mapeie mais variáveis para fazer uma expressão significativa. Toque ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) para salvar as alterações.

### Exemplo 1: Consulte uma variável XML para definir o valor de uma variável de string {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

Selecione uma variável do tipo XML para armazenar um arquivo XML. Consulte a variável XML para definir o valor de uma variável de string para a propriedade disponível no arquivo XML. Use **Especificar XPATH para a variável XML** para definir a propriedade a ser armazenada na variável da string.

Neste exemplo, selecione um **formdata** Variável XML para armazenar a variável **cc-app.xml** arquivo. Consulte o **formdata** para definir o valor da variável **email address** variável de string para armazenar o valor da variável **emailAddress** propriedade disponível na **cc-app.xml** arquivo.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "Definir valor de uma variável")

### Exemplo 2: Use uma expressão para armazenar valor com base em outras variáveis {#example2}

Use uma expressão para calcular a soma das variáveis e armazenar o resultado em uma variável.

Neste exemplo, use o editor de expressão para definir uma expressão para calcular a soma de **custo dos ativos** e **valor do saldo** e armazene o resultado em **valor total** variável.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## Usar editor de expressão {#use-expression-editor}

Também é possível usar expressões para calcular o valor de uma variável no tempo de execução. As variáveis fornecem um editor de expressão para definir expressões.

Use o editor de expressão para:

* Defina o valor das variáveis usando outras variáveis, números ou expressões matemáticas do fluxo de trabalho.
* Use variáveis de fluxo de trabalho, string, número ou uma expressão em uma expressão matemática
* Adicione condições para definir valores de variáveis.
* Adicione operadores entre condições.

![Editor de expressão](assets/variables_expression_editor_new.png)

É baseado no editor de regras de formulários adaptáveis com as seguintes alterações. Editor de regras em variáveis:

* Não suporta funções.
* Não fornece uma interface do usuário para exibir o resumo das regras
* Não tem editor de código.
* Não suporta a ativação e desativação do valor de um objeto.
* Não suporta a configuração da propriedade de um objeto.
* Não suporta chamar um serviço da Web.

Para obter mais informações, consulte [editor de regras de formulários adaptáveis](/help/forms/using/rule-editor.md).

## Usar uma variável {#use-a-variable}

Você pode usar variáveis para recuperar entradas e saídas ou salvar o resultado de uma etapa. O editor de workflow fornece dois tipos de etapas de workflow:

* Etapas de fluxo de trabalho com suporte para variáveis
* Etapas de fluxo de trabalho sem suporte para variáveis

### Etapas de fluxo de trabalho com suporte para variáveis {#workflow-steps-with-support-for-variables}

A etapa Ir para ou Split e todas as etapas do fluxo de trabalho do AEM Forms suportam variáveis.

#### OU Split step {#or-split-step}

A divisão OR cria uma divisão no fluxo de trabalho, após a qual apenas uma ramificação está ativa. Essa etapa permite introduzir caminhos de processamento condicional no fluxo de trabalho. Adicione etapas de fluxo de trabalho a cada ramificação, conforme necessário.

Você pode definir uma expressão de roteamento para uma ramificação usando uma definição de regra, um script ECMA ou um script externo.

Você pode usar variáveis para definir a expressão de roteamento usando o editor de expressão. Para obter mais informações sobre o uso de expressões de roteamento para a etapa OU Dividir , consulte [OU Split step](/help/sites-developing/workflows-step-ref.md#or-split).

Neste exemplo, antes de definir a expressão de roteamento, use [exemplo 2](/help/sites-developing/using-variables-in-aem-workflows.md#example2) para definir o valor da variável **valor total** variável. A Ramificação 1 estará ativa se o valor da variável **valor total** for maior que 50000. Da mesma forma, é possível definir uma regra para tornar a Ramificação 2 ativa se o valor da variável **valor total** é menor que 50000.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

Da mesma forma, selecione um caminho de script externo ou especifique o script ECMA para expressões de roteamento para avaliar a ramificação ativa. Toque **[!UICONTROL Renomear Ramificação]** para especificar um nome alternativo para a ramificação.

Para obter mais exemplos, consulte [Criar um modelo de fluxo de trabalho](/help/forms/using/aem-forms-workflow.md#create-a-workflow-model).

#### Etapa Ir para {#go-to-step}

O **Etapa Ir para** permite especificar a próxima etapa no modelo de fluxo de trabalho a ser executado, dependendo do resultado de uma expressão de roteamento.

Semelhante à etapa OU Dividir , é possível definir a expressão de roteamento para a etapa Ir para usando uma definição de regra, um script ECMA ou um script externo.

Você pode usar variáveis para definir a expressão de roteamento usando o editor de expressão. Para obter mais informações sobre o uso de expressões de roteamento para a etapa Ir para , consulte [Etapa Ir para](/help/sites-developing/workflows-step-ref.md#goto-step).

![Ir para regra](assets/variables_goto_rule1_new.png)

Neste exemplo, a etapa Ir especifica a opção Revisar aplicativo de cartão de crédito como a próxima etapa se o valor da variável **ação** é igual a **Precisa de mais informações**.

Para obter mais exemplos sobre o uso da definição de regra na etapa Ir para , consulte [Simulação de um loop For](/help/sites-developing/workflows-step-ref.md#simulateforloop).

#### Etapas de fluxo de trabalho centradas no fluxo de trabalho do Forms {#forms-workflow-centric-workflow-steps}

Todas as etapas do fluxo de trabalho do AEM Forms suportam variáveis. Para obter mais informações, consulte [Fluxo de trabalho centrado no Forms no OSGi](/help/forms/using/aem-forms-workflow-step-reference.md).

### Etapas de fluxo de trabalho sem suporte para variáveis {#workflow-steps-without-support-for-variables}

Você pode usar [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) para acessar variáveis em etapas de fluxo de trabalho que não suportam variáveis.

#### Recuperar o valor da variável {#retrieve-the-variable-value}

Use as seguintes APIs no script ECMA para recuperar valores para variáveis existentes com base no tipo de dados:

| Tipo de dados da variável | API |
|---|---|
| Primitivo (Longo, Duplo, Booliano, Data e Cadeia de Caracteres) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| XML | Pacotes.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |

Para obter informações sobre APIs para tipos de dados de variáveis complexas adicionais disponíveis nos fluxos de trabalho do AEM Forms, consulte [Variáveis em workflows do AEM Forms](/help/forms/using/variable-in-aem-workflows.md).

**Exemplo**

Recupere o valor do tipo de dados da string usando a seguinte API:

```
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### Atualizar o valor da variável {#update-the-variable-value}

Use a seguinte API no script ECMA para atualizar o valor de uma variável:

```
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**Exemplo**

```
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

atualiza o valor da variável **salário** para 50000.

### Definir variáveis para invocar workflows {#apiinvokeworkflow}

Você pode usar uma API para definir variáveis e passá-las para chamar instâncias de fluxo de trabalho.

[workflowSession.startWorkflow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) O usa modelo, wfData e metaData como argumentos. Use o MetaDataMap para definir o valor da variável.

Nessa API, a variável **variableName** estiver definida como **value** utilização de metaData.put(variableName, value);

```java
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## Editar uma variável {#edit-a-variable}

1. Na página Editar fluxo de trabalho , toque no ícone Variáveis disponível no sidekick do modelo de fluxo de trabalho. A seção Variáveis no painel esquerdo exibe todas as variáveis existentes.
1. Toque no ![](https://helpx.adobe.com/content/dam/help/images/en/edit.png) (Editar) ícone ao lado do nome da variável que você deseja editar.
1. Edite as informações da variável e toque em ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) para salvar as alterações. Não é possível editar o **[!UICONTROL Nome]** e **[!UICONTROL Tipo]** campos para uma variável.

## Excluir uma variável {#delete-a-variable}

Antes de excluir a variável , remova todas as referências da variável do fluxo de trabalho. Certifique-se de que a variável não seja usada no workflow.

Execute as seguintes etapas para excluir uma variável:

1. Na página Editar fluxo de trabalho , toque no ícone Variáveis disponível no sidekick do modelo de fluxo de trabalho. A seção Variáveis no painel esquerdo exibe todas as variáveis existentes.
1. Toque no ícone Excluir ao lado do nome da variável que você deseja excluir.
1. Toque ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) para confirmar e excluir a variável.
