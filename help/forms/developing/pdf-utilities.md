---
title: Trabalhar com utilitários PDF
seo-title: Working with PDF Utilities
description: Use o serviço Utilitários do PDF para converter entre formatos de arquivo PDF e XDP, definir e recuperar propriedades de documento do PDF e manipular metadados de XMP.
seo-description: Use the PDF Utilities service to convert between PDF and XDP file formats, set and retrieve PDF document properties, and manipulate XMP metadata.
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2579'
ht-degree: 1%

---

# Trabalhar com utilitários PDF {#working-with-pdf-utilities}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

**Sobre o serviço de utilitários do PDF**

O serviço Utilitários PDF pode converter entre formatos de arquivo PDF e XDP, definir e recuperar propriedades de documento PDF e manipular metadados XMP. Por exemplo, antes de converter um documento PDF para outro formato, é útil inspecionar suas propriedades para determinar qual operação de serviço chamar para a conversão.

Você pode realizar essas tarefas usando o serviço Utilitários PDF:

* Converta documentos PDF em documentos XDP.
* Converta documentos XDP em documentos PDF. (Consulte [Convertendo documentos XDP em documentos do PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* Recupere as propriedades do documento PDF. (Consulte [Recuperando propriedades do documento do PDF](pdf-utilities.md#retrieving-pdf-document-properties).)
* Salve um documento do PDF e otimize-o para exibição rápida da Web. (Consulte [Definindo Modos de Salvamento do Documento do PDF](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Convertendo documentos PDF em documentos XDP {#converting-pdf-documents-into-xdp-documents}

Você pode usar o Java e as APIs de serviço da Web dos Utilitários do PDF para converter programaticamente documentos do PDF em documentos XDP.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para converter um documento PDF em um documento XDP, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente PDFUUtilityService.
1. Chame o PDF para a operação de conversão XDP.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PDFUtilmentService**

Antes de poder executar programaticamente uma operação Utilitários do PDF, tem de criar um cliente PDFUUtilityService. Com a API do Java, isso é feito criando uma `PDFUtilityServiceClient` objeto. Com a API do serviço da Web, isso é feito usando um `PDFUtilityServiceService` objeto.

**Chame a operação de conversão PDF para XDP**

Após criar o cliente de serviço, você pode chamar o PDF para a operação de conversão XDP.

**Consulte também**

[Converter documentos do PDF em documentos XDP usando a API do Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Converter documentos PDF em documentos XDP usando a API de serviço da Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos do PDF em documentos XDP usando a API do Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Converta documentos do PDF em documentos XDP usando a API de utilitários do PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

1. Criar um cliente PDFUtilmentService

   Crie um `PDFUtilityServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Chame a operação de conversão PDF para XDP

   Para executar a conversão, chame o `PDFUtilityServiceClient` do objeto `convertPDFtoXDP` e passar em um `com.adobe.idp.Document` que representa o arquivo PDF. O método retorna um `com.adobe.idp.Document` que representa o arquivo XDP recém-criado.

**Consulte também**

[Convertendo documentos PDF em documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos PDF em documentos XDP usando a API de serviço da Web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Converta documentos do PDF em documentos XDP usando a PDF Utilities API (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o arquivo WSDL do serviço Utilitários PDF.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um cliente PDFUtilmentService

   Crie um `PDFUtilityServiceService` usando seu construtor de classe proxy.

1. Chame a operação de conversão PDF para XDP

   Chame o `PDFUtilityServiceService` do objeto `convertPDFtoXDP` e passar em um `BLOB` que representa o arquivo PDF. O método retorna um `BLOB` que representa o arquivo XDP recém-criado.

**Consulte também**

[Convertendo documentos PDF em documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Convertendo documentos XDP em documentos do PDF {#converting-xdp-documents-into-pdf-documents}

Você pode usar o Java e as APIs de serviço da Web dos Utilitários do PDF para converter programaticamente documentos XDP em documentos do PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-1}

Para converter um documento XDP em um documento PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente PDFUUtilityService.
1. Chame o XDP para operação de conversão de PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PDFUtilmentService**

Antes de poder executar programaticamente uma operação Utilitários do PDF, tem de criar um cliente PDFUUtilityService. Com a API do Java, isso é feito criando uma `PDFUtilityServiceClient` objeto. Com a API do serviço da Web, isso é feito usando um `PDFUtilityServiceService` objeto.

**Chamar a operação de conversão XDP em PDF**

Após criar o cliente de serviço, você pode chamar a operação de conversão XDP em PDF.

**Consulte também**

[Converter documentos XDP em documentos PDF usando a API Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversão de documentos XDP em documentos PDF usando a API de serviço da Web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos XDP em documentos PDF usando a API Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Converta documentos XDP em documentos PDF usando a API de utilitários do PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

1. Criar um cliente PDFUtilmentService

   Crie um `PDFUtilityServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Chamar a operação de conversão XDP em PDF

   Para executar a conversão, chame o `PDFUtilityServiceClient` do objeto `convertXDPtoPDF` e passar em um `com.adobe.idp.Document` que representa o arquivo XDP. O método retorna um `com.adobe.idp.Document` objeto que representa o arquivo PDF recém-criado.

**Consulte também**

[Convertendo documentos XDP em documentos do PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversão de documentos XDP em documentos PDF usando a API de serviço da Web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Converta documentos XDP em documentos PDF usando a API de utilitários do PDF (API de serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o arquivo WSDL do serviço Utilitários PDF.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um cliente PDFUtilmentService

   Crie um `PDFUtilityServiceService` usando seu construtor de classe proxy.

1. Chamar a operação de conversão XDP em PDF

   Para executar a conversão, chame o `PDFUtilityServiceService` do objeto `convertXDPtoPDF` e passar em um `BLOB` que representa o arquivo XDP. O método retorna um `BLOB` objeto que representa o arquivo PDF recém-criado.

**Consulte também**

[Convertendo documentos XDP em documentos do PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Recuperando propriedades do documento do PDF {#retrieving-pdf-document-properties}

Você pode usar o Java e as APIs de serviço da Web dos Utilitários do PDF para recuperar programaticamente as propriedades do documento do PDF, como se o documento é um formulário que pode ser preenchido ou a versão mínima do Acrobat necessária para ler o documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumo das etapas {#summary_of_steps-2}

Para recuperar as propriedades do documento PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente PDFUUtilityService.
1. Chame a operação de recuperação de propriedades.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PDFUtilmentService**

Antes de poder executar programaticamente uma operação Utilitários do PDF, tem de criar um cliente PDFUUtilityService. Com a API do Java, isso é feito criando uma `PDFUtilityServiceClient` objeto. Com a API do serviço da Web, isso é feito usando um `PDFUtilityServiceService` objeto.

**Chame a operação de recuperação de propriedades**

Após criar o cliente de serviço, você pode chamar a operação de recuperação de propriedades.

**Consulte também**

[Recupere as propriedades do documento do PDF usando a API do Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Recuperar propriedades do documento do PDF usando a API do serviço da Web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recupere as propriedades do documento do PDF usando a API do Java {#retrieve-pdf-document-properties-using-the-java-api}

Recupere as propriedades do documento do PDF usando a API de utilitários do PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

1. Criar um cliente PDFUtilmentService

   Crie um `PDFUtilityServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Chame a operação de recuperação de propriedades

   Para executar a conversão, chame o `PDFUtilityServiceClient` do objeto `getPDFProperties` e passam no seguinte:

   * A `com.adobe.idp.Document` objeto que representa o documento PDF.
   * A `PDFPropertiesOptionSpec` objeto que contém as propriedades a serem avaliadas.

   O método retorna um `PDFPropertiesResult` que contém os resultados da consulta.

**Consulte também**

[Recuperando propriedades do documento do PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propriedades do documento do PDF usando a API do serviço da Web {#retrieve-pdf-document-properties-using-the-web-service-api}

Recupere as propriedades do documento do PDF usando a API de serviço da Web Utilitários do PDF:

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o arquivo WSDL do serviço Utilitários PDF.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um cliente PDFUtilmentService

   Crie um `PDFUtilityServiceService` usando seu construtor de classe proxy.

1. Chame a operação de recuperação de propriedades

   Para executar a conversão, chame o `PDFUtilityServiceService` do objeto `getPDFProperties` e passam no seguinte:

   * A `BLOB` objeto que representa o documento PDF.
   * A `PDFPropertiesOptionSpec` objeto que contém as propriedades a serem avaliadas.

   O método retorna um `PDFPropertiesResult` que contém os resultados da consulta.

**Consulte também**

[Recuperando propriedades do documento do PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Definindo Modos de Salvamento do Documento do PDF {#setting-pdf-document-save-modes}

Você pode usar o Java e as APIs de serviço da Web do serviço Utilitários do PDF para definir programaticamente um modo de salvamento para um documento do PDF. Ao usar o serviço Utilitários do PDF para definir um modo de salvamento, o serviço Utilitários do PDF só define o modo de salvamento e não salva o documento PDF. O documento PDF é salvo quando é passado para outra operação de serviço. Por exemplo, você pode usar o serviço Utilitários do PDF para definir um modo de salvamento específico e passá-lo para o serviço de Criptografia, onde o documento PDF é realmente salvo e criptografado.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-3}

Para definir a opção de salvar para documentos do PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente PDFUUtilityService.
1. Defina o modo de salvamento.
1. Chame a operação de salvamento.
1. Transmita o documento PDF para outra operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PDFUtilmentService**

Antes de poder executar programaticamente uma operação Utilitários do PDF, tem de criar um cliente PDFUUtilityService. Com a API do Java, isso é feito criando uma `PDFUtilityServiceClient` objeto. Com a API do serviço da Web, isso é feito usando um `PDFUtilityServiceService` objeto.

**Definir o modo Salvar**

Você pode escolher uma das seguintes opções de gravação:

* `INCREMENTAL`: Para economizar de forma incremental, reduza o tempo necessário para economizar
* `FAST_WEB_VIEW`: salvar para exibição rápida da Web
* `FULL`: Para salvar usando um salvamento completo (sem otimizações)

**Chamar a operação salvar estilo**

Após criar o cliente de serviço, você pode chamar a operação de recuperação de propriedades.

**Transmita o documento PDF para outra operação AEM Forms**

Depois que o serviço Utilitários do PDF definir o modo Salvar especificado, passe o documento do PDF para outra operação do AEM Forms. Depois de retornado dessa operação, o documento PDF é salvo no modo especificado. Por exemplo, se você usar o serviço Utilitários do PDF para definir a variável `FAST_WEB_VIEW` e, em seguida, passe o documento do PDF para o do serviço de criptografia `encryptUsingPassword` , o documento PDF retornado é criptografado com uma senha e salvo no `FAST_WEB_VIEW` modo.

>[!NOTE]
>
>O Início Rápido associado a esta seção define a variável `FAST_WEB_VIEW` e, em seguida, passa o documento PDF para o do serviço de criptografia `encryptUsingPassword` operação.

**Consulte também**

[Definir opções de salvamento do documento do PDF usando a API Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Definir opções de gravação de documento do PDF usando a API de serviço da Web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Criptografar documentos do PDF com uma senha](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Definir opções de salvamento do documento do PDF usando a API Java {#set-pdf-document-save-options-using-the-java-api}

Defina as opções de salvamento do documento do PDF usando a API de utilitários do PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

1. Criar um cliente PDFUtilmentService

   Crie um `PDFUtilityServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Definir o modo Salvar

   * Crie um `PDFUtilitySaveMode` usando seu construtor.
   * Defina o modo de salvamento chamando o `PDFUtilitySaveMode` do objeto `setSaveStyle` e transmitindo um valor de string que especifica o modo de salvamento. Por exemplo, para salvar para exibição rápida da Web, passe `FAST_WEB_VIEW`.

1. Chamar a operação salvar estilo

   Chame o `PDFUtilityServiceClient` do objeto `setSaveMode` e transmita os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o documento PDF.
   * A `PDFUtilitySaveMode` objeto que contém o estilo de salvamento a ser usado.
   * Um valor booleano usado para determinar se deve substituir alguma configuração anterior.

   O método retorna um `com.adobe.idp.Document` objeto formatado usando o estilo de gravação especificado.

1. Transmita o documento PDF para outra operação AEM Forms

   * Envie o relatório `com.adobe.idp.Document` para outra operação do AEM Forms.

**Consulte também**

[Definindo Modos de Salvamento do Documento do PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Definir opções de gravação de documento do PDF usando a API de serviço da Web {#set-pdf-document-save-options-using-the-web-service-api}

Defina as opções de salvamento do documento do PDF usando o PDF Utilities AP (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o arquivo WSDL do serviço Utilitários PDF.
   * Faça referência ao assembly do cliente Microsoft .NET.

1. Criar um cliente PDFUtilmentService

   Crie um `PDFUtilityServiceService` usando seu construtor de classe proxy.

1. Definir o modo Salvar

   * Crie um `PDFUtilitySaveMode` usando seu construtor.
   * Defina o modo de salvamento atribuindo um valor de string à variável `PDFUtilitySaveMode` do objeto `saveStyle` que especifica o modo de salvamento. Por exemplo, para salvar para exibição rápida da Web, especifique `FAST_WEB_VIEW`.

1. Chamar a operação salvar estilo

   Chame o `PDFUtilityServiceService` do objeto `setSaveMode` e transmita os seguintes valores:

   * A `BLOB` objeto que representa o documento PDF.
   * A `PDFUtilitySaveMode` objeto que contém o estilo de salvamento a ser usado.
   * Um valor booleano usado para determinar se deve substituir alguma configuração anterior.

   O método retorna um `BLOB` objeto formatado usando o estilo de gravação especificado. Em seguida, você pode salvar esse objeto como um documento PDF.

1. Transmita o documento PDF para outra operação Forms

   * Envie o relatório `BLOB` para outra operação do AEM Forms.

**Consulte também**

[Definindo Modos de Salvamento do Documento do PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criando um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Como limpar documentos do PDF {#sanitizing-pdf-documents}

Você pode usar as APIs Java de utilitários do PDF para converter programaticamente documentos do PDF em documentos XDP.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-4}

Para limpar o documento PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um cliente PDFUUtilityService.
1. Chame a operação de purificação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Para criar um aplicativo cliente usando Java, inclua os arquivos JAR necessários.

**Criar um cliente PDFUtilmentService**

Antes de poder executar uma operação de limpeza programaticamente, você deve criar um cliente PDFUUtilityService . Com a API do Java, isso é feito criando uma `PDFUtilityServiceClient` objeto.

**Chame a operação de conversão PDF para XDP**

Após criar o cliente de serviço, você pode invocar a operação de limpeza.

**Consulte também**

[Converter documentos do PDF em documentos XDP usando a API do Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Converter documentos PDF em documentos XDP usando a API de serviço da Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Limpar documentos do PDF usando a API do Java {#sanitize-pdf-documents-using-the-java-api}

Limpe documentos usando a API de utilitários do PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

1. Criar um cliente PDFUtilmentService

   Crie um `PDFUtilityServiceClient` usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contém propriedades de conexão.

1. Chame a operação de conversão PDF para XDP

   Para executar a conversão, chame o `PDFUtilityServiceClient` do objeto `convertPDFtoXDP` e passar em um `com.adobe.idp.Document` que representa o arquivo PDF. O método retorna um `com.adobe.idp.Document` que representa o arquivo XDP recém-criado.

**Consulte também**

[Como sanear documentos PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
