---
title: Assinatura digital e documentos de certificação
description: Use o serviço de assinatura para adicionar e excluir campos de assinatura digital a um documento PDF, recuperar os nomes de campos de assinatura em um documento PDF, modificar campos de assinatura, assinar digitalmente documentos PDF, certificar documentos PDF, validar assinaturas digitais em um documento PDF, validar todas as assinaturas digitais em um documento PDF e remover uma assinatura digital de um campo de assinatura.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '16917'
ht-degree: 0%

---

# Assinatura digital e documentos de certificação {#digitally-signing-and-certifying-documents}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o Serviço de Assinatura**

O serviço de Assinatura permite que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que ele distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipients desejados possam alterar os documentos. Como os recursos de segurança são aplicados ao próprio documento, o documento permanece seguro e controlado durante todo o ciclo de vida. Um documento permanece seguro além do firewall, quando é baixado offline e quando é enviado de volta à sua organização.

>[!NOTE]
>
>Você pode criar um manipulador de assinatura personalizado para o serviço de assinatura que é chamado quando determinadas operações são chamadas, como a assinatura de um documento PDF.

**Nomes de campos de assinatura**

Algumas operações do Serviço de assinatura exigem que você especifique o nome do campo de assinatura no qual uma operação é executada. Por exemplo, ao assinar um documento PDF, você especifica o nome do campo de assinatura a ser assinado. O nome completo de um campo de assinatura deve ser `form1[0].Form1[0].SignatureField1[0]`. Você pode especificar `SignatureField1[0]` em vez de `form1[0].Form1[0].SignatureField1[0]`.

Às vezes, um conflito faz com que o serviço de Assinatura assine (ou execute outra operação que exija o nome do campo de assinatura) o campo errado. Este conflito é o resultado do nome `SignatureField1[0]` aparecer em dois ou mais lugares no mesmo documento PDF. Por exemplo, considere um documento PDF que contenha dois campos de assinatura chamados `form1[0].Form1[0].SignatureField1[0]` e `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` e você especifique `SignatureField1[0]`. Nessa situação, o serviço de Assinatura assina o primeiro campo de assinatura encontrado ao iterar todos os campos de assinatura no documento.

Se houver vários campos de assinatura localizados em um documento PDF, é recomendável especificar os nomes completos dos campos de assinatura. Ou seja, especifique `form1[0].Form1[0].SignatureField1[0]`em vez de `SignatureField1[0]`.

Você pode realizar essas tarefas usando o serviço de Assinatura:

* Adicione e exclua campos de assinatura digital a um documento PDF. (Consulte [Adição De Campos De Assinatura](digitally-signing-certifying-documents.md#adding-signature-fields).)
* Recupere os nomes dos campos de assinatura em um documento PDF. (Consulte [Recuperando Nomes de Campos de Assinatura](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* Modifique os campos de assinatura. (Consulte [Modificação De Campos De Assinatura](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* Assinar digitalmente os documentos do PDF. (Consulte [Assinatura digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* Certificar documentos do PDF. (Consulte [Documentos de PDF de Certificação](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* Validar assinaturas digitais em um documento PDF. (Consulte [Verificação de assinaturas digitais](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Valide todas as assinaturas digitais em um documento PDF. (Consulte [Verificação de várias assinaturas digitais](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Remova uma assinatura digital de um campo de assinatura. (Consulte [Remoção De Assinaturas Digitais](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de assinatura, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Adição de campos de assinatura {#adding-signature-fields}

As assinaturas digitais aparecem em campos de assinatura, que são campos de formulário que contêm uma representação gráfica da assinatura. Os campos de assinatura podem ser visíveis ou invisíveis. Os assinantes podem usar um campo de assinatura pré-existente ou um campo de assinatura pode ser adicionado programaticamente. Em ambos os casos, o campo de assinatura deve existir antes que um documento PDF possa ser assinado.

Você pode adicionar programaticamente um campo de assinatura usando a API Java do serviço de assinatura ou a API do serviço Web de assinatura. Você pode adicionar mais de um campo de assinatura a um documento PDF; no entanto, cada nome de campo de assinatura deve ser exclusivo.

>[!NOTE]
>
>Alguns tipos de documentos PDF não permitem adicionar programaticamente um campo de assinatura. Para obter mais informações sobre o Serviço de assinatura e a adição de campos de assinatura, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para adicionar um campo de assinatura a um documento PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha um documento PDF ao qual um campo de assinatura é adicionado.
1. Adicione um campo de assinatura.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação do serviço de Assinatura, você deve criar um cliente do serviço de Assinatura.

**Obtenha um documento PDF ao qual um campo de assinatura é adicionado**

Obtenha um documento de PDF ao qual um campo de assinatura é adicionado.

**Adicionar um campo de assinatura**

Para adicionar com êxito um campo de assinatura a um documento PDF, especifique valores de coordenadas que identifiquem o local do campo de assinatura. (Se você adicionar um campo de assinatura invisível, esses valores não serão obrigatórios.) Além disso, você pode especificar quais campos no documento PDF são bloqueados depois que uma assinatura é aplicada ao campo de assinatura.

**Salvar o documento PDF como um arquivo PDF**

Depois que o serviço de Assinatura adicionar um campo de assinatura ao documento PDF, você poderá salvar o documento como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou no Adobe Reader.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assinatura digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Adicionar campos de assinatura usando a API Java {#add-signature-fields-using-the-java-api}

Adicione um campo de assinatura usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signatures-client.jar, no classpath do projeto Java.

1. Criar um cliente de assinatura

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha um documento PDF ao qual um campo de assinatura é adicionado

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF ao qual um campo de assinatura é adicionado usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Adicionar um campo de assinatura

   * Crie um objeto `PositionRectangle` que especifique a localização do campo de assinatura usando seu construtor. No construtor, especifique valores de coordenadas.
   * Se desejar, crie um objeto `FieldMDPOptions` que especifique os campos que são bloqueados quando uma assinatura digital é aplicada ao campo de assinatura.
   * Adicione um campo de assinatura a um documento PDF invocando o método `addSignatureField` do objeto `SignatureServiceClient` e transmitindo os seguintes valores:

      * UM `com.adobe.idp`. Objeto `Document` que representa o documento PDF ao qual um campo de assinatura é adicionado.
      * Um valor de cadeia de caracteres que especifica o nome do campo de assinatura.
      * Um valor `java.lang.Integer` que representa o número da página à qual um campo de assinatura é adicionado.
      * Um objeto `PositionRectangle` que especifica o local do campo de assinatura.
      * Um objeto `FieldMDPOptions` que especifica campos no documento PDF que são bloqueados após uma assinatura digital ser aplicada ao campo de assinatura. Este valor de parâmetro é opcional, e você pode passar `null`.

   * Um objeto `PDFSeedValueOptions` que especifica vários valores de tempo de execução. Este valor de parâmetro é opcional, e você pode passar `null`.

     O método `addSignatureField` retorna um `com.adobe.idp`. Objeto `Document` que representa um documento PDF que contém um campo de assinatura.

   >[!NOTE]
   >
   >Você pode invocar o método `addInvisibleSignatureField` do objeto `SignatureServiceClient` para adicionar um campo de assinatura invisível.

1. Salve o documento PDF como um arquivo PDF

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o `com.adobe.idp`. Método `copyToFile` do objeto `Document` para copiar o conteúdo do objeto `Document` para o arquivo. Certifique-se de usar o `com.adobe.idp`. Objeto `Document` retornado pelo método `addSignatureField`.

**Consulte também**

[Início Rápido da API do Serviço de Assinatura](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Adicionar campos de assinatura usando a API do serviço Web {#add-signature-fields-using-the-web-service-api}

Para adicionar um campo de assinatura usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha um documento PDF ao qual um campo de assinatura é adicionado

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF que conterá um campo de assinatura.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` com o conteúdo da matriz de bytes.

1. Adicionar um campo de assinatura

   Adicione um campo de assinatura ao documento PDF invocando o método `addSignatureField` do objeto `SignatureServiceClient` e transmitindo os seguintes valores:

   * Um objeto `BLOB` que representa o documento PDF ao qual um campo de assinatura é adicionado.
   * Um valor de cadeia de caracteres que especifica o nome do campo de assinatura.
   * Um valor inteiro que representa o número da página à qual um campo de assinatura é adicionado.
   * Um objeto `PositionRect` que especifica o local do campo de assinatura.
   * Um objeto `FieldMDPOptions` que especifica campos no documento PDF que são bloqueados após uma assinatura digital ser aplicada ao campo de assinatura. Este valor de parâmetro é opcional, e você pode passar `null`.
   * Um objeto `PDFSeedValueOptions` que especifica vários valores de tempo de execução. Este valor de parâmetro é opcional, e você pode passar `null`.

   O método `addSignatureField` retorna um objeto `BLOB` que representa um documento PDF que contém um campo de assinatura.

1. Salve o documento PDF como um arquivo PDF

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF que conterá o campo de assinatura e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `addSignatureField`. Popular a matriz de bytes obtendo o valor do membro de dados `binaryData` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperando nomes de campos de assinatura {#retrieving-signature-field-names}

Você pode recuperar os nomes de todos os campos de assinatura que estão em um documento PDF que você deseja assinar ou certificar. Se não tiver certeza dos nomes dos campos de assinatura que estão em um documento PDF ou se quiser verificar os nomes, você poderá recuperá-los programaticamente. O serviço de Assinatura retorna o nome totalmente qualificado do campo de assinatura, como `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de assinatura, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumo das etapas {#summary_of_steps-1}

Para recuperar nomes de campos de assinatura, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém campos de assinatura.
1. Recupere os nomes dos campos de assinatura.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação do serviço de Assinatura, você deve criar um cliente do serviço de Assinatura.

**Obtenha o documento PDF que contém campos de assinatura**

Recupere um documento PDF que contenha campos de assinatura.

**Recuperar os nomes dos campos de assinatura**

Você pode recuperar nomes de campos de assinatura depois de recuperar um documento PDF que contenha um ou mais campos de assinatura.

**Consulte também**

[Recuperar nomes de campo de assinatura usando a API Java](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Recuperar campo de assinatura usando a API do serviço Web](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adição de campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields)

### Recuperar nomes de campo de assinatura usando a API Java {#retrieve-signature-field-names-using-the-java-api}

Recupere nomes de campos de assinatura usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signatures-client.jar, no classpath do projeto Java.

1. Criar um cliente de assinatura

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento PDF que contém campos de assinatura

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF que contém campos de assinatura usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Recuperar os nomes dos campos de assinatura

   * Recupere os nomes de campo de assinatura invocando o método `getSignatureFieldList` do objeto `SignatureServiceClient` e transmitindo o objeto `com.adobe.idp.Document` que contém o documento PDF que contém campos de assinatura. Este método retorna um objeto `java.util.List`, em que cada elemento contém um objeto `PDFSignatureField`. Usando esse objeto, você pode obter informações adicionais sobre um campo de assinatura, como se ele está visível ou não.
   * Repita através do objeto `java.util.List` para determinar se há nomes de campo de assinatura. Para cada campo de assinatura no documento PDF, você pode obter um objeto `PDFSignatureField` separado. Para obter o nome do campo de assinatura, chame o método `getName` do objeto `PDFSignatureField`. Este método retorna um valor de string que especifica o nome do campo de assinatura.

**Consulte também**

[Recuperando nomes de campos de assinatura](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Início rápido (modo SOAP): recuperação de nomes de campos de assinatura usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar campo de assinatura usando a API do serviço Web {#retrieve-signature-field-using-the-web-service-api}

Recuperar nomes de campos de assinatura usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF que contém campos de assinatura

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF que contém campos de assinatura.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Recuperar os nomes dos campos de assinatura

   * Recupere os nomes de campo de assinatura invocando o método `getSignatureFieldList` do objeto `SignatureServiceClient` e transmitindo o objeto `BLOB` que contém o documento PDF que contém campos de assinatura. Este método retorna um objeto de coleção `MyArrayOfPDFSignatureField` em que cada elemento contém um objeto `PDFSignatureField`.
   * Repita através do objeto `MyArrayOfPDFSignatureField` para determinar se há nomes de campo de assinatura. Para cada campo de assinatura no documento PDF, você pode obter um objeto `PDFSignatureField`. Para obter o nome do campo de assinatura, chame o método `getName` do objeto `PDFSignatureField`. Este método retorna um valor de string que especifica o nome do campo de assinatura.

**Consulte também**

[Recuperando nomes de campos de assinatura](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificação de campos de assinatura {#modifying-signature-fields}

Você pode modificar campos de assinatura que estão em um documento PDF usando a API Java e a API de serviço da Web. A modificação de um campo de assinatura envolve a manipulação de seus valores de dicionário de bloqueio de campo de assinatura ou valores de dicionário de valor de seed.

Um *dicionário de bloqueio de campo* especifica uma lista de campos que são bloqueados quando o campo de assinatura é assinado. Um campo bloqueado impede que os usuários façam alterações no campo. Um *dicionário de valor de propagação* contém informações de restrição que são usadas no momento em que a assinatura é aplicada. Por exemplo, você pode alterar permissões que controlam as ações que podem ocorrer sem invalidar uma assinatura.

Ao modificar um campo de assinatura existente, você pode alterar o documento PDF para refletir as necessidades comerciais em alteração. Por exemplo, um novo requisito comercial pode exigir o bloqueio de todos os campos do documento depois que ele for assinado.

Esta seção explica como modificar um campo de assinatura alterando os valores do dicionário de bloqueio de campo e do dicionário de valor de seed. As alterações feitas no dicionário de bloqueio de campo de assinatura resultam no bloqueio de todos os campos no documento PDF quando um campo de assinatura é assinado. As alterações feitas no dicionário do valor de propagação proíbem tipos específicos de alterações no documento.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de assinatura e a modificação dos campos de assinatura, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para modificar campos de assinatura em um documento PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém o campo de assinatura a ser modificado.
1. Definir valores do dicionário.
1. Modifique o campo de assinatura.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do LiveCycle](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação do serviço de Assinatura, você deve criar um cliente do serviço de Assinatura.

**Obter o documento de PDF que contém o campo de assinatura a ser modificado**

Recupere um documento PDF que contenha o campo de assinatura a ser modificado.

**Definir valores do dicionário**

Para modificar um campo de assinatura, atribua valores ao dicionário de bloqueio de campo ou ao dicionário de valor de seed. A especificação de valores de dicionário de bloqueio de campo de assinatura envolve a especificação de campos de documento de PDF que são bloqueados quando o campo de assinatura é assinado. (Esta seção discute como bloquear todos os campos.)

Os seguintes valores do dicionário de seed value podem ser definidos:

* **Verificação de revisão**: especifica se a verificação de revogação é executada quando uma assinatura é aplicada ao campo de assinatura.
* **Opções de certificado**: atribui valores ao dicionário do valor de propagação do certificado. Antes de especificar as opções de certificado, é recomendável que você se familiarize com um dicionário do valor inicial do certificado. (Consulte [Referência de PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opções de resumo**: atribui algoritmos de resumo que são usados para assinatura. Os valores válidos são SHA1, SHA256, SHA384, SHA512 e RIPEMD160.
* **Filtro**: especifica o filtro usado com o campo de assinatura. Por exemplo, você pode usar o filtro Adobe.PPKLite. (Consulte [Referência de PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opções de sinalizador**: especifica os valores de sinalizador associados a este campo de assinatura. Um valor de 1 significa que um signatário deve usar somente os valores especificados para a entrada. Um valor de 0 significa que outros valores são permitidos. Estas são as posições dos bits:

   * **1(Filtro):** O manipulador de assinatura a ser usado para assinar o campo de assinatura
   * **2 (SubFilter):** uma matriz de nomes que indica codificações aceitáveis a serem usadas ao assinar
   * **3 (V)**: o número de versão mínimo necessário do manipulador de assinatura a ser usado para assinar o campo de assinatura
   * **4 (Motivos):** Uma matriz de cadeias de caracteres que especifica os possíveis motivos para assinar um documento
   * **5 (PDFLegalWarnings):** Uma matriz de cadeias de caracteres que especifica possíveis atestados legais

* **Atestados legais**: quando um documento é certificado, ele é automaticamente verificado em busca de tipos específicos de conteúdo que possam tornar o conteúdo visível de um documento ambíguo ou enganoso. Por exemplo, uma anotação pode obscurecer texto importante para entender o que está sendo certificado. O processo de digitalização gera avisos que indicam a presença desse tipo de conteúdo. Também fornece uma explicação adicional do conteúdo que pode ter gerado avisos.
* **Permissões**: especifica as permissões que podem ser usadas em um documento PDF sem invalidar a assinatura.
* **Motivos**: especifica os motivos pelos quais este documento deve ser assinado.
* **Carimbo de data/hora**: especifica as opções de carimbo de data/hora. Você pode, por exemplo, definir a URL do servidor de carimbo de data e hora usado.
* **Versão**: especifica o número de versão mínimo do manipulador de assinatura a ser usado para assinar o campo de assinatura.

**Modificar o campo de assinatura**

Depois de criar um cliente de serviço de Assinatura, recuperar o documento PDF que contém o campo de assinatura a ser modificado e definir os valores do dicionário, você pode instruir o serviço de Assinatura a modificar o campo de assinatura. O serviço de Assinatura retorna um documento PDF que contém o campo de assinatura modificado. O documento PDF original não é afetado.

**Salvar o documento PDF como um arquivo PDF**

Salve o documento PDF que contém o campo de assinatura modificado como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou no Adobe Reader.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API do Serviço de Assinatura](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[Assinatura digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Modificar campos de assinatura usando a API Java {#modify-signature-fields-using-the-java-api}

Modifique um campo de assinatura usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signatures-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente de assinatura

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento PDF que contém o campo de assinatura a ser modificado

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF que contém o campo de assinatura a ser modificado usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Definir valores do dicionário

   * Crie um objeto `PDFSignatureFieldProperties` usando seu construtor. Um objeto `PDFSignatureFieldProperties` armazena informações do dicionário de bloqueio de campo de assinatura e do dicionário de valor de semente.
   * Crie um objeto `PDFSeedValueOptionSpec` usando seu construtor. Este objeto permite que você defina valores do dicionário do seed value.
   * Não permita alterações no documento PDF invocando o método `setMdpValue` do objeto `PDFSeedValueOptionSpec` e transmitindo o valor de enumeração `MDPPermissions.NoChanges`.
   * Crie um objeto `FieldMDPOptionSpec` usando seu construtor. Esse objeto permite definir valores do dicionário de bloqueio de campo de assinatura.
   * Bloqueie todos os campos no documento PDF chamando o método `setMdpValue` do objeto `FieldMDPOptionSpec` e passando o valor de enumeração `FieldMDPAction.ALL`.
   * Defina as informações do dicionário do valor de propagação chamando o método `setSeedValue` do objeto `PDFSignatureFieldProperties` e transmitindo o objeto `PDFSeedValueOptionSpec`.
   * Defina as informações do dicionário de bloqueio de campo de assinatura invocando o método `setFieldMDP` do `PDFSignatureFieldProperties`objeto e transmitindo o objeto `FieldMDPOptionSpec`.

   >[!NOTE]
   >
   >Para ver todos os valores do dicionário de valor de propagação que você pode definir, consulte a referência de classe `PDFSeedValueOptionSpec`. (Consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. Modificar o campo de assinatura

   Modifique o campo de assinatura chamando o método `modifySignatureField` do objeto `SignatureServiceClient` e passando os seguintes valores:

   * O objeto `com.adobe.idp.Document` que armazena o documento PDF que contém o campo de assinatura a ser modificado
   * Um valor de string que especifica o nome do campo de assinatura
   * O objeto `PDFSignatureFieldProperties` que armazena informações do dicionário de bloqueio de campo de assinatura e do dicionário de valor de semente

   O método `modifySignatureField` retorna um objeto `com.adobe.idp.Document` que armazena um documento PDF que contém o campo de assinatura modificado.

1. Salve o documento PDF como um arquivo PDF

   * Crie um objeto `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo. Certifique-se de usar o objeto `com.adobe.idp.Document` retornado pelo método `modifySignatureField`.

### Modificar campos de assinatura usando a API do serviço Web {#modify-signature-fields-using-the-web-service-api}

Modifique um campo de assinatura usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF que contém o campo de assinatura a ser modificado

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF que contém o campo de assinatura a ser modificado.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo à propriedade `MTOM` o conteúdo da matriz de bytes.

1. Definir valores do dicionário

   * Crie um objeto `PDFSignatureFieldProperties` usando seu construtor. Esse objeto armazena informações do dicionário de bloqueio de campo de assinatura e do dicionário de valor de seed.
   * Crie um objeto `PDFSeedValueOptionSpec` usando seu construtor. Este objeto permite que você defina valores do dicionário do seed value.
   * Não permita alterações no documento PDF atribuindo o valor de enumeração `MDPPermissions.NoChanges` ao membro de dados `mdpValue` do objeto `PDFSeedValueOptionSpec`.
   * Crie um objeto `FieldMDPOptionSpec` usando seu construtor. Esse objeto permite definir valores do dicionário de bloqueio de campo de assinatura.
   * Bloqueie todos os campos no documento PDF atribuindo o valor de enumeração `FieldMDPAction.ALL` ao membro de dados `mdpValue` do objeto `FieldMDPOptionSpec`.
   * Defina as informações do dicionário do valor de propagação atribuindo o objeto `PDFSeedValueOptionSpec` ao membro de dados `seedValue` do objeto `PDFSignatureFieldProperties`.
   * Defina as informações do dicionário de bloqueio de campo de assinatura atribuindo o objeto `FieldMDPOptionSpec` ao membro de dados `fieldMDP` do objeto `PDFSignatureFieldProperties`.

   >[!NOTE]
   >
   >Para ver todos os valores do dicionário de valor de propagação que você pode definir, consulte a referência de classe `PDFSeedValueOptionSpec`. (Consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. Modificar o campo de assinatura

   Modifique o campo de assinatura chamando o método `modifySignatureField` do objeto `SignatureServiceClient` e passando os seguintes valores:

   * O objeto `BLOB` que armazena o documento PDF que contém o campo de assinatura a ser modificado
   * Um valor de string que especifica o nome do campo de assinatura
   * O objeto `PDFSignatureFieldProperties` que armazena informações do dicionário de bloqueio de campo de assinatura e do dicionário de valor de semente

   O método `modifySignatureField` retorna um objeto `BLOB` que armazena um documento PDF que contém o campo de assinatura modificado.

1. Salve o documento PDF como um arquivo PDF

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF que conterá o campo de assinatura e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `addSignatureField`. Popular a matriz de bytes obtendo o valor do membro de dados `MTOM` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Assinatura digital de documentos PDF {#digitally-signing-pdf-documents}

As assinaturas digitais podem ser aplicadas a documentos PDF para fornecer um nível de segurança. As assinaturas digitais, como as assinaturas manuscritas, fornecem um meio pelo qual os signatários se identificam e fazem declarações sobre um documento. A tecnologia usada para assinar documentos digitalmente ajuda a garantir que tanto o signatário quanto os recipients estejam claros sobre o que foi assinado e confiantes de que o documento não foi alterado desde que foi assinado.

Os documentos PDF são assinados por meio de tecnologia de chave pública. Um signatário tem duas chaves: uma chave pública e uma chave privada. A chave privada é armazenada na credencial de um usuário que deve estar disponível no momento da assinatura. A chave pública é armazenada no certificado do usuário que deve estar disponível para os recipients validarem a assinatura. Informações sobre certificados revogados são encontradas nas listas de certificados revogados (CRLs) e respostas do Protocolo de Status de Certificados Online (OCSP) distribuídas pelas Autoridades de Certificação (CAs). A hora da assinatura pode ser obtida de uma fonte confiável conhecida como Autoridade de carimbo de data e hora.

>[!NOTE]
>
>Antes de assinar digitalmente um documento PDF, você deve garantir que adicione o certificado ao AEM Forms. Um certificado é adicionado usando o console de administração ou de forma programática usando a API do Gerenciador de Confiança. (Consulte [Importar Credenciais usando a API do Gerenciador de Confiança](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Você pode assinar documentos PDF de forma programática e digital. Ao assinar digitalmente um documento PDF, você deve fazer referência a uma credencial de segurança que existe no AEM Forms. A credencial é a chave privada usada para assinatura.

O serviço de Assinatura executa as seguintes etapas quando um documento PDF é assinado:

1. O serviço de Assinatura recupera a credencial do Truststore transmitindo o alias especificado na solicitação.
1. O Truststore procura a credencial especificada.
1. A credencial é retornada ao serviço de Assinatura e usada para assinar o documento. A credencial também é armazenada em cache com o alias para solicitações futuras.

Para obter informações sobre como manipular a credencial de segurança, consulte o guia *Instalação e Implantação do AEM Forms* para o seu servidor de aplicativos.

>[!NOTE]
>
>Há diferenças entre os documentos de assinatura e certificação. (Consulte [Documentos de PDF de Certificação](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>Nem todos os documentos do PDF suportam assinatura. Para obter mais informações sobre o serviço de Assinatura e a assinatura digital de documentos, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>O serviço de Assinatura não oferece suporte a arquivos XDP com dados de PDF incorporados como entrada para uma operação, como a certificação de um documento. Esta ação resulta no serviço de Assinatura lançar um `PDFOperationException`. Para resolver esse problema, converta o arquivo XDP em um arquivo PDF usando o serviço Utilitários PDF e passe o arquivo PDF convertido para uma operação do serviço de Assinatura. (Consulte [Trabalhando com Utilitários PDF](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**Credencial HSM do Cipher nShield**

Ao usar uma credencial HSM do nCipher nShield para assinar ou certificar um documento PDF, a nova credencial não pode ser usada até que o servidor de aplicativos J2EE no qual o AEM Forms está implantado seja reiniciado. No entanto, você pode definir um valor de configuração, o que faz com que a operação sign ou certify funcione sem reiniciar o servidor de aplicativos J2EE.

Você pode adicionar o seguinte valor de configuração no arquivo cknfastrc, localizado em /opt/nfast/cknfastrc (ou c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Depois de adicionar esse valor de configuração ao arquivo cknfastrc, a nova credencial pode ser usada sem reiniciar o servidor de aplicativos J2EE.

    >[!NOTE]
    >
    > É recomendável usar o comando &#39;Ctrl + C&#39; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

**Assinatura não confiável**

Ao certificar e assinar o mesmo documento de PDF, se a assinatura de certificação não for confiável, um triângulo amarelo aparecerá contra a primeira assinatura ao abrir o documento de PDF no Acrobat ou Adobe Reader. A assinatura de certificação deve ser confiável para evitar essa situação.

**Assinando documentos que são formulários baseados em XFA**

Se você tentar assinar um formulário baseado em XFA usando a API do serviço de assinatura, os dados podem estar ausentes do `View` `Signed` `Version` no Acrobat. Por exemplo, considere o seguinte workflow:

* Usando um arquivo XDP criado com o Designer, você mescla um design de formulário que contém um campo de assinatura e dados XML que contêm dados de formulário. Você usa o serviço Forms para gerar um documento PDF interativo.
* Você assina o documento PDF usando a API de serviço de assinatura.

### Resumo das etapas {#summary_of_steps-3}

Para assinar digitalmente um documento PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente do serviço de assinatura.
1. Obtenha o documento PDF para assinar.
1. Assine o documento PDF.
1. Salve o documento PDF assinado como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

**Criar um cliente de assinaturas**

Antes de executar programaticamente uma operação do serviço de Assinatura, você deve criar um cliente do serviço de Assinatura.

**Obter o documento PDF para assinar**

Para assinar um documento PDF, você deve obter um documento PDF que contenha um campo de assinatura. Se um documento PDF não contiver um campo de assinatura, ele não poderá ser assinado. Um campo de assinatura pode ser adicionado usando o Designer ou de forma programática.

**Assinar o documento PDF**

Ao assinar um documento PDF, você pode definir opções de tempo de execução que são usadas pelo serviço de Assinatura. É possível definir as seguintes opções:

* Opções de aparência
* Verificação de revogação
* Valores de carimbo de data e hora

Você define as opções de aparência usando um objeto `PDFSignatureAppearanceOptionSpec`. Por exemplo, você pode exibir a data em uma assinatura chamando o método `setShowDate` do objeto `PDFSignatureAppearanceOptionSpec` e transmitindo `true`.

Você também pode especificar se deve ou não executar uma verificação de revogação que determina se o certificado usado para assinar digitalmente um documento PDF foi revogado. Para executar a verificação de revogação, você pode especificar um dos seguintes valores:

* **NoCheck**: não executar verificação de revogação.
* **BestEffort**: sempre tente verificar a revogação de todos os certificados na cadeia. Se ocorrer algum problema na verificação, a revogação será considerada válida. Se ocorrer alguma falha, considere que o certificado não foi revogado.
* **CheckIfAvailable:** verifique a revogação de todos os certificados na cadeia se as informações de revogação estiverem disponíveis. Se ocorrer algum problema na verificação, presume-se que a revogação é inválida. Se ocorrer alguma falha, considere que o certificado foi revogado e é inválido. (Este é o valor padrão.)
* **AlwaysCheck**: verifique a revogação de todos os certificados na cadeia. Se não houver informações de revogação em nenhum certificado, a revogação será considerada inválida.

Para executar a verificação de revogação em um certificado, você pode especificar uma URL para um servidor de lista de certificados revogados (CRL) usando um objeto `CRLOptionSpec`. No entanto, se você quiser executar a verificação de revogação e não especificar um URL para um servidor CRL, o serviço de Assinatura obterá o URL do certificado.

Em vez de usar um servidor CRL, você pode usar um servidor OCSP (protocolo de status de certificado online) ao executar a verificação de revogação. Normalmente, ao usar um servidor OCSP em vez de um servidor CRL, a verificação de revogação é executada mais rapidamente. (Consulte &quot;Protocolo de Status de Certificados Online&quot; em [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

Você pode definir a ordem do servidor CRL e OCSP que o serviço de Assinatura usa usando Aplicativos e Serviços Adobe. Por exemplo, se o servidor OCSP for definido primeiro em Aplicativos e Serviços Adobe, o servidor OCSP será verificado, seguido pelo servidor CRL. (Consulte &quot;Gerenciar certificados e credenciais usando o Trust Store&quot; na Ajuda da AAC).

Se você optar por não executar a verificação de revogação, o Serviço de assinatura não verificará se o certificado usado para assinar ou certificar um documento foi revogado. Ou seja, as informações do servidor CRL e OCSP são ignoradas.

>[!NOTE]
>
>Embora uma CRL ou um servidor OCSP possa ser especificado no certificado, você pode substituir a URL especificada no certificado usando um objeto `CRLOptionSpec` e `OCSPOptionSpec`. Por exemplo, para substituir o servidor CRL, você pode invocar o método `setLocalURI` do objeto `CRLOptionSpec`.

Carimbo de data e hora refere-se ao processo de rastrear a hora em que um documento assinado ou certificado foi modificado. Depois que um documento é assinado, ele não deve ser modificado, nem mesmo pelo proprietário do documento. O carimbo de data e hora ajuda a impor a validade de um documento assinado ou certificado. Você pode definir opções de carimbo de data/hora usando um objeto `TSPOptionSpec`. Por exemplo, você pode especificar a URL de um servidor TSP (provedor de carimbo de data e hora).

>[!NOTE]
>
>Nas seções de passo a passo do Java e do serviço Web e nas inicializações rápidas correspondentes, a verificação de revogação é usada. Como nenhuma informação do servidor CRL ou OCSP é especificada, as informações do servidor são obtidas do certificado usado para assinar digitalmente o documento PDF.

Para assinar com êxito um documento PDF, você pode especificar o nome totalmente qualificado do campo de assinatura que conterá a assinatura digital, como `form1[0].#subform[1].SignatureField3[3]`. Ao usar um campo de formulário XFA, o nome parcial do campo de assinatura também pode ser usado: `SignatureField3[3]`.

Você também deve fazer referência a uma credencial de segurança para assinar digitalmente um documento PDF. Para fazer referência a uma credencial de segurança, especifique um alias. O alias é uma referência a uma credencial real que pode estar em um arquivo PKCS#12 (com uma extensão .pfx) ou em um módulo de segurança de hardware (HSM). Para obter informações sobre a credencial de segurança, consulte o guia *Instalação e Implantação do AEM Forms* para o seu servidor de aplicativos.

**Salvar o documento PDF assinado**

Depois que o serviço de Assinatura assinar digitalmente o documento PDF, você poderá salvá-lo como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou no Adobe Reader.

**Consulte também**

[Assinar digitalmente documentos PDF usando a API Java](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Assinatura digital de documentos PDF usando a API do serviço Web](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adição de campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields)

[Recuperando nomes de campos de assinatura](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Assinar digitalmente documentos PDF usando a API Java {#digitally-sign-pdf-documents-using-the-java-api}

Assine digitalmente um documento PDF usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signatures-client.jar, no classpath do projeto Java.

1. Criar um cliente de assinaturas

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento PDF para assinar

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF para assinar digitalmente usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Assine o documento PDF

   Assine o documento PDF invocando o método `sign` do objeto `SignatureServiceClient` e transmitindo os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento PDF a ser assinado.
   * Um valor de string que representa o nome do campo de assinatura que conterá a assinatura digital.
   * Um objeto `Credential` que representa a credencial usada para assinar digitalmente o documento PDF. Crie um objeto `Credential` chamando o método `getInstance` estático do objeto `Credential` e transmitindo um valor de cadeia de caracteres que especifica o valor de alias que corresponde à credencial de segurança.
   * Um objeto `HashAlgorithm` que especifica um membro de dados estáticos que representa o algoritmo de hash a ser usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi assinado digitalmente.
   * Um valor de string que representa as informações de contato do signatário.
   * Um objeto `PDFSignatureAppearanceOptions` que controla a aparência da assinatura digital. Por exemplo, você pode usar esse objeto para adicionar um logotipo personalizado a uma assinatura digital.
   * Um objeto `java.lang.Boolean` que especifica se a verificação de revogação no certificado do signatário deve ser executada.
   * Um objeto `OCSPOptionSpec` que armazena preferências para o suporte ao Protocolo de Status de Certificados Online (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `CRLPreferences` que armazena as preferências da lista de certificados revogados (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `TSPPreferences` que armazena preferências para suporte ao provedor de carimbo de data/hora (TSP). Este parâmetro é opcional e pode ser `null`. Para obter mais informações, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   O método `sign` retorna um objeto `com.adobe.idp.Document` que representa o documento PDF assinado.

1. Salve o documento PDF assinado

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` e passe `java.io.File` para copiar o conteúdo do objeto `Document` para o arquivo. Use o objeto `com.adobe.idp.Document` retornado pelo método `sign`.

**Consulte também**

[Assinatura digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Início rápido (modo SOAP): assinatura digital de um documento PDF usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Assinatura digital de documentos PDF usando a API do serviço Web {#digitally-signing-pdf-documents-using-the-web-service-api}

Para assinar digitalmente um documento PDF usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinaturas

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF para assinar

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que está assinado.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF a ser assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo à propriedade `MTOM` o conteúdo da matriz de bytes.

1. Assine o documento PDF

   Assine o documento PDF invocando o método `sign` do objeto `SignatureServiceClient` e transmitindo os seguintes valores:

   * Um objeto `BLOB` que representa o documento PDF a ser assinado.
   * Um valor de string que representa o nome do campo de assinatura que conterá a assinatura digital.
   * Um objeto `Credential` que representa a credencial usada para assinar digitalmente o documento PDF. Crie um objeto `Credential` usando seu construtor e especifique o alias atribuindo um valor à propriedade `alias` do objeto `Credential`.
   * Um objeto `HashAlgorithm` que especifica um membro de dados estáticos que representa o algoritmo de hash a ser usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor booliano que especifica se o algoritmo de hash é usado.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi assinado digitalmente.
   * Um valor de string que representa a localização do signatário.
   * Um valor de string que representa as informações de contato do signatário.
   * Um objeto `PDFSignatureAppearanceOptions` que controla a aparência da assinatura digital. Por exemplo, você pode usar esse objeto para adicionar um logotipo personalizado a uma assinatura digital.
   * Um objeto `System.Boolean` que especifica se a verificação de revogação no certificado do signatário deve ser executada. Se esta verificação de revogação for feita, ela será incorporada na assinatura. O padrão é `false`.
   * Um objeto `OCSPOptionSpec` que armazena preferências para o suporte ao Protocolo de Status de Certificados Online (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`. Para obter informações sobre este objeto, consulte [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Um objeto `CRLPreferences` que armazena as preferências da lista de certificados revogados (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `TSPPreferences` que armazena preferências para suporte ao provedor de carimbo de data/hora (TSP). Este parâmetro é opcional e pode ser `null`.

   O método `sign` retorna um objeto `BLOB` que representa o documento PDF assinado.

1. Salve o documento PDF assinado

   * Crie um objeto `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento de PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `sign`. Popular a matriz de bytes obtendo o valor do membro de dados `MTOM` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Assinatura digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Assinatura digital do Forms interativo {#digitally-signing-interactive-forms}

Você pode assinar um formulário interativo criado pelo serviço Forms. Por exemplo, considere o seguinte workflow:

* Você mescla um formulário PDF baseado em XFA criado usando Designer e dados de formulário em um documento XML usando o serviço Forms. O servidor do Forms renderiza um formulário interativo.
* Você assina o formulário interativo usando a API do serviço de assinatura.

O resultado é um formulário PDF interativo assinado digitalmente. Ao assinar um formulário de PDF baseado em um formulário XFA, salve o arquivo de PDF como um formulário de PDF Estático de Adobe. Se você tentar assinar um formulário de PDF salvo como um formulário de PDF dinâmico de Adobe, ocorrerá uma exceção. Como você está assinando o formulário retornado pelo serviço Forms, verifique se ele contém um campo de assinatura.

>[!NOTE]
>
>Antes de assinar digitalmente um formulário interativo, você deve garantir que adicionou o certificado ao AEM Forms. Um certificado é adicionado usando o console de administração ou de forma programática usando a API do Gerenciador de Confiança. (Consulte [Importar Credenciais usando a API do Gerenciador de Confiança](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Ao usar a API de Serviço Forms, defina a opção de tempo de execução `GenerateServerAppearance` como `true`. Essa opção de tempo de execução garante que a aparência do formulário gerado no servidor permaneça válida quando aberta no Acrobat ou no Adobe Reader. É recomendável definir essa opção de tempo de execução ao gerar um formulário interativo para assinar usando a API do Forms.

>[!NOTE]
>
>Antes de ler Forms interativo com assinatura digital, é recomendável que você esteja familiarizado com a assinatura de documentos PDF. (Consulte [Assinatura digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### Resumo das etapas {#summary_of_steps-4}

Para assinar digitalmente um formulário interativo retornado pelo serviço Forms, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente do Forms e do Sigatures.
1. Obtenha o formulário interativo usando o serviço Forms.
1. Assine o formulário interativo.
1. Salve o documento PDF assinado como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente do Forms e de assinaturas**

Como esse fluxo de trabalho invoca os serviços Forms e Signature, crie um cliente de serviço Forms e um cliente de serviço Signature.

**Obter o formulário interativo usando o serviço Forms**

Você pode usar o serviço Forms para obter o formulário PDF interativo para assinar. A partir do AEM Forms, você pode passar um objeto `com.adobe.idp.Document` para o serviço Forms que contém o formulário a ser renderizado. O nome deste método é `renderPDFForm2`. Este método retorna um objeto `com.adobe.idp.Document` que contém o formulário a ser assinado. Você pode passar esta instância `com.adobe.idp.Document` para o serviço de Assinatura.

Da mesma forma, se estiver usando serviços Web, você pode passar a instância `BLOB` que o serviço Forms retorna para o serviço de Assinatura.

>[!NOTE]
>
>O início rápido associado à seção Forms Interativa com Assinatura Digital invoca o método `renderPDFForm2`.

**Assinar o formulário interativo**

Ao assinar um documento PDF, você pode definir as opções de tempo de execução que o serviço de Assinatura usa. É possível definir as seguintes opções:

* Opções de aparência
* Verificação de revogação
* Valores de carimbo de data e hora

Você define as opções de aparência usando um objeto `PDFSignatureAppearanceOptionSpec`. Por exemplo, você pode exibir a data em uma assinatura chamando o método `setShowDate` do objeto `PDFSignatureAppearanceOptionSpec` e transmitindo `true`.

**Salvar o documento PDF assinado**

Depois que o serviço de Assinatura assinar digitalmente o documento PDF, você poderá salvá-lo como um arquivo PDF. O arquivo PDF pode ser aberto no Acrobat ou no Adobe Reader.

**Consulte também**

[Assinar digitalmente um formulário interativo usando a API do Java](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Assinar digitalmente um formulário interativo usando a API do serviço Web](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assinatura digital de documentos PDF](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Assinar digitalmente um formulário interativo usando a API do Java {#digitally-sign-an-interactive-form-using-the-java-api}

Assine digitalmente um formulário interativo usando o Forms e a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signatures-client.jar e adobe-forms-client.jar, no classpath do projeto Java.

1. Criar um cliente do Forms e de assinaturas

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obter o formulário interativo usando o serviço Forms

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF a ser passado para o serviço Forms usando seu construtor. Transmita um valor de string que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.
   * Crie um objeto `java.io.FileInputStream` que represente o documento XML que contém dados de formulário a serem transmitidos para o serviço Forms usando seu construtor. Transmita um valor de string que especifique o local do arquivo XML.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.
   * Crie um objeto `PDFFormRenderSpec` usado para definir opções de tempo de execução. Invoque o método `setGenerateServerAppearance` do objeto `PDFFormRenderSpec` e passe `true`.
   * Invoque o método `renderPDFForm2` do objeto `FormsServiceClient` e passe os seguintes valores:

      * Um objeto `com.adobe.idp.Document` que contém o formulário PDF a ser renderizado.
      * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário.
      * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução.
      * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms. Você pode especificar `null` para este valor de parâmetro.
      * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

     O método `renderPDFForm2` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário

   * Recupere o formulário PDF invocando o método `getOutputContent` do objeto `FormsResult`. Este método retorna um objeto `com.adobe.idp.Document` que representa o formulário interativo.

1. Assinar o formulário interativo

   Assine o documento PDF invocando o método `sign` do objeto `SignatureServiceClient` e transmitindo os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento PDF a ser assinado. Certifique-se de que este objeto é o objeto `com.adobe.idp.Document` obtido do serviço Forms.
   * Um valor de string que representa o nome do campo de assinatura que está assinado.
   * Um objeto `Credential` que representa a credencial usada para assinar digitalmente o documento PDF. Crie um objeto `Credential` invocando o método `getInstance` estático do objeto `Credential`. Transmita um valor de cadeia de caracteres que especifique o valor de alias que corresponde à credencial de segurança.
   * Um objeto `HashAlgorithm` que especifica um membro de dados estáticos que representa o algoritmo de hash a ser usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi assinado digitalmente.
   * Um valor de string que representa as informações de contato do signatário.
   * Um objeto `PDFSignatureAppearanceOptions` que controla a aparência da assinatura digital. Por exemplo, você pode usar esse objeto para adicionar um logotipo personalizado a uma assinatura digital.
   * Um objeto `java.lang.Boolean` que especifica se a verificação de revogação no certificado do signatário deve ser executada.
   * Um objeto `OCSPPreferences` que armazena preferências para o suporte ao Protocolo de Status de Certificados Online (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `CRLPreferences` que armazena as preferências da lista de certificados revogados (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `TSPPreferences` que armazena preferências para suporte ao provedor de carimbo de data/hora (TSP). Este parâmetro é opcional e pode ser `null`.

   O método `sign` retorna um objeto `com.adobe.idp.Document` que representa o documento PDF assinado.

1. Salve o documento PDF assinado

   * Crie um objeto `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` e passe `java.io.File` para copiar o conteúdo do objeto `Document` para o arquivo. Certifique-se de usar o objeto `com.adobe.idp.Document` retornado pelo método `sign`.

**Consulte também**

[Assinatura digital do Forms interativo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Início rápido (modo SOAP): assinatura digital de um documento PDF usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Assinar digitalmente um formulário interativo usando a API do serviço Web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Assine digitalmente um formulário interativo usando o Forms e a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Como este aplicativo cliente invoca dois serviços AEM Forms, crie duas referências de serviço. Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Assinatura: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Use a seguinte definição WSDL para a referência de serviço associada ao serviço Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Como o tipo de dados `BLOB` é comum a ambas as referências de serviço, qualifique totalmente o tipo de dados `BLOB` ao usá-lo. No início rápido do serviço Web correspondente, todas as `BLOB` instâncias são totalmente qualificadas.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente do Forms e de assinaturas

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita essas etapas para o cliente de serviço Forms.

1. Obter o formulário interativo usando o serviço Forms

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que está assinado.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF a ser assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo à propriedade `MTOM` o conteúdo da matriz de bytes.
   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar dados de formulário.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo XML que contém dados de formulário e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo à propriedade `MTOM` o conteúdo da matriz de bytes.
   * Crie um objeto `PDFFormRenderSpec` usado para definir opções de tempo de execução. Atribua o valor `true` ao campo `generateServerAppearance` do objeto `PDFFormRenderSpec`.
   * Invoque o método `renderPDFForm2` do objeto `FormsServiceClient` e passe os seguintes valores:

      * Um objeto `BLOB` que contém o formulário PDF a ser renderizado.
      * Um objeto `BLOB` que contém dados para mesclar com o formulário.
      * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução.
      * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms. Você pode especificar `null` para este valor de parâmetro.
      * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
      * Um parâmetro de saída longo usado para armazenar o número de páginas no formulário.
      * Um parâmetro de saída de string que é usado para o valor do local.
      * Um valor `FormResult` que é um parâmetro de saída usado para armazenar o formulário interativo.

   * Recupere o formulário PDF invocando o campo `outputContent` do objeto `FormsResult`. Este campo armazena um objeto `BLOB` que representa o formulário interativo.

1. Assinar o formulário interativo

   Assine o documento PDF invocando o método `sign` do objeto `SignatureServiceClient` e transmitindo os seguintes valores:

   * Um objeto `BLOB` que representa o documento PDF a ser assinado. Use a instância `BLOB` retornada pelo serviço Forms.
   * Um valor de string que representa o nome do campo de assinatura que está assinado.
   * Um objeto `Credential` que representa a credencial usada para assinar digitalmente o documento PDF. Crie um objeto `Credential` usando seu construtor e especifique o alias atribuindo um valor à propriedade `alias` do objeto `Credential`.
   * Um objeto `HashAlgorithm` que especifica um membro de dados estáticos que representa o algoritmo de hash a ser usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor booliano que especifica se o algoritmo de hash é usado.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi assinado digitalmente.
   * Um valor de string que representa a localização do signatário.
   * Um valor de string que representa as informações de contato do signatário.
   * Um objeto `PDFSignatureAppearanceOptions` que controla a aparência da assinatura digital. Por exemplo, você pode usar esse objeto para adicionar um logotipo personalizado a uma assinatura digital.
   * Um objeto `System.Boolean` que especifica se a verificação de revogação no certificado do signatário deve ser executada. Se esta verificação de revogação for feita, ela será incorporada na assinatura. O padrão é `false`.
   * Um objeto `OCSPPreferences` que armazena preferências para o suporte ao Protocolo de Status de Certificados Online (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`. Para obter informações sobre este objeto, consulte [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Um objeto `CRLPreferences` que armazena as preferências da lista de certificados revogados (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `TSPPreferences` que armazena preferências para suporte ao provedor de carimbo de data/hora (TSP). Este parâmetro é opcional e pode ser `null`.

   O método `sign` retorna um objeto `BLOB` que representa o documento PDF assinado.

1. Salve o documento PDF assinado

   * Crie um objeto `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento de PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `sign`. Popular a matriz de bytes obtendo o valor do membro de dados `MTOM` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Assinatura digital do Forms interativo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Documentos de PDF de certificação {#certifying-pdf-documents}

Você pode proteger um documento PDF certificando-o com um tipo específico de assinatura chamado assinatura certificada. Uma assinatura certificada distingue-se de uma assinatura digital das seguintes formas:

* Deve ser a primeira assinatura aplicada ao documento PDF; ou seja, no momento em que a assinatura certificada é aplicada, todos os outros campos de assinatura no documento devem ser não assinados. Apenas uma assinatura certificada é permitida em um documento PDF. Se você quiser assinar e certificar um documento PDF, deverá certificá-lo antes de assiná-lo. Após certificar um documento PDF, é possível assinar digitalmente campos de assinatura adicionais.
* O autor ou o originador do documento pode especificar que o documento pode ser modificado de determinadas maneiras sem invalidar a assinatura certificada. Por exemplo, o documento pode permitir o preenchimento de formulários ou comentários. Se o autor especificar que uma determinada modificação não é permitida, o Acrobat restringirá os usuários de modificar o documento dessa maneira. Se essas modificações forem feitas, como ao usar outro aplicativo, a assinatura certificada será inválida e o Acrobat emitirá um aviso quando um usuário abrir o documento. (Com assinaturas não certificadas, as modificações não são impedidas e as operações normais de edição não invalidam a assinatura original.)
* No momento da assinatura, o documento é digitalizado em busca de tipos específicos de conteúdo que possam tornar o conteúdo de um documento ambíguo ou enganoso. Por exemplo, uma anotação pode obscurecer algum texto em uma página que é importante para entender o que está sendo certificado. Pode ser fornecida uma explicação (atestado legal) sobre esse conteúdo.

Você pode certificar documentos PDF de forma programática usando a API Java do serviço de assinatura ou a API do serviço Web de assinatura. Ao certificar um documento PDF, você deve fazer referência a uma credencial de segurança que existe no serviço de credenciais. Para obter informações sobre a credencial de segurança, consulte o guia *Instalação e Implantação do AEM Forms* para o seu servidor de aplicativos.

>[!NOTE]
>
>Ao certificar e assinar o mesmo documento PDF, se a assinatura certificada não for confiável, um triângulo amarelo aparecerá ao lado da primeira assinatura assinada quando você abrir o documento PDF no Acrobat ou Adobe Reader. A assinatura de certificação deve ser confiável para evitar essa situação.

>[!NOTE]
>
>Ao usar uma credencial HSM do nCipher nShield para assinar ou certificar um documento PDF, a nova credencial não pode ser usada até que o servidor de aplicativos J2EE no qual o AEM Forms é implantado seja reiniciado. No entanto, você pode definir um valor de configuração, o que faz com que a operação sign ou certify funcione sem reiniciar o servidor de aplicativos J2EE.

Você pode adicionar o seguinte valor de configuração no arquivo cknfastrc, localizado em /opt/nfast/cknfastrc (ou c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Depois de adicionar esse valor de configuração ao arquivo cknfastrc, a nova credencial pode ser usada sem reiniciar o servidor de aplicativos J2EE.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de assinatura e a certificação de um documento, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-5}

Para certificar um documento PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF para certificar.
1. Certifique o documento PDF.
1. Salve o documento PDF certificado como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação de assinatura, você deve criar um cliente de assinatura.

**Obtenha o documento PDF para certificar**

Para certificar um documento PDF, você deve obter um documento PDF que contenha um campo de assinatura. Se um documento PDF não contiver um campo de assinatura, ele não poderá ser certificado. Um campo de assinatura pode ser adicionado usando o Designer ou de forma programática. Para obter informações sobre como adicionar um campo de assinatura de forma programática, consulte [Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields).

**Certificar o documento PDF**

Para certificar com êxito um documento de PDF, você precisa dos seguintes valores de entrada que são usados pelo serviço de Assinatura para certificar um documento de PDF:

* **documento PDF**: um documento PDF que contém um campo de assinatura, que é um campo de formulário que contém uma representação gráfica da assinatura certificada. Um documento PDF deve conter um campo de assinatura para que possa ser certificado. Um campo de assinatura pode ser adicionado usando o Designer ou de forma programática. (Consulte [Adição De Campos De Assinatura](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **Nome do campo de assinatura**: o nome totalmente qualificado do campo de assinatura certificado. O seguinte valor é um exemplo: `form1[0].#subform[1].SignatureField3[3]`. Ao usar um campo de formulário XFA, o nome parcial do campo de assinatura também pode ser usado: `SignatureField3[3]`. Se um valor nulo for transmitido para o nome do campo, um campo de assinatura invisível será criado e certificado dinamicamente.
* **Credencial de segurança**: uma credencial usada para certificar o documento PDF. Esta credencial de segurança contém uma senha e um alias, que devem corresponder a um alias que aparece na credencial localizada no serviço de credencial. O alias é uma referência a uma credencial real que pode estar em um arquivo PKCS#12 (com uma extensão .pfx) ou em um módulo de segurança de hardware (HSM).
* **Algoritmo de hash**: um algoritmo de hash a ser usado para compilar o documento PDF.
* **Motivo da assinatura**: um valor que é exibido no Acrobat ou no Adobe Reader para que outros usuários saibam o motivo pelo qual o documento PDF foi certificado.
* **Local do signatário**: o local do signatário especificado pela credencial.
* **Informações de contato**: informações de contato, como endereço e número de telefone, do signatário.
* **Informações de permissão**: permissões que controlam as ações que um usuário final pode executar em um documento sem fazer com que a assinatura certificada seja inválida. Por exemplo, você pode definir a permissão para que qualquer alteração no documento PDF faça com que a assinatura certificada seja inválida.
* **Explicação legal**: quando um documento é certificado, ele é automaticamente verificado em busca de tipos específicos de conteúdo que possam tornar o conteúdo de um documento ambíguo ou enganoso. Por exemplo, uma anotação pode obscurecer algum texto em uma página que é importante para entender o que está sendo certificado. O processo de digitalização gera avisos sobre esses tipos de conteúdo. Esse valor fornece uma explicação adicional do conteúdo que pode ter gerado avisos.
* **Opções de aparência**: opções que controlam a aparência da assinatura certificada. Por exemplo, a assinatura certificada pode exibir informações de data.
* **Verificação de revogação**: este valor especifica se a verificação de revogação é feita para o certificado do signatário. A configuração padrão de `false` significa que a verificação de revogação não foi feita.
* **Configurações de OCSP**: configurações para suporte ao protocolo OCSP, que fornece informações sobre o status da credencial usada para certificar o documento PDF. Você pode, por exemplo, especificar o URL do servidor que fornece informações sobre a credencial que você está usando para entrar no documento PDF.
* **Configurações de CRL**: configurações de preferências da lista de certificados revogados (CRL) se a verificação de revogação estiver concluída. Por exemplo, você pode especificar sempre verificar se uma credencial foi revogada.
* **Carimbo de data/hora**: configurações que definem as informações de carimbo de data/hora aplicadas à assinatura certificada. Um carimbo de data e hora indica que dados específicos foram estabelecidos antes de um determinado período. Esse conhecimento ajuda a criar uma relação de confiança entre o signatário e o verificador.

**Salvar o documento PDF certificado como um arquivo PDF**

Depois que o serviço de Assinatura certificar o documento PDF, você poderá salvá-lo como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou no Adobe Reader.

**Consulte também**

[Certificar documentos PDF usando a API Java](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certificar documentos PDF usando a API de serviço Web](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adição de campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certificar documentos PDF usando a API Java {#certify-pdf-documents-using-the-java-api}

Certifique um documento PDF usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signatures-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente de assinatura

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento do PDF para certificar

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF a ser certificado usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Certificar o documento PDF

   Certifique o documento PDF chamando o método `certify` do objeto `SignatureServiceClient` e transmitindo os seguintes valores:

   * O objeto `com.adobe.idp.Document` que representa o documento PDF a ser certificado.
   * Um valor de string que representa o nome do campo de assinatura que conterá a assinatura.
   * Um objeto `Credential` que representa a credencial usada para certificar o documento PDF. Crie um objeto `Credential` chamando o método `getInstance` estático do objeto `Credential` e transmitindo um valor de cadeia de caracteres que especifica o valor de alias que corresponde à credencial de segurança.
   * Um objeto `HashAlgorithm` que especifica um membro de dados estáticos que representa o algoritmo de hash usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi certificado.
   * Um valor de string que representa as informações de contato do signatário.
   * Um objeto `MDPPermissions` que especifica ações que podem ser executadas no documento PDF que invalida a assinatura.
   * Um objeto `PDFSignatureAppearanceOptions` que controla a aparência da assinatura certificada. Se desejar, modifique a aparência da assinatura invocando um método, como `setShowDate`.
   * Um valor de string que fornece uma explicação de quais ações invalidam a assinatura.
   * Um objeto `java.lang.Boolean` que especifica se a verificação de revogação no certificado do signatário deve ser executada. Se esta verificação de revogação for feita, ela será incorporada na assinatura. O padrão é `false`.
   * Um objeto `java.lang.Boolean` que especifica se o campo de assinatura sendo certificado está bloqueado. Se o campo estiver bloqueado, o campo de assinatura é marcado como somente leitura, suas propriedades não podem ser modificadas e não pode ser limpo por ninguém que não tenha as permissões necessárias. O padrão é `false`.
   * Um objeto `OCSPPreferences` que armazena preferências para o suporte ao Protocolo de Status de Certificados Online (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`. Para obter informações sobre este objeto, consulte [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Um objeto `CRLPreferences` que armazena as preferências da lista de certificados revogados (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `TSPPreferences` que armazena preferências para suporte ao provedor de carimbo de data/hora (TSP). Por exemplo, após criar um objeto `TSPPreferences`, você pode definir a URL do servidor TSP chamando o método `setTspServerURL` do objeto `TSPPreferences`. Este parâmetro é opcional e pode ser `null`. Para obter mais informações, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

   O método `certify` retorna um objeto `com.adobe.idp.Document` que representa o documento PDF certificado.

1. Salve o documento PDF certificado como um arquivo PDF

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo.

**Consulte também**

[Documentos de PDF de certificação](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Início rápido (modo SOAP): certificar um documento PDF usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certificar documentos PDF usando a API de serviço Web {#certify-pdf-documents-using-the-web-service-api}

Certifique um documento PDF usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento do PDF para certificar

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que é certificado.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF a ser certificado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo ao membro de dados `MTOM` o conteúdo da matriz de bytes.

1. Certificar o documento PDF

   Certifique o documento PDF chamando o método `certify` do objeto `SignatureServiceClient` e transmitindo os seguintes valores:

   * O objeto `BLOB` que representa o documento PDF a ser certificado.
   * Um valor de string que representa o nome do campo de assinatura que conterá a assinatura.
   * Um objeto `Credential` que representa a credencial usada para certificar o documento PDF. Crie um objeto `Credential` usando seu construtor e especifique o alias atribuindo um valor à propriedade `alias` do objeto `Credential`.
   * Um objeto `HashAlgorithm` que especifica um membro de dados estáticos que representa o algoritmo de hash usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor booliano que especifica se o algoritmo de hash é usado.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi certificado.
   * Um valor de string que representa a localização do signatário.
   * Um valor de string que representa as informações de contato do signatário.
   * Membro de dados estáticos de um objeto `MDPPermissions` que especifica ações que podem ser executadas no documento PDF que invalidam a assinatura.
   * Um valor booliano que especifica se o objeto `MDPPermissions` passado como o valor de parâmetro anterior deve ser usado.
   * Um valor de string que explica quais ações invalidam a assinatura.
   * Um objeto `PDFSignatureAppearanceOptions` que controla a aparência da assinatura certificada. Crie um objeto `PDFSignatureAppearanceOptions` usando seu construtor. Você pode modificar a aparência da assinatura definindo um de seus membros de dados.
   * Um objeto `System.Boolean` que especifica se a verificação de revogação no certificado do signatário deve ser executada. Se esta verificação de revogação for feita, ela será incorporada na assinatura. O padrão é `false`.
   * Um objeto `System.Boolean` que especifica se o campo de assinatura sendo certificado está bloqueado. Se o campo estiver bloqueado, o campo de assinatura é marcado como somente leitura, suas propriedades não podem ser modificadas e não pode ser limpo por ninguém que não tenha as permissões necessárias. O padrão é `false`.
   * Um objeto `System.Boolean` que especifica se o campo de assinatura está bloqueado. Ou seja, se você passar `true` para o parâmetro anterior, então passar `true` para esse parâmetro.
   * Um objeto `OCSPPreferences` que armazena preferências para o suporte ao Protocolo de Status de Certificados Online (OCSP), que fornece informações sobre o status da credencial usada para certificar o documento PDF. Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `CRLPreferences` que armazena as preferências da lista de certificados revogados (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `TSPPreferences` que armazena preferências para suporte ao provedor de carimbo de data/hora (TSP). Por exemplo, após criar um objeto `TSPPreferences`, você pode definir a URL do TSP definindo o membro de dados `tspServerURL` do objeto `TSPPreferences`. Este parâmetro é opcional e pode ser `null`.

   O método `certify` retorna um objeto `BLOB` que representa o documento PDF certificado.

1. Salve o documento PDF certificado como um arquivo PDF

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF que conterá o documento de PDF certificado e o modo no qual abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `certify`. Popular a matriz de bytes obtendo o valor do membro de dados `binaryData` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Documentos de PDF de certificação](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificação de assinaturas digitais {#verifying-digital-signatures}

As assinaturas digitais podem ser verificadas para garantir que um documento PDF assinado não foi modificado e que a assinatura digital é válida. Ao verificar uma assinatura digital, você pode verificar o status da assinatura e suas propriedades, como a identidade do assinante. Antes de confiar em uma assinatura digital, é recomendável verificá-la. Ao verificar uma assinatura digital, consulte um documento PDF que contenha uma assinatura digital.

Suponha que a identidade do signatário seja desconhecida. Quando você abre o documento PDF no Acrobat, uma mensagem de aviso declara que a identidade do signatário é desconhecida, como mostrado na ilustração a seguir.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

Da mesma forma, ao verificar programaticamente uma assinatura digital, é possível determinar o status da identidade do signatário. Por exemplo, se você verificar a assinatura digital no documento mostrado na ilustração anterior, o resultado seria que a identidade do signatário é desconhecida.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Assinatura e a verificação de assinaturas digitais, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-6}

Para verificar uma assinatura digital, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém a assinatura a ser verificada.
1. Definir opções de tempo de execução de PKI.
1. Verifique a assinatura digital.
1. Determine o status da assinatura.
1. Determine a identidade do signatário.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação do serviço de Assinatura, crie um cliente do serviço de Assinatura.

**Obtenha o documento PDF que contém a assinatura a ser verificada**

Para verificar uma assinatura usada para assinar digitalmente ou certificar um documento PDF, obtenha um documento PDF que contenha uma assinatura.

**Definir opções de tempo de execução de PKI**

Defina estas opções de tempo de execução de PKI que o serviço de Assinatura usa ao verificar assinaturas em um documento PDF:

* Tempo de verificação
* Verificação de revogação
* Valores de carimbo de data e hora

Como parte da configuração dessas opções, você pode especificar o tempo de verificação. Por exemplo, você pode selecionar a hora atual (a hora no computador do validador), que indica a utilização da hora atual. Para obter informações sobre os diferentes valores de hora, consulte o valor de enumeração `VerificationTime` na [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Você também pode especificar se deseja executar a verificação de revogação como parte do processo de verificação. Por exemplo, você pode executar uma verificação de revogação para determinar se o certificado foi revogado. Para obter informações sobre as opções de verificação de revogação, consulte o valor de enumeração `RevocationCheckStyle` na [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Para executar a verificação de revogação em um certificado, especifique uma URL para um servidor de lista de certificados revogados (CRL) usando um objeto `CRLOptionSpec`. No entanto, se você não especificar um URL para o servidor da CRL, o serviço de Assinatura obterá o URL do certificado.

Em vez de usar um servidor CRL, você pode usar um servidor OCSP (protocolo de status de certificado online) ao executar a verificação de revogação. Normalmente, ao usar um servidor OCSP em vez de um servidor CRL, a verificação de revogação é executada mais rapidamente. (Consulte [Protocolo de Status de Certificados Online](https://tools.ietf.org/html/rfc2560).)

Você pode definir a ordem do servidor CRL e OCSP que o serviço de Assinatura usa usando Aplicativos e Serviços Adobe. Por exemplo, se o servidor OCSP for definido primeiro em Aplicativos e Serviços Adobe, o servidor OCSP será verificado, seguido pelo servidor CRL.

Se você não executar a verificação de revogação, o Serviço de assinatura não verificará se o certificado foi revogado. Ou seja, as informações do servidor CRL e OCSP são ignoradas.

>[!NOTE]
>
>Você pode substituir a URL especificada no certificado usando um objeto `CRLOptionSpec` e `OCSPOptionSpec`. Por exemplo, para substituir o servidor CRL, você pode invocar o método `setLocalURI` do objeto `CRLOptionSpec`.

Carimbo de data e hora é o processo de rastrear a hora em que um documento assinado ou certificado foi modificado. Depois que um documento é assinado, ninguém pode modificá-lo. O carimbo de data e hora ajuda a impor a validade de um documento assinado ou certificado. Você pode definir opções de carimbo de data/hora usando um objeto `TSPOptionSpec`. Por exemplo, você pode especificar a URL de um servidor TSP (provedor de carimbo de data e hora).

>[!NOTE]
>
>Nas inicializações rápidas do Java e do serviço Web, a hora de verificação está definida como `VerificationTime.CURRENT_TIME` e a verificação de revogação está definida como `RevocationCheckStyle.BestEffort`. Como nenhuma informação do servidor CRL ou OCSP é especificada, as informações do servidor são obtidas do certificado.

**Verificar a assinatura digital**

Para verificar uma assinatura com êxito, especifique o nome totalmente qualificado do campo de assinatura que contém a assinatura, como `form1[0].#subform[1].SignatureField3[3]`. Ao usar um campo de formulário XFA, você também pode usar o nome parcial do campo de assinatura: `SignatureField3`.

Por padrão, o serviço de Assinatura limita para 65 minutos o tempo que um documento pode ser assinado após o tempo de validação. Se um usuário tentar verificar uma assinatura na hora atual e a hora da assinatura for posterior à hora atual e estiver dentro de 65 minutos, o serviço de Assinatura não criará um erro de verificação.

>[!NOTE]
>
>Para outros valores necessários ao verificar uma assinatura, consulte a [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Determinar o status da assinatura**

Como parte da verificação de uma assinatura digital, você pode verificar o status da assinatura.

**Determinar a identidade do signatário**

Você pode determinar a identidade do signatário, que pode ser um dos seguintes valores:

* **Desconhecido**: este signatário é desconhecido porque a verificação do signatário não pode ser executada.
* **Confiável**: este signatário é confiável.
* **Não confiável**: este signatário não é confiável.

**Consulte também**

[Verificar assinaturas digitais usando a API Java](#verify-digital-signatures-using-the-java-api)

[Verificar assinaturas digitais usando a API do serviço Web](#verify-digital-signatures-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar assinaturas digitais usando a API Java {#verify-digital-signatures-using-the-java-api}

Verifique uma assinatura digital usando a API do serviço de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signatures-client.jar, no classpath do projeto Java.

1. Criar um cliente de assinatura

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento PDF que contém a assinatura a ser verificada

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF que contém a assinatura a ser verificada usando seu construtor. Transmita um valor de string que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Definir opções de tempo de execução de PKI

   * Crie um objeto `PKIOptions` usando seu construtor.
   * Defina a hora da verificação invocando o método `setVerificationTime` do objeto `PKIOptions` e transmitindo um valor de enumeração `VerificationTime` que especifica a hora da verificação.
   * Defina a opção de verificação de revogação invocando o método `setRevocationCheckStyle` do objeto `PKIOptions` e transmitindo um valor de enumeração `RevocationCheckStyle` que especifica se deve ser executada uma verificação de revogação.

1. Verificar a assinatura digital

   Verifique a assinatura chamando o método `verify2` do objeto `SignatureServiceClient` e transmitindo os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que contém um documento PDF assinado digitalmente ou certificado.
   * Um valor de string que representa o nome do campo de assinatura que contém a assinatura a ser verificada.
   * Um objeto `PKIOptions` que contém opções de tempo de execução de PKI.
   * Uma instância `VerifySPIOptions` que contém informações SPI. Você pode especificar `null` para este parâmetro.

   O método `verify2` retorna um objeto `PDFSignatureVerificationInfo` que contém informações que podem ser usadas para verificar a assinatura digital.

1. Determinar o status da assinatura

   * Determine o status da assinatura invocando o método `getStatus` do objeto `PDFSignatureVerificationInfo`. Este método retorna um objeto `SignatureStatus` que especifica o status da assinatura. Por exemplo, se um documento PDF assinado não for modificado, esse método retornará `SignatureStatus.DocumentSigNoChanges`.

1. Determinar a identidade do signatário

   * Determine a identidade do signatário invocando o método `getSigner` do objeto `PDFSignatureVerificationInfo`. Este método retorna um objeto `IdentityInformation`.
   * Invoque o método `getStatus` do objeto `IdentityInformation` para determinar a identidade do signatário. Este método retorna um valor de enumeração `IdentityStatus` que especifica a identidade. Por exemplo, se o signatário for confiável, esse método retornará `IdentityStatus.TRUSTED`.

**Consulte também**

[Verificação de assinaturas digitais](#verify-digital-signatures-using-the-java-api)

[Início rápido (modo SOAP): verificação de uma assinatura digital usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar assinaturas digitais usando a API do serviço Web {#verify-digital-signatures-using-the-web-service-api}

Verifique uma assinatura digital usando a API do Serviço de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF que contém a assinatura a ser verificada

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que contém uma assinatura digital ou certificada para verificação.
   * Crie um objeto `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento de PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo à propriedade `MTOM` o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução de PKI

   * Crie um objeto `PKIOptions` usando seu construtor.
   * Defina o tempo de verificação atribuindo ao membro de dados `verificationTime` do objeto `PKIOptions` um valor de enumeração `VerificationTime` que especifique o tempo de verificação.
   * Defina a opção de verificação de revogação atribuindo ao membro de dados `revocationCheckStyle` do objeto `PKIOptions` um valor de enumeração `RevocationCheckStyle` que especifique se a verificação de revogação deve ser executada.

1. Verificar a assinatura digital

   Verifique a assinatura chamando o método `verify2` do objeto `SignatureServiceClient` e transmitindo os seguintes valores:

   * O objeto `BLOB` que contém um documento PDF assinado digitalmente ou certificado.
   * Um valor de string que representa o nome do campo de assinatura que contém a assinatura a ser verificada.
   * Um objeto `PKIOptions` que contém opções de tempo de execução de PKI.
   * Uma instância `VerifySPIOptions` que contém informações SPI. Você pode especificar `null` para este parâmetro.

   O método `verify2` retorna um objeto `PDFSignatureVerificationInfo` que contém informações que podem ser usadas para verificar a assinatura digital.

1. Determinar o status da assinatura

   Determine o status da assinatura obtendo o valor do membro de dados `status` do objeto `PDFSignatureVerificationInfo`. Este membro de dados armazena um objeto `SignatureStatus` que especifica o status da assinatura. Por exemplo, se um documento PDF assinado for modificado, o membro de dados `status` armazenará o valor `SignatureStatus.DocumentSigNoChanges`.

1. Determinar a identidade do signatário

   * Determine a identidade do signatário recuperando o valor do membro de dados `signer` do objeto `PDFSignatureVerificationInfo`. Este membro retorna um objeto `IdentityInformation`.
   * Recupere o membro de dados `status` do objeto `IdentityInformation` para determinar a identidade do signatário. Este membro de dados retorna um valor de enumeração `IdentityStatus` que especifica a identidade. Por exemplo, se o signatário for confiável, esse membro retornará `IdentityStatus.TRUSTED`.

**Consulte também**

[Verificação de assinaturas digitais](#verify-digital-signatures-using-the-java-api)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificação de várias assinaturas digitais {#verifying-multiple-digital-signatures}

O AEM Forms fornece o meio de verificar todas as assinaturas digitais que estão em um documento PDF. Suponha que um documento PDF contenha várias assinaturas digitais como resultado de um processo comercial que requer assinaturas de vários signatários. Por exemplo, considere uma transação financeira que requer a assinatura de um gerente e de um gerente de empréstimo. Você pode usar a API Java do serviço de assinatura ou a API do serviço da Web para verificar todas as assinaturas no documento do PDF. Ao verificar várias assinaturas digitais, você pode verificar o status e as propriedades de cada assinatura. Antes de confiar em uma assinatura digital, é recomendável verificá-la. É recomendável que você esteja familiarizado com a verificação de uma única assinatura digital.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Assinatura e a verificação de assinaturas digitais, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-7}

Para verificar várias assinaturas digitais, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém as assinaturas a serem verificadas.
1. Definir opções de tempo de execução de PKI.
1. Recuperar todas as assinaturas digitais.
1. Repita todas as assinaturas.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação do serviço de Assinatura, crie um cliente do serviço de Assinatura.

**Obtenha o documento PDF que contém as assinaturas a serem verificadas**

Para verificar uma assinatura usada para assinar digitalmente ou certificar um documento PDF, obtenha um documento PDF que contenha uma assinatura.

**Definir opções de tempo de execução de PKI**

Defina estas opções de tempo de execução de PKI que o serviço de Assinatura usa ao verificar todas as assinaturas em um documento PDF:

* Tempo de verificação
* Verificação de revogação
* Valores de carimbo de data e hora

Como parte da configuração dessas opções, você pode especificar o tempo de verificação. Por exemplo, você pode selecionar a hora atual (a hora no computador do validador), que indica a utilização da hora atual. Para obter informações sobre os diferentes valores de hora, consulte o valor de enumeração `VerificationTime` na [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Você também pode especificar se deseja executar a verificação de revogação como parte do processo de verificação. Por exemplo, você pode executar uma verificação de revogação para determinar se o certificado foi revogado. Para obter informações sobre as opções de verificação de revogação, consulte o valor de enumeração `RevocationCheckStyle` na [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Para executar a verificação de revogação em um certificado, especifique uma URL para um servidor de lista de certificados revogados (CRL) usando um objeto `CRLOptionSpec`. No entanto, se você não especificar um URL para um servidor CRL, o serviço de Assinatura obterá o URL do certificado.

Em vez de usar um servidor CRL, você pode usar um servidor OCSP (protocolo de status de certificado online) ao executar a verificação de revogação. Normalmente, ao usar um servidor OCSP em vez de um servidor CRL, a verificação de revogação é executada mais rapidamente. (Consulte [Protocolo de Status de Certificados Online](https://tools.ietf.org/html/rfc2560).)

Você pode definir a ordem do servidor CRL e OCSP que o serviço de Assinatura usa usando Aplicativos e Serviços Adobe. Por exemplo, se o servidor OCSP for definido primeiro em Aplicativos e Serviços Adobe, o servidor OCSP será verificado, seguido pelo servidor CRL.

Se você não executar a verificação de revogação, o Serviço de assinatura não verificará se o certificado foi revogado. Ou seja, as informações do servidor CRL e OCSP são ignoradas.

>[!NOTE]
>
>Você pode substituir a URL especificada no certificado usando um objeto `CRLOptionSpec` e `OCSPOptionSpec`. Por exemplo, para substituir o servidor CRL, você pode invocar o método `setLocalURI` do objeto `CRLOptionSpec`.

Carimbo de data e hora é o processo de rastrear a hora em que um documento assinado ou certificado foi modificado. Depois que um documento é assinado, ninguém pode modificá-lo. O carimbo de data e hora ajuda a impor a validade de um documento assinado ou certificado. Você pode definir opções de carimbo de data/hora usando um objeto `TSPOptionSpec`. Por exemplo, você pode especificar a URL de um servidor TSP (provedor de carimbo de data e hora).

>[!NOTE]
>
>Nas inicializações rápidas do Java e do serviço Web, a hora de verificação está definida como `VerificationTime.CURRENT_TIME` e a verificação de revogação está definida como `RevocationCheckStyle.BestEffort`. Como nenhuma informação do servidor CRL ou OCSP é especificada, as informações do servidor são obtidas do certificado.

**Recuperar todas as assinaturas digitais**

Para verificar todas as assinaturas digitais em um documento PDF, recupere as assinaturas digitais do documento PDF. Todas as assinaturas são retornadas em uma lista. Como parte da verificação de uma assinatura digital, verifique o status da assinatura.

>[!NOTE]
>
>Ao contrário da verificação de uma única assinatura digital, ao verificar várias assinaturas, não é necessário especificar o nome do campo de assinatura.

**Iterar todas as assinaturas**

Repita em cada assinatura. Ou seja, para cada assinatura, verifique a assinatura digital e a identidade do signatário e o status de cada assinatura. (Consulte [Verificação de assinaturas digitais](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>Não é necessário iterar em todas as assinaturas se o requisito for o documento inteiro.

**Consulte também**

[Verificar várias assinaturas digitais usando a API Java](#verify-digital-signatures-using-the-java-api)

[Verificação de várias assinaturas digitais usando a API do serviço Web](#verify-digital-signatures-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar várias assinaturas digitais usando a API Java {#verify-multiple-digital-signatures-using-the-java-api}

Verifique várias assinaturas digitais usando a API de serviço de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signatures-client.jar, no classpath do projeto Java.

1. Criar um cliente de assinatura

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento PDF que contém as assinaturas a serem verificadas

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF que contém várias assinaturas digitais a serem verificadas usando seu construtor. Transmita um valor de string que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Definir opções de tempo de execução de PKI

   * Crie um objeto `PKIOptions` usando seu construtor.
   * Defina a hora da verificação invocando o método `setVerificationTime` do objeto `PKIOptions` e transmitindo um valor de enumeração `VerificationTime` que especifica a hora da verificação.
   * Defina a opção de verificação de revogação invocando o método `setRevocationCheckStyle` do objeto `PKIOptions` e transmitindo um valor de enumeração `RevocationCheckStyle` que especifica se deve ser executada uma verificação de revogação.

1. Recuperar todas as assinaturas digitais

   Invoque o método `verifyPDFDocument` do objeto `SignatureServiceClient` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que contém um documento PDF que contém várias assinaturas digitais.
   * Um objeto `PKIOptions` que contém opções de tempo de execução de PKI.
   * Uma instância `VerifySPIOptions` que contém informações SPI. Você pode especificar `null` para este parâmetro.

   O método `verifyPDFDocument` retorna um objeto `PDFDocumentVerificationInfo` que contém informações sobre todas as assinaturas digitais no documento PDF.

1. Iterar em todas as assinaturas

   * Repita todas as assinaturas invocando o método `getVerificationInfos` do objeto `PDFDocumentVerificationInfo`. Este método retorna um objeto `java.util.List` em que cada elemento é um objeto `PDFSignatureVerificationInfo`. Use um objeto `java.util.Iterator` para iterar através da lista de assinaturas.
   * Usando o objeto `PDFSignatureVerificationInfo`, você pode executar tarefas como determinar o status da assinatura chamando o método `getStatus` do objeto `PDFSignatureVerificationInfo`. Este método retorna um objeto `SignatureStatus` cujo membro de dados estáticos informa sobre o status da assinatura. Por exemplo, se a assinatura for desconhecida, esse método retornará `SignatureStatus.DocumentSignatureUnknown`.

**Consulte também**

[Verificação de várias assinaturas digitais](#verifying-multiple-digital-signatures)

[Início rápido (modo SOAP): verificação de várias assinaturas digitais usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Verificação de assinaturas digitais](#verify-digital-signatures-using-the-java-api)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificação de várias assinaturas digitais usando a API do serviço Web {#verifying-multiple-digital-signatures-using-the-web-service-api}

Verificar várias assinaturas digitais usando a API de Serviço de Assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF que contém as assinaturas a serem verificadas

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` armazena um documento PDF que contém várias assinaturas digitais a serem verificadas.
   * Crie um objeto `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo à propriedade `MTOM` o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução de PKI

   * Crie um objeto `PKIOptions` usando seu construtor.
   * Defina o tempo de verificação atribuindo ao membro de dados `verificationTime` do objeto `PKIOptions` um valor de enumeração `VerificationTime` que especifique o tempo de verificação.
   * Defina a opção de verificação de revogação atribuindo ao membro de dados `revocationCheckStyle` do objeto `PKIOptions` um valor de enumeração `RevocationCheckStyle` que especifique se a verificação de revogação deve ser executada.

1. Recuperar todas as assinaturas digitais

   Invoque o método `verifyPDFDocument` do objeto `SignatureServiceClient` e passe os seguintes valores:

   * Um objeto `BLOB` que contém um documento PDF que contém várias assinaturas digitais.
   * Um objeto `PKIOptions` que contém opções de tempo de execução de PKI.
   * Uma instância `VerifySPIOptions` que contém informações SPI. Você pode especificar nulo para este parâmetro.

   O método `verifyPDFDocument` retorna um objeto `PDFDocumentVerificationInfo` que contém informações sobre todas as assinaturas digitais no documento PDF.

1. Iterar em todas as assinaturas

   * Repita todas as assinaturas obtendo o membro de dados `verificationInfos` do objeto `PDFDocumentVerificationInfo`. Este membro de dados retorna uma matriz `Object` em que cada elemento é um objeto `PDFSignatureVerificationInfo`.
   * Usando o objeto `PDFSignatureVerificationInfo`, você pode executar tarefas como determinar o status da assinatura obtendo o membro de dados `status` do objeto `PDFSignatureVerificationInfo`. Este membro de dados retorna um objeto `SignatureStatus` cujo membro de dados estático informa sobre o status da assinatura. Por exemplo, se a assinatura for desconhecida, esse método retornará `SignatureStatus.DocumentSignatureUnknown`.

**Consulte também**

[Verificação de várias assinaturas digitais](#verifying-multiple-digital-signatures)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Remoção de assinaturas digitais {#removing-digital-signatures}

As assinaturas digitais devem ser removidas de um campo de assinatura para que uma assinatura digital mais recente possa ser aplicada. Uma assinatura digital não pode ser substituída. Se você tentar aplicar uma assinatura digital a um campo de assinatura que contém uma assinatura, ocorrerá uma exceção.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de assinatura, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-8}

Para remover uma assinatura digital de um campo de assinatura, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém uma assinatura para remover.
1. Remova a assinatura digital do campo de assinatura.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação do serviço de Assinatura, você deve criar um cliente do serviço de Assinatura.

**Obter o documento PDF que contém uma assinatura a ser removida**

Para remover uma assinatura de um documento PDF, você deve obter um documento PDF que contenha uma assinatura.

**Remover a assinatura digital do campo de assinatura**

Para remover com êxito uma assinatura digital de um documento PDF, você deve especificar o nome do campo de assinatura que contém a assinatura digital. Além disso, você deve ter permissão para remover a assinatura digital; caso contrário, ocorrerá uma exceção.

**Salvar o documento PDF como um arquivo PDF**

Depois que o serviço de Assinatura remover uma assinatura digital de um campo de assinatura, você poderá salvar o documento PDF como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou no Adobe Reader.

**Consulte também**

[Remover assinaturas digitais usando a API Java](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Remover assinaturas digitais usando a API de serviço Web](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adição de campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields)

### Remover assinaturas digitais usando a API Java {#remove-digital-signatures-using-the-java-api}

Remova uma assinatura digital usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signatures-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente de assinatura.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento PDF que contém uma assinatura a ser removida

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF que contém a assinatura a ser removida usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Remover a assinatura digital do campo de assinatura

   Remova uma assinatura digital de um campo de assinatura invocando o método `clearSignatureField` do objeto `SignatureServiceClient` e transmitindo os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento PDF que contém a assinatura a ser removida.
   * Um valor de cadeia de caracteres que especifica o nome do campo de assinatura que contém a assinatura digital.

   O método `clearSignatureField` retorna um objeto `com.adobe.idp.Document` que representa o documento PDF do qual a assinatura digital foi removida.

1. Salve o documento PDF como um arquivo PDF

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document`. Passe o objeto `java.io.File` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo. Use o objeto `Document` retornado pelo método `clearSignatureField`.

**Consulte também**

[Remoção de assinaturas digitais](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Início rápido (modo SOAP): remoção de uma assinatura digital usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Remover assinaturas digitais usando a API de serviço Web {#remove-digital-signatures-using-the-web-service-api}

Remova uma assinatura digital usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF que contém uma assinatura a ser removida

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que contém uma assinatura digital a ser removida.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` com o conteúdo da matriz de bytes.

1. Remover a assinatura digital do campo de assinatura

   Remova a assinatura digital chamando o método `clearSignatureField` do objeto `SignatureServiceClient` e transmitindo os seguintes valores:

   * Um objeto `BLOB` que contém o documento PDF assinado.
   * Um valor de string que representa o nome do campo de assinatura que contém a assinatura digital a ser removida.

   O método `clearSignatureField` retorna um objeto `BLOB` que representa o documento PDF do qual a assinatura digital foi removida.

1. Salve o documento PDF como um arquivo PDF

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF que contém um campo de assinatura vazio e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `sign`. Popular a matriz de bytes obtendo o valor do membro de dados `MTOM` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes no arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Remoção de assinaturas digitais](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
