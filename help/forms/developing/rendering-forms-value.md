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
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---

# Renderização do Forms por valor {#rendering-forms-by-value}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

Normalmente, um design de formulário criado no Designer é transmitido por referência ao serviço do Forms. Os designs de formulário podem ser grandes e, como resultado, é mais eficiente passá-los por referência para evitar a necessidade de empacotar bytes de design de formulário por valor. O serviço Forms também pode armazenar o design do formulário em cache para que, quando armazenado em cache, ele não precise ler o design do formulário continuamente.

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
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

**Referenciar o design do formulário**

Ao renderizar um formulário por valor, é necessário criar um objeto `com.adobe.idp.Document` que contenha o design do formulário a ser renderizado. Você pode referenciar um arquivo XDP existente ou criar dinamicamente um design de formulário em tempo de execução e preencher um `com.adobe.idp.Document` com esses dados.

>[!NOTE]
>
>Esta seção e o início rápido correspondente fazem referência a um arquivo XDP existente.

**Renderizar um formulário pelo valor**

Para renderizar um formulário por valor, passe uma instância `com.adobe.idp.Document` que contenha o design do formulário para o parâmetro `inDataDoc` do método de renderização (pode ser qualquer um dos métodos de renderização do objeto `FormsServiceClient`, como `renderPDFForm`, `(Deprecated) renderHTMLForm` e assim por diante). Normalmente, esse valor de parâmetro é reservado para dados mesclados com o formulário. Da mesma forma, passe um valor de cadeia de caracteres vazio para o parâmetro `formQuery`. Normalmente, esse parâmetro requer um valor de sequência de caracteres que especifica o nome do design do formulário.

>[!NOTE]
>
>Para exibir dados no formulário, os dados devem ser especificados no elemento `xfa:datasets`. Para obter informações sobre a arquitetura XFA, acesse [https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf).

**Gravar o fluxo de dados de formulário no navegador Web cliente**

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

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Referência ao design do formulário

   * Crie um objeto `java.io.FileInputStream` que represente o design do formulário a ser renderizado usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do arquivo XDP.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Renderizar um formulário por valor

   Invoque o método `renderPDFForm` do objeto `FormsServiceClient` e passe os seguintes valores:

   * Um valor de string vazio. (Normalmente, esse parâmetro requer um valor de sequência de caracteres que especifica o nome do design do formulário.)
   * Um objeto `com.adobe.idp.Document` que contém o design do formulário. Normalmente, esse valor de parâmetro é reservado para dados que são mesclados com o formulário.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que pode ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `com.adobe.idp.Document` invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie um objeto `java.io.InputStream` invocando o método `getInputStream` do objeto `com.adobe.idp.Document`.
   * Crie uma matriz de bytes e aloque o tamanho do objeto `InputStream`. Invoque o método `available` do objeto `InputStream` para obter o tamanho do objeto `InputStream`.
   * Preencha a matriz de bytes com o fluxo de dados de formulário chamando o método `read` do objeto `InputStream` e transmitindo a matriz de bytes como um argumento.
   * Invoque o método `write` do objeto `javax.servlet.ServletOutputStream` para enviar o fluxo de dados de formulário para o navegador Web cliente. Passar a matriz de bytes para o método `write`.

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

   Crie um objeto `FormsService` e defina valores de autenticação.

1. Referência ao design do formulário

   * Crie um objeto `java.io.FileInputStream` usando seu construtor. Transmita um valor de string que especifique o local do arquivo XDP.
   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que está criptografado com uma senha.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `java.io.FileInputStream`. Você pode determinar o tamanho da matriz de bytes obtendo o tamanho do objeto `java.io.FileInputStream` usando seu método `available`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `read` do objeto `java.io.FileInputStream` e transmitindo a matriz de bytes.
   * Preencha o objeto `BLOB` invocando seu método `setBinaryData` e transmitindo a matriz de bytes.

1. Renderizar um formulário por valor

   Invoque o método `renderPDFForm` do objeto `FormsService` e passe os seguintes valores:

   * Um valor de string vazio. (Normalmente, esse parâmetro requer um valor de sequência de caracteres que especifica o nome do design do formulário.)
   * Um objeto `BLOB` que contém o design do formulário. Normalmente, esse valor de parâmetro é reservado para dados que são mesclados com o formulário.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um objeto `com.adobe.idp.services.holders.BLOBHolder` vazio preenchido pelo método. Isso é usado para armazenar o formulário de PDF renderizado.
   * Um objeto `javax.xml.rpc.holders.LongHolder` vazio preenchido pelo método. (Esse argumento armazena o número de páginas no formulário.)
   * Um objeto `javax.xml.rpc.holders.StringHolder` vazio preenchido pelo método. (Esse argumento armazena o valor do local.)
   * Um objeto `com.adobe.idp.services.holders.FormsResultHolder` vazio que conterá os resultados desta operação.

   O método `renderPDFForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador Web cliente.

1. Gravar o fluxo de dados do formulário no navegador Web cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `value` do objeto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Crie um objeto `BLOB` que contenha dados de formulário invocando o método `getOutputContent` do objeto `FormsResult`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` invocando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` invocando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados de formulário no navegador da Web cliente, chamando o método `getOutputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie uma matriz de bytes e preencha-a chamando o método `getBinaryData` do objeto `BLOB`. Esta tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Invoque o método `write` do objeto `javax.servlet.http.HttpServletResponse` para enviar o fluxo de dados de formulário para o navegador Web cliente. Passar a matriz de bytes para o método `write`.

**Consulte também**

[Renderização do Forms por valor](#rendering-forms-by-value)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
