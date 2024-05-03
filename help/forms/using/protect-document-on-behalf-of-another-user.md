---
title: Protect um documento em nome de outro usuário
description: Saiba como o SDK do Java&trade; para Segurança de documentos do AEM Forms oferece APIs para uma conta de usuário para proteger um documento em nome de outro usuário.
geptopics: SG_AEMFORMS/categories/working_with_document_security
feature: Document Security
exl-id: e5c80569-d3c0-4358-9b91-b98a64d1c004
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Protect um documento em nome de outro usuário {#protect-a-document-on-behalf-of-another-user}

O SDK do Java™ para Segurança de documentos da AEM Forms fornece APIs para permitir que uma conta de usuário proteja um documento em nome de outro usuário sem obter as permissões para editar o documento. Você pode usar as APIs em um processo de fluxo de trabalho ou programaticamente como um serviço de documento. As novas APIs são:

* **protectDocumentUse** a API ProtectDocument para que você possa aplicar uma política a um documento em nome de

  outra conta de usuário. As permissões da conta de usuário usada para aplicar a política permanecem limitadas à proteção do documento. Ele não tem o direito de abrir e visualizar o documento. RMSecureDocumentResult protectDocument(Document inDoc, String documentName, String policySetName, String policyName, RMLocale locale, booleano bExactMatchForNames)

* **createLicenseUse** Use a API CreateLicense para criar uma licença para uma política em nome de outra conta de usuário. PublishLicenseDTO createLicense(String policyId, String documentName, booleano logSecureDocEvent)
* **protectDocumentWithCoverPageUse** Use a API ProtectDocumentWithCoverPage para aplicar uma política e adicionar uma página de capa a um documento em nome de outro usuário. As permissões da conta de usuário usada para aplicar a política permanecem limitadas à proteção do documento. Ele não tem o direito de abrir e visualizar o documento. RMSecureDocumentResult protectDocumentWithCoverPage(Documento no documento, Nome do documento da cadeia de caracteres, Nome do conjunto de políticas da cadeia de caracteres, Nome da política da cadeia de caracteres, Documento coverDoc, Booleano bExactMatchForNames)

## Uso das APIs para proteger um documento em nome de outro usuário {#using-the-apis-to-protect-a-document-on-behalf-of-another-user}

Faça o seguinte para proteger um documento em nome de outro usuário e sem obter as permissões para editar o documento:

1. Criar um conjunto de políticas. Por exemplo, PolicySet1.
1. Crie uma política no conjunto de políticas recém-criado. Por exemplo, Política1 em PolicySet1.
1. Crie um usuário com a função Rights Management Usuário final. Por exemplo, User1. Forneça ao usuário recém-criado as permissões para visualizar documentos protegidos usando a Política 1.
1. Crie uma função. Por exemplo, Função1. Forneça a permissão Chamar serviço para a função recém-criada. Crie um usuário com a função recém-criada. Por exemplo, Usuário2. Você pode usar o Usuário2 ou um administrador para criar uma conexão com o SDK e chamar o serviço protectDocument.

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
