---
title: Tratamento de formulários enviados
seo-title: Tratamento de formulários enviados
description: 'null'
seo-description: 'null'
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
translation-type: tm+mt
source-git-commit: b97452eb42275d889a82eb9364b5daf7075fcc41

---


# Tratamento de formulários enviados {#handling-submitted-forms}

Aplicativos baseados na Web que permitem que um usuário preencha formulários interativos exigem que os dados sejam enviados de volta ao servidor. Usando o serviço de Formulários, é possível recuperar os dados inseridos pelo usuário em um formulário interativo. Depois de recuperar os dados, você pode processá-los para atender às suas necessidades comerciais. Por exemplo, você pode armazenar os dados em um banco de dados, enviar os dados para outro aplicativo, enviar os dados para outro serviço, unir os dados em um design de formulário, exibir os dados em um navegador da Web e assim por diante.

Os dados do formulário são enviados ao serviço de Formulários como dados XML ou PDF, que é uma opção definida no Designer. Um formulário enviado como XML permite extrair valores de dados de campo individuais. Ou seja, você pode extrair o valor de cada campo de formulário que o usuário inseriu no formulário. Um formulário enviado como dados PDF são dados binários, não dados XML. É possível salvar o formulário como um arquivo PDF ou enviá-lo para outro serviço. Se você quiser extrair dados de um formulário enviado como XML e, em seguida, usar os dados do formulário para criar um documento PDF, execute outra operação do AEM Forms. (Consulte [Criação de Documentos PDF com dados](/help/forms/developing/creating-pdf-documents-submitted-xml.md)XML enviados)

O diagrama a seguir mostra os dados que estão sendo enviados para um Java Servlet com o nome `HandleData` de um formulário interativo exibido em um navegador da Web.

![hs_hs_handlesubmit](assets/hs_hs_handlesubmit.png)

A tabela a seguir explica as etapas no diagrama.

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
   <td><p>Os dados são enviados para o Servlet <code>HandleData</code> Java como dados XML.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>O <code>HandleData</code> Java Servlet contém a lógica do aplicativo para recuperar os dados.</p></td>
  </tr>
 </tbody>
</table>

## Tratamento de dados XML enviados {#handling-submitted-xml-data}

Quando os dados do formulário são enviados como XML, é possível recuperar dados XML que representam os dados enviados. Todos os campos de formulário são exibidos como nós em um schema XML. Os valores de nó correspondem aos valores preenchidos pelo usuário. Considere um formulário de empréstimo no qual cada campo no formulário aparece como um nó dentro dos dados XML. O valor de cada nó corresponde ao valor que um usuário preenche. Suponha que um usuário preencha o formulário de empréstimo com os dados mostrados no formulário a seguir.

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

A ilustração a seguir mostra os dados XML correspondentes recuperados usando a API do cliente do serviço de formulários.

![hs_hs_loandata](assets/hs_hs_loandata.png)

Os campos no formulário de empréstimo. Esses valores podem ser recuperados usando classes Java XML.

>[!NOTE]
>
>O design de formulário deve ser configurado corretamente no Designer para que os dados sejam enviados como dados XML. Para configurar corretamente o design de formulário para enviar dados XML, verifique se o botão Enviar localizado no design de formulário está definido para enviar dados XML. Para obter informações sobre como configurar o botão Enviar para enviar dados XML, consulte [AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Tratamento de dados PDF enviados {#handling-submitted-pdf-data}

Considere um aplicativo da Web que chama o serviço de Formulários. Depois que o serviço Forms renderiza um formulário PDF interativo para um navegador da Web cliente, o usuário preenche o formulário e o envia como dados PDF. Quando o serviço Forms recebe os dados PDF, ele pode enviar os dados PDF para outro serviço ou salvá-los como um arquivo PDF. O diagrama a seguir mostra o fluxo lógico do aplicativo.

![hs_hs_savingforms](assets/hs_hs_savingforms.png)

A tabela a seguir descreve as etapas neste diagrama.

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
   <td><p>O serviço Forms renderiza um formulário PDF interativo no navegador da Web do cliente.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>O usuário preenche um formulário interativo e clica em um botão Enviar. O formulário é enviado de volta ao serviço Forms como dados PDF. Essa opção está definida no Designer.</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>O serviço Forms salva os dados PDF como um arquivo PDF. </p></td>
  </tr>
 </tbody>
</table>

## Tratamento de dados UTF-16 de URL enviados {#handling-submitted-url-utf-16-data}

Se os dados do formulário forem enviados como URL UTF-16, o computador cliente exigirá o Adobe Reader ou o Acrobat 8.1 ou posterior. Além disso, se o design de formulário contiver um botão Enviar com dados codificados por URL (HTTP Post) e a opção de codificação de dados for UTF-16, o design de formulário deverá ser modificado em um editor de texto, como o Bloco de notas. É possível definir a opção de codificação como `UTF-16LE` ou `UTF-16BE` para o botão Enviar. O Designer não fornece essa funcionalidade.

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Formulários, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

## Resumo das etapas {#summary-of-steps}

Para manipular formulários enviados, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto da API do Forms Client.
1. Recuperar dados do formulário.
1. Determine se o envio do formulário contém anexos de arquivo.
1. Processar os dados enviados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto da API do cliente Forms**

Antes de executar programaticamente uma operação de API do cliente do serviço Forms, é necessário criar um cliente do serviço Forms. Se você estiver usando a API Java, crie um `FormsServiceClient` objeto. Se você estiver usando a API de serviço da Web do Forms, crie um `FormsService` objeto.

**Recuperar dados do formulário**

Para recuperar dados de formulário enviados, chame o `FormsServiceClient` método do `processFormSubmission` objeto. Ao invocar esse método, é necessário especificar o tipo de conteúdo do formulário enviado. Quando os dados são enviados de um navegador da Web cliente para o serviço Forms , eles podem ser enviados como dados XML ou PDF. Para recuperar os dados inseridos nos campos do formulário, eles podem ser enviados como dados XML.

Também é possível recuperar campos de formulário de um formulário enviado como dados PDF definindo as seguintes opções de tempo de execução:

* Passe o seguinte valor para o `processFormSubmission` método como parâmetro de tipo de conteúdo: `CONTENT_TYPE=application/pdf`.
* Defina o valor do `RenderOptionsSpec` objeto como `PDFToXDP``true`
* Defina o valor do `RenderOptionsSpec` objeto como `ExportDataFormat``XMLData`

Especifique o tipo de conteúdo do formulário enviado ao chamar o `processFormSubmission` método. A lista a seguir especifica os valores de tipo de conteúdo aplicáveis:

* **text/xml**: Representa o tipo de conteúdo a ser usado quando um formulário PDF envia dados de formulário como XML.
* **application/x-www-form-urlencoded**: Representa o tipo de conteúdo a ser usado quando um formulário HTML envia dados como XML.
* **application/pdf**: Representa o tipo de conteúdo a ser usado quando um formulário PDF envia dados como PDF.

>[!NOTE]
>
>Você observará que existem três start rápidos correspondentes associados à seção Manuseio de formulários enviados. O start rápido Manipular formulários PDF enviados como PDF usando a API Java demonstra como lidar com dados PDF enviados. O tipo de conteúdo especificado neste start rápido é `application/pdf`. O start rápido Handling PDF forms enviados como XML usando a API Java demonstra como manipular dados XML enviados de um formulário PDF. O tipo de conteúdo especificado neste start rápido é `text/xml`. Da mesma forma, os formulários HTML de manuseio enviados como XML usando o start rápido da API Java demonstram como lidar com dados XML enviados enviados de um formulário HTML. O tipo de conteúdo especificado neste start rápido é application/x-www-form-urlencoded.

Você recupera dados de formulário publicados no serviço Forms e determina seu estado de processamento. Ou seja, quando os dados são submetidos ao serviço Forms, isso não significa necessariamente que o serviço Forms terminou de processar os dados e os dados estão prontos para serem processados. Por exemplo, os dados podem ser enviados ao serviço de Formulários para que um cálculo possa ser executado. Quando o cálculo é concluído, o formulário é renderizado de volta ao usuário com os resultados do cálculo exibidos. Antes de processar os dados enviados, recomenda-se que você determine se o serviço Forms terminou de processar os dados.

O serviço Forms retorna os seguintes valores para indicar se o processamento dos dados foi concluído:

* **0 (Enviar):** Os dados enviados estão prontos para serem processados.
* **1 (Calcular):** O serviço Forms executou uma operação de cálculo nos dados e os resultados devem ser renderizados de volta ao usuário.
* **2 (Validar):** Os dados de formulário validados do serviço Forms e os resultados devem ser renderizados de volta ao usuário.
* **3 (Próximo):** A página atual foi alterada com os resultados que devem ser gravados no aplicativo cliente.
* **4 (Anterior**): A página atual foi alterada com os resultados que devem ser gravados no aplicativo cliente.

>[!NOTE]
>
>Os cálculos e validações devem ser renderizados de volta ao usuário. (Consulte [Cálculo de dados](/help/forms/developing/calculating-form-data.md#calculating-form-data)de formulário.

**Determine se o envio do formulário contém anexos de arquivo**

Os formulários enviados ao serviço de Formulários podem conter anexos de arquivo. Por exemplo, usando o painel de anexos incorporado do Acrobat, um usuário pode selecionar anexos de arquivo para enviar junto com o formulário. Além disso, um usuário também pode selecionar anexos de arquivo usando uma barra de ferramentas HTML que é renderizada com um arquivo HTML.

Depois de determinar se um formulário contém anexos de arquivo, é possível processar os dados. Por exemplo, você pode salvar o anexo de arquivo no sistema de arquivos local.

>[!NOTE]
>
>O formulário deve ser enviado como dados PDF para recuperar anexos de arquivo. Se o formulário for submetido como dados XML, os anexos do arquivo não serão enviados.

**Processar os dados enviados**

Dependendo do tipo de conteúdo dos dados enviados, é possível extrair valores de campo de formulário individuais dos dados XML enviados ou salvar os dados PDF enviados como um arquivo PDF (ou enviá-los para outro serviço). Para extrair campos de formulário individuais, converta dados XML enviados em uma fonte de dados XML e recupere os valores da fonte de dados XML usando `org.w3c.dom` classes.

**Consulte também:**

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Transmissão de Documentos ao serviço de formulários](/help/forms/developing/passing-documents-forms-service.md)

[Criação de Aplicações web que renderizam formulários](/help/forms/developing/creating-web-applications-renders-forms.md)

## Manipular formulários enviados usando a API Java {#handle-submitted-forms-using-the-java-api}

Tratar um formulário enviado usando a API de formulários (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto da API do cliente Forms

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `FormsServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar dados do formulário

   * Para recuperar dados de formulário que foram publicados em um Java Servlet, crie um `com.adobe.idp.Document` objeto usando seu construtor e chamando o `javax.servlet.http.HttpServletResponse` `getInputStream` método do objeto de dentro do construtor.
   * Crie um `RenderOptionsSpec` objeto usando seu construtor. Defina o valor da localidade chamando o método do `RenderOptionsSpec` `setLocale` objeto e transmitindo um valor de string que especifica o valor da localidade.
   >[!NOTE]
   >
   >Você pode instruir o serviço de Formulários a criar dados XDP ou XML a partir de conteúdo PDF enviado, chamando o `RenderOptionsSpec` método do `setPDF2XDP` objeto e transmitindo `true` e também chamando `setXMLData` e transmitindo `true`. Em seguida, é possível invocar o método do `FormsResult` `getOutputXML` objeto para recuperar os dados XML que correspondem aos dados XDP/XML. (O `FormsResult` objeto é retornado pelo `processFormSubmission` método, que é explicado na próxima subetapa.)

   * Chame o método do `FormsServiceClient` objeto `processFormSubmission` e passe os seguintes valores:

      * O `com.adobe.idp.Document` objeto que contém os dados do formulário.
      * Um valor de string que especifica variáveis de ambiente, incluindo todos os cabeçalhos HTTP relevantes. Especifique o tipo de conteúdo a ser tratado. Para manipular dados XML, especifique o seguinte valor de string para esse parâmetro: `CONTENT_TYPE=text/xml`. Para manipular dados PDF, especifique o seguinte valor de string para esse parâmetro: `CONTENT_TYPE=application/pdf`.
      * Um valor de string que especifica o valor do `HTTP_USER_AGENT` cabeçalho, por exemplo, . `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Esse valor de parâmetro é opcional.
      * Um `RenderOptionsSpec` objeto que armazena opções de tempo de execução.
      O `processFormSubmission` método retorna um `FormsResult` objeto que contém os resultados do envio do formulário.

   * Determine se o serviço Forms terminou de processar os dados do formulário chamando o método do `FormsResult` objeto `getAction` . Se esse método retornar o valor `0`, os dados estarão prontos para serem processados.



1. Determine se o envio do formulário contém anexos de arquivo

   * Chame o `FormsResult` método do `getAttachments` objeto. Esse método retorna um `java.util.List` objeto que contém arquivos que foram enviados com o formulário.
   * Itere pelo `java.util.List` objeto para determinar se há anexos de arquivo. Se houver anexos de arquivo, cada elemento será uma `com.adobe.idp.Document` instância. É possível salvar os anexos do arquivo chamando o `com.adobe.idp.Document` método do objeto `copyToFile` e transmitindo um `java.io.File` objeto.
   >[!NOTE]
   >
   >Essa etapa só se aplica se o formulário for enviado como PDF.

1. Processar os dados enviados

   * Se o tipo de conteúdo de dados for `application/vnd.adobe.xdp+xml` ou `text/xml`, crie uma lógica de aplicativo para recuperar valores de dados XML.

      * Crie um `com.adobe.idp.Document` objeto chamando o `FormsResult` método do `getOutputContent` objeto.
      * Crie um `java.io.InputStream` objeto chamando o `java.io.DataInputStream` construtor e transmitindo o `com.adobe.idp.Document` objeto.
      * Crie um `org.w3c.dom.DocumentBuilderFactory` objeto chamando o `org.w3c.dom.DocumentBuilderFactory` método do `newInstance` objeto estático.
      * Crie um `org.w3c.dom.DocumentBuilder` objeto chamando o `org.w3c.dom.DocumentBuilderFactory` método do `newDocumentBuilder` objeto.
      * Crie um `org.w3c.dom.Document` objeto chamando o `org.w3c.dom.DocumentBuilder` método do `parse` objeto e transmitindo o `java.io.InputStream` .
      * Recupere o valor de cada nó dentro do documento XML. Uma maneira de realizar essa tarefa é criar um método personalizado que aceite dois parâmetros: o `org.w3c.dom.Document` objeto e o nome do nó cujo valor você deseja recuperar. Este método retorna um valor de string representando o valor do nó. No exemplo de código que segue esse processo, esse método personalizado é chamado `getNodeText`. O corpo deste método é mostrado.
   * Se o tipo de conteúdo de dados for `application/pdf`, crie a lógica do aplicativo para salvar os dados PDF enviados como um arquivo PDF.

      * Crie um `com.adobe.idp.Document` objeto chamando o `FormsResult` método do `getOutputContent` objeto.
      * Crie um `java.io.File` objeto usando seu construtor público. Certifique-se de especificar PDF como a extensão do nome do arquivo.
      * Preencha o arquivo PDF chamando o `com.adobe.idp.Document` método do objeto `copyToFile` e transmitindo o `java.io.File` objeto.


**Consulte também:**

[Start rápido (modo SOAP): Manuseio de formulários PDF enviados como XML usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[Start rápido (modo SOAP): Tratamento de formulários HTML enviados como XML usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[Start rápido (modo SOAP): Como manipular formulários PDF enviados como PDF usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Tratar dados PDF enviados usando a API de serviço da Web {#handle-submitted-pdf-data-using-the-web-service-api}

Tratar um formulário enviado usando a API de formulários (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto da API do cliente Forms

   Crie um `FormsService` objeto e defina valores de autenticação.

1. Recuperar dados do formulário

   * Para recuperar dados de formulário publicados em um Java Servlet, crie um `BLOB` objeto usando seu construtor.
   * Crie um `java.io.InputStream` objeto chamando o `javax.servlet.http.HttpServletResponse` método do `getInputStream` objeto.
   * Crie um `java.io.ByteArrayOutputStream` objeto usando seu construtor e transmitindo o comprimento do `java.io.InputStream` objeto.
   * Copie o conteúdo do `java.io.InputStream` objeto no `java.io.ByteArrayOutputStream` objeto.
   * Crie uma matriz de bytes chamando o `java.io.ByteArrayOutputStream` método do `toByteArray` objeto.
   * Preencha o `BLOB` objeto chamando seu `setBinaryData` método e transmitindo a matriz de bytes como um argumento.
   * Crie um `RenderOptionsSpec` objeto usando seu construtor. Defina o valor da localidade chamando o método do `RenderOptionsSpec` `setLocale` objeto e transmitindo um valor de string que especifica o valor da localidade.
   * Chame o método do `FormsService` objeto `processFormSubmission` e passe os seguintes valores:

      * O `BLOB` objeto que contém os dados do formulário.
      * Um valor de string que especifica variáveis de ambiente, incluindo todos os cabeçalhos HTTP relevantes. Especifique o tipo de conteúdo a ser tratado. Para manipular dados XML, especifique o seguinte valor de string para esse parâmetro: `CONTENT_TYPE=text/xml`. Para manipular dados PDF, especifique o seguinte valor de string para esse parâmetro: `CONTENT_TYPE=application/pdf`.
      * Um valor de string que especifica o valor do `HTTP_USER_AGENT` cabeçalho; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Um `RenderOptionsSpec` objeto que armazena opções de tempo de execução.
      * Um `BLOBHolder` objeto vazio que é preenchido pelo método.
      * Um `javax.xml.rpc.holders.StringHolder` objeto vazio que é preenchido pelo método.
      * Um `BLOBHolder` objeto vazio que é preenchido pelo método.
      * Um `BLOBHolder` objeto vazio que é preenchido pelo método.
      * Um `javax.xml.rpc.holders.ShortHolder` objeto vazio que é preenchido pelo método.
      * Um `MyArrayOf_xsd_anyTypeHolder` objeto vazio que é preenchido pelo método. Esse parâmetro é usado para armazenar anexos de arquivo enviados junto com o formulário.
      * Um `FormsResultHolder` objeto vazio que é preenchido pelo método com o formulário enviado.
      O `processFormSubmission` método preenche o `FormsResultHolder` parâmetro com os resultados do envio do formulário.

   * Determine se o serviço Forms terminou de processar os dados do formulário chamando o método do `FormsResult` objeto `getAction` . Se esse método retornar o valor `0`, os dados do formulário estarão prontos para serem processados. Você pode obter um `FormsResult` objeto obtendo o valor do membro de `FormsResultHolder` dados do `value` objeto.


1. Determine se o envio do formulário contém anexos de arquivo

   Obtenha o valor do membro de `MyArrayOf_xsd_anyTypeHolder` dados do `value` objeto (o `MyArrayOf_xsd_anyTypeHolder` objeto foi passado para o `processFormSubmission` método). Esse membro de dados retorna uma matriz de `Objects`. Cada elemento dentro da `Object` matriz é um elemento `Object`que corresponde aos arquivos que foram enviados junto com o formulário. É possível obter cada elemento dentro da matriz e convertê-lo em um `BLOB` objeto.

1. Processar os dados enviados

   * Se o tipo de conteúdo de dados for `application/vnd.adobe.xdp+xml` ou `text/xml`, crie uma lógica de aplicativo para recuperar valores de dados XML.

      * Crie um `BLOB` objeto chamando o `FormsResult` método do `getOutputContent` objeto.
      * Crie uma matriz de bytes chamando o `BLOB` método do `getBinaryData` objeto.
      * Crie um `java.io.InputStream` objeto chamando o `java.io.ByteArrayInputStream` construtor e transmitindo a matriz de bytes.
      * Crie um `org.w3c.dom.DocumentBuilderFactory` objeto chamando o `org.w3c.dom.DocumentBuilderFactory` método do `newInstance` objeto estático.
      * Crie um `org.w3c.dom.DocumentBuilder` objeto chamando o `org.w3c.dom.DocumentBuilderFactory` método do `newDocumentBuilder` objeto.
      * Crie um `org.w3c.dom.Document` objeto chamando o `org.w3c.dom.DocumentBuilder` método do `parse` objeto e transmitindo o `java.io.InputStream` .
      * Recupere o valor de cada nó dentro do documento XML. Uma maneira de realizar essa tarefa é criar um método personalizado que aceite dois parâmetros: o `org.w3c.dom.Document` objeto e o nome do nó cujo valor você deseja recuperar. Este método retorna um valor de string representando o valor do nó. No exemplo de código que segue esse processo, esse método personalizado é chamado `getNodeText`. O corpo deste método é mostrado.
   * Se o tipo de conteúdo de dados for `application/pdf`, crie a lógica do aplicativo para salvar os dados PDF enviados como um arquivo PDF.

      * Crie um `BLOB` objeto chamando o `FormsResult` método do `getOutputContent` objeto.
      * Crie uma matriz de bytes chamando o `BLOB` método do `getBinaryData` objeto.
      * Crie um `java.io.File` objeto usando seu construtor público. Certifique-se de especificar PDF como a extensão do nome do arquivo.
      * Crie um `java.io.FileOutputStream` objeto usando seu construtor e transmitindo o `java.io.File` objeto.
      * Preencha o arquivo PDF chamando o método do `java.io.FileOutputStream` objeto `write` e transmitindo a matriz de bytes.


**Consulte também:**

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)