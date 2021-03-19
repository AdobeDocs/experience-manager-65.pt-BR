---
title: Como trabalhar com documentos PDF/A
seo-title: Como trabalhar com documentos PDF/A
description: Use o serviço Conversor de documentos para determinar se um documento PDF é um documento PDF/A e converter documentos PDF em documentos PDF/A.
seo-description: Use o serviço Conversor de documentos para determinar se um documento PDF é um documento PDF/A e converter documentos PDF em documentos PDF/A.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2387'
ht-degree: 0%

---


# Trabalhar com documentos PDF/A {#working-with-pdf-a-documents}

**Sobre o Serviço DocConverter**

O serviço DocConverter pode converter documentos PDF em documentos PDA/A. Você pode realizar essas tarefas usando este serviço:

* Converta documentos PDF em documentos PDF/A. (Consulte [Convertendo documentos em documentos PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* Determine se documentos PDF são documentos PDF/A. (Consulte [Determinando programaticamente a conformidade do PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço DocConverter, consulte [Referência de Serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Convertendo documentos em documentos PDF/A {#converting-documents-to-pdf-a-documents}

Você pode usar o serviço Conversor de Documentos para converter um documento PDF em um documento PDF/A. Como o PDF/A é um formato de arquivo para a preservação de longo prazo do conteúdo do documento, todas as fontes são incorporadas e o arquivo é descompactado. Como resultado, um documento PDF/A normalmente é maior do que um documento PDF padrão. Além disso, um documento PDF/A não contém conteúdo de áudio e vídeo. Antes de converter um documento PDF em um documento PDF/A, verifique se o documento PDF não é um documento PDF/A.

A especificação PDF/A-1 consiste em dois níveis de conformidade, a saber, A e B. A principal diferença entre os dois é em relação ao suporte à estrutura lógica (acessibilidade), que não é necessário para o nível de conformidade B. Independentemente do nível de conformidade, o PDF/A-1 determina que todas as fontes sejam incorporadas dentro do documento PDF/A gerado. No momento, somente o PDF/A-1b é compatível com a validação (e conversão).

Embora o PDF/A seja o padrão para arquivamento de documentos PDF, não é obrigatório que o PDF/A seja usado para arquivamento se um documento PDF padrão atender aos requisitos de sua empresa. A finalidade do padrão PDF/A é estabelecer um arquivo PDF destinado a necessidades de arquivamento e preservação de documentos a longo prazo.

>[!NOTE]
>
>Para obter mais informações sobre o serviço DocConverter, consulte [Referência de Serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente DocConvert**

Antes de executar programaticamente uma operação DocConverter, você deve criar um cliente DocConverter . Se estiver usando a API do Java, crie um objeto `DocConverterServiceClient` . Se estiver usando a API do serviço da Web DocConverter, crie um objeto `DocConverterServiceService`.

**Referência a um documento PDF para converter em um documento PDF/A**

Recupere um documento PDF para converter em um documento PDF/A. Se você tentar converter um documento PDF, como um formulário Acrobat, em um documento PDF/A, ocorrerá uma exceção.

**Definir informações de rastreamento**

Você pode definir uma opção de tempo de execução que determina quantas informações são rastreadas durante o processo de conversão. Ou seja, você pode definir nove níveis diferentes que especificam quantas informações o serviço DocConverter rastreia ao converter um documento PDF em um documento PDF/A.

**Converter o documento**

Depois de criar o cliente do serviço DocConverter, faça referência ao documento PDF para converter e defina a opção de tempo de execução que especifica quantas informações são rastreadas, é possível converter o documento PDF em um documento PDF/A.

**Salvar o documento PDF/A**

Você pode salvar o documento PDF/A como um arquivo PDF.

**Consulte também:**

[Converter documentos em documentos PDF/A usando a API Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Converter documentos em documentos PDF/A usando a API de serviço da Web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Determinação programática da conformidade do PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Converter documentos em documentos PDF/A usando a API Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Converta um documento PDF em um documento PDF/A usando a API do Java:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-docconverter-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente DocConvert

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `DocConverterServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Referência a um documento PDF para converter em um documento PDF/A

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF a ser convertido usando seu construtor e transmitindo um valor de string que especifique o local do arquivo PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Definir informações de rastreamento

   * Crie um objeto `PDFAConversionOptionSpec` usando seu construtor.
   * Defina o nível de rastreamento de informações chamando o método `PDFAConversionOptionSpec` do objeto e passando um valor de string que especifica o nível de rastreamento. `setLogLevel` Por exemplo, passe o valor `FINE`. Para obter informações sobre os diferentes valores, consulte o método `setLogLevel` no [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Converter o documento

   Converta o documento PDF em um documento PDF/A chamando o método `DocConverterServiceClient` do objeto `toPDFA` e passando os seguintes valores:

   * O objeto `com.adobe.idp.Document` que contém o documento PDF a ser convertido
   * O objeto `PDFAConversionOptionSpec` que especifica as informações de rastreamento

   O método `toPDFA` retorna um objeto `PDFAConversionResult` que contém o documento PDF/A.

1. Salvar o documento PDF/A

   * Recupere o documento PDF/A chamando o método `PDFAConversionResult` do objeto `getPDFA`. Esse método retorna um objeto `com.adobe.idp.Document` que representa o documento PDF/A.
   * Crie um objeto `java.io.File` que represente o arquivo PDF/A. Certifique-se de que a extensão de nome de arquivo seja .pdf.
   * Preencha o arquivo com dados PDF/A chamando o método `com.adobe.idp.Document` do objeto e transmitindo o objeto `java.io.File`.`copyToFile`

**Consulte também:**

[Como trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Início rápido (modo SOAP): Converter um documento em um documento PDF/A usando a API do Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos em documentos PDF/A usando a API de serviço da Web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Converta um documento PDF em um documento PDF/A usando a API DocConverter (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL DocConverter.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um cliente DocConvert

   * Usando o assembly do cliente Microsoft .NET, crie um objeto `DocConverterServiceService` chamando seu construtor padrão.
   * Defina o membro de dados `DocConverterServiceService` do objeto `Credentials` com um valor `System.Net.NetworkCredential` que especifique o nome de usuário e o valor da senha.

1. Referência a um documento PDF para converter em um documento PDF/A

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF convertido em um documento PDF/A.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e passando a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `binaryData` ao conteúdo da matriz de bytes.

1. Definir informações de rastreamento

   * Crie um objeto `PDFAConversionOptionSpec` usando seu construtor.
   * Defina o nível de rastreamento de informações atribuindo um valor que especifique o nível de rastreamento para o `PDFAConversionOptionSpec` membro de dados `logLevel` do objeto. Por exemplo, atribua o valor `FINE` a esse membro de dados.

1. Converter o documento

   Converta o documento PDF em um documento PDF/A chamando o método `DocConverterServiceService` do objeto `toPDFA` e passando os seguintes valores:

   * O objeto `BLOB` que contém o documento PDF a ser convertido
   * O objeto `PDFAConversionOptionSpec` que especifica as informações de rastreamento

   O método `toPDFA` retorna um objeto `PDFAConversionResult` que contém o documento PDF/A.

1. Salvar o documento PDF/A

   * Crie um objeto `BLOB` que armazene o documento PDF/A obtendo o valor do `PDFAConversionResult` membro de dados `PDFADocument` do objeto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` que foi retornado usando o objeto `PDFAConversionResult`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `binaryData`.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF/A.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e passando o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Como trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Determinando programaticamente a conformidade do PDF/A {#programmatically-determining-pdf-a-compliancy}

Você pode usar o serviço Conversor de Documentos para determinar se um documento PDF é compatível com PDF/A. Para obter informações sobre um documento PDF/A e como converter um documento PDF em um documento PDF/A, consulte [Convertendo documentos em documentos PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Para obter mais informações sobre o serviço DocConverter, consulte [Referência de Serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para determinar a conformidade com PDF/A, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Criar um cliente DocConvert
1. Faça referência a um documento PDF usado para determinar a conformidade com PDF/A.
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

Para obter informações sobre a localização desses arquivos JAR, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente DocConvert**

Antes de executar programaticamente uma operação DocConverter, você deve criar um cliente DocConverter . Se estiver usando a API do Java, crie um objeto `DocConverterServiceClient` . Se estiver usando a API do serviço da Web DocConverter, crie um objeto `DocConverterServiceService`.

**Referência a um documento PDF usado para determinar a conformidade com PDF/A**

Um documento PDF deve ser referenciado e passado ao serviço Conversor de Documentos para determinar se ele é compatível com PDF/A.

**Definir opções de tempo de execução**

Você pode definir uma opção de tempo de execução que determina quantas informações são rastreadas durante o processo de conversão. Ou seja, você pode definir nove níveis diferentes que especificam quantas informações o serviço DocConverter rastreia ao converter um documento PDF em um documento PDF/A.

**Recuperar informações sobre o documento PDF**

Depois de criar o cliente de serviço DocConverter, consultar o documento PDF e definir as opções de tempo de execução, você pode determinar se o documento PDF é um documento compatível com PDF/A.

**Consulte também:**

[Determine a conformidade do PDF/A usando a API do Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Determine a conformidade do PDF/A usando a API do serviço da Web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determine a conformidade do PDF/A usando a API Java {#determine-pdf-a-compliancy-using-the-java-api}

Determine a conformidade do PDF/A usando a API do Java:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-docconverter-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente DocConvert

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `DocConverterServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Referência a um documento PDF usado para determinar a conformidade com PDF/A

   * Crie um objeto `java.io.FileInputStream` que represente o documento PDF a ser convertido usando seu construtor e transmitindo um valor de string que especifique o local do arquivo PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Definir opções de tempo de execução

   * Crie um objeto `PDFAValidationOptionSpec` usando seu construtor.
   * Defina o nível de conformidade chamando o método `PDFAValidationOptionSpec` do objeto `setCompliance` e passando `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Defina o nível de rastreamento de informações chamando o método `PDFAValidationOptionSpec` do objeto e passando um valor de string que especifica o nível de rastreamento. `setLogLevel` Por exemplo, passe o valor `FINE`. Para obter informações sobre os diferentes valores, consulte o método `setLogLevel` no [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Recuperar informações sobre o documento PDF

   Determine a conformidade do PDF/A chamando o método `DocConverterServiceClient` do objeto `isPDFA` e passando os seguintes valores:

   * O objeto `com.adobe.idp.Document` que contém o documento PDF.
   * O objeto `PDFAValidationOptionSpec` que especifica as opções de tempo de execução.

   O método `isPDFA` retorna um objeto `PDFAValidationResult` que contém os resultados dessa operação.

**Consulte também:**

[Como trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Início rápido (modo SOAP): Como determinar a conformidade do PDF/A com a API do Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Determine a conformidade do PDF/A usando a API do serviço da Web {#determine-pdf-a-compliancy-using-the-web-service-api}

Determine a conformidade do PDF/A usando a API do serviço da Web:

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o WSDL DocConverter.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um cliente DocConvert

   * Usando o assembly do cliente Microsoft .NET, crie um objeto `DocConverterServiceService` chamando seu construtor padrão.
   * Defina o membro de dados `DocConverterServiceService` do objeto `Credentials` com um valor `System.Net.NetworkCredential` que especifique o nome de usuário e o valor da senha.

1. Referência a um documento PDF usado para determinar a conformidade com PDF/A

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF convertido em um documento PDF/A.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e passando a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `binaryData` ao conteúdo da matriz de bytes.

1. Definir opções de tempo de execução

   * Crie um objeto `PDFAValidationOptionSpec` usando seu construtor.
   * Defina o nível de conformidade atribuindo o `PDFAValidationOptionSpec` membro de dados `compliance` do objeto com o valor `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Defina o nível de rastreamento de informações atribuindo o membro de dados `resultLevel` do objeto `PDFAValidationOptionSpec` com o valor `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Recuperar informações sobre o documento PDF

   Determine a conformidade do PDF/A chamando o método `DocConverterServiceService` do objeto `isPDFA` e passando os seguintes valores:

   * O objeto `BLOB` que contém o documento PDF.
   * O objeto `PDFAValidationOptionSpec` que contém opções de tempo de execução.

   O método `isPDFA` retorna um objeto `PDFAValidationResult` que contém os resultados dessa operação.

**Consulte também:**

[Como trabalhar com documentos PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
