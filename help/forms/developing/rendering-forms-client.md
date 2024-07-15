---
title: Renderização do Forms no cliente
description: Otimizar a entrega de conteúdo PDF e melhorar a capacidade do serviço Forms de lidar com a carga da rede usando o recurso de renderização do cliente do Acrobat ou Adobe Reader
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e485980d-f200-46b7-9284-c9996003aa47
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 0%

---

# Renderização do Forms no cliente {#rendering-forms-at-the-client}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

## Renderização do Forms no cliente {#rendering-forms-at-the-client-inner}

Você pode otimizar a entrega de conteúdo de PDF e melhorar a capacidade do serviço Forms de lidar com a carga da rede usando o recurso de renderização do cliente do Acrobat ou Adobe Reader. Esse processo é conhecido como renderização de um formulário no cliente. Para renderizar um formulário no cliente, o dispositivo cliente (normalmente um navegador da Web) deve usar o Acrobat 7.0, Adobe Reader 7.0 ou posterior.

As alterações em um formulário resultante da execução de script do lado do servidor não são refletidas em um formulário renderizado no cliente, a menos que o subformulário raiz contenha o atributo `restoreState` definido como `auto`. Para obter mais informações sobre este atributo, consulte [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para renderizar um formulário no cliente, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Definir opções de tempo de execução de renderização do cliente.
1. Renderize um formulário no cliente.
1. Escreva o formulário no navegador web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente do Forms**

Antes de executar programaticamente uma operação da API do cliente de serviço do Forms, você deve criar um cliente de serviço do Forms. Se você estiver usando a API Java, crie um objeto `FormsServiceClient`. Se você estiver usando a API de serviço Web Forms, crie um objeto `FormsService`.

**Definir opções de tempo de execução de renderização do cliente**

Defina a opção de tempo de execução de renderização do cliente para renderizar um formulário no cliente definindo a opção de tempo de execução `RenderAtClient` como `true`. Isso resulta no formulário ser entregue ao dispositivo cliente onde é renderizado. Se `RenderAtClient` for `auto` (valor padrão), o design do formulário determinará se ele será renderizado no cliente. O design do formulário deve ser um design de formulário com layout fluível.

Uma opção opcional de tempo de execução que você pode definir é a opção `SeedPDF`. A opção `SeedPDF` combina o contêiner PDF (documento PDF de propagação) com o design do formulário e os dados XML. O design do formulário e os dados XML são entregues no Acrobat ou Adobe Reader, onde o formulário é renderizado. A opção `SeedPDF` pode ser usada quando o computador cliente não tem fontes que são usadas no formulário, como quando um usuário final não está licenciado para usar uma fonte que o proprietário do formulário está licenciado para usar.

Você pode usar o Designer para criar um arquivo PDF dinâmico simples para usar como um arquivo PDF de seed. As seguintes etapas são necessárias para executar essa tarefa:

1. Determine se é necessário incorporar fontes no arquivo de seed PDF. O arquivo de PDF de propagação deve conter fontes adicionais exigidas pelo formulário que está sendo renderizado. Ao incorporar fontes no arquivo seed PDF, certifique-se de que você não esteja violando nenhum contrato de licenciamento de fontes. No Designer, é possível determinar se as fontes podem ser incorporadas legalmente. Ao salvar, se houver fontes que não podem ser incorporadas ao formulário, o Designer exibirá uma mensagem listando as fontes que não podem ser incorporadas. Esta mensagem não é exibida no Designer para documentos de PDF estáticos.
1. Se você estiver criando o arquivo de PDF de propagação no Designer, é recomendável que, no mínimo, você adicione um campo de texto que contenha uma mensagem. A mensagem deve ser direcionada a usuários de versões anteriores do Adobe Reader informando que precisam do Acrobat 7.0 ou posterior, ou do Adobe Reader 7.0 ou posterior, para visualizar o documento.
1. Salve o arquivo de PDF de seed como um arquivo de PDF dinâmico com a extensão de nome de arquivo de PDF.

>[!NOTE]
>
>Não é necessário definir a opção de tempo de execução de seed PDF para renderizar um formulário no cliente. Se você não especificar um PDF de propagação, o serviço Forms cria um pdf de shell que não conterá objetos COS, mas conterá um invólucro de PDF com o conteúdo XDP real incorporado. As etapas nesta seção não definem a opção de tempo de execução de seed PDF. Para obter informações sobre objetos COS, consulte o Adobe PDF Reference guide.

**Renderizar um formulário no cliente**

Para renderizar um formulário no cliente, você deve garantir que as opções de tempo de execução de renderização do cliente sejam incluídas na lógica do aplicativo para renderizar um formulário.

**Gravar o fluxo de dados de formulário no navegador Web cliente**

O serviço Forms cria um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário é renderizado pelo Acrobat 7.0 ou Adobe Reader 7.0 ou posterior e fica visível para o usuário.

**Consulte também**

[Renderizar um formulário no cliente usando a API Java](#render-a-form-at-the-client-using-the-java-api)

[Renderizar um formulário no cliente usando a API do serviço Web](#render-a-form-at-the-client-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Passar documentos para o serviço da Forms](/help/forms/developing/passing-documents-forms-service.md)

[Criação de aplicações Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Renderizar um formulário no cliente usando a API Java {#render-a-form-at-the-client-using-the-java-api}

Renderize um formulário no cliente usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto da API do cliente do Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Definir opções de tempo de execução de renderização do cliente

   * Crie um objeto `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de tempo de execução `RenderAtClient` invocando o método `setRenderAtClient` do objeto `PDFFormRenderSpec` e transmitindo o valor de enumeração `RenderAtClient.Yes`.

1. Renderizar um formulário no cliente

   Chame o método `renderPDFForm` do objeto `FormsServiceClient` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você referenciar um design de formulário que faça parte de um aplicativo do AEM Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `com.adobe.idp.Document` vazio.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução necessárias para renderizar um formulário no cliente.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms para renderizar um formulário.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `com.adobe.idp.Document` invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie um objeto `java.io.InputStream` invocando o método `getInputStream` do objeto `com.adobe.idp.Document`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados de formulário, chamando o método `read` do objeto `InputStream` e transmitindo a matriz de bytes como argumento.
   * Invoque o método `write` do objeto `javax.servlet.ServletOutputStream` para enviar o fluxo de dados de formulário para o navegador da Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Início rápido (modo SOAP): renderização de um formulário no cliente usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Renderizar um formulário no cliente usando a API do serviço Web {#render-a-form-at-the-client-using-the-web-service-api}

Renderize um formulário no cliente usando a API do Forms (serviço Web):

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms.
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar um objeto da API do cliente do Forms

   Crie um objeto `FormsService` e defina valores de autenticação.

1. Definir opções de tempo de execução de renderização do cliente

   * Crie um objeto `PDFFormRenderSpec` usando seu construtor.
   * Defina a opção de tempo de execução `RenderAtClient` invocando o método `setRenderAtClient` do objeto `PDFFormRenderSpec` e passando o valor da cadeia de caracteres `RenderAtClient.Yes`.

1. Renderizar um formulário no cliente

   Chame o método `renderPDFForm` do objeto `FormsService` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você referenciar um design de formulário que faça parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um objeto `BLOB` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe `null`. (Consulte [Preenchimento prévio de Forms com Layouts Fluxáveis](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução necessárias para renderizar um formulário no cliente.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um objeto `com.adobe.idp.services.holders.BLOBHolder` vazio preenchido pelo método. Esse parâmetro é usado para armazenar o formulário de PDF renderizado.
   * Um objeto `javax.xml.rpc.holders.LongHolder` vazio preenchido pelo método. (Esse argumento armazenará o número de páginas no formulário).
   * Um objeto `javax.xml.rpc.holders.StringHolder` vazio preenchido pelo método. (Esse argumento armazenará o valor do local).
   * Um objeto `com.adobe.idp.services.holders.FormsResultHolder` vazio que conterá os resultados desta operação.

   O método `renderPDFForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `value` do objeto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Crie um objeto `BLOB` que contenha dados de formulário invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie uma matriz de bytes e preencha-a chamando o método `getBinaryData` do objeto `BLOB`. Esta tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Invoque o método `write` do objeto `javax.servlet.http.HttpServletResponse` para enviar o fluxo de dados de formulário para o navegador da Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Renderização do Forms no cliente](#rendering-forms-at-the-client)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
