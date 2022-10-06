---
title: Criação dinâmica de documentos DDX
seo-title: Dynamically Creating DDX Documents
description: Crie um documento DDX dinamicamente usando a API Java e a API do serviço da Web. Criar dinamicamente um documento DDX permite usar valores no documento DDX obtidos durante o tempo de execução.
seo-description: Create a DDX document dynamically using the Java API and Web Service API. Dynamically creating a DDX document enables you to use values in the DDX document that are obtained during run-time.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 0%

---

# Criação dinâmica de documentos DDX {#dynamically-creating-ddx-documents}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

Você pode criar dinamicamente um documento DDX que possa ser usado para executar uma operação Assembler. Criar dinamicamente um documento DDX permite usar valores no documento DDX obtidos durante o tempo de execução. Para criar dinamicamente um documento DDX, use classes que pertencem à linguagem de programação que você está usando. Por exemplo, se você estiver desenvolvendo seu aplicativo cliente usando Java, use classes que pertencem à variável `org.w3c.dom.*`pacote. Da mesma forma, se você estiver usando o Microsoft .NET, use classes que pertencem ao `System.Xml` namespace.

Antes de passar o documento DDX para o serviço Assembler, converta o XML de um `org.w3c.dom.Document` para uma `com.adobe.idp.Document` instância. Se você estiver usando serviços da Web, converta o XML do tipo de dados usado para criar o XML (por exemplo, `XmlDocument`) a um `BLOB` instância.

Para essa discussão, suponha que o seguinte documento DDX seja criado dinamicamente.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Este documento DDX desmonta um documento PDF. Recomenda-se que você esteja familiarizado com a desmontagem de documentos do PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para desmontar um documento PDF usando um documento DDX criado dinamicamente, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Assembler PDF.
1. Crie o documento DDX.
1. Converta o documento DDX.
1. Defina as opções de tempo de execução.
1. Desmonte o documento PDF.
1. Salve os documentos de PDF desmontados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

**Criar um cliente do Assembler do PDF**

Antes de executar programaticamente uma operação Assembler, crie um cliente de serviço Assembler.

**Criar o documento DDX**

Crie um documento DDX usando a linguagem de programação que você está usando. Para criar um documento DDX que desmonta um documento PDF, verifique se ele contém a variável `PDFsFromBookmarks` elemento. Converter o tipo de dados usado para criar o documento DDX em um `com.adobe.idp.Document` se estiver usando a API do Java. Se você estiver usando serviços da Web, converta o tipo de dados em um `BLOB` instância.

**Converter o documento DDX**

Um documento DDX criado usando `org.w3c.dom` classes devem ser convertidas em um `com.adobe.idp.Document` objeto. Para executar essa tarefa ao usar a API Java, use classes de transformação Java XML. Se você estiver usando serviços da Web, converta o documento DDX em um `BLOB` objeto.

**Referência a um documento PDF para desmontar**

Para desmontar um documento PDF, consulte um arquivo PDF que representa o documento PDF para desmontar. Quando passado para o serviço Assembler, um documento PDF separado é retornado para cada marcador de nível 1 no documento.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrua o serviço Assembler a continuar processando um trabalho se um erro for encontrado. Para definir opções de tempo de execução, use um `AssemblerOptionSpec` objeto.

**Desmonte o documento PDF**

Desmonte o documento PDF chamando a `invokeDDX` operação. Passe o documento DDX que foi criado dinamicamente. O serviço Assembler retorna documentos PDF desmontados dentro de um objeto de coleção.

**Salve os documentos de PDF desmontados**

Todos os documentos PDF desmontados são retornados em um objeto de coleção. Itere pelo objeto de coleção e salve cada documento PDF como um arquivo PDF.

**Consulte também**

[Criar dinamicamente um documento DDX usando a API Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Criar dinamicamente um documento DDX usando a API do serviço da Web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontando documentos do PDF de maneira programática](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Criar dinamicamente um documento DDX usando a API Java {#dynamically-create-a-ddx-document-using-the-java-api}

Crie dinamicamente um documento DDX e desmonte um documento PDF usando a API do serviço de Assembler (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente Assembler PDF.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `AssemblerServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Crie o documento DDX.

   * Criar um Java `DocumentBuilderFactory` chamando o `DocumentBuilderFactory` classe&quot; `newInstance` método .
   * Criar um Java `DocumentBuilder` chamando o `DocumentBuilderFactory` do objeto `newDocumentBuilder` método .
   * Chame o `DocumentBuilder` do objeto `newDocument` para instanciar um `org.w3c.dom.Document` objeto.
   * Crie o elemento raiz do documento DDX chamando a função `org.w3c.dom.Document` do objeto `createElement` método . Esse método cria um `Element` objeto que representa o elemento raiz. Passe um valor de string representando o nome do elemento para a `createElement` método . Converta o valor de retorno para `Element`. Em seguida, defina um valor para o elemento filho, chamando seu `setAttribute` método . Finalmente, anexe o elemento ao elemento de cabeçalho ao chamar a função do elemento de cabeçalho `appendChild` e transmita o objeto de elemento filho como um argumento. As linhas de código a seguir mostram essa lógica de aplicativo:
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Crie o `PDFsFromBookmarks` chamando o `Document` do objeto `createElement` método . Passe um valor de string representando o nome do elemento para a `createElement` método . Converta o valor de retorno para `Element`. Defina um valor para a variável `PDFsFromBookmarks` elemento chamando seu `setAttribute` método . Anexar o `PDFsFromBookmarks` para `DDX` chamando o elemento DDX `appendChild` método . Passe o `PDFsFromBookmarks` objeto de elemento como um argumento. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Crie um `PDF` chamando o `Document` do objeto `createElement` método . Passe um valor de string que representa o nome do elemento. Converta o valor de retorno para `Element`. Defina um valor para a variável `PDF` elemento chamando seu `setAttribute` método . Anexar o `PDF` para `PDFsFromBookmarks` chamando o `PDFsFromBookmarks` element&#39;s `appendChild` método . Passe o `PDF` objeto de elemento como um argumento. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Converta o documento DDX.

   * Crie um `javax.xml.transform.Transformer` chamando o `javax.xml.transform.Transformer` estático do objeto `newInstance` método .
   * Crie um `Transformer` chamando o `TransformerFactory` do objeto `newTransformer` método .
   * Crie um `ByteArrayOutputStream` usando seu construtor.
   * Crie um `javax.xml.transform.dom.DOMSource` usando seu construtor. Passe o `org.w3c.dom.Document` objeto que representa o documento DDX.
   * Crie um `javax.xml.transform.dom.DOMSource` usando seu construtor e passando o `ByteArrayOutputStream` objeto.
   * Preencha o Java `ByteArrayOutputStream` chamando o `javax.xml.transform.Transformer` do objeto `transform` método . Passe o `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult` objetos.
   * Crie uma matriz de bytes e aloque o tamanho da variável `ByteArrayOutputStream` para a matriz de bytes.
   * Preencha a matriz de bytes chamando o `ByteArrayOutputStream` do objeto `toByteArray` método .
   * Crie um `com.adobe.idp.Document` usando seu construtor e transmitindo a matriz de bytes.

1. Faça referência a um documento PDF para desmontar.

   * Crie um `java.util.Map` objeto usado para armazenar documentos PDF de entrada usando um `HashMap` construtor.
   * Crie um `java.io.FileInputStream` usando seu construtor e passando o local do documento PDF para desmontar.
   * Crie um `com.adobe.idp.Document` objeto. Passe o `java.io.FileInputStream` objeto que contém o documento PDF para desmontagem.
   * Adicione uma entrada à `java.util.Map` ao invocar seu `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento PDF source especificado no documento DDX. (No documento DDX criado dinamicamente, o valor é `AssemblerResultPDF.pdf`.)
      * A `com.adobe.idp.Document` objeto que contém o documento PDF para desmontagem.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios, chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, chame a função `AssemblerOptionSpec` do objeto `setFailOnError` método e pass `false`.

1. Desmonte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e transmita os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX criado dinamicamente
   * A `java.util.Map` objeto que contém o documento PDF para desmontar
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log da tarefa

   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém os documentos PDF desmontados e quaisquer exceções que ocorreram.

1. Salve os documentos de PDF desmontados.

   Para obter os documentos de PDF desmontados, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método . Esse método retorna um `java.util.Map` objeto.
   * Iterar por meio do `java.util.Map` até encontrar o resultante `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento PDF.

**Consulte também**

[Início rápido (modo SOAP): Criação dinâmica de um documento DDX usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Criar dinamicamente um documento DDX usando a API do serviço da Web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Crie dinamicamente um documento DDX e desmonte um documento PDF usando a API do serviço Assembler (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao definir uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente Assembler PDF.

   * Crie um `AssemblerServiceClient` usando seu construtor padrão.
   * Crie um `AssemblerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `AssemblerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Crie o documento DDX.

   * Crie um `System.Xml.XmlElement` usando seu construtor.
   * Crie o elemento raiz do documento DDX chamando a função `XmlElement` do objeto `CreateElement` método . Esse método cria um `Element` objeto que representa o elemento raiz. Passe um valor de string representando o nome do elemento para a `CreateElement` método . Defina um valor para o elemento DDX chamando seu `SetAttribute` método . Por fim, anexe o elemento ao documento DDX ao chamar a função `XmlElement` do objeto `AppendChild` método . Passe o objeto DDX como um argumento. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Crie o documento DDX `PDFsFromBookmarks` chamando o `XmlElement` do objeto `CreateElement` método . Passe um valor de string representando o nome do elemento para a `CreateElement` método . Em seguida, defina um valor para o elemento chamando seu `SetAttribute` método . Anexar o `PDFsFromBookmarks` para o elemento raiz, chamando a função `DDX` element&#39;s `AppendChild` método . Passe o `PDFsFromBookmarks` objeto de elemento como um argumento. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Crie o documento DDX `PDF` chamando o `XmlElement` do objeto `CreateElement` método . Passe um valor de string representando o nome do elemento para a `CreateElement` método . Em seguida, defina um valor para o elemento filho, chamando seu `SetAttribute` método . Anexar o `PDF` para `PDFsFromBookmarks` chamando o `PDFsFromBookmarks` element&#39;s `AppendChild` método . Passe o `PDF` objeto de elemento como um argumento. As linhas de código a seguir mostram essa lógica de aplicativo:

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Converta o documento DDX.

   * Crie um `System.IO.MemoryStream` usando seu construtor.
   * Preencha o `MemoryStream` com o documento DDX usando o `XmlElement` objeto que representa o documento DDX. Chame o `XmlElement` do objeto `Save` e passe o `MemoryStream` objeto.
   * Crie uma matriz de bytes e preencha-a com os dados localizados na `MemoryStream` objeto. O código a seguir mostra essa lógica do aplicativo:

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Crie um `BLOB` objeto. Atribua a matriz de bytes à `BLOB` do objeto `MTOM` campo.

1. Faça referência a um documento PDF para desmontar.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento PDF de entrada. Essa `BLOB` é passado para o `invokeOneDocument` como um argumento.
   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` propriedade do conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos da empresa, atribuindo um valor a um membro de dados pertencente à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, atribua `false` para `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Desmonte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e transmita os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX criado dinamicamente
   * O `mapItem` matriz que contém o documento PDF de entrada
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   O `invokeDDX` retorna um método `AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Salve os documentos de PDF desmontados.

   Para obter os documentos PDF recém-criados, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` , que é um `Map` objeto que contém os documentos PDF desmontados.
   * Iterar por meio do `Map` para obter cada documento resultante. Em seguida, converta esse membro da matriz `value` para `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando seu `BLOB` do objeto `MTOM` propriedade. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
