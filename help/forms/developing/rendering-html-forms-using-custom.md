---
title: Renderização de HTML Forms usando arquivos CSS personalizados
seo-title: Renderização de HTML Forms usando arquivos CSS personalizados
description: 'null'
seo-description: nulo
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
translation-type: tm+mt
source-git-commit: fcbe1d860410e215cb7c438f94579e0b14d262a5
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 0%

---


# Renderização de HTML Forms usando arquivos CSS personalizados {#rendering-html-forms-using-custom-css-files}

O serviço Forms renderiza formulários HTML em resposta a uma solicitação HTTP de um navegador da Web. Ao renderizar um formulário HTML, o serviço Forms pode fazer referência a um arquivo CSS personalizado. Você pode criar um arquivo CSS personalizado para atender às suas necessidades comerciais e fazer referência a esse arquivo CSS ao usar o serviço Forms para renderizar formulários HTML.

O serviço Forms analisa silenciosamente o arquivo CSS personalizado. Ou seja, o serviço Forms não informa erros que podem ser encontrados se o arquivo CSS personalizado não estiver em conformidade com os padrões CSS. Nessa situação, o serviço Forms ignora o estilo e continua com os estilos restantes localizados no arquivo CSS.

A lista a seguir especifica estilos suportados em um arquivo CSS personalizado:

* **Pares** de estilo do seletor de nível de classe: Se estiverem presentes em um arquivo CSS personalizado, os seletores usados no formulário HTML como estilos de classe serão usados. Os estilos de classe não utilizados são ignorados.
* **Pares** de estilo seletor de nível de identificador: Todos os estilos de identificador serão usados se forem usados no formulário HTML.
* **Pares** de estilo seletor de nível de elemento: Todos os estilos de elemento serão usados se forem usados no formulário HTML.
* **Prioridade** do estilo: A prioridade de estilo (como importante) é suportada e pode ser usada em um arquivo CSS personalizado.
* **Tipo** de mídia: Um ou mais pares de estilo seletor podem ser vinculados no estilo @media para definir o tipo de mídia. O serviço Forms não verifica se o tipo de mídia especificado é suportado. O tipo de mídia especificado no arquivo CSS personalizado é mesclado no formulário HTML.

Você pode recuperar um arquivo CSS de amostra usando o aplicativo FormsIVS. Carregue o formulário, selecione-o na página Testar design de formulário e clique em Gerar CSS. Não é necessário definir o tipo de transformação HTML antes de clicar no botão. Em seguida, selecione salvar. Você pode editar esse arquivo CSS para atender às suas necessidades comerciais.

>[!NOTE]
>
>Antes de renderizar um formulário HTML que usa um arquivo CSS personalizado, é importante que você tenha uma compreensão sólida da renderização de formulários HTML. (Consulte [Renderizando o Forms como HTML](/help/forms/developing/rendering-forms-html.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário HTML que usa um arquivo CSS, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto Forms Java API.
1. Consulte o arquivo CSS.
1. Renderize um formulário HTML.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API Java Forms**

Antes de executar programaticamente uma operação suportada pelo serviço Forms, você deve criar um objeto cliente Forms.

**Referência ao arquivo CSS**

Para renderizar um formulário HTML que usa um arquivo CSS personalizado, certifique-se de fazer referência a um arquivo CSS existente.

**Renderizar um formulário HTML**

Para renderizar um formulário HTML, você deve especificar um design de formulário criado no Designer e salvo como um arquivo XDP. Você também deve selecionar um tipo de transformação HTML. Por exemplo, você pode especificar o tipo de transformação HTML que renderiza um HTML dinâmico para o Internet Explorer 5.0 ou posterior.

A renderização de um formulário HTML também requer valores, como valores URI necessários para renderizar outros tipos de formulário.

**Gravar o fluxo de dados do formulário no navegador da Web do cliente**

Quando o serviço Forms renderiza um formulário HTML, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente para tornar o formulário HTML visível para o usuário.

**Consulte também:**

[Renderizar um formulário HTML que usa um arquivo CSS usando a API Java](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API de serviço da Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderizando Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Criação de Aplicações web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Renderizar um formulário HTML que usa um arquivo CSS usando a API Java {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Renderize um formulário HTML que usa um arquivo CSS personalizado usando a API da Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto da API Java Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Referência ao arquivo CSS

   * Crie um objeto `HTMLRenderSpec` usando seu construtor.
   * Para renderizar o formulário HTML que usa um arquivo CSS personalizado, chame o método `HTMLRenderSpec` do objeto `setCustomCSSURI` e transmita um valor de string que especifica o local e o nome do arquivo CSS.

1. Renderizar um formulário HTML

   Chame o método `FormsServiceClient` do objeto `(Deprecated) (Deprecated) renderHTMLForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor de enumeração `TransformTo` que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um objeto `com.adobe.idp.Document` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe um objeto `com.adobe.idp.Document` vazio.
   * O objeto `HTMLRenderSpec` que armazena as opções de tempo de execução HTML.
   * Um valor de string que especifica o valor do cabeçalho `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Um objeto `URLSpec` que armazena valores de URI necessários para renderizar um formulário HTML.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `(Deprecated) renderHTMLForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o método `javax.servlet.h\ttp.HttpServletResponse` do objeto `getOutputStream`.
   * Crie um objeto `java.io.InputStream` invocando o método `com.adobe.idp.Document` do objeto `getInputStream`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário chamando o método `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Renderização de HTML Forms usando arquivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Start rápido (modo SOAP): Renderização de um formulário HTML que usa um arquivo CSS usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar um formulário HTML que usa um arquivo CSS usando a API de serviço da Web {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Renderize um formulário HTML que usa um arquivo CSS personalizado usando a API da Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no seu caminho de classe.

1. Criar um objeto da API Java Forms

   Crie um objeto `FormsService` e defina os valores de autenticação.

1. Referência ao arquivo CSS

   * Crie um objeto `HTMLRenderSpec` usando seu construtor.
   * Para renderizar o formulário HTML que usa um arquivo CSS personalizado, chame o método `HTMLRenderSpec` do objeto `setCustomCSSURI` e transmita um valor de string que especifica o local e o nome do arquivo CSS.

1. Renderizar um formulário HTML

   Chame o método `FormsService` do objeto `(Deprecated) renderHTMLForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor de enumeração `TransformTo` que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um objeto `BLOB` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe `null`. (Consulte [Pré-preencher o Forms com layouts flutuantes](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
   * O objeto `HTMLRenderSpec` que armazena as opções de tempo de execução HTML.
   * Um valor de string que especifica o valor do cabeçalho `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Você pode passar uma string vazia se não quiser definir esse valor.
   * Um objeto `URLSpec` que armazena valores de URI necessários para renderizar um formulário HTML.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método `(Deprecated) renderHTMLForm`. Esse valor de parâmetro armazena o formulário renderizado.
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método `(Deprecated) renderHTMLForm`. Esse parâmetro armazena os dados XML de saída.
   * Um objeto vazio `javax.xml.rpc.holders.LongHolder` que é preenchido pelo método `(Deprecated) renderHTMLForm`. Esse argumento armazena o número de páginas no formulário.
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método `(Deprecated) renderHTMLForm`. Este argumento armazena o valor de localidade.
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método `(Deprecated) renderHTMLForm`. Esse argumento armazena o valor de renderização HTML usado.
   * Um objeto vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O método `(Deprecated) renderHTMLForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` transmitido como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value`.
   * Crie um objeto `BLOB` que contenha dados de formulário chamando o método `FormsResult` do objeto `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie uma matriz de bytes e preencha-a chamando o método `BLOB` do objeto `getBinaryData`. Essa tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Renderização de HTML Forms usando arquivos CSS personalizados](#rendering-html-forms-using-custom-css-files)

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
