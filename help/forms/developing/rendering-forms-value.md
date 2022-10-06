---
title: Renderizar Forms por valor
seo-title: Rendering Forms By Value
description: Use a API do Forms (Java) para renderizar um formulário por valor usando a API do Java e a API do serviço da Web.
seo-description: Use the Forms API (Java) to render a form by value using the Java API and Web Service API.
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '1835'
ht-degree: 0%

---

# Renderizar Forms por valor {#rendering-forms-by-value}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

Normalmente, um design de formulário criado no Designer é passado por referência ao serviço da Forms. Os designs de formulário podem ser grandes e, como resultado, é mais eficiente passá-los por referência para evitar a necessidade de marcar os bytes de design de formulário por valor. O serviço Forms também pode armazenar em cache o design de formulário para que, quando armazenado em cache, ele não precise ler continuamente o design de formulário.

Se um design de formulário contiver um atributo UUID, ele será armazenado em cache. O valor UUID é exclusivo para todos os designs de formulário e é usado para identificar um formulário de maneira exclusiva. Ao renderizar um formulário por valor, o formulário só deve ser armazenado em cache quando for usado repetidamente. No entanto, se o formulário não for usado repetidamente e tiver que ser exclusivo, é possível evitar o armazenamento do formulário em cache usando opções de armazenamento em cache definidas usando a API do AEM Forms.

O serviço Forms também pode resolver o local do conteúdo vinculado no design de formulário. Por exemplo, imagens vinculadas que são referenciadas no design de formulário são URLs relativos. O conteúdo vinculado é sempre considerado relativo ao local do design de formulário. Portanto, a resolução do conteúdo vinculado é uma questão de determinar sua localização ao aplicar o caminho relativo ao local absoluto do design de formulário.

Em vez de passar um design de formulário por referência, você pode passar um design de formulário por valor. O envio de um design de formulário por valor é eficiente quando um design de formulário é criado dinamicamente; ou seja, quando um aplicativo cliente gera o XML que cria um design de formulário durante o tempo de execução. Nessa situação, um design de formulário não é armazenado em um repositório físico porque é armazenado na memória. Ao criar dinamicamente um design de formulário em tempo de execução e passá-lo por valor, é possível armazenar o formulário em cache e melhorar o desempenho do serviço Forms.

**Limitações do envio de um formulário por valor**

As seguintes limitações se aplicam quando um design de formulário é passado pelo valor:

* Nenhum conteúdo vinculado relativo pode estar no design de formulário. Todas as imagens e fragmentos devem ser incorporados no design de formulário ou absolutamente referenciados.
* Os cálculos do lado do servidor não podem ser executados após a renderização do formulário. Se o formulário for enviado de volta ao serviço da Forms, os dados serão extraídos e retornados sem nenhum cálculo do lado do servidor.
* Como o HTML só pode usar imagens vinculadas em tempo de execução, não é possível gerar HTML com imagens incorporadas. Isso ocorre porque o serviço Forms suporta imagens incorporadas com HTML recuperando as imagens de um design de formulário referenciado. Como um design de formulário passado pelo valor não tem um local referenciado, as imagens incorporadas não podem ser extraídas quando a página HTML é exibida. Portanto, as referências de imagem devem ser caminhos absolutos para serem renderizados no HTML.

>[!NOTE]
>
>Embora seja possível renderizar diferentes tipos de formulários por valor (por exemplo, formulários HTML ou formulários que contenham direitos de uso), esta seção discute a renderização de PDF forms interativos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário por valor, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Consulte o design de formulário.
1. Renderizar um formulário por valor.
1. Grave o fluxo de dados do formulário no navegador da Web cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente do Forms**

Antes de poder importar dados de forma programática para uma API do cliente do PDF, é necessário criar um cliente do serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço.

**Referência ao design de formulário**

Ao renderizar um formulário por valor, é necessário criar um `com.adobe.idp.Document` objeto que contém o design de formulário a ser renderizado. Você pode fazer referência a um arquivo XDP existente ou pode criar dinamicamente um design de formulário em tempo de execução e preencher um `com.adobe.idp.Document` com esses dados.

>[!NOTE]
>
>Esta seção e o início rápido correspondente fazem referência a um arquivo XDP existente.

**Renderizar um formulário por valor**

Para renderizar um formulário por valor, passe um `com.adobe.idp.Document` instância que contém o design de formulário para o método de renderização `inDataDoc` (pode ser qualquer um dos `FormsServiceClient` métodos de renderização do objeto, como `renderPDFForm`, `(Deprecated) renderHTMLForm`e assim por diante). Normalmente, esse valor de parâmetro é reservado para dados unidos ao formulário. Da mesma forma, passe um valor de string vazia para a variável `formQuery` parâmetro. Normalmente, esse parâmetro requer um valor de string que especifica o nome do design de formulário.

>[!NOTE]
>
>Para exibir dados no formulário, os dados devem ser especificados na variável `xfa:datasets` elemento. Para obter informações sobre a arquitetura XFA, acesse [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

**Gravar o fluxo de dados do formulário no navegador da Web cliente**

Quando o serviço Forms renderiza um formulário por valor, ele retorna um fluxo de dados de formulário que deve ser gravado no navegador da Web cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.

**Consulte também**

[Renderizar um formulário por valor usando a API Java](#render-a-form-by-value-using-the-java-api)

[Renderizar um formulário por valor usando a API do serviço da Web](#render-a-form-by-value-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Enviar documentos para o serviço do Forms](/help/forms/developing/passing-documents-forms-service.md)

[Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Renderizar um formulário por valor usando a API Java {#render-a-form-by-value-using-the-java-api}

Renderize um formulário por valor usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente do Forms

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `FormsServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Referência ao design de formulário

   * Crie um `java.io.FileInputStream` objeto que representa o design de formulário a ser renderizado usando seu construtor e passando um valor de string que especifica o local do arquivo XDP.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Renderizar um formulário por valor

   Chame o `FormsServiceClient` do objeto `renderPDFForm` e transmita os seguintes valores:

   * Um valor de string vazio. (Normalmente, esse parâmetro requer um valor de string que especifica o nome do design de formulário.)
   * A `com.adobe.idp.Document` objeto que contém o design de formulário. Normalmente, esse valor de parâmetro é reservado para dados que são unidos ao formulário.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se você não quiser especificar opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que pode ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `com.adobe.idp.Document` chamando o `FormsResult` objeto &quot;s `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `com.adobe.idp.Document` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie um `java.io.InputStream` chamando o `com.adobe.idp.Document` do objeto `getInputStream` método .
   * Crie uma matriz de bytes e aloque o tamanho da variável `InputStream` objeto. Chame o `InputStream` do objeto `available` para obter o tamanho da variável `InputStream` objeto.
   * Preencha a matriz de bytes com o fluxo de dados do formulário chamando a variável `InputStream` do objeto `read`e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Renderizar Forms por valor](/help/forms/developing/rendering-forms.md)

[Início rápido (modo SOAP): Renderização por valor usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar um formulário por valor usando a API do serviço da Web {#render-a-form-by-value-using-the-web-service-api}

Renderize um formulário por valor usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do cliente do Forms

   Crie um `FormsService` e definir valores de autenticação.

1. Referência ao design de formulário

   * Crie um `java.io.FileInputStream` usando seu construtor. Passe um valor de string que especifica o local do arquivo XDP.
   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar um documento PDF criptografado com uma senha.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `java.io.FileInputStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `java.io.FileInputStream` tamanho do objeto usando sua `available` método .
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `java.io.FileInputStream` do objeto `read` e transmitindo a matriz de bytes.
   * Preencha o `BLOB` ao invocar seu `setBinaryData` e transmitindo a matriz de bytes.

1. Renderizar um formulário por valor

   Chame o `FormsService` do objeto `renderPDFForm` e transmita os seguintes valores:

   * Um valor de string vazio. (Normalmente, esse parâmetro requer um valor de string que especifica o nome do design de formulário.)
   * A `BLOB` objeto que contém o design de formulário. Normalmente, esse valor de parâmetro é reservado para dados que são unidos ao formulário.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se você não quiser especificar opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto preenchido pelo método . Isso é usado para armazenar o formulário PDF renderizado.
   * Um vazio `javax.xml.rpc.holders.LongHolder` objeto preenchido pelo método . (Esse argumento armazena o número de páginas no formulário.)
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método . (Esse argumento armazena o valor da localidade.)
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

[Renderizar Forms por valor](#rendering-forms-by-value)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
