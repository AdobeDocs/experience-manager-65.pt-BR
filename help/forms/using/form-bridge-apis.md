---
title: APIs Form Bridge para formulários HTML5
seo-title: Form Bridge APIs for HTML5 forms
description: Aplicativos externos usam a API FormBridge para se conectar ao Formulário móvel XFA. A API despacha um evento FormBridgeInitialized na janela pai.
seo-description: External applications use the FormBridge API to connect to the XFA Mobile Form. The API dispatches a FormBridgeInitialized event on the parent window.
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# APIs Form Bridge para formulários HTML5 {#form-bridge-apis-for-html-forms}

Você pode usar as APIs Form Bridge para abrir um canal de comunicação entre formulários HTML5 baseados em XFA e seus aplicativos. As APIs do Form Bridge fornecem um **connect** API para criar a conexão.

O **connect** A API aceita um manipulador como argumento. Depois que uma conexão bem-sucedida é criada entre o formulário HTML5 baseado em XFA e o Form Bridge, o identificador é chamado.

Você pode usar o seguinte código de exemplo para criar a conexão.

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

## API Form Bridge disponível  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

Retorna o número da versão da biblioteca de scripts

* **Entrada**: Nenhum
* **Saída**: Número da versão da biblioteca de scripts
* **Erros**: Nenhum

**isConnected()** Verifica se o Estado do Formulário foi inicializado

* **Entrada**: Nenhum
* **Saída**: **Verdadeiro** se o Estado do formulário XFA tiver sido inicializado

* **Erros**: Nenhum

**connect(manipulador, contexto)** Faz uma conexão com o FormBridge e executa a função depois que a conexão é feita e o Estado do formulário é inicializado

* **Entrada**:

   * **manipulador**: Função a ser executada após a conexão do Form Bridge
   * **contexto**: O objeto ao qual o contexto (este) da variável *manipulador* são definidas.

* **Saída**: Nenhum
* **Erro**: Nenhum

**getDataXML(options)** Retorna os dados de formulário atuais em Formato XML

* **Entrada:**

   * **opções:** Objeto JavaScript contendo as seguintes propriedades:

      * **Erro**: Função do manipulador de erros
      * **success**: Função de manipulador de sucesso. Essa função passou um objeto contendo XML em *dados* propriedade.
      * **contexto**: O objeto ao qual o contexto (este) da variável *success* é definida
      * **validationChecker**: Função para chamar para verificar erros de validação recebidos do servidor. A função de validação recebe uma matriz de sequências de erro.
      * **formState**: O estado JSON do formulário XFA para o qual o XML de dados deve ser retornado. Se não especificado, retorna o XML de dados para o formulário renderizado no momento.

* **Saída:** Nenhum
* **Erro:** Nenhum

**registerConfig(configName, config)** Registra configurações específicas do usuário/portal com o FormBridge. Essas configurações substituem as configurações padrão. As configurações compatíveis são especificadas na seção de configuração.

* **Entrada:**

   * **configName:** Nome da configuração a ser substituída

      * **widgetConfig:** Permite que o usuário substitua os widgets padrão no formulário por widgets personalizados. A configuração é substituída da seguinte maneira:

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** Permite que o usuário substitua o comportamento padrão de renderização somente na primeira página. A configuração é substituída da seguinte maneira:

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true false=&quot;&quot;>, deletePageDisabled: &lt;true false=&quot;&quot;> }).*

      * **LoggingConfig:** Permite que o usuário substitua o nível de registro, desative o registro em uma categoria ou exiba o console de logs ou envie para o servidor. A configuração pode ser substituída da seguinte maneira:

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

      * **SubmitServiceProxyConfig:** Permitir que os usuários registrem os serviços de envio e proxy do agente de log.

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **configuração:** Valor da configuração



* **Saída:** Objeto que contém o valor original da configuração em *dados* propriedade.

* **Erro:** Nenhum

**hideFields(fieldArray)** Oculta os campos cujas expressões Som são fornecidas no fieldArray. Define a propriedade presence dos campos especificados como invisíveis

* **Entrada:**

   * **fieldArray:** Matriz de expressões Algumas para os campos a serem ocultados

* **Saída:** Nenhum
* **Erro:** Nenhum

**showFields(fieldArray)** Mostra os campos cujas expressões Som são fornecidas no fieldArray. Define a propriedade presence dos campos fornecidos como visíveis

* **Entrada:**

   * **fieldArray:** Matriz de expressões Algumas para os campos serem exibidos

* **Saída:** Nenhum
* **Erro:** Nenhum

**hideSubmitButtons()** Oculta todos os botões Enviar no formulário

* **Entrada**: Nenhum
* **Saída**: Nenhum
* **Erro**: Lança a exceção se o Estado do Formulário não for inicializado

**getFormState()** Retorna o JSON que representa o Estado do formulário

* **Entrada:** Nenhum
* **Saída:** Objeto que contém JSON que representa o Estado de Formulário atual em *dados* propriedade.

* **Erro:** Nenhum

**restoreFormState(options)** Restaura o Estado do formulário a partir do estado JSON fornecido no objeto de opções. O estado é aplicado e os manipuladores de erro ou sucesso são chamados após a conclusão da operação

* **Entrada:**

   * **Opções:** Objeto JavaScript contendo as seguintes propriedades:

      * **Erro**: Função do manipulador de erros
      * **success**: Função do manipulador de sucesso
      * **contexto**: O objeto ao qual o contexto (este) da variável *success* estão definidas
      * **formState**: Estado JSON do formulário. O formulário é restaurado para o estado JSON.

* **Saída:** Nenhum
* **Erro:** Nenhum

**setFocus (som)** Define o foco no campo especificado na expressão Som

* **Entrada:** Algumas expressões do campo em que o foco deve ser definido
* **Saída:** Nenhum
* **Erro:** Lança uma exceção no caso de expressão Som incorreta

**setFieldValue (som, valor)** Define o valor dos campos para as expressões Som fornecidas

* **Entrada:**

   * **som:** Matriz contendo expressões Som do campo. A expressão som para definir o valor dos campos.
   * **valor:** Matriz contendo valores correspondentes a expressões Som fornecidas em um **som** matriz. Se o tipo de dados do valor não for o mesmo que fieldType, o valor não será modificado.

* **Saída:** Nenhum
* **Erro:** Lança uma Exceção no caso de uma expressão Som incorreta

**getFieldValue (som)** Retorna o valor dos campos para as expressões Algumas fornecidas

* **Entrada:** Matriz contendo expressões Som dos campos cujo valor deve ser recuperado
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

**getFieldProperties(som, propriedade)** Recupere a lista de valores para determinada propriedade dos campos especificados nas expressões Som

* **Entrada:**

   * **som:** Matriz contendo expressões Som para os campos
   * **propriedade**: Nome da propriedade cujo valor é obrigatório

* **Saída:** Objeto que contém o resultado como Matriz em *dados* propriedade

* **Erro:** Nenhum

**setFieldProperties(som, propriedade, valores)** Define o valor da propriedade fornecida para todos os campos especificados nas expressões Som

* **Entrada:**

   * **som:** Matriz contendo expressões Som dos campos cujo valor deve ser definido
   * **propriedade**: Propriedade cujo valor deve ser definido
   * **valor:** Matriz contendo valores da propriedade fornecida para campos especificados em expressões Som

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
