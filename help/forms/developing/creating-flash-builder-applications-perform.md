---
title: Criação de aplicativos Flash Builder que executam autenticação SSO usando tokens HTTP
seo-title: Criação de aplicativos Flash Builder que executam autenticação SSO usando tokens HTTP
description: 'null'
seo-description: 'null'
uuid: 273db00a-a665-4e52-88fa-4fca06d05f8c
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0ff30df7-b3ad-4c34-9644-87c689acc294
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Criação de aplicativos Flash Builder que executam autenticação SSO usando tokens HTTP {#creating-flash-builder-applicationsthat-perform-sso-authentication-using-http-tokens}

Você pode criar um aplicativo cliente usando o Flash Builder que executa autenticação de logon único (SSO) usando tokens HTTP. Considere, por exemplo, que você cria um aplicativo baseado na Web usando o Flash Builder. Em seguida, suponha que o aplicativo contenha visualizações diferentes, nas quais cada visualização chama uma operação diferente do AEM Forms. Em vez de autenticar um usuário para cada operação do Forms, você pode criar uma página de logon que permite que um usuário se autentique uma vez. Depois de autenticado, um usuário pode chamar várias operações sem precisar autenticar novamente. Por exemplo, se um usuário tiver feito logon no Workspace (ou em outro aplicativo do Forms), ele não precisará autenticar novamente.

Embora o aplicativo cliente contenha a lógica de aplicativo necessária para executar a autenticação SSO, o Gerenciamento de usuários de formulários AEM executa a autenticação de usuário real. Para autenticar um usuário usando tokens HTTP, o aplicativo cliente chama a operação do serviço do Authentication Manager `authenticateWithHTTPToken` . O Gerenciamento de usuários pode autenticar usuários usando um token HTTP. Para chamadas remotas ou de serviço da Web subsequentes para o AEM Forms, você não precisa passar as credenciais para autenticação.

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a opção Invocar formulários AEM usando o recurso Remoting. (Consulte [Invocar formulários AEM usando o AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

O seguinte processo de vida curta do AEM Forms, chamado `MyApplication/EncryptDocument`, é chamado depois que um usuário é autenticado usando SSO. (Para obter informações sobre esse processo, como seus valores de entrada e saída, consulte o exemplo [](/help/forms/developing/aem-forms-processes.md)de processo de duração curta.)

![cf_cf_encryptdocumentprocess2](assets/cf_cf_encryptdocumentprocess2.png)

>[!NOTE]
>
>Esse processo não se baseia em um processo de formulários AEM existente. Para seguir juntamente com os exemplos de código que discutem como invocar esse processo, crie um processo chamado `MyApplication/EncryptDocument` usando o workbench. (Consulte [Usando o Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

O aplicativo cliente criado usando o Flash Builder interage com o servlet de segurança do Gerenciador de usuários configurado em `/um/login` e `/um/logout`. Ou seja, o aplicativo cliente envia uma solicitação para o `/um/login` URL durante a inicialização para determinar o status do usuário. Em seguida, o Gerenciador de usuários responde com o status do usuário. O aplicativo cliente e o servlet de segurança do Gerenciador de usuários se comunicam usando HTTP.

**Formato de solicitação**

O servlet de segurança requer as seguintes variáveis de entrada:

* `um_no_redirect` - Este valor deve ser `true`. Essa variável acompanha todas as solicitações feitas ao servlet de segurança do Gerenciador de usuários. Também ajuda o servlet de segurança a diferenciar a solicitação recebida de um cliente flexível ou de outros aplicativos da Web.
* `j_username` - Esse valor é o valor do identificador de login do usuário, conforme fornecido no formulário de logon.
* `j_password` - Esse valor é a senha correspondente do usuário, conforme fornecido no formulário de logon.

O `j_password` valor é necessário somente para solicitações de credenciais. Se o valor da senha não for especificado, o servlet de segurança verificará se a conta que você está usando já está autenticada. Em caso afirmativo, pode prosseguir; no entanto, o servlet de segurança não o autentica novamente.

>[!NOTE]
>
>Para manuseio correto do i18n, verifique se esses valores estão na forma POST.

**Formato de resposta**

O servlet de segurança configurado em `/um/login` responde usando o `URLVariables` formato. Nesse formato, a saída do tipo de conteúdo é text/plain. A saída contém pares de valores de nome separados por um caractere de E comercial (&amp;). A resposta contém as seguintes variáveis:

* `authenticated` - O valor é `true` ou `false`.
* `authstate` - Esse valor pode conter um dos seguintes valores:

   * `CREDENTIAL_CHALLENGE` - Esse estado indica que o Gerenciador de usuários não pode determinar a identidade do usuário por qualquer meio. Para que a autenticação ocorra, o nome de usuário e a senha do usuário são obrigatórios.
   * `SPNEGO_CHALLENGE`- Este estado é tratado da mesma forma `CREDENTIAL_CHALLENGE`.
   * `COMPLETE` - Esse estado indica que o Gerenciador de usuários pode autenticar o usuário.
   * `FAILED` - Esse estado indica que o Gerenciador de usuários não pôde autenticar o usuário. Como resposta a esse estado, o cliente flex pode mostrar uma mensagem de erro para o usuário.
   * `LOGGED_OUT` - Esse estado indica que o usuário fez logout com êxito.

* `assertionid` - Se o estado foi `COMPLETE` então ele contém o `assertionId` valor do usuário. Um aplicativo cliente pode obter o `AuthResult` para o usuário.

**Processo de logon**

Quando um aplicativo cliente é start, você pode fazer uma solicitação POST para o servlet `/um/login` de segurança. Por exemplo, `https://<your_serverhost>:<your_port>/um/login?um_no_redirect=true`. Quando a solicitação chega ao servlet de segurança do Gerenciador de usuários, ele executa as seguintes etapas:

1. Ele procura um cookie chamado `lcAuthToken`. Se o usuário já tiver feito logon em outro aplicativo do Forms, esse cookie estará presente. Se o cookie for encontrado, seu conteúdo será validado.
1. Se o SSO baseado em cabeçalho estiver ativado, o servlet procurará cabeçalhos configurados para determinar a identidade do usuário.
1. Se o SPNEGO estiver ativado, o servlet tentará iniciar o SPNEGO e tentar determinar a identidade do usuário.

Se o servlet de segurança localizar um token válido que corresponda a um usuário, ele permitirá que você continue e responda com `authstate=COMPLETE`. Caso contrário, o servlet de segurança responderá com `authstate=CREDENTIAL_CHALLENGE`. A lista a seguir explica esses valores:

* `Case authstate=COMPLETE`: Indica que o usuário está autenticado e que o `assertionid` valor contém o identificador de asserção do usuário. Neste estágio, o aplicativo cliente pode se conectar ao AEM Forms. O servlet configurado para esse URL pode obter o `AuthResult` para o usuário chamando o `AuthenticationManager.authenticate(HttpRequestToken)` método. A `AuthResult` instância pode criar o contexto do gerenciador de usuários e armazená-lo na sessão.
* `Case authstate=CREDENTIAL_CHALLENGE`: Indica que o servlet de segurança requer as credenciais do usuário. Como resposta, o aplicativo cliente pode exibir a tela de logon para o usuário e enviar a credencial obtida para o servlet de segurança (por exemplo, `https://<your_serverhost>:<your_port>/um/login?um_no_redirect=true&j_username=administrator&j_password=password)`. Se a autenticação for bem-sucedida, o servlet de segurança responderá com `authstate=COMPLETE`.

Se a autenticação ainda não for bem-sucedida, o servlet de segurança responderá com `authstate=FAILED`. Para responder a esse valor, o aplicativo cliente pode exibir uma mensagem para obter as credenciais novamente.

>[!NOTE]
>
>Embora `authstate=CREDENTIAL_CHALLENGE`, é recomendável que o cliente envie a credencial obtida para o servlet de segurança em um formulário POST.

**Processo de logout**

Quando um aplicativo cliente faz logout, você pode enviar uma solicitação para o seguinte URL:

`https://<your_serverhost>:<your_port>/um/logout?um_no_redirect=true`

Ao receber essa solicitação, o servlet de segurança do Gerenciador de usuários exclui o `lcAuthToken` cookie e responde com `authstate=LOGGED_OUT`. Depois que o aplicativo cliente receber esse valor, o aplicativo poderá executar tarefas de limpeza.

## Criação de um aplicativo cliente que autentique usuários de formulários AEM usando SSO {#creating-a-client-application-that-authenticates-aem-forms-users-using-sso}

Para demonstrar como criar um aplicativo cliente que execute a autenticação SSO, um aplicativo cliente de exemplo é criado. A ilustração a seguir mostra as etapas que o aplicativo cliente executa para autenticar um usuário usando SSO.

![cf_cf_flexsso](assets/cf_cf_flexsso.png)

A ilustração anterior descreve o fluxo do aplicativo que ocorre quando o aplicativo cliente é start.

1. O aplicativo cliente aciona o `applicationComplete` evento.
1. A chamada para `ISSOManager.singleSignOn` foi feita. O aplicativo cliente envia uma solicitação para o servlet de segurança do Gerenciador de usuários.
1. Se o servlet de segurança autenticar o usuário, ele será `ISSOManager` despachado `SSOEvent.AUTHENTICATION_SUCCESS`. Como resposta, o aplicativo cliente mostra a página principal. Neste exemplo, a página principal chama o processo de vida curta do AEM Forms chamado MyApplication/EncryptDocument.
1. Se o servlet de segurança não puder determinar se o usuário é válido, o aplicativo solicitará as credenciais do usuário novamente. A `ISSOManager` classe despacha o `SSOEvent.AUTHENTICATION_REQUIRED` evento. O aplicativo cliente exibe a página de logon.
1. As credenciais fornecidas na página de logon são enviadas para o `ISSOManager.login` método. Se a autenticação for bem-sucedida, isso leva à etapa 3. Caso contrário, o `SSOEvent.AUTHENTICATION_FAILED` evento será acionado. O aplicativo cliente exibe a página de logon e uma mensagem de erro apropriada.

### Criação do aplicativo cliente {#creating-the-client-application}

O aplicativo cliente consiste nos seguintes arquivos:

* `SSOStandalone.mxml`: O arquivo MXML principal que representa o aplicativo cliente. (Consulte [Criação do arquivo](creating-flash-builder-applications-perform.md#creating-the-ssostandalone-mxml-file)SSOStandalone.mxml.)
* `um/ISSOManager.as`: Exponha as operações relacionadas ao Logon único (SSO). (Consulte [Criação do arquivo](creating-flash-builder-applications-perform.md#creating-the-issomanager-as-file)ISSOManager.as.)
* `um/SSOEvent.as`: O `SSOEvent` é despachado para eventos relacionados ao SSO. (Consulte [Criação do arquivo](creating-flash-builder-applications-perform.md#creating-the-ssoevent-as-file)SSOEEvent.as.)
* `um/SSOManager.as`: Gerencia as operações relacionadas ao SSO e despacha os eventos apropriados. (Consulte [Criação do arquivo](creating-flash-builder-applications-perform.md#creating-the-ssomanager-as-file)SSOManager.as.)
* `um/UserManager.as`: Contém lógica de aplicativo que chama o serviço Authentication Manager usando seu WSDL. (Consulte [Criação do arquivo](creating-flash-builder-applications-perform.md#creating-the-usermanager-as-file)UserManager.as.)
* `views/login.mxml`: Representa a tela de login. (Consulte [Criação do arquivo](creating-flash-builder-applications-perform.md#creating-the-login-mxml-file)login.mxml.)
* `views/logout.mxml`: Representa a tela de logout. (Consulte [Criação do arquivo](creating-flash-builder-applications-perform.md#creating-the-logout-mxml-file)logout.mxml.)
* `views/progress.mxml`: Representa uma visualização de progresso. (Consulte [Criação do arquivo](creating-flash-builder-applications-perform.md#creating-the-progress-mxml-file)progress.mxml.)
* `views/remoting.mxml`: Representa a visualização que chama o processo de vida curta do AEM Forms chamado MyApplication/EncryptDocument usando remoting. (Consulte [Criação do arquivo](creating-flash-builder-applications-perform.md#creating-the-remoting-mxml-file)remoting.mxml.)

A ilustração a seguir fornece uma representação visual do aplicativo cliente.

![cf_cf_sso_project](assets/cf_cf_sso_project.png)

>[!NOTE]
>
>Observe que existem dois pacotes chamados um e visualização. Ao criar o aplicativo cliente, certifique-se de colocar os arquivos em seus pacotes apropriados. Além disso, adicione o arquivo adobe-remoting-provider.swc ao caminho de classe do seu projeto. (Consulte [Inclusão do arquivo](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)da biblioteca Flex do AEM Forms.)

### Criação do arquivo SSOStandalone.mxml {#creating-the-ssostandalone-mxml-file}

O código a seguir representa o arquivo SSOStandalone.mxml.

```as3
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application
                 layout="absolute"
                 applicationComplete="initApp()"
                 height="400" width="550"
                 xmlns:v="views.*"
                 backgroundColor="#EDE8F0" viewSourceURL="srcview/index.html">
     <mx:Script>
         <![CDATA[
             import mx.utils.URLUtil;
             import um.SSOEvent;
             import mx.core.UIComponent;
             import um.SSOManager;
             import mx.rpc.events.ResultEvent;
             import mx.utils.ObjectUtil;
             import mx.controls.Alert;
 
             [Bindable]
             private var _serverURL:String;
 
             private var _ssoManager:SSOManager;
 
             private var _progress:UIComponent;
 
             private var _loginPage:UIComponent;
 
             private function initApp():void{
                 _serverURL = determineServerUrl();
                 _ssoManager = new SSOManager(_serverURL);
 
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_FAILED,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_SUCCESS,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_REQUIRED,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.LOGOUT_COMPLETE,loginHandler);
                 _ssoManager.addEventListener(SSOEvent.AUTHENTICATION_FAULT,loginHandler);
 
                 trace("[Main] Add the required event handlers for authentication");
                 _ssoManager.singleSignOn();
 
                 showBusy();
             }
 
             private function determineServerUrl():String
             {
                 var s:String ;
                 var appUrl:String = Application.application.url;
                 var givenUrl:String  = ExternalInterface.call("serverUrl.toString");
                 trace("[Main] Application url ["+appUrl+"] Given url ["+givenUrl+"]");
                 if(appUrl != null && appUrl.search("^http") != -1){
                     s = appUrl;
                 }
                 if(s == null){
                     s = givenUrl;
                 }
                 if(s== null){
                     s = "https://hiro-xp:8080/";
                 }
                 s = URLUtil.getFullURL(s,"/");
                 trace("[Main] Would be using ["+s+"] as serverUrl");
                 return s;
             }
 
             private function loginHandler(event:SSOEvent):void
             {
                 trace("[Main] Handling event "+event.type);
                 switch(event.type)
                 {
                     case SSOEvent.AUTHENTICATION_FAILED:
                         viewContent.selectedChild = login;
                         login.showLoginFailed();
                         break;
                     case SSOEvent.AUTHENTICATION_SUCCESS:
                         viewContent.selectedChild = remoting;
                         break;
                     case SSOEvent.AUTHENTICATION_REQUIRED:
                         viewContent.selectedChild = login;
                         break;
                     case SSOEvent.LOGOUT_COMPLETE:
                         viewContent.selectedChild = logout;
                         break;
                     case SSOEvent.AUTHENTICATION_FAULT:
                         Alert.show("Error doing authentication. Root error ["+event.rootEvent+"]","Authentication Fault",Alert.OK);
                 }
             }
 
             public function get ssoManager():SSOManager
             {
                 return _ssoManager;
             }
 
             public function showBusy():void
             {
                 viewContent.selectedChild = progress;
             }
 
             public function get serverUrl():String
             {
                 return _serverURL;
             }
 
         ]]>
     </mx:Script>
     <mx:ViewStack x="0" y="0" id="viewContent" >
         <v:login id="login" />
         <v:remoting id="remoting"  />
         <v:progress id="progress" />
         <v:logout id="logout"/>
     </mx:ViewStack>
 </mx:Application>
 
```

### Criação do arquivo ISSOManager.as {#creating-the-issomanager-as-file}

O código a seguir representa o arquivo ISSOManager.as.

```as3
 package um
 {
     import flash.events.IEventDispatcher;
 
     /**
      * The <code>ISSOManager</code> expose operations related to Single Sign On (SSO) in AEM Forms
      * environment. The application should register appropriate <code>SSOEvent</code> handlers prior
      * to calling any of the following operations
      */
     public interface ISSOManager extends IEventDispatcher
     {
         /**
          * Tries to validate whether the user has an already existing session or not (SSO Scenarios). The application
          * may call this method during the initialization. In general this call would lead to one of the
          * following events getting dispatched
          * <ul>
          * <li>SSOEvent.AUTHENTICATION_SUCCESS - If a SSO session was found and valid
          * <li>SSOEvent.AUTHENTICATION_REQUIRED - No SSO session was found and as such authentication is required in
          * the form of username and password.
          * <li>SSOEvent.AUTHENTICATION_FAULT - Some error has occured while connecting to the server
          * </ul>
          */
         function singleSignOn():void;
 
         /**
          * Authenticates the user using username and password. It may lead to one of the following events
          * <ul>
          * <li>SSOEvent.AUTHENTICATION_SUCCESS - The authentication is successful and a session is established
          * <li>SSOEvent.AUTHENTICATION_FAILED - Authentication has failed
          * </ul>
          */
         function login(username:String, password:String):void;
 
         /**
          * Terminates the current session and logs out the user.
          */
         function logout():void;
 
         /**
          * Get the assertionId for the logged in user
          */
         function get assertionId():String;
     }
 }
```

### Criação do arquivo SSOEEvent.as {#creating-the-ssoevent-as-file}

O código a seguir representa o arquivo SSOEEvent.as.

```as3
 package um
 {
     import flash.events.Event;
 
     /**
      * The <code>SSOEvent</code> is dispatched for SSO related events
      */
     public class SSOEvent extends Event
     {
         /**
          * This type of event would be dispatched when the Authentication process is successful. Authentication
          * might have been done with SSO or username and password. As a response to this event the application
          * can show the welcome page to the user
          * The application may want to perform specific check for permission/role so as to verify the user is allowed.
          * So as a response to this event the application would do those checks and then only show the welcome page
          */
         public static const AUTHENTICATION_SUCCESS:String = "authenticationSuccess";
 
         /**
          * This type of event would be dispatched when authentication fails using the username, password.
          * As a response to this type of event an application can show an error message to the user.
          * This event would only happen when authentication is done using username and password and NOT in
          * SSO case.
          */
         public static const AUTHENTICATION_FAILED:String = "authenticationFailed";
 
         /**
          * This type of event would be dispatched when authentication using SSO is not achieved. And due to
          * that we require the user's username and password for authentication. As a response to this event
          * the application can show the login page to the user.
          */
         public static const AUTHENTICATION_REQUIRED:String = "authenticationRequired";
 
         /**
          * This type of event would be dispatched when logout is complete. As a response to this event the
          * application may show a logout page informing the user that he has been logged out. Or the application
          * can take the user back to login page
          */
         public static const LOGOUT_COMPLETE:String = "logoutComplete";
 
         /**
          * This type of event would be dispatched when ever there is a problem in doing Authentication. The root cause
          * can be obtained from the <code>rootEvent</code>.
          */
         public static const AUTHENTICATION_FAULT:String = "authenticationFault";
 
         private var _rootEvent:Event;
 
         public function SSOEvent(type:String, rootEvent:Event=null)
         {
             super(type,true,false);
             _rootEvent = rootEvent;
         }
 
         /**
          * The root event. If current event type is <code>AUTHENTICATION_FAULT</code> then it would be an
          * <code>IOErrorEvent</code> in other cases it would be complete event. Its basic use is to extract the root
          * cause in case of an authentication fault.
          */
         public function get rootEvent():Event
         {
             return _rootEvent;
         }
     }
 }
```

### Criação do arquivo SSOManager.as {#creating-the-ssomanager-as-file}

O código a seguir representa o arquivo SSOManager.as.

```as3
 package um
 {
     import flash.events.Event;
     import flash.events.EventDispatcher;
     import flash.events.IOErrorEvent;
     import flash.external.ExternalInterface;
     import flash.net.URLLoader;
     import flash.net.URLLoaderDataFormat;
     import flash.net.URLRequest;
     import flash.net.URLVariables;
 
     import mx.utils.ObjectUtil;
 
     /**
      * Manages the SSO related operations and dispatches appropriate events. It would connect to the UM Filter/Servlet
      * at <code>um/login</code> The UM response would be of form of url encoded variables. It would look for
      * <code>authstate</code> value in the response and depending on that it would proceed.
      *
      * <p>If there is an IO_Error while initial attempt to UM then it would assume it as a 401 response. And it would
      * be assumed that SPNEGO based authenticatin is not working and therefore user would be shown a login page.
      */
     public class SSOManager extends EventDispatcher implements ISSOManager
     {
         private static const SSO_URL:String = "um/login";
         private static const SSO_LOGOUT_URL:String = "um/logout";
         private static const AUTH_COOKIE_NAME:String = "lcAuthToken";
 
         private var _serverUrl:String;
         private var _assertionId:String;
 
         /**
          * Constructs an SSOManager with the given server url.
          *
          * @param serverUrl - The uri of the server to connect to. it must be without any context path e.g
          * http://localhost:8080/. The SSOManager would directly append the path of UM exposed SSO url to it
          * for its operations
          */
         public function SSOManager(serverUrl:String)
         {
             _serverUrl = serverUrl;
         }
 
         public function singleSignOn():void
         {
             sendRequest(SSO_URL,true);
         }
 
         public function login(username:String, password:String):void
         {
             sendRequest(SSO_URL,false,
                 function(request:URLRequest,vars:URLVariables):void
                 {
                     vars.j_username = username;
                     vars.j_password = password;
                 }
             );
         }
 
         public function logout():void
         {
             sendRequest(SSO_LOGOUT_URL);
         }
 
         public function get assertionId():String
         {
             return _assertionId;
         }
 
 
 
         /**
          * Connects to the UM security service.
          */
         private function sendRequest(relativeUrl:String,authenticationRequest:Boolean=false, requestProcessor:Function=null):void
         {
             var loader:URLLoader = new URLLoader();
             loader.dataFormat = URLLoaderDataFormat.VARIABLES;
             var request:URLRequest = new URLRequest(_serverUrl + relativeUrl);
             trace("[SSOmanager] Contacting ["+request.url+"]");
             var vars:URLVariables = new URLVariables();
             vars.um_no_redirect = "true";
             request.data = vars;
             if(requestProcessor != null){
                 requestProcessor(request,vars);
             }
 
             loader.addEventListener(Event.COMPLETE,authHandler);
             //if its an authentication request then only treat io error as a possible 401
             //for others treat them as faults
             if(authenticationRequest){
                 loader.addEventListener(IOErrorEvent.IO_ERROR,httpAuthenticationHandler);
             }else{
                 loader.addEventListener(IOErrorEvent.IO_ERROR,authFaultHandler);
             }
             trace("[SSOmanager] Sending request "+ ObjectUtil.toString(request));
             loader.load(request);
         }
 
         private function authHandler(event:Event):void
         {
             var loader:URLLoader = URLLoader(event.target);
             var response:URLVariables = URLVariables(loader.data);
             trace("[SSOmanager] Processing response ["+ObjectUtil.toString(response)+"]");
             handleAuthResult(response["authstate"],response);
         }
 
         /**
          * Handles the IOErrorEvent. Flash would dispatch IOEvent in response to HTTP 401.
          * There is no way to distinguish it from the genuine IOError.
          */
         private function httpAuthenticationHandler(event:IOErrorEvent):void
         {
             trace("[SSOmanager] Processing IOErrorEvent ["+ObjectUtil.toString(event)+"]");
             handleAuthResult("CREDENTIAL_CHALLENGE");
 
         }
 
         /**
          * Dispatches appropriate <code>SSOEvent</code> on the basis of the <code>authstate</code>
          * value of the response.
          * The response is url encoded in for of
          * <pre>
          * authenticated=false&authstate=SPNEGO_CHALLENGE
          * </pre>
          * Depending on <code>authstate</code> the SSOEvent is dispatched
          */
         private function handleAuthResult(authState:String,response:URLVariables = null):void
         {
             trace("[SSOmanager] processing state "+authState);
             switch(authState)
             {
                 case "FAILED"  :
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_FAILED));
                     break;
                 case "COMPLETE" :
                     _assertionId = response ? response["assertionid"] : null;
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_SUCCESS));
                     break;
                 case "CREDENTIAL_CHALLENGE" :
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_REQUIRED));
                     break;
                 case "LOGGED_OUT" :
                     dispatchEvent(new SSOEvent(SSOEvent.LOGOUT_COMPLETE));
                     break;
                 default:
                     dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_REQUIRED));
                     break;
             }
         }
 
         private function authFaultHandler(event:Event):void
         {
             dispatchEvent(new SSOEvent(SSOEvent.AUTHENTICATION_FAULT,event));
         }
 
     }
 }
```

### Criação do arquivo UserManager.as {#creating-the-usermanager-as-file}

O código a seguir representa o arquivo UserManager.as.

```as3
 package um
 {
     import flash.events.Event;
     import mx.rpc.soap.WebService;
     import mx.rpc.soap.Operation;
     import mx.rpc.IResponder;
     import mx.rpc.events.FaultEvent;
     import mx.rpc.events.ResultEvent;
     import mx.rpc.soap.LoadEvent;
 
     public class UserManager
     {
         private var _ssoManager:ISSOManager;
         private var _serverUrl:String;
 
         public function UserManager(ssoManager:ISSOManager,serverUrl:String)
         {
             _serverUrl = serverUrl;
             _ssoManager = ssoManager;
         }
 
         public function retrieveAssertion(responder:IResponder):String
         {
             var assertionId:String = _ssoManager.assertionId;
             if(!assertionId)
             {
                 trace("[UserManager] AssertionId not found");
                 return null;
             }
 
             var ws:WebService = new WebService();
             var wsdl:String = _serverUrl+'soap/services/AuthenticationManagerService?wsdl&lc_version=8.2.1';
             ws.loadWSDL(wsdl);
             ws.addEventListener(LoadEvent.LOAD,
                 function(event:Event):void
                 {
                     trace("[UserManager] WSDL loaded");
                     var authenticate:Operation = ws.authenticateWithHttpToken as Operation;
                     authenticate.resultFormat = "e4x";
                     authenticate.addEventListener(ResultEvent.RESULT,
                         function(event:Event):void
                         {
                             responder.result(event);
                         }
                     );
                     authenticate.send({assertionId:assertionId});
                 }
             );
 
             ws.addEventListener(FaultEvent.FAULT,
                 function(event:Event):void
                 {
                     responder.fault(event);
                 }
             );
             return null;
         }
     }
 }
```

### Criação do arquivo login.mxml {#creating-the-login-mxml-file}

O código a seguir representa o arquivo login.mxml.

```as3
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="500" height="400">
     <mx:Script>
         <![CDATA[
             import mx.core.Application;
             public function showLoginFailed():void
             {
                 loginMessage.text = "Username or Password incorrect";
             }
 
             private function doLogin():void
             {
                 Application.application.ssoManager.login(j_username.text,j_password.text);
                 Application.application.showBusy();
             }
 
         ]]>
     </mx:Script>
 
     <mx:VBox height="113" width="244" x="128" y="144" horizontalAlign="center" verticalGap="10">
         <mx:HBox width="100%">
             <mx:HBox width="100%" verticalAlign="middle" horizontalAlign="center" height="32">
                 <mx:Label text="Username" fontWeight="bold"/>
                 <mx:TextInput id="j_username"/>
             </mx:HBox>
         </mx:HBox>
         <mx:HBox width="100%" height="33" horizontalAlign="center" horizontalGap="10" verticalAlign="middle">
             <mx:Label text="Password" fontWeight="bold"/>
             <mx:TextInput displayAsPassword="true" id="j_password"/>
         </mx:HBox>
         <mx:Button label="Login" click="doLogin()"/>
     </mx:VBox>
     <mx:Text x="128" y="122" id="loginMessage" width="230" height="14"/>
     <mx:Label x="154" y="65" text="AEM Forms SSO Demo" fontFamily="Georgia" fontSize="20" color="#0A0A0A"/>
 </mx:Canvas>
 
```

### Criação do arquivo logout.mxml {#creating-the-logout-mxml-file}

O código a seguir representa o arquivo logout.mxml.

```as3
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="500" height="400">
     <mx:Label x="97" y="188" text="You have successfully logged out from the application"/>
 
 </mx:Canvas>
 
```

### Criação do arquivo progress.mxml {#creating-the-progress-mxml-file}

O código a seguir representa o arquivo progress.mxml.

```as3
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas >
     <mx:Label x="151" y="141" text="Wait...."/>
     <mx:SWFLoader source="LoadingCircle.swf" width="50" height="50" horizontalCenter="0" verticalCenter="0"/>
 </mx:Canvas>
```

### Criação do arquivo remoting.mxml {#creating-the-remoting-mxml-file}

O código a seguir representa o arquivo remoting.mxml que chama o `MyApplication/EncryptDocument` processo. Como um documento é passado para o processo, a lógica do aplicativo responsável por passar um documento seguro para o AEM Forms está localizada nesse arquivo. (Consulte [Passando documentos protegidos para chamar processos usando o recurso Remoto](/help/forms/developing/invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).)

```as3
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Canvas  width="664" height="400" creationComplete="initializeChannelSet()" xmlns:views="views.*">
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
             import um.UserManager;
             import mx.rpc.events.ResultEvent;
             import mx.rpc.events.FaultEvent;
             import mx.core.Application;
             import mx.rpc.Responder;
             import mx.utils.ObjectUtil;
 
             // Classes used in file retrieval
             private var fileRef:FileReference = new FileReference();
             private var docRef:DocumentReference = new DocumentReference();
             private var parentResourcePath:String = "/";
             //private var serverPort:String = "'[server]:[port]'";
             private var serverPort:String = "'[server]:[port]'";
             private var now1:Date;
             private var userManager:UserManager;
 
             // Define a ChannelSet object.
             public var cs:ChannelSet;
 
             // Holds information returned from AEM Forms
             [Bindable]
             public var progressList:ArrayCollection = new ArrayCollection();
 
 
             // Set up channel set to invoke AEM Forms.
             // This must be done before calling any service or process, but only
             // once for the entire application.
             private function initializeChannelSet():void {
                 cs = new ChannelSet();
                 cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
                 EncryptDocument.channelSet = cs;
 
             //Get the user that is authenticated
             userManager = new UserManager(Application.application.ssoManager,Application.application.serverUrl);
             userManager.retrieveAssertion(
                     new mx.rpc.Responder(
                         function(event:ResultEvent):void
                         {
                             var name:String = XML(event.currentTarget.lastResult)..*::authenticatedUser.*::userid.text();
                             username.text = "Welcome "+name;
                         },
                         function(event:FaultEvent):void
                         {
                             mx.controls.Alert.show(event.fault.faultString,'Error')
                         }
                     )
                 );
 
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
 
                 // Set the docRefs url and referenceType parameters
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
                 token = EncryptDocument.invoke(params);
                 token.name = name;
             }
 
 
             // This method handles a successful conversion invocation
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
 
 
             private function resultHandler(event:ResultEvent):void {
             // Do anything else here.
 
             }
 
             private function logout():void
             {
                 Application.application.ssoManager.logout();
                 Application.application.showBusy();
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
                   id="username"/>
 
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
     <mx:Button label="Select File" click="uploadFile()" />
     <mx:Button label="Logout"  click="logout()" />
     </mx:Panel>
 </mx:Canvas>
 
 
```

### Informações adicionais {#additional-information}

As seções a seguir fornecem detalhes adicionais que descrevem a comunicação entre o aplicativo cliente e o servlet de segurança do Gerenciador de usuários.

### Uma nova autenticação ocorre {#a-new-authentication-occurs}

Nessa situação, o usuário tenta fazer logon de um aplicativo cliente para o AEM Forms pela primeira vez. (nenhuma sessão anterior envolvendo o usuário existe.) No `applicationComplete` evento, é chamado o `SSOManager.singleSignOn` método que envia uma solicitação para o Gerenciador de usuários.

`GET /um/login?um%5Fno%5Fredirect=true HTTP/1.1`

O servlet de segurança do Gerenciador de usuários responde com o seguinte valor:

`HTTP/1.1 200 OK`

`authenticated=false&authstate=CREDENTIAL_CHALLENGE`

Como resposta a esse valor, um `SSOEvent.AUTHENTICATION_REQUIRED` valor é despachado. Como resultado, o aplicativo cliente exibe uma tela de logon para o usuário. As credenciais são enviadas de volta ao servlet de segurança do Gerenciador de usuários.

`GET /um/login?um%5Fno%5Fredirect=true&j%5Fusername=administrator&j%5Fpassword=password HTTP/1.1`

O servlet de segurança do Gerenciador de usuários responde com o seguinte valor:

```as3
 HTTP/1.1 200 OK
 Set-Cookie: lcAuthToken=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A; Path=/
 authenticated=true&authstate=COMPLETE&assertionid=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

Como resultado, `authstate=COMPLETE the SSOEvent.AUTHENTICATION_SUCCESS` é despachado. O aplicativo cliente pode executar processamento adicional, se necessário. Por exemplo, um log que rastreia a data e a hora em que o usuário foi autenticado pode ser criado.

### O usuário já está autenticado {#the-user-is-already-authenticated}

Nessa situação, o usuário já fez logon no AEM Forms e, em seguida, navega para o aplicativo cliente. O aplicativo cliente se conecta ao servlet de segurança do Gerenciador de usuários durante a inicialização.

```as3
 GET /um/login?um%5Fno%5Fredirect=true HTTP/1.1
 Cookie: JSESSIONID=A4E0BCC2DD4BCCD3167C45FA350BD72A; lcAuthToken=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

Como o usuário já está autenticado, o cookie do Gerenciador de usuários está presente e é enviado para o servlet de segurança do Gerenciador de usuários. O servlet obtém o `assertionId` valor e verifica se é válido. Se for válido, então `authstate=COMPLETE` será retornado. Caso contrário, `authstate=CREDENTIAL_CHALLENGE` será retornado. A seguir está uma resposta típica:

```as3
 HTTP/1.1 200 OK
        authenticated=true&authstate=COMPLETE&assertionid=53630BC8-F6D4-F588-5D5B-4668EFB2EC7A
```

Nessa situação, o usuário não é exibido na tela de login e, em vez disso, é direcionado diretamente para uma tela de boas-vindas.
