---
title: Use o HSM para assinar digitalmente ou certificar documentos
seo-title: Use HSM to certify eSigned documents
description: Usar dispositivos HSM ou de token para certificar documentos assinados eletronicamente
seo-description: Use HSM or etoken devices to certify eSigned documents
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
exl-id: 4d423881-18e0-430a-849d-e1762366a849
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# Use o HSM para assinar digitalmente ou certificar documentos {#use-hsm-to-digitally-sign-or-certify-documents}

Os módulos de segurança de hardware (HSM) e os etokens são dispositivos de computação dedicados, rígidos e resistentes à violação projetados para gerenciar, processar e armazenar chaves digitais com segurança. Esses dispositivos são conectados diretamente a um computador ou servidor de rede.

A Adobe Experience Manager Forms pode usar credenciais armazenadas em um HSM ou token para assinar ou aplicar assinaturas digitais do lado do servidor a um documento. Para usar um HSM ou dispositivo de token com o AEM Forms:

1. Habilite o serviço DocAssurance.
1. Configurar certificados para a extensão Reader.
1. Crie um alias para o HSM ou dispositivo de token AEM Web Console.
1. Use as APIs do serviço de garantia de documentos para assinar ou certificar os documentos com chaves digitais armazenadas no dispositivo.

## Antes de configurar os dispositivos HSM ou de token com o AEM Forms {#configurehsmetoken}

* Instalar [Complemento do AEM Forms](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) pacote.
* Instale e configure o software cliente HSM ou etoken no mesmo computador que o servidor AEM. O software cliente é necessário para se comunicar com os dispositivos HSM e de token.
* (Somente Microsoft Windows) Defina a variável de ambiente JAVA_HOME_32 para apontar para o diretório onde a versão de 32 bits do Java 8 Development Kit (JDK 8) está instalada. O caminho padrão do diretório é C:\Program Files(x86)\Java\jdk&lt;version>
* (AEM Forms somente em OSGi) Instale o certificado raiz no armazenamento de confiança. É necessário verificar o PDF assinado

>[!NOTE]
>
>No Microsoft Windows, somente clientes LunaSA ou EToken de 32 bits são compatíveis.

## Ativar o serviço DocAssurance {#configuredocassurance}

Por padrão, o serviço DocAssurance não está ativado. Execute as seguintes etapas para habilitar o serviço:

1. Pare a instância Autor do seu ambiente AEM Forms.

1. Abra o [AEM_root]\crx-quickstart\conf\sling.properties para edição.

   >[!NOTE]
   >
   >Se tiver usado o [AEM_root]\crx-quickstart\bin\start.bat para iniciar a instância do AEM e abra o [AEM_root]\crx-quickstart\sling.properties para edição.

1. Adicione ou substitua as seguintes propriedades ao arquivo sling.properties :

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Salve e feche o arquivo sling.properties .
1. Reinicie a instância de AEM.

## Configurar certificados para extensões do Reader {#set-up-certificates-for-reader-extensions}

Execute as seguintes etapas para configurar certificados:

1. Faça logon na instância do AEM Author como administrador.

1. Clique em **Adobe Experience Manager** na Barra de Navegação Global. Ir para **Ferramentas** >  **Segurança** >  **Usuários**.
1. Clique no botão **name** do campo da conta do usuário. O **Editar configurações de usuário** será aberta.
1. Na instância do autor do AEM, os certificados residem em um KeyStore. Se você não criou um KeyStore anteriormente, clique em **Criar KeyStore** e defina uma nova senha para o KeyStore. Se o servidor já tiver um KeyStore, pule esta etapa.

1. No **Editar configurações de usuário** página, clique em **Gerenciar KeyStore**.

1. Na caixa de diálogo Gerenciamento do KeyStore , expanda a **Adicionar chave privada do arquivo de armazenamento de chaves** e forneça um alias. O alias é usado para executar a operação Reader Extensions .
1. Para fazer upload do arquivo de certificado, clique em **Selecionar arquivo de armazenamento de chaves** e fazer upload de um `.pfx` arquivo.
1. Adicione o **Senha do Armazenamento de Chaves**,**Senha da chave privada** e **Alias da chave privada** que está associada ao certificado aos respectivos campos. Clique em **Enviar**.

   >[!NOTE]
   >
   >Para determinar a **Alias da Chave de Recuperação** de um certificado, você pode usar o comando keytool do Java: `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >No **Senha do Armazenamento de Chaves** e **Senha da chave privada** especifique a senha fornecida com o arquivo de certificado.

>[!NOTE]
>
>Para AEM Forms no OSGi, para verificar o PDF assinado, o certificado raiz instalado no Armazenamento de confiança.

>[!NOTE]
>
>Ao migrar para o ambiente de produção, substitua suas credenciais de avaliação por credenciais de produção. Certifique-se de excluir suas credenciais antigas das extensões do Reader antes de atualizar uma credencial expirada ou de avaliações.

## Criar um alias para o dispositivo {#configuredeviceinaemconsole}

O alias contém todos os parâmetros que um HSM ou um token requer. Execute as instruções listadas abaixo para criar um alias para cada credencial do HSM ou do token que o eSign ou o Digital Signatures usa:

1. Abra AEM console. O URL padrão AEM console é https://&lt;host>:&lt;port>/system/console/configMgr
1. Abra o **Serviço de configuração de credenciais do HSM** e especifique os valores para os seguintes campos:

   * **Alias da Credencial**: Especifique uma string usada para identificar o alias. Esse valor é usado como uma propriedade para algumas operações de Assinaturas Digitais, como a operação Assinar campo de assinatura.
   * **Caminho DLL**: Especifique o caminho totalmente qualificado de sua biblioteca do cliente HSM ou de tokens no servidor. Por exemplo, C:\Program Files\LunaSA\cryptoki.dll. Em um ambiente em cluster, esse caminho deve ser idêntico para todos os servidores no cluster.
   * **Pino do HSM**: Especifique a senha necessária para acessar a chave do dispositivo.
   * **Id do slot do HSM**: Especifique um identificador de slot do tipo inteiro. A ID do slot é definida cliente a cliente. Se você registrar uma segunda máquina em uma partição diferente (por exemplo, HSMPART2 no mesmo dispositivo HSM), o slot 1 será associado à partição HSMPART2 para o cliente.

   >[!NOTE]
   >
   >Ao configurar o Etoken, especifique um valor numérico para o campo ID do slot do HSM. É necessário um valor numérico para fazer com que as operações de Assinaturas funcionem.

   * **Certificado SHA1**: Especifique o valor SHA1 (impressão digital) do arquivo de chave pública (.cer) para a credencial que você está usando. Certifique-se de que não haja espaços usados no valor SHA1. Se você estiver usando um certificado físico, ele não será necessário.
   * **Tipo de dispositivo HSM**: Selecione o fabricante do HSM (Luna ou outro) ou do dispositivo eToken.

   Clique em **Salvar**. O módulo de segurança de hardware está configurado para o AEM Forms. Agora, você pode usar o módulo de segurança de hardware com o AEM Forms para assinar ou certificar documentos.

## Use as APIs do serviço de garantia de documentos para assinar ou certificar um documento com chaves digitais armazenadas no dispositivo  {#programatically}

O código de exemplo a seguir usa um HSM ou um token para assinar ou certificar um documento.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.IOException;
import java.io.InputStream;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * Digital signatures can be applied to PDF documents to provide a level of security. Digital signatures, like handwritten signatures, provide a means by which signers
 * identify themselves and make statements about a document. The technology used to digitally sign documents helps to ensure that both the signer and recipients are clear
 * about what was signed and confident that the document was not altered since it was signed.
 *
 * PDF documents are signed by means of public-key technology. A signer has two keys: a public key and a private key. The private key is stored in a user's credential that
 * must be available at the time of signing. The public key is stored in the user's certificate that must be available to recipients to validate the signature. Information
 * about revoked certificates is found in certificate revocation lists (CRLs) and Online Certificate Status Protocol (OCSP) responses distributed by Certificate Authorities (CAs).
 * The time of signing can be obtained from a trusted source known as a Timestamping Authority.
 *
 * The following Java code example digitally signs a PDF document that is based on a PDF file.
 * The alias that is specified for the security credential is secure, and revocation checking is performed.
 * Because no CRL or OCSP server information is specified, the server information is obtained from the certificate used to
 * digitally sign the PDF document
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=Sign.class)
public class Sign{
 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at JCR node
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void signExtend(String inputFile, String outputFile, String alias) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  Document inDoc = new Document(inputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //as we don't want encryption in this case, passing null for Encryption Options
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, null, getSignatureOptions(alias,resourceResolver),null,null);
        }
  catch(Exception e){
   e.printStackTrace();
  }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        //flush the output document contents to JCR Node
  flush(outDoc, outputFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(String alias, ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr, true));
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
    /**
     * This method copies the data from {@code Document}, to the specified file at the given resourcePath.
     * @param doc
     * @param resourcePath
     * @throws IOException
     */
    private void flush(Document doc, String resourcePath) throws IOException {
   //extracts the byte data from Document
   byte[] output = doc.getInlineData();
   Binary opBin;
   Session adminSession = null;
      try {
         adminSession = slingRepository.loginAdministrative(null);

         //get access to the specific node
         //here we are assuming that node exists
           Node node = adminSession.getNode(resourcePath);

           //convert byte[] to Binary
           opBin = adminSession.getValueFactory().createBinary((InputStream)new ByteArrayInputStream(output));

           //set the Binary data value to node's jcr:data
           node.getNode("jcr:content").getProperty("jcr:data").setValue(opBin);
      } catch (RepositoryException e) {

      }
      finally{

       if(adminSession != null && adminSession.isLive()){
        try {
      adminSession.save();
      adminSession.logout();
     } catch (RepositoryException e) {

     }

             }
      }

  }
}
```

Se você atualizou de AEM 6.0 Form ou AEM 6.1 Forms e estava usando o serviço DocAssurance na versão anterior, então:

* Para usar o serviço DocAssurance sem um HSM ou dispositivo de token, continue usando o código existente.
* Para usar o serviço DocAssurance com um HSM ou dispositivo de token, substitua o código de objeto CredencialContext existente pela API listada abaixo.

```java
/**
  *
  * @param credentialAlias alias of the PKI Credential stored in CQ Key Store or
  * the alias of the HSM Credential configured using HSM Credentials Configuration Service.
  * @param resourceResolver corresponding to the user with the access to the key store and trust store.
  * @param isHSMCredential if the alias is corresponding to HSM Credential.
  */
 public CredentialContext(String credentialAlias, ResourceResolver resourceResolver, boolean isHSMCredential);
```

Para obter informações detalhadas sobre APIs e código de amostra do serviço DocAssurance, consulte [Uso do AEM Document Services Programaticamente](/help/forms/using/aem-document-services-programmatically.md).
