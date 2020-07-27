---
title: APIs Form Bridge para formulários HTML5
seo-title: APIs Form Bridge para formulários HTML5
description: Aplicativos externos usam a API FormBridge para se conectar ao formulário móvel XFA. A API despacha um evento FormBridgeInitialized na janela pai.
seo-description: Aplicativos externos usam a API FormBridge para se conectar ao formulário móvel XFA. A API despacha um evento FormBridgeInitialized na janela pai.
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# APIs Form Bridge para formulários HTML5 {#form-bridge-apis-for-html-forms}

Você pode usar as APIs Form Bridge para abrir um canal de comunicação entre formulários HTML5 baseados em XFA e seus aplicativos. As APIs Form Bridge fornecem uma API de **conexão** para criar a conexão.

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

## API do Form Bridge disponível  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

Retorna o número da versão da biblioteca de scripts

* **Entrada**: Nenhum
* **Saída**: Número da versão da biblioteca de scripts
* **Erros**: Nenhum

**isConnected()** Verifica se o Estado do Formulário foi inicializado

* **Entrada**: Nenhum
* **Saída**: **Verdadeiro** se o Estado de Formulário XFA foi inicializado

* **Erros**: Nenhum

**connect(handler, context)** Faz uma conexão com o FormBridge e executa a função depois que a conexão é feita e o Form State é inicializado

* **Entrada**:

   * **manipulador**: Função a ser executada após a conexão do Form Bridge
   * **contexto**: O objeto ao qual o contexto (this) da função do *manipulador* está definido.

* **Saída**: Nenhum
* **Erro**: Nenhum

**getDataXML(options)** Retorna os dados de formulário atuais no Formato XML

* **Entrada:**

   * **opções:** Objeto JavaScript que contém as seguintes propriedades:

      * **Erro**: Função de manipulador de erros
      * **sucesso**: Função de manipulador de sucesso. Essa função é transmitida a um objeto que contém XML na propriedade *data* .
      * **contexto**: O objeto ao qual o contexto (esta) da função de *sucesso* está definido
      * **validationChecker**: Função para chamar para verificar os erros de validação recebidos do servidor. A função de validação é transmitida por uma matriz de sequências de caracteres de erro.
      * **formState**: O estado JSON do Formulário XFA para o qual o XML de dados deve ser retornado. Se não for especificado, retornará o XML de dados para o formulário renderizado no momento.

* **Saída:** Nenhum
* **Erro:** Nenhum

**registerConfig(configName, config)** Registra configurações específicas do usuário/portal com o FormBridge. Essas configurações substituem as configurações padrão. As configurações compatíveis são especificadas na seção de configuração.

* **Entrada:**

   * **configName:** Nome da configuração a ser substituída

      * **widgetConfig:** Permite que o usuário substitua os widgets padrão no formulário por widgets personalizados. A configuração é substituída da seguinte maneira:

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** Permite que o usuário substitua o comportamento padrão de renderização somente da primeira página. A configuração é substituída da seguinte maneira:

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true | false>, saninkPageDisabled: &lt;true | false> }).*

      * **LoggingConfig:** Permite que o usuário substitua o nível de registro, desative o registro para uma categoria ou exiba o console de registros ou envie para o servidor. A configuração pode ser substituída da seguinte maneira:

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

      * **SubmitServiceProxyConfig:** Permitir que os usuários registrem os serviços de envio e proxy de agente de log.

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **configuração:** Valor da configuração



* **Saída:** Objeto que contém o valor original da configuração na propriedade *data* .

* **Erro:** Nenhum

**hideFields(fieldArray)** Oculta os campos cujas expressões Som são fornecidas no fieldArray. Define a propriedade presence dos campos especificados como invisível

* **Entrada:**

   * **fieldArray:** Matriz de expressões Som para os campos ocultarem

* **Saída:** Nenhum
* **Erro:** Nenhum

**showFields(fieldArray)** Mostra os campos cujas expressões Som são fornecidas no fieldArray. Define a propriedade presence dos campos fornecidos como visível

* **Entrada:**

   * **fieldArray:** Matriz de expressões Som para os campos serem exibidos

* **Saída:** Nenhum
* **Erro:** Nenhum

**hideSubmitButtons()** Oculta todos os botões Enviar no formulário

* **Entrada**: Nenhum
* **Saída**: Nenhum
* **Erro**: Lançará a exceção se o Estado do formulário não for inicializado

**getFormState()** Retorna o JSON que representa o Estado do Formulário

* **Entrada:** Nenhum
* **Saída:** Objeto que contém JSON que representa o Estado de formulário atual na propriedade *data* .

* **Erro:** Nenhum

**restoreFormState(opções)** Restaura o Estado do formulário a partir do estado JSON fornecido no objeto options. O estado é aplicado e os manipuladores bem-sucedidos ou de erros são chamados depois que a operação é concluída

* **Entrada:**

   * **Opções:** Objeto JavaScript que contém as seguintes propriedades:

      * **Erro**: Função de manipulador de erros
      * **sucesso**: Função de manipulador de sucesso
      * **contexto**: O objeto ao qual o contexto (esta) da função de *sucesso* está definido
      * **formState**: Estado JSON do formulário. O formulário é restaurado para o estado JSON.

* **Saída:** Nenhum
* **Erro:** Nenhum

**setFocus (som)** Define o foco no campo especificado na expressão Som

* **Entrada:** Algumas expressões do campo em que o foco deve ser definido
* **Saída:** Nenhum
* **Erro:** Emite uma exceção em caso de expressão Som incorreta

**setFieldValue (som, valor)** Define o valor dos campos para as expressões Som fornecidas

* **Entrada:**

   * **som:** Matriz contendo algumas expressões do campo. A expressão para definir o valor dos campos.
   * **valor:** Matriz que contém valores correspondentes a expressões Som fornecidas em uma **** matriz sombria. Se o tipo de dados do valor não for igual ao fieldType, o valor não será modificado.

* **Saída:** Nenhum
* **Erro:** Emite uma Exceção no caso de uma expressão Som incorreta

**getFieldValue (som)** Retorna o valor dos campos para as expressões Som fornecidas

* **Entrada:** Matriz contendo expressões Som dos campos cujo valor precisa ser recuperado
* **Saída:** Objeto que contém o resultado como Matriz na propriedade **data** .

* **Erro:** Nenhum

### Exemplo da API getFieldValue() {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue(“xfa.form.form1.Subform1.TextField”);
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, propriedade)** Recupera a lista de valores para determinada propriedade dos campos especificados no Som expressão

* **Entrada:**

   * **som:** Matriz contendo expressões Som para os campos
   * **propriedade**: Nome da propriedade cujo valor é obrigatório

* **Saída:** Objeto que contém o resultado como Matriz na propriedade *data*

* **Erro:** Nenhum

**setFieldProperties(som, propriedade, valores)** Define o valor de determinada propriedade para todos os campos especificados nas expressões Som

* **Entrada:**

   * **som:** Matriz contendo expressões Som dos campos cujo valor precisa ser definido
   * **propriedade**: Propriedade cujo valor deve ser definido
   * **valor:** Matriz que contém valores de determinada propriedade para campos especificados em expressões Som

* **Saída:** Nenhum
* **Erro:** Nenhum

## Exemplo de uso da API Form Bridge {#sample-usage-of-form-bridge-api}

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
