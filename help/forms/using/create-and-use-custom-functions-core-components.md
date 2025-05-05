---
title: Criar e adicionar funções personalizadas em um Formulário adaptável
description: O AEM Forms é compatível com funções personalizadas que permitem aos usuários criar e usar suas próprias funções no editor de regras.
keywords: Adicionar uma função personalizada, usar uma função personalizada, criar uma função personalizada, usar a função personalizada no editor de regras.
content-type: reference
feature: Adaptive Forms, Core Components
role: Admin, User, Developer
exl-id: 00073e3a-f1b5-4c42-9fea-4a14b8a22c81
source-git-commit: 7f1283898cbeebdedb7bdea6f0a8d9db567617ee
workflow-type: tm+mt
source-wordcount: '3385'
ht-degree: 0%

---

# Funções personalizadas nos Componentes principais do Forms adaptável

Este artigo descreve como criar funções personalizadas com o componente principal de formulário adaptável mais recente, que tem os recursos mais recentes, como:

* Recurso de armazenamento em cache para funções personalizadas
* Suporte a objetos de escopo global e objetos de campo para Funções personalizadas
* Suporte para recursos modernos do JavaScript, como funções de esquerda e seta (suporte para ES10)

Defina a [versão mais recente do formulário](https://github.com/adobe/aem-core-forms-components/tree/release/650) no ambiente do Componente principal do AEM Forms para usar os recursos mais recentes nas Funções personalizadas. </span>


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | Este artigo |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |

## Introdução

O AEM Forms 6.5 inclui funções do JavaScript que permitem definir regras de negócios complexas usando o editor de regras. Embora o AEM Forms ofereça várias funções personalizadas prontas para uso, muitos casos de uso exigem a definição de suas próprias funções personalizadas para serem usadas em vários formulários. Essas funções personalizadas aprimoram os recursos de formulários permitindo que a manipulação e o processamento dos dados inseridos atendam a requisitos específicos. Além disso, elas permitem a alteração dinâmica do comportamento do formulário com base nos critérios predefinidos.

### Usos de funções personalizadas {#uses-of-custom-function}

As vantagens de usar funções personalizadas nos Componentes principais do Forms adaptável são:


* **Gerenciamento de dados**: funções personalizadas gerenciam e processam dados inseridos nos campos de formulários.
* **Processamento de dados**: as funções personalizadas ajudam a processar dados inseridos nos campos de formulários.
* **Validação de dados**: as funções personalizadas permitem que você execute verificações personalizadas nas entradas do formulário e forneça mensagens de erro especificadas.
* **Comportamento dinâmico**: as funções personalizadas permitem que você controle o comportamento dinâmico de seus formulários com base em condições específicas. Por exemplo, você pode mostrar/ocultar campos, modificar valores de campo ou ajustar a lógica do formulário dinamicamente.
* **Integração**: você pode usar funções personalizadas para integrar-se a APIs ou serviços externos. Ele ajuda a buscar dados de fontes externas, enviar dados para endpoints Rest externos ou executar ações personalizadas com base em eventos externos.

As funções personalizadas são essencialmente bibliotecas de clientes adicionadas ao arquivo do JavaScript. Depois de criar uma Função personalizada, ela fica disponível no editor de regras para seleção pelo usuário em um Formulário adaptável. As funções personalizadas são identificadas pelas anotações do JavaScript no editor de regras.

### Anotações do JavaScript compatíveis com a função personalizada {#js-annotations}

**As anotações do JavaScript fornecem metadados para o código JavaScript**. Inclui comentários que começam com símbolos específicos, por exemplo, `/**` e `@`. As anotações fornecem informações importantes sobre funções, variáveis e outros elementos no código. O Formulário adaptável é compatível com as seguintes anotações do JavaScript para funções personalizadas:

#### Nome

O **Name** é usado para identificar a função personalizada no editor de regras de um formulário adaptável. As seguintes sintaxes são usadas para nomear uma Função Personalizada:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`

>[!NOTE]
>`[functionName]` é o nome da função. Espaços não são permitidos.
>`<Function Name>` é o nome de exibição da função no editor de regras do Adaptive Forms.
>Se o nome da função for idêntico ao nome da própria função, você poderá omitir `[functionName]` da sintaxe.

#### Parâmetro

O **Parâmetro** é uma lista de argumentos usados por funções personalizadas. Uma função pode suportar vários parâmetros. As sintaxes a seguir são usadas para definir um parâmetro em uma função personalizada:

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`

  `{type}` representa o tipo de parâmetro. Os tipos de parâmetros permitidos são:

   * string: representa um único valor de string.
   * number: representa um único valor numérico.
   * booleano: representa um único valor booleano (verdadeiro ou falso).
   * cadeia de caracteres []: representa uma matriz de valores de cadeia de caracteres.
   * número[]: representa uma matriz de valores numéricos.
   * booleano[]: representa uma matriz de valores booleanos.
   * date: representa um único valor de data.
   * date[]: representa uma matriz de valores de data.
   * array: representa uma matriz genérica contendo valores de vários tipos.
   * object: representa o objeto de formulário passado para uma função personalizada em vez de passar seu valor diretamente.
   * escopo: representa o objeto global, que contém variáveis somente leitura, como instâncias de formulário, instâncias de campo de destino e métodos para executar modificações de formulário nas funções personalizadas. Ele é declarado como o último parâmetro nas anotações do JavaScript e não está visível para o editor de regras de um Formulário adaptável. O parâmetro scope acessa o objeto do formulário ou componente para acionar a regra ou o evento necessário para o processamento do formulário. Para obter mais informações sobre o objeto Globals e como usá-lo, [clique aqui](/help/forms/using/create-and-use-custom-functions-core-components.md#field-and-global-scope-objects-in-custom-functions-support-field-and-global-objects)

O tipo Parameter é **não diferencia maiúsculas de minúsculas** e espaços não são permitidos no nome do parâmetro.

`<Parameter Description>` contém detalhes sobre a finalidade do parâmetro. Ele pode ter várias palavras.

<!--

**Optional Parameters**
By default, all parameters are mandatory. You can define a parameter as optional by either adding `=` after the parameter type or enclosing the parameter name in `[]`. Parameters defined as optional in JavaScript annotations are displayed as optional in the rule editor.
To define a variable as an optional parameter, you can use the any of the following syntaxes:
  
* `@param {type=} Input1`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {string=<value>} input1`
        
`input1` as an optional parameter with the default value set to `value`. 

* `@param {type} [Input1]`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {array} [input1=<value>]`

    `input1` is an optional parameter of array type with the default value set to `value`. 
    Ensure that the parameter type is enclosed in curly brackets {} and the parameter name is enclosed in square brackets []. 

Consider the following code snippet, where input2 is defined as an optional parameter:

```javascript

        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

The following illustration displays using the `OptionalParameterFunction` csutom function in the rule editor:

![Optional or required parameters ](/help/forms/using/assets/optional-default-params.png)

You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

![incomplete rule warning](/help/forms/using/assets/incomplete-rule.png)

When user leaves the optional parameter empty, then the "Undefined" value is passed to the custom function for the optional parameter.

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

-->

#### Tipo de retorno

O tipo de retorno especifica o tipo de valor que a função personalizada retorna após a execução. As sintaxes a seguir são usadas para definir um tipo de retorno em uma função personalizada:

* `@return {type}`
* `@returns {type}`
  `{type}` representa o tipo de retorno da função. Os tipos de retorno permitidos são:
* string: representa um único valor de string.
* number: representa um único valor numérico.
* booleano: representa um único valor booleano (verdadeiro ou falso).
* cadeia de caracteres []: representa uma matriz de valores de cadeia de caracteres.
* número[]: representa uma matriz de valores numéricos.
* booleano[]: representa uma matriz de valores booleanos.
* date: representa um único valor de data.
* date[]: representa uma matriz de valores de data.
* array: representa uma matriz genérica contendo valores de vários tipos.
* object: representa o objeto de formulário diretamente em vez do seu valor.

O tipo de retorno não diferencia maiúsculas de minúsculas.

#### Privado

A função personalizada, declarada como privada, não aparece na lista de funções personalizadas no editor de regras de um formulário adaptável. Por padrão, as funções personalizadas são públicas. A sintaxe para declarar função personalizada como privada é `@private`.

<!--
#### Member

  Syntax: `@memberof namespace`
  Attaches a namespace to the function.
-->

<!--

#### This

   Syntax: `@this currentComponent`

   Use @this to refer to the Adaptive Form component on which the rule is written. 
  
   The following example is based on the field value. In the following example, the rule hides a field in the form. The `this` portion of `this.value` refers to underlying Adaptive Form component, on which the rule is written.

   ```
      /**
      * @function myTestFunction
      * @this currentComponent
      * @param {scope} scope in which code inside function will be executed.
      */
      myTestFunction = function (scope) {
         if(this.value == "O"){
               scope.age.visible = true;
         } else {
            scope.age.visible = false;
         }
      }

   ```

    >[!NOTE]
    >
    >Comments before custom function are used for summary. Summary can extend to multiple lines until a tag is encountered. Limit the size to a single for a concise description in the rule builder.

-->

<!--

## Function declaration supported types {#function-declaration-supported-types}

**Function Statement**

```javascript
function area(len) {
    return len*len;
}
```

This function is included without `jsdoc` comments.

**Function Expression**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Function Expression and Statement**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Function Declaration as Variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitation: custom function picks only the first function declaration from the variable list, if together. You can use function expression for every function declared.

**Function Declaration as Object**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```
-->

## Diretrizes ao criar funções personalizadas {#considerations}

Para listar as funções personalizadas no editor de regras, você pode usar qualquer um dos seguintes formatos:

### Instrução Function com ou sem comentários jsdoc

Você pode criar uma função personalizada com ou sem comentários jsdoc.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```

Se o usuário não adicionar anotações do JavaScript à função personalizada, ela será listada no editor de regras pelo nome da função. No entanto, é recomendável incluir anotações do JavaScript para melhorar a legibilidade das funções personalizadas.


### Função de seta com anotações ou comentários obrigatórios do JavaScript

É possível criar uma função personalizada com uma sintaxe de função de seta:

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

Se o usuário não adicionar anotações JavaScript à função personalizada, a função personalizada não será listada no editor de regras de um Formulário adaptável.

### Expressão de função com anotações ou comentários obrigatórios do JavaScript

Para listar funções personalizadas no editor de regras de um Formulário adaptável, crie funções personalizadas no seguinte formato:

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

Se o usuário não adicionar anotações JavaScript à função personalizada, a função personalizada não será listada no editor de regras de um Formulário adaptável.

### Pré-requisitos para criar uma função personalizada

Antes de começar a adicionar uma função personalizada ao Adaptive Forms, verifique se você tem o seguinte Software instalado em sua máquina:

* **Editor de Texto sem Formatação (IDE)**: embora qualquer editor de texto sem formatação possa funcionar, um IDE (Ambiente de Desenvolvimento Integrado) como o Microsoft Visual Studio Code oferece recursos avançados para facilitar a edição.

* **Git:** este sistema de controle de versão é necessário para gerenciar alterações de código. Se não estiver instalado, baixe-o de https://git-scm.com.


## Criar uma função personalizada {#create-custom-function}

As etapas para criar funções personalizadas são:
1. [Crie uma biblioteca do lado do cliente usando o Arquétipo de Projeto AEM e adicione uma função personalizada](#create-client-library-archetype)
OU
   [Criar funções personalizadas através do CRXDE](#create-add-custom-function)
1. [Adicionar a biblioteca do cliente a um Formulário adaptável](#add-client-library)
1. [Usar função personalizada em um formulário adaptável](#use-custom-functions)


### Criar uma biblioteca do cliente usando o Arquétipo de projeto AEM{#create-client-library-archetype}

Você pode adicionar funções personalizadas adicionando uma biblioteca do cliente ao projeto criado [usando o Arquétipo de Projeto AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/developing/archetype/using#getting-started).
Se você tiver um projeto existente <!--and have already the project structure as shown in the image below,-->, poderá adicionar diretamente [funções personalizadas](#create-add-custom-function) ao seu projeto local.

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->

Depois de criar um Projeto do Arquétipo ou usar um projeto existente, crie uma biblioteca do cliente. Para criar uma biblioteca do cliente, execute as seguintes etapas:

**Adicionar uma pasta da biblioteca do cliente**

Para adicionar uma nova pasta da biblioteca do cliente ao seu [diretório do projeto AEM], siga estas etapas:

1. Abra o [diretório do projeto AEM] em um editor.

   ![estrutura de pasta de função personalizada](assets/custom-library-folder-structure.png)

1. Localizar `ui.apps`.
1. Adicionar nova pasta. Por exemplo, adicione uma pasta chamada `experience-league`.
1. Navegue até a pasta `/experience-league/` e adicione um `ClientLibraryFolder`. Por exemplo, crie uma pasta da biblioteca do cliente chamada `customclientlibs`.

   O local é: `[AEM project directory]/ui.apps/src/main/content/jcr_root/apps/`

**Adicionar arquivos e pastas à pasta da Biblioteca do Cliente**

Adicione o seguinte à pasta da biblioteca do cliente adicionada:

* `.content.xml` arquivo
* `js.txt` arquivo
* Pasta `js`

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. Em `.content.xml`, adicione as seguintes linhas de código:

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > Você pode escolher qualquer nome para a propriedade `client library folder` e `categories`.

1. Em `js.txt`, adicione as seguintes linhas de código:

   ```javascript
         #base=js
       function.js
   ```

1. Na pasta `js`, adicione o arquivo javascript como `function.js`, o que inclui as funções personalizadas:

   ```javascript
   /**
       * Calculates Age
       * @name calculateAge
       * @param {object} field
       * @return {string} 
   */
   
   function calculateAge(field) {
   var dob = new Date(field);
   var now = new Date();
   
   var age = now.getFullYear() - dob.getFullYear();
   var monthDiff = now.getMonth() - dob.getMonth();
   
   if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
   age--;
   }
   
   return age;
   }
   ```

1. Salve os arquivos.

![estrutura de pasta de função personalizada](assets/custom-function-added-files.png)

**Incluir a nova pasta no filter.xml**:

1. Navegue até o arquivo `/ui.apps/src/main/content/META-INF/vault/filter.xml` no seu [diretório do projeto AEMaaCS].

1. Abra o arquivo e adicione a seguinte linha no final:

   `<filter root="/apps/experience-league" />`
1. Salve o arquivo.

   ![xml de filtro de função personalizada](assets/custom-function-filterxml.png)

1. Crie a pasta da biblioteca do cliente recém-criada em seu ambiente AEM seguindo as etapas fornecidas na [seção Como criar](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype#how-to-build).

## Criar e implantar funções personalizadas por meio do CRXDE{#create-add-custom-function}

Se você estiver usando o complemento mais recente do AEM Forms e do Forms, poderá criar uma função personalizada por meio do CRXDE para usar as atualizações mais recentes de funções personalizadas. Para fazer isso, execute as seguintes etapas:

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->


1. Faça logon em `http://server:port/crx/de/index.jsp#`.
1. Crie uma pasta na pasta `/apps`. Por exemplo, crie uma pasta chamada `experience-league`.
1. Salve as alterações.
1. Navegue até a pasta criada e crie um nó do tipo `cq:ClientLibraryFolder` como `clientlibs`.
1. Navegue até a pasta `clientlibs` recém-criada e adicione as propriedades `allowProxy` e `categories`:

   ![Propriedades do nó de biblioteca personalizado](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > Você pode fornecer qualquer nome no lugar de `customfunctionsdemo`.

1. Salve as alterações.

1. Crie uma pasta chamada `js` na pasta `clientlibs`.
1. Crie um arquivo JavaScript chamado `functions.js` na pasta `js`.
1. Crie um arquivo chamado `js.txt` na pasta `clientlibs`.
1. Salve as alterações.
A estrutura de pastas criada é semelhante a:

   ![Estrutura da pasta de biblioteca do cliente criada](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. Clique duas vezes no arquivo `functions.js` para abrir o editor. O arquivo é composto pelo código da função personalizada.
Vamos adicionar o seguinte código ao arquivo do JavaScript para calcular a idade com base na Data de nascimento (AAAA-MM-DD).

   ```javascript
       /**
            * Calculates Age
            * @name calculateAge 
            * @return {string} 
       */
   
       function calculateAge(dateOfBirthString) {
       var dob = new Date(dateOfBirthString);
       var now = new Date();
   
       var age = now.getFullYear() - dob.getFullYear();
       var monthDiff = now.getMonth() - dob.getMonth();
   
       if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
       age--;
       }
   
       return age;
       }
   ```

1. Salve `function.js`.
1. Navegue até `js.txt` e adicione o seguinte código:

   ```javascript
       #base=js
       functions.js
   ```

1. Salve o arquivo `js.txt`.

Você pode consultar a seguinte pasta [função personalizada](/help/forms/using/assets/customfunction.zip). Baixe e instale essa pasta na instância do AEM.

Agora, você pode usar a função personalizada no Formulário adaptável adicionando a biblioteca do cliente.

## Adicionar biblioteca do cliente em um Formulário adaptável{#add-client-library}

Depois de implantar a biblioteca do cliente no ambiente do AEM Forms, use os recursos dela no Formulário adaptável. Para adicionar a biblioteca do cliente no Formulário adaptável

1. Abra o formulário no modo de edição. Para abrir um formulário no modo de edição, selecione um formulário e selecione **[!UICONTROL Editar]**.
1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Contêiner do guia. A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Abra a guia **[!UICONTROL Básico]** e selecione o nome da **[!UICONTROL categoria da biblioteca do cliente]** na lista suspensa (neste caso, selecione `customfunctionscategory`).

   ![Adicionando a biblioteca cliente de função personalizada](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. Clique em **[!UICONTROL Concluído]**.

Agora, é possível criar uma regra para usar funções personalizadas no editor de regras:

![Adicionando a biblioteca cliente de função personalizada](/help/forms/using//assets/calculateage-customfunction.png)

Agora, vamos entender como configurar e usar uma função personalizada usando o serviço Chamar do [Editor de regras no AEM Forms 6.5](/help/forms/using/rule-editor-core-components.md#invoke-form-data-model-service-invoke)

## Utilização da função personalizada em um formulário adaptável {#use-custom-functions}

Em um Formulário adaptável, você pode usar [Funções personalizadas no editor de regras](/help/forms/using/rule-editor-core-components.md).
Vamos adicionar o seguinte código ao arquivo JavaScript (arquivo `Function.js`) para calcular a idade com base na Data de Nascimento (AAAA-MM-DD). Crie uma função personalizada como `calculateAge()` que use a data de nascimento como entrada e retorne a idade:

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

No exemplo acima, quando o usuário insere a data de nascimento no formato (AAAA-MM-DD), a função personalizada `calculateAge` é invocada e retorna a idade.

![Função personalizada Calcular Idade no Editor de Regras](/help/forms/using/assets/custom-function-calculate-age.png)

Vamos visualizar o formulário para observar como as funções personalizadas são implementadas por meio do editor de regras:

![Função personalizada Calcular Idade na Visualização de Formulário do Editor de Regras](/help/forms/using/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Você pode consultar a seguinte pasta [funções personalizadas](/help/forms/using/assets/customfunctions.zip). Baixe e instale esta pasta na instância do AEM usando o [Gerenciador de Pacotes](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager).

### Suporte para funções assíncronas em funções personalizadas {#support-of-async-functions}

As funções personalizadas assíncronas não aparecem na lista do editor de regras. No entanto, é possível chamar funções assíncronas em funções personalizadas criadas usando expressões de função síncrona.

![Função personalizada síncrona e assíncrona](/help/forms/using/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> A vantagem de chamar funções assíncronas em funções personalizadas é que as funções assíncronas permitem a execução simultânea de várias tarefas, com o resultado de cada função usada nas funções personalizadas.

Examine o código abaixo para ver como podemos chamar funções assíncronas usando funções personalizadas:

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

No exemplo acima, a função asyncFunction é um `asynchronous function`. Ele executa uma operação assíncrona fazendo uma solicitação `GET` para `https://petstore.swagger.io/v2/store/inventory`. Ele aguarda a resposta usando `await`, analisa o corpo da resposta como JSON usando `response.json()` e retorna os dados. A função `callAsyncFunction` é uma função personalizada síncrona que chama a função `asyncFunction` e exibe os dados de resposta no console. Embora a função `callAsyncFunction` seja síncrona, ela chama a função asyncFunction assíncrona e manipula seu resultado com instruções `then` e `catch`.

Para ver seu funcionamento, vamos adicionar um botão e criar uma regra para o botão que chama a função assíncrona em um clique de botão.

![criando regra para função assíncrona](/help/forms/using/assets/rule-for-async-funct.png)

Consulte a ilustração da janela de console abaixo para demonstrar que, quando o usuário clica no botão `Fetch`, a função personalizada `callAsyncFunction` é invocada, o que, por sua vez, chama uma função assíncrona `asyncFunction`. Inspect na janela do console para exibir a resposta ao clicar no botão:

![Janela de console](/help/forms/using/assets/async-custom-funct-console.png)

Vamos analisar os recursos de funções personalizadas.

## Vários recursos para funções personalizadas

Você pode usar funções personalizadas para adicionar recursos personalizados a formulários. Essas funções oferecem suporte a várias habilidades, como trabalhar com campos específicos, usar campos globais ou armazenar em cache. Essa flexibilidade permite personalizar formulários de acordo com os requisitos de sua organização.

### Objetos de escopo de campo e global em funções personalizadas {#support-field-and-global-objects}

Objetos de campo referem-se aos componentes ou elementos individuais em um formulário, como campos de texto e caixas de seleção. O objeto Globals contém variáveis somente leitura, como instância de formulário, instância de campo de destino e métodos para fazer modificações de formulário em funções personalizadas.

>[!NOTE]
>
> O `param {scope} globals` deve ser o último parâmetro e não é exibido no editor de regras de um Formulário adaptável.

<!-- Let us look at the following code snippet:

```JavaScript
   
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

Saiba como as funções personalizadas usam campos e objetos globais com a ajuda de um formulário `Contact Us` usando diferentes casos de uso.

![Formulário Contate-nos](/help/forms/using/assets/contact-us-form.png)

#### **Caso de uso**: mostrar um painel usando a regra `SetProperty`

Adicione o seguinte código na função personalizada, como explicado na seção [create-custom-function](#create-custom-function), para definir o campo de formulário como `Required`.

```javascript
    
    /**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> * Você pode configurar as propriedades de campo usando as propriedades disponíveis localizadas em `[form-path]/jcr:content/guideContainer.model.json`.
> * As modificações feitas no formulário usando o método `setProperty` do objeto Globals são de natureza assíncrona e não são refletidas durante a execução da função personalizada.

Neste exemplo, a validação do painel `personaldetails` ocorre ao clicar no botão. Se nenhum erro for detectado no painel, outro painel, o painel `feedback`, ficará visível ao clicar no botão.

Vamos criar uma regra para o botão `Next`, que valida o painel `personaldetails` e torna o painel `feedback` visível quando o usuário clica no botão `Next`.

![Definir Propriedade](/help/forms/using/assets/custom-function-set-property.png)

Consulte a ilustração abaixo para demonstrar onde o painel `personaldetails` é validado ao clicar no botão `Next`. Caso todos os campos em `personaldetails` sejam validados, o painel `feedback` ficará visível.

![Definir Propriedade de Visualização de Formulário](/help/forms/using/assets/set-property-form-preview.png)

Se houver erros nos campos do painel `personaldetails`, eles serão exibidos no nível do campo ao clicar no botão `Next` e o painel `feedback` permanecerá invisível.

![Definir Propriedade de Visualização de Formulário](/help/forms/using/assets/set-property-panel.png)

#### **Caso de uso**: validar o campo.

Adicione o seguinte código na função personalizada conforme explicado na seção [create-custom-function](#create-custom-function) para validar o campo.

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> Se nenhum argumento for passado na função `validate()`, ele validará o formulário.

Neste exemplo, um padrão de validação personalizado é aplicado ao campo `contact`. Os usuários precisam inserir um número de telefone começando com `10` seguido de `8` dígitos. Se o usuário digitar um número de telefone que não comece com `10` ou contenha mais ou menos de `8` dígitos, uma mensagem de erro de validação será exibida ao clicar no botão:

![Padrão de Validação de Endereço de Email](/help/forms/using/assets/custom-function-validation-pattern.png)

Agora, a próxima etapa é criar uma regra para o botão `Next` que valide o campo `contact` no clique de botão.

![Padrão de validação](/help/forms/using/assets/custom-function-validate.png)

Consulte a ilustração abaixo para demonstrar que, se o usuário digitar um número de telefone que não comece com `10`, uma mensagem de erro será exibida no nível do campo:

![Padrão de Validação de Endereço de Email](/help/forms/using/assets/custom-function-validate-error-message.png)

Se o usuário digitar um número de telefone válido e todos os campos no painel `personaldetails` forem validados, o painel `feedback` aparecerá na tela:

![Padrão de Validação de Endereço de Email](/help/forms/using/assets/validate-form-preview-form.png)

#### **Caso de uso**: redefinir um painel

Adicione o seguinte código na função personalizada, como explicado na seção [create-custom-function](#create-custom-function), para redefinir o painel.

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> Se nenhum argumento for passado na função `reset()`, ele validará o formulário.

Neste exemplo, o painel `personaldetails` é redefinido ao clicar no botão `Clear`. A próxima etapa é criar uma regra para o botão `Clear` que redefina o painel no clique do botão.

![Botão Limpar](/help/forms/using/assets/custom-function-reset-field.png)

Consulte a ilustração abaixo para mostrar que, se o usuário clicar no botão `clear`, o painel `personaldetails` será redefinido:

![Redefinir Formulário](assets/custom-function-reset-form.png)

#### **Caso de uso**: para exibir uma mensagem personalizada no nível do campo e marcar o campo como inválido

Você pode usar a função `markFieldAsInvalid()` para definir um campo como inválido e definir uma mensagem de erro personalizada em nível de campo. O valor `fieldIdentifier` pode ser `fieldId`, `field qualifiedName` ou `field dataRef`. O valor do objeto nomeado `option` pode ser `{useId: true}`, `{useQualifiedName: true}` ou `{useDataRef: true}`.
As sintaxes usadas para marcar o campo como inválido e definir uma mensagem personalizada são:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Adicione o seguinte código na função personalizada conforme explicado na seção [create-custom-function](#create-custom-function) para habilitar a mensagem personalizada no nível do campo.

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

Neste exemplo, se o usuário inserir menos de 15 caracteres na caixa de texto comentários, uma mensagem personalizada será exibida no nível do campo.

A próxima etapa é criar uma regra para o campo `comments`:

![Marcar campo como Inválido](/help/forms/using/assets/custom-function-invalid-field.png)

Veja a demonstração abaixo para mostrar que inserir comentários negativos no campo `comments` aciona a exibição de uma mensagem personalizada no nível do campo:

![Marcar campo como Formulário de visualização inválido](/help/forms/using/assets/custom-function-invalidfield-form.png)

Se o usuário inserir mais de 15 caracteres na caixa de texto de comentários, o campo será validado e o formulário será enviado:

![Marcar campo como formulário de Visualização válido](/help/forms/using/assets/custom-function-validfield-form.png)


#### **Caso de uso**: enviar dados alterados para o servidor

A seguinte linha de código:
`globals.functions.submitForm(globals.functions.exportData(), false);` é usado para enviar os dados do formulário após manipulação.
* O primeiro argumento diz respeito aos dados a apresentar.
* O segundo argumento representa se o formulário deve ser validado antes do envio. Ele é `optional` e definido como `true` por padrão.
* O terceiro argumento é o `contentType` do envio, que também é opcional com o valor padrão como `multipart/form-data`. Os outros valores podem ser `application/json` e `application/x-www-form-urlencoded`.

Adicione o seguinte código na função personalizada, conforme explicado na seção [create-custom-function](#create-custom-function), para enviar os dados manipulados no servidor:

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */
    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

Neste exemplo, se o usuário deixar a caixa de texto `comments` vazia, o `NA` será enviado ao servidor no envio do formulário.

Agora crie uma regra para o botão `Submit` que envia dados:

![Enviar dados](/help/forms/using/assets/custom-function-submit-data.png)

Consulte a ilustração da `console window` abaixo para demonstrar que, se o usuário deixar a caixa de texto `comments` vazia, o valor como `NA` será enviado ao servidor:

![Enviar dados na janela do console](/help/forms/using/assets/custom-function-submit-data-form.png)

Você também pode inspecionar a janela do console para visualizar os dados enviados para o servidor:

![Dados do Inspect na janela do console](/help/forms/using/assets/custom-function-submit-data-console-data.png)

<!--

#### **Use Case**: Display form submission and failure messages for custom submit action 

Add the following line of code as explained in the [create-custom-function ](#create-custom-function) section, to customize the submission or failure message for form submissions and display the form submission messages in a modal box:

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

In this example, when the user uses the `customSubmitSuccessHandler` and `customSubmitErrorHandler` custom functions, the success and failure messages are displayed in a modal. The JavaScript function `showModal(type, message)` is used to dynamically create and display a modal dialog box on a screen.

Now, create a rule for successful form submission:

![Form submission success](/help/forms/using/assets/form-submission-success.png)

Refer to the illustration below to demonstrate that when the form is submitted successfully, the success message is displayed in a modal:

![Form submission success message](/help/forms/using/assets/form-submission-success-message.png )
 
Similarly, let us create a rule for failed form submissions:

![Form submission fail](/help/forms/using/assets/form-submission-fail.png)

Refer to the illustration below to demonstrate that when the form submission fails, the error message is displayed in a modal:

![Form submission fail message](/help/forms/using/assets/form-submission-fail-message.png )

To display form submission success and failure in a default manner, the `Default submit Form Success Handler` and `Default submit Form Error Handler` functions are available out of the box.

In case, the custom submit action fails to perform as expected in existing AEM projects or forms, refer to the [troubleshooting](#troubleshooting) section.

-->

## Suporte de cache para função personalizada

O Forms adaptável implementa o armazenamento em cache de funções personalizadas para melhorar o tempo de resposta ao recuperar a lista de funções personalizadas no editor de regras. Uma mensagem como `Fetched following custom functions list from cache` aparece no arquivo `error.log`.

![função personalizada com suporte a cache](/help/forms/using/assets/custom-function-cache-error.png)

Caso as funções personalizadas sejam modificadas, o armazenamento em cache é invalidado e é analisado.

## Resolução de problemas {#troubleshooting}

* O usuário precisa garantir que o [componente principal e a versão da especificação estejam definidos com a versão mais recente](https://github.com/adobe/aem-core-forms-components/tree/release/650). No entanto, para projetos e formulários de AEM existentes, há etapas adicionais a seguir:

   * Para o projeto AEM, o usuário deve substituir todas as instâncias de `submitForm('custom:submitSuccess', 'custom:submitError')` por `submitForm()` e implantar o projeto.

   * Para formulários existentes, se os manipuladores de envio personalizados não estiverem funcionando corretamente, o usuário precisará abrir e salvar a regra `submitForm` no botão **Enviar** usando o Editor de Regras. Esta ação substitui a regra existente de `submitForm('custom:submitSuccess', 'custom:submitError')` por `submitForm()` no formulário.


* Se o arquivo JavaScript que contém o código para funções personalizadas tiver um erro, as funções personalizadas não serão listadas no editor de regras de um Formulário adaptável. Para verificar a lista de funções personalizadas, você pode navegar até o arquivo `error.log` para localizar o erro. No caso de um erro, a lista de funções personalizadas aparece vazia:

  ![arquivo de log de erros](/help/forms/using/assets/custom-function-list-error-file.png)

  Caso não haja erro, as funções personalizadas são buscadas e aparecem no arquivo `error.log`. Uma mensagem como `Fetched following custom functions list` aparece no arquivo `error.log`:

  ![arquivo de log de erros com a função personalizada adequada](/help/forms/using/assets/custom-function-list-fetched-in-error.png)

## Considerações

* O `parameter type` e o `return type` não dão suporte a `None`.

* As funções não suportadas na lista de funções personalizadas são:
   * Funções geradoras
   * Funções assíncronas/Await
   * Definições de método
   * Métodos de classe
   * Parâmetros padrão
   * Parâmetros rest
