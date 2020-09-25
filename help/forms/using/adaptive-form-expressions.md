---
title: Expressões de formulário adaptáveis
seo-title: Expressões de formulário adaptáveis
description: Use expressões de formulários adaptáveis para adicionar validação automática, cálculo e ativar ou desativar a visibilidade de uma seção.
seo-description: Use expressões de formulários adaptáveis para adicionar validação automática, cálculo e ativar ou desativar a visibilidade de uma seção.
uuid: c274dce5-8b87-472f-bff5-53b246fa6584
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2fd2276e-cfe3-47ad-94c1-9c7af56b7a17
docset: aem65
translation-type: tm+mt
source-git-commit: 26a65772c43a5176d178bb6625604d18ac91e894
workflow-type: tm+mt
source-wordcount: '2767'
ht-degree: 0%

---


# Expressões de formulário adaptáveis{#adaptive-form-expressions}

Formulários adaptáveis fornecem experiência de preenchimento de formulário otimizada e simplificada para usuários finais com recursos de script dinâmico. Ele permite que você escreva expressões para adicionar vários comportamentos, como mostrar/ocultar dinâmicos campos e painéis. Ela também permite que você adicione campos calculados, torne os campos somente leitura, adicione lógica de validação e muito mais. O comportamento dinâmico é baseado na entrada do usuário ou nos dados pré-preenchidos.

JavaScript é a linguagem expressão de formulários adaptáveis. Todas as expressões são expressões JavaScript válidas e usam APIs de modelo de script de formulários adaptáveis. Essas expressões retornam valores de certos tipos. Para obter a lista completa de classes de formulários adaptáveis, eventos, objetos e APIs públicas, consulte Referência da API da biblioteca [JavaScript para formulários](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html)adaptáveis.

## Práticas recomendadas para gravar expressões {#best-practices-for-writing-expressions}

* Ao gravar expressões, para acessar campos e painéis, é possível usar o nome do campo ou painel. Para acessar o valor de um campo, use a propriedade value. Por exemplo, `field1.value`
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

## Tipos de expressão {#expression-types}

Em formulários adaptáveis, é possível gravar expressões para adicionar comportamentos como mostrar/ocultar campos e painéis dinâmicos. Também é possível gravar expressões para adicionar campos calculados, tornar os campos somente leitura, lógica de validação e muito mais. Os formulários adaptáveis suportam as seguintes expressões:

* **[Expressões](#access-expression-enablement-expression)** de acesso: para ativar/desativar um campo.
* **[Calcular expressões](#calculate-expression)**: para calcular automaticamente o valor de um campo.
* **[Clique em expressão](#click-expression)**: para manipular ações ao clicar no evento de um botão.
* **[Script](#initialization-script)de inicialização:** execute uma ação na inicialização de um campo.
* **[Expressão](#options-expression)** de opções: para preencher dinamicamente uma lista suspensa.
* **[Expressão](#summary)** de resumo: para calcular dinamicamente o título de um acordeão.
* **[Validar expressões](#validate-expression)**: para validar um campo.
* **[Script](#value-commit-script)de confirmação de valor:** para alterar os componentes de um formulário após a alteração do valor de um campo.
* **[Expressão](#visibility-expression)** de visibilidade: para controlar a visibilidade de um campo e painel.
* **[Expressão](#step-completion-expression)** de conclusão de etapas: para impedir que um usuário vá para a próxima etapa de um assistente.

### Expressão de acesso (Expressão de ativação) {#access-expression-enablement-expression}

Você pode usar a expressão de acesso para ativar ou desativar um campo. Se a expressão usar o valor de um campo, sempre que o valor do campo for alterado, a expressão será reacionada.

**Aplica-se a**: campos

**Tipo** de retorno: A expressão retorna um valor booliano, representando se o campo está ativado ou desativado. **true** representa que o campo está ativado e **false** representa que o campo está desativado.

**Exemplo**: Para ativar um campo somente quando o valor de **field1** estiver definido como **X**, a expressão de acesso é: `field1.value == "X"`

### Calcular Expressão {#calculate-expression}

A expressão calculate é usada para calcular automaticamente o valor de um campo usando uma expressão. Normalmente, essa expressão usa a propriedade value de outros campos. Por exemplo, `field2.value + field3.value`. Sempre que o valor do `field2`ou `field3`muda, a expressão é acionada novamente e o valor é recomposto.

**Aplica-se a**: campos

**Tipo** de retorno: A expressão retorna um valor compatível com o campo onde o resultado da expressão é exibido (por exemplo, decimal).

**Exemplo**: A expressão calculate para mostrar a soma de dois campos no **campo1** é:
`field2.value + field3.value`

### Clique em Expressão {#click-expression}

A expressão click manipula as ações executadas no evento click de um botão. O GuideBridge fornece APIs para executar várias funções, como enviar, validar, usadas junto com a expressão de cliques. Para obter a lista completa das APIs, consulte [GuideBridge APIs](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**Aplica-se a**: Campos de botão

**Tipo** de retorno: A expressão click não retorna nenhum valor. Se qualquer expressão retornar um valor, ele será ignorado.

**Exemplo**: Para preencher uma caixa de texto **caixa1** na ação de clique de um botão com valor **AEM Forms**, a expressão de clique do botão é `textbox1.value="AEM Forms"`

### Script de inicialização {#initialization-script}

O script de inicialização é acionado quando um formulário adaptável é inicializado. Dependendo dos cenários, o script de inicialização se comporta da seguinte maneira:

* Quando um formulário adaptável é renderizado sem um preenchimento prévio de dados, o script de inicialização é executado após a inicialização do formulário.
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

**Exemplo:** Para converter as letras maiúsculas e minúsculas digitadas no campo em maiúsculas na confirmação, a expressão de confirmação de valor é:
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>Você pode desativar a execução do Script de confirmação de valor quando o valor de um campo é alterado de forma programática. Para fazer isso, vá para https://&#39;[server]:[port]&#39;/system/console/configMgr e altere a versão **adaptável do Forms para Compatibilidade** com o **AEM Forms 6.1**. Em seguida, o script de confirmação de valor é executado somente quando o usuário altera o valor do campo da interface do usuário.

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

Há vários padrões de validação prontos para uso disponíveis para um campo. Para selecionar um padrão de validação, na caixa de diálogo **Editar** do componente, localize a seção **Padrões** e selecione **padrões**. Você pode criar seu próprio padrão de validação personalizado em uma caixa de texto **Padrão** . O status de validação será retornado **Verdadeiro** somente se os dados preenchidos forem compatíveis com o padrão de validação, caso contrário, será retornado **Falso** . Para gravar seu próprio padrão de validação personalizado, consulte Suporte a cláusula [de imagem para formulários](/help/forms/using/picture-clause-support.md)HTML5.

### Expressões de validação {#validation-expressions}

A validação de um campo também pode ser calculada usando expressões em campos diferentes. Essas expressões são gravadas no campo Script **de** validação da guia **Script** da caixa de diálogo **Editar** do componente. O status de validação de um campo depende do valor retornado pela expressão. Para obter informações sobre como gravar tais expressões, consulte [Validar Expressão](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p).

## Informações adicionais {#additional-information}

### Uso do formato de exibição de campo {#using-field-display-format}

Formato de exibição pode ser usado para exibir os dados em diferentes formatos. Por exemplo, você pode usar o formato de exibição para exibir um número de telefone com hífens, formatar código ZIP ou seletor de data. Esses padrões de exibição podem ser selecionados na seção **Padrões** da caixa de diálogo Editar de um componente. Você pode gravar padrões de exibição personalizados semelhantes aos padrões de validação mencionados acima.

### GuideBridge - APIs e Eventos {#guidebridge-apis-and-events}

O GuideBridge é uma coleção de APIs que podem ser usadas para interagir com formulários adaptáveis no modelo de memória em um navegador. Para obter uma introdução detalhada à API do Guide Bridge, métodos de classe, eventos expostos, consulte Referência da API da biblioteca [JavaScript para formulários](https://helpx.adobe.com/aem-forms/6/javascript-api/)adaptáveis.

>[!NOTE]
>
>É recomendável não usar os ouvintes do evento GuideBridge no expressão.

#### Uso do GuideBridge em várias expressões {#guidebridge-usage-in-various-expressions}

* Para redefinir campos de formulário, é possível acionar a `guideBridge.reset()` API na expressão de clique de um botão. Da mesma forma, há uma API de envio que pode ser chamada como uma expressão de clique `guideBridge.submit()`**.**

* Você pode usar a `setFocus()` API para definir o foco em vários campos ou painéis (para que o foco do painel seja definido automaticamente para o primeiro campo). `setFocus()`fornece uma grande variedade de opções para navegar, como navegação em painéis, travessia anterior/seguinte, definição de foco para um campo específico e muito mais. Por exemplo, para ir para o próximo painel, você pode usar: `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* Para validar um formulário adaptável ou seus painéis específicos, use `guideBridge.validate(errorList, somExpression).`

#### Uso do GuideBridge fora do Expressão  {#using-guidebridge-outside-expressions-nbsp}

Você também pode usar as APIs do GuideBridge fora do expressão. Por exemplo, você pode usar a API GuideBridge para definir a comunicação entre a página HTML que hospeda o formulário adaptável e o Modelo de formulário. Além disso, é possível definir o valor que vem do pai do Iframe que hospeda o formulário.

Para usar a API GuideBridge para o exemplo acima mencionado, capture uma instância do GuideBridge. Para capturar a instância, ouça o `bridgeInitializeStart`evento de um `window`objeto:

```javascript
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
>No AEM, é uma boa prática gravar o código em um clientLib e incluí-lo na sua página (header.jsp ou footer.jsp da página)

Para usar o GuideBridge após a inicialização do formulário (o `bridgeInitializeComplete` evento é despachado), use a instância do GuideBridge `window.guideBridge`. Você pode verificar o status de inicialização do GuideBridge usando a `guideBride.isConnected` API.

#### Eventos GuideBridge {#guidebridge-events}

O GuideBridge também fornece determinados eventos para scripts externos na página de hospedagem. Scripts externos podem ouvir esses eventos e executar várias operações. Por exemplo, sempre que o nome de usuário em um formulário é alterado, o nome mostrado no cabeçalho da página também é alterado. Para obter mais detalhes sobre esses eventos, consulte Referência da API da biblioteca [JavaScript para formulários](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)adaptáveis.

Use o seguinte código para registrar manipuladores:

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### Criação de padrões personalizados para um campo {#creating-custom-patterns-for-a-field}

Como mencionado acima, formulários adaptáveis permitem que o autor forneça padrões para formatos de validação ou exibição. Além de usar padrões fora da caixa, você pode definir padrões personalizados reutilizáveis para um componente de formulário adaptável. Por exemplo, é possível definir um campo de texto ou um campo numérico. Depois de definidos, você pode usar esses padrões em todos os formulários para o tipo de componente especificado. Por exemplo, você pode criar um padrão personalizado para um campo de texto e usá-lo nos campos de texto em seus formulários adaptáveis. Você pode selecionar o padrão personalizado acessando a seção padrão na caixa de diálogo de edição de um componente. Para obter detalhes sobre a definição ou o formato de padrão, consulte Suporte a cláusula [de imagem para formulários](/help/forms/using/picture-clause-support.md)HTML5.

Execute as seguintes etapas para criar um padrão personalizado para um tipo de campo específico e reutilize-o para outros campos do mesmo tipo:

1. Navegue até CRXDE Lite na sua instância de criação.
1. Crie uma pasta para manter seus padrões personalizados. No diretório /apps, crie um nó do tipo sling:folder. Por exemplo, crie um nó com o nome `customPatterns`. Neste nó, crie outro nó do tipo `nt:unstructed` e nomeie-o `textboxpatterns`. Este nó contém os vários padrões personalizados que você deseja adicionar.
1. Abra a guia Propriedades do nó criado. Por exemplo, abra a guia Propriedades de `textboxpatterns`. Adicione a `guideComponentType` propriedade a esse nó e defina seu valor como *fd/af/components/formatter/guideTextBox*.

1. O valor dessa propriedade varia dependendo do campo para o qual você deseja definir os padrões. Para o campo numérico, o valor da `guideComponentType` propriedade é *fd/af/components/formatter/guideNumericBox*. O valor do campo Datepicker é *fd/af/components/formatter/guideDatepicker*.
&quot;
1. É possível adicionar um padrão personalizado atribuindo uma propriedade ao `textboxpatterns` nó. Adicione uma propriedade com um nome (por exemplo `pattern1`) e defina seu valor para o padrão que deseja adicionar. Por exemplo, adicione uma propriedade `pattern1` com o valor Fax=text{99-999-999999}. O padrão está disponível para todas as caixas de texto usadas no Forms adaptável.

   ![Criação de padrões personalizados para campos no CrxDe](assets/creating-custom-patterns.png)

   Criação de padrões personalizados

