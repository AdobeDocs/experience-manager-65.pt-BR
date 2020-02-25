---
title: Renderização de formulários por valor
seo-title: Renderização de formulários por valor
description: 'null'
seo-description: 'null'
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Renderização de formulários por valor {#rendering-forms-by-value}

Normalmente, um design de formulário criado no Designer é transmitido por referência ao serviço de Formulários. Os designs de formulário podem ser grandes e, como resultado, é mais eficiente passá-los por referência para evitar a necessidade de empacotar bytes de design de formulário por valor. O serviço Forms também pode armazenar o design de formulário em cache para que, quando armazenado em cache, ele não precise ler continuamente o design de formulário.

Se um design de formulário contiver um atributo UUID, ele será armazenado em cache. O valor UUID é exclusivo para todos os designs de formulário e é usado para identificar exclusivamente um formulário. Ao renderizar um formulário por valor, o formulário só deve ser armazenado em cache quando for usado repetidamente. No entanto, se o formulário não for usado repetidamente e tiver que ser exclusivo, será possível evitar o armazenamento em cache do formulário usando as opções de armazenamento em cache definidas usando a API de formulários do AEM.

O serviço Forms também pode resolver o local do conteúdo vinculado no design de formulário. Por exemplo, imagens vinculadas que são referenciadas no design de formulário são URLs relativos. O conteúdo vinculado é sempre considerado como sendo relativo ao local do design de formulário. Portanto, resolver o conteúdo vinculado é uma questão de determinar sua localização aplicando o caminho relativo à localização absoluta do design de formulário.

Em vez de passar um design de formulário por referência, é possível passar um design de formulário por valor. A transmissão de um design de formulário por valor é eficiente quando um design de formulário é criado dinamicamente; ou seja, quando um aplicativo cliente gera o XML que cria um design de formulário durante o tempo de execução. Nesse caso, um design de formulário não é armazenado em um repositório físico porque é armazenado na memória. Ao criar dinamicamente um design de formulário em tempo de execução e passá-lo por valor, é possível armazenar o formulário em cache e melhorar o desempenho do serviço Forms.

**Limitações de passagem de um formulário por valor**

As limitações a seguir se aplicam quando um design de formulário é aprovado pelo valor:

* Nenhum conteúdo vinculado relativo pode estar no design de formulário. Todas as imagens e fragmentos devem ser incorporados dentro do design de formulário ou absolutamente referenciados.
* Os cálculos do lado do servidor não podem ser executados após a renderização do formulário. Se o formulário for submetido de volta ao serviço Forms, os dados serão extraídos e retornados sem qualquer cálculo no servidor.
* Como o HTML só pode usar imagens vinculadas em tempo de execução, não é possível gerar HTML com imagens incorporadas. Isso ocorre porque o serviço do Forms oferece suporte a imagens incorporadas com HTML recuperando as imagens de um design de formulário referenciado. Como um design de formulário transmitido pelo valor não tem um local referenciado, as imagens incorporadas não podem ser extraídas quando a página HTML é exibida. Portanto, as referências de imagem devem ser caminhos absolutos a serem renderizados em HTML.

>[!NOTE]
>
>Embora seja possível renderizar diferentes tipos de formulários por valor (por exemplo, formulários HTML ou formulários que contenham direitos de uso), esta seção aborda a renderização de formulários PDF interativos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Formulários, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário por valor, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Forms Client.
1. Consulte o design de formulário.
1. Renderize um formulário por valor.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente Forms**

Antes de poder importar dados de forma programática para uma API do cliente de formulário PDF, é necessário criar um cliente de serviço de Integração de dados. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço.

**Referência ao design de formulário**

Ao renderizar um formulário por valor, é necessário criar um `com.adobe.idp.Document` objeto que contenha o design de formulário a ser renderizado. É possível fazer referência a um arquivo XDP existente ou criar um design de formulário dinamicamente em tempo de execução e preencher um arquivo com `com.adobe.idp.Document` esses dados.

>[!NOTE]
>
>Esta seção e o início rápido correspondente fazem referência a um arquivo XDP existente.

**Renderizar um formulário por valor**

Para renderizar um formulário por valor, passe uma `com.adobe.idp.Document` instância que contenha o design de formulário para o `inDataDoc` parâmetro do método de renderização (pode ser qualquer um dos métodos de renderização do `FormsServiceClient` objeto, como `renderPDFForm`, `(Deprecated) renderHTMLForm`etc.). Normalmente, esse valor de parâmetro é reservado para dados que são unidos ao formulário. Da mesma forma, passe um valor de string vazio para o `formQuery` parâmetro. Normalmente, esse parâmetro requer um valor de string que especifica o nome do design de formulário.

>[!NOTE]
>
>Se você quiser exibir dados dentro do formulário, os dados devem ser especificados dentro do `xfa:datasets` elemento. Para obter informações sobre a arquitetura XFA, acesse [https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html).

**Gravar o fluxo de dados do formulário no navegador da Web do cliente**

Quando o serviço Forms renderiza um formulário por valor, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente. Quando gravado no navegador da Web do cliente, o formulário fica visível para o usuário.

**Consulte também:**

[Renderizar um formulário por valor usando a API Java](#render-a-form-by-value-using-the-java-api)

[Renderizar um formulário por valor usando a API de serviço da Web](#render-a-form-by-value-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do serviço de formulários](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmissão de documentos ao serviço Forms](/help/forms/developing/passing-documents-forms-service.md)

[Criação de aplicativos da Web que renderizam formulários](/help/forms/developing/creating-web-applications-renders-forms.md)

## Renderizar um formulário por valor usando a API Java {#render-a-form-by-value-using-the-java-api}

Renderize um formulário por valor usando a API de formulários (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto da API do cliente Forms

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `FormsServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Referência ao design de formulário

   * Crie um `java.io.FileInputStream` objeto que represente o design de formulário a ser renderizado usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XDP.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Renderizar um formulário por valor

   Chame o método do `FormsServiceClient` objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string vazio. (Normalmente, esse parâmetro requer um valor de string que especifica o nome do design de formulário.)
   * Um `com.adobe.idp.Document` objeto que contém o design de formulário. Normalmente, esse valor de parâmetro é reservado para dados que são unidos ao formulário.
   * Um `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Esse é um parâmetro opcional e você pode especificar `null` se não deseja especificar opções de tempo de execução.
   * Um `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que pode ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um `com.adobe.idp.Document` objeto chamando o `FormsResult` método do objeto `getOutputContent` .
   * Obtenha o tipo de conteúdo do `com.adobe.idp.Document` objeto chamando seu `getContentType` método.
   * Defina o tipo de conteúdo do `javax.servlet.http.HttpServletResponse` objeto chamando seu `setContentType` método e transmitindo o tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o `javax.servlet.http.HttpServletResponse` `getOutputStream` método do objeto.
   * Crie um `java.io.InputStream` objeto chamando o `com.adobe.idp.Document` método do `getInputStream` objeto.
   * Crie uma matriz de bytes e aloce o tamanho do `InputStream` objeto. Chame o `InputStream` método do `available` objeto para obter o tamanho do `InputStream` objeto.
   * Preencha a matriz de bytes com o fluxo de dados do formulário chamando o `InputStream` método do `read`objeto e transmitindo a matriz de bytes como um argumento.
   * Chame o método do `javax.servlet.ServletOutputStream` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também:**

[Renderização de formulários por valor](/help/forms/developing/rendering-forms.md#rendering-forms-by-value)

[Início rápido (modo SOAP): Renderização por valor usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar um formulário por valor usando a API de serviço da Web {#render-a-form-by-value-using-the-web-service-api}

Renderize um formulário por valor usando a API de formulários (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto da API do cliente Forms

   Crie um `FormsService` objeto e defina valores de autenticação.

1. Referência ao design de formulário

   * Crie um `java.io.FileInputStream` objeto usando seu construtor. Passe um valor de string que especifica o local do arquivo XDP.
   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar um documento PDF criptografado com uma senha.
   * Crie uma matriz de bytes que armazene o conteúdo do `java.io.FileInputStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo o tamanho do `java.io.FileInputStream` objeto usando seu `available` método.
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `java.io.FileInputStream` objeto `read` e transmitindo a matriz de bytes.
   * Preencha o `BLOB` objeto chamando seu `setBinaryData` método e transmitindo a matriz de bytes.

1. Renderizar um formulário por valor

   Chame o método do `FormsService` objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string vazio. (Normalmente, esse parâmetro requer um valor de string que especifica o nome do design de formulário.)
   * Um `BLOB` objeto que contém o design de formulário. Normalmente, esse valor de parâmetro é reservado para dados que são unidos ao formulário.
   * Um `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Esse é um parâmetro opcional e você pode especificar `null` se não deseja especificar opções de tempo de execução.
   * Um `URLSpec` objeto que contém valores de URI exigidos pelo serviço Forms.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   * Um `com.adobe.idp.services.holders.BLOBHolder` objeto vazio que é preenchido pelo método. Isso é usado para armazenar o formulário PDF renderizado.
   * Um `javax.xml.rpc.holders.LongHolder` objeto vazio que é preenchido pelo método. (Esse argumento armazena o número de páginas no formulário.)
   * Um `javax.xml.rpc.holders.StringHolder` objeto vazio que é preenchido pelo método. (Este argumento armazena o valor de localidade.)
   * Um `com.adobe.idp.services.holders.FormsResultHolder` objeto vazio que conterá os resultados dessa operação.
   O `renderPDFForm` método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um `FormResult` objeto obtendo o valor do membro de `com.adobe.idp.services.holders.FormsResultHolder` dados do `value` objeto.
   * Crie um `BLOB` objeto que contenha dados de formulário chamando o `FormsResult` método do `getOutputContent` objeto.
   * Obtenha o tipo de conteúdo do `BLOB` objeto chamando seu `getContentType` método.
   * Defina o tipo de conteúdo do `javax.servlet.http.HttpServletResponse` objeto chamando seu `setContentType` método e transmitindo o tipo de conteúdo do `BLOB` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o `javax.servlet.http.HttpServletResponse` `getOutputStream` método do objeto.
   * Crie uma matriz de bytes e preencha-a chamando o método do `BLOB` objeto `getBinaryData` . Essa tarefa atribui o conteúdo do `FormsResult` objeto à matriz de bytes.
   * Chame o método do `javax.servlet.http.HttpServletResponse` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.

**Consulte também:**

[Renderização de formulários por valor](#rendering-forms-by-value)

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
