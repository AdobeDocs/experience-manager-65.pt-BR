---
title: Forms com direitos de renderização ativados
seo-title: Forms com direitos de renderização ativados
description: 'null'
seo-description: nulo
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 0%

---


# Renderizando Forms habilitado para direitos {#rendering-rights-enabled-forms}

O serviço Forms pode renderizar formulários com direitos de uso aplicados a eles. Os direitos de uso pertencem à funcionalidade que está disponível por padrão no Acrobat, mas não no Adobe Reader, como a capacidade de adicionar comentários a um formulário ou preencher campos de formulário e salvar o formulário. O Forms que tem direitos de uso aplicados a eles são chamados de formulários habilitados para direitos. Um usuário que abre um formulário com direitos ativados no Adobe Reader pode executar operações ativadas para esse formulário.

Para aplicar direitos de uso a um formulário, o serviço de extensões da Acrobat Reader DC deve fazer parte da instalação de formulários AEM. Além disso, você deve ter uma credencial válida que permita aplicar direitos de uso a documentos PDF. Ou seja, você deve configurar corretamente o serviço de extensões do Acrobat Reader DC antes de poder renderizar um formulário com direitos ativados. (Consulte [Sobre o Serviço de extensões do Acrobat Reader DC](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service).)

>[!NOTE]
>
>Para renderizar um formulário que contenha direitos de uso, é necessário usar um arquivo XDP como entrada, não como um arquivo PDF. Se um arquivo PDF for usado como entrada, o formulário ainda será renderizado; no entanto, não será um formulário com direitos ativados.

>[!NOTE]
>
>Não é possível pré-preencher um formulário com dados XML ao especificar os seguintes direitos de uso: `enableComments`, `enableCommentsOnline`, `enableEmbeddedFiles` ou `enableDigitalSignatures`. (Consulte [Pré-preencher o Forms com layouts flutuantes](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário com direitos ativados, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do Forms Client.
1. Defina opções de tempo de execução de direitos de uso.
1. Renderize um formulário com direitos ativados.
1. Grave o formulário com direitos habilitados no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Forms Client**

Antes de executar programaticamente uma operação de API do cliente de serviço da Forms, você deve criar um cliente de serviço da Forms.

**Definir opções de tempo de execução de direitos de uso**

É necessário definir opções de tempo de execução de direitos de uso para renderizar um formulário habilitado para direitos. Você também deve especificar o alias da credencial usada para aplicar direitos de uso a um formulário. Depois de especificar o valor do alias, especifique cada direito de uso a ser aplicado ao formulário.

**Renderizar um formulário habilitado para direitos**

Para renderizar um formulário com direitos ativados, use a mesma lógica de aplicativo que renderizar um formulário sem direitos de uso. A única diferença é que você deve garantir que as opções de tempo de execução de direitos de uso sejam incluídas na lógica do aplicativo.

>[!NOTE]
>
>Ao renderizar um formulário habilitado para direitos usando a API de serviço da Web da Forms, não é possível anexar arquivos ao formulário.

**Gravar o fluxo de dados do formulário no navegador da Web do cliente**

Quando o serviço Forms renderiza um formulário com direitos ativados, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente. Depois de gravado no navegador da Web do cliente, o formulário fica visível para o usuário. Um usuário que exibe o formulário com direitos ativados no Adobe Reader pode executar operações ativadas para esse formulário.

**Consulte também:**

[Renderizar formulários ativados por direitos usando a API Java](#render-rights-enabled-forms-using-the-java-api)

[Renderizar formulários habilitados por direitos usando a API de serviço da Web](#render-rights-enabled-forms-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API de serviço da Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Criação de Aplicações web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Renderizar formulários ativados por direitos usando a API Java {#render-rights-enabled-forms-using-the-java-api}

Renderize um formulário habilitado para direitos usando a API da Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do Forms Client

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Definir opções de tempo de execução de direitos de uso

   * Crie um objeto `ReaderExtensionSpec` usando seu construtor.
   * Especifique o alias da credencial chamando o método `ReaderExtensionSpec` do objeto `setReCredentialAlias` e especifique um valor de string que representa o valor do alias.
   * Defina cada direito de uso chamando o método correspondente que pertence ao objeto `ReaderExtensionSpec`. No entanto, você só pode definir um direito de uso se a credencial que você menciona permitir que você o faça. Ou seja, você não pode definir um direito de uso se a credencial não permitir que você o defina. Por exemplo. para definir o direito de uso que permite ao usuário preencher campos de formulário e salvar o formulário, chame o método `ReaderExtensionSpec` do objeto `setReFillIn` e passe `true`.

   >[!NOTE]
   >
   >Não é necessário invocar o método `ReaderExtensionSpec` do objeto `setReCredentialPassword`. Este método não é usado pelo serviço Forms.

1. Renderizar um formulário habilitado para direitos

   Chame o método `FormsServiceClient` do objeto `renderPDFFormWithUsageRights` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um objeto `com.adobe.idp.Document` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe um objeto `com.adobe.idp.Document` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução.
   * Um objeto `ReaderExtensionSpec` que armazena opções de tempo de execução de direitos de uso.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.

   O método `renderPDFFormWithUsageRights` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie um objeto `java.io.InputStream` invocando o método `com.adobe.idp.Document` do objeto `getInputStream`.
   * Crie uma matriz de bytes para preenchê-la com o fluxo de dados do formulário, chamando o método `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Start rápido (modo SOAP): Como renderizar um formulário habilitado para direitos usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar formulários ativados por direitos usando a API de serviço da Web {#render-rights-enabled-forms-using-the-web-service-api}

Renderize um formulário habilitado para direitos usando a API da Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do Forms Client

   Crie um objeto `FormsService` e defina os valores de autenticação.

1. Definir opções de tempo de execução de direitos de uso

   * Crie um objeto `ReaderExtensionSpec` usando seu construtor.
   * Especifique o alias da credencial chamando o método `ReaderExtensionSpec` do objeto `setReCredentialAlias` e especifique um valor de string que representa o valor do alias.
   * Defina cada direito de uso chamando o método correspondente que pertence ao objeto `ReaderExtensionSpec`. No entanto, você só pode definir um direito de uso se a credencial que você menciona permitir que você o faça. Ou seja, você não pode definir um direito de uso se a credencial não permitir que você o defina. Para definir o direito de uso que permite ao usuário preencher campos de formulário e salvar o formulário, chame o método `ReaderExtensionSpec` do objeto `setReFillIn` e passe `true`.

1. Renderizar um formulário habilitado para direitos

   Chame o método `FormsService` do objeto `renderPDFFormWithUsageRights` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um objeto `BLOB` que contém dados a serem unidos ao formulário. Se você não quiser unir dados ao formulário, é necessário enviar um objeto `BLOB` que seja baseado em uma fonte de dados XML vazia. Não é possível transmitir um objeto `BLOB` nulo; caso contrário, uma exceção será lançada.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução.
   * Um objeto `ReaderExtensionSpec` que armazena opções de tempo de execução de direitos de uso.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.

   O método `renderPDFFormWithUsageRights` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `BLOB` que contenha dados de formulário chamando o método `FormsResult` do objeto `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie uma matriz de bytes e preencha-a chamando o método `BLOB` do objeto `getBinaryData`. Essa tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Forms com direitos de renderização ativados](#rendering-rights-enabled-forms)

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
