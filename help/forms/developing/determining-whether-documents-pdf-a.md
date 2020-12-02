---
title: Determinar se os Documentos são compatíveis com PDF/A
seo-title: Determinar se os Documentos são compatíveis com PDF/A
description: 'null'
seo-description: nulo
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2069'
ht-degree: 0%

---


# Determinando se os Documentos são compatíveis com PDF/A {#determining-whether-documents-are-pdf-a-compliant}

É possível determinar se um documento PDF é compatível com PDF/A usando o serviço Assembler. Um documento PDF/A existe como um formato de arquivo destinado à preservação de longo prazo do conteúdo do documento. As fontes são incorporadas no documento e o arquivo é descompactado. Como resultado, um documento PDF/A geralmente é maior do que um documento PDF padrão. Além disso, um documento PDF/A não contém conteúdo de áudio e vídeo.

A especificação PDF/A-1 consiste em dois níveis de conformidade, a A e a B. A principal diferença entre os dois níveis é o suporte à estrutura lógica (acessibilidade), que não é necessário para o nível de conformidade B. Independentemente do nível de conformidade, o PDF/A-1 determina que todas as fontes sejam incorporadas no documento PDF/A gerado. No momento, apenas o PDF/A-1b é suportado na validação (e conversão).

Para a finalidade desta discussão, suponha que o seguinte documento DX seja usado.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

Dentro desse documento DDX, o elemento `DocumentInformation` instrui o serviço Assembler a retornar informações sobre o documento PDF de entrada. No elemento `DocumentInformation`, o elemento `PDFAValidation` instrui o serviço Assembler a indicar se o documento PDF de entrada é compatível com PDF/A.

O serviço Assembler retorna informações que especificam se o documento PDF de entrada é compatível com PDF/A em um documento XML que contém um elemento `PDFAConformance`. Se o documento PDF de entrada for compatível com PDF/A, o valor do atributo `PDFAConformance` do elemento `isCompliant` será `true`. Se o documento PDF não for compatível com PDF/A, o valor do atributo `PDFAConformance` do elemento `isCompliant` será `false`.

>[!NOTE]
>
>Como o documento DX especificado nesta seção contém um elemento `DocumentInformation`, o serviço Assembler retorna dados XML em vez de um documento PDF. Ou seja, o serviço Assembler não monta nem desmonta um documento PDF; ele retorna informações sobre o documento PDF de entrada em um documento XML.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para determinar se um documento PDF é compatível com PDF/A, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente do Montador de PDF.
1. Faça referência a um documento DDX existente.
1. Faça referência a um documento PDF usado para determinar a conformidade do PDF/A.
1. Defina as opções de tempo de execução.
1. Recupere informações sobre o documento PDF.
1. Salve o documento XML retornado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

se a AEM Forms for implantada em um servidor de aplicativos J2EE compatível que não seja JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual a AEM Forms está implantada. Para obter informações sobre a localização de todos os arquivos AEM Forms JAR, consulte [Incluindo arquivos da biblioteca AEM Forms Java](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente de Montador de PDF**

Antes de poder executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para executar uma operação de serviço do Assembler. Para determinar se um documento PDF de entrada é compatível com PDF/A, verifique se o documento DDX contém o elemento `PDFAValidation` em um elemento `DocumentInformation`. O elemento `PDFAValidation` instrui o serviço Assembler a retornar um documento XML que especifica se o documento PDF de entrada é compatível com PDF/A.

**Referência a um documento PDF usado para determinar a conformidade do PDF/A**

Um documento PDF deve ser referenciado e passado ao serviço Assembler para determinar se o documento PDF é compatível com PDF/A.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando uma tarefa se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte a referência de classe `AssemblerOptionSpec` em [Referência de API da AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recuperar informações sobre o documento PDF**

Depois de criar o cliente do serviço Assembler, consulte o documento DDX, faça referência a um documento PDF interativo e defina as opções de tempo de execução, você pode chamar a operação `invokeDDX`. Como o documento DX contém o elemento `DocumentInformation`, o serviço Assembler retorna dados XML em vez de um documento PDF.

**Salvar o documento XML retornado**

O documento XML retornado pelo serviço Assembler especifica se o documento PDF de entrada é compatível com PDF/A. Por exemplo, se o documento PDF de entrada não for compatível com PDF/A, o serviço Assembler retornará um documento XML que contém o seguinte elemento:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Salve o documento XML como um arquivo XML para que você possa abrir o arquivo e visualização os resultados.

**Consulte também:**

[Determine se um documento é compatível com PDF/A usando a API Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determine se um documento é compatível com PDF/A usando a API de serviço da Web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determine se um documento é compatível com PDF/A usando a API Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determine se um documento PDF é compatível com PDF/A usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente do Montador de PDF.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Faça referência a um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DX. Para determinar se o documento PDF é compatível com PDF/A, verifique se o documento DX contém o elemento `PDFAValidation` contido em um elemento `DocumentInformation`.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Faça referência a um documento PDF usado para determinar a conformidade do PDF/A.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local de um documento PDF usado para determinar a conformidade com PDF/A.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream` que contém o documento PDF.
   * Crie um objeto `java.util.Map` que seja usado para armazenar o documento PDF de entrada usando um construtor `HashMap`.
   * Adicione uma entrada ao objeto `java.util.Map` invocando seu método `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem especificado no documento DDX. Por exemplo, o valor do elemento de origem localizado no documento DDX introduzido nesta seção é Loan.pdf.
      * Um objeto `com.adobe.idp.Document` que contém o documento PDF de entrada.

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios chamando um método que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, chame o método `AssemblerOptionSpec` do objeto `setFailOnError` e passe `false`.

1. Recupere informações sobre o documento PDF.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX a ser usado
   * Um objeto `java.util.Map` que contém o arquivo PDF de entrada usado para determinar a conformidade do PDF/A
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução

   O método `invokeDDX` retorna um objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contém dados XML que especificam se o documento PDF de entrada é compatível com PDF/A.

1. Salve o documento XML retornado.

   Para obter dados XML que especifiquem se o documento PDF de entrada é um documento PDF/A, execute as seguintes ações:

   * Chame o método `AssemblerResult` do objeto `getDocuments`. Isso retorna um objeto `java.util.Map`.
   * Itere pelo objeto `java.util.Map` até encontrar o objeto `com.adobe.idp.Document` resultante.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento XML. Certifique-se de salvar os dados XML como um arquivo XML.

**Consulte também:**

[Start rápido (modo SOAP): Determinar se um documento é compatível com PDF/A usando a API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api)  Java (modo SOAP)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determine se um documento é compatível com PDF/A usando a API de serviço da Web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determine se um documento PDF é compatível com PDF/A usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente do Montador de PDF.

   * Crie um objeto `AssemblerServiceClient` usando seu construtor padrão.
   * Crie um objeto `AssemblerServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar o atributo `lc_version`. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `AssemblerServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a um documento DDX existente.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento DDX.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DX e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Faça referência a um documento PDF usado para determinar a conformidade do PDF/A.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF de entrada.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` ao conteúdo da matriz de bytes.
   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType`. Esse objeto de coleção é usado para armazenar o documento PDF.
   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Atribua um valor de string que representa o nome da chave ao campo `MyMapOf_xsd_string_To_xsd_anyType_Item` `key` do objeto. Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX.
   * Atribua o objeto `BLOB` que armazena o documento PDF ao campo `MyMapOf_xsd_string_To_xsd_anyType_Item` `value` do objeto.
   * Adicione o objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` ao objeto `MyMapOf_xsd_string_To_xsd_anyType`. Chame o método `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` e passe o objeto `MyMapOf_xsd_string_To_xsd_anyType`.

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios atribuindo um valor a um membro de dados que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, atribua `false` ao membro de dados `AssemblerOptionSpec` do objeto `failOnError`.

1. Recupere informações sobre o documento PDF.

   Chame o método `AssemblerServiceService` do objeto `invoke` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX.
   * O objeto `MyMapOf_xsd_string_To_xsd_anyType` que contém o documento PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem do PDF e seus valores devem ser o objeto `BLOB` que corresponde ao arquivo PDF de entrada.
   * Um objeto `AssemblerOptionSpec` que especifica opções de tempo de execução.

   O método `invoke` retorna um objeto `AssemblerResult` que contém dados XML que especificam se o documento PDF de entrada é um documento PDF/A.

1. Salve o documento XML retornado.

   Para obter dados XML que especifiquem se o documento PDF de entrada é um documento PDF/A, execute as seguintes ações:

   * Acesse o campo `AssemblerResult` do objeto `documents`, que é um objeto `Map` que contém os dados XML que especificam se o documento PDF de entrada é um documento PDF/A.
   * Itere pelo objeto `Map` para obter cada documento resultante. Em seguida, converta o valor desse membro da matriz em `BLOB`.
   * Extraia os dados binários que representam os dados XML acessando o campo `BLOB` `MTOM` do objeto. Este campo armazena uma matriz de bytes que você pode gravar como um arquivo XML.

**Consulte também:**

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
