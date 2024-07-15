---
title: Manuseio de Forms enviado
description: Use o serviço Forms para recuperar os dados enviados inseridos em um formulário interativo. O usuário pode enviar os dados do formulário nos formatos XML, PDF e URL UTF-16.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2894'
ht-degree: 0%

---

# Manuseio de Forms enviado {#handling-submitted-forms}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

Aplicativos baseados na Web que permitem que um usuário preencha formulários interativos exigem que os dados sejam enviados de volta ao servidor. Usando o serviço Forms, você pode recuperar os dados inseridos pelo usuário em um formulário interativo. Após recuperar os dados, você pode processá-los para atender aos requisitos da empresa. Por exemplo, você pode armazenar os dados em um banco de dados, enviar os dados para outro aplicativo, enviar os dados para outro serviço, mesclar os dados em um design de formulário, exibir os dados em um navegador da Web e assim por diante.

Os dados de formulário são enviados ao serviço Forms como dados XML ou PDF, que é uma opção definida no Designer. Um formulário enviado como XML permite extrair valores de dados de campo individuais. Ou seja, você pode extrair o valor de cada campo de formulário inserido pelo usuário no formulário. Um formulário enviado como dados de PDF é um dado binário, não um dado XML. Você pode salvar o formulário como um arquivo PDF ou enviá-lo para outro serviço. Se quiser extrair dados de um formulário enviado como XML e, em seguida, usar os dados do formulário para criar um documento PDF, chame outra operação do AEM Forms. (Consulte [Criando Documentos PDF com Dados XML Enviados](/help/forms/developing/creating-pdf-documents-submitted-xml.md))

O diagrama a seguir mostra os dados sendo enviados para um Servlet Java chamado `HandleData` de um formulário interativo exibido em um navegador da Web.

![hs_hs_handlesubmit](assets/hs_hs_handlesubmit.png)

A tabela a seguir explica as etapas do diagrama.

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Um usuário preenche um formulário interativo e clica no botão Enviar do formulário.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Os dados são enviados para o Servlet Java <code>HandleData</code> como dados XML.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>O Servlet Java <code>HandleData</code> contém lógica de aplicativo para recuperar os dados.</p></td>
  </tr>
 </tbody>
</table>

## Manuseio de dados XML enviados {#handling-submitted-xml-data}

Quando os dados do formulário forem enviados como XML, você poderá recuperar dados XML que representam os dados enviados. Todos os campos de formulário aparecem como nós em um esquema XML. Os valores do nó correspondem aos valores que o usuário preencheu. Considere um formulário de empréstimo em que cada campo no formulário aparece como um nó nos dados XML. O valor de cada nó corresponde ao valor que um usuário preenche. Suponha que um usuário preencha o formulário de empréstimo com os dados mostrados no formulário a seguir.

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

A ilustração a seguir mostra dados XML correspondentes que são recuperados usando a API do cliente de serviço do Forms.

![hs_hs_loandata](assets/hs_hs_loandata.png)

Os campos no formulário de empréstimo. Esses valores podem ser recuperados
usando classes Java XML.

>[!NOTE]
>
>O design do formulário deve ser configurado corretamente no Designer para que os dados sejam enviados como dados XML. Para configurar corretamente o design do formulário para enviar dados XML, verifique se o botão Submit localizado no design do formulário está definido para enviar dados XML. Para obter informações sobre como configurar o botão Enviar para enviar dados XML, consulte [AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Tratamento de dados de PDF enviados {#handling-submitted-pdf-data}

Considere um aplicativo web que invoca o serviço Forms. Depois que o serviço Forms renderiza um formulário PDF interativo para um navegador web cliente, o usuário preenche o formulário e o envia de volta como dados PDF. Quando o serviço Forms recebe os dados de PDF, pode enviar os dados de PDF para outro serviço ou salvá-los como um arquivo PDF. O diagrama a seguir mostra o fluxo lógico do aplicativo.

![hs_hs_savingforms](assets/hs_hs_savingforms.png)

A tabela a seguir descreve as etapas deste diagrama.

<table>
 <thead>
  <tr>
   <th><p>Etapa</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Uma página da Web contém um link que acessa um Servlet Java que chama o serviço Forms.</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>O serviço Forms renderiza um formulário PDF interativo para o navegador web do cliente.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>O usuário preenche um formulário interativo e clica em um botão Enviar. O formulário é enviado de volta ao serviço Forms como dados de PDF. Essa opção é definida no Designer.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>O serviço Forms salva os dados do PDF como um arquivo PDF. </p></td>
  </tr>
 </tbody>
</table>

## Manuseio de dados UTF-16 de URL enviado {#handling-submitted-url-utf-16-data}

Se os dados de formulário forem enviados como dados URL UTF-16, o computador cliente exigirá o Adobe Reader ou Acrobat 8.1 ou posterior. Além disso, se o design do formulário contiver um botão de envio com dados codificados em URL (HTTP Post) e a opção de codificação de dados for UTF-16, o design do formulário deverá ser modificado em um editor de texto como o Notepad. Você pode definir a opção de codificação como `UTF-16LE` ou `UTF-16BE` para o botão enviar. A Designer não fornece essa funcionalidade.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para controlar forms enviados, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Recuperar dados do formulário.
1. Determine se o envio do formulário contém anexos de arquivo.
1. Processe os dados enviados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente do Forms**

Antes de executar programaticamente uma operação da API do cliente de serviço do Forms, você deve criar um cliente de serviço do Forms. Se você estiver usando a API Java, crie um objeto `FormsServiceClient`. Se você estiver usando a API de serviço Web Forms, crie um objeto `FormsService`.

**Recuperar dados do formulário**

Para recuperar os dados de formulário enviados, chame o método `processFormSubmission` do objeto `FormsServiceClient`. Ao chamar esse método, você precisa especificar o tipo de conteúdo do formulário enviado. Quando os dados são enviados de um navegador da Web cliente para o serviço Forms, eles podem ser enviados como dados XML ou PDF. Para recuperar os dados inseridos nos campos de formulário, os dados podem ser enviados como dados XML.

Você também pode recuperar campos de formulário enviados como dados de PDF definindo as seguintes opções de tempo de execução:

* Passe o seguinte valor para o método `processFormSubmission` como o parâmetro de tipo de conteúdo: `CONTENT_TYPE=application/pdf`.
* Defina o valor `PDFToXDP` do objeto `RenderOptionsSpec` como `true`
* Defina o valor `ExportDataFormat` do objeto `RenderOptionsSpec` como `XMLData`

Você especifica o tipo de conteúdo do formulário enviado quando invoca o método `processFormSubmission`. A lista a seguir especifica os valores de tipo de conteúdo aplicáveis:

* **text/xml**: representa o tipo de conteúdo a ser usado quando um formulário PDF envia dados de formulário como XML.
* **application/x-www-form-urlencoded**: representa o tipo de conteúdo a ser usado quando um formulário HTML envia dados como XML.
* **application/pdf**: representa o tipo de conteúdo a ser usado quando um formulário PDF envia dados como PDF.

>[!NOTE]
>
>Você observará que há três inicializações rápidas correspondentes associadas à seção Manipulação de Forms enviada. O Manipulação de PDF forms enviado como PDF usando o início rápido da API Java demonstra como lidar com os dados de PDF enviados. O tipo de conteúdo especificado neste início rápido é `application/pdf`. O Manipulação de PDF forms enviado como XML usando o início rápido da API Java demonstra como lidar com dados XML enviados enviados a partir de um formulário PDF. O tipo de conteúdo especificado neste início rápido é `text/xml`. Da mesma forma, o Manipulando formulários de HTML enviados como XML usando o início rápido da API Java demonstra como manipular dados XML enviados que são enviados de um formulário de HTML. O tipo de conteúdo especificado neste início rápido é application/x-www-form-urlencoded.

Você recupera dados de formulário publicados no serviço Forms e determina o estado de processamento. Ou seja, quando os dados são enviados para o serviço Forms, isso não significa necessariamente que o serviço Forms terminou de processar os dados e eles estão prontos para serem processados. Por exemplo, os dados podem ser enviados para o serviço Forms para que um cálculo possa ser executado. Quando o cálculo é concluído, o formulário é renderizado para o usuário com os resultados do cálculo exibidos. Antes de processar os dados enviados, é recomendável determinar se o serviço Forms terminou de processar os dados.

O serviço Forms retorna os seguintes valores para indicar se terminou de processar os dados:

* **0 (Enviar):** Os dados enviados estão prontos para serem processados.
* **1 (Calcular):** o serviço Forms executou uma operação de cálculo nos dados e os resultados devem ser renderizados para o usuário.
* **2 (Validar):** Os dados de formulário validados pelo serviço Forms e os resultados devem ser renderizados para o usuário.
* **3 (Próximo):** A página atual foi alterada com resultados que devem ser gravados no aplicativo cliente.
* **4 (Anterior**): a página atual foi alterada com resultados que devem ser gravados no aplicativo cliente.

>[!NOTE]
>
>Os cálculos e validações devem ser renderizados para o usuário. (Consulte [Calculando Dados De Formulário](/help/forms/developing/calculating-form-data.md#calculating-form-data).

**Determine se o envio do formulário contém anexos de arquivo**

O Forms enviado para o serviço Forms pode conter anexos de arquivo. Por exemplo, usando o painel de anexos integrado do Acrobat, um usuário pode selecionar anexos de arquivo para enviar junto com o formulário. Além disso, um usuário também pode selecionar anexos de arquivo usando uma barra de ferramentas HTML que é renderizada com um arquivo HTML.

Depois de determinar se um formulário contém anexos de arquivo, você pode processar os dados. Por exemplo, você pode salvar o anexo de arquivo no sistema de arquivos local.

>[!NOTE]
>
>O formulário deve ser enviado como dados de PDF para recuperar anexos de arquivo. Se o formulário for enviado como dados XML, os anexos de arquivo não serão enviados.

**Processar os dados enviados**

Dependendo do tipo de conteúdo dos dados enviados, você pode extrair valores de campo de formulário individuais dos dados XML enviados ou salvar os dados de PDF enviados como um arquivo de PDF (ou enviá-los para outro serviço). Para extrair campos de formulário individuais, converta dados XML enviados em uma fonte de dados XML e recupere valores de fonte de dados XML usando classes `org.w3c.dom`.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Passar documentos para o serviço da Forms](/help/forms/developing/passing-documents-forms-service.md)

[Criação de aplicações Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Lidar com formulários enviados usando a API Java {#handle-submitted-forms-using-the-java-api}

Manipule um formulário enviado usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto da API do cliente do Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recuperar dados do formulário

   * Para recuperar dados de formulário postados em um Servlet Java, crie um objeto `com.adobe.idp.Document` usando seu construtor e invocando o método `getInputStream` do objeto `javax.servlet.http.HttpServletResponse` de dentro do construtor.
   * Crie um objeto `RenderOptionsSpec` usando seu construtor. Defina o valor da localidade invocando o método `setLocale` do objeto `RenderOptionsSpec` e transmitindo um valor de cadeia de caracteres que especifique o valor da localidade.

   >[!NOTE]
   >
   >Você pode instruir o serviço Forms a criar dados XDP ou XML a partir do conteúdo de PDF enviado, chamando o método `setPDF2XDP` do objeto `RenderOptionsSpec` e passando `true`, além de chamar `setXMLData` e passar `true`. Em seguida, você pode invocar o método `getOutputXML` do objeto `FormsResult` para recuperar os dados XML que correspondem aos dados XDP/XML. (O objeto `FormsResult` é retornado pelo método `processFormSubmission`, que é explicado na próxima subetapa.)

   * Chame o método `processFormSubmission` do objeto `FormsServiceClient` e passe os seguintes valores:

      * O objeto `com.adobe.idp.Document` que contém os dados de formulário.
      * Um valor de string que especifica variáveis de ambiente, incluindo todos os cabeçalhos HTTP relevantes. Especifique o tipo de conteúdo a ser manipulado. Para manipular dados XML, especifique o seguinte valor de cadeia de caracteres para este parâmetro: `CONTENT_TYPE=text/xml`. Para manipular dados de PDF, especifique o seguinte valor de cadeia de caracteres para este parâmetro: `CONTENT_TYPE=application/pdf`.
      * Um valor de cadeia de caracteres que especifica o valor do cabeçalho `HTTP_USER_AGENT`, por exemplo, . `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Esse valor de parâmetro é opcional.
      * Um objeto `RenderOptionsSpec` que armazena opções de tempo de execução.

     O método `processFormSubmission` retorna um objeto `FormsResult` contendo os resultados do envio do formulário.

   * Determine se o serviço Forms terminou de processar os dados do formulário invocando o método `getAction` do objeto `FormsResult`. Se esse método retornar o valor `0`, os dados estarão prontos para serem processados.

1. Determine se o envio do formulário contém anexos de arquivo

   * Invoque o método `getAttachments` do objeto `FormsResult`. Este método retorna um objeto `java.util.List` que contém arquivos enviados com o formulário.
   * Repita através do objeto `java.util.List` para determinar se há anexos de arquivo. Se houver anexos de arquivo, cada elemento será uma instância `com.adobe.idp.Document`. Você pode salvar os anexos de arquivo chamando o método `copyToFile` do objeto `com.adobe.idp.Document` e transmitindo um objeto `java.io.File`.

   >[!NOTE]
   >
   >Esta etapa só será aplicável se o formulário for enviado como PDF.

1. Processar os dados enviados

   * Se o tipo de conteúdo de dados for `application/vnd.adobe.xdp+xml` ou `text/xml`, crie uma lógica de aplicativo para recuperar valores de dados XML.

      * Crie um objeto `com.adobe.idp.Document` invocando o método `getOutputContent` do objeto `FormsResult`.
      * Crie um objeto `java.io.InputStream` invocando o construtor `java.io.DataInputStream` e transmitindo o objeto `com.adobe.idp.Document`.
      * Crie um objeto `org.w3c.dom.DocumentBuilderFactory` chamando o método `newInstance` estático do objeto `org.w3c.dom.DocumentBuilderFactory`.
      * Crie um objeto `org.w3c.dom.DocumentBuilder` invocando o método `newDocumentBuilder` do objeto `org.w3c.dom.DocumentBuilderFactory`.
      * Crie um objeto `org.w3c.dom.Document` invocando o método `parse` do objeto `org.w3c.dom.DocumentBuilder` e transmitindo o objeto `java.io.InputStream`.
      * Recupere o valor de cada nó no documento XML. Uma maneira de realizar essa tarefa é criar um método personalizado que aceite dois parâmetros: o objeto `org.w3c.dom.Document` e o nome do nó cujo valor você deseja recuperar. Esse método retorna um valor de string que representa o valor do nó. No exemplo de código que segue esse processo, esse método personalizado é chamado de `getNodeText`. O corpo desse método é mostrado.

   * Se o tipo de conteúdo de dados for `application/pdf`, crie uma lógica de aplicativo para salvar os dados de PDF enviados como um arquivo de PDF.

      * Crie um objeto `com.adobe.idp.Document` invocando o método `getOutputContent` do objeto `FormsResult`.
      * Crie um objeto `java.io.File` usando seu construtor público. Certifique-se de especificar PDF como a extensão do nome do arquivo.
      * Preencha o arquivo PDF chamando o método `copyToFile` do objeto `com.adobe.idp.Document` e transmitindo o objeto `java.io.File`.

**Consulte também**

[Início rápido (modo SOAP): lidar com PDF forms enviados como XML usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Início rápido (modo SOAP): lidando com formulários HTML enviados como XML usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Início rápido (modo SOAP): lidar com PDF forms enviados como PDF usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Lidar com dados de PDF enviados usando a API do serviço Web {#handle-submitted-pdf-data-using-the-web-service-api}

Manipule um formulário enviado usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms.
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar um objeto da API do cliente do Forms

   Crie um objeto `FormsService` e defina valores de autenticação.

1. Recuperar dados do formulário

   * Para recuperar dados de formulário postados em um Servlet Java, crie um objeto `BLOB` usando seu construtor.
   * Crie um objeto `java.io.InputStream` invocando o método `getInputStream` do objeto `javax.servlet.http.HttpServletResponse`.
   * Crie um objeto `java.io.ByteArrayOutputStream` usando seu construtor e transmitindo o comprimento do objeto `java.io.InputStream`.
   * Copie o conteúdo do objeto `java.io.InputStream` no objeto `java.io.ByteArrayOutputStream`.
   * Crie uma matriz de bytes invocando o método `toByteArray` do objeto `java.io.ByteArrayOutputStream`.
   * Preencha o objeto `BLOB` invocando seu método `setBinaryData` e transmitindo a matriz de bytes como um argumento.
   * Crie um objeto `RenderOptionsSpec` usando seu construtor. Defina o valor da localidade invocando o método `setLocale` do objeto `RenderOptionsSpec` e transmitindo um valor de cadeia de caracteres que especifique o valor da localidade.
   * Chame o método `processFormSubmission` do objeto `FormsService` e passe os seguintes valores:

      * O objeto `BLOB` que contém os dados de formulário.
      * Um valor de string que especifica variáveis de ambiente, incluindo todos os cabeçalhos HTTP relevantes. Especifique o tipo de conteúdo a ser manipulado. Para manipular dados XML, especifique o seguinte valor de cadeia de caracteres para este parâmetro: `CONTENT_TYPE=text/xml`. Para manipular dados de PDF, especifique o seguinte valor de cadeia de caracteres para este parâmetro: `CONTENT_TYPE=application/pdf`.
      * Um valor de cadeia de caracteres que especifica o valor do cabeçalho `HTTP_USER_AGENT`; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Um objeto `RenderOptionsSpec` que armazena opções de tempo de execução.
      * Um objeto `BLOBHolder` vazio preenchido pelo método.
      * Um objeto `javax.xml.rpc.holders.StringHolder` vazio preenchido pelo método.
      * Um objeto `BLOBHolder` vazio preenchido pelo método.
      * Um objeto `BLOBHolder` vazio preenchido pelo método.
      * Um objeto `javax.xml.rpc.holders.ShortHolder` vazio preenchido pelo método.
      * Um objeto `MyArrayOf_xsd_anyTypeHolder` vazio preenchido pelo método. Esse parâmetro é usado para armazenar anexos de arquivo enviados junto com o formulário.
      * Um objeto `FormsResultHolder` vazio que é preenchido pelo método com o formulário enviado.

     O método `processFormSubmission` preenche o parâmetro `FormsResultHolder` com os resultados do envio do formulário.

   * Determine se o serviço Forms terminou de processar os dados do formulário invocando o método `getAction` do objeto `FormsResult`. Se esse método retornar o valor `0`, os dados do formulário estarão prontos para serem processados. Você pode obter um objeto `FormsResult` obtendo o valor do membro de dados `value` do objeto `FormsResultHolder`.

1. Determine se o envio do formulário contém anexos de arquivo

   Obtenha o valor do membro de dados `value` do objeto `MyArrayOf_xsd_anyTypeHolder` (o objeto `MyArrayOf_xsd_anyTypeHolder` foi passado para o método `processFormSubmission`). Este membro de dados retorna uma matriz de `Objects`. Cada elemento na matriz `Object` é um `Object` que corresponde aos arquivos enviados junto com o formulário. Você pode obter cada elemento dentro da matriz e convertê-lo em um objeto `BLOB`.

1. Processar os dados enviados

   * Se o tipo de conteúdo de dados for `application/vnd.adobe.xdp+xml` ou `text/xml`, crie uma lógica de aplicativo para recuperar valores de dados XML.

      * Crie um objeto `BLOB` invocando o método `getOutputContent` do objeto `FormsResult`.
      * Crie uma matriz de bytes invocando o método `getBinaryData` do objeto `BLOB`.
      * Crie um objeto `java.io.InputStream` invocando o construtor `java.io.ByteArrayInputStream` e transmitindo a matriz de bytes.
      * Crie um objeto `org.w3c.dom.DocumentBuilderFactory` chamando o método `newInstance` estático do objeto `org.w3c.dom.DocumentBuilderFactory`.
      * Crie um objeto `org.w3c.dom.DocumentBuilder` invocando o método `newDocumentBuilder` do objeto `org.w3c.dom.DocumentBuilderFactory`.
      * Crie um objeto `org.w3c.dom.Document` invocando o método `parse` do objeto `org.w3c.dom.DocumentBuilder` e transmitindo o objeto `java.io.InputStream`.
      * Recupere o valor de cada nó no documento XML. Uma maneira de realizar essa tarefa é criar um método personalizado que aceite dois parâmetros: o objeto `org.w3c.dom.Document` e o nome do nó cujo valor você deseja recuperar. Esse método retorna um valor de string que representa o valor do nó. No exemplo de código que segue esse processo, esse método personalizado é chamado de `getNodeText`. O corpo desse método é mostrado.

   * Se o tipo de conteúdo de dados for `application/pdf`, crie uma lógica de aplicativo para salvar os dados de PDF enviados como um arquivo de PDF.

      * Crie um objeto `BLOB` invocando o método `getOutputContent` do objeto `FormsResult`.
      * Crie uma matriz de bytes invocando o método `getBinaryData` do objeto `BLOB`.
      * Crie um objeto `java.io.File` usando seu construtor público. Certifique-se de especificar PDF como a extensão do nome do arquivo.
      * Crie um objeto `java.io.FileOutputStream` usando seu construtor e transmitindo o objeto `java.io.File`.
      * Preencha o arquivo PDF chamando o método `write` do objeto `java.io.FileOutputStream` e transmitindo a matriz de bytes.

**Consulte também**

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
