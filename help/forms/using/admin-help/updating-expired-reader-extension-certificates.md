---
title: Expiração dos certificados de extensões Reader e seu impacto
description: Expiração dos certificados de extensões Reader e seu impacto
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: f35a35577f06686558bb1277b0d9bb17f6f0b7bf
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 2%

---


# Expiração dos certificados de extensões Reader e seu impacto {#expiration-of-reader-extensions-certificates-and-its-impact}

Os clientes da Adobe Experience Manager Forms (AEM Forms) com o Adobe Managed Services ou licenças no local da Enterprise Base têm direito de usar o serviço de extensões da Acrobat Reader DC. O serviço permite que uma organização compartilhe facilmente documentos interativos do PDF, estendendo a funcionalidade do Acrobat Reader com direitos de uso adicionais. O serviço adiciona direitos de uso a um documento do PDF e ativa recursos que não estão disponíveis quando um documento do PDF é aberto usando o Adobe Acrobat Reader, como adicionar comentários a um documento, preencher formulários e salvar o documento. Usuários de terceiros não exigem software ou plug-ins adicionais para trabalhar com documentos ativados por direitos. Os documentos do PDF com direitos de uso adicionados são chamados de documentos ativados por direitos. Um usuário que abre um documento do PDF habilitado para direitos no Acrobat Reader pode executar as operações ativadas para esse documento.

O Adobe utiliza uma PKI (infraestrutura de chave pública) para emitir certificados digitais para uso em licenciamento e ativação de recursos. A Adobe está emitindo certificados sob a autoridade de certificação &quot;Adobe Root CA&quot;, que expira em 7 de janeiro de 2023. Uma nova autoridade de certificação, &quot;Adobe Root CA G2&quot;, e certificados baseados na nova autoridade de certificação estão disponíveis.

Certificados antigos (certificados baseados em &quot;CA Adobe&quot;) não funcionam mais após 7 de janeiro de 2023. A Adobe recomenda que você comece a usar os novos certificados — aqueles baseados em &quot;Adobe Root CA G2&quot; — para Reader estender seus documentos do PDF em ou antes de 7 de janeiro de 2023.  Você pode [obter novos certificados do site de licenciamento de Adobe](https://licensing.adobe.com/) ou Suporte ao Adobe.

Todos os documentos do PDF, Reader estendidos usando os certificados mais antigos antes de 7 de janeiro de 2023, incluindo os baixados pelos clientes, continuariam a funcionar com todos os direitos de uso que são aplicados a eles e não exigiriam atualizações.

## Perguntas frequentes

**P. Qual é a diferença entre um certificado de raiz Adobe e um certificado de extensões Acrobat Reader? O certificado raiz Adobe depende de um certificado de extensões Acrobat Reader? Ambos os certificados estão expirando em janeiro de 2023?**

A. CA raiz Adobe é a autoridade de certificação da qual um certificado de extensões Acrobat Reader é emitido. Em 7 de janeiro de 2023, &quot;Adobe Root CA&quot; e todos os certificados emitidos a partir dele estão expirando.

**P. Houve uma comunicação anterior do Adobe sobre a expiração dos certificados e o impacto na utilização/abertura de documentos do PDF. Essa comunicação deveria ser ignorada?**
A. Com base na reavaliação da situação, todos os documentos de PDF estendidos por meio de certificados de produção emitidos pela antiga &quot;Adobe Root CA&quot; antes de 7 de janeiro de 2023 continuam a funcionar sem qualquer alteração após 7 de janeiro de 2023. Se você já atualizou suas PDF, não haverá mudança na experiência

**P. Com quem devo entrar em contato se tiver perguntas adicionais?**

A. Você pode entrar em contato [Suporte a Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=pt-BR#support) ou crie um tíquete de suporte.

**P. O que acontece se eu não atualizar meu certificado antes de 7 de janeiro de 2023?**

A. Todos os documentos de PDF estendidos por meio de certificados de produção emitidos da antiga &quot;CA Adobe Root&quot; antes de 7 de janeiro de 2023 continuam a funcionar sem alterações após 7 de janeiro de 2023. PDF estendido com certificados de avaliação não funciona após a data de expiração.

**P. A descrição dos novos certificados é diferente dos antigos?**

A. A descrição dos novos certificados de Extensões do Acrobat Reader menciona **G3-P24** como o nome do programa. Na descrição de certificados mais antigos (certificados baseados em &quot;Adobe Root CA&quot;), **P24** é mencionado como o nome do programa.

**P. Como obter os certificados mais recentes?**

A. Todos os clientes da Forms qualificados (com licença ativa) podem baixar os novos certificados (certificados baseados em &quot;Adobe Root CA G2&quot;) da [Site de licenciamento de Adobe](https://licensing.adobe.com/). Se você não conseguir encontrar o certificado no site de licenciamento do Adobe, entre em contato com [Suporte a Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=en#support) ou crie um tíquete de suporte.

**P. Meus documentos de PDF estendidos usando certificados emitidos do &quot;Adobe Root CA&quot; (a antiga autoridade de certificação) continuam a funcionar após 7 de janeiro de 2023?**

R. Sim, todos os documentos de PDF estendidos usando certificados de produção emitidos da &quot;autoridade de certificação Adobe Root&quot; (antiga autoridade de certificação) antes de 7 de janeiro de 2023 continuam a funcionar sem qualquer alteração após 7 de janeiro de 2023. Os documentos de PDF estendidos com certificados de avaliação não funcionam após a data de expiração.

**P. Qual versão do Adobe Acrobat Reader é necessária para continuar usando documentos PDF estendidos com certificados emitidos de &quot;Adobe Root CA&quot; (a antiga autoridade de certificação)?**

A. O Adobe Acrobat Reader 2020 ou posterior é necessário para usar documentos PDF estendidos com &quot;Adobe Root CA&quot; (a antiga autoridade de certificação). É a versão compatível do Acrobat Reader no momento da publicação deste documento. Se estiver usando um [versão não compatível do Adobe Acrobat](https://helpx.adobe.com/br/support/programs/eol-matrix.html), o Adobe recomenda que você [baixar e instalar a versão mais recente do Adobe Acrobat Reader](https://get.adobe.com/reader/).

**P. Qual versão do Adobe Acrobat Reader é necessária para continuar usando documentos PDF estendidos com certificados emitidos de &quot;Adobe Root CA 2&quot; (a nova autoridade de certificação)?**

A. O Adobe Acrobat Reader 2020 ou posterior é necessário para usar documentos PDF estendidos com &quot;Adobe Root CA 2&quot; (a nova autoridade de certificação). Se estiver usando um [versão não compatível do Adobe Acrobat Reader](https://helpx.adobe.com/support/programs/eol-matrix.html), o Adobe recomenda que você [baixar e instalar a versão mais recente do Adobe Acrobat Reader](https://get.adobe.com/reader/).

**P. Posso excluir um certificado antigo de extensões do Acrobat Reader e adicionar um novo em um Servidor Adobe Experience Manager Forms enquanto continuo usando o alias existente?**

R. Sim, você pode excluir um certificado antigo de Extensões do Acrobat Reader e adicionar um novo com o alias existente a um Adobe Experience Manager Forms Server.

**P. Posso manter certificados de extensões Acrobat Reader novos e antigos em um servidor Adobe Experience Manager Forms?**

R. Sim, você pode manter ambos os certificados, mas com aliases diferentes, em um Servidor Adobe Experience Manager Forms. Após 7 de janeiro de 2023, você poderá usar somente o novo certificado para estender Reader um documento de PDF.

**P. Posso importar o mesmo certificado de extensões do Acrobat Reader para todos os ambientes Adobe Experience Manager Forms?**

R. Sim, o mesmo certificado de extensões do Acrobat Reader pode ser usado em vários ambientes.

**P. Como faço para verificar os direitos de uso aplicados a um documento do PDF?**

A. Você pode usar o [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=en#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) API para recuperar as informações sobre os direitos de uso aplicados a um documento do PDF.

**P. Como faço para alterar a senha de um arquivo de certificado das extensões do Acrobat Reader?**

R. No Microsoft Windows, para alterar a Senha do certificado, instale o certificado usando o Console de Gerenciamento do Microsoft (MMC) e selecione **Marcar a chave como exportável**. Depois de instalado, exporte o certificado com uma chave privada e use outra senha para o arquivo PFX.


<!-- 
## Applying the certificates {#obtaning-and-applying-the-certificates} 

You can choose one of the following paths to apply latest certificates:

* [Updating certificates for an AEM Forms on JEE environment](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment) 
* [Updating certificates for an AEM Forms on OSGi environment](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>The document uses the term certificates and credentials interchangeably.

### Pre-requisites {#Pre-requisites}

Updating the certificates requires using actions available on AEM Forms administrator console and Reader Extension APIs provided by AEM Forms. The document is intended for users and administrators with knowledge of using Adobe Experience Manger Forms APIs. Before you start, ensure that: 

* the user has administrator rights on underlying AEM Forms environment. 
* the user has setup the [development environment](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) and has access to it.
* [obtain the certificates](#obtain-the-certificates).


### Obtain the certificates {#obtain-the-certificates}

The Rights credential is delivered as a digital certificate that contains the public key, the private key, and the password used to access the credential.

If your organization purchases a production version of Reader Extensions, the production Rights credential is delivered by Adobe Licensing Website (LWS). A production Rights credential is unique to your organization and can enable the specific usage rights that you require.

If you obtained Reader Extensions through a partner or software provider who integrated Reader Extensions into their software, the Rights credential is provided to you by that partner who, in turn, receives this credential from Adobe.

>[!NOTE]
>
>The Rights credential cannot be used for typical document signing or assertion of identity. For these applications, you can use a self-sign certificate or acquire an identity certificate from a Certificate Authority (CA).

The following types of Rights credentials are available:

**Customer Evaluation**: A credential with a short validity period that is provided to customers who want to evaluate Reader Extensions. Usage rights applied to documents using this credential expire when the credential expires. This type of credential is valid only for two to three months.

**Production**: A credential with a long validity period that is provided to customers who purchased the full product. Production credentials are unique to each customer but can be installed on multiple systems.

If you have already used certificates to reader extend PDF files, download a production certificate from [Adobe Licensing Website (LWS)](https://licensing.adobe.com/).

### Applying certificates for an AEM Forms on JEE environment {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment} 

Applying new certificates on AEM Forms on JEE stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import and configure credentials 

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. You must designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

* If you import a Reader Extensions credential and the Trust Store contains no other Reader Extensions credentials, it is set as the default.
* If you import a Reader Extensions credential with the Default option selected, the default type is removed from an existing default credential. The imported credential becomes the default.
* You cannot delete a default Reader Extensions credential. To delete the default credential, first set another credential as the default. An exception to this rule is that if there is only one credential, you can delete it even though it is the default.
* You cannot update a default Reader Extensions credential.

To import the credentials: 

1. In administration console, click Settings > Trust Store Management > Local Credentials.
1. Click Import and, under Trust Store Type, select Acrobat Reader DC extensions Credential.
1. (Optional) To indicate that this credential is the default credential to use with Acrobat Reader DC extensions, select Default.
1. In the Alias box, type an identifier for the credential. This identifier is used as the display name for the credential in Acrobat Reader DC extensions. This alias is also used to access the credential programmatically using the AEM forms SDK.
1. Click Choose File to locate the credential, type the password of the credential, and then click OK.

If the error message "Failed to import credential due to either incorrect file format, or incorrect password" appears, verify that the password is valid.

You can also import and delete credentials programmatically. (See [Programming with AEM forms](../../developing/credentials.md).)

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. AEM Forms on JEE provides APIs to remove usage rights. For detailed instructions, see [Removing Usage Rights from PDF Documents](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

To remove usage rights for AEM Forms on JEE processes developed in Workbench, see [Workbench Help](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf). 

#### Apply the usage rights to PDF documents 

After importing new credentials, you can apply usage rights to PDF documents using the Acrobat Reader DC extensions Java Client API and web service.  For details, see [Applying Usage Rights to PDF Documents](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents). 


### Applying certificates for an AEM Forms on OSGi environment {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

Applying new certificates on AEM Forms on OSGi stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import credentials {#Import-credentials}

In an AEM Forms on OSGi environment, a Reader Extension credential is associated with fd-service user. Before adding credentials for fd-user key store, perform the following steps to create a key store: 

1. Log in to your AEM Author instance as an Administrator.
1. Go to **[!UICONTROL Tools]**> **[!UICONTROL Security]**>**[!UICONTROL Users]**.
1. Scroll down the list of users until you find fd-service user account.
1. Click **[!UICONTROL fd-service]** user.
1. Click keystore tab.
1. Click **[!UICONTROL Create KeyStore]**.
1. Set the KeyStore Access Password and save your settings to create the KeyStore password.

After creating the key-store, add credentials to fd-service user. The following video explains the steps: 

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

The following command list the details of the pfx file. Before running the command, navigate to the directory that contains the .pfx file.

`keytool -v -list -storetype pkcs12 -keystore [name of your .pfx file]`

For example keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).  -->
