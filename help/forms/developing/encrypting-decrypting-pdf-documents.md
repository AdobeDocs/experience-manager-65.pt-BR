---
title: Criptografar e descriptografar documentos do PDF
seo-title: Encrypting and Decrypting PDF Documents
description: Use o Serviço de criptografia para criptografar e descriptografar documentos. As tarefas do serviço de criptografia incluem criptografar um documento PDF com senha, criptografar um documento PDF com um certificado, remover criptografia com base em senha de um documento PDF, remover criptografia com base em certificado de um documento PDF, desbloquear o documento PDF para que outras operações de serviço possam ser executadas e determinar o tipo de criptografia de um documento PDF seguro.
seo-description: Use the Encryption service to encrypt and decrypt documents. The Encryption service tasks include encrypting a PDF document with a password, encrypting a PDF document with a certificate, removing password-based encryption from a PDF document, removing certificate-based encryption from a PDF document, unlocking the PDF document so that other service operations can be performed, and determining the encryption type of a secured PDF document.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '8189'
ht-degree: 0%

---

# Criptografar e descriptografar documentos do PDF {#encrypting-and-decrypting-pdf-documents}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

**Sobre o serviço de criptografia**

O Serviço de criptografia permite criptografar e descriptografar documentos. Quando um documento é criptografado, seu conteúdo se torna ilegível. Um usuário autorizado pode descriptografar o documento para obter acesso ao conteúdo. Se um documento do PDF for criptografado com uma senha, o usuário deverá especificar a senha de abertura para que o documento possa ser visualizado no Adobe Reader ou Adobe Acrobat. Da mesma forma, se um documento PDF for criptografado com um certificado, o usuário deverá descriptografar o documento PDF com a chave pública que corresponde ao certificado (chave privada) que foi usado para criptografar o documento PDF.

Você pode realizar essas tarefas usando o Serviço de criptografia:

* Criptografe um documento PDF com uma senha. (Consulte [Criptografar documentos do PDF com uma senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Criptografe um documento PDF com um certificado. (Consulte [Criptografar documentos PDF com certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Remova a criptografia baseada em senha de um documento PDF. (Consulte [Remover criptografia de senha](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Remova a criptografia baseada em certificado de um documento PDF. (Consulte [Remover criptografia baseada em certificado](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Desbloqueie o documento PDF para que outras operações de serviço possam ser executadas. Por exemplo, depois que um documento PDF criptografado por senha é desbloqueado, você pode aplicar uma assinatura digital a ele. (Consulte [Desbloquear documentos PDF criptografados](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Determine o tipo de criptografia de um documento PDF seguro. (Consulte [Determinar o tipo de criptografia](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Criptografar documentos do PDF com uma senha {#encrypting-pdf-documents-with-a-password}

Ao criptografar um documento do PDF com uma senha, o usuário deve especificar a senha para abrir o documento do PDF no Adobe Reader ou Acrobat. Além disso, antes que outra operação do AEM Forms, como assinar digitalmente o documento PDF, possa ser executada no documento, um documento PDF criptografado por senha deve ser desbloqueado.

>[!NOTE]
>
>Se você carregar um documento PDF criptografado no repositório AEM Forms, ele não poderá descriptografar o documento PDF e extrair o conteúdo XDP. É recomendável não criptografar um documento antes de fazer upload para o repositório do AEM Forms. (Consulte [Escrever recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para criptografar um documento PDF com uma senha, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do cliente de criptografia.
1. Obtenha um documento PDF para criptografar.
1. Defina as opções de tempo de execução da criptografia.
1. Adicione a senha.
1. Salve o documento PDF criptografado como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

**Criar um objeto de API do cliente de criptografia**

Para executar programaticamente uma operação do serviço de criptografia, é necessário criar um cliente do serviço de criptografia.

**Obter um documento PDF para criptografar**

Você deve obter um documento PDF não criptografado para criptografar o documento com uma senha. Se você tentar proteger um documento PDF já criptografado, ocorrerá uma exceção.

**Definir opções de tempo de execução de criptografia**

Para criptografar um documento PDF com uma senha, especifique quatro valores, incluindo dois valores de senha. O primeiro valor de senha é usado para criptografar o documento PDF e deve ser especificado ao abrir o documento PDF. O segundo valor de senha, chamado de principal valor de senha, é usado para remover a criptografia do documento PDF. Os valores de senha fazem distinção entre maiúsculas e minúsculas e esses dois valores de senha não podem ser os mesmos valores.

Você deve especificar os recursos do documento PDF para criptografar. Você pode criptografar todo o documento do PDF, tudo exceto os metadados do documento ou apenas os anexos do documento. Se você criptografar apenas os anexos do documento, um usuário será solicitado a fornecer uma senha ao tentar acessar os anexos do arquivo.

Ao criptografar um documento PDF, você pode especificar permissões associadas ao documento protegido. Ao especificar permissões, você pode controlar as ações que um usuário que abre um documento PDF criptografado por senha pode executar. Por exemplo, para extrair dados de formulário com êxito, você deve definir as seguintes permissões:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>As permissões são especificadas como `PasswordEncryptionPermission` valores de enumeração.

**Adicionar a senha**

Depois de recuperar um documento PDF não seguro e definir valores de tempo de execução de criptografia, você pode adicionar uma senha ao documento PDF.

**Salve o documento PDF criptografado como um arquivo PDF**

Você pode salvar o documento PDF criptografado por senha como um arquivo PDF.

**Consulte também**

[Criptografar um documento do PDF usando a API do Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Criptografar um documento do PDF usando a API do serviço da Web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de criptografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Criptografar documentos PDF com certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Criptografar um documento do PDF usando a API do Java {#encrypt-a-pdf-document-using-the-java-api}

Criptografe um documento do PDF com uma senha usando a API de criptografia (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-encryption-client.jar, no caminho de classe do seu projeto Java.

1. Crie uma API do cliente de criptografia.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `EncryptionServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obtenha um documento PDF para criptografar.

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF para criptografar usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Defina as opções de tempo de execução da criptografia.

   * Crie um `PasswordEncryptionOptionSpec` chamando seu construtor.
   * Especifique os recursos do documento do PDF a serem criptografados chamando a variável `PasswordEncryptionOptionSpec` do objeto `setEncryptOption` e a transmissão de um `PasswordEncryptionOption` valor de enumeração que especifica os recursos do documento a serem criptografados. Por exemplo, para criptografar todo o documento PDF, incluindo seus metadados e seus anexos, especifique `PasswordEncryptionOption.ALL`.
   * Crie um `java.util.List` que armazena as permissões de criptografia usando o `ArrayList` construtor.
   * Especifique uma permissão chamando o `java.util.List` objeto &quot;s `add` e transmitindo um valor de enumeração que corresponda à permissão que você deseja definir. Por exemplo, para definir a permissão que permite ao usuário copiar dados localizados no documento PDF, especifique `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Repita essa etapa para cada permissão a ser definida).
   * Especifique a opção de compatibilidade do Acrobat chamando o `PasswordEncryptionOptionSpec` do objeto `setCompatability` e transmitindo um valor de enumeração que especifica o nível de compatibilidade do Acrobat. Por exemplo, você pode especificar `PasswordEncryptionCompatability.ACRO_7`.
   * Especifique o valor da senha que permite que um usuário abra o documento PDF criptografado chamando a função `PasswordEncryptionOptionSpec` do objeto `setDocumentOpenPassword` e transmitindo um valor de string que represente a senha aberta.
   * Especifique o valor da senha principal que permite que um usuário remova a criptografia do documento PDF, chamando o `PasswordEncryptionOptionSpec` do objeto `setPermissionPassword` e transmitindo um valor de string que represente a senha principal.

1. Adicione a senha.

   Criptografe o documento do PDF chamando o `EncryptionServiceClient` do objeto `encryptPDFUsingPassword` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que contém o documento PDF para criptografar com a senha.
   * O `PasswordEncryptionOptionSpec` objeto que contém opções de tempo de execução de criptografia.

   O `encryptPDFUsingPassword` método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF criptografado por senha.

1. Salve o documento PDF criptografado como um arquivo PDF.

   * Crie um `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` ao arquivo. Certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `encryptPDFUsingPassword` método .

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): Criptografar um documento do PDF usando a API do Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criptografar um documento do PDF usando a API do serviço da Web {#encrypting-a-pdf-document-using-the-web-service-api}

Criptografe um documento do PDF com uma senha usando a API de criptografia (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto da API do cliente de criptografia.

   * Crie um `EncryptionServiceClient` usando seu construtor padrão.
   * Crie um `EncryptionServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `EncryptionServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha um documento PDF para criptografar.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF criptografado com uma senha.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento do PDF a ser criptografado e o modo no qual abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` atribuindo o conteúdo da matriz de bytes ao `BLOB` do objeto `MTOM` membro de dados.

1. Defina as opções de tempo de execução da criptografia.

   * Crie um `PasswordEncryptionOptionSpec` usando seu construtor.
   * Especifique os recursos do documento do PDF a serem criptografados atribuindo um `PasswordEncryptionOption` valor de enumeração para a `PasswordEncryptionOptionSpec` do objeto `encryptOption` membro de dados. Para criptografar toda a PDF, incluindo seus metadados e seus anexos, atribua `PasswordEncryptionOption.ALL` para esse membro de dados.
   * Especifique a opção de compatibilidade do Acrobat atribuindo um `PasswordEncryptionCompatability` valor de enumeração para a `PasswordEncryptionOptionSpec` do objeto `compatability` membro de dados. Por exemplo, atribuir `PasswordEncryptionCompatability.ACRO_7` para esse membro de dados.
   * Especifique o valor da senha que permite que um usuário abra o documento PDF criptografado atribuindo um valor de string que representa a senha aberta à `PasswordEncryptionOptionSpec` do objeto `documentOpenPassword` membro de dados.
   * Especifique o valor da senha que permite que um usuário remova a criptografia do documento PDF atribuindo um valor de string que representa a senha principal para o `PasswordEncryptionOptionSpec` do objeto `permissionPassword` membro de dados.

1. Adicione a senha.

   Criptografe o documento do PDF chamando o `EncryptionServiceClient` do objeto `encryptPDFUsingPassword` e transmitindo os seguintes valores:

   * O `BLOB` objeto que contém o documento PDF para criptografar com a senha.
   * O `PasswordEncryptionOptionSpec` objeto que contém opções de tempo de execução de criptografia.

   O `encryptPDFUsingPassword` método retorna um `BLOB` objeto que contém um documento PDF criptografado por senha.

1. Salve o documento PDF criptografado como um arquivo PDF.

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento de PDF seguro.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `encryptPDFUsingPassword` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Criptografar documentos PDF com certificados {#encrypting-pdf-documents-with-certificates}

A criptografia baseada em certificado permite criptografar um documento para recipients específicos por meio da tecnologia de chave pública. Vários destinatários podem receber permissões diferentes para o documento. Muitos aspectos da criptografia são viabilizados pela tecnologia de chave pública. Um algoritmo é usado para gerar dois números grandes, conhecidos como *teclas*, que têm as seguintes propriedades:

* Uma chave é usada para criptografar um conjunto de dados. Posteriormente, somente a outra chave poderá ser usada para descriptografar os dados.
* É impossível distinguir uma chave da outra.

Uma das chaves atua como chave privada do usuário. É importante que somente o usuário tenha acesso a essa chave. A outra chave é a chave pública do usuário, que pode ser compartilhada com outras pessoas.

Um certificado de chave pública contém a chave pública de um usuário e as informações de identificação. O formato X.509 é usado para armazenar certificados. Normalmente, os certificados são emitidos e assinados digitalmente por uma autoridade de certificação (CA), que é uma entidade reconhecida que fornece uma medida de confiança na validade do certificado. Os certificados têm uma data de expiração, depois da qual não são mais válidos. Além disso, as listas de revogação de certificados (CRLs) fornecem informações sobre certificados que foram revogados antes da data de expiração. As LCR são publicadas periodicamente pelas autoridades de certificação. O status de revogação de um certificado também pode ser recuperado por meio do protocolo OCSP (Online Certificate Status Protocol) pela rede.

>[!NOTE]
>
>Se você carregar um documento PDF criptografado no repositório AEM Forms, ele não poderá descriptografar o documento PDF e extrair o conteúdo XDP. É recomendável não criptografar um documento antes de fazer upload para o repositório do AEM Forms. (Consulte [Escrever recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Antes de criptografar um documento do PDF com um certificado, é necessário adicionar o certificado à AEM Forms. Um certificado é adicionado usando o console de administração ou de forma programática usando a API do Gerenciador de Confiança. (Consulte [Importando credenciais usando a API do Gerenciador de Confiança](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para criptografar um documento PDF com um certificado, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do cliente de criptografia.
1. Obtenha um documento PDF para criptografar.
1. Faça referência ao certificado.
1. Defina as opções de tempo de execução da criptografia.
1. Crie um documento PDF criptografado por certificado.
1. Salve o documento PDF criptografado como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

**Criar um objeto de API do cliente de criptografia**

Para executar programaticamente uma operação do serviço de criptografia, é necessário criar um cliente do serviço de criptografia. Se estiver usando a API do Serviço de criptografia Java, crie um `EncrytionServiceClient` objeto. Se estiver usando a API do serviço de criptografia da Web, crie um `EncryptionServiceService` objeto.

**Obter um documento PDF para criptografar**

Você deve obter um documento PDF não criptografado para criptografar. Se você tentar proteger um documento PDF já criptografado, uma exceção será lançada.

**Fazer referência ao certificado**

Para criptografar um documento PDF com um certificado, consulte um certificado usado para criptografar um documento PDF. O certificado é um arquivo .cer, um arquivo .crt ou um arquivo .pem. Um arquivo PKCS#12 é usado para armazenar chaves privadas com certificados correspondentes.

Ao criptografar um documento PDF com um certificado, especifique as permissões associadas ao documento protegido. Ao especificar permissões, você pode controlar as ações que um usuário que abre um documento PDF criptografado por certificado pode executar.

**Definir opções de tempo de execução de criptografia**

Especifique os recursos do documento PDF para criptografar. Você pode criptografar todo o documento do PDF, tudo exceto os metadados do documento ou apenas os anexos do documento.

**Criar um documento PDF criptografado por certificado**

Depois de recuperar um documento PDF não seguro, fazer referência ao certificado e definir opções de tempo de execução, você pode criar um documento PDF criptografado por certificado. Depois que o documento PDF for criptografado, será necessário ter a chave pública correspondente para descriptografá-lo.

**Salve o documento PDF criptografado como um arquivo PDF**

Você pode salvar o documento PDF criptografado como um arquivo PDF.

**Consulte também**

[Criptografar um documento do PDF com um certificado usando a API do Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Criptografar um documento do PDF com um certificado usando a API do serviço da Web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de criptografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Criptografar documentos do PDF com uma senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Criptografar um documento do PDF com um certificado usando a API do Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Criptografe um documento do PDF com um certificado usando a API de criptografia (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-encryption-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto da API do cliente de criptografia.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `EncryptionServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obtenha um documento PDF para criptografar.

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF para criptografar usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Faça referência ao certificado.

   * Crie um `java.util.List` objeto que armazena informações de permissão usando seu construtor.
   * Especifique a permissão associada ao documento criptografado chamando a função `java.util.List` do objeto `add` e a transmissão de um `CertificateEncryptionPermissions` valor de enumeração que representa as permissões concedidas ao usuário que abre o documento de PDF seguro. Por exemplo, para especificar todas as permissões, passe `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Crie um `Recipient` usando seu construtor.
   * Crie um `java.io.FileInputStream` objeto que representa o certificado usado para criptografar o documento PDF usando seu construtor e transmitindo um valor de string que especifica o local do certificado.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` que representa o certificado.
   * Chame o `Recipient` do objeto `setX509Cert` e passe o `com.adobe.idp.Document` objeto que contém o certificado. (Além disso, a variável `Recipient`pode ter um alias de certificado Truststore ou URL LDAP como uma fonte de certificado.)
   * Crie um `CertificateEncryptionIdentity` objeto que armazena informações de permissão e certificado usando seu construtor.
   * Chame o `CertificateEncryptionIdentity` do objeto `setPerms` e passe o `java.util.List` objeto que armazena informações de permissão.
   * Chame o `CertificateEncryptionIdentity` do objeto `setRecipient` e passe o `Recipient` objeto que armazena informações de certificado.
   * Crie um `java.util.List` objeto que armazena informações de certificado usando seu construtor.
   * Chame o `java.util.List` adicione o método do objeto e passe o `CertificateEncryptionIdentity` objeto. (Este `java.util.List` é passado como parâmetro para a variável `encryptPDFUsingCertificates` método .)

1. Defina as opções de tempo de execução da criptografia.

   * Crie um `CertificateEncryptionOptionSpec` chamando seu construtor.
   * Especifique os recursos do documento do PDF a serem criptografados chamando a variável `CertificateEncryptionOptionSpec` do objeto `setOption` e a transmissão de um `CertificateEncryptionOption` valor de enumeração que especifica os recursos do documento a serem criptografados. Por exemplo, para criptografar todo o documento PDF, incluindo seus metadados e seus anexos, especifique `CertificateEncryptionOption.ALL`.
   * Especifique a opção de compatibilidade do Acrobat chamando o `CertificateEncryptionOptionSpec` do objeto `setCompat` e a transmissão de um `CertificateEncryptionCompatibility` valor de enumeração que especifica o nível de compatibilidade do Acrobat. Por exemplo, você pode especificar `CertificateEncryptionCompatibility.ACRO_7`.

1. Crie um documento PDF criptografado por certificado.

   Criptografe o documento do PDF com um certificado chamando o `EncryptionServiceClient` do objeto `encryptPDFUsingCertificates` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que contém o documento PDF para criptografar.
   * O `java.util.List` objeto que armazena informações de certificado.
   * O `CertificateEncryptionOptionSpec` objeto que contém opções de tempo de execução de criptografia.

   O `encryptPDFUsingCertificates` método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF criptografado por certificado.

1. Salve o documento PDF criptografado como um arquivo PDF.

   * Crie um `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` ao arquivo. Certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `encryptPDFUsingCertificates` método .

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): Criptografar um documento do PDF com um certificado usando a API do Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criptografar um documento do PDF com um certificado usando a API do serviço da Web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Criptografe um documento do PDF com um certificado usando a API de criptografia (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto da API do cliente de criptografia.

   * Crie um `EncryptionServiceClient` usando seu construtor padrão.
   * Crie um `EncryptionServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `EncryptionServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha um documento PDF para criptografar.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF criptografado com um certificado.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento do PDF a ser criptografado e o modo no qual abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Faça referência ao certificado.

   * Crie um `Recipient` usando seu construtor. Esse objeto armazenará informações de certificado.
   * Crie um `BLOB` usando seu construtor. Essa `BLOB` armazenará o certificado que criptografa o documento PDF.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do certificado e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` atribuindo o conteúdo da matriz de bytes ao `BLOB` do objeto `MTOM` membro de dados.
   * Atribua o `BLOB` objeto que armazena o certificado para a variável `Recipient` do objeto `x509Cert` membro de dados.
   * Crie um `CertificateEncryptionIdentity` objeto que armazena informações de certificado usando seu construtor.
   * Atribua o `Recipient` objeto que armazena o certificado para a variável `CertificateEncryptionIdentity`membro de dados do destinatário do objeto.
   * Crie um `Object` e atribua o `CertificateEncryptionIdentity` ao primeiro elemento da variável `Object` matriz. Essa `Object` A matriz é passada como parâmetro para a variável `encryptPDFUsingCertificates` método .

1. Defina as opções de tempo de execução da criptografia.

   * Crie um `CertificateEncryptionOptionSpec` usando seu construtor.
   * Especifique os recursos do documento do PDF a serem criptografados atribuindo um `CertificateEncryptionOption` valor de enumeração para a `CertificateEncryptionOptionSpec` do objeto `option` membro de dados. Para criptografar todo o documento do PDF, incluindo seus metadados e seus anexos, atribua `CertificateEncryptionOption.ALL` para esse membro de dados.
   * Especifique a opção de compatibilidade do Acrobat atribuindo um `CertificateEncryptionCompatibility` valor de enumeração para a `CertificateEncryptionOptionSpec` do objeto `compat` membro de dados. Por exemplo, atribuir `CertificateEncryptionCompatibility.ACRO_7` para esse membro de dados.

1. Crie um documento PDF criptografado por certificado.

   Criptografe o documento do PDF com um certificado chamando o `EncryptionServiceService` do objeto `encryptPDFUsingCertificates` e transmitindo os seguintes valores:

   * O `BLOB` objeto que contém o documento PDF para criptografar.
   * O `Object` matriz que armazena informações de certificado.
   * O `CertificateEncryptionOptionSpec` objeto que contém opções de tempo de execução de criptografia.

   O `encryptPDFUsingCertificates` método retorna um `BLOB` objeto que contém um documento PDF criptografado por certificado.

1. Salve o documento PDF criptografado como um arquivo PDF.

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento de PDF seguro.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `encryptPDFUsingCertificates` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `binaryData` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Remover criptografia baseada em certificado {#removing-certificate-based-encryption}

A criptografia baseada em certificado pode ser removida de um documento PDF para que os usuários possam abrir o documento PDF no Adobe Reader ou Acrobat. Para remover a criptografia de um documento PDF criptografado com um certificado, uma chave pública deve ser referenciada. Depois que a criptografia é removida de um documento PDF, ela não é mais segura.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para remover a criptografia baseada em certificado de um documento PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente de serviço de criptografia.
1. Obtenha o documento PDF criptografado.
1. Remova a criptografia.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

**Criar um cliente de serviço de criptografia**

Para executar programaticamente uma operação do serviço de criptografia, é necessário criar um cliente do serviço de criptografia. Se estiver usando a API do Serviço de criptografia Java, crie um `EncrytionServiceClient` objeto. Se estiver usando a API do serviço de criptografia da Web, crie um `EncryptionServiceService` objeto.

**Obter o documento PDF criptografado**

Você deve obter um documento PDF criptografado para remover a criptografia baseada em certificado. Se você tentar remover a criptografia de um documento PDF que não está criptografado, uma exceção será lançada. Da mesma forma, se você tentar remover a criptografia baseada em certificado de um documento criptografado por senha, uma exceção será lançada.

**Remover criptografia**

Para remover a criptografia baseada em certificado de um documento PDF criptografado, você precisa de um documento PDF criptografado e da chave privada que corresponda à chave usada para criptografar o documento PDF. O valor alias da chave privada é especificado ao remover a criptografia baseada em certificado de um documento PDF criptografado. Para obter informações sobre a chave pública, consulte [Criptografar documentos PDF com certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Uma chave privada é armazenada na AEM Forms Trust Store. Quando um certificado é colocado lá, um valor de alias é especificado.

**Salve o documento do PDF**

Depois que a criptografia baseada em certificado é removida de um documento PDF criptografado, é possível salvar o documento PDF como um arquivo PDF. Os usuários podem abrir o documento do PDF no Adobe Reader ou Acrobat.

**Consulte também**

[Remova a criptografia baseada em certificado usando a API Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Remover criptografia baseada em certificado usando a API de serviço da Web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de criptografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Remova a criptografia baseada em certificado usando a API Java {#remove-certificate-based-encryption-using-the-java-api}

Remova a criptografia baseada em certificado de um documento do PDF usando a API de criptografia (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-encryption-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente de serviço de criptografia.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `EncryptionServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obtenha o documento PDF criptografado.

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF criptografado usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF criptografado.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Remova a criptografia.

   Remova a criptografia baseada em certificado do documento PDF chamando o `EncryptionServiceClient` do objeto `removePDFCertificateSecurity` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que contém o documento PDF criptografado.
   * Um valor de string que especifica o nome do alias da chave privada que corresponde à chave usada para criptografar o documento PDf.

   O `removePDFCertificateSecurity` método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF não seguro.

1. Salve o documento PDF.

   * Crie um `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `Document` ao arquivo. Certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `removePDFCredentialSecurity` método .

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): Remoção da criptografia baseada em certificado usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Remover criptografia baseada em certificado usando a API de serviço da Web {#remove-certificate-based-encryption-using-the-web-service-api}

Remova a criptografia baseada em certificado usando a API de criptografia (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente de serviço de criptografia.

   * Crie um `EncryptionServiceClient` usando seu construtor padrão.
   * Crie um `EncryptionServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `EncryptionServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF criptografado.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento PDF criptografado.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF criptografado e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` atribuindo o conteúdo da matriz de bytes ao `BLOB` do objeto `MTOM` membro de dados.

1. Remova a criptografia.

   Chame o `EncryptionServiceClient` do objeto `removePDFCertificateSecurity` e transmita os seguintes valores:

   * O `BLOB` objeto que contém dados de fluxo de arquivo que representam um documento PDF criptografado.
   * Um valor de string que especifica o nome do alias da chave pública que corresponde à chave privada usada para criptografar o documento PDf.

   O `removePDFCredentialSecurity` método retorna um `BLOB` objeto que contém um documento PDF não seguro.

1. Salve o documento PDF.

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF não seguro.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto retornado pelo `removePDFPasswordSecurity` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Remover criptografia de senha {#removing-password-encryption}

A criptografia com base em senha pode ser removida de um documento PDF para que os usuários possam abrir o documento do PDF no Adobe Reader ou no Acrobat sem precisar especificar uma senha. Depois que a criptografia com base em senha é removida de um documento PDF, o documento não é mais seguro.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-3}

Para remover a criptografia baseada em senha de um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Crie um cliente de serviço de criptografia.
1. Obtenha o documento PDF criptografado.
1. Remova a senha.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

**Criar um cliente de serviço de criptografia**

Para executar programaticamente uma operação do serviço de criptografia, é necessário criar um cliente do serviço de criptografia. Se estiver usando a API do Serviço de criptografia Java, crie um `EncrytionServiceClient` objeto. Se estiver usando a API do serviço de criptografia da Web, crie um `EncryptionServiceService` objeto.

**Obter o documento PDF criptografado**

Você deve obter um documento PDF criptografado para remover a criptografia baseada em senha. Se você tentar remover a criptografia de um documento PDF que não está criptografado, uma exceção será lançada.

**Remover a senha**

Para remover a criptografia baseada em senha de um documento PDF criptografado, você precisa de um documento PDF criptografado e de um valor de senha principal usado para remover a criptografia do documento PDF. A senha usada para abrir um documento PDF criptografado por senha não pode ser usada para remover a criptografia. Uma senha principal é especificada quando o documento PDF é criptografado com uma senha. (Consulte [Criptografar documentos do PDF com uma senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**Salve o documento do PDF**

Depois que o serviço de criptografia remover a criptografia baseada em senha de um documento PDF, você poderá salvar o documento PDF como um arquivo PDF. Os usuários podem abrir o documento do PDF no Adobe Reader ou Acrobat sem especificar uma senha.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de criptografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Criptografar documentos do PDF com uma senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Remova a criptografia baseada em senha usando a API Java {#remove-password-based-encryption-using-the-java-api}

Remova a criptografia baseada em senha de um documento do PDF usando a API de criptografia (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-encryption-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente de serviço de criptografia.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `EncryptionServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obtenha o documento PDF criptografado.

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF criptografado usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Remova a senha.

   Remova a criptografia baseada em senha do documento PDF chamando o `EncryptionServiceClient` do objeto `removePDFPasswordSecurity` e transmitindo os seguintes valores:

   * A `com.adobe.idp.Document` objeto que contém o documento PDF criptografado.
   * Um valor de string que especifica o valor de senha principal usado para remover a criptografia do documento PDF.

   O `removePDFPasswordSecurity` método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF não seguro.

1. Salve o documento PDF.

   * Crie um `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `Document` ao arquivo. Certifique-se de usar a variável `Document` objeto retornado pelo `removePDFPasswordSecurity` método .

**Consulte também**

[Início rápido (modo SOAP): Remoção da criptografia baseada em senha usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Remover criptografia baseada em senha usando a API de serviço da Web {#remove-password-based-encryption-using-the-web-service-api}

Remova a criptografia baseada em senha usando a API de criptografia (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente de serviço de criptografia.

   * Crie um `EncryptionServiceClient` usando seu construtor padrão.
   * Crie um `EncryptionServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `EncryptionServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF criptografado.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF criptografado por senha.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF criptografado e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` atribuindo o conteúdo da matriz de bytes ao `BLOB` do objeto `MTOM` membro de dados.

1. Remova a senha.

   Chame o `EncryptionServiceService` do objeto `removePDFPasswordSecurity` e transmita os seguintes valores:

   * O `BLOB` objeto que contém dados de fluxo de arquivo que representam um documento PDF criptografado.
   * Um valor da string que especifica o valor da senha usado para remover a criptografia do documento PDF. Esse valor é especificado ao criptografar o documento PDF com uma senha.

   O `removePDFPasswordSecurity` método retorna um `BLOB` objeto que contém um documento PDF não seguro.

1. Salve o documento PDF.

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF não seguro.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto retornado pelo `removePDFPasswordSecurity` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Desbloquear documentos PDF criptografados {#unlocking-encrypted-pdf-documents}

Um documento PDF criptografado por senha ou por certificado deve ser desbloqueado antes que outra operação do AEM Forms possa ser executada. Se você tentar executar uma operação em um documento PDF criptografado, gerará uma exceção. Após desbloquear um documento PDF criptografado, é possível executar uma ou mais operações nele. Essas operações podem pertencer a outros serviços, como o Serviço de extensões da Acrobat Reader DC.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-4}

Para desbloquear um documento PDF criptografado, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente de serviço de criptografia.
1. Obtenha o documento PDF criptografado.
1. Desbloqueie o documento.
1. Execute uma operação AEM Forms.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

**Criar um cliente de serviço de criptografia**

Para executar programaticamente uma operação do serviço de criptografia, é necessário criar um cliente do serviço de criptografia. Se estiver usando a API do Serviço de criptografia Java, crie um `EncrytionServiceClient` objeto. Se estiver usando a API do serviço de criptografia da Web, crie um `EncryptionServiceService` objeto.

**Obter o documento PDF criptografado**

Você deve obter um documento PDF criptografado para desbloqueá-lo. Se você tentar desbloquear um documento PDF que não está criptografado, uma exceção será lançada.

**Desbloquear o documento**

Para desbloquear um documento PDF criptografado por senha, você precisa de um documento PDF criptografado e um valor de senha usado para abrir um documento PDF criptografado por senha. Esse valor é especificado ao criptografar o documento PDF com uma senha. (Consulte [Criptografar documentos do PDF com uma senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

Para desbloquear um documento PDF criptografado por certificado, você precisa de um documento PDF criptografado e do valor alias da chave pública que corresponde à chave privada usada para criptografar o documento PDF.

**Executar uma operação do AEM Forms**

Depois que um documento PDF criptografado é desbloqueado, você pode executar outra operação de serviço nele, como aplicar direitos de uso a ele. Essa operação pertence ao serviço de extensões do Acrobat Reader DC.

**Consulte também**

[Desbloquear um documento PDF criptografado usando a API Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Desbloquear um documento PDF criptografado usando a API do serviço da Web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de criptografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Desbloquear um documento PDF criptografado usando a API Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Desbloqueie um documento PDF criptografado usando a API de criptografia (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-encryption-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente de serviço de criptografia.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `EncryptionServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obtenha o documento PDF criptografado.

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF criptografado usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF criptografado.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Desbloqueie o documento.

   Desbloqueie um documento PDF criptografado chamando o `EncryptionServiceClient` do objeto `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` método .

   Para desbloquear um documento PDF criptografado com uma senha, chame a função `unlockPDFUsingPassword` e transmita os seguintes valores:

   * A `com.adobe.idp.Document` objeto que contém o documento PDF criptografado por senha.
   * Um valor de string que especifica o valor de senha usado para abrir um documento PDF criptografado por senha. Esse valor é especificado ao criptografar o documento PDF com uma senha.

   Para desbloquear um documento PDF criptografado com um certificado, chame o `unlockPDFUsingCredential` e transmita os seguintes valores:

   * A `com.adobe.idp.Document` objeto que contém o documento PDF criptografado por certificado.
   * Um valor de string que especifica o nome do alias da chave pública que corresponde à chave privada usada para criptografar o documento PDF.

   O `unlockPDFUsingPassword` e `unlockPDFUsingCredential` ambos os métodos retornam um `com.adobe.idp.Document` objeto que é passado para outro método AEM Forms Java para executar uma operação.

1. Execute uma operação AEM Forms.

   Execute uma operação AEM Forms no documento PDF desbloqueado para atender aos requisitos de sua empresa. Por exemplo, supondo que você deseja aplicar direitos de uso a um documento PDF desbloqueado, passe a variável `com.adobe.idp.Document` objeto retornado pelo `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` métodos para `ReaderExtensionsServiceClient` do objeto `applyUsageRights` método .

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): Desbloquear um documento PDF criptografado usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) (Modo SOAP)

[Aplicação de direitos de uso a documentos do PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Desbloquear um documento PDF criptografado usando a API do serviço da Web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Desbloqueie um documento de PDF criptografado usando a API de criptografia (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente de serviço de criptografia.

   * Crie um `EncryptionServiceClient` usando seu construtor padrão.
   * Crie um `EncryptionServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `EncryptionServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha um documento PDF criptografado.

   * Crie um `BLOB` usando seu construtor.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF criptografado e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` atribuindo o conteúdo da matriz de bytes ao `BLOB` do objeto `MTOM` membro de dados.

1. Desbloqueie o documento.

   Desbloqueie um documento PDF criptografado chamando o `EncryptionServiceClient` do objeto `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` método .

   Para desbloquear um documento PDF criptografado com uma senha, chame a função `unlockPDFUsingPassword` e transmita os seguintes valores:

   * A `BLOB` objeto que contém o documento PDF criptografado por senha.
   * Um valor de string que especifica o valor de senha usado para abrir um documento PDF criptografado por senha. Esse valor é especificado ao criptografar o documento PDF com uma senha.

   Para desbloquear um documento PDF criptografado com um certificado, chame o `unlockPDFUsingCredential` e transmita os seguintes valores:

   * A `BLOB` objeto que contém o documento PDF criptografado por certificado.
   * Um valor de string que especifica o nome do alias da chave pública que corresponde à chave privada usada para criptografar o documento PDf.

   O `unlockPDFUsingPassword` e `unlockPDFUsingCredential` ambos os métodos retornam um `com.adobe.idp.Document` objeto que é passado para outro método AEM Forms para executar uma operação.

1. Execute uma operação AEM Forms.

   Execute uma operação AEM Forms no documento PDF desbloqueado para atender aos requisitos de sua empresa. Por exemplo, supondo que você deseja aplicar direitos de uso ao documento de PDF desbloqueado, passe o `BLOB` objeto retornado pelo `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` métodos para `ReaderExtensionsServiceClient` do objeto `applyUsageRights` método .

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinar o tipo de criptografia {#determining-encryption-type}

Você pode determinar programaticamente o tipo de criptografia que está protegendo um documento do PDF usando a API do serviço de criptografia Java ou a API do serviço de criptografia da Web. Às vezes, é necessário determinar dinamicamente se um documento PDF está criptografado e, em caso positivo, o tipo de criptografia. Por exemplo, você pode determinar se um documento do PDF está protegido com criptografia baseada em senha ou com uma política de Rights Management.

Um documento PDF pode ser protegido pelos seguintes tipos de criptografia:

* Criptografia baseada em senha
* Criptografia baseada em certificado
* Uma política criada pelo serviço Rights Management
* Outro tipo de criptografia

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-5}

Para determinar o tipo de criptografia que está protegendo um documento PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente de serviço de criptografia.
1. Obtenha o documento PDF criptografado.
1. Determine o tipo de criptografia.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

**Criar um cliente de serviço**

Para executar programaticamente uma operação do serviço de criptografia, é necessário criar um cliente do serviço de criptografia. Se estiver usando a API do Serviço de criptografia Java, crie um `EncrytionServiceClient` objeto. Se estiver usando a API do serviço de criptografia da Web, crie um `EncryptionServiceService` objeto.

**Obter o documento PDF criptografado**

Você deve obter um documento do PDF para determinar o tipo de criptografia que o está protegendo.

**Determine o tipo de criptografia**

Você pode determinar o tipo de criptografia que está protegendo um documento PDF. Se o documento PDF não estiver protegido, o serviço de Criptografia informará que o documento PDF não está protegido.

**Consulte também**

[Determine o tipo de criptografia usando a API Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determine o tipo de criptografia usando a API do serviço da Web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de criptografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protegendo documentos com políticas](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determine o tipo de criptografia usando a API Java {#determine-the-encryption-type-using-the-java-api}

Determine o tipo de criptografia que está protegendo um documento do PDF usando a API de criptografia (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-encryption-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente de serviço.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `EncryptionServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obtenha o documento PDF criptografado.

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Determine o tipo de criptografia.

   * Determine o tipo de criptografia chamando a função `EncryptionServiceClient` do objeto `getPDFEncryption` e a aprovação do `com.adobe.idp.Document` objeto que contém o documento PDF. Esse método retorna um `EncryptionTypeResult` objeto.
   * Chame o `EncryptionTypeResult` do objeto `getEncryptionType` método . Esse método retorna um `EncryptionType` valor enum que especifica o tipo de criptografia. Por exemplo, se o documento PDF estiver protegido com criptografia baseada em senha, esse método retornará `EncryptionType.PASSWORD`.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): Determinar o tipo de criptografia usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determine o tipo de criptografia usando a API do serviço da Web {#determine-the-encryption-type-using-the-web-service-api}

Determine o tipo de criptografia que está protegendo um documento do PDF usando a API de criptografia (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente de serviço.

   * Crie um `EncryptionServiceClient` usando seu construtor padrão.
   * Crie um `EncryptionServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `EncryptionServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF criptografado.

   * Crie um `BLOB` usando seu construtor.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF criptografado e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` atribuindo o conteúdo da matriz de bytes ao `BLOB` do objeto `MTOM` membro de dados.

1. Determine o tipo de criptografia.

   * Chame o `EncryptionServiceClient` do objeto `getPDFEncryption` e passe o `BLOB` objeto que contém o documento PDF. Esse método retorna um `EncryptionTypeResult` objeto.
   * Obtenha o valor da variável `EncryptionTypeResult` do objeto `encryptionType` método de dados. Por exemplo, se o documento PDF estiver protegido com criptografia baseada em senha, o valor desse membro de dados será `EncryptionType.PASSWORD`.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
