---
title: Criação dinâmica de Documentos DDX
seo-title: Criação dinâmica de Documentos DDX
description: 'null'
seo-description: 'null'
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 0%

---


# Criação dinâmica de Documentos DDX {#dynamically-creating-ddx-documents}

Você pode criar dinamicamente um documento DDX que pode ser usado para executar uma operação do Assembler. A criação dinâmica de um documento DX permite usar valores no documento DDX obtidos durante o tempo de execução. Para criar dinamicamente um documento DX, use classes que pertencem à linguagem de programação que você está usando. Por exemplo, se você estiver desenvolvendo seu aplicativo cliente usando Java, use classes que pertencem ao `org.w3c.dom.*`pacote. Da mesma forma, se você estiver usando o Microsoft .NET, use classes que pertencem à `System.Xml` namespace.

Antes de poder passar o documento DDX para o serviço Assembler, converta o XML de uma `org.w3c.dom.Document` instância para uma `com.adobe.idp.Document` . Se você estiver usando serviços da Web, converta o XML do tipo de dados usado para criar o XML (por exemplo, `XmlDocument`) em uma `BLOB` instância.

Para essa discussão, considere que o seguinte documento DDX foi criado dinamicamente.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Este documento DDX desmonta um documento PDF. É recomendável que você esteja familiarizado com a desmontagem de documentos PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para desmontar um documento PDF usando um documento DX criado dinamicamente, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente do Montador de PDF.
1. Crie o documento DDX.
1. Converta o documento DDX.
1. Defina as opções de tempo de execução.
1. Desmonte o documento PDF.
1. Salve os documentos PDF desmontados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se os AEM Forms forem implantados em JBoss)
* jbossall-client.jar (obrigatório se os AEM Forms forem implantados em JBoss)

**Criar um cliente de Montador de PDF**

Antes de executar programaticamente uma operação de Assembler, crie um cliente de serviço de Assembler.

**Criar o documento DDX**

Crie um documento DDX usando a linguagem de programação que você está usando. Para criar um documento DDX que desmonte um documento PDF, verifique se ele contém o `PDFsFromBookmarks` elemento . Converta o tipo de dados usado para criar o documento DDX em uma `com.adobe.idp.Document` instância se você estiver usando a API Java. Se você estiver usando serviços da Web, converta o tipo de dados em uma `BLOB` instância.

**Converter o documento DDX**

Um documento DDX criado usando `org.w3c.dom` classes deve ser convertido em um `com.adobe.idp.Document` objeto. Para executar essa tarefa ao usar a API Java, use classes de transformação Java XML. Se você estiver usando serviços da Web, converta o documento DDX em um `BLOB` objeto.

**Referência a um documento PDF para desmontar**

Para desmontar um documento PDF, consulte um arquivo PDF que representa o documento PDF a ser desmontado. Quando passado para o serviço Assembler, um documento PDF separado é retornado para cada marcador de nível 1 no documento.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando uma tarefa se um erro for encontrado. Para definir opções de tempo de execução, use um `AssemblerOptionSpec` objeto.

**Desmonte o documento PDF**

Desmonte o documento PDF chamando a operação. `invokeDDX` Passe o documento DDX que foi criado dinamicamente. O serviço Assembler retorna documentos PDF desmontados em um objeto de coleção.

**Salve os documentos PDF desmontados**

Todos os documentos PDF desmontados são retornados dentro de um objeto de coleção. Insira o objeto de coleção e salve cada documento PDF como um arquivo PDF.

**Consulte também:**

[Criar dinamicamente um documento DX usando a API Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Criar dinamicamente um documento DX usando a API de serviço da Web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontagem programática de Documentos PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Criar dinamicamente um documento DX usando a API Java {#dynamically-create-a-ddx-document-using-the-java-api}

Crie dinamicamente um documento DX e desmonte um documento PDF usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente do Montador de PDF.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `AssemblerServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Crie o documento DDX.

   * Crie um objeto Java `DocumentBuilderFactory` chamando o `DocumentBuilderFactory` método da classe `newInstance` .
   * Crie um objeto Java `DocumentBuilder` chamando o `DocumentBuilderFactory` método do `newDocumentBuilder` objeto.
   * Chame o `DocumentBuilder` método do `newDocument` objeto para instanciar um `org.w3c.dom.Document` objeto.
   * Crie o elemento raiz do documento DDX chamando o método do `org.w3c.dom.Document` objeto `createElement` . Esse método cria um `Element` objeto que representa o elemento raiz. Passe um valor de string representando o nome do elemento para o `createElement` método. Converta o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho chamando seu `setAttribute` método. Finalmente, acrescente o elemento ao elemento header chamando o `appendChild` método do elemento header e passe o objeto de elemento filho como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Crie o `PDFsFromBookmarks` elemento chamando o `Document` método do `createElement` objeto. Passe um valor de string representando o nome do elemento para o `createElement` método. Converta o valor de retorno em `Element`. Defina um valor para o `PDFsFromBookmarks` elemento chamando seu `setAttribute` método. Anexe o `PDFsFromBookmarks` elemento ao `DDX` elemento chamando o `appendChild` método do elemento DDX. Passe o objeto `PDFsFromBookmarks` element como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Crie um `PDF` elemento chamando o `Document` método do `createElement` objeto. Passe um valor de string que representa o nome do elemento. Converta o valor de retorno em `Element`. Defina um valor para o `PDF` elemento chamando seu `setAttribute` método. Anexar o `PDF` elemento ao `PDFsFromBookmarks` elemento chamando o `PDFsFromBookmarks` método do elemento `appendChild` . Passe o objeto `PDF` element como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Converta o documento DDX.

   * Crie um `javax.xml.transform.Transformer` objeto chamando o `javax.xml.transform.Transformer` método estático do `newInstance` objeto.
   * Crie um `Transformer` objeto chamando o `TransformerFactory` método do `newTransformer` objeto.
   * Crie um `ByteArrayOutputStream` objeto usando seu construtor.
   * Crie um `javax.xml.transform.dom.DOMSource` objeto usando seu construtor. Passe o `org.w3c.dom.Document` objeto que representa o documento DDX.
   * Crie um `javax.xml.transform.dom.DOMSource` objeto usando seu construtor e transmitindo o `ByteArrayOutputStream` objeto.
   * Preencha o objeto Java `ByteArrayOutputStream` chamando o `javax.xml.transform.Transformer` método do `transform` objeto. Passe os objetos `javax.xml.transform.dom.DOMSource` e os `javax.xml.transform.stream.StreamResult` objetos.
   * Crie uma matriz de bytes e aloque o tamanho do `ByteArrayOutputStream` objeto na matriz de bytes.
   * Preencha a matriz de bytes chamando o `ByteArrayOutputStream` método do `toByteArray` objeto.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo a matriz de bytes.

1. Consulte um documento PDF para desmontar.

   * Crie um `java.util.Map` objeto usado para armazenar documentos PDF de entrada usando um `HashMap` construtor.
   * Crie um `java.io.FileInputStream` objeto usando seu construtor e transmitindo o local do documento PDF a ser desmontado.
   * Create a `com.adobe.idp.Document` object. Passe o `java.io.FileInputStream` objeto que contém o documento PDF para desmontar.
   * Adicione uma entrada ao `java.util.Map` objeto chamando seu `put` método e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX. (No documento DDX criado dinamicamente, o valor é `AssemblerResultPDF.pdf`.)
      * Um `com.adobe.idp.Document` objeto que contém o documento PDF a ser desmontado.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, chame o `AssemblerOptionSpec` método do `setFailOnError` objeto e passe `false`.

1. Desmonte o documento PDF.

   Chame o método do `AssemblerServiceClient` objeto `invokeDDX` e passe os seguintes valores:

   * Um `com.adobe.idp.Document` objeto que representa o documento DDX criado dinamicamente
   * Um `java.util.Map` objeto que contém o documento PDF a ser desmontado
   * Um `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log de trabalhos

   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém os documentos PDF desmontados e quaisquer exceções que ocorreram.

1. Salve os documentos PDF desmontados.

   Para obter os documentos PDF desmontados, execute as seguintes ações:

   * Chame o `AssemblerResult` método do `getDocuments` objeto. Esse método retorna um `java.util.Map` objeto.
   * Iterar pelo `java.util.Map` objeto até encontrar o `com.adobe.idp.Document` objeto resultante.
   * Chame o `com.adobe.idp.Document` `copyToFile` método do objeto para extrair o documento PDF.

**Consulte também:**

[Start rápido (modo SOAP): Criação dinâmica de um documento DX usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Criar dinamicamente um documento DX usando a API de serviço da Web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Crie dinamicamente um documento DX e desmonte um documento PDF usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao definir uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um cliente do Montador de PDF.

   * Crie um `AssemblerServiceClient` objeto usando seu construtor padrão.
   * Crie um `AssemblerServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar o `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `AssemblerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Crie o documento DDX.

   * Crie um `System.Xml.XmlElement` objeto usando seu construtor.
   * Crie o elemento raiz do documento DDX chamando o método do `XmlElement` objeto `CreateElement` . Esse método cria um `Element` objeto que representa o elemento raiz. Passe um valor de string representando o nome do elemento para o `CreateElement` método. Defina um valor para o elemento DDX chamando seu `SetAttribute` método. Por fim, acrescente o elemento ao documento DDX chamando o método do `XmlElement` objeto `AppendChild` . Passe o objeto DDX como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Crie o `PDFsFromBookmarks` elemento do documento DX chamando o `XmlElement` método do `CreateElement` objeto. Passe um valor de string representando o nome do elemento para o `CreateElement` método. Em seguida, defina um valor para o elemento chamando seu `SetAttribute` método. Anexe o `PDFsFromBookmarks` elemento ao elemento raiz chamando o `DDX` método do elemento `AppendChild` . Passe o objeto `PDFsFromBookmarks` element como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Crie o `PDF` elemento do documento DX chamando o `XmlElement` método do `CreateElement` objeto. Passe um valor de string representando o nome do elemento para o `CreateElement` método. Em seguida, defina um valor para o elemento filho chamando seu `SetAttribute` método. Anexar o `PDF` elemento ao `PDFsFromBookmarks` elemento chamando o `PDFsFromBookmarks` método do elemento `AppendChild` . Passe o objeto `PDF` element como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Converta o documento DDX.

   * Crie um `System.IO.MemoryStream` objeto usando seu construtor.
   * Preencha o `MemoryStream` objeto com o documento DDX usando o `XmlElement` objeto que representa o documento DX. Chame o `XmlElement` método do `Save` objeto e passe o `MemoryStream` objeto.
   * Crie uma matriz de bytes e preencha-a com os dados localizados no `MemoryStream` objeto. O código a seguir mostra esta lógica do aplicativo:

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Create a `BLOB` object. Atribua a matriz de bytes ao `BLOB` campo do `MTOM` objeto.

1. Consulte um documento PDF para desmontar.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento PDF de entrada. Esse `BLOB` objeto é passado para o `invokeOneDocument` como um argumento.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo a sua `MTOM` propriedade o conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios, atribuindo um valor a um membro de dados que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, atribua `false` ao membro de `AssemblerOptionSpec` dados do objeto `failOnError` .

1. Desmonte o documento PDF.

   Chame o método do `AssemblerServiceClient` objeto `invokeDDX` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o documento DDX criado dinamicamente
   * O `mapItem` storage que contém o documento PDF de entrada
   * Um `AssemblerOptionSpec` objeto que especifica opções de tempo de execução

   O `invokeDDX` método retorna um `AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Salve os documentos PDF desmontados.

   Para obter os documentos PDF recém-criados, execute as seguintes ações:

   * Acesse o `AssemblerResult` campo do `documents` objeto, que é um `Map` objeto que contém os documentos PDF desmontados.
   * Iterar pelo `Map` objeto para obter cada documento resultante. Em seguida, converta o membro do storage `value` em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade do `BLOB` objeto `MTOM` . Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também:**

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
