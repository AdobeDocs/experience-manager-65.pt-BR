---
title: Pré-preenchimento do Forms com layouts flutuantes
seo-title: Pré-preenchimento do Forms com layouts flutuantes
description: Preencha os formulários com layout flutuante para exibir dados aos usuários em um formulário renderizado usando a API do Java e a API do serviço da Web.
seo-description: Preencha os formulários com layout flutuante para exibir dados aos usuários em um formulário renderizado usando a API do Java e a API do serviço da Web.
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3534'
ht-degree: 0%

---


# Pré-preencher o Forms com layouts flutuantes {#prepopulating-forms-with-flowable-layouts1}

## Pré-preencher o Forms com layouts flutuantes {#prepopulating-forms-with-flowable-layouts2}

O pré-preenchimento de formulários exibe dados aos usuários em um formulário renderizado. Por exemplo, suponha que um usuário faça logon em um site com um nome de usuário e senha. Se a autenticação for bem-sucedida, o aplicativo cliente consultará um banco de dados para obter informações do usuário. Os dados são unidos no formulário e, em seguida, ele é renderizado para o usuário. Como resultado, o usuário pode exibir dados personalizados dentro do formulário.

O pré-preenchimento de um formulário tem as seguintes vantagens:

* Permite que o usuário exiba dados personalizados em um formulário.
* Reduz a quantidade de digitação que o usuário faz para preencher um formulário.
* Garante integridade dos dados por meio do controle de onde os dados são colocados.

As duas fontes de dados XML a seguir podem pré-preencher um formulário:

* Uma fonte de dados XDP, que é um XML em conformidade com a sintaxe XFA (ou dados XFDF para pré-preencher um formulário criado usando o Acrobat).
* Uma fonte de dados XML arbitrária que contém pares de nome/valor correspondentes aos nomes de campo do formulário (os exemplos nesta seção usam uma fonte de dados XML arbitrária).

Um elemento XML deve existir para cada campo de formulário que você deseja pré-preencher. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML é ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos, desde que todos os elementos XML sejam especificados.

Ao pré-preencher um formulário que já contém dados, você deve especificar os dados que já são exibidos na fonte de dados XML. Suponha que um formulário contendo 10 campos tenha dados em quatro campos. Em seguida, suponha que você deseja pré-preencher os seis campos restantes. Nessa situação, você deve especificar 10 elementos XML na fonte de dados XML usada para pré-preencher o formulário. Se você especificar apenas seis elementos, os quatro campos originais ficarão vazios.

Por exemplo, é possível pré-preencher um formulário, como o formulário de confirmação de amostra. (Consulte &quot;Formulário de confirmação&quot; em [Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md).)

Para preencher previamente o formulário de confirmação de amostra, é necessário criar uma fonte de dados XML que contenha três elementos XML que correspondam aos três campos no formulário. Este formulário contém os três campos a seguir: `FirstName`, `LastName` e `Amount`. A primeira etapa é criar uma fonte de dados XML que contenha elementos XML correspondentes aos campos localizados no design de formulário. A próxima etapa é atribuir valores de dados aos elementos XML, conforme mostrado no código XML a seguir.

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

Depois de preencher previamente o formulário de confirmação com essa fonte de dados XML e renderizar o formulário, os valores de dados atribuídos aos elementos XML serão exibidos, conforme mostrado no diagrama a seguir.

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### Pré-preenchimento de formulários com layouts flutuantes {#prepopulating_forms_with_flowable_layouts-1}

O Forms com layouts flutuantes é útil para exibir uma quantidade indeterminada de dados para os usuários. Como o layout do formulário se ajusta automaticamente à quantidade de dados que é unida, não é necessário predeterminar um layout fixo ou um número de páginas para o formulário, conforme necessário, com um formulário com layout fixo.

Normalmente, um formulário é preenchido com dados obtidos durante o tempo de execução. Como resultado, é possível pré-preencher um formulário criando uma fonte de dados XML na memória e colocando os dados diretamente na fonte de dados XML na memória.

Considere um aplicativo baseado na Web, como uma loja online. Depois que um comprador online terminar de comprar itens, todos os itens comprados serão colocados em uma fonte de dados XML na memória usada para pré-preencher um formulário. O diagrama a seguir mostra esse processo, que é explicado na tabela a seguir ao diagrama.

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

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
   <td><p>Um usuário compra itens de uma loja online baseada na Web. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Depois que o usuário finaliza a compra de itens e clica no botão Enviar , uma fonte de dados XML na memória é criada. Os itens comprados e as informações do usuário são colocados na fonte de dados XML na memória. </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>A fonte de dados XML é usada para pré-preencher um formulário de pedido de compra (um exemplo desse formulário é mostrado após a tabela). </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>O formulário de pedido de compra é renderizado no navegador da Web do cliente. </p></td>
  </tr>
 </tbody>
</table>

O diagrama a seguir mostra um exemplo de formulário de pedido de compra. As informações na tabela podem se ajustar ao número de registros nos dados XML.

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>Um formulário pode ser pré-preenchido com dados de outras fontes, como um banco de dados corporativo ou aplicativos externos.

### Considerações sobre design de formulário {#form-design-considerations}

O Forms com layouts flutuantes é baseado em designs de formulário criados no Designer. Um design de formulário especifica um conjunto de regras de layout, apresentação e captura de dados, incluindo o cálculo de valores com base na entrada do usuário. As regras são aplicadas quando os dados são inseridos em um formulário. Os campos adicionados a um formulário são subformulários que estão dentro do design de formulário. Por exemplo, no formulário de pedido de compra mostrado no diagrama anterior, cada linha é um subformulário. Para obter informações sobre como criar um design de formulário que contenha subformulários, consulte [Criação de um formulário de pedido de compra com layout flutuante](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9).

### Como entender subgrupos de dados {#understanding-data-subgroups}

Uma fonte de dados XML é usada para pré-preencher formulários com layouts fixos e layouts flutuantes. No entanto, a diferença é que uma fonte de dados XML que pré-preenche um formulário com um layout flutuante contém elementos XML repetitivos usados para pré-preencher subformulários que são repetidos dentro do formulário. Esses elementos XML repetitivos são chamados de subgrupos de dados.

Uma fonte de dados XML usada para pré-preencher o formulário de pedido de compra mostrado no diagrama anterior contém quatro subgrupos de dados repetitivos. Cada subgrupo de dados corresponde a um item comprado. Os itens comprados são um monitor, uma lâmpada de mesa, um telefone e um catálogo de endereços.

A seguinte fonte de dados XML é usada para pré-preencher o formulário de pedido de compra.

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

O nome do elemento XML pai de um subgrupo de dados deve corresponder ao nome do subformulário localizado no design de formulário. Por exemplo, no diagrama anterior, observe que o nome do elemento primário XML do subgrupo de dados é `detail`. Isso corresponde ao nome do subformulário localizado no design de formulário no qual o formulário de pedido de compra é baseado. Se o nome do elemento primário XML do subgrupo de dados e o subformulário não corresponderem, um formulário do lado do servidor não será pré-preenchido.

Cada subgrupo de dados deve conter elementos XML que correspondam aos nomes dos campos no subformulário. O subformulário `detail` localizado no design de formulário contém os seguintes campos:

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>Se você tentar preencher previamente um formulário com uma fonte de dados que contém elementos XML repetitivos e definir a opção `RenderAtClient` como `No`, somente o primeiro registro de dados será unido ao formulário. Para garantir que todos os registros de dados sejam mesclados no formulário, defina `RenderAtClient` como `Yes`. Para obter informações sobre a opção `RenderAtClient`, consulte [Renderizar Forms no Client](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para preencher previamente um formulário com um layout flutuante, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie uma fonte de dados XML na memória.
1. Converta a fonte de dados XML.
1. Renderizar um formulário pré-preenchido.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar uma fonte de dados XML na memória**

Você pode usar as classes `org.w3c.dom` para criar uma fonte de dados XML na memória para pré-preencher um formulário com um layout flutuante. Você deve colocar os dados em uma fonte de dados XML que esteja em conformidade com o formulário. Para obter informações sobre a relação entre um formulário com um layout flutuante e a fonte de dados XML, consulte [Entendendo subgrupos de dados](#understanding-data-subgroups).

**Converter a fonte de dados XML**

Uma fonte de dados XML na memória criada usando classes `org.w3c.dom` pode ser convertida em um objeto `com.adobe.idp.Document` antes de poder ser usada para pré-preencher um formulário. Uma fonte de dados XML na memória pode ser convertida usando classes de transformação Java XML.

>[!NOTE]
>
>Se estiver usando o WSDL do serviço Forms para pré-preencher um formulário, é necessário converter um objeto `org.w3c.dom.Document` em um objeto `BLOB`.

**Renderizar um formulário pré-preenchido**

Você renderiza um formulário pré-preenchido como qualquer outro formulário. A única diferença é que você usa o objeto `com.adobe.idp.Document` que contém a fonte de dados XML para pré-preencher o formulário.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Pré-preenchimento de formulários usando a API Java {#prepopulating-forms-using-the-java-api}

Para pré-preencher um formulário com um layout flutuante usando a API do Forms (Java), execute as seguintes etapas:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java. Para obter informações sobre a localização desses arquivos, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Criar uma fonte de dados XML na memória

   * Crie um objeto Java `DocumentBuilderFactory` chamando o método `DocumentBuilderFactory` class&#39; `newInstance`.
   * Crie um objeto Java `DocumentBuilder` chamando o método `DocumentBuilderFactory` do objeto `newDocumentBuilder`.
   * Chame o método `DocumentBuilder` do objeto `newDocument` para instanciar um objeto `org.w3c.dom.Document`.
   * Crie o elemento raiz da fonte de dados XML chamando o método `org.w3c.dom.Document` do objeto `createElement`. Isso cria um objeto `Element` que representa o elemento raiz. Passe um valor de string representando o nome do elemento para o método `createElement` . Converta o valor de retorno em `Element`. Em seguida, anexe o elemento raiz ao documento, chamando o método `Document` do objeto `appendChild` e transmita o objeto do elemento raiz como um argumento. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Crie o elemento de cabeçalho da fonte de dados XML, chamando o método `Document` do objeto `createElement`. Passe um valor de string representando o nome do elemento para o método `createElement` . Converta o valor de retorno em `Element`. Em seguida, anexe o elemento de cabeçalho ao elemento raiz, chamando o método `root` do objeto `appendChild` e transmita o objeto de elemento de cabeçalho como um argumento. Os elementos XML anexados ao elemento de cabeçalho correspondem à parte estática do formulário. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Crie um elemento filho que pertence ao elemento de cabeçalho, chamando o método `Document` do objeto `createElement` e transmita um valor de string que representa o nome do elemento. Converta o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho, chamando seu método `appendChild` e transmitindo o método `Document` do objeto `createTextNode` como um argumento. Especifique um valor de string que apareça como o valor do elemento filho. Por fim, anexe o elemento filho ao elemento de cabeçalho, chamando o método `appendChild` do elemento de cabeçalho e transmita o objeto de elemento filho como um argumento. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * Adicione todos os elementos restantes ao elemento de cabeçalho repetindo a última subetapa para cada campo que aparece na parte estática do formulário (no diagrama de fonte de dados XML, esses campos são mostrados na seção A. (Consulte [Entendendo subgrupos de dados](#understanding-data-subgroups).)
   * Crie o elemento detalhado da fonte de dados XML, chamando o método `Document` do objeto `createElement`. Passe um valor de string representando o nome do elemento para o método `createElement` . Converta o valor de retorno em `Element`. Em seguida, anexe o elemento detalhado ao elemento raiz, chamando o método `root` do objeto `appendChild` e transmita o objeto de elemento detalhado como um argumento. Os elementos XML anexados ao elemento de detalhes correspondem à parte dinâmica do formulário. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Crie um elemento filho que pertence ao elemento detalhado, chamando o método `Document` do objeto `createElement` e transmita um valor de string que representa o nome do elemento. Converta o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho, chamando seu método `appendChild` e transmitindo o método `Document` do objeto `createTextNode` como um argumento. Especifique um valor de string que apareça como o valor do elemento filho. Finalmente, anexe o elemento filho ao elemento detalhado ao chamar o método `appendChild` do elemento detalhado e transmitir o objeto do elemento filho como um argumento. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita a última subetapa para todos os elementos XML a serem anexados ao elemento detalhado. Para criar corretamente a fonte de dados XML usada para preencher o formulário de pedido de compra, você deve anexar os seguintes elementos XML ao elemento detalhado: `txtDescription`, `numQty` e `numUnitPrice`.
   * Repita as duas últimas subetapas para todos os itens de dados usados para pré-preencher o formulário.

1. Converter a fonte de dados XML

   * Crie um objeto `javax.xml.transform.Transformer` chamando o método `javax.xml.transform.Transformer` estático `newInstance` do objeto.
   * Crie um objeto `Transformer` chamando o método `TransformerFactory` `newTransformer` do objeto.
   * Crie um objeto `ByteArrayOutputStream` usando seu construtor.
   * Crie um objeto `javax.xml.transform.dom.DOMSource` usando seu construtor e transmitindo o objeto `org.w3c.dom.Document` criado na etapa 1.
   * Crie um objeto `javax.xml.transform.dom.DOMSource` usando seu construtor e transmitindo o objeto `ByteArrayOutputStream`.
   * Preencha o objeto Java `ByteArrayOutputStream` chamando o método `javax.xml.transform.Transformer` do objeto `transform` e passando os objetos `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult`.
   * Crie uma matriz de bytes e aloque o tamanho do objeto `ByteArrayOutputStream` na matriz de bytes.
   * Preencha a matriz de bytes chamando o método `ByteArrayOutputStream` do objeto `toByteArray`.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo a matriz de bytes.

1. Renderizar um formulário pré-preenchido

   Chame o método `FormsServiceClient` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo.
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário. Certifique-se de usar o objeto `com.adobe.idp.Document` criado nas etapas um e dois.
   * Um objeto `PDFFormRenderSpec` que armazena opções de tempo de execução.
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderPDFForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

   * Crie um objeto `javax.servlet.ServletOutputStream` usado para enviar um fluxo de dados de formulário para o navegador da Web do cliente.
   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Crie um objeto `java.io.InputStream` chamando o método `com.adobe.idp.Document` `getInputStream` do objeto.
   * Crie uma matriz de bytes para preenchê-la com o fluxo de dados do formulário, chamando o método `InputStream` do objeto e passando a matriz de bytes como um argumento.`read`
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Passe a matriz de bytes para o método `write` .


**Consulte também:**

[Início rápido (modo SOAP): Pré-preencher o Forms com layouts flutuantes usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Pré-preenchimento de formulários usando a API do serviço da Web {#prepopulating-forms-using-the-web-service-api}

Para pré-preencher um formulário com um layout flutuante usando a API do Forms (serviço da Web), execute as seguintes etapas:

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms. (Consulte [Criação de classes proxy Java usando o Apache Axis](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * Inclua as classes proxy Java no caminho da classe.

1. Criar uma fonte de dados XML na memória

   * Crie um objeto Java `DocumentBuilderFactory` chamando o método `DocumentBuilderFactory` class&#39; `newInstance`.
   * Crie um objeto Java `DocumentBuilder` chamando o método `DocumentBuilderFactory` do objeto `newDocumentBuilder`.
   * Chame o método `DocumentBuilder` do objeto `newDocument` para instanciar um objeto `org.w3c.dom.Document`.
   * Crie o elemento raiz da fonte de dados XML chamando o método `org.w3c.dom.Document` do objeto `createElement`. Isso cria um objeto `Element` que representa o elemento raiz. Passe um valor de string representando o nome do elemento para o método `createElement` . Converta o valor de retorno em `Element`. Em seguida, anexe o elemento raiz ao documento, chamando o método `Document` do objeto `appendChild` e transmita o objeto do elemento raiz como um argumento. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Crie o elemento de cabeçalho da fonte de dados XML, chamando o método `Document` do objeto `createElement`. Passe um valor de string representando o nome do elemento para o método `createElement` . Converta o valor de retorno em `Element`. Em seguida, anexe o elemento de cabeçalho ao elemento raiz, chamando o método `root` do objeto `appendChild` e transmita o objeto de elemento de cabeçalho como um argumento. Os elementos XML anexados ao elemento de cabeçalho correspondem à parte estática do formulário. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Crie um elemento filho que pertence ao elemento de cabeçalho, chamando o método `Document` do objeto `createElement` e transmita um valor de string que representa o nome do elemento. Converta o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho, chamando seu método `appendChild` e transmitindo o método `Document` do objeto `createTextNode` como um argumento. Especifique um valor de string que apareça como o valor do elemento filho. Por fim, anexe o elemento filho ao elemento de cabeçalho, chamando o método `appendChild` do elemento de cabeçalho e transmita o objeto de elemento filho como um argumento. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * Adicione todos os elementos restantes ao elemento de cabeçalho repetindo a última subetapa para cada campo que aparece na parte estática do formulário (no diagrama de fonte de dados XML, esses campos são mostrados na seção A. (Consulte [Entendendo subgrupos de dados](#understanding-data-subgroups).)
   * Crie o elemento detalhado da fonte de dados XML, chamando o método `Document` do objeto `createElement`. Passe um valor de string representando o nome do elemento para o método `createElement` . Converta o valor de retorno em `Element`. Em seguida, anexe o elemento detalhado ao elemento raiz, chamando o método `root` do objeto `appendChild` e transmita o objeto de elemento detalhado como um argumento. Os elementos XML anexados ao elemento de detalhes correspondem à parte dinâmica do formulário. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Crie um elemento filho que pertence ao elemento detalhado, chamando o método `Document` do objeto `createElement` e transmita um valor de string que representa o nome do elemento. Converta o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho, chamando seu método `appendChild` e transmitindo o método `Document` do objeto `createTextNode` como um argumento. Especifique um valor de string que apareça como o valor do elemento filho. Finalmente, anexe o elemento filho ao elemento detalhado ao chamar o método `appendChild` do elemento detalhado e transmitir o objeto do elemento filho como um argumento. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Repita a última subetapa para todos os elementos XML a serem anexados ao elemento detalhado. Para criar corretamente a fonte de dados XML usada para preencher o formulário de pedido de compra, você deve anexar os seguintes elementos XML ao elemento detalhado: `txtDescription`, `numQty` e `numUnitPrice`.
   * Repita as duas últimas subetapas para todos os itens de dados usados para pré-preencher o formulário.

1. Converter a fonte de dados XML

   * Crie um objeto `javax.xml.transform.Transformer` chamando o método `javax.xml.transform.Transformer` estático `newInstance` do objeto.
   * Crie um objeto `Transformer` chamando o método `TransformerFactory` `newTransformer` do objeto.
   * Crie um objeto `ByteArrayOutputStream` usando seu construtor.
   * Crie um objeto `javax.xml.transform.dom.DOMSource` usando seu construtor e transmitindo o objeto `org.w3c.dom.Document` criado na etapa 1.
   * Crie um objeto `javax.xml.transform.dom.DOMSource` usando seu construtor e transmitindo o objeto `ByteArrayOutputStream`.
   * Preencha o objeto Java `ByteArrayOutputStream` chamando o método `javax.xml.transform.Transformer` do objeto `transform` e passando os objetos `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult`.
   * Crie uma matriz de bytes e aloque o tamanho do objeto `ByteArrayOutputStream` na matriz de bytes.
   * Preencha a matriz de bytes chamando o método `ByteArrayOutputStream` do objeto `toByteArray`.
   * Crie um objeto `BLOB` usando seu construtor e chame seu método `setBinaryData` e passe a matriz de bytes.

1. Renderizar um formulário pré-preenchido

   Chame o método `FormsService` do objeto `renderPDFForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo.
   * Um objeto `BLOB` que contém dados para mesclar com o formulário. Certifique-se de usar o objeto `BLOB` criado nas etapas um e dois.
   * Um objeto `PDFFormRenderSpecc` que armazena opções de tempo de execução. Para obter mais informações, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Um objeto `URLSpec` que contém valores de URI exigidos pelo serviço Forms.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método . Usado para armazenar o formulário PDF renderizado.
   * Um objeto vazio `javax.xml.rpc.holders.LongHolder` que é preenchido pelo método . (Esse argumento armazenará o número de páginas no formulário).
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método . (Esse argumento armazenará o valor da localidade).
   * Um objeto vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O método `renderPDFForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value`.
   * Crie um objeto `BLOB` que contenha dados de formulário chamando o método `FormsResult` do objeto `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e passando o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie uma matriz de bytes e preencha-a chamando o método `BLOB` do objeto `getBinaryData`. Essa tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Passe a matriz de bytes para o método `write` .

   >[!NOTE]
   >
   >O método `renderPDFForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

**Consulte também:**

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

