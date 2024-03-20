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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
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

Neste documento DDX, a variável `DocumentInformation` elemento instrui o serviço Assembler para retornar informações sobre o documento PDF de entrada. No prazo de `DocumentInformation` elemento, a variável `PDFAValidation` element instrui o serviço Assembler para indicar se o documento de PDF de entrada é compatível com PDF/A.

O serviço do Assembler retorna informações que especificam se o documento de PDF de entrada é compatível com PDF/A dentro de um documento XML que contém um `PDFAConformance` elemento. Se o documento de PDF de entrada for compatível com PDF/A, o valor do `PDFAConformance` do elemento `isCompliant` atributo é `true`. Se o documento PDF não for compatível com PDF/A, o valor do `PDFAConformance` do elemento `isCompliant` atributo é `false`.

>[!NOTE]
>
>Como o documento DDX especificado nesta seção contém uma `DocumentInformation` elemento, o serviço Assembler retorna dados XML em vez de um documento PDF. Ou seja, o serviço Assembler não monta ou desmonta um documento PDF; ele retorna informações sobre o documento PDF de entrada dentro de um documento XML.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado. Para obter informações sobre a localização de todos os arquivos JAR do AEM Forms, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente do PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referencie um documento DDX existente**

Um documento DDX deve ser referenciado para executar uma operação de serviço do Assembler. Para determinar se um documento de PDF de entrada é compatível com PDF/A, verifique se o documento DDX contém a `PDFAValidation` elemento dentro de um `DocumentInformation` elemento. A variável `PDFAValidation` elemento instrui o serviço Assembler a retornar um documento XML que especifica se o documento PDF de entrada é compatível com PDF/A.

**Referência a um documento de PDF usado para determinar a conformidade com PDF/A**

Um documento PDF deve ser referenciado e passado ao serviço Assembler para determinar se o documento PDF é compatível com PDF/A.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte `AssemblerOptionSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Recuperar informações sobre o documento PDF**

Depois de criar o cliente de serviço do Assembler, fazer referência ao documento DDX, fazer referência a um documento PDF interativo e definir opções de tempo de execução, você poderá chamar o `invokeDDX` operação. Como o documento DDX contém o `DocumentInformation` elemento, o serviço Assembler retorna dados XML em vez de um documento PDF.

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

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `AssemblerServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Consulte um documento DDX existente.

   * Criar um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DDX. Para determinar se o documento PDF é compatível com PDF/A, verifique se o documento DDX contém a `PDFAValidation` elemento contido em um `DocumentInformation` elemento.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Consulte um documento de PDF usado para determinar a conformidade com PDF/A.

   * Criar um `java.io.FileInputStream` usando seu construtor e transmitindo o local de um documento PDF que é usado para determinar a conformidade PDF/A.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto que contém o documento PDF.
   * Criar um `java.util.Map` objeto usado para armazenar o documento de PDF de entrada usando um `HashMap` construtor.
   * Adicione uma entrada à `java.util.Map` ao invocar seu `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem especificado no documento DDX. Por exemplo, o valor do elemento de origem no documento DDX introduzido nesta seção é Loan.pdf.
      * A `com.adobe.idp.Document` objeto que contém o documento PDF de entrada.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa, chamando um método que pertence à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler para continuar processando um job quando ocorrer um erro, chame o `AssemblerOptionSpec` do objeto `setFailOnError` e passar `false`.

1. Recupere informações sobre o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado
   * A `java.util.Map` objeto que contém o arquivo de PDF de entrada usado para determinar a conformidade PDF/A
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   A variável `invokeDDX` o método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém dados XML que especifica se o documento de PDF de entrada é compatível com PDF/A.

1. Salve o documento XML retornado.

   Para obter dados XML que especificam se o documento de PDF de entrada é um documento PDF/A, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método. Isso retorna um `java.util.Map` objeto.
   * Repita através do `java.util.Map` até encontrar o resultado `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento XML. Salve os dados XML como um arquivo XML.

**Consulte também**

[Início rápido (modo SOAP): determinar se um documento é compatível com o PDF/A usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) (modo SOAP)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Determine se um documento é compatível com o PDF/A usando a API de serviço Web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Determine se um documento de PDF é compatível com PDF/A usando a API de serviço do Assembler (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente PDF Assembler.

   * Criar um `AssemblerServiceClient` usando seu construtor padrão.
   * Criar um `AssemblerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `AssemblerServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Consulte um documento DDX existente.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento DDX.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DDX e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Consulte um documento de PDF usado para determinar a conformidade com PDF/A.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento PDF de entrada.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.
   * Criar um `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de coleção é usado para armazenar o documento PDF.
   * Criar um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua um valor de string que represente o nome da chave à `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` campo. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX.
   * Atribua a `BLOB` objeto que armazena o documento PDF para o `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` campo.
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto para o `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` e transmita o `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa atribuindo um valor a um membro de dados que pertença à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando um job quando ocorrer um erro, atribua `false` para o `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Recupere informações sobre o documento PDF.

   Chame o `AssemblerServiceService` do objeto `invoke` e passe os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX.
   * A variável `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém o documento PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem de PDF e seus valores devem ser os `BLOB` objeto que corresponde ao arquivo PDF de entrada.
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução.

   A variável `invoke` o método retorna um `AssemblerResult` objeto que contém dados XML que especifica se o documento de PDF de entrada é um documento PDF/A.

1. Salve o documento XML retornado.

   Para obter dados XML que especificam se o documento de PDF de entrada é um documento PDF/A, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` que é um `Map` objeto que contém os dados XML que especifica se o documento de PDF de entrada é um documento PDF/A.
   * Repita através do `Map` para obter cada documento resultante. Em seguida, converta o valor desse membro da matriz em um `BLOB`.
   * Extrair os dados binários que representam os dados XML acessando seus `BLOB` do objeto `MTOM` campo. Esse campo armazena uma matriz de bytes que você pode gravar como um arquivo XML.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
