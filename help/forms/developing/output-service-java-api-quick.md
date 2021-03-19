---
title: Início rápido da API Java do Serviço de Saída (SOAP)
seo-title: Início rápido da API Java do Serviço de Saída (SOAP)
description: Use o SOAP (Java API Quick Start) do serviço de saída para criar um documento PDF, criar um documento PDF com base no arquivo XDP do aplicativo, criar um documento PDF/A, enviar documentos para o serviço de saída, passar um documento localizado no repositório AEM Forms para o serviço de saída, criar um documento PDF com base em fragmentos, imprimir em um arquivo, enviar um fluxo de impressão para uma impressora de rede, criar vários arquivos PDF, criar regras de pesquisa, transformar um documento PDF.
seo-description: Use o SOAP (Java API Quick Start) do serviço de saída para criar um documento PDF, criar um documento PDF com base no arquivo XDP do aplicativo, criar um documento PDF/A, enviar documentos para o serviço de saída, passar um documento localizado no repositório AEM Forms para o serviço de saída, criar um documento PDF com base em fragmentos, imprimir em um arquivo, enviar um fluxo de impressão para uma impressora de rede, criar vários arquivos PDF, criar regras de pesquisa, transformar um documento PDF.
uuid: 34cb1fc7-50a9-4db8-aed1-dbd3480d1323
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f4415aeb-5c1b-4087-b60f-b2ea952c52b5
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 0%

---


# Início rápido da API Java do Serviço de saída (SOAP) {#output-service-java-api-quick-start-soap}

O Java API Quick Start (SOAP) está disponível para o serviço de Saída.

[Início rápido (modo SOAP): Criação de um documento PDF usando a API do Java](output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Início rápido (modo SOAP): Criação de um documento PDF com base em um arquivo XDP do aplicativo usando a API Java](output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)

[Início rápido (modo SOAP): Criação de um documento PDF/A usando a API do Java](output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[Início rápido (modo SOAP): Passar documentos para o serviço de saída usando a API Java](output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Início rápido (modo SOAP): Passar um documento localizado no Repositório AEM Forms para o serviço de saída usando a API do Java](output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[Início rápido (modo SOAP): Criação de um documento PDF com base em fragmentos usando a API do Java](#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Início rápido (modo SOAP): Impressão em um arquivo usando a API Java](#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[Início rápido (modo SOAP): Envio de um fluxo de impressão para uma impressora de rede usando a API Java](output-service-java-api-quick.md#quick-start-soap-mode-sending-a-print-stream-to-a-network-printer-using-the-java-api)

[Início rápido (modo SOAP): Criação de vários arquivos PDF usando a API Java](output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[Início rápido (modo SOAP): Criação de regras de pesquisa usando a API do Java](output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Início rápido (modo SOAP): Transformar um documento PDF usando a API do Java](output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

As operações do AEM Forms podem ser executadas usando a API altamente digitada do AEM Forms e o modo de conexão deve ser definido como SOAP.

>[!NOTE]
>
>Os Inícios rápidos localizados em Programação com formulários de AEM são baseados no sistema operacional Forms Server. No entanto, se estiver usando outro sistema operacional, como UNIX, substitua caminhos específicos do Windows por caminhos compatíveis com o sistema operacional aplicável. Da mesma forma, se estiver usando outro servidor de aplicativos J2EE, certifique-se de especificar propriedades de conexão válidas. Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## Início rápido (modo SOAP): Criação de um documento PDF usando a API Java {#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api}

O seguinte exemplo de código Java cria um documento PDF chamado *Loan.pdf*. Este documento PDF é baseado em um design de formulário chamado *Loan.xdp* e um arquivo de dados XML chamado *Loan.xml*. O *Loan.pdf* é gravado no C:\Adobe folder located on the J2EE application server hosting AEM Forms, não no computador cliente. (Consulte [Criação de documentos PDF](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
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
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
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
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class CreatePDFDocument {
 
     public static void main(String[] args) {
 
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
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference form data
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
         Document inXMData = new Document (fileInputStream);
 
         //Set PDF run-time options
         PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setFileURI("C:\\Adobe\Loan.pdf");
 
         //Set rendering run-time options
         RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
         pdfOptions.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
         //Create a PDF document
         OutputResult outputDocument = outClient.generatePDFOutput(
             TransformationFormat.PDF,
             "Loan.xdp",
             "C:\\Adobe",
             outputOptions,
             pdfOptions,
             inXMData
         );
 
         //Retrieve the results of the operation
         Document metaData = outputDocument.getStatusDoc();
         File myFile = new File("C:\\Adobe\Output.xml");
         metaData.copyToFile(myFile);
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
 
```

## Início rápido (modo SOAP): Criação de um documento PDF com base em um arquivo XDP do aplicativo usando a API Java {#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api}

O seguinte exemplo de código Java cria um documento PDF chamado *Loan.pdf*. Este documento PDF é baseado em um design de formulário chamado *Loan.xdp* e um arquivo de dados XML chamado *Loan.xml*. O arquivo XDP é implantado como parte de um aplicativo AEM Forms chamado `Applications/FormsApplication`. Observe que o caminho do URI é `repository:///Applications/FormsApplication/1.0/FormsFolder/`. O *Loan.pdf* é gravado no C:\Adobe folder located on the J2EE application server hosting AEM Forms, não no computador cliente. (Consulte [Criação de documentos PDF](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents).)

>[!NOTE]
>
>Antes de executar esse início rápido, certifique-se de criar um aplicativo AEM Forms chamado Aplicativos/FormsApplication. Crie uma pasta no aplicativo chamado FormsFolder e coloque o arquivo XDP na pasta . Para obter mais informações, consulte [Gerar um documento PDF ](/help/forms/developing/creating-document-output-streams.md)*.*

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
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
     * These JAR files are located in the following path:
     * <install directory>/Adobe/adobe_experience_manager_forms/SDK/client-libs/common
     *
     * <install directory>/Adobe/adobe_experience_manager_forms/SDK/client-libs/jboss
     *
     * <install directory>/Adobe/adobe_experience_manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/Adobe/adobe_experience_manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class CreatePDFDocumentFromLCApp {
 
     public static void main(String[] args) {
 
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
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference form data
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
         Document inXMData = new Document (fileInputStream);
 
         //Set PDF run-time options
         PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setFileURI("C:\\Adobe\Loan.pdf");
 
         //Set rendering run-time options
         RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
         pdfOptions.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
         //Create a PDF document -- reference an XDP file named Loan.xdp that is deployed as part of
         //a AEM Forms application named Applications/FormsApplication. The XDP file is located
         //in a folder named FormsFolder
         OutputResult outputDocument = outClient.generatePDFOutput(
             TransformationFormat.PDF,
             "Loan.xdp",
             "repository:///Applications/FormsApplication/1.0/FormsFolder/",
             outputOptions,
             pdfOptions,
             inXMData
         );
 
         //Retrieve the results of the operation
         Document metaData = outputDocument.getStatusDoc();
         File myFile = new File("C:\\Adobe\Output.xml");
         metaData.copyToFile(myFile);
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
 
 
```

## Início rápido (modo SOAP): Passar um documento localizado no Repositório para o serviço de saída usando a API Java {#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api}

O código Java a seguir recupera um arquivo XDP do Repositório e o transmite para o serviço de saída na instância `com.adobe.idp.Document`. O arquivo XDP é implantado como parte de um aplicativo AEM Forms chamado `Applications/FormsApplication`. Observe que o caminho do URI é `repository:///Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>A API do Repositório é usada para recuperar o arquivo XDP desse local. (Consulte [Lendo Recursos](/help/forms/developing/aem-forms-repository.md#reading-resources).)

Observe também que o valor da raiz de conteúdo `repository:///Applications/FormsApplication/1.0/FormsFolder/` é passado para o método `OutputClient` do objeto `generatePDFOutput2` (o segundo parâmetro). Esse valor é passado para o serviço de Saída para informar ao serviço de Saída que o formulário de garantia, como imagens, é armazenado nesse local.

>[!NOTE]
>
>Você pode definir o valor raiz de conteúdo da mesma maneira ao chamar o método `generatePrintedOutput2`.

O *Loan.pdf* é gravado no diretório C:\Adobe folder located on the J2EE application server hosting AEM Forms. (Consulte [Passando documentos localizados no Repositório para o Serviço de Saída](/help/forms/developing/creating-document-output-streams.md#passing-documents-located-in-the-repository-to-the-output-service).)

>[!NOTE]
>
>Antes de executar esse início rápido, certifique-se de criar um aplicativo AEM Forms chamado Aplicativos/FormsApplication. Crie uma pasta no aplicativo chamado FormsFolder e coloque o arquivo XDP na pasta .

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-repository-client.jar
     * 3. adobe-livecycle-client.jar
     * 4. adobe-usermanager-client.jar
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
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
 import com.adobe.livecycle.output.client.*;
 import com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient;
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class CreatePDFFFromRepository {
 
     public static void main(String[] args) {
 
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
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference form data
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
         Document inXMData = new Document (fileInputStream);
 
         //Set PDF run-time options
         PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setFileURI("C:\\Adobe\Loan.pdf"); // this PDF form is saved on the server
 
         //Get the form design from the AEM Forms Repository
         Document formDesign =  GetFormDesign(myFactory);
 
         //Set rendering run-time options
         RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
         pdfOptions.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
         //Create a non-interactive PDF document
         OutputResult outputDocument = outClient.generatePDFOutput2(
             TransformationFormat.PDF,
             "repository:///Applications/FormsApplication/1.0/FormsFolder/",
             formDesign,
             outputOptions,
             pdfOptions,
             inXMData
         );
 
         //Save the non-interactive PDF form as a PDF file on the client computer
         Document pdfForm = outputDocument.getGeneratedDoc();
         File myFile = new File("C:\\Adobe\Loan.pdf");
         pdfForm.copyToFile(myFile);
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 
     // Retrieve the form design from the following Repository path:
     // /Applications/FormsApplication/1.0/FormsFolder/Loan.xdp
     private static Document GetFormDesign(ServiceClientFactory myFactory)
     {
     try{
 
         // Create a ResourceRepositoryClient object using the service client factory
         ResourceRepositoryClient repositoryClient = new ResourceRepositoryClient(myFactory);
 
         // Specify the path in the Repository to Loan.xdp
         String resourceUri =  "/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";
 
         // Retrieve the XDP file
         Document doc = repositoryClient.readResourceContent(resourceUri);
 
            //Return the Document instance
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

## Início rápido (modo SOAP): Criação de um documento PDF usando a API Java {#quick_start_soap_mode_creating_a_pdf_document_using_the_java_api-1}

O seguinte exemplo de código Java cria um documento PDF chamado *Loan.pdf*. Este documento PDF é baseado em um design de formulário chamado *Loan.xdp* e um arquivo de dados XML chamado *Loan.xml*. O *Loan.pdf* é gravado no C:\Adobe folder located on the J2EE application server hosting AEM Forms, não no computador cliente. (Consulte [Criação de documentos PDF](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
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
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class CreatePDFDocumentSOAP {
 
     public static void main(String[] args) {
 
     try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference form data
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
         Document inXMData = new Document (fileInputStream);
 
         //Set PDF run-time options
         PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setFileURI("C:\\Adobe\Loan.pdf");
 
         //Set rendering run-time options
         RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
         pdfOptions.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
         //Create a PDF document
         OutputResult outputDocument = outClient.generatePDFOutput(
             TransformationFormat.PDF,
             "Loan.xdp",
             "C:\\Adobe",
             outputOptions,
             pdfOptions,
             inXMData
         );
 
         //Retrieve the results of the operation
         Document metaData = outputDocument.getStatusDoc();
         File myFile = new File("C:\\Adobe\Output.xml");
         metaData.copyToFile(myFile);
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
```

## Início rápido (modo SOAP): Criação de um documento PDF/A usando a API Java {#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api}

O seguinte exemplo de código Java cria um documento PDF/A chamado *LoanArchive.pdf*. Este documento PDF é baseado em um design de formulário chamado *Loan.xdp* e um arquivo de dados XML chamado *Loan.xml*. O *LoanArchive.pdf* é gravado no C:\Adobe folder located on the J2EE application server hosting AEM Forms, não no computador cliente. (Consulte [Criação de documentos PDF/A](/help/forms/developing/creating-document-output-streams.md#creating-pdf-a-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
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
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
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
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class CreatePDFADocument {
 
     public static void main(String[] args) {
 
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
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference an XML data source to merge with the form design
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
         Document inXMData = new Document (fileInputStream);
 
         //Set PDF run-time options
         PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setFileURI("C:\\Adobe\LoanArchive.pdf");
 
         //Set rendering run-time options
         RenderOptionsSpec pdfAOptions = new RenderOptionsSpec();
         pdfAOptions.setPDFAConformance(PDFAConformance.A);
         pdfAOptions.setPDFARevisionNumber(PDFARevisionNumber.Revision_1);
 
 
         //Create a PDF/A document
         OutputResult outputDocument = outClient.generatePDFOutput(
             TransformationFormat.PDFA,
             "Loan.xdp",
             "C:\\Adobe",
             outputOptions,
             pdfAOptions,
             inXMData
         );
 
         //Write the results of the operation to OutputLog.xml
         Document resultData = outputDocument.getStatusDoc();
         File myFile = new File("C:\\Adobe\OutputLog.xml");
         resultData.copyToFile(myFile);
 
         }catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
 
```

## Início rápido (modo SOAP): Passar documentos para o serviço de saída usando a API Java {#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api}

O seguinte início rápido do Java recupera o arquivo *Loan.xdp* dos Serviços de conteúdo. Esse arquivo XDP está localizado no `space /Company Home/Form Designs`. O arquivo XDP é retornado em uma instância `com.adobe.idp.Document`. A instância `com.adobe.idp.Document` é passada para o serviço de Saída. O formulário não interativo é salvo como um arquivo PDF chamado *Loan.pdf *no computador cliente. Como a opção File URI está definida, o arquivo PDF *Loan.pdf *também é salvo no servidor de aplicativos J2EE que hospeda o AEM Forms. (Consulte [Passando documentos localizados em Content Services ES2 para o Output Service](/help/forms/developing/creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe-contentservices-client.jar
     * 3. adobe-livecycle-client.jar
     * 4. adobe-usermanager-client.jar
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
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
 import com.adobe.livecycle.contentservices.client.CRCResult;
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl;
 import com.adobe.livecycle.output.client.*;
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class CreatePDFFFromContentServices {
 
     public static void main(String[] args) {
 
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
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference form data
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
         Document inXMData = new Document (fileInputStream);
 
         //Set PDF run-time options
         PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
         outputOptions.setFileURI("C:\\Adobe\Loan.pdf"); // this PDF form is saved on the server
 
         //Get the form design from Content Services
         Document formDesign =  GetFormDesign(myFactory);
 
         //Set rendering run-time options
         RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
         pdfOptions.setLinearizedPDF(true);
         pdfOptions.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
         //Create a non-interactive PDF document
         OutputResult outputDocument = outClient.generatePDFOutput2(
             TransformationFormat.PDF,
             "C:\\Adobe",
             formDesign,
             outputOptions,
             pdfOptions,
             inXMData
         );
 
         //Save the non-interactive PDF form as a PDF file on the client computer
         Document pdfForm = outputDocument.getGeneratedDoc();
         File myFile = new File("C:\\Adobe\Loan.pdf");
         pdfForm.copyToFile(myFile);
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 
     //Retrieve the form design from Content Services ES2
     private static Document GetFormDesign(ServiceClientFactory myFactory)
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

## Início rápido (modo SOAP): Criação de um documento PDF com base em fragmentos usando a API Java {#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api}

O exemplo de código Java a seguir cria um documento PDF baseado em um design de formulário montado pelo serviço Assembler. O serviço Assembler monta fragmentos localizados em vários arquivos XDP em um único design de formulário. A lógica do aplicativo que chama o serviço Assembler está localizada em um método definido pelo usuário chamado `GetFormDesign`. O formulário não interativo é salvo como um arquivo PDF chamado *Loan.pdf *no computador cliente. (Consulte [Criação de documentos PDF usando fragmentos](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
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
     * 20. adobe-assembler-client.jar
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
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
     *
     * This is the DDX file is used to assemble multiple XDP documents:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <XDP result="tuc018result.xdp">
     * <XDP source="tuc018_template_flowed.xdp">
     * <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
     * <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
     * <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
     * </XDP>
     * </XDP>
     * </DDX>
     */
 import com.adobe.livecycle.assembler.client.AssemblerOptionSpec;
 import com.adobe.livecycle.assembler.client.AssemblerResult;
 import com.adobe.livecycle.assembler.client.AssemblerServiceClient;
 import com.adobe.livecycle.output.client.*;
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class CreatePDFFromFragments {
 
     public static void main(String[] args) {
 
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
 
             //Create an OutputClient object
             OutputClient outClient = new OutputClient(myFactory);
 
             //Reference form data
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
             Document inXMData = new Document (fileInputStream);
 
             //Set PDF run-time options
             PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
             outputOptions.setFileURI("C:\\Adobe\Loan.pdf"); // this PDF form is saved on the server
 
             //Get the form design from Assembler service
             Document formDesign =  GetFormDesign(myFactory);
 
             //Set rendering run-time options
             RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
             pdfOptions.setLinearizedPDF(true);
             pdfOptions.setAcrobatVersion(AcrobatVersion.Acrobat_9);
 
             //Create a non-interactive PDF document
             OutputResult outputDocument = outClient.generatePDFOutput2(
                 TransformationFormat.PDF,
                 "C:\\Adobe",
                 formDesign,
                 outputOptions,
                 pdfOptions,
                 inXMData
             );
 
             //Save the non-interactive PDF form as a PDF file on the client computer
             Document pdfForm = outputDocument.getGeneratedDoc();
             File myFile = new File("C:\\Adobe\Loan.pdf");
             pdfForm.copyToFile(myFile);
             }
             catch (Exception ee)
             {
                 ee.printStackTrace();
             }
         }
 
         //Retrieve the form design from Assembler service
         private static Document GetFormDesign(ServiceClientFactory myFactory)
         {
             try{
 
                 //Create an AssemblerServiceClient object
                 AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
                 //Create a FileInputStream object based on an existing DDX file
                 FileInputStream myDDXFile = new FileInputStream("C:\\Adobe\fragmentDDX.xml");
 
                 //Create a Document object based on the DDX file
                 Document myDDX = new Document(myDDXFile);
 
                 //Create a Map object to store the input XDP files
                 Map inputs = new HashMap();
                 FileInputStream inSource = new FileInputStream("C:\\Adobe\tuc018_template_flowed.xdp");
                 FileInputStream inFragment1 = new FileInputStream("C:\\Adobe\tuc018_contact.xdp");
                 FileInputStream inFragment2 = new FileInputStream("C:\\Adobe\tuc018_patient.xdp");
 
                 //Create a Document object
                 Document myMapSource = new Document(inSource);
 
                 //Create a Document object
                 Document inFragment1Doc = new Document(inFragment1);
 
                 //Create a Document object
                 Document inFragment2Doc = new Document(inFragment2);
 
                 //Place all of the XDP files into the MAP
                 inputs.put("tuc018_template_flowed.xdp",myMapSource);
                 inputs.put("tuc018_contact.xdp",inFragment1Doc);
                 inputs.put("tuc018_patient.xdp",inFragment2Doc);
 
 
                 //Create an AssemblerOptionsSpec object
                 AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
                 assemblerSpec.setFailOnError(false);
 
                 //Submit the job to Assembler service
                 AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
                 java.util.Map allDocs = jobResult.getDocuments();
 
                 //Retrieve the result PDF document from the Map object
                 Document outDoc = null;
 
                 //Iterate through the map object to retrieve the result XDP document
                 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                     // Retrieve the Map object?s value
                     Map.Entry e = (Map.Entry)i.next();
 
                     //Get the key name as specified in the
                     //DDX document
                     String keyName = (String)e.getKey();
                     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                     {
                         Object o = e.getValue();
                         outDoc = (Document)o;
 
                     }
                 }
 
             return outDoc;
             }catch (Exception e) {
                 e.printStackTrace();
             }
             return null;
         }
     }
 
 
```

## Início rápido (modo SOAP): Impressão em um arquivo usando a API Java {#quick-start-soap-mode-printing-to-a-file-using-the-java-api}

O exemplo de código Java a seguir imprime um fluxo de saída em um arquivo PostScript chamado *MortgaugeForm.ps*. (Consulte [Imprimindo em Arquivos](/help/forms/developing/creating-document-output-streams.md#printing-to-files).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
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
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
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
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class PrintToFile {
 
     public static void main(String[] args) {
 
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
 
             //Create an OutputClient object
             OutputClient outClient = new OutputClient(myFactory);
 
             //Reference XML data that represents form data
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
             Document inputXML = new Document(fileInputStream);
 
             //Set print run-time options required to print to a file
             PrintedOutputOptionsSpec printOptions = new PrintedOutputOptionsSpec();
             printOptions.setFileURI("C:\\Adobe\MortgageForm.ps");
 
             //Print the print stream to a PostScript file
             OutputResult outputDocument = outClient.generatePrintedOutput(
                     PrintFormat.PostScript,
                     "Loan.xdp",
                     "C:\\Adobe",
                     null,
                     printOptions,
                     inputXML);
 
             //Write the results of the operation to OutputLog.xml
             Document resultData = outputDocument.getStatusDoc();
             File myFile = new File("C:\\Adobe\OutputLog.xml");
             resultData.copyToFile(myFile);
             System.out.println("AEM Forms printed to MortgageForm.ps");
         }
     catch (Exception ee)
             {
             ee.printStackTrace();
         }
     }
 }
 
```

## Início rápido (modo SOAP): Envio de um fluxo de impressão para uma impressora de rede usando a API Java {#quick-start-soap-mode-sending-a-print-stream-to-a-network-printer-using-the-java-api}

O exemplo de código Java a seguir envia um fluxo de impressão PostScript para uma impressora de rede chamada *\\Printer1\Printer*. Duas cópias são enviadas para a impressora. (Consulte [Envio de fluxos de impressão para impressoras](/help/forms/developing/creating-document-output-streams.md#sending-print-streams-to-printers).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
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
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
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
 import java.util.*;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.output.client.*;
 
 public class SendToPrinter {
 
     public static void main(String[] args) {
 
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
 
             //Create an OutputClient object
             OutputClient outClient = new OutputClient(myFactory);
 
             //Reference XML data that represents form data
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
             Document inputXML = new Document(fileInputStream);
 
             //Set print run-time options required to print to a file
             PrintedOutputOptionsSpec printOptions = new PrintedOutputOptionsSpec();
 
             //Set the number of copies to print
             printOptions.setCopies(2);
 
             //Turn on the Staple option
             printOptions.setStaple(Staple.on);
 
             //Create a PostScript output stream based on the form design named Loan.xdp and
             //the data located in the XML file
             OutputResult outputDocument = outClient.generatePrintedOutput(
                     PrintFormat.PostScript,
                     "Loan.xdp",
                     "C:\\Adobe",
                     "C:\\Adobe",
                     printOptions,
                     inputXML);
 
             //Get a Document object that stores the PostScript print stream
             Document psPrintStream = outputDocument.getGeneratedDoc();
 
             //Specify the print server and the printer name
             String printServer = "\\\ottprint";
             String printerName = "\\\ottprint\Balsom";
 
             //Send the PostScript print stream to the printer
             outClient.sendToPrinter(
                     psPrintStream,
                     PrinterProtocol.SharedPrinter,
                     printServer,
                     printerName);
             }
         catch (Exception ee)
             {
             ee.printStackTrace();
             }
     }
 }
 
```

## Início rápido (modo SOAP): Criação de vários arquivos PDF usando a API Java {#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api}

O código Java a seguir cria vários arquivos PDF para cada registro de dados localizado em um arquivo de dados XML chamado *Loan_data_batch.xml*. Os arquivos são gravados na pasta C:\Adobe directory. Os arquivos PDF são gravados no C:\Adobe folder located on the J2EE application server hosting AEM Forms, não no computador cliente. (Consulte [Criação de vários arquivos de saída](/help/forms/developing/creating-document-output-streams.md#creating-multiple-output-files).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
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
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
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
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.output.client.*;
 
 public class CreateBatchFiles {
 
     public static void main(String[] args) {
 
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
 
             //Create an OutputClient object
             OutputClient outClient = new OutputClient(myFactory);
 
             //Reference form data that contains multiple records
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan_data_batch.xml");
             Document inXMData = new Document (fileInputStream);
 
             //Set run-time options to generate many PDF files
             PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
             outputOptions.setFileURI("C:\\Adobe\Loan.pdf");
             outputOptions.setGenerateManyFiles(true);
             outputOptions.setRecordName("LoanRecord");
 
 
             //Set rendering run-time options
             RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
             pdfOptions.setCacheEnabled(new Boolean(true));
 
 
             //Create multiple PDF files
             OutputResult outputDocument = outClient.generatePDFOutput(
                 TransformationFormat.PDF,
                 "Loan.xdp",
                 "C:\\Adobe",
                 outputOptions,
                 pdfOptions,
                 inXMData
                 );
 
             //Retrieve the results of the operation
             Document metaData = outputDocument.getStatusDoc();
             File myFile = new File("C:\\Adobe\Output.xml");
             metaData.copyToFile(myFile);
             }
             catch (Exception ee)
             {
                 ee.printStackTrace();
             }
     }
 }
 
 
```

## Início rápido (modo SOAP): Criação de regras de pesquisa usando a API Java {#quick-start-soap-mode-creating-search-rules-using-the-java-api}

O exemplo de código Java a seguir cria dois padrões de texto que o serviço de saída procura. O primeiro padrão de texto é o Hipermedidor. Se encontrado, o serviço de Saída usa o design de formulário chamado *Mortgauge.xdp*. O segundo padrão de texto é Automóvel. Se encontrado, o Serviço de saída usa o design de formulário chamado *AutomobileLoan.xdp*. Se nenhum padrão de texto estiver localizado, o Serviço de saída usará o design de formulário padrão chamado* Loan.xdp. *(Consulte [Criando Regras de Pesquisa](/help/forms/developing/creating-document-output-streams.md#creating-search-rules).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
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
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
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
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class CreateSearchRules {
 
     public static void main(String[] args) {
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
 
             //Create an OutputClient object
             OutputClient outClient = new OutputClient(myFactory);
 
             //Reference form data
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xml");
             Document inXMData = new Document (fileInputStream);
 
             //Define two text patterns
             Rule mortageRule = new Rule();
             mortageRule.setPattern("Mortgage");
             mortageRule.setForm("Mortgage.xdp");
 
             Rule automobileRule = new Rule();
             automobileRule.setPattern("Automobile");
             automobileRule.setForm("AutomobileLoan.xdp");
 
             //Add the Rules to a List object
             List<Rule> myList = new ArrayList<Rule>();
             myList.add(mortageRule);
             myList.add(automobileRule);
 
             //Define PDF run-time options which includes Search Rules
             PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec();
             outputOptions.setFileURI("C:\\Adobe\Loan.pdf");
             outputOptions.setRules(myList);
             outputOptions.setLookAhead(900);
 
             //Define rendering run-time options
             RenderOptionsSpec pdfOptions = new RenderOptionsSpec();
             pdfOptions.setCacheEnabled(new Boolean(true));
 
             //Create a PDF document based on multiple form designs
             OutputResult outputDocument = outClient.generatePDFOutput(
                 TransformationFormat.PDF,
                 "Loan.xdp",
                 "C:\\Adobe",
                 outputOptions,
                 pdfOptions,
                 inXMData
             );
 
             //Write the results of the operation to OutputLog.xml
             Document resultData = outputDocument.getStatusDoc();
             File myFile = new File("C:\\Adobe\OutputLog.xml");
             resultData.copyToFile(myFile);
             }
         catch (Exception ee)
                 {
                     ee.printStackTrace();
                 }
         }
 }
 
```

## Início rápido (modo SOAP): Transformar um documento PDF usando a API Java {#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api}

O seguinte exemplo de código Java transforma um documento PDF interativo chamado *Loan.pdf* em um documento PDF não interativo chamado *NonInterativeLoan.pdf*. (Consulte [Nivelar documentos PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
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
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
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
 import com.adobe.livecycle.output.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class TransformPDF {
 
     public static void main(String[] args) {
 
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
 
         //Create an OutputClient object
         OutputClient outClient = new OutputClient(myFactory);
 
         //Reference an interactive PDF document to transform
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
         Document inPDFDoc = new Document (fileInputStream);
 
         //Transform the PDF document to a non-interactive PDF document
         Document transformedDocument = outClient.transformPDF(
                 inPDFDoc,
                 TransformationFormat.PDF,
                 null,
                 null,
                 null);
 
         //Save the non-interactive PDF document
         File myFile = new File("C:\\Adobe\NonInteractiveLoan.pdf");
         transformedDocument.copyToFile(myFile);
 
     }catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
 
```

