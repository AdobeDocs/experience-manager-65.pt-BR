---
title: Criar e adicionar funções personalizadas em um Formulário adaptável
description: O AEM Forms é compatível com funções personalizadas que permitem aos usuários criar e usar suas próprias funções no editor de regras.
feature: Adaptive Forms, Foundation Components
role: Admin, User, Developer
exl-id: 14a52bc1-c1b4-4a12-b8e1-54523e5f30bd
source-git-commit: a0ef9925d1bcb84ea5bf733221875d0322cc6df1
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 0%

---

# Funções personalizadas no Adaptive Forms

## Introdução

>[!NOTE]
>
> As funções personalizadas devem ser compatíveis com o ECMAScript 5 (ES5). O Foundation Forms é compatível apenas com ES5; o uso de versões mais recentes do ECMAScript (ES6 e superior) não é compatível e pode resultar em erros ou comportamento inesperado.

O AEM Forms 6.5 apresentou a capacidade de definir funções do JavaScript que podem ser usadas na definição de regras de negócios complexas usando o editor de regras. O AEM Forms fornece várias dessas funções personalizadas prontas para uso, mas você terá a necessidade de definir suas próprias funções personalizadas e usá-las em vários formulários.

As funções personalizadas estendem os recursos dos formulários facilitando a manipulação e o processamento dos dados inseridos para atender a requisitos especificados. Elas também permitem a alteração dinâmica do comportamento do formulário com base em critérios predefinidos.
No Adaptive Forms, você pode usar funções personalizadas no [editor de regras de um Formulário adaptável](/help/forms/using/rule-editor.md) para criar regras de validação específicas para campos de formulário.
Vamos entender o uso da função personalizada em que os usuários inserem o endereço de email e você deseja garantir que o endereço de email inserido siga um formato específico (ele contém um símbolo &quot;@&quot; e um nome de domínio). Crie uma função personalizada como &quot;ValidateEmail&quot; que assume o endereço de email como entrada e retorna true se for válido, caso contrário, retorna false.

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

No exemplo acima, quando o usuário tenta enviar o formulário, a função personalizada &quot;ValidateEmail&quot; é invocada para verificar se o endereço de email inserido é válido.

## Usos de funções personalizadas {#uses-of-custom-function}

As vantagens de usar funções personalizadas no Adaptive Forms são:

* **Manipulação de dados**: funções personalizadas manipulam e processam dados inseridos nos campos de formulários.
* **Validação de dados**: as funções personalizadas permitem que você execute verificações personalizadas nas entradas do formulário e forneça mensagens de erro especificadas.
* **Comportamento dinâmico**: as funções personalizadas permitem que você controle o comportamento dinâmico de seus formulários com base em condições específicas. Por exemplo, você pode mostrar/ocultar campos, modificar valores de campo ou ajustar a lógica do formulário dinamicamente.
* **Integração**: você pode usar funções personalizadas para integrar-se a APIs ou serviços externos. Ele ajuda a buscar dados de fontes externas, enviar dados para endpoints Rest externos ou executar ações personalizadas com base em eventos externos.

## Anotações JS suportadas

Certifique-se de que a função personalizada que você grava esteja acompanhada pelo `jsdoc` acima dela; caso contrário, você precisará de configuração e descrição personalizadas. Há várias maneiras de declarar uma função em `JavaScript,` e os comentários permitem que você acompanhe as funções. Para obter mais informações, consulte [usejsdoc.org](https://jsdoc.app/).

`jsdoc` marcas com suporte:

* **Particular**
Sintaxe: `@private`
Uma função privada não está incluída como uma função personalizada.

* **Nome**
Sintaxe: `@name funcName <Function Name>`
Alternativamente, o `,` é possível usar o `@function funcName <Function Name>` **ou o** `@func` `funcName <Function Name>`.
  `funcName` é o nome da função (nenhum espaço é permitido).
  `<Function Name>` é o nome para exibição da função.

* **Membro**
Sintaxe: `@memberof namespace`
Anexa um namespace à função.

* **Parâmetro**
Sintaxe: `@param {type} name <Parameter Description>`
Como alternativa, você pode usar: `@argument` `{type} name <Parameter Description>` **ou** `@arg` `{type}` `name <Parameter Description>`.
Mostra os parâmetros usados pela função. Uma função pode ter várias tags de parâmetro, uma tag para cada parâmetro na ordem de ocorrência.
  `{type}` representa o tipo de parâmetro. Os tipos de parâmetros permitidos são:

   1. string
   2. número
   3. booleano
   4. escopo

  O escopo é usado para campos de referência de um Formulário adaptável. Quando um formulário usa carregamento lento, você pode usar `scope` para acessar seus campos. Você pode acessar campos quando eles forem carregados ou se estiverem marcados como globais.

  Todos os outros tipos de parâmetros são categorizados em um dos acima. Nenhum não é compatível. Selecione um dos tipos acima. Os tipos não diferenciam maiúsculas de minúsculas. Não são permitidos espaços no parâmetro `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **Tipo de Retorno**
Sintaxe: `@return {type}`
Como alternativa, você pode usar `@returns {type}`.
Adiciona informações sobre a função, como seu objetivo.
  {type} representa o tipo de retorno da função. Os tipos de retorno permitidos são:

   1. string
   1. número
   1. booleano

  Todos os outros tipos de retorno são categorizados em um dos itens acima. Nenhum não é compatível. Selecione um dos tipos acima. Os tipos de retorno não diferenciam maiúsculas de minúsculas.

* **Isto**
Sintaxe: `@this currentComponent`

  Use @this para se referir ao componente de Formulário adaptável no qual a regra é gravada.

  O exemplo a seguir é baseado no valor do campo. No exemplo a seguir, a regra oculta um campo no formulário. A parte `this` de `this.value` refere-se ao componente de Formulário adaptável subjacente, no qual a regra é gravada.

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
  >Comentários antes da função personalizada são usados para resumo. O resumo pode ser estendido para várias linhas até que uma tag seja encontrada. Limite o tamanho a um único para obter uma descrição concisa no construtor de regras.

## Tipos suportados de declaração de função {#function-declaration-supported-types}

**Instrução da Função**

```javascript
function area(len) {
    return len*len;
}
```

Esta função está incluída sem `jsdoc` comentários.

**Expressão de função**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Expressão e Instrução da Função**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Declaração de função como variável**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitação: a função personalizada escolhe somente a primeira declaração de função da lista de variáveis, se estiver junto. Você pode usar a expressão de função para cada função declarada.

**Declaração de Função como Objeto**

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

## Criar função personalizada {#create-custom-function}

Para criar uma função personalizada, execute as seguintes etapas:

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
1. Crie um arquivo JavaScript chamado `functions.js` na pasta `js`
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

## Adicionar biblioteca do cliente em um Formulário adaptável{#use-custom-function}

Depois de implantar a biblioteca do cliente no ambiente do Forms CS, use os recursos dela no Formulário adaptável. Para adicionar a biblioteca do cliente no Formulário adaptável

1. Abra o formulário no modo de edição. Para abrir um formulário no modo de edição, selecione um formulário e selecione **[!UICONTROL Editar]**.
1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Contêiner do guia. A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Abra a guia **[!UICONTROL Básico]** e selecione o nome da **[!UICONTROL categoria da biblioteca do cliente]** na lista suspensa (neste caso, selecione `customfunctionscategory`).

   ![Adicionando a biblioteca cliente de função personalizada](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. Clique em **[!UICONTROL Concluído]**.

Agora, é possível criar uma regra para usar funções personalizadas no editor de regras:

![Adicionando a biblioteca cliente de função personalizada](/help/forms/using//assets/calculateage-customfunction.png)

Agora, vamos entender como configurar e usar uma função personalizada usando o [serviço Chamar do Editor de regras no AEM Forms](/help//forms/using/rule-editor.md).
