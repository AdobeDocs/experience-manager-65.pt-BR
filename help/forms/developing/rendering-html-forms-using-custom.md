---
title: Renderização do HTML Forms usando arquivos CSS personalizados
description: Use o serviço Forms para consultar arquivos CSS personalizados e renderizar formulários HTML em resposta a uma solicitação HTTP de um navegador da Web. Você pode renderizar um formulário HTML que usa um arquivo CSS usando a API Java e a API do serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 5fa385a7-f030-4c0c-8938-0991d02ef361
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 0%

---

# Renderização do HTML Forms usando arquivos CSS personalizados {#rendering-html-forms-using-custom-css-files}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

O serviço Forms renderiza formulários HTML em resposta a uma solicitação HTTP de um navegador da Web. Ao renderizar um formulário HTML, o serviço Forms pode fazer referência a um arquivo CSS personalizado. Você pode criar um arquivo CSS personalizado para atender aos requisitos da empresa e fazer referência a esse arquivo CSS ao usar o serviço Forms para renderizar formulários HTML.

O serviço Forms analisa silenciosamente o arquivo CSS personalizado. Ou seja, o serviço Forms não relata erros que podem ser encontrados se o arquivo CSS personalizado não estiver em conformidade com os padrões CSS. Nessa situação, o serviço Forms ignora o estilo e continua com os estilos restantes no arquivo CSS.

A lista a seguir especifica estilos compatíveis com um arquivo CSS personalizado:

* **Pares de estilo do seletor de nível de classe**: Se presente em um arquivo CSS personalizado, os seletores usados no formulário HTML como estilos de classe são usados. Estilos de classe não utilizados são ignorados.
* **Pares de estilo do seletor de nível do identificador**: Todos os estilos de identificador são usados se forem usados no formato HTML.
* **Pares de estilo do seletor de nível de elemento**: Todos os estilos de elemento são usados se forem usados no formato HTML.
* **Prioridade do estilo**: a prioridade do estilo (como importante) é compatível e pode ser usada em um arquivo CSS personalizado.
* **Tipo de mídia**: um ou mais pares de estilos do seletor podem ser encapsulados no estilo @media para definir o tipo de mídia. O serviço Forms não verifica se o tipo de mídia especificado é compatível. O tipo de mídia especificado no arquivo CSS personalizado é mesclado no formulário HTML.

Você pode recuperar um arquivo CSS de amostra usando o aplicativo FormsIVS. Carregue o formulário, selecione-o na página Testar design de formulário e clique em Gerar CSS. Não é necessário definir o tipo de transformação de HTML antes de clicar no botão. Em seguida, selecione salvar. Você pode editar esse arquivo CSS para atender aos requisitos da sua empresa.

>[!NOTE]
>
>Antes de renderizar um formulário HTML que use um arquivo CSS personalizado, é importante ter uma sólida compreensão dos formulários HTML de renderização. (Consulte [Renderização do Forms como HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário HTML que use um arquivo CSS, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API Java do Forms.
1. Faça referência ao arquivo CSS.
1. Renderize um formulário HTML.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API Java do Forms**

Antes de executar programaticamente uma operação compatível com o serviço Forms, você deve criar um objeto cliente Forms.

**Referência ao arquivo CSS**

Para renderizar um formulário HTML que use um arquivo CSS personalizado, certifique-se de fazer referência a um arquivo CSS existente.

**Renderizar um formulário HTML**

Para renderizar um formulário HTML, especifique um design de formulário que foi criado no Designer e salvo como um arquivo XDP. Selecione um tipo de transformação HTML. Por exemplo, você pode especificar o tipo de transformação de HTML que renderiza um HTML dinâmico para o Internet Explorer 5.0 ou posterior.

A renderização de um formulário HTML também requer valores, como valores de URI necessários para renderizar outros tipos de formulário.

**Gravar o fluxo de dados do formulário no navegador Web cliente**

Quando o serviço Forms renderiza um formulário HTML, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente para tornar o formulário HTML visível para o usuário.

**Consulte também**

[Renderize um formulário HTML que use um arquivo CSS usando a API Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderização do Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Criação de aplicações Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Renderize um formulário HTML que use um arquivo CSS usando a API Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Renderize um formulário HTML que use um arquivo CSS personalizado usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto de API Java do Forms

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `FormsServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Referência ao arquivo CSS

   * Criar um `HTMLRenderSpec` usando seu construtor.
   * Para renderizar o formulário HTML que usa um arquivo CSS personalizado, chame o `HTMLRenderSpec` do objeto `setCustomCSSURI` e transmitem um valor de string que especifica a localização e o nome do arquivo CSS.

1. Renderizar um formulário HTML

   Chame o `FormsServiceClient` do objeto `(Deprecated) (Deprecated) renderHTMLForm` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor de enumeração que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário de HTML que seja compatível com o HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` objeto que contém dados a serem mesclados com o formulário. Se não quiser mesclar dados, passe uma tag vazia `com.adobe.idp.Document` objeto.
   * A variável `HTMLRenderSpec` objeto que armazena opções de tempo de execução de HTML.
   * Um valor de string que especifica a `HTTP_USER_AGENT` valor do cabeçalho, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` objeto que armazena valores de URI necessários para renderizar um formulário HTML.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Este é um parâmetro opcional, e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   A variável `(Deprecated) renderHTMLForm` o método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Criar um `com.adobe.idp.Document` ao invocar o `FormsResult` do objeto `getOutputContent` método.
   * Obter o tipo de conteúdo do `com.adobe.idp.Document` ao invocar seu `getContentType` método.
   * Defina o `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto chamando seu `setContentType` e transmitindo o tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Criar um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados de formulário no navegador da web cliente, chamando o `javax.servlet.h\ttp.HttpServletResponse` do objeto `getOutputStream` método.
   * Criar um `java.io.InputStream` ao invocar o `com.adobe.idp.Document` do objeto `getInputStream` método.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados de formulário chamando o `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

**Consulte também**

[Renderização do HTML Forms usando arquivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Início rápido (modo SOAP): renderização de um formulário HTML que usa um arquivo CSS usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderize um formulário HTML que use um arquivo CSS usando a API do serviço Web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Renderize um formulário HTML que use um arquivo CSS personalizado usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms.
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar um objeto de API Java do Forms

   Criar um `FormsService` objeto e definir valores de autenticação.

1. Referência ao arquivo CSS

   * Criar um `HTMLRenderSpec` usando seu construtor.
   * Para renderizar o formulário HTML que usa um arquivo CSS personalizado, chame o `HTMLRenderSpec` do objeto `setCustomCSSURI` e transmitem um valor de string que especifica a localização e o nome do arquivo CSS.

1. Renderizar um formulário HTML

   Chame o `FormsService` do objeto `(Deprecated) renderHTMLForm` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do Forms, certifique-se de especificar o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor de enumeração que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário de HTML que seja compatível com o HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * A `BLOB` objeto que contém dados a serem mesclados com o formulário. Se não quiser mesclar dados, transmita `null`. (Consulte [Pré-preenchimento do Forms com layouts fluíveis](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * A variável `HTMLRenderSpec` objeto que armazena opções de tempo de execução de HTML.
   * Um valor de string que especifica a `HTTP_USER_AGENT` valor do cabeçalho, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Você pode passar uma string vazia se não quiser definir esse valor.
   * A `URLSpec` objeto que armazena valores de URI necessários para renderizar um formulário HTML.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Este é um parâmetro opcional, e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto que é preenchido pelo `(Deprecated) renderHTMLForm` método. Esse valor de parâmetro armazena o formulário renderizado.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto que é preenchido pelo `(Deprecated) renderHTMLForm` método. Esse parâmetro armazena os dados XML de saída.
   * Um vazio `javax.xml.rpc.holders.LongHolder` objeto que é preenchido pelo `(Deprecated) renderHTMLForm` método. Esse argumento armazena o número de páginas no formulário.
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto que é preenchido pelo `(Deprecated) renderHTMLForm` método. Esse argumento armazena o valor do local.
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto que é preenchido pelo `(Deprecated) renderHTMLForm` método. Esse argumento armazena o valor de renderização do HTML usado.
   * Um vazio `com.adobe.idp.services.holders.FormsResultHolder` objeto que conterá os resultados desta operação.

   A variável `(Deprecated) renderHTMLForm` O método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Criar um `FormResult` obtendo o valor do `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value` membro de dados.
   * Criar um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método.
   * Obter o tipo de conteúdo do `BLOB` ao invocar seu `getContentType` método.
   * Defina o `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto chamando seu `setContentType` e transmitindo o tipo de conteúdo do `BLOB` objeto.
   * Criar um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados de formulário no navegador da web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método.
   * Crie uma matriz de bytes e preencha-a chamando o `BLOB` do objeto `getBinaryData` método. Esta tarefa atribui o conteúdo do `FormsResult` à matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

**Consulte também**

[Renderização do HTML Forms usando arquivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
