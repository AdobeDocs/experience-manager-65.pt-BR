---
title: Chamada do AEM Forms usando solicitações REST
seo-title: Chamada do AEM Forms usando solicitações REST
description: Chame processos criados no Workbench usando solicitações REST.
seo-description: Chame processos criados no Workbench usando solicitações REST.
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 0%

---


# Invocando o AEM Forms usando solicitações REST {#invoking-aem-forms-using-rest-requests}

Os processos criados no Workbench podem ser configurados para que você possa invocá-los por meio de solicitações de transferência de estado de representação (REST). As solicitações REST são enviadas de páginas HTML. Ou seja, você pode invocar um processo do Forms diretamente de uma página da Web usando uma solicitação REST. Por exemplo, você pode abrir uma nova instância de uma página da Web. Em seguida, você pode invocar um processo Forms e carregar um documento PDF renderizado com dados que foram enviados em uma solicitação de POST HTTP.

Existem dois tipos de clientes HTML. O primeiro cliente HTML é um cliente AJAX gravado em JavaScript. O segundo cliente é um formulário HTML que contém um botão Enviar. Um aplicativo cliente baseado em HTML não é o único cliente REST possível. Qualquer aplicativo cliente que suporte solicitações HTTP pode chamar um serviço usando uma chamada REST. Por exemplo, é possível invocar um serviço usando uma invocação REST de um formulário PDF. (Consulte [Invocando o processo MyApplication/EncryptDocument do Acrobat](#rest-invocation-examples).)

Ao usar solicitações REST, recomenda-se que você não chame os serviços Forms diretamente. Em vez disso, chame processos que foram criados no Workbench. Ao criar um processo destinado à invocação REST, use um ponto de start programático. Nessa situação, o terminal REST é adicionado automaticamente. Para obter informações sobre como criar processos no Workbench, consulte [Usando o Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Ao chamar um serviço usando REST, você é solicitado a fornecer um nome de usuário e senha para formulários AEM. No entanto, se você não quiser especificar um nome de usuário e senha, poderá desativar a segurança do serviço.

Para chamar um serviço Forms (um processo se torna um serviço quando o processo é ativado) usando REST, configure um terminal REST. (Consulte &quot;Gerenciando Pontos de Extremidade&quot; em [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_63).)

Depois que um terminal REST é configurado, você pode chamar um serviço Forms usando um método de GET HTTP ou um método POST.

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

O valor `ServiceName` obrigatório é o nome do serviço Forms a ser chamado. O valor opcional `OperationName` é o nome da operação do serviço. Se esse valor não for especificado, esse nome assumirá `invoke` como padrão, que é o nome da operação que start o processo. O valor opcional `ServiceVersion` é a versão codificada no formato X.Y. Se esse valor não for especificado, a versão mais recente será usada. O valor `enctype` também pode ser `application/x-www-form-urlencoded`.

## Tipos de dados suportados {#supported-data-types}

Os seguintes tipos de dados são suportados ao chamar serviços AEM Forms usando solicitações REST:

* Tipos de dados primitivos Java, como Strings e inteiros
* `com.adobe.idp.Document` tipo de dados
* Tipos de dados XML, como `org.w3c.Document` e `org.w3c.Element`
* Objetos de coleção como `java.util.List` e `java.util.Map`

   Esses tipos de dados são comumente aceitos como valores de entrada para processos criados no Workbench.

   Se um serviço Forms for chamado com o método POST HTTP, os argumentos serão transmitidos dentro do corpo da solicitação HTTP. Se a assinatura do serviço AEM Forms tiver um parâmetro de entrada de string, o corpo da solicitação poderá conter o valor de texto do parâmetro de entrada. Se a assinatura do serviço definir vários parâmetros de string, a solicitação poderá seguir a notação `application/x-www-form-urlencoded` do HTTP com os nomes dos parâmetros usados como nomes de campo do formulário.

   Se um serviço Forms retornar um parâmetro de string, o resultado será uma representação textual do parâmetro de saída. Se um serviço retornar vários parâmetros de string, o resultado será um documento XML codificando os parâmetros de saída no seguinte formato:
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >O valor `output-paramater1` representa o nome do parâmetro de saída.

   Se um serviço Forms exigir um parâmetro `com.adobe.idp.Document`, o serviço só poderá ser chamado usando o método POST HTTP. Se o serviço exigir um parâmetro `com.adobe.idp.Document`, o corpo da solicitação HTTP se tornará o conteúdo do objeto de Documento de entrada.

   Se um serviço AEM Forms exigir vários parâmetros de entrada, o corpo da solicitação HTTP deverá ser uma mensagem MIME multiparte, conforme definido pela RFC 1867. (RFC 1867 é um padrão usado por navegadores da Web para fazer upload de arquivos para sites.) Cada parâmetro de entrada deve ser enviado como uma parte separada da mensagem multiparte e codificado no formato `multipart/form-data`. O nome de cada parte deve corresponder ao nome do parâmetro.

   Listas e mapas também são usados como valores de entrada para processos AEM Forms criados no Workbench. Como resultado, você pode usar esses tipos de dados ao usar uma solicitação REST. As matrizes Java não são suportadas porque não são usadas como um valor de entrada para um processo AEM Forms.

   Se um parâmetro de entrada for uma lista, um cliente REST poderá enviá-lo especificando o parâmetro várias vezes (uma vez para cada item na lista). Por exemplo, se A for uma lista de documentos, a entrada deverá ser uma mensagem multiparte que consiste em várias partes chamadas A. Nesse caso, cada parte chamada A se torna um item na lista de entrada. Se B for uma lista de strings, a entrada pode ser uma mensagem `application/x-www-form-urlencoded` que consiste em vários campos chamados B. Nesse caso, cada campo de formulário chamado B se torna um item na lista de entrada.

   Se um parâmetro de entrada for um mapa e for o parâmetro de entrada somente serviços, então cada parte/campo da mensagem de entrada se tornará um registro de chave/valor no mapa. O nome de cada parte/campo se torna a chave do registro. O conteúdo de cada parte/campo se torna o valor do registro.

   Se um mapa de entrada não for o parâmetro de entrada somente serviços, cada registro de chave/valor que pertence ao mapa pode ser enviado usando um parâmetro chamado concatenação do nome do parâmetro e da chave do registro. Por exemplo, um mapa de entrada chamado `attributes` pode ser enviado com uma lista dos seguintes pares de chave/valores:

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   Isso se traduz em um mapa de três registros: `Color=red`, `Shape=box` e `Width=5`.

   Os parâmetros de saída dos tipos de lista e mapa tornam-se parte da mensagem XML resultante. A lista de saída é representada em XML como uma série de elementos XML com um elemento para cada item na lista. Todo elemento recebe o mesmo nome do parâmetro de lista de saída. O valor de cada elemento XML é uma das duas coisas:

* Uma representação em texto do item na lista (se a lista consistir em tipos de string)
* Um URL que aponta para o conteúdo do Documento (se a lista consistir em `com.adobe.idp.Document` objetos)

   O exemplo a seguir é uma mensagem XML retornada por um serviço que tem um único parâmetro de saída chamado *lista*, que é uma lista de números inteiros.
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`Um parâmetro de mapa de saída é representado na mensagem XML resultante como uma série de elementos XML com um elemento para cada registro no mapa. Todos os elementos recebem o mesmo nome que a chave do registro do mapa. O valor de cada elemento é uma representação em texto do valor do registro do mapa (se o mapa consiste em registros com um valor de sequência) ou um URL que aponta para o conteúdo do Documento (se o mapa consiste em registros com o valor `com.adobe.idp.Document`). Abaixo está um exemplo de uma mensagem XML retornada por um serviço que tem um único parâmetro de saída chamado `map`. Este valor de parâmetro é um mapa que consiste em registros que associam letras a objetos `com.adobe.idp.Document`.
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## invocações assíncronas {#asynchronous-invocations}

Alguns serviços da AEM Forms, como processos de longa duração centrados no ser humano, exigem muito tempo para serem concluídos. Esses serviços podem ser chamados de forma assíncrona de maneira não bloqueada. (Consulte [Invocando processos de longa vida centrados em humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Um serviço AEM Forms pode ser chamado de forma assíncrona, substituindo `services` por `async_invoke` no URL de invocação, como mostrado no exemplo a seguir.

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

Esse URL retorna o valor identificador (no formato &quot;texto/simples&quot;) do trabalho responsável por essa invocação.

O status da invocação assíncrona pode ser recuperado usando um URL de invocação com `services` substituído por `async_status`. O URL deve conter um parâmetro `job_id` que especifique o valor identificador do trabalho associado a esta invocação. Por exemplo:

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

Esse URL retorna um valor inteiro (no formato &quot;texto/simples&quot;) codificando o status do job de acordo com a especificação do Gerenciador de Jobs (por exemplo, 2 significa execução, 3 significa concluído, 4 significa falha e assim por diante).

Se o trabalho for concluído, o URL retornará o mesmo resultado que se o serviço fosse chamado de forma síncrona.

Quando o trabalho é concluído e o resultado é recuperado, o trabalho pode ser descartado usando um URL de invocação com `services` é substituído por `async_dispose`. O URL também deve conter um parâmetro `job_id` especificando o valor identificador do trabalho. Por exemplo:

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

Se o trabalho for descartado com êxito, esse URL retornará uma mensagem vazia.

## Relatórios de erro {#error-reporting}

Se não for possível concluir uma solicitação de invocação síncrona ou assíncrona devido a uma exceção ser lançada no servidor, a exceção será relatada como parte da mensagem de resposta HTTP. Se o URL de invocação (ou o URL `async_result` no caso de uma invocação assíncrona) não tiver um sufixo .xml, o Provedor REST retornará o código HTTP `500 Internal Server Error` seguido por uma mensagem de exceção.

Se o URL de invocação (ou o URL `async_result` no caso de uma invocação assíncrona) tiver um sufixo .xml, o Provedor REST retornará o código HTTP `200 OK`seguido por um documento XML descrevendo a exceção no formato a seguir.

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

O elemento `DSCError` é opcional e está presente somente se a exceção for uma instância de `com.adobe.idp.dsc.DSCException`.

## Segurança e autenticação {#security-and-authentication}

Para fornecer invocações REST com um transporte seguro, um administrador de formulários AEM pode habilitar o protocolo HTTPS no servidor de aplicativos J2EE que hospeda o AEM Forms. Esta configuração é específica do servidor de aplicações J2EE; ela não faz parte da configuração do servidor de formulários.

>[!NOTE]
>
>Como um desenvolvedor do Workbench que deseja expor seus processos por meio de um terminal REST, lembre-se do problema de vulnerabilidade XSS. As vulnerabilidades XSS podem ser usadas para roubar ou manipular cookies, modificar a apresentação do conteúdo e comprometer as informações confidenciais. É recomendável estender a lógica do processo com as regras adicionais de validação de dados de entrada e saída se a vulnerabilidade XSS for um problema.

## Serviços AEM Forms que oferecem suporte para a invocação REST {#aem-forms-services-that-support-rest-invocation}

Embora seja recomendável que você chame processos criados usando o Workbench em vez de serviços diretamente, há alguns serviços da AEM Forms que suportam a invocação REST. O motivo pelo qual é recomendado que você chame um processo em vez de um serviço diretamente é porque é mais eficiente invocar um processo. Considere o seguinte cenário. Suponha que você deseja criar uma política a partir de um cliente REST. Ou seja, você deseja que o cliente REST defina valores como o nome da política, o período de empréstimo offline.

Para criar uma política, é necessário definir tipos de dados complexos, como um objeto `PolicyEntry`. Um objeto `PolicyEntry` define atributos como permissões associadas à política. (Consulte [Criando Políticas](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

Em vez de enviar uma solicitação REST para criar uma política (que incluiria a definição de tipos de dados complexos, como um objeto `PolicyEntry`), crie um processo que crie uma política usando o Workbench. Defina o processo para aceitar variáveis de entrada primitivas, como um valor de string que define o nome do processo ou um número inteiro que define o período de empréstimo offline.

Dessa forma, não é necessário criar uma solicitação de invocação REST que inclua tipos de dados complexos exigidos pela operação. O processo define os tipos de dados complexos e tudo o que você faz do cliente REST é chamar o processo e passar por tipos de dados primitivos. Para obter informações sobre como invocar um processo usando REST, consulte [Invocando o processo MyApplication/EncryptDocument usando REST](#rest-invocation-examples).

As listas a seguir especificam os serviços AEM Forms que oferecem suporte à invocação REST direta.

* Serviço Distiller
* serviço Rights Management
* Serviço GeneratePDF
* Gerar serviço 3dPDF
* FormDataIntegration

## Exemplos de invocação REST {#rest-invocation-examples}

Os seguintes exemplos de invocação REST são fornecidos:

* Transmissão de valores booleanos para um processo AEM Forms
* Transmissão de valores de data para um processo AEM Forms
* Transmissão de documentos para um processo AEM Forms
* Transmissão de valores de documento e texto para um processo AEM Forms
* Transmissão de valores de lista discriminada para um processo AEM Forms
* Chamada do processo MyApplication/EncryptDocument usando REST
* Chamada do processo MyApplication/EncryptDocument da Acrobat

   Cada exemplo demonstra como passar tipos de dados diferentes para um processo AEM Forms

**Transmissão de valores booleanos para um processo**

O exemplo HTML a seguir transmite dois valores `Boolean` para um processo AEM Forms chamado `RestTest2`. O nome do método de invocação é `invoke` e a versão é 1.0. Observe que o método HTML Post é usado.

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

O exemplo HTML a seguir transmite um valor de data para um processo AEM Forms chamado `SOAPEchoService`. O nome do método de invocação é `echoCalendar`. Observe que o método HTML `Post` é usado.

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

**Transmissão de documentos para um processo**

O exemplo HTML a seguir chama um processo AEM Forms chamado `MyApplication/EncryptDocument` que requer um documento PDF. Para obter informações sobre esse processo, consulte [Invocando o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

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

**Transmissão de valores de documento e texto para um processo**

O exemplo HTML a seguir chama um processo AEM Forms chamado `RestTest3` que requer um documento e dois valores de texto. Observe que o método HTML Post é usado.

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

**Transmissão de valores de lista discriminada para um processo**

O exemplo HTML a seguir chama um processo AEM Forms chamado `SOAPEchoService` que requer um valor de lista discriminada. Observe que o método HTML Post é usado.

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

**Chamada do processo MyApplication/EncryptDocument usando REST**

Você pode chamar um processo de duração curta da AEM Forms chamado *MyApplication/EncryptDocument* usando REST.

>[!NOTE]
>
>Esse processo não se baseia em um processo AEM Forms existente. Para acompanhar o exemplo de código, crie um processo chamado `MyApplication/EncryptDocument` usando o workbench. (Consulte [Usando o Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não protegido passado para o processo. Esta ação se baseia na operação `SetValue`. O parâmetro de entrada para esse processo é uma variável de processo `document` chamada `inDoc`.
1. Criptografa o documento PDF com uma senha. Esta ação se baseia na operação `PasswordEncryptPDF`. O documento PDF criptografado por senha é retornado em uma variável de processo chamada `outDoc`.

   Quando esse processo é chamado usando uma solicitação REST, o documento PDF criptografado é exibido no navegador da Web. Antes de visualização o documento PDF, especifique a senha (a menos que a segurança esteja desativada). O código HTML a seguir representa uma solicitação de invocação REST para o processo `MyApplication/EncryptDocument`.

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

**Chamada do processo MyApplication/EncryptDocument da Acrobat** {#invoke-process-acrobat}

Você pode invocar um processo Forms da Acrobat usando uma solicitação REST. Por exemplo, você pode chamar o processo *MyApplication/EncryptDocument*. Para chamar um processo do Forms do Acrobat, coloque um botão Enviar em um arquivo XDP no Designer. (Consulte [Ajuda do Designer](https://www.adobe.com/go/learn_aemforms_designer_63).)

Especifique o URL para invocar o processo no campo *Enviar para URL* do botão, conforme mostrado na ilustração a seguir.

O URL completo para invocar o processo é https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument.

Se o processo exigir um documento PDF como valor de entrada, certifique-se de enviar o formulário como PDF, como mostrado na ilustração anterior. Além disso, para chamar um processo com êxito, o processo deve retornar um documento PDF. Caso contrário, o Acrobat não poderá lidar com o valor de retorno e ocorrerá um erro. Não é necessário especificar o nome da variável de processo de entrada. Por exemplo, o processo *MyApplication/EncryptDocument* tem uma variável de entrada chamada `inDoc`. Não é necessário especificar inDoc, desde que o formulário seja enviado como PDF.

Você também pode enviar dados de formulário como XML para um processo Forms. Para enviar dados XML, certifique-se de que o menu suspenso `Submit As` especifique XML. Como o valor de retorno do processo deve ser um documento PDF, o documento PDF é exibido no Acrobat.
