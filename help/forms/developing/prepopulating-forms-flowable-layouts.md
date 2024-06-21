---
title: Pré-preenchimento do Forms com layouts fluíveis
description: Preencha previamente os formulários com layout fluível para exibir dados aos usuários em um formulário renderizado usando a API Java e a API de serviço da Web.
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: ff087084-fb1c-43a4-ae54-cc77eb862493
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '3478'
ht-degree: 0%

---

# Pré-preenchimento do Forms com layouts fluíveis {#prepopulating-forms-with-flowable-layouts1}

## Pré-preenchimento do Forms com layouts fluíveis {#prepopulating-forms-with-flowable-layouts2}

O pré-preenchimento de formulários exibe dados para usuários em um formulário renderizado. Por exemplo, suponha que um usuário faça logon em um site com um nome de usuário e senha. Se a autenticação for bem-sucedida, o aplicativo cliente consultará um banco de dados para obter informações sobre o usuário. Os dados são mesclados no formulário e em seguida o formulário é renderizado para o usuário. Como resultado, o usuário pode visualizar dados personalizados no formulário.

O pré-preenchimento de um formulário tem as seguintes vantagens:

* Permite que o usuário visualize dados personalizados em um formulário.
* Reduz a quantidade de digitação que o usuário faz para preencher um formulário.
* Garante a integridade dos dados, tendo controle sobre onde eles são colocados.

As duas fontes de dados XML a seguir podem preencher previamente um formulário:

* Uma fonte de dados XDP, que é um XML que está em conformidade com a sintaxe XFA (ou dados XFDF para preencher previamente um formulário criado usando o Acrobat).
* Uma fonte de dados XML arbitrária que contém pares de nome/valor correspondentes aos nomes de campo do formulário (os exemplos nesta seção usam uma fonte de dados XML arbitrária).

Um elemento XML deve existir para cada campo de formulário que você deseja preencher previamente. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML será ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos, desde que todos os elementos XML sejam especificados.

Quando você preenche um formulário que já contém dados, deve especificar os dados que já são exibidos na fonte de dados XML. Suponha que um formulário contendo 10 campos tenha dados em quatro campos. Em seguida, suponha que você queira preencher previamente os seis campos restantes. Nessa situação, você deve especificar 10 elementos XML na fonte de dados XML usada para preencher previamente o formulário. Se você especificar apenas seis elementos, os quatro campos originais estarão vazios.

Por exemplo, você pode preencher previamente um formulário, como o formulário de confirmação de amostra. (Consulte &quot;Formulário de confirmação&quot; em [Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md).)

Para preencher previamente o formulário de confirmação de amostra, é necessário criar uma fonte de dados XML que contenha três elementos XML que correspondam aos três campos no formulário. Este formulário contém os três campos a seguir: `FirstName`, `LastName`, e `Amount`. A primeira etapa é criar uma fonte de dados XML que contenha elementos XML que correspondam aos campos no design do formulário. A próxima etapa é atribuir valores de dados aos elementos XML, conforme mostrado no código XML a seguir.

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

Depois de preencher previamente o formulário de confirmação com essa fonte de dados XML e, em seguida, renderizar o formulário, os valores de dados atribuídos aos elementos XML serão exibidos, como mostrado no diagrama a seguir.

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### Pré-preenchimento de formulários com layouts fluíveis {#prepopulating_forms_with_flowable_layouts-1}

O Forms com layouts fluíveis é útil para exibir uma quantidade indeterminada de dados para os usuários. Como o layout do formulário se ajusta automaticamente à quantidade de dados mesclados, não é necessário predeterminar um layout fixo ou um número de páginas para o formulário, conforme necessário para um formulário com layout fixo.

Um formulário normalmente é preenchido com dados obtidos durante o tempo de execução. Como resultado, você pode preencher previamente um formulário criando uma fonte de dados XML na memória e colocando os dados diretamente na fonte de dados XML na memória.

Considere um aplicativo baseado na Web, como uma loja online. Depois que um comprador online conclui a compra de itens, todos os itens comprados são colocados em uma fonte de dados XML na memória usada para preencher previamente um formulário. O diagrama a seguir mostra esse processo, que é explicado na tabela abaixo do diagrama.

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

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
   <td><p>Um usuário compra itens de uma loja online baseada na Web. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Depois que o usuário terminar de comprar itens e clicar no botão Enviar, uma fonte de dados XML na memória será criada. Os itens comprados e as informações do usuário são colocados na fonte de dados XML na memória. </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>A fonte de dados XML é usada para preencher previamente um formulário de ordem de compra (um exemplo desse formulário é mostrado após esta tabela). </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>O formulário de ordem de compra é renderizado no navegador da Web do cliente. </p></td>
  </tr>
 </tbody>
</table>

O diagrama a seguir mostra um exemplo de um form de ordem de compra. As informações na tabela podem se ajustar ao número de registros nos dados XML.

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>Um formulário pode ser pré-preenchido com dados de outras fontes, como um banco de dados empresarial ou aplicativos externos.

### Considerações de design do formulário {#form-design-considerations}

O Forms com layouts fluíveis é baseado em designs de formulário criados no Designer. Um design de formulário especifica um conjunto de regras de layout, apresentação e captura de dados, incluindo o cálculo de valores com base na entrada do usuário. As regras são aplicadas quando os dados são inseridos em um formulário. Os campos adicionados a um formulário são subformulários que estão dentro do design do formulário. Por exemplo, no formulário de ordem de compra mostrado no diagrama anterior, cada linha é um subformulário. Para obter informações sobre como criar um design de formulário que contenha subformulários, consulte [Criando um formulário de ordem de compra com um layout de fluxo](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9).

### Entender subgrupos de dados {#understanding-data-subgroups}

Uma fonte de dados XML é usada para preencher formulários previamente com layouts fixos e layouts fluíveis. No entanto, a diferença é que uma fonte de dados XML que preenche um formulário com um layout fluível contém elementos XML repetidos que são usados para preencher previamente subformulários que são repetidos dentro do formulário. Esses elementos XML repetidos são chamados de subgrupos de dados.

Uma fonte de dados XML usada para preencher previamente o formulário de ordem de compra mostrado no diagrama anterior contém quatro subgrupos de dados repetidos. Cada subgrupo de dados corresponde a um item comprado. Os itens comprados são um monitor, uma lâmpada de mesa, um telefone e uma lista de endereços.

A fonte de dados XML a seguir é usada para preencher previamente o formulário de ordem de compra.

```xml
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

Observe que cada subgrupo de dados contém quatro elementos XML que correspondem a essas informações:

* Número de peça dos itens
* Descrição dos itens
* Quantidade de itens
* Preço unitário

O nome do elemento XML pai de um subgrupo de dados deve corresponder ao nome do subformulário que está no design do formulário. Por exemplo, no diagrama anterior, observe que o nome do elemento XML pai do subgrupo de dados é `detail`. Isso corresponde ao nome do subformulário que está no design do formulário no qual o formulário de ordem de compra se baseia. Se o nome do elemento XML pai do subgrupo de dados e o subformulário não corresponderem, um formulário do lado do servidor não será pré-preenchido.

Cada subgrupo de dados deve conter elementos XML que correspondam aos nomes de campo no subformulário. A variável `detail` o subformulário no design do formulário contém os seguintes campos:

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>Se você tentar preencher previamente um formulário com uma fonte de dados que contenha elementos XML repetidos e definir a variável `RenderAtClient` opção para `No`, somente o primeiro registro de dados é mesclado ao formulário. Para garantir que todos os registros de dados sejam mesclados no formulário, defina o `RenderAtClient` para `Yes`. Para obter informações sobre o `RenderAtClient` , consulte [Renderização do Forms no cliente](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para preencher previamente um formulário com um layout fluível, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie uma fonte de dados XML na memória.
1. Converta a fonte de dados XML.
1. Renderize um formulário pré-preenchido.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar uma fonte de dados XML na memória**

Você pode usar `org.w3c.dom` para criar uma fonte de dados XML na memória para preencher previamente um formulário com um layout fluível. Insira os dados em uma fonte de dados XML que esteja em conformidade com o formulário. Para obter informações sobre a relação entre um formulário com um layout fluível e a fonte de dados XML, consulte [Entender subgrupos de dados](#understanding-data-subgroups).

**Converter a fonte de dados XML**

Uma fonte de dados XML na memória criada com o uso de `org.w3c.dom` as classes podem ser convertidas em um `com.adobe.idp.Document` antes de poder ser usado para preencher um formulário previamente. Uma fonte de dados XML na memória pode ser convertida usando classes de transformação Java XML.

>[!NOTE]
>
>Se você estiver usando o WSDL do serviço Forms para preencher previamente um formulário, converta um `org.w3c.dom.Document` em um `BLOB` objeto.

**Renderizar um formulário pré-preenchido**

Você renderiza um formulário pré-preenchido como qualquer outro formulário. A única diferença é que você usa o `com.adobe.idp.Document` objeto que contém a fonte de dados XML para preencher previamente o formulário.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Criação de aplicações Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Pré-preenchimento de formulários usando a API Java {#prepopulating-forms-using-the-java-api}

Para preencher previamente um formulário com um layout fluível usando a API do Forms (Java), execute as seguintes etapas:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Criar uma fonte de dados XML na memória

   * Criar um Java `DocumentBuilderFactory` ao chamar o `DocumentBuilderFactory` class&#39; `newInstance` método.
   * Criar um Java `DocumentBuilder` ao chamar o `DocumentBuilderFactory` do objeto `newDocumentBuilder` método.
   * Chame o `DocumentBuilder` do objeto `newDocument` método para instanciar um `org.w3c.dom.Document` objeto.
   * Crie o elemento raiz da fonte de dados XML chamando o `org.w3c.dom.Document` do objeto `createElement` método. Isso cria uma `Element` objeto que representa o elemento raiz. Transmita um valor de string que represente o nome do elemento para a variável `createElement` método. Converter o valor de retorno em `Element`. Em seguida, anexe o elemento raiz ao documento chamando o `Document` do objeto `appendChild` e transmita o objeto de elemento raiz como um argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Crie o elemento de cabeçalho da fonte de dados XML chamando o `Document` do objeto `createElement` método. Transmita um valor de string que represente o nome do elemento para a variável `createElement` método. Converter o valor de retorno em `Element`. Em seguida, anexe o elemento de cabeçalho ao elemento raiz chamando o `root` do objeto `appendChild` e transmita o objeto do elemento de cabeçalho como um argumento. Os elementos XML anexados ao elemento de cabeçalho correspondem à parte estática do formulário. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Crie um elemento filho que pertença ao elemento de cabeçalho chamando o `Document` do objeto `createElement` e passe um valor de string que represente o nome do elemento. Converter o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho chamando seu `appendChild` e transmita o `Document` do objeto `createTextNode` como um argumento. Especifique um valor de string que apareça como o valor do elemento filho. Finalmente, anexe o elemento filho ao elemento de cabeçalho chamando o do elemento de cabeçalho `appendChild` e transmita o objeto de elemento filho como um argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * Adicione todos os elementos restantes ao elemento de cabeçalho repetindo a última subetapa para cada campo que aparece na parte estática do formulário (no diagrama de fonte de dados XML, esses campos são mostrados na seção A. (Consulte [Entender subgrupos de dados](#understanding-data-subgroups).)
   * Crie o elemento de detalhes da fonte de dados XML chamando o `Document` do objeto `createElement` método. Transmita um valor de string que represente o nome do elemento para a variável `createElement` método. Converter o valor de retorno em `Element`. Em seguida, anexe o elemento de detalhes ao elemento raiz chamando o `root` do objeto `appendChild` e transmita o objeto do elemento de detalhe como um argumento. Os elementos XML anexados ao elemento de detalhes correspondem à parte dinâmica do formulário. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Crie um elemento filho que pertença ao elemento de detalhes chamando o `Document` do objeto `createElement` e passe um valor de string que represente o nome do elemento. Converter o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho chamando seu `appendChild` e transmita o `Document` do objeto `createTextNode` como um argumento. Especifique um valor de string que apareça como o valor do elemento filho. Por fim, anexe o elemento filho ao elemento de detalhes, chamando a função do elemento de detalhes `appendChild` e transmita o objeto de elemento filho como um argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita a última subetapa para todos os elementos XML a serem anexados ao elemento de detalhes. Para criar corretamente a origem de dados XML usada para preencher o formulário de ordem de compra, você deve anexar os seguintes elementos XML ao elemento de detalhes: `txtDescription`, `numQty`, e `numUnitPrice`.
   * Repita as duas últimas subetapas para todos os itens de dados usados para preencher previamente o formulário.

1. Converter a fonte de dados XML

   * Criar um `javax.xml.transform.Transformer` ao invocar o `javax.xml.transform.Transformer` estática do objeto `newInstance` método.
   * Criar um `Transformer` ao invocar o `TransformerFactory` do objeto `newTransformer` método.
   * Criar um `ByteArrayOutputStream` usando seu construtor.
   * Criar um `javax.xml.transform.dom.DOMSource` usando seu construtor e transmitindo o `org.w3c.dom.Document` objeto criado na etapa 1.
   * Criar um `javax.xml.transform.dom.DOMSource` usando seu construtor e transmitindo o `ByteArrayOutputStream` objeto.
   * Preencha o Java `ByteArrayOutputStream` ao invocar o `javax.xml.transform.Transformer` do objeto `transform` e transmitindo o `javax.xml.transform.dom.DOMSource` e a variável `javax.xml.transform.stream.StreamResult` objetos.
   * Crie uma matriz de bytes e aloque o tamanho da variável `ByteArrayOutputStream` à matriz de bytes.
   * Preencha a matriz de bytes chamando o `ByteArrayOutputStream` do objeto `toByteArray` método.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo a matriz de bytes.

1. Renderizar um formulário pré-preenchido

   Chame o `FormsServiceClient` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo.
   * A `com.adobe.idp.Document` objeto que contém dados a serem mesclados com o formulário. Certifique-se de usar o `com.adobe.idp.Document` objeto criado nas etapas um e dois.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço do Forms.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   A variável `renderPDFForm` o método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

   * Criar um `javax.servlet.ServletOutputStream` objeto usado para enviar um fluxo de dados de formulário para o navegador da web cliente.
   * Criar um `com.adobe.idp.Document` ao invocar o `FormsResult` do objeto `getOutputContent` método.
   * Criar um `java.io.InputStream` ao invocar o `com.adobe.idp.Document` do objeto `getInputStream` método.
   * Crie uma matriz de bytes para preenchê-la com o fluxo de dados de formulário, chamando o `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

**Consulte também**

[Início rápido (modo SOAP): pré-preenchimento do Forms com layouts fluíveis usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Pré-preenchimento de formulários usando a API do serviço Web {#prepopulating-forms-using-the-web-service-api}

Para preencher previamente um formulário com um layout fluível usando a API do Forms (serviço da Web), execute as seguintes etapas:

1. Incluir arquivos de projeto

   * Crie classes de proxy Java que consomem o serviço WSDL do Forms. (Consulte [Criando classes de proxy Java usando o Apache Axis](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * Inclua as classes de proxy Java no caminho da classe.

1. Criar uma fonte de dados XML na memória

   * Criar um Java `DocumentBuilderFactory` ao chamar o `DocumentBuilderFactory` class&#39; `newInstance` método.
   * Criar um Java `DocumentBuilder` ao chamar o `DocumentBuilderFactory` do objeto `newDocumentBuilder` método.
   * Chame o `DocumentBuilder` do objeto `newDocument` método para instanciar um `org.w3c.dom.Document` objeto.
   * Crie o elemento raiz da fonte de dados XML chamando o `org.w3c.dom.Document` do objeto `createElement` método. Isso cria uma `Element` objeto que representa o elemento raiz. Transmita um valor de string que represente o nome do elemento para a variável `createElement` método. Converter o valor de retorno em `Element`. Em seguida, anexe o elemento raiz ao documento chamando o `Document` do objeto `appendChild` e transmita o objeto de elemento raiz como um argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Crie o elemento de cabeçalho da fonte de dados XML chamando o `Document` do objeto `createElement` método. Transmita um valor de string que represente o nome do elemento para a variável `createElement` método. Converter o valor de retorno em `Element`. Em seguida, anexe o elemento de cabeçalho ao elemento raiz chamando o `root` do objeto `appendChild` e transmita o objeto do elemento de cabeçalho como um argumento. Os elementos XML anexados ao elemento de cabeçalho correspondem à parte estática do formulário. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Crie um elemento filho que pertença ao elemento de cabeçalho chamando o `Document` do objeto `createElement` e passe um valor de string que represente o nome do elemento. Converter o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho chamando seu `appendChild` e transmita o `Document` do objeto `createTextNode` como um argumento. Especifique um valor de string que apareça como o valor do elemento filho. Finalmente, anexe o elemento filho ao elemento de cabeçalho chamando o do elemento de cabeçalho `appendChild` e transmita o objeto de elemento filho como um argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * Adicione todos os elementos restantes ao elemento de cabeçalho repetindo a última subetapa para cada campo que aparece na parte estática do formulário (no diagrama de fonte de dados XML, esses campos são mostrados na seção A. (Consulte [Entender subgrupos de dados](#understanding-data-subgroups).)
   * Crie o elemento de detalhes da fonte de dados XML chamando o `Document` do objeto `createElement` método. Transmita um valor de string que represente o nome do elemento para a variável `createElement` método. Converter o valor de retorno em `Element`. Em seguida, anexe o elemento de detalhes ao elemento raiz chamando o `root` do objeto `appendChild` e transmita o objeto do elemento de detalhe como um argumento. Os elementos XML anexados ao elemento de detalhes correspondem à parte dinâmica do formulário. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Crie um elemento filho que pertença ao elemento de detalhes chamando o `Document` do objeto `createElement` e passe um valor de string que represente o nome do elemento. Converter o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho chamando seu `appendChild` e transmita o `Document` do objeto `createTextNode` como um argumento. Especifique um valor de string que apareça como o valor do elemento filho. Por fim, anexe o elemento filho ao elemento de detalhes, chamando a função do elemento de detalhes `appendChild` e transmita o objeto de elemento filho como um argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita a última subetapa para todos os elementos XML a serem anexados ao elemento de detalhes. Para criar corretamente a origem de dados XML usada para preencher o formulário de ordem de compra, você deve anexar os seguintes elementos XML ao elemento de detalhes: `txtDescription`, `numQty`, e `numUnitPrice`.
   * Repita as duas últimas subetapas para todos os itens de dados usados para preencher previamente o formulário.

1. Converter a fonte de dados XML

   * Criar um `javax.xml.transform.Transformer` ao invocar o `javax.xml.transform.Transformer` estática do objeto `newInstance` método.
   * Criar um `Transformer` ao invocar o `TransformerFactory` do objeto `newTransformer` método.
   * Criar um `ByteArrayOutputStream` usando seu construtor.
   * Criar um `javax.xml.transform.dom.DOMSource` usando seu construtor e transmitindo o `org.w3c.dom.Document` objeto criado na etapa 1.
   * Criar um `javax.xml.transform.dom.DOMSource` usando seu construtor e transmitindo o `ByteArrayOutputStream` objeto.
   * Preencha o Java `ByteArrayOutputStream` ao invocar o `javax.xml.transform.Transformer` do objeto `transform` e transmitindo o `javax.xml.transform.dom.DOMSource` e a variável `javax.xml.transform.stream.StreamResult` objetos.
   * Crie uma matriz de bytes e aloque o tamanho da variável `ByteArrayOutputStream` à matriz de bytes.
   * Preencha a matriz de bytes chamando o `ByteArrayOutputStream` do objeto `toByteArray` método.
   * Criar um `BLOB` objeto usando seu construtor e invocando seu `setBinaryData` e transmitem a matriz de bytes.

1. Renderizar um formulário pré-preenchido

   Chame o `FormsService` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de cadeia de caracteres que especifica o nome de design do formulário, incluindo a extensão de nome de arquivo.
   * A `BLOB` objeto que contém dados a serem mesclados com o formulário. Certifique-se de usar o `BLOB` objeto criado nas etapas um e dois.
   * A `PDFFormRenderSpecc` objeto que armazena opções de tempo de execução. Para obter mais informações, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `URLSpec` objeto que contém valores de URI exigidos pelo serviço do Forms.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto preenchido pelo método. Isso é usado para armazenar o formulário de PDF renderizado.
   * Um vazio `javax.xml.rpc.holders.LongHolder` objeto preenchido pelo método. (Esse argumento armazenará o número de páginas no formulário).
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método. (Esse argumento armazenará o valor do local).
   * Um vazio `com.adobe.idp.services.holders.FormsResultHolder` objeto que conterá os resultados desta operação.

   A variável `renderPDFForm` O método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

   * Criar um `FormResult` obtendo o valor do `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value` membro de dados.
   * Criar um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método.
   * Obter o tipo de conteúdo do `BLOB` ao invocar seu `getContentType` método.
   * Defina o `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto chamando seu `setContentType` e transmitindo o tipo de conteúdo do `BLOB` objeto.
   * Criar um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados de formulário no navegador da web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método.
   * Crie uma matriz de bytes e preencha-a chamando o `BLOB` do objeto `getBinaryData` método. Esta tarefa atribui o conteúdo do `FormsResult` à matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

   >[!NOTE]
   >
   >A variável `renderPDFForm` O método preenche o `com.adobe.idp.services.holders.FormsResultHolder` objeto que é passado como o último valor de argumento com um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

**Consulte também**

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
