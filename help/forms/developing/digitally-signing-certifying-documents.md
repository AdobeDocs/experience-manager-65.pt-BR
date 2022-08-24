---
title: Assinar e certificar documentos digitalmente
seo-title: Digitally Signing and Certifying Documents
description: Use o Serviço de assinatura para adicionar e excluir campos de assinatura digital em um documento PDF, recuperar os nomes dos campos de assinatura localizados em um documento PDF, modificar campos de assinatura, assinar digitalmente documentos PDF, certificar documentos PDF, validar assinaturas digitais localizadas em um documento PDF, validar todas as assinaturas digitais localizadas em um documento PDF e remover uma assinatura digital de um campo de assinatura.
seo-description: Use the Signature service to add and delete digital signature fields to a PDF document, retrieve the names of signature fields located in a PDF document, modify signature fields, digitally sign PDF documents, certify PDF documents, validate digital signatures located in a PDF document, validate all digital signatures located in a PDF document, and remove a digital signature from a signature field.
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '17046'
ht-degree: 0%

---

# Assinar e certificar documentos digitalmente {#digitally-signing-and-certifying-documents}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

**Sobre o Serviço de Assinatura**

O serviço de assinatura permite que sua organização proteja a segurança e a privacidade de documentos da Adobe PDF que distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients pretendidos possam alterar documentos. Como os recursos de segurança são aplicados ao próprio documento, ele permanece protegido e controlado por todo o seu ciclo de vida. Um documento permanece protegido além do firewall, quando é baixado offline e quando é enviado de volta à sua organização.

>[!NOTE]
>
>Você pode criar um manipulador de assinatura personalizado para o serviço de assinatura chamado quando determinadas operações são invocadas, como a assinatura de um documento PDF.

**Nomes de campos de assinatura**

Algumas operações do serviço de assinatura exigem a especificação do nome do campo de assinatura no qual uma operação é executada. Por exemplo, ao assinar um documento PDF, especifique o nome do campo de assinatura a ser assinado. Suponha que o nome completo de um campo de assinatura seja `form1[0].Form1[0].SignatureField1[0]`. Você pode especificar `SignatureField1[0]` em vez de `form1[0].Form1[0].SignatureField1[0]`.

Às vezes, um conflito faz com que o serviço de assinatura assine (ou execute outra operação que exija o nome do campo de assinatura) o campo errado. Este conflito é o resultado do nome `SignatureField1[0]` que aparece em dois ou mais lugares no mesmo documento PDF. Por exemplo, considere um documento PDF que contém dois campos de assinatura nomeados `form1[0].Form1[0].SignatureField1[0]` e `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` e você especificar `SignatureField1[0]`. Nessa situação, o serviço de assinatura assina o primeiro campo de assinatura encontrado ao iterar todos os campos de assinatura no documento.

Se houver vários campos de assinatura localizados em um documento PDF, é recomendável especificar os nomes completos dos campos de assinatura. Ou seja, especifique `form1[0].Form1[0].SignatureField1[0]`em vez de `SignatureField1[0]`.

Você pode realizar essas tarefas usando o Serviço de assinatura:

* Adicione e exclua campos de assinatura digital a um documento PDF. (Consulte [Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields).)
* Recupere os nomes dos campos de assinatura localizados em um documento PDF. (Consulte [Recuperando nomes de campos de assinatura](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* Modifique campos de assinatura. (Consulte [Modificação de campos de assinatura](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* Assine digitalmente documentos PDF. (Consulte [Assinar documentos do PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* Certifique documentos PDF. (Consulte [Certificando documentos de PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* Valide as assinaturas digitais localizadas em um documento PDF. (Consulte [Verificação de assinaturas digitais](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Valide todas as assinaturas digitais localizadas em um documento PDF. (Consulte [Verificação de várias assinaturas digitais](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Remova uma assinatura digital de um campo de assinatura. (Consulte [Remover assinaturas digitais](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)...

## Adicionar campos de assinatura {#adding-signature-fields}

Assinaturas digitais são exibidas em campos de assinatura, que são campos de formulário que contêm uma representação gráfica da assinatura. Os campos de assinatura podem ser visíveis ou invisíveis. Os signatários podem usar um campo de assinatura preexistente ou um campo de assinatura pode ser adicionado programaticamente. Em ambos os casos, o campo de assinatura deve existir antes que um documento PDF possa ser assinado.

Você pode adicionar um campo de assinatura por programação usando a API Java do serviço de assinatura ou a API do serviço da Web de assinatura. É possível adicionar mais de um campo de assinatura a um documento PDF; no entanto, cada nome de campo de assinatura deve ser exclusivo.

>[!NOTE]
>
>Alguns tipos de documento PDF não permitem adicionar um campo de assinatura por programação. Para obter mais informações sobre o serviço de assinatura e adicionar campos de assinatura, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para adicionar um campo de assinatura a um documento PDF, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha um documento PDF ao qual um campo de assinatura é adicionado.
1. Adicione um campo de assinatura.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

**Criar um cliente de assinatura**

Antes de poder executar programaticamente uma operação de serviço de assinatura, é necessário criar um cliente de serviço de assinatura.

**Obter um documento PDF ao qual um campo de assinatura é adicionado**

Você deve obter um documento PDF ao qual um campo de assinatura é adicionado.

**Adicionar um campo de assinatura**

Para adicionar um campo de assinatura a um documento PDF, especifique valores de coordenadas que identificam o local do campo de assinatura. (Se você adicionar um campo de assinatura invisível, esses valores não serão necessários.) Além disso, você pode especificar quais campos no documento PDF são bloqueados depois que uma assinatura é aplicada ao campo de assinatura.

**Salve o documento PDF como um arquivo PDF**

Depois que o serviço de assinatura adiciona um campo de assinatura ao documento PDF, você pode salvar o documento como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou Adobe Reader.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assinar documentos do PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Adicionar campos de assinatura usando a API Java {#add-signature-fields-using-the-java-api}

Adicione um campo de assinatura usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-assinaturas-client.jar, no classpath do seu projeto Java.

1. Criar um cliente de assinatura

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `SignatureServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obter um documento PDF ao qual um campo de assinatura é adicionado

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF ao qual um campo de assinatura é adicionado usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Adicionar um campo de assinatura

   * Crie um `PositionRectangle` que especifica o local do campo de assinatura usando seu construtor. No construtor, especifique valores de coordenadas.
   * Se desejar, crie uma `FieldMDPOptions` que especifica os campos bloqueados quando uma assinatura digital é aplicada ao campo de assinatura.
   * Adicione um campo de assinatura a um documento PDF chamando o `SignatureServiceClient` do objeto `addSignatureField` e transmitindo os seguintes valores:

      * A `com.adobe.idp`. `Document` objeto que representa o documento PDF ao qual um campo de assinatura é adicionado.
      * Um valor de string que especifica o nome do campo de assinatura.
      * A `java.lang.Integer` que representa o número da página à qual um campo de assinatura é adicionado.
      * A `PositionRectangle` que especifica o local do campo de assinatura.
      * A `FieldMDPOptions` objeto que especifica os campos no documento PDF bloqueados depois que uma assinatura digital é aplicada ao campo de assinatura. Esse valor de parâmetro é opcional e você pode passar `null`.
   * A `PDFSeedValueOptions` que especifica vários valores de tempo de execução. Esse valor de parâmetro é opcional e você pode passar `null`.

      O `addSignatureField` método retorna um `com.adobe.idp`. `Document` objeto que representa um documento PDF que contém um campo de assinatura.
   >[!NOTE]
   >
   >Você pode invocar o `SignatureServiceClient` do objeto `addInvisibleSignatureField` para adicionar um campo de assinatura invisível.

1. Salve o documento PDF como um arquivo PDF

   * Crie um `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o `com.adobe.idp`. `Document` do objeto `copyToFile` para copiar o conteúdo da `Document` ao arquivo. Certifique-se de usar a variável `com.adobe.idp`. `Document` objeto retornado pelo `addSignatureField` método .

**Consulte também**

[Início rápido da API do Serviço de assinatura](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Adicionar campos de assinatura usando a API do serviço da Web {#add-signature-fields-using-the-web-service-api}

Para adicionar um campo de assinatura usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Criar um cliente de assinatura

   * Crie um `SignatureServiceClient` usando seu construtor padrão.
   * Crie um `SignatureServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `SignatureServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obter um documento PDF ao qual um campo de assinatura é adicionado

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento PDF que conterá um campo de assinatura.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Adicionar um campo de assinatura

   Adicione um campo de assinatura ao documento PDF chamando o `SignatureServiceClient` do objeto `addSignatureField` e transmitindo os seguintes valores:

   * A `BLOB` objeto que representa o documento PDF ao qual um campo de assinatura é adicionado.
   * Um valor de string que especifica o nome do campo de assinatura.
   * Um valor inteiro que representa o número da página à qual um campo de assinatura é adicionado.
   * A `PositionRect` que especifica o local do campo de assinatura.
   * A `FieldMDPOptions` objeto que especifica os campos no documento PDF bloqueados depois que uma assinatura digital é aplicada ao campo de assinatura. Esse valor de parâmetro é opcional e você pode passar `null`.
   * A `PDFSeedValueOptions` que especifica vários valores de tempo de execução. Esse valor de parâmetro é opcional e você pode passar `null`.

   O `addSignatureField` método retorna um `BLOB` objeto que representa um documento PDF que contém um campo de assinatura.

1. Salve o documento PDF como um arquivo PDF

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF que conterá o campo de assinatura e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto retornado pelo `addSignatureField` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `binaryData` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperando nomes de campos de assinatura {#retrieving-signature-field-names}

Você pode recuperar os nomes de todos os campos de assinatura localizados em um documento do PDF que deseja assinar ou certificar. Se você não tiver certeza dos nomes dos campos de assinatura localizados em um documento PDF ou quiser verificar os nomes, poderá recuperá-los programaticamente. O serviço de assinatura retorna o nome totalmente qualificado do campo de assinatura, como `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumo das etapas {#summary_of_steps-1}

Para recuperar nomes de campos de assinatura, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém campos de assinatura.
1. Recupere os nomes dos campos de assinatura.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de poder executar programaticamente uma operação de serviço de assinatura, é necessário criar um cliente de serviço de assinatura.

**Obter o documento PDF que contém campos de assinatura**

Recupere um documento PDF que contenha campos de assinatura.

**Recuperar os nomes dos campos de assinatura**

Você pode recuperar nomes de campos de assinatura depois de recuperar um documento PDF que contenha um ou mais campos de assinatura.

**Consulte também**

[Recuperar nomes de campos de assinatura usando a API Java](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Recuperar campo de assinatura usando a API do serviço da Web](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields)

### Recuperar nomes de campos de assinatura usando a API Java {#retrieve-signature-field-names-using-the-java-api}

Recupere nomes de campos de assinatura usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-assinaturas-client.jar, no classpath do seu projeto Java.

1. Criar um cliente de assinatura

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `SignatureServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obter o documento PDF que contém campos de assinatura

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF que contém campos de assinatura usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Recuperar os nomes dos campos de assinatura

   * Recupere os nomes dos campos de assinatura chamando o `SignatureServiceClient` do objeto `getSignatureFieldList` e a aprovação do `com.adobe.idp.Document` objeto que contém o documento PDF que contém os campos de assinatura. Esse método retorna um `java.util.List` objeto, no qual cada elemento contém uma `PDFSignatureField` objeto. Com esse objeto, é possível obter informações adicionais sobre um campo de assinatura, como se ele estivesse visível.
   * Iterar por meio do `java.util.List` para determinar se há nomes de campos de assinatura. Para cada campo de assinatura no documento PDF, você pode obter um `PDFSignatureField` objeto. Para obter o nome do campo de assinatura, chame o `PDFSignatureField` do objeto `getName` método . Esse método retorna um valor de string que especifica o nome do campo de assinatura.

**Consulte também**

[Recuperando nomes de campos de assinatura](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Início rápido (modo SOAP): Recuperação de nomes de campos de assinatura usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar campo de assinatura usando a API do serviço da Web {#retrieve-signature-field-using-the-web-service-api}

Recupere nomes de campos de assinatura usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Criar um cliente de assinatura

   * Crie um `SignatureServiceClient` usando seu construtor padrão.
   * Crie um `SignatureServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `SignatureServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obter o documento PDF que contém campos de assinatura

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento PDF que contém campos de assinatura.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` no campo do conteúdo da matriz de bytes.

1. Recuperar os nomes dos campos de assinatura

   * Recupere os nomes dos campos de assinatura chamando `SignatureServiceClient` do objeto `getSignatureFieldList` e a aprovação do `BLOB` objeto que contém o documento PDF que contém os campos de assinatura. Esse método retorna um `MyArrayOfPDFSignatureField` objeto de coleção em que cada elemento contém uma `PDFSignatureField` objeto.
   * Iterar por meio do `MyArrayOfPDFSignatureField` para determinar se há nomes de campos de assinatura. Para cada campo de assinatura no documento PDF, você pode obter um `PDFSignatureField` objeto. Para obter o nome do campo de assinatura, chame o `PDFSignatureField` do objeto `getName` método . Esse método retorna um valor de string que especifica o nome do campo de assinatura.

**Consulte também**

[Recuperando nomes de campos de assinatura](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificação de campos de assinatura {#modifying-signature-fields}

Você pode modificar campos de assinatura localizados em um documento do PDF usando a API do Java e a API do serviço da Web. A modificação de um campo de assinatura envolve manipular seus valores de dicionário de bloqueio de campo de assinatura ou valores de dicionário de valor de semente.

A *dicionário de bloqueio de campo* especifica uma lista de campos que são bloqueados quando o campo de assinatura é assinado. Um campo bloqueado impede que os usuários façam alterações no campo. A *dicionário de valor de semente* contém informações de restrição que são usadas no momento em que a assinatura é aplicada. Por exemplo, você pode alterar permissões que controlam as ações que podem ocorrer sem invalidar uma assinatura.

Ao modificar um campo de assinatura existente, é possível fazer alterações no documento PDF para refletir as necessidades comerciais em alteração. Por exemplo, um novo requisito comercial pode exigir o bloqueio de todos os campos de documento depois que o documento é assinado.

Esta seção explica como modificar um campo de assinatura alterando tanto o dicionário de bloqueio de campo quanto os valores do dicionário de valor de semente. As alterações feitas no dicionário de bloqueio do campo de assinatura resultam no bloqueio de todos os campos no documento PDF quando um campo de assinatura é assinado. As alterações feitas no dicionário de valor de semente proíbem tipos específicos de alterações no documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura e modificar campos de assinatura, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para modificar campos de assinatura localizados em um documento PDF, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém o campo de assinatura a ser modificado.
1. Defina os valores do dicionário.
1. Modifique o campo de assinatura.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do LiveCycle](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de poder executar programaticamente uma operação de serviço de assinatura, é necessário criar um cliente de serviço de assinatura.

**Obtenha o documento PDF que contém o campo de assinatura para modificar**

Recupere um documento PDF que contenha o campo de assinatura a ser modificado.

**Definir valores do dicionário**

Para modificar um campo de assinatura, atribua valores ao dicionário de bloqueio de campo ou ao dicionário de valor de propagação. Especificar valores de dicionário de bloqueio de campo de assinatura envolve especificar campos de documento PDF que estão bloqueados quando o campo de assinatura é assinado. (Esta seção discute como bloquear todos os campos.)

Os seguintes valores do dicionário de valor de propagação podem ser definidos:

* **Verificação de revisão**: Especifica se a verificação de revogação é executada quando uma assinatura é aplicada ao campo de assinatura.
* **Opções de certificado**: Atribui valores ao dicionário de valores de propagação de certificado. Antes de especificar as opções de certificado, é recomendável familiarizar-se com um dicionário de valor de propagação de certificado. (Consulte [Referência PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opções de compilação**: Atribui algoritmos de resumo usados para assinatura. Os valores válidos são SHA1, SHA256, SHA384, SHA512 e RIPEMD160.
* **Filtro**: Especifica o filtro usado com o campo de assinatura. Por exemplo, você pode usar o filtro Adobe.PPKLite. (Consulte [Referência PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opções de sinalizador**: Especifica os valores de sinalizador associados a este campo de assinatura. Um valor de 1 significa que um assinante deve usar apenas os valores especificados para a entrada. Um valor de 0 significa que outros valores são permitidos. Estas são as posições do Bit:

   * **1 (Filtro):** O manipulador de assinatura a ser usado para assinar o campo de assinatura
   * **2 (Subfiltro):** Uma matriz de nomes que indicam codificações aceitáveis a serem usadas ao assinar
   * **3 (V)**: O número mínimo de versão exigido do manipulador de assinatura a ser usado para assinar o campo de assinatura
   * **4 (Motivos):** Uma matriz de strings que especifica possíveis motivos para assinar um documento
   * **5 (PDFLegalWarnings):** Uma matriz de strings que especifica possíveis atestados legais

* **Certificados jurídicos**: Quando um documento é certificado, ele é verificado automaticamente para tipos específicos de conteúdo que podem tornar o conteúdo visível de um documento ambíguo ou enganoso. Por exemplo, uma anotação pode obscurecer o texto que é importante para entender o que está sendo certificado. O processo de varredura gera avisos que indicam a presença desse tipo de conteúdo. Também fornece uma explicação adicional do conteúdo que pode ter gerado avisos.
* **Permissões**: Especifica permissões que podem ser usadas em um documento PDF sem invalidar a assinatura.
* **Motivos**: Especifica os motivos pelos quais este documento deve ser assinado.
* **Carimbo de data/hora**: Especifica as opções de carimbo de data e hora. Você pode, por exemplo, definir o URL do servidor de carimbo de data/hora usado.
* **Versão**: Especifica o número mínimo da versão do manipulador de assinatura a ser usado para assinar o campo de assinatura.

**Modificar o campo de assinatura**

Depois de criar um cliente do Serviço de assinatura, recupere o documento PDF que contém o campo de assinatura a ser modificado e defina os valores do dicionário, instrua o Serviço de assinatura a modificar o campo de assinatura. O Serviço de assinatura retorna um documento PDF que contém o campo de assinatura modificado. O documento PDF original não é afetado.

**Salve o documento PDF como um arquivo PDF**

Salve o documento do PDF que contém o campo de assinatura modificado como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou Adobe Reader.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de assinatura](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[Assinar documentos do PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Modificar campos de assinatura usando a API Java {#modify-signature-fields-using-the-java-api}

Modifique um campo de assinatura usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como o adobe-assinaturas-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de assinatura

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `SignatureServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obtenha o documento PDF que contém o campo de assinatura para modificar

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF que contém o campo de assinatura a ser modificado usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Definir valores do dicionário

   * Crie um `PDFSignatureFieldProperties` usando seu construtor. A `PDFSignatureFieldProperties` O objeto armazena informações do dicionário de bloqueio do campo de assinatura e do dicionário do valor de propagação.
   * Crie um `PDFSeedValueOptionSpec` usando seu construtor. Esse objeto permite que você defina valores do dicionário de valores de propagação.
   * Não permitir alterações ao documento do PDF chamando a `PDFSeedValueOptionSpec` do objeto `setMdpValue` e a aprovação do `MDPPermissions.NoChanges` valor de enumeração.
   * Crie um `FieldMDPOptionSpec` usando seu construtor. Esse objeto permite que você defina valores do dicionário de bloqueio do campo de assinatura.
   * Bloquear todos os campos no documento PDF chamando a `FieldMDPOptionSpec` do objeto `setMdpValue` e a aprovação do `FieldMDPAction.ALL` valor de enumeração.
   * Defina as informações do dicionário do valor de propagação chamando o `PDFSignatureFieldProperties` do objeto `setSeedValue` e a aprovação do `PDFSeedValueOptionSpec` objeto.
   * Defina as informações do dicionário de bloqueio do campo de assinatura chamando o `PDFSignatureFieldProperties`do objeto `setFieldMDP` e a aprovação do `FieldMDPOptionSpec` objeto.

   >[!NOTE]
   >
   >Para ver todos os valores do dicionário do valor de propagação que você pode definir, consulte `PDFSeedValueOptionSpec` referência de classe. (Consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. Modificar o campo de assinatura

   Modifique o campo de assinatura chamando o `SignatureServiceClient` do objeto `modifySignatureField` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que armazena o documento PDF que contém o campo de assinatura a ser modificado
   * Um valor de string que especifica o nome do campo de assinatura
   * O `PDFSignatureFieldProperties` objeto que armazena o dicionário de bloqueio de campo de assinatura e as informações do dicionário de valor de propagação

   O `modifySignatureField` método retorna um `com.adobe.idp.Document` objeto que armazena um documento PDF que contém o campo de assinatura modificado.

1. Salve o documento PDF como um arquivo PDF

   * Crie um `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` ao arquivo. Certifique-se de usar a variável `com.adobe.idp.Document` que a variável `modifySignatureField` método retornado.

### Modificar campos de assinatura usando a API do serviço da Web {#modify-signature-fields-using-the-web-service-api}

Modifique um campo de assinatura usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Criar um cliente de assinatura

   * Crie um `SignatureServiceClient` usando seu construtor padrão.
   * Crie um `SignatureServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `SignatureServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF que contém o campo de assinatura para modificar

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento PDF que contém o campo de assinatura a ser modificado.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` propriedade do conteúdo da matriz de bytes.

1. Definir valores do dicionário

   * Crie um `PDFSignatureFieldProperties` usando seu construtor. Esse objeto armazena informações do dicionário de bloqueio de campo de assinatura e do dicionário do valor de propagação.
   * Crie um `PDFSeedValueOptionSpec` usando seu construtor. Esse objeto permite que você defina valores do dicionário de valores de propagação.
   * Não permitir alterações ao documento do PDF atribuindo a variável `MDPPermissions.NoChanges` valor de enumeração para a `PDFSeedValueOptionSpec` do objeto `mdpValue` membro de dados.
   * Crie um `FieldMDPOptionSpec` usando seu construtor. Esse objeto permite que você defina valores do dicionário de bloqueio do campo de assinatura.
   * Bloquear todos os campos no documento PDF atribuindo a variável `FieldMDPAction.ALL` valor de enumeração para a `FieldMDPOptionSpec` do objeto `mdpValue` membro de dados.
   * Defina as informações do dicionário do valor de propagação atribuindo a variável `PDFSeedValueOptionSpec` para `PDFSignatureFieldProperties` do objeto `seedValue` membro de dados.
   * Defina as informações do dicionário de bloqueio do campo de assinatura atribuindo `FieldMDPOptionSpec` para `PDFSignatureFieldProperties` do objeto `fieldMDP` membro de dados.

   >[!NOTE]
   >
   >Para ver todos os valores do dicionário do valor de propagação que você pode definir, consulte `PDFSeedValueOptionSpec` referência de classe. (Consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. Modificar o campo de assinatura

   Modifique o campo de assinatura chamando o `SignatureServiceClient` do objeto `modifySignatureField` e transmitindo os seguintes valores:

   * O `BLOB` objeto que armazena o documento PDF que contém o campo de assinatura a ser modificado
   * Um valor de string que especifica o nome do campo de assinatura
   * O `PDFSignatureFieldProperties` objeto que armazena o dicionário de bloqueio de campo de assinatura e as informações do dicionário de valor de propagação

   O `modifySignatureField` método retorna um `BLOB` objeto que armazena um documento PDF que contém o campo de assinatura modificado.

1. Salve o documento PDF como um arquivo PDF

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF que conterá o campo de assinatura e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` que a variável `addSignatureField` retorna o método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Assinar documentos do PDF digitalmente {#digitally-signing-pdf-documents}

Assinaturas digitais podem ser aplicadas a documentos PDF para fornecer um nível de segurança. Assinaturas digitais, como assinaturas manuscritas, fornecem um meio pelo qual os signatários se identificam e fazem declarações sobre um documento. A tecnologia usada para assinar digitalmente documentos ajuda a garantir que tanto o assinante quanto os destinatários sejam claros sobre o que foi assinado e confiantes de que o documento não foi alterado desde que foi assinado.

Os documentos de PDF são assinados por meio de tecnologia de chave pública. Um assinante tem duas chaves: uma chave pública e uma chave privada. A chave privada é armazenada em uma credencial do usuário que deve estar disponível no momento da assinatura. A chave pública é armazenada no certificado do usuário que deve estar disponível para os recipients validarem a assinatura. Informações sobre certificados revogados são encontradas nas listas de revogação de certificados (CRLs) e nas respostas do Protocolo de Status de Certificado Online (OCSP) distribuídas pelas Autoridades de Certificados (CAs). O horário da assinatura pode ser obtido de uma fonte confiável conhecida como Autoridade de carimbo de data e hora.

>[!NOTE]
>
>Antes de poder assinar digitalmente um documento PDF, você deve garantir que adiciona o certificado ao AEM Forms. Um certificado é adicionado usando o console de administração ou de forma programática usando a API do Gerenciador de Confiança. (Consulte [Importando credenciais usando a API do Gerenciador de Confiança](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Você pode assinar digitalmente documentos PDF. Ao assinar digitalmente um documento PDF, você deve fazer referência a uma credencial de segurança que existe no AEM Forms. A credencial é a chave privada usada para assinatura.

O serviço de assinatura executa as seguintes etapas quando um documento PDF é assinado:

1. O serviço de assinatura recupera a credencial do Truststore ao passar o alias especificado na solicitação.
1. A Truststore pesquisa a credencial especificada.
1. A credencial é retornada ao Serviço de assinatura e é usada para assinar o documento. A credencial também é armazenada em cache no alias para solicitações futuras.

Para obter informações sobre como lidar com a credencial de segurança, consulte o *Instalação e implantação do AEM Forms* guia para o servidor de aplicativos.

>[!NOTE]
>
>Há diferenças entre documentos de assinatura e de certificação. (Consulte [Certificando documentos de PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>Nem todos os documentos PDF suportam assinatura. Para obter mais informações sobre o serviço de assinatura e a assinatura digital de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>O serviço de assinatura não oferece suporte a arquivos XDP com dados PDF incorporados como entrada para uma operação, como a certificação de um documento. Esta ação resulta no serviço de assinatura lançar um `PDFOperationException`. Para resolver esse problema, converta o arquivo XDP em um arquivo PDF usando o serviço Utilitários do PDF e passe o arquivo PDF convertido para uma operação de serviço de assinatura. (Consulte [Trabalhar com utilitários PDF](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**Credencial do HSM nShield do Cifrador**

Ao usar uma credencial HSM do nShield do Cifrador para assinar ou certificar um documento do PDF, a nova credencial não poderá ser usada até que o servidor de aplicativos J2EE no qual o AEM Forms é implantado seja reiniciado. No entanto, você pode definir um valor de configuração, resultando na operação de assinatura ou certificação funcionando sem reiniciar o servidor de aplicativos J2EE.

Você pode adicionar o seguinte valor de configuração no arquivo cknfastrc, que está localizado em /opt/nfast/cknfastrc (ou c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Após adicionar esse valor de configuração ao arquivo cknfastrc, a nova credencial poderá ser usada sem reiniciar o servidor de aplicativos J2EE.

**Assinatura não confiável**

Ao certificar e assinar o mesmo documento PDF, se a assinatura de certificação não for confiável, um triângulo amarelo será exibido contra a primeira assinatura ao abrir o documento PDF no Acrobat ou Adobe Reader. A assinatura de certificação deve ser confiável para evitar essa situação.

**Assinar documentos que são formulários baseados em XFA**

Se você tentar assinar um formulário baseado em XFA usando a API do serviço de assinatura, os dados podem estar ausentes no `View` `Signed` `Version` localizada em Acrobat. Por exemplo, considere o seguinte workflow:

* Usando um arquivo XDP criado usando o Designer, você mescla um design de formulário que contém um campo de assinatura e dados XML que contêm dados de formulário. Use o serviço Forms para gerar um documento PDF interativo.
* Você assina o documento do PDF usando a API do serviço de assinatura.

### Resumo das etapas {#summary_of_steps-3}

Para assinar digitalmente um documento PDF, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Criar um cliente do Serviço de assinatura.
1. Obtenha o documento PDF para assinar.
1. Assine o documento PDF.
1. Salve o documento PDF assinado como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

**Criar um cliente de Assinaturas**

Antes de poder executar programaticamente uma operação de serviço de assinatura, é necessário criar um cliente de serviço de assinatura.

**Obter o documento do PDF para assinar**

Para assinar um documento PDF, você deve obter um documento PDF que contenha um campo de assinatura. Se um documento PDF não contiver um campo de assinatura, ele não poderá ser assinado. Um campo de assinatura pode ser adicionado usando o Designer ou de forma programática.

**Assinar o documento de PDF**

Ao assinar um documento do PDF, você pode definir opções de tempo de execução usadas pelo serviço de assinatura. Você pode definir as seguintes opções:

* Opções de aparência
* Verificação de revogação
* Valores de carimbo de data e hora

Você define as opções de aparência usando um `PDFSignatureAppearanceOptionSpec` objeto. Por exemplo, você pode exibir a data dentro de uma assinatura chamando a variável `PDFSignatureAppearanceOptionSpec` do objeto `setShowDate` método e aprovação `true`.

Você também pode especificar se deve executar ou não uma verificação de revogação que determina se o certificado usado para assinar digitalmente um documento PDF foi revogado. Para executar a verificação de revogação, é possível especificar um dos seguintes valores:

* **NoCheck**: Não executar verificação de revogação.
* **MelhorEsforço**: Sempre tente verificar a revogação de todos os certificados na cadeia. Se ocorrer algum problema na verificação, a revogação é considerada válida. Se ocorrer alguma falha, suponha que o certificado não seja revogado.
* **CheckIfAvailable:** Verifique a revogação de todos os certificados da cadeia se houver informações de revogação disponíveis. Se ocorrer algum problema na verificação, a revogação será considerada inválida. Se ocorrer alguma falha, suponha que o certificado seja revogado e inválido. (Este é o valor padrão.)
* **SempreVerificar**: Verifique a revogação de todos os certificados na cadeia. Se as informações de revogação não estiverem presentes em nenhum certificado, presume-se que a revogação é inválida.

Para executar a verificação de revogação em um certificado, você pode especificar um URL para um servidor de lista de revogação de certificado (CRL) usando um `CRLOptionSpec` objeto. No entanto, se você quiser executar a verificação de revogação e não especificar um URL para um servidor CRL, o Serviço de assinatura obterá o URL do certificado.

Em vez de usar um servidor CRL, você pode usar um servidor OCSP (protocolo de status de certificado) online ao executar a verificação de revogação. Normalmente, ao usar um servidor OCSP em vez de um servidor CRL, a verificação de revogação é executada mais rápido. (Consulte &quot;Protocolo de status de certificado online&quot; em [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

Você pode definir a ordem de servidor CRL e OCSP que o serviço de assinatura usa usando Aplicativos e Serviços do Adobe. Por exemplo, se o servidor OCSP estiver definido primeiro em Aplicativos e Serviços do Adobe, o servidor OCSP será verificado, seguido pelo servidor CRL. (Consulte &quot;Gerenciando certificados e credenciais usando o Armazenamento de confiança&quot; na Ajuda do AAC).

Se você especificar não executar a verificação de revogação, o serviço de assinatura não verificará se o certificado usado para assinar ou certificar um documento foi revogado. Ou seja, as informações do CRL e do servidor OCSP são ignoradas.

>[!NOTE]
>
>Embora uma CRL ou um servidor OCSP possa ser especificado no certificado, você pode substituir a URL especificada no certificado usando um `CRLOptionSpec` e um `OCSPOptionSpec` objeto. Por exemplo, para substituir o servidor CRL, você pode chamar a variável `CRLOptionSpec` do objeto `setLocalURI` método .

O carimbo de data e hora refere-se ao processo de rastreamento da hora em que um documento assinado ou certificado foi modificado. Depois que um documento é assinado, ele não deve ser modificado, mesmo pelo proprietário do documento. O carimbo de data e hora ajuda a impor a validade de um documento assinado ou certificado. É possível definir opções de carimbo de data e hora usando uma `TSPOptionSpec` objeto. Por exemplo, você pode especificar o URL de um servidor de provedor de carimbo de data e hora (TSP).

>[!NOTE]
>
>No Java e no serviço da Web, percorra as seções e os início rápidos correspondentes, a verificação de revogação é usada. Como nenhuma informação do servidor CRL ou OCSP é especificada, as informações do servidor são obtidas do certificado usado para assinar digitalmente o documento PDF.

Para assinar com êxito um documento PDF, você pode especificar o nome totalmente qualificado do campo de assinatura que conterá a assinatura digital, como `form1[0].#subform[1].SignatureField3[3]`. Ao usar um campo de formulário XFA, o nome parcial do campo de assinatura também pode ser usado: `SignatureField3[3]`.

Você também deve referenciar uma credencial de segurança para assinar digitalmente um documento PDF. Para fazer referência a uma credencial de segurança, especifique um alias. O alias é uma referência a uma credencial real que pode estar em um arquivo PKCS#12 (com uma extensão .pfx) ou em um módulo de segurança de hardware (HSM). Para obter informações sobre a credencial de segurança, consulte o *Instalação e implantação do AEM Forms* guia para o servidor de aplicativos.

**Salve o documento PDF assinado**

Depois que o serviço de assinatura assinar digitalmente o documento PDF, você poderá salvá-lo como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou Adobe Reader.

**Consulte também**

[Assine digitalmente documentos do PDF usando a API Java](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Assinar documentos do PDF digitalmente usando a API do serviço da Web](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields)

[Recuperando nomes de campos de assinatura](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Assine digitalmente documentos do PDF usando a API Java {#digitally-sign-pdf-documents-using-the-java-api}

Assine digitalmente um documento do PDF usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-assinaturas-client.jar, no classpath do seu projeto Java.

1. Criar um cliente de Assinaturas

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `SignatureServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obter o documento do PDF para assinar

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF para assinar digitalmente usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Assinar o documento de PDF

   Assine o documento PDF chamando o `SignatureServiceClient` do objeto `sign` e transmitindo os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o documento PDF a ser assinado.
   * Um valor de string que representa o nome do campo de assinatura que conterá a assinatura digital.
   * A `Credential` objeto que representa a credencial usada para assinar digitalmente o documento PDF. Crie um `Credential` chamando o `Credential` estático do objeto `getInstance` e transmitindo um valor de string que especifica o valor do alias que corresponde à credencial de segurança.
   * A `HashAlgorithm` objeto que especifica um membro de dados estáticos que representa o algoritmo de hash a ser usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi assinado digitalmente.
   * Um valor de string que representa as informações de contato do assinante.
   * A `PDFSignatureAppearanceOptions` objeto que controla a aparência da assinatura digital. Por exemplo, você pode usar esse objeto para adicionar um logotipo personalizado a uma assinatura digital.
   * A `java.lang.Boolean` objeto que especifica se a verificação de revogação deve ser realizada no certificado do assinante.
   * Um `OCSPOptionSpec` objeto que armazena preferências para suporte ao Protocolo de status de certificado online (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * A `CRLPreferences` objeto que armazena as preferências da lista de revogação de certificado (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * A `TSPPreferences` objeto que armazena preferências para suporte ao provedor de carimbo de data/hora (TSP). Esse parâmetro é opcional e pode ser `null`. Para obter mais informações, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   O `sign` método retorna um `com.adobe.idp.Document` objeto que representa o documento PDF assinado.

1. Salve o documento PDF assinado

   * Crie um `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método e pass `java.io.File`para copiar o conteúdo da `Document` ao arquivo. Certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `sign` método .

**Consulte também**

[Assinar documentos do PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Início rápido (modo SOAP): Assinando digitalmente um documento do PDF usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Assinar documentos do PDF digitalmente usando a API do serviço da Web {#digitally-signing-pdf-documents-using-the-web-service-api}

Para assinar digitalmente um documento do PDF usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Criar um cliente de Assinaturas

   * Crie um `SignatureServiceClient` usando seu construtor padrão.
   * Crie um `SignatureServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `SignatureServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obter o documento do PDF para assinar

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF assinado.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento do PDF a ser assinado e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` propriedade do conteúdo da matriz de bytes.

1. Assinar o documento de PDF

   Assine o documento PDF chamando o `SignatureServiceClient` do objeto `sign` e transmitindo os seguintes valores:

   * A `BLOB` objeto que representa o documento PDF a ser assinado.
   * Um valor de string que representa o nome do campo de assinatura que conterá a assinatura digital.
   * A `Credential` objeto que representa a credencial usada para assinar digitalmente o documento PDF. Crie um `Credential` ao usar seu construtor e especificar o alias, atribuindo um valor à variável `Credential` do objeto `alias` propriedade.
   * A `HashAlgorithm` objeto que especifica um membro de dados estáticos que representa o algoritmo de hash a ser usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor booleano que especifica se o algoritmo de hash é usado.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi assinado digitalmente.
   * Um valor de string que representa a localização do assinante.
   * Um valor de string que representa as informações de contato do assinante.
   * A `PDFSignatureAppearanceOptions` objeto que controla a aparência da assinatura digital. Por exemplo, você pode usar esse objeto para adicionar um logotipo personalizado a uma assinatura digital.
   * A `System.Boolean` objeto que especifica se a verificação de revogação deve ser realizada no certificado do assinante. Se essa verificação de revogação for feita, ela será incorporada na assinatura. O padrão é `false`.
   * Um `OCSPOptionSpec` objeto que armazena preferências para suporte ao Protocolo de status de certificado online (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`. Para obter informações sobre esse objeto, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` objeto que armazena as preferências da lista de revogação de certificado (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * A `TSPPreferences` objeto que armazena preferências para suporte ao provedor de carimbo de data/hora (TSP). Esse parâmetro é opcional e pode ser `null`.

   O `sign` método retorna um `BLOB` objeto que representa o documento PDF assinado.

1. Salve o documento PDF assinado

   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento de PDF assinado e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto retornado pelo `sign` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Assinar documentos do PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Assinatura digital - Forms interativo {#digitally-signing-interactive-forms}

Você pode assinar um formulário interativo criado pelo serviço Forms. Por exemplo, considere o seguinte workflow:

* É possível mesclar um formulário PDF baseado em XFA criado usando o Designer e dados de formulário localizados em um documento XML usando o serviço Forms. O servidor do Forms renderiza um formulário interativo.
* Você assina o formulário interativo usando a API do serviço de assinatura.

O resultado é um formulário PDF interativo assinado digitalmente. Ao assinar um formulário PDF baseado em um formulário XFA, salve o arquivo PDF como um formulário PDF Adobe. Se você tentar assinar um formulário PDF que é salvo como um formulário Adobe Dynamic PDF, ocorrerá uma exceção. Como você está assinando o formulário retornado do serviço Forms, verifique se ele contém um campo de assinatura.

>[!NOTE]
>
>Antes de assinar digitalmente um formulário interativo, adicione o certificado à AEM Forms. Um certificado é adicionado usando o console de administração ou de forma programática usando a API do Gerenciador de Confiança. (Consulte [Importando credenciais usando a API do Gerenciador de Confiança](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Ao usar a API do serviço do Forms, defina a variável `GenerateServerAppearance` opção de tempo de execução para `true`. Essa opção de tempo de execução garante que a aparência do formulário gerado no servidor permaneça válida quando aberto no Acrobat ou Adobe Reader. É recomendável definir essa opção de tempo de execução ao gerar um formulário interativo para assinar usando a API do Forms.

>[!NOTE]
>
>Antes de ler Digitalmente Signing Interative Forms, recomenda-se que você esteja familiarizado com a assinatura de documentos PDF. (Consulte [Assinar documentos do PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### Resumo das etapas {#summary_of_steps-4}

Para assinar digitalmente um formulário interativo retornado pelo serviço Forms, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Forms e Assinaturas.
1. Obtenha o formulário interativo usando o serviço Forms.
1. Assine o formulário interativo.
1. Salve o documento PDF assinado como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente Forms e Assinaturas**

Como esse fluxo de trabalho chama os serviços Forms e Signature, crie um cliente de serviço Forms e um cliente de serviço Signature.

**Obter o formulário interativo usando o serviço Forms**

Você pode usar o serviço Forms para obter o formulário PDF interativo para assinar. A partir do AEM Forms, você pode enviar uma `com.adobe.idp.Document` ao serviço Forms que contém o formulário a ser renderizado. O nome deste método é `renderPDFForm2`. Esse método retorna um `com.adobe.idp.Document` objeto que contém o formulário a ser assinado. Você pode passar isso `com.adobe.idp.Document` para o serviço de assinatura.

Da mesma forma, se você estiver usando serviços da Web, poderá passar a variável `BLOB` instância que o serviço Forms retorna ao serviço de assinatura.

>[!NOTE]
>
>A seção Início rápido associado à Assinatura digital do Forms interativo chama o `renderPDFForm2` método .

**Assinar o formulário interativo**

Ao assinar um documento PDF, você pode definir opções de tempo de execução que o serviço de assinatura usa. Você pode definir as seguintes opções:

* Opções de aparência
* Verificação de revogação
* Valores de carimbo de data e hora

Você define as opções de aparência usando um `PDFSignatureAppearanceOptionSpec` objeto. Por exemplo, você pode exibir a data dentro de uma assinatura chamando a variável `PDFSignatureAppearanceOptionSpec` do objeto `setShowDate` método e aprovação `true`.

**Salve o documento PDF assinado**

Depois que o serviço de assinatura assinar digitalmente o documento PDF, você poderá salvá-lo como um arquivo PDF. O arquivo PDF pode ser aberto no Acrobat ou Adobe Reader.

**Consulte também**

[Assine um formulário interativo digitalmente usando a API Java](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Assinar um formulário interativo digitalmente usando a API do serviço da Web](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assinar documentos do PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Assine um formulário interativo digitalmente usando a API Java {#digitally-sign-an-interactive-form-using-the-java-api}

Assine um formulário interativo digitalmente usando a Forms e a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-assinaturas-client.jar e adobe-forms-client.jar, no classpath do seu projeto Java.

1. Criar um cliente Forms e Assinaturas

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `SignatureServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.
   * Crie um `FormsServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obter o formulário interativo usando o serviço Forms

   * Crie um `java.io.FileInputStream` objeto que representa o documento do PDF a ser transmitido ao serviço Forms usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.
   * Crie um `java.io.FileInputStream` objeto que representa o documento XML que contém dados de formulário a serem passados para o serviço Forms usando seu construtor. Passe um valor de string que especifica o local do arquivo XML.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.
   * Crie um `PDFFormRenderSpec` objeto usado para definir opções de tempo de execução. Chame o `PDFFormRenderSpec` do objeto `setGenerateServerAppearance` método e pass `true`.
   * Chame o `FormsServiceClient` do objeto `renderPDFForm2` e transmita os seguintes valores:

      * A `com.adobe.idp.Document` objeto que contém o formulário PDF para renderizar.
      * A `com.adobe.idp.Document` objeto que contém dados para mesclar com o formulário.
      * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução.
      * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms. Você pode especificar `null` para esse valor de parâmetro.
      * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

      O `renderPDFForm2` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário

   * Recupere o formulário PDF chamando o `FormsResult` do objeto `getOutputContent` método . Esse método retorna um `com.adobe.idp.Document` objeto que representa o formulário interativo.


1. Assinar o formulário interativo

   Assine o documento PDF chamando o `SignatureServiceClient` do objeto `sign` e transmitindo os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o documento PDF a ser assinado. Certifique-se de que esse objeto seja o `com.adobe.idp.Document` objeto obtido do serviço Forms.
   * Um valor de string que representa o nome do campo de assinatura assinado.
   * A `Credential` objeto que representa a credencial usada para assinar digitalmente o documento PDF. Crie um `Credential` chamando o `Credential` estático do objeto `getInstance` método . Passe um valor de string que especifica o valor do alias que corresponde à credencial de segurança.
   * A `HashAlgorithm` objeto que especifica um membro de dados estáticos que representa o algoritmo de hash a ser usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi assinado digitalmente.
   * Um valor de string que representa as informações de contato do assinante.
   * A `PDFSignatureAppearanceOptions` objeto que controla a aparência da assinatura digital. Por exemplo, você pode usar esse objeto para adicionar um logotipo personalizado a uma assinatura digital.
   * A `java.lang.Boolean` objeto que especifica se a verificação de revogação deve ser realizada no certificado do assinante.
   * Um `OCSPPreferences` objeto que armazena preferências para suporte ao Protocolo de status de certificado online (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * A `CRLPreferences` objeto que armazena as preferências da lista de revogação de certificado (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * A `TSPPreferences` objeto que armazena preferências para suporte ao provedor de carimbo de data/hora (TSP). Esse parâmetro é opcional e pode ser `null`.

   O `sign` método retorna um `com.adobe.idp.Document` objeto que representa o documento PDF assinado.

1. Salve o documento PDF assinado

   * Crie um `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método e pass `java.io.File`para copiar o conteúdo da `Document` ao arquivo. Certifique-se de usar a variável `com.adobe.idp.Document` que a variável `sign` método retornado.

**Consulte também**

[Assinatura digital - Forms interativo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Início rápido (modo SOAP): Assinando digitalmente um documento do PDF usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Assinar um formulário interativo digitalmente usando a API do serviço da Web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Assine um formulário interativo digitalmente usando a Forms e a Signature API (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Como esse aplicativo cliente chama dois serviços AEM Forms, crie duas referências de serviço. Use a seguinte definição WSDL para a referência de serviço associada ao serviço de assinatura: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Use a seguinte definição de WSDL para a referência de serviço associada ao serviço do Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Porque a variável `BLOB` o tipo de dados é comum a ambas as referências de serviço, qualifica totalmente a variável `BLOB` tipo de dados ao usá-lo. Na inicialização rápida do serviço da Web correspondente, todas as `BLOB` as instâncias são totalmente qualificadas.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Criar um cliente Forms e Assinaturas

   * Crie um `SignatureServiceClient` usando seu construtor padrão.
   * Crie um `SignatureServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `SignatureServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita essas etapas para o cliente de serviço do Forms.

1. Obter o formulário interativo usando o serviço Forms

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF assinado.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento do PDF a ser assinado e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` propriedade do conteúdo da matriz de bytes.
   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar dados de formulário.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo XML que contém os dados do formulário e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` propriedade do conteúdo da matriz de bytes.
   * Crie um `PDFFormRenderSpec` objeto usado para definir opções de tempo de execução. Atribua o valor `true` para `PDFFormRenderSpec` do objeto `generateServerAppearance` campo.
   * Chame o `FormsServiceClient` do objeto `renderPDFForm2` e transmita os seguintes valores:

      * A `BLOB` objeto que contém o formulário PDF para renderizar.
      * A `BLOB` objeto que contém dados para mesclar com o formulário.
      * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução.
      * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms. Você pode especificar `null` para esse valor de parâmetro.
      * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
      * Um parâmetro de saída longo usado para armazenar o número de páginas no formulário.
      * Um parâmetro de saída da string usado para o valor da localidade.
      * A `FormResult` que é um parâmetro de saída usado para armazenar o formulário interativo.
   * Para recuperar o formulário PDF, chame o `FormsResult` do objeto `outputContent` campo. Esse campo armazena um `BLOB` objeto que representa o formulário interativo.


1. Assinar o formulário interativo

   Assine o documento PDF chamando o `SignatureServiceClient` do objeto `sign` e transmitindo os seguintes valores:

   * A `BLOB` objeto que representa o documento PDF a ser assinado. Use o `BLOB` instância retornada pelo serviço Forms.
   * Um valor de string que representa o nome do campo de assinatura assinado.
   * A `Credential` objeto que representa a credencial usada para assinar digitalmente o documento PDF. Crie um `Credential` ao usar seu construtor e especificar o alias, atribuindo um valor à variável `Credential` do objeto `alias` propriedade.
   * A `HashAlgorithm` objeto que especifica um membro de dados estáticos que representa o algoritmo de hash a ser usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor booleano que especifica se o algoritmo de hash é usado.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi assinado digitalmente.
   * Um valor de string que representa a localização do assinante.
   * Um valor de string que representa as informações de contato do assinante.
   * A `PDFSignatureAppearanceOptions` objeto que controla a aparência da assinatura digital. Por exemplo, você pode usar esse objeto para adicionar um logotipo personalizado a uma assinatura digital.
   * A `System.Boolean` objeto que especifica se a verificação de revogação deve ser realizada no certificado do assinante. Se essa verificação de revogação for feita, ela será incorporada na assinatura. O padrão é `false`.
   * Um `OCSPPreferences` objeto que armazena preferências para suporte ao Protocolo de status de certificado online (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`. Para obter informações sobre esse objeto, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` objeto que armazena as preferências da lista de revogação de certificado (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * A `TSPPreferences` objeto que armazena preferências para suporte ao provedor de carimbo de data/hora (TSP). Esse parâmetro é opcional e pode ser `null`.

   O `sign` método retorna um `BLOB` objeto que representa o documento PDF assinado.

1. Salve o documento PDF assinado

   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento de PDF assinado e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto retornado pelo `sign` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Assinatura digital - Forms interativo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certificando documentos de PDF {#certifying-pdf-documents}

Você pode proteger um documento PDF certificando-o com um tipo específico de assinatura chamada assinatura certificada. Uma assinatura certificada é distinguida de uma assinatura digital destas maneiras:

* Deve ser a primeira assinatura aplicada ao documento PDF; ou seja, no momento em que a assinatura certificada é aplicada, qualquer outro campo de assinatura no documento deve ser cancelado. Apenas uma assinatura certificada é permitida em um documento PDF. Se quiser assinar e certificar um documento do PDF, certifique-o antes de assiná-lo. Depois de certificar um documento PDF, você pode assinar digitalmente campos de assinatura adicionais.
* O autor ou o originador do documento pode especificar que o documento pode ser modificado de determinadas maneiras sem invalidar a assinatura certificada. Por exemplo, o documento pode permitir o preenchimento de formulários ou comentários. Se o autor especificar que uma determinada modificação não é permitida, o Acrobat impedirá que os usuários modifiquem o documento dessa maneira. Se tais modificações forem feitas, como usando outro aplicativo, a assinatura certificada será inválida e o Acrobat emitirá um aviso quando um usuário abrir o documento. (Com assinaturas não certificadas, as modificações não são impedidas e as operações normais de edição não invalidam a assinatura original.)
* No momento da assinatura, o documento é examinado quanto a tipos específicos de conteúdo que podem tornar o conteúdo de um documento ambíguo ou enganoso. Por exemplo, uma anotação pode obscurecer algum texto em uma página que seja importante para entender o que está sendo certificado. Pode ser fornecida uma explicação (atestado jurídico) sobre esse conteúdo.

Você pode certificar documentos do PDF por programação usando a API Java do serviço de assinatura ou a API do serviço da Web de assinatura. Ao certificar um documento do PDF, você deve fazer referência a uma credencial de segurança que existe no serviço de Credencial. Para obter informações sobre a credencial de segurança, consulte o *Instalação e implantação do AEM Forms* guia para o servidor de aplicativos.

>[!NOTE]
>
>Ao certificar e assinar o mesmo documento PDF, se a assinatura de certificação não for confiável, um triângulo amarelo será exibido ao lado da primeira assinatura quando você abrir o documento PDF no Acrobat ou Adobe Reader. A assinatura de certificação deve ser confiável para evitar essa situação.

>[!NOTE]
>
>Ao usar uma credencial HSM do nShield do Cifrador para assinar ou certificar um documento do PDF, a nova credencial não poderá ser usada até que o servidor de aplicativos J2EE no qual o AEM Forms é implantado seja reiniciado. No entanto, você pode definir um valor de configuração, resultando na operação de assinatura ou certificação funcionando sem reiniciar o servidor de aplicativos J2EE.

Você pode adicionar o seguinte valor de configuração no arquivo cknfastrc, que está localizado em /opt/nfast/cknfastrc (ou c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Após adicionar esse valor de configuração ao arquivo cknfastrc, a nova credencial poderá ser usada sem reiniciar o servidor de aplicativos J2EE.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura e certificar um documento, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-5}

Para certificar um documento PDF, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF para certificar.
1. Certifique o documento PDF.
1. Salve o documento do PDF certificado como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de poder executar uma operação de Assinatura por programação, você deve criar um cliente de Assinatura.

**Obtenha o documento do PDF para certificar**

Para certificar um documento PDF, você deve obter um documento PDF que contenha um campo de assinatura. Se um documento PDF não contiver um campo de assinatura, ele não poderá ser certificado. Um campo de assinatura pode ser adicionado usando o Designer ou de forma programática. Para obter informações sobre como adicionar um campo de assinatura por programação, consulte [Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields).

**Certificar o documento de PDF**

Para certificar um documento do PDF com êxito, você precisa dos seguintes valores de entrada usados pelo Serviço de assinatura para certificar um documento do PDF:

* **documento PDF**: Um documento PDF que contém um campo de assinatura, que é um campo de formulário que contém uma representação gráfica da assinatura certificada. Um documento PDF deve conter um campo de assinatura antes de poder ser certificado. Um campo de assinatura pode ser adicionado usando o Designer ou de forma programática. (Consulte [Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **Nome do campo de assinatura**: O nome totalmente qualificado do campo de assinatura certificado. O seguinte valor é um exemplo: `form1[0].#subform[1].SignatureField3[3]`. Ao usar um campo de formulário XFA, o nome parcial do campo de assinatura também pode ser usado: `SignatureField3[3]`. Se um valor nulo for passado para o nome do campo, um campo de assinatura invisível será criado e certificado dinamicamente.
* **Credencial de segurança**: Uma credencial usada para certificar o documento PDF. Esta credencial de segurança contém uma senha e um alias, que devem corresponder a um alias que aparece na credencial localizada no serviço de Credencial. O alias é uma referência a uma credencial real que pode estar em um arquivo PKCS#12 (com uma extensão .pfx) ou em um módulo de segurança de hardware (HSM).
* **Algoritmo de hash**: Um algoritmo de hash a ser usado para compilar o documento PDF.
* **Motivo da assinatura**: Um valor exibido no Acrobat ou Adobe Reader para que outros usuários saibam o motivo pelo qual o documento PDF foi certificado.
* **Localização do signatário**: O local do assinante especificado pela credencial.
* **Informações de contato**: Informações de contato, como endereço e número de telefone, do assinante.
* **Informações de permissão**: Permissões que controlam as ações que um usuário final pode executar em um documento sem fazer com que a assinatura certificada seja inválida. Por exemplo, você pode definir a permissão para que qualquer alteração no documento PDF faça com que a assinatura certificada seja inválida.
* **Explicação jurídica**: Quando um documento é certificado, ele é verificado automaticamente para tipos específicos de conteúdo que podem tornar o conteúdo de um documento ambíguo ou enganoso. Por exemplo, uma anotação pode obscurecer algum texto em uma página que seja importante para entender o que está sendo certificado. O processo de varredura gera avisos sobre esses tipos de conteúdo. Esse valor fornece uma explicação adicional do conteúdo que pode ter gerado avisos.
* **Opções de aparência**: Opções que controlam a aparência da assinatura certificada. Por exemplo, a assinatura certificada pode exibir informações de data.
* **Verificação de revogação**: Este valor especifica se a verificação de revogação é feita para o certificado do assinante. A configuração padrão de `false` significa que a verificação de revogação não é efetuada.
* **Configurações do OCSP**: Configurações para suporte ao Protocolo de Status de Certificado Online (OCSP), que fornece informações sobre o status da credencial usada para certificar o documento do PDF. Você pode, por exemplo, especificar o URL do servidor que fornece informações sobre a credencial que está usando para fazer logon no documento do PDF.
* **Configurações de CRL**: Configurações para as preferências da lista de revogação de certificado (CRL) se a verificação de revogação for feita. Por exemplo, você pode especificar sempre verificar se uma credencial foi revogada.
* **Carimbo de data e hora**: Configurações que definem informações de carimbo de data e hora aplicadas à assinatura certificada. Um carimbo de data/hora indica que dados específicos foram estabelecidos antes de um determinado período. Este conhecimento ajuda a construir uma relação de confiança entre o assinante e o verificador.

**Salve o documento do PDF certificado como um arquivo PDF**

Depois que o serviço de assinatura certifica o documento do PDF, você pode salvá-lo como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou Adobe Reader.

**Consulte também**

[Certificar documentos do PDF usando a API do Java](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certificar documentos do PDF usando a API do serviço da Web](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certificar documentos do PDF usando a API do Java {#certify-pdf-documents-using-the-java-api}

Certifique um documento do PDF usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-assinaturas-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de assinatura

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `SignatureServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obtenha o documento do PDF para certificar

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF a ser certificado usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Certificar o documento de PDF

   Certifique o documento do PDF chamando o `SignatureServiceClient` do objeto `certify` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que representa o documento PDF a ser certificado.
   * Um valor de string que representa o nome do campo de assinatura que conterá a assinatura.
   * A `Credential` que representa a credencial usada para certificar o documento PDF. Crie um `Credential` chamando o `Credential` estático do objeto `getInstance` e transmitindo um valor de string que especifica o valor do alias que corresponde à credencial de segurança.
   * A `HashAlgorithm` objeto que especifica um membro de dados estáticos que representa o algoritmo de hash usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi certificado.
   * Um valor de string que representa as informações de contato do assinante.
   * A `MDPPermissions` objeto que especifica ações que podem ser executadas no documento PDF que invalida a assinatura.
   * A `PDFSignatureAppearanceOptions` objeto que controla a aparência da assinatura certificada. Se desejar, modifique a aparência da assinatura chamando um método, como `setShowDate`.
   * Um valor de string que fornece uma explicação de quais ações invalidam a assinatura.
   * A `java.lang.Boolean` objeto que especifica se a verificação de revogação deve ser realizada no certificado do assinante. Se essa verificação de revogação for feita, ela será incorporada na assinatura. O padrão é `false`.
   * A `java.lang.Boolean` que especifica se o campo de assinatura que está sendo certificado está bloqueado. Se o campo estiver bloqueado, o campo de assinatura será marcado como somente leitura, suas propriedades não poderão ser modificadas e ele não poderá ser apagado por ninguém que não tenha as permissões necessárias. O padrão é `false`.
   * Um `OCSPPreferences` objeto que armazena preferências para suporte ao Protocolo de status de certificado online (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`. Para obter informações sobre esse objeto, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `CRLPreferences` objeto que armazena as preferências da lista de revogação de certificado (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * A `TSPPreferences` objeto que armazena preferências para suporte ao provedor de carimbo de data/hora (TSP). Por exemplo, depois de criar uma `TSPPreferences` , é possível definir o URL do servidor TSP chamando o `TSPPreferences` do objeto `setTspServerURL` método . Esse parâmetro é opcional e pode ser `null`. Para obter mais informações, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

   O `certify` método retorna um `com.adobe.idp.Document` que representa o documento PDF certificado.

1. Salve o documento do PDF certificado como um arquivo PDF

   * Crie um `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` ao arquivo.

**Consulte também**

[Certificando documentos de PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Início rápido (modo SOAP): Certificar um documento do PDF usando a API do Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certificar documentos do PDF usando a API do serviço da Web {#certify-pdf-documents-using-the-web-service-api}

Certifique um documento do PDF usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Criar um cliente de assinatura

   * Crie um `SignatureServiceClient` usando seu construtor padrão.
   * Crie um `SignatureServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `SignatureServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento do PDF para certificar

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF certificado.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento do PDF a ser certificado e o modo no qual abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` membro de dados o conteúdo da matriz de bytes.

1. Certificar o documento de PDF

   Certifique o documento do PDF chamando o `SignatureServiceClient` do objeto `certify` e transmitindo os seguintes valores:

   * O `BLOB` objeto que representa o documento PDF a ser certificado.
   * Um valor de string que representa o nome do campo de assinatura que conterá a assinatura.
   * A `Credential` que representa a credencial usada para certificar o documento PDF. Crie um `Credential` usando seu construtor e especifique o alias atribuindo um valor à variável `Credential` do objeto `alias` propriedade.
   * A `HashAlgorithm` objeto que especifica um membro de dados estáticos que representa o algoritmo de hash usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor booleano que especifica se o algoritmo de hash é usado.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi certificado.
   * Um valor de string que representa a localização do assinante.
   * Um valor de string que representa as informações de contato do assinante.
   * Um `MDPPermissions` membro de dados estáticos do objeto que especifica ações que podem ser executadas no documento PDF que invalidam a assinatura.
   * Um valor booleano que especifica se deve ser usada a variável `MDPPermissions` objeto que foi passado como valor de parâmetro anterior.
   * Um valor de string que explica quais ações invalidam a assinatura.
   * A `PDFSignatureAppearanceOptions` objeto que controla a aparência da assinatura certificada. Crie um `PDFSignatureAppearanceOptions` usando seu construtor. Você pode modificar a aparência da assinatura definindo um de seus membros de dados.
   * A `System.Boolean` objeto que especifica se a verificação de revogação deve ser realizada no certificado do assinante. Se essa verificação de revogação for feita, ela será incorporada na assinatura. O padrão é `false`.
   * A `System.Boolean` que especifica se o campo de assinatura que está sendo certificado está bloqueado. Se o campo estiver bloqueado, o campo de assinatura será marcado como somente leitura, suas propriedades não poderão ser modificadas e ele não poderá ser apagado por ninguém que não tenha as permissões necessárias. O padrão é `false`.
   * A `System.Boolean` que especifica se o campo de assinatura está bloqueado. Ou seja, se você passar `true` para o parâmetro anterior, em seguida, passe `true` para este parâmetro.
   * Um `OCSPPreferences` objeto que armazena preferências para suporte ao Protocolo de Status de Certificado Online (OCSP), que fornece informações sobre o status da credencial usada para certificar o documento do PDF. Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * A `CRLPreferences` objeto que armazena as preferências da lista de revogação de certificado (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * A `TSPPreferences` objeto que armazena preferências para suporte ao provedor de carimbo de data/hora (TSP). Por exemplo, depois de criar uma `TSPPreferences` , é possível definir o URL do TSP definindo a variável `TSPPreferences` do objeto `tspServerURL` membro de dados. Esse parâmetro é opcional e pode ser `null`.

   O `certify` método retorna um `BLOB` que representa o documento PDF certificado.

1. Salve o documento do PDF certificado como um arquivo PDF

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF que conterá o documento PDF certificado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto retornado pelo `certify` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `binaryData` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Certificando documentos de PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificação de assinaturas digitais {#verifying-digital-signatures}

Assinaturas digitais podem ser verificadas para garantir que um documento PDF assinado não foi modificado e que a assinatura digital é válida. Ao verificar uma assinatura digital, você pode verificar o status da assinatura e as propriedades da assinatura, como a identidade do assinante. Antes de confiar em uma assinatura digital, é recomendável verificá-la. Ao verificar uma assinatura digital, consulte um documento PDF que contenha uma assinatura digital.

Suponha que a identidade do assinante seja desconhecida. Ao abrir o documento PDF no Acrobat, uma mensagem de aviso indica que a identidade do assinante é desconhecida, como mostrado na ilustração a seguir.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

Da mesma forma, ao verificar programaticamente uma assinatura digital, você pode determinar o status da identidade do assinante. Por exemplo, se você verificar a assinatura digital no documento mostrado na ilustração anterior, o resultado seria que a identidade do assinante é desconhecida.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura e verificar assinaturas digitais, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-6}

Para verificar uma assinatura digital, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém a assinatura a ser verificada.
1. Definir opções de tempo de execução de PKI.
1. Verifique a assinatura digital.
1. Determine o status da assinatura.
1. Determine a identidade do assinante.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação de serviço de assinatura, crie um cliente de serviço de assinatura.

**Obtenha o documento PDF que contém a assinatura a ser verificada**

Para verificar uma assinatura usada para assinar digitalmente ou certificar um documento PDF, obtenha um documento PDF que contenha uma assinatura.

**Definir opções de tempo de execução de PKI**

Defina essas opções de tempo de execução de PKI que o serviço de assinatura usa ao verificar assinaturas em um documento PDF:

* Hora da verificação
* Verificação de revogação
* Valores de carimbo de data e hora

Como parte da configuração dessas opções, você pode especificar o tempo de verificação. Por exemplo, você pode selecionar a hora atual (a hora no computador do validador), que indica o uso da hora atual. Para obter informações sobre os diferentes valores de tempo, consulte o `VerificationTime` valor de enumeração em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Também é possível especificar se a verificação de revogação deve ser executada como parte do processo de verificação. Por exemplo, você pode executar uma verificação de revogação para determinar se o certificado foi revogado. Para obter informações sobre as opções de verificação de revogação, consulte `RevocationCheckStyle` valor de enumeração em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Para executar a verificação de revogação em um certificado, especifique um URL para um servidor de lista de revogação de certificado (CRL) usando um `CRLOptionSpec` objeto. No entanto, se você não especificar um URL para o servidor CRL, o Serviço de assinatura obterá o URL do certificado.

Em vez de usar um servidor CRL, você pode usar um servidor OCSP (protocolo de status de certificado) online ao executar a verificação de revogação. Normalmente, ao usar um servidor OCSP em vez de um servidor CRL, a verificação de revogação é executada mais rápido. (Consulte [Protocolo de Status de Certificado Online](https://tools.ietf.org/html/rfc2560).)

Você pode definir a ordem de servidor CRL e OCSP que o serviço de assinatura usa usando Aplicativos e Serviços do Adobe. Por exemplo, se o servidor OCSP estiver definido primeiro em Aplicativos e Serviços do Adobe, o servidor OCSP será verificado, seguido pelo servidor CRL.

Se você não executar a verificação de revogação, o serviço de assinatura não verificará se o certificado foi revogado. Ou seja, as informações do CRL e do servidor OCSP são ignoradas.

>[!NOTE]
>
>Você pode substituir o URL especificado no certificado usando um `CRLOptionSpec` e um `OCSPOptionSpec` objeto. Por exemplo, para substituir o servidor CRL, você pode chamar a variável `CRLOptionSpec` do objeto `setLocalURI` método .

O registro de data e hora é o processo de rastreamento da hora em que um documento assinado ou certificado foi modificado. Depois que um documento é assinado, ninguém pode modificá-lo. O carimbo de data e hora ajuda a impor a validade de um documento assinado ou certificado. É possível definir opções de carimbo de data e hora usando uma `TSPOptionSpec` objeto. Por exemplo, você pode especificar o URL de um servidor de provedor de carimbo de data e hora (TSP).

>[!NOTE]
>
>No início rápido do Java e do serviço da Web, o tempo de verificação é definido como `VerificationTime.CURRENT_TIME` e a verificação de revogação está definida como `RevocationCheckStyle.BestEffort`. Como nenhuma informação do servidor CRL ou OCSP é especificada, as informações do servidor são obtidas do certificado.

**Verificar a assinatura digital**

Para verificar uma assinatura com êxito, especifique o nome totalmente qualificado do campo de assinatura que contém a assinatura, como `form1[0].#subform[1].SignatureField3[3]`. Ao usar um campo de formulário XFA, também é possível usar o nome parcial do campo de assinatura : `SignatureField3`.

Por padrão, o serviço de assinatura limita o tempo que um documento pode ser assinado após o tempo de validação para 65 minutos. Se um usuário tentar verificar uma assinatura no momento atual e a hora de assinatura for posterior à hora atual e estiver dentro de 65 minutos, o serviço de assinatura não criará um erro de verificação.

>[!NOTE]
>
>Para outros valores necessários ao verificar uma assinatura, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Determine o status da assinatura**

Como parte da verificação de uma assinatura digital, você pode verificar o status da assinatura.

**Determinar a identidade do assinante**

Você pode determinar a identidade do assinante, que pode ser um dos seguintes valores:

* **Desconhecido**: Este assinante é desconhecido porque não é possível executar a verificação do assinante.
* **Confiável**: Esse assinante é confiável.
* **Não confiável**: Este assinante não é confiável.

**Consulte também**

[Verificar assinaturas digitais usando a API do Java](#verify-digital-signatures-using-the-java-api)

[Verificar assinaturas digitais usando a API de serviço da Web](#verify-digital-signatures-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar assinaturas digitais usando a API do Java {#verify-digital-signatures-using-the-java-api}

Verifique uma assinatura digital usando a API do serviço de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-assinaturas-client.jar, no classpath do seu projeto Java.

1. Criar um cliente de assinatura

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `SignatureServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obtenha o documento PDF que contém a assinatura a ser verificada

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF que contém a assinatura a ser verificada usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Definir opções de tempo de execução de PKI

   * Crie um `PKIOptions` usando seu construtor.
   * Defina o tempo de verificação chamando o `PKIOptions` do objeto `setVerificationTime` e a transmissão de um `VerificationTime` valor de enumeração que especifica o tempo de verificação.
   * Defina a opção de verificação de revogação chamando `PKIOptions` do objeto `setRevocationCheckStyle` e a transmissão de um `RevocationCheckStyle` valor de enumeração que especifica se a verificação de revogação deve ser executada.

1. Verificar a assinatura digital

   Verifique a assinatura chamando o `SignatureServiceClient` do objeto `verify2` e transmitindo os seguintes valores:

   * A `com.adobe.idp.Document` objeto que contém um documento PDF assinado digitalmente ou certificado.
   * Um valor de string que representa o nome do campo de assinatura que contém a assinatura a ser verificada.
   * A `PKIOptions` objeto que contém opções de tempo de execução de PKI.
   * A `VerifySPIOptions` instância que contém informações de SPI. Você pode especificar `null` para este parâmetro.

   O `verify2` método retorna um `PDFSignatureVerificationInfo` objeto que contém informações que podem ser usadas para verificar a assinatura digital.

1. Determine o status da assinatura

   * Determine o status da assinatura chamando o `PDFSignatureVerificationInfo` do objeto `getStatus` método . Esse método retorna um `SignatureStatus` que especifica o status da assinatura. Por exemplo, se um documento PDF assinado não for modificado, esse método retornará `SignatureStatus.DocumentSigNoChanges`.

1. Determinar a identidade do assinante

   * Determine a identidade do assinante chamando o `PDFSignatureVerificationInfo` do objeto `getSigner` método . Esse método retorna um `IdentityInformation` objeto.
   * Chame o `IdentityInformation` do objeto `getStatus` para determinar a identidade do assinante. Esse método retorna um `IdentityStatus` valor de enumeração que especifica a identidade. Por exemplo, se o assinante for confiável, esse método retornará `IdentityStatus.TRUSTED`.

**Consulte também**

[Verificação de assinaturas digitais](#verify-digital-signatures-using-the-java-api)

[Início rápido (modo SOAP): Verificação de uma assinatura digital usando a API do Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar assinaturas digitais usando a API de serviço da Web {#verify-digital-signatures-using-the-web-service-api}

Verifique uma assinatura digital usando a API do Serviço de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Criar um cliente de assinatura

   * Crie um `SignatureServiceClient` usando seu construtor padrão.
   * Crie um `SignatureServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `SignatureServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF que contém a assinatura a ser verificada

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF que contém uma assinatura digital ou certificada para verificar.
   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento de PDF assinado e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` propriedade do conteúdo da matriz de bytes.

1. Definir opções de tempo de execução de PKI

   * Crie um `PKIOptions` usando seu construtor.
   * Defina o tempo de verificação atribuindo a variável `PKIOptions` do objeto `verificationTime` membro de dados a `VerificationTime` valor de enumeração que especifica o tempo de verificação.
   * Defina a opção de verificação de revogação atribuindo a variável `PKIOptions` do objeto `revocationCheckStyle` membro de dados a `RevocationCheckStyle` valor de enumeração que especifica se a verificação de revogação deve ser executada.

1. Verificar a assinatura digital

   Verifique a assinatura chamando o `SignatureServiceClient` do objeto `verify2` e transmitindo os seguintes valores:

   * O `BLOB` objeto que contém um documento PDF assinado digitalmente ou certificado.
   * Um valor de string que representa o nome do campo de assinatura que contém a assinatura a ser verificada.
   * A `PKIOptions` objeto que contém opções de tempo de execução de PKI.
   * A `VerifySPIOptions` instância que contém informações de SPI. Você pode especificar `null` para este parâmetro.

   O `verify2` método retorna um `PDFSignatureVerificationInfo` objeto que contém informações que podem ser usadas para verificar a assinatura digital.

1. Determine o status da assinatura

   Determine o status da assinatura obtendo o valor da variável `PDFSignatureVerificationInfo` do objeto `status` membro de dados. Esse membro de dados armazena um `SignatureStatus` que especifica o status da assinatura. Por exemplo, se um documento PDF assinado for modificado, a variável `status` o membro de dados armazena o valor `SignatureStatus.DocumentSigNoChanges`.

1. Determinar a identidade do assinante

   * Determine a identidade do assinante recuperando o valor da variável `PDFSignatureVerificationInfo` do objeto `signer` membro de dados. Esse membro retorna um `IdentityInformation` objeto.
   * Recupere o `IdentityInformation` do objeto `status` membro de dados para determinar a identidade do assinante. Esse membro de dados retorna um `IdentityStatus` valor de enumeração que especifica a identidade. Por exemplo, se o assinante for confiável, esse membro retornará `IdentityStatus.TRUSTED`.

**Consulte também**

[Verificação de assinaturas digitais](#verify-digital-signatures-using-the-java-api)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificação de várias assinaturas digitais {#verifying-multiple-digital-signatures}

O AEM Forms fornece os meios para verificar todas as assinaturas digitais localizadas em um documento PDF. Suponha que um documento do PDF contenha várias assinaturas digitais como resultado de um processo de negócios que requer assinaturas de vários signatários. Por exemplo, considere uma transação financeira que requer a assinatura de um agente de empréstimo e de um gestor. Você pode usar a API Java do serviço de assinatura ou a API do serviço da Web para verificar todas as assinaturas no documento do PDF. Ao verificar várias assinaturas digitais, você pode verificar o status e as propriedades de cada assinatura. Antes de confiar em uma assinatura digital, é recomendável verificá-la. É recomendável que você esteja familiarizado com a verificação de uma assinatura digital única.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura e verificar assinaturas digitais, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-7}

Para verificar várias assinaturas digitais, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém as assinaturas a serem verificadas.
1. Definir opções de tempo de execução de PKI.
1. Recupere todas as assinaturas digitais.
1. Iterar por todas as assinaturas.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação de serviço de assinatura, crie um cliente de serviço de assinatura.

**Obtenha o documento do PDF que contém as assinaturas para verificar**

Para verificar uma assinatura usada para assinar digitalmente ou certificar um documento PDF, obtenha um documento PDF que contenha uma assinatura.

**Definir opções de tempo de execução de PKI**

Defina essas opções de tempo de execução de PKI que o serviço de assinatura usa ao verificar todas as assinaturas em um documento PDF:

* Hora da verificação
* Verificação de revogação
* Valores de carimbo de data e hora

Como parte da configuração dessas opções, você pode especificar o tempo de verificação. Por exemplo, você pode selecionar a hora atual (a hora no computador do validador), que indica o uso da hora atual. Para obter informações sobre os diferentes valores de tempo, consulte o `VerificationTime` valor de enumeração em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Também é possível especificar se a verificação de revogação deve ser executada como parte do processo de verificação. Por exemplo, você pode executar uma verificação de revogação para determinar se o certificado foi revogado. Para obter informações sobre as opções de verificação de revogação, consulte `RevocationCheckStyle` valor de enumeração em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Para executar a verificação de revogação em um certificado, especifique um URL para um servidor de lista de revogação de certificado (CRL) usando um `CRLOptionSpec` objeto. No entanto, se você não especificar um URL para um servidor CRL, o Serviço de assinatura obterá o URL do certificado.

Em vez de usar um servidor CRL, você pode usar um servidor OCSP (protocolo de status de certificado) online ao executar a verificação de revogação. Normalmente, ao usar um servidor OCSP em vez de um servidor CRL, a verificação de revogação é executada mais rápido. (Consulte [Protocolo de Status de Certificado Online](https://tools.ietf.org/html/rfc2560).)

Você pode definir a ordem de servidor CRL e OCSP que o serviço de assinatura usa usando Aplicativos e Serviços do Adobe. Por exemplo, se o servidor OCSP for definido primeiro em Aplicativos e Serviços do Adobe, o servidor OCSP será verificado, seguido pelo servidor CRL.

Se você não executar a verificação de revogação, o serviço de assinatura não verificará se o certificado foi revogado. Ou seja, as informações do CRL e do servidor OCSP são ignoradas.

>[!NOTE]
>
>Você pode substituir o URL especificado no certificado usando um `CRLOptionSpec` e um `OCSPOptionSpec` objeto. Por exemplo, para substituir o servidor CRL, você pode chamar a variável `CRLOptionSpec` do objeto `setLocalURI` método .

O registro de data e hora é o processo de rastreamento da hora em que um documento assinado ou certificado foi modificado. Depois que um documento é assinado, ninguém pode modificá-lo. O carimbo de data e hora ajuda a impor a validade de um documento assinado ou certificado. Você pode definir opções de carimbo de data e hora usando uma `TSPOptionSpec` objeto. Por exemplo, você pode especificar o URL de um servidor de provedor de carimbo de data e hora (TSP).

>[!NOTE]
>
>No início rápido do Java e do serviço da Web, o tempo de verificação é definido como `VerificationTime.CURRENT_TIME` e a verificação de revogação está definida como `RevocationCheckStyle.BestEffort`. Como nenhuma informação do servidor CRL ou OCSP é especificada, as informações do servidor são obtidas do certificado.

**Recuperar todas as assinaturas digitais**

Para verificar todas as assinaturas digitais localizadas em um documento PDF, recupere as assinaturas digitais do documento PDF. Todas as assinaturas são retornadas em uma lista. Como parte da verificação de uma assinatura digital, verifique o status da assinatura.

>[!NOTE]
>
>Ao contrário de quando você verifica uma única assinatura digital, ao verificar várias assinaturas, não é necessário especificar o nome do campo de assinatura.

**Iterar por todas as assinaturas**

Iterar por cada assinatura. Ou seja, para cada assinatura, verifique a assinatura digital e verifique a identidade do assinante e o status de cada assinatura. (Consulte [Verificação de assinaturas digitais](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>Você não precisa repetir todas as assinaturas se o requisito for todo o documento.

**Consulte também**

[Verificar várias assinaturas digitais usando a API do Java](#verify-digital-signatures-using-the-java-api)

[Verificação de várias assinaturas digitais usando a API do serviço da Web](#verify-digital-signatures-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar várias assinaturas digitais usando a API do Java {#verify-multiple-digital-signatures-using-the-java-api}

Verifique várias assinaturas digitais usando a API do serviço de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-assinaturas-client.jar, no classpath do seu projeto Java.

1. Criar um cliente de assinatura

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `SignatureServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obtenha o documento do PDF que contém as assinaturas para verificar

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF que contém várias assinaturas digitais para verificar usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Definir opções de tempo de execução de PKI

   * Crie um `PKIOptions` usando seu construtor.
   * Defina o tempo de verificação chamando o `PKIOptions` do objeto `setVerificationTime` e a transmissão de um `VerificationTime` valor de enumeração que especifica o tempo de verificação.
   * Defina a opção de verificação de revogação chamando `PKIOptions` do objeto `setRevocationCheckStyle` e a transmissão de um `RevocationCheckStyle` valor de enumeração que especifica se a verificação de revogação deve ser executada.

1. Recuperar todas as assinaturas digitais

   Chame o `SignatureServiceClient` do objeto `verifyPDFDocument` e transmita os seguintes valores:

   * A `com.adobe.idp.Document` objeto que contém um documento PDF que contém várias assinaturas digitais.
   * A `PKIOptions` objeto que contém opções de tempo de execução de PKI.
   * A `VerifySPIOptions` instância que contém informações de SPI. Você pode especificar `null` para este parâmetro.

   O `verifyPDFDocument` método retorna um `PDFDocumentVerificationInfo` objeto que contém informações sobre todas as assinaturas digitais localizadas no documento PDF.

1. Iterar por todas as assinaturas

   * Iterar por meio de todas as assinaturas, chamando o `PDFDocumentVerificationInfo` do objeto `getVerificationInfos` método . Esse método retorna um `java.util.List` objeto no qual cada elemento é um `PDFSignatureVerificationInfo` objeto. Use um `java.util.Iterator` objeto a ser repetido na lista de assinaturas.
   * Usar o `PDFSignatureVerificationInfo` , é possível executar tarefas como determinar o status da assinatura chamando o `PDFSignatureVerificationInfo` do objeto `getStatus` método . Esse método retorna um `SignatureStatus` objeto cujo membro de dados estáticos informa sobre o status da assinatura. Por exemplo, se a assinatura for desconhecida, esse método retornará `SignatureStatus.DocumentSignatureUnknown`.

**Consulte também**

[Verificação de várias assinaturas digitais](#verifying-multiple-digital-signatures)

[Início rápido (modo SOAP): Verificação de várias assinaturas digitais usando a API do Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Verificação de assinaturas digitais](#verify-digital-signatures-using-the-java-api)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificação de várias assinaturas digitais usando a API do serviço da Web {#verifying-multiple-digital-signatures-using-the-web-service-api}

Verifique várias assinaturas digitais usando a API do Serviço de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Criar um cliente de assinatura

   * Crie um `SignatureServiceClient` usando seu construtor padrão.
   * Crie um `SignatureServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `SignatureServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento do PDF que contém as assinaturas para verificar

   * Crie um `BLOB` usando seu construtor. O `BLOB` O objeto armazena um documento PDF que contém várias assinaturas digitais para verificação.
   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` propriedade do conteúdo da matriz de bytes.

1. Definir opções de tempo de execução de PKI

   * Crie um `PKIOptions` usando seu construtor.
   * Defina o tempo de verificação atribuindo a variável `PKIOptions` do objeto `verificationTime` membro de dados a `VerificationTime` valor de enumeração que especifica o tempo de verificação.
   * Defina a opção de verificação de revogação atribuindo a variável `PKIOptions` do objeto `revocationCheckStyle` membro de dados a `RevocationCheckStyle` valor de enumeração que especifica se a verificação de revogação deve ser executada.

1. Recuperar todas as assinaturas digitais

   Chame o `SignatureServiceClient` do objeto `verifyPDFDocument` e transmita os seguintes valores:

   * A `BLOB` objeto que contém um documento PDF que contém várias assinaturas digitais.
   * A `PKIOptions` objeto que contém opções de tempo de execução de PKI.
   * A `VerifySPIOptions` instância que contém informações de SPI. Você pode especificar null para este parâmetro.

   O `verifyPDFDocument` método retorna um `PDFDocumentVerificationInfo` objeto que contém informações sobre todas as assinaturas digitais localizadas no documento PDF.

1. Iterar por todas as assinaturas

   * Iterar todas as assinaturas obtendo o `PDFDocumentVerificationInfo` do objeto `verificationInfos` membro de dados. Esse membro de dados retorna um `Object` matriz em que cada elemento é um `PDFSignatureVerificationInfo` objeto.
   * Usar o `PDFSignatureVerificationInfo` , é possível executar tarefas como determinar o status da assinatura obtendo o `PDFSignatureVerificationInfo` do objeto `status` membro de dados. Esse membro de dados retorna um `SignatureStatus` objeto cujo membro de dados estáticos informa sobre o status da assinatura. Por exemplo, se a assinatura for desconhecida, esse método retornará `SignatureStatus.DocumentSignatureUnknown`.

**Consulte também**

[Verificação de várias assinaturas digitais](#verifying-multiple-digital-signatures)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Remover assinaturas digitais {#removing-digital-signatures}

Assinaturas digitais devem ser removidas de um campo de assinatura antes que uma assinatura digital mais recente possa ser aplicada. Uma assinatura digital não pode ser substituída. Se você tentar aplicar uma assinatura digital a um campo de assinatura que contenha uma assinatura, ocorrerá uma exceção.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-8}

Para remover uma assinatura digital de um campo de assinatura, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém uma assinatura a ser removida.
1. Remova a assinatura digital do campo de assinatura.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de poder executar programaticamente uma operação de serviço de assinatura, é necessário criar um cliente de serviço de assinatura.

**Obtenha o documento PDF que contém uma assinatura para remover**

Para remover uma assinatura de um documento PDF, você deve obter um documento PDF que contenha uma assinatura.

**Remova a assinatura digital do campo de assinatura**

Para remover com êxito uma assinatura digital de um documento PDF, você deve especificar o nome do campo de assinatura que contém a assinatura digital. Além disso, você deve ter permissão para remover a assinatura digital; caso contrário, ocorrerá uma exceção.

**Salve o documento PDF como um arquivo PDF**

Depois que o serviço de assinatura remove uma assinatura digital de um campo de assinatura, você pode salvar o documento do PDF como um arquivo PDF, para que os usuários possam abri-lo no Acrobat ou Adobe Reader.

**Consulte também**

[Remova assinaturas digitais usando a API Java](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Remover assinaturas digitais usando a API de serviço da Web](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields)

### Remova assinaturas digitais usando a API Java {#remove-digital-signatures-using-the-java-api}

Remova uma assinatura digital usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-assinaturas-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de assinatura.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `SignatureServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Obtenha o documento PDF que contém uma assinatura para remover

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF que contém a assinatura a ser removida usando seu construtor e passando um valor de string que especifica o local do documento PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Remova a assinatura digital do campo de assinatura

   Remova uma assinatura digital de um campo de assinatura chamando o `SignatureServiceClient` do objeto `clearSignatureField` e transmitindo os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o documento PDF que contém a assinatura a ser removida.
   * Um valor de string que especifica o nome do campo de assinatura que contém a assinatura digital.

   O `clearSignatureField` método retorna um `com.adobe.idp.Document` objeto que representa o documento PDF do qual a assinatura digital foi removida.

1. Salve o documento PDF como um arquivo PDF

   * Crie um `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método . Passe o `java.io.File` objeto para copiar o conteúdo da `com.adobe.idp.Document` ao arquivo. Certifique-se de usar a variável `Document` objeto retornado pelo `clearSignatureField` método .

**Consulte também**

[Remover assinaturas digitais](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Início rápido (modo SOAP): Remoção de uma assinatura digital usando a API do Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Remover assinaturas digitais usando a API de serviço da Web {#remove-digital-signatures-using-the-web-service-api}

Remova uma assinatura digital usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Criar um cliente de assinatura

   * Crie um `SignatureServiceClient` usando seu construtor padrão.
   * Crie um `SignatureServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `SignatureServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF que contém uma assinatura para remover

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF que contém uma assinatura digital a ser removida.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento de PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Remova a assinatura digital do campo de assinatura

   Remova a assinatura digital chamando o `SignatureServiceClient` do objeto `clearSignatureField` e transmitindo os seguintes valores:

   * A `BLOB` objeto que contém o documento PDF assinado.
   * Um valor de string que representa o nome do campo de assinatura que contém a assinatura digital a ser removida.

   O `clearSignatureField` método retorna um `BLOB` objeto que representa o documento PDF do qual a assinatura digital foi removida.

1. Salve o documento PDF como um arquivo PDF

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF que contém um campo de assinatura vazio e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto retornado pelo `sign` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes no arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Remover assinaturas digitais](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
