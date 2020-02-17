---
title: Trabalhar com utilitários de PDF
seo-title: Trabalhar com utilitários de PDF
description: 'null'
seo-description: 'null'
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Trabalhar com utilitários de PDF {#working-with-pdf-utilities}

**Sobre o serviço de utilitários de PDF**

O serviço Utilitários PDF pode converter entre formatos de arquivo PDF e XDP, definir e recuperar propriedades de documentos PDF e manipular metadados XMP. Por exemplo, antes de converter um documento PDF em outro formato, é útil inspecionar suas propriedades para determinar qual operação de serviço chamar para a conversão.

É possível realizar essas tarefas usando o serviço Utilitários PDF:

* Converta documentos PDF em documentos XDP.
* Converta documentos XDP em documentos PDF. (Consulte [Convertendo documentos XDP em documentos](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)PDF.)
* Recuperar propriedades do documento PDF. (Consulte [Recuperando propriedades](pdf-utilities.md#retrieving-pdf-document-properties)do documento PDF.)
* Salve um documento PDF e otimize-o para visualização rápida na Web. (Consulte [Configuração dos modos](pdf-utilities.md#setting-pdf-document-save-modes)de gravação do documento PDF.)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

## Convertendo documentos PDF em documentos XDP {#converting-pdf-documents-into-xdp-documents}

Você pode usar o Java Utilities de PDF e as APIs de serviço da Web para converter documentos PDF de forma programática em documentos XDP.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary-of-steps}

Para converter um documento PDF em um documento XDP, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDFUutilityService.
1. Chame a operação de conversão PDF em XDP.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Crie um cliente PDFUutilityService**

Antes de executar programaticamente uma operação de Utilitários de PDF, você deve criar um cliente PDFUutilityService. Com a API Java, isso é feito criando um `PDFUtilityServiceClient` objeto. Com a API de serviço da Web, isso é feito usando um `PDFUtilityServiceService` objeto.

**Chamar a operação de conversão de PDF em XDP**

Depois de criar o cliente de serviço, você pode invocar a operação de conversão de PDF em XDP.

**Consulte também:**

[Converta documentos PDF em documentos XDP usando a API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Converter documentos PDF em documentos XDP usando a API de serviço da Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converta documentos PDF em documentos XDP usando a API Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Converta documentos PDF em documentos XDP usando a PDF Utilities API (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente PDFUutilityService

   Crie um `PDFUtilityServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Chamar a operação de conversão de PDF em XDP

   Para executar a conversão, chame o `PDFUtilityServiceClient` método do `convertPDFtoXDP` objeto e passe um `com.adobe.idp.Document` objeto que represente o arquivo PDF. O método retorna um `com.adobe.idp.Document` objeto que representa o arquivo XDP recém-criado.

**Consulte também:**

[Convertendo documentos PDF em documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos PDF em documentos XDP usando a API de serviço da Web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Converta documentos PDF em documentos XDP usando a PDF Utilities API (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o arquivo WSDL do serviço de Utilitários PDF.
   * Consulte o assembly do cliente Microsoft .NET.

1. Crie um cliente PDFUutilityService

   Crie um `PDFUtilityServiceService` objeto usando seu construtor de classe proxy.

1. Chamar a operação de conversão de PDF em XDP

   Chame o `PDFUtilityServiceService` método do `convertPDFtoXDP` objeto e transmita um `BLOB` objeto que representa o arquivo PDF. O método retorna um `BLOB` objeto que representa o arquivo XDP recém-criado.

**Consulte também:**

[Convertendo documentos PDF em documentos XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criação de um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Convertendo documentos XDP em documentos PDF {#converting-xdp-documents-into-pdf-documents}

Você pode usar o Java Utilities do PDF e as APIs de serviço da Web para converter documentos XDP de forma programada em documentos PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary_of_steps-1}

Para converter um documento XDP em um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDFUutilityService.
1. Chame a operação de conversão XDP em PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Crie um cliente PDFUutilityService**

Antes de executar programaticamente uma operação de Utilitários de PDF, você deve criar um cliente PDFUutilityService. Com a API Java, isso é feito criando um `PDFUtilityServiceClient` objeto. Com a API de serviço da Web, isso é feito usando um `PDFUtilityServiceService` objeto.

**Chamar a operação de conversão XDP em PDF**

Depois de criar o cliente de serviço, você pode chamar a operação de conversão XDP em PDF.

**Consulte também:**

[Converta documentos XDP em documentos PDF usando a API Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Converter documentos XDP em documentos PDF usando a API de serviço da Web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converta documentos XDP em documentos PDF usando a API Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Converta documentos XDP em documentos PDF usando a API de utilitários de PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente PDFUutilityService

   Crie um `PDFUtilityServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Chamar a operação de conversão XDP em PDF

   Para executar a conversão, chame o `PDFUtilityServiceClient` método do `convertXDPtoPDF` objeto e transmita um `com.adobe.idp.Document` objeto que representa o arquivo XDP. O método retorna um `com.adobe.idp.Document` objeto que representa o arquivo PDF recém-criado.

**Consulte também:**

[Convertendo documentos XDP em documentos PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Converter documentos XDP em documentos PDF usando a API de serviço da Web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Converta documentos XDP em documentos PDF usando a PDF Utilities API (API de serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o arquivo WSDL do serviço de Utilitários PDF.
   * Consulte o assembly do cliente Microsoft .NET.

1. Crie um cliente PDFUutilityService

   Crie um `PDFUtilityServiceService` objeto usando seu construtor de classe proxy.

1. Chamar a operação de conversão XDP em PDF

   Para executar a conversão, chame o `PDFUtilityServiceService` método do `convertXDPtoPDF` objeto e transmita um `BLOB` objeto que representa o arquivo XDP. O método retorna um `BLOB` objeto que representa o arquivo PDF recém-criado.

**Consulte também:**

[Convertendo documentos XDP em documentos PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criação de um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Recuperando propriedades do documento PDF {#retrieving-pdf-document-properties}

Você pode usar o Java Utilities de PDF e as APIs de serviço da Web para recuperar programaticamente as propriedades do documento PDF, como se o documento é um formulário preenchível ou a versão mínima do Acrobat necessária para ler o documento.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte Referência de [serviços para formulários AEM](https://www.adobe.com/go/learn_aemforms_services_63)

### Resumo das etapas {#summary_of_steps-2}

Para recuperar as propriedades do documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDFUutilityService.
1. Chame a operação de recuperação de propriedades.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Crie um cliente PDFUutilityService**

Antes de executar programaticamente uma operação de Utilitários de PDF, você deve criar um cliente PDFUutilityService. Com a API Java, isso é feito criando um `PDFUtilityServiceClient` objeto. Com a API de serviço da Web, isso é feito usando um `PDFUtilityServiceService` objeto.

**Chamar a operação de recuperação de propriedades**

Depois de criar o cliente de serviço, você pode chamar a operação de recuperação de propriedades.

**Consulte também:**

[Recuperar propriedades do documento PDF usando a API Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Recuperar propriedades de documentos PDF usando a API de serviço da Web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propriedades do documento PDF usando a API Java {#retrieve-pdf-document-properties-using-the-java-api}

Recupere as propriedades do documento PDF usando a API de utilitários de PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente PDFUutilityService

   Crie um `PDFUtilityServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Chamar a operação de recuperação de propriedades

   Para executar a conversão, chame o método do `PDFUtilityServiceClient` objeto `getPDFProperties` e passe o seguinte:

   * Um `com.adobe.idp.Document` objeto que representa o documento PDF.
   * Um `PDFPropertiesOptionSpec` objeto que contém as propriedades a serem avaliadas.
   O método retorna um `PDFPropertiesResult` objeto que contém os resultados da consulta.

**Consulte também:**

[Recuperando propriedades do documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Recuperar propriedades de documentos PDF usando a API de serviço da Web {#retrieve-pdf-document-properties-using-the-web-service-api}

Recupere as propriedades do documento PDF usando a API de serviço da Web Utilitários PDF:

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o arquivo WSDL do serviço de Utilitários PDF.
   * Consulte o assembly do cliente Microsoft .NET.

1. Crie um cliente PDFUutilityService

   Crie um `PDFUtilityServiceService` objeto usando seu construtor de classe proxy.

1. Chamar a operação de recuperação de propriedades

   Para executar a conversão, chame o método do `PDFUtilityServiceService` objeto `getPDFProperties` e passe o seguinte:

   * Um `BLOB` objeto que representa o documento PDF.
   * Um `PDFPropertiesOptionSpec` objeto que contém as propriedades a serem avaliadas.
   O método retorna um `PDFPropertiesResult` objeto que contém os resultados da consulta.

**Consulte também:**

[Recuperando propriedades do documento PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criação de um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Como configurar modos de gravação de documentos PDF {#setting-pdf-document-save-modes}

Você pode usar Java e APIs de serviço da Web do serviço Utilitários PDF para definir programaticamente um modo de gravação para um documento PDF. Ao usar o serviço Utilitários PDF para definir um modo de gravação, o serviço Utilitários PDF define somente o modo de gravação e não salva o documento PDF. O documento PDF é salvo quando é passado para outra operação de serviço. Por exemplo, você pode usar o serviço Utilitários PDF para definir um modo de gravação específico e passá-lo para o serviço de Criptografia, onde o documento PDF é realmente salvo e criptografado.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary_of_steps-3}

Para definir a opção de salvar para documentos PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDFUutilityService.
1. Defina o modo de gravação.
1. Chame a operação de salvamento.
1. Transmita o documento PDF para outra operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Crie um cliente PDFUutilityService**

Antes de executar programaticamente uma operação de Utilitários de PDF, você deve criar um cliente PDFUutilityService. Com a API Java, isso é feito criando um `PDFUtilityServiceClient` objeto. Com a API de serviço da Web, isso é feito usando um `PDFUtilityServiceService` objeto.

**Definir o modo Salvar**

Você pode escolher uma das seguintes opções de gravação:

* `INCREMENTAL`: Para salvar incrementalmente para reduzir o tempo necessário para salvar
* `FAST_WEB_VIEW`: salvar para visualização rápida na Web
* `FULL`: Para salvar usando um salvamento completo (sem otimizações)

**Chamar a operação de estilo de gravação**

Depois de criar o cliente de serviço, você pode chamar a operação de recuperação de propriedades.

**Enviar o documento PDF para outra operação do AEM Forms**

Depois que o serviço Utilitários PDF definir o modo Salvar especificado, passe o documento PDF para outra operação do AEM Forms. Depois de retornado dessa operação, o documento PDF é salvo no modo especificado. Por exemplo, se você usar o serviço Utilitários PDF para definir o `FAST_WEB_VIEW` modo e, em seguida, passar o documento PDF para a operação do serviço de Criptografia, o documento PDF retornado será criptografado com uma senha e salvo no `encryptUsingPassword` `FAST_WEB_VIEW` modo.

>[!NOTE]
>
>O Início rápido associado a esta seção define o `FAST_WEB_VIEW` modo e passa o documento PDF para a `encryptUsingPassword` operação do serviço de criptografia.

**Consulte também:**

[Definir opções de gravação de documento PDF usando a API Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Definir opções de gravação de documento PDF usando a API de serviço da Web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Como criptografar documentos PDF com uma senha](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Definir opções de gravação de documento PDF usando a API Java {#set-pdf-document-save-options-using-the-java-api}

Defina as opções de gravação do documento PDF usando a API de utilitários de PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente PDFUutilityService

   Crie um `PDFUtilityServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Definir o modo Salvar

   * Crie um `PDFUtilitySaveMode` objeto usando seu construtor.
   * Defina o modo de salvamento chamando o método do `PDFUtilitySaveMode` objeto `setSaveStyle` e transmitindo um valor de string que especifica o modo de salvamento. Por exemplo, para salvar para exibição rápida da Web, passe `FAST_WEB_VIEW`.

1. Chamar a operação de estilo de gravação

   Chame o método do `PDFUtilityServiceClient` objeto `setSaveMode` e passe os seguintes valores:

   * Um `com.adobe.idp.Document` objeto que representa o documento PDF.
   * Um `PDFUtilitySaveMode` objeto que contém o estilo de gravação a ser usado.
   * Um valor booliano usado para determinar se as configurações anteriores devem ser substituídas.
   O método retorna um `com.adobe.idp.Document` objeto formatado usando o estilo de gravação especificado.

1. Enviar o documento PDF para outra operação do AEM Forms

   * Passe o objeto retornado para outra operação do AEM Forms. `com.adobe.idp.Document`

**Consulte também:**

[Como configurar modos de gravação de documentos PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Definir opções de gravação de documento PDF usando a API de serviço da Web {#set-pdf-document-save-options-using-the-web-service-api}

Defina as opções de gravação do documento PDF usando o PDF Utilities AP (serviço da Web):

1. Incluir arquivos de projeto

   * Crie um assembly de cliente Microsoft .NET que consuma o arquivo WSDL do serviço de Utilitários PDF.
   * Consulte o assembly do cliente Microsoft .NET.

1. Crie um cliente PDFUutilityService

   Crie um `PDFUtilityServiceService` objeto usando seu construtor de classe proxy.

1. Definir o modo Salvar

   * Crie um `PDFUtilitySaveMode` objeto usando seu construtor.
   * Defina o modo de salvamento atribuindo um valor de string ao método do `PDFUtilitySaveMode` `saveStyle` objeto que especifica o modo de salvamento. Por exemplo, para salvar para exibição rápida da Web, especifique `FAST_WEB_VIEW`.

1. Chamar a operação de estilo de gravação

   Chame o método do `PDFUtilityServiceService` objeto `setSaveMode` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o documento PDF.
   * Um `PDFUtilitySaveMode` objeto que contém o estilo de gravação a ser usado.
   * Um valor booliano usado para determinar se as configurações anteriores devem ser substituídas.
   O método retorna um `BLOB` objeto formatado usando o estilo de gravação especificado. Em seguida, é possível salvar esse objeto como um documento PDF.

1. Enviar o documento PDF para outra operação do Forms

   * Passe o objeto retornado para outra operação do AEM Forms. `BLOB`

**Consulte também:**

[Como configurar modos de gravação de documentos PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Criação de um assembly de cliente .NET que usa codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Como limpar documentos PDF {#sanitizing-pdf-documents}

Você pode usar as APIs Java de utilitários de PDF para converter documentos PDF de forma programática em documentos XDP.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Utilitários PDF, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary_of_steps-4}

Para limpar o documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDFUutilityService.
1. Chame a operação de limpeza.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Para criar um aplicativo cliente usando Java, inclua os arquivos JAR necessários.

**Crie um cliente PDFUutilityService**

Antes de executar programaticamente uma operação de limpeza, você deve criar um cliente PDFUutilityService. Com a API Java, isso é feito criando um `PDFUtilityServiceClient` objeto.

**Chamar a operação de conversão de PDF em XDP**

Depois de criar o cliente de serviço, você pode chamar a operação de limpeza.

**Consulte também:**

[Converta documentos PDF em documentos XDP usando a API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Converter documentos PDF em documentos XDP usando a API de serviço da Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Como limpar documentos PDF usando a API Java {#sanitize-pdf-documents-using-the-java-api}

Limpe documentos usando a API de utilitários de PDF (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-pdfutility-client.jar, no caminho da classe do seu projeto Java.

1. Crie um cliente PDFUutilityService

   Crie um `PDFUtilityServiceClient` objeto usando seu construtor e transmitindo um `ServiceClientFactory` objeto que contenha propriedades de conexão.

1. Chamar a operação de conversão de PDF em XDP

   Para executar a conversão, chame o `PDFUtilityServiceClient` método do `convertPDFtoXDP` objeto e passe um `com.adobe.idp.Document` objeto que represente o arquivo PDF. O método retorna um `com.adobe.idp.Document` objeto que representa o arquivo XDP recém-criado.

**Consulte também:**

[Como limpar documentos PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
