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
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 1%

---

# Trabalhar com documentos PDF/A {#working-with-pdf-a-documents}

**Sobre o serviço DocConverter**

O serviço DocConverter pode converter documentos PDF em documentos PDA/A. Você pode realizar estas tarefas usando este serviço:

* Converta documentos PDF em documentos PDF/A. (Consulte [Conversão de documentos em documentos PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* Determine se os documentos PDF são documentos PDF/A. (Consulte [Determinação Programática Da Conformidade Com PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

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

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente DocConvert**

Antes de executar programaticamente uma operação DocConverter, você deve criar um cliente DocConverter. Se estiver usando a API Java, crie uma `DocConverterServiceClient` objeto. Se você estiver usando a API do serviço Web DocConverter, crie uma `DocConverterServiceService` objeto.

**Referencie um documento PDF para converter em um documento PDF/A**

Recupere um documento PDF para converter em um documento PDF/A. Se você tentar converter um documento PDF, como um formulário Acrobat, em um documento PDF/A, causará uma exceção.

**Definir informações de rastreamento**

Você pode definir uma opção de tempo de execução que determine quantas informações são rastreadas durante o processo de conversão. Ou seja, você pode definir nove níveis diferentes que especificam quantas informações o serviço DocConverter rastreia quando converte um documento PDF em um documento PDF/A.

**Converter o documento**

Depois de criar o cliente de serviço DocConverter, faça referência ao documento PDF a ser convertido e defina a opção de tempo de execução que especifica quantas informações são rastreadas, você pode converter o documento PDF em um documento PDF/A.

**Salve o documento PDF/A**

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

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `DocConverterServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Referencie um documento PDF para converter em um documento PDF/A

   * Criar um `java.io.FileInputStream` objeto que representa o documento PDF a ser convertido usando seu construtor e transmitindo um valor de string que especifica o local do arquivo PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Definir informações de rastreamento

   * Criar um `PDFAConversionOptionSpec` usando seu construtor.
   * Defina o nível de rastreamento de informações invocando o `PDFAConversionOptionSpec` do objeto `setLogLevel` e transmitindo um valor de string que especifica o nível de rastreamento. Por exemplo, passe o valor `FINE`. Para obter informações sobre os diferentes valores, consulte `setLogLevel` no [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Converter o documento

   Converta o documento PDF em um documento PDF/A chamando o `DocConverterServiceClient` do objeto `toPDFA` e transmitindo os seguintes valores:

   * A variável `com.adobe.idp.Document` objeto que contém o documento PDF a ser convertido
   * A variável `PDFAConversionOptionSpec` objeto que especifica informações de rastreamento

   A variável `toPDFA` o método retorna um `PDFAConversionResult` objeto que contém o documento PDF/A.

1. Salve o documento PDF/A

   * Recupere o documento PDF/A chamando o `PDFAConversionResult` do objeto `getPDFA` método. Este método retorna um valor de `com.adobe.idp.Document` objeto que representa o documento PDF/A.
   * Criar um `java.io.File` objeto que representa o arquivo PDF/A. Verifique se a extensão do nome do arquivo é .pdf.
   * Preencha o arquivo com dados PDF/A chamando o `com.adobe.idp.Document` do objeto `copyToFile` e transmitindo o `java.io.File` objeto.

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

   * Usando o assembly cliente Microsoft .NET, crie um `DocConverterServiceService` chamando seu construtor padrão.
   * Defina o `DocConverterServiceService` do objeto `Credentials` membro de dados com um `System.Net.NetworkCredential` valor que especifica o nome de usuário e o valor da senha.

1. Referencie um documento PDF para converter em um documento PDF/A

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` O objeto é usado para armazenar o documento PDF que é convertido em um documento PDF/A.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `binaryData` com o conteúdo da matriz de bytes.

1. Definir informações de rastreamento

   * Criar um `PDFAConversionOptionSpec` usando seu construtor.
   * Defina o nível de rastreamento de informações atribuindo um valor que especifique o nível de rastreamento ao `PDFAConversionOptionSpec` do objeto `logLevel` membro de dados. Por exemplo, atribuir o valor `FINE` para esse membro de dados.

1. Converter o documento

   Converta o documento PDF em um documento PDF/A chamando o `DocConverterServiceService` do objeto `toPDFA` e transmitindo os seguintes valores:

   * A variável `BLOB` objeto que contém o documento PDF a ser convertido
   * A variável `PDFAConversionOptionSpec` objeto que especifica informações de rastreamento

   A variável `toPDFA` o método retorna um `PDFAConversionResult` objeto que contém o documento PDF/A.

1. Salve o documento PDF/A

   * Criar um `BLOB` objeto que armazena o documento PDF/A obtendo o valor do `PDFAConversionResult` do objeto `PDFADocument` membro de dados.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto que foi retornado usando o `PDFAConversionResult` objeto. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `binaryData` membro de dados.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF/A.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinação Programática Da Conformidade Com PDF/A {#programmatically-determining-pdf-a-compliancy}

Você pode usar o serviço DocConverter para determinar se um documento de PDF é compatível com PDF/A. Para obter informações sobre um documento PDF/A e como converter um documento PDF para um documento PDF/A, consulte [Conversão de documentos em documentos PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

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

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente DocConvert**

Antes de executar programaticamente uma operação DocConverter, você deve criar um cliente DocConverter. Se estiver usando a API Java, crie uma `DocConverterServiceClient` objeto. Se você estiver usando a API do serviço Web DocConverter, crie uma `DocConverterServiceService` objeto.

**Referência a um documento de PDF usado para determinar a conformidade com PDF/A**

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

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `DocConverterServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Referência a um documento de PDF usado para determinar a conformidade com PDF/A

   * Criar um `java.io.FileInputStream` objeto que representa o documento PDF a ser convertido usando seu construtor e transmitindo um valor de string que especifica o local do arquivo PDF.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Definir opções de tempo de execução

   * Criar um `PDFAValidationOptionSpec` usando seu construtor.
   * Defina o nível de conformidade chamando o `PDFAValidationOptionSpec` do objeto `setCompliance` método e transmissão `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Defina o nível de rastreamento de informações invocando o `PDFAValidationOptionSpec` do objeto `setLogLevel` e transmitindo um valor de string que especifica o nível de rastreamento. Por exemplo, passe o valor `FINE`. Para obter informações sobre os diferentes valores, consulte `setLogLevel` no [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Recuperar informações sobre o documento PDF

   Determine a conformidade PDF/A chamando o `DocConverterServiceClient` do objeto `isPDFA` e transmitindo os seguintes valores:

   * A variável `com.adobe.idp.Document` objeto que contém o documento PDF.
   * A variável `PDFAValidationOptionSpec` objeto que especifica as opções de tempo de execução.

   A variável `isPDFA` o método retorna um `PDFAValidationResult` objeto que contém os resultados desta operação.

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

   * Usando o assembly cliente Microsoft .NET, crie um `DocConverterServiceService` chamando seu construtor padrão.
   * Defina o `DocConverterServiceService` do objeto `Credentials` membro de dados com um `System.Net.NetworkCredential` valor que especifica o nome de usuário e o valor da senha.

1. Referência a um documento de PDF usado para determinar a conformidade com PDF/A

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` O objeto é usado para armazenar o documento PDF que é convertido em um documento PDF/A.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `binaryData` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução

   * Criar um `PDFAValidationOptionSpec` usando seu construtor.
   * Defina o nível de conformidade atribuindo o `PDFAValidationOptionSpec` do objeto `compliance` membro de dados com o valor `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Defina o nível de rastreamento de informações atribuindo o `PDFAValidationOptionSpec` do objeto `resultLevel` membro de dados com o valor `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Recuperar informações sobre o documento PDF

   Determine a conformidade PDF/A chamando o `DocConverterServiceService` do objeto `isPDFA` e transmitindo os seguintes valores:

   * A variável `BLOB` objeto que contém o documento PDF.
   * A variável `PDFAValidationOptionSpec` objeto que contém opções de tempo de execução.

   A variável `isPDFA` o método retorna um `PDFAValidationResult` objeto que contém os resultados desta operação.

**Consulte também**

[Trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
