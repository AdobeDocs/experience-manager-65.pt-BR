---
title: Chamada de AEM Forms usando solicitações REST
seo-title: Invoking AEM Forms using REST Requests
description: Chame processos criados no Workbench usando solicitações REST.
seo-description: Invoke processes created in Workbench using REST requests.
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
role: Developer
exl-id: 991fbc56-f144-4ae6-b010-8d02f780d347
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 0%

---

# Chamada de AEM Forms usando solicitações REST {#invoking-aem-forms-using-rest-requests}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

Os processos criados no Workbench podem ser configurados para que você possa chamá-los por meio de solicitações de Transferência de Estado Representacional (REST). As solicitações REST são enviadas de HTML pages. Ou seja, você pode invocar um processo do Forms diretamente de uma página da Web usando uma solicitação REST. Por exemplo, você pode abrir uma nova instância de uma página da Web. Em seguida, você pode invocar um processo Forms e carregar um documento PDF renderizado com dados que foram enviados em uma solicitação HTTP POST.

Existem dois tipos de clientes HTML. O primeiro cliente do HTML é um cliente AJAX gravado em JavaScript. O segundo cliente é um formulário HTML que contém um botão Enviar. Um aplicativo cliente baseado em HTML não é o único cliente REST possível. Qualquer aplicativo cliente que suporta solicitações HTTP pode chamar um serviço usando uma invocação REST. Por exemplo, você pode invocar um serviço usando uma invocação REST de um formulário PDF. (Consulte [Chamar o processo MyApplication/EncryptDocument do Acrobat](#rest-invocation-examples).)

Ao usar solicitações REST, é recomendável não chamar os serviços Forms diretamente. Em vez disso, chame processos que foram criados no Workbench. Ao criar um processo que se destina à invocação REST, use um ponto de início programático. Nessa situação, o endpoint REST é adicionado automaticamente. Para obter informações sobre como criar processos no Workbench, consulte [Uso do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Ao chamar um serviço usando REST, você é solicitado a fornecer um nome de usuário e senha dos formulários AEM. No entanto, se você não quiser especificar um nome de usuário e senha, poderá desativar a segurança de serviço.

Para chamar um serviço Forms (um processo se torna um serviço quando o processo é ativado) usando REST, configure um terminal REST. (Consulte &quot;Gerenciamento de endpoints&quot; em [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).)

Depois que um endpoint REST é configurado, é possível chamar um serviço Forms usando um método GET HTTP ou um método POST.

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

O `ServiceName` é o nome do serviço Forms a ser chamado. O `OperationName` é o nome da operação do serviço. Se esse valor não for especificado, esse nome assumirá `invoke`, que é o nome da operação que inicia o processo. O `ServiceVersion` é a versão codificada no formato X.Y. Se esse valor não for especificado, a versão mais recente será usada. O `enctype` também pode ser `application/x-www-form-urlencoded`.

## Tipos de dados compatíveis {#supported-data-types}

Os seguintes tipos de dados são compatíveis ao chamar serviços da AEM Forms usando solicitações REST:

* Tipos de dados primitivos Java, como sequências e números inteiros
* `com.adobe.idp.Document` tipo de dados
* Tipos de dados XML, como `org.w3c.Document` e `org.w3c.Element`
* Objetos de coleção como `java.util.List` e `java.util.Map`

   Esses tipos de dados são comumente aceitos como valores de entrada para processos criados no Workbench.

   Se um serviço Forms for chamado com o método POST HTTP, os argumentos serão passados dentro do corpo da solicitação HTTP. Se a assinatura do serviço AEM Forms tiver um parâmetro de entrada de string, o corpo da solicitação poderá conter o valor de texto do parâmetro de entrada. Se a assinatura do serviço definir vários parâmetros de string, a solicitação poderá seguir o `application/x-www-form-urlencoded` notação com os nomes de parâmetro usados como nomes de campo do formulário.

   Se um serviço Forms retornar um parâmetro de string, o resultado será uma representação textual do parâmetro de saída. Se um serviço retornar vários parâmetros de string, o resultado será um documento XML codificando os parâmetros de saída no seguinte formato:
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >O `output-paramater1` representa o nome do parâmetro de saída.

   Se um serviço Forms exigir um `com.adobe.idp.Document` , o serviço só pode ser chamado usando o método POST HTTP. Se o serviço exigir um `com.adobe.idp.Document` , o corpo da solicitação HTTP se torna o conteúdo do objeto Documento de entrada.

   Se um serviço AEM Forms exigir vários parâmetros de entrada, o corpo da solicitação HTTP deverá ser uma mensagem MIME multipart, conforme definido pela RFC 1867. (RFC 1867 é um padrão usado por navegadores da Web para fazer upload de arquivos para sites.) Cada parâmetro de entrada deve ser enviado como uma parte separada da mensagem multipart e codificado no `multipart/form-data` formato. O nome de cada parte deve corresponder ao nome do parâmetro.

   Listas e mapas também são usados como valores de entrada para processos do AEM Forms criados no Workbench. Como resultado, você pode usar esses tipos de dados ao usar uma solicitação REST. Matrizes Java não são compatíveis porque não são usadas como um valor de entrada para um processo AEM Forms.

   Se um parâmetro de entrada for uma lista, um cliente REST poderá enviá-lo especificando o parâmetro várias vezes (uma vez para cada item na lista). Por exemplo, se A for uma lista de documentos, a entrada deverá ser uma mensagem multiparte consistindo em várias partes chamadas A. Nesse caso, cada parte chamada A se tornará um item na lista de entrada. Se B for uma lista de cadeias de caracteres, a entrada pode ser uma `application/x-www-form-urlencoded` mensagem que consiste em vários campos chamados B. Nesse caso, cada campo de formulário chamado B se torna um item na lista de entrada.

   Se um parâmetro de entrada for um mapa e for o parâmetro de entrada somente serviços, cada parte/campo da mensagem de entrada se tornará um registro de chave/valor no mapa. O nome de cada parte/campo torna-se a chave do registro. O conteúdo de cada parte/campo torna-se o valor do registro.

   Se um mapa de entrada não for o parâmetro de entrada somente de serviços, cada registro de chave/valor que pertence ao mapa poderá ser enviado usando um parâmetro chamado como concatenação do nome do parâmetro e da chave do registro. Por exemplo, um mapa de entrada chamado `attributes` pode ser enviado com uma lista dos seguintes pares chave/valores:

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   Isso se traduz em um mapa de três registros: `Color=red`, `Shape=box`e `Width=5`.

   Os parâmetros de saída da lista e os tipos de mapa tornam-se parte da mensagem XML resultante. A lista de saída é representada em XML como uma série de elementos XML com um elemento para cada item na lista. Cada elemento recebe o mesmo nome do parâmetro da lista de saída. O valor de cada elemento XML é uma das duas coisas:

* Uma representação de texto do item na lista (se a lista consistir em tipos de sequência de caracteres)
* Um URL que aponta para o conteúdo do Documento (se a lista consiste em `com.adobe.idp.Document` objetos)

   O exemplo a seguir é uma mensagem XML retornada por um serviço que tem um único parâmetro de saída chamado *lista*, que é uma lista de números inteiros.
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`Um parâmetro de mapa de saída é representado na mensagem XML resultante como uma série de elementos XML com um elemento para cada registro no mapa. Cada elemento recebe o mesmo nome da chave do registro de mapa. O valor de cada elemento é uma representação de texto do valor do registro de mapa (se o mapa consiste em registros com um valor de string) ou um URL apontando para o conteúdo do Documento (se o mapa consiste em registros com a variável `com.adobe.idp.Document` valor). Abaixo está um exemplo de uma mensagem XML retornada por um serviço que tem um único parâmetro de saída chamado `map`. Esse valor de parâmetro é um mapa que consiste em registros que associam letras a `com.adobe.idp.Document` objetos.
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## Chamadas assíncronas {#asynchronous-invocations}

Alguns serviços da AEM Forms, como processos de longa duração centrados no ser humano, exigem muito tempo para serem concluídos. Esses serviços podem ser invocados de forma assíncrona e sem bloqueio. (Consulte [Invocando processos de longa vida centrados em seres humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Um serviço AEM Forms pode ser chamado de forma assíncrona, substituindo `services` com `async_invoke` no URL de invocação, como mostrado no exemplo a seguir.

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

Esse URL retorna o valor identificador (no formato &quot;text/plain&quot;) do trabalho responsável por essa invocação.

O status da invocação assíncrona pode ser recuperado usando um URL de invocação com `services` substituído por `async_status`. O URL deve conter um `job_id` parâmetro que especifica o valor de identificador do trabalho associado a esta invocação. Por exemplo:

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

Este URL retorna um valor inteiro (no formato &quot;text/plain&quot;) codificando o status do trabalho de acordo com a especificação do Gerenciador de trabalhos (por exemplo, 2 significa execução, 3 significa concluído, 4 significa falha e assim por diante).

Se a tarefa estiver concluída, o URL retornará o mesmo resultado que se o serviço fosse chamado de forma síncrona.

Quando o trabalho é concluído e o resultado é recuperado, o trabalho pode ser descartado usando um URL de invocação com `services` é substituído por `async_dispose`. O URL também deve conter uma `job_id` especifica o valor do identificador da tarefa. Por exemplo:

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

Se o trabalho for descartado com êxito, esse URL retornará uma mensagem vazia.

## Relatório de erros {#error-reporting}

Se não for possível concluir uma solicitação de invocação síncrona ou assíncrona devido a uma exceção ser lançada no servidor, a exceção será relatada como parte da mensagem de resposta HTTP. Se o URL de invocação (ou o `async_result` URL no caso de uma invocação assíncrona) não tem um sufixo .xml, o Provedor REST retorna o código HTTP `500 Internal Server Error` seguido por uma mensagem de exceção.

Se o URL de invocação (ou o `async_result` O URL no caso de uma invocação assíncrona) tem um sufixo .xml, o Provedor REST retorna o código HTTP `200 OK`seguido por um documento XML que descreve a exceção no formato a seguir.

```xml
 <exception>
       <exception_class_name>[
       <DSCError>
          <componentUID>component_UUD</componentUID>
         <errorCode>error_code</errorCode>
         <minorCode>minor_code</minorCode>
         <message>error_message</message>
       </DSCError>
 ]
       <message>exception_message</message>
     <stackTrace>exception_stack_trace</stackTrace>
       </exception_class_name>
     <exception>
       </exception>
 </exception>
```

O `DSCError` é opcional e está presente somente se a exceção for uma instância de `com.adobe.idp.dsc.DSCException`.

## Segurança e autenticação {#security-and-authentication}

Para fornecer invocações REST com um transporte seguro, um administrador de formulários AEM pode habilitar o protocolo HTTPS no servidor de aplicativos J2EE que hospeda o AEM Forms. Esta configuração é específica do servidor de aplicativos J2EE; ela não faz parte da configuração do servidor de formulários.

>[!NOTE]
>
>Como um desenvolvedor do Workbench que deseja expor seus processos por meio de um terminal REST, lembre-se do problema de vulnerabilidade XSS. As vulnerabilidades XSS podem ser usadas para roubar ou manipular cookies, modificar a apresentação do conteúdo e comprometer as informações confidenciais. É recomendável estender a lógica do processo com as regras adicionais de validação de dados de entrada e saída se a vulnerabilidade XSS for um problema.

## Serviços AEM Forms que oferecem suporte para a invocação REST {#aem-forms-services-that-support-rest-invocation}

Embora seja recomendável invocar processos criados usando o Workbench em vez de serviços diretamente, há alguns serviços da AEM Forms que suportam a invocação REST. O motivo pelo qual é recomendável invocar um processo em vez de um serviço diretamente é porque é mais eficiente invocar um processo. Considere o seguinte cenário. Suponha que você deseja criar uma política de um cliente REST. Ou seja, você deseja que o cliente REST defina valores como o nome da política, o período de concessão offline.

Para criar uma política, é necessário definir tipos de dados complexos, como um `PolicyEntry` objeto. A `PolicyEntry` O objeto define atributos como permissões associadas à política. (Consulte [Criando Políticas](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

Em vez de enviar uma solicitação REST para criar uma política (que incluiria a definição de tipos de dados complexos, como um `PolicyEntry` objeto ), crie um processo que crie uma política usando o Workbench. Defina o processo para aceitar variáveis de entrada primitivas, como um valor de string que defina o nome do processo ou um número inteiro que defina o período de concessão offline.

Dessa forma, não é necessário criar uma solicitação de invocação REST que inclua tipos de dados complexos exigidos pela operação. O processo define os tipos de dados complexos e tudo o que você faz do cliente REST é chamar o processo e passar os tipos de dados primitivos. Para obter informações sobre invocar um processo usando REST, consulte [Chamar o processo MyApplication/EncryptDocument usando REST](#rest-invocation-examples).

As listas a seguir especificam os serviços do AEM Forms que oferecem suporte à invocação REST direta.

* Serviço Distiller
* serviço Rights Management
* Serviço GeneratePDF
* Gerar serviço3dPDF
* FormDataIntegration

## Exemplos de invocação REST {#rest-invocation-examples}

Os seguintes exemplos de invocação REST são fornecidos:

* Transmissão de valores booleanos a um processo AEM Forms
* Transmissão de valores de data para um processo AEM Forms
* Envio de documentos a um processo do AEM Forms
* Transmissão de valores de documento e texto para um processo do AEM Forms
* Passar valores de enumeração para um processo do AEM Forms
* Chamar o processo MyApplication/EncryptDocument usando REST
* Chamar o processo MyApplication/EncryptDocument do Acrobat

   Cada exemplo demonstra como transmitir tipos de dados diferentes para um processo AEM Forms

**Transmissão de valores booleanos a um processo**

O exemplo de HTML a seguir passa dois `Boolean` para um processo AEM Forms chamado `RestTest2`. O nome do método de invocação é `invoke` e a versão é 1.0. Observe que o método HTML Post é usado.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest2/invoke/1.0" method="post">
 
 Boolean 1: <input type="text" name="inBooleanList" value="true">
 Boolean 2: <input type="text" name="inBooleanList" value="false">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Transmissão de valores de data para um processo**

O exemplo de HTML a seguir passa um valor de data para um processo AEM Forms chamado `SOAPEchoService`. O nome do método de invocação é `echoCalendar`. Observe que o HTML `Post` é usado.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post">
 
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Transmissão de documentos a um processo**

O exemplo de HTML a seguir chama um processo AEM Forms chamado `MyApplication/EncryptDocument` que requer um documento PDF. Para obter informações sobre esse processo, consulte [Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/MyApplication/EncryptDocument/invoke" method="post"
          enctype="multipart/form-data">
 
 File: <input type="file" name="value-to-echo">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**Transmissão de valores de documento e texto a um processo**

O exemplo de HTML a seguir chama um processo AEM Forms chamado `RestTest3` que requer um documento e dois valores de texto. Observe que o método HTML Post é usado.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest3" method="post"
          enctype="multipart/form-data">
 
 Doc: <input type="file" name="inDoc">
 String 1: <input type="text" name="inListOfStrings" value="hello">
 String 2: <input type="text" name="inListOfStrings" value="privet">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**Transmissão de valores de enumeração a um processo**

O exemplo de HTML a seguir chama um processo AEM Forms chamado `SOAPEchoService` que requer um valor de enumeração. Observe que o método HTML Post é usado.

```html
 <html>
 <body>
 
 <form name="input" action="https://hiro-xp:8080/rest/services/SOAPEchoService/echoEnum" method="post">
 
 Color Enum Value: <input type="text" name="value-to-echo" value="green">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Chamar o processo MyApplication/EncryptDocument usando REST**

Você pode chamar um processo de duração curta da AEM Forms chamado *MyApplication/EncryptDocument* utilizando REST.

>[!NOTE]
>
>Esse processo não se baseia em um processo AEM Forms existente. Para seguir junto com o exemplo de código, crie um processo chamado `MyApplication/EncryptDocument` usando o workbench. (Consulte [Uso do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não seguro passado para o processo. Essa ação se baseia na variável `SetValue` operação. O parâmetro de entrada para esse processo é um `document` variável de processo nomeada `inDoc`.
1. Criptografa o documento PDF com uma senha. Essa ação se baseia na variável `PasswordEncryptPDF` operação. O documento PDF criptografado por senha é retornado em uma variável de processo chamada `outDoc`.

   Quando esse processo é chamado usando uma solicitação REST, o documento PDF criptografado é exibido no navegador da Web. Antes de exibir o documento PDF, especifique a senha (a menos que a segurança esteja desativada). O código de HTML a seguir representa uma solicitação de invocação REST para o `MyApplication/EncryptDocument` processo.

   ```html
    <html>
    <body>
    <form action="https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument" method="post" enctype="multipart/form-data">
         <p>Chose a PDF file (.pdf) to send to the EncryptDocument process.</p>
         <p>file:
           <input type="file" name="inDoc" />
         </p>
         <p>
           <input type="submit"/>
         </p>
    </form>
    </body>
   ```

**Chamar o processo MyApplication/EncryptDocument do Acrobat** {#invoke-process-acrobat}

Você pode invocar um processo do Forms a partir do Acrobat usando uma solicitação REST. Por exemplo, você pode chamar a variável *MyApplication/EncryptDocument* processo. Para invocar um processo do Forms a partir do Acrobat, coloque um botão de envio em um arquivo XDP no Designer. (Consulte [Ajuda do Designer](https://www.adobe.com/go/learn_aemforms_designer_63).)

Especifique o URL para invocar o processo no botão *Enviar para URL* , conforme mostrado na ilustração a seguir.

O URL completo para invocar o processo é https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument.

Se o processo exigir um documento PDF como valor de entrada, certifique-se de enviar o formulário como PDF, conforme mostrado na ilustração anterior. Além disso, para invocar um processo com êxito, o processo deve retornar um documento PDF. Caso contrário, o Acrobat não poderá lidar com o valor de retorno e ocorrerá um erro. Não é necessário especificar o nome da variável de processo de entrada. Por exemplo, a variável *MyApplication/EncryptDocument* o processo tem uma variável de entrada chamada `inDoc`. Não é necessário especificar inDoc, desde que o formulário seja enviado como PDF.

Também é possível enviar dados de formulário como XML para um processo Forms. Para enviar dados XML, verifique se a variável `Submit As` O menu suspenso especifica XML. Como o valor de retorno do processo deve ser um documento PDF, o documento PDF é exibido no Acrobat.
