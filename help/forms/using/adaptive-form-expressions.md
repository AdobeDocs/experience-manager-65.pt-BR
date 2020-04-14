---
title: Adaptive Form Expressions
seo-title: Adaptive Form Expressions
description: Use expressões de formulários adaptáveis para adicionar validação automática, cálculo e ativar ou desativar a visibilidade de uma seção.
seo-description: Use expressões de formulários adaptáveis para adicionar validação automática, cálculo e ativar ou desativar a visibilidade de uma seção.
uuid: c274dce5-8b87-472f-bff5-53b246fa6584
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2fd2276e-cfe3-47ad-94c1-9c7af56b7a17
docset: aem65
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Adaptive Form Expressions{#adaptive-form-expressions}

Adaptive forms provide optimized and simplified form filling experience for end users with dynamic scripting capabilities. Ele permite que você escreva expressões para adicionar vários comportamentos, como mostrar/ocultar dinâmicos campos e painéis. It also lets you add calculated fields, make fields read-only, add validation logic, and many more. The dynamic behavior is based on the user input or prefilled data.

JavaScript is the expression language of adaptive forms. All the expressions are valid JavaScript expressions and use adaptive forms scripting model APIs. Essas expressões retornam valores de certos tipos. Para obter a lista completa de classes de formulários adaptáveis, eventos, objetos e APIs públicas, consulte Referência da API da biblioteca [JavaScript para formulários](https://helpx.adobe.com/aem-forms/6/javascript-api/index.html)adaptáveis.

## Best practices for writing expressions {#best-practices-for-writing-expressions}

* While writing expressions, to access fields and panels, you can use name of field or panel. Para acessar o valor de um campo, use a propriedade value. Por exemplo, `field1.value`
* Use nomes exclusivos para campos e painéis no formulário. Ele ajuda a evitar possíveis conflitos com nomes de campo usados ao gravar expressões.
* Enquanto escreve expressões de várias linhas, use ponto e vírgula para encerrar uma instrução.

## Práticas recomendadas para expressões que envolvam painel repetitivo {#best-practices-for-expressions-involving-repeating-panel}

Painéis repetitivos são instâncias de um painel que são adicionadas ou removidas dinamicamente, usando API de script ou dados pré-preenchidos. Para obter informações detalhadas sobre como usar o painel repetitivo, consulte [criação de formulários com seções](/help/forms/using/creating-forms-repeatable-sections.md)repetíveis.

* Para criar um painel repetitivo, na caixa de diálogo do painel, abra as configurações e defina o valor do campo de contagem máxima como mais de 1.
* O valor da contagem mínima das configurações de repetição do painel pode ser um ou mais, mas não pode ser maior que o valor da contagem máxima.
* Quando uma expressão se refere a um campo de painel repetitivo, os nomes de campo na expressão são resolvidos para o elemento repetitivo mais próximo.
* Formulários adaptáveis fornecem algumas funções especiais para simplificar a computação para painéis repetíveis, como soma, contagem, mín, máx, filtro e muito mais. Para obter a lista completa de funções, consulte Referência da API da biblioteca [JavaScript para formulários adaptáveis](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* As APIs para manipular instâncias do painel repetitivo são:

   * Para adicionar uma instância de painel: `panel1.instanceManager.addInstance()`
   * Para obter um índice de repetição de painel: `panel1.instanceIndex`
   * Para obter o instanceManager de um painel: `_panel1 or panel1.instanceManager`
   * Para remover uma instância de um painel: `_panel1.removeInstance(panel1.instanceIndex)`

## Tipos de Expressão {#expression-types}

Em formulários adaptáveis, é possível gravar expressões para adicionar comportamentos como mostrar/ocultar campos e painéis dinâmicos. Também é possível gravar expressões para adicionar campos calculados, tornar os campos somente leitura, lógica de validação e muito mais. Os formulários adaptáveis suportam as seguintes expressões:

* **[expressões](#access-expression-enablement-expression)**de acesso: para ativar/desativar um campo.
* **[Calcular expressões](#calculate-expression)**: para calcular automaticamente o valor de um campo.
* **[Clique em expressão](#click-expression)**: para manipular ações ao clicar no evento de um botão.
* **[Script](#initialization-script)de inicialização:**execute uma ação na inicialização de um campo.
* **[expressão](#options-expression)**de opções: para preencher dinamicamente uma lista suspensa.
* **[expressão](#summary)**de resumo: para calcular dinamicamente o título de um acordeão.
* **[Validar expressões](#validate-expression)**: para validar um campo.
* **[Script](#value-commit-script)de confirmação de valor:**para alterar os componentes de um formulário após a alteração do valor de um campo.
* **[expressão](#visibility-expression)**de visibilidade: para controlar a visibilidade de um campo e painel.
* **[expressão](#step-completion-expression)**de conclusão de etapas: para impedir que um usuário vá para a próxima etapa de um assistente.

### Expressão de acesso (Expressão de ativação) {#access-expression-enablement-expression}

Você pode usar a expressão de acesso para ativar ou desativar um campo. Se a expressão usar o valor de um campo, sempre que o valor do campo for alterado, a expressão será reacionada.

**Aplica-se a**: campos

**Tipo** de retorno: A expressão retorna um valor booliano, representando se o campo está ativado ou desativado. **true** representa que o campo está ativado e **false** representa que o campo está desativado.

**Exemplo**: Para ativar um campo somente quando o valor de **field1** estiver definido como **X**, a expressão de acesso é: `field1.value == "X"`

### Calcular Expressão {#calculate-expression}

A expressão calculate é usada para calcular automaticamente o valor de um campo usando uma expressão. Typically, such expression use value property of another fields. Por exemplo, `field2.value + field3.value`. Whenever value of the `field2`or `field3`changes, the expression is retriggered and the value is recomputed.

**Applies to**: fields

**Return Type**: The expression returns a value that is compatible to the field where the expression result is displayed (for example, decimal).

**Exemplo**: A expressão calculate para mostrar a soma de dois campos no **campo1** é:
`field2.value + field3.value`

### Click Expression {#click-expression}

The click expression handles the actions performed on the click event of a button. O GuideBridge fornece APIs para executar várias funções, como enviar, validar, usadas junto com a expressão de cliques. For complete list of the APIs, see [GuideBridge APIs](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**Aplica-se a**: Campos de botão

**Return Type**: The click expression does not return any value. If any expression returns a value, the value is ignored.

**Example**: To populate a text box **textbox1** on the click action of a button with value **AEM Forms**, the click expression of the button is `textbox1.value="AEM Forms"`

### Script de inicialização {#initialization-script}

The initialization script is triggered when an adaptive form is initialized. Depending on scenarios, the initialization script behaves in the following manner:

* When an adaptive form is rendered without a data prefill, the initialization script runs after the form is initialized.
* Quando um formulário adaptável é renderizado com um pré-preenchimento de dados, o script é executado após a conclusão da operação de pré-preenchimento.
* Quando a revalidação de um formulário adaptável pelo lado do servidor é acionada, o script de inicialização é executado.

**Aplica-se a:** campos e painel

**Tipo de retorno:** A expressão de script Initialization não retorna nenhum valor. Se qualquer expressão retornar um valor, ele será ignorado.

**Exemplo:** Em um cenário de preenchimento prévio de dados, para preencher campos com valor padrão `'Adaptive Forms'` quando seu valor for salvo como nulo, a expressão do script de inicialização é:
`if(this.value==null) this.value='Adaptive Forms';`

### Expressão Opções {#options-expression}

A expressão de opções é usada para preencher dinamicamente as opções de um campo de lista suspenso.

**Aplica-se a**: campos de lista suspensos

**Tipo** de retorno: A expressão options retorna uma matriz de valores de string. Cada valor pode ser uma sequência simples, como **Masculino**, ou em um formato de par key=value, como **1=Masculino**

**Exemplo**: Para preencher o valor de um campo, com base no valor de outro campo, forneça uma expressão de opções simples. Por exemplo, para preencher um campo, **Número de Crianças**, com base no Status **** Marital expresso em outro campo, a expressão é:

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

Sempre que o valor do campo **marital_status** for alterado, a expressão será reacionada. Você também pode preencher a lista suspensa de um serviço REST. Para obter informações detalhadas, consulte Preenchimento [dinâmico de menus](../../forms/using/dynamically-populate-dropdowns.md).

### Expressão de resumo {#summary}

A expressão Resumo calcula dinamicamente o título de um painel filho de um painel de layout acordeão. É possível especificar a expressão Resumo em uma regra, que usa um campo de formulário ou uma lógica personalizada para avaliar o título. A expressão é executada quando o formulário é inicializado. Se você estiver preenchendo um formulário previamente, a expressão será executada depois que os dados forem preenchidos previamente ou quando o valor dos campos dependentes usados na expressão for alterado.

A expressão Resumo é normalmente usada para filhos repetitivos de um painel de layout acordeão para fornecer um título significativo para cada painel filho.

**Aplica-se a:** Painéis que são filhos diretos de um painel cujo layout está configurado como Acordeão.

**Tipo de retorno:** A expressão retorna uma String que se torna o título do acordeão.

**Exemplo:** &quot;Número da conta : &quot;+ textbox1.value

### Validar Expressão {#validate-expression}

A expressão validate é usada para validar os campos usando a expressão especificada. Normalmente, essas expressões usam expressões regulares juntamente com o valor do campo para validar um campo. A expressão é acionada novamente e o status de validação do campo é recomendado em qualquer alteração no valor de um campo.

**Aplica-se a**: campos

**Tipo** de retorno: A expressão retorna um valor booliano, representando o status de validação do campo. O valor **false** representa que o campo é inválido e **true** representa que o campo é válido.
**Exemplo**: Para um campo que representa o código postal do Reino Unido, a expressão de validação é:

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

No exemplo acima, se o valor não vazio não corresponder ao padrão, a expressão retornará **false** para indicar que o campo não é válido.

>[!NOTE]
>
>Se você gravar uma expressão de validação para um campo não obrigatório ou obrigatório, a expressão será avaliada independentemente do status de visibilidade do campo. Para interromper a validação dos campos ocultos, defina a propriedade validationsDisabled no Script de Confirmação de Inicialização ou Valor como true. Por exemplo, `this.validationsDisabled=true`

### Script de Value Commit {#value-commit-script}

O script de Confirmação de Valor é acionado quando:

* Um usuário altera o valor de um campo da interface do usuário.
* O valor de um campo muda de forma programática devido a uma alteração em outro campo.

**Aplica-se a:** campos

**Tipo de retorno:** A expressão de script commit de valor não retorna nenhum valor. Se qualquer expressão retornar um valor, ele será ignorado.

**Example:** To convert the case of alphabets entered in the field to uppercase on commit, the value commit expression is:
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>Você pode desativar a execução do Script de confirmação de valor quando o valor de um campo é alterado de forma programática. Para fazer isso, vá para https://&#39;[server]:[port]&#39;/system/console/configMgr e altere Versão de formulários **adaptáveis para Compatibilidade** com o **AEM Forms 6.1**. Em seguida, o script de confirmação de valor é executado somente quando o usuário altera o valor do campo da interface do usuário.

### Expressão de visibilidade {#visibility-expression}

A expressão de visibilidade é usada para controlar a visibilidade do campo/painel. Normalmente, a expressão de visibilidade usa a propriedade value de um campo e é acionada novamente sempre que esse valor é alterado.

**Aplica-se a**: campos e painel

**Tipo** de retorno: Expressão retorna um valor booliano, que representa que o campo/painel está visível ou não. **false** representa que o campo ou painel não está visível e true representa que o campo ou painel está visível.

**Exemplo**: Para um painel que se torna visível somente se o valor de **field1** estiver definido como **Masculino**, a expressão de visibilidade é: `field1.value == "Male"`

### Expressão de conclusão de etapas {#step-completion-expression}

A expressão de conclusão de etapas é usada para impedir que um usuário vá para a próxima etapa de um layout do assistente. Essas expressões são usadas quando os painéis têm um layout de assistente (formulários em várias etapas que mostram uma etapa por vez). O usuário só poderá se mover para a próxima etapa, painel ou subseção se todos os valores necessários na seção atual forem preenchidos e válidos.

**Aplica-se a**: Painéis com o layout do item definido como assistente.

**Tipo** de retorno: Expressão retorna um valor booliano, representando o painel atual como válido ou não. **True** representa que o painel atual é válido e que o usuário pode navegar para o próximo painel.

**Exemplo**: Em um formulário organizado em vários painéis, antes de navegar para o painel seguinte, o painel atual é validado. Nesses casos, as expressões de conclusão de etapas são usadas. Geralmente, essas expressões usam a API de validação do GuideBridge. Um exemplo de expressão de conclusão de etapas é:
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## Validações no formulário adaptável {#validations-in-adaptive-form}

Há vários métodos para adicionar a validação de campo a um formulário adaptável. Se uma verificação de validação for adicionada em um campo, **Verdadeiro** representa que o valor digitado no campo é válido. **False** representa que o valor é inválido. Se você digitar dentro e fora de um campo, a mensagem de erro não será gerada.

Os métodos para adicionar validações em um campo são:

### Obrigatório {#required}

Para tornar um componente obrigatório, na caixa de diálogo **Editar** do componente, é possível selecionar a opção **Título e Texto > Obrigatório**. Você também pode adicionar a mensagem **** obrigatória apropriada (opcional). .

### Padrões de validação {#validation-patterns}

There are multiple out of the box validation patterns available for a field. Para selecionar um padrão de validação, na caixa de diálogo **Editar** do componente, localize a seção **Padrões** e selecione **padrões**. You can create your own custom validation pattern in a **Pattern** text box. The validation status is returned **True** only if the data filled is compliant to the validation pattern, else **False** is returned. To write your own custom validation pattern, see [Picture clause support for HTML5 forms](/help/forms/using/picture-clause-support.md).

### Validation Expressions {#validation-expressions}

The validation of a field can also be computed using expressions on different fields. These expressions are written inside **Validation Script** field of the **Script** tab of **Edit** dialog of the component. The validation status of a field depends upon the value that the expression returns. For information on how to write such expressions, see [Validate Expression](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p).

## Informações adicionais {#additional-information}

### Using Field Display Format {#using-field-display-format}

Formato de exibição pode ser usado para exibir os dados em diferentes formatos. For example, you can use the display format to display a telephone number with hyphens, format ZIP code, or date picker. These display patterns can be selected from the **Patterns** section of the Edit dialog of a component. You can write custom display patterns similar to the validation patterns mentioned above.

### GuideBridge - APIs and Events {#guidebridge-apis-and-events}

GuideBridge is collection of APIs’ that can be used to interact with adaptive forms in memory model in a browser. For detailed introduction to Guide Bridge API, class methods, events exposed, see [JavaScript Library API reference for adaptive forms](https://helpx.adobe.com/aem-forms/6/javascript-api/).

>[!NOTE]
>
>It is recommended not to use the GuideBridge event listeners in expressions.

#### GuideBridge usage in various expressions {#guidebridge-usage-in-various-expressions}

* To reset form fields, you can trigger `guideBridge.reset()` API on the click expression of a button. Similarly there is a submit API which can be called as a click expression `guideBridge.submit()`**.**

* You can use the `setFocus()` API to set focus across various fields or panels (for panel focus is set to the first field automatically). `setFocus()`provides a wide range of options to navigate such as navigation across panels, previous/next traversal, setting focus to a particular field, and many more. For example, to move to the next panel, you can use: `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* To validate an adaptive form or its specific panels, use `guideBridge.validate(errorList, somExpression).`

#### Using GuideBridge outside Expressions  {#using-guidebridge-outside-expressions-nbsp}

Você também pode usar as APIs do GuideBridge fora do expressão. For example, you can use the GuideBridge API to set communication between page HTML hosting the adaptive form and the Form Model. Além disso, é possível definir o valor que vem do pai do Iframe que hospeda o formulário.

Para usar a API GuideBridge para o exemplo acima mencionado, capture uma instância do GuideBridge. Para capturar a instância, ouça o `bridgeInitializeStart`evento de um `window`objeto:

```
window.addEventListener("bridgeInitializeStart", function(evnt) {

     // get hold of the guideBridge object

     var gb = evnt.detail.guideBridge;

     //wait for the completion of AF

     gb.connect(function (){

        //this function will be called after Adaptive Form is initialized

     })

})
```

>[!NOTE]
>
>No AEM, é uma boa prática gravar um código em um clientLib e incluí-lo em sua página (header.jsp ou footer.jsp da página)

Para usar o GuideBridge após a inicialização do formulário (o `bridgeInitializeComplete` evento é despachado), use a instância do GuideBridge `window.guideBridge`. Você pode verificar o status de inicialização do GuideBridge usando a `guideBride.isConnected` API.

#### Eventos GuideBridge {#guidebridge-events}

GuideBridge also provides certain events for external scripts on the hosting page. External scripts can listen to these events and perform various operations. For example, whenever the user name in a form change, the name shown in the header of the page also changes. For more details about such events, see [JavaScript Library API reference for adaptive forms](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

Use the following code to register handlers:

```
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### Creating custom patterns for a field {#creating-custom-patterns-for-a-field}

As mentioned above, adaptive forms allows author to provide patterns for validation or display formats. In addition to using out of the box patterns, you can define reusable custom pattern for an adaptive form component. For example, you can define a text field or a numeric field. Once defined, you can use these patterns in all the forms for specified type of component. For example, you can create a custom pattern for a text field and use it in the text fields in their adaptive forms. You can select the custom pattern by accessing the pattern section in the edit dialog of a component. For details about Pattern definition or format, see [Picture clause support for HTML5 forms](/help/forms/using/picture-clause-support.md).

Perform the following steps to create a custom pattern for a specific field type and reuse it for other fields of the same type:

1. Navigate to CRXDE Lite on your authoring instance.
1. Create a folder to maintain your custom patterns. Under the /apps directory, create a node of type sling:folder. For example, create a node with the name `customPatterns`. Under this node, create another node of type `nt:unstructed` and name it `textboxpatterns`. This node contains the various custom patterns that you want to add.
1. Open the Properties tab of the node created. For example, open the Properties tab of `textboxpatterns`. Add the `guideComponentType` property to this node and set its value to *fd/af/components/formatter/guideTextBox*.

1. The value of this property varies depending on the field for which you want to define the patterns. Para o campo numérico, o valor da `guideComponentType` propriedade é *fd/af/components/formatter/guideNumericBox*. O valor do campo Datepicker é *fd/af/components/formatter/guideDatepicker*.
&quot;
1. You can add a custom pattern by assigning a property to the `textboxpatterns` node. Adicione uma propriedade com um nome (por exemplo `pattern1`) e defina seu valor para o padrão que deseja adicionar. Por exemplo, adicione uma propriedade `pattern1` com o valor Fax=text{99-999-999999}. O padrão está disponível para todas as Caixas de texto usadas em Formulários adaptáveis.

   ![Criação de padrões personalizados para campos no CrxDe](assets/creating-custom-patterns.png)

   Creating custom patterns

