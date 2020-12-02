---
title: Renderizando Forms por valor
seo-title: Renderizando Forms por valor
description: 'null'
seo-description: nulo
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
translation-type: tm+mt
source-git-commit: 66bfd6870b4c09dc2ca1b66058e0b9e040a71507
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 0%

---


# Renderizando Forms por valor {#rendering-forms-by-value}

Normalmente, um design de formulário criado no Designer é transmitido por referência ao serviço Forms. Os designs de formulário podem ser grandes e, como resultado, é mais eficiente passá-los por referência para evitar a necessidade de empacotar bytes de design de formulário por valor. O serviço Forms também pode armazenar em cache o design de formulário para que, quando armazenado em cache, ele não precise ler continuamente o design de formulário.

Se um design de formulário contiver um atributo UUID, ele será armazenado em cache. O valor UUID é exclusivo para todos os designs de formulário e é usado para identificar exclusivamente um formulário. Ao renderizar um formulário por valor, o formulário só deve ser armazenado em cache quando for usado repetidamente. No entanto, se o formulário não for usado repetidamente e tiver que ser exclusivo, será possível evitar o armazenamento em cache do formulário usando opções de armazenamento em cache definidas com a API do AEM Forms.

O serviço Forms também pode resolver a localização do conteúdo vinculado no design de formulário. Por exemplo, imagens vinculadas que são referenciadas no design de formulário são URLs relativos. O conteúdo vinculado é sempre considerado como sendo relativo ao local do design de formulário. Portanto, resolver o conteúdo vinculado é uma questão de determinar sua localização aplicando o caminho relativo à localização absoluta do design de formulário.

Em vez de passar um design de formulário por referência, é possível passar um design de formulário por valor. A transmissão de um design de formulário por valor é eficiente quando um design de formulário é criado dinamicamente; ou seja, quando um aplicativo cliente gera o XML que cria um design de formulário durante o tempo de execução. Nesse caso, um design de formulário não é armazenado em um repositório físico porque é armazenado na memória. Ao criar dinamicamente um design de formulário em tempo de execução e passá-lo por valor, é possível armazenar o formulário em cache e melhorar o desempenho do serviço Forms.

**Limitações de passagem de um formulário por valor**

As limitações a seguir se aplicam quando um design de formulário é aprovado pelo valor:

* Nenhum conteúdo vinculado relativo pode estar no design de formulário. Todas as imagens e fragmentos devem ser incorporados dentro do design de formulário ou absolutamente referenciados.
* Os cálculos do lado do servidor não podem ser executados depois que o formulário é renderizado. Se o formulário for enviado de volta ao serviço da Forms, os dados serão extraídos e retornados sem cálculos do lado do servidor.
* Como o HTML só pode usar imagens vinculadas em tempo de execução, não é possível gerar HTML com imagens incorporadas. Isso ocorre porque o serviço Forms oferece suporte a imagens incorporadas com HTML recuperando as imagens de um design de formulário referenciado. Como um design de formulário transmitido pelo valor não tem um local referenciado, as imagens incorporadas não podem ser extraídas quando a página HTML é exibida. Portanto, as referências de imagem devem ser caminhos absolutos a serem renderizados em HTML.

>[!NOTE]
>
>Embora seja possível renderizar diferentes tipos de formulários por valor (por exemplo, formulários HTML ou formulários que contenham direitos de uso), esta seção aborda a renderização de PDF forms interativos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário por valor, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto de API do Forms Client.
1. Consulte o design de formulário.
1. Renderize um formulário por valor.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do Forms Client**

Antes de poder importar dados de forma programática para uma API do cliente de formulário PDF, é necessário criar um cliente de serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço.

**Referência ao design de formulário**

Ao renderizar um formulário por valor, é necessário criar um objeto `com.adobe.idp.Document` que contenha o design de formulário a ser renderizado. Você pode fazer referência a um arquivo XDP existente ou pode criar dinamicamente um design de formulário em tempo de execução e preencher um `com.adobe.idp.Document` com esses dados.

>[!NOTE]
>
>Esta seção e o start rápido correspondente fazem referência a um arquivo XDP existente.

**Renderizar um formulário por valor**

Para renderizar um formulário pelo valor, passe uma instância `com.adobe.idp.Document` que contenha o design de formulário para o parâmetro `inDataDoc` do método de renderização (pode ser qualquer um dos métodos de renderização do objeto `FormsServiceClient`, como `renderPDFForm`, `(Deprecated) renderHTMLForm` e assim por diante). Normalmente, esse valor de parâmetro é reservado para dados que são unidos ao formulário. Da mesma forma, passe um valor de string vazio para o parâmetro `formQuery`. Normalmente, esse parâmetro requer um valor de string que especifica o nome do design de formulário.

>[!NOTE]
>
>Se você quiser exibir dados dentro do formulário, os dados devem ser especificados dentro do elemento `xfa:datasets`. Para obter informações sobre a arquitetura XFA, acesse [https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html).

**Gravar o fluxo de dados do formulário no navegador da Web do cliente**

Quando o serviço Forms renderiza um formulário por valor, ele retorna um fluxo de dados do formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.

**Consulte também:**

[Renderizar um formulário por valor usando a API Java](#render-a-form-by-value-using-the-java-api)

[Renderizar um formulário por valor usando a API de serviço da Web](#render-a-form-by-value-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API de serviço da Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmissão de Documentos ao serviço Forms](/help/forms/developing/passing-documents-forms-service.md)

[Criação de Aplicações web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Renderizar um formulário por valor usando a API Java {#render-a-form-by-value-using-the-java-api}

Renderize um formulário por valor usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do Forms Client

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Referência ao design de formulário

   * Crie um objeto `java.io.FileInputStream` que represente o design de formulário a ser renderizado usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XDP.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Renderizar um formulário por valor

   Chame o método `FormsServiceClient` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string vazio. (Normalmente, esse parâmetro requer um valor de string que especifica o nome do design de formulário.)
   * Um objeto `com.adobe.idp.Document` que contém o design de formulário. Normalmente, esse valor de parâmetro é reservado para dados que são unidos ao formulário.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que pode ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie um objeto `java.io.InputStream` invocando o método `com.adobe.idp.Document` do objeto `getInputStream`.
   * Crie uma matriz de bytes e aloce o tamanho do objeto `InputStream`. Chame o método `InputStream` do objeto `available` para obter o tamanho do objeto `InputStream`.
   * Preencha a matriz de bytes com o fluxo de dados do formulário chamando o método `InputStream` do objeto `read`e transmitindo a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Renderizando Forms por valor](/help/forms/developing/rendering-forms.md)

[Start rápido (modo SOAP): Renderização por valor usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar um formulário pelo valor usando a API de serviço da Web {#render-a-form-by-value-using-the-web-service-api}

Renderize um formulário por valor usando a Forms API (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do Forms Client

   Crie um objeto `FormsService` e defina os valores de autenticação.

1. Referência ao design de formulário

   * Crie um objeto `java.io.FileInputStream` usando seu construtor. Passe um valor de string que especifica o local do arquivo XDP.
   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar um documento PDF que é criptografado com uma senha.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `java.io.FileInputStream`. Você pode determinar o tamanho da matriz de bytes obtendo o tamanho do objeto `java.io.FileInputStream` usando seu método `available`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `java.io.FileInputStream` do objeto `read` e transmitindo a matriz de bytes.
   * Preencha o objeto `BLOB` chamando seu método `setBinaryData` e transmitindo a matriz de bytes.

1. Renderizar um formulário por valor

   Chame o método `FormsService` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string vazio. (Normalmente, esse parâmetro requer um valor de string que especifica o nome do design de formulário.)
   * Um objeto `BLOB` que contém o design de formulário. Normalmente, esse valor de parâmetro é reservado para dados que são unidos ao formulário.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução. Este é um parâmetro opcional e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método. Isso é usado para armazenar o formulário PDF renderizado.
   * Um objeto vazio `javax.xml.rpc.holders.LongHolder` que é preenchido pelo método. (Esse argumento armazena o número de páginas no formulário.)
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método. (Este argumento armazena o valor de localidade.)
   * Um objeto vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O método `renderPDFForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` transmitido como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value`.
   * Crie um objeto `BLOB` que contenha dados de formulário chamando o método `FormsResult` do objeto `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie uma matriz de bytes e preencha-a chamando o método `BLOB` do objeto `getBinaryData`. Essa tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Renderizando Forms por valor](#rendering-forms-by-value)

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
