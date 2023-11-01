---
title: Renderização do Forms com direitos ativados
seo-title: Rendering Rights-Enabled Forms
description: Use o serviço Forms para renderizar formulários que tenham direitos de uso aplicados. Você pode renderizar formulários com direitos ativados usando a API Java e a API de serviço da Web.
seo-description: Use the Forms service to render forms that have usage rights applied to them. You can render rights-enabled forms using the Java API and Web Service API.
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: Developer
exl-id: 012a3a9f-542c-4ed1-a092-572bfccbdf21
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 0%

---

# Renderização do Forms com direitos ativados {#rendering-rights-enabled-forms}

O serviço Forms pode renderizar formulários com direitos de uso aplicados. Os direitos de uso pertencem à funcionalidade que está disponível por padrão no Acrobat, mas não no Adobe Reader, como a capacidade de adicionar comentários a um formulário ou preencher campos de formulário e salvar o formulário. Os Forms que têm direitos de uso aplicados a eles são chamados de formulários habilitados por direitos. Um usuário que abre um formulário habilitado para direitos no Adobe Reader pode executar operações habilitadas para esse formulário.

Para aplicar direitos de uso a um formulário, o serviço de extensões do Acrobat Reader DC deve fazer parte da instalação do AEM Forms. Além disso, você deve ter uma credencial válida que permita aplicar direitos de uso a documentos do PDF. Ou seja, você deve configurar corretamente o serviço de extensões do Acrobat Reader DC antes de renderizar um formulário habilitado para direitos. (Consulte [Sobre o serviço de extensões da Acrobat Reader DC](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>Para renderizar um formulário que contém direitos de uso, você deve usar um arquivo XDP como entrada, não um arquivo PDF. Se você usar um arquivo PDF como entrada, o formulário ainda será renderizado; no entanto, não será um formulário habilitado para direitos.

>[!NOTE]
>
>Não é possível preencher previamente um formulário com dados XML ao especificar os seguintes direitos de uso: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles`ou `enableDigitalSignatures`. (Consulte [Pré-preenchimento do Forms com layouts fluíveis](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Você deve definir opções de tempo de execução de direitos de uso para renderizar um formulário habilitado para direitos. Você também deve especificar o alias da credencial usada para aplicar direitos de uso a um formulário. Depois de especificar o valor do alias, especifique cada direito de uso a ser aplicado ao formulário.

**Renderizar um formulário habilitado para direitos**

Para renderizar um formulário habilitado para direitos, use a mesma lógica de aplicativo que renderizar um formulário sem direitos de uso. A única diferença é que você deve garantir que as opções de tempo de execução de direitos de uso sejam incluídas na lógica do aplicativo.

>[!NOTE]
>
>Ao renderizar um formulário habilitado para direitos usando a API de serviço Web do Forms, não é possível anexar arquivos ao formulário.

**Gravar o fluxo de dados do formulário no navegador Web cliente**

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

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `FormsServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Definir opções de tempo de execução de direitos de uso

   * Criar um `ReaderExtensionSpec` usando seu construtor.
   * Especifique o alias da credencial invocando o `ReaderExtensionSpec` do objeto `setReCredentialAlias` e especifique um valor de string que represente o valor do alias.
   * Defina cada direito de uso invocando o método correspondente pertencente ao `ReaderExtensionSpec` objeto. No entanto, você só poderá definir um direito de uso se a credencial à qual você faz referência permitir. Ou seja, você não pode definir um direito de uso se a credencial não permitir sua definição. Por exemplo. para definir o direito de uso que permite ao usuário preencher campos de formulário e salvar o formulário, chame o `ReaderExtensionSpec` do objeto `setReFillIn` e passar `true`.

   >[!NOTE]
   >
   >Não é necessário invocar o princípio `ReaderExtensionSpec` do objeto `setReCredentialPassword` método. Esse método não é usado pelo serviço Forms.

1. Renderizar um formulário habilitado para direitos

   Chame o `FormsServiceClient` do objeto `renderPDFFormWithUsageRights` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` objeto que contém dados a serem mesclados com o formulário. Se não quiser mesclar dados, passe uma tag vazia `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução.
   * A `ReaderExtensionSpec` objeto que armazena opções de tempo de execução de direitos de uso.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço do Forms.

   A variável `renderPDFFormWithUsageRights` o método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Criar um `com.adobe.idp.Document` ao invocar o `FormsResult` object&#39;s `getOutputContent` método.
   * Obter o tipo de conteúdo do `com.adobe.idp.Document` ao invocar seu `getContentType` método.
   * Defina o `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto chamando seu `setContentType` e transmitindo o tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Criar um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados de formulário no navegador da web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método.
   * Criar um `java.io.InputStream` ao invocar o `com.adobe.idp.Document` do objeto `getInputStream` método.
   * Crie uma matriz de bytes para preenchê-la com o fluxo de dados de formulário, chamando o `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

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

   Criar um `FormsService` objeto e definir valores de autenticação.

1. Definir opções de tempo de execução de direitos de uso

   * Criar um `ReaderExtensionSpec` usando seu construtor.
   * Especifique o alias da credencial invocando o `ReaderExtensionSpec` do objeto `setReCredentialAlias` e especifique um valor de string que represente o valor do alias.
   * Defina cada direito de uso invocando o método correspondente pertencente ao `ReaderExtensionSpec` objeto. No entanto, você só poderá definir um direito de uso se a credencial à qual você faz referência permitir. Ou seja, você não pode definir um direito de uso se a credencial não permitir sua definição. Para definir o direito de uso que permite ao usuário preencher campos de formulário e salvar o formulário, chame o `ReaderExtensionSpec` do objeto `setReFillIn` e passar `true`.

1. Renderizar um formulário habilitado para direitos

   Chame o `FormsService` do objeto `renderPDFFormWithUsageRights` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` objeto que contém dados a serem mesclados com o formulário. Se não quiser mesclar dados com o formulário, você deve passar um `BLOB` objeto baseado em uma fonte de dados XML vazia. Você não pode passar um `BLOB` objeto nulo; caso contrário, uma exceção será lançada.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução.
   * A `ReaderExtensionSpec` objeto que armazena opções de tempo de execução de direitos de uso.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço do Forms.

   A variável `renderPDFFormWithUsageRights` o método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Criar um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método.
   * Obter o tipo de conteúdo do `BLOB` ao invocar seu `getContentType` método.
   * Defina o `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto chamando seu `setContentType` e transmitindo o tipo de conteúdo do `BLOB` objeto.
   * Criar um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados de formulário no navegador da web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método.
   * Crie uma matriz de bytes e preencha-a chamando o `BLOB` do objeto `getBinaryData` método. Esta tarefa atribui o conteúdo do `FormsResult` à matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

**Consulte também**

[Renderização do Forms com direitos ativados](#rendering-rights-enabled-forms)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
