---
title: Start rápidos da API do Forms Service
seo-title: Start rápidos da API do Forms Service
description: 'null'
seo-description: 'null'
uuid: dfce259a-e392-4929-ad7e-6d902faceaeb
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 9fe48243-24c6-4e08-9886-148cd99dec87
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Start rápidos da API do Forms Service {#forms-service-api-quick-starts}

Os seguintes Start rápidos estão disponíveis para o serviço de Formulários:

[Start rápido (modo SOAP): Como renderizar um formulário PDF interativo usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-interactive-pdf-form-using-the-java-api)

[Start rápido (modo SOAP): Como renderizar um formulário no cliente usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Start rápido (modo SOAP): Como renderizar um formulário com base em fragmentos usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[Start rápido (modo SOAP): Como renderizar um formulário habilitado para direitos usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Start rápido (modo SOAP): Como renderizar um formulário HTML usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Start rápido (modo SOAP): Como renderizar um formulário HTML com uma barra de ferramentas personalizada usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Start rápido (modo SOAP): Manuseio de formulários PDF enviados como XML usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Start rápido (modo SOAP): Como manipular formulários PDF enviados como PDF usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Start rápido (modo SOAP): Tratamento de formulários HTML enviados como XML usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Start rápido (modo SOAP): Criação de Documentos PDF com dados XML enviados usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api)

[Start rápido (modo SOAP): Pré-preenchimento de formulários com layouts flutuantes usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Start rápido (modo SOAP): Manuseio de um formulário contendo um script de cálculo usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-a-form-containing-a-calculation-script-using-the-java-api)

[Start rápido (modo SOAP): Otimização do desempenho usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[Start rápido (modo SOAP): Renderização por valor usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Start rápido (modo SOAP): Transmissão de documentos ao serviço de formulários usando a API Java](forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

A lógica do aplicativo que usa a API de serviço do Forms é implementada como servlets Java. As operações do AEM Forms podem ser executadas usando a AEM Forms fortemente tipada API e o modo de conexão deve ser definido como SOAP.

>[!NOTE]
>
>Os start rápidos localizados em Programação com v são baseados no servidor de formulários que está sendo usado por outro sistema operacional, como o Unix, e substituem caminhos específicos de janelas por caminhos suportados pelo sistema operacional aplicável. Da mesma forma, se você estiver usando outro servidor de aplicativos J2EE, certifique-se de especificar propriedades de conexão válidas. Consulte [Configuração de propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.

**Dica**: O site do Adobe Developer contém o seguinte artigo que discute como criar um aplicativo ASP.NET que chama o serviço Forms e renderiza formulários. Consulte [Criação de aplicativos](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)ASP.NET de renderização de formulário.

## Start rápido (modo SOAP): Como renderizar um formulário PDF interativo usando a API Java {#quick-start-soap-mode-rendering-an-interactive-pdf-form-using-the-java-api}

O exemplo de código a seguir renderiza um formulário PDF interativo chamado *Loan.xdp* para um navegador da Web do cliente. Um arquivo é anexado ao formulário. Observe que o design de formulário faz parte de um aplicativo e é referenciado usando o valor do URI raiz do conteúdo `repository:///`. (Consulte [Renderização de formulários](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)PDF interativos.)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms.
     */
 import java.io.FileInputStream;
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderPDFForm extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
 
             byte[]    cData = "".getBytes();
             Document oInputData = new Document(cData);
 
             //Set run-time options using a PDFFormRenderSpec instance
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
             pdfFormRenderSpec.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
             //Specify URI values that are required to render a form
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
             //Specify file attachments to attach to the form
             FileInputStream fileAttachment = new FileInputStream("C:\\rideau1.jpg");
             Document attachment1 = new Document(fileAttachment);
             String fileName = "rideau1.jpg";
             Map fileAttachments = new HashMap();
             fileAttachments.put(fileName, attachment1);
 
             //Invoke the renderPDFForm method and write the
             //results to a client web browser
             FormsResult formOut = formsClient.renderPDFForm(
                         formName,               //formQuery
                         oInputData,             //inDataDoc
                         pdfFormRenderSpec,      //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         fileAttachments            //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse objects content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
             }catch (Exception e) {
                  e.printStackTrace();
               }
         }
 }
```

## Start rápido (modo SOAP): Como renderizar um formulário no cliente usando a API Java {#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api}

O exemplo de código a seguir renderiza um formulário chamado *Loan.xdp* no cliente usando a API Java do serviço Forms. Observe que o design de formulário faz parte de um aplicativo e é referenciado usando o valor do URI raiz do conteúdo `repository:///`. (Consulte [Renderização de formulários no cliente](/help/forms/developing/rendering-forms.md#rendering-forms-at-the-client).)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms.
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderPDFFormClient extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
     try{
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a FormsServiceClient object
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
         //Set parameter values required by the renderPDFForm method
         String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
         byte[]    cData = "".getBytes();
         Document oInputData = new Document(cData);
 
         //Set a run-time option required to render a form on the client
         PDFFormRenderSpec pdfRenderSpec = new PDFFormRenderSpec();
         pdfRenderSpec.setRenderAtClient(RenderAtClient.Yes);
 
         //Specify URI values required to render a form
         URLSpec uriValues = new URLSpec();
         uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsServiceClientApp");
         uriValues.setContentRootURI("repository:///");
         uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
         //Invoke the renderPDFForm method to render
         //an interactive PDF form on the client
         FormsResult formOut = formsClient.renderPDFForm(
                 formName,
                 oInputData,
                 pdfRenderSpec,
                 uriValues,
                 null
             );
 
         //Create a Document object that stores form data
         Document myData = formOut.getOutputContent();
 
         //Get the content type of the response and
         //set the HttpServletResponse objects content type
         String contentType = myData.getContentType();
         resp.setContentType(contentType);
 
         //Create a ServletOutputStream object
         ServletOutputStream oOutput = resp.getOutputStream();
 
         //Create an InputStream object
         InputStream inputStream = myData.getInputStream();
 
         //Write the data stream to the web browser
         byte[] data = new byte[4096];
         int bytesRead = 0;
         while ((bytesRead = inputStream.read(data)) > 0)
         {
             oOutput.write(data, 0, bytesRead);
         }
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
          }
     }
 }
 
```

## Start rápido (modo SOAP): Renderização de um guia (obsoleto) usando a API Java {#quick-start-soap-mode-rendering-a-guide-deprecated-using-the-java-api}

O exemplo de código a seguir renderiza um Guia (obsoleto) chamado *TLALifeClaim.xdp* para um navegador da Web do cliente.

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import java.io.InputStream;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormGuide extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
     try{
 
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
         //Specify the parameters for the renderActivityGuide method
         String formName = "Applications/FormsApplication/1.0/FormsFolder/TLALifeClaim.xdp";
         byte[] cData = "".getBytes();
         Document oInputData = new Document(cData);
 
         //Cache the PDF form
         PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
         pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
         //Set Form Guide run-time options
         ActivityGuideRenderSpec renderSpec = new ActivityGuideRenderSpec();
         renderSpec.setGuidePDF(false);
 
         //Specify URI values that are required to render a form
         //design located in the AEM Forms repository
         URLSpec uriValues = new URLSpec();
         uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
         uriValues.setContentRootURI("repository:///");
         uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
 
         //Invoke the renderFormGuide method
         FormsResult formOut = formsClient.renderFormGuide(
                 formName,            //formQuery
                 oInputData,          //inDataDoc
                 pdfFormRenderSpec,    //pdfFormRenderSpec
                 renderSpec,           //activityGuideRenderSpec
                 uriValues              //urlSpec
                 );
 
         //Create a Document object that stores form data
         Document myData = formOut.getOutputContent();
 
         //Get the content type of the response
         String contentType = myData.getContentType();
         resp.setContentType(contentType);
 
         //Create a ServletOutputStream object
         ServletOutputStream oOutput = resp.getOutputStream();
 
         //Create an InputStream object
         InputStream inputStream = myData.getInputStream();
 
         //Write the data stream to the web browser
         byte[] data = new byte[4096];
         int bytesRead = 0;
         while ((bytesRead = inputStream.read(data)) > 0)
         {
             oOutput.write(data, 0, bytesRead);
         }
 
     }catch (Exception e) {
              System.out.println("The following exception occured: "+e.getMessage());
               }
      }
 }
 
```

## Start rápido (modo SOAP): Como renderizar um formulário com base em fragmentos usando a API Java {#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api}

O exemplo de código a seguir renderiza um formulário baseado em fragmentos. O nome do design de formulário é *PurchaseOrderDynamic.xdp* e está localizado no repositório AEM Forms (o arquivo XDP é armazenado em uma pasta chamada FormsFolder localizada no repositório). Além disso, os fragmentos aos quais o formulário POFragment faz referência também devem estar localizados no repositório. (Consulte [Renderização de formulários com base em fragmentos](/help/forms/developing/rendering-forms.md#rendering-forms-based-on-fragments).)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.FileInputStream;
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormFragments extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
 
     }
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
     throws ServletException, IOException {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/PurchaseOrderDynamic.xdp";
 
             FileInputStream myFormData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
             Document oInputData = new Document(myFormData);
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Specify URI values that are required to render a form
             //design based on fragments
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsServiceClientApp");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
             //Invoke the renderPDFForm method and write the
             //results to a client web browser
             FormsResult formOut = formsClient.renderPDFForm(
                         formName,               //formQuery
                         oInputData,             //inDataDoc
                         pdfFormRenderSpec,      //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         null                    //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object’s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
```

## Start rápido (modo SOAP): Como renderizar um formulário habilitado para direitos usando a API Java {#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api}

O exemplo de código a seguir renderiza um formulário habilitado para direitos em um navegador da Web do cliente. Os direitos de uso definidos neste exemplo de código permitem que um usuário adicione comentários no formulário e salve os dados do formulário. (Consulte [Renderizando Formulários](/help/forms/developing/rendering-forms.md#rendering-rights-enabled-forms)Ativados Por Direitos.)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class RenderUsageRightsForms extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
     try{
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a FormsServiceClient object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
         //Set parameter values for the renderPDFFormWithUsageRights method
         String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
         byte[]    cData = "".getBytes();
         Document oInputData = new Document(cData);
 
         //Set run-time options
         PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
         pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
         //Set usage-rights run-time options
         ReaderExtensionSpec reOptions = new ReaderExtensionSpec();
         reOptions.setReCredentialAlias("RE2");
         reOptions.setReCommenting(true);
         reOptions.setReFillIn(true);
 
         //Specify URI values required to render the form
         URLSpec uriValues = new URLSpec();
         uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
         uriValues.setContentRootURI("repository:///");
         uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
         //Render a rights-enabled PDF form
         FormsResult formOut = formsClient.renderPDFFormWithUsageRights(
             formName,            //formQuery
             oInputData,          //inDataDoc
             pdfFormRenderSpec,   //renderFormOptionsSpec
             reOptions,              //applicationWebRoot
             uriValues            //targetURL
             );
 
         //Create a Document object that stores form data
         Document myData = formOut.getOutputContent();
 
         //Get the content type of the response and
         //set the HttpServletResponse objects content type
         String contentType = myData.getContentType();
         resp.setContentType(contentType);
 
         //Create a ServletOutputStream object
         ServletOutputStream oOutput = resp.getOutputStream();
 
         //Create an InputStream object
         InputStream inputStream = myData.getInputStream();
 
         //Write the data stream to the web browser
         byte[] data = new byte[4096];
         int bytesRead = 0;
         while ((bytesRead = inputStream.read(data)) > 0)
         {
             oOutput.write(data, 0, bytesRead);
         }
 
     }catch (Exception e) {
          System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
 
 
```

## Start rápido (modo SOAP): Como renderizar um formulário HTML usando a API Java {#quick-start-soap-mode-rendering-an-html-form-using-the-java-api}

O exemplo de código a seguir renderiza um formulário HTML usando a API Java do serviço Forms. Uma barra de ferramentas é adicionada ao formulário HTML e dois anexos de arquivo. Além disso, o valor do agente do usuário é obtido do `HttpServletRequest` objeto. (Consulte [Renderizar formulários como HTML](/help/forms/developing/rendering-forms.md#rendering-forms-as-html).)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import java.io.FileInputStream;
 
 
 public class RenderHTMLForms extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
             try{
 
                 //Set connection properties required to invoke AEM Forms
                 Properties connectionProps = new Properties();
                 connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'");
                 connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");
                 connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss");
                 connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
                 connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");
 
                 //Create a FormsServiceClient object
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
                 FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
                 //Set parameter values for the (Deprecated) renderHTMLForm method
                 String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
                 byte[]    cData = "".getBytes();
                 Document oInputData = new Document(cData);
 
                 //Obtain the user agent value from the HttpServletRequest object
                 String userAgent = req.getHeader("user-agent");
 
                 //Create an HTMLRenderSpec object to store HTML run-time options
                 HTMLRenderSpec htmlRS = new HTMLRenderSpec();
                 htmlRS.setHTMLToolbar(HTMLToolbar.Vertical);
 
                 //Specify the locale value
                 htmlRS.setLocale("en_US");
 
                 //Render the HTML form within full HTML tags
                 htmlRS.setOutputType(OutputType.FullHTMLTags);
 
                 //Set style information that controls the presentation of the HTML form
                 htmlRS.setStyleGenerationLevel(StyleGenerationLevel.InlineAndInternalStyles);
 
                 //Specify URI values that are required to render a form
                 URLSpec uriValues = new URLSpec();
                 uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
                 uriValues.setContentRootURI("repository:///");
                 uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleSubmittedHTMLForm");
 
                 //Specify file attachments
                 FileInputStream myForm = new FileInputStream("C:\\Attach1.txt");
                 Document attachment1 = new Document(myForm);
                 FileInputStream myForm2 = new FileInputStream("C:\\Attach2.txt");
                 Document attachment2 = new Document(myForm2);
                 String fileName = "Attach1.txt";
                 String fileName2 = "Attach2.txt";
 
                 Map fileAttachments = new HashMap();
                 fileAttachments.put(fileName, attachment1);
                 fileAttachments.put(fileName2, attachment2);
 
                 //Invoke the (Deprecated) renderHTMLForm method
                 FormsResult formOut = formsClient.renderHTMLForm(
                     formName,               //formQuery
                     TransformTo.MSDHTML,    //transformTo
                     oInputData,             //inDataDoc
                     htmlRS,                    //renderHTMLSpec
                     userAgent,                //User Agent
                     uriValues,                //urlSpec
                     fileAttachments            //attachments
                     );
 
                 //Create a Document object that stores form data
                 Document myData = formOut.getOutputContent();
 
                 //Get the content type of the response and
                 //set the HttpServletResponse object’s content type
                 String contentType = myData.getContentType();
                 resp.setContentType(contentType);
 
                 //Create a ServletOutputStream object
                 ServletOutputStream oOutput = resp.getOutputStream();
 
                 //Create an InputStream object
                 InputStream inputStream = myData.getInputStream();
 
                 //Write the data stream to the web browser
                 byte[] data = new byte[4096];
                 int bytesRead = 0;
                 while ((bytesRead = inputStream.read(data)) > 0)
                 {
                     oOutput.write(data, 0, bytesRead);
                 }
 
                 }catch (Exception e) {
                      System.out.println("The following exception occurred: "+e.getMessage());
                      }
             }
 }
 
 
 
 
```

## Start rápido (modo SOAP): Renderização de um formulário HTML que usa um arquivo CSS usando a API Java {#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api}

O exemplo de código a seguir renderiza um formulário HTML usando a API do cliente do serviço Forms. O nome do arquivo CSS personalizado referenciado é *custom.css*. (Consulte [Renderização de formulários HTML usando arquivos](/help/forms/developing/rendering-forms.md#rendering-html-forms-using-custom-css-files)CSS personalizados.)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 import java.io.FileInputStream;
 
 
 public class RenderHTMLCSS extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
             try{
                 //Set connection properties required to invoke AEM Forms
                 Properties connectionProps = new Properties();
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
                 //Create a FormsServiceClient object
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
                 FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
                 //Set parameter values for the (Deprecated) renderHTMLForm method
                 String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
                 byte[]    cData = "".getBytes();
                 Document oInputData = new Document(cData);
                 String userAgent = "" ;
 
                 //Create an HTMLRenderSpec object to store HTML run-time options
                 HTMLRenderSpec htmlRS = new HTMLRenderSpec();
 
                 //Specify the locale value
                 htmlRS.setLocale("en_US");
 
                 //Specify a custom CSS file to use
                 htmlRS.setCustomCSSURI("C:\\Adobe\custom.css");
 
                 //Render the HTML form within full HTML tags
                 htmlRS.setOutputType(OutputType.FullHTMLTags);
 
                 //Specify URI values that are required to render a form
                 URLSpec uriValues = new URLSpec();
                 uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
                 uriValues.setContentRootURI("repository:///");
                 uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
                 //Specify file attachments
                 FileInputStream myForm = new FileInputStream("C:\\Attach1.txt");
                 Document attachment1 = new Document(myForm);
                 FileInputStream myForm2 = new FileInputStream("C:\\Attach2.txt");
                 Document attachment2 = new Document(myForm2);
                 String fileName = "Attach1.txt";
                 String fileName2 = "Attach2.txt";
 
                 Map fileAttachments = new HashMap();
                 fileAttachments.put(fileName, attachment1);
                 fileAttachments.put(fileName2, attachment2);
 
                 //Invoke the (Deprecated) renderHTMLForm method
                 FormsResult formOut = formsClient.renderHTMLForm(
                     formName,               //formQuery
                     TransformTo.MSDHTML,    //transformTo
                     oInputData,             //inDataDoc
                     htmlRS,                    //renderHTMLSpec
                     userAgent,                //User Agent
                     uriValues,                //urlSpec
                     fileAttachments            //attachments
                     );
 
                 //Create a Document object that stores form data
                 Document myData = formOut.getOutputContent();
 
                 //Get the content type of the response and
                 //set the HttpServletResponse object’s content type
                 String contentType = myData.getContentType();
                 resp.setContentType(contentType);
 
                 //Create a ServletOutputStream object
                 ServletOutputStream oOutput = resp.getOutputStream();
 
                 //Create an InputStream object
                 InputStream inputStream = myData.getInputStream();
 
                 //Write the data stream to the web browser
                 byte[] data = new byte[4096];
                 int bytesRead = 0;
                 while ((bytesRead = inputStream.read(data)) > 0)
                 {
                     oOutput.write(data, 0, bytesRead);
                 }
 
             }catch (Exception e) {
                      System.out.println("The following exception occurred: "+e.getMessage());
              }
     }
 }
```

## Start rápido (modo SOAP): Como renderizar um formulário HTML com uma barra de ferramentas personalizada usando a API Java {#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api}

O exemplo de código a seguir renderiza um formulário HTML com uma barra de ferramentas exibida em francês. O local do fscmenu.xml é C:\Adobe (essa pasta deve estar no servidor que hospeda os formulários AEM). Observe que o valor de localidade é `fr_FR`. A seção que discute como renderizar um formulário HTML com uma barra de ferramentas personalizada mostra a sintaxe do arquivo fscmenu.xml usada neste start rápido. (Consulte [Renderização de formulários HTML com barras de ferramentas](/help/forms/developing/rendering-forms.md#rendering-html-forms-with-custom-toolbars)personalizadas.)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import java.io.FileInputStream;
 
 
 public class RenderCustomToolbar extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
             try{
                 //Set connection properties required to invoke AEM Forms
                 Properties connectionProps = new Properties();
                 connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'");
                 connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");
                 connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss");
                 connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator");
                 connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password");
 
                 //Create a FormsServiceClient object
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
                 FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
                 //Set parameter values for the renderHTMLForm method
                 String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
                 byte[]    cData = "".getBytes();
                 Document oInputData = new Document(cData);
                 String userAgent = "" ;
 
                 //Create an HTMLRenderSpec object to store HTML run-time options
                 HTMLRenderSpec htmlRS = new HTMLRenderSpec();
                 htmlRS.setHTMLToolbar(HTMLToolbar.Vertical);
 
                 //Specify the URI location of the
                 // fscmenu.xml file that contains French
                 htmlRS.setToolbarURI("C:\\Adobe");
 
                 //Specify the locale value
                 htmlRS.setLocale("fr_FR");
 
                 //Render the HTML form within full HTML tags
                 htmlRS.setOutputType(OutputType.FullHTMLTags);
 
                 //Specify URI values that are required to render a form
                 URLSpec uriValues = new URLSpec();
                 uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
                 uriValues.setContentRootURI("repository:///");
                 uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
                 //Specify file attachments
                 FileInputStream myForm = new FileInputStream("C:\\Attach1.txt");
                 Document attachment1 = new Document(myForm);
                 FileInputStream myForm2 = new FileInputStream("C:\\Attach2.txt");
                 Document attachment2 = new Document(myForm2);
                 String fileName = "Attach1.txt";
                 String fileName2 = "Attach2.txt";
 
                 Map fileAttachments = new HashMap();
                 fileAttachments.put(fileName, attachment1);
                 fileAttachments.put(fileName2, attachment2);
 
                 //Invoke the renderHTMLForm method
                 FormsResult formOut = formsClient.renderHTMLForm(
                     formName,               //formQuery
                     TransformTo.MSDHTML,    //transformTo
                     oInputData,             //inDataDoc
                     htmlRS,                    //renderHTMLSpec
                     userAgent,                //User Agent
                     uriValues,                //urlSpec
                     fileAttachments            //attachments
                     );
 
                 //Create a Document object that stores form data
                 Document myData = formOut.getOutputContent();
 
                 //Get the content type of the response and
                 //set the HttpServletResponse object’s content type
                 String contentType = myData.getContentType();
                 resp.setContentType(contentType);
 
                 //Create a ServletOutputStream object
                 ServletOutputStream oOutput = resp.getOutputStream();
 
                 //Create an InputStream object
                 InputStream inputStream = myData.getInputStream();
 
                 //Write the data stream to the web browser
                 byte[] data = new byte[4096];
                 int bytesRead = 0;
                 while ((bytesRead = inputStream.read(data)) > 0)
                 {
                     oOutput.write(data, 0, bytesRead);
                 }
 
                 }catch (Exception e) {
                      System.out.println("The following exception occurred: "+e.getMessage());
                      }
             }
 }
 
```

## Start rápido (modo SOAP): Manuseio de formulários PDF enviados como XML usando a API Java {#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api}

O exemplo de código a seguir trata um formulário enviado como XML. O valor do tipo de conteúdo passado para o `processFormSubmission` método é `CONTENT_TYPE=text/xml`. Os valores que correspondem aos campos nomeados `mortgageAmount`, `lastName`e `firstName` são exibidos. Um método definido pelo usuário nomeado `getNodeText` é usado neste start rápido. Aceita uma `org.w3c.dom.Document` instância e um valor de string que especifica o nome do nó. Esse método retorna um valor de string que representa o valor do nó. (Consulte [Manuseio De Formulários](/help/forms/developing/rendering-forms.md#handling-submitted-forms)Enviados.)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 9. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.DataInputStream;
 import java.io.File;
 import java.io.InputStream;
 import java.io.PrintWriter;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 //Import DOM libraries
 import org.w3c.dom.NodeList;
 import org.w3c.dom.Node;
 import javax.xml.parsers.*;
 
 public class HandleData extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
                 doPost(req,resp);
         }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             PrintWriter pp = resp.getWriter();
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get Form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
              RenderOptionsSpec processSpec = new RenderOptionsSpec();
              processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,
             "CONTENT_TYPE=text/xml",
             "",
             processSpec);
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is ready to be processed
             //This code example checks only for submitted data (value is 0)
             if (processState == 0)
             {
               //Determine the content type of the data
               String myContentType = formOut.getContentType();
               System.out.println("THE CONTENT TYPS IS" +myContentType);
 
                if (myContentType.equals("application/vnd.adobe.xdp+xml"))    {
 
                 //Get the form data
                 Document formOutput = formOut.getOutputContent();
                 InputStream formInputStream = new DataInputStream(formOutput.getInputStream());
 
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
                 org.w3c.dom.Document myDOM = builder.parse(formInputStream);
 
                 //Call for each field in the form
                 String Amount = getNodeText("mortgageAmount", myDOM);
                 String myLastName =  getNodeText("lastName", myDOM);
                 String myFirstName = getNodeText("firstName", myDOM);
 
                 //Write the form data to the web browser
                 pp.println("<p> The form data is :<br><br>" +
                         "<li> The mortgage amount is "+ Amount+"" +
                         "<li> Last name is "+ myLastName+"" +
                         "<li> First name is "+ myFirstName+"")    ;
 
 
                 }
              }
             }
         catch (Exception e) {
              e.printStackTrace();
           }
     }
 
     //This method returns the value of the specified node
     private String getNodeText(String nodeName, org.w3c.dom.Document myDOM)
     {
       //Get the XML node by name
       NodeList oList = myDOM.getElementsByTagName(nodeName);
       Node myNode = oList.item(0);
       NodeList oChildNodes = myNode.getChildNodes();
 
      String sText = "";
      for (int i = 0; i < oChildNodes.getLength(); i++)
      {
          Node oItem = oChildNodes.item(i);
         if (oItem.getNodeType() == Node.TEXT_NODE)
          {
            sText = sText.concat(oItem.getNodeValue());
          }
      }
     return sText;
     }
 }
 
```

>[!NOTE]
>
>Ao usar um `com.adobe.idp.Document` objeto e um objeto `org.w3c.dom.Document` no mesmo aplicativo, qualifice-se totalmente `org.w3c.dom.Document`.

## Start rápido (modo SOAP): Como manipular formulários PDF enviados como PDF usando a API Java {#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api}

O exemplo de código a seguir trata um formulário enviado como dados PDF. O valor do tipo de conteúdo passado para o `processFormSubmission` método é `CONTENT_TYPE=application/pdf`. O formulário enviado é salvo como um arquivo PDF chamado *tempPDF.pdf*. Além disso, como o formulário é enviado como PDF, os anexos de arquivo podem ser recuperados. Todos os anexos de arquivo são salvos como arquivos JPEG. (Consulte [Manuseio De Formulários](/help/forms/developing/rendering-forms.md#handling-submitted-forms)Enviados.)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.DataInputStream;
 import java.io.File;
 import java.io.InputStream;
 import java.io.PrintWriter;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 //Import DOM libraries
 import org.w3c.dom.NodeList;
 import org.w3c.dom.Node;
 import javax.xml.parsers.*;
 
 public class HandleSubmittedPDFData extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
                 doPost(req,resp);
         }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             PrintWriter pp = resp.getWriter();
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get Form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
              RenderOptionsSpec processSpec = new RenderOptionsSpec();
              processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,
             "CONTENT_TYPE=application/pdf",
             "",
             processSpec);
 
             //Determine if the form contains file attachments
             //It is assumed that file attachments are JPG files
             List fileAttachments = formOut.getAttachments();
 
             //Create an Iterator object and iterate through
             //the List object
             Iterator iter = fileAttachments.iterator();
             int i = 0 ;
             while (iter.hasNext()) {
                 Document file = (Document)iter.next();
                 file.copyToFile(new File("C:\\Adobe\tempFile"+i+".jpg"));
                 i++;
             }
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is ready to be processed
             //This code example checks only for submitted data (value is 0)
             if (processState == 0)
             {
               //Determine the content type of the data
               String myContentType = formOut.getContentType();
 
               if (myContentType.equals("application/pdf")){
 
                     //Get the form data
                     Document myPDFfile = formOut.getOutputContent();
 
                     //Create a PDF object
                     File myPDFFile = new File("C:\\Adobe\tempPDF.pdf");
 
                     //Populate the PDF file
                     myPDFfile.copyToFile(myPDFFile);
                     pp.println("<p> The PDF file is saved as C:\\Adobe\tempPDF.pdf") ;
 
                 }
               }
         }
         catch (Exception e) {
              e.printStackTrace();
           }
     }
 
 }
 
 
 
```

## Start rápido (modo SOAP): Tratamento de formulários HTML enviados como XML usando a API Java {#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api}

O exemplo de código a seguir trata um formulário HTML enviado como dados XML. O valor do tipo de conteúdo passado para o `processFormSubmission` método é `CONTENT_TYPE=application/x-www-form-urlencoded`.Os valores que correspondem aos campos nomeados `mortgageAmount`, `lastName`e `firstName` são exibidos. Um método definido pelo usuário nomeado `getNodeText` é usado neste start rápido. Aceita uma `org.w3c.dom.Document` instância e um valor de string que especifica o nome do nó. Esse método retorna um valor de string que representa o valor do nó. (Consulte [Manuseio De Formulários](/help/forms/developing/rendering-forms.md#handling-submitted-forms)Enviados.)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.DataInputStream;
 import java.io.File;
 import java.io.InputStream;
 import java.io.PrintWriter;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 //Import DOM libraries
 import org.w3c.dom.NodeList;
 import org.w3c.dom.Node;
 import javax.xml.parsers.*;
 
 /*
     * This quick start handles data submitted as XML from a rendered HTML form
     */
 public class HandleSubmittedHTMLForm extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
                 doPost(req,resp);
         }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             PrintWriter pp = resp.getWriter();
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get Form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
              RenderOptionsSpec processSpec = new RenderOptionsSpec();
              processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,
             "CONTENT_TYPE=application/x-www-form-urlencoded",
             "",
             processSpec);
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is ready to be processed
             //This code example checks only for submitted data (value is 0)
             if (processState == 0)
             {
 
                     //Get the form data
                     Document formOutput = formOut.getOutputContent();
                     InputStream formInputStream = new DataInputStream(formOutput.getInputStream());
 
                     //Create DocumentBuilderFactory and DocumentBuilder objects
                     DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                     DocumentBuilder builder = factory.newDocumentBuilder();
                     org.w3c.dom.Document myDOM = builder.parse(formInputStream);
 
                     //Call for each field in the form
                     String Amount = getNodeText("mortgageAmount", myDOM);
                     String myLastName =  getNodeText("lastName", myDOM);
                     String myFirstName = getNodeText("firstName", myDOM);
 
                     //Write the form data to the web browser
                     pp.println("<p> The form data is :<br><br>" +
                             "<li> The mortgage amount is "+ Amount+"" +
                             "<li> Last name is "+ myLastName+"" +
                             "<li> First name is "+ myFirstName+"")    ;
                      }
                 }
             catch (Exception e) {
                  e.printStackTrace();
               }
         }
 
         //This method returns the value of the specified node
         private String getNodeText(String nodeName, org.w3c.dom.Document myDOM)
         {
           //Get the XML node by name
           NodeList oList = myDOM.getElementsByTagName(nodeName);
           Node myNode = oList.item(0);
           NodeList oChildNodes = myNode.getChildNodes();
 
          String sText = "";
          for (int i = 0; i < oChildNodes.getLength(); i++)
          {
              Node oItem = oChildNodes.item(i);
             if (oItem.getNodeType() == Node.TEXT_NODE)
              {
                sText = sText.concat(oItem.getNodeValue());
              }
          }
         return sText;
         }
     }
 
```

## Start rápido (modo SOAP): Criação de Documentos PDF com dados XML enviados usando a API Java {#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api}

O exemplo de código Java a seguir trata dados de formulário enviados como XML. Os dados do formulário são recuperados do envio do formulário usando a API de formulários e enviados para o serviço de Saída. Os dados do formulário e um design de formulário são usados para criar um documento PDF não interativo. O documento PDF não interativo é armazenado em um nó do Content Services (obsoleto) chamado `/Company Home/Test Directory`. O nome do formulário é criado dinamicamente. Ou seja, o nome e o sobrenome do usuário são usados para nomear o arquivo PDF. O identificador de recurso do novo conteúdo é gravado no navegador da Web do cliente. (Consulte [Criação de Documentos PDF com dados](/help/forms/developing/rendering-forms.md#creating-pdf-documents-with-submitted-xml-data)XML enviados.)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
     * 20. adobe-output-client.jar
     * 21. adobe-contentservices-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 
 import com.adobe.livecycle.contentservices.client.CRCResult;
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl;
 import com.adobe.livecycle.contentservices.client.impl.UpdateVersionType;
 import com.adobe.livecycle.formsservice.client.*;
 import com.adobe.livecycle.output.client.OutputClient;
 import com.adobe.livecycle.output.client.OutputResult;
 import com.adobe.livecycle.output.client.PDFOutputOptionsSpec;
 import com.adobe.livecycle.output.client.TransformationFormat;
 
 import java.util.*;
 import java.io.DataInputStream;
 import java.io.File;
 import java.io.InputStream;
 import java.io.PrintWriter;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.InvocationRequest;
 import com.adobe.idp.dsc.InvocationResponse;
 import com.adobe.idp.dsc.clientsdk.ServiceClient;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 //Import DOM libraries
 import org.w3c.dom.NodeList;
 import org.w3c.dom.Node;
 import javax.xml.parsers.*;
 
 public class HandleDataSendToOutput extends HttpServlet implements Servlet {
 
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
                 doPost(req,resp);
         }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             PrintWriter pp = resp.getWriter();
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get Form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
              RenderOptionsSpec processSpec = new RenderOptionsSpec();
              processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,
             "CONTENT_TYPE=text/xml",
             "",
             processSpec);
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is ready to be processed
             //This code example checks only for submitted data (value is 0)
             if (processState == 0)
             {
               //Determine the content type of the data
               String myContentType = formOut.getContentType();
 
               if (myContentType.equals("application/vnd.adobe.xdp+xml"))    {
 
                 //Get the form data
                 Document formOutput = formOut.getOutputContent();
                 InputStream formInputStream = new DataInputStream(formOutput.getInputStream());
 
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
                 org.w3c.dom.Document myDOM = builder.parse(formInputStream);
 
                 //Call for each field in the form
                 String Amount = getNodeText("mortgageAmount", myDOM);
                 String myLastName =  getNodeText("lastName", myDOM);
                 String myFirstName = getNodeText("firstName", myDOM);
 
                 //Write the form data to the web browser
                 pp.println("<p> The form data is :<br><br>" +
                         "<li> The mortgage amount is "+ Amount+"" +
                         "<li> Last name is "+ myLastName+"" +
                         "<li> First name is "+ myFirstName+"")    ;
 
 
                 //Create a non-interactive PDF document by invoking the Output service
                 Document myPDFform = GeneratePDFDocument(myFactory, formOutput);
 
                 //Create the name of the PDF file to store
                 String pdfName = "Loan_"+myLastName+"_"+myFirstName+".pdf" ;
                 String userName = myFirstName+" "+myLastName ;
 
                 //Store the PDF form into Content Services (deprecated)
                 String resourceID = StorePDFDocument(myFactory, myPDFform, pdfName,userName);
                 pp.println("<p> The pdf document was store in :<br><br>" +
                         "<li> /Company home "+
                         "<li> The identifier value of the new resource is "+ resourceID+"");
                   }
             }
         }
         catch (Exception e) {
              e.printStackTrace();
           }
     }
 
 
     //Store the PDF document in /Company Home/Test Directory using the
     //AEM Forms Content Service API
     private String StorePDFDocument(ServiceClientFactory myFactory, com.adobe.idp.Document pdfDoc, String formName, String userName)
     {
         try
         {
             //Create a DocumentManagementServiceClientImpl object
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);
 
             //Specify the store and node name
             String storeName ="SpacesStore";
             String nodeName = "/Company Home/Test Directory";
 
             //Create a MAP instance to store attributes
             Map<String,Object> inputs = new HashMap<String,Object>();
 
             //Specify attributes that belong to the new content
             String creator = "{https://www.alfresco.org/model/content/1.0}creator";
             String description = "{https://www.alfresco.org/model/content/1.0}description";
 
             inputs.put(creator,userName);
             inputs.put(description,"A mortgage application form");
 
             //Store MortgageForm.pdf in /Company Home/Test Directory
             CRCResult result = docManager.storeContent(storeName,
                      nodeName,
                      formName,
                     "{https://www.alfresco.org/model/content/1.0}content",
                     pdfDoc,
                     "UTF-8",
                     UpdateVersionType.INCREMENT_MAJOR_VERSION,
                     null,
                     inputs);
             //Get the identifier value of the new resource
             String id = result.getNodeUuid();
             return id;
     }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
         return null ;
     }
 
 
     //This method returns the value of the specified node
     private com.adobe.idp.Document GeneratePDFDocument(ServiceClientFactory myFactory, com.adobe.idp.Document formData)
     {
         try
         {
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Set PDF run-time options
         com.adobe.livecycle.output.client.PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setLocale("en_US");
 
         //Set rendering run-time options
         com.adobe.livecycle.output.client.RenderOptionsSpec pdfOptions = new com.adobe.livecycle.output.client.RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
 
         //Create a PDF document
         OutputResult outputDocument = outClient.generatePDFOutput(
             TransformationFormat.PDF,
             "Loan.xdp",
             "C:\\Adobe",
             outputOptions,
             pdfOptions,
             formData
         );
 
         //Get the Generated PDF file
         Document ouputDoc = outputDocument.getGeneratedDoc();
         return ouputDoc ;
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
         return null;
     }
 
     //This method returns the value of the specified node
     private String getNodeText(String nodeName, org.w3c.dom.Document myDOM)
     {
       //Get the XML node by name
       NodeList oList = myDOM.getElementsByTagName(nodeName);
       Node myNode = oList.item(0);
       NodeList oChildNodes = myNode.getChildNodes();
 
      String sText = "";
      for (int i = 0; i < oChildNodes.getLength(); i++)
      {
          Node oItem = oChildNodes.item(i);
         if (oItem.getNodeType() == Node.TEXT_NODE)
          {
            sText = sText.concat(oItem.getNodeValue());
          }
      }
     return sText;
     }
 }
```

## Start rápido (modo SOAP): Pré-preenchimento de formulários com layouts flutuantes usando a API Java {#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api}

O exemplo de código a seguir pré-preenche um formulário com uma fonte de dados dinâmica. Ou seja, a fonte de dados é criada em tempo de execução e não está contida em um arquivo XML ou criada durante o tempo de design. Este exemplo de código contém três métodos definidos pelo usuário:

* `createDataSource`: Cria um `org.w3c.dom.Document` objeto que representa a fonte de dados usada para pré-preencher o formulário. Esse método definido pelo usuário retorna o `org.w3c.dom.Document` objeto.
* `convertDataSource`: Converte um `org.w3c.dom.Document` objeto em um `com.adobe.idp.Document` objeto. Esse método aceita um `org.w3c.dom.Document` objeto como parâmetro de entrada e retorna um `com.adobe.idp.Document` objeto.
* `renderPOForm`: Usa a API Java do serviço Forms para renderizar um formulário de pedido de compra dinâmico. O `com.adobe.idp.Document` objeto retornado pelo `convertDataSource` método é usado para pré-preencher o formulário.

   Todos esses métodos são chamados de dentro do `doPost` método do servlet Java. (Consulte [Pré-preenchimento de formulários com layouts](/help/forms/developing/rendering-forms.md#prepopulating-forms-with-flowable-layouts)flutuantes.)

```java
/*
* This Java Quick Start uses the following JAR files
* 1. adobe-forms-client.jar
* 2. adobe-livecycle-client.jar
* 3. adobe-usermanager-client.jar
* 4. activation.jar (required for SOAP mode)
* 5. axis.jar (required for SOAP mode)
* 6. commons-codec-1.3.jar (required for SOAP mode)
* 7. commons-collections-3.2.jar (required for SOAP mode)
* 8. commons-discovery.jar (required for SOAP mode)
* 9. commons-logging.jar (required for SOAP mode)
* 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
* 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
* 12. jaxrpc.jar (required for SOAP mode)
* 13. log4j.jar (required for SOAP mode)
* 14. mail.jar (required for SOAP mode)
* 15. saaj.jar (required for SOAP mode)
* 16. wsdl4j.jar (required for SOAP mode)
* 17. xalan.jar (required for SOAP mode)
* 18. xbean.jar (required for SOAP mode)
* 19. xercesImpl.jar (required for SOAP mode)
*
* (Because Forms quick starts are implemented as Java servlets, it is
* not necessary to include J2EE specific JAR files - the Java project
* that contains this quick start is exported as a WAR file which
* is deployed to the J2EE application server)
*
* These JAR files are located in the following path:
* <install directory>/sdk/client-libs/common
*
* For complete details about the location of these JAR files,
* see "Including AEM Forms library files" in Programming with AEM forms
*/
import java.io.IOException;
import javax.servlet.Servlet;
import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import com.adobe.livecycle.formsservice.client. * ;
import java.util. * ;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import org.w3c.dom.Element;
import javax.xml.parsers. * ;
import javax.xml.transform. * ;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;
public class RenderDynamicForm extends HttpServlet implements Servlet {
 public void doGet(HttpServletRequest req, HttpServletResponse resp)
 throws ServletException,
 IOException {
  doPost(req, resp);
 }
 public void doPost(HttpServletRequest req, HttpServletResponse resp)
 throws ServletException,
 IOException {
  //Render a dynamic purchase order form
  //Create an org.w3c.dom.Document object
  org.w3c.dom.Document myDom = createDataSource();
  //Convert the org.w3c.dom.Document object
  //to a com.adobe.idp.Document object
  com.adobe.idp.Document formData = convertDataSource(myDom);
  //Render the dynamic form using data located within the
  //com.adobe.idp.Document object
  renderPOForm(resp, formData);
 }
 //Creates an org.w3c.dom.Document object
 private org.w3c.dom.Document createDataSource() {
  org.w3c.dom.Document document = null;
  try {
   //Create DocumentBuilderFactory and DocumentBuilder objects
   DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
   DocumentBuilder builder = factory.newDocumentBuilder();
   //Create a new Document object
   document = builder.newDocument();
   //Create the root element and append it to the XML DOM
   Element root = (Element) document.createElement("transaction");
   document.appendChild(root);
   //Create the header element
   Element header = (Element) document.createElement("header");
   root.appendChild(header);
   //Create the txtPONum element and append it to the
   //header element
   Element txtPONum = (Element) document.createElement("txtPONum");
   txtPONum.appendChild(document.createTextNode("8745236985"));
   header.appendChild(txtPONum);
   //Create the dtmDate element and append it to the
   //header element
   Element dtmDate = (Element) document.createElement("dtmDate");
   dtmDate.appendChild(document.createTextNode("2007-02-08"));
   header.appendChild(dtmDate);
   //Create the orderedByAddress element and append
   //it to the header element
   Element orderedByAddress = (Element) document.createElement("orderedByAddress");
   orderedByAddress.appendChild(document.createTextNode("222, Any Blvd"));
   header.appendChild(orderedByAddress);
   //Create the txtOrderedByPhone element and append
   //it to the header element
   Element txtOrderedByPhone = (Element) document.createElement("txtOrderedByPhone");
   txtOrderedByPhone.appendChild(document.createTextNode("(555) 555-2334"));
   header.appendChild(txtOrderedByPhone);
   //Create the txtOrderedByFax element and append
   //it to the header element
   Element txtOrderedByFax = (Element) document.createElement("txtOrderedByFax");
   txtOrderedByFax.appendChild(document.createTextNode("(555) 555-9334"));
   header.appendChild(txtOrderedByFax);
   //Create the txtOrderedByContactName element and append
   //it to the header element
   Element txtOrderedByContactName = (Element) document.createElement("txtOrderedByContactName");
   txtOrderedByContactName.appendChild(document.createTextNode("Frank Jones"));
   header.appendChild(txtOrderedByContactName);
   //Create the deliverToAddress element and append
   //it to the header element
   Element deliverToAddress = (Element) document.createElement("deliverToAddress");
   deliverToAddress.appendChild(document.createTextNode("555, Any Blvd"));
   header.appendChild(deliverToAddress);
   //Create the txtDeliverToPhone element and append
   //it to the header element
   Element txtDeliverToPhone = (Element) document.createElement("txtDeliverToPhone");
   txtDeliverToPhone.appendChild(document.createTextNode("(555) 555-9098"));
   header.appendChild(txtDeliverToPhone);
   //Create the txtDeliverToFax element and append
   //it to the header element
   Element txtDeliverToFax = (Element) document.createElement("txtDeliverToFax");
   txtDeliverToFax.appendChild(document.createTextNode("(555) 555-9000"));
   header.appendChild(txtDeliverToFax);
   //Create the txtDeliverToContactName element and
   //append it to the header element
   Element txtDeliverToContactName = (Element) document.createElement("txtDeliverToContactName");
   txtDeliverToContactName.appendChild(document.createTextNode("Jerry Johnson"));
   header.appendChild(txtDeliverToContactName);
   //Create the detail element and append it to the root
   Element detail = (Element) document.createElement("detail");
   root.appendChild(detail);

   //Create the txtPartNum element and append it to the
   //detail element
   Element txtPartNum = (Element) document.createElement("txtPartNum");
   txtPartNum.appendChild(document.createTextNode("00010-100"));
   detail.appendChild(txtPartNum);
   //Create the txtDescription element and append it
   //to the detail element
   Element txtDescription = (Element) document.createElement("txtDescription");
   txtDescription.appendChild(document.createTextNode("Monitor"));
   detail.appendChild(txtDescription);
   //Create the numQty element and append it to
   //the detail element
   Element numQty = (Element) document.createElement("numQty");
   numQty.appendChild(document.createTextNode("1"));
   detail.appendChild(numQty);
   //Create the numUnitPrice element and append it
   //to the detail element
   Element numUnitPrice = (Element) document.createElement("numUnitPrice");
   numUnitPrice.appendChild(document.createTextNode("350.00"));
   detail.appendChild(numUnitPrice);
   //Create another detail element named detail2 and
   //append it to root
   Element detail2 = (Element) document.createElement("detail");
   root.appendChild(detail2);
   //Create the txtPartNum element and append it to the
   //detail2 element
   Element txtPartNum2 = (Element) document.createElement("txtPartNum");
   txtPartNum2.appendChild(document.createTextNode("00010-200"));
   detail2.appendChild(txtPartNum2);
   //Create the txtDescription element and append it
   //to the detail2 element
   Element txtDescription2 = (Element) document.createElement("txtDescription");
   txtDescription2.appendChild(document.createTextNode("Desk lamps"));
   detail2.appendChild(txtDescription2);
   //Create the numQty element and append it to the
   //detail2 element
   Element numQty2 = (Element) document.createElement("numQty");
   numQty2.appendChild(document.createTextNode("3"));
   detail2.appendChild(numQty2);
   //Create the NUMUNITPRICE element
   Element numUnitPrice2 = (Element) document.createElement("numUnitPrice");
   numUnitPrice2.appendChild(document.createTextNode("55.00"));
   detail2.appendChild(numUnitPrice2);
  }
  catch(Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
  return document;

 }
 //Converts an org.w3c.dom.Document object to a
 //com.adobe.idp.Document object
 private Document convertDataSource(org.w3c.dom.Document myDOM) {
  byte[] mybytes = null;
  try {
   //Create a Java Transformer object
   TransformerFactory transFact = TransformerFactory.newInstance();
   Transformer transForm = transFact.newTransformer();
   //Create a Java ByteArrayOutputStream object
   ByteArrayOutputStream myOutStream = new ByteArrayOutputStream();
   //Create a Java Source object
   javax.xml.transform.dom.DOMSource myInput = new DOMSource(myDOM);
   //Create a Java Result object
   javax.xml.transform.stream.StreamResult myOutput = new StreamResult(myOutStream);
   //Populate the Java ByteArrayOutputStream object
   transForm.transform(myInput, myOutput);
   // Get the size of the ByteArrayOutputStream buffer
   int myByteSize = myOutStream.size();
   //Allocate myByteSize to the byte array
   mybytes = new byte[myByteSize];
   //Copy the content to the byte array
   mybytes = myOutStream.toByteArray();
  }
  catch(Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
  //Create a com.adobe.idp.Document object and copy the
  //contents of the byte array
  Document myDocument = new Document(mybytes);
  return myDocument;
 }
 //Render the purchase order form using the specified
 //com.adobe.idp.Document object
 private void renderPOForm(HttpServletResponse resp, Document formData) {
  try {
   //Set connection properties required to invoke AEM Forms
   Properties connectionProps = new Properties();
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceC
   lientFactoryProperties.DSC_SOAP_PROTOCOL);
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
   //Create a ServiceClientFactory object
   ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
   //Create a FormsServiceClient object
   FormsServiceClient formsClient = new FormsServiceClient(myFactory);
   //Set the parameter values for the renderPDFForm method
   String formName = "Applications/FormsApplication/1.0/FormsFolder/PO.xdp";
   //Cache the form
   PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
   pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
   //Specify URI values that are required to render a form
   URLSpec uriValues = new URLSpec();
   uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
   uriValues.setContentRootURI("repository:///");
   uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
   //Invoke the renderForm method
   FormsResult formOut = formsClient.renderPDFForm(
   formName, //formQuery
   formData, //inDataDoc
   pdfFormRenderSpec, //PDFFormRenderSpec
   uriValues, //urlSpec
   null //attachments
   );
   //Create a ServletOutputStream object
   ServletOutputStream oOutput = resp.getOutputStream();
   //Create a Document object that stores form data
   Document myData = formOut.getOutputContent();
   //Create an InputStream object
   InputStream inputStream = myData.getInputStream();
   //Write the data stream to the web browser
   byte[] data = new byte[4096];
   int bytesRead = 0;
   while ((bytesRead = inputStream.read(data)) > 0) {
    oOutput.write(data, 0, bytesRead);
   }
  } catch(Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
 }
}
```

## Start rápido (modo SOAP): Manuseio de um formulário contendo um script de cálculo usando a API Java {#quick-start-soap-mode-handling-a-form-containing-a-calculation-script-using-the-java-api}

O exemplo de código a seguir processa um formulário que contém um script de cálculo e grava os resultados de volta no navegador da Web do cliente. (Consulte [Calculando dados](/help/forms/developing/rendering-forms.md#calculating-form-data)do formulário.)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class CalculateData extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Get form data to pass to the processFormSubmission method
             Document formData = new Document(req.getInputStream());
 
             //Set run-time options
             RenderOptionsSpec processSpec = new RenderOptionsSpec();
             processSpec.setLocale("en_US");
 
             //Invoke the processFormSubmission method
             FormsResult formOut = formsClient.processFormSubmission(formData,"CONTENT_TYPE=application/pdf&CONTENT_TYPE=application/vnd.adobe.xdp+xml","",processSpec);
 
             //Get the processing state
             short processState = formOut.getAction();
 
             //Determine if the form data is calculated
             if (processState == 1)
             {
 
                 //Write the data back to to the client web browser
                 ServletOutputStream oOutput = resp.getOutputStream();
                 Document calData = formOut.getOutputContent();
 
                 //Create an InputStream object
                 InputStream inputStream = calData.getInputStream();
 
                 //Write the data stream to the web browser
                 byte[] data = new byte[4096];
                 int bytesRead = 0;
                 while ((bytesRead = inputStream.read(data)) > 0)
                 {
                     oOutput.write(data, 0, bytesRead);
                 }
              }
             }
         catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
         }
     }
 }
```

## Start rápido (modo SOAP): Otimização do desempenho usando a API Java {#quick-start-soap-mode-optimizing-performance-using-the-java-api}

O exemplo de código a seguir otimiza o desempenho ao configurar as opções de cache, independente e linearizada. Um arquivo linearizado é otimizado para delivery na Web. (Consulte [Otimizando o desempenho do serviço](/help/forms/developing/rendering-forms.md#optimizing-the-performance-of-the-forms-service)de formulários.)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormsPerformance extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
     try{
 
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a FormsServiceClient object
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
         //Set the parameter values for the renderForm method
         String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
         byte[]    cData = "".getBytes();
         Document oInputData = new Document(cData);
 
         //Set performance run-time options
         PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
         renderSpec.setCacheEnabled(new Boolean(true));
         renderSpec.setLinearizedPDF(true);
 
         //Specify URI values that are required to render a form
         //design located in the AEM Forms Repository
         URLSpec uriValues = new URLSpec();
         uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsServiceClientApp");
         uriValues.setContentRootURI("repository:///");
         uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
         //Invoke the renderPDFForm method and write the
         //results to a client web browser
         FormsResult formOut = formsClient.renderPDFForm(
                     formName,       //formQuery
                     oInputData,     //inDataDoc
                     renderSpec,     //PDFFormRenderSpec
                     uriValues,        //urlSpec
                     null            //attachments
                     );
 
         //Create a ServletOutputStream object
         ServletOutputStream oOutput = resp.getOutputStream();
 
         //Create a Document object that stores form data
         Document myData = formOut.getOutputContent();
 
         //Create an InputStream object
         InputStream inputStream = myData.getInputStream();
 
         //Write the data stream to the web browser
         byte[] data = new byte[4096];
         int bytesRead = 0;
         while ((bytesRead = inputStream.read(data)) > 0)
         {
             oOutput.write(data, 0, bytesRead);
         }
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
```

## Start rápido (modo SOAP): Renderização por valor usando a API Java {#quick-start-soap-mode-rendering-by-value-using-the-java-api}

O start rápido do Java a seguir renderiza um formulário PDF interativo com base em um design de formulário chamado *Loan.xdp* por valor. Observe que o design de formulário é usado para preencher um `com.adobe.idp.Document` objeto chamado *inputXDP*. (Consulte [Renderizando Formulários Por Valor](/help/forms/developing/rendering-forms.md#rendering-forms-by-value).)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
    *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms.
     */
 import java.io.FileInputStream;
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderByValue extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Retrieve the form design
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xdp");
             Document inputXDP = new Document(fileInputStream);
 
             //Specify URI values that are required to render a form
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/FormsQS");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsQS/HandleData");
 
             //Invoke the renderPDFForm method and pass the
             //form design by value
             FormsResult formOut = formsClient.renderPDFForm(
                         "",                     //formQuery
                         inputXDP,                 //inDataDoc
                         new PDFFormRenderSpec(), //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         null                    //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object?s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
             }catch (Exception e) {
                  e.printStackTrace();
               }
         }
 }
```

## Start rápido (modo SOAP): Transmissão de documentos ao serviço de formulários usando a API Java {#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api}

O seguinte start rápido do Java recupera o arquivo Loan.xdp do Content Services (obsoleto). Este arquivo XDP está localizado no espaço `/Company Home/Form Designs`. O arquivo XDP é retornado em uma `com.adobe.idp.Document` instância. A `com.adobe.idp.Document` instância é passada para o serviço Forms. O formulário interativo é gravado em um navegador da Web do cliente. (Consulte [Transmissão de Documentos ao serviço](/help/forms/developing/passing-documents-forms-service.md)de formulários.)

```as3
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-contentservices-client.jar
     * 3. adobe-livecycle-client.jar
     * 4. adobe-usermanager-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms.
     */
 import java.io.IOException;
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 
 import com.adobe.livecycle.contentservices.client.CRCResult;
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl;
 import com.adobe.livecycle.formsservice.client.*;
 
 import java.util.*;
 import java.io.InputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormsFromContentServices extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
     }
 
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Create an empty Document that represents form data
             byte[]    cData = "".getBytes();
             Document oInputData = new Document(cData);
 
             //Get the form design from Content Services (deprecated)
             Document formDesign =  GetFormDesign(myFactory);
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Invoke the renderPDFForm2 and pass to the
             //Document that contains the form design
             FormsResult formOut = formsClient.renderPDFForm2(
                     formDesign,
                     oInputData,
                     pdfFormRenderSpec,
                     null,
                     null
                     );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object?s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
             }catch (Exception e) {
                  e.printStackTrace();
               }
         }
 
     //Retrieve the form design from Content Services (deprecated)
     private Document GetFormDesign(ServiceClientFactory myFactory)
     {
         try{
 
         //Create a DocumentManagementServiceClientImpl object
         DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);
 
         //Specify the name of the store and the content to retrieve
            String storeName = "SpacesStore";
            String nodeName  = "/Company Home/Form Designs/Loan.xdp";
 
            //Retrieve /Company Home/Form Designs/Loan.xdp
            CRCResult content = docManager.retrieveContent(
                      storeName,
                      nodeName,
                      "");
 
            //Return the Document instance
             Document doc =content.getDocument();
             return  doc;
          }
 
         catch(Exception e)
         {
             e.printStackTrace();
         }
         return null;
     }
 
 }
 
```

