---
title: Determinar se os Documentos são compatíveis com PDF/A
seo-title: Determinar se os Documentos são compatíveis com PDF/A
description: 'null'
seo-description: 'null'
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


# Determinar se os Documentos são compatíveis com PDF/A {#determining-whether-documents-are-pdf-a-compliant}

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

Dentro desse documento DDX, o `DocumentInformation` elemento instrui o serviço Assembler a retornar informações sobre o documento PDF de entrada. No `DocumentInformation` elemento, o `PDFAValidation` elemento instrui o serviço Assembler a indicar se o documento PDF de entrada é compatível com PDF/A.

O serviço Assembler retorna informações que especificam se o documento PDF de entrada é compatível com PDF/A em um documento XML que contém um `PDFAConformance` elemento. Se o documento PDF de entrada for compatível com PDF/A, o valor do `PDFAConformance` atributo do `isCompliant` elemento será `true`. Se o documento PDF não for compatível com PDF/A, o valor do `PDFAConformance` atributo do `isCompliant` elemento será `false`.

>[!NOTE]
>
>Como o documento DX especificado nesta seção contém um `DocumentInformation` elemento, o serviço Assembler retorna dados XML em vez de um documento PDF. Ou seja, o serviço Assembler não monta nem desmonta um documento PDF; ele retorna informações sobre o documento PDF de entrada em um documento XML.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-utilities.jar (necessário se os AEM Forms forem implantados em JBoss)
* jbossall-client.jar (obrigatório se os AEM Forms forem implantados em JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms está implantado. Para obter informações sobre a localização de todos os arquivos JAR de AEM Forms, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java de AEM Forms.

**Criar um cliente de Montador de PDF**

Antes de poder executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para executar uma operação de serviço do Assembler. Para determinar se um documento PDF de entrada é compatível com PDF/A, verifique se o documento DDX contém o `PDFAValidation` elemento dentro de um `DocumentInformation` elemento. O `PDFAValidation` elemento instrui o serviço Assembler a retornar um documento XML que especifica se o documento PDF de entrada é compatível com PDF/A.

**Referência a um documento PDF usado para determinar a conformidade do PDF/A**

Um documento PDF deve ser referenciado e passado ao serviço Assembler para determinar se o documento PDF é compatível com PDF/A.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando uma tarefa se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte a referência de `AssemblerOptionSpec` classe em Referência [de API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Recuperar informações sobre o documento PDF**

Depois de criar o cliente do serviço Assembler, consulte o documento DDX, faça referência a um documento PDF interativo e defina as opções de tempo de execução, você pode chamar a `invokeDDX` operação. Como o documento DDX contém o `DocumentInformation` elemento, o serviço Assembler retorna dados XML em vez de um documento PDF.

**Salvar o documento XML retornado**

O documento XML retornado pelo serviço Assembler especifica se o documento PDF de entrada é compatível com PDF/A. Por exemplo, se o documento PDF de entrada não for compatível com PDF/A, o serviço Assembler retornará um documento XML que contém o seguinte elemento:

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Salve o documento XML como um arquivo XML para que você possa abrir o arquivo e visualização os resultados.

**Consulte também:**

[Determine se um documento é compatível com PDF/A usando a API Java](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Determine se um documento é compatível com PDF/A usando a API de serviço da Web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Determine se um documento é compatível com PDF/A usando a API Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Determine se um documento PDF é compatível com PDF/A usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente do Montador de PDF.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `AssemblerServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DX. Para determinar se o documento PDF é compatível com PDF/A, verifique se o documento DX contém o `PDFAValidation` elemento contido em um `DocumentInformation` elemento.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Faça referência a um documento PDF usado para determinar a conformidade do PDF/A.

   * Crie um `java.io.FileInputStream` objeto usando seu construtor e transmitindo o local de um documento PDF usado para determinar a conformidade com PDF/A.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto que contém o documento PDF.
   * Crie um `java.util.Map` objeto usado para armazenar o documento PDF de entrada usando um `HashMap` construtor.
   * Adicione uma entrada ao `java.util.Map` objeto chamando seu `put` método e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem especificado no documento DDX. Por exemplo, o valor do elemento de origem localizado no documento DDX introduzido nesta seção é Loan.pdf.
      * Um `com.adobe.idp.Document` objeto que contém o documento PDF de entrada.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, chame o `AssemblerOptionSpec` método do `setFailOnError` objeto e passe `false`.

1. Recupere informações sobre o documento PDF.

   Chame o `AssemblerServiceClient` método do `invokeDDX` objeto e passe os seguintes valores obrigatórios:

   * Um `com.adobe.idp.Document` objeto que representa o documento DX a ser usado
   * Um `java.util.Map` objeto que contém o arquivo PDF de entrada usado para determinar a conformidade do PDF/A
   * Um `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém dados XML que especifica se o documento PDF de entrada é compatível com PDF/A.

1. Salve o documento XML retornado.

   Para obter dados XML que especifiquem se o documento PDF de entrada é um documento PDF/A, execute as seguintes ações:

   * Chame o `AssemblerResult` método do `getDocuments` objeto. Isso retorna um `java.util.Map` objeto.
   * Iterar pelo `java.util.Map` objeto até encontrar o `com.adobe.idp.Document` objeto resultante.
   * Chame o método `com.adobe.idp.Document` `copyToFile` do objeto para extrair o documento XML. Certifique-se de salvar os dados XML como um arquivo XML.

**Consulte também:**

[Start rápido (modo SOAP): Determinar se um documento é compatível com PDF/A usando a API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) Java (modo SOAP)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determine se um documento é compatível com PDF/A usando a API de serviço da Web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determine se um documento PDF é compatível com PDF/A usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um cliente do Montador de PDF.

   * Crie um `AssemblerServiceClient` objeto usando seu construtor padrão.
   * Crie um `AssemblerServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar o `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `AssemblerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a um documento DDX existente.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento DDX.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DX e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Faça referência a um documento PDF usado para determinar a conformidade do PDF/A.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento PDF de entrada.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo sua `MTOM` propriedade ao conteúdo da matriz de bytes.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Esse objeto de coleção é usado para armazenar o documento PDF.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * Atribua um valor de string que representa o nome da chave ao campo do `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto `key` . Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX.
   * Atribua o `BLOB` objeto que armazena o documento PDF ao `MyMapOf_xsd_string_To_xsd_anyType_Item` campo do `value` objeto.
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto ao `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o método do `MyMapOf_xsd_string_To_xsd_anyType` objeto `Add` e passe o `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios, atribuindo um valor a um membro de dados que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, atribua `false` ao membro de `AssemblerOptionSpec` dados do objeto `failOnError` .

1. Recupere informações sobre o documento PDF.

   Chame o método do `AssemblerServiceService` objeto `invoke` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o documento DDX.
   * O `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém o documento PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem do PDF e seus valores devem ser o `BLOB` objeto que corresponde ao arquivo PDF de entrada.
   * Um `AssemblerOptionSpec` objeto que especifica opções de tempo de execução.

   O `invoke` método retorna um `AssemblerResult` objeto que contém dados XML que especifica se o documento PDF de entrada é um documento PDF/A.

1. Salve o documento XML retornado.

   Para obter dados XML que especifiquem se o documento PDF de entrada é um documento PDF/A, execute as seguintes ações:

   * Acesse o `AssemblerResult` campo do `documents` objeto, que é um `Map` objeto que contém os dados XML que especifica se o documento PDF de entrada é um documento PDF/A.
   * Iterar pelo `Map` objeto para obter cada documento resultante. Em seguida, converta o valor do membro da matriz em um `BLOB`.
   * Extraia os dados binários que representam os dados XML acessando o `BLOB` campo do `MTOM` objeto. Este campo armazena uma matriz de bytes para os quais você pode gravar como um arquivo XML.

**Consulte também:**

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
