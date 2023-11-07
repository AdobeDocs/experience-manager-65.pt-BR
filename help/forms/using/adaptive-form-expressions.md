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
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2802'
ht-degree: 0%

---

# Expressões de formulário adaptável{#adaptive-form-expressions}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

Os formulários adaptáveis fornecem experiência de preenchimento de formulário otimizada e simplificada para usuários finais com recursos de script dinâmicos. Ele permite escrever expressões para adicionar vários comportamentos, como campos e painéis de exibição/ocultação dinâmicos. Também permite adicionar campos calculados, tornar os campos somente leitura, adicionar lógica de validação e muito mais. O comportamento dinâmico é baseado na entrada do usuário ou em dados pré-preenchidos.

JavaScript é a linguagem de expressão de formulários adaptáveis. Todas as expressões são expressões JavaScript válidas e usam APIs de modelo de script de formulários adaptáveis. Essas expressões retornam valores de determinados tipos. Para obter a lista completa de classes de formulários adaptáveis, eventos, objetos e APIs públicas, consulte [Referência da API da biblioteca JavaScript para formulários adaptáveis](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## Práticas recomendadas para escrever expressões {#best-practices-for-writing-expressions}

* Ao escrever expressões, para acessar campos e painéis, é possível usar o nome do campo ou painel. Para acessar o valor de um campo, use a propriedade value. Por exemplo, `field1.value`
* Use nomes exclusivos para campos e painéis em todo o formulário. Ajuda a evitar possíveis conflitos com nomes de campo usados ao gravar expressões.
* Ao gravar expressões de várias linhas, use um ponto e vírgula para encerrar uma instrução.

## Práticas recomendadas para expressões envolvendo o painel de repetição {#best-practices-for-expressions-involving-repeating-panel}

Os painéis repetitivos são instâncias de um painel que são adicionadas ou removidas dinamicamente, usando a API de script ou dados pré-preenchidos. Para obter informações detalhadas sobre o uso do painel repetitivo, consulte [criação de formulários com seções repetíveis](/help/forms/using/creating-forms-repeatable-sections.md).

* Para criar um painel de repetição, na caixa de diálogo do painel, abra as configurações e defina o valor do campo contagem máxima como mais de 1.
* O valor da contagem mínima das configurações de repetição do painel pode ser um ou mais, mas não pode ser maior do que o valor da contagem máxima.
* Quando uma expressão se refere a um campo do painel de repetição, os nomes de campo na expressão são resolvidos para o elemento de repetição mais próximo.
* Formulários adaptáveis fornecem algumas funções especiais para simplificar a computação para painéis repetíveis, como soma, contagem, mínimo, máximo, filtro e muito mais. Para obter a lista completa das funções, consulte [Referência da API da biblioteca JavaScript para formulários adaptáveis](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* As APIs para manipular instâncias do painel de repetição são:

   * Para adicionar uma ocorrência de painel: `panel1.instanceManager.addInstance()`
   * Para obter um índice de repetição do painel: `panel1.instanceIndex`
   * Para obter o instanceManager de um painel: `_panel1 or panel1.instanceManager`
   * Para remover uma ocorrência de um painel: `_panel1.removeInstance(panel1.instanceIndex)`

## Tipos de expressão {#expression-types}

Nos formulários adaptáveis, é possível escrever expressões para adicionar comportamentos, como campos e painéis de exibição/ocultação dinâmicos. Você também pode escrever expressões para adicionar campos calculados, tornar os campos somente leitura, lógica de validação e muito mais. Os formulários adaptáveis oferecem suporte às seguintes expressões:

* **[Acessar expressões](#access-expression-enablement-expression)**: para ativar/desativar um campo.
* **[Calcular expressões](#calculate-expression)**: para calcular automaticamente o valor de um campo.
* **[Expressão de clique](#click-expression)**: para lidar com ações no evento de clique de um botão.
* **[Script de inicialização](#initialization-script):** executar uma ação na inicialização de um campo.
* **[Expressão de opções](#options-expression)**: para preencher dinamicamente uma lista suspensa.
* **[Expressão de resumo](#summary)**: para calcular dinamicamente o título de um acordeão.
* **[Validar expressões](#validate-expression)**: para validar um campo.
* **[Script de Value Commit](#value-commit-script):** para alterar os componentes de um formulário depois que o valor de um campo é alterado.
* **[Expressão de visibilidade](#visibility-expression)**: para controlar a visibilidade de um campo e painel.
* **[Expressão de conclusão da etapa](#step-completion-expression)**: para impedir que um usuário vá para a próxima etapa de um assistente.

### Expressão de acesso (expressão de ativação) {#access-expression-enablement-expression}

Você pode usar a expressão de acesso para ativar ou desativar um campo. Se a expressão usar o valor de um campo, sempre que o valor do campo for alterado, a expressão será acionada novamente.

**Aplicável a**: campos

**Tipo de retorno**: a expressão retorna um valor booliano que representa se o campo está ativado ou desativado. **true** representa que o campo está ativado e **false** representa que o campo está desativado.

**Exemplo**: para habilitar um campo somente quando o valor de **campo1** está definida como **X**, a expressão de acesso é: `field1.value == "X"`

### Calcular expressão {#calculate-expression}

A expressão calculate é usada para calcular automaticamente o valor de um campo usando uma expressão. Normalmente, essa expressão usa a propriedade value de outros campos. Por exemplo, `field2.value + field3.value`. Sempre que o valor de `field2`ou `field3`for alterada, a expressão será acionada novamente e o valor será recalculado.

**Aplicável a**: campos

**Tipo de retorno**: a expressão retorna um valor compatível com o campo onde o resultado da expressão é exibido (por exemplo, decimal).

**Exemplo**: a expressão Calculado para mostrar a soma de dois campos em **campo1** é:
`field2.value + field3.value`

### Expressão de clique {#click-expression}

A expressão de clique lida com as ações executadas no evento de clique de um botão. Imediatamente, o GuideBridge fornece APIs para executar várias funções, como enviar, validar, que são usadas junto com a expressão de clique. Para obter uma lista completa das APIs, consulte [APIs do GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**Aplicável a**: Campos de botão

**Tipo de retorno**: a expressão de clique não retorna nenhum valor. Se qualquer expressão retornar um valor, ele será ignorado.

**Exemplo**: para preencher uma caixa de texto **caixa de texto1** na ação de clique de um botão com valor **AEM Forms**, a expressão de clique do botão é `textbox1.value="AEM Forms"`

### Script de inicialização {#initialization-script}

O script de inicialização é acionado quando um formulário adaptável é inicializado. Dependendo dos cenários, o script de inicialização se comporta da seguinte maneira:

* Quando um formulário adaptável é renderizado sem um preenchimento prévio de dados, o script de inicialização é executado depois que o formulário é inicializado.
* Quando um formulário adaptável é renderizado com um preenchimento prévio de dados, o script é executado após a conclusão da operação de preenchimento prévio.
* Quando a revalidação de um formulário adaptável pelo lado do servidor é acionada, o script de inicialização é executado.

**Aplicável a:** campos e painel

**Tipo de retorno:** A expressão do script de Inicialização não retorna nenhum valor. Se qualquer expressão retornar um valor, ele será ignorado.

**Exemplo:** Em um cenário de pré-preenchimento de dados, para preencher campos com o valor padrão `'Adaptive Forms'` quando o valor é salvo como nulo, a expressão do script de inicialização é:
`if(this.value==null) this.value='Adaptive Forms';`

### Expressão de opções {#options-expression}

A expressão options é usada para preencher dinamicamente as opções de um campo de lista suspensa.

**Aplicável a**: campos de lista suspensa

**Tipo de retorno**: a expressão options retorna uma matriz de valores de sequência. Cada valor pode ser uma string simples, como **Masculino** ou em um formato de par chave=valor, como **1=Masculino**

**Exemplo**: para preencher o valor de um campo, com base no valor de outro campo, forneça uma expressão de opções simples. Por exemplo, para preencher um campo, **Número de crianças**, com base no **Estado civil** expressa em outro campo, a expressão é:

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

Sempre que o valor de **estado civil** for alterada, a expressão será acionada novamente. Você também pode preencher a lista suspensa de um serviço REST. Para obter informações detalhadas, consulte [Preenchimento dinâmico de menus suspensos](../../forms/using/dynamically-populate-dropdowns.md).

### Expressão de resumo {#summary}

A expressão Resumo calcula dinamicamente o título de um painel secundário de um painel de layout do Accordion. Você pode especificar a expressão Summary em uma regra, que usa um campo de formulário ou uma lógica personalizada para avaliar o título. A expressão é executada quando o formulário é inicializado. Se você estiver preenchendo previamente um formulário, a expressão será executada após o preenchimento prévio dos dados ou quando o valor dos campos dependentes usados na expressão for alterado.

A expressão Resumo é normalmente usada para repetir filhos de um painel de layout de acordeão a fim de fornecer um título significativo para cada painel filho.

**Aplicável a:** Painéis que são filhos diretos de um painel cujo layout está configurado como Acordeão.

**Tipo de retorno:** A expressão retorna uma Cadeia de caracteres que se torna o título do acordeão.

**Exemplo:** &quot;Número da conta : &quot; + textbox1.value

### Validar expressão {#validate-expression}

A expressão validate é usada para validar os campos usando a expressão fornecida. Normalmente, essas expressões usam expressões regulares junto com o valor do campo para validar um campo. A expressão é acionada novamente e o status de validação do campo é recalculado em qualquer alteração no valor de um campo.

**Aplicável a**: campos

**Tipo de retorno**: a expressão retorna um valor booliano, representando o status de validação do campo. O valor **false** representa que o campo é inválido e **true** representa que o campo é válido.
**Exemplo**: para um campo que representa o código postal do Reino Unido, a expressão de validação é:

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

No exemplo acima, se o valor não vazio não corresponder ao padrão, a expressão retornará **false** para indicar que o campo não é válido.

>[!NOTE]
>
>Se você escrever uma expressão de validação para um campo não obrigatório ou obrigatório, a expressão será avaliada independentemente do status de visibilidade do campo. Para interromper a validação para os campos ocultos, defina a propriedade validationsDisabled no Script de Inicialização ou Confirmação de Valor como true. Por exemplo, `this.validationsDisabled=true`

### Script de Value Commit {#value-commit-script}

O script de Value Commit é acionado quando:

* Um usuário altera o valor de um campo da interface do.
* O valor de um campo muda programaticamente devido à alteração em outro campo.

**Aplicável a:** campos

**Tipo de retorno:** A expressão de script de confirmação de valor não retorna nenhum valor. Se qualquer expressão retornar um valor, ele será ignorado.

**Exemplo:** Para converter letras maiúsculas e minúsculas inseridas no campo em confirmação, a expressão de confirmação de valor é:
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>Você poderá desativar a execução do Script de Value Commit quando o valor de um campo for alterado programaticamente. Para fazer isso, acesse https://&#39;[server]:[porta]&#39;/system/console/configMgr e alteração **Versão adaptável do Forms para compatibilidade** para **AEM Forms 6.1**. Consequentemente, o Script de confirmação de valor é executado somente quando o usuário altera o valor do campo da interface do usuário.

### Expressão de visibilidade {#visibility-expression}

A expressão Visibility é usada para controlar a visibilidade do campo/painel. Normalmente, a expressão de visibilidade usa a propriedade de valor de um campo e é acionada novamente sempre que esse valor é alterado.

**Aplicável a**: campos e painel

**Tipo de retorno**: a expressão retorna um valor booleano, representando que o campo/painel está visível ou não. **false** representa que o campo ou painel não está visível e true representa que o campo ou painel está visível.

**Exemplo**: para um painel que se torna visível somente se o valor de **campo1** está definida como **Masculino**, a expressão de visibilidade é: `field1.value == "Male"`

### Expressão de conclusão da etapa {#step-completion-expression}

A expressão de conclusão da etapa é usada para impedir que um usuário vá para a próxima etapa de um layout do assistente. Essas expressões são usadas quando os painéis têm um layout de assistente (um formulário de várias etapas que mostra uma etapa de cada vez). O usuário pode mover para a próxima etapa, painel ou subseção somente se todos os valores necessários na seção atual estiverem preenchidos e forem válidos.

**Aplicável a**: painéis com layout de item definido como assistente.

**Tipo de retorno**: a expressão retorna um valor booleano, representando que o painel atual é válido ou não. **True** representa que o painel atual é válido e que o usuário pode navegar até o próximo painel.

**Exemplo**: em um formulário organizado em vários painéis, antes de navegar até o próximo painel, o painel atual é validado. Nesses casos, as expressões de conclusão da etapa são usadas. Geralmente, essas expressões usam a API de validação do GuideBridge. Um exemplo de expressão de conclusão de etapa é:
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## Validações no Formulário adaptável {#validations-in-adaptive-form}

Há vários métodos para adicionar validação de campo a um formulário adaptável. Se uma verificação de validação for adicionada em um campo, **True** representa que o valor inserido no campo é válido. **Falso** representa que o valor é inválido. Se você inserir e sair por tabulação em um campo, a mensagem de erro não será gerada.

Os métodos para adicionar validações em um campo são:

### Obrigatório {#required}

Para tornar um componente obrigatório, na variável **Editar** caixa de diálogo do componente, é possível selecionar a opção **Título e texto > Obrigatório**. Você também pode adicionar as **mensagem obrigatória** (opcional) também. .

### Padrões de validação {#validation-patterns}

Há vários padrões de validação prontos para uso disponíveis para um campo. Para selecionar um padrão de validação, na variável **Editar** caixa de diálogo do componente, localize a **Padrões** e selecione **padrões**. Você pode criar seu próprio padrão de validação personalizado em uma **Padrão** texto. O status de validação é retornado **True** se os dados preenchidos forem compatíveis com o padrão de validação, caso contrário **Falso** é retornado. Para escrever seu próprio padrão de validação personalizado, consulte [Suporte a cláusula de imagem para formulários HTML5](/help/forms/using/picture-clause-support.md).

### Expressões de validação {#validation-expressions}

A validação de um campo também pode ser calculada usando expressões em campos diferentes. Essas expressões são escritas dentro de **Script de validação** do campo **Script** guia de **Editar** caixa de diálogo do componente. O status de validação de um campo depende do valor retornado pela expressão. Para obter informações sobre como escrever essas expressões, consulte [Validar expressão](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p).

## Informações adicionais {#additional-information}

### Utilização do formato de exibição de campo {#using-field-display-format}

O Formato de Exibição pode ser usado para exibir os dados em diferentes formatos. Por exemplo, você pode usar o formato de exibição para exibir um número de telefone com hifens, código postal de formato ou seletor de datas. Esses padrões de exibição podem ser selecionados no **Padrões** seção da caixa de diálogo Editar de um componente. Você pode gravar padrões de exibição personalizados semelhantes aos padrões de validação mencionados acima.

### GuideBridge - APIs e eventos {#guidebridge-apis-and-events}

O GuideBridge é uma coleção de APIs que podem ser usadas para interagir com formulários adaptáveis no modelo de memória em um navegador. Para obter uma introdução detalhada à API do Guide Bridge, aos métodos de classe e aos eventos expostos, consulte [Referência da API da biblioteca JavaScript para formulários adaptáveis](https://helpx.adobe.com/aem-forms/6/javascript-api/).

>[!NOTE]
>
>É recomendável não usar os ouvintes de eventos do GuideBridge nas expressões.

#### Uso do GuideBridge em várias expressões {#guidebridge-usage-in-various-expressions}

* Para redefinir campos de formulário, é possível acionar `guideBridge.reset()` API na expressão de clique de um botão. Da mesma forma, há uma API de envio que pode ser chamada como uma expressão de clique `guideBridge.submit()`**.**

* Você pode usar o `setFocus()` API para definir o foco em vários campos ou painéis (para foco do painel, é definido para o primeiro campo automaticamente). `setFocus()`O fornece uma grande variedade de opções para navegar, como navegar pelos painéis, percorrer antes/depois, definir o foco para um campo específico e muito mais. Por exemplo, para mover para o próximo painel, é possível usar: `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* Para validar um formulário adaptável ou seus painéis específicos, use `guideBridge.validate(errorList, somExpression).`

#### Usando expressões externas do GuideBridge  {#using-guidebridge-outside-expressions-nbsp}

Você também pode usar as APIs do GuideBridge fora das expressões. Por exemplo, você pode usar a API do GuideBridge para definir a comunicação entre o HTML de página que hospeda o formulário adaptável e o Modelo de formulário. Além disso, você pode definir o valor que vem do pai do Iframe que hospeda o formulário.

Para usar a API do GuideBridge para o exemplo mencionado acima, capture uma instância do GuideBridge. Para capturar a instância, acompanhe `bridgeInitializeStart`evento de um `window`objeto:

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
>No AEM, é uma boa prática escrever código em uma clientLib e incluí-lo em sua página (header.jsp ou footer.jsp da página)

Para usar o GuideBridge depois que o formulário for inicializado (o `bridgeInitializeComplete` for despachado), obtenha a instância do GuideBridge usando `window.guideBridge`. Você pode verificar o status de inicialização do GuideBridge usando o `guideBride.isConnected` API.

#### Eventos do GuideBridge {#guidebridge-events}

O GuideBridge também fornece determinados eventos para scripts externos na página de hospedagem. Os scripts externos podem ouvir esses eventos e executar várias operações. Por exemplo, sempre que o nome de usuário em um formulário for alterado, o nome mostrado no cabeçalho da página também será alterado. Para obter mais detalhes sobre esses eventos, consulte [Referência da API da biblioteca JavaScript para formulários adaptáveis](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

Use o código a seguir para registrar manipuladores:

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### Criação de padrões personalizados para um campo {#creating-custom-patterns-for-a-field}

Como mencionado acima, os formulários adaptáveis permitem que o autor forneça padrões para validação ou formatos de exibição. Além de usar padrões prontos para uso, é possível definir um padrão personalizado reutilizável para um componente de formulário adaptável. Por exemplo, você pode definir um campo de texto ou numérico. Depois de definido, é possível usar esses padrões em todos os formulários para o tipo especificado de componente. Por exemplo, você pode criar um padrão personalizado para um campo de texto e usá-lo nos campos de texto em seus formulários adaptáveis. Você pode selecionar o padrão personalizado acessando a seção Padrão na caixa de diálogo de edição de um componente. Para obter detalhes sobre definição ou formato do Padrão, consulte [Suporte a cláusula de imagem para formulários HTML5](/help/forms/using/picture-clause-support.md).

Execute as seguintes etapas para criar um padrão personalizado para um tipo de campo específico e reutilizá-lo para outros campos do mesmo tipo:

1. Navegue até o CRXDE Lite na instância de criação.
1. Crie uma pasta para manter seus padrões personalizados. No diretório /apps, crie um nó do tipo sling:folder. Por exemplo, crie um nó com o nome `customPatterns`. Neste nó, crie outro nó do tipo `nt:unstructed` e nomeie-o `textboxpatterns`. Este nó contém vários padrões personalizados que você deseja adicionar.
1. Abra a guia Properties do nó criado. Por exemplo, abra a guia Propriedades de `textboxpatterns`. Adicione o `guideComponentType` para esse nó e defina seu valor como *fd/af/components/formatter/guideTextBox*.

1. O valor dessa propriedade varia dependendo do campo para o qual você deseja definir os padrões. Para campo numérico, o valor de `guideComponentType` propriedade é *fd/af/components/formatter/guideNumericBox*. O valor do campo Datepicker é *fd/af/components/formatter/guideDatepicker*. &quot;
1. Você pode adicionar um padrão personalizado atribuindo uma propriedade à variável `textboxpatterns` nó. Adicione uma propriedade com um nome (por exemplo, `pattern1`) e defina seu valor com o padrão que deseja adicionar. Por exemplo, adicionar uma propriedade `pattern1` com o valor Fax=text{99-999-9999999}. O padrão está disponível para todas as Caixas de texto usadas no Forms adaptável.

   ![Criação de padrões personalizados para campos no CrxDe](assets/creating-custom-patterns.png)

   Criação de padrões personalizados
