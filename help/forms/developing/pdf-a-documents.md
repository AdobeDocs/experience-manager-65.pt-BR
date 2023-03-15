---
title: Trabalhar com documentos do PDF/A
seo-title: Working with PDF/A Documents
description: Use o serviço DocConverter para determinar se um documento PDF é um documento PDF/A e converter documentos PDF para documentos PDF/A.
seo-description: Use the  DocConverter service to determine if a PDF document is a PDF/A document and convert PDF documents to PDF/A documents.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
role: Developer
exl-id: 966c3554-25df-4467-866e-11c43cc15b58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 1%

---

# Trabalhar com documentos do PDF/A {#working-with-pdf-a-documents}

**Sobre o Serviço DocConverter**

O serviço DocConverter pode converter documentos PDF para documentos PDA/A. Você pode realizar essas tarefas usando este serviço:

* Converta documentos PDF em documentos PDF/A. (Consulte [Convertendo documentos em documentos PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* Determine se os documentos PDF são documentos PDF/A. (Consulte [Determinar de forma programática a conformidade do PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço DocConverter, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Convertendo documentos em documentos PDF/A {#converting-documents-to-pdf-a-documents}

Você pode usar o serviço DocConverter para converter um documento PDF em um documento PDF/A. Como o PDF/A é um formato de arquivo para a preservação de longo prazo do conteúdo do documento, todas as fontes são incorporadas e o arquivo é descompactado. Como resultado, um documento PDF/A geralmente é maior do que um documento PDF padrão. Além disso, um documento PDF/A não contém conteúdo de áudio e vídeo. Antes de converter um documento PDF em um documento PDF/A, verifique se o documento PDF não é um documento PDF/A.

A especificação PDF/A-1 consiste em dois níveis de conformidade, a saber, A e B. A principal diferença entre os dois é no que diz respeito ao suporte à estrutura lógica (acessibilidade), que não é necessário para o nível de conformidade B. Independentemente do nível de conformidade, PDF/A-1 determina que todas as fontes são incorporadas dentro do documento PDF/A gerado. No momento, somente PDF/A-1b é suportado na validação (e conversão).

Embora o PDF/A seja o padrão para arquivamento de documentos de PDF, não é obrigatório que o PDF/A seja usado para arquivamento se um documento PDF padrão atender aos requisitos de sua empresa. O objetivo do padrão PDF/A é estabelecer um arquivo de PDF destinado às necessidades de arquivamento e preservação de documentos a longo prazo.

>[!NOTE]
>
>Para obter mais informações sobre o serviço DocConverter, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para converter um documento PDF em um documento PDF/A, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Criar um cliente DocConvert
1. Faça referência a um documento PDF para conversão em um documento PDF/A.
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
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente DocConvert**

Antes de executar programaticamente uma operação DocConverter, você deve criar um cliente DocConverter . Se estiver usando a API do Java, crie um `DocConverterServiceClient` objeto. Se estiver usando a API do serviço da Web DocConverter, crie um `DocConverterServiceService` objeto.

**Referência a um documento PDF para converter em um documento PDF/A**

Recupere um documento PDF para converter em um documento PDF/A. Se você tentar converter um documento PDF, como um formulário Acrobat, em um documento PDF/A, ocorrerá uma exceção.

**Definir informações de rastreamento**

Você pode definir uma opção de tempo de execução que determina quantas informações são rastreadas durante o processo de conversão. Ou seja, você pode definir nove níveis diferentes que especificam quantas informações o serviço DocConverter rastreia quando converte um documento PDF em um documento PDF/A.

**Converter o documento**

Depois de criar o cliente do serviço DocConverter, faça referência ao documento PDF para converter e defina a opção de tempo de execução que especifica quantas informações são rastreadas, é possível converter o documento PDF para um documento PDF/A.

**Salve o documento PDF/A**

Você pode salvar o documento PDF/A como um arquivo PDF.

**Consulte também**

[Converter documentos em documentos PDF/A usando a API do Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Converter documentos em documentos PDF/A usando a API de serviço da Web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinar de forma programática a conformidade do PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Converter documentos em documentos PDF/A usando a API do Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Converta um documento do PDF em um documento PDF/A usando a API do Java:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-docconverter-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente DocConvert

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `DocConverterServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Referência a um documento PDF para converter em um documento PDF/A

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF para converter usando seu construtor e passando um valor de string que especifica o local do arquivo PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Definir informações de rastreamento

   * Crie um `PDFAConversionOptionSpec` usando seu construtor.
   * Defina o nível de rastreamento de informações chamando o `PDFAConversionOptionSpec` do objeto `setLogLevel` e transmitindo um valor de string que especifica o nível de rastreamento. Por exemplo, passe o valor `FINE`. Para obter informações sobre os diferentes valores, consulte o `setLogLevel` no método [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Converter o documento

   Converta o documento PDF em um documento PDF/A chamando o `DocConverterServiceClient` do objeto `toPDFA` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que contém o documento PDF para converter
   * O `PDFAConversionOptionSpec` objeto que especifica informações de rastreamento

   O `toPDFA` método retorna um `PDFAConversionResult` objeto que contém o documento PDF/A.

1. Salve o documento PDF/A

   * Recupere o documento PDF/A chamando o `PDFAConversionResult` do objeto `getPDFA` método . Esse método retorna um `com.adobe.idp.Document` objeto que representa o documento PDF/A.
   * Crie um `java.io.File` objeto que representa o arquivo PDF/A. Certifique-se de que a extensão de nome de arquivo seja .pdf.
   * Preencha o arquivo com dados PDF/A chamando a variável `com.adobe.idp.Document` do objeto `copyToFile` e a aprovação do `java.io.File` objeto.

**Consulte também**

[Trabalhar com documentos do PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Início rápido (modo SOAP): Conversão de um documento em um documento PDF/A usando a API do Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos em documentos PDF/A usando a API de serviço da Web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Converta um documento do PDF em um documento PDF/A usando a API DocConverter (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um conjunto de clientes Microsoft .NET que consuma o WSDL do Conversor de Documentos.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um cliente DocConvert

   * Usando o assembly do cliente Microsoft .NET, crie um `DocConverterServiceService` chamando seu construtor padrão.
   * Defina as `DocConverterServiceService` do objeto `Credentials` membro de dados com um `System.Net.NetworkCredential` que especifica o nome de usuário e o valor da senha.

1. Referência a um documento PDF para converter em um documento PDF/A

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento PDF convertido em um documento PDF/A.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo para abrir o arquivo no.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `binaryData` com o conteúdo da matriz de bytes.

1. Definir informações de rastreamento

   * Crie um `PDFAConversionOptionSpec` usando seu construtor.
   * Defina o nível de rastreamento de informações atribuindo um valor que especifique o nível de rastreamento como `PDFAConversionOptionSpec` do objeto `logLevel` membro de dados. Por exemplo, atribua o valor `FINE` para esse membro de dados.

1. Converter o documento

   Converta o documento PDF em um documento PDF/A chamando o `DocConverterServiceService` do objeto `toPDFA` e transmitindo os seguintes valores:

   * O `BLOB` objeto que contém o documento PDF para converter
   * O `PDFAConversionOptionSpec` objeto que especifica informações de rastreamento

   O `toPDFA` método retorna um `PDFAConversionResult` objeto que contém o documento PDF/A.

1. Salve o documento PDF/A

   * Crie um `BLOB` objeto que armazena o documento PDF/A obtendo o valor da variável `PDFAConversionResult` do objeto `PDFADocument` membro de dados.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto que foi retornado usando o `PDFAConversionResult` objeto. Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `binaryData` membro de dados.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF/A.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Trabalhar com documentos do PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinar de forma programática a conformidade do PDF/A {#programmatically-determining-pdf-a-compliancy}

Você pode usar o serviço DocConverter para determinar se um documento PDF é compatível com PDF/A. Para obter informações sobre um documento PDF/A e como converter um documento PDF para um documento PDF/A, consulte [Convertendo documentos em documentos PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Para obter mais informações sobre o serviço DocConverter, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para determinar a conformidade de PDF/A, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Criar um cliente DocConvert
1. Consulte um documento PDF usado para determinar a conformidade com PDF/A.
1. Defina as opções de tempo de execução.
1. Recupere informações sobre o documento PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss Application Server)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss Application Server)

Para obter informações sobre a localização desses arquivos JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente DocConvert**

Antes de executar programaticamente uma operação DocConverter, você deve criar um cliente DocConverter . Se estiver usando a API do Java, crie um `DocConverterServiceClient` objeto. Se estiver usando a API do serviço da Web DocConverter, crie um `DocConverterServiceService` objeto.

**Referência a um documento PDF usado para determinar a conformidade de PDF/A**

Um documento PDF deve ser referenciado e passado ao serviço DocConverter para determinar se o documento PDF é compatível com PDF/A.

**Definir opções de tempo de execução**

Você pode definir uma opção de tempo de execução que determina quantas informações são rastreadas durante o processo de conversão. Ou seja, você pode definir nove níveis diferentes que especificam quantas informações o serviço DocConverter rastreia quando converte um documento PDF em um documento PDF/A.

**Recuperar informações sobre o documento PDF**

Depois de criar o cliente do serviço DocConverter, consultar o documento PDF e definir as opções de tempo de execução, pode determinar se o documento PDF é um documento compatível com PDF/A.

**Consulte também**

[Determine a conformidade do PDF/A usando a API do Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Determine a conformidade de PDF/A usando a API do serviço da Web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determine a conformidade do PDF/A usando a API do Java {#determine-pdf-a-compliancy-using-the-java-api}

Determine a conformidade de PDF/A usando a API do Java:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-docconverter-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente DocConvert

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `DocConverterServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Referência a um documento PDF usado para determinar a conformidade de PDF/A

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF para converter usando seu construtor e passando um valor de string que especifica o local do arquivo PDF.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Definir opções de tempo de execução

   * Crie um `PDFAValidationOptionSpec` usando seu construtor.
   * Defina o nível de conformidade chamando o `PDFAValidationOptionSpec` do objeto `setCompliance` método e aprovação `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Defina o nível de rastreamento de informações chamando o `PDFAValidationOptionSpec` do objeto `setLogLevel` e transmitindo um valor de string que especifica o nível de rastreamento. Por exemplo, passe o valor `FINE`. Para obter informações sobre os diferentes valores, consulte o `setLogLevel` no método [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Recuperar informações sobre o documento PDF

   Determine a conformidade de PDF/A chamando o `DocConverterServiceClient` do objeto `isPDFA` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que contém o documento PDF.
   * O `PDFAValidationOptionSpec` que especifica as opções de tempo de execução.

   O `isPDFA` método retorna um `PDFAValidationResult` que contém os resultados desta operação.

**Consulte também**

[Trabalhar com documentos do PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Início rápido (modo SOAP): Determinar a conformidade de PDF/A usando a API do Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determine a conformidade de PDF/A usando a API do serviço da Web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determine a conformidade de PDF/A usando a API do serviço da Web:

1. Incluir arquivos de projeto

   * Crie um conjunto de clientes Microsoft .NET que consuma o WSDL do Conversor de Documentos.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um cliente DocConvert

   * Usando o assembly do cliente Microsoft .NET, crie um `DocConverterServiceService` chamando seu construtor padrão.
   * Defina as `DocConverterServiceService` do objeto `Credentials` membro de dados com um `System.Net.NetworkCredential` que especifica o nome de usuário e o valor da senha.

1. Referência a um documento PDF usado para determinar a conformidade de PDF/A

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento PDF convertido em um documento PDF/A.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo para abrir o arquivo no.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `binaryData` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução

   * Crie um `PDFAValidationOptionSpec` usando seu construtor.
   * Defina o nível de conformidade atribuindo a variável `PDFAValidationOptionSpec` do objeto `compliance` membro de dados com o valor `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Defina o nível de rastreamento de informações atribuindo a variável `PDFAValidationOptionSpec` do objeto `resultLevel` membro de dados com o valor `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Recuperar informações sobre o documento PDF

   Determine a conformidade de PDF/A chamando o `DocConverterServiceService` do objeto `isPDFA` e transmitindo os seguintes valores:

   * O `BLOB` objeto que contém o documento PDF.
   * O `PDFAValidationOptionSpec` objeto que contém opções de tempo de execução.

   O `isPDFA` método retorna um `PDFAValidationResult` que contém os resultados desta operação.

**Consulte também**

[Trabalhar com documentos do PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
