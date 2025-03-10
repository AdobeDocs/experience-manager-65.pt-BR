---
title: Trabalhando com utilitários PDF
description: Use o serviço Utilitários de PDF para converter entre formatos de arquivo PDF e XDP, definir e recuperar propriedades do documento PDF XMP e manipular metadados de.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2549'
ht-degree: 1%

---

# Trabalhando com utilitários PDF {#working-with-pdf-utilities}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o Serviço de Utilitários PDF**

O serviço de Utilitários de PDF pode converter entre formatos de arquivo PDF e XDP, definir e recuperar propriedades de documento PDF XMP e manipular metadados de. Por exemplo, antes de converter um documento PDF em outro formato, é útil inspecionar suas propriedades para determinar qual operação de serviço chamar para a conversão.

Você pode realizar essas tarefas usando o serviço Utilitários PDF:

* Converta documentos PDF em documentos XDP.
* Converter documentos XDP em documentos PDF. (Consulte [Conversão de documentos XDP em documentos PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* Recupere as propriedades do documento de PDF. (Consulte [Recuperando Propriedades do Documento PDF](pdf-utilities.md#retrieving-pdf-document-properties).)
* Salve um documento PDF e otimize-o para obter uma visualização rápida na Web. (Consulte [Definindo Modos de Salvamento de Documento PDF](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversão de documentos PDF em documentos XDP {#converting-pdf-documents-into-xdp-documents}

Você pode usar o PDF Utilitários Java e APIs de serviço da Web para converter programaticamente documentos PDF em documentos XDP.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para converter um documento PDF em um documento XDP, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDFUutilityService.
1. Chame o PDF para a operação de conversão XDP.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PDFUtilityService**

Antes de executar programaticamente uma operação PDF Utilities, você deve criar um cliente PDFUtilityService. Com a API Java, isso é feito criando um objeto `PDFUtilityServiceClient`. Com a API de serviço Web, isso é feito usando um objeto `PDFUtilityServiceService`.

**Invocar a operação de conversão de PDF para XDP**

Depois de criar o cliente de serviço, você pode chamar a operação de conversão de PDF para XDP.

**Consulte também**

[Converter documentos PDF em documentos XDP usando a API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Converter documentos PDF em documentos XDP usando a API do serviço Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos PDF em documentos XDP usando a API Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Converta documentos PDF em documentos XDP usando a API de utilitários PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente PDFUutilityService

   Crie um objeto `PDFUtilityServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Chame a operação de conversão de PDF para XDP

   Para executar a conversão, chame o método `convertPDFtoXDP` do objeto `PDFUtilityServiceClient` e passe um objeto `com.adobe.idp.Document` que represente o arquivo PDF. O método retorna um objeto `com.adobe.idp.Document` que representa o arquivo XDP recém-criado.

**Consulte também**

[Conversão de documentos PDF em documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos PDF em documentos XDP usando a API do serviço Web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Converta documentos PDF em documentos XDP usando a API de utilitários de PDF (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o arquivo WSDL do serviço de Utilitários PDF.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar um cliente PDFUutilityService

   Crie um objeto `PDFUtilityServiceService` usando seu construtor de classe de proxy.

1. Chame a operação de conversão de PDF para XDP

   Invoque o método `convertPDFtoXDP` do objeto `PDFUtilityServiceService` e passe um objeto `BLOB` que represente o arquivo PDF. O método retorna um objeto `BLOB` que representa o arquivo XDP recém-criado.

**Consulte também**

[Conversão de documentos PDF em documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Conversão de documentos XDP em documentos PDF {#converting-xdp-documents-into-pdf-documents}

Você pode usar o PDF Utilitários Java e APIs de serviço da Web para converter programaticamente documentos XDP em documentos PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para converter um documento XDP em um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDFUutilityService.
1. Chame o XDP para a operação de conversão de PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PDFUtilityService**

Antes de executar programaticamente uma operação PDF Utilities, você deve criar um cliente PDFUtilityService. Com a API Java, isso é feito criando um objeto `PDFUtilityServiceClient`. Com a API de serviço Web, isso é feito usando um objeto `PDFUtilityServiceService`.

**Invocar o XDP para a operação de conversão de PDF**

Depois de criar o cliente de serviço, você pode chamar a operação de conversão XDP para PDF.

**Consulte também**

[Converter documentos XDP em documentos PDF usando a API Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversão de documentos XDP em documentos PDF usando a API de serviço da Web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos XDP em documentos PDF usando a API Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Converta documentos XDP em documentos PDF usando a API de utilitários de PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente PDFUutilityService

   Crie um objeto `PDFUtilityServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Chame a operação de conversão de XDP para PDF

   Para executar a conversão, chame o método `convertXDPtoPDF` do objeto `PDFUtilityServiceClient` e passe um objeto `com.adobe.idp.Document` que represente o arquivo XDP. O método retorna um objeto `com.adobe.idp.Document` que representa o arquivo PDF recém-criado.

**Consulte também**

[Conversão de documentos XDP em documentos PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversão de documentos XDP em documentos PDF usando a API de serviço da Web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Converta documentos XDP em documentos PDF usando a API de utilitários de PDF (API de serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o arquivo WSDL do serviço de Utilitários PDF.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar um cliente PDFUutilityService

   Crie um objeto `PDFUtilityServiceService` usando seu construtor de classe de proxy.

1. Chame a operação de conversão de XDP para PDF

   Para executar a conversão, chame o método `convertXDPtoPDF` do objeto `PDFUtilityServiceService` e passe um objeto `BLOB` que represente o arquivo XDP. O método retorna um objeto `BLOB` que representa o arquivo PDF recém-criado.

**Consulte também**

[Conversão de documentos XDP em documentos PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Recuperando Propriedades do Documento PDF {#retrieving-pdf-document-properties}

Você pode usar o PDF Utilitários Java e as APIs de serviço da Web para recuperar programaticamente as propriedades do documento do PDF, como se o documento é um formulário preenchível ou a versão mínima do Acrobat necessária para ler o documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumo das etapas {#summary_of_steps-2}

Para recuperar as propriedades do documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDFUutilityService.
1. Chame a operação de recuperação de propriedades.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PDFUtilityService**

Antes de executar programaticamente uma operação PDF Utilities, você deve criar um cliente PDFUtilityService. Com a API Java, isso é feito criando um objeto `PDFUtilityServiceClient`. Com a API do serviço Web, isso é feito usando um objeto `PDFUtilityServiceService`.

**Invocar a operação de recuperação de propriedades**

Depois de criar o cliente de serviço, você pode chamar a operação de recuperação de propriedades.

**Consulte também**

[Recuperar propriedades do documento PDF usando a API Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Recuperar propriedades do documento PDF usando a API de serviço Web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propriedades do documento PDF usando a API Java {#retrieve-pdf-document-properties-using-the-java-api}

Recupere as propriedades do documento de PDF usando a API de utilitários de PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente PDFUutilityService

   Crie um objeto `PDFUtilityServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Chamar a operação de recuperação de propriedades

   Para executar a conversão, chame o método `getPDFProperties` do objeto `PDFUtilityServiceClient` e passe o seguinte:

   * Um objeto `com.adobe.idp.Document` que representa o documento PDF.
   * Um objeto `PDFPropertiesOptionSpec` que contém as propriedades a serem avaliadas.

   O método retorna um objeto `PDFPropertiesResult` que contém os resultados da consulta.

**Consulte também**

[Recuperando Propriedades do Documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propriedades do documento PDF usando a API de serviço Web {#retrieve-pdf-document-properties-using-the-web-service-api}

Recupere as propriedades do documento de PDF usando a API de serviço Web de Utilitários de PDF:

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o arquivo WSDL do serviço de Utilitários PDF.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar um cliente PDFUutilityService

   Crie um objeto `PDFUtilityServiceService` usando seu construtor de classe de proxy.

1. Chamar a operação de recuperação de propriedades

   Para executar a conversão, chame o método `getPDFProperties` do objeto `PDFUtilityServiceService` e passe o seguinte:

   * Um objeto `BLOB` que representa o documento PDF.
   * Um objeto `PDFPropertiesOptionSpec` que contém as propriedades a serem avaliadas.

   O método retorna um objeto `PDFPropertiesResult` que contém os resultados da consulta.

**Consulte também**

[Recuperando Propriedades do Documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Configuração dos modos de salvamento do documento PDF {#setting-pdf-document-save-modes}

Você pode usar o serviço de Utilitários de PDF Java e APIs de serviço da Web para definir programaticamente um modo de salvamento para um documento de PDF. Ao usar o serviço Utilitários de PDF para definir um modo de salvamento, o serviço Utilitários de PDF define apenas o modo de salvamento e não salva realmente o documento PDF. O documento PDF é salvo quando passado para outra operação de serviço. Por exemplo, você pode usar o serviço PDF Utilities para definir um modo de salvamento específico e transmiti-lo para o serviço de Criptografia, onde o documento PDF é realmente salvo e criptografado.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-3}

Para definir a opção de salvar para documentos PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDFUutilityService.
1. Defina o modo de salvamento.
1. Chame a operação de salvamento.
1. Passe o documento PDF para outra operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PDFUtilityService**

Antes de executar programaticamente uma operação PDF Utilities, você deve criar um cliente PDFUtilityService. Com a API Java, isso é feito criando um objeto `PDFUtilityServiceClient`. Com a API do serviço Web, isso é feito usando um objeto `PDFUtilityServiceService`.

**Definir o modo de Salvamento**

Você pode escolher uma das seguintes opções de gravação:

* `INCREMENTAL`: Para economizar de forma incremental para reduzir o tempo necessário para economizar
* `FAST_WEB_VIEW`: salvar para exibição rápida na Web
* `FULL`: Para salvar usando um salvamento completo (sem otimizações)

**Invocar a operação de salvar estilo**

Depois de criar o cliente de serviço, você pode chamar a operação de recuperação de propriedades.

**Passar o documento PDF para outra operação do AEM Forms**

Quando o serviço Utilitários PDF definir o modo Salvar especificado, passe o documento PDF para outra operação AEM Forms. Depois de retornado dessa operação, o documento PDF é salvo no modo especificado. Por exemplo, se você usar o serviço Utilitários PDF para definir o modo `FAST_WEB_VIEW` e, em seguida, passar o documento PDF para a operação `encryptUsingPassword` do serviço de Criptografia, o documento PDF retornado será criptografado com uma senha e salvo no modo `FAST_WEB_VIEW`.

>[!NOTE]
>
>O Início Rápido associado a esta seção define o modo `FAST_WEB_VIEW` e passa o documento PDF para a operação `encryptUsingPassword` do serviço de Criptografia.

**Consulte também**

[Definir opções de salvamento de documento PDF usando a API Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Definir opções de salvamento de documento PDF usando a API de serviço da Web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Criptografar documentos PDF com senha](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Definir opções de salvamento de documento PDF usando a API Java {#set-pdf-document-save-options-using-the-java-api}

Defina as opções de salvamento do documento PDF usando a API de utilitários de PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente PDFUutilityService

   Crie um objeto `PDFUtilityServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Definir o modo Salvar

   * Crie um objeto `PDFUtilitySaveMode` usando seu construtor.
   * Defina o modo de salvamento invocando o método `setSaveStyle` do objeto `PDFUtilitySaveMode` e transmitindo um valor de cadeia de caracteres que especifica o modo de salvamento. Por exemplo, para salvar para exibição rápida na Web, passe `FAST_WEB_VIEW`.

1. Chamar a operação de salvar estilo

   Chame o método `setSaveMode` do objeto `PDFUtilityServiceClient` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento PDF.
   * Um objeto `PDFUtilitySaveMode` que contém o estilo de salvamento a ser usado.
   * Um valor booleano usado para determinar se as configurações anteriores devem ser substituídas.

   O método retorna um objeto `com.adobe.idp.Document` formatado com o estilo de salvamento especificado.

1. Transmita o documento PDF para outra operação AEM Forms

   * Passe o objeto `com.adobe.idp.Document` retornado para outra operação AEM Forms.

**Consulte também**

[Configuração dos modos de salvamento do documento PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Definir opções de salvamento de documento PDF usando a API de serviço da Web {#set-pdf-document-save-options-using-the-web-service-api}

Defina as opções de salvamento do documento PDF usando o AP de utilitários de PDF (serviço Web):

1. Incluir arquivos de projeto

   * Crie um assembly cliente Microsoft .NET que consuma o arquivo WSDL do serviço de Utilitários PDF.
   * Referencie o assembly do cliente Microsoft .NET.

1. Criar um cliente PDFUutilityService

   Crie um objeto `PDFUtilityServiceService` usando seu construtor de classe de proxy.

1. Definir o modo Salvar

   * Crie um objeto `PDFUtilitySaveMode` usando seu construtor.
   * Defina o modo de salvamento atribuindo um valor de cadeia de caracteres ao método `saveStyle` do objeto `PDFUtilitySaveMode` que especifica o modo de salvamento. Por exemplo, para salvar para exibição rápida na Web, especifique `FAST_WEB_VIEW`.

1. Chamar a operação de salvar estilo

   Chame o método `setSaveMode` do objeto `PDFUtilityServiceService` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento PDF.
   * Um objeto `PDFUtilitySaveMode` que contém o estilo de salvamento a ser usado.
   * Um valor booleano usado para determinar se as configurações anteriores devem ser substituídas.

   O método retorna um objeto `BLOB` formatado com o estilo de salvamento especificado. Você pode salvar esse objeto como um documento PDF.

1. Transmita o documento PDF para outra operação Forms

   * Passe o objeto `BLOB` retornado para outra operação AEM Forms.

**Consulte também**

[Configuração dos modos de salvamento do documento PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Limpeza de documentos do PDF {#sanitizing-pdf-documents}

Você pode usar as APIs Java dos Utilitários PDF para converter programaticamente documentos PDF em documentos XDP.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-4}

Para limpar o documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDFUutilityService.
1. Chame a operação de limpeza.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Para criar um aplicativo cliente usando Java, inclua os arquivos JAR necessários.

**Criar um cliente PDFUtilityService**

Antes de executar programaticamente uma operação de limpeza, você deve criar um cliente PDFUtilityService. Com a API Java, isso é feito criando um objeto `PDFUtilityServiceClient`.

**Invocar a operação de conversão de PDF para XDP**

Depois de criar o cliente de serviço, você pode chamar a operação de limpeza.

**Consulte também**

[Converter documentos PDF em documentos XDP usando a API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Converter documentos PDF em documentos XDP usando a API do serviço Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Limpar documentos do PDF usando a API do Java {#sanitize-pdf-documents-using-the-java-api}

Limpe documentos usando a API de utilitários do PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente PDFUutilityService

   Crie um objeto `PDFUtilityServiceClient` usando seu construtor e transmitindo um objeto `ServiceClientFactory` que contenha propriedades de conexão.

1. Chame a operação de conversão de PDF para XDP

   Para executar a conversão, chame o método `convertPDFtoXDP` do objeto `PDFUtilityServiceClient` e passe um objeto `com.adobe.idp.Document` que represente o arquivo PDF. O método retorna um objeto `com.adobe.idp.Document` que representa o arquivo XDP recém-criado.

**Consulte também**

[Limpeza de documentos do PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
