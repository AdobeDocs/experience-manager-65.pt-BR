---
title: Gerar o QuickStart (SOAP) da API Java do serviço PDF
seo-title: Gerar o QuickStart (SOAP) da API Java do serviço PDF
description: 'null'
seo-description: 'null'
uuid: f8c4a476-de5e-440a-b419-0bd1d7fde5ca
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a7c0c4cf-7476-41e7-8d4e-564e6a21458d
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Gerar o Start rápido SOAP (Java API) do serviço PDF {#generate-pdf-service-java-api-quickstart-soap}

O SOAP (Java API Quick Start) está disponível para o serviço Gerar PDF.

[Start rápido (modo SOAP): Converter um documento do Microsoft Word em um documento PDF usando a API Java](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[Start rápido (modo SOAP): Converter conteúdo HTML em um documento PDF usando a API Java](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Start rápido (modo SOAP): Converter um documento PDF em um arquivo RTF usando a API Java (modo SOAP)](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-an-rtf-file-using-the-java-api-soap-mode)

As operações do AEM Forms podem ser executadas usando a AEM Forms fortemente tipada API e o modo de conexão deve ser definido como SOAP.

***Observação **: O Start rápido localizado em Programação com AEM Forms baseia-se no Forms Server que está sendo implantado no JBoss Application Server e no sistema operacional Microsoft Windows. No entanto, se você estiver usando outro sistema operacional, como UNIX, substitua caminhos específicos do Windows por caminhos compatíveis com o sistema operacional aplicável. Da mesma forma, se você estiver usando outro servidor de aplicativos J2EE, certifique-se de especificar propriedades de conexão válidas. (Consulte[Configuração das propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.)*

## Start rápido (modo SOAP): Converter um documento do Microsoft Word em um documento PDF usando a API Java {#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api}

O exemplo de código a seguir converte um arquivo do Word chamado *Loan.doc* em um documento PDF chamado *Loan.pdf*. (Consulte [Converter Documentos do Word em Documentos](/help/forms/developing/converting-file-formats-pdf.md#converting-word-documents-to-pdf-documents)PDF.)

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
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
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 
 public class ConvertWordDocumentSOAP {
 
     public static void main(String[] args)
     {
         try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a GeneratePdfServiceClient object
         GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(myFactory);
 
         //Get a Microsoft Word file document to convert to a PDF document
         String inputFileName = "C:\\Adobe\\Loan.doc";
         FileInputStream fileInputStream = new FileInputStream(inputFileName);
         Document inDoc = new Document(fileInputStream);
 
         //Set createPDF2 parameter values
         String adobePDFSettings = "Smallest_File_Size";
          String securitySettings = "No Security";
          String fileTypeSettings = "Filetype Settings";
 
          //Convert the Word document to a PDF document
          CreatePDFResult result = pdfGenClient.createPDF2(
             inDoc,
             inputFileName,
             fileTypeSettings,
             adobePDFSettings,
             securitySettings,
             null,
             null);
 
          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();
 
          //Save the converted PDF document as a PDF file
         createdDocument.copyToFile(new File("C:\\Adobe\\Loan.pdf"));
     }
     catch (Exception e) {
         System.out.println("Error OCCURRED: " + e.getMessage());
         }
     }
 }
```

## Start rápido (modo SOAP): Converter conteúdo HTML em um documento PDF usando a API Java {#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api}

O exemplo de código Java a seguir converte o conteúdo HTML localizado em https://www.adobe.com para um documento PDF chamado *AdobeHTML.pdf*. (Consulte [Converter Documentos HTML em Documentos](/help/forms/developing/converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)PDF.)

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
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
 import java.io.File;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 import com.adobe.livecycle.generatepdf.client.HtmlToPdfResult;
 
 public class ConvertHTMLSOAP {
 
     public static void main(String[] args)
     {
         try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a GeneratePdfServiceClient object
         GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(myFactory);
 
         //Get an HTML document to convert to a PDF document a
         String inputFileName = "https://www.adobe.com";
 
          String securitySettings = "No Security";
         String fileTypeSettings = "Standard";
 
          //Convert HTML content to a PDF document
          HtmlToPdfResult result = pdfGenClient.htmlToPDF2(
                  inputFileName,
                  fileTypeSettings,
                  securitySettings,
                  null,
                 null);
 
          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();
 
          //Save the PDF document as a PDF file
         createdDocument.copyToFile(new File("C:\\AdobeHTML.pdf"));
     }
     catch (Exception e) {
         System.out.println("Error OCCURRED: " + e.getMessage());
     }
     }
 }
```

## Start rápido (modo SOAP): Converter um documento PDF em um arquivo RTF usando a API Java (modo SOAP) {#quick-start-soap-mode-converting-a-pdf-document-to-an-rtf-file-using-the-java-api-soap-mode}

O exemplo de código a seguir converte um documento PDF chamado *Loan.pdf* em um documento RTF chamado *Loan.rtf*. (Consulte [Converter Documentos PDF em formatos](/help/forms/developing/converting-file-formats-pdf.md#converting-pdf-documents-to-non-image-formats)que não sejam de imagem.)

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
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
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.ConvertPDFFormatType;
 import com.adobe.livecycle.generatepdf.client.ExportPDFResult;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 
 
 public class GeneratePdf_ExportPDFSOAP {
 
     public static void main(String[] args)
     {
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a GeneratePdfServiceClient object
             GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(factory);
 
             //Get a PDF document to convert to an RTF document
             String inputFileName = "C:\\Adobe\\Loan.pdf.pdf";
             FileInputStream fileInputStream = new FileInputStream(inputFileName);
             Document inDoc = new Document(fileInputStream);
 
             //Convert a PDF document to a RTF document
             ExportPDFResult result = pdfGenClient.exportPDF2(
                 inDoc,
                 inputFileName,
                 ConvertPDFFormatType.RTF,
                 null);
 
          //Get the newly created RTF document
          Document createdDocument = result.getConvertedDocument();
 
          //Save the RTF file
         createdDocument.copyToFile(new File("C:\\Adobe\\Loan.pdf.rtf"));
         }
         catch (Exception e) {
             System.out.println("Error OCCURRED: " + e.getMessage());
         }
     }
 }
```

