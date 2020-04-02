---
title: Como renderizar formulários HTML usando arquivos CSS personalizados
seo-title: Como renderizar formulários HTML usando arquivos CSS personalizados
description: 'null'
seo-description: 'null'
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
translation-type: tm+mt
source-git-commit: fcbe1d860410e215cb7c438f94579e0b14d262a5

---


# Como renderizar formulários HTML usando arquivos CSS personalizados {#rendering-html-forms-using-custom-css-files}

O serviço Forms renderiza formulários HTML em resposta a uma solicitação HTTP de um navegador da Web. Ao renderizar um formulário HTML, o serviço Forms pode fazer referência a um arquivo CSS personalizado. Você pode criar um arquivo CSS personalizado para atender aos requisitos de negócios e fazer referência a esse arquivo CSS ao usar o serviço Forms para renderizar formulários HTML.

O serviço Forms analisa silenciosamente o arquivo CSS personalizado. Ou seja, o serviço Forms não relata erros que podem ser encontrados se o arquivo CSS personalizado não estiver em conformidade com os padrões CSS. Nessa situação, o serviço Forms ignora o estilo e continua com os estilos restantes localizados no arquivo CSS.

A lista a seguir especifica estilos suportados em um arquivo CSS personalizado:

* **Pares** de estilo do seletor de nível de classe: Se estiverem presentes em um arquivo CSS personalizado, os seletores usados no formulário HTML como estilos de classe serão usados. Os estilos de classe não utilizados são ignorados.
* **Pares** de estilo seletor de nível de identificador: Todos os estilos de identificador serão usados se forem usados no formulário HTML.
* **Pares** de estilo seletor de nível de elemento: Todos os estilos de elemento serão usados se forem usados no formulário HTML.
* **Prioridade** do estilo: A prioridade de estilo (como importante) é suportada e pode ser usada em um arquivo CSS personalizado.
* **Tipo** de mídia: Um ou mais pares de estilo seletor podem ser vinculados no estilo @media para definir o tipo de mídia. O serviço Forms não verifica se o tipo de mídia especificado é suportado. O tipo de mídia especificado no arquivo CSS personalizado é mesclado no formulário HTML.

Você pode recuperar um arquivo CSS de amostra usando o aplicativo FormsIVS. Carregue o formulário, selecione-o na página Testar design de formulário e clique em Gerar CSS. Não é necessário definir o tipo de transformação HTML antes de clicar no botão. Em seguida, selecione salvar. Você pode editar esse arquivo CSS para atender às suas necessidades comerciais.

>[!NOTE]
>
>Antes de renderizar um formulário HTML que usa um arquivo CSS personalizado, é importante que você tenha uma compreensão sólida da renderização de formulários HTML. (Consulte [Renderizar formulários como HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Formulários, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário HTML que usa um arquivo CSS, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API Java do Forms.
1. Consulte o arquivo CSS.
1. Renderize um formulário HTML.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API Java do Forms**

Antes de executar programaticamente uma operação suportada pelo serviço Forms, é necessário criar um objeto cliente Forms.

**Referência ao arquivo CSS**

Para renderizar um formulário HTML que usa um arquivo CSS personalizado, certifique-se de fazer referência a um arquivo CSS existente.

**Renderizar um formulário HTML**

Para renderizar um formulário HTML, você deve especificar um design de formulário criado no Designer e salvo como um arquivo XDP. Você também deve selecionar um tipo de transformação HTML. Por exemplo, você pode especificar o tipo de transformação HTML que renderiza um HTML dinâmico para o Internet Explorer 5.0 ou posterior.

A renderização de um formulário HTML também requer valores, como valores URI necessários para renderizar outros tipos de formulário.

**Gravar o fluxo de dados do formulário no navegador da Web do cliente**

Quando o serviço Forms renderiza um formulário HTML, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente para tornar o formulário HTML visível para o usuário.

**Consulte também:**

[Renderizar um formulário HTML que usa um arquivo CSS usando a API Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Como renderizar formulários PDF interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderizar formulários como HTML](/help/forms/developing/rendering-forms-html.md)

[Criação de Aplicações web que renderizam formulários](/help/forms/developing/creating-web-applications-renders-forms.md)

## Renderizar um formulário HTML que usa um arquivo CSS usando a API Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Renderize um formulário HTML que use um arquivo CSS personalizado usando a API de formulários (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto da API Java do Forms

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `FormsServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Referência ao arquivo CSS

   * Crie um `HTMLRenderSpec` objeto usando seu construtor.
   * Para renderizar o formulário HTML que usa um arquivo CSS personalizado, chame o método do `HTMLRenderSpec` `setCustomCSSURI` objeto e transmita um valor de string que especifica o local e o nome do arquivo CSS.

1. Renderizar um formulário HTML

   Chame o método do `FormsServiceClient` objeto `(Deprecated) (Deprecated) renderHTMLForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor `TransformTo` enum que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um `com.adobe.idp.Document` objeto que contém dados para mesclar com o formulário. Se você não quiser unir dados, passe um `com.adobe.idp.Document` objeto vazio.
   * O `HTMLRenderSpec` objeto que armazena as opções de tempo de execução HTML.
   * Um valor de string que especifica o valor do `HTTP_USER_AGENT` cabeçalho, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Um `URLSpec` objeto que armazena valores de URI necessários para renderizar um formulário HTML.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   O `(Deprecated) renderHTMLForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um `com.adobe.idp.Document` objeto chamando o `FormsResult` método do objeto `getOutputContent` .
   * Obtenha o tipo de conteúdo do `com.adobe.idp.Document` objeto chamando seu `getContentType` método.
   * Defina o tipo de conteúdo do `javax.servlet.http.HttpServletResponse` objeto chamando seu `setContentType` método e transmitindo o tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o `javax.servlet.h\ttp.HttpServletResponse` `getOutputStream` método do objeto.
   * Crie um `java.io.InputStream` objeto chamando o `com.adobe.idp.Document` método do `getInputStream` objeto.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, invocando o método do `InputStream` objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o método do `javax.servlet.ServletOutputStream` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também:**

[Como renderizar formulários HTML usando arquivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Start rápido (modo SOAP): Renderização de um formulário HTML que usa um arquivo CSS usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar um formulário HTML que usa um arquivo CSS usando a API de serviço da Web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Renderize um formulário HTML que use um arquivo CSS personalizado usando a API de formulários (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no seu caminho de classe.

1. Criar um objeto da API Java do Forms

   Crie um `FormsService` objeto e defina valores de autenticação.

1. Referência ao arquivo CSS

   * Crie um `HTMLRenderSpec` objeto usando seu construtor.
   * Para renderizar o formulário HTML que usa um arquivo CSS personalizado, chame o método do `HTMLRenderSpec` `setCustomCSSURI` objeto e transmita um valor de string que especifica o local e o nome do arquivo CSS.

1. Renderizar um formulário HTML

   Chame o método do `FormsService` objeto `(Deprecated) renderHTMLForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo do Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor `TransformTo` enum que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um `BLOB` objeto que contém dados para mesclar com o formulário. Se você não deseja unir dados, passe `null`. (Consulte [Pré-preenchimento de formulários com layouts](/help/forms/developing/prepopulating-forms-flowable-layouts.md)flutuantes.)
   * O `HTMLRenderSpec` objeto que armazena as opções de tempo de execução HTML.
   * Um valor de string que especifica o valor do `HTTP_USER_AGENT` cabeçalho, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Você pode passar uma string vazia se não quiser definir esse valor.
   * Um `URLSpec` objeto que armazena valores de URI necessários para renderizar um formulário HTML.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   * Um `com.adobe.idp.services.holders.BLOBHolder` objeto vazio que é preenchido pelo `(Deprecated) renderHTMLForm` método. Esse valor de parâmetro armazena o formulário renderizado.
   * Um `com.adobe.idp.services.holders.BLOBHolder` objeto vazio que é preenchido pelo `(Deprecated) renderHTMLForm` método. Esse parâmetro armazena os dados XML de saída.
   * Um `javax.xml.rpc.holders.LongHolder` objeto vazio que é preenchido pelo `(Deprecated) renderHTMLForm` método. Esse argumento armazena o número de páginas no formulário.
   * Um `javax.xml.rpc.holders.StringHolder` objeto vazio que é preenchido pelo `(Deprecated) renderHTMLForm` método. Este argumento armazena o valor de localidade.
   * Um `javax.xml.rpc.holders.StringHolder` objeto vazio que é preenchido pelo `(Deprecated) renderHTMLForm` método. Esse argumento armazena o valor de renderização HTML usado.
   * Um `com.adobe.idp.services.holders.FormsResultHolder` objeto vazio que conterá os resultados dessa operação.
   O `(Deprecated) renderHTMLForm` método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um `FormResult` objeto obtendo o valor do membro de `com.adobe.idp.services.holders.FormsResultHolder` dados do `value` objeto.
   * Crie um `BLOB` objeto que contenha dados de formulário chamando o `FormsResult` método do `getOutputContent` objeto.
   * Obtenha o tipo de conteúdo do `BLOB` objeto chamando seu `getContentType` método.
   * Defina o tipo de conteúdo do `javax.servlet.http.HttpServletResponse` objeto chamando seu `setContentType` método e transmitindo o tipo de conteúdo do `BLOB` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o `javax.servlet.http.HttpServletResponse` `getOutputStream` método do objeto.
   * Crie uma matriz de bytes e preencha-a chamando o método do `BLOB` objeto `getBinaryData` . Essa tarefa atribui o conteúdo do `FormsResult` objeto à matriz de bytes.
   * Chame o método do `javax.servlet.http.HttpServletResponse` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também:**

[Como renderizar formulários HTML usando arquivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
