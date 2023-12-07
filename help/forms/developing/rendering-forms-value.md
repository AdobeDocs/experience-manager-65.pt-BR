---
title: Renderização do Forms por valor
description: Use a API do Forms (Java) para renderizar um formulário por valor usando a API do Java e a API do serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---

# Renderização do Forms por valor {#rendering-forms-by-value}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

Normalmente, um design de formulário criado no Designer é transmitido por referência ao serviço Forms. Os designs de formulário podem ser grandes e, como resultado, é mais eficiente passá-los por referência para evitar a necessidade de empacotar bytes de design de formulário por valor. O serviço Forms também pode armazenar o design do formulário em cache para que, quando armazenado em cache, ele não precise ler o design do formulário continuamente.

Se um design de formulário contiver um atributo UUID, ele será armazenado em cache. O valor UUID é exclusivo para todos os designs de formulário e é usado para identificar exclusivamente um formulário. Ao renderizar um formulário por valor, o formulário só deve ser armazenado em cache quando usado repetidamente. No entanto, se o formulário não for usado repetidamente e precisar ser exclusivo, é possível evitar o armazenamento em cache usando as opções de armazenamento em cache definidas com a API do AEM Forms.

O serviço Forms também pode resolver o local do conteúdo vinculado no design do formulário. Por exemplo, imagens vinculadas referenciadas no design do formulário são URLs relativas. O conteúdo vinculado é sempre considerado como relativo ao local de design do formulário. Portanto, resolver o conteúdo vinculado é uma questão de determinar sua localização aplicando o caminho relativo ao local absoluto do design do formulário.

Em vez de passar um design de formulário por referência, você pode passar um design de formulário por valor. Transmitir um design de formulário por valor é eficiente quando um design de formulário é criado dinamicamente; ou seja, quando um aplicativo cliente gera o XML que cria um design de formulário durante o tempo de execução. Nessa situação, um design de formulário não é armazenado em um repositório físico porque ele é armazenado na memória. Ao criar dinamicamente um design de formulário em tempo de execução e passá-lo por valor, você pode armazenar o formulário em cache e melhorar o desempenho do serviço do Forms.

**Limitações da transmissão de um formulário por valor**

As seguintes limitações se aplicam quando um design de formulário é passado pelo valor:

* Nenhum conteúdo vinculado relativo pode estar dentro do design do formulário. Todas as imagens e fragmentos devem ser incorporados no design do formulário ou referenciados de forma absoluta.
* Os cálculos do lado do servidor não podem ser executados após o formulário ser renderizado. Se o formulário for enviado de volta para o serviço Forms, os dados serão extraídos e retornados sem nenhum cálculo do lado do servidor.
* Como o HTML só pode usar imagens vinculadas em tempo de execução, não é possível gerar o HTML com imagens incorporadas. Isso ocorre porque o serviço Forms oferece suporte a imagens incorporadas com HTML ao recuperar as imagens de um design de formulário referenciado. Como um design de formulário transmitido por valor não tem um local de referência, as imagens incorporadas não podem ser extraídas quando a página de HTML é exibida. Portanto, as referências de imagem devem ser caminhos absolutos para serem renderizados em HTML.

>[!NOTE]
>
>Embora seja possível renderizar diferentes tipos de formulários por valor (por exemplo, formulários HTML ou formulários que contêm direitos de uso), esta seção discute a renderização de PDF forms interativos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário por valor, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Faça referência ao design do formulário.
1. Renderiza um formulário por valor.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente do Forms**

Antes de importar dados programaticamente para uma API do cliente do formulário PDF, você deve criar um cliente do serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço.

**Referência ao design do formulário**

Ao renderizar um formulário por valor, é necessário criar um `com.adobe.idp.Document` objeto que contém o design de formulário a ser renderizado. Você pode fazer referência a um arquivo XDP existente ou criar dinamicamente um design de formulário em tempo de execução e preencher um `com.adobe.idp.Document` dados.

>[!NOTE]
>
>Esta seção e o início rápido correspondente fazem referência a um arquivo XDP existente.

**Renderizar um formulário por valor**

Para renderizar um formulário por valor, passe um `com.adobe.idp.Document` instância que contém o design do formulário para o método de renderização `inDataDoc` (pode ser qualquer um dos `FormsServiceClient` métodos de renderização do objeto, como `renderPDFForm`, `(Deprecated) renderHTMLForm`e assim por diante). Normalmente, esse valor de parâmetro é reservado para dados mesclados com o formulário. Da mesma forma, passe um valor de string vazio para o `formQuery` parâmetro. Normalmente, esse parâmetro requer um valor de sequência de caracteres que especifica o nome do design do formulário.

>[!NOTE]
>
>Para exibir dados no formulário, os dados devem ser especificados na variável `xfa:datasets` elemento. Para obter informações sobre a arquitetura XFA, acesse [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

**Gravar o fluxo de dados do formulário no navegador Web cliente**

Quando o serviço Forms renderiza um formulário por valor, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.

**Consulte também**

[Renderizar um formulário por valor usando a API Java](#render-a-form-by-value-using-the-java-api)

[Renderizar um formulário por valor usando a API do serviço Web](#render-a-form-by-value-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Passar documentos para o serviço da Forms](/help/forms/developing/passing-documents-forms-service.md)

[Criação de aplicações Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Renderizar um formulário por valor usando a API Java {#render-a-form-by-value-using-the-java-api}

Renderize um formulário por valor usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto da API do cliente do Forms

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `FormsServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Referência ao design do formulário

   * Criar um `java.io.FileInputStream` objeto que representa o design do formulário a ser renderizado usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XDP.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Renderizar um formulário por valor

   Chame o `FormsServiceClient` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string vazio. (Normalmente, esse parâmetro requer um valor de sequência de caracteres que especifica o nome do design do formulário.)
   * A `com.adobe.idp.Document` objeto que contém o design do formulário. Normalmente, esse valor de parâmetro é reservado para dados que são mesclados com o formulário.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço do Forms.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   A variável `renderPDFForm` o método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que pode ser gravado no navegador da web do cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Criar um `com.adobe.idp.Document` ao invocar o `FormsResult` do objeto `getOutputContent` método.
   * Obter o tipo de conteúdo do `com.adobe.idp.Document` ao invocar seu `getContentType` método.
   * Defina o `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto chamando seu `setContentType` e transmitindo o tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Criar um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados de formulário no navegador da web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método.
   * Criar um `java.io.InputStream` ao invocar o `com.adobe.idp.Document` do objeto `getInputStream` método.
   * Crie uma matriz de bytes e aloque o tamanho da variável `InputStream` objeto. Chame o `InputStream` do objeto `available` para obter o tamanho do `InputStream` objeto.
   * Preencha a matriz de bytes com o fluxo de dados de formulário chamando o `InputStream` do objeto `read`e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

**Consulte também**

[Renderização do Forms por valor](/help/forms/developing/rendering-forms.md)

[Início rápido (modo SOAP): renderização por valor usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar um formulário por valor usando a API do serviço Web {#render-a-form-by-value-using-the-web-service-api}

Renderize um formulário por valor usando a API do Forms (serviço Web):

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms.
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar um objeto da API do cliente do Forms

   Criar um `FormsService` objeto e definir valores de autenticação.

1. Referência ao design do formulário

   * Criar um `java.io.FileInputStream` usando seu construtor. Transmita um valor de string que especifique o local do arquivo XDP.
   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar um documento PDF que é criptografado com uma senha.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `java.io.FileInputStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `java.io.FileInputStream` tamanho do objeto usando seu `available` método.
   * Preencha a matriz de bytes com dados de fluxo invocando o `java.io.FileInputStream` do objeto `read` e transmitindo a matriz de bytes.
   * Preencha o `BLOB` ao invocar seu `setBinaryData` e transmitindo a matriz de bytes.

1. Renderizar um formulário por valor

   Chame o `FormsService` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string vazio. (Normalmente, esse parâmetro requer um valor de sequência de caracteres que especifica o nome do design do formulário.)
   * A `BLOB` objeto que contém o design do formulário. Normalmente, esse valor de parâmetro é reservado para dados que são mesclados com o formulário.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço do Forms.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto preenchido pelo método. Isso é usado para armazenar o formulário de PDF renderizado.
   * Um vazio `javax.xml.rpc.holders.LongHolder` objeto preenchido pelo método. (Esse argumento armazena o número de páginas no formulário.)
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método. (Esse argumento armazena o valor do local.)
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

[Renderização do Forms por valor](#rendering-forms-by-value)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
