---
title: Invocar o AEM Forms usando o recurso Remoting
seo-title: Invocar o AEM Forms usando o recurso Remoting
description: Use o recurso Remoto para chamar um processo AEM Forms para chamar os processos criados no Workbench. Você pode invocar um processo AEM Forms de um aplicativo cliente criado com o Flex.
seo-description: Use o recurso Remoto para chamar um processo AEM Forms para chamar os processos criados no Workbench. Você pode invocar um processo AEM Forms de um aplicativo cliente criado com o Flex.
uuid: 592d1519-c38b-4b33-8cf3-61e2bff81501
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 3d8bb2d3-b1f8-49e1-a529-b3e7a28da4bb
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '4647'
ht-degree: 0%

---


# Invocando o AEM Forms usando a opção Remoting {#invoking-aem-forms-using-remoting}

Os processos criados no Workbench podem ser chamados usando o Remoting. Ou seja, você pode invocar um processo AEM Forms de um aplicativo cliente criado com a Flex. Esse recurso tem por base os Serviços de dados.

>[!NOTE]
>
>Ao usar o Remoting, é recomendável chamar os processos criados no Workbench em vez dos serviços da AEM Forms. No entanto, é possível chamar diretamente os serviços da AEM Forms. (Consulte Criptografar documentos PDF usando a opção Remota localizada no Centro de desenvolvedores AEM Forms.)

>[!NOTE]
>
>Se um serviço AEM Forms não estiver configurado para permitir acesso anônimo, as solicitações de um cliente Flex resultarão em um desafio de navegador da Web. O usuário deve digitar as credenciais de nome de usuário e senha.

O seguinte processo AEM Forms de curta duração, chamado `MyApplication/EncryptDocument`, pode ser chamado usando o Remoting. (Para obter informações sobre esse processo, como seus valores de entrada e saída, consulte [Exemplo de processo de duração curta](/help/forms/developing/aem-forms-processes.md).)

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>Para chamar um processo AEM Forms usando um aplicativo Flex, verifique se um terminal remoto está ativado. Por padrão, um terminal remoto é ativado ao implantar um processo.

Quando esse processo é chamado, ele executa as seguintes ações:

1. Obtém o documento PDF não protegido que é transmitido como um valor de entrada. Esta ação se baseia na operação `SetValue`. O nome do parâmetro de entrada é `inDoc` e seu tipo de dados é `document`. (O tipo de dados `document` é um tipo de dados disponível no Workbench.)
1. Criptografa o documento PDF com uma senha. Esta ação se baseia na operação `PasswordEncryptPDF`. O nome do valor de saída desse processo é `outDoc` e representa o documento PDF criptografado por senha. O tipo de dados de outDoc é `document`.
1. Salva o documento PDF criptografado por senha como um arquivo PDF no sistema de arquivos local. Esta ação se baseia na operação `WriteDocument`.

>[!NOTE]
>
>O processo `MyApplication/EncryptDocument` não se baseia em um processo AEM Forms existente. Para seguir junto com os exemplos de código, crie um processo chamado `MyApplication/EncryptDocument` usando o Workbench.

>[!NOTE]
>
>Para obter informações sobre como usar o recurso Remoto para invocar um processo de longa duração, consulte [Invocando processos de longa vida centrados em humanos](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

**Consulte também:**

[Incluindo o arquivo da biblioteca do AEM Forms Flex](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Tratamento de documentos com (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Invocar um processo de duração curta transmitindo um documento não seguro usando (obsoleto para formulários AEM) o AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticação de aplicativos cliente criados com a Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Transmissão de documentos protegidos para chamar processos usando Remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[Invocar serviços de componentes personalizados usando Remota](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[Criação de um aplicativo cliente criado com a Flex que invoca um processo de longa duração centrado no ser humano](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[Criação de aplicativos de Flash Builder que executam autenticação SSO usando tokens HTTP](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

Para obter informações sobre como exibir dados de processo em um controle de gráfico do Flex, consulte [Exibição de dados de processo do AEM Forms em gráficos do Flex](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html).

>[!NOTE]
>
>*Certifique-se de colocar o arquivo crossdomain.xml no local apropriado. Por exemplo, assumindo que você implantou o AEM Forms em JBoss, coloque esse arquivo no seguinte local: &lt;install_diretory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war.*

## Incluindo o arquivo da biblioteca do AEM Forms Flex {#including-the-aem-forms-flex-library-file}

Para chamar de forma programática os processos do AEM Forms usando o Remoting, adicione o arquivo adobe-remoting-provider.swc ao caminho de classe do seu projeto Flex. Esse arquivo SWC está localizado no seguinte local:

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   onde &lt;*install_diretory*> é o diretório onde o AEM Forms está instalado.

**Consulte também:**

[Invocar o AEM Forms usando (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Tratamento de documentos com (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Invocar um processo de duração curta transmitindo um documento não seguro usando (obsoleto para formulários AEM) o AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticação de aplicativos cliente criados com a Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Manuseio de documentos com Remoting {#handling-documents-with-remoting}

Um dos mais importantes tipos Java não primitivos usados no AEM Forms é a classe `com.adobe.idp.Document`. Um documento geralmente é necessário para chamar uma operação do AEM Forms. É principalmente um documento PDF, mas pode conter outros tipos de documentos, como SWF, HTML, XML ou um arquivo DOC. (Consulte [Passar dados para os serviços da AEM Forms usando a API do Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Um aplicativo cliente criado com a Flex não pode solicitar diretamente um documento. Por exemplo, não é possível iniciar o Adobe Reader para solicitar um URL que produza um arquivo PDF. As solicitações para tipos de documentos, como documentos PDF e Microsoft Word, retornam um resultado que é um URL. É responsabilidade do cliente exibir o conteúdo do URL. O serviço Gerenciamento de Documentos ajuda a gerar as informações de URL e tipo de conteúdo. As solicitações de documentos XML retornam o documento XML completo no resultado.

### Passar um documento como um parâmetro de entrada {#passing-a-document-as-an-input-parameter}

Um aplicativo cliente criado com o Flex não pode enviar um documento diretamente para um processo AEM Forms. Em vez disso, o aplicativo cliente usa uma instância da classe de ActionScript `mx.rpc.livecycle.DocumentReference` para passar os parâmetros de entrada para uma operação que espera uma instância `com.adobe.idp.Document`. Um aplicativo cliente Flex tem várias opções para configurar um objeto `DocumentReference`:

* Quando o documento estiver no servidor e seu local de arquivo for conhecido, defina a propriedade referenceType do objeto DocumentReference como REF_TYPE_FILE. Defina a propriedade fileRef para o local do arquivo, como mostra o exemplo a seguir:

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* Quando o documento estiver no servidor e você souber seu URL, defina a propriedade referenceType do objeto DocumentReference como REF_TYPE_URL. Defina a propriedade url como URL, como mostra o exemplo a seguir:

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* Para criar um objeto DocumentReference a partir de uma string de texto no aplicativo cliente, defina a propriedade referenceType do objeto DocumentReference como REF_TYPE_INLINE. Defina a propriedade text como o texto a ser incluído no objeto, como mostra o exemplo a seguir:

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server’s default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* Quando o documento não estiver no servidor, use o servlet de upload Remoto para fazer upload de um documento para a AEM Forms. A novidade no AEM Forms é a capacidade de carregar documentos protegidos. Ao fazer upload de um documento seguro, é necessário usar um usuário que tenha a função *Carregar usuário do aplicativo de Documento*. Sem essa função, o usuário não pode carregar um documento seguro. É recomendável usar logon único para fazer upload de um documento seguro. (Consulte [Passando documentos protegidos para chamar processos usando Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).)

>[!NOTE]
se a AEM Forms estiver configurada para permitir o carregamento de documentos não protegidos, você poderá usar um usuário que não tenha a função de Carregar Documento Usuário do Aplicativo para fazer upload de um documento. Um usuário também pode ter a permissão de Upload de Documento. No entanto, se a AEM Forms estiver configurada para permitir apenas documentos protegidos, verifique se o usuário tem a função Usuário do aplicativo de upload de Documento ou a permissão de Upload de Documento. (Consulte [Configurar a AEM Forms para aceitar documentos seguros e não protegidos](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).

Use os recursos padrão de upload de Flashes para o URL de upload designado: `https://SERVER:PORT/remoting/lcfileupload`. Você pode usar o objeto `DocumentReference` sempre que for esperado um parâmetro de entrada do tipo `Document`
` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`O Start Remoting Quick usa o servlet de upload Remoting para enviar um arquivo PDF ao processo `MyApplication/EncryptDocument`. (Consulte [Invocar um processo de duração curta transmitindo um documento não seguro usando (Obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

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

O Start Remoting Quick usa o servlet Remoting upload para enviar um arquivo PDF para o processo `MyApplication/EncryptDocument`. (Consulte [Invocar um processo de duração curta transmitindo um documento não seguro usando (Obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

### Repassar um documento para um aplicativo cliente {#passing-a-document-back-to-a-client-application}

Um aplicativo cliente recebe um objeto do tipo `mx.rpc.livecycle.DocumentReference` para uma operação de serviço que retorna uma instância `com.adobe.idp.Document` como um parâmetro de saída. Como um aplicativo cliente lida com objetos de ActionScript e não com Java, você não pode repassar um objeto de Documento baseado em Java para um cliente Flex. Em vez disso, o servidor gera um URL para o documento e repassa o URL para o cliente. A propriedade `DocumentReference` do objeto `referenceType` especifica se o conteúdo está no objeto `DocumentReference` ou deve ser recuperado de um URL na propriedade `DocumentReference.url`. A propriedade `DocumentReference.contentType` especifica o tipo de documento.

**Consulte também:**

[Invocar o AEM Forms usando (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Incluindo o arquivo da biblioteca do AEM Forms Flex](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Invocar um processo de duração curta transmitindo um documento não seguro usando (obsoleto para formulários AEM) o AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticação de aplicativos cliente criados com a Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Transmissão de documentos protegidos para chamar processos usando Remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Invocando um processo de duração curta transmitindo um documento inseguro usando Remoting {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

Para invocar um processo AEM Forms de um aplicativo criado com o Flex, execute as seguintes tarefas:

1. Crie uma instância `mx:RemoteObject`.
1. Crie uma instância `ChannelSet`.
1. Passe os valores de entrada necessários.
1. Tratar valores de retorno.

>[!NOTE]
Esta seção discute como invocar um processo do AEM Forms e fazer upload de um documento quando o AEM Forms estiver configurado para fazer upload de documentos não protegidos. Para obter informações sobre como chamar processos da AEM Forms e fazer upload de documentos protegidos e como configurar a AEM Forms para aceitar documentos seguros e não protegidos, consulte [Passando documentos protegidos para chamar processos usando Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).

**Criação de uma instância mx:RemoteObject**

Você cria uma instância `mx:RemoteObject` para chamar um processo AEM Forms criado no Workbench. Para criar uma instância `mx:RemoteObject`, especifique os seguintes valores:

* **id:** O nome da  `mx:RemoteObject` instância que representa o processo a ser chamado.
* **destino:** O nome do processo AEM Forms a ser chamado. Por exemplo, para chamar o processo `MyApplication/EncryptDocument`, especifique `MyApplication/EncryptDocument`.
* **resultado:** o nome do método Flex que manipula o resultado.

Na tag `mx:RemoteObject`, especifique uma tag `<mx:method>` que especifique o nome do método de invocação do processo. Normalmente, o nome de um método de invocação do Forms é `invoke`.

O exemplo de código a seguir cria uma instância `mx:RemoteObject` que chama o processo `MyApplication/EncryptDocument`.

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**Criar um Canal para o AEM Forms**

Um aplicativo cliente pode chamar o AEM Forms especificando um Canal em MXML ou ActionScript, como mostra o exemplo de ActionScript a seguir. O Canal deve ser `AMFChannel`, `SecureAMFChannel`, `HTTPChannel` ou `SecureHTTPChannel`.

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

Atribua a instância `ChannelSet` ao campo `mx:RemoteObject` da instância `channelSet` (conforme mostrado no exemplo de código anterior). Geralmente, você importa a classe do canal em uma declaração de importação em vez de especificar o nome totalmente qualificado ao chamar o método `ChannelSet.addChannel`.

**Passar valores de entrada**

Um processo criado no Workbench pode usar zero ou mais parâmetros de entrada e retornar um valor de saída. Um aplicativo cliente passa os parâmetros de entrada dentro de um objeto `ActionScript` com campos que correspondem aos parâmetros que pertencem ao processo AEM Forms. O processo de duração curta, chamado `MyApplication/EncryptDocument`, requer um parâmetro de entrada chamado `inDoc`. O nome da operação exposto pelo processo é `invoke` (o nome padrão para um processo de duração curta). (Consulte [Invocar o AEM Forms usando (Obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

O exemplo de código a seguir transmite um documento PDF para o processo `MyApplication/EncryptDocument`:

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

Neste exemplo de código, `pdfDocument` é uma instância `DocumentReference` que contém um documento PDF não protegido. Para obter informações sobre um `DocumentReference`, consulte [Manuseio de documentos com (Obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting).

**Invocar uma versão específica de um serviço**

Você pode invocar uma versão específica de um serviço Forms usando um parâmetro `_version` no mapa de parâmetros da invocação. Por exemplo, para invocar a versão 1.2 do serviço `MyApplication/EncryptDocument`:

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

O parâmetro `version` deve ser uma string contendo um único ponto. Os valores à esquerda, versão principal e versão secundária à direita do período devem ser inteiros. Se esse parâmetro não for especificado, a versão ativa do cabeçalho será chamada.

**Tratamento de valores de retorno**

Os parâmetros de saída do processo AEM Forms são desserializados em objetos de ActionScript dos quais o aplicativo cliente extrai parâmetros específicos por nome, como mostra o exemplo a seguir. (O valor de saída do processo `MyApplication/EncryptDocument` é nomeado `outDoc`.)

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**Invocando o processo MyApplication/EncryptDocument**

Você pode invocar o processo `MyApplication/EncryptDocument` executando as seguintes etapas:

1. Crie uma instância `mx:RemoteObject` por meio de ActionScript ou MXML. Consulte Criação de uma instância mx:RemoteObject.
1. Configure uma instância `ChannelSet` para se comunicar com o AEM Forms e associe-a à instância `mx:RemoteObject`. Consulte Criar um Canal para a AEM Forms.
1. Chame o método `login` do ChannelSet ou o método `setCredentials` do serviço para especificar o valor e a senha do identificador do usuário. (Consulte [Usando logon único](invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. Preencha uma instância `mx.rpc.livecycle.DocumentReference` com um documento PDF não protegido para passar para o processo `MyApplication/EncryptDocument`. (Consulte [Passar um documento como um parâmetro de entrada](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter).)
1. Criptografe o documento PDF chamando o método `mx:RemoteObject` da instância `invoke`. Passe o `Object` que contém o parâmetro de entrada (que é o documento PDF não protegido). Consulte Passando valores de entrada.
1. Recupere o documento PDF criptografado por senha que é retornado do processo. Consulte Tratamento de valores de retorno.

[Start rápido: Invocar um processo de duração curta transmitindo um documento não seguro usando (obsoleto para formulários AEM) o AEM Forms Remoting](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## Autenticação de aplicativos cliente criados com o Flex {#authenticating-client-applications-built-with-flex}

Há várias maneiras de AEM o Gerenciador de usuários de formulários poder autenticar uma solicitação de Remoto de um aplicativo Flex, incluindo logon único do AEM Forms por meio do serviço de logon central, autenticação básica e autenticação personalizada. Quando nem o logon único nem o acesso anônimo estiverem ativados, uma solicitação de Remotagem resultará em autenticação básica (o padrão) ou autenticação personalizada.

A autenticação básica depende da autenticação básica J2EE padrão do container da aplicação Web. Para autenticação básica, um erro HTTP 401 causa um desafio no navegador. Isso significa que quando você tenta se conectar a um aplicativo Forms usando o RemoteObject e ainda não se conectou do aplicativo Flex, o navegador solicita um nome de usuário e uma senha.

Para autenticação personalizada, o servidor envia uma falha ao cliente para indicar que a autenticação é necessária.

>[!NOTE]
Para obter informações sobre como executar a autenticação usando tokens HTTP, consulte [Criar aplicativos de Flash Builder que executam a autenticação SSO usando tokens HTTP](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens).

### Usando autenticação personalizada {#using-custom-authentication}

Você habilita a autenticação personalizada no console de administração alterando o método de autenticação de Básico para Personalizado no terminal remoto. Se você usar a autenticação personalizada, seu aplicativo cliente chamará o método `ChannelSet.login` para fazer logon e o método `ChannelSet.logout` para fazer logoff.

>[!NOTE]
Na versão anterior do AEM Forms, você enviou credenciais para um destino chamando o método `RemoteObject.setCredentials`. Na verdade, o método `setCredentials` não passou as credenciais para o servidor até a primeira tentativa do componente de se conectar ao servidor. Portanto, se o componente emitiu um evento de falha, você não pode ter certeza se a falha ocorreu devido a um erro de autenticação ou por outro motivo. O método `ChannelSet.login` se conecta ao servidor quando você o chama para que você possa lidar com um problema de autenticação imediatamente. Embora você possa continuar a usar o método `setCredentials`, recomenda-se usar o método `ChannelSet.login`.

Como vários destinos podem usar os mesmos canais e o objeto ChannelSet correspondente, fazer logon em um destino faz logon do usuário em qualquer outro destino que use o mesmo canal ou canais. Se dois componentes aplicarem credenciais diferentes ao mesmo objeto ChannelSet, as últimas credenciais aplicadas serão usadas. Se vários componentes usarem o mesmo objeto ChannelSet autenticado, chamar o método `logout` fará o logout de todos os componentes dos destinos.

O exemplo a seguir usa os métodos `ChannelSet.login` e `ChannelSet.logout` com um controle RemoteObject. Este aplicativo executa as seguintes ações:

* Cria um objeto `ChannelSet` no manipulador `creationComplete` que representa os canais usados pelo componente `RemoteObject`
* Passa as credenciais para o servidor chamando a função `ROLogin` em resposta a um evento de clique do botão
* Usa o componente RemoteObject para enviar uma String para o servidor em resposta a um evento de clique do botão. O servidor retorna a mesma String de volta ao componente RemoteObject
* Usa o evento resultante do componente RemoteObject para exibir a String em um controle TextArea
* Faz logout do servidor chamando a função `ROLogout` em resposta a um evento de clique do botão

```java
 <?xml version=”1.0”?>
 <!-- security/SecurityConstraintCustom.mxml -->
 <mx:Application xmlns:mx=”https://www.adobe.com/2006/mxml” width=”100%”
     height=”100%” creationComplete=”creationCompleteHandler();”>
 
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
                     token = cs.login(“sampleuser”, “samplepassword”);
                     // Add result and fault handlers.
                     token.addResponder(new AsyncResponder(LoginResultEvent,
                     LoginFaultEvent));
                 }
             }
 
             // Handle successful login.
             private function LoginResultEvent(event:ResultEvent,
                 token:Object=null):void  {
                     switch(event.result) {
                         case “success”:
                             authenticatedCB.selected = true;
                             break;
                             default:
                     }
                 }
 
                 // Handle login failure.
                 private function LoginFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         switch(event.fault.faultCode) {
                             case “Client.Authentication”:
                                 default:
                                 authenticatedCB.selected = false;
                                 Alert.show(“Login failure: “ + event.fault.faultString);
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
                             case “success”:
                                 authenticatedCB.selected = false;
                                 break;
                                 default:
                     }
                 }
 
                 // Handle logout failure.
                 private function LogoutFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         Alert.show(“Logout failure: “ + event.fault.faultString);
                 }
                 // Handle message recevied by RemoteObject component.
                 private function resultHandler(event:ResultEvent):void {
                     ta.text += “Server responded: “+ event.result + “\n”;
                 }
 
                 // Handle fault from RemoteObject component.
                 private function faultHandler(event:FaultEvent):void {
                     ta.text += “Received fault: “ + event.fault + “\n”;
                 }
             ]]>
     </mx:Script>
     <mx:HBox>
         <mx:Label text=”Enter a text for the server to echo”/>
         <mx:TextInput id=”ti” text=”Hello World!”/>
         <mx:Button label=”Login”
             click=”ROLogin();”/>
         <mx:Button label=”Echo”
             enabled=”{authenticatedCB.selected}”
             click=”remoteObject.echo(ti.text);”/>
         <mx:Button label=”Logout”
             click=”ROLogout();”/>
         <mx:CheckBox id=”authenticatedCB”
             label=”Authenticated?”
             enabled=”false”/>
     </mx:HBox>
     <mx:TextArea id=”ta” width=”100%” height=”100%”/>
 
     <mx:RemoteObject id=”remoteObject”
         destination=”myDest”
         result=”resultHandler(event);”
         fault=”faultHandler(event);”/>
 </mx:Application>
```

Os métodos `login` e `logout` retornam um objeto AsyncToken. Atribua manipuladores de evento ao objeto AsyncToken para que o evento resultante manipule uma chamada bem-sucedida e para que o evento de falha gerencie uma falha.

### Usando logon único {#using-single-sign-on}

AEM formulários os usuários podem se conectar a vários aplicativos da Web AEM Forms para executar uma tarefa. À medida que os usuários mudam de um aplicativo da Web para outro, não é eficiente exigir que eles façam logon separadamente em cada aplicativo da Web. O mecanismo de logon único da AEM Forms permite que os usuários façam logon uma vez e acessem qualquer aplicativo da Web da AEM Forms. Como os desenvolvedores da AEM Forms podem criar aplicativos clientes para uso com a AEM Forms, eles também devem ser capazes de aproveitar o mecanismo de logon único.

Cada aplicativo da Web da AEM Forms é empacotado em seu próprio arquivo Web Archive (WAR), que é empacotado como parte de um arquivo Enterprise Archive (EAR). Como um servidor de aplicativos não permite o compartilhamento de dados de sessão em diferentes aplicativos da Web, a AEM Forms usa cookies HTTP para armazenar informações de autenticação. Os cookies de autenticação permitem que um usuário faça logon em um aplicativo Forms e se conecte a outros aplicativos da Web da AEM Forms. Essa técnica é conhecida como logon único.

Os desenvolvedores do AEM Forms gravam aplicativos clientes para estender a funcionalidade dos Guias de formulário (obsoletos) e personalizar o Workspace. Por exemplo, um aplicativo do Workspace pode start um processo. O aplicativo cliente usa um terminal remoto para recuperar dados do serviço Forms.

Quando um serviço AEM Forms é chamado usando (obsoleto para formulários AEM) o AEM Forms Remoting, o aplicativo cliente passa o cookie de autenticação como parte da solicitação. Como o usuário já foi autenticado, nenhum logon adicional é necessário para fazer uma conexão do aplicativo cliente com o serviço AEM Forms.

>[!NOTE]
Se um cookie for inválido ou estiver ausente, não haverá redirecionamento implícito para uma página de logon. Portanto, você ainda pode chamar um serviço anônimo.

Você pode ignorar o mecanismo de logon único do AEM Forms escrevendo um aplicativo cliente que faz logon e logout sozinho. Se você ignorar o mecanismo de logon único, poderá usar a autenticação básica ou personalizada com seu aplicativo.

Como esse mecanismo não usa o mecanismo de logon único da AEM Forms, nenhum cookie de autenticação é gravado no cliente. As credenciais de logon são armazenadas no objeto `ChannelSet` para o canal remoto. Portanto, quaisquer chamadas `RemoteObject` feitas por você sobre o mesmo `ChannelSet` são feitas no contexto dessas credenciais.

### Configurando o logon único no AEM Forms {#setting-up-single-sign-on-in-aem-forms}

Para usar o logon único no AEM Forms, instale o componente de fluxo de trabalho dos formulários, que inclui o serviço de logon centralizado. Depois que um usuário faz login com êxito, o serviço de logon centralizado retorna um cookie de autenticação ao usuário. Cada solicitação subsequente para aplicativos da Web da Forms contém o cookie. Se o cookie for válido, o usuário será considerado autenticado e não precisará fazer logon novamente.

### Gravando um aplicativo cliente que usa logon único {#writing-a-client-application-that-uses-single-sign-on}

Quando você tira proveito do mecanismo de logon único, espera que os usuários façam logon usando o serviço de logon centralizado antes de iniciar um aplicativo cliente. Ou seja, um aplicativo cliente não faz logon pelo navegador ou chamando o método `ChannelSet.login`.

Se você estiver usando o mecanismo de logon único da AEM Forms, configure o terminal Remoting para usar a autenticação personalizada, não básica. Caso contrário, ao usar a autenticação básica, um erro de autenticação resultará em um desafio do navegador, que você não deseja que o usuário veja. Em vez disso, seu aplicativo detecta o erro de autenticação e exibe uma mensagem instruindo o usuário a fazer logon usando o serviço de logon centralizado.

Um aplicativo cliente acessa o AEM Forms por meio de um terminal remoto usando o componente `RemoteObject`, como mostra o exemplo a seguir.

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

**Efetuar logon como um novo usuário enquanto o aplicativo Flex ainda estiver em execução**

Um aplicativo criado com a Flex inclui o cookie de autenticação com cada solicitação a um serviço AEM Forms. Por motivos de desempenho, a AEM Forms não valida o cookie em cada solicitação. No entanto, a AEM Forms detecta quando um cookie de autenticação é substituído por outro cookie de autenticação.

Por exemplo, você start um aplicativo cliente e, enquanto o aplicativo está ativo, usa o serviço de logon centralizado para fazer logoff. Em seguida, você pode fazer logon como um usuário diferente. O logon como um usuário diferente substitui o cookie de autenticação existente por um cookie de autenticação para o novo usuário.

Na próxima solicitação do aplicativo cliente, a AEM Forms detecta que o cookie foi alterado e faz logout do usuário. Portanto, a primeira solicitação após uma alteração de cookie falha. Todas as solicitações subsequentes são feitas no contexto do novo cookie e são bem-sucedidas.

**Desconectando**

Para sair do AEM Forms e invalidar uma sessão, o cookie de autenticação deve ser excluído do computador do cliente. Como o objetivo do logon único é permitir que um usuário faça logon uma vez, você não deseja que um aplicativo cliente exclua o cookie. Esta ação efetua logout do usuário.

Portanto, chamar o método `RemoteObject.logout` em um aplicativo cliente gera uma mensagem de erro no cliente especificando que a sessão não está desconectada. Em vez disso, o usuário pode usar o serviço de logon centralizado para fazer logout e excluir o cookie de autenticação.

**Desconectando enquanto o aplicativo Flex ainda está em execução**

Você pode start um aplicativo cliente criado com a Flex e usar o serviço de logon centralizado para fazer logoff. Como parte do processo de logout, o cookie de autenticação é excluído. Se uma solicitação remota for feita sem um cookie ou com um cookie inválido, a sessão do usuário será invalidada. Esta ação é, de fato, um logout. Na próxima vez que o aplicativo cliente tentar se conectar a um serviço AEM Forms, o usuário será solicitado a fazer logon.

**Consulte também:**

[Invocar o AEM Forms usando (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Tratamento de documentos com (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Incluindo o arquivo da biblioteca do AEM Forms Flex](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Invocar um processo de duração curta transmitindo um documento não seguro usando (obsoleto para formulários AEM) o AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Transmissão de documentos protegidos para chamar processos usando Remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Passar documentos protegidos para chamar processos usando Remoting {#passing-secure-documents-to-invoke-processes-using-remoting}

Você pode passar documentos seguros para a AEM Forms ao chamar um processo que exija um ou mais documentos. Ao enviar um documento seguro, você está protegendo informações comerciais e documentos confidenciais. Nessa situação, um documento pode fazer referência a um documento PDF, a um documento XML, a um documento do Word e assim por diante. Quando a AEM Forms está configurada para permitir documentos seguros, é necessário enviar um documento seguro para a AEM Forms a partir de um aplicativo cliente gravado na Flex. (Consulte [Configurar a AEM Forms para aceitar documentos seguros e não protegidos](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).)

Ao transmitir um documento seguro, use o logon único e especifique um usuário de formulários AEM que tenha a função *Documento Upload Application User*. Sem essa função, o usuário não pode carregar um documento seguro. Você pode atribuir uma função programaticamente a um usuário. (Consulte [Gerenciando Funções e Permissões](/help/forms/developing/users.md#managing-roles-and-permissions).)

>[!NOTE]
Ao criar uma nova função e desejar que os membros dessa função façam upload de documentos protegidos, especifique a permissão de Upload de Documento.

A AEM Forms oferece suporte a uma operação chamada `getFileUploadToken` que retorna um token passado para o servlet de upload. O método `DocumentReference.constructRequestForUpload` requer um URL para o AEM Forms, juntamente com o token retornado pelo método `LC.FileUploadAuthenticator.getFileUploadToken`. Este método retorna um objeto `URLRequest` que é usado na invocação para o servlet de upload. O código a seguir demonstra essa lógica do aplicativo.

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

### Configurar a AEM Forms para aceitar documentos seguros e não protegidos {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

Você pode usar o console de administração para especificar se os documentos são seguros ao passar um documento de um aplicativo cliente Flex para um processo AEM Forms. Por padrão, a AEM Forms está configurada para aceitar documentos seguros. Você pode configurar a AEM Forms para aceitar documentos protegidos executando as seguintes etapas:

1. Faça logon no console de administração.
1. Clique em **Configurações**.
1. Clique em **Principais configurações do sistema.**
1. Clique em Configurações.
1. Certifique-se de que a opção Permitir upload de documentos não protegidos de aplicativos Flex esteja desmarcada.

>[!NOTE]
Para configurar a AEM Forms para aceitar documentos não protegidos, selecione a opção Permitir upload de documentos não protegidos de aplicativos Flex. Em seguida, reinicie um aplicativo ou serviço para garantir que a configuração entre em vigor.

### Start rápido: Invocando um processo de duração curta transmitindo um documento seguro usando Remoting {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

O exemplo de código a seguir chama `MyApplication/EncryptDocument.`Um usuário deve fazer logon para clicar no botão Selecionar arquivo usado para carregar um arquivo PDF e chamar o processo. Ou seja, assim que o usuário for autenticado, o botão Selecionar arquivo será ativado. A ilustração a seguir mostra o aplicativo cliente Flex depois que um usuário é autenticado. Observe que a caixa de seleção autenticada está ativada.

![iu_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

se a AEM Forms estiver configurada para permitir apenas o carregamento de documentos protegidos e o usuário não tiver a função *Documento Upload Application User*, uma exceção será lançada. Se o usuário tiver essa função, o arquivo será carregado e o processo será chamado.

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
 
        // Set the docRef’s url and referenceType parameters
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

**Consulte também:**

[Invocar o AEM Forms usando (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Tratamento de documentos com (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Incluindo o arquivo da biblioteca do AEM Forms Flex](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Invocar um processo de duração curta transmitindo um documento não seguro usando (obsoleto para formulários AEM) o AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticação de aplicativos cliente criados com a Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Invocar serviços de componentes personalizados usando Remoting {#invoking-custom-component-services-using-remoting}

Você pode chamar os serviços localizados em um componente personalizado usando o Remoting. Por exemplo, considere o componente Banco que contém o Serviço de atendimento ao cliente. Você pode chamar operações que pertencem ao Serviço de atendimento ao cliente usando um aplicativo cliente gravado na Flex. Antes de executar o start rápido associado a esta seção, é necessário criar o componente personalizado do Banco.

O Serviço de atendimento ao cliente expõe uma operação chamada `createCustomer`. Esta discussão descreve como criar um aplicativo cliente Flex que chame o Serviço de atendimento ao cliente e crie um cliente. Esta operação requer um objeto complexo do tipo `com.adobe.livecycle.sample.customer.Customer` que representa o novo cliente. A ilustração a seguir mostra o aplicativo cliente que chama o Serviço de atendimento ao cliente e cria um novo cliente. A operação `createCustomer` retorna um valor identificador do cliente. O valor do identificador é exibido na caixa de texto Identificador do cliente.

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
   <td><p>Especifica o nome de rua do cliente.</p></td>
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
   <td><p>Especifica o valor do identificador do cliente ao qual a nova conta pertence. Essa caixa de texto é preenchida pelo valor de retorno da operação <code>createCustomer</code> do Serviço de atendimento ao cliente. </p></td>
  </tr>
 </tbody>
</table>

### Mapeamento de tipos de dados complexos do AEM Forms {#mapping-aem-forms-complex-data-types}

Algumas operações do AEM Forms exigem tipos de dados complexos como valores de entrada. Esses tipos de dados complexos definem valores de tempo de execução usados pela operação. Por exemplo, a operação `createCustomer` do serviço do Cliente requer uma instância `Customer` que contenha valores de tempo de execução exigidos pelo serviço. Sem o tipo complexo, o Serviço de atendimento ao cliente lança uma exceção e não executa a operação.

Ao chamar um serviço AEM Forms, crie objetos de ActionScript que mapeiam para os tipos complexos AEM Forms necessários. Para cada tipo de dados complexo que uma operação requer, crie um objeto de ActionScript separado.

Na classe ActionScript, use a tag de metadados `RemoteClass` para mapear para o tipo complexo AEM Forms. Por exemplo, ao invocar a operação `createCustomer` do Serviço de atendimento ao cliente, crie uma classe de ActionScript que mapeie para o tipo de dados `com.adobe.livecycle.sample.customer.Customer`.

A classe de ActionScript a seguir chamada Customer mostra como mapear para o tipo de dados AEM Forms `com.adobe.livecycle.sample.customer.Customer`.

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

Os campos da classe do ActionScript correspondem aos campos que pertencem ao tipo complexo AEM Forms. Os seis campos localizados na classe ActionScript do Cliente correspondem aos campos que pertencem a `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
Uma boa maneira de determinar os nomes de campo que pertencem a um tipo complexo da Forms é visualização de um WSDL de serviço em um navegador da Web. Uma WSDL especifica os tipos complexos de um serviço e os membros de dados correspondentes. O WSDL a seguir é usado para o serviço de Atendimento ao cliente: `https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

A classe Customer ActionScript pertence a um pacote chamado customer. É recomendável colocar todas as classes de ActionScripts que mapeiam para tipos de dados complexos do AEM Forms em seus próprios pacotes. Crie uma pasta na pasta src do projeto Flex e coloque o arquivo de ActionScript na pasta, como mostrado na ilustração a seguir.

![iu_iu_customeras](assets/iu_iu_customeras.png)

### Start rápido: Invocar o serviço personalizado do Cliente usando Remoting {#quick-start-invoking-the-customer-custom-service-using-remoting}

O exemplo de código a seguir chama o Serviço de atendimento ao cliente e cria um novo cliente. Ao executar esse exemplo de código, certifique-se de preencher todas as caixas de texto. Além disso, certifique-se de criar o arquivo Customer.as que mapeia para `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
Antes de executar esse start rápido, é necessário criar e implantar o componente personalizado do Banco.

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

**Folha de estilos**

Este start rápido contém uma folha de estilos chamada *bank.css*. O código a seguir representa a folha de estilos usada.

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

**Consulte também:**

[Invocar o AEM Forms usando (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Tratamento de documentos com (obsoleto para formulários AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Incluindo o arquivo da biblioteca do AEM Forms Flex](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Invocar um processo de duração curta transmitindo um documento não seguro usando (obsoleto para formulários AEM) o AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticação de aplicativos cliente criados com a Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Transmissão de documentos protegidos para chamar processos usando Remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
