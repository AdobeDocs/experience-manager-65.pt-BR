---
title: Determinar Se Os Documentos São Compatíveis Com O PDF/A
description: Use o serviço Assembler para determinar se um documento PDF é compatível com PDF/A usando a API Java e a API de serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 096fd2ac-616f-484a-b093-9d98b2f87093
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2065'
ht-degree: 2%

---

# Determinar Se Os Documentos São Compatíveis Com O PDF/A {#determining-whether-documents-are-pdf-a-compliant}

Você pode determinar se um documento de PDF é compatível com PDF/A usando o serviço Assembler. Um documento PDF/A existe como um formato de arquivo destinado à preservação do conteúdo do documento a longo prazo. As fontes são incorporadas no documento e o arquivo é descompactado. Como resultado, um documento PDF/A geralmente é maior do que um documento PDF padrão. Além disso, um documento PDF/A não contém conteúdo de áudio e vídeo.

A especificação PDF/A-1 consiste em dois níveis de conformidade, a saber, A e B. A principal diferença entre os dois níveis é o suporte à estrutura lógica (acessibilidade), que não é necessário para o nível de conformidade B. Independentemente do nível de conformidade, o PDF/A-1 determina que todas as fontes sejam incorporadas no documento PDF/A gerado. No momento, somente o PDF/A-1b é suportado na validação (e na conversão).

Para o propósito desta discussão, suponha que o seguinte documento DDX seja usado.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

Neste documento DDX, o elemento `DocumentInformation` instrui o serviço Assembler a retornar informações sobre o documento PDF de entrada. No elemento `DocumentInformation`, o elemento `PDFAValidation` instrui o serviço Assembler a indicar se o documento de PDF de entrada é compatível com PDF/A.

O serviço Assembler retorna informações que especificam se o documento de PDF de entrada é compatível com PDF/A em um documento XML que contém um elemento `PDFAConformance`. Se o documento de PDF de entrada for compatível com PDF/A, o valor do atributo `isCompliant` do elemento `PDFAConformance` será `true`. Se o documento PDF não for compatível com PDF/A, o valor do atributo `isCompliant` do elemento `PDFAConformance` será `false`.

>[!NOTE]
>
>Como o documento DDX especificado nesta seção contém um elemento `DocumentInformation`, o serviço Assembler retorna dados XML em vez de um documento PDF. Ou seja, o serviço Assembler não monta ou desmonta um documento PDF; ele retorna informações sobre o documento PDF de entrada dentro de um documento XML.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço do Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para determinar se um documento de PDF é compatível com PDF/A, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDF Assembler.
1. Consulte um documento DDX existente.
1. Consulte um documento de PDF usado para determinar a conformidade com PDF/A.
1. Definir opções de tempo de execução.
1. Recupere informações sobre o documento PDF.
1. Salve o documento XML retornado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado. Para obter informações sobre a localização de todos os arquivos JAR do AEM Forms, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referenciar um documento DDX existente**

Um documento DDX deve ser referenciado para executar uma operação de serviço do Assembler. Para determinar se um documento de PDF de entrada é compatível com PDF/A, verifique se o documento DDX contém o elemento `PDFAValidation` em um elemento `DocumentInformation`. O elemento `PDFAValidation` instrui o serviço Assembler a retornar um documento XML que especifica se o documento de PDF de entrada é compatível com PDF/A.

**Referenciar um documento PDF usado para determinar a conformidade PDF/A**

Um documento PDF deve ser referenciado e passado ao serviço Assembler para determinar se o documento PDF é compatível com PDF/A.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que você pode definir, consulte a referência de classe `AssemblerOptionSpec` na [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recuperar informações sobre o documento PDF**

Depois de criar o cliente de serviço do Assembler, fazer referência ao documento DDX, referenciar um documento PDF interativo e definir opções de tempo de execução, você poderá invocar a operação `invokeDDX`. Como o documento DDX contém o elemento `DocumentInformation`, o serviço Assembler retorna dados XML em vez de um documento PDF.

**Salvar o documento XML retornado**

O documento XML que o serviço Assembler retorna especifica se o documento de PDF de entrada é compatível com PDF/A. Por exemplo, se o documento de PDF de entrada não for compatível com PDF/A, o serviço do Assembler retornará um documento XML que contém o seguinte elemento:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Salve o documento XML como um arquivo XML para que você possa abrir o arquivo e exibir os resultados.

**Consulte também**

[Determine se um documento é compatível com o PDF/A usando a API Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determine se um documento é compatível com o PDF/A usando a API de serviço Web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determine se um documento é compatível com o PDF/A usando a API Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determine se um documento de PDF é compatível com PDF/A usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente PDF Assembler.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Consulte um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do arquivo DDX. Para determinar se o documento PDF é compatível com PDF/A, verifique se o documento DDX contém o elemento `PDFAValidation` contido em um elemento `DocumentInformation`.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Consulte um documento de PDF usado para determinar a conformidade com PDF/A.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local de um documento PDF que é usado para determinar a conformidade PDF/A.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream` que contém o documento PDF.
   * Crie um objeto `java.util.Map` que seja usado para armazenar o documento de PDF de entrada usando um construtor `HashMap`.
   * Adicione uma entrada ao objeto `java.util.Map` invocando seu método `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem especificado no documento DDX. Por exemplo, o valor do elemento de origem no documento DDX introduzido nesta seção é Loan.pdf.
      * Um objeto `com.adobe.idp.Document` que contém o documento de PDF de entrada.

1. Definir opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos da sua empresa invocando um método que pertença ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, chame o método `setFailOnError` do objeto `AssemblerOptionSpec` e passe `false`.

1. Recupere informações sobre o documento PDF.

   Chame o método `invokeDDX` do objeto `AssemblerServiceClient` e passe os seguintes valores obrigatórios:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX a ser usado
   * Um objeto `java.util.Map` que contém o arquivo de PDF de entrada usado para determinar a conformidade com PDF/A
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução

   O método `invokeDDX` retorna um objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contém dados XML que especificam se o documento de PDF de entrada é compatível com PDF/A.

1. Salve o documento XML retornado.

   Para obter dados XML que especificam se o documento de PDF de entrada é um documento PDF/A, execute as seguintes ações:

   * Invoque o método `getDocuments` do objeto `AssemblerResult`. Isso retorna um objeto `java.util.Map`.
   * Repita o objeto `java.util.Map` até encontrar o objeto `com.adobe.idp.Document` resultante.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para extrair o documento XML. Salve os dados XML como um arquivo XML.

**Consulte também**

[Início Rápido (modo SOAP): Determinando se um documento é compatível com PDF/A usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) (modo SOAP)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determine se um documento é compatível com o PDF/A usando a API de serviço Web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determine se um documento de PDF é compatível com PDF/A usando a API de serviço do Assembler (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente PDF Assembler.

   * Crie um objeto `AssemblerServiceClient` usando seu construtor padrão.
   * Crie um objeto `AssemblerServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `AssemblerServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Consulte um documento DDX existente.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento DDX.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento DDX e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` com o conteúdo da matriz de bytes.

1. Consulte um documento de PDF usado para determinar a conformidade com PDF/A.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento de PDF de entrada.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` com o conteúdo da matriz de bytes.
   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de coleção é usado para armazenar o documento PDF.
   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Atribua um valor de cadeia de caracteres que represente o nome da chave para o campo `key` do objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX.
   * Atribua o objeto `BLOB` que armazena o documento PDF ao campo `value` do objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Adicione o objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` ao objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque o método `Add` do objeto `MyMapOf_xsd_string_To_xsd_anyType` e passe o objeto `MyMapOf_xsd_string_To_xsd_anyType`.

1. Definir opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos comerciais atribuindo um valor a um membro de dados que pertença ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, atribua `false` ao membro de dados `failOnError` do objeto `AssemblerOptionSpec`.

1. Recupere informações sobre o documento PDF.

   Chame o método `invoke` do objeto `AssemblerServiceService` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX.
   * O objeto `MyMapOf_xsd_string_To_xsd_anyType` que contém o documento de PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem de PDF, e seus valores devem ser o objeto `BLOB` que corresponde ao arquivo de PDF de entrada.
   * Um objeto `AssemblerOptionSpec` que especifica opções de tempo de execução.

   O método `invoke` retorna um objeto `AssemblerResult` que contém dados XML que especificam se o documento de PDF de entrada é um documento PDF/A.

1. Salve o documento XML retornado.

   Para obter dados XML que especificam se o documento de PDF de entrada é um documento PDF/A, execute as seguintes ações:

   * Acesse o campo `documents` do objeto `AssemblerResult`, que é um objeto `Map` que contém os dados XML que especificam se o documento de PDF de entrada é um documento PDF/A.
   * Repita através do objeto `Map` para obter cada documento resultante. Em seguida, converta o valor desse membro de matriz em um `BLOB`.
   * Extraia os dados binários que representam os dados XML acessando o campo `MTOM` do objeto `BLOB`. Esse campo armazena uma matriz de bytes que você pode gravar como um arquivo XML.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
