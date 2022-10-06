---
title: Renderização do Forms no cliente
seo-title: Rendering Forms at the Client
description: Otimizar a entrega de conteúdo de PDF e melhorar a capacidade do serviço Forms de lidar com a carga da rede usando o recurso de renderização do lado do cliente do Acrobat ou Adobe Reader
seo-description: Optimize the delivery of PDF content and improve the Forms service’s ability to handle network load by using the client-side rendering capability of Acrobat or Adobe Reader
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Developer
exl-id: e485980d-f200-46b7-9284-c9996003aa47
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 0%

---

# Renderização do Forms no cliente {#rendering-forms-at-the-client}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

## Renderização do Forms no cliente {#rendering-forms-at-the-client-inner}

Você pode otimizar a entrega de conteúdo de PDF e melhorar a capacidade do serviço Forms de lidar com a carga da rede usando o recurso de renderização do lado do cliente do Acrobat ou Adobe Reader. Esse processo é conhecido como renderização de um formulário no cliente. Para renderizar um formulário no cliente, o dispositivo cliente (geralmente um navegador da Web) deve usar o Acrobat 7.0 ou Adobe Reader 7.0 ou posterior.

As alterações em um formulário resultantes da execução de scripts do lado do servidor não são refletidas em um formulário renderizado no cliente, a menos que o subformulário raiz contenha a variável `restoreState` atributo definido como `auto`. Para obter mais informações sobre esse atributo, consulte [Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para renderizar um formulário no cliente, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Defina as opções de tempo de execução da renderização do cliente.
1. Renderize um formulário no cliente.
1. Escreva o formulário no navegador da Web cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente do Forms**

Antes de executar programaticamente uma operação de API do cliente de serviço do Forms, é necessário criar um cliente de serviço do Forms. Se estiver usando a API do Java, crie um `FormsServiceClient` objeto. Se estiver usando a API do serviço da Web da Forms, crie um `FormsService` objeto.

**Definir opções de tempo de execução de renderização do cliente**

É necessário definir a opção de tempo de execução de renderização do cliente para renderizar um formulário no cliente definindo a variável `RenderAtClient` opção de tempo de execução para `true`. Isso resulta no formulário ser entregue ao dispositivo cliente onde é renderizado. If `RenderAtClient` é `auto` (o valor padrão), o design de formulário determina se o formulário é renderizado no cliente. O design de formulário deve ser um design de formulário com um layout flutuante.

Uma opção opcional de tempo de execução que você pode definir é o `SeedPDF` opção. O `SeedPDF` combina o PDF container (documento de PDF de distribuição) com o design de formulário e os dados XML. Tanto o design de formulário quanto os dados XML são fornecidos para o Acrobat ou Adobe Reader, onde o formulário é renderizado. O `SeedPDF` pode ser usada quando o computador cliente não tem fontes usadas no formulário, como quando um usuário final não está licenciado para usar uma fonte que o proprietário do formulário está licenciado para usar.

Você pode usar o Designer para criar um arquivo de PDF dinâmico simples para usar como um arquivo de PDF de propagação. As etapas a seguir são necessárias para executar essa tarefa:

1. Determine se você precisa incorporar alguma fonte no arquivo seed PDF. O arquivo seed PDF precisará conter fontes adicionais necessárias para o formulário que está sendo renderizado. Ao incorporar fontes no arquivo seed PDF, certifique-se de não estar violando quaisquer contratos de licenciamento de fontes. No Designer, você pode determinar se pode incorporar fontes legalmente. Ao salvar, se houver fontes que não possam ser incorporadas ao formulário, o Designer exibirá uma mensagem listando as fontes que não podem ser incorporadas. Essa mensagem não é exibida no Designer para documentos PDF estáticos.
1. Se você estiver criando o arquivo seed PDF no Designer, é recomendável adicionar um campo de texto que contenha uma mensagem, no mínimo. A mensagem deve ser direcionada a usuários de versões anteriores do Adobe Reader declarando que eles precisam do Acrobat 7.0 ou posterior ou do Adobe Reader 7.0 ou posterior para visualizar o documento.
1. Salve o arquivo seed PDF como um arquivo PDF dinâmico com a extensão do nome do arquivo PDF.

>[!NOTE]
>
>Não é necessário definir a opção de tempo de execução do seed PDF para renderizar um formulário no cliente. Se você não especificar um seed PDF, o serviço Forms cria um pdf de shell que não conterá objetos COS, mas conterá um wrapper PDF com o conteúdo XDP real incorporado no. As etapas nesta seção não definem a opção de tempo de execução do PDF de distribuição. Para obter informações sobre objetos COS, consulte o Guia de referência do Adobe PDF.

**Renderizar um formulário no cliente**

Para renderizar um formulário no cliente, você deve garantir que as opções de tempo de execução da renderização do cliente sejam incluídas na lógica do aplicativo para renderizar um formulário.

**Gravar o fluxo de dados do formulário no navegador da Web cliente**

O serviço Forms cria um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário é renderizado pelo Acrobat 7.0 ou Adobe Reader 7.0 ou posterior e é visível para o usuário.

**Consulte também**

[Renderizar um formulário no cliente usando a API do Java](#render-a-form-at-the-client-using-the-java-api)

[Renderizar um formulário no cliente usando a API do serviço da Web](#render-a-form-at-the-client-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Enviar documentos para o serviço do Forms](/help/forms/developing/passing-documents-forms-service.md)

[Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Renderizar um formulário no cliente usando a API do Java {#render-a-form-at-the-client-using-the-java-api}

Renderize um formulário no cliente usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente do Forms

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `FormsServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Definir opções de tempo de execução de renderização do cliente

   * Crie um `PDFFormRenderSpec` usando seu construtor.
   * Defina as `RenderAtClient` opção de tempo de execução chamando o `PDFFormRenderSpec` do objeto `setRenderAtClient` e transmitindo o valor de enum `RenderAtClient.Yes`.

1. Renderizar um formulário no cliente

   Chame o `FormsServiceClient` do objeto `renderPDFForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo AEM Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` objeto que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um vazio `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução necessárias para renderizar um formulário no cliente.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms para renderizar um formulário.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `com.adobe.idp.Document` chamando o `FormsResult` objeto &quot;s `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `com.adobe.idp.Document` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie um `java.io.InputStream` chamando o `com.adobe.idp.Document` do objeto `getInputStream` método .
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Início rápido (modo SOAP): Renderização de um formulário no cliente usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Renderizar um formulário no cliente usando a API do serviço da Web {#render-a-form-at-the-client-using-the-web-service-api}

Renderize um formulário no cliente usando a Forms API (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do cliente do Forms

   Crie um `FormsService` e definir valores de autenticação.

1. Definir opções de tempo de execução de renderização do cliente

   * Crie um `PDFFormRenderSpec` usando seu construtor.
   * Defina as `RenderAtClient` opção de tempo de execução chamando o `PDFFormRenderSpec` do objeto `setRenderAtClient` e transmitindo o valor da string `RenderAtClient.Yes`.

1. Renderizar um formulário no cliente

   Chame o `FormsService` do objeto `renderPDFForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` objeto que contém dados para mesclar com o formulário. Se você não deseja mesclar dados, use `null`. (Consulte [Pré-preenchimento do Forms com layouts flutuantes](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução necessárias para renderizar um formulário no cliente.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto preenchido pelo método . Esse parâmetro é usado para armazenar o formulário PDF renderizado.
   * Um vazio `javax.xml.rpc.holders.LongHolder` objeto preenchido pelo método . (Esse argumento armazenará o número de páginas no formulário).
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método . (Esse argumento armazenará o valor da localidade).
   * Um vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O `renderPDFForm` O método preenche a variável `com.adobe.idp.services.holders.FormsResultHolder` objeto que é passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `FormResult` obtendo o valor da variável `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value` membro de dados.
   * Crie um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `BLOB` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `BLOB` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie uma matriz de bytes e preencha-a chamando a variável `BLOB` do objeto `getBinaryData` método . Essa tarefa atribui o conteúdo da `FormsResult` para a matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Renderização do Forms no cliente](#rendering-forms-at-the-client)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
