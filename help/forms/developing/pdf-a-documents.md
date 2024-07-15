---
title: Trabalhar com documentos PDF/A
description: Use o serviço DocConverter para determinar se um documento PDF é um documento PDF/A e converter documentos PDF em documentos PDF/A.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 966c3554-25df-4467-866e-11c43cc15b58
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 1%

---

# Trabalhar com documentos PDF/A {#working-with-pdf-a-documents}

**Sobre o Serviço DocConverter**

O serviço DocConverter pode converter documentos PDF em documentos PDA/A. Você pode realizar estas tarefas usando este serviço:

* Converta documentos PDF em documentos PDF/A. (Consulte [Conversão de documentos em documentos PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* Determine se os documentos PDF são documentos PDF/A. (Consulte [Determinando Programaticamente A Conformidade De PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço DocConverter, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversão de documentos em documentos PDF/A {#converting-documents-to-pdf-a-documents}

Você pode usar o serviço DocConverter para converter um documento PDF em um documento PDF/A. Como PDF/A é um formato de arquivamento para preservação de longo prazo do conteúdo do documento, todas as fontes são incorporadas e o arquivo é descompactado. Como resultado, um documento PDF/A geralmente é maior do que um documento PDF padrão. Além disso, um documento PDF/A não contém conteúdo de áudio e vídeo. Antes de converter um documento PDF em um documento PDF/A, verifique se o documento PDF não é um documento PDF/A.

A especificação PDF/A-1 consiste em dois níveis de conformidade, a saber, A e B. A principal diferença entre os dois é em relação ao suporte de estrutura lógica (acessibilidade), que não é necessário para o nível de conformidade B. Independentemente do nível de conformidade, o PDF/A-1 determina que todas as fontes sejam incorporadas no documento PDF/A gerado. No momento, somente o PDF/A-1b é suportado na validação (e na conversão).

Embora PDF/A seja o padrão para o arquivamento de documentos de PDF, não é obrigatório usar PDF/A para arquivamento se um documento de PDF padrão atender aos requisitos de sua empresa. O objetivo do padrão PDF/A é estabelecer um arquivo PDF para as necessidades de arquivamento de longo prazo e preservação de documentos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço DocConverter, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para converter um documento PDF em um documento PDF/A, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente DocConvert
1. Referencie um documento PDF para converter em um documento PDF/A.
1. Definir informações de rastreamento.
1. Converta o documento.
1. Salve o documento PDF/A.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente DocConvert**

Antes de executar programaticamente uma operação DocConverter, você deve criar um cliente DocConverter. Se você estiver usando a API Java, crie um objeto `DocConverterServiceClient`. Se você estiver usando a API do serviço Web DocConverter, crie um objeto `DocConverterServiceService`.

**Referencie um documento PDF para converter em um documento PDF/A**

Recupere um documento PDF para converter em um documento PDF/A. Se você tentar converter um documento PDF, como um formulário Acrobat, em um documento PDF/A, causará uma exceção.

**Definir informações de rastreamento**

Você pode definir uma opção de tempo de execução que determine quantas informações são rastreadas durante o processo de conversão. Ou seja, você pode definir nove níveis diferentes que especificam quantas informações o serviço DocConverter rastreia quando converte um documento PDF em um documento PDF/A.

**Converter o documento**

Depois de criar o cliente de serviço DocConverter, faça referência ao documento PDF a ser convertido e defina a opção de tempo de execução que especifica quantas informações são rastreadas, você pode converter o documento PDF em um documento PDF/A.

**Salvar o documento PDF/A**

Você pode salvar o documento PDF/A como um arquivo PDF.

**Consulte também**

[Converter documentos em documentos PDF/A usando a API Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Converter documentos em documentos PDF/A usando a API de serviço Web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinação Programática Da Conformidade Com PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Converter documentos em documentos PDF/A usando a API Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Converta um documento PDF em um documento PDF/A usando a API Java:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-docconverter-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente DocConvert

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `DocConverterServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Referencie um documento PDF para converter em um documento PDF/A

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF a ser convertido usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do arquivo PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Definir informações de rastreamento

   * Crie um objeto `PDFAConversionOptionSpec` usando seu construtor.
   * Defina o nível de rastreamento de informações invocando o método `setLogLevel` do objeto `PDFAConversionOptionSpec` e transmitindo um valor de cadeia de caracteres que especifica o nível de rastreamento. Por exemplo, passe o valor `FINE`. Para obter informações sobre os diferentes valores, consulte o método `setLogLevel` na [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Converter o documento

   Converta o documento PDF em um documento PDF/A invocando o método `toPDFA` do objeto `DocConverterServiceClient` e transmitindo os seguintes valores:

   * O objeto `com.adobe.idp.Document` que contém o documento PDF a ser convertido
   * O objeto `PDFAConversionOptionSpec` que especifica informações de rastreamento

   O método `toPDFA` retorna um objeto `PDFAConversionResult` que contém o documento PDF/A.

1. Salve o documento PDF/A

   * Recupere o documento PDF/A invocando o método `getPDFA` do objeto `PDFAConversionResult`. Este método retorna um objeto `com.adobe.idp.Document` que representa o documento PDF/A.
   * Crie um objeto `java.io.File` que represente o arquivo PDF/A. Verifique se a extensão do nome do arquivo é .pdf.
   * Preencha o arquivo com dados PDF/A invocando o método `copyToFile` do objeto `com.adobe.idp.Document` e transmitindo o objeto `java.io.File`.

**Consulte também**

[Trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Início rápido (modo SOAP): conversão de um documento em um documento PDF/A usando a API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos em documentos PDF/A usando a API de serviço Web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Converta um documento PDF em um documento PDF/A usando a API DocConverter (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o WSDL DocConverter.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar um cliente DocConvert

   * Usando o assembly do cliente Microsoft .NET, crie um objeto `DocConverterServiceService` invocando seu construtor padrão.
   * Defina o membro de dados `Credentials` do objeto `DocConverterServiceService` com um valor `System.Net.NetworkCredential` que especifique o nome de usuário e o valor da senha.

1. Referencie um documento PDF para converter em um documento PDF/A

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF que é convertido em um documento PDF/A.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `binaryData` com o conteúdo da matriz de bytes.

1. Definir informações de rastreamento

   * Crie um objeto `PDFAConversionOptionSpec` usando seu construtor.
   * Defina o nível de rastreamento de informações atribuindo um valor que especifique o nível de rastreamento ao membro de dados `logLevel` do objeto `PDFAConversionOptionSpec`. Por exemplo, atribua o valor `FINE` a esse membro de dados.

1. Converter o documento

   Converta o documento PDF em um documento PDF/A invocando o método `toPDFA` do objeto `DocConverterServiceService` e transmitindo os seguintes valores:

   * O objeto `BLOB` que contém o documento PDF a ser convertido
   * O objeto `PDFAConversionOptionSpec` que especifica informações de rastreamento

   O método `toPDFA` retorna um objeto `PDFAConversionResult` que contém o documento PDF/A.

1. Salve o documento PDF/A

   * Crie um objeto `BLOB` que armazene o documento PDF/A obtendo o valor do membro de dados `PDFADocument` do objeto `PDFAConversionResult`.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` que foi retornado usando o objeto `PDFAConversionResult`. Popular a matriz de bytes obtendo o valor do membro de dados `binaryData` do objeto `BLOB`.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF/A.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

**Consulte também**

[Trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinação Programática Da Conformidade Com PDF/A {#programmatically-determining-pdf-a-compliancy}

Você pode usar o serviço DocConverter para determinar se um documento de PDF é compatível com PDF/A. Para obter informações sobre um documento PDF/A e como converter um documento PDF em um documento PDF/A, consulte [Conversão de documentos em documentos PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Para obter mais informações sobre o serviço DocConverter, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para determinar a conformidade PDF/A, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente DocConvert
1. Consulte um documento de PDF usado para determinar a conformidade com PDF/A.
1. Definir opções de tempo de execução.
1. Recupere informações sobre o documento PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente DocConvert**

Antes de executar programaticamente uma operação DocConverter, você deve criar um cliente DocConverter. Se você estiver usando a API Java, crie um objeto `DocConverterServiceClient`. Se você estiver usando a API do serviço Web DocConverter, crie um objeto `DocConverterServiceService`.

**Referenciar um documento PDF usado para determinar a conformidade PDF/A**

Um documento PDF deve ser referenciado e passado para o serviço DocConverter para determinar se o documento PDF é compatível com PDF/A.

**Definir opções de tempo de execução**

Você pode definir uma opção de tempo de execução que determine quantas informações são rastreadas durante o processo de conversão. Ou seja, você pode definir nove níveis diferentes que especificam quantas informações o serviço DocConverter rastreia quando converte um documento PDF em um documento PDF/A.

**Recuperar informações sobre o documento PDF**

Depois de criar o cliente de serviço DocConverter, referenciar o documento de PDF e definir as opções de tempo de execução, você pode determinar se o documento de PDF é um documento compatível com PDF/A.

**Consulte também**

[Determine a conformidade PDF/A usando a API Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Determine a conformidade PDF/A usando a API do serviço Web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determine a conformidade PDF/A usando a API Java {#determine-pdf-a-compliancy-using-the-java-api}

Determine a conformidade PDF/A usando a API Java:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-docconverter-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente DocConvert

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `DocConverterServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Referência a um documento de PDF usado para determinar a conformidade com PDF/A

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF a ser convertido usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do arquivo PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Definir opções de tempo de execução

   * Crie um objeto `PDFAValidationOptionSpec` usando seu construtor.
   * Defina o nível de conformidade chamando o método `setCompliance` do objeto `PDFAValidationOptionSpec` e transmitindo `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Defina o nível de rastreamento de informações invocando o método `setLogLevel` do objeto `PDFAValidationOptionSpec` e transmitindo um valor de cadeia de caracteres que especifica o nível de rastreamento. Por exemplo, passe o valor `FINE`. Para obter informações sobre os diferentes valores, consulte o método `setLogLevel` na [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Recuperar informações sobre o documento PDF

   Determine a conformidade PDF/A chamando o método `isPDFA` do objeto `DocConverterServiceClient` e transmitindo os seguintes valores:

   * O objeto `com.adobe.idp.Document` que contém o documento PDF.
   * O objeto `PDFAValidationOptionSpec` que especifica as opções de tempo de execução.

   O método `isPDFA` retorna um objeto `PDFAValidationResult` que contém os resultados desta operação.

**Consulte também**

[Trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Início rápido (modo SOAP): determinação da conformidade PDF/A usando a API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determine a conformidade PDF/A usando a API do serviço Web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determine a conformidade PDF/A usando a API de serviço da Web:

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o WSDL DocConverter.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar um cliente DocConvert

   * Usando o assembly do cliente Microsoft .NET, crie um objeto `DocConverterServiceService` invocando seu construtor padrão.
   * Defina o membro de dados `Credentials` do objeto `DocConverterServiceService` com um valor `System.Net.NetworkCredential` que especifique o nome de usuário e o valor da senha.

1. Referência a um documento de PDF usado para determinar a conformidade com PDF/A

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF que é convertido em um documento PDF/A.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento PDF e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `binaryData` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução

   * Crie um objeto `PDFAValidationOptionSpec` usando seu construtor.
   * Defina o nível de conformidade atribuindo o membro de dados `compliance` do objeto `PDFAValidationOptionSpec` com o valor `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Defina o nível de rastreamento de informações atribuindo o membro de dados `resultLevel` do objeto `PDFAValidationOptionSpec` com o valor `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Recuperar informações sobre o documento PDF

   Determine a conformidade PDF/A chamando o método `isPDFA` do objeto `DocConverterServiceService` e transmitindo os seguintes valores:

   * O objeto `BLOB` que contém o documento PDF.
   * O objeto `PDFAValidationOptionSpec` que contém opções de tempo de execução.

   O método `isPDFA` retorna um objeto `PDFAValidationResult` que contém os resultados desta operação.

**Consulte também**

[Trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
