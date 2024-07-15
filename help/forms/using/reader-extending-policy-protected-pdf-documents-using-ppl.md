---
title: Reader estendendo documentos PDF protegidos por política usando a Biblioteca de proteção portátil
description: As extensões Reader habilitam recursos interativos em documentos do Adobe PDF por meio do Acrobat Reader. Você pode usar a Portable Protection Library (PPL) para estender os documentos de PDF protegidos do DRM.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Security,Reader Extensions
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Reader estendendo documentos PDF protegidos por política usando a Biblioteca de proteção portátil {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

Familiarize-se com os conceitos de segurança de documentos, extensão do leitor e linguagem de programação Java para ler e estender os documentos de PDF protegidos por política de segurança de documentos.

Você pode usar a segurança de documentos para restringir o acesso de documentos específicos do PDF somente a usuários autorizados. Você também pode determinar como um destinatário pode usar um documento protegido. Por exemplo, você pode especificar se os destinatários podem imprimir, copiar ou editar o texto de um documento protegido por política de segurança de documentos. Para saber mais sobre segurança de documentos, consulte [sobre segurança de documentos](/help/forms/using/admin-help/document-security.md).

Você pode usar extensões de leitor para ativar recursos interativos no documento do Adobe PDF por meio do Acrobat Reader. Esses recursos interativos que normalmente estão disponíveis apenas no Adobe Acrobat Professional e Standard. Para saber mais sobre os recursos interativos que a extensão do Reader pode habilitar, consulte [serviço Adobe Experience Manager Forms DocAssurance ](/help/forms/using/overview-aem-document-services.md)**.**

Você pode usar a biblioteca de proteção portátil para aplicar políticas no documento sem a necessidade de documentos que viajem pela rede. Somente credenciais de segurança e detalhes de políticas de proteção viajam pela rede. O documento real nunca sai do cliente e as políticas de proteção são aplicadas localmente no cliente.

## Reader estendendo documentos PDF protegidos por política de segurança de documentos {#reader-extending-document-security-policy-protected-pdf-documents}

Os documentos protegidos por política são documentos criptografados. Não é possível usar APIs de extensão de leitor padrão para aplicar, remover e recuperar direitos de uso de documentos PDF protegidos por política. Somente o serviço Reader Extensions da Portable Protection Library fornece APIs para aplicar, remover e recuperar direitos de uso de documentos PDF protegidos por política de segurança de documentos.

### Serviço de extensões do Reader {#reader-extensions-service}

O serviço de extensão do Reader adiciona direitos de uso a um documento PDF protegido por política, ativando recursos que normalmente não estão disponíveis quando um documento PDF é aberto usando o Adobe Acrobat Reader. Ele também tem APIs para remover e recuperar direitos de uso de um documento protegido por política.

O serviço de extensões do Reader suporta totalmente os documentos do PDF baseados no PDF padrão 1.6 e mais recente. Além do Acrobat Reader, os usuários de terceiros não exigem nenhum software ou plug-in adicional para usar os documentos PDF protegidos por política.

Você pode realizar as seguintes tarefas com o serviço de extensões Reader:

* Aplique direitos de uso a um documento PDF protegido por política.
* Remova os direitos de uso de um documento PDF protegido por política.
* Recuperar direitos de uso aplicados a um documento PDF protegido por política.

### Aplicar direitos de uso a um documento PDF protegido por política de segurança de documentos {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

Você pode usar a `applyUsageRights`API Java para aplicar direitos de uso a documentos PDF protegidos por política. Os direitos de uso pertencem à funcionalidade que está disponível por padrão no Acrobat, mas não no Adobe Reader, como a capacidade de adicionar comentários a um formulário ou preencher campos de formulário e salvar o formulário. os documentos PDF que têm direitos de uso aplicados a eles são chamados de documentos habilitados por direitos. Um usuário que abre um documento com direitos ativados no Adobe Reader pode executar operações ativadas para esse documento específico.

**Sintaxe:** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parâmetro</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>Especifique InputStream que representa o documento PDF ao qual os direitos de uso devem ser aplicados. Você pode usar o LiveCycle do Rights Management ou o AEM Forms documentos protegidos por segurança de documentos.</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>Especifique o objeto File que representa um arquivo .jks. O arquivo .jks é um arquivo de armazenamento de chaves. Ele aponta para um certificado que concede direitos de uso.</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>Especifique a senha do keystore. </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>Especifica um objeto do tipo <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>. O objeto usageRights representa direitos individuais que podem ser aplicados a um documento PDF protegido por política.</p> </td>
  </tr>
 </tbody>
</table>

### Recuperar direitos de uso aplicados a um documento PDF protegido por política.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

Você pode usar a `getDocumentUsageRights`API Java para recuperar os direitos de uso da extensão do leitor aplicados a um documento PDF protegido por política. Ao recuperar informações sobre direitos de uso, você pode saber mais sobre os recursos que a extensão do leitor habilitou para o documento PDF protegido por política.

**Sintaxe:** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parâmetro</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>Especifique InputStream que representa o documento PDF do qual os direitos de uso devem ser recuperados. Você pode usar o LiveCycle do Rights Management ou o AEM Forms documentos protegidos por segurança de documentos.</p> </td>
  </tr>
 </tbody>
</table>

#### Amostra de código {#code-sample}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\protected.pdf"; //Input file can be RM protected or unprotected pdf file
File certFile = new File("C:\\Sample\\cert.jks"); //RE certificate file
String password = "password"; //password for RE certificate
UsageRights usageRights = getUsageRights(true,true,false,false,true,true,false,false,false,false,true);

//RE rights to be applied on the file : FormFillIn, FormDataImportExport, SubmitStandalone, OnlineForms, DynamicFormField, DynamicFormPages, BarcodeDecoding, DigitalSignatures, Comments, CommentsOnline, EmbeddedFiles

InputStream inputFileStream = new FileInputStream(inputFileName);
InputStream output = rmClient2.getRightsManagementReaderExtensionService().applyUsageRights(inputFileStream, certFile, credentialPassword, rights);

String outputFileName = "C:\\Sample\\ReAdded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = output.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}

System.out.println("UsageRights applied successfully to the document. ");
 outputStream.close();
inputFileStream.close();

//Get Usage Rights for the output pdf document
InputStream fileWithRe = new FileInputStream(myFile);

GetUsageRightsResult usageRights = rmClient2.getRightsManagementReaderExtensionService().getDocumentUsageRights(fileWithRe);

UsageRights rights = usageRights.getRights();
String right1 = rights1.toString();
System.out.println("RE rights for the file are :\n"+right1);
 fileWithRe.close();
```

### Remover direitos de uso de um documento de PDF protegido por política {#remove-usage-rights-of-a-policy-protected-pdf-document}

Você pode usar a `removeUsageRights`API Java para remover direitos de uso de um documento protegido por política. A remoção de direitos de uso de um documento de PDF protegido por política é necessária para executar outras operações do AEM Forms no documento. Por exemplo, você deve assinar digitalmente (ou certificar) um documento PDF antes de definir os direitos de uso. Portanto, se você quiser executar operações em um documento protegido por política, remova os direitos de uso do documento PDF, execute as outras operações, como assinar digitalmente o documento e reaplique os direitos de uso ao documento.

**Sintaxe:** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parâmetro</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>Especifique InputStream que representa o documento PDF do qual os direitos de uso <br /> devem ser removidos. Você pode usar o LiveCycle do Rights Management ou o AEM Forms documentos protegidos por segurança de documentos.</td>
  </tr>
 </tbody>
</table>

#### Amostra de código {#code-sample-1}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\fileWithRe.pdf"; //Input file can be RM protected or unprotected pdf file
InputStream inputFileStream = new FileInputStream(inputFileName);

InputStream fileStream = rmClient2.getRightsManagementReaderExtensionService().removeUsageRights(inputFileStream);

String outputFileName = "C:\\Sample\\ReRemoveded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = fileStream.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}
System.out.println("RE rights removed successfully from the document.");
outputStream.close();
inputFileStream.close();
```
