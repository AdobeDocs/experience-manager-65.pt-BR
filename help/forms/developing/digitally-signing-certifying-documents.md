---
title: Assinando e certificando Documentos digitalmente
seo-title: Assinando e certificando Documentos digitalmente
description: Use o serviço de assinatura para adicionar e excluir campos de assinatura digital em um documento PDF, recuperar os nomes dos campos de assinatura localizados em um documento PDF, modificar campos de assinatura, assinar documentos PDF digitalmente, certificar documentos PDF, validar assinaturas digitais localizadas em um documento PDF, validar todas as assinaturas digitais localizadas em um documento PDF e remover uma assinatura digital de um campo de assinatura.
seo-description: Use o serviço de assinatura para adicionar e excluir campos de assinatura digital em um documento PDF, recuperar os nomes dos campos de assinatura localizados em um documento PDF, modificar campos de assinatura, assinar documentos PDF digitalmente, certificar documentos PDF, validar assinaturas digitais localizadas em um documento PDF, validar todas as assinaturas digitais localizadas em um documento PDF e remover uma assinatura digital de um campo de assinatura.
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '17099'
ht-degree: 0%

---


# Assinando e certificando Documentos digitalmente {#digitally-signing-and-certifying-documents}

**Sobre o serviço de assinatura**

O serviço de assinatura permite que sua organização proteja a segurança e a privacidade dos documentos Adobe PDF que ele distribui e recebe. Esse serviço usa assinaturas digitais e certificação para garantir que somente os recipient pretendidos possam alterar documentos. Como os recursos de segurança são aplicados ao próprio documento, ele permanece protegido e controlado por todo o seu ciclo de vida. Um documento permanece protegido além do firewall, quando é baixado offline e quando é enviado de volta à sua organização.

>[!NOTE]
>
>Você pode criar um manipulador de assinatura personalizado para o serviço de Assinatura chamado quando determinadas operações são invocadas, como assinar um documento PDF.

**Nomes de campos de assinatura**

Algumas operações do serviço de assinatura exigem que você especifique o nome do campo de assinatura no qual uma operação é executada. Por exemplo, ao assinar um documento PDF, especifique o nome do campo de assinatura a ser assinado. Suponha que o nome completo de um campo de assinatura seja `form1[0].Form1[0].SignatureField1[0]`. Você pode especificar `SignatureField1[0]` em vez de `form1[0].Form1[0].SignatureField1[0]`.

Às vezes, um conflito faz com que o serviço de assinatura assine (ou execute outra operação que exija o nome do campo de assinatura) o campo errado. Esse conflito resulta da exibição do nome `SignatureField1[0]` em dois ou mais lugares no mesmo documento PDF. Por exemplo, considere um documento PDF que contenha dois campos de assinatura chamados `form1[0].Form1[0].SignatureField1[0]` e `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` e especifique `SignatureField1[0]`. Nessa situação, o serviço de assinatura assina o primeiro campo de assinatura encontrado ao iterar sobre todos os campos de assinatura no documento.

Se houver vários campos de assinatura localizados em um documento PDF, é recomendável especificar os nomes completos dos campos de assinatura. Ou seja, especifique `form1[0].Form1[0].SignatureField1[0]`em vez de `SignatureField1[0]`.

É possível realizar essas tarefas usando o serviço de assinatura:

* Adicione e exclua campos de assinatura digital a um documento PDF. (Consulte [Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields).)
* Recupere os nomes dos campos de assinatura localizados em um documento PDF. (Consulte [Recuperando Nomes de Campos de Assinatura](digitally-signing-certifying-documents.md#retrieving-signature-field-names).)
* Modifique os campos de assinatura. (Consulte [Modificando campos de assinatura](digitally-signing-certifying-documents.md#modifying-signature-fields).)
* Assine digitalmente documentos PDF. (Consulte [Assinando Documentos PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* Certificar documentos PDF. (Consulte [Certificando Documentos PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* Valide as assinaturas digitais localizadas em um documento PDF. (Consulte [Verificando Assinaturas Digitais](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Valide todas as assinaturas digitais localizadas em um documento PDF. (Consulte [Verificando várias assinaturas digitais](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* Remova uma assinatura digital de um campo de assinatura. (Consulte [Remoção de Assinaturas Digitais](digitally-signing-certifying-documents.md#removing-digital-signatures).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Adicionar campos de assinatura {#adding-signature-fields}

As assinaturas digitais aparecem nos campos de assinatura, que são campos de formulário que contêm uma representação gráfica da assinatura. Os campos de assinatura podem ser visíveis ou invisíveis. Os signatários podem usar um campo de assinatura preexistente ou um campo de assinatura pode ser adicionado de forma programática. Em ambos os casos, o campo de assinatura deve existir antes que um documento PDF possa ser assinado.

Você pode adicionar um campo de assinatura de forma programática usando a API Java do serviço de assinatura ou a API do serviço da Web de assinatura. É possível adicionar mais de um campo de assinatura a um documento PDF; no entanto, cada nome de campo de assinatura deve ser exclusivo.

>[!NOTE]
>
>Alguns tipos de documentos PDF não permitem que você adicione um campo de assinatura de forma programática. Para obter mais informações sobre o serviço de assinatura e como adicionar campos de assinatura, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para adicionar um campo de assinatura a um documento PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
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
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação de serviço de assinatura, você deve criar um cliente de serviço de assinatura.

**Obter um documento PDF ao qual um campo de assinatura é adicionado**

É necessário obter um documento PDF ao qual um campo de assinatura é adicionado.

**Adicionar um campo de assinatura**

Para adicionar com êxito um campo de assinatura a um documento PDF, especifique valores de coordenadas que identificam o local do campo de assinatura. (Se você adicionar um campo de assinatura invisível, esses valores não serão obrigatórios.) Além disso, você pode especificar quais campos no documento PDF serão bloqueados depois que uma assinatura for aplicada ao campo de assinatura.

**Salvar o documento PDF como um arquivo PDF**

Depois que o serviço de assinatura adicionar um campo de assinatura ao documento PDF, você poderá salvar o documento como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou Adobe Reader.

**Consulte também:**

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assinando Documentos PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Adicionar campos de assinatura usando a API Java {#add-signature-fields-using-the-java-api}

Adicione um campo de assinatura usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signature-client.jar, no classpath do seu projeto Java.

1. Criar um cliente de assinatura

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obter um documento PDF ao qual um campo de assinatura é adicionado

   * Crie um objeto `java.io.FileInputStream` que representa o documento PDF ao qual um campo de assinatura é adicionado usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Adicionar um campo de assinatura

   * Crie um objeto `PositionRectangle` que especifique o local do campo de assinatura usando seu construtor. No construtor, especifique os valores de coordenadas.
   * Se desejar, crie um objeto `FieldMDPOptions` que especifique os campos que estão bloqueados quando uma assinatura digital for aplicada ao campo de assinatura.
   * Adicione um campo de assinatura a um documento PDF chamando o método `SignatureServiceClient` do objeto `addSignatureField` e transmitindo os seguintes valores:

      * A `com.adobe.idp`. `Document` objeto que representa o documento PDF ao qual um campo de assinatura é adicionado.
      * Um valor de string que especifica o nome do campo de assinatura.
      * Um valor `java.lang.Integer` que representa o número da página à qual um campo de assinatura é adicionado.
      * Um objeto `PositionRectangle` que especifica o local do campo de assinatura.
      * Um objeto `FieldMDPOptions` que especifica campos no documento PDF que são bloqueados depois que uma assinatura digital é aplicada ao campo de assinatura. Esse valor de parâmetro é opcional e você pode passar `null`.
   * Um objeto `PDFSeedValueOptions` que especifica vários valores de tempo de execução. Esse valor de parâmetro é opcional e você pode passar `null`.

      O método `addSignatureField` retorna um `com.adobe.idp`. `Document` que representa um documento PDF que contém um campo de assinatura.
   >[!NOTE]
   >
   >Você pode chamar o método `SignatureServiceClient` do objeto `addInvisibleSignatureField` para adicionar um campo de assinatura invisível.

1. Salvar o documento PDF como um arquivo PDF

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame `com.adobe.idp`. `Document` o  `copyToFile` método do objeto para copiar o conteúdo do  `Document` objeto para o arquivo. Certifique-se de usar o `com.adobe.idp`. `Document` objeto que foi retornado pelo  `addSignatureField` método.

**Consulte também:**

[Start rápidos da API do serviço de assinatura](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Adicionar campos de assinatura usando a API de serviço da Web {#add-signature-fields-using-the-web-service-api}

Para adicionar um campo de assinatura usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obter um documento PDF ao qual um campo de assinatura é adicionado

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF que conterá um campo de assinatura.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Adicionar um campo de assinatura

   Adicione um campo de assinatura ao documento PDF chamando o método `SignatureServiceClient` do objeto `addSignatureField` e transmitindo os seguintes valores:

   * Um objeto `BLOB` que representa o documento PDF ao qual um campo de assinatura é adicionado.
   * Um valor de string que especifica o nome do campo de assinatura.
   * Um valor inteiro que representa o número da página à qual um campo de assinatura é adicionado.
   * Um objeto `PositionRect` que especifica o local do campo de assinatura.
   * Um objeto `FieldMDPOptions` que especifica campos no documento PDF que são bloqueados depois que uma assinatura digital é aplicada ao campo de assinatura. Esse valor de parâmetro é opcional e você pode passar `null`.
   * Um objeto `PDFSeedValueOptions` que especifica vários valores de tempo de execução. Esse valor de parâmetro é opcional e você pode passar `null`.

   O método `addSignatureField` retorna um objeto `BLOB` que representa um documento PDF que contém um campo de assinatura.

1. Salvar o documento PDF como um arquivo PDF

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF que conterá o campo de assinatura e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` que foi retornado pelo método `addSignatureField`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `binaryData`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Recuperando Nomes de Campos de Assinatura {#retrieving-signature-field-names}

Você pode recuperar os nomes de todos os campos de assinatura localizados em um documento PDF que deseja assinar ou certificar. Se você não tiver certeza dos nomes dos campos de assinatura localizados em um documento PDF ou quiser verificar os nomes, poderá recuperá-los de forma programática. O serviço de assinatura retorna o nome totalmente qualificado do campo de assinatura, como `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumo das etapas {#summary_of_steps-1}

Para recuperar nomes de campos de assinatura, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém campos de assinatura.
1. Recupere os nomes dos campos de assinatura.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação de serviço de assinatura, você deve criar um cliente de serviço de assinatura.

**Obter o documento PDF que contém os campos de assinatura**

Recupere um documento PDF que contenha campos de assinatura.

**Recuperar os nomes dos campos de assinatura**

É possível recuperar nomes de campos de assinatura depois de recuperar um documento PDF que contém um ou mais campos de assinatura.

**Consulte também:**

[Recuperar nomes de campos de assinatura usando a API Java](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Recuperar campo de assinatura usando a API de serviço da Web](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields)

### Recuperar nomes de campos de assinatura usando a API Java {#retrieve-signature-field-names-using-the-java-api}

Recupere nomes de campos de assinatura usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signature-client.jar, no classpath do seu projeto Java.

1. Criar um cliente de assinatura

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obter o documento PDF que contém os campos de assinatura

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF que contém campos de assinatura usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Recuperar os nomes dos campos de assinatura

   * Recupere os nomes dos campos de assinatura chamando o método `SignatureServiceClient` do objeto `getSignatureFieldList` e transmitindo o objeto `com.adobe.idp.Document` que contém o documento PDF que contém os campos de assinatura. Este método retorna um objeto `java.util.List`, no qual cada elemento contém um objeto `PDFSignatureField`. Usando esse objeto, você pode obter informações adicionais sobre um campo de assinatura, como se ele está visível.
   * Interaja pelo objeto `java.util.List` para determinar se há nomes de campos de assinatura. Para cada campo de assinatura no documento PDF, é possível obter um objeto `PDFSignatureField` separado. Para obter o nome do campo de assinatura, chame o método `PDFSignatureField` do objeto `getName`. Esse método retorna um valor de string que especifica o nome do campo de assinatura.

**Consulte também:**

[Recuperando Nomes de Campos de Assinatura](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Start rápido (modo SOAP): Recuperar nomes de campos de assinatura usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar campo de assinatura usando a API de serviço da Web {#retrieve-signature-field-using-the-web-service-api}

Recuperar nomes de campos de assinatura usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obter o documento PDF que contém os campos de assinatura

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF que contém campos de assinatura.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Recuperar os nomes dos campos de assinatura

   * Recupere os nomes dos campos de assinatura chamando o método `SignatureServiceClient` do objeto `getSignatureFieldList` e transmitindo o objeto `BLOB` que contém o documento PDF que contém os campos de assinatura. Este método retorna um objeto de coleção `MyArrayOfPDFSignatureField` em que cada elemento contém um objeto `PDFSignatureField`.
   * Interaja pelo objeto `MyArrayOfPDFSignatureField` para determinar se há nomes de campos de assinatura. Para cada campo de assinatura no documento PDF, é possível obter um objeto `PDFSignatureField`. Para obter o nome do campo de assinatura, chame o método `PDFSignatureField` do objeto `getName`. Esse método retorna um valor de string que especifica o nome do campo de assinatura.

**Consulte também:**

[Recuperando Nomes de Campos de Assinatura](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modificando campos de assinatura {#modifying-signature-fields}

É possível modificar campos de assinatura localizados em um documento PDF usando a API Java e a API de serviço da Web. Modificar um campo de assinatura envolve manipular seus valores de dicionário de bloqueio de campo de assinatura ou valores de dicionário de valor semente.

Um *dicionário de bloqueio de campo* especifica uma lista de campos bloqueados quando o campo de assinatura é assinado. Um campo bloqueado impede que os usuários façam alterações no campo. Um *dicionário de valores semente* contém informações de restrição que são usadas no momento em que a assinatura é aplicada. Por exemplo, você pode alterar permissões que controlam as ações que podem ocorrer sem invalidar uma assinatura.

Ao modificar um campo de assinatura existente, você pode fazer alterações no documento PDF para refletir as necessidades comerciais em mudança. Por exemplo, um novo requisito comercial pode exigir o bloqueio de todos os campos de documento depois que o documento é assinado.

Esta seção explica como modificar um campo de assinatura alterando o dicionário de bloqueio de campo e os valores do dicionário de valor semente. As alterações feitas no dicionário de bloqueio do campo de assinatura resultaram no bloqueio de todos os campos no documento PDF quando um campo de assinatura é assinado. As alterações feitas no dicionário de valor semente proíbem tipos específicos de alterações no documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura e a modificação dos campos de assinatura, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para modificar os campos de assinatura localizados em um documento PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém o campo de assinatura a ser modificado.
1. Defina os valores do dicionário.
1. Modifique o campo de assinatura.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo os arquivos da biblioteca Java do LiveCycle](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação de serviço de assinatura, você deve criar um cliente de serviço de assinatura.

**Obtenha o documento PDF que contém o campo de assinatura para modificar**

Recupere um documento PDF que contenha o campo de assinatura a ser modificado.

**Definir valores do dicionário**

Para modificar um campo de assinatura, atribua valores ao dicionário de bloqueios de campos ou ao dicionário de valores semente. A especificação de valores de dicionário de bloqueio de campo de assinatura envolve a especificação de campos de documento PDF que são bloqueados quando o campo de assinatura é assinado. (Esta seção discute como bloquear todos os campos.)

Os seguintes valores do dicionário de valores semente podem ser definidos:

* **Verificação** de revisão: Especifica se a verificação de revogação é executada quando uma assinatura é aplicada ao campo de assinatura.
* **Opções** de certificado: Atribui valores ao dicionário de valores semente do certificado. Antes de especificar as opções de certificado, é recomendável que você se familiarize com um dicionário de valores semente de certificado. (Consulte [Referência de PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opções** de compilação: Atribui algoritmos de compilação usados para assinatura. Os valores válidos são SHA1, SHA256, SHA384, SHA512 e RIPEMD160.
* **Filtro**: Especifica o filtro usado com o campo de assinatura. Por exemplo, você pode usar o filtro Adobe.PPKLite. (Consulte [Referência de PDF](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf).)
* **Opções** de sinalizador: Especifica os valores de sinalizador associados a esse campo de assinatura. Um valor de 1 significa que um assinante deve usar apenas os valores especificados para a entrada. Um valor de 0 significa que outros valores são permitidos. Estas são as posições do Bit:

   * **1(Filtro):** O manipulador de assinatura a ser usado para assinar o campo de assinatura
   * **2 (Subfiltro):** uma matriz de nomes que indica codificações aceitáveis para usar ao assinar
   * **3 (V)**: O número mínimo de versão necessário do manipulador de assinatura a ser usado para assinar o campo de assinatura
   * **4 (Motivos):** Uma matriz de strings que especifica possíveis motivos para assinar um documento
   * **5 (PDFLegalWarnings):** Uma matriz de strings que especificam possíveis atestados legais

* **Atestados** jurídicos: Quando um documento é certificado, ele é verificado automaticamente em busca de tipos específicos de conteúdo que podem tornar o conteúdo visível de um documento ambíguo ou enganoso. Por exemplo, uma anotação pode obscurecer o texto que é importante para entender o que está sendo certificado. O processo de varredura gera avisos que indicam a presença desse tipo de conteúdo. Também fornece uma explicação adicional do conteúdo que pode ter gerado avisos.
* **Permissões**: Especifica permissões que podem ser usadas em um documento PDF sem invalidar a assinatura.
* **Motivos**: Especifica os motivos pelos quais esse documento deve ser assinado.
* **Carimbo** de data/hora: Especifica opções de carimbo de data e hora. Você pode, por exemplo, definir o URL do servidor de carimbo de data e hora usado.
* **Versão**: Especifica o número mínimo de versão do manipulador de assinatura a ser usado para assinar o campo de assinatura.

**Modificar o campo de assinatura**

Depois de criar um cliente de serviço de assinatura, recuperar o documento PDF que contém o campo de assinatura a ser modificado e definir valores de dicionário, você pode instruir o serviço de assinatura a modificar o campo de assinatura. O serviço de assinatura retorna um documento PDF que contém o campo de assinatura modificado. O documento PDF original não é afetado.

**Salvar o documento PDF como um arquivo PDF**

Salve o documento PDF que contém o campo de assinatura modificado como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou no Adobe Reader.

**Consulte também:**

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do serviço de assinatura](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[Assinando Documentos PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Modifique os campos de assinatura usando a API Java {#modify-signature-fields-using-the-java-api}

Modifique um campo de assinatura usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signature-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de assinatura

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento PDF que contém o campo de assinatura para modificar

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF que contém o campo de assinatura a ser modificado usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Definir valores do dicionário

   * Crie um objeto `PDFSignatureFieldProperties` usando seu construtor. Um objeto `PDFSignatureFieldProperties` armazena informações do dicionário de bloqueios de campos de assinatura e do dicionário de valores semente.
   * Crie um objeto `PDFSeedValueOptionSpec` usando seu construtor. Esse objeto permite que você defina valores de dicionário de valor semente.
   * Não permita alterações no documento PDF invocando o método `PDFSeedValueOptionSpec` do objeto `setMdpValue` e transmitindo o valor da lista discriminada `MDPPermissions.NoChanges`.
   * Crie um objeto `FieldMDPOptionSpec` usando seu construtor. Esse objeto permite definir valores de dicionário de bloqueio de campo de assinatura.
   * Bloqueie todos os campos no documento PDF chamando o método `FieldMDPOptionSpec` do objeto `setMdpValue` e transmitindo o valor da lista discriminada `FieldMDPAction.ALL`.
   * Defina as informações do dicionário de valores semente chamando o método `PDFSignatureFieldProperties` do objeto `setSeedValue` e transmitindo o objeto `PDFSeedValueOptionSpec`.
   * Defina as informações do dicionário de bloqueio do campo de assinatura chamando o método `PDFSignatureFieldProperties`do objeto `setFieldMDP` e transmitindo o objeto `FieldMDPOptionSpec`.

   >[!NOTE]
   >
   >Para ver todos os valores do dicionário de valor semente que você pode definir, consulte a referência da classe `PDFSeedValueOptionSpec`. (Consulte [Referência de API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

1. Modificar o campo de assinatura

   Modifique o campo de assinatura chamando o método `SignatureServiceClient` do objeto `modifySignatureField` e transmitindo os seguintes valores:

   * O objeto `com.adobe.idp.Document` que armazena o documento PDF que contém o campo de assinatura a ser modificado
   * Um valor de string que especifica o nome do campo de assinatura
   * O objeto `PDFSignatureFieldProperties` que armazena informações do dicionário de bloqueios de campos de assinatura e do dicionário de valores semente

   O método `modifySignatureField` retorna um objeto `com.adobe.idp.Document` que armazena um documento PDF que contém o campo de assinatura modificado.

1. Salvar o documento PDF como um arquivo PDF

   * Crie um objeto `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo. Certifique-se de usar o objeto `com.adobe.idp.Document` retornado pelo método `modifySignatureField`.

### Modifique os campos de assinatura usando a API de serviço da Web {#modify-signature-fields-using-the-web-service-api}

Modifique um campo de assinatura usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF que contém o campo de assinatura para modificar

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF que contém o campo de assinatura a ser modificado.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo a propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Definir valores do dicionário

   * Crie um objeto `PDFSignatureFieldProperties` usando seu construtor. Este objeto armazena informações do dicionário de bloqueios de campos de assinatura e do dicionário de valores semente.
   * Crie um objeto `PDFSeedValueOptionSpec` usando seu construtor. Esse objeto permite que você defina valores de dicionário de valor semente.
   * Não permita alterações no documento PDF atribuindo o valor de lista discriminada `MDPPermissions.NoChanges` ao membro de dados `PDFSeedValueOptionSpec` do objeto `mdpValue`.
   * Crie um objeto `FieldMDPOptionSpec` usando seu construtor. Esse objeto permite definir valores de dicionário de bloqueio de campo de assinatura.
   * Bloqueie todos os campos no documento PDF atribuindo o valor de lista discriminada `FieldMDPAction.ALL` ao membro de dados `FieldMDPOptionSpec` do objeto `mdpValue`.
   * Defina as informações do dicionário de valores semente atribuindo o objeto `PDFSeedValueOptionSpec` ao membro de dados `PDFSignatureFieldProperties` do objeto `seedValue`.
   * Defina as informações do dicionário de bloqueio do campo de assinatura atribuindo o objeto `FieldMDPOptionSpec` ao membro de dados `PDFSignatureFieldProperties` do objeto `fieldMDP`.

   >[!NOTE]
   >
   >Para ver todos os valores do dicionário de valor semente que você pode definir, consulte a referência da classe `PDFSeedValueOptionSpec`. (Consulte [Referência de API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

1. Modificar o campo de assinatura

   Modifique o campo de assinatura chamando o método `SignatureServiceClient` do objeto `modifySignatureField` e transmitindo os seguintes valores:

   * O objeto `BLOB` que armazena o documento PDF que contém o campo de assinatura a ser modificado
   * Um valor de string que especifica o nome do campo de assinatura
   * O objeto `PDFSignatureFieldProperties` que armazena informações do dicionário de bloqueios de campos de assinatura e do dicionário de valores semente

   O método `modifySignatureField` retorna um objeto `BLOB` que armazena um documento PDF que contém o campo de assinatura modificado.

1. Salvar o documento PDF como um arquivo PDF

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF que conterá o campo de assinatura e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `addSignatureField`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Assinando Documentos PDF digitalmente {#digitally-signing-pdf-documents}

Assinaturas digitais podem ser aplicadas a documentos PDF para fornecer um nível de segurança. As assinaturas digitais, como assinaturas manuscritas, fornecem um meio pelo qual os signatários se identificam e fazem declarações sobre um documento. A tecnologia usada para assinar documentos digitalmente ajuda a garantir que tanto o assinante quanto os recipient sejam claros sobre o que foi assinado e confiem que o documento não foi alterado desde que foi assinado.

DOCUMENTOS PDF são assinados por meio de tecnologia de chave pública. Um assinante tem duas chaves: uma chave pública e uma chave privada. A chave privada é armazenada em uma credencial do usuário que deve estar disponível no momento da assinatura. A chave pública é armazenada no certificado do usuário que deve estar disponível para os recipient para validar a assinatura. Informações sobre certificados revogados são encontradas nas listas de revogação de certificados (CRLs) e nas respostas do Protocolo de Status de Certificado Online (OCSP) distribuídas pelas Autoridades de Certificação (CAs). O tempo de assinatura pode ser obtido de uma fonte confiável conhecida como uma autoridade de carimbo de data e hora.

>[!NOTE]
>
>Antes de poder assinar digitalmente um documento PDF, é necessário adicionar o certificado à AEM Forms. Um certificado é adicionado usando o console de administração ou de forma programática usando a API do Trust Manager. (Consulte [Importando credenciais usando a API do Gerenciador de Confiança](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Você pode assinar documentos PDF digitalmente de forma programática. Ao assinar digitalmente um documento PDF, é necessário fazer referência a uma credencial de segurança que existe no AEM Forms. A credencial é a chave privada usada para assinatura.

O serviço de assinatura executa as seguintes etapas quando um documento PDF é assinado:

1. O serviço de assinatura recupera a credencial do Truststore transmitindo o alias especificado na solicitação.
1. A Truststore pesquisa a credencial especificada.
1. A credencial é retornada ao serviço de assinatura e é usada para assinar o documento. A credencial também é armazenada em cache no alias para solicitações futuras.

Para obter informações sobre como lidar com as credenciais de segurança, consulte o guia *Instalação e implantação do AEM Forms* para o servidor de aplicativos.

>[!NOTE]
>
>Há diferenças entre documentos de assinatura e certificação. (Consulte [Certificando Documentos PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>Nem todos os documentos PDF suportam assinatura. Para obter mais informações sobre o serviço de assinatura e documentos de assinatura digital, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>O serviço de assinatura não suporta arquivos XDP com dados PDF incorporados como entrada para uma operação, como a certificação de um documento. Essa ação resulta no serviço de assinatura lançando um `PDFOperationException`. Para resolver esse problema, converta o arquivo XDP em um arquivo PDF usando o serviço Utilitários de PDF e passe o arquivo PDF convertido para uma operação do serviço de assinatura. (Consulte [Trabalhar com utilitários PDF](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities).)

**Credencial HSM nShield do Cifrador**

Ao usar uma credencial nShield HSM da Central para assinar ou certificar um documento PDF, a nova credencial não poderá ser usada até que o servidor de aplicativos J2EE no qual a AEM Forms está implantada seja reiniciado. No entanto, você pode definir um valor de configuração, resultando na operação de assinatura ou certificação funcionando sem reiniciar o servidor de aplicativos J2EE.

Você pode adicionar o seguinte valor de configuração no arquivo cknfastrc, localizado em /opt/nfast/cknfastrc (ou c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Após adicionar esse valor de configuração ao arquivo cknfastrc, a nova credencial poderá ser usada sem reiniciar o servidor de aplicativos J2EE.

**A assinatura não é confiável**

Ao certificar e assinar o mesmo documento PDF, se a assinatura de certificação não for confiável, um triângulo amarelo será exibido contra a primeira assinatura ao abrir o documento PDF no Acrobat ou Adobe Reader. A assinatura de certificação deve ser confiável para evitar essa situação.

**Assinar documentos que são formulários baseados em XFA**

Se você tentar assinar um formulário baseado em XFA usando a API do serviço de assinatura, os dados podem estar ausentes do `View` `Signed` `Version` localizado no Acrobat. Por exemplo, considere o seguinte fluxo de trabalho:

* Usando um arquivo XDP criado usando o Designer, é possível mesclar um design de formulário que contenha um campo de assinatura e dados XML que contenham dados de formulário. Use o serviço Forms para gerar um documento PDF interativo.
* Você assina o documento PDF usando a API de serviço de assinatura.

### Resumo das etapas {#summary_of_steps-3}

Para assinar digitalmente um documento PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de serviço de assinatura.
1. Faça com que o documento PDF assine.
1. Assine o documento PDF.
1. Salve o documento PDF assinado como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

**Criar um cliente de Assinaturas**

Antes de executar programaticamente uma operação de serviço de assinatura, você deve criar um cliente de serviço de assinatura.

**Obtenha o documento PDF para assinar**

Para assinar um documento PDF, é necessário obter um documento PDF que contenha um campo de assinatura. Se um documento PDF não contiver um campo de assinatura, ele não poderá ser assinado. Um campo de assinatura pode ser adicionado usando o Designer ou de forma programática.

**Assinar o documento PDF**

Ao assinar um documento PDF, você pode definir opções de tempo de execução usadas pelo serviço de assinatura. É possível definir as seguintes opções:

* Opções de aparência
* Verificação de revogação
* Valores de carimbo de data e hora

Você define opções de aparência usando um objeto `PDFSignatureAppearanceOptionSpec`. Por exemplo, você pode exibir a data em uma assinatura chamando o método `PDFSignatureAppearanceOptionSpec` do objeto `setShowDate` e transmitindo `true`.

Você também pode especificar se deve ou não executar uma verificação de revogação que determina se o certificado usado para assinar digitalmente um documento PDF foi revogado. Para executar a verificação de revogação, você pode especificar um dos seguintes valores:

* **NoCheck**: Não efetuar a verificação de revogação.
* **MelhorEsforço**: Sempre tente verificar a revogação de todos os certificados na cadeia. Se ocorrer algum problema na verificação, a revogação será considerada válida. Se ocorrer alguma falha, suponha que o certificado não seja revogado.
* **CheckIfAvailable:** Verifique a revogação de todos os certificados na cadeia se as informações de revogação estão disponíveis. Se ocorrer algum problema na verificação, a revogação será considerada inválida. Se ocorrer alguma falha, suponha que o certificado seja revogado e inválido. (Esse é o valor padrão.)
* **SempreVerificar**: Verifique a revogação de todos os certificados na cadeia. Se as informações de revogação não estiverem presentes em nenhum certificado, presume-se que a revogação é inválida.

Para executar a verificação de revogação em um certificado, você pode especificar um URL para um servidor de lista de revogação de certificado (CRL) usando um objeto `CRLOptionSpec`. No entanto, se você quiser realizar a verificação de revogação e não especificar um URL para um servidor CRL, o serviço de assinatura obterá o URL do certificado.

Em vez de usar um servidor CRL, você pode usar um servidor OCSP (protocolo de status de certificado) online ao executar a verificação de revogação. Normalmente, ao usar um servidor OCSP em vez de um servidor CRL, a verificação de revogação é executada mais rapidamente. (Consulte &quot;Online Certificate Status Protocol&quot; em [https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560).)

Você pode definir a ordem do servidor CRL e OCSP que o serviço de assinatura usa com aplicativos e serviços de Adobe. Por exemplo, se o servidor OCSP for definido primeiro em Aplicativos e Serviços de Adobe, então o servidor OCSP será marcado, seguido pelo servidor CRL. (Consulte &quot;Gerenciamento de certificados e credenciais usando o Armazenamento de confiança&quot; na Ajuda do AAC).

Se você especificar não executar a verificação de revogação, o serviço de Assinatura não verificará se o certificado usado para assinar ou certificar um documento foi revogado. Ou seja, as informações do CRL e do servidor OCSP são ignoradas.

>[!NOTE]
>
>Embora um CRL ou um servidor OCSP possa ser especificado no certificado, você pode substituir o URL especificado no certificado usando um objeto `CRLOptionSpec` e `OCSPOptionSpec`. Por exemplo, para substituir o servidor CRL, você pode chamar o método `CRLOptionSpec` do objeto `setLocalURI`.

O carimbo de data e hora se refere ao processo de rastreamento da hora em que um documento assinado ou certificado foi modificado. Depois que um documento é assinado, ele não deve ser modificado, nem mesmo pelo proprietário do documento. O carimbo de data e hora ajuda a reforçar a validade de um documento assinado ou certificado. É possível definir opções de carimbo de data e hora usando um objeto `TSPOptionSpec`. Por exemplo, você pode especificar o URL de um servidor de provedor de carimbo de data e hora (TSP).

>[!NOTE]
>
>No Java e nos serviços da Web, percorram seções e os start rápidos correspondentes, a verificação de revogação é usada. Como nenhuma informação CRL ou OCSP do servidor é especificada, as informações do servidor são obtidas do certificado usado para assinar digitalmente o documento PDF.

Para assinar com êxito um documento PDF, você pode especificar o nome totalmente qualificado do campo de assinatura que conterá a assinatura digital, como `form1[0].#subform[1].SignatureField3[3]`. Ao usar um campo de formulário XFA, o nome parcial do campo de assinatura também pode ser usado: `SignatureField3[3]`.

Também é necessário referenciar uma credencial de segurança para assinar digitalmente um documento PDF. Para referenciar uma credencial de segurança, especifique um alias. O alias é uma referência a uma credencial real que pode estar em um arquivo PKCS#12 (com uma extensão .pfx) ou em um módulo de segurança de hardware (HSM). Para obter informações sobre as credenciais de segurança, consulte o guia *Instalação e implantação do AEM Forms* para o servidor de aplicativos.

**Salvar o documento PDF assinado**

Depois que o serviço de assinatura assinar digitalmente o documento PDF, você poderá salvá-lo como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou Adobe Reader.

**Consulte também:**

[Assine digitalmente documentos PDF usando a API Java](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Assinatura digital de documentos PDF usando a API de serviço da Web](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields)

[Recuperando Nomes de Campos de Assinatura](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Assine digitalmente documentos PDF usando a API Java {#digitally-sign-pdf-documents-using-the-java-api}

Assine digitalmente um documento PDF usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signature-client.jar, no classpath do seu projeto Java.

1. Criar um cliente de Assinaturas

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento PDF para assinar

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF para assinar digitalmente usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Assinar o documento PDF

   Assine o documento PDF chamando o método `SignatureServiceClient` do objeto `sign` e transmitindo os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento PDF a ser assinado.
   * Um valor de string que representa o nome do campo de assinatura que conterá a assinatura digital.
   * Um objeto `Credential` que representa a credencial usada para assinar digitalmente o documento PDF. Crie um objeto `Credential` invocando o método estático `Credential` do objeto `getInstance` e transmitindo um valor de string que especifica o valor alias que corresponde à credencial de segurança.
   * Um objeto `HashAlgorithm` que especifica um membro de dados estáticos que representa o algoritmo de hash a ser usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi assinado digitalmente.
   * Um valor de string que representa as informações de contato do assinante.
   * Um objeto `PDFSignatureAppearanceOptions` que controla a aparência da assinatura digital. Por exemplo, você pode usar esse objeto para adicionar um logotipo personalizado a uma assinatura digital.
   * Um objeto `java.lang.Boolean` que especifica se a verificação de revogação deve ser executada no certificado do assinante.
   * Um objeto `OCSPOptionSpec` que armazena preferências para suporte ao Online Certificate Status Protocol (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `CRLPreferences` que armazena as preferências de lista de revogação de certificado (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `TSPPreferences` que armazena preferências para suporte ao provedor de carimbo de data e hora (TSP). Esse parâmetro é opcional e pode ser `null`. Para obter mais informações, consulte [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   O método `sign` retorna um objeto `com.adobe.idp.Document` que representa o documento PDF assinado.

1. Salvar o documento PDF assinado

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` e passe `java.io.File`para copiar o conteúdo do objeto `Document` para o arquivo. Certifique-se de usar o objeto `com.adobe.idp.Document` retornado pelo método `sign`.

**Consulte também:**

[Assinando Documentos PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Start rápido (modo SOAP): Assinando digitalmente um documento PDF usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Assinatura digital de documentos PDF usando a API de serviço da Web {#digitally-signing-pdf-documents-using-the-web-service-api}

Para assinar digitalmente um documento PDF usando a Signature API (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de Assinaturas

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF para assinar

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF assinado.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF a ser assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo a propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Assinar o documento PDF

   Assine o documento PDF chamando o método `SignatureServiceClient` do objeto `sign` e transmitindo os seguintes valores:

   * Um objeto `BLOB` que representa o documento PDF a ser assinado.
   * Um valor de string que representa o nome do campo de assinatura que conterá a assinatura digital.
   * Um objeto `Credential` que representa a credencial usada para assinar digitalmente o documento PDF. Crie um objeto `Credential` usando seu construtor e especifique o alias atribuindo um valor à propriedade `Credential` do objeto `alias`.
   * Um objeto `HashAlgorithm` que especifica um membro de dados estáticos que representa o algoritmo de hash a ser usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor booliano que especifica se o algoritmo hash é usado.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi assinado digitalmente.
   * Um valor de string que representa a localização do assinante.
   * Um valor de string que representa as informações de contato do assinante.
   * Um objeto `PDFSignatureAppearanceOptions` que controla a aparência da assinatura digital. Por exemplo, você pode usar esse objeto para adicionar um logotipo personalizado a uma assinatura digital.
   * Um objeto `System.Boolean` que especifica se a verificação de revogação deve ser executada no certificado do assinante. Se essa verificação de revogação for feita, ela será incorporada à assinatura. O padrão é `false`.
   * Um objeto `OCSPOptionSpec` que armazena preferências para suporte ao Online Certificate Status Protocol (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`. Para obter informações sobre esse objeto, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Um objeto `CRLPreferences` que armazena as preferências de lista de revogação de certificado (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `TSPPreferences` que armazena preferências para suporte ao provedor de carimbo de data e hora (TSP). Esse parâmetro é opcional e pode ser `null`.

   O método `sign` retorna um objeto `BLOB` que representa o documento PDF assinado.

1. Salvar o documento PDF assinado

   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` que foi retornado pelo método `sign`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Assinando Documentos PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Assinando Digitalmente o Forms Interativo {#digitally-signing-interactive-forms}

Você pode assinar um formulário interativo criado pelo serviço Forms. Por exemplo, considere o seguinte fluxo de trabalho:

* É possível unir um formulário PDF baseado em XFA criado usando o Designer e dados de formulário localizados em um documento XML usando o serviço Forms. O servidor Forms renderiza um formulário interativo.
* Você assina o formulário interativo usando a API de serviço de assinatura.

O resultado é um formulário PDF interativo assinado digitalmente. Ao assinar um formulário PDF baseado em um formulário XFA, salve o arquivo PDF como um formulário PDF Adobe Static. Se você tentar assinar um formulário PDF salvo como um formulário PDF dinâmico de Adobe, ocorrerá uma exceção. Como você está assinando o formulário que é retornado do serviço Forms, verifique se o formulário contém um campo de assinatura.

>[!NOTE]
>
>Antes de poder assinar digitalmente um formulário interativo, é necessário adicionar o certificado à AEM Forms. Um certificado é adicionado usando o console de administração ou de forma programática usando a API do Trust Manager. (Consulte [Importando credenciais usando a API do Gerenciador de Confiança](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

Ao usar a Forms Service API, defina a opção `GenerateServerAppearance` de tempo de execução como `true`. Essa opção de tempo de execução garante que a aparência do formulário gerado no servidor permaneça válida quando aberto no Acrobat ou Adobe Reader. É recomendável definir essa opção de tempo de execução ao gerar um formulário interativo para assinar usando a API do Forms.

>[!NOTE]
>
>Antes de ler Digitally Signing Interative Forms, recomenda-se que você esteja familiarizado com a assinatura de documentos PDF. (Consulte [Assinando Documentos PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### Resumo das etapas {#summary_of_steps-4}

Para assinar digitalmente um formulário interativo retornado pelo serviço Forms, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente Forms e Signatures.
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
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente Forms e Signatures**

Como esse fluxo de trabalho chama os serviços Forms e Signature, crie um cliente de serviço Forms e um cliente de serviço Signature.

**Obter o formulário interativo usando o serviço Forms**

Você pode usar o serviço Forms para obter o formulário PDF interativo para assinar. A partir do AEM Forms, você pode enviar um objeto `com.adobe.idp.Document` para o serviço Forms que contém o formulário a ser renderizado. O nome deste método é `renderPDFForm2`. Esse método retorna um objeto `com.adobe.idp.Document` que contém o formulário a ser assinado. Você pode passar esta instância `com.adobe.idp.Document` para o serviço de assinatura.

Da mesma forma, se você estiver usando serviços da Web, poderá passar a instância `BLOB` que o serviço Forms retorna ao serviço de assinatura.

>[!NOTE]
>
>O start rápido associado à seção Assinatura digital interativa do Forms chama o método `renderPDFForm2`.

**Assinar o formulário interativo**

Ao assinar um documento PDF, você pode definir opções de tempo de execução que o serviço de assinatura usa. É possível definir as seguintes opções:

* Opções de aparência
* Verificação de revogação
* Valores de carimbo de data e hora

Você define opções de aparência usando um objeto `PDFSignatureAppearanceOptionSpec`. Por exemplo, você pode exibir a data em uma assinatura chamando o método `PDFSignatureAppearanceOptionSpec` do objeto `setShowDate` e transmitindo `true`.

**Salvar o documento PDF assinado**

Depois que o serviço de assinatura assinar digitalmente o documento PDF, você poderá salvá-lo como um arquivo PDF. O arquivo PDF pode ser aberto no Acrobat ou Adobe Reader.

**Consulte também:**

[Assine digitalmente um formulário interativo usando a API Java](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Assinar digitalmente um formulário interativo usando a API de serviço da Web](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assinando Documentos PDF digitalmente](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Assine digitalmente um formulário interativo usando a API Java {#digitally-sign-an-interactive-form-using-the-java-api}

Assine digitalmente um formulário interativo usando a API de assinatura e o Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signature-client.jar e adobe-forms-client.jar, no classpath do seu projeto Java.

1. Criar um cliente Forms e Signatures

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obter o formulário interativo usando o serviço Forms

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF a ser enviado para o serviço Forms usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.
   * Crie um objeto `java.io.FileInputStream` que represente o documento XML que contém dados de formulário a serem enviados para o serviço Forms usando seu construtor. Passe um valor de string que especifica o local do arquivo XML.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.
   * Crie um objeto `PDFFormRenderSpec` usado para definir opções de tempo de execução. Chame o método `PDFFormRenderSpec` do objeto `setGenerateServerAppearance` e passe `true`.
   * Chame o método `FormsServiceClient` do objeto `renderPDFForm2` e passe os seguintes valores:

      * Um objeto `com.adobe.idp.Document` que contém o formulário PDF a ser renderizado.
      * Um objeto `com.adobe.idp.Document` que contém dados a serem unidos ao formulário.
      * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução.
      * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms. Você pode especificar `null` para esse valor de parâmetro.
      * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

      O método `renderPDFForm2` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário

   * Recupere o formulário PDF chamando o método `FormsResult` do objeto `getOutputContent`. Este método retorna um objeto `com.adobe.idp.Document` que representa o formulário interativo.


1. Assinar o formulário interativo

   Assine o documento PDF chamando o método `SignatureServiceClient` do objeto `sign` e transmitindo os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento PDF a ser assinado. Verifique se esse objeto é o objeto `com.adobe.idp.Document` obtido do serviço Forms.
   * Um valor de string que representa o nome do campo de assinatura assinado.
   * Um objeto `Credential` que representa a credencial usada para assinar digitalmente o documento PDF. Crie um objeto `Credential` chamando o método estático `Credential` do objeto `getInstance`. Passe um valor de string que especifica o valor alias que corresponde à credencial de segurança.
   * Um objeto `HashAlgorithm` que especifica um membro de dados estáticos que representa o algoritmo de hash a ser usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi assinado digitalmente.
   * Um valor de string que representa as informações de contato do assinante.
   * Um objeto `PDFSignatureAppearanceOptions` que controla a aparência da assinatura digital. Por exemplo, você pode usar esse objeto para adicionar um logotipo personalizado a uma assinatura digital.
   * Um objeto `java.lang.Boolean` que especifica se a verificação de revogação deve ser executada no certificado do assinante.
   * Um objeto `OCSPPreferences` que armazena preferências para suporte ao Online Certificate Status Protocol (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `CRLPreferences` que armazena as preferências de lista de revogação de certificado (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `TSPPreferences` que armazena preferências para suporte ao provedor de carimbo de data e hora (TSP). Esse parâmetro é opcional e pode ser `null`.

   O método `sign` retorna um objeto `com.adobe.idp.Document` que representa o documento PDF assinado.

1. Salvar o documento PDF assinado

   * Crie um objeto `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` e passe `java.io.File`para copiar o conteúdo do objeto `Document` para o arquivo. Certifique-se de usar o objeto `com.adobe.idp.Document` retornado pelo método `sign`.

**Consulte também:**

[Assinando Digitalmente o Forms Interativo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Start rápido (modo SOAP): Assinando digitalmente um documento PDF usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Assine digitalmente um formulário interativo usando a API de serviço da Web {#digitally-sign-an-interactive-form-using-the-web-service-api}

Assine digitalmente um formulário interativo usando a Forms e Signature API (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Como este aplicativo cliente chama dois serviços da AEM Forms, crie duas referências de serviço. Use a seguinte definição WSDL para a referência de serviço associada ao serviço de assinatura: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Use a seguinte definição WSDL para a referência de serviço associada ao serviço Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Como o tipo de dados `BLOB` é comum a ambas as referências de serviço, qualifique totalmente o tipo de dados `BLOB` ao usá-lo. No start rápido do serviço da Web correspondente, todas as instâncias `BLOB` são totalmente qualificadas.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente Forms e Signatures

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita essas etapas para o cliente de serviço Forms.

1. Obter o formulário interativo usando o serviço Forms

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF assinado.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF a ser assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo a propriedade `MTOM` ao conteúdo da matriz de bytes.
   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar dados de formulário.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo XML que contém os dados do formulário e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo a propriedade `MTOM` ao conteúdo da matriz de bytes.
   * Crie um objeto `PDFFormRenderSpec` usado para definir opções de tempo de execução. Atribua o valor `true` ao campo `PDFFormRenderSpec` do objeto `generateServerAppearance`.
   * Chame o método `FormsServiceClient` do objeto `renderPDFForm2` e passe os seguintes valores:

      * Um objeto `BLOB` que contém o formulário PDF a ser renderizado.
      * Um objeto `BLOB` que contém dados a serem unidos ao formulário.
      * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução.
      * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms. Você pode especificar `null` para esse valor de parâmetro.
      * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
      * Um parâmetro de saída longo usado para armazenar o número de páginas no formulário.
      * Um parâmetro de saída de string usado para o valor de localidade.
      * Um valor `FormResult` que é um parâmetro de saída usado para armazenar o formulário interativo.
   * Recupere o formulário PDF chamando o campo `FormsResult` `outputContent` do objeto. Este campo armazena um objeto `BLOB` que representa o formulário interativo.


1. Assinar o formulário interativo

   Assine o documento PDF chamando o método `SignatureServiceClient` do objeto `sign` e transmitindo os seguintes valores:

   * Um objeto `BLOB` que representa o documento PDF a ser assinado. Use a instância `BLOB` retornada pelo serviço Forms.
   * Um valor de string que representa o nome do campo de assinatura assinado.
   * Um objeto `Credential` que representa a credencial usada para assinar digitalmente o documento PDF. Crie um objeto `Credential` usando seu construtor e especifique o alias atribuindo um valor à propriedade `Credential` do objeto `alias`.
   * Um objeto `HashAlgorithm` que especifica um membro de dados estáticos que representa o algoritmo de hash a ser usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor booliano que especifica se o algoritmo hash é usado.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi assinado digitalmente.
   * Um valor de string que representa a localização do assinante.
   * Um valor de string que representa as informações de contato do assinante.
   * Um objeto `PDFSignatureAppearanceOptions` que controla a aparência da assinatura digital. Por exemplo, você pode usar esse objeto para adicionar um logotipo personalizado a uma assinatura digital.
   * Um objeto `System.Boolean` que especifica se a verificação de revogação deve ser executada no certificado do assinante. Se essa verificação de revogação for feita, ela será incorporada à assinatura. O padrão é `false`.
   * Um objeto `OCSPPreferences` que armazena preferências para suporte ao Online Certificate Status Protocol (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`. Para obter informações sobre esse objeto, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Um objeto `CRLPreferences` que armazena as preferências de lista de revogação de certificado (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `TSPPreferences` que armazena preferências para suporte ao provedor de carimbo de data e hora (TSP). Esse parâmetro é opcional e pode ser `null`.

   O método `sign` retorna um objeto `BLOB` que representa o documento PDF assinado.

1. Salvar o documento PDF assinado

   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` que foi retornado pelo método `sign`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Assinando Digitalmente o Forms Interativo](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Certificando Documentos de PDF {#certifying-pdf-documents}

É possível proteger um documento PDF certificando-o com um tipo específico de assinatura chamada assinatura certificada. Uma assinatura certificada é diferenciada de uma assinatura digital destas maneiras:

* Deve ser a primeira assinatura aplicada ao documento PDF; ou seja, no momento em que a assinatura certificada é aplicada, qualquer outro campo de assinatura no documento deve estar sem assinatura. Somente uma assinatura certificada é permitida em um documento PDF. Se você quiser assinar e certificar um documento PDF, deverá certificá-lo antes de assiná-lo. Depois de certificar um documento PDF, você pode assinar digitalmente campos de assinatura adicionais.
* O autor ou o originador do documento pode especificar que o documento pode ser modificado de certas formas sem invalidar a assinatura certificada. Por exemplo, o documento pode permitir o preenchimento de formulários ou comentários. Se o autor especificar que uma determinada modificação não é permitida, a Acrobat impedirá os usuários de modificar o documento dessa forma. Se tais modificações forem feitas, como ao usar outro aplicativo, a assinatura certificada será inválida e a Acrobat emitirá um aviso quando um usuário abrir o documento. (Com assinaturas não certificadas, as modificações não são impedidas e as operações normais de edição não invalidam a assinatura original.)
* No momento da assinatura, o documento é verificado quanto a tipos específicos de conteúdo que podem tornar o conteúdo de um documento ambíguo ou enganoso. Por exemplo, uma anotação pode obscurecer algum texto em uma página que é importante para entender o que está sendo certificado. Pode ser fornecida uma explicação (atestado legal) sobre esse conteúdo.

Você pode certificar documentos PDF de forma programática usando a API Java do serviço de assinatura ou a API do serviço da Web de assinatura. Ao certificar um documento PDF, você deve fazer referência a uma credencial de segurança que existe no serviço de Credenciais. Para obter informações sobre as credenciais de segurança, consulte o guia *Instalação e implantação do AEM Forms* para o servidor de aplicativos.

>[!NOTE]
>
>Ao certificar e assinar o mesmo documento PDF, se a assinatura da certificação não for confiável, um triângulo amarelo será exibido ao lado da primeira assinatura ao abrir o documento PDF no Acrobat ou Adobe Reader. A assinatura de certificação deve ser confiável para evitar essa situação.

>[!NOTE]
>
>Ao usar uma credencial de HSM nShield do Criador para assinar ou certificar um documento PDF, a nova credencial não poderá ser usada até que o servidor de aplicativos J2EE no qual o AEM Forms está implantado seja reiniciado. No entanto, você pode definir um valor de configuração, resultando na operação de assinatura ou certificação funcionando sem reiniciar o servidor de aplicativos J2EE.

Você pode adicionar o seguinte valor de configuração no arquivo cknfastrc, localizado em /opt/nfast/cknfastrc (ou c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

Após adicionar esse valor de configuração ao arquivo cknfastrc, a nova credencial poderá ser usada sem reiniciar o servidor de aplicativos J2EE.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura e como certificar um documento, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-5}

Para certificar um documento PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF para certificar.
1. Certifique o documento PDF.
1. Salve o documento PDF certificado como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar uma operação de assinatura de forma programática, você deve criar um cliente de assinatura.

**Obtenha o documento PDF para certificar**

Para certificar um documento PDF, é necessário obter um documento PDF que contenha um campo de assinatura. Se um documento PDF não contiver um campo de assinatura, ele não poderá ser certificado. Um campo de assinatura pode ser adicionado usando o Designer ou de forma programática. Para obter informações sobre como adicionar programaticamente um campo de assinatura, consulte [Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields).

**Certificar o documento PDF**

Para certificar um documento PDF com êxito, é necessário os seguintes valores de entrada usados pelo serviço de assinatura para certificar um documento PDF:

* **DOCUMENTO** PDF: Um documento PDF que contém um campo de assinatura, que é um campo de formulário que contém uma representação gráfica da assinatura certificada. Um documento PDF deve conter um campo de assinatura antes de poder ser certificado. Um campo de assinatura pode ser adicionado usando o Designer ou de forma programática. (Consulte [Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields).)
* **Nome** do campo de assinatura: O nome totalmente qualificado do campo de assinatura certificado. O valor a seguir é um exemplo: `form1[0].#subform[1].SignatureField3[3]`. Ao usar um campo de formulário XFA, o nome parcial do campo de assinatura também pode ser usado: `SignatureField3[3]`. Se um valor nulo for passado para o nome do campo, um campo de assinatura invisível será criado e certificado dinamicamente.
* **Credencial** de segurança: Uma credencial usada para certificar o documento PDF. Esta credencial de segurança contém uma senha e um alias, que devem corresponder a um alias que aparece na credencial localizada no serviço de Credencial. O alias é uma referência a uma credencial real que pode estar em um arquivo PKCS#12 (com uma extensão .pfx) ou em um módulo de segurança de hardware (HSM).
* **Algoritmo** de hash: Um algoritmo de hash a ser usado para compilar o documento PDF.
* **Motivo para assinatura**: Um valor exibido no Acrobat ou Adobe Reader para que outros usuários saibam o motivo pelo qual o documento PDF foi certificado.
* **Localização do assinante**: O local do assinante especificado pela credencial.
* **Informações** de contato: Informações de contato, como endereço e número de telefone, do assinante.
* **Informações** de permissão: Permissões que controlam as ações que um usuário final pode executar em um documento sem fazer com que a assinatura certificada seja inválida. Por exemplo, é possível definir a permissão para que qualquer alteração no documento PDF faça com que a assinatura certificada seja inválida.
* **Explicação** jurídica: Quando um documento é certificado, ele é verificado automaticamente em busca de tipos específicos de conteúdo que possam tornar o conteúdo de um documento ambíguo ou enganoso. Por exemplo, uma anotação pode obscurecer algum texto em uma página que é importante para entender o que está sendo certificado. O processo de digitalização gera avisos sobre esses tipos de conteúdo. Esse valor fornece uma explicação adicional do conteúdo que pode ter gerado avisos.
* **Opções** de aparência: Opções que controlam a aparência da assinatura certificada. Por exemplo, a assinatura certificada pode exibir informações de data.
* **Verificação** de revogação: Esse valor especifica se a verificação de revogação é feita para o certificado do assinante. A configuração padrão de `false` significa que a verificação de revogação não é feita.
* **Configurações** OCSP: Configurações para suporte ao protocolo OCSP (Online Certificate Status Protocol), que fornece informações sobre o status da credencial usada para certificar o documento PDF. Você pode, por exemplo, especificar o URL do servidor que fornece informações sobre a credencial que você está usando para fazer logon no documento PDF.
* **Configurações** de CRL: Configurações para as preferências de lista de revogação de certificado (CRL) se a verificação de revogação for feita. Por exemplo, você pode especificar para sempre verificar se uma credencial foi revogada.
* **Carimbo** de data/hora: Configurações que definem informações de marcação de data e hora aplicadas à assinatura certificada. Um carimbo de data/hora indica que dados específicos foram estabelecidos antes de um determinado momento. Este conhecimento ajuda a construir uma relação de confiança entre o assinante e o verificador.

**Salvar o documento PDF certificado como um arquivo PDF**

Depois que o serviço de assinatura certifica o documento PDF, você pode salvá-lo como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou no Adobe Reader.

**Consulte também:**

[Certificar documentos PDF usando a API Java](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Certificar documentos PDF usando a API de serviço da Web](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields)

### Certificar documentos PDF usando a API Java {#certify-pdf-documents-using-the-java-api}

Certifique um documento PDF usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signature-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de assinatura

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento PDF para certificar

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF a ser certificado usando seu construtor e transmitindo um valor de string que especifique o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Certificar o documento PDF

   Certifique o documento PDF chamando o método `SignatureServiceClient` do objeto `certify` e transmitindo os seguintes valores:

   * O objeto `com.adobe.idp.Document` que representa o documento PDF a ser certificado.
   * Um valor de string que representa o nome do campo de assinatura que conterá a assinatura.
   * Um objeto `Credential` que representa a credencial usada para certificar o documento PDF. Crie um objeto `Credential` invocando o método estático `Credential` do objeto `getInstance` e transmitindo um valor de string que especifica o valor alias que corresponde à credencial de segurança.
   * Um objeto `HashAlgorithm` que especifica um membro de dados estáticos que representa o algoritmo de hash usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi certificado.
   * Um valor de string que representa as informações de contato do assinante.
   * Um objeto `MDPPermissions` que especifica ações que podem ser executadas no documento PDF que invalida a assinatura.
   * Um objeto `PDFSignatureAppearanceOptions` que controla a aparência da assinatura certificada. Se desejar, modifique a aparência da assinatura chamando um método, como `setShowDate`.
   * Um valor de string que fornece uma explicação de quais ações invalidam a assinatura.
   * Um objeto `java.lang.Boolean` que especifica se a verificação de revogação deve ser executada no certificado do assinante. Se essa verificação de revogação for feita, ela será incorporada à assinatura. O padrão é `false`.
   * Um objeto `java.lang.Boolean` que especifica se o campo de assinatura que está sendo certificado está bloqueado. Se o campo estiver bloqueado, o campo de assinatura será marcado como somente leitura, suas propriedades não poderão ser modificadas e não poderão ser limpas por ninguém que não tenha as permissões necessárias. O padrão é `false`.
   * Um objeto `OCSPPreferences` que armazena preferências para suporte ao Online Certificate Status Protocol (OCSP). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`. Para obter informações sobre esse objeto, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Um objeto `CRLPreferences` que armazena as preferências de lista de revogação de certificado (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `TSPPreferences` que armazena preferências para suporte ao provedor de carimbo de data e hora (TSP). Por exemplo, depois de criar um objeto `TSPPreferences`, você pode definir o URL do servidor TSP chamando o método `TSPPreferences` do objeto `setTspServerURL`. Esse parâmetro é opcional e pode ser `null`. Para obter mais informações, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

   O método `certify` retorna um objeto `com.adobe.idp.Document` que representa o documento PDF certificado.

1. Salvar o documento PDF certificado como um arquivo PDF

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo.

**Consulte também:**

[Como certificar Documentos PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Start rápido (modo SOAP): Como certificar um documento PDF usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Certificar documentos PDF usando a API de serviço da Web {#certify-pdf-documents-using-the-web-service-api}

Certifique um documento PDF usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF para certificar

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF certificado.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF a ser certificado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo ao membro de dados `MTOM` o conteúdo da matriz de bytes.

1. Certificar o documento PDF

   Certifique o documento PDF chamando o método `SignatureServiceClient` do objeto `certify` e transmitindo os seguintes valores:

   * O objeto `BLOB` que representa o documento PDF a ser certificado.
   * Um valor de string que representa o nome do campo de assinatura que conterá a assinatura.
   * Um objeto `Credential` que representa a credencial usada para certificar o documento PDF. Crie um objeto `Credential` usando seu construtor e especifique o alias atribuindo um valor à propriedade `Credential` do objeto `alias`.
   * Um objeto `HashAlgorithm` que especifica um membro de dados estáticos que representa o algoritmo de hash usado para compilar o documento PDF. Por exemplo, você pode especificar `HashAlgorithm.SHA1` para usar o algoritmo SHA1.
   * Um valor booliano que especifica se o algoritmo hash é usado.
   * Um valor de string que representa o motivo pelo qual o documento PDF foi certificado.
   * Um valor de string que representa a localização do assinante.
   * Um valor de string que representa as informações de contato do assinante.
   * Um membro de dados estáticos de `MDPPermissions` objeto que especifica ações que podem ser executadas no documento PDF que invalidam a assinatura.
   * Um valor booliano que especifica se o objeto `MDPPermissions` que foi transmitido como valor de parâmetro anterior deve ser usado.
   * Um valor de string que explica quais ações invalidam a assinatura.
   * Um objeto `PDFSignatureAppearanceOptions` que controla a aparência da assinatura certificada. Crie um objeto `PDFSignatureAppearanceOptions` usando seu construtor. É possível modificar a aparência da assinatura definindo um de seus membros de dados.
   * Um objeto `System.Boolean` que especifica se a verificação de revogação deve ser executada no certificado do assinante. Se essa verificação de revogação for feita, ela será incorporada à assinatura. O padrão é `false`.
   * Um objeto `System.Boolean` que especifica se o campo de assinatura que está sendo certificado está bloqueado. Se o campo estiver bloqueado, o campo de assinatura será marcado como somente leitura, suas propriedades não poderão ser modificadas e não poderão ser limpas por ninguém que não tenha as permissões necessárias. O padrão é `false`.
   * Um objeto `System.Boolean` que especifica se o campo de assinatura está bloqueado. Ou seja, se você passar `true` para o parâmetro anterior, passe `true` para esse parâmetro.
   * Um objeto `OCSPPreferences` que armazena preferências para suporte ao Protocolo de status de certificado on-line (OCSP), que fornece informações sobre o status da credencial usada para certificar o documento PDF. Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `CRLPreferences` que armazena as preferências de lista de revogação de certificado (CRL). Se a verificação de revogação não for feita, esse parâmetro não será usado e você poderá especificar `null`.
   * Um objeto `TSPPreferences` que armazena preferências para suporte ao provedor de carimbo de data e hora (TSP). Por exemplo, depois de criar um objeto `TSPPreferences`, você pode definir o URL do TSP definindo o membro de dados `TSPPreferences` do objeto `tspServerURL`. Esse parâmetro é opcional e pode ser `null`.

   O método `certify` retorna um objeto `BLOB` que representa o documento PDF certificado.

1. Salvar o documento PDF certificado como um arquivo PDF

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF que conterá o documento PDF certificado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` que foi retornado pelo método `certify`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `binaryData`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Como certificar Documentos PDF](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificando Assinaturas Digitais {#verifying-digital-signatures}

Assinaturas digitais podem ser verificadas para garantir que um documento PDF assinado não foi modificado e que a assinatura digital é válida. Ao verificar uma assinatura digital, você pode verificar o status da assinatura e as propriedades da assinatura, como a identidade do assinante. Antes de confiar em uma assinatura digital, é recomendável que você a verifique. Ao verificar uma assinatura digital, consulte um documento PDF que contém uma assinatura digital.

Suponha que a identidade do assinante seja desconhecida. Ao abrir o documento PDF no Acrobat, uma mensagem de aviso indica que a identidade do assinante é desconhecida, como mostra a ilustração a seguir.

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

Da mesma forma, ao verificar programaticamente uma assinatura digital, você pode determinar o status da identidade do assinante. Por exemplo, se você verificar a assinatura digital no documento mostrado na ilustração anterior, o resultado seria que a identidade do assinante é desconhecida.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura e verificação de assinaturas digitais, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-6}

Para verificar uma assinatura digital, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém a assinatura a ser verificada.
1. Defina opções de tempo de execução de PKI.
1. Verifique a assinatura digital.
1. Determine o status da assinatura.
1. Determine a identidade do assinante.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação de serviço de assinatura, crie um cliente de serviço de assinatura.

**Obtenha o documento PDF que contém a assinatura para verificar**

Para verificar uma assinatura usada para assinar digitalmente ou certificar um documento PDF, obtenha um documento PDF que contenha uma assinatura.

**Definir opções de tempo de execução de PKI**

Defina estas opções de tempo de execução PKI que o serviço de assinatura usa ao verificar assinaturas em um documento PDF:

* Hora da verificação
* Verificação de revogação
* Valores de carimbo de data e hora

Como parte da configuração dessas opções, você pode especificar o tempo de verificação. Por exemplo, você pode selecionar a hora atual (a hora no computador do validador), que indica o uso da hora atual. Para obter informações sobre os diferentes valores de tempo, consulte o valor de lista discriminada `VerificationTime` em [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Também é possível especificar se a verificação de revogação deve ser executada como parte do processo de verificação. Por exemplo, você pode executar uma verificação de revogação para determinar se o certificado foi revogado. Para obter informações sobre as opções de verificação de revogação, consulte o valor de lista discriminada `RevocationCheckStyle` em [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Para executar a verificação de revogação em um certificado, especifique um URL para um servidor de lista de revogação de certificado (CRL) usando um objeto `CRLOptionSpec`. No entanto, se você não especificar um URL para o servidor CRL, o serviço de assinatura obterá o URL do certificado.

Em vez de usar um servidor CRL, você pode usar um servidor OCSP (protocolo de status de certificado) online ao executar a verificação de revogação. Normalmente, ao usar um servidor OCSP em vez de um servidor CRL, a verificação de revogação é executada mais rapidamente. (Consulte [Protocolo de Estado de Certificado Online](https://tools.ietf.org/html/rfc2560).)

Você pode definir a ordem do servidor CRL e OCSP que o serviço de assinatura usa usando Aplicativos e Serviços de Adobe. Por exemplo, se o servidor OCSP for definido primeiro em Aplicativos e Serviços de Adobe, então o servidor OCSP será marcado, seguido pelo servidor CRL.

Se você não executar a verificação de revogação, o serviço de Assinatura não verificará se o certificado foi revogado. Ou seja, as informações do CRL e do servidor OCSP são ignoradas.

>[!NOTE]
>
>Você pode substituir o URL especificado no certificado usando um `CRLOptionSpec` e um objeto `OCSPOptionSpec`. Por exemplo, para substituir o servidor CRL, você pode chamar o método `CRLOptionSpec` do objeto `setLocalURI`.

O carimbo de data e hora é o processo de rastreamento da hora em que um documento assinado ou certificado foi modificado. Depois que um documento é assinado, ninguém pode modificá-lo. O carimbo de data e hora ajuda a reforçar a validade de um documento assinado ou certificado. É possível definir opções de carimbo de data e hora usando um objeto `TSPOptionSpec`. Por exemplo, você pode especificar o URL de um servidor de provedor de carimbo de data e hora (TSP).

>[!NOTE]
>
>Nos start rápidos do serviço da Web e Java, o tempo de verificação é definido como `VerificationTime.CURRENT_TIME` e a verificação de revogação é definida como `RevocationCheckStyle.BestEffort`. Como nenhuma informação CRL ou OCSP do servidor é especificada, as informações do servidor são obtidas do certificado.

**Verificar a assinatura digital**

Para verificar uma assinatura com êxito, especifique o nome totalmente qualificado do campo de assinatura que contém a assinatura, como `form1[0].#subform[1].SignatureField3[3]`. Ao usar um campo de formulário XFA, você também pode usar o nome parcial do campo de assinatura: `SignatureField3`.

Por padrão, o serviço de assinatura limita o tempo que um documento pode ser assinado após o tempo de validação para 65 minutos. Se um usuário tentar verificar uma assinatura no momento atual e a hora de assinatura for posterior à hora atual e estiver dentro de 65 minutos, o serviço de assinatura não criará um erro de verificação.

>[!NOTE]
>
>Para obter outros valores necessários ao verificar uma assinatura, consulte [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Determine o status da assinatura**

Como parte da verificação de uma assinatura digital, você pode verificar o status da assinatura.

**Determinar a identidade do assinante**

Você pode determinar a identidade do assinante, que pode ser um dos seguintes valores:

* **Desconhecido**: Este assinante é desconhecido porque não é possível executar a verificação do assinante.
* **Confiável**: Este assinante é confiável.
* **Não confiável**: Este assinante não é confiável.

**Consulte também:**

[Verificar assinaturas digitais usando a API Java](#verify-digital-signatures-using-the-java-api)

[Verificar assinaturas digitais usando a API de serviço da Web](#verify-digital-signatures-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar assinaturas digitais usando a API Java {#verify-digital-signatures-using-the-java-api}

Verifique uma assinatura digital usando a API do serviço de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signature-client.jar, no classpath do seu projeto Java.

1. Criar um cliente de assinatura

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento PDF que contém a assinatura para verificar

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF que contém a assinatura a ser verificada usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Definir opções de tempo de execução de PKI

   * Crie um objeto `PKIOptions` usando seu construtor.
   * Defina o tempo de verificação chamando o método `PKIOptions` do objeto `setVerificationTime` e transmitindo um valor de lista discriminada `VerificationTime` que especifica o tempo de verificação.
   * Defina a opção de verificação de revogação chamando o método `PKIOptions` do objeto `setRevocationCheckStyle` e transmitindo um valor de lista discriminada `RevocationCheckStyle` que especifica se a verificação de revogação deve ser executada.

1. Verificar a assinatura digital

   Verifique a assinatura chamando o método `SignatureServiceClient` do objeto `verify2` e transmitindo os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que contém um documento PDF assinado digitalmente ou certificado.
   * Um valor de string que representa o nome do campo de assinatura que contém a assinatura a ser verificada.
   * Um objeto `PKIOptions` que contém opções de tempo de execução de PKI.
   * Uma instância `VerifySPIOptions` que contém informações de SPI. Você pode especificar `null` para este parâmetro.

   O método `verify2` retorna um objeto `PDFSignatureVerificationInfo` que contém informações que podem ser usadas para verificar a assinatura digital.

1. Determine o status da assinatura

   * Determine o status da assinatura chamando o método `PDFSignatureVerificationInfo` do objeto `getStatus`. Este método retorna um objeto `SignatureStatus` que especifica o status da assinatura. Por exemplo, se um documento PDF assinado não for modificado, esse método retornará `SignatureStatus.DocumentSigNoChanges`.

1. Determinar a identidade do assinante

   * Determine a identidade do assinante chamando o método `PDFSignatureVerificationInfo` do objeto `getSigner`. Este método retorna um objeto `IdentityInformation`.
   * Chame o método `IdentityInformation` do objeto `getStatus` para determinar a identidade do assinante. Este método retorna um valor de lista discriminada `IdentityStatus` que especifica a identidade. Por exemplo, se o assinante for confiável, esse método retornará `IdentityStatus.TRUSTED`.

**Consulte também:**

[Verificação de assinaturas digitais](#verify-digital-signatures-using-the-java-api)

[Start rápido (modo SOAP): Verificação de uma assinatura digital usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificar assinaturas digitais usando a API de serviço da Web {#verify-digital-signatures-using-the-web-service-api}

Verifique uma assinatura digital usando a Signature Service API (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF que contém a assinatura para verificar

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que contém uma assinatura digital ou certificada para verificação.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo a propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Definir opções de tempo de execução de PKI

   * Crie um objeto `PKIOptions` usando seu construtor.
   * Defina o tempo de verificação atribuindo ao membro de dados `PKIOptions` do objeto &lt;a0/> um valor de lista discriminada `VerificationTime` que especifica o tempo de verificação.`verificationTime`
   * Defina a opção de verificação de revogação atribuindo ao membro de dados `PKIOptions` do objeto `revocationCheckStyle` um valor de lista discriminada `RevocationCheckStyle` que especifica se a verificação de revogação deve ser executada.

1. Verificar a assinatura digital

   Verifique a assinatura chamando o método `SignatureServiceClient` do objeto `verify2` e transmitindo os seguintes valores:

   * O objeto `BLOB` que contém um documento PDF assinado digitalmente ou certificado.
   * Um valor de string que representa o nome do campo de assinatura que contém a assinatura a ser verificada.
   * Um objeto `PKIOptions` que contém opções de tempo de execução de PKI.
   * Uma instância `VerifySPIOptions` que contém informações de SPI. Você pode especificar `null` para este parâmetro.

   O método `verify2` retorna um objeto `PDFSignatureVerificationInfo` que contém informações que podem ser usadas para verificar a assinatura digital.

1. Determine o status da assinatura

   Determine o status da assinatura obtendo o valor do `PDFSignatureVerificationInfo` membro de dados `status` do objeto. Esse membro de dados armazena um objeto `SignatureStatus` que especifica o status da assinatura. Por exemplo, se um documento PDF assinado for modificado, o membro de dados `status` armazenará o valor `SignatureStatus.DocumentSigNoChanges`.

1. Determinar a identidade do assinante

   * Determine a identidade do assinante recuperando o valor do `PDFSignatureVerificationInfo` membro de dados `signer` do objeto. Esse membro retorna um objeto `IdentityInformation`.
   * Recupere o membro de dados `IdentityInformation` do objeto `status` para determinar a identidade do assinante. Esse membro de dados retorna um valor de lista discriminada `IdentityStatus` que especifica a identidade. Por exemplo, se o assinante for confiável, esse membro retornará `IdentityStatus.TRUSTED`.

**Consulte também:**

[Verificação de assinaturas digitais](#verify-digital-signatures-using-the-java-api)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verificando várias assinaturas digitais {#verifying-multiple-digital-signatures}

A AEM Forms fornece os meios de verificar todas as assinaturas digitais localizadas em um documento PDF. Considere que um documento PDF contém várias assinaturas digitais como resultado de um processo de negócios que requer assinaturas de vários assinantes. Por exemplo, considere uma transação financeira que exija a assinatura de um agente de empréstimo e de um gerente. Você pode usar a API Java do serviço de assinatura ou a API do serviço da Web para verificar todas as assinaturas no documento PDF. Ao verificar várias assinaturas digitais, você pode verificar o status e as propriedades de cada assinatura. Antes de confiar em uma assinatura digital, é recomendável que você a verifique. É recomendável que você esteja familiarizado com a verificação de uma única assinatura digital.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura e verificação de assinaturas digitais, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-7}

Para verificar várias assinaturas digitais, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente de assinatura.
1. Obtenha o documento PDF que contém as assinaturas para verificação.
1. Defina opções de tempo de execução de PKI.
1. Recupere todas as assinaturas digitais.
1. Iterar por todas as assinaturas.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação de serviço de assinatura, crie um cliente de serviço de assinatura.

**Obtenha o documento PDF que contém as assinaturas para verificar**

Para verificar uma assinatura usada para assinar digitalmente ou certificar um documento PDF, obtenha um documento PDF que contenha uma assinatura.

**Definir opções de tempo de execução de PKI**

Defina estas opções de tempo de execução PKI que o serviço de assinatura usa ao verificar todas as assinaturas em um documento PDF:

* Hora da verificação
* Verificação de revogação
* Valores de carimbo de data e hora

Como parte da configuração dessas opções, você pode especificar o tempo de verificação. Por exemplo, você pode selecionar a hora atual (a hora no computador do validador), que indica o uso da hora atual. Para obter informações sobre os diferentes valores de tempo, consulte o valor de lista discriminada `VerificationTime` em [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Também é possível especificar se a verificação de revogação deve ser executada como parte do processo de verificação. Por exemplo, você pode executar uma verificação de revogação para determinar se o certificado foi revogado. Para obter informações sobre as opções de verificação de revogação, consulte o valor de lista discriminada `RevocationCheckStyle` em [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

Para executar a verificação de revogação em um certificado, especifique um URL para um servidor de lista de revogação de certificado (CRL) usando um objeto `CRLOptionSpec`. No entanto, se você não especificar um URL para um servidor CRL, o serviço de assinatura obterá o URL do certificado.

Em vez de usar um servidor CRL, você pode usar um servidor OCSP (protocolo de status de certificado) online ao executar a verificação de revogação. Normalmente, ao usar um servidor OCSP em vez de um servidor CRL, a verificação de revogação é executada mais rapidamente. (Consulte [Protocolo de Estado de Certificado Online](https://tools.ietf.org/html/rfc2560).)

Você pode definir a ordem do servidor CRL e OCSP que o serviço de assinatura usa usando Aplicativos e Serviços de Adobe. Por exemplo, se o servidor OCSP for definido primeiro em Aplicativos e Serviços de Adobe, o servidor OCSP será marcado, seguido pelo servidor CRL.

Se você não executar a verificação de revogação, o serviço de Assinatura não verificará se o certificado foi revogado. Ou seja, as informações do CRL e do servidor OCSP são ignoradas.

>[!NOTE]
>
>Você pode substituir o URL especificado no certificado usando um `CRLOptionSpec` e um objeto `OCSPOptionSpec`. Por exemplo, para substituir o servidor CRL, você pode chamar o método `CRLOptionSpec` do objeto `setLocalURI`.

O carimbo de data e hora é o processo de rastreamento da hora em que um documento assinado ou certificado foi modificado. Depois que um documento é assinado, ninguém pode modificá-lo. O carimbo de data e hora ajuda a reforçar a validade de um documento assinado ou certificado. É possível definir opções de carimbo de data e hora usando um objeto `TSPOptionSpec`. Por exemplo, você pode especificar o URL de um servidor de provedor de carimbo de data e hora (TSP).

>[!NOTE]
>
>Nos start rápidos do serviço da Web e Java, o tempo de verificação é definido como `VerificationTime.CURRENT_TIME` e a verificação de revogação é definida como `RevocationCheckStyle.BestEffort`. Como nenhuma informação CRL ou OCSP do servidor é especificada, as informações do servidor são obtidas do certificado.

**Recuperar todas as assinaturas digitais**

Para verificar todas as assinaturas digitais localizadas em um documento PDF, recupere as assinaturas digitais do documento PDF. Todas as assinaturas são retornadas em uma lista. Como parte da verificação de uma assinatura digital, verifique o status da assinatura.

>[!NOTE]
>
>Diferente de quando você verifica uma única assinatura digital, ao verificar várias assinaturas, não é necessário especificar o nome do campo de assinatura.

**Iterar por todas as assinaturas**

Iterar por cada assinatura. Ou seja, para cada assinatura, verifique a assinatura digital e verifique a identidade do assinante e o status de cada assinatura. (Consulte [Verificando Assinaturas Digitais](#verify-digital-signatures-using-the-java-api).)

>[!NOTE]
>
>Você não precisa repetir todas as assinaturas se o requisito for o documento inteiro.

**Consulte também:**

[Verificar várias assinaturas digitais usando a API Java](#verify-digital-signatures-using-the-java-api)

[Verificação de várias assinaturas digitais usando a API de serviço da Web](#verify-digital-signatures-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verifique várias assinaturas digitais usando a API Java {#verify-multiple-digital-signatures-using-the-java-api}

Verifique várias assinaturas digitais usando a API do serviço de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signature-client.jar, no classpath do seu projeto Java.

1. Criar um cliente de assinatura

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento PDF que contém as assinaturas para verificar

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF que contém várias assinaturas digitais para verificar usando seu construtor. Passe um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Definir opções de tempo de execução de PKI

   * Crie um objeto `PKIOptions` usando seu construtor.
   * Defina o tempo de verificação chamando o método `PKIOptions` do objeto `setVerificationTime` e transmitindo um valor de lista discriminada `VerificationTime` que especifica o tempo de verificação.
   * Defina a opção de verificação de revogação chamando o método `PKIOptions` do objeto `setRevocationCheckStyle` e transmitindo um valor de lista discriminada `RevocationCheckStyle` que especifica se a verificação de revogação deve ser executada.

1. Recuperar todas as assinaturas digitais

   Chame o método `SignatureServiceClient` do objeto `verifyPDFDocument` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que contém um documento PDF que contém várias assinaturas digitais.
   * Um objeto `PKIOptions` que contém opções de tempo de execução de PKI.
   * Uma instância `VerifySPIOptions` que contém informações de SPI. Você pode especificar `null` para este parâmetro.

   O método `verifyPDFDocument` retorna um objeto `PDFDocumentVerificationInfo` que contém informações sobre todas as assinaturas digitais localizadas no documento PDF.

1. Iterar por todas as assinaturas

   * Interaja por todas as assinaturas invocando o método `PDFDocumentVerificationInfo` do objeto `getVerificationInfos`. Este método retorna um objeto `java.util.List` em que cada elemento é um objeto `PDFSignatureVerificationInfo`. Use um objeto `java.util.Iterator` para iterar pela lista de assinaturas.
   * Usando o objeto `PDFSignatureVerificationInfo`, é possível executar tarefas como determinar o status da assinatura chamando o método `PDFSignatureVerificationInfo` do objeto `getStatus`. Este método retorna um objeto `SignatureStatus` cujo membro de dados estáticos informa sobre o status da assinatura. Por exemplo, se a assinatura for desconhecida, esse método retornará `SignatureStatus.DocumentSignatureUnknown`.

**Consulte também:**

[Verificando várias assinaturas digitais](#verifying-multiple-digital-signatures)

[Start rápido (modo SOAP): Verificação de várias assinaturas digitais usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Verificação de assinaturas digitais](#verify-digital-signatures-using-the-java-api)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Verificação de várias assinaturas digitais usando a API de serviço da Web {#verifying-multiple-digital-signatures-using-the-web-service-api}

Verifique várias assinaturas digitais usando a Signature Service API (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF que contém as assinaturas para verificar

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` armazena um documento PDF que contém várias assinaturas digitais para verificação.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo a propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Definir opções de tempo de execução de PKI

   * Crie um objeto `PKIOptions` usando seu construtor.
   * Defina o tempo de verificação atribuindo ao membro de dados `PKIOptions` do objeto &lt;a0/> um valor de lista discriminada `VerificationTime` que especifica o tempo de verificação.`verificationTime`
   * Defina a opção de verificação de revogação atribuindo ao membro de dados `PKIOptions` do objeto `revocationCheckStyle` um valor de lista discriminada `RevocationCheckStyle` que especifica se a verificação de revogação deve ser executada.

1. Recuperar todas as assinaturas digitais

   Chame o método `SignatureServiceClient` do objeto `verifyPDFDocument` e passe os seguintes valores:

   * Um objeto `BLOB` que contém um documento PDF que contém várias assinaturas digitais.
   * Um objeto `PKIOptions` que contém opções de tempo de execução de PKI.
   * Uma instância `VerifySPIOptions` que contém informações de SPI. Você pode especificar null para esse parâmetro.

   O método `verifyPDFDocument` retorna um objeto `PDFDocumentVerificationInfo` que contém informações sobre todas as assinaturas digitais localizadas no documento PDF.

1. Iterar por todas as assinaturas

   * Faça iterações em todas as assinaturas obtendo o membro de dados `PDFDocumentVerificationInfo` do objeto `verificationInfos`. Esse membro de dados retorna uma matriz `Object` na qual cada elemento é um objeto `PDFSignatureVerificationInfo`.
   * Usando o objeto `PDFSignatureVerificationInfo`, é possível executar tarefas como determinar o status da assinatura obtendo o membro de dados `PDFSignatureVerificationInfo` do objeto `status`. Esse membro de dados retorna um objeto `SignatureStatus` cujo membro de dados estáticos informa você sobre o status da assinatura. Por exemplo, se a assinatura for desconhecida, esse método retornará `SignatureStatus.DocumentSignatureUnknown`.

**Consulte também:**

[Verificando várias assinaturas digitais](#verifying-multiple-digital-signatures)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Remoção de assinaturas digitais {#removing-digital-signatures}

As assinaturas digitais devem ser removidas de um campo de assinatura antes que uma assinatura digital mais recente possa ser aplicada. Uma assinatura digital não pode ser substituída. Se você tentar aplicar uma assinatura digital a um campo de assinatura que contenha uma assinatura, ocorrerá uma exceção.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de assinatura, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-8}

Para remover uma assinatura digital de um campo de assinatura, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
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
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo os arquivos da biblioteca Java da AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de assinatura**

Antes de executar programaticamente uma operação de serviço de assinatura, você deve criar um cliente de serviço de assinatura.

**Obtenha o documento PDF que contém uma assinatura para remover**

Para remover uma assinatura de um documento PDF, é necessário obter um documento PDF que contenha uma assinatura.

**Remover a assinatura digital do campo de assinatura**

Para remover com êxito uma assinatura digital de um documento PDF, você deve especificar o nome do campo de assinatura que contém a assinatura digital. Além disso, você deve ter permissão para remover a assinatura digital; caso contrário, ocorrerá uma exceção.

**Salvar o documento PDF como um arquivo PDF**

Depois que o serviço de assinatura remover uma assinatura digital de um campo de assinatura, você poderá salvar o documento PDF como um arquivo PDF para que os usuários possam abri-lo no Acrobat ou no Adobe Reader.

**Consulte também:**

[Remover assinaturas digitais usando a API Java](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Remover assinaturas digitais usando a API de serviço da Web](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Adicionar campos de assinatura](digitally-signing-certifying-documents.md#adding-signature-fields)

### Remova assinaturas digitais usando a API Java {#remove-digital-signatures-using-the-java-api}

Remova uma assinatura digital usando a API de assinatura (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-signature-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente de assinatura.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `SignatureServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Obtenha o documento PDF que contém uma assinatura para remover

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF que contém a assinatura a ser removida usando seu construtor e transmitindo um valor de string que especifica o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Remover a assinatura digital do campo de assinatura

   Remova uma assinatura digital de um campo de assinatura chamando o método `SignatureServiceClient` do objeto `clearSignatureField` e transmitindo os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento PDF que contém a assinatura a ser removida.
   * Um valor de string que especifica o nome do campo de assinatura que contém a assinatura digital.

   O método `clearSignatureField` retorna um objeto `com.adobe.idp.Document` que representa o documento PDF do qual a assinatura digital foi removida.

1. Salvar o documento PDF como um arquivo PDF

   * Crie um objeto `java.io.File` e verifique se a extensão do arquivo é .pdf.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile`. Passe o objeto `java.io.File` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo. Certifique-se de usar o objeto `Document` retornado pelo método `clearSignatureField`.

**Consulte também:**

[Como remover assinaturas digitais](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Start rápido (modo SOAP): Remoção de uma assinatura digital usando a API Java](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Remover assinaturas digitais usando a API de serviço da Web {#remove-digital-signatures-using-the-web-service-api}

Remova uma assinatura digital usando a API de assinatura (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente de assinatura

   * Crie um objeto `SignatureServiceClient` usando seu construtor padrão.
   * Crie um objeto `SignatureServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/SignatureService?WSDL`). Não é necessário usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `SignatureServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `SignatureServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `SignatureServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Obtenha o documento PDF que contém uma assinatura para remover

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que contém uma assinatura digital a ser removida.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF assinado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Remover a assinatura digital do campo de assinatura

   Remova a assinatura digital chamando o método `SignatureServiceClient` do objeto `clearSignatureField` e transmitindo os seguintes valores:

   * Um objeto `BLOB` que contém o documento PDF assinado.
   * Um valor de string que representa o nome do campo de assinatura que contém a assinatura digital a ser removida.

   O método `clearSignatureField` retorna um objeto `BLOB` que representa o documento PDF do qual a assinatura digital foi removida.

1. Salvar o documento PDF como um arquivo PDF

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF que contém um campo de assinatura vazio e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` que foi retornado pelo método `sign`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes no arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Como remover assinaturas digitais](digitally-signing-certifying-documents.md#removing-digital-signatures)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
