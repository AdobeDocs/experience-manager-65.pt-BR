---
title: APIs do Form Bridge para formulários HTML5
description: Aplicativos externos usam a API FormBridge para se conectar ao Formulário móvel XFA. A API despacha um evento FormBridgeInitialized na janela principal.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---

# APIs do Form Bridge para formulários HTML5 {#form-bridge-apis-for-html-forms}

Você pode usar as APIs do Form Bridge para abrir um canal de comunicação entre um formulário HTML5 baseado em XFA e seus aplicativos. As APIs do Form Bridge fornecem uma **conectar** API para criar a conexão.

A variável **conectar** A API aceita um manipulador como argumento. Depois que uma conexão bem-sucedida é criada entre o formulário HTML5 baseado em XFA e o Form Bridge, o identificador é chamado.

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

## API de ponte de formulário disponível  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

Retorna o número da versão da biblioteca de Scripts

* **Entrada**: Nenhuma
* **Output**: número de versão da Biblioteca de scripts
* **Erros**: Nenhuma

**isConnected()** Verifica se o Estado do Formulário foi inicializado

* **Entrada**: Nenhuma
* **Output**: **True** se o estado do formulário XFA tiver sido inicializado

* **Erros**: Nenhuma

**connect(handler, contexto)** Faz uma conexão com FormBridge e executa a função depois que a conexão é feita e o Estado do formulário é inicializado

* **Entrada**:

   * **manipulador**: função a ser executada após a conexão do Form Bridge
   * **contexto**: o objeto ao qual o contexto (este) do *manipulador* são definidas.

* **Output**: Nenhuma
* **Erro**: Nenhuma

**getDataXML(options)** Retorna os dados do formulário atual no formato XML

* **Entrada:**

   * **opções:** Objeto JavaScript contendo as seguintes propriedades:

      * **Erro**: Função do manipulador de erros
      * **success**: função do manipulador de sucesso. Esta função recebe um objeto contendo XML em *dados* propriedade.
      * **contexto**: o objeto ao qual o contexto (este) do *success* função está definida
      * **validationChecker**: Função para chamar a verificação de erros de validação recebidos do servidor. A função de validação recebe uma matriz de cadeias de caracteres de erro.
      * **formState**: o estado JSON do formulário XFA para o qual o XML de dados deve ser retornado. Se não for especificado, retorna o XML de dados para o formulário renderizado atualmente.

* **Saída:** Nenhum
* **Erro:** Nenhum

**registerConfig(configName, config)** Registra configurações específicas do usuário/portal no FormBridge. Essas configurações substituem as configurações padrão. As configurações compatíveis são especificadas na seção de configuração.

* **Entrada:**

   * **configName:** Nome da configuração a ser substituída

      * **widgetConfig:** Permite que o usuário substitua os widgets padrão do formulário por widgets personalizados. A configuração é substituída da seguinte maneira:

        *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** Permite que o usuário substitua o comportamento padrão de renderização somente da primeira página. A configuração é substituída da seguinte maneira:

        *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true false=&quot;&quot;>, shrinkPageDisabled: &lt;true false=&quot;&quot;> }).*

      * **LoggingConfig:** Permite que o usuário substitua o nível de registro, desative o registro em uma categoria ou exiba o console de registros ou envie para o servidor. A configuração pode ser substituída da seguinte maneira:

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

      * **SubmitServiceProxyConfig:** Permitir que os usuários registrem serviços de proxy de envio e log.

        ```javascript
        window.formBridge.registerConfig("submitServiceProxyConfig",
        {
        "submitServiceProxy" : "`<submitServiceProxy>`",
        "logServiceProxy": "`<logServiceProxy>`",
        "submitUrl" : "`<submitUrl>`"
        });
        ```

   * **config:** Valor da configuração

* **Saída:** Objeto que contém o valor original da configuração em *dados* propriedade.

* **Erro:** Nenhum

**hideFields(fieldArray)** Oculta os campos cujas expressões Som são fornecidas em fieldArray. Define a propriedade de presença dos campos especificados como invisíveis

* **Entrada:**

   * **fieldArray:** Matriz de expressões Som para os campos a serem ocultados

* **Saída:** Nenhum
* **Erro:** Nenhum

**showFields(fieldArray)** Mostra os campos cujas expressões Som são fornecidas em fieldArray. Define a propriedade de presença dos campos fornecidos como visíveis

* **Entrada:**

   * **fieldArray:** Matriz de expressões Som para os campos a serem exibidos

* **Saída:** Nenhum
* **Erro:** Nenhum

**hideSubmitButtons()** Oculta todos os botões de envio no formulário

* **Entrada**: Nenhuma
* **Output**: Nenhuma
* **Erro**: gera uma exceção se o estado do formulário não for inicializado

**getFormState()** Retorna o JSON que representa o Estado do Formulário

* **Entrada:** Nenhum
* **Saída:** Objeto que contém JSON que representa o Estado de formulário atual em *dados* propriedade.

* **Erro:** Nenhum

**restoreFormState(options)** Restaura o Estado do formulário do estado JSON fornecido no objeto de opções. O estado é aplicado e manipuladores de sucesso ou erro são chamados após a conclusão da operação

* **Entrada:**

   * **Opções:** Objeto JavaScript contendo as seguintes propriedades:

      * **Erro**: Função do manipulador de erros
      * **success**: função do manipulador de sucesso
      * **contexto**: o objeto ao qual o contexto (este) do *success* são definidas
      * **formState**: estado JSON do formulário. O formulário é restaurado para o estado JSON.

* **Saída:** Nenhum
* **Erro:** Nenhum

**setFocus (som)** Define o foco para o campo especificado na expressão Som

* **Entrada:** Alguma expressão do campo para definir o foco
* **Saída:** Nenhum
* **Erro:** Gera uma exceção se houver uma expressão Som incorreta

**setFieldValue (som, valor)** Define o valor dos campos para as expressões Som fornecidas

* **Entrada:**

   * **som:** Matriz que contém Algumas expressões do campo. A expressão som para definir o valor dos campos.
   * **valor:** Matriz que contém valores correspondentes a Algumas expressões fornecidas em uma **som** matriz. Se o tipo de dados do valor não for o mesmo que fieldType, o valor não será modificado.

* **Saída:** Nenhum
* **Erro:** Gera uma Exceção se houver uma expressão Som incorreta

**getFieldValue (som)** Retorna o valor dos campos para as expressões Som fornecidas

* **Entrada:** Matriz que contém Algumas expressões dos campos cujo valor deve ser recuperado
* **Saída:** Objeto que contém o resultado como Matriz em **dados** propriedade.

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

**getFieldProperties(som, propriedade)** Recupera a lista de valores para determinada propriedade dos campos especificados em Algumas expressões

* **Entrada:**

   * **som:** Matriz contendo algumas expressões para os campos
   * **propriedade**: Nome da propriedade cujo valor é obrigatório

* **Saída:** Objeto que contém o resultado como Matriz em *dados* propriedade

* **Erro:** Nenhum

**setFieldProperties(som, propriedade, valores)** Define o valor da propriedade especificada para todos os campos especificados nas expressões Som

* **Entrada:**

   * **som:** Matriz que contém Algumas expressões dos campos cujo valor deve ser definido
   * **propriedade**: propriedade cujo valor deve ser definido
   * **valor:** Matriz que contém valores da propriedade especificada para campos especificados em Algumas expressões

* **Saída:** Nenhum
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
