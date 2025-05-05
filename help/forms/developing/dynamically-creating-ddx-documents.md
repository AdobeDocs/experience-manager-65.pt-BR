---
title: Criação dinâmica de documentos DDX
description: Crie um documento DDX dinamicamente usando a API Java e a API de serviço da Web. A criação dinâmica de um documento DDX permite usar valores nele obtidos durante o tempo de execução.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2153'
ht-degree: 0%

---

# Criação dinâmica de documentos DDX {#dynamically-creating-ddx-documents}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

Você pode criar dinamicamente um documento DDX que pode ser usado para executar uma operação do Assembler. A criação dinâmica de um documento DDX permite usar valores nele obtidos durante o tempo de execução. Para criar dinamicamente um documento DDX, use classes que pertençam à linguagem de programação que você está usando. Por exemplo, se você estiver desenvolvendo seu aplicativo cliente usando Java, use classes que pertencem ao pacote `org.w3c.dom.*`. Da mesma forma, se você estiver usando o Microsoft .NET, use classes que pertençam ao namespace `System.Xml`.

Antes de passar o documento DDX para o serviço do Assembler, converta o XML de uma instância `org.w3c.dom.Document` em uma instância `com.adobe.idp.Document`. Se você estiver usando serviços da Web, converta o XML do tipo de dados usado para criar o XML (por exemplo, `XmlDocument`) em uma instância `BLOB`.

Nesta discussão, suponha que o documento DDX a seguir seja criado dinamicamente.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Este documento DDX desmonta um documento PDF. É recomendável que você esteja familiarizado com a desmontagem de documentos do PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço do Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para desmontar um documento PDF usando um documento DDX criado dinamicamente, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDF Assembler.
1. Crie o documento DDX.
1. Converta o documento DDX.
1. Definir opções de tempo de execução.
1. Desmonte o documento PDF.
1. Salve os documentos de PDF desmontados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

**Criar um cliente PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, crie um cliente de serviço do Assembler.

**Criar o documento DDX**

Crie um documento DDX usando a linguagem de programação que você está usando. Para criar um documento DDX que desmonte um documento PDF, verifique se ele contém o elemento `PDFsFromBookmarks`. Converta o tipo de dados usado para criar o documento DDX em uma instância `com.adobe.idp.Document` se estiver usando a API Java. Se você estiver usando serviços Web, converta o tipo de dados em uma instância `BLOB`.

**Converter o documento DDX**

Um documento DDX criado usando classes `org.w3c.dom` deve ser convertido em um objeto `com.adobe.idp.Document`. Para executar essa tarefa ao usar a API Java, use classes de transformação Java XML. Se você estiver usando serviços Web, converta o documento DDX em um objeto `BLOB`.

**Referenciar um documento PDF para desmontar**

Para desmontar um documento PDF, consulte um arquivo PDF que representa o documento PDF a ser desmontado. Quando passado para o serviço Assembler, um documento PDF separado é retornado para cada marcador de nível 1 no documento.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado. Para definir opções de tempo de execução, use um objeto `AssemblerOptionSpec`.

**Desmontar o documento PDF**

Desmonte o documento PDF invocando a operação `invokeDDX`. Transmita o documento DDX criado dinamicamente. O serviço Assembler retorna documentos PDF desmontados dentro de um objeto de coleção.

**Salvar os documentos de PDF desmontados**

Todos os documentos de PDF desmontados são retornados dentro de um objeto de coleção. Repita o processo através do objeto de coleção e salve cada documento de PDF como um arquivo de PDF.

**Consulte também**

[Criar dinamicamente um documento DDX usando a API do Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Criar dinamicamente um documento DDX usando a API do serviço Web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontando Documentos PDF de Forma Programática](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Criar dinamicamente um documento DDX usando a API do Java {#dynamically-create-a-ddx-document-using-the-java-api}

Crie dinamicamente um documento DDX e desmonte um documento PDF usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente PDF Assembler.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Crie o documento DDX.

   * Crie um objeto Java `DocumentBuilderFactory` chamando o método `newInstance` da classe `DocumentBuilderFactory`.
   * Crie um objeto Java `DocumentBuilder` chamando o método `newDocumentBuilder` do objeto `DocumentBuilderFactory`.
   * Chame o método `newDocument` do objeto `DocumentBuilder` para instanciar um objeto `org.w3c.dom.Document`.
   * Crie o elemento raiz do documento DDX invocando o método `createElement` do objeto `org.w3c.dom.Document`. Este método cria um objeto `Element` que representa o elemento raiz. Passe um valor de cadeia de caracteres que representa o nome do elemento para o método `createElement`. Converter o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho chamando seu método `setAttribute`. Finalmente, anexe o elemento ao elemento de cabeçalho chamando o método `appendChild` do elemento de cabeçalho e passe o objeto de elemento filho como argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Crie o elemento `PDFsFromBookmarks` chamando o método `createElement` do objeto `Document`. Passe um valor de cadeia de caracteres que representa o nome do elemento para o método `createElement`. Converter o valor de retorno em `Element`. Defina um valor para o elemento `PDFsFromBookmarks` chamando seu método `setAttribute`. Anexe o elemento `PDFsFromBookmarks` ao elemento `DDX`, chamando o método `appendChild` do elemento DDX. Passe o objeto de elemento `PDFsFromBookmarks` como argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Crie um elemento `PDF` chamando o método `createElement` do objeto `Document`. Transmita um valor de string que represente o nome do elemento. Converter o valor de retorno em `Element`. Defina um valor para o elemento `PDF` chamando seu método `setAttribute`. Anexe o elemento `PDF` ao elemento `PDFsFromBookmarks`, chamando o método `appendChild` do elemento `PDFsFromBookmarks`. Passe o objeto de elemento `PDF` como argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Converta o documento DDX.

   * Crie um objeto `javax.xml.transform.Transformer` invocando o método `newInstance` estático do objeto `javax.xml.transform.Transformer`.
   * Crie um objeto `Transformer` invocando o método `newTransformer` do objeto `TransformerFactory`.
   * Crie um objeto `ByteArrayOutputStream` usando seu construtor.
   * Crie um objeto `javax.xml.transform.dom.DOMSource` usando seu construtor. Transmita o objeto `org.w3c.dom.Document` que representa o documento DDX.
   * Crie um objeto `javax.xml.transform.dom.DOMSource` usando seu construtor e transmitindo o objeto `ByteArrayOutputStream`.
   * Preencha o objeto Java `ByteArrayOutputStream` invocando o método `transform` do objeto `javax.xml.transform.Transformer`. Passar os objetos `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult`.
   * Crie uma matriz de bytes e aloque o tamanho do objeto `ByteArrayOutputStream` à matriz de bytes.
   * Preencha a matriz de bytes invocando o método `toByteArray` do objeto `ByteArrayOutputStream`.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo a matriz de bytes.

1. Referencie um documento do PDF para desmontar.

   * Crie um objeto `java.util.Map` usado para armazenar documentos de PDF de entrada usando um construtor `HashMap`.
   * Crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local do documento PDF a ser desmontado.
   * Crie um objeto `com.adobe.idp.Document`. Passe o objeto `java.io.FileInputStream` que contém o documento PDF a ser desmontado.
   * Adicione uma entrada ao objeto `java.util.Map` invocando seu método `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX. (No documento DDX criado dinamicamente, o valor é `AssemblerResultPDF.pdf`.)
      * Um objeto `com.adobe.idp.Document` que contém o documento PDF a ser desmontado.

1. Definir opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos da sua empresa invocando um método que pertença ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, chame o método `setFailOnError` do objeto `AssemblerOptionSpec` e passe `false`.

1. Desmonte o documento PDF.

   Invoque o método `invokeDDX` do objeto `AssemblerServiceClient` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX criado dinamicamente
   * Um objeto `java.util.Map` que contém o documento PDF a ser desmontado
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do trabalho

   O método `invokeDDX` retorna um objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contém os documentos PDF desmontados e as exceções que ocorreram.

1. Salve os documentos de PDF desmontados.

   Para obter os documentos de PDF desmontados, execute as seguintes ações:

   * Invoque o método `getDocuments` do objeto `AssemblerResult`. Este método retorna um objeto `java.util.Map`.
   * Repita o objeto `java.util.Map` até encontrar o objeto `com.adobe.idp.Document` resultante.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para extrair o documento PDF.

**Consulte também**

[Início rápido (modo SOAP): criando dinamicamente um documento DDX usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Criar dinamicamente um documento DDX usando a API do serviço Web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Crie dinamicamente um documento DDX e desmonte um documento PDF usando a API de serviço do Assembler (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao definir uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente PDF Assembler.

   * Crie um objeto `AssemblerServiceClient` usando seu construtor padrão.
   * Crie um objeto `AssemblerServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `AssemblerServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Crie o documento DDX.

   * Crie um objeto `System.Xml.XmlElement` usando seu construtor.
   * Crie o elemento raiz do documento DDX invocando o método `CreateElement` do objeto `XmlElement`. Este método cria um objeto `Element` que representa o elemento raiz. Passe um valor de cadeia de caracteres que representa o nome do elemento para o método `CreateElement`. Defina um valor para o elemento DDX chamando seu método `SetAttribute`. Finalmente, anexe o elemento ao documento DDX chamando o método `AppendChild` do objeto `XmlElement`. Passe o objeto DDX como argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Crie o elemento `PDFsFromBookmarks` do documento DDX chamando o método `CreateElement` do objeto `XmlElement`. Passe um valor de cadeia de caracteres que representa o nome do elemento para o método `CreateElement`. Em seguida, defina um valor para o elemento chamando seu método `SetAttribute`. Anexe o elemento `PDFsFromBookmarks` ao elemento raiz, chamando o método `AppendChild` do elemento `DDX`. Passe o objeto de elemento `PDFsFromBookmarks` como argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Crie o elemento `PDF` do documento DDX chamando o método `CreateElement` do objeto `XmlElement`. Passe um valor de cadeia de caracteres que representa o nome do elemento para o método `CreateElement`. Em seguida, defina um valor para o elemento filho chamando seu método `SetAttribute`. Anexe o elemento `PDF` ao elemento `PDFsFromBookmarks`, chamando o método `AppendChild` do elemento `PDFsFromBookmarks`. Passe o objeto de elemento `PDF` como argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Converta o documento DDX.

   * Crie um objeto `System.IO.MemoryStream` usando seu construtor.
   * Preencha o objeto `MemoryStream` com o documento DDX usando o objeto `XmlElement` que representa o documento DDX. Invoque o método `Save` do objeto `XmlElement` e passe o objeto `MemoryStream`.
   * Crie uma matriz de bytes e preencha-a com dados no objeto `MemoryStream`. O código a seguir mostra essa lógica de aplicação:

     ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Crie um objeto `BLOB`. Atribua a matriz de bytes ao campo `MTOM` do objeto `BLOB`.

1. Referencie um documento do PDF para desmontar.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento de PDF de entrada. Este objeto `BLOB` é passado para `invokeOneDocument` como argumento.
   * Crie um objeto `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo à propriedade `MTOM` o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos comerciais atribuindo um valor a um membro de dados que pertença ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, atribua `false` ao membro de dados `failOnError` do objeto `AssemblerOptionSpec`.

1. Desmonte o documento PDF.

   Invoque o método `invokeDDX` do objeto `AssemblerServiceClient` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX criado dinamicamente
   * A matriz `mapItem` que contém o documento PDF de entrada
   * Um objeto `AssemblerOptionSpec` que especifica as opções de tempo de execução

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém os resultados do trabalho e as exceções que ocorreram.

1. Salve os documentos de PDF desmontados.

   Para obter os documentos PDF recém-criados, execute as seguintes ações:

   * Acesse o campo `documents` do objeto `AssemblerResult`, que é um objeto `Map` que contém os documentos PDF desmontados.
   * Repita através do objeto `Map` para obter cada documento resultante. Em seguida, converta os `value` do membro da matriz em `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade `MTOM` do objeto `BLOB`. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
