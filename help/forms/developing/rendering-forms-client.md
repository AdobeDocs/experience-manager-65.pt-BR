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
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 0%

---

# Renderização do Forms no cliente {#rendering-forms-at-the-client}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

## Renderização do Forms no cliente {#rendering-forms-at-the-client-inner}

Você pode otimizar a entrega de conteúdo de PDF e melhorar a capacidade do serviço Forms de lidar com a carga da rede usando o recurso de renderização do cliente do Acrobat ou Adobe Reader. Esse processo é conhecido como renderização de um formulário no cliente. Para renderizar um formulário no cliente, o dispositivo cliente (normalmente um navegador da Web) deve usar o Acrobat 7.0, Adobe Reader 7.0 ou posterior.

As alterações em um formulário resultante da execução do script do lado do servidor não são refletidas em um formulário renderizado no cliente, a menos que o subformulário raiz contenha a variável `restoreState` atributo definido como `auto`. Para obter mais informações sobre este atributo, consulte [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Antes de executar programaticamente uma operação da API do cliente de serviço do Forms, você deve criar um cliente de serviço do Forms. Se estiver usando a API Java, crie uma `FormsServiceClient` objeto. Se estiver usando a API do serviço Web Forms, crie uma `FormsService` objeto.

**Definir opções de tempo de execução de renderização do cliente**

Defina a opção de tempo de execução de renderização do cliente para renderizar um formulário no cliente definindo o `RenderAtClient` opção de tempo de execução para `true`. Isso resulta no formulário ser entregue ao dispositivo cliente onde é renderizado. Se `RenderAtClient` é `auto` (o valor padrão), o design do formulário determina se ele é renderizado no cliente. O design do formulário deve ser um design de formulário com layout fluível.

Uma opção opcional de tempo de execução que você pode definir é a `SeedPDF` opção. A variável `SeedPDF` A opção combina o contêiner PDF (documento de PDF de propagação) com o design do formulário e os dados XML. O design do formulário e os dados XML são entregues no Acrobat ou Adobe Reader, onde o formulário é renderizado. A variável `SeedPDF` A opção pode ser usada quando o computador cliente não tem fontes que são usadas no formulário, como quando um usuário final não está licenciado para usar uma fonte que o proprietário do formulário está licenciado a usar.

Você pode usar o Designer para criar um arquivo PDF dinâmico simples para usar como um arquivo PDF de seed. As seguintes etapas são necessárias para executar essa tarefa:

1. Determine se é necessário incorporar fontes no arquivo de seed PDF. O arquivo de PDF de propagação deve conter fontes adicionais exigidas pelo formulário que está sendo renderizado. Ao incorporar fontes no arquivo seed PDF, certifique-se de que você não esteja violando nenhum contrato de licenciamento de fontes. No Designer, é possível determinar se as fontes podem ser incorporadas legalmente. Ao salvar, se houver fontes que não podem ser incorporadas ao formulário, o Designer exibirá uma mensagem listando as fontes que não podem ser incorporadas. Esta mensagem não é exibida no Designer para documentos de PDF estáticos.
1. Se você estiver criando o arquivo de PDF de propagação no Designer, é recomendável que, no mínimo, você adicione um campo de texto que contenha uma mensagem. A mensagem deve ser direcionada a usuários de versões anteriores do Adobe Reader informando que precisam do Acrobat 7.0 ou posterior, ou do Adobe Reader 7.0 ou posterior, para visualizar o documento.
1. Salve o arquivo de PDF de seed como um arquivo de PDF dinâmico com a extensão de nome de arquivo de PDF.

>[!NOTE]
>
>Não é necessário definir a opção de tempo de execução de seed PDF para renderizar um formulário no cliente. Se você não especificar um PDF de propagação, o serviço Forms cria um pdf de shell que não conterá objetos COS, mas conterá um invólucro de PDF com o conteúdo XDP real incorporado. As etapas nesta seção não definem a opção de tempo de execução de seed PDF. Para obter informações sobre objetos COS, consulte o Adobe PDF Reference guide.

**Renderizar um formulário no cliente**

Para renderizar um formulário no cliente, você deve garantir que as opções de tempo de execução de renderização do cliente sejam incluídas na lógica do aplicativo para renderizar um formulário.

**Gravar o fluxo de dados do formulário no navegador Web cliente**

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

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `FormsServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Definir opções de tempo de execução de renderização do cliente

   * Criar um `PDFFormRenderSpec` usando seu construtor.
   * Defina o `RenderAtClient` opção de tempo de execução chamando o botão `PDFFormRenderSpec` do objeto `setRenderAtClient` e transmitindo o valor de enum `RenderAtClient.Yes`.

1. Renderizar um formulário no cliente

   Chame o `FormsServiceClient` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do AEM Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` objeto que contém dados a serem mesclados com o formulário. Se não quiser mesclar dados, passe uma tag vazia `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` objeto que armazena as opções de tempo de execução necessárias para renderizar um formulário no cliente.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms para renderizar um formulário.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   A variável `renderPDFForm` o método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Criar um `com.adobe.idp.Document` ao invocar o `FormsResult` object&#39;s `getOutputContent` método.
   * Obter o tipo de conteúdo do `com.adobe.idp.Document` ao invocar seu `getContentType` método.
   * Defina o `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto chamando seu `setContentType` e transmitindo o tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Criar um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados de formulário no navegador da web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método.
   * Criar um `java.io.InputStream` ao invocar o `com.adobe.idp.Document` do objeto `getInputStream` método.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados de formulário chamando o `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

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

   Criar um `FormsService` objeto e definir valores de autenticação.

1. Definir opções de tempo de execução de renderização do cliente

   * Criar um `PDFFormRenderSpec` usando seu construtor.
   * Defina o `RenderAtClient` opção de tempo de execução chamando o botão `PDFFormRenderSpec` do objeto `setRenderAtClient` e transmitindo o valor da string `RenderAtClient.Yes`.

1. Renderizar um formulário no cliente

   Chame o `FormsService` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` objeto que contém dados a serem mesclados com o formulário. Se não quiser mesclar dados, transmita `null`. (Consulte [Pré-preenchimento do Forms com layouts fluíveis](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * A `PDFFormRenderSpec` objeto que armazena as opções de tempo de execução necessárias para renderizar um formulário no cliente.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço do Forms.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto preenchido pelo método. Esse parâmetro é usado para armazenar o formulário de PDF renderizado.
   * Um vazio `javax.xml.rpc.holders.LongHolder` objeto preenchido pelo método. (Esse argumento armazenará o número de páginas no formulário).
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método. (Esse argumento armazenará o valor do local).
   * Um vazio `com.adobe.idp.services.holders.FormsResultHolder` objeto que conterá os resultados desta operação.

   A variável `renderPDFForm` O método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Criar um `FormResult` obtendo o valor do `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value` membro de dados.
   * Criar um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método.
   * Obter o tipo de conteúdo do `BLOB` ao invocar seu `getContentType` método.
   * Defina o `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto chamando seu `setContentType` e transmitindo o tipo de conteúdo do `BLOB` objeto.
   * Criar um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados de formulário no navegador da web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método.
   * Crie uma matriz de bytes e preencha-a chamando o `BLOB` do objeto `getBinaryData` método. Esta tarefa atribui o conteúdo do `FormsResult` à matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

**Consulte também**

[Renderização do Forms no cliente](#rendering-forms-at-the-client)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
