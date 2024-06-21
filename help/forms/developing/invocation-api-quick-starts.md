---
title: Início Rápido da API de Chamada
description: Use os Quick Starts para chamar os serviços da AEM Forms de forma programática.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
exl-id: bee0eebb-c21d-472c-bbdf-28d8c3a5ed4a
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 3%

---

# Início Rápido da API de Chamada {#invocation-api-quick-starts}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

Os seguintes Quick Starts estão disponíveis para chamar programaticamente os serviços da AEM Forms:

<table>
 <thead>
  <tr>
   <th><p>Descrição</p></th>
   <th><p>API remota</p></th>
   <th><p>API Java</p></th>
   <th><p>API do serviço Web</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-human-centric-long-lived.md#invoking_human_centric_long_lived_processes">Chamar processos de longa vida centrados no ser humano</a></p></td>
   <td><p><a href="/help/forms/developing/invoking-human-centric-long-lived.md#invoking-a-long-lived-process-using-remoting">Chamar um processo de longa vida usando (obsoleto para formulários AEM) AEM Forms Remoting</a></p></td>
   <td><p><a href="/help/forms/developing/invoking-human-centric-long-lived.md#quick_start_invoking_a_long_lived_process_using_the_invocation_api">Início Rápido: Chamar um processo de longa duração usando a API de Chamada</a></p></td>
   <td><p><a href="/help/forms/developing/invoking-human-centric-long-lived.md#quick_start_invoking_a_long_lived_process_using_the_web_service_api">Início rápido: chamar um processo de longa duração usando a API do serviço da Web</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking_a_short_lived_process_using_the_invocation_api">Chamar um processo de vida curta usando a API de chamada</a></p></td>
   <td><p>N/A</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_short_lived_process_using_the_invocation_api">Início Rápido: Chamar um processo de vida curta usando a API de Chamada</a></p></td>
   <td><p>N/A</p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding">Chamada de AEM Forms usando codificação Base64</a> (Proxy de serviço Web Java)</p></td>
   <td><p>N/A</p></td>
   <td><p>N/A</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_java_proxy_files_and_base64_encoding">Início rápido: chamar um serviço usando arquivos proxy Java e codificação Base64</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding">Chamada de AEM Forms usando codificação Base64</a> (proxy do serviço Web .NET)</p></td>
   <td><p>N/A</p></td>
   <td><p>N/A</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_base64_in_a_microsoft_net_project">Início rápido: chamar um serviço usando base64 em um projeto Microsoft .NET</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom">Chamar o AEM Forms usando MTOM</a> ( exemplo de serviço Web .NET)</p></td>
   <td><p>N/A</p></td>
   <td><p>N/A</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_mtom_in_a_net_project">Início Rápido: Chamar um serviço usando MTOM em um projeto .NET</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref">Chamar o AEM Forms usando SwaRef</a> (Exemplo de serviço Web Java)</p></td>
   <td><p>N/A</p></td>
   <td><p>N/A</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_swaref_in_a_java_project">Início rápido: chamar um serviço usando SwaRef em um projeto Java</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http">Chamar o AEM Forms usando dados BLOB por HTTP</a> (Exemplo de serviço Web Java)</p></td>
   <td><p>N/A</p></td>
   <td><p>N/A</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_blob_data_over_http_in_a_net_project">Início Rápido: Chamar um serviço usando dados BLOB por HTTP em um projeto .NET</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http">Chamar o AEM Forms usando dados BLOB por HTTP</a> ( exemplo de serviço Web .NET)</p></td>
   <td><p>N/A</p></td>
   <td><p>N/A</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_blob_data_over_http_in_a_java_project">Início rápido: chamar um serviço usando dados BLOB por HTTP em um projeto Java</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime">Chamada de AEM Forms usando DIME</a> (Exemplo de serviço Web Java)</p></td>
   <td><p>N/A</p></td>
   <td><p>N/A</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_dime_in_a_java_project">Início rápido: chamar um serviço usando DIME em um projeto Java</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">Chamada do AEM Forms usando (obsoleto para o AEM formulários) AEM Forms Remoting</a></p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting">Início rápido: chamar um processo de vida curta transmitindo um documento não seguro usando o AEM Forms Remoting (obsoleto para formulários AEM)</a></p></td>
   <td><p>N/A</p></td>
   <td><p>N/A</p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#passing_secure_documents_to_invoke_processes_using_remoting">Enviar documentos seguros para invocar processos usando comunicação remota</a></p></td>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting">Início rápido: invocar um processo de vida curta transmitindo um documento seguro usando o AEM Forms Remoting (obsoleto para formulários AEM)</a></p></td>
   <td><p>N/A</p></td>
   <td><p>N/A</p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking_custom_component_services_using_remoting">Chamar serviços de componente personalizado usando Comunicação Remota</a></p></td>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#quick-start-invoking-the-customer-custom-service-using-remoting">Início rápido: chamar o serviço personalizado do cliente usando o (obsoleto para formulários AEM) AEM Forms Remoting</a></p></td>
   <td><p>N/A</p></td>
   <td><p>N/A</p></td>
  </tr>
 </tbody>
</table>

As operações do AEM Forms podem ser executadas usando a API altamente tipada do AEM Forms e o modo de conexão deve ser definido como SOAP.

>[!NOTE]
>
>Os Quick Starts na programação com formulários AEM são baseados no servidor do Forms que está sendo implantado no JBoss Application Server e no sistema operacional Microsoft Windows. No entanto, se você estiver usando outro sistema operacional, como o UNIX, substitua caminhos específicos do Windows por caminhos compatíveis com o sistema operacional aplicável. Da mesma forma, se estiver usando outro servidor de aplicações J2EE, certifique-se de especificar propriedades de conexão válidas. Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Início Rápido: Chamar um processo de vida curta usando a API de Chamada {#quick-start-invoking-a-short-lived-process-using-the-invocation-api}

O exemplo de código Java a seguir invoca um processo de vida curta chamado `MyApplication/EncryptDocument`. Observe que esse processo é chamado de forma síncrona. O parâmetro de entrada para esse processo é nomeado como `inDoc`. O parâmetro de saída desse processo é denominado `outDoc`. O documento PDF criptografado por senha é salvo como um arquivo PDF chamado `EncryptLoan.pdf`. (Consulte [Chamar um processo de vida curta usando a API de chamada](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-convertpdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. jacorb.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     * 7. jnp-client.jar (use a different JAR file if the Forms Server is not deployed on JBoss)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.io.InputStream;
 import java.util.HashMap;
 import java.util.Map;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.InvocationRequest;
 import com.adobe.idp.dsc.InvocationResponse;
 import com.adobe.idp.dsc.clientsdk.ServiceClient;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
     public class InvokeDocumentEncryptLooselyTypedAPI {
 
         public static void main(String[] args)
         {
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a ServiceClient object
             ServiceClient myServiceClient = factory.getServiceClient();
 
             //Create a Map object to store the parameter value
             Map params = new HashMap();
 
             InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
             Document inDoc = new Document(inFile);
 
             //Populate the Map object with a parameter value
             //required to invoke the MyApplication/EncryptDocument short-lived process
             //inDoc refers to the name of the input parameter for the process
             params.put("inDoc", inDoc);
 
             //Create an InvocationRequest object
             InvocationRequest request =  factory.createInvocationRequest(
                     "MyApplication/EncryptDocument",        //Specify the short-lived process name
                     "invoke",           //Specify the operation name
                     params,               //Specify input values
                     true);               //Create a synchronous request
 
             //Send the invocation request to the short-lived process and
             //get back an invocation response -- outDoc refers to the output parameter for the
             //MyApplication/EncryptDocument process
             InvocationResponse response = myServiceClient.invoke(request);
             Document encryptDoc = (Document) response.getOutputParameter("outDoc");
 
             //Save the encrypted PDF document returned by the process
             //Save the password-encrypted PDF document
             File outFile = new File("C:\\Adobe\EncryptLoan.pdf");
             encryptDoc.copyToFile (outFile);
             }catch (Exception e) {
                 e.printStackTrace();
             }
         }
 }
```

## Início rápido: chamar um serviço usando base64 em um projeto Microsoft .NET {#quick-start-invoking-a-service-using-base64-in-a-microsoft-net-project}

O código C# a seguir invoca um processo chamado `MyApplication/EncryptDocument` de um projeto Microsoft .NET usando a codificação Base64. (Consulte [Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

Um documento PDF não seguro baseado em um arquivo PDF chamado *Loan.pdf* é passado para o processo do AEM Forms. O processo retorna um documento PDF criptografado por senha que é salvo como um arquivo PDF chamado *PDF criptografado.pdf*.

```java
 /*
     * Ensure that you create a .NET client assembly that uses
     * base64 encoding. This is required to populate a BLOB
     * object with data or retrieve data from a BLOB object.
     *
     * For information, see "Invoking AEM Forms using Base64 Encoding" in
     * Programming with AEM forms
     */
 using System;
 using System.Collections;
 using System.ComponentModel;
 using System.Data;
 using System.IO;
 
 namespace InvokeEncryptDocumentBase64
 {
 
        class InvokeEncryptDocumentUsingBase64
        {
 
            const int BUFFER_SIZE = 4096;
            [STAThread]
            static void Main(string[] args)
            {
 
                try
                {
                    String pdfFile = "C:\\Adobe\Loan.pdf";
                    String encryptedPDF = "C:\\Adobe\EncryptedPDF.pdf";
 
 
                    //Create an MyApplication_EncryptDocumentService object and set authentication values
                    MyApplication2_EncryptDocumentService encryptClient = new MyApplication2_EncryptDocumentService();
                    encryptClient.Credentials = new System.Net.NetworkCredential("administrator", "password");
 
                    //Reference the PDF file to send to the EncryptDocument process
                    FileStream fs = new FileStream(pdfFile, FileMode.Open);
 
                    //Create a BLOB object
                    BLOB inDoc = new BLOB();
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    //Populate the byte array with the contents of the FileStream object
                    fs.Read(ByteArray, 0, len);
                    inDoc.binaryData = ByteArray;
 
                    //Invoke the EncryptDocument process
                    BLOB outDoc = encryptClient.invoke(inDoc);
 
                    //Populate a byte array with BLOB data
                    byte[] outByteArray = outDoc.binaryData;
 
                    //Create a file named UsageRightsLoan.pdf
                    FileStream fs2 = new FileStream(encryptedPDF, FileMode.OpenOrCreate);
 
                    //Create a BinaryWriter object
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(outByteArray);
                    w.Close();
                    fs2.Close();
                 }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
```

## Início rápido: chamar um serviço usando arquivos proxy Java e codificação Base64 {#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding}

O exemplo de código Java a seguir chama um processo chamado `MyApplication/EncryptDocument` usando arquivos proxy Java criados usando a codificação JAX-WS e Base64. (Consulte [Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

Um documento PDF não seguro baseado em um arquivo PDF chamado *Loan.pdf* é passado para o processo do AEM Forms. O processo retorna um documento PDF criptografado por senha que é salvo como um arquivo PDF chamado *EncryptedDocument.pdf*.

```java
 /**
     * Ensure that you create Java proxy files that consume
     *theAEM Forms service WSDL. You can use JAX-WS to create
     * the Java proxy files.
     *
     * This Java quick start uses Base64 to invoke a short-lived process named
     * EncryptDocument. For information, see
     * "Invoking AEM Forms using Base64" in Programming with AEM forms.
     */
 
 import java.io.*;
 
 import javax.xml.ws.BindingProvider;
 import com.adobe.idp.services.*;
 
 public class InvokeEncryptDocumentBase64 {
     public static void main(String[] args){
 
         try{
             //Create a MyApplicationEncryptDocument object
             MyApplicationEncryptDocumentService encClient = new MyApplicationEncryptDocumentService();
             MyApplicationEncryptDocument encryptDocClient = encClient.getEncryptDocument();
 
             //Set connection values required to invoke AEM Forms
             String url = "'[server]:[port]'/soap/services/MyApplication/EncryptDocument?blob=base64";
             String username = "administrator";
             String password = "password";
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
 
                // Get the input PDF document to send to the EncryptDocument process
                BLOB inDoc = new BLOB();
 
             // Get the input DDX document and input PDF sources
             File fileName = new File("C:\\Adobe\Loan.pdf");
             FileInputStream inFs = new FileInputStream(fileName);
 
             // Get the length of the file stream and create a byte array
             int inLen = (int)fileName.length();
             byte[] inByteArray = new byte[inLen];
 
                // Populate the byte array with the content of the file stream
             inFs.read(inByteArray, 0, inLen);
 
                // Populate the BLOB objects
             inDoc.setBinaryData(inByteArray);
 
                //invoke the short-lived process named MyApplication/EncryptDocument
             BLOB outDoc = encryptDocClient.invoke(inDoc);
 
             //Save the encrypted file as a PDF file
             byte[] encryptedDocument = outDoc.getBinaryData();
 
             //Create a File object
             File outFile = new File("C:\\Adobe\EncryptedDocument.pdf");
 
             //Create a FileOutputStream object.
             FileOutputStream myFileW = new FileOutputStream(outFile);
 
             //Call the FileOutputStream object's write method and pass the pdf data
             myFileW.write(encryptedDocument);
 
             //Close the FileOutputStream object
             myFileW.close();
                System.out.println("The short-lived process named MyApplication/EncryptDocument was successfully invoked.");
         }
         catch(Exception e)
         {
             e.printStackTrace();
         }
 
     }
 
 }
 
 
```

## Início rápido: chamar um processo de vida curta transmitindo um documento não seguro usando o AEM Forms Remoting (obsoleto para formulários AEM) {#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting}

O exemplo de código Flex a seguir invoca um processo de vida curta chamado `MyApplication/EncryptDocument`. (Consulte [Chamada do AEM Forms usando (obsoleto para o AEM formulários) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

>[!NOTE]
>
>Essa inicialização rápida invoca um processo do AEM Forms e carrega um documento não seguro. Para executar esse início rápido, o AEM Forms deve ser configurado para carregar documentos não seguros. Para obter informações sobre como configurar o AEM Forms para aceitar documentos não seguros, consulte [Configuração do AEM Forms para aceitar documentos protegidos e não protegidos](/help/forms/developing/invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  xmlns="*"
      creationComplete="initializeChannelSet();">
      <mx:Script>
        <![CDATA[
 
      import mx.rpc.AEM Forms.DocumentReference;
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
 
       // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var docRef:DocumentReference = new DocumentReference();
      private var parentResourcePath:String = "/";
      private var serverPort:String = "'[server]:[port]'";
      private var now1:Date;
      private  var cs:ChannelSet
 
      // Holds information returned from AEM Forms
      [Bindable]
      public var progressList:ArrayCollection = new ArrayCollection();
 
      // Set up channel set to invoke AEM Forms.
      // This must be done before calling any service or process, but only
      // once for the entire application.
       private function initializeChannelSet():void {
        cs = new ChannelSet();
        cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
        EncryptDocument.setCredentials("administrator", "password");
        EncryptDocument.channelSet = cs;
      }
 
      // Call this method to upload the file.
      // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process.
      private function uploadFile():void {
        fileRef.addEventListener(Event.SELECT, selectHandler);
        fileRef.browse();
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
             var request:URLRequest = DocumentReference.constructRequestForUpload("https://'[server]:[port]'", token);
 
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
        now1 = new Date();
 
        // Set the docRefs url and referenceType parameters
        docRef.url = event.data as String;
        docRef.referenceType=DocumentReference.REF_TYPE_URL;
        executeInvokeProcess();
      }
 
      //This method invokes the EncryptDocument process
      public function executeInvokeProcess():void {
 
         //Create an Object to store the input value for the EncryptDocument process
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
          progObject.link = "<a href=" + dr.url + "> open </a>";
          progressList.addItem(progObject);
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
        <mx:Button label="Select File" click="uploadFile()" />
      </mx:Panel>
 </mx:Application>
 
```

## Início Rápido: Chamar um serviço usando DIME em um projeto .NET {#quick-start-invoking-a-service-using-dime-in-a-net-project}

O código C# a seguir invoca um processo chamado `MyApplication/EncryptDocument` de um projeto Microsoft .NET usando Dime. (Consulte [Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

Um documento PDF não seguro baseado em um arquivo PDF chamado *map.pdf* é passado para o processo AEM Forms usando DIME. O processo retorna um documento PDF criptografado por senha que é salvo como um arquivo PDF chamado *mapEncrypt.pdf*.

```java
 /**
     *
     * Ensure that you create a .NET project that uses
     * Web Services Enhancements 2.0. This is required to send a
     * AEM Forms process an attachment using DIME.
     *
     * For information, see "Invoking AEM Forms using DIME" in Programming with AEM forms.
     */
 
 using System;
 using System.Collections;
 using System.ComponentModel;
 using System.Data;
 using System.IO;
 using Microsoft.Web.Services2.Dime;
 using Microsoft.Web.Services2.Attachments;
 using Microsoft.Web.Services2.Configuration;
 using Microsoft.Web.Services2;
 
 //The following statement represents a web reference to
 //the Forms Server that contains the process that
 //is invoked
 using ConsoleApplication1.LC_Host;
 
 namespace ConsoleApplication1
 {
 
      class InvokeEncryptDocumentUsingDime
        {
 
            const int BUFFER_SIZE = 4096;
            [STAThread]
            static void Main(string[] args)
            {
 
            try
               {
                   String pdfFile = "C:\\Adobe\map.pdf";
                   String encryptedPDF = "C:\\Adobe\mapEncrypt.pdf";
 
                   //Create an EncryptDocumentServiceWse object and set authentication values
                   EncryptDocumentServiceWse encryptClient = new EncryptDocumentServiceWse();
                   encryptClient.Credentials = new System.Net.NetworkCredential("administrator", "password");
 
                   // Create the DIME attachment representing a PDF document
                   DimeAttachment inputDocAttachment = new DimeAttachment(
                       System.Guid.NewGuid().ToString(),
                       "application/pdf",
                       TypeFormat.MediaType,
                       pdfFile);
 
                    //Create a BLOB object
                    BLOB inDoc = new BLOB();
 
                    //Set the DIME attachment ID
                    inDoc.attachmentID = inputDocAttachment.Id;
                    encryptClient.RequestSoapContext.Attachments.Add(inputDocAttachment);
 
                    //Invoke the EncryptDocument process
                    BLOB outDoc = encryptClient.invoke(inDoc);
 
                    //Get the returned attachment identifier value
                    String encryptedDocId = outDoc.attachmentID;
                    FileStream myStream = new FileStream(encryptedPDF, FileMode.Create, FileAccess.Write);
 
                    //Iterate through the attachments
                    foreach (Attachment attachment in encryptClient.ResponseSoapContext.Attachments)
                      {
                        if (attachment.Id.Equals(encryptedDocId))
                          {
                            //Create a byte array that contains the encrypted PDF document
                            System.IO.Stream mySteam2 = attachment.Stream;
                            byte[] myBytes = new byte[mySteam2.Length];
                            int size = (int)mySteam2.Length;
                            mySteam2.Read(myBytes, 0, size);
 
                            //Save the encrypted PDF document as a PDF file
                            FileStream fs2 = new FileStream(encryptedPDF, FileMode.OpenOrCreate);
 
                            //Create a BinaryWriter object
                            BinaryWriter w = new BinaryWriter(fs2);
                            w.Write(myBytes);
                            w.Close();
                            fs2.Close();
                            Console.Out.WriteLine("Saved converted document at:" + encryptedPDF);
                        }
                   }
                }
                catch (Exception ee)
               {
                   Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
```

## Início rápido: chamar um serviço usando DIME em um projeto Java {#quick-start-invoking-a-service-using-dime-in-a-java-project}

O exemplo de código Java a seguir chama um processo chamado `MyApplication/EncryptDocument` usando DIME. (Consulte [Chamada de AEM Forms usando DIME](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime).)

Um documento PDF não seguro baseado em um arquivo PDF chamado *Loan.pdf* é passado para o processo AEM Forms usando DIME. O processo retorna um documento PDF criptografado por senha que é salvo como um arquivo PDF chamado *EncryptLoan.pdf*.

```java
 /**
     * Ensure that you create Java Axis files that
     * are required to send a AEM Forms process
     * an attachment using DIME.
     *
     * For information, see "Invoking AEM Forms using DIME" in Programming with AEM forms.
     */
 import com.adobe.idp.services.*;
 import java.io.File;
 import java.io.FileOutputStream;
 import java.io.InputStream;
 import java.net.URL;
 import javax.activation.DataHandler;
 import javax.activation.FileDataSource;
 
 import org.apache.axis.attachments.AttachmentPart;
 
 public class InvokeDocumentEncryptDime {
     public static void main(String[] args) {
 
     try{
 
         //Create a MyApplicationEncryptDocumentServiceLocator object
         MyApplicationEncryptDocumentServiceLocator locate = new MyApplicationEncryptDocumentServiceLocator ();
 
         //specify the service target URL and object type
         URL serviceURL = new URL("https://'[server]:[port]'/soap/services/MyApplication/EncryptDocument?blob=dime");
 
         //Use the binding stub with the locator
         EncryptDocumentSoapBindingStub encryptionClientStub = new EncryptDocumentSoapBindingStub(serviceURL,locate);
         encryptionClientStub.setUsername("administrator");
         encryptionClientStub.setPassword("password");
 
          //Get the DIME Attachments - which is the PDF document to encrypt
          java.io.File file = new java.io.File("C:\\Adobe\Loan.pdf");
 
          //Create a DataHandler object
          DataHandler buildFile = new DataHandler(new FileDataSource(file));
 
          //Use the DataHandler object to create an AttachmentPart object
          AttachmentPart part = new AttachmentPart(buildFile);
         //get the attachment ID
         String attachmentID = part.getContentId();
 
         //Add the attachment to the encryption service stub
         encryptionClientStub.addAttachment(part);
 
         //Inform ES where the attachment is stored by providing the attachment id
         BLOB inDoc = new BLOB();
         inDoc.setAttachmentID(attachmentID);
 
         BLOB outDoc = encryptionClientStub.invoke(inDoc);
 
         //Go through the returned attachments and get the encrypted PDF document
         byte[] resultByte = null;
         attachmentID = outDoc.getAttachmentID();
 
         //Find the proper attachment
         Object[] parts = encryptionClientStub.getAttachments();
         for (int i=0;i<parts.length;i++){
             AttachmentPart attPart = (AttachmentPart)  parts[i];
             if (attPart.getContentId().equals(attachmentID)) {
                 //DataHandler
                 buildFile = attPart.getDataHandler();
                 InputStream stream = buildFile.getInputStream();
 
                 byte[] pdfStream = new byte[stream.available()];
                 stream.read(pdfStream);
 
                 //Create a File object
                 File outFile = new File("C:\\Adobe\EncryptLoan.pdf");
 
                 //Create a FileOutputStream object.
                 FileOutputStream myFileW = new FileOutputStream(outFile);
 
                 //Call the FileOutputStream object?s write method and pass the pdf data
                 myFileW.write(pdfStream);
 
                 //Close the FileOutputStream object
                 myFileW.close();
 
             }
         }
     }
     catch(Exception e)
     {
         e.printStackTrace();
     }
     }
 
 }
 
```

## Início rápido: chamar um serviço usando dados BLOB por HTTP em um projeto Java {#quick-start-invoking-a-service-using-blob-data-over-http-in-a-java-project}

O exemplo de código Java a seguir chama um processo chamado `MyApplication/EncryptDocument` uso de dados por HTTP. (Consulte [Chamar o AEM Forms usando dados BLOB por HTTP](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http).)

Um documento PDF não seguro baseado em um arquivo PDF chamado *Loan.pdf* é transmitido para o processo do AEM Forms usando SOAP por HTTP. O arquivo PDF está localizado no seguinte URL: `https://'[server]:[port]'/FormsQS`. O processo retorna um documento PDF criptografado por senha que é salvo como um arquivo PDF chamado *EncryptedDocument.pdf*.

```java
 /**
     * Ensure that you create Java proxy files that consume
     *theAEM Forms service WSDL. You can use JAX-WS to create
     * the Java proxy files.
     *
     * This Java quick start uses BLOB over HTTP to invoke a short-lived process named
     * EncryptDocument. For information, see
     * "Invoking AEM Forms using BLOB over HTTP" in Programming with AEM forms.
     */
 import java.io.*;
 import java.net.URL;
 
 import javax.xml.ws.BindingProvider;
 import com.adobe.idp.services.*;
 
 public class InvokeEncryptDocumentHTTP {
     public static void main(String[] args){
 
         try{
             //Create a MyApplicationEncryptDocument object
             MyApplicationEncryptDocumentService encClient = new MyApplicationEncryptDocumentService();
             MyApplicationEncryptDocument encryptDocClient = encClient.getEncryptDocument();
 
             //Set connection values required to invoke AEM Forms using BLOB over HTTP
             String url = "https://'[server]:[port]'/soap/services/MyApplication/EncryptDocument?blob=http";
             String username = "administrator";
             String password = "password";
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
 
             //Create a BLOB object and populate it by invoking the setRemoteURL method
             BLOB inDoc = new BLOB();
             inDoc.setRemoteURL("https://'[server]:[port]'/FormsQS/Loan.pdf");
 
                //invoke the short-lived process named MyApplication/EncryptDocument
             BLOB outDoc = encryptDocClient.invoke(inDoc);
 
             //Retrieve an InputStream from the returned BLOB instance
             URL myURL = new URL(outDoc.getRemoteURL());
             InputStream inputStream = myURL.openStream();
 
             //Create a file containing the returned PDF document
             File f = new File("C:\\Adobe\EncryptedDocument.pdf");
             OutputStream out = new FileOutputStream(f);
 
             //Iterate through the buffer
             byte buf[] = new byte[1024];
             int len;
             while ((len = inputStream.read(buf)) > 0)
                 out.write(buf, 0, len);
             out.close();
             inputStream.close();
 
              System.out.println("The short-lived process named EncryptDocument was successfully invoked.");
         }
         catch(Exception e)
         {
             e.printStackTrace();
         }
 
     }
 
 }
 
 
```

## Início Rápido: Chamar um serviço usando dados BLOB por HTTP em um projeto .NET {#quick-start-invoking-a-service-using-blob-data-over-http-in-a-net-project}

O código C# a seguir invoca um processo chamado `MyApplication/EncryptDocument` de um projeto Microsoft .NET usando dados por HTTP. (Consulte [Chamar o AEM Forms usando dados BLOB por HTTP](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http).)

Um documento PDF não seguro baseado em um arquivo PDF chamado *Loan.pdf* é transmitido para o processo AEM Forms usando BLOB sobre HTTP. O processo retorna um documento PDF criptografado por senha que é salvo como um arquivo PDF chamado *PDF criptografado.pdf*.

```java
 /*
     * Ensure that you create a .NET client assembly that uses
     * SOAP over HTTP. This is required to populate a BLOB
     * object’s remote URL data memeber.
     *
     * For information, see "Invoking AEM Forms using BLOB data over HTTP" in
     * Programming with AEM forms
     */
 using System;
 using System.Collections;
 using System.ComponentModel;
 using System.Data;
 using System.IO;
 using System.Security.Policy;
 
 namespace InvokeEncryptDocumentHTTP
 {
 
        class InvokeEncryptDocumentUsingHTTP
        {
 
            const int BUFFER_SIZE = 4096;
            [STAThread]
            static void Main(string[] args)
            {
 
                try
                {
                    String urlData = "https://'[server]:[port]'/FormsQS/Loan.pdf";
 
                    //Create a MyApplication_EncryptDocumentService object and set authentication values
                    MyApplication_EncryptDocumentService encryptClient = new MyApplication_EncryptDocumentService();
                    encryptClient.Credentials = new System.Net.NetworkCredential("administrator", "password");
 
                    //Create a BLOB object
                    BLOB inDoc = new BLOB();
 
                    //Populate the BLOB object’s remoteURL data member
                    inDoc.remoteURL = urlData;
 
                    //Invoke the EncryptDocument process
                    BLOB outDoc = encryptClient.invoke(inDoc);
 
                    //Create a UriBuilder object using the
                    //BLOB object’s remoteURL data member field
                    UriBuilder uri = new UriBuilder(outDoc.remoteURL);
 
                   //Convert the UriBuilder to a Stream object
                    System.Net.WebRequest wr = System.Net.WebRequest.Create(uri.Uri);
                    System.Net.WebResponse response = wr.GetResponse();
                    System.IO.StreamReader sr = new System.IO.StreamReader(response.GetResponseStream());
                    Stream mySteam = sr.BaseStream;
 
                    //Create a byte array
                    byte[] myData = new byte[BUFFER_SIZE];
 
                   //Populate the byte array
                   PopulateArray(mySteam, myData);
 
                   //Create a file named UsageRightsLoan.pdf
                   FileStream fs2 = new FileStream("C:\\Adobe\EncryptedPDF.pdf", FileMode.OpenOrCreate);
 
                   //Create a BinaryWriter object
                   BinaryWriter w = new BinaryWriter(fs2);
                   w.Write(myData);
                   w.Close();
                   fs2.Close();
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
 
            public static void PopulateArray(Stream stream, byte[] data)
            {
                int offset = 0;
                int remaining = data.Length;
                while (remaining > 0)
                {
                    int read = stream.Read(data, offset, remaining);
                    if (read <= 0)
                        throw new EndOfStreamException();
                    remaining -= read;
                    offset += read;
                }
            }
 
        }
 }
 
```

## Início Rápido: Chamar um serviço usando MTOM em um projeto .NET {#quick-start-invoking-a-service-using-mtom-in-a-net-project}

O código C# a seguir invoca um processo chamado `MyApplication/EncryptDocument` de um projeto Microsoft .NET usando MTOM. (Consulte [Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).)

Um documento PDF não seguro baseado em um arquivo PDF chamado *loan.pdf* é transmitido ao processo do AEM Forms usando MTOM. O processo retorna um documento PDF criptografado por senha que é salvo como um arquivo PDF chamado *EncryptedDocument.pdf*.

```java
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
     *
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms
     */
 using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;
 using System.ServiceModel;
 using EncryptDocumentMTOM.ServiceReference1;
 using System.IO;
 
 //Invoke the EncryptDocument process using MTOM
 namespace EncryptDocumentUsingMTOM
 {
        class Program
        {
            static void Main(string[] args)
            {
                try
                {
                    //Specify the name of the PDF file to encrypt
                    String pdfFile = "C:\\Adobe\loan.pdf";
 
                    //Create an EncryptDocumentClient object
                    MyApplication_EncryptDocumentClient encryptProcess = new MyApplication_EncryptDocumentClient();
                    encryptProcess.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://'[server]:[port]'/soap/services/MyApplication/EncryptDocument?blob=mtom");
                    BasicHttpBinding b = (BasicHttpBinding)encryptProcess.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
 
                    //Enable BASIC HTTP authentication
                    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
                    encryptProcess.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 4000000;
                    b.MaxBufferSize = 4000000;
                    b.ReaderQuotas.MaxArrayLength = 4000000;
 
                    //Reference the PDF file to send to the EncryptDocument process
                    FileStream fs = new FileStream(pdfFile, FileMode.Open);
 
                    //Create a BLOB object
                    BLOB inDoc = new BLOB();
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    //Populate the byte array with the contents of the FileStream object
                    fs.Read(ByteArray, 0, len);
                    inDoc.MTOM = ByteArray;
 
                    //Invoke the EncryptDocument short-lived process
                    BLOB outDoc = encryptProcess.invoke(inDoc);
                    byte[] encryptDoc = outDoc.MTOM;
 
                    //Create a file containing the encrypted PDF document
                    string FILE_NAME = "C:\\Adobe\EncryptedDocument.pdf";
                    FileStream fs2 = new FileStream(FILE_NAME, FileMode.OpenOrCreate);
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(encryptDoc);
                    w.Close();
                    fs2.Close();
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
```

>[!NOTE]
>
>Muitos inícios rápidos que mostram como executar operações de serviço do AEM Forms incluem um exemplo de código MTOM.

## Início rápido: chamar um serviço usando SwaRef em um projeto Java {#quick-start-invoking-a-service-using-swaref-in-a-java-project}

O exemplo de código Java a seguir chama um processo chamado `MyApplication/EncryptDocument` de um projeto Java. Este projeto Java usa classes de proxy que foram criadas usando JAX-WS e SwaRef como o tipo de codificação. (Consulte [Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref).)

Um documento PDF não seguro baseado em um arquivo PDF chamado *Loan.pdf* é transmitido para o processo AEM Forms usando SwaRef. O documento PDF criptografado é salvo como um arquivo PDF chamado *EncryptedDocument.pdf*.

```java
 /**
     * Ensure that you create Java proxy files that consume
     *theAEM Forms service WSDL. You can use JAX-WS to create
     * the Java proxy files.
     *
     * This Java quick start uses SwaRef to invoke a short-lived process named
     * EncryptDocument. For information, see
     * "Invoking AEM Forms using SwaRef" in Programming with AEM forms.
     */
 
 import javax.xml.ws.BindingProvider;
 import javax.activation.DataHandler;
 import javax.activation.DataSource;
 import javax.activation.FileDataSource;
 import java.io.*;
 
 import com.adobe.idp.services.*;
 
 public class InvokeEncryptDocumentSwaRef {
 
 public static void main(String[] args) {
 
         try{
 
         //Specify connection values required to invoke the MyApplication/EncryptDocument process
         //using SwaRef
         String url = "https://'[server]:[port]'/soap/services/MyApplication/EncryptDocument?blob=swaref";
         String username = "administrator";
         String password = "password";
         String pdfFile = "C:\\Adobe\Loan.pdf";
 
         //Create a MyApplicationEncryptDocument object
         MyApplicationEncryptDocumentService encClient = new MyApplicationEncryptDocumentService();
         MyApplicationEncryptDocument encryptDocClient = encClient.getEncryptDocument();
 
         ((BindingProvider)encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
         ((BindingProvider)encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
         ((BindingProvider)encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
 
          //Create a file object
          File pdf = new File(pdfFile);
 
          //Create a DataSource object
          DataSource myDS = new FileDataSource(pdf);
 
          //Create a DataHandler object
          DataHandler dataHandler = new DataHandler(myDS);
 
         //Create a BLOB object and populate it with the DataHandler
         BLOB inDoc = new BLOB();
         inDoc.setSwaRef(dataHandler);
 
         //Invoke the EncryptDocument process
         BLOB outDoc = encryptDocClient.invoke(inDoc);
 
         //Save the encrypted file as a PDF file
         DataHandler handler = outDoc.getSwaRef();
 
         //Create a file containing the returned PDF document
         File f = new File("C:\\Adobe\EncryptedDocument.pdf");
         InputStream inputStream = handler.getInputStream();
         OutputStream out = new FileOutputStream(f);
 
         //Iterate through the buffer
         byte buf[] = new byte[1024];
         int len;
         while ((len = inputStream.read(buf)) > 0)
             out.write(buf, 0, len);
         out.close();
         inputStream.close();
 
          System.out.println("The short-lived process named MyApplication/EncryptDocument was successfully invoked.");
 
         }catch (Exception e) {
              e.printStackTrace();
             }
         }
 }
 
 
```

>[!NOTE]
>
>Muitos inícios rápidos que mostram como executar operações de serviço incluem um exemplo de código SwaRef.
