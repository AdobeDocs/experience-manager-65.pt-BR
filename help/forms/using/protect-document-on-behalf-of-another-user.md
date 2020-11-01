---
title: Protect um documento em nome de outro usuário
seo-title: Protect um documento em nome de outro usuário
description: Protect um documento em nome de outro usuário
uuid: 76f4b30b-6d0c-4cae-98b3-334efdbf27bb
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: 7cb8140d-dd62-4659-8cc7-21361bd5d3f6
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Protect um documento em nome de outro usuário {#protect-a-document-on-behalf-of-another-user}

O AEM Forms Documento Security Java SDK fornece APIs para permitir que uma conta de usuário proteja um documento em nome de outro usuário sem obter as permissões para editar o documento. Você pode usar as APIs em um processo de fluxo de trabalho ou programaticamente como um serviço de documento. As novas APIs são:

* **protectDocumentUse** a API ProtectDocument para aplicar uma política a um documento em nome de

   outra conta de usuário. As permissões da conta de usuário usada para aplicar a política permanecem limitadas à proteção do documento. Não obtém direitos para abrir e visualização o documento. RMSecureDocumentResult protectDocument(Documento inDoc, String documentName, String policySetName, String policyName, RMLocale locale, boolean bExactMatchForNames)

* **createLicenseUse** a API CreateLicense para criar uma licença para uma política em nome de outra conta de usuário. PublishLicenseDTO createLicense(String policyId, String documentName, boolean logSecureDocEvent)
* **protectedDocumentWithCoverPageUse** a API ProtectDocumentWithCoverPage para aplicar uma política e adicionar uma página de capa a um documento em nome de outro usuário. As permissões da conta de usuário usada para aplicar a política permanecem limitadas à proteção do documento. Não alcança os direitos de abertura e visualização do documento. RMSecureDocumentResult protectDocumentWithCoverPage(Documento inDoc, String documentName, String policySetName, String policyName, coverDoc, boolean bExactMatchForNames)

## Usar as APIs para proteger um documento em nome de outro usuário {#using-the-apis-to-protect-a-document-on-behalf-of-another-user}

Execute as seguintes etapas para proteger um documento em nome de outro usuário e sem obter as permissões para editar o documento:

1. Criar um conjunto de políticas. Por exemplo, PolicySet1.
1. Crie uma política no conjunto de políticas recém-criado. Por exemplo, Policy1 em PolicySet1.
1. Crie um usuário com a função Rights Management Usuário final. Por exemplo, User1. Forneça as permissões para documentos de visualização protegidos usando a Política1 ao usuário recém-criado.
1. Crie uma nova função. Por exemplo, Role1. Forneça a permissão Invocar serviço para a função recém-criada. Crie um usuário com uma função recém-criada. Por exemplo, User2.Você pode usar User2 ou um administrador para criar uma conexão SDK e chamar o serviço protectDocument.

   Agora, você pode executar o seguinte código de amostra para proteger um documento sem fornecer permissões para editar o documento ao usuário que o protege:

   ```java
   import java.io.File;
   import java.io.FileInputStream;
   import java.io.FileNotFoundException;
   import java.io.FileOutputStream;
   import java.io.IOException;
   import java.io.InputStream;
   import java.util.Properties;
   
   import com.adobe.edc.common.dto.PublishLicenseDTO;
   import com.adobe.edc.sdk.SDKException;
   import com.adobe.idp.Document;
   import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
   import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
   import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;
   import com.adobe.livecycle.rightsmanagement.client.DocumentManager;
   import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient;
   import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient2;
   
   public class PublishAsProtectAPI {
   
   private static final String unprotectedFileName = "C:\\unprotected.pdf";
   private static final String protectedFileName = "C:\\protect.pdf";
   private static final String coverFileName = "C:\\CoverPage.pdf";
   private static final String POLICY_ID = "2EF66008-5E2D-1034-9B06-00000A292C18"; 
   
   public static void main(String[] args) {
   
   try {
   
   Properties connectionProps = new Properties();
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,"http://localhost:8080");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,"password");
   
   // Create a ServiceClientFactory instance
   ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
   testProtectDocument(factory);
   testProtectDocumentWithCoverPage(factory);
   testProtectDocumentJavaPPL(factory);
   
   } 
   catch (Exception ex) {
   ex.printStackTrace(); }
   }
   
   private static void testProtectDocument(ServiceClientFactory factory) throws FileNotFoundException, SDKException {
   // Create a RightsManagementClient object
   RightsManagementClient rmClient = new RightsManagementClient(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient.getDocumentManager();
   //Reference a policy-protected PDF document from which to remove a policy
   FileInputStream is = new FileInputStream(unprotectedFileName);
   Document inPDF = new Document(is);
   long startTime = System.currentTimeMillis();
   //Remove a policy from the policy-protected PDF document
   RMSecureDocumentResult securePDF = documentManager.protectDocument(inPDF, "test", "newPolicySet", "latest", "DefaultDom", "administrator", null, true);
   System.out.println("Total Time taken for protectDocument = " + (System.currentTimeMillis() - startTime));
   //Save the unsecured PDF document
   File myFile = new File(protectedFileName);
   securePDF.getProtectedDoc().copyToFile(myFile);
   }
   
   private static void testProtectDocumentWithCoverPage(ServiceClientFactory factory) throws FileNotFoundException, SDKException {
   // Create a RightsManagementClient object
   RightsManagementClient rmClient = new RightsManagementClient(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient.getDocumentManager();
   //Reference a policy-protected PDF document from which to remove a policy
   FileInputStream is = new FileInputStream(unprotectedFileName);
   Document inPDF = new Document(is);
   FileInputStream coverIS = new FileInputStream(coverFileName);
   Document inCoverPDF = new Document(coverIS);
   long startTime = System.currentTimeMillis();
   //Remove a policy from the policy-protected PDF document
   RMSecureDocumentResult securePDF = documentManager.protectDocumentWithCoverPage(inPDF, "test", "newPolicySet", "latestPolicy", inCoverPDF, true);
   System.out.println("Total Time taken for Page0ProtectDocument = " + (System.currentTimeMillis() - startTime));
   //Save the unsecured PDF document
   File myFile = new File(protectedFileName);
   securePDF.getProtectedDoc().copyToFile(myFile);
   }
   
   private static PublishLicenseDTO testProtectDocumentJavaPPL (ServiceClientFactory factory) throws SDKException, FileNotFoundException, IOException {
   // Create a RightsManagementClient object
   RightsManagementClient2 rmClient2 = new RightsManagementClient2(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient2.getDocumentManager();
   long startTime = System.currentTimeMillis();
   PublishLicenseDTO license = documentManager.createLicense(POLICY_ID, "Out.pdf", true);
   System.out.println("Create License totalTime = " + (System.currentTimeMillis() - startTime));
   startTime = System.currentTimeMillis();
   // Reference a PDF document to which a policy is applied
   InputStream inputFileStream = new FileInputStream(unprotectedFileName);
   // Apply a policy to the PDF document
   InputStream protectPDF = rmClient2.getRightsManagementEncryptionService().protectDocument(inputFileStream, license);
   // Save the policy-protected PDF document
   File myFile = new File(protectedFileName);
   // write the inputStream to a FileOutputStream
   FileOutputStream outputStream = new FileOutputStream(myFile);
   int read = 0;
   byte[] bytes = new byte[1024];
   while ((read = protectPDF.read(bytes)) != -1) {
   outputStream.write(bytes, 0, read);
   }
   System.out.println("protectPDFDocument totalTime = " + (System.currentTimeMillis() - startTime));
   outputStream.close();
   inputFileStream.close();
   System.out.println("Document Protected Successfully");
   return license;
   }
   }
   ```

