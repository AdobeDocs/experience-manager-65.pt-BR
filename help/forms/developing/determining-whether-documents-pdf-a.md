---
title: Determinar se os documentos são compatíveis com PDF/A
seo-title: Determining Whether Documents Are PDF/A-Compliant
description: Use o serviço Assembler para determinar se um documento PDF é compatível com PDF/A usando a API Java e a API de serviço da Web.
seo-description: Use the Assembler service to determine if a PDF document is PDF/A-compliant using the Java API and Web Service API.
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Developer
exl-id: 096fd2ac-616f-484a-b093-9d98b2f87093
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 2%

---

# Determinar se os documentos são compatíveis com PDF/A {#determining-whether-documents-are-pdf-a-compliant}

Você pode determinar se um documento PDF é compatível com PDF/A usando o serviço Assembler. Um documento PDF/A existe como um formato de arquivo destinado à preservação de longo prazo do conteúdo do documento. As fontes são incorporadas no documento e o arquivo é descompactado. Como resultado, um documento PDF/A geralmente é maior do que um documento PDF padrão. Além disso, um documento PDF/A não contém conteúdo de áudio e vídeo.

A especificação PDF/A-1 consiste em dois níveis de conformidade, a saber, A e B. A principal diferença entre os dois níveis é o suporte à estrutura lógica (acessibilidade), que não é necessário para o nível de conformidade B. Independentemente do nível de conformidade, PDF/A-1 determina que todas as fontes são incorporadas dentro do documento PDF/A gerado. No momento, somente PDF/A-1b é suportado na validação (e conversão).

Para a finalidade desta discussão, suponha que o seguinte documento DDX seja usado.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

Nesse documento DDX, a variável `DocumentInformation` instrui o serviço Assembler a retornar informações sobre o documento PDF de entrada. No `DocumentInformation` , o `PDFAValidation` instrui o serviço Assembler a indicar se o documento PDF de entrada é compatível com PDF/A.

O serviço Assembler retorna informações que especificam se o documento PDF de entrada é compatível com PDF/A em um documento XML que contém um `PDFAConformance` elemento. Se o documento PDF de entrada for compatível com PDF/A, o valor da variável `PDFAConformance` element&#39;s `isCompliant` atributo é `true`. Se o documento PDF não for compatível com PDF/A, o valor da variável `PDFAConformance` element&#39;s `isCompliant` atributo é `false`.

>[!NOTE]
>
>Porque o documento DDX especificado nesta seção contém um `DocumentInformation` elemento , o serviço Assembler retorna dados XML em vez de um documento PDF. Ou seja, o serviço Assembler não monta nem desmonta um documento PDF; ele retorna informações sobre o documento PDF de entrada em um documento XML.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para determinar se um documento PDF é compatível com PDF/A, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Assembler PDF.
1. Faça referência a um documento DDX existente.
1. Consulte um documento PDF usado para determinar a conformidade com PDF/A.
1. Defina as opções de tempo de execução.
1. Recupere informações sobre o documento PDF.
1. Salve o documento XML retornado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para obter informações sobre a localização de todos os arquivos AEM Forms JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente do Assembler do PDF**

Antes de poder executar programaticamente uma operação Assembler, é necessário criar um cliente de serviço Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para executar uma operação de serviço Assembler. Para determinar se um documento PDF de entrada é compatível com PDF/A, verifique se o documento DDX contém a variável `PDFAValidation` elemento dentro de um `DocumentInformation` elemento. O `PDFAValidation` O elemento instrui o serviço Assembler a retornar um documento XML que especifica se o documento PDF de entrada é compatível com PDF/A.

**Referência a um documento PDF usado para determinar a conformidade de PDF/A**

Um documento PDF deve ser referenciado e passado ao serviço Assembler para determinar se o documento PDF é compatível com PDF/A.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrua o serviço Assembler a continuar processando um trabalho se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte o `AssemblerOptionSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recuperar informações sobre o documento PDF**

Depois de criar o cliente do serviço Assembler, fazer referência ao documento DDX, fazer referência a um documento de PDF interativo e definir opções de tempo de execução, você pode chamar o `invokeDDX` operação. Porque o documento DDX contém a variável `DocumentInformation` elemento , o serviço Assembler retorna dados XML em vez de um documento PDF.

**Salvar o documento XML retornado**

O documento XML retornado pelo serviço Assembler especifica se o documento PDF de entrada é compatível com PDF/A. Por exemplo, se o documento PDF de entrada não for compatível com PDF/A, o serviço Assembler retornará um documento XML que contém o seguinte elemento:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Salve o documento XML como um arquivo XML para que você possa abrir o arquivo e exibir os resultados.

**Consulte também**

[Determine se um documento é compatível com PDF/A usando a API do Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determine se um documento é compatível com PDF/A usando a API do serviço da Web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determine se um documento é compatível com PDF/A usando a API do Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determine se um documento do PDF é compatível com PDF/A usando a API do serviço de Assembler (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente Assembler PDF.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `AssemblerServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e passando um valor de string que especifica o local do arquivo DX. Para determinar se o documento PDF é compatível com PDF/A, verifique se o documento DDX contém a variável `PDFAValidation` elemento contido em um `DocumentInformation` elemento.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Consulte um documento PDF usado para determinar a conformidade com PDF/A.

   * Crie um `java.io.FileInputStream` usando seu construtor e passando o local de um documento PDF usado para determinar a conformidade de PDF/A.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto que contém o documento PDF.
   * Crie um `java.util.Map` objeto usado para armazenar o documento PDF de entrada usando um `HashMap` construtor.
   * Adicione uma entrada à `java.util.Map` ao invocar seu `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem especificado no documento DX. Por exemplo, o valor do elemento de origem localizado no documento DDX que é introduzido nesta seção é Loan.pdf.
      * A `com.adobe.idp.Document` objeto que contém o documento PDF de entrada.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios, chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, chame a função `AssemblerOptionSpec` do objeto `setFailOnError` método e pass `false`.

1. Recupere informações sobre o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado
   * A `java.util.Map` objeto que contém o arquivo PDF de entrada usado para determinar a conformidade de PDF/A
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém dados XML que especifica se o documento PDF de entrada é compatível com PDF/A.

1. Salve o documento XML retornado.

   Para obter dados XML que especificam se o documento PDF de entrada é um documento PDF/A, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método . Isso retorna uma `java.util.Map` objeto.
   * Iterar por meio do `java.util.Map` até encontrar o resultante `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento XML. Salve os dados XML como um arquivo XML.

**Consulte também**

[Início rápido (modo SOAP): Determinar se um documento é compatível com PDF/A usando a API do Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) (Modo SOAP)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determine se um documento é compatível com PDF/A usando a API do serviço da Web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determine se um documento do PDF é compatível com PDF/A usando a API do Assembler Service (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente Assembler PDF.

   * Crie um `AssemblerServiceClient` usando seu construtor padrão.
   * Crie um `AssemblerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `AssemblerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a um documento DDX existente.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento DDX.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento DX e o modo para abrir o arquivo no.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Consulte um documento PDF usado para determinar a conformidade com PDF/A.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento PDF de entrada.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.
   * Crie um `MyMapOf_xsd_string_To_xsd_anyType` objeto. Esse objeto de coleção é usado para armazenar o documento PDF.
   * Crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua um valor de string que represente o nome da chave à variável `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` campo. Esse valor deve corresponder ao valor do elemento PDF source especificado no documento DDX.
   * Atribua o `BLOB` objeto que armazena o documento PDF para o `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` campo.
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` para `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` e passe o `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos da empresa, atribuindo um valor a um membro de dados pertencente à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, atribua `false` para `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Recupere informações sobre o documento PDF.

   Chame o `AssemblerServiceService` do objeto `invoke` e transmita os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX.
   * O `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém o documento PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem do PDF e seus valores devem ser o `BLOB` que corresponde ao arquivo PDF de entrada.
   * Um `AssemblerOptionSpec` que especifica as opções de tempo de execução.

   O `invoke` retorna um método `AssemblerResult` objeto que contém dados XML que especifica se o documento PDF de entrada é um documento PDF/A.

1. Salve o documento XML retornado.

   Para obter dados XML que especificam se o documento PDF de entrada é um documento PDF/A, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` , que é um `Map` objeto que contém os dados XML que especificam se o documento PDF de entrada é um documento PDF/A.
   * Iterar por meio do `Map` para obter cada documento resultante. Em seguida, converta o valor desse membro de matriz em um `BLOB`.
   * Extraia os dados binários que representam os dados XML acessando seus `BLOB` do objeto `MTOM` campo. Este campo armazena uma matriz de bytes para os quais você pode gravar como um arquivo XML.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
