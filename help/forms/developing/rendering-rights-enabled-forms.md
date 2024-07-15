---
title: Renderização do Forms com direitos ativados
description: Use o serviço Forms para renderizar formulários que tenham direitos de uso aplicados. Você pode renderizar formulários com direitos ativados usando a API Java e a API de serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 012a3a9f-542c-4ed1-a092-572bfccbdf21
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 0%

---

# Renderização do Forms com direitos ativados {#rendering-rights-enabled-forms}

O serviço Forms pode renderizar formulários com direitos de uso aplicados. Os direitos de uso pertencem à funcionalidade que está disponível por padrão no Acrobat, mas não no Adobe Reader, como a capacidade de adicionar comentários a um formulário ou preencher campos de formulário e salvar o formulário. Os Forms que têm direitos de uso aplicados a eles são chamados de formulários habilitados por direitos. Um usuário que abre um formulário habilitado para direitos no Adobe Reader pode executar operações habilitadas para esse formulário.

Para aplicar direitos de uso a um formulário, o serviço de extensões do Acrobat Reader DC deve fazer parte da instalação do AEM Forms. Além disso, você deve ter uma credencial válida que permita aplicar direitos de uso a documentos do PDF. Ou seja, você deve configurar corretamente o serviço de extensões do Acrobat Reader DC antes de renderizar um formulário habilitado para direitos. (Consulte [Sobre o Serviço de extensões da Acrobat Reader DC](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>Para renderizar um formulário que contém direitos de uso, você deve usar um arquivo XDP como entrada, não um arquivo PDF. Se você usar um arquivo PDF como entrada, o formulário ainda será renderizado; no entanto, não será um formulário habilitado para direitos.

>[!NOTE]
>
>Não é possível preencher previamente um formulário com dados XML quando você especifica os seguintes direitos de uso: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles` ou `enableDigitalSignatures`. (Consulte [Preenchimento prévio de Forms com Layouts Fluxáveis](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário habilitado para direitos, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Definir opções de tempo de execução de direitos de uso.
1. Renderize um formulário habilitado para direitos.
1. Grave o formulário com direitos ativados no navegador web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente do Forms**

Antes de executar programaticamente uma operação da API do cliente de serviço do Forms, você deve criar um cliente de serviço do Forms.

**Definir opções de tempo de execução de direitos de uso**

Defina as opções de tempo de execução de direitos de uso para renderizar um formulário habilitado para direitos. Especifique o alias da credencial usada para aplicar direitos de uso a um formulário. Depois de especificar o valor do alias, especifique cada direito de uso a ser aplicado ao formulário.

**Renderizar um formulário habilitado para direitos**

Para renderizar um formulário habilitado para direitos, use a mesma lógica de aplicativo que renderizar um formulário sem direitos de uso. A única diferença é que você deve garantir que as opções de tempo de execução de direitos de uso sejam incluídas na lógica do aplicativo.

>[!NOTE]
>
>Ao renderizar um formulário habilitado para direitos usando a API de serviço Web do Forms, não é possível anexar arquivos ao formulário.

**Gravar o fluxo de dados de formulário no navegador Web cliente**

Quando o serviço Forms renderiza um formulário com direitos ativados, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente. Depois de gravado no navegador da Web do cliente, o formulário fica visível para o usuário. Um usuário que visualiza o formulário habilitado para direitos no Adobe Reader pode executar operações habilitadas para esse formulário.

**Consulte também**

[Renderizar formulários com direitos habilitados usando a API Java](#render-rights-enabled-forms-using-the-java-api)

[Renderizar formulários com direitos habilitados usando a API de serviço Web](#render-rights-enabled-forms-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Criação de aplicações Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Renderizar formulários com direitos habilitados usando a API Java {#render-rights-enabled-forms-using-the-java-api}

Renderize um formulário habilitado para direitos usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto da API do cliente do Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Definir opções de tempo de execução de direitos de uso

   * Crie um objeto `ReaderExtensionSpec` usando seu construtor.
   * Especifique o alias da credencial invocando o método `setReCredentialAlias` do objeto `ReaderExtensionSpec` e especifique um valor de cadeia de caracteres que represente o valor do alias.
   * Defina cada direito de uso invocando o método correspondente que pertence ao objeto `ReaderExtensionSpec`. No entanto, você só poderá definir um direito de uso se a credencial à qual você faz referência permitir. Ou seja, você não pode definir um direito de uso se a credencial não permitir sua definição. Por exemplo. para definir o direito de uso que permite ao usuário preencher campos de formulário e salvar o formulário, chame o método `setReFillIn` do objeto `ReaderExtensionSpec` e passe `true`.

   >[!NOTE]
   >
   >Não é necessário invocar o método `setReCredentialPassword` do objeto `ReaderExtensionSpec`. Esse método não é usado pelo serviço Forms.

1. Renderizar um formulário habilitado para direitos

   Invoque o método `renderPDFFormWithUsageRights` do objeto `FormsServiceClient` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você referenciar um design de formulário que faça parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `com.adobe.idp.Document` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução.
   * Um objeto `ReaderExtensionSpec` que armazena opções de tempo de execução de direitos de uso.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.

   O método `renderPDFFormWithUsageRights` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `com.adobe.idp.Document` invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie um objeto `java.io.InputStream` invocando o método `getInputStream` do objeto `com.adobe.idp.Document`.
   * Crie uma matriz de bytes para preenchê-la com o fluxo de dados de formulário, chamando o método `read` do objeto `InputStream` e transmitindo a matriz de bytes como argumento.
   * Invoque o método `write` do objeto `javax.servlet.ServletOutputStream` para enviar o fluxo de dados de formulário para o navegador Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Início rápido (modo SOAP): renderização de um formulário habilitado para direitos usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar formulários com direitos habilitados usando a API de serviço Web {#render-rights-enabled-forms-using-the-web-service-api}

Renderize um formulário habilitado para direitos usando a API do Forms (serviço Web):

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms.
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar um objeto da API do cliente do Forms

   Crie um objeto `FormsService` e defina valores de autenticação.

1. Definir opções de tempo de execução de direitos de uso

   * Crie um objeto `ReaderExtensionSpec` usando seu construtor.
   * Especifique o alias da credencial invocando o método `setReCredentialAlias` do objeto `ReaderExtensionSpec` e especifique um valor de cadeia de caracteres que represente o valor do alias.
   * Defina cada direito de uso invocando o método correspondente que pertence ao objeto `ReaderExtensionSpec`. No entanto, você só poderá definir um direito de uso se a credencial à qual você faz referência permitir. Ou seja, você não pode definir um direito de uso se a credencial não permitir sua definição. Para definir o direito de uso que permite ao usuário preencher campos de formulário e salvar o formulário, chame o método `setReFillIn` do objeto `ReaderExtensionSpec` e passe `true`.

1. Renderizar um formulário habilitado para direitos

   Invoque o método `renderPDFFormWithUsageRights` do objeto `FormsService` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você referenciar um design de formulário que faça parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um objeto `BLOB` que contém dados para mesclar com o formulário. Se não quiser mesclar dados com o formulário, você deve passar um objeto `BLOB` baseado em uma fonte de dados XML vazia. Você não pode passar um objeto `BLOB` que seja nulo; caso contrário, uma exceção será lançada.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução.
   * Um objeto `ReaderExtensionSpec` que armazena opções de tempo de execução de direitos de uso.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.

   O método `renderPDFFormWithUsageRights` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `BLOB` que contenha dados de formulário invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie uma matriz de bytes e preencha-a chamando o método `getBinaryData` do objeto `BLOB`. Esta tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Invoque o método `write` do objeto `javax.servlet.http.HttpServletResponse` para enviar o fluxo de dados de formulário para o navegador Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Renderização do Forms com direitos ativados](#rendering-rights-enabled-forms)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
