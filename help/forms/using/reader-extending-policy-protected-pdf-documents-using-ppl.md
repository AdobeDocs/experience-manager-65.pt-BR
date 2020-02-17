---
title: O Reader estende documentos PDF protegidos por política usando a Biblioteca de proteção portátil
seo-title: O Reader estende documentos PDF protegidos por política usando a Biblioteca de proteção portátil
description: As extensões do Reader permitem recursos interativos em documentos Adobe PDF por meio do Acrobat Reader. Você pode usar a Biblioteca de proteção portátil (PPL) para ler a extensão dos documentos PDF protegidos por DRM.
seo-description: As extensões do Reader permitem recursos interativos em documentos Adobe PDF por meio do Acrobat Reader. Você pode usar a Biblioteca de proteção portátil (PPL) para ler a extensão dos documentos PDF protegidos por DRM.
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# O Reader estende documentos PDF protegidos por política usando a Biblioteca de proteção portátil {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library}

É necessário conhecer os conceitos de segurança do documento, extensão do leitor e linguagem de programação Java para que o leitor estenda os documentos PDF protegidos por política de segurança do documento.

Você pode usar a segurança do documento para restringir o acesso de documentos PDF específicos somente a usuários autorizados. Você também pode determinar como um destinatário pode usar um documento protegido. Por exemplo, você pode especificar se os destinatários podem imprimir, copiar ou editar o texto de um documento protegido por política de segurança do documento. Para saber mais sobre segurança de documentos, consulte [sobre segurança](/help/forms/using/admin-help/document-security.md)de documentos.

Você pode usar extensões de leitores para ativar recursos interativos no documento Adobe PDF por meio do Acrobat Reader. Esses recursos interativos normalmente estão disponíveis somente pelo Adobe Acrobat Professional e Standard. Para saber mais sobre os recursos interativos que a extensão do leitor pode ativar, consulte o serviço [DocAssurance do](/help/forms/using/overview-aem-document-services.md)**Adobe Experience Manager Forms.**

Você pode usar a biblioteca de proteção portátil para aplicar políticas no documento, sem a necessidade de documentos viajando pela rede. Apenas as credenciais de segurança e os detalhes da política de proteção viajam pela rede. O documento real nunca deixa o cliente e as políticas de proteção são aplicadas localmente no cliente.

## O Reader estende documentos PDF protegidos por política de segurança do documento {#reader-extending-document-security-policy-protected-pdf-documents}

Os documentos protegidos por política são documentos criptografados. Não é possível usar APIs padrão de extensão de leitor para aplicar, remover e recuperar direitos de uso de documentos PDF protegidos por política. Somente o serviço Reader Extensions da Biblioteca de Proteção Portátil fornece APIs para aplicar, remover e recuperar direitos de uso de documentos PDF protegidos por política de segurança do documento.

### Serviço Reader Extensions {#reader-extensions-service}

O serviço de extensão do leitor adiciona direitos de uso a um documento PDF protegido por política, ativando recursos que normalmente não estão disponíveis quando um documento PDF é aberto usando o Adobe Acrobat Reader. Ele também tem APIs para remover e recuperar direitos de uso de um documento protegido por política.

O serviço Reader Extensions oferece suporte total a documentos PDF com base no padrão PDF 1.6 e posterior. Além do Acrobat Reader, os usuários de terceiros não exigem software ou plug-ins adicionais para usar os documentos PDF protegidos por política.

É possível realizar as seguintes tarefas com o serviço Reader Extensions:

* Aplique direitos de uso a um documento PDF protegido por política.
* Remova os direitos de uso de um documento PDF protegido por política.
* Recuperar direitos de uso aplicados a um documento PDF protegido por política.

### Aplicar direitos de uso a um documento PDF protegido por política de segurança de documento {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

Você pode usar a API `applyUsageRights`Java para aplicar direitos de uso a documentos PDF protegidos por política. Os direitos de uso pertencem à funcionalidade que está disponível por padrão no Acrobat, mas não no Adobe Reader, como a capacidade de adicionar comentários a um formulário ou preencher campos de formulário e salvar o formulário. Os documentos PDF que têm direitos de uso aplicados a eles são chamados de documentos habilitados por direitos. Um usuário que abre um documento habilitado para direitos no Adobe Reader pode executar operações ativadas para esse documento específico.

**** Sintaxe: `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parâmetro</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>Especifique InputStream que representa o documento PDF ao qual os direitos de uso devem ser aplicados. Você pode usar documentos protegidos por segurança do documento do LiveCycle Rights Management ou do AEM Forms.</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>Especifique o objeto File que representa um arquivo .jks. O arquivo .jks é um arquivo keystore. Ele aponta para um certificado que concede direitos de uso.</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>Especifique a senha do armazenamento de chaves. </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p>Especifica um objeto do tipo <a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a>. O objeto usageRights representa direitos individuais que podem ser aplicados a um documento PDF protegido por política.</p> </td>
  </tr>
 </tbody>
</table>

### Recuperar direitos de uso aplicados a um documento PDF protegido por política.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

Você pode usar a API `getDocumentUsageRights`Java para recuperar os direitos de uso da extensão do leitor aplicados a um documento PDF protegido por política. Ao recuperar informações sobre direitos de uso, você pode saber mais sobre os recursos que a extensão do leitor habilitou para o documento PDF protegido por política.

**** Sintaxe: `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parâmetro</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>Especifique InputStream que representa o documento PDF a partir do qual os direitos de uso devem ser recuperados. Você pode usar documentos protegidos por segurança do documento do LiveCycle Rights Management ou do AEM Forms.</p> </td>
  </tr>
 </tbody>
</table>

#### Exemplo de código {#code-sample}

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

System.out.println("UsageRights applied successfully to the document. ”);
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

### Remover direitos de uso de um documento PDF protegido por política {#remove-usage-rights-of-a-policy-protected-pdf-document}

Você pode usar a API `removeUsageRights`Java para remover direitos de uso de um documento protegido por política. A remoção de direitos de uso de um documento PDF protegido por política é necessária para executar outras operações do AEM Forms no documento. Por exemplo, você deve assinar digitalmente (ou certificar) um documento PDF antes de definir direitos de uso. Portanto, se você quiser executar operações em um documento protegido por política, remova os direitos de uso do documento PDF, execute as outras operações, como assinar digitalmente o documento e aplique novamente os direitos de uso ao documento.

**** Sintaxe: `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>Parâmetro</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>Especifique InputStream que representa o documento PDF a partir do qual os direitos de uso<br /> devem ser removidos. Você pode usar documentos protegidos por segurança do documento do LiveCycle Rights Management ou do AEM Forms.</td>
  </tr>
 </tbody>
</table>

#### Exemplo de código {#code-sample-1}

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
System.out.println("RE rights removed successfully from the document.”);
outputStream.close();
inputFileStream.close();
```

