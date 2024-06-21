---
title: Expiração dos certificados de extensões Reader e seu impacto
description: Expiração dos certificados de extensões Reader e seu impacto
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---


# Expiração dos certificados de extensões Reader e seu impacto {#expiration-of-reader-extensions-certificates-and-its-impact}

Os clientes do Adobe Experience Manager Forms (AEM Forms) com licenças Adobe Managed Services ou Enterprise Base no local estão autorizados a usar o serviço Acrobat Reader DC Extensions. O serviço permite que uma organização compartilhe facilmente documentos PDF interativos, estendendo a funcionalidade do Acrobat Reader com direitos de uso adicionais. O serviço adiciona direitos de uso a um documento PDF e ativa recursos que não estão disponíveis quando um documento PDF é aberto usando o Adobe Acrobat Reader, como adicionar comentários a um documento, preencher formulários e salvar o documento. Usuários de terceiros não precisam de software ou plug-ins adicionais para trabalhar com documentos habilitados por direitos. Os documentos PDF que possuem direitos de uso adicionados são chamados de documentos habilitados para direitos. Um usuário que abre um documento PDF habilitado para direitos no Acrobat Reader pode executar as operações habilitadas para esse documento.

O Adobe usa uma infraestrutura de chave pública (PKI) para emitir certificados digitais para uso no licenciamento e na ativação de recursos. Adobe tem emitido certificados sob a autoridade de certificação **CA Raiz Adobe**, que deve expirar em 7 de janeiro de 2023. A expiração do certificado não afeta documentos PDF estendidos usando certificados de produção emitidos pelo **CA Raiz Adobe** certificados baseados (certificados antigos). Todos os documentos de PDF, Reader estendidos usando os certificados antigos antes de 7 de janeiro de 2023, incluindo os baixados pelos clientes, continuariam a funcionar com todos os direitos de uso aplicados a eles e não exigem atualizações.

Uma nova autoridade de certificação, **Adobe Root CA G2** e os certificados baseados na nova autoridade de certificação agora estão disponíveis. Até 7 de janeiro de 2023, comece a usar os novos certificados — aqueles com base em **Adobe Root CA G2** Reader — para estender os novos documentos PDF.  Você pode [obter novos certificados no site de licenciamento do Adobe](https://licensing.adobe.com/) ou Suporte para Adobe.

## Perguntas frequentes

**P. Qual é a diferença entre um certificado Adobe Root e um certificado de extensões do Acrobat Reader? O certificado Adobe Root depende de um certificado de extensões da Acrobat Reader? Ambos os certificados expiram em janeiro de 2023?**

A. A CA raiz do Adobe é a autoridade de certificação da qual um certificado de extensões do Acrobat Reader é emitido. Em 7 de janeiro de 2023, &quot;Adobe Root CA&quot; e todos os certificados emitidos a partir dele estão expirando.

**P. Houve uma comunicação anterior do Adobe sobre a expiração de certificados e o impacto no uso/abertura de documentos PDF. Essa comunicação deve ser ignorada?**

A. Com base na reavaliação da situação, todos os documentos de PDF estendidos usando certificados de produção emitidos da antiga &quot;Adobe Root CA&quot; antes de 7 de janeiro de 2023 continuam a funcionar sem nenhuma alteração após 7 de janeiro de 2023. Se você já atualizou seus documentos PDF, não há alteração na experiência.

**P. Com quem devo entrar em contato caso tenha dúvidas adicionais?**

A. Você pode entrar em contato com a [Suporte para Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=pt-BR#support) ou criar um tíquete de suporte.

**P. O que acontece se eu não atualizar meu certificado antes de 7 de janeiro de 2023?**

A. Todos os documentos de PDF estendidos usando certificados de produção emitidos da antiga &#39;Adobe Root CA&#39; antes de 7 de janeiro de 2023 continuam a funcionar sem qualquer alteração após 7 de janeiro de 2023. Os PDF estendidos com certificados de avaliação não funcionam após a data de expiração.

**P. A descrição dos novos certificados é diferente dos certificados antigos?**

A. A descrição dos novos certificados de extensões da Acrobat Reader menciona **G3-P24** como o nome do programa. Na descrição de certificados mais antigos (certificados baseados em &quot;Adobe Root CA&quot;), **P24** é mencionado como o nome do programa.

**P. Como obter os certificados mais recentes?**

A. Todos os clientes da Forms qualificados (com licença ativa) podem fazer download dos novos certificados (certificados baseados em &quot;Adobe Root CA G2&quot;) no [Site de licenciamento do Adobe](https://licensing.adobe.com/). Se não conseguir encontrar o certificado no site de licenciamento do Adobe, entre em contato com [Suporte para Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=en#support) ou criar um tíquete de suporte.

**P. Meus documentos de PDF estendidos usando certificados emitidos pela &quot;Autoridade de Certificação Raiz do Adobe&quot; (a antiga autoridade de certificação) continuam a funcionar após 7 de janeiro de 2023?**

R. Sim, todos os documentos de PDF estendidos usando certificados de produção emitidos pela &quot;Autoridade de Certificação Raiz do Adobe&quot; (a antiga autoridade de certificação) antes de 7 de janeiro de 2023 continuarão funcionando sem nenhuma alteração após 7 de janeiro de 2023. Os documentos PDF estendidos com certificados de avaliação deixam de funcionar após a data de expiração.

**P. Qual versão do Adobe Acrobat Reader é necessária para continuar usando documentos do PDF estendidos com certificados emitidos da &quot;Autoridade de Certificação Raiz do Adobe&quot; (a autoridade de certificação antiga)?**

R. O Adobe Acrobat Reader 2020 ou posterior é necessário para usar documentos PDF estendidos com &quot;Autoridade de certificação raiz Adobe&quot; (a autoridade de certificação antiga). É a versão compatível do Acrobat Reader no momento da publicação deste documento. Se você estiver usando um [versão não compatível do Adobe Acrobat](https://helpx.adobe.com/br/support/programs/eol-matrix.html), o Adobe recomenda que você [baixe e instale a versão mais recente do Adobe Acrobat Reader](https://get.adobe.com/reader/).

**P. Qual versão do Adobe Acrobat Reader é necessária para continuar usando documentos do PDF estendidos com certificados emitidos da &quot;Autoridade de Certificação Raiz Adobe 2&quot; (a nova autoridade de certificação)?**

R. O Adobe Acrobat Reader 2020 ou posterior é necessário para usar documentos PDF estendidos com &quot;Adobe Root CA 2&quot; (a nova autoridade de certificação). Se você estiver usando um [versão não compatível do Adobe Acrobat Reader](https://helpx.adobe.com/br/support/programs/eol-matrix.html), o Adobe recomenda que você [baixe e instale a versão mais recente do Adobe Acrobat Reader](https://get.adobe.com/reader/).

**P. É possível excluir um certificado antigo de extensões da Acrobat Reader e adicionar um novo em um Adobe Experience Manager Forms Server enquanto continuo a usar o alias existente?**

R. Sim, você pode excluir um certificado antigo de extensões da Acrobat Reader e adicionar um novo com o alias existente a um Adobe Experience Manager Forms Server.

**P. Posso manter certificados de extensões novas e antigas do Acrobat Reader em um servidor Adobe Experience Manager Forms?**

R. Sim, você pode manter ambos os certificados, mas com aliases diferentes em um Adobe Experience Manager Forms Server. Reader Após 7 de janeiro de 2023, você poderá usar somente o novo certificado para estender um documento PDF.

**P. Posso importar o mesmo certificado de extensões do Acrobat Reader para todos os ambientes do Adobe Experience Manager Forms?**

R. Sim, o mesmo certificado de Extensões da Acrobat Reader pode ser usado em vários ambientes.

**P. Como verificar os direitos de uso aplicados a um documento PDF?**

A. Você pode usar a variável [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=en#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) API para recuperar as informações sobre os direitos de uso aplicados a um documento PDF.

**P. Como alterar a senha de um arquivo de certificado de extensões da Acrobat Reader?**

A. No Microsoft Windows, para alterar a Senha do certificado, instale o certificado usando o Microsoft Management Console (MMC) e selecione **Marcar a chave como Exportável**. Depois de instalado, exporte o certificado com uma chave privada e use outra senha para o arquivo PFX.


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

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. Designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

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

For example, keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).  -->
