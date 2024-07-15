---
title: Criptografar e descriptografar documentos do PDF
description: Use o serviço de criptografia para criptografar e descriptografar documentos. As tarefas do serviço de criptografia incluem criptografar um documento PDF com uma senha, criptografar um documento PDF com um certificado, remover a criptografia baseada em senha de um documento PDF, remover a criptografia baseada em certificado de um documento PDF, desbloquear o documento PDF para que outras operações de serviço possam ser executadas e determinar o tipo de criptografia de um documento PDF protegido.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '8133'
ht-degree: 0%

---

# Criptografar e descriptografar documentos do PDF {#encrypting-and-decrypting-pdf-documents}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o Serviço de Criptografia**

O serviço de criptografia permite criptografar e descriptografar documentos. Quando um documento é criptografado, seu conteúdo fica ilegível. Um usuário autorizado pode descriptografar o documento para obter acesso ao conteúdo. Se um documento PDF for criptografado com uma senha, o usuário deverá especificar a senha aberta para que o documento possa ser visualizado no Adobe Reader ou no Adobe Acrobat. Da mesma forma, se um documento PDF for criptografado com um certificado, o usuário deverá descriptografar o documento PDF com a chave pública que corresponde ao certificado (chave privada) usado para criptografar o documento PDF.

Você pode realizar essas tarefas usando o Serviço de criptografia:

* Criptografar um documento PDF com uma senha. (Consulte [Criptografar documentos do PDF com uma senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)
* Criptografe um documento PDF com um certificado. (Consulte [Criptografar documentos PDF com certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).)
* Remova a criptografia baseada em senha de um documento PDF. (Consulte [Removendo a Criptografia de Senha](encrypting-decrypting-pdf-documents.md#removing-password-encryption).)
* Remova a criptografia baseada em certificado de um documento PDF. (Consulte [Removendo a Criptografia Baseada em Certificado](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption).)
* Desbloqueie o documento PDF para que outras operações de serviço possam ser executadas. Por exemplo, depois que um documento PDF criptografado por senha é desbloqueado, você pode aplicar uma assinatura digital a ele. (Consulte [Desbloqueando Documentos PDF Criptografados](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents).)
* Determine o tipo de criptografia de um documento de PDF protegido. (Consulte [Determinando o Tipo de Criptografia](encrypting-decrypting-pdf-documents.md#determining-encryption-type).)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Criptografar documentos PDF com senha {#encrypting-pdf-documents-with-a-password}

Quando você criptografa um documento PDF com uma senha, um usuário deve especificar a senha para abrir o documento PDF no Adobe Reader ou Acrobat. Além disso, antes que outra operação do AEM Forms, como a assinatura digital do documento PDF, possa ser executada no documento, um documento PDF criptografado por senha deve ser desbloqueado.

>[!NOTE]
>
>Se você fizer upload de um documento PDF criptografado para o repositório do AEM Forms, ele não poderá descriptografar o documento PDF e extrair o conteúdo XDP. É recomendável não criptografar um documento antes de carregá-lo no repositório do AEM Forms. (Consulte [Gravando Recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

**Criar um objeto de API de Cliente de Criptografia**

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
>As permissões estão especificadas como `PasswordEncryptionPermission` valores de enumeração.

**Adicionar a senha**

Depois de recuperar um documento de PDF não seguro e definir valores de tempo de execução de criptografia, você pode adicionar uma senha ao documento de PDF.

**Salvar o documento PDF criptografado como um arquivo PDF**

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

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EncryptionServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha um documento PDF para criptografar.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF a ser criptografado usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Definir opções de tempo de execução de criptografia.

   * Crie um objeto `PasswordEncryptionOptionSpec` invocando seu construtor.
   * Especifique os recursos do documento de PDF a serem criptografados chamando o método `setEncryptOption` do objeto `PasswordEncryptionOptionSpec` e transmitindo um valor de enumeração `PasswordEncryptionOption` que especifica os recursos do documento a serem criptografados. Por exemplo, para criptografar o documento PDF inteiro, incluindo seus metadados e anexos, especifique `PasswordEncryptionOption.ALL`.
   * Crie um objeto `java.util.List` que armazene as permissões de criptografia usando o construtor `ArrayList`.
   * Especifique uma permissão invocando o método `add` do objeto `java.util.List` e transmitindo um valor de enumeração que corresponda à permissão que deseja definir. Por exemplo, para definir a permissão que permite a um usuário copiar dados no documento PDF, especifique `PasswordEncryptionPermission.PASSWORD_EDIT_COPY`. (Repita essa etapa para cada permissão a ser definida).
   * Especifique a opção de compatibilidade do Acrobat invocando o método `setCompatability` do objeto `PasswordEncryptionOptionSpec` e transmitindo um valor de enumeração que especifica o nível de compatibilidade do Acrobat. Por exemplo, você pode especificar `PasswordEncryptionCompatability.ACRO_7`.
   * Especifique o valor da senha que permite que um usuário abra o documento de PDF criptografado, chamando o método `setDocumentOpenPassword` do objeto `PasswordEncryptionOptionSpec` e transmitindo um valor de cadeia de caracteres que representa a senha aberta.
   * Especifique o valor da senha mestra que permite que um usuário remova a criptografia do documento PDF, chamando o método `setPermissionPassword` do objeto `PasswordEncryptionOptionSpec` e transmitindo um valor de cadeia de caracteres que representa a senha mestra.

1. Adicione a senha.

   Criptografe o documento PDF invocando o método `encryptPDFUsingPassword` do objeto `EncryptionServiceClient` e transmitindo os seguintes valores:

   * O objeto `com.adobe.idp.Document` que contém o documento PDF a ser criptografado com a senha.
   * O objeto `PasswordEncryptionOptionSpec` que contém opções de tempo de execução de criptografia.

   O método `encryptPDFUsingPassword` retorna um objeto `com.adobe.idp.Document` que contém um documento PDF criptografado por senha.

1. Salve o documento PDF criptografado como um arquivo PDF.

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo. Use o objeto `com.adobe.idp.Document` retornado pelo método `encryptPDFUsingPassword`.

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
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto de API do cliente de criptografia.

   * Crie um objeto `EncryptionServiceClient` usando seu construtor padrão.
   * Crie um objeto `EncryptionServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de cadeia de caracteres que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `EncryptionServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha um documento PDF para criptografar.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que está criptografado com uma senha.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF a ser criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Popular o objeto `BLOB` atribuindo o conteúdo da matriz de bytes ao membro de dados `MTOM` do objeto `BLOB`.

1. Definir opções de tempo de execução de criptografia.

   * Crie um objeto `PasswordEncryptionOptionSpec` usando seu construtor.
   * Especifique os recursos do documento de PDF para criptografar atribuindo um valor de enumeração `PasswordEncryptionOption` ao membro de dados `encryptOption` do objeto `PasswordEncryptionOptionSpec`. Para criptografar todo o PDF, incluindo seus metadados e seus anexos, atribua `PasswordEncryptionOption.ALL` a esse membro de dados.
   * Especifique a opção de compatibilidade do Acrobat atribuindo um valor de enumeração `PasswordEncryptionCompatability` ao membro de dados `compatability` do objeto `PasswordEncryptionOptionSpec`. Por exemplo, atribua `PasswordEncryptionCompatability.ACRO_7` a esse membro de dados.
   * Especifique o valor da senha que permite que um usuário abra o documento de PDF criptografado, atribuindo um valor de cadeia de caracteres que representa a senha aberta para o membro de dados `documentOpenPassword` do objeto `PasswordEncryptionOptionSpec`.
   * Especifique o valor da senha que permite que um usuário remova a criptografia do documento PDF, atribuindo um valor de cadeia de caracteres que representa a senha mestra ao membro de dados `permissionPassword` do objeto `PasswordEncryptionOptionSpec`.

1. Adicione a senha.

   Criptografe o documento PDF invocando o método `encryptPDFUsingPassword` do objeto `EncryptionServiceClient` e transmitindo os seguintes valores:

   * O objeto `BLOB` que contém o documento PDF a ser criptografado com a senha.
   * O objeto `PasswordEncryptionOptionSpec` que contém opções de tempo de execução de criptografia.

   O método `encryptPDFUsingPassword` retorna um objeto `BLOB` que contém um documento PDF criptografado por senha.

1. Salve o documento PDF criptografado como um arquivo PDF.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF seguro.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` retornado pelo método `encryptPDFUsingPassword`. Popular a matriz de bytes obtendo o valor do membro de dados `MTOM` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

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
>Se você fizer upload de um documento PDF criptografado para o repositório do AEM Forms, ele não poderá descriptografar o documento PDF e extrair o conteúdo XDP. É recomendável não criptografar um documento antes de carregá-lo no repositório do AEM Forms. (Consulte [Gravando Recursos](/help/forms/developing/aem-forms-repository.md#writing-resources).)

>[!NOTE]
>
>Antes de criptografar um documento PDF com um certificado, você deve garantir que adicionou o certificado ao AEM Forms. Um certificado é adicionado usando o console de administração ou de forma programática usando a API do Gerenciador de Confiança. (Consulte [Importar Credenciais usando a API do Gerenciador de Confiança](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

**Criar um objeto de API de Cliente de Criptografia**

Para executar programaticamente uma operação de Serviço de criptografia, você deve criar um cliente de Serviço de criptografia. Se você estiver usando a API de Serviço de Criptografia Java, crie um objeto `EncrytionServiceClient`. Se você estiver usando a API de Serviço de Criptografia do serviço Web, crie um objeto `EncryptionServiceService`.

**Obter um documento PDF para criptografar**

Obter um documento PDF não criptografado para criptografar. Se você tentar proteger um documento PDF que já está criptografado, uma exceção será lançada.

**Referenciar o certificado**

Para criptografar um documento PDF com um certificado, faça referência a um certificado usado para criptografar um documento PDF. O certificado é um arquivo .cer, .crt ou .pem. Um arquivo PKCS#12 é usado para armazenar chaves privadas com certificados correspondentes.

Ao criptografar um documento PDF com um certificado, especifique as permissões associadas ao documento protegido. Especificando permissões, você pode controlar as ações que um usuário que abre um documento PDF criptografado por certificado pode executar.

**Definir opções de tempo de execução de criptografia**

Especifique os recursos do documento PDF a serem criptografados. Você pode criptografar todo o documento PDF, tudo exceto os metadados do documento ou somente os anexos do documento.

**Criar um documento de PDF criptografado por certificado**

Depois de recuperar um documento de PDF não seguro, fazer referência ao certificado e definir opções de tempo de execução, você pode criar um documento de PDF criptografado para certificado. Depois que o documento PDF for criptografado, será necessária a chave pública correspondente para descriptografá-lo.

**Salvar o documento PDF criptografado como um arquivo PDF**

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

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EncryptionServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha um documento PDF para criptografar.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF a ser criptografado usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Faça referência ao certificado.

   * Crie um objeto `java.util.List` que armazene informações de permissão usando seu construtor.
   * Especifique a permissão associada ao documento criptografado invocando o método `add` do objeto `java.util.List` e transmitindo um valor de enumeração `CertificateEncryptionPermissions` que representa as permissões concedidas ao usuário que abre o documento PDF protegido. Por exemplo, para especificar todas as permissões, passe `CertificateEncryptionPermissions.PKI_ALL_PERM`.
   * Crie um objeto `Recipient` usando seu construtor.
   * Crie um objeto `java.io.FileInputStream` que represente o certificado usado para criptografar o documento PDF usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do certificado.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream` que representa o certificado.
   * Invoque o método `setX509Cert` do objeto `Recipient` e passe o objeto `com.adobe.idp.Document` que contém o certificado. (Além disso, o objeto `Recipient`pode ter um alias de certificado Truststore ou URL LDAP como uma origem de certificado.)
   * Crie um objeto `CertificateEncryptionIdentity` que armazene informações de permissão e certificado usando seu construtor.
   * Invoque o método `setPerms` do objeto `CertificateEncryptionIdentity` e passe o objeto `java.util.List` que armazena informações de permissão.
   * Invoque o método `setRecipient` do objeto `CertificateEncryptionIdentity` e passe o objeto `Recipient` que armazena informações de certificado.
   * Crie um objeto `java.util.List` que armazene informações de certificado usando seu construtor.
   * Chame o método add do objeto `java.util.List` e passe o objeto `CertificateEncryptionIdentity`. (Este objeto `java.util.List` é passado como parâmetro para o método `encryptPDFUsingCertificates`.)

1. Definir opções de tempo de execução de criptografia.

   * Crie um objeto `CertificateEncryptionOptionSpec` invocando seu construtor.
   * Especifique os recursos do documento de PDF a serem criptografados chamando o método `setOption` do objeto `CertificateEncryptionOptionSpec` e transmitindo um valor de enumeração `CertificateEncryptionOption` que especifica os recursos do documento a serem criptografados. Por exemplo, para criptografar o documento PDF inteiro, incluindo seus metadados e anexos, especifique `CertificateEncryptionOption.ALL`.
   * Especifique a opção de compatibilidade do Acrobat invocando o método `setCompat` do objeto `CertificateEncryptionOptionSpec` e transmitindo um valor de enumeração `CertificateEncryptionCompatibility` que especifica o nível de compatibilidade do Acrobat. Por exemplo, você pode especificar `CertificateEncryptionCompatibility.ACRO_7`.

1. Crie um documento de PDF criptografado por certificado.

   Criptografe o documento PDF com um certificado invocando o método `encryptPDFUsingCertificates` do objeto `EncryptionServiceClient` e transmitindo os seguintes valores:

   * O objeto `com.adobe.idp.Document` que contém o documento PDF a ser criptografado.
   * O objeto `java.util.List` que armazena informações de certificado.
   * O objeto `CertificateEncryptionOptionSpec` que contém opções de tempo de execução de criptografia.

   O método `encryptPDFUsingCertificates` retorna um objeto `com.adobe.idp.Document` que contém um documento PDF criptografado por certificado.

1. Salve o documento PDF criptografado como um arquivo PDF.

   * Crie um objeto `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo. Use o objeto `com.adobe.idp.Document` retornado pelo método `encryptPDFUsingCertificates`.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): criptografia de um documento PDF com um certificado usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criptografar um documento PDF com um certificado usando a API do serviço Web {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

Criptografe um documento PDF com um certificado usando a API de criptografia (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto de API do cliente de criptografia.

   * Crie um objeto `EncryptionServiceClient` usando seu construtor padrão.
   * Crie um objeto `EncryptionServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de cadeia de caracteres que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `EncryptionServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha um documento PDF para criptografar.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que está criptografado com um certificado.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF a ser criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` com o conteúdo da matriz de bytes.

1. Faça referência ao certificado.

   * Crie um objeto `Recipient` usando seu construtor. Este objeto armazenará informações de certificado.
   * Crie um objeto `BLOB` usando seu construtor. Este objeto `BLOB` armazenará o certificado que criptografa o documento PDF.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do certificado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Popular o objeto `BLOB` atribuindo o conteúdo da matriz de bytes ao membro de dados `MTOM` do objeto `BLOB`.
   * Atribua o objeto `BLOB` que armazena o certificado ao membro de dados `x509Cert` do objeto `Recipient`.
   * Crie um objeto `CertificateEncryptionIdentity` que armazene informações de certificado usando seu construtor.
   * Atribua o objeto `Recipient` que armazena o certificado ao membro de dados do destinatário do objeto `CertificateEncryptionIdentity`.
   * Crie uma matriz `Object` e atribua o objeto `CertificateEncryptionIdentity` ao primeiro elemento da matriz `Object`. Esta matriz `Object` é passada como parâmetro para o método `encryptPDFUsingCertificates`.

1. Definir opções de tempo de execução de criptografia.

   * Crie um objeto `CertificateEncryptionOptionSpec` usando seu construtor.
   * Especifique os recursos do documento de PDF para criptografar atribuindo um valor de enumeração `CertificateEncryptionOption` ao membro de dados `option` do objeto `CertificateEncryptionOptionSpec`. Para criptografar todo o documento de PDF, incluindo seus metadados e seus anexos, atribua `CertificateEncryptionOption.ALL` a esse membro de dados.
   * Especifique a opção de compatibilidade do Acrobat atribuindo um valor de enumeração `CertificateEncryptionCompatibility` ao membro de dados `compat` do objeto `CertificateEncryptionOptionSpec`. Por exemplo, atribua `CertificateEncryptionCompatibility.ACRO_7` a esse membro de dados.

1. Crie um documento de PDF criptografado por certificado.

   Criptografe o documento PDF com um certificado invocando o método `encryptPDFUsingCertificates` do objeto `EncryptionServiceService` e transmitindo os seguintes valores:

   * O objeto `BLOB` que contém o documento PDF a ser criptografado.
   * A matriz `Object` que armazena informações de certificado.
   * O objeto `CertificateEncryptionOptionSpec` que contém opções de tempo de execução de criptografia.

   O método `encryptPDFUsingCertificates` retorna um objeto `BLOB` que contém um documento PDF criptografado por certificado.

1. Salve o documento PDF criptografado como um arquivo PDF.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF seguro.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do objeto `BLOB` retornado pelo método `encryptPDFUsingCertificates`. Popular a matriz de bytes obtendo o valor do membro de dados `binaryData` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Removendo a Criptografia Baseada em Certificado {#removing-certificate-based-encryption}

A criptografia baseada em certificado pode ser removida de um documento PDF para que os usuários possam abrir o documento PDF no Adobe Reader ou Acrobat. Para remover a criptografia de um documento PDF que está criptografado com um certificado, uma chave pública deve ser referenciada. Depois que a criptografia é removida de um documento PDF, ela não é mais segura.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Para executar programaticamente uma operação de Serviço de criptografia, você deve criar um cliente de Serviço de criptografia. Se você estiver usando a API de Serviço de Criptografia Java, crie um objeto `EncrytionServiceClient`. Se você estiver usando a API de Serviço de Criptografia do serviço Web, crie um objeto `EncryptionServiceService`.

**Obter o documento de PDF criptografado**

Obtenha um documento PDF criptografado para remover a criptografia baseada em certificado. Se você tentar remover a criptografia de um documento PDF que não está criptografado, uma exceção será lançada. Da mesma forma, se você tentar remover a criptografia baseada em certificado de um documento criptografado por senha, será lançada uma exceção.

**Remover criptografia**

Para remover a criptografia baseada em certificado de um documento PDF criptografado, você precisa de um documento PDF criptografado e da chave privada que corresponde à chave usada para criptografar o documento PDF. O valor de alias da chave privada é especificado ao remover a criptografia baseada em certificado de um documento PDF criptografado. Para obter informações sobre a chave pública, consulte [Criptografando Documentos PDF com Certificados](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates).

>[!NOTE]
>
>Uma chave privada é armazenada no AEM Forms Trust Store. Quando um certificado é colocado lá, um valor de alias é especificado.

**Salvar o documento do PDF**

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

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EncryptionServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento de PDF criptografado.

   * Crie um objeto `java.io.FileInputStream` que represente o documento de PDF criptografado usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento de PDF criptografado.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Remover criptografia.

   Remova a criptografia baseada em certificado do documento PDF, chamando o método `removePDFCertificateSecurity` do objeto `EncryptionServiceClient` e transmitindo os seguintes valores:

   * O objeto `com.adobe.idp.Document` que contém o documento PDF criptografado.
   * Um valor de string que especifica o nome de alias da chave privada que corresponde à chave usada para criptografar o documento PDf.

   O método `removePDFCertificateSecurity` retorna um objeto `com.adobe.idp.Document` que contém um documento PDF não seguro.

1. Salve o documento PDF.

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para copiar o conteúdo do objeto `Document` para o arquivo. Use o objeto `com.adobe.idp.Document` retornado pelo método `removePDFCredentialSecurity`.

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
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de serviço de criptografia.

   * Crie um objeto `EncryptionServiceClient` usando seu construtor padrão.
   * Crie um objeto `EncryptionServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de cadeia de caracteres que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `EncryptionServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento de PDF criptografado.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF criptografado.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Popular o objeto `BLOB` atribuindo o conteúdo da matriz de bytes ao membro de dados `MTOM` do objeto `BLOB`.

1. Remover criptografia.

   Chame o método `removePDFCertificateSecurity` do objeto `EncryptionServiceClient` e passe os seguintes valores:

   * O objeto `BLOB` que contém dados de fluxo de arquivos que representam um documento PDF criptografado.
   * Um valor de string que especifica o nome de alias da chave pública que corresponde à chave privada usada para criptografar o documento PDf.

   O método `removePDFCredentialSecurity` retorna um objeto `BLOB` que contém um documento PDF não seguro.

1. Salve o documento PDF.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF não seguro.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `removePDFPasswordSecurity`. Popular a matriz de bytes obtendo o valor do membro de dados `MTOM` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Remoção da criptografia de senha {#removing-password-encryption}

A criptografia baseada em senha pode ser removida de um documento PDF para que os usuários possam abrir o documento PDF no Adobe Reader ou Acrobat sem precisar especificar uma senha. Depois que a criptografia baseada em senha é removida de um documento PDF, o documento não é mais seguro.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Para executar programaticamente uma operação de Serviço de criptografia, você deve criar um cliente de Serviço de criptografia. Se você estiver usando a API de Serviço de Criptografia Java, crie um objeto `EncrytionServiceClient`. Se você estiver usando a API de Serviço de Criptografia do serviço Web, crie um objeto `EncryptionServiceService`.

**Obter o documento de PDF criptografado**

Obtenha um documento de PDF criptografado para remover a criptografia baseada em senha. Se você tentar remover a criptografia de um documento PDF que não está criptografado, uma exceção será lançada.

**Remover a senha**

Para remover a criptografia baseada em senha de um documento PDF criptografado, você precisa de um documento PDF criptografado e um valor de senha mestre usado para remover a criptografia do documento PDF. A senha usada para abrir um documento de PDF criptografado por senha não pode ser usada para remover a criptografia. Uma senha mestra é especificada quando o documento PDF é criptografado com uma senha. (Consulte [Criptografar documentos do PDF com uma senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

**Salvar o documento do PDF**

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

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EncryptionServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento de PDF criptografado.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF criptografado usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Remova a senha.

   Remova a criptografia baseada em senha do documento PDF, chamando o método `removePDFPasswordSecurity` do objeto `EncryptionServiceClient` e transmitindo os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que contém o documento PDF criptografado.
   * Um valor de string que especifica o valor da senha mestre usado para remover a criptografia do documento PDF.

   O método `removePDFPasswordSecurity` retorna um objeto `com.adobe.idp.Document` que contém um documento PDF não seguro.

1. Salve o documento PDF.

   * Crie um objeto `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para copiar o conteúdo do objeto `Document` para o arquivo. Use o objeto `Document` retornado pelo método `removePDFPasswordSecurity`.

**Consulte também**

[Início rápido (modo SOAP): remoção da criptografia baseada em senha usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### Remover criptografia baseada em senha usando a API do serviço Web {#remove-password-based-encryption-using-the-web-service-api}

Remova a criptografia com base em senha usando a API de criptografia (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de serviço de criptografia.

   * Crie um objeto `EncryptionServiceClient` usando seu construtor padrão.
   * Crie um objeto `EncryptionServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de cadeia de caracteres que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `EncryptionServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento de PDF criptografado.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF criptografado por senha.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Popular o objeto `BLOB` atribuindo o conteúdo da matriz de bytes ao membro de dados `MTOM` do objeto `BLOB`.

1. Remova a senha.

   Chame o método `removePDFPasswordSecurity` do objeto `EncryptionServiceService` e passe os seguintes valores:

   * O objeto `BLOB` que contém dados de fluxo de arquivos que representam um documento PDF criptografado.
   * Um valor de string que especifica o valor da senha usado para remover a criptografia do documento PDF. Esse valor é especificado ao criptografar o documento PDF com uma senha.

   O método `removePDFPasswordSecurity` retorna um objeto `BLOB` que contém um documento PDF não seguro.

1. Salve o documento PDF.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF não seguro.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `removePDFPasswordSecurity`. Popular a matriz de bytes obtendo o valor do membro de dados `MTOM` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Desbloquear documentos PDF criptografados {#unlocking-encrypted-pdf-documents}

Um documento PDF criptografado por senha ou certificado deve ser desbloqueado antes que outra operação AEM Forms possa ser executada nele. Se você tentar executar uma operação em um documento de PDF criptografado, gerará uma exceção. Depois de desbloquear um documento PDF criptografado, é possível executar uma ou mais operações nele. Essas operações podem pertencer a outros serviços, como o Serviço de extensões da Acrobat Reader DC.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Para executar programaticamente uma operação de Serviço de criptografia, você deve criar um cliente de Serviço de criptografia. Se você estiver usando a API de Serviço de Criptografia Java, crie um objeto `EncrytionServiceClient`. Se você estiver usando a API de Serviço de Criptografia do serviço Web, crie um objeto `EncryptionServiceService`.

**Obter o documento de PDF criptografado**

Obtenha um documento PDF criptografado para desbloqueá-lo. Se você tentar desbloquear um documento PDF que não está criptografado, uma exceção será lançada.

**Desbloquear o documento**

Para desbloquear um documento PDF criptografado por senha, você precisa de um documento PDF criptografado e um valor de senha usado para abrir um documento PDF criptografado por senha. Esse valor é especificado ao criptografar o documento PDF com uma senha. (Consulte [Criptografar documentos do PDF com uma senha](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password).)

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

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EncryptionServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento de PDF criptografado.

   * Crie um objeto `java.io.FileInputStream` que represente o documento de PDF criptografado usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento de PDF criptografado.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Desbloquear o documento.

   Desbloqueie um documento PDF criptografado invocando o método `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` do objeto `EncryptionServiceClient`.

   Para desbloquear um documento PDF criptografado com uma senha, chame o método `unlockPDFUsingPassword` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que contém o documento PDF criptografado por senha.
   * Um valor de string que especifica o valor da senha usado para abrir um documento PDF criptografado por senha. Esse valor é especificado ao criptografar o documento PDF com uma senha.

   Para desbloquear um documento PDF que está criptografado com um certificado, chame o método `unlockPDFUsingCredential` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que contém o documento PDF criptografado por certificado.
   * Um valor de string que especifica o nome de alias da chave pública que corresponde à chave privada usada para criptografar o documento PDF.

   Os métodos `unlockPDFUsingPassword` e `unlockPDFUsingCredential` retornam um objeto `com.adobe.idp.Document` que você passa para outro método Java do AEM Forms para executar uma operação.

1. Execute uma operação do AEM Forms.

   Execute uma operação AEM Forms no documento PDF desbloqueado para atender aos requisitos de sua empresa. Por exemplo, supondo que você deseja aplicar direitos de uso a um documento PDF desbloqueado, passe o objeto `com.adobe.idp.Document` que foi retornado pelos métodos `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` para o método `applyUsageRights` do objeto `ReaderExtensionsServiceClient`.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Início rápido (modo SOAP): desbloqueando um documento PDF criptografado usando a API Java](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api) (modo SOAP)

[Aplicação de direitos de uso a documentos PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Desbloquear um documento PDF criptografado usando a API de serviço Web {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

Desbloqueie um documento PDF criptografado usando a API de criptografia (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de serviço de criptografia.

   * Crie um objeto `EncryptionServiceClient` usando seu construtor padrão.
   * Crie um objeto `EncryptionServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de cadeia de caracteres que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `EncryptionServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha um documento PDF criptografado.

   * Crie um objeto `BLOB` usando seu construtor.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Popular o objeto `BLOB` atribuindo o conteúdo da matriz de bytes ao membro de dados `MTOM` do objeto `BLOB`.

1. Desbloquear o documento.

   Desbloqueie um documento PDF criptografado invocando o método `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` do objeto `EncryptionServiceClient`.

   Para desbloquear um documento PDF criptografado com uma senha, chame o método `unlockPDFUsingPassword` e passe os seguintes valores:

   * Um objeto `BLOB` que contém o documento PDF criptografado por senha.
   * Um valor de string que especifica o valor da senha usado para abrir um documento PDF criptografado por senha. Esse valor é especificado ao criptografar o documento PDF com uma senha.

   Para desbloquear um documento PDF que está criptografado com um certificado, chame o método `unlockPDFUsingCredential` e passe os seguintes valores:

   * Um objeto `BLOB` que contém o documento PDF criptografado por certificado.
   * Um valor de string que especifica o nome de alias da chave pública que corresponde à chave privada usada para criptografar o documento PDf.

   Os métodos `unlockPDFUsingPassword` e `unlockPDFUsingCredential` retornam um objeto `com.adobe.idp.Document` que você passa para outro método AEM Forms para executar uma operação.

1. Execute uma operação do AEM Forms.

   Execute uma operação AEM Forms no documento PDF desbloqueado para atender aos requisitos de sua empresa. Por exemplo, supondo que você deseja aplicar direitos de uso ao documento PDF desbloqueado, passe o objeto `BLOB` que foi retornado pelos métodos `unlockPDFUsingPassword` ou `unlockPDFUsingCredential` para o método `applyUsageRights` do objeto `ReaderExtensionsServiceClient`.

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
>Para obter mais informações sobre o Serviço de criptografia, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Para executar programaticamente uma operação de Serviço de criptografia, você deve criar um cliente de Serviço de criptografia. Se você estiver usando a API de Serviço de Criptografia Java, crie um objeto `EncrytionServiceClient`. Se você estiver usando a API de Serviço de Criptografia do serviço Web, crie um objeto `EncryptionServiceService`.

**Obter o documento de PDF criptografado**

Obtenha um documento PDF para determinar o tipo de criptografia que está protegendo-o.

**Determinar o tipo de criptografia**

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

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `EncryptionServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento de PDF criptografado.

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Determine o tipo de criptografia.

   * Determine o tipo de criptografia chamando o método `getPDFEncryption` do objeto `EncryptionServiceClient` e transmitindo o objeto `com.adobe.idp.Document` que contém o documento PDF. Este método retorna um objeto `EncryptionTypeResult`.
   * Invoque o método `getEncryptionType` do objeto `EncryptionTypeResult`. Este método retorna um valor de enumeração `EncryptionType` que especifica o tipo de criptografia. Por exemplo, se o documento PDF estiver protegido com criptografia baseada em senha, esse método retornará `EncryptionType.PASSWORD`.

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
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de serviço.

   * Crie um objeto `EncryptionServiceClient` usando seu construtor padrão.
   * Crie um objeto `EncryptionServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de cadeia de caracteres que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/EncryptionService?WSDL`.) Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `EncryptionServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `EncryptionServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `EncryptionServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento de PDF criptografado.

   * Crie um objeto `BLOB` usando seu construtor.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Popular o objeto `BLOB` atribuindo o conteúdo da matriz de bytes ao membro de dados `MTOM` do objeto `BLOB`.

1. Determine o tipo de criptografia.

   * Chame o método `getPDFEncryption` do objeto `EncryptionServiceClient` e passe o objeto `BLOB` que contém o documento PDF. Este método retorna um objeto `EncryptionTypeResult`.
   * Obtenha o valor do método de dados `encryptionType` do objeto `EncryptionTypeResult`. Por exemplo, se o documento PDF estiver protegido com criptografia baseada em senha, o valor desse membro de dados será `EncryptionType.PASSWORD`.

**Consulte também**

[Resumo das etapas](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
