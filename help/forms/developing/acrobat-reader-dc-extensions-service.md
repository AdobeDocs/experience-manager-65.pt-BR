---
title: Start rápido (SOAP) da API Java do Acrobat Reader DC para extensões do serviço
seo-title: Start rápido (SOAP) da API Java do Acrobat Reader DC para extensões do serviço
description: 'null'
seo-description: 'null'
uuid: 8e72ca94-a8c1-43aa-9845-a0da597051c5
contentOwner: admin
content-type: reference
topic-tags: develop
discoiquuid: 31a9bfc6-462d-4535-888f-31026b8fa674
translation-type: tm+mt
source-git-commit: 21efe30c6a69d04c737bc523aeaab504db8f605b

---


# Serviço de extensões do Acrobat Reader DClStart rápido da API Java (SOAP) {#acrobat-reader-dc-extensions-servicejava-api-quick-start-soap}

Os Start Rápidos a seguir estão disponíveis para o serviço Extensões do Acrobat Reader DC.

[Start rápido (modo SOAP):Aplicar direitos de uso usando a API Java](#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[Remoção de direitos de uso de Documentos PDF](#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[Start rápido (modo SOAP): Recuperando informações de credenciais usando a API Java](acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

As operações do AEM Forms podem ser executadas usando a AEM Forms fortemente tipada API e o modo de conexão deve ser definido como SOAP.

>[!NOTE]
>
>Start rápidos localizados em Programação com AEM Forms são baseados no sistema operacional do servidor Forms. No entanto, se você estiver usando outro sistema operacional, como UNIX, substitua caminhos específicos do Windows por caminhos compatíveis com o sistema operacional aplicável. Da mesma forma, se você estiver usando outro servidor de aplicativos J2EE, certifique-se de especificar propriedades de conexão válidas. Consulte [Configuração de propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.

## Start rápido (modo SOAP):Aplicar direitos de uso usando a API Java {#quick-start-soap-mode-applying-usage-rights-using-the-java-api}

O exemplo de código Java a seguir aplica direitos de uso a um documento PDF chamado *Loan.pdf*. O documento PDF habilitado para direitos é salvo como um arquivo PDF chamado *LoanUsageRights.pdf*. Os seguintes direitos de uso são aplicados a este documento PDF: `enabledComments`, `enabledFormFillIn`e `enabledDigitalSignatures`. (Consulte [Aplicar direitos de uso a Documentos](/help/forms/developing/assigning-usage-rights.md)PDF.)


```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-reader-extensions-client.jar 
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
 import com.adobe.livecycle.readerextensions.client.*; 
 import java.util.*; 
 import java.io.File; 
 import java.io.FileInputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class ApplyUsageRightsSOAP{ 
  
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
          
           //Create a ReaderExtensionsServiceClient object 
           ReaderExtensionsServiceClient reClient = new ReaderExtensionsServiceClient(myFactory);  
          
           //Retrieve the PDF document to which to apply usage rights 
           FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");  
           Document inputPDF = new Document(fileInputStream); 
                   
           //Create a UsageRight object and specify specific usage rights 
           UsageRights useRight = new UsageRights();  
           useRight.setEnabledDynamicFormFields(true); 
           useRight.setEnabledComments(true); 
           useRight.setEnabledFormFillIn(true); 
           useRight.setEnabledDigitalSignatures(true); 
          
           //Create a ReaderExtensionsOptions object 
           ReaderExtensionsOptionSpec reOptions = new ReaderExtensionsOptionSpec();  
                   
           //Set the usage rights  
           reOptions.setUsageRights(useRight);  
           reOptions.setMessage("This is a Rights-Enabled PDF Document"); 
          
           //Apply usage rights to a PDF document 
           Document rightsEnabledPDF = reClient.applyUsageRights( 
              inputPDF, 
              "RE2", 
             null, 
             reOptions);  
          
           //Create a new PDF file that represents the rights-enabled PDF document 
           File resultFile = new File("C:\\Adobe\LoanUsageRights.pdf");  
           rightsEnabledPDF.copyToFile(resultFile); 
                          
         }catch (Exception e) { 
              e.printStackTrace(); 
         }     
     } 
 } 
  
  
 
```

## Start rápido (modo SOAP): Remoção de direitos de uso de um documento PDF usando a API Java {#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api}

O exemplo de código Java a seguir remove os direitos de uso de um documento PDF habilitado para direitos chamado *LoanUsageRights.pdf*. (Consulte [Remoção de direitos de uso de Documentos](/help/forms/developing/assigning-usage-rights.md)PDF.)

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-reader-extensions-client.jar 
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
 import com.adobe.livecycle.readerextensions.client.*; 
 import java.util.*; 
 import java.io.File; 
 import java.io.FileInputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RemoveUsageRights{ 
  
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
                  
           //Create a ReaderExtensionsServiceClient object 
           ReaderExtensionsServiceClient reClient = new ReaderExtensionsServiceClient(myFactory);  
          
                //Retrieve a rights-enabled PDF document from 
                //which to remove usage rights 
           FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanUsageRights.pdf");  
           Document inputPDF = new Document(fileInputStream); 
                   
           //Remove usage rights from the PDF document 
           Document rightsEnabledPDF = reClient.removeUsageRights(inputPDF);  
          
           //Save the PDF document as a PDF file 
           File resultFile = new File("C:\\Adobe\noUsageRightsLoan.pdf");  
           rightsEnabledPDF.copyToFile(resultFile); 
           System.out.println("Usage rights were removed from the document");  
                          
         }catch (Exception e) { 
              e.printStackTrace(); 
         }     
     } 
 } 
 
```

## Start rápido (modo SOAP): Recuperando informações de credenciais usando a API Java {#quick-start-soap-mode-retrieving-credential-information-using-the-java-api}

O exemplo de código Java a seguir recupera informações sobre a credencial usada para aplicar direitos de uso a um documento PDF habilitado para direitos chamado *LoanUsageRights.pdf*. (Consulte [Recuperando Informações](/help/forms/developing/assigning-usage-rights.md)de Credenciais.)

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-reader-extensions-client.jar 
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
 import com.adobe.livecycle.readerextensions.client.*; 
 import java.util.*; 
 import java.io.FileInputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RetrieveCredentialInformation { 
  
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
                  
           //Create a ReaderExtensionsServiceClient object 
           ReaderExtensionsServiceClient reClient = new ReaderExtensionsServiceClient(myFactory);  
          
           //Retrieve a rights-enabled PDF document 
           FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanUsageRights.pdf");  
           Document inputPDF = new Document(fileInputStream); 
                   
           //Retrieve credential information 
           GetUsageRightsResult usageRightsResult = reClient.getDocumentUsageRights(inputPDF);  
          
           //Get the date after which the credential is no longer valid 
           Date endDate = usageRightsResult.getNotAfter(); 
          
           //Get the message displayed in Adobe Reader when the rights-enabled 
           //document is opened 
           String message = usageRightsResult.getMessage(); 
          
           //Get usage rights to see if the enableFormFillIn is enabled 
           UsageRights myRights = usageRightsResult.getRights(); 
           boolean ans = myRights.isEnabledFormFillIn(); 
          
           if (ans==true) 
              System.out.println("The enableFormFillIn usage right is enabled"); 
           else 
             System.out.println("The enableFormFillIn usage right is not enabled"); 
                                                   
         }catch (Exception e) { 
              e.printStackTrace(); 
         }     
                  
     } 
 } 
 
```

