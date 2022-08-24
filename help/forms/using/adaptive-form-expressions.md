---
title: Expressões de formulário adaptável
seo-title: Adaptive Form Expressions
description: Use expressões de formulários adaptáveis para adicionar validação automática, cálculo e ativar ou desativar a visibilidade de uma seção.
seo-description: Use adaptive forms expressions to add automatic validation, calculation, and turn visibility of a section on or off.
uuid: c274dce5-8b87-472f-bff5-53b246fa6584
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2fd2276e-cfe3-47ad-94c1-9c7af56b7a17
docset: aem65
feature: Adaptive Forms
exl-id: 048bd9e8-ef34-40fb-9f46-73743d7b47c8
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2746'
ht-degree: 0%

---

# Expressões de formulário adaptável{#adaptive-form-expressions}

Os formulários adaptáveis fornecem experiência de preenchimento de formulários otimizada e simplificada para usuários finais com recursos de script dinâmico. Permite gravar expressões para adicionar vários comportamentos, como mostrar/ocultar campos e painéis dinâmicos. Também permite adicionar campos calculados, tornar campos somente leitura, adicionar lógica de validação e muito mais. O comportamento dinâmico é baseado na entrada do usuário ou nos dados pré-preenchidos.

JavaScript é a linguagem de expressão de formulários adaptáveis. Todas as expressões são expressões JavaScript válidas e usam APIs de modelo de script de formulários adaptáveis. Essas expressões retornam valores de determinados tipos. Para obter a lista completa de classes de formulários adaptáveis, eventos, objetos e APIs públicas, consulte [Referência da API da biblioteca JavaScript para formulários adaptáveis](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## Práticas recomendadas para escrever expressões {#best-practices-for-writing-expressions}

* Ao gravar expressões, para acessar campos e painéis, é possível usar o nome do campo ou do painel. Para acessar o valor de um campo, use a propriedade value . Por exemplo, `field1.value`
* Use nomes exclusivos para campos e painéis no formulário. Isso ajuda a evitar possíveis conflitos com os nomes de campo usados ao gravar expressões.
* Ao escrever expressões de várias linhas, use um ponto e vírgula para encerrar uma instrução.

## Práticas recomendadas para expressões envolvendo painel repetitivo {#best-practices-for-expressions-involving-repeating-panel}

Painéis repetitivos são instâncias de um painel que são adicionadas ou removidas dinamicamente usando a API de scripts ou dados pré-preenchidos. Para obter informações detalhadas sobre o uso do painel repetitivo, consulte [criação de formulários com seções repetíveis](/help/forms/using/creating-forms-repeatable-sections.md).

* Para criar um painel repetitivo, na caixa de diálogo do painel, abra as configurações e defina o valor do campo de contagem máxima como mais de 1.
* O valor da contagem mínima das configurações de repetição do painel pode ser um ou mais, mas não pode ser maior que o valor da contagem máxima.
* Quando uma expressão se refere a um campo de painel repetitivo, os nomes de campo na expressão são resolvidos para o elemento repetitivo mais próximo.
* Formulários adaptáveis oferecem algumas funções especiais para simplificar o cálculo de painéis repetidos, como soma, contagem, mín, máx, filtro e muito mais. Para obter a lista completa de funções, consulte [Referência da API da biblioteca JavaScript para formulários adaptáveis](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* As APIs para manipular instâncias do painel repetitivo são:

   * Para adicionar uma instância de painel: `panel1.instanceManager.addInstance()`
   * Para obter um índice de repetição de painel: `panel1.instanceIndex`
   * Para obter o instanceManager de um painel: `_panel1 or panel1.instanceManager`
   * Para remover uma instância de um painel: `_panel1.removeInstance(panel1.instanceIndex)`

## Tipos de expressão {#expression-types}

Em formulários adaptáveis, você pode gravar expressões para adicionar comportamentos, como campos dinâmicos de mostrar/ocultar e painéis. Também é possível gravar expressões para adicionar campos calculados, tornar campos somente leitura, lógica de validação e muito mais. Os formulários adaptáveis suportam as seguintes expressões:

* **[Expressões de acesso](#access-expression-enablement-expression)**: para ativar/desativar um campo.
* **[Calcular expressões](#calculate-expression)**: para calcular automaticamente o valor de um campo.
* **[Expressão Click](#click-expression)**: para lidar com ações no evento click de um botão.
* **[Script de inicialização](#initialization-script):** executar uma ação na inicialização de um campo.
* **[Expressão de opções](#options-expression)**: para preencher dinamicamente uma lista suspensa.
* **[Expressão de resumo](#summary)**: para calcular dinamicamente o título de um acordeão.
* **[Validar expressões](#validate-expression)**: para validar um campo.
* **[Script de confirmação de valor](#value-commit-script):** para alterar os componentes de um formulário depois que o valor de um campo é alterado.
* **[Expressão de visibilidade](#visibility-expression)**: para controlar a visibilidade de um campo e painel.
* **[Expressão de conclusão de etapa](#step-completion-expression)**: para impedir que um usuário vá para a próxima etapa de um assistente.

### Expressão de acesso (Expressão de ativação) {#access-expression-enablement-expression}

Você pode usar a expressão de acesso para ativar ou desativar um campo. Se a expressão usar o valor de um campo, sempre que o valor do campo for alterado, a expressão será reacionada.

**Aplica-se a**: campos

**Tipo de retorno**: A expressão retorna um valor booleano, representando se o campo está ativado ou desativado. **true** representa que o campo está ativado e **false** representa que o campo está desativado.

**Exemplo**: Para ativar um campo somente quando o valor de **field1** está definida como **X**, a expressão de acesso é: `field1.value == "X"`

### Calcular expressão {#calculate-expression}

A expressão calculate é usada para calcular automaticamente o valor de um campo usando uma expressão. Normalmente, essa expressão usa a propriedade value de outros campos. Por exemplo, `field2.value + field3.value`. Sempre que o valor da variável `field2`ou `field3`for alterada, a expressão será reacionada e o valor será recalculado.

**Aplica-se a**: campos

**Tipo de retorno**: A expressão retorna um valor compatível com o campo onde o resultado da expressão é exibido (por exemplo, decimal).

**Exemplo**: A expressão calculate para mostrar a soma de dois campos em **field1** é:
`field2.value + field3.value`

### Expressão de cliques {#click-expression}

A expressão click manipula as ações executadas no evento click de um botão. Pronto para uso, o GuideBridge fornece APIs para executar várias funções, como enviar, validar e serem usadas junto com a expressão de clique. Para obter uma lista completa das APIs, consulte [APIs do GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**Aplica-se a**: Campos de botão

**Tipo de retorno**: A expressão click não retorna nenhum valor. Se qualquer expressão retornar um valor, o valor será ignorado.

**Exemplo**: Preencher uma caixa de texto **caixa de texto1** na ação clicar de um botão com valor **AEM Forms**, a expressão click do botão é `textbox1.value="AEM Forms"`

### Script de inicialização {#initialization-script}

O script de inicialização é acionado quando um formulário adaptável é inicializado. Dependendo dos cenários, o script de inicialização se comporta da seguinte maneira:

* Quando um formulário adaptável é renderizado sem um preenchimento prévio de dados, o script de inicialização é executado depois que o formulário é inicializado.
* Quando um formulário adaptável é renderizado com um preenchimento prévio de dados, o script é executado após a conclusão da operação de preenchimento prévio.
* Quando a revalidação de um formulário adaptável pelo lado do servidor é acionada, o script de inicialização é executado.

**Aplica-se a:** campos e painel

**Tipo de retorno:** A expressão do script de Inicialização não retorna nenhum valor. Se qualquer expressão retornar um valor, o valor será ignorado.

**Exemplo:** Em um cenário de pré-preenchimento de dados, para preencher campos com valor padrão `'Adaptive Forms'` quando seu valor é salvo como nulo, a expressão do script de inicialização é:
`if(this.value==null) this.value='Adaptive Forms';`

### Expressão de opções {#options-expression}

A expressão options é usada para preencher dinamicamente as opções de um campo de lista suspensa.

**Aplica-se a**: campos de lista suspensa

**Tipo de retorno**: A expressão options retorna uma matriz de valores de string. Cada valor pode ser uma string simples, como **Masculino** ou em um formato de par chave=valor, como **1=Masculino**

**Exemplo**: Para preencher o valor de um campo, com base no valor de outro campo, forneça uma expressão de opções simples. Por exemplo, para preencher um campo, **Número de crianças**, com base no **Estado civil** expresso em outro campo, a expressão é:

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

Sempre que o valor de **estado_civil** for alterado, a expressão será reacionada. Também é possível preencher a lista suspensa em um serviço REST. Para obter informações detalhadas, consulte [Preenchimento dinâmico de menus suspensos](../../forms/using/dynamically-populate-dropdowns.md).

### Expressão de resumo {#summary}

A expressão Resumo calcula dinamicamente o título de um painel filho de um painel de layout de acordeão. Você pode especificar a expressão Resumo em uma regra, que usa um campo de formulário ou uma lógica personalizada para avaliar o título. A expressão é executada quando o formulário é inicializado. Se um formulário estiver sendo preenchido previamente, a expressão será executada depois que os dados forem preenchidos previamente ou quando o valor dos campos dependentes usados na expressão for alterado.

Normalmente, a expressão Resumo é usada para filhos repetitivos de um painel de layout de acordeão para fornecer um título significativo para cada painel filho.

**Aplica-se a:** Painéis que são filhos diretos de um painel cujo layout está configurado como Acordeão.

**Tipo de retorno:** A expressão retorna uma String que se torna o título da opção.

**Exemplo:** &quot;Número da conta : &quot; + textbox1.value

### Validar expressão {#validate-expression}

A expressão validate é usada para validar os campos usando a expressão fornecida. Normalmente, essas expressões usam expressões regulares juntamente com o valor do campo para validar um campo. A expressão é reacionada e o status de validação do campo é recalculado em qualquer alteração no valor de um campo.

**Aplica-se a**: campos

**Tipo de retorno**: A expressão retorna um valor booleano, representando o status de validação do campo. O valor **false** representa que o campo é inválido e **true** representa que o campo é válido.
**Exemplo**: Para um campo que representa código postal do Reino Unido, a expressão de validação é:

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

No exemplo acima, se o valor que não está vazio não corresponder ao padrão, a expressão retornará **false** para indicar que o campo não é válido.

>[!NOTE]
>
>Se você gravar uma expressão de validação para um campo não obrigatório ou obrigatório, a expressão será avaliada independentemente do status de visibilidade do campo. Para interromper a validação dos campos ocultos, defina a propriedade validationsDisabled no Script de confirmação de inicialização ou valor como true. Por exemplo, `this.validationsDisabled=true`

### Script de Value Commit {#value-commit-script}

O script Value Commit é acionado quando:

* Um usuário altera o valor de um campo da interface do usuário.
* O valor de um campo é alterado programaticamente devido a uma alteração em outro campo.

**Aplica-se a:** campos

**Tipo de retorno:** A expressão de script de confirmação de valor não retorna nenhum valor. Se qualquer expressão retornar um valor, o valor será ignorado.

**Exemplo:** Para converter as letras maiúsculas e minúsculas digitadas no campo em commit, a expressão de confirmação de valor é:
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>Você pode desativar a execução do Script de confirmação de valor quando o valor de um campo é alterado programaticamente. Para fazer isso, acesse https://&#39;[server]:[porta]&#39;/system/console/configMgr and change **Versão adaptável do Forms para compatibilidade** para **AEM Forms 6.1**. Consequentemente, o script de confirmação de valor é executado somente quando o usuário altera o valor do campo da interface do usuário.

### Expressão de visibilidade {#visibility-expression}

A expressão Visibility é usada para controlar a visibilidade do campo/painel. Normalmente, a expressão de visibilidade usa a propriedade value de um campo e é reacionada sempre que esse valor é alterado.

**Aplica-se a**: campos e painel

**Tipo de retorno**: A expressão retorna um valor booleano, representando o campo/painel que está visível ou não. **false** representa que o campo ou painel não está visível e true representa que o campo ou painel está visível.

**Exemplo**: Para um painel que se torna visível somente se o valor de **field1** está definida como **Masculino**, a expressão de visibilidade é: `field1.value == "Male"`

### Expressão de conclusão de etapa {#step-completion-expression}

A expressão de conclusão de etapa é usada para impedir que um usuário vá para a próxima etapa de um layout de assistente. Essas expressões são usadas quando os painéis têm um layout de assistente (um formulário de várias etapas que mostra uma etapa de cada vez). O usuário pode se mover para a próxima etapa, painel ou subseção somente se todos os valores necessários na seção atual forem preenchidos e válidos.

**Aplica-se a**: Painéis com layout do item definido como assistente.

**Tipo de retorno**: A expressão retorna um valor booleano, representando o painel atual como válido ou não. **Verdadeiro** representa que o painel atual é válido e o usuário pode navegar para o próximo painel.

**Exemplo**: Em um formulário organizado em vários painéis, antes de navegar até o próximo painel, o painel atual é validado. Nesses casos, as expressões de conclusão de etapas são usadas. Geralmente, essas expressões usam a API de validação GuideBridge. Um exemplo de expressão de conclusão de etapa é:
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## Validações no formulário adaptável {#validations-in-adaptive-form}

Existem vários métodos para adicionar a validação de campo a um formulário adaptável. Se uma verificação de validação for adicionada em um campo, **Verdadeiro** representa que o valor inserido no campo é válido. **Falso** representa que o valor é inválido. Se você inserir ou sair de um campo, a mensagem de erro não será gerada.

Os métodos para adicionar validações em um campo são:

### Obrigatório {#required}

Para tornar um componente obrigatório, no **Editar** da caixa de diálogo do componente, é possível selecionar a opção **Título e texto > Obrigatório**. Você também pode adicionar o **mensagem obrigatória** (opcional) também. .

### Padrões de validação {#validation-patterns}

Há vários padrões de validação prontos para uso disponíveis para um campo. Para selecionar um padrão de validação, na **Editar** da caixa de diálogo do componente, localize o **Padrões** e selecione **padrões**. Você pode criar seu próprio padrão de validação personalizado em um **Padrão** caixa de texto. O status de validação é retornado **Verdadeiro** somente se os dados preenchidos estiverem em conformidade com o padrão de validação, ou **Falso** é retornado. Para escrever seu próprio padrão de validação personalizado, consulte [Suporte a cláusula de imagem para formulários HTML5](/help/forms/using/picture-clause-support.md).

### Expressões de validação {#validation-expressions}

A validação de um campo também pode ser calculada usando expressões em campos diferentes. Essas expressões são escritas dentro de **Script de validação** do **Script** guia de **Editar** do componente. O status de validação de um campo depende do valor retornado pela expressão. Para obter informações sobre como gravar essas expressões, consulte [Validar expressão](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p).

## Informações adicionais {#additional-information}

### Uso do formato de exibição de campo {#using-field-display-format}

Formato de exibição pode ser usado para exibir os dados em diferentes formatos. Por exemplo, você pode usar o formato de exibição para exibir um número de telefone com hifens, formatar CEP ou seletor de data. Esses padrões de exibição podem ser selecionados no **Padrões** seção da caixa de diálogo Editar de um componente. Você pode gravar padrões de exibição personalizados semelhantes aos padrões de validação mencionados acima.

### GuideBridge - APIs e eventos {#guidebridge-apis-and-events}

O GuideBridge é uma coleção de APIs que podem ser usadas para interagir com formulários adaptáveis no modelo de memória em um navegador. Para obter uma introdução detalhada da API do Guide Bridge, métodos de classe, eventos expostos, consulte [Referência da API da biblioteca JavaScript para formulários adaptáveis](https://helpx.adobe.com/aem-forms/6/javascript-api/).

>[!NOTE]
>
>É recomendável não usar os ouvintes de eventos do GuideBridge nas expressões.

#### Uso do GuideBridge em várias expressões {#guidebridge-usage-in-various-expressions}

* Para redefinir campos de formulário, é possível acionar `guideBridge.reset()` API na expressão click de um botão. Da mesma forma, há uma API de envio que pode ser chamada como uma expressão de clique `guideBridge.submit()`**.**

* Você pode usar o `setFocus()` API para definir o foco em vários campos ou painéis (para que o foco do painel seja definido automaticamente para o primeiro campo). `setFocus()`O fornece uma grande variedade de opções para navegar, como navegação em painéis, travessia anterior/seguinte, definição do foco para um campo específico e muito mais. Por exemplo, para ir para o próximo painel, você pode usar: `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* Para validar um formulário adaptável ou seus painéis específicos, use `guideBridge.validate(errorList, somExpression).`

#### Uso do GuideBridge fora das expressões  {#using-guidebridge-outside-expressions-nbsp}

Também é possível usar as APIs do GuideBridge fora das expressões. Por exemplo, você pode usar a API GuideBridge para definir a comunicação entre a HTML de página que hospeda o formulário adaptável e o Modelo de formulário. Além disso, é possível definir o valor que vem do pai do Iframe que hospeda o formulário.

Para usar a API GuideBridge para o exemplo acima mencionado, capture uma instância de GuideBridge. Para capturar a instância, analise `bridgeInitializeStart`de um `window`objeto:

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
>No AEM, é uma boa prática gravar código em um clientLib e incluí-lo em sua página (header.jsp ou footer.jsp da página)

Para usar o GuideBridge após a inicialização do formulário (a variável `bridgeInitializeComplete` for despachado), obtenha a instância do GuideBridge usando `window.guideBridge`. Você pode verificar o status de inicialização do GuideBridge usando o `guideBride.isConnected` API.

#### Eventos GuideBridge {#guidebridge-events}

O GuideBridge também fornece determinados eventos para scripts externos na página de hospedagem. Os scripts externos podem acompanhar esses eventos e executar várias operações. Por exemplo, sempre que o nome de usuário em um formulário é alterado, o nome mostrado no cabeçalho da página também é alterado. Para obter mais detalhes sobre esses eventos, consulte [Referência da API da biblioteca JavaScript para formulários adaptáveis](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

Use o seguinte código para registrar manipuladores:

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### Criação de padrões personalizados para um campo {#creating-custom-patterns-for-a-field}

Como mencionado acima, formulários adaptáveis permitem que o autor forneça padrões para formatos de validação ou exibição. Além de usar padrões prontos para uso, você pode definir padrões personalizados reutilizáveis para um componente de formulário adaptável. Por exemplo, é possível definir um campo de texto ou um campo numérico. Depois de definido, você pode usar esses padrões em todos os formulários para o tipo especificado de componente. Por exemplo, você pode criar um padrão personalizado para um campo de texto e usá-lo nos campos de texto em seus formulários adaptáveis. Você pode selecionar o padrão personalizado acessando a seção padrão na caixa de diálogo Editar de um componente. Para obter detalhes sobre a definição ou o formato do padrão, consulte [Suporte a cláusula de imagem para formulários HTML5](/help/forms/using/picture-clause-support.md).

Execute as seguintes etapas para criar um padrão personalizado para um tipo de campo específico e reutilizá-lo para outros campos do mesmo tipo:

1. Navegue até o CRXDE Lite na sua instância de criação.
1. Crie uma pasta para manter seus padrões personalizados. No diretório /apps, crie um nó do tipo sling:folder. Por exemplo, crie um nó com o nome `customPatterns`. Nesse nó, crie outro nó do tipo `nt:unstructed` e nomeá-lo `textboxpatterns`. Este nó contém os vários padrões personalizados que você deseja adicionar.
1. Abra a guia Properties do nó criado. Por exemplo, abra a guia Propriedades de `textboxpatterns`. Adicione o `guideComponentType` para esse nó e defina seu valor como *fd/af/components/formatter/guideTextBox*.

1. O valor dessa propriedade varia dependendo do campo para o qual você deseja definir os padrões. Para campos numéricos, o valor da variável `guideComponentType` a propriedade é *fd/af/components/formatter/guideNumericBox*. O valor do campo Datepicker é *fd/af/components/formatter/guideDatepicker*. &quot;
1. Você pode adicionar um padrão personalizado atribuindo uma propriedade ao `textboxpatterns` nó . Adicionar uma propriedade com um nome (por exemplo, `pattern1`) e defina seu valor para o padrão que deseja adicionar. Por exemplo, adicione uma propriedade `pattern1` com o valor Fax=text{99-999-999999}. O padrão está disponível para todas as caixas de texto usadas no Adaptive Forms.

   ![Criação de padrões personalizados para campos no CrxDe](assets/creating-custom-patterns.png)

   Criação de padrões personalizados
