---
title: Renderização do HTML Forms usando arquivos CSS personalizados
seo-title: Rendering HTML Forms Using Custom CSS Files
description: Use o serviço Forms para fazer referência a arquivos CSS personalizados para renderizar formulários HTML em resposta a uma solicitação HTTP de um navegador da Web. É possível renderizar um formulário HTML que use um arquivo CSS usando a API do Java e a API do serviço da Web.
seo-description: Use the Forms service to refer to custom CSS files to render HTML forms in response to an HTTP request from a web browser. You can render an HTML form that uses a CSS file using the Java API and Web Service API.
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
role: Developer
exl-id: 5fa385a7-f030-4c0c-8938-0991d02ef361
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1688'
ht-degree: 0%

---

# Renderização do HTML Forms usando arquivos CSS personalizados {#rendering-html-forms-using-custom-css-files}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

O serviço Forms renderiza formulários HTML em resposta a uma solicitação HTTP de um navegador da Web. Ao renderizar um formulário HTML, o serviço Forms pode fazer referência a um arquivo CSS personalizado. Você pode criar um arquivo CSS personalizado para atender aos requisitos da sua empresa e fazer referência a esse arquivo CSS ao usar o serviço Forms para renderizar formulários de HTML.

O serviço Forms analisa silenciosamente o arquivo CSS personalizado. Ou seja, o serviço Forms não relata erros que podem ser encontrados se o arquivo CSS personalizado não estiver em conformidade com os padrões CSS. Nessa situação, o serviço Forms ignora o estilo e continua com os estilos restantes localizados no arquivo CSS.

A lista a seguir especifica os estilos compatíveis com um arquivo CSS personalizado:

* **Pares de estilo do seletor de nível de classe**: Se presentes em um arquivo CSS personalizado, são usados seletores usados no formulário HTML como estilos de classe. Os estilos de classe não usados são ignorados.
* **Pares de estilo do seletor de nível de identificador**: Todos os estilos de identificador são usados no formulário HTML.
* **Pares de estilo do seletor de nível de elemento**: Todos os estilos de elemento são usados no formulário HTML.
* **Prioridade de estilo**: A prioridade de estilo (como importante) é suportada e pode ser usada em um arquivo CSS personalizado.
* **Tipo de mídia**: Um ou mais pares de estilo do seletor podem ser vinculados no estilo @media para definir o tipo de mídia. O serviço Forms não verifica se o tipo de mídia especificado é compatível. O tipo de mídia especificado no arquivo CSS personalizado é unido no formulário HTML.

Você pode recuperar um arquivo CSS de amostra usando o aplicativo FormsIVS. Carregue o formulário, selecione-o na página Testar design de formulário e clique em Gerar CSS. Não é necessário definir o tipo de transformação HTML antes de clicar no botão. Em seguida, selecione salvar. Você pode editar esse arquivo CSS para atender aos requisitos de sua empresa.

>[!NOTE]
>
>Antes de renderizar um formulário HTML que use um arquivo CSS personalizado, é importante ter uma compreensão sólida da renderização de formulários HTML. (Consulte [Renderizar o Forms como HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário HTML que use um arquivo CSS, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API Java do Forms.
1. Faça referência ao arquivo CSS.
1. Renderize um formulário HTML.
1. Grave o fluxo de dados do formulário no navegador da Web cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API Java do Forms**

Antes de executar programaticamente uma operação suportada pelo serviço Forms, é necessário criar um objeto cliente Forms.

**Referência ao arquivo CSS**

Para renderizar um formulário HTML que use um arquivo CSS personalizado, certifique-se de fazer referência a um arquivo CSS existente.

**Renderizar um formulário de HTML**

Para renderizar um formulário HTML, você deve especificar um design de formulário criado no Designer e salvo como um arquivo XDP. Você também deve selecionar um tipo de transformação HTML. Por exemplo, você pode especificar o tipo HTML transformation que renderiza um HTML dinâmico para o Internet Explorer 5.0 ou posterior.

A renderização de um formulário HTML também requer valores, como valores URI necessários para renderizar outros tipos de formulário.

**Gravar o fluxo de dados do formulário no navegador da Web cliente**

Quando o serviço Forms renderiza um formulário HTML, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web cliente para tornar o formulário HTML visível para o usuário.

**Consulte também**

[Renderizar um formulário HTML que usa um arquivo CSS usando a API do Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderizar o Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Renderizar um formulário HTML que usa um arquivo CSS usando a API do Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Renderize um formulário HTML que use um arquivo CSS personalizado usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto da API Java do Forms

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `FormsServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Referência ao arquivo CSS

   * Crie um `HTMLRenderSpec` usando seu construtor.
   * Para renderizar o formulário HTML que usa um arquivo CSS personalizado, chame a função `HTMLRenderSpec` do objeto `setCustomCSSURI` e transmita um valor de string que especifica o local e o nome do arquivo CSS.

1. Renderizar um formulário de HTML

   Chame o `FormsServiceClient` do objeto `(Deprecated) (Deprecated) renderHTMLForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor enum que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com o HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` objeto que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um vazio `com.adobe.idp.Document` objeto.
   * O `HTMLRenderSpec` objeto que armazena opções de tempo de execução HTML.
   * Um valor de string que especifica a variável `HTTP_USER_AGENT` valor de cabeçalho, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` objeto que armazena valores de URI necessários para renderizar um formulário HTML.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O `(Deprecated) renderHTMLForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `com.adobe.idp.Document` chamando o `FormsResult` objeto &quot;s `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `com.adobe.idp.Document` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o `javax.servlet.h\ttp.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie um `java.io.InputStream` chamando o `com.adobe.idp.Document` do objeto `getInputStream` método .
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Renderização do HTML Forms usando arquivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Início rápido (modo SOAP): Renderização de um formulário HTML que usa um arquivo CSS usando a API do Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar um formulário HTML que usa um arquivo CSS usando a API do serviço da Web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Renderize um formulário HTML que use um arquivo CSS personalizado usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto da API Java do Forms

   Crie um `FormsService` e definir valores de autenticação.

1. Referência ao arquivo CSS

   * Crie um `HTMLRenderSpec` usando seu construtor.
   * Para renderizar o formulário HTML que usa um arquivo CSS personalizado, chame a função `HTMLRenderSpec` do objeto `setCustomCSSURI` e transmita um valor de string que especifica o local e o nome do arquivo CSS.

1. Renderizar um formulário de HTML

   Chame o `FormsService` do objeto `(Deprecated) renderHTMLForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor enum que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com o HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * A `BLOB` objeto que contém dados para mesclar com o formulário. Se você não deseja mesclar dados, use `null`. (Consulte [Pré-preenchimento do Forms com layouts flutuantes](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * O `HTMLRenderSpec` objeto que armazena opções de tempo de execução HTML.
   * Um valor de string que especifica a variável `HTTP_USER_AGENT` valor de cabeçalho, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Você pode passar uma string vazia se não quiser definir esse valor.
   * A `URLSpec` objeto que armazena valores de URI necessários para renderizar um formulário HTML.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pela variável `(Deprecated) renderHTMLForm` método . Esse valor de parâmetro armazena o formulário renderizado.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pela variável `(Deprecated) renderHTMLForm` método . Esse parâmetro armazena os dados XML de saída.
   * Um vazio `javax.xml.rpc.holders.LongHolder` que é preenchido pela variável `(Deprecated) renderHTMLForm` método . Esse argumento armazena o número de páginas no formulário.
   * Um vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pela variável `(Deprecated) renderHTMLForm` método . Esse argumento armazena o valor da localidade.
   * Um vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pela variável `(Deprecated) renderHTMLForm` método . Esse argumento armazena o valor de renderização de HTML usado.
   * Um vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O `(Deprecated) renderHTMLForm` O método preenche a variável `com.adobe.idp.services.holders.FormsResultHolder` objeto que é passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `FormResult` obtendo o valor da variável `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value` membro de dados.
   * Crie um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `BLOB` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `BLOB` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie uma matriz de bytes e preencha-a chamando a variável `BLOB` do objeto `getBinaryData` método . Essa tarefa atribui o conteúdo da `FormsResult` para a matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Renderização do HTML Forms usando arquivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
