---
title: Chamar o AEM Forms usando comunicação remota
description: Use o Remoting para chamar um processo do AEM Forms para chamar processos criados no Workbench. Você pode chamar um processo do AEM Forms de um aplicativo cliente criado com o Flex.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 94a48776-f537-4b4e-8d71-51b08e463cba
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '4593'
ht-degree: 0%

---

# Chamar o AEM Forms usando comunicação remota {#invoking-aem-forms-using-remoting}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

Os processos criados no Workbench podem ser chamados usando a Comunicação Remota. Ou seja, você pode chamar um processo do AEM Forms de um aplicativo cliente criado com o Flex. Este recurso é baseado no Data Services.

>[!NOTE]
>
>Ao usar a Comunicação remota, é recomendável chamar processos que foram criados no Workbench, em vez de serviços da AEM Forms. No entanto, é possível chamar os serviços da AEM Forms diretamente. (Consulte Criptografar documentos do PDF usando o recurso Remoto, localizado no Centro de Desenvolvedores AEM Forms.)

>[!NOTE]
>
>Se um serviço do AEM Forms não estiver configurado para permitir acesso anônimo, as solicitações de um cliente Flex resultarão em um desafio de navegador da Web. O usuário deve digitar as credenciais de nome de usuário e senha.

O seguinte processo de vida curta do AEM Forms, chamado `MyApplication/EncryptDocument`, pode ser chamado usando Comunicação Remota. (Para obter informações sobre esse processo, como seus valores de entrada e saída, consulte [Exemplo de processo de vida curta](/help/forms/developing/aem-forms-processes.md).)

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>Para invocar um processo do AEM Forms usando um aplicativo do Flex, verifique se um endpoint remoto está ativado. Por padrão, um ponto de extremidade remoto é ativado ao implantar um processo.

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não seguro passado como um valor de entrada. Esta ação baseia-se no `SetValue` operação. O nome do parâmetro de entrada é `inDoc` e seu tipo de dados é `document`. (O `document` tipo de dados é um tipo de dados disponível no Workbench.)
1. Criptografa o documento PDF com uma senha. Esta ação baseia-se no `PasswordEncryptPDF` operação. O nome do valor de saída desse processo é `outDoc` e representa o documento PDF criptografado por senha. O tipo de dados do outDoc é `document`.
1. Salva o documento PDF criptografado por senha como um arquivo PDF no sistema de arquivos local. Esta ação baseia-se no `WriteDocument` operação.

>[!NOTE]
>
>A variável `MyApplication/EncryptDocument` O processo não se baseia em um processo AEM Forms existente. Para seguir junto com os exemplos de código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench.

>[!NOTE]
>
>Para obter informações sobre como usar o Remoting para invocar um processo de longa duração, consulte [Chamar processos de longa vida centrados no ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

**Consulte também**

[Inclusão do arquivo da biblioteca Flex do AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Lidar com documentos com (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Chamar um processo de vida curta transmitindo um documento não seguro usando o AEM Forms Remoting (obsoleto para formulários AEM)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticação de aplicativos clientes criados com o Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Enviar documentos seguros para invocar processos usando comunicação remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[Chamar serviços de componente personalizado usando Comunicação Remota](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[Criar um aplicativo cliente criado com o Flex que chame um processo de longa vida centrado no ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[Criação de aplicativos do Flash Builder que executam autenticação SSO usando tokens HTTP](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

<!-- For information on how to display process data in a Flex graph control, see [Displaying AEM Forms process data in Flex graphs](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

>[!NOTE]
>
>*Certifique-se de colocar o arquivo crossdomain.xml no lugar adequado. Por exemplo, supondo que você implantou o AEM Forms no JBoss, coloque esse arquivo no seguinte local: &lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war.*

## Inclusão do arquivo da biblioteca Flex do AEM Forms {#including-the-aem-forms-flex-library-file}

Para chamar programaticamente processos do AEM Forms usando Comunicação remota, adicione o arquivo adobe-remoting-provider.swc ao caminho de classe do projeto do Flex. Esse arquivo SWC está no seguinte local:

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

  onde &lt;*install_diretory*> é o diretório onde o AEM Forms está instalado.

**Consulte também**

[Chamar o AEM Forms usando (obsoleto para o AEM formulários) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Lidar com documentos com (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Chamar um processo de vida curta transmitindo um documento não seguro usando o AEM Forms Remoting (obsoleto para formulários AEM)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticação de aplicativos clientes criados com o Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Lidar com documentos com Comunicação remota {#handling-documents-with-remoting}

Um dos tipos Java™ não primitivos mais importantes usados no AEM Forms é o `com.adobe.idp.Document` classe. Geralmente, um documento é necessário para chamar uma operação do AEM Forms. É principalmente um documento PDF, mas pode conter outros tipos de documento, como SWF, HTML, XML ou um arquivo DOC. (Consulte [Passagem de dados para serviços da AEM Forms usando a API do Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Um aplicativo cliente criado com o Flex não pode solicitar diretamente um documento. Por exemplo, não é possível iniciar o Adobe Reader para solicitar um URL que produz um arquivo PDF. As solicitações para tipos de documentos, como documentos PDF e Microsoft® Word, retornam um resultado que é um URL. É responsabilidade do cliente exibir o conteúdo do URL. O serviço de Gerenciamento de documentos ajuda a gerar informações de URL e tipo de conteúdo. As solicitações de documentos XML retornam o documento XML completo no resultado.

### Transmitir um documento como parâmetro de entrada {#passing-a-document-as-an-input-parameter}

Um aplicativo cliente criado com o Flex não pode passar um documento diretamente para um processo do AEM Forms. Em vez disso, o aplicativo cliente usa uma instância do `mx.rpc.livecycle.DocumentReference` classe ActionScript para passar parâmetros de entrada para uma operação que espera uma `com.adobe.idp.Document` instância. Um aplicativo cliente do Flex tem várias opções para configurar um `DocumentReference` objeto:

* Quando o documento estiver no servidor e seu local de arquivo for conhecido, defina a propriedade referenceType do objeto DocumentReference como REF_TYPE_FILE. Defina a propriedade fileRef para o local do arquivo, como mostra o exemplo a seguir:

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* Quando o documento estiver no servidor e você souber seu URL, defina a propriedade referenceType do objeto DocumentReference como REF_TYPE_URL. Defina a propriedade url como o URL, conforme mostrado no exemplo a seguir:

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* Para criar um objeto DocumentReference a partir de uma sequência de caracteres de texto no aplicativo cliente, defina a propriedade referenceType do objeto DocumentReference como REF_TYPE_INLINE. Defina a propriedade text como o texto a ser incluído no objeto, conforme mostrado no exemplo a seguir:

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server's default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* Quando o documento não estiver no servidor, use o servlet de upload Remoto para carregar um documento no AEM Forms. Uma novidade no AEM Forms é a capacidade de fazer upload de documentos seguros. Ao fazer upload de um documento seguro, é necessário usar um usuário que tenha a *Usuário do aplicativo de carregamento de documento* função. Sem essa função, o usuário não pode carregar um documento seguro. É recomendável que você use o logon único para carregar um documento seguro. (Consulte [Enviar documentos seguros para invocar processos usando comunicação remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).)

>[!NOTE]
>
se o AEM Forms estiver configurado para permitir que documentos não seguros sejam carregados, você poderá usar um usuário que não tenha a função Usuário do aplicativo de carregamento de documentos para carregar um documento. Um usuário também pode ter a permissão Carregar documento. No entanto, se o AEM Forms estiver configurado para permitir somente documentos seguros, verifique se o usuário tem a função Usuário do aplicativo de upload de documentos ou a permissão Upload de documentos. (Consulte [Configuração do AEM Forms para aceitar documentos protegidos e não protegidos](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).

Você usa recursos padrão de upload de Flash para o URL de upload designado: `https://SERVER:PORT/remoting/lcfileupload`. Em seguida, você pode usar o `DocumentReference` sempre que um parâmetro de entrada do tipo `Document` é esperado
` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`O Início rápido da comunicação remota usa o servlet de upload da comunicação remota para passar um arquivo PDF para o `MyApplication/EncryptDocument`processo. (Consulte [Chamar um processo de vida curta transmitindo um documento não seguro usando o AEM Forms Remoting (obsoleto para formulários AEM)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

```java
 
private
function startUpload(): void  { 
 fileRef.addEventListener(Event.SELECT, selectHandler); 
 fileRef.addEventListener("uploadCompleteData", completeHandler); 
 try  { 
  var success: Boolean = fileRef.browse(); 
 }  
 catch (error: Error)  { 
  trace("Unable to browse for files."); 
 } 
}   
private
function selectHandler(event: Event): void { 
 var request: URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try  { 
  fileRef.upload(request); 
 }  
 catch (error: Error)  { 
  trace("Unable to upload file."); 
 } 
}  
private
function completeHandler(event: DataEvent): void  { 
 var params: Object = new Object(); 
 var docRef: DocumentReference = new DocumentReference(); 
 docRef.url = event.data as String; 
 docRef.referenceType = DocumentReference.REF_TYPE_URL; 
}
```

O Início rápido da comunicação remota usa o servlet de upload da comunicação remota para passar um arquivo PDF para o `MyApplication/EncryptDocument`processo. (Consulte [Chamar um processo de vida curta transmitindo um documento não seguro usando o AEM Forms Remoting (obsoleto para formulários AEM)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

### Envio de um documento de volta para um aplicativo cliente {#passing-a-document-back-to-a-client-application}

Um aplicativo cliente recebe um objeto do tipo `mx.rpc.livecycle.DocumentReference` para uma operação de serviço que retorna um `com.adobe.idp.Document` como um parâmetro de saída. Como um aplicativo cliente lida com objetos ActionScript e não com Java, você não pode transmitir um objeto Documento baseado em Java de volta para um cliente Flex. Em vez disso, o servidor gera um URL para o documento e transmite o URL de volta para o cliente. A variável `DocumentReference` do objeto `referenceType` propriedade especifica se o conteúdo está na variável `DocumentReference` objeto ou devem ser recuperados de um URL na `DocumentReference.url` propriedade. A variável `DocumentReference.contentType` propriedade especifica o tipo de documento.

**Consulte também**

[Chamar o AEM Forms usando (obsoleto para o AEM formulários) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Inclusão do arquivo da biblioteca Flex do AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Chamar um processo de vida curta transmitindo um documento não seguro usando o AEM Forms Remoting (obsoleto para formulários AEM)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticação de aplicativos clientes criados com o Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Enviar documentos seguros para invocar processos usando comunicação remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Chamar um processo de vida curta transmitindo um documento não seguro usando Comunicação Remota {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

Para chamar um processo do AEM Forms a partir de um aplicativo criado com o Flex, execute as seguintes tarefas:

1. Criar um `mx:RemoteObject` instância.
1. Criar um `ChannelSet` instância.
1. Transmita os valores de entrada necessários.
1. Manipule valores de retorno.

>[!NOTE]
>
Esta seção discute como chamar um processo do AEM Forms e carregar um documento quando o AEM Forms está configurado para carregar documentos não seguros. Para obter informações sobre como chamar processos do AEM Forms e fazer upload de documentos protegidos e como configurar o AEM Forms para aceitar documentos protegidos e não protegidos, consulte [Enviar documentos seguros para invocar processos usando comunicação remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).

**Criação de uma instância mx:RemoteObject**

Você cria um `mx:RemoteObject` instância para invocar um processo AEM Forms criado no Workbench. Para criar um `mx:RemoteObject` especifique os seguintes valores:

* **id:** O nome do `mx:RemoteObject` instância que representa o processo a ser chamado.
* **destino:** O nome do processo AEM Forms a ser chamado. Por exemplo, para chamar a variável `MyApplication/EncryptDocument` processo, especificar `MyApplication/EncryptDocument`.
* **resultado:** O nome do método Flex que manipula o resultado.

No prazo de `mx:RemoteObject` , especifique um `<mx:method>` tag que especifica o nome do método de chamada do processo. Normalmente, o nome de um método de chamada Forms é `invoke`.

O código de exemplo a seguir cria um `mx:RemoteObject` que invoca a variável `MyApplication/EncryptDocument` processo.

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**Criar um canal para o AEM Forms**

Um aplicativo cliente pode chamar o AEM Forms especificando um Canal no MXML ou ActionScript, como mostra o exemplo de ActionScript a seguir. O Canal deve ser um `AMFChannel`, `SecureAMFChannel`, `HTTPChannel`ou `SecureHTTPChannel`.

```java
     ...
     private function refresh():void{
         var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("my-amf",
             "https://yourlcserver:8080/remoting/messagebroker/amf"));
         EncryptDocument.setCredentials("administrator", "password");
         EncryptDocument.channelSet = cs;
     }
     ...
```

Atribua a `ChannelSet` para a instância `mx:RemoteObject` da instância `channelSet` (conforme mostrado no exemplo de código anterior). Geralmente, você importa a classe de canal em uma instrução import em vez de especificar o nome totalmente qualificado quando invoca o `ChannelSet.addChannel` método.

**Transmissão de valores de entrada**

Um processo criado no Workbench pode receber zero ou mais parâmetros de entrada e retornar um valor de saída. Um aplicativo cliente passa parâmetros de entrada em um `ActionScript` com campos que correspondem a parâmetros que pertencem ao processo do AEM Forms. O processo de vida curta, chamado `MyApplication/EncryptDocument`, requer um parâmetro de entrada chamado `inDoc`. O nome da operação exposta pelo processo é `invoke` (o nome padrão para um processo de vida curta). (Consulte [Chamar o AEM Forms usando (obsoleto para o AEM formulários) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

O código de exemplo a seguir passa um documento PDF para o `MyApplication/EncryptDocument` processo:

```java
     ...
     var params:Object = new Object();
 
     //Document is an instance of DocumentReference
     //that store an unsecured PDF document
     params["inDoc"] = pdfDocument;
 
     // Invoke an operation synchronously:
     EncryptDocument.invoke(params);
     ...
```

Neste exemplo de código, `pdfDocument` é um `DocumentReference` instância que contém um documento PDF não seguro. Para obter informações sobre uma `DocumentReference`, consulte [Lidar com documentos com (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting).

**Chamada de uma versão específica de um serviço**

Você pode chamar uma versão específica de um serviço Forms usando um `_version` parâmetro no mapa de parâmetros da invocação. Por exemplo, para invocar a versão 1.2 do `MyApplication/EncryptDocument` serviço:

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

A variável `version` O parâmetro deve ser uma cadeia de caracteres contendo um único ponto. Os valores à esquerda, versão principal e direita, versão secundária, do período devem ser números inteiros. Se este parâmetro não for especificado, a versão principal ativa é chamada.

**Manuseio de valores de retorno**

Os parâmetros de saída do processo do AEM Forms são desserializados em objetos do ActionScript a partir dos quais o aplicativo cliente extrai parâmetros específicos por nome, conforme mostrado no exemplo a seguir. (O valor de saída da variável `MyApplication/EncryptDocument` o processo é nomeado `outDoc`.)

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**Chamar o processo MyApplication/EncryptDocument**

Você pode chamar a variável `MyApplication/EncryptDocument` execute as seguintes etapas:

1. Criar um `mx:RemoteObject` instância por meio do ActionScript ou MXML. Consulte Criação de uma instância mx:RemoteObject.
1. Configurar um `ChannelSet` instância para se comunicar com o AEM Forms e associá-la à `mx:RemoteObject` instância. Consulte Criar um canal para o AEM Forms.
1. Chame o do ChannelSet `login` método ou o do serviço `setCredentials` para especificar o valor e a senha do identificador do usuário. (Consulte [Usando o logon único](invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. Preencher um `mx.rpc.livecycle.DocumentReference` instância com um documento PDF não seguro para passar para o `MyApplication/EncryptDocument` processo. (Consulte [Transmitir um documento como parâmetro de entrada](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter).)
1. Criptografe o documento PDF chamando o `mx:RemoteObject` da instância `invoke` método. Passe o `Object` que contém o parâmetro de entrada (que é o documento PDF não seguro). Consulte Transmissão de valores de entrada.
1. Recupere o documento PDF criptografado por senha retornado do processo. Consulte Tratamento de valores de retorno.

[Início rápido: chamar um processo de vida curta transmitindo um documento não seguro usando o AEM Forms Remoting (obsoleto para formulários AEM)](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## Autenticação de aplicativos clientes criados com o Flex {#authenticating-client-applications-built-with-flex}

Há várias maneiras das quais o gerente de usuários dos formulários AEM pode autenticar uma solicitação de comunicação remota de um aplicativo da Flex, incluindo o logon único da AEM Forms por meio do serviço de logon central, a autenticação básica e a autenticação personalizada. Quando nem o logon único nem o acesso anônimo estão habilitados, uma solicitação de Comunicação remota resulta em autenticação básica (padrão) ou autenticação personalizada.

A autenticação básica depende da autenticação básica J2EE padrão do container da aplicação Web. Para autenticação básica, um erro HTTP 401 causa um desafio do navegador. Isso significa que quando você tentar se conectar a um aplicativo Forms usando RemoteObject e ainda não tiver feito logon no aplicativo Flex, o navegador solicitará um nome de usuário e uma senha.

Para autenticação personalizada, o servidor envia uma falha ao cliente para indicar que a autenticação é necessária.

>[!NOTE]
>
Para obter informações sobre como executar a autenticação usando tokens HTTP, consulte [Criação de aplicativos do Flash Builder que executam autenticação SSO usando tokens HTTP](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens).

### Uso da autenticação personalizada {#using-custom-authentication}

Você habilita a autenticação personalizada no console de administração alterando o método de autenticação de Básico para Personalizado no ponto de extremidade remoto. Se você usar a autenticação personalizada, o aplicativo cliente chamará o `ChannelSet.login` para fazer logon e a variável `ChannelSet.logout` para fazer logoff.

>[!NOTE]
>
Na versão anterior do AEM Forms, você enviou credenciais para um destino chamando o `RemoteObject.setCredentials` método. A variável `setCredentials` O método de não passou as credenciais para o servidor até a primeira tentativa do componente de se conectar ao servidor. Portanto, se o componente emitiu um evento de falha, você não poderia ter certeza se a falha aconteceu devido a um erro de autenticação ou por outro motivo. A variável `ChannelSet.login` se conecta ao servidor quando você o chama, para que você possa lidar com um problema de autenticação imediatamente. Embora você possa continuar usando o `setCredentials` , é recomendável usar o método `ChannelSet.login` método.

Como vários destinos podem usar os mesmos canais e o objeto ChannelSet correspondente, fazer logon em um destino conecta o usuário a qualquer outro destino que use o mesmo canal ou canais. Se dois componentes aplicarem credenciais diferentes ao mesmo objeto ChannelSet, as últimas credenciais aplicadas serão usadas. Se vários componentes usarem o mesmo objeto ChannelSet autenticado, chamando o `logout` O método do registra todos os componentes fora dos destinos.

O exemplo a seguir usa o `ChannelSet.login` e `ChannelSet.logout` métodos com um controle RemoteObject. Este aplicativo executa as seguintes ações:

* Cria um `ChannelSet` objeto no `creationComplete` manipulador que representa os canais usados pelo `RemoteObject` componente
* Passa as credenciais para o servidor, chamando o `ROLogin` função em resposta a um evento de clique de botão
* Usa o componente RemoteObject para enviar uma String ao servidor em resposta a um evento de clique de botão. O servidor retorna a mesma Cadeia de Caracteres de volta para o componente RemoteObject
* Usa o evento result do componente RemoteObject para exibir a String em um controle TextArea
* Efetua logout do servidor, chamando o `ROLogout` função em resposta a um evento de clique de botão

```java
 <?xml version="1.0"?>
 <!-- security/SecurityConstraintCustom.mxml -->
 <mx:Application xmlns:mx="https://www.adobe.com/2006/mxml" width="100%"
     height="100%" creationComplete="creationCompleteHandler();">
 
     <mx:Script>
         <![CDATA[
             import mx.controls.Alert;
             import mx.messaging.config.ServerConfig;
             import mx.rpc.AsyncToken;
             import mx.rpc.AsyncResponder;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import mx.messaging.ChannelSet;
 
             // Define a ChannelSet object.
             public var cs:ChannelSet;
 
             // Define an AsyncToken object.
             public var token:AsyncToken;
 
             // Initialize ChannelSet object based on the
             // destination of the RemoteObject component.
             private function creationCompleteHandler():void {
                 if (cs == null)
                 cs = ServerConfig.getChannelSet(remoteObject.destination);
             }
 
             // Login and handle authentication success or failure.
             private function ROLogin():void {
                 // Make sure that the user is not already logged in.
                 if (cs.authenticated == false) {
                     token = cs.login("sampleuser", "samplepassword");
                     // Add result and fault handlers.
                     token.addResponder(new AsyncResponder(LoginResultEvent,
                     LoginFaultEvent));
                 }
             }
 
             // Handle successful login.
             private function LoginResultEvent(event:ResultEvent,
                 token:Object=null):void  {
                     switch(event.result) {
                         case "success":
                             authenticatedCB.selected = true;
                             break;
                             default:
                     }
                 }
 
                 // Handle login failure.
                 private function LoginFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         switch(event.fault.faultCode) {
                             case "Client.Authentication":
                                 default:
                                 authenticatedCB.selected = false;
                                 Alert.show("Login failure: " + event.fault.faultString);
                     }
                 }
 
                 // Logout and handle success or failure.
                 private function ROLogout():void {
                     // Add result and fault handlers.
                     token = cs.logout();
                     token.addResponder(new
                         AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
                 }
 
                 // Handle successful logout.
                 private function LogoutResultEvent(event:ResultEvent,
                     token:Object=null):void {
                         switch (event.result) {
                             case "success":
                                 authenticatedCB.selected = false;
                                 break;
                                 default:
                     }
                 }
 
                 // Handle logout failure.
                 private function LogoutFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         Alert.show("Logout failure: " + event.fault.faultString);
                 }
                 // Handle message recevied by RemoteObject component.
                 private function resultHandler(event:ResultEvent):void {
                     ta.text += "Server responded: "+ event.result + "\n";
                 }
 
                 // Handle fault from RemoteObject component.
                 private function faultHandler(event:FaultEvent):void {
                     ta.text += "Received fault: " + event.fault + "\n";
                 }
             ]]>
     </mx:Script>
     <mx:HBox>
         <mx:Label text="Enter a text for the server to echo"/>
         <mx:TextInput id="ti" text="Hello World!"/>
         <mx:Button label="Login"
             click="ROLogin();"/>
         <mx:Button label="Echo"
             enabled="{authenticatedCB.selected}"
             click="remoteObject.echo(ti.text);"/>
         <mx:Button label="Logout"
             click="ROLogout();"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
     <mx:TextArea id="ta" width="100%" height="100%"/>
 
     <mx:RemoteObject id="remoteObject"
         destination="myDest"
         result="resultHandler(event);"
         fault="faultHandler(event);"/>
 </mx:Application>
```

A variável `login` e `logout` Os métodos do retornam um objeto AsyncToken. Atribua manipuladores de eventos ao objeto AsyncToken para que o evento resultante manipule uma chamada bem-sucedida e para que o evento de falha manipule uma falha.

### Usando o logon único {#using-single-sign-on}

Os usuários de formulários AEM podem se conectar a vários aplicativos web do AEM Forms para executar uma tarefa. Conforme os usuários mudam de um aplicativo web para outro, não é eficiente exigir que façam logon separadamente em cada aplicativo web. O mecanismo de logon único do AEM Forms permite que os usuários façam logon uma vez e, em seguida, acessem qualquer aplicativo Web do AEM Forms. Como os desenvolvedores do AEM Forms podem criar aplicativos clientes para usar com o AEM Forms, eles também devem poder aproveitar o mecanismo de logon único.

Cada aplicativo da Web do AEM Forms é empacotado em seu próprio arquivo WAR (Web Archive), que é empacotado como parte de um arquivo EAR (Enterprise Archive). Como um servidor de aplicativos não permite o compartilhamento de dados da sessão em diferentes aplicativos da Web, o AEM Forms usa cookies HTTP para armazenar informações de autenticação. Os cookies de autenticação permitem que um usuário faça logon em um aplicativo do Forms e, em seguida, se conecte a outros aplicativos Web do AEM Forms. Essa técnica é conhecida como logon único.

Os desenvolvedores do AEM Forms criam aplicativos clientes para estender a funcionalidade dos Guias de formulário (obsoletos) e personalizar o Workspace. Por exemplo, um aplicativo do Workspace pode iniciar um processo. O aplicativo cliente usa um ponto de extremidade remoto para recuperar dados do serviço do Forms.

Quando um serviço do AEM Forms é chamado usando o (obsoleto para formulários AEM) AEM Forms Remoting, o aplicativo cliente passa o cookie de autenticação como parte da solicitação. Como o usuário já foi autenticado, não é necessário logon adicional para fazer uma conexão do aplicativo cliente com o serviço AEM Forms.

>[!NOTE]
>
Se um cookie for inválido ou estiver ausente, não haverá redirecionamento implícito para uma página de logon. Portanto, você ainda pode chamar um serviço anônimo.

Você pode ignorar o mecanismo de logon único do AEM Forms gravando um aplicativo cliente que faz logon e logout por conta própria. Se você ignorar o mecanismo de logon único, poderá usar a autenticação básica ou personalizada com seu aplicativo.

Como esse mecanismo não usa o mecanismo de logon único do AEM Forms, nenhum cookie de autenticação é gravado no cliente. As credenciais de logon são armazenadas na `ChannelSet` para o canal remoto. Por conseguinte, qualquer `RemoteObject` chamadas que você faz na mesma `ChannelSet` são feitas no contexto dessas credenciais.

### Configuração do logon único no AEM Forms {#setting-up-single-sign-on-in-aem-forms}

Para usar o logon único no AEM Forms, instale o componente de fluxo de trabalho de formulários, que inclui o serviço de logon centralizado. Depois que um usuário faz logon, o serviço de logon centralizado retorna um cookie de autenticação para o usuário. Cada solicitação subsequente para um aplicativo web do Forms contém o cookie. Se o cookie for válido, o usuário será considerado autenticado e não precisará fazer logon novamente.

### Gravando um aplicativo cliente que usa logon único {#writing-a-client-application-that-uses-single-sign-on}

Ao aproveitar o mecanismo de logon único, você espera que os usuários façam logon usando o serviço de logon centralizado antes de iniciar um aplicativo cliente. Ou seja, um aplicativo cliente não faz logon por meio do navegador ou chamando o `ChannelSet.login` método.

Se você estiver usando o mecanismo de logon único da AEM Forms, configure o endpoint de Comunicação Remota para usar a autenticação personalizada, não a básica. Caso contrário, ao usar a autenticação básica, um erro de autenticação causa um desafio do navegador, que você não deseja que o usuário veja. Em vez disso, o aplicativo detecta o erro de autenticação e exibe uma mensagem instruindo o usuário a fazer logon usando o serviço de logon centralizado.

Um aplicativo cliente acessa o AEM Forms por meio de um terminal remoto usando o `RemoteObject` componente, como mostra o exemplo a seguir.

```java
 <?xml version="1.0"?>
 <mx:Application
        backgroundColor="#FFFFFF">
 
       <mx:Script>
          <![CDATA[
 
            import mx.controls.Alert;
            import mx.rpc.events.FaultEvent;
 
            // Prompt user to login on a fault.
            private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
         }
          ]]>
       </mx:Script>
 
       <mx:RemoteObject id="srv"
           destination="product"
           fault="faultHandler(event);"/>
 
       <mx:DataGrid
           width="100%" height="100%"
           dataProvider="{srv.getProducts.lastResult}"/>
 
       <mx:Button label="Get Data"
           click="srv.getProducts();"/>
 
 </mx:Application>
```

**Fazer logon como um novo usuário enquanto o aplicativo Flex ainda está em execução**

Um aplicativo criado com o Flex inclui o cookie de autenticação com cada solicitação para um serviço do AEM Forms. Por motivos de desempenho, o AEM Forms não valida o cookie em cada solicitação. No entanto, o AEM Forms detecta quando um cookie de autenticação é substituído por outro cookie de autenticação.

Por exemplo, você inicia um aplicativo cliente e, enquanto o aplicativo está ativo, usa o serviço de logon centralizado para fazer logoff. Em seguida, você pode fazer logon como um usuário diferente. Fazer logon como um usuário diferente substitui o cookie de autenticação existente por um cookie de autenticação para o novo usuário.

Na próxima solicitação do aplicativo cliente do, o AEM Forms detecta que o cookie foi alterado e faz logoff do usuário. Portanto, a primeira solicitação após uma alteração de cookie falha. Todas as solicitações subsequentes são feitas no contexto do novo cookie e são bem-sucedidas.

**Efetuando logout**

Para fazer logoff do AEM Forms e invalidar uma sessão, o cookie de autenticação deve ser excluído do computador do cliente. Como a finalidade do logon único é permitir que um usuário faça logon uma vez, você não deseja que um aplicativo cliente exclua o cookie. Essa ação efetivamente faz logout do usuário.

Portanto, ao chamar a variável `RemoteObject.logout` em um aplicativo cliente gera uma mensagem de erro no cliente especificando que a sessão não foi desconectada. Em vez disso, o usuário pode usar o serviço de logon centralizado para fazer logoff e excluir o cookie de autenticação.

**Efetuando logout enquanto o aplicativo Flex ainda está em execução**

Você pode iniciar um aplicativo cliente criado com o Flex e usar o serviço de logon centralizado para fazer logoff. Como parte do processo de logout, o cookie de autenticação é excluído. Se uma solicitação de comunicação remota for feita sem um cookie ou com um cookie inválido, a sessão do usuário será invalidada. Esta ação está em efeito como logout. Na próxima vez que o aplicativo cliente tentar se conectar a um serviço AEM Forms, o usuário deverá fazer logon.

**Consulte também**

[Chamar o AEM Forms usando (obsoleto para o AEM formulários) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Lidar com documentos com (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusão do arquivo da biblioteca Flex do AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Chamar um processo de vida curta transmitindo um documento não seguro usando o AEM Forms Remoting (obsoleto para formulários AEM)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Enviar documentos seguros para invocar processos usando comunicação remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Enviar documentos seguros para invocar processos usando comunicação remota {#passing-secure-documents-to-invoke-processes-using-remoting}

Você pode passar documentos seguros para o AEM Forms ao chamar um processo que requer um ou mais documentos. Ao transmitir um documento seguro, você está protegendo as informações de negócios e os documentos confidenciais. Nessa situação, um documento pode se referir a um documento PDF, um documento XML, um documento Word e assim por diante. Passar um documento seguro para o AEM Forms a partir de um aplicativo cliente escrito no Flex é necessário quando o AEM Forms é configurado para permitir documentos seguros. (Consulte [Configuração do AEM Forms para aceitar documentos protegidos e não protegidos](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).)

Ao transmitir um documento seguro, use logon único e especifique um usuário de formulários AEM que tenha a *Usuário do aplicativo de carregamento de documento* função. Sem essa função, o usuário não pode carregar um documento seguro. Você pode atribuir uma função de maneira programática a um usuário. (Consulte [Gerenciamento de funções e permissões](/help/forms/developing/users.md#managing-roles-and-permissions).)

>[!NOTE]
>
Ao criar uma função e quiser que os membros dessa função façam upload de documentos protegidos, certifique-se de especificar a permissão Upload de documentos.

O AEM Forms oferece suporte a uma operação chamada `getFileUploadToken` que retorna um token passado para o servlet de upload. A variável `DocumentReference.constructRequestForUpload` requer um URL para o AEM Forms junto com o token retornado pelo `LC.FileUploadAuthenticator.getFileUploadToken` método. Este método retorna um valor de `URLRequest` objeto que é usado na chamada ao servlet de upload. O código a seguir demonstra essa lógica de aplicação.

```java
     ...
         private function startUpload():void
         {
             fileRef.addEventListener(Event.SELECT, selectHandler);
             fileRef.addEventListener("uploadCompleteData", completeHandler);
             try
             {
         var success:Boolean = fileRef.browse();
             }
             catch (error:Error)
             {
                 trace("Unable to browse for files.");
             }
 
         }
 
          private function selectHandler(event:Event):void
             {
             var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
             authTokenService.addEventListener("result", authTokenReceived);
             authTokenService.channelSet = cs;
             authTokenService.getFileUploadToken();
             }
 
         private function authTokenReceived(event:ResultEvent):void
             {
             var token:String = event.result as String;
             var request:URLRequest = DocumentReference.constructRequestForUpload("http://localhost:8080", token);
 
             try
             {
           fileRef.upload(request);
             }
             catch (error:Error)
             {
             trace("Unable to upload file.");
             }
             }
 
         private function completeHandler(event:DataEvent):void
         {
 
             var params:Object = new Object();
             var docRef:DocumentReference = new DocumentReference();
             docRef.url = event.data as String;
             docRef.referenceType = DocumentReference.REF_TYPE_URL;
         }
         ...
```

)

### Configuração do AEM Forms para aceitar documentos protegidos e não protegidos {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

Você pode usar o console de administração para especificar se os documentos são seguros ao passar um documento de um aplicativo cliente do Flex para um processo do AEM Forms. Por padrão, o AEM Forms é configurado para aceitar documentos seguros. Você pode configurar o AEM Forms para aceitar documentos seguros executando as seguintes etapas:

1. Faça logon no console de administração.
1. Clique em **Configurações**.
1. Clique em **Configurações principais do sistema.**
1. Clique em Configurações.
1. Certifique-se de que a opção Permitir upload de documento não seguro de aplicativos do Flex não esteja selecionada.

>[!NOTE]
>
Para configurar o AEM Forms para aceitar documentos não seguros, selecione a opção Permitir upload de documento não seguro de aplicativos do Flex. Em seguida, reinicie um aplicativo ou serviço para garantir que a configuração seja aplicada.

### Início Rápido: Invocar um processo de vida curta transmitindo um documento seguro usando Comunicação Remota {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

O código de exemplo a seguir chama a variável `MyApplication/EncryptDocument.`O usuário deve fazer logon para clicar no botão Selecionar arquivo usado para fazer upload de um arquivo PDF e chamar o processo. Ou seja, depois que o usuário é autenticado, o botão Selecionar arquivo é ativado. A ilustração a seguir mostra o aplicativo cliente do Flex depois que um usuário é autenticado. Observe que a caixa de seleção Autenticado está ativada.

![iu_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

se o AEM Forms estiver configurado para permitir que apenas documentos seguros sejam carregados e o usuário não tiver o *Usuário do aplicativo de carregamento de documento* e, em seguida, uma exceção é lançada. Se o usuário tiver essa função, o arquivo será carregado e o processo será chamado.

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  xmlns="*"
      creationComplete="initializeChannelSet();">
        <mx:Script>
        <![CDATA[
      import mx.rpc.livecycle.DocumentReference;
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.controls.Alert;
      import mx.rpc.events.FaultEvent;
      import mx.rpc.AsyncResponder;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var docRef:DocumentReference = new DocumentReference();
      private var parentResourcePath:String = "/";
      private var now1:Date;
      private var serverPort:String = "hiro-xp:8080";
 
      // Define a ChannelSet object.
      public var cs:ChannelSet;
 
      // Define an AsyncToken object.
      public var token:AsyncToken;
 
       // Holds information returned from AEM Forms
      [Bindable]
      public var progressList:ArrayCollection = new ArrayCollection();
 
 
      // Handles a successful login
     private function LoginResultEvent(event:ResultEvent,
         token:Object=null):void  {
             switch(event.result) {
                 case "success":
                     authenticatedCB.selected = true;
                     btnFile.enabled = true;
                     btnLogout.enabled = true;
                     btnLogin.enabled = false;
                         break;
                     default:
                 }
             }
 
 
 // Handle login failure.
 private function LoginFaultEvent(event:FaultEvent,
     token:Object=null):void {
     switch(event.fault.faultCode) {
                 case "Client.Authentication":
                         default:
                         authenticatedCB.selected = false;
                         Alert.show("Login failure: " + event.fault.faultString);
                 }
             }
 
 
      // Set up channel set to invoke AEM Forms
      private function initializeChannelSet():void {
        cs = new ChannelSet();
        cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
        EncryptDocument2.channelSet = cs;
      }
 
     // Call this method to upload the file.
      // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process.
      private function uploadFile():void {
        fileRef.addEventListener(Event.SELECT, selectHandler);
        fileRef.addEventListener(DataEvent.UPLOAD_COMPLETE_DATA,completeHandler);
        fileRef.browse();
      }
 
      // Gets called for selected file. Does the actual upload via the file upload servlet.
      private function selectHandler(event:Event):void {
              var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
         authTokenService.addEventListener("result", authTokenReceived);
         authTokenService.channelSet = cs;
         authTokenService.getFileUploadToken();
      }
 
     private function authTokenReceived(event:ResultEvent):void
     {
     var token:String = event.result as String;
     var request:URLRequest = DocumentReference.constructRequestForUpload("https://hiro-xp:8080", token);
 
     try
     {
           fileRef.upload(request);
     }
     catch (error:Error)
     {
         trace("Unable to upload file.");
     }
 }
 
      // Called once the file is completely uploaded.
      private function completeHandler(event:DataEvent):void {
 
        // Set the docRef's url and referenceType parameters
        docRef.url = event.data as String;
        docRef.referenceType=DocumentReference.REF_TYPE_URL;
        executeInvokeProcess();
      }
 
     //This method invokes the EncryptDocument process
      public function executeInvokeProcess():void {
         //Create an Object to store the input value for the EncryptDocument process
           now1 = new Date();
 
         var params:Object = new Object();
         params["inDoc"]=docRef;
 
         // Invoke the EncryptDocument process
         var token:AsyncToken;
         token = EncryptDocument2.invoke(params);
         token.name = name;
      }
 
      // AEM Forms  login method
      private function ROLogin():void {
         // Make sure that the user is not already logged in.
 
         //Get the User and Password
         var userName:String = txtUser.text;
         var pass:String = txtPassword.text;
 
        if (cs.authenticated == false) {
             token = cs.login(userName, pass);
 
         // Add result and fault handlers.
         token.addResponder(new AsyncResponder(LoginResultEvent,    LoginFaultEvent));
                 }
             }
 
      // This method handles a successful process invocation
      public function handleResult(event:ResultEvent):void
      {
            //Retrieve information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var dr:DocumentReference = res["outDoc"] as DocumentReference;
          var now2:Date = new Date();
 
           // These fields map to columns in the DataGrid
          var progObject:Object = new Object();
          progObject.filename = token.name;
          progObject.timing = (now2.time - now1.time).toString();
          progObject.state = "Success";
          progObject.link = "<a href='" + dr.url + "'> open </a>";
          progressList.addItem(progObject);
      }
 
      // Prompt user to login on a fault.
       private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
            }
 
       // AEM Forms  logout method
     private function ROLogout():void {
         // Add result and fault handlers.
         token = cs.logout();
         token.addResponder(new AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
     }
 
     // Handle successful logout.
     private function LogoutResultEvent(event:ResultEvent,
         token:Object=null):void {
         switch (event.result) {
         case "success":
                 authenticatedCB.selected = false;
                 btnFile.enabled = false;
                 btnLogout.enabled = false;
                 btnLogin.enabled = true;
                 break;
                 default:
             }
     }
 
     // Handle logout failure.
     private function LogoutFaultEvent(event:FaultEvent,
             token:Object=null):void {
             Alert.show("Logout failure: " + event.fault.faultString);
     }
 
          private function resultHandler(event:ResultEvent):void {
          // Do anything else here.
          }
        ]]>
 
      </mx:Script>
      <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleResult(event)"/>
      </mx:RemoteObject>
 
       <!--//This consists of what is displayed on the webpage-->
      <mx:Panel id="lcPanel" title="EncryptDocument  (Deprecated for AEM forms) AEM Forms Remoting Example"
           height="25%" width="25%" paddingTop="10" paddingLeft="10" paddingRight="10"
           paddingBottom="10">
         <mx:Label width="100%" color="blue"
                text="Select a PDF file to pass to the EncryptDocument process"/>
        <mx:DataGrid x="10" y="0" width="500" id="idProgress" editable="false"
           dataProvider="{progressList}" height="231" selectable="false" >
          <mx:columns>
            <mx:DataGridColumn headerText="Filename" width="200" dataField="filename" editable="false"/>
            <mx:DataGridColumn headerText="State" width="75" dataField="state" editable="false"/>
            <mx:DataGridColumn headerText="Timing" width="75" dataField="timing" editable="false"/>
            <mx:DataGridColumn headerText="Click to Open" dataField="link" editable="false" >
             <mx:itemRenderer>
                <mx:Component>
                   <mx:Text x="0" y="0" width="100%" htmlText="{data.link}"/>
                </mx:Component>
             </mx:itemRenderer>
            </mx:DataGridColumn>
          </mx:columns>
        </mx:DataGrid>
        <mx:Button label="Select File" click="uploadFile()"  id="btnFile" enabled="false"/>
        <mx:Button label="Login" click="ROLogin();" id="btnLogin"/>
        <mx:Button label="LogOut" click="ROLogout();" enabled="false" id="btnLogout"/>
        <mx:HBox>
         <mx:Label text="User:"/>
         <mx:TextInput id="txtUser" text=""/>
         <mx:Label text="Password:"/>
         <mx:TextInput id="txtPassword" text="" displayAsPassword="true"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
      </mx:Panel>
 </mx:Application>
```

**Consulte também**

[Chamar o AEM Forms usando (obsoleto para o AEM formulários) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Lidar com documentos com (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusão do arquivo da biblioteca Flex do AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Chamar um processo de vida curta transmitindo um documento não seguro usando o AEM Forms Remoting (obsoleto para formulários AEM)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticação de aplicativos clientes criados com o Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Chamar serviços de componente personalizado usando Comunicação Remota {#invoking-custom-component-services-using-remoting}

Você pode chamar serviços em um componente personalizado usando Comunicação Remota. Por exemplo, considere o componente Banco que contém o Serviço ao cliente. Você pode invocar operações que pertencem ao Serviço de atendimento ao cliente usando um aplicativo de cliente escrito em Flex. Antes de executar o início rápido associado a esta seção, é necessário criar o componente personalizado Bank.

O Serviço de atendimento ao cliente expõe uma operação chamada `createCustomer`. Esta discussão descreve como criar um aplicativo de cliente do Flex que chama o Serviço de atendimento ao cliente e cria um cliente. Esta operação requer um objeto complexo de tipo `com.adobe.livecycle.sample.customer.Customer` que representa o novo cliente. A ilustração a seguir mostra o aplicativo cliente que chama o Serviço de atendimento ao cliente e cria um novo cliente. A variável `createCustomer` a operação retorna um valor de identificador do cliente. O valor do identificador é exibido na caixa de texto Identificador do cliente.

![iu_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

A tabela a seguir lista os controles que fazem parte deste aplicativo cliente.

<table>
 <thead>
  <tr>
   <th><p>Nome do controle</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>txtFirst</p></td>
   <td><p>Especifica o nome do cliente. </p></td>
  </tr>
  <tr>
   <td><p>txtLast</p></td>
   <td><p>Especifica o sobrenome do cliente. </p></td>
  </tr>
  <tr>
   <td><p>txtPhone</p></td>
   <td><p>Especifica o número de telefone do cliente.</p></td>
  </tr>
  <tr>
   <td><p>txtStreet</p></td>
   <td><p>Especifica o nome da rua do cliente.</p></td>
  </tr>
  <tr>
   <td><p>txtState</p></td>
   <td><p>Especifica o estado do cliente. </p></td>
  </tr>
  <tr>
   <td><p>txtZIP</p></td>
   <td><p>Especifica o CEP do cliente. </p></td>
  </tr>
  <tr>
   <td><p>txtCity</p></td>
   <td><p>Especifica a cidade do cliente.</p></td>
  </tr>
  <tr>
   <td><p>txtCustId</p></td>
   <td><p>Especifica o valor do identificador do cliente ao qual a nova conta pertence. Esta caixa de texto é preenchida pelo valor de retorno do campo <code>createCustomer</code> operação. </p></td>
  </tr>
 </tbody>
</table>

### Mapeamento de tipos de dados complexos do AEM Forms {#mapping-aem-forms-complex-data-types}

Algumas operações do AEM Forms exigem tipos de dados complexos como valores de entrada. Esses tipos de dados complexos definem valores de tempo de execução usados pela operação. Por exemplo, o campo do Serviço de clientes `createCustomer` a operação requer um `Customer` instância que contém valores de tempo de execução exigidos pelo serviço. Sem o tipo complexo, o atendimento ao cliente lança uma exceção e não executa a operação.

Ao chamar um serviço do AEM Forms, crie objetos do ActionScript que mapeiam para os tipos complexos necessários do AEM Forms. Para cada tipo de dados complexo exigido por uma operação, crie um objeto de ActionScript separado.

Na classe ActionScript, use o `RemoteClass` tag de metadados para mapear para o tipo complexo AEM Forms. Por exemplo, ao invocar a função do Serviço de atendimento ao cliente `createCustomer` criar uma classe de ActionScript que mapeie para `com.adobe.livecycle.sample.customer.Customer` tipo de dados.

A seguinte classe de ActionScript chamada Cliente mostra como mapear para o tipo de dados AEM Forms `com.adobe.livecycle.sample.customer.Customer`.

```java
 package customer
 
 {
     [RemoteClass(alias="com.adobe.livecycle.sample.customer.Customer")]
     public class Customer
     {
            public var name:String;
            public var street:String;
            public var city:String;
            public var state:String;
            public var phone:String;
            public var zip:int;
        }
 }
```

O tipo de dados totalmente qualificado do tipo complexo AEM Forms é atribuído à tag alias.

Os campos da classe ActionScript correspondem aos campos que pertencem ao tipo complexo AEM Forms. Os seis campos na classe de ActionScript do cliente correspondem aos campos aos quais pertence `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
>
Uma boa maneira de determinar os nomes de campo que pertencem a um tipo complexo do Forms é exibir o WSDL de um serviço em um navegador da Web. Um WSDL especifica os tipos complexos de um serviço e os membros de dados correspondentes. O seguinte WSDL é usado para o serviço de atendimento ao cliente: `https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

A classe de ActionScript Cliente pertence a um pacote chamado cliente. É recomendável colocar todas as classes de ActionScript que mapeiam para tipos de dados complexos do AEM Forms em seu próprio pacote. Crie uma pasta na pasta src do projeto Flex e coloque o arquivo ActionScript na pasta, conforme mostrado na ilustração a seguir.

![iu_iu_customeras](assets/iu_iu_customeras.png)

### Início Rápido: Chamar o serviço personalizado do Cliente usando Comunicação Remota {#quick-start-invoking-the-customer-custom-service-using-remoting}

O código de exemplo a seguir chama o Serviço de clientes e cria um cliente. Ao executar esse exemplo de código, preencha todas as caixas de texto. Além disso, crie o arquivo Customer.as que mapeia para `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
>
Antes de executar este início rápido, é necessário criar e implantar o componente personalizado do Bank.

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  layout="absolute" backgroundColor="#B1ABAB">
 
 <mx:Script>
            <![CDATA[
 
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.managers.CursorManager;
      import mx.rpc.remoting.mxml.RemoteObject;
 
 
      // Custom class that corresponds to an input to the
      // AEM Forms encryption method
      import customer.Customer;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var parentResourcePath:String = "/";
      private var serverPort:String = "hiro-xp:8080";
      private var now1:Date;
      private var fileName:String;
 
      // Prepares parameters for encryptPDFUsingPassword method call
      public function executeCreateCustomer():void
      {
 
        var cs:ChannelSet= new ChannelSet();
     cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
 
     customerService.setCredentials("administrator", "password");
     customerService.channelSet = cs;
 
     //Create a Customer object required to invoke the Customer service's
     //createCustomer operation
     var myCust:Customer = new Customer();
 
     //Get values from the user of the Flex application
     var fullName:String = txtFirst.text +" "+txtLast.text ;
     var Phone:String = txtPhone.text;
     var Street:String = txtStreet.text;
     var State:String = txtState.text;
     var Zip:int = parseInt(txtZIP.text);
     var City:String = txtCity.text;
 
     //Populate Customer fields
     myCust.name = fullName;
     myCust.phone = Phone;
     myCust.street= Street;
     myCust.state= State;
     myCust.zip = Zip;
     myCust.city = City;
 
     //Invoke the Customer service's createCustomer operation
     var params:Object = new Object();
        params["inCustomer"]=myCust;
     var token:AsyncToken;
        token = customerService.createCustomer(params);
        token.name = name;
      }
 
      private function handleResult(event:ResultEvent):void
      {
          // Retrieve the information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var custId:String = res["CustomerId"] as String;
 
          //Assign to the custId to the text box
          txtCustId.text = custId;
      }
 
 
      private function resultHandler(event:ResultEvent):void
      {
 
      }
            ]]>
 </mx:Script>
 <mx:RemoteObject id="customerService" destination="CustomerService" result="resultHandler(event);">
 <mx:method name="createCustomer" result="handleResult(event)"/>
 </mx:RemoteObject>
 
 
 <mx:Style source="../bank.css"/>
     <mx:Grid>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="New Customer" fontSize="16" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="First Name:" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtFirst"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:Button label="Create Customer" id="btnCreateCustomer" click="executeCreateCustomer()"/>
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Last Name" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtLast"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Phone" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtPhone"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Street" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtStreet"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="State" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtState"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="ZIP" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtZIP"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="City" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCity"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                             <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Customer Identifier" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCustId" editable="false"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                 </mx:Grid>
 </mx:Application>
 
```

**Folha de estilo**

Este início rápido contém uma folha de estilos chamada *bank.css*. O código a seguir representa a folha de estilos usada.

```css
 /* CSS file */
 global
 {
          backgroundGradientAlphas: 1.0, 1.0;
          backgroundGradientColors: #525152,#525152;
          borderColor: #424444;
          verticalAlign: middle;
          color: #FFFFFF;
          font-size:12;
          font-weight:normal;
 }
 
 ApplicationControlBar
 {
          fillAlphas: 1.0, 1.0;
          fillColors: #393839, #393839;
 }
 
 .textField
 {
          backgroundColor: #393839;
          background-disabled-color: #636563;
 }
 
 
 .button
 {
          fillColors: #636563, #424242;
 }
 
 .dropdownMenu
 {
          backgroundColor: #DDDDDD;
          fillColors: #636563, #393839;
          alternatingItemColors: #888888, #999999;
 }
 
 .questionLabel
 {
 
 }
 
 ToolTip
 {
        backgroundColor: black;
        backgroundAlpha: 1.0;
        cornerRadius: 0;
        color: white;
 }
 
 DateChooser
 {
        cornerRadius: 0; /* pixels */
        headerColors: black, black;
        borderColor: black;
        themeColor: black;
        todayColor: red;
        todayStyleName: myTodayStyleName;
        headerStyleName: myHeaderStyleName;
        weekDayStyleName: myWeekDayStyleName;
        dropShadowEnabled: true;
 }
 
 .myTodayStyleName
 {
        color: white;
 }
 
 .myWeekDayStyleName
 {
        fontWeight: normal;
 }
 
 .myHeaderStyleName
 {
        color: red;
        fontSize: 16;
        fontWeight: bold;
 }
```

**Consulte também**

[Chamar o AEM Forms usando (obsoleto para o AEM formulários) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Lidar com documentos com (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusão do arquivo da biblioteca Flex do AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Chamar um processo de vida curta transmitindo um documento não seguro usando o AEM Forms Remoting (obsoleto para formulários AEM)](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticação de aplicativos clientes criados com o Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Enviar documentos seguros para invocar processos usando comunicação remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
