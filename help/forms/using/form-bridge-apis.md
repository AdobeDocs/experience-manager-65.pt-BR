---
title: APIs de Bridge de formulários para formulários HTML5
description: Aplicativos externos usam a API FormBridge para se conectar ao Formulário móvel XFA. A API despacha um evento FormBridgeInitialized na janela principal.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---

# APIs de Bridge de formulários para formulários HTML5 {#form-bridge-apis-for-html-forms}

Você pode usar as APIs do Form Bridge para abrir um canal de comunicação entre um formulário HTML5 baseado em XFA e seus aplicativos. As APIs do Form Bridge fornecem uma API **connect** para criar a conexão.

A API **connect** aceita um manipulador como argumento. Depois que uma conexão bem-sucedida é criada entre o formulário HTML5 baseado em XFA e o Form Bridge, o identificador é chamado.

Você pode usar o código de amostra a seguir para criar a conexão.

```javascript
// Example showing how to connect to FormBridge
window.addEventListener("FormBridgeInitialized",
                                function(event) {
                                    var fb = event.detail.formBridge;
                                    fb.connect(function() {
                                           //use form bridge functions
                         })
                            })
```

>[!NOTE]
>
>Certifique-se de criar uma conexão antes de incluir o arquivo formRuntime.jsp.

## API do Bridge do formulário disponível  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

Retorna o número da versão da biblioteca de Scripts

* **Entrada**: Nenhuma
* **Saída**: Número da versão da biblioteca de Scripts
* **Erros**: Nenhum

**isConnected()** Verifica se o Estado do Formulário foi inicializado

* **Entrada**: Nenhuma
* **Saída**: **Verdadeiro** se o Estado de Formulário XFA tiver sido inicializado

* **Erros**: Nenhum

**connect(handler, context)** Faz uma conexão com FormBridge e executa a função depois que a conexão é feita e o Estado do Formulário é inicializado

* **Entrada**:

   * **manipulador**: função a ser executada após a conexão do Form Bridge
   * **contexto**: o objeto ao qual o contexto (este) da função *manipulador* está definido.

* **Saída**: nenhuma
* **Erro**: Nenhum

**getDataXML(options)** Retorna os dados atuais do formulário no Formato XML

* **Entrada:**

   * **opções:** objeto JavaScript contendo as seguintes propriedades:

      * **Erro**: Função de Manipulador de Erros
      * **sucesso**: função de manipulador de sucesso. Esta função recebeu um objeto contendo XML na propriedade *data*.
      * **contexto**: o objeto ao qual o contexto (este) da função *success* está definido
      * **validationChecker**: função para chamar para verificar erros de validação recebidos do servidor. A função de validação recebe uma matriz de cadeias de caracteres de erro.
      * **formState**: o estado JSON do Formulário XFA para o qual o XML de dados deve ser retornado. Se não for especificado, retorna o XML de dados para o formulário renderizado atualmente.

* **Saída:** Nenhuma
* **Erro:** Nenhum

**registerConfig(configName, config)** registra configurações específicas de usuário/portal com o FormBridge. Essas configurações substituem as configurações padrão. As configurações compatíveis são especificadas na seção de configuração.

* **Entrada:**

   * **configName:** Nome da configuração a ser substituída

      * **widgetConfig:** permite que o usuário substitua os widgets padrão do formulário por widgets personalizados. A configuração é substituída da seguinte maneira:

        *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** permite que o usuário substitua o comportamento padrão de renderizar somente a primeira página. A configuração é substituída da seguinte maneira:

        *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true | false>, shrinkPageDisabled: &lt;true | false> }).*

      * **LoggingConfig:** permite que o usuário substitua o nível de log, desabilite o log de uma categoria ou exiba o console de logs ou envie para o servidor. A configuração pode ser substituída da seguinte maneira:

     ```javascript
     formBridge.registerConfig{
       "LoggerConfig" : {
     {
     "on":`<true *| *false>`,
     "category":`<array of categories>`,
     "level":`<level of categories>`, "
     type":`<"console"/"server"/"both">`
     }
       }
     ```

      * **SubmitServiceProxyConfig:** Permita que os usuários registrem serviços de proxy de envio e agente de log.

        ```javascript
        window.formBridge.registerConfig("submitServiceProxyConfig",
        {
        "submitServiceProxy" : "`<submitServiceProxy>`",
        "logServiceProxy": "`<logServiceProxy>`",
        "submitUrl" : "`<submitUrl>`"
        });
        ```

   * **config:** Valor da configuração

* **Saída:** Objeto que contém o valor original da configuração na propriedade *data*.

* **Erro:** Nenhum

**hideFields(fieldArray)** Oculta os campos cujas expressões Som são fornecidas em fieldArray. Define a propriedade de presença dos campos especificados como invisíveis

* **Entrada:**

   * **fieldArray:** Matriz de expressões Som para os campos a serem ocultados

* **Saída:** Nenhuma
* **Erro:** Nenhum

**showFields(fieldArray)** Mostra os campos cujas expressões Som são fornecidas em fieldArray. Define a propriedade de presença dos campos fornecidos como visíveis

* **Entrada:**

   * **fieldArray:** Matriz de expressões Som para os campos a serem exibidos

* **Saída:** Nenhuma
* **Erro:** Nenhum

**hideSubmitButtons()** Oculta todos os botões de envio no formulário

* **Entrada**: Nenhuma
* **Saída**: nenhuma
* **Erro**: gera uma exceção se o Estado do Formulário não for inicializado

**getFormState()** Retorna o JSON que representa o Estado de Formulário

* **Entrada:** Nenhuma
* **Saída:** objeto contendo JSON representando o Estado de Formulário atual na propriedade *data*.

* **Erro:** Nenhum

**restoreFormState(options)** Restaura o Estado do Formulário a partir do estado JSON fornecido no objeto de opções. O estado é aplicado e manipuladores de sucesso ou erro são chamados após a conclusão da operação

* **Entrada:**

   * **Opções:** objeto JavaScript contendo as seguintes propriedades:

      * **Erro**: Função de Manipulador de Erros
      * **sucesso**: função de manipulador de sucesso
      * **contexto**: o objeto ao qual o contexto (este) da função *success* está definido
      * **formState**: estado JSON do formulário. O formulário é restaurado para o estado JSON.

* **Saída:** Nenhuma
* **Erro:** Nenhum

**setFocus (som)** Define o foco no campo especificado na expressão Som

* **Entrada:** Alguma expressão do campo no qual definir o foco
* **Saída:** Nenhuma
* **Erro:** lança uma exceção se houver uma expressão Som incorreta

**setFieldValue (som, valor)** Define o valor dos campos para as expressões Som fornecidas

* **Entrada:**

   * **som:** Matriz contendo expressões Som do campo. A expressão som para definir o valor dos campos.
   * **value:** Matriz contendo valores correspondentes a Algumas expressões fornecidas em uma matriz **som**. Se o tipo de dados do valor não for o mesmo que fieldType, o valor não será modificado.

* **Saída:** Nenhuma
* **Erro:** lança uma exceção se houver uma expressão Som incorreta

**getFieldValue (som)** Retorna o valor dos campos das expressões Som fornecidas

* **Entrada:** Matriz contendo Algumas expressões dos campos cujo valor deve ser recuperado
* **Saída:** objeto que contém o resultado como Matriz na propriedade **data**.

* **Erro:** Nenhum

### Exemplo de API getFieldValue() {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue("xfa.form.form1.Subform1.TextField");
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, propriedade)** Recupere a lista de valores da propriedade especificada dos campos especificados em expressões Som

* **Entrada:**

   * **som:** Matriz contendo expressões Som para os campos
   * **propriedade**: nome da propriedade cujo valor é obrigatório

* **Saída:** Objeto que contém o resultado como Matriz na propriedade *data*

* **Erro:** Nenhum

**setFieldProperties(som, propriedade, valores)** Define o valor da propriedade especificada para todos os campos especificados nas expressões Som

* **Entrada:**

   * **som:** Matriz contendo Algumas expressões dos campos cujo valor deve ser definido
   * **propriedade**: propriedade cujo valor deve ser definido
   * **value:** Matriz contendo valores da propriedade especificada para campos especificados em expressões Som

* **Saída:** Nenhuma
* **Erro:** Nenhum

## Exemplo de uso da API do Form Bridge {#sample-usage-of-form-bridge-api}

```JavaScript
// Example 1: FormBridge.restoreFormState
  function loadFormState() {
    var suc = function(obj) {
             //success
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
        var _formState = // load form state from storage
    formBridge.restoreFormState({success:suc,error:err,formState:_formState}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }

//--------------------------------------------------------------------------------------------------

//Example 2: FormBridge.submitForm
  function SubmitForm() {
    var suc = function(obj) {
             var data = obj.data;
         // submit the data to a url;
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
    formBridge.submitForm({success:suc,error:err}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }
```
