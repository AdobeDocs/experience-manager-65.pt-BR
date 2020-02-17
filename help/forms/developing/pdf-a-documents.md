---
title: Como trabalhar com documentos PDF/A
seo-title: Como trabalhar com documentos PDF/A
description: 'null'
seo-description: 'null'
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Como trabalhar com documentos PDF/A {#working-with-pdf-a-documents}

**Sobre o Serviço DocConverter**

O serviço DocConverter pode converter documentos PDF em documentos PDA/A. Você pode realizar essas tarefas usando este serviço:

* Converta documentos PDF em documentos PDF/A. (Consulte [Convertendo documentos em documentos](pdf-a-documents.md#converting-documents-to-pdf-a-documents)PDF/A.)
* Determine se documentos PDF são documentos PDF/A. (Consulte Determinando [Programaticamente a conformidade](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)do PDF/A.)

>[!NOTE]
>
>Para obter mais informações sobre o serviço DocConverter, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

## Convertendo documentos em documentos PDF/A {#converting-documents-to-pdf-a-documents}

Você pode usar o serviço DocConverter para converter um documento PDF em um documento PDF/A. Como o PDF/A é um formato de arquivamento para a preservação de longo prazo do conteúdo do documento, todas as fontes são incorporadas e o arquivo é descompactado. Como resultado, um documento PDF/A geralmente é maior que um documento PDF padrão. Além disso, um documento PDF/A não contém conteúdo de áudio e vídeo. Antes de converter um documento PDF em um documento PDF/A, verifique se o documento PDF não é um documento PDF/A.

A especificação PDF/A-1 consiste em dois níveis de conformidade, a A e a B. A principal diferença entre os dois é no que se refere ao suporte à estrutura lógica (acessibilidade), que não é necessário para o nível de conformidade B. Independentemente do nível de conformidade, o PDF/A-1 determina que todas as fontes sejam incorporadas no documento PDF/A gerado. No momento, apenas o PDF/A-1b é suportado na validação (e conversão).

Embora o PDF/A seja o padrão para arquivamento de documentos PDF, não é obrigatório que o PDF/A seja usado para arquivamento se um documento PDF padrão atender aos requisitos de sua empresa. A finalidade do padrão PDF/A é estabelecer um arquivo PDF destinado a necessidades de arquivamento de longo prazo e preservação de documentos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço DocConverter, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary-of-steps}

Para converter um documento PDF em um documento PDF/A, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente DocConvert
1. Faça referência a um documento PDF para converter em um documento PDF/A.
1. Defina as informações de rastreamento.
1. Converta o documento.
1. Salve o documento PDF/A.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um cliente DocConvert**

Antes de executar programaticamente uma operação DocConverter, você deve criar um cliente DocConverter. Se você estiver usando a API Java, crie um `DocConverterServiceClient` objeto. Se você estiver usando a API de serviço da Web DocConverter, crie um `DocConverterServiceService` objeto.

**Referência a um documento PDF para converter em um documento PDF/A**

Recupere um documento PDF para converter em um documento PDF/A. Se você tentar converter um documento PDF, como um formulário Acrobat, em um documento PDF/A, causará uma exceção.

**Definir informações de rastreamento**

Você pode definir uma opção de tempo de execução que determina quantas informações são rastreadas durante o processo de conversão. Ou seja, você pode definir nove níveis diferentes que especifiquem quantas informações o serviço DocConverter rastreia quando converte um documento PDF em um documento PDF/A.

**Converter o documento**

Depois de criar o cliente de serviço DocConverter, consulte o documento PDF para converter e defina a opção de tempo de execução que especifica quantas informações são rastreadas, converta o documento PDF em um documento PDF/A.

**Salvar o documento PDF/A**

É possível salvar o documento PDF/A como um arquivo PDF.

**Consulte também:**

[Converter documentos em documentos PDF/A usando a API Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Converter documentos em documentos PDF/A usando a API de serviço da Web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinando programaticamente a conformidade do PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Converter documentos em documentos PDF/A usando a API Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Converta um documento PDF em um documento PDF/A usando a API Java:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-docconverter-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente DocConvert

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `DocConverterServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Referência a um documento PDF para converter em um documento PDF/A

   * Crie um `java.io.FileInputStream` objeto que represente o documento PDF a ser convertido usando seu construtor e transmitindo um valor de string que especifica o local do arquivo PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Definir informações de rastreamento

   * Crie um `PDFAConversionOptionSpec` objeto usando seu construtor.
   * Defina o nível de rastreamento de informações chamando o método do `PDFAConversionOptionSpec` objeto `setLogLevel` e transmitindo um valor de string que especifica o nível de rastreamento. For example, pass the value `FINE`. Para obter informações sobre os diferentes valores, consulte o `setLogLevel` método na Referência [da API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

1. Converter o documento

   Converta o documento PDF em um documento PDF/A chamando o método do `DocConverterServiceClient` objeto `toPDFA` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que contém o documento PDF a ser convertido
   * O `PDFAConversionOptionSpec` objeto que especifica informações de rastreamento
   O `toPDFA` método retorna um `PDFAConversionResult` objeto que contém o documento PDF/A.

1. Salvar o documento PDF/A

   * Recupere o documento PDF/A chamando o `PDFAConversionResult` método do `getPDFA` objeto. Esse método retorna um `com.adobe.idp.Document` objeto que representa o documento PDF/A.
   * Crie um `java.io.File` objeto que represente o arquivo PDF/A. Verifique se a extensão do nome do arquivo é .pdf.
   * Preencha o arquivo com dados PDF/A chamando o método do `com.adobe.idp.Document` objeto `copyToFile` e transmitindo o `java.io.File` objeto.

**Consulte também:**

[Como trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Início rápido (modo SOAP): Converter um documento em um documento PDF/A usando a API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos em documentos PDF/A usando a API de serviço da Web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Converta um documento PDF em um documento PDF/A usando a API DocConverter (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o DocConverter WSDL.
   * Consulte o assembly do cliente Microsoft .NET.

1. Criar um cliente DocConvert

   * Usando o assembly do cliente Microsoft .NET, crie um `DocConverterServiceService` objeto chamando seu construtor padrão.
   * Defina o membro `DocConverterServiceService` de dados do `Credentials` objeto com um `System.Net.NetworkCredential` valor que especifique o nome de usuário e o valor da senha.

1. Referência a um documento PDF para converter em um documento PDF/A

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento PDF convertido em um documento PDF/A.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo sua `binaryData` propriedade ao conteúdo da matriz de bytes.

1. Definir informações de rastreamento

   * Crie um `PDFAConversionOptionSpec` objeto usando seu construtor.
   * Defina o nível de rastreamento de informações atribuindo um valor que especifica o nível de rastreamento ao membro de `PDFAConversionOptionSpec` dados do `logLevel` objeto. Por exemplo, atribua o valor `FINE` a esse membro de dados.

1. Converter o documento

   Converta o documento PDF em um documento PDF/A chamando o método do `DocConverterServiceService` objeto `toPDFA` e transmitindo os seguintes valores:

   * O `BLOB` objeto que contém o documento PDF a ser convertido
   * O `PDFAConversionOptionSpec` objeto que especifica informações de rastreamento
   O `toPDFA` método retorna um `PDFAConversionResult` objeto que contém o documento PDF/A.

1. Salvar o documento PDF/A

   * Crie um `BLOB` objeto que armazene o documento PDF/A obtendo o valor do membro de `PDFAConversionResult` dados do `PDFADocument` objeto.
   * Crie uma matriz de bytes que armazene o conteúdo do `BLOB` objeto que foi retornado usando o `PDFAConversionResult` objeto. Preencha a matriz de bytes obtendo o valor do membro de `BLOB` dados do `binaryData` objeto.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF/A.
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Como trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criação de um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinando programaticamente a conformidade do PDF/A {#programmatically-determining-pdf-a-compliancy}

Você pode usar o serviço DocConverter para determinar se um documento PDF é compatível com PDF/A. Para obter informações sobre um documento PDF/A e como converter um documento PDF em um documento PDF/A, consulte [Convertendo documentos em documentos](pdf-a-documents.md#converting-documents-to-pdf-a-documents)PDF/A.

>[!NOTE]
>
>Para obter mais informações sobre o serviço DocConverter, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary_of_steps-1}

Para determinar a conformidade do PDF/A, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente DocConvert
1. Faça referência a um documento PDF usado para determinar a conformidade do PDF/A.
1. Defina as opções de tempo de execução.
1. Recupere informações sobre o documento PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um cliente DocConvert**

Antes de executar programaticamente uma operação DocConverter, você deve criar um cliente DocConverter. Se você estiver usando a API Java, crie um `DocConverterServiceClient` objeto. Se você estiver usando a API de serviço da Web DocConverter, crie um `DocConverterServiceService` objeto.

**Referência a um documento PDF usado para determinar a conformidade do PDF/A**

Um documento PDF deve ser referenciado e passado ao serviço DocConverter para determinar se o documento PDF é compatível com PDF/A.

**Definir opções de tempo de execução**

Você pode definir uma opção de tempo de execução que determina quantas informações são rastreadas durante o processo de conversão. Ou seja, você pode definir nove níveis diferentes que especifiquem quantas informações o serviço DocConverter rastreia quando converte um documento PDF em um documento PDF/A.

**Recuperar informações sobre o documento PDF**

Depois de criar o cliente de serviço DocConverter, consultar o documento PDF e definir as opções de tempo de execução, você pode determinar se o documento PDF é um documento compatível com PDF/A.

**Consulte também:**

[Determine a conformidade do PDF/A usando a API Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Determine a conformidade do PDF/A usando a API de serviço da Web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determine a conformidade do PDF/A usando a API Java {#determine-pdf-a-compliancy-using-the-java-api}

Determine a conformidade do PDF/A usando a API Java:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-docconverter-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente DocConvert

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `DocConverterServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Referência a um documento PDF usado para determinar a conformidade do PDF/A

   * Crie um `java.io.FileInputStream` objeto que represente o documento PDF a ser convertido usando seu construtor e transmitindo um valor de string que especifica o local do arquivo PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Definir opções de tempo de execução

   * Crie um `PDFAValidationOptionSpec` objeto usando seu construtor.
   * Defina o nível de conformidade chamando o `PDFAValidationOptionSpec` método do `setCompliance` objeto e transmitindo `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Defina o nível de rastreamento de informações chamando o método do `PDFAValidationOptionSpec` objeto `setLogLevel` e transmitindo um valor de string que especifica o nível de rastreamento. For example, pass the value `FINE`. Para obter informações sobre os diferentes valores, consulte o `setLogLevel` método na Referência [da API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

1. Recuperar informações sobre o documento PDF

   Determine a conformidade do PDF/A chamando o `DocConverterServiceClient` método do objeto `isPDFA` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que contém o documento PDF.
   * O `PDFAValidationOptionSpec` objeto que especifica opções de tempo de execução.
   O `isPDFA` método retorna um `PDFAValidationResult` objeto que contém os resultados dessa operação.

**Consulte também:**

[Como trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Início rápido (modo SOAP): Como determinar a conformidade do PDF/A usando a API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determine a conformidade do PDF/A usando a API de serviço da Web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determine a conformidade do PDF/A usando a API de serviço da Web:

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o DocConverter WSDL.
   * Consulte o assembly do cliente Microsoft .NET.

1. Criar um cliente DocConvert

   * Usando o assembly do cliente Microsoft .NET, crie um `DocConverterServiceService` objeto chamando seu construtor padrão.
   * Defina o membro `DocConverterServiceService` de dados do `Credentials` objeto com um `System.Net.NetworkCredential` valor que especifique o nome de usuário e o valor da senha.

1. Referência a um documento PDF usado para determinar a conformidade do PDF/A

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento PDF convertido em um documento PDF/A.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo sua `binaryData` propriedade ao conteúdo da matriz de bytes.

1. Definir opções de tempo de execução

   * Crie um `PDFAValidationOptionSpec` objeto usando seu construtor.
   * Defina o nível de conformidade atribuindo o membro de `PDFAValidationOptionSpec` dados do `compliance` objeto ao valor `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Defina o nível de rastreamento de informações atribuindo o membro de `PDFAValidationOptionSpec` dados do `resultLevel` objeto ao valor `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Recuperar informações sobre o documento PDF

   Determine a conformidade do PDF/A chamando o `DocConverterServiceService` método do objeto `isPDFA` e transmitindo os seguintes valores:

   * O `BLOB` objeto que contém o documento PDF.
   * O `PDFAValidationOptionSpec` objeto que contém opções de tempo de execução.
   O `isPDFA` método retorna um `PDFAValidationResult` objeto que contém os resultados dessa operação.

**Consulte também:**

[Como trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criação de um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
