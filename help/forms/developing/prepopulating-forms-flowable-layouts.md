---
title: Prepopulating Forms with Flowable Layouts
seo-title: Prepopulating Forms with Flowable Layouts
description: 'null'
seo-description: 'null'
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
translation-type: tm+mt
source-git-commit: ebb60e79aa7fb45e059e2d2451f6d549cd24b8b0

---


# Prepopulating Forms with Flowable Layouts {#prepopulating-forms-with-flowable-layouts1}

## Prepopulating Forms with Flowable Layouts {#prepopulating-forms-with-flowable-layouts2}

Prepopulating forms displays data to users within a rendered form. For example, assume a user logs in to a website with a user name and password. If authentication is successful, the client application queries a database for user information. Os dados são unidos ao formulário e, em seguida, ele é renderizado ao usuário. As a result, the user is able to view personalized data within the form.

Prepopulating a form has the following advantages:

* Permite que o usuário exiba dados personalizados em um formulário.
* Reduz a quantidade de digitação que o usuário faz para preencher um formulário.
* Garante integridade dos dados por meio do controle de onde os dados são colocados.

As duas fontes de dados XML a seguir podem pré-preencher um formulário:

* An XDP data source, which is XML that conforms to XFA syntax (or XFDF data to prepopulate a form created using Acrobat).
* An arbitrary XML data source that contains name/value pairs matching the form’s field names (the examples in this section use an arbitrary XML data source).

An XML element must exist for every form field that you want to prepopulate. The XML element name must match the field name. An XML element is ignored if it does not correspond to a form field or if the XML element name does not match the field name. It is not necessary to match the order in which the XML elements are displayed, as long as all XML elements are specified.

When you prepopulate a form that already contains data, you must specify the data that is already displayed within the XML data source. Assume that a form containing 10 fields has data in four fields. Next, assume that you want to prepopulate the remaining six fields. In this situation, you must specify 10 XML elements in the XML data source that is used to prepopulate the form. Se você especificar apenas seis elementos, os quatro campos originais ficarão vazios.

Por exemplo, é possível pré-preencher um formulário, como o formulário de confirmação de amostra. (Consulte &quot;Formulário de confirmação&quot; na [renderização de formulários](/help/forms/developing/rendering-interactive-pdf-forms.md)PDF interativos.)

Para pré-preencher o formulário de confirmação de amostra, é necessário criar uma fonte de dados XML que contenha três elementos XML que correspondam aos três campos no formulário. Este formulário contém os três campos a seguir: `FirstName`, `LastName`e `Amount`. A primeira etapa é criar uma fonte de dados XML que contenha elementos XML correspondentes aos campos localizados no design de formulário. A próxima etapa é atribuir valores de dados aos elementos XML, como mostrado no código XML a seguir.

```as3
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

Depois de pré-preencher o formulário de confirmação com essa fonte de dados XML e, em seguida, renderizar o formulário, os valores de dados atribuídos aos elementos XML serão exibidos, conforme mostrado no diagrama a seguir.

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### Prepopulating forms with flowable layouts {#prepopulating_forms_with_flowable_layouts-1}

Formulários com layouts flutuantes são úteis para exibir uma quantidade indeterminada de dados aos usuários. Because the layout of the form adjusts automatically to the amount of data that is merged, you do not need to predetermine a fixed layout or number of pages for the form as you need to do with a form with a fixed layout.

A form is typically populated with data that is obtained during run-time. As a result, you can prepopulate a form by creating an in-memory XML data source and placing the data directly into the in-memory XML data source.

Consider a web-based application, such as an online store. After an online shopper finishes purchasing items, all purchased items are placed into an in-memory XML data source that is used to prepopulate a form. The following diagram shows this process, which is explained in the table following the diagram.

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

The following table describes the steps in this diagram.

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
   <td><p>A user purchases items from a web-based online store. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>After the user finishes purchasing items and clicks the Submit button, an in-memory XML data source is created. Os itens comprados e as informações do usuário são colocados na fonte de dados XML na memória. </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>The XML data source is used to prepopulate a purchase order form (an example of this form is shown following this table). </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>O formulário de pedido de compra é renderizado no navegador da Web do cliente. </p></td>
  </tr>
 </tbody>
</table>

The following diagram shows an example of a purchase order form. As informações na tabela podem se ajustar ao número de registros nos dados XML.

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>Um formulário pode ser pré-preenchido com dados de outras fontes, como um banco de dados corporativo ou aplicativos externos.

### Considerações sobre design de formulário {#form-design-considerations}

Formulários com layouts flutuantes são baseados em designs de formulário criados no Designer. Um design de formulário especifica um conjunto de regras de layout, apresentação e captura de dados, incluindo o cálculo de valores com base na entrada do usuário. As regras são aplicadas quando os dados são inseridos em um formulário. Os campos adicionados a um formulário são subformulários que estão dentro do design de formulário. For example, in the purchase order form shown in the previous diagram, each line is a subform. For information about creating a form design that contains subforms, see [Creating a purchase order form that has a flowable layout](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9).

### Understanding data subgroups {#understanding-data-subgroups}

An XML data source is used to prepopulate forms with fixed layouts and flowable layouts. No entanto, a diferença é que uma fonte de dados XML que pré-preenche um formulário com um layout flutuante contém elementos XML repetitivos usados para pré-preencher subformulários repetidos no formulário. These repeating XML elements are called data subgroups.

Uma fonte de dados XML usada para pré-preencher o formulário de pedido de compra mostrado no diagrama anterior contém quatro subgrupos de dados repetitivos. Each data subgroup corresponds to a purchased item. Os itens comprados são um monitor, uma lâmpada de mesa, um telefone e um catálogo de endereços.

The following XML data source is used to prepopulate the purchase order form.

```as3
     <header>
         <!-- XML elements used to prepopulate non-repeating fields such as address
         <!and city
         <txtPONum>8745236985</txtPONum>
         <dtmDate>2004-02-08</dtmDate>
         <txtOrderedByCompanyName>Any Company Name</txtOrderedByCompanyName>
         <txtOrderedByAddress>555, Any Blvd.</txtOrderedByAddress>
         <txtOrderedByCity>Any City</txtOrderedByCity>
         <txtOrderedByStateProv>ST</txtOrderedByStateProv>
         <txtOrderedByZipCode>12345</txtOrderedByZipCode>
         <txtOrderedByCountry>Any Country</txtOrderedByCountry>
         <txtOrderedByPhone>(123) 456-7890</txtOrderedByPhone>
         <txtOrderedByFax>(123) 456-7899</txtOrderedByFax>
         <txtOrderedByContactName>Contact Name</txtOrderedByContactName>
         <txtDeliverToCompanyName>Any Company Name</txtDeliverToCompanyName>
         <txtDeliverToAddress>7895, Any Street</txtDeliverToAddress>
         <txtDeliverToCity>Any City</txtDeliverToCity>
         <txtDeliverToStateProv>ST</txtDeliverToStateProv>
         <txtDeliverToZipCode>12346</txtDeliverToZipCode>
         <txtDeliverToCountry>Any Country</txtDeliverToCountry>
         <txtDeliverToPhone>(123) 456-7891</txtDeliverToPhone>
         <txtDeliverToFax>(123) 456-7899</txtDeliverToFax>
         <txtDeliverToContactName>Contact Name</txtDeliverToContactName>
     </header>
     <detail>
         <!-- A data subgroup that contains information about the monitor>
         <txtPartNum>00010-100</txtPartNum>
         <txtDescription>Monitor</txtDescription>
         <numQty>1</numQty>
         <numUnitPrice>350.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the desk lamp>
         <txtPartNum>00010-200</txtPartNum>
         <txtDescription>Desk lamps</txtDescription>
         <numQty>3</numQty>
         <numUnitPrice>55.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the Phone>
             <txtPartNum>00025-275</txtPartNum>
             <txtDescription>Phone</txtDescription>
             <numQty>5</numQty>
             <numUnitPrice>85.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the address book>
         <txtPartNum>00300-896</txtPartNum>
         <txtDescription>Address book</txtDescription>
         <numQty>2</numQty>
         <numUnitPrice>15.00</numUnitPrice>
     </detail>
```

Notice that each data subgroup contains four XML elements that correspond to this information:

* Items part number
* Items description
* Quantity of items
* Unit price

The name of a data subgroup’s parent XML element must match the name of the subform that is located in the form design. For example, in the previous diagram, notice that the name of the data subgroup’s parent XML element is `detail`. This corresponds to the name of the subform that is located in the form design on which the purchase order form is based. If the name of the data subgroup’s parent XML element and the subform do not match, a server-side form is not prepopulated.

Each data subgroup must contain XML elements that match the field names in the subform. The `detail` subform located in the form design contains the following fields:

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>Se você tentar pré-preencher um formulário com uma fonte de dados que contenha elementos XML repetitivos e definir a `RenderAtClient` opção como `No`, somente o primeiro registro de dados será unido ao formulário. Para garantir que todos os registros de dados sejam mesclados no formulário, defina `RenderAtClient` como `Yes`. For information about the `RenderAtClient` option, see [Rendering Forms at the Client](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>Para obter mais informações sobre o serviço de Formulários, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

### Resumo das etapas {#summary-of-steps}

Para pré-preencher um formulário com um layout flutuante, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie uma fonte de dados XML na memória.
1. Convert the XML data source.
1. Renderize um formulário pré-preenchido.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Create an in-memory XML data source**

You can use `org.w3c.dom` classes to create an in-memory XML data source to prepopulate a form with a flowable layout. You must place data into an XML data source that conforms to the form. For information about the relationship between a form with a flowable layout and the XML data source, see [Understanding data subgroups](#understanding-data-subgroups).

**Converter a fonte de dados XML**

An in-memory XML data source that is created by using `org.w3c.dom` classes can be converted to a `com.adobe.idp.Document` object before it can be used to prepopulate a form. Uma fonte de dados XML na memória pode ser convertida usando classes de transformação Java XML.

>[!NOTE]
>
>Se você estiver usando o WSDL do serviço Forms para pré-preencher um formulário, é necessário converter um `org.w3c.dom.Document` objeto em um `BLOB` objeto.

**Render a prepopulated form**

You render a prepopulated form just like other form. A única diferença é que você usa o `com.adobe.idp.Document` objeto que contém a fonte de dados XML para pré-preencher o formulário.

**Consulte também:**

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Como renderizar formulários PDF interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Criação de Aplicações web que renderizam formulários](/help/forms/developing/creating-web-applications-renders-forms.md)

### Pré-preenchimento de formulários usando a API Java {#prepopulating-forms-using-the-java-api}

Para pré-preencher um formulário com um layout flutuante usando a API de formulários (Java), execute as seguintes etapas:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java. For information about the location of these files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Create an in-memory XML data source

   * Crie um objeto Java `DocumentBuilderFactory` chamando o `DocumentBuilderFactory` método da classe `newInstance` .
   * Crie um objeto Java `DocumentBuilder` chamando o `DocumentBuilderFactory` método do `newDocumentBuilder` objeto.
   * Chame o `DocumentBuilder` método do `newDocument` objeto para instanciar um `org.w3c.dom.Document` objeto.
   * Crie o elemento raiz da fonte de dados XML chamando o `org.w3c.dom.Document` método do `createElement` objeto. Isso cria um `Element` objeto que representa o elemento raiz. Pass a string value representing the name of the element to the `createElement` method. Converta o valor de retorno em `Element`. Next, append the root element to the document by calling the `Document` object’s `appendChild` method, and pass the root element object as an argument. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Create the XML data source’s header element by calling the `Document` object’s `createElement` method. Pass a string value representing the name of the element to the `createElement` method. Converta o valor de retorno em `Element`. Next, append the header element to the root element by calling the `root` object’s `appendChild` method, and pass the header element object as an argument. Os elementos XML anexados ao elemento header correspondem à parte estática do formulário. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Crie um elemento filho que pertença ao elemento header chamando o `Document` método do `createElement` objeto e transmita um valor de string que representa o nome do elemento. Converta o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho chamando seu `appendChild` método e transmita o `Document` `createTextNode` método do objeto como um argumento. Especifique um valor de string que apareça como o valor do elemento filho. Por fim, acrescente o elemento filho ao elemento header chamando o `appendChild` método do elemento header e passe o objeto de elemento filho como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * Adicione todos os elementos restantes ao elemento header repetindo a última subetapa para cada campo que aparece na parte estática do formulário (no diagrama da fonte de dados XML, esses campos são mostrados na seção A. (Consulte [Entendendo subgrupos](#understanding-data-subgroups)de dados.)
   * Crie o elemento detail da fonte de dados XML chamando o `Document` método do `createElement` objeto. Passe um valor de string representando o nome do elemento para o `createElement` método. Converta o valor de retorno em `Element`. Em seguida, anexe o elemento detail ao elemento raiz, chamando o método do `root` objeto `appendChild` , e passe o objeto detail element como um argumento. Os elementos XML anexados ao elemento detail correspondem à parte dinâmica do formulário. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Crie um elemento filho que pertence ao elemento detail chamando o `Document` método do `createElement` objeto e transmita um valor de string que representa o nome do elemento. Converta o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho chamando seu `appendChild` método e transmita o `Document` `createTextNode` método do objeto como um argumento. Especifique um valor de string que apareça como o valor do elemento filho. Finalmente, acrescente o elemento filho ao elemento detail chamando o `appendChild` método do elemento detail e transmita o objeto de elemento filho como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita a última subetapa para que todos os elementos XML sejam anexados ao elemento detail. Para criar corretamente a fonte de dados XML usada para preencher o formulário de pedido de compra, acrescente os seguintes elementos XML ao elemento detail: `txtDescription`, `numQty`e `numUnitPrice`.
   * Repita as duas últimas subetapas para todos os itens de dados usados para pré-preencher o formulário.

1. Converter a fonte de dados XML

   * Crie um `javax.xml.transform.Transformer` objeto chamando o `javax.xml.transform.Transformer` método estático do `newInstance` objeto.
   * Crie um `Transformer` objeto chamando o `TransformerFactory` método do `newTransformer` objeto.
   * Crie um `ByteArrayOutputStream` objeto usando seu construtor.
   * Crie um `javax.xml.transform.dom.DOMSource` objeto usando seu construtor e transmitindo o `org.w3c.dom.Document` objeto criado na etapa 1.
   * Crie um `javax.xml.transform.dom.DOMSource` objeto usando seu construtor e transmitindo o `ByteArrayOutputStream` objeto.
   * Preencha o objeto Java `ByteArrayOutputStream` chamando o método do `javax.xml.transform.Transformer` objeto e transmitindo os objetos `transform` e os `javax.xml.transform.dom.DOMSource` `javax.xml.transform.stream.StreamResult` .
   * Crie uma matriz de bytes e aloque o tamanho do `ByteArrayOutputStream` objeto na matriz de bytes.
   * Preencha a matriz de bytes chamando o `ByteArrayOutputStream` método do `toByteArray` objeto.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo a matriz de bytes.

1. Renderizar um formulário pré-preenchido

   Chame o método do `FormsServiceClient` objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo.
   * Um `com.adobe.idp.Document` objeto que contém dados para mesclar com o formulário. Certifique-se de usar o `com.adobe.idp.Document` objeto criado nas etapas um e dois.
   * Um `PDFFormRenderSpec` objeto que armazena opções de tempo de execução.
   * Um `URLSpec` objeto que contém valores de URI exigidos pelo serviço de Formulários.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

   * Crie um `javax.servlet.ServletOutputStream` objeto usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um `com.adobe.idp.Document` objeto chamando o `FormsResult` método do objeto `getOutputContent` .
   * Crie um `java.io.InputStream` objeto chamando o `com.adobe.idp.Document` método do `getInputStream` objeto.
   * Crie uma matriz de bytes para preenchê-la com o fluxo de dados do formulário, chamando o método do `InputStream` objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` `write` do objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.


**Consulte também:**

[Start rápido (modo SOAP): Pré-preenchimento de formulários com layouts flutuantes usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Pré-preenchimento de formulários usando a API de serviço da Web {#prepopulating-forms-using-the-web-service-api}

Para pré-preencher um formulário com um layout flutuante usando a API de formulários (serviço da Web), execute as seguintes etapas:

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL. (Consulte [Criação de classes proxy Java usando o Apache Axis](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * Inclua as classes proxy Java no caminho da classe.

1. Criar uma fonte de dados XML na memória

   * Crie um objeto Java `DocumentBuilderFactory` chamando o `DocumentBuilderFactory` método da classe `newInstance` .
   * Crie um objeto Java `DocumentBuilder` chamando o `DocumentBuilderFactory` método do `newDocumentBuilder` objeto.
   * Chame o `DocumentBuilder` método do `newDocument` objeto para instanciar um `org.w3c.dom.Document` objeto.
   * Crie o elemento raiz da fonte de dados XML chamando o `org.w3c.dom.Document` método do `createElement` objeto. Isso cria um `Element` objeto que representa o elemento raiz. Passe um valor de string representando o nome do elemento para o `createElement` método. Converta o valor de retorno em `Element`. Em seguida, acrescente o elemento raiz ao documento chamando o método do `Document` objeto `appendChild` e transmita o objeto do elemento raiz como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Crie o elemento de cabeçalho da fonte de dados XML chamando o `Document` método do `createElement` objeto. Passe um valor de string representando o nome do elemento para o `createElement` método. Converta o valor de retorno em `Element`. Em seguida, acrescente o elemento header ao elemento raiz, chamando o método do `root` objeto `appendChild` , e passe o objeto do elemento header como um argumento. Os elementos XML anexados ao elemento header correspondem à parte estática do formulário. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Crie um elemento filho que pertença ao elemento header chamando o `Document` método do `createElement` objeto e transmita um valor de string que representa o nome do elemento. Converta o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho chamando seu `appendChild` método e transmita o `Document` `createTextNode` método do objeto como um argumento. Especifique um valor de string que apareça como o valor do elemento filho. Por fim, acrescente o elemento filho ao elemento header chamando o `appendChild` método do elemento header e passe o objeto de elemento filho como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * Adicione todos os elementos restantes ao elemento header repetindo a última subetapa para cada campo que aparece na parte estática do formulário (no diagrama da fonte de dados XML, esses campos são mostrados na seção A. (Consulte [Entendendo subgrupos](#understanding-data-subgroups)de dados.)
   * Crie o elemento detail da fonte de dados XML chamando o `Document` método do `createElement` objeto. Passe um valor de string representando o nome do elemento para o `createElement` método. Converta o valor de retorno em `Element`. Em seguida, anexe o elemento detail ao elemento raiz, chamando o método do `root` objeto `appendChild` , e passe o objeto detail element como um argumento. Os elementos XML anexados ao elemento detail correspondem à parte dinâmica do formulário. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Crie um elemento filho que pertence ao elemento detail chamando o `Document` método do `createElement` objeto e transmita um valor de string que representa o nome do elemento. Converta o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho chamando seu `appendChild` método e transmita o `Document` `createTextNode` método do objeto como um argumento. Especifique um valor de string que apareça como o valor do elemento filho. Finalmente, acrescente o elemento filho ao elemento detail chamando o `appendChild` método do elemento detail e transmita o objeto de elemento filho como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita a última subetapa para que todos os elementos XML sejam anexados ao elemento detail. Para criar corretamente a fonte de dados XML usada para preencher o formulário de pedido de compra, acrescente os seguintes elementos XML ao elemento detail: `txtDescription`, `numQty`e `numUnitPrice`.
   * Repita as duas últimas subetapas para todos os itens de dados usados para pré-preencher o formulário.

1. Converter a fonte de dados XML

   * Crie um `javax.xml.transform.Transformer` objeto chamando o `javax.xml.transform.Transformer` método estático do `newInstance` objeto.
   * Crie um `Transformer` objeto chamando o `TransformerFactory` método do `newTransformer` objeto.
   * Crie um `ByteArrayOutputStream` objeto usando seu construtor.
   * Crie um `javax.xml.transform.dom.DOMSource` objeto usando seu construtor e transmitindo o `org.w3c.dom.Document` objeto criado na etapa 1.
   * Crie um `javax.xml.transform.dom.DOMSource` objeto usando seu construtor e transmitindo o `ByteArrayOutputStream` objeto.
   * Preencha o objeto Java `ByteArrayOutputStream` chamando o método do `javax.xml.transform.Transformer` objeto e transmitindo os objetos `transform` e os `javax.xml.transform.dom.DOMSource` `javax.xml.transform.stream.StreamResult` .
   * Crie uma matriz de bytes e aloque o tamanho do `ByteArrayOutputStream` objeto na matriz de bytes.
   * Preencha a matriz de bytes chamando o `ByteArrayOutputStream` método do `toByteArray` objeto.
   * Crie um `BLOB` objeto usando seu construtor e chame seu `setBinaryData` método e passe a matriz de bytes.

1. Renderizar um formulário pré-preenchido

   Chame o método do `FormsService` objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo.
   * Um `BLOB` objeto que contém dados para mesclar com o formulário. Certifique-se de usar o `BLOB` objeto criado nas etapas um e dois.
   * Um `PDFFormRenderSpecc` objeto que armazena opções de tempo de execução. Para obter mais informações, consulte Referência [da API de formulários](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM.
   * Um `URLSpec` objeto que contém valores de URI exigidos pelo serviço de Formulários.
   * Um `java.util.HashMap` objeto que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não deseja anexar arquivos ao formulário.
   * Um `com.adobe.idp.services.holders.BLOBHolder` objeto vazio que é preenchido pelo método. Isso é usado para armazenar o formulário PDF renderizado.
   * Um `javax.xml.rpc.holders.LongHolder` objeto vazio que é preenchido pelo método. (Esse argumento armazenará o número de páginas no formulário).
   * Um `javax.xml.rpc.holders.StringHolder` objeto vazio que é preenchido pelo método. (Esse argumento armazenará o valor da localidade).
   * Um `com.adobe.idp.services.holders.FormsResultHolder` objeto vazio que conterá os resultados dessa operação.
   O `renderPDFForm` método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

   * Crie um `FormResult` objeto obtendo o valor do membro de `com.adobe.idp.services.holders.FormsResultHolder` dados do `value` objeto.
   * Crie um `BLOB` objeto que contenha dados de formulário chamando o `FormsResult` método do `getOutputContent` objeto.
   * Obtenha o tipo de conteúdo do `BLOB` objeto chamando seu `getContentType` método.
   * Defina o tipo de conteúdo do `javax.servlet.http.HttpServletResponse` objeto chamando seu `setContentType` método e transmitindo o tipo de conteúdo do `BLOB` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web do cliente, chamando o `javax.servlet.http.HttpServletResponse` `getOutputStream` método do objeto.
   * Crie uma matriz de bytes e preencha-a chamando o método do `BLOB` objeto `getBinaryData` . Essa tarefa atribui o conteúdo do `FormsResult` objeto à matriz de bytes.
   * Chame o método do `javax.servlet.http.HttpServletResponse` `write` objeto para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o `write` método.
   >[!NOTE]
   >
   >O `renderPDFForm` método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

**Consulte também:**

[Invocar formulários AEM usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

