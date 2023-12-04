---
title: Criptografar e descriptografar documentos do PDF
seo-title: Encrypting and Decrypting PDF Documents
description: Use o serviço de criptografia para criptografar e descriptografar documentos. As tarefas do serviço de criptografia incluem criptografar um documento PDF com uma senha, criptografar um documento PDF com um certificado, remover a criptografia baseada em senha de um documento PDF, remover a criptografia baseada em certificado de um documento PDF, desbloquear o documento PDF para que outras operações de serviço possam ser executadas e determinar o tipo de criptografia de um documento PDF protegido.
seo-description: Use the Encryption service to encrypt and decrypt documents. The Encryption service tasks include encrypting a PDF document with a password, encrypting a PDF document with a certificate, removing password-based encryption from a PDF document, removing certificate-based encryption from a PDF document, unlocking the PDF document so that other service operations can be performed, and determining the encryption type of a secured PDF document.
uuid: 4e4e2716-c21f-4bfe-ae7a-7e91442414ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 5e4bda3a-5648-4c0f-b2f8-bdbebb88f537
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '8133'
ht-degree: 0%

---

# Criptografar e descriptografar documentos do PDF {#encrypting-and-decrypting-pdf-documents}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o Serviço de Criptografia**

O serviço de criptografia permite criptografar e descriptografar documentos. Quando um documento é criptografado, seu conteúdo fica ilegível. Um usuário autorizado pode descriptografar o documento para obter acesso ao conteúdo. Se um documento PDF for criptografado com uma senha, o usuário deverá especificar a senha aberta para que o documento possa ser visualizado no Adobe Reader ou no Adobe Acrobat. Da mesma forma, se um documento PDF for criptografado com um certificado, o usuário deverá descriptografar o documento PDF com a chave pública que corresponde ao certificado (chave privada) usado para criptografar o documento PDF.

Você pode realizar essas tarefas usando o Serviço de criptografia:

* Criptografar um documento PDF com uma senha. (Consulte [Criptografar documentos PDF com senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Criptografe um documento PDF com um certificado. (Consulte [Criptografar documentos PDF com certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Remova a criptografia baseada em senha de um documento PDF. (Consulte [Remoção da criptografia de senha](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Remova a criptografia baseada em certificado de um documento PDF. (Consulte [Removendo a Criptografia Baseada em Certificado](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Desbloqueie o documento PDF para que outras operações de serviço possam ser executadas. Por exemplo, depois que um documento PDF criptografado por senha é desbloqueado, você pode aplicar uma assinatura digital a ele. (Consulte [Desbloquear documentos PDF criptografados](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Determine o tipo de criptografia de um documento de PDF protegido. (Consulte [Determinação do tipo de criptografia](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Criptografar documentos PDF com senha {#encrypting-pdf-documents-with-a-password}

Quando você criptografa um documento PDF com uma senha, um usuário deve especificar a senha para abrir o documento PDF no Adobe Reader ou Acrobat. Além disso, antes que outra operação do AEM Forms, como a assinatura digital do documento PDF, possa ser executada no documento, um documento PDF criptografado por senha deve ser desbloqueado.

>[!NOTE]
>
>Se você fizer upload de um documento PDF criptografado para o repositório do AEM Forms, ele não poderá descriptografar o documento PDF e extrair o conteúdo XDP. É recomendável não criptografar um documento antes de carregá-lo no repositório do AEM Forms. (Consulte [Recursos de gravação](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para criptografar um documento PDF com uma senha, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um objeto de API do cliente de criptografia.
1. Obtenha um documento PDF para criptografar.
1. Definir opções de tempo de execução de criptografia.
1. Adicione a senha.
1. Salve o documento PDF criptografado como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

**Criar um objeto de API do cliente de criptografia**

Para executar programaticamente uma operação de Serviço de criptografia, você deve criar um cliente de Serviço de criptografia.

**Obter um documento PDF para criptografar**

Obtenha um documento PDF não criptografado para criptografar o documento com uma senha. Se você tentar proteger um documento PDF que já está criptografado, causará uma exceção.

**Definir opções de tempo de execução de criptografia**

Para criptografar um documento PDF com uma senha, você especifica quatro valores, incluindo dois valores de senha. O primeiro valor de senha é usado para criptografar o documento PDF e deve ser especificado ao abrir o documento PDF. O segundo valor de senha, chamado de valor de senha mestre, é usado para remover a criptografia do documento PDF. Os valores de senha fazem distinção entre maiúsculas e minúsculas, e esses dois valores não podem ser os mesmos.

Especifique os recursos do documento PDF a serem criptografados. Você pode criptografar todo o documento PDF, tudo exceto os metadados do documento ou apenas os anexos do documento. Se você criptografar somente os anexos do documento, será solicitada uma senha ao usuário quando ele tentar acessar os anexos do arquivo.

Ao criptografar um documento PDF, você pode especificar permissões associadas ao documento protegido. Especificando permissões, você pode controlar as ações que um usuário que abre um documento PDF criptografado por senha pode executar. Por exemplo, para extrair dados de formulário com êxito, você deve definir as seguintes permissões:

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>As permissões são especificadas como `PasswordEncryptionPermission` valores de enumeração.

**Adicionar a senha**

Depois de recuperar um documento de PDF não seguro e definir valores de tempo de execução de criptografia, você pode adicionar uma senha ao documento de PDF.

**Salve o documento PDF criptografado como um arquivo PDF**

Você pode salvar o documento PDF criptografado por senha como um arquivo PDF.

**Consulte também**

[Criptografar um documento PDF usando a API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[Criptografar um documento PDF usando a API de serviço Web](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API do Serviço de Criptografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Criptografar documentos PDF com certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### Criptografar um documento PDF usando a API Java {#encrypt-a-pdf-document-using-the-java-api}

Criptografe um documento PDF com uma senha usando a API de criptografia (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-encryption-client.jar, no caminho de classe do projeto Java.

1. Criar uma API do cliente de criptografia.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EncryptionServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Obtenha um documento PDF para criptografar.

   * Criar um `java.io.FileInputStream` objeto que representa o documento PDF a ser criptografado usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Definir opções de tempo de execução de criptografia.

   * Criar um `PasswordEncryptionOptionSpec` invocando seu construtor.
   * Especifique os recursos do documento PDF a serem criptografados chamando o `PasswordEncryptionOptionSpec` do objeto `setEncryptOption` e passar um `PasswordEncryptionOption` valor de enumeração que especifica os recursos do documento a serem criptografados. Por exemplo, para criptografar todo o documento PDF, incluindo seus metadados e anexos, especifique `PasswordEncryptionOption.ALL`.
   * Criar um `java.util.List` objeto que armazena as permissões de criptografia usando o `ArrayList` construtor.
   * Especifique uma permissão invocando o `java.util.List` object&#39;s `add` e transmitindo um valor de enumeração que corresponde à permissão que você deseja definir. Por exemplo, para definir a permissão que permite a um usuário copiar dados no documento PDF, especifique `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Repita essa etapa para cada permissão a ser definida).
   * Especifique a opção de compatibilidade do Acrobat chamando o `PasswordEncryptionOptionSpec` do objeto `setCompatability` e transmitindo um valor de enumeração que especifica o nível de compatibilidade do Acrobat. Por exemplo, você pode especificar `PasswordEncryptionCompatability.ACRO_7`.
   * Especifique o valor da senha que permite que um usuário abra o documento de PDF criptografado invocando o `PasswordEncryptionOptionSpec` do objeto `setDocumentOpenPassword` e transmitindo um valor de string que representa a senha aberta.
   * Especifique o valor da senha mestre que permite que um usuário remova a criptografia do documento PDF, chamando o `PasswordEncryptionOptionSpec` do objeto `setPermissionPassword` e transmitindo um valor de string que representa a senha mestre.

1. Adicione a senha.

   Criptografe o documento PDF chamando o `EncryptionServiceClient` do objeto `encryptPDFUsingPassword` e transmitindo os seguintes valores:

   * A variável `com.adobe.idp.Document` objeto que contém o documento PDF a ser criptografado com a senha.
   * A variável `PasswordEncryptionOptionSpec` objeto que contém opções de tempo de execução de criptografia.

   A variável `encryptPDFUsingPassword` o método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF criptografado por senha.

1. Salve o documento PDF criptografado como um arquivo PDF.

   * Criar um `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo. Certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `encryptPDFUsingPassword` método.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): criptografia de um documento PDF usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criptografar um documento PDF usando a API de serviço Web {#encrypting-a-pdf-document-using-the-web-service-api}

Criptografe um documento PDF com uma senha usando a API de criptografia (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto de API do cliente de criptografia.

   * Criar um `EncryptionServiceClient` usando seu construtor padrão.
   * Criar um `EncryptionServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `EncryptionServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha um documento PDF para criptografar.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar um documento PDF que é criptografado com uma senha.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF a ser criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo o conteúdo da matriz de bytes à variável `BLOB` do objeto `MTOM` membro de dados.

1. Definir opções de tempo de execução de criptografia.

   * Criar um `PasswordEncryptionOptionSpec` usando seu construtor.
   * Especificar os recursos do documento PDF a serem criptografados atribuindo um `PasswordEncryptionOption` valor de enumeração para o `PasswordEncryptionOptionSpec` do objeto `encryptOption` membro de dados. Para criptografar o PDF inteiro, incluindo seus metadados e anexos, atribua `PasswordEncryptionOption.ALL` para esse membro de dados.
   * Especifique a opção de compatibilidade do Acrobat atribuindo um `PasswordEncryptionCompatability` valor de enumeração para o `PasswordEncryptionOptionSpec` do objeto `compatability` membro de dados. Por exemplo, atribuir `PasswordEncryptionCompatability.ACRO_7` para esse membro de dados.
   * Especifique o valor da senha que permite que um usuário abra o documento de PDF criptografado atribuindo um valor de sequência de caracteres que representa a senha aberta à `PasswordEncryptionOptionSpec` do objeto `documentOpenPassword` membro de dados.
   * Especifique o valor da senha que permite que um usuário remova a criptografia do documento PDF, atribuindo um valor de sequência de caracteres que representa a senha mestra à `PasswordEncryptionOptionSpec` do objeto `permissionPassword` membro de dados.

1. Adicione a senha.

   Criptografe o documento PDF chamando o `EncryptionServiceClient` do objeto `encryptPDFUsingPassword` e transmitindo os seguintes valores:

   * A variável `BLOB` objeto que contém o documento PDF a ser criptografado com a senha.
   * A variável `PasswordEncryptionOptionSpec` objeto que contém opções de tempo de execução de criptografia.

   A variável `encryptPDFUsingPassword` o método retorna um `BLOB` objeto que contém um documento PDF criptografado por senha.

1. Salve o documento PDF criptografado como um arquivo PDF.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF protegido.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `encryptPDFUsingPassword` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Criptografar documentos PDF com certificados {#encrypting-pdf-documents-with-certificates}

A criptografia baseada em certificado permite criptografar um documento para destinatários específicos por meio da tecnologia de chave pública. Vários destinatários podem receber diferentes permissões para o documento. Muitos aspectos da criptografia são viabilizados pela tecnologia de chave pública. Um algoritmo é usado para gerar dois números grandes, conhecidos como *chaves*, que têm as seguintes propriedades:

* Uma chave é usada para criptografar um conjunto de dados. Posteriormente, somente a outra chave pode ser usada para descriptografar os dados.
* É impossível distinguir uma chave da outra.

Uma das chaves atua como a chave privada de um usuário. É importante que somente o usuário tenha acesso a essa chave. A outra chave é a chave pública do usuário, que pode ser compartilhada com outras pessoas.

Um certificado de chave pública contém a chave pública de um usuário e informações de identificação. O formato X.509 é usado para armazenar certificados. Normalmente, os certificados são emitidos e assinados digitalmente por uma autoridade de certificação (CA), que é uma entidade reconhecida que fornece uma medida de confiança na validade do certificado. Os certificados têm uma data de expiração, após a qual não são mais válidos. Além disso, as listas de certificados revogados (CRLs) fornecem informações sobre os certificados revogados antes da data de expiração. As CRLs são publicadas periodicamente pelas autoridades de certificação. O status de revogação de um certificado também pode ser recuperado por meio do Protocolo de Status de Certificados Online (OCSP) na rede.

>[!NOTE]
>
>Se você fizer upload de um documento PDF criptografado para o repositório do AEM Forms, ele não poderá descriptografar o documento PDF e extrair o conteúdo XDP. É recomendável não criptografar um documento antes de carregá-lo no repositório do AEM Forms. (Consulte [Recursos de gravação](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Antes de criptografar um documento PDF com um certificado, você deve garantir que adicionou o certificado ao AEM Forms. Um certificado é adicionado usando o console de administração ou de forma programática usando a API do Gerenciador de Confiança. (Consulte [Importando Credenciais usando a API do Gerenciador de Confiança](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para criptografar um documento PDF com um certificado, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um objeto de API do cliente de criptografia.
1. Obtenha um documento PDF para criptografar.
1. Faça referência ao certificado.
1. Definir opções de tempo de execução de criptografia.
1. Crie um documento de PDF criptografado por certificado.
1. Salve o documento PDF criptografado como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

**Criar um objeto de API do cliente de criptografia**

Para executar programaticamente uma operação de Serviço de criptografia, você deve criar um cliente de Serviço de criptografia. Se você estiver usando a API do Serviço de criptografia Java, crie uma `EncrytionServiceClient` objeto. Se você estiver usando a API de Serviço de criptografia do serviço Web, crie uma `EncryptionServiceService` objeto.

**Obter um documento PDF para criptografar**

Obter um documento PDF não criptografado para criptografar. Se você tentar proteger um documento PDF que já está criptografado, uma exceção será lançada.

**Fazer referência ao certificado**

Para criptografar um documento PDF com um certificado, faça referência a um certificado usado para criptografar um documento PDF. O certificado é um arquivo .cer, .crt ou .pem. Um arquivo PKCS#12 é usado para armazenar chaves privadas com certificados correspondentes.

Ao criptografar um documento PDF com um certificado, especifique as permissões associadas ao documento protegido. Especificando permissões, você pode controlar as ações que um usuário que abre um documento PDF criptografado por certificado pode executar.

**Definir opções de tempo de execução de criptografia**

Especifique os recursos do documento PDF a serem criptografados. Você pode criptografar todo o documento PDF, tudo exceto os metadados do documento ou somente os anexos do documento.

**Criar um documento de PDF criptografado por certificado**

Depois de recuperar um documento de PDF não seguro, fazer referência ao certificado e definir opções de tempo de execução, você pode criar um documento de PDF criptografado para certificado. Depois que o documento PDF for criptografado, será necessária a chave pública correspondente para descriptografá-lo.

**Salve o documento PDF criptografado como um arquivo PDF**

Você pode salvar o documento PDF criptografado como um arquivo PDF.

**Consulte também**

[Criptografar um documento PDF com um certificado usando a API Java](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[Criptografar um documento PDF com um certificado usando a API do serviço Web](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API do Serviço de Criptografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Criptografar documentos PDF com senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Criptografar um documento PDF com um certificado usando a API Java {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

Criptografe um documento PDF com um certificado usando a API de criptografia (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-encryption-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto de API do cliente de criptografia.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EncryptionServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Obtenha um documento PDF para criptografar.

   * Criar um `java.io.FileInputStream` objeto que representa o documento PDF a ser criptografado usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Faça referência ao certificado.

   * Criar um `java.util.List` objeto que armazena informações de permissão usando seu construtor.
   * Especifique a permissão associada ao documento criptografado invocando o `java.util.List` do objeto `add` e passar um `CertificateEncryptionPermissions` valor de enumeração que representa as permissões concedidas ao usuário que abre o documento PDF protegido. Por exemplo, para especificar todas as permissões, passe `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Criar um `Recipient` usando seu construtor.
   * Criar um `java.io.FileInputStream` objeto que representa o certificado usado para criptografar o documento PDF usando seu construtor e transmitindo um valor de cadeia de caracteres que especifica o local do certificado.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto que representa o certificado.
   * Chame o `Recipient` do objeto `setX509Cert` e transmita o `com.adobe.idp.Document` objeto que contém o certificado. (Além disso, a `Recipient`o objeto pode ter um alias de certificado Truststore ou um URL LDAP como uma origem de certificado.)
   * Criar um `CertificateEncryptionIdentity` objeto que armazena informações de permissão e certificado usando seu construtor.
   * Chame o `CertificateEncryptionIdentity` do objeto `setPerms` e transmita o `java.util.List` objeto que armazena informações de permissão.
   * Chame o `CertificateEncryptionIdentity` do objeto `setRecipient` e transmita o `Recipient` objeto que armazena informações de certificado.
   * Criar um `java.util.List` objeto que armazena informações de certificado usando seu construtor.
   * Chame o `java.util.List` método add do objeto e transmita o `CertificateEncryptionIdentity` objeto. (Esta `java.util.List` objeto é passado como parâmetro para o `encryptPDFUsingCertificates` método.)

1. Definir opções de tempo de execução de criptografia.

   * Criar um `CertificateEncryptionOptionSpec` invocando seu construtor.
   * Especifique os recursos do documento PDF a serem criptografados chamando o `CertificateEncryptionOptionSpec` do objeto `setOption` e passar um `CertificateEncryptionOption` valor de enumeração que especifica os recursos do documento a serem criptografados. Por exemplo, para criptografar todo o documento PDF, incluindo seus metadados e anexos, especifique `CertificateEncryptionOption.ALL`.
   * Especifique a opção de compatibilidade do Acrobat chamando o `CertificateEncryptionOptionSpec` do objeto `setCompat` e passar um `CertificateEncryptionCompatibility` valor de enumeração que especifica o nível de compatibilidade do Acrobat. Por exemplo, você pode especificar `CertificateEncryptionCompatibility.ACRO_7`.

1. Crie um documento de PDF criptografado por certificado.

   Criptografe o documento PDF com um certificado invocando o `EncryptionServiceClient` do objeto `encryptPDFUsingCertificates` e transmitindo os seguintes valores:

   * A variável `com.adobe.idp.Document` objeto que contém o documento PDF a ser criptografado.
   * A variável `java.util.List` objeto que armazena informações de certificado.
   * A variável `CertificateEncryptionOptionSpec` objeto que contém opções de tempo de execução de criptografia.

   A variável `encryptPDFUsingCertificates` o método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF criptografado por certificado.

1. Salve o documento PDF criptografado como um arquivo PDF.

   * Criar um `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo. Certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `encryptPDFUsingCertificates` método.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): criptografar um documento PDF com um certificado usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criptografar um documento PDF com um certificado usando a API do serviço Web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Criptografe um documento PDF com um certificado usando a API de criptografia (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto de API do cliente de criptografia.

   * Criar um `EncryptionServiceClient` usando seu construtor padrão.
   * Criar um `EncryptionServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `EncryptionServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha um documento PDF para criptografar.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar um documento PDF que está criptografado com um certificado.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF a ser criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Faça referência ao certificado.

   * Criar um `Recipient` usando seu construtor. Este objeto armazenará informações de certificado.
   * Criar um `BLOB` usando seu construtor. Este `BLOB` O objeto armazenará o certificado que criptografa o documento PDF.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do certificado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo o conteúdo da matriz de bytes à variável `BLOB` do objeto `MTOM` membro de dados.
   * Atribua a `BLOB` objeto que armazena o certificado para o `Recipient` do objeto `x509Cert` membro de dados.
   * Criar um `CertificateEncryptionIdentity` objeto que armazena informações de certificado usando seu construtor.
   * Atribua a `Recipient` objeto que armazena o certificado para o `CertificateEncryptionIdentity`membro de dados do recipient do objeto.
   * Criar um `Object` e atribua a variável `CertificateEncryptionIdentity` para o primeiro elemento da variável `Object` matriz. Este `Object` matriz é passada como parâmetro para a variável `encryptPDFUsingCertificates` método.

1. Definir opções de tempo de execução de criptografia.

   * Criar um `CertificateEncryptionOptionSpec` usando seu construtor.
   * Especificar os recursos do documento PDF a serem criptografados atribuindo um `CertificateEncryptionOption` valor de enumeração para o `CertificateEncryptionOptionSpec` do objeto `option` membro de dados. Para criptografar todo o documento PDF, incluindo seus metadados e anexos, atribua `CertificateEncryptionOption.ALL` para esse membro de dados.
   * Especifique a opção de compatibilidade do Acrobat atribuindo um `CertificateEncryptionCompatibility` valor de enumeração para o `CertificateEncryptionOptionSpec` do objeto `compat` membro de dados. Por exemplo, atribuir `CertificateEncryptionCompatibility.ACRO_7` para esse membro de dados.

1. Crie um documento de PDF criptografado por certificado.

   Criptografe o documento PDF com um certificado invocando o `EncryptionServiceService` do objeto `encryptPDFUsingCertificates` e transmitindo os seguintes valores:

   * A variável `BLOB` objeto que contém o documento PDF a ser criptografado.
   * A variável `Object` matriz que armazena informações de certificado.
   * A variável `CertificateEncryptionOptionSpec` objeto que contém opções de tempo de execução de criptografia.

   A variável `encryptPDFUsingCertificates` o método retorna um `BLOB` objeto que contém um documento PDF criptografado por certificado.

1. Salve o documento PDF criptografado como um arquivo PDF.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF protegido.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `encryptPDFUsingCertificates` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `binaryData` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Removendo a Criptografia Baseada em Certificado {#removing-certificate-based-encryption}

A criptografia baseada em certificado pode ser removida de um documento PDF para que os usuários possam abrir o documento PDF no Adobe Reader ou Acrobat. Para remover a criptografia de um documento PDF que está criptografado com um certificado, uma chave pública deve ser referenciada. Depois que a criptografia é removida de um documento PDF, ela não é mais segura.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para remover a criptografia baseada em certificado de um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de criptografia.
1. Obtenha o documento de PDF criptografado.
1. Remover criptografia.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

**Criar um cliente de serviço de criptografia**

Para executar programaticamente uma operação de Serviço de criptografia, você deve criar um cliente de Serviço de criptografia. Se você estiver usando a API do Serviço de criptografia Java, crie uma `EncrytionServiceClient` objeto. Se você estiver usando a API de Serviço de criptografia do serviço Web, crie uma `EncryptionServiceService` objeto.

**Obter o documento PDF criptografado**

Obtenha um documento PDF criptografado para remover a criptografia baseada em certificado. Se você tentar remover a criptografia de um documento PDF que não está criptografado, uma exceção será lançada. Da mesma forma, se você tentar remover a criptografia baseada em certificado de um documento criptografado por senha, será lançada uma exceção.

**Remover criptografia**

Para remover a criptografia baseada em certificado de um documento PDF criptografado, você precisa de um documento PDF criptografado e da chave privada que corresponde à chave usada para criptografar o documento PDF. O valor de alias da chave privada é especificado ao remover a criptografia baseada em certificado de um documento PDF criptografado. Para obter informações sobre a chave pública, consulte [Criptografar documentos PDF com certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Uma chave privada é armazenada no AEM Forms Trust Store. Quando um certificado é colocado lá, um valor de alias é especificado.

**Salve o documento PDF**

Depois que a criptografia baseada em certificado for removida de um documento PDF criptografado, você poderá salvar o documento PDF como um arquivo PDF. Os usuários podem abrir o documento PDF no Adobe Reader ou Acrobat.

**Consulte também**

[Remover a criptografia baseada em certificado usando a API do Java](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[Remover a criptografia baseada em certificado usando a API do serviço Web](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API do Serviço de Criptografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Remover a criptografia baseada em certificado usando a API do Java {#remove-certificate-based-encryption-using-the-java-api}

Remova a criptografia baseada em certificado de um documento PDF usando a API de criptografia (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-encryption-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente de serviço de criptografia.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EncryptionServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Obtenha o documento de PDF criptografado.

   * Criar um `java.io.FileInputStream` objeto que representa o documento de PDF criptografado usando seu construtor e transmitindo um valor de string que especifica o local do documento de PDF criptografado.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Remover criptografia.

   Remova a criptografia baseada em certificado do documento PDF, chamando o `EncryptionServiceClient` do objeto `removePDFCertificateSecurity` e transmitindo os seguintes valores:

   * A variável `com.adobe.idp.Document` objeto que contém o documento PDF criptografado.
   * Um valor de string que especifica o nome de alias da chave privada que corresponde à chave usada para criptografar o documento PDf.

   A variável `removePDFCertificateSecurity` o método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF não seguro.

1. Salve o documento PDF.

   * Criar um `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo. Certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `removePDFCredentialSecurity` método.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): remoção da criptografia baseada em certificado usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Remover a criptografia baseada em certificado usando a API do serviço Web {#remove-certificate-based-encryption-using-the-web-service-api}

Remova a criptografia baseada em certificado usando a API de criptografia (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de serviço de criptografia.

   * Criar um `EncryptionServiceClient` usando seu construtor padrão.
   * Criar um `EncryptionServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `EncryptionServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento de PDF criptografado.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento PDF criptografado.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo o conteúdo da matriz de bytes à variável `BLOB` do objeto `MTOM` membro de dados.

1. Remover criptografia.

   Chame o `EncryptionServiceClient` do objeto `removePDFCertificateSecurity` e passe os seguintes valores:

   * A variável `BLOB` objeto que contém dados de fluxo de arquivos que representam um documento PDF criptografado.
   * Um valor de string que especifica o nome de alias da chave pública que corresponde à chave privada usada para criptografar o documento PDf.

   A variável `removePDFCredentialSecurity` o método retorna um `BLOB` objeto que contém um documento PDF não seguro.

1. Salve o documento PDF.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF não seguro.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto que foi retornado pelo `removePDFPasswordSecurity` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Remoção da criptografia de senha {#removing-password-encryption}

A criptografia baseada em senha pode ser removida de um documento PDF para que os usuários possam abrir o documento PDF no Adobe Reader ou Acrobat sem precisar especificar uma senha. Depois que a criptografia baseada em senha é removida de um documento PDF, o documento não é mais seguro.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-3}

Para remover a criptografia baseada em senha de um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto
1. Criar um cliente de serviço de criptografia.
1. Obtenha o documento de PDF criptografado.
1. Remova a senha.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

**Criar um cliente de serviço de criptografia**

Para executar programaticamente uma operação de Serviço de criptografia, você deve criar um cliente de Serviço de criptografia. Se você estiver usando a API do Serviço de criptografia Java, crie uma `EncrytionServiceClient` objeto. Se você estiver usando a API de Serviço de criptografia do serviço Web, crie uma `EncryptionServiceService` objeto.

**Obter o documento PDF criptografado**

Obtenha um documento de PDF criptografado para remover a criptografia baseada em senha. Se você tentar remover a criptografia de um documento PDF que não está criptografado, uma exceção será lançada.

**Remover a senha**

Para remover a criptografia baseada em senha de um documento PDF criptografado, você precisa de um documento PDF criptografado e um valor de senha mestre usado para remover a criptografia do documento PDF. A senha usada para abrir um documento de PDF criptografado por senha não pode ser usada para remover a criptografia. Uma senha mestra é especificada quando o documento PDF é criptografado com uma senha. (Consulte [Criptografar documentos PDF com senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**Salve o documento PDF**

Depois que o serviço de Criptografia remover a criptografia baseada em senha de um documento PDF, você poderá salvar o documento PDF como um arquivo PDF. Os usuários podem abrir o documento PDF no Adobe Reader ou no Acrobat sem especificar uma senha.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API do Serviço de Criptografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Criptografar documentos PDF com senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Remover a criptografia baseada em senha usando a API Java {#remove-password-based-encryption-using-the-java-api}

Remova a criptografia baseada em senha de um documento PDF usando a API de criptografia (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-encryption-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente de serviço de criptografia.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EncryptionServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Obtenha o documento de PDF criptografado.

   * Criar um `java.io.FileInputStream` objeto que representa o documento PDF criptografado usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Remova a senha.

   Remova a criptografia baseada em senha do documento PDF chamando o `EncryptionServiceClient` do objeto `removePDFPasswordSecurity` e transmitindo os seguintes valores:

   * A `com.adobe.idp.Document` objeto que contém o documento PDF criptografado.
   * Um valor de string que especifica o valor da senha mestre usado para remover a criptografia do documento PDF.

   A variável `removePDFPasswordSecurity` o método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF não seguro.

1. Salve o documento PDF.

   * Criar um `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo. Certifique-se de usar o `Document` objeto que foi retornado pelo `removePDFPasswordSecurity` método.

**Consulte também**

[Início rápido (modo SOAP): remoção da criptografia baseada em senha usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Remover criptografia baseada em senha usando a API do serviço Web {#remove-password-based-encryption-using-the-web-service-api}

Remova a criptografia com base em senha usando a API de criptografia (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de serviço de criptografia.

   * Criar um `EncryptionServiceClient` usando seu construtor padrão.
   * Criar um `EncryptionServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `EncryptionServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento de PDF criptografado.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar um documento PDF criptografado por senha.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo o conteúdo da matriz de bytes à variável `BLOB` do objeto `MTOM` membro de dados.

1. Remova a senha.

   Chame o `EncryptionServiceService` do objeto `removePDFPasswordSecurity` e passe os seguintes valores:

   * A variável `BLOB` objeto que contém dados de fluxo de arquivos que representam um documento PDF criptografado.
   * Um valor de string que especifica o valor da senha usado para remover a criptografia do documento PDF. Esse valor é especificado ao criptografar o documento PDF com uma senha.

   A variável `removePDFPasswordSecurity` o método retorna um `BLOB` objeto que contém um documento PDF não seguro.

1. Salve o documento PDF.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF não seguro.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto que foi retornado pelo `removePDFPasswordSecurity` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Desbloquear documentos PDF criptografados {#unlocking-encrypted-pdf-documents}

Um documento PDF criptografado por senha ou certificado deve ser desbloqueado antes que outra operação AEM Forms possa ser executada nele. Se você tentar executar uma operação em um documento de PDF criptografado, gerará uma exceção. Depois de desbloquear um documento PDF criptografado, é possível executar uma ou mais operações nele. Essas operações podem pertencer a outros serviços, como o Serviço de extensões da Acrobat Reader DC.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-4}

Para desbloquear um documento PDF criptografado, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de criptografia.
1. Obtenha o documento de PDF criptografado.
1. Desbloquear o documento.
1. Execute uma operação do AEM Forms.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

**Criar um cliente de serviço de criptografia**

Para executar programaticamente uma operação de Serviço de criptografia, você deve criar um cliente de Serviço de criptografia. Se você estiver usando a API do Serviço de criptografia Java, crie uma `EncrytionServiceClient` objeto. Se você estiver usando a API de Serviço de criptografia do serviço Web, crie uma `EncryptionServiceService` objeto.

**Obter o documento PDF criptografado**

Obtenha um documento PDF criptografado para desbloqueá-lo. Se você tentar desbloquear um documento PDF que não está criptografado, uma exceção será lançada.

**Desbloquear o documento**

Para desbloquear um documento PDF criptografado por senha, você precisa de um documento PDF criptografado e um valor de senha usado para abrir um documento PDF criptografado por senha. Esse valor é especificado ao criptografar o documento PDF com uma senha. (Consulte [Criptografar documentos PDF com senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

Para desbloquear um documento PDF criptografado por certificado, é necessário um documento PDF criptografado e o valor de alias da chave pública que corresponde à chave privada usada para criptografar o documento PDF.

**Executar uma operação do AEM Forms**

Depois que um documento PDF criptografado for desbloqueado, você poderá executar outra operação de serviço nele, como aplicar direitos de uso a ele. Esta operação pertence ao serviço de extensões do Acrobat Reader DC.

**Consulte também**

[Desbloquear um documento PDF criptografado usando a API Java](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[Desbloquear um documento PDF criptografado usando a API de serviço Web](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API do Serviço de Criptografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### Desbloquear um documento PDF criptografado usando a API Java {#unlock-an-encrypted-pdf-document-using-the-java-api}

Desbloqueie um documento PDF criptografado usando a API de criptografia (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-encryption-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente de serviço de criptografia.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EncryptionServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Obtenha o documento de PDF criptografado.

   * Criar um `java.io.FileInputStream` objeto que representa o documento de PDF criptografado usando seu construtor e transmitindo um valor de string que especifica o local do documento de PDF criptografado.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Desbloquear o documento.

   Desbloqueie um documento PDF criptografado invocando o `EncryptionServiceClient` do objeto `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` método.

   Para desbloquear um documento PDF criptografado com uma senha, chame o `unlockPDFUsingPassword` e passe os seguintes valores:

   * A `com.adobe.idp.Document` objeto que contém o documento PDF criptografado por senha.
   * Um valor de string que especifica o valor da senha usado para abrir um documento PDF criptografado por senha. Esse valor é especificado ao criptografar o documento PDF com uma senha.

   Para desbloquear um documento PDF criptografado com um certificado, chame o `unlockPDFUsingCredential` e passe os seguintes valores:

   * A `com.adobe.idp.Document` objeto que contém o documento PDF criptografado por certificado.
   * Um valor de string que especifica o nome de alias da chave pública que corresponde à chave privada usada para criptografar o documento PDF.

   A variável `unlockPDFUsingPassword` e `unlockPDFUsingCredential` ambos os métodos retornam um `com.adobe.idp.Document` que você passa para outro método Java do AEM Forms para executar uma operação.

1. Execute uma operação do AEM Forms.

   Execute uma operação AEM Forms no documento PDF desbloqueado para atender aos requisitos de sua empresa. Por exemplo, supondo que você deseja aplicar direitos de uso a um documento PDF desbloqueado, transmita a `com.adobe.idp.Document` objeto que foi retornado por um dos `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` métodos para o `ReaderExtensionsServiceClient` do objeto `applyUsageRights` método.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): desbloqueio de um documento PDF criptografado usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) (modo SOAP)

[Aplicação de direitos de uso a documentos PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Desbloquear um documento PDF criptografado usando a API de serviço Web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Desbloqueie um documento PDF criptografado usando a API de criptografia (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de serviço de criptografia.

   * Criar um `EncryptionServiceClient` usando seu construtor padrão.
   * Criar um `EncryptionServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `EncryptionServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha um documento PDF criptografado.

   * Criar um `BLOB` usando seu construtor.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo o conteúdo da matriz de bytes à variável `BLOB` do objeto `MTOM` membro de dados.

1. Desbloquear o documento.

   Desbloqueie um documento PDF criptografado invocando o `EncryptionServiceClient` do objeto `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` método.

   Para desbloquear um documento PDF criptografado com uma senha, chame o `unlockPDFUsingPassword` e passe os seguintes valores:

   * A `BLOB` objeto que contém o documento PDF criptografado por senha.
   * Um valor de string que especifica o valor da senha usado para abrir um documento PDF criptografado por senha. Esse valor é especificado ao criptografar o documento PDF com uma senha.

   Para desbloquear um documento PDF criptografado com um certificado, chame o `unlockPDFUsingCredential` e passe os seguintes valores:

   * A `BLOB` objeto que contém o documento PDF criptografado por certificado.
   * Um valor de string que especifica o nome de alias da chave pública que corresponde à chave privada usada para criptografar o documento PDf.

   A variável `unlockPDFUsingPassword` e `unlockPDFUsingCredential` ambos os métodos retornam um `com.adobe.idp.Document` objeto que você passa para outro método AEM Forms para executar uma operação.

1. Execute uma operação do AEM Forms.

   Execute uma operação AEM Forms no documento PDF desbloqueado para atender aos requisitos de sua empresa. Por exemplo, supondo que você deseja aplicar direitos de uso ao documento PDF desbloqueado, transmita a `BLOB` objeto que foi retornado por um dos `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` métodos para o `ReaderExtensionsServiceClient` do objeto `applyUsageRights` método.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Determinação do tipo de criptografia {#determining-encryption-type}

Você pode determinar programaticamente o tipo de criptografia que está protegendo um documento PDF usando a API de Serviço de Criptografia Java ou a API de Serviço de Criptografia do serviço Web. Às vezes, é necessário determinar dinamicamente se um documento PDF está criptografado e, nesse caso, o tipo de criptografia. Por exemplo, você pode determinar se um documento PDF está protegido por criptografia baseada em senha ou por uma política Rights Management.

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

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de criptografia.
1. Obtenha o documento de PDF criptografado.
1. Determine o tipo de criptografia.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

**Criar um cliente de serviço**

Para executar programaticamente uma operação de Serviço de criptografia, você deve criar um cliente de Serviço de criptografia. Se você estiver usando a API do Serviço de criptografia Java, crie uma `EncrytionServiceClient` objeto. Se você estiver usando a API de Serviço de criptografia do serviço Web, crie uma `EncryptionServiceService` objeto.

**Obter o documento PDF criptografado**

Obtenha um documento PDF para determinar o tipo de criptografia que está protegendo-o.

**Determine o tipo de criptografia**

Você pode determinar o tipo de criptografia que está protegendo um documento PDF. Se o documento PDF não estiver protegido, o Serviço de criptografia informará que o documento PDF não está protegido.

**Consulte também**

[Determine o tipo de criptografia usando a API Java](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[Determine o tipo de criptografia usando a API do serviço Web](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API do Serviço de Criptografia](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[Protegendo documentos com políticas](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### Determine o tipo de criptografia usando a API Java {#determine-the-encryption-type-using-the-java-api}

Determine o tipo de criptografia que está protegendo um documento PDF usando a API de criptografia (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-encryption-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente de serviço.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `EncryptionServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Obtenha o documento de PDF criptografado.

   * Criar um `java.io.FileInputStream` objeto que representa o documento PDF usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Determine o tipo de criptografia.

   * Determine o tipo de criptografia chamando o `EncryptionServiceClient` do objeto `getPDFEncryption` e transmitindo o `com.adobe.idp.Document` objeto que contém o documento PDF. Este método retorna um valor de `EncryptionTypeResult` objeto.
   * Chame o `EncryptionTypeResult` do objeto `getEncryptionType` método. Este método retorna um valor de `EncryptionType` valor enum que especifica o tipo de criptografia. Por exemplo, se o documento PDF estiver protegido com criptografia baseada em senha, esse método retornará `EncryptionType.PASSWORD`.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): determinação do tipo de criptografia usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determine o tipo de criptografia usando a API do serviço Web {#determine-the-encryption-type-using-the-web-service-api}

Determine o tipo de criptografia que está protegendo um documento PDF usando a API de Criptografia (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de serviço.

   * Criar um `EncryptionServiceClient` usando seu construtor padrão.
   * Criar um `EncryptionServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `EncryptionServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento de PDF criptografado.

   * Criar um `BLOB` usando seu construtor.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo o conteúdo da matriz de bytes à variável `BLOB` do objeto `MTOM` membro de dados.

1. Determine o tipo de criptografia.

   * Chame o `EncryptionServiceClient` do objeto `getPDFEncryption` e transmita o `BLOB` objeto que contém o documento PDF. Este método retorna um valor de `EncryptionTypeResult` objeto.
   * Obtenha o valor do `EncryptionTypeResult` do objeto `encryptionType` método de dados. Por exemplo, se o documento PDF estiver protegido com criptografia baseada em senha, o valor desse membro de dados será `EncryptionType.PASSWORD`.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
