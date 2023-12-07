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
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2153'
ht-degree: 0%

---

# Criação dinâmica de documentos DDX {#dynamically-creating-ddx-documents}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

Você pode criar dinamicamente um documento DDX que pode ser usado para executar uma operação do Assembler. A criação dinâmica de um documento DDX permite usar valores nele obtidos durante o tempo de execução. Para criar dinamicamente um documento DDX, use classes que pertençam à linguagem de programação que você está usando. Por exemplo, se você estiver desenvolvendo seu aplicativo cliente usando Java, use classes que pertencem à variável `org.w3c.dom.*`pacote. Da mesma forma, se você estiver usando o Microsoft .NET, use classes que pertençam ao `System.Xml` namespace.

Antes de passar o documento DDX para o serviço do Assembler, converta o XML de um `org.w3c.dom.Document` instância para um `com.adobe.idp.Document` instância. Se você estiver usando serviços da Web, converta o XML a partir do tipo de dados usado para criar o XML (por exemplo, `XmlDocument`) para um `BLOB` instância.

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
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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

**Criar um cliente do PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, crie um cliente de serviço do Assembler.

**Criar o documento DDX**

Crie um documento DDX usando a linguagem de programação que você está usando. Para criar um documento DDX que desmonte um documento PDF, verifique se ele contém o `PDFsFromBookmarks` elemento. Converta o tipo de dados usado para criar o documento DDX em um `com.adobe.idp.Document` instância se estiver usando a API Java. Se você estiver usando serviços da Web, converta o tipo de dados em um `BLOB` instância.

**Converter o documento DDX**

Um documento DDX criado usando `org.w3c.dom` as classes devem ser convertidas em um `com.adobe.idp.Document` objeto. Para executar essa tarefa ao usar a API Java, use classes de transformação Java XML. Se você estiver usando serviços da Web, converta o documento DDX em um `BLOB` objeto.

**Referencie um documento do PDF para desmontar**

Para desmontar um documento PDF, consulte um arquivo PDF que representa o documento PDF a ser desmontado. Quando passado para o serviço Assembler, um documento PDF separado é retornado para cada marcador de nível 1 no documento.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado. Para definir opções de tempo de execução, use um `AssemblerOptionSpec` objeto.

**Desmontar o documento PDF**

Desmonte o documento PDF chamando o `invokeDDX` operação. Transmita o documento DDX criado dinamicamente. O serviço Assembler retorna documentos PDF desmontados dentro de um objeto de coleção.

**Salve os documentos de PDF desmontados**

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

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `AssemblerServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Crie o documento DDX.

   * Criar um Java `DocumentBuilderFactory` ao chamar o `DocumentBuilderFactory` class&#39; `newInstance` método.
   * Criar um Java `DocumentBuilder` ao chamar o `DocumentBuilderFactory` do objeto `newDocumentBuilder` método.
   * Chame o `DocumentBuilder` do objeto `newDocument` método para instanciar um `org.w3c.dom.Document` objeto.
   * Crie o elemento raiz do documento DDX chamando o `org.w3c.dom.Document` do objeto `createElement` método. Este método cria um `Element` objeto que representa o elemento raiz. Transmita um valor de string que represente o nome do elemento para a variável `createElement` método. Converter o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho chamando seu `setAttribute` método. Finalmente, anexe o elemento ao elemento de cabeçalho chamando o do elemento de cabeçalho `appendChild` e transmita o objeto de elemento filho como um argumento. As linhas de código a seguir mostram essa lógica de aplicação:
     ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Crie o `PDFsFromBookmarks` ao chamar o `Document` do objeto `createElement` método. Transmita um valor de string que represente o nome do elemento para a variável `createElement` método. Converter o valor de retorno em `Element`. Defina um valor para a variável `PDFsFromBookmarks` elemento ao chamar sua `setAttribute` método. Anexe o `PDFsFromBookmarks` elemento para o `DDX` chamando o do elemento DDX `appendChild` método. Passe o `PDFsFromBookmarks` objeto de elemento como argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Criar um `PDF` ao chamar o `Document` do objeto `createElement` método. Transmita um valor de string que represente o nome do elemento. Converter o valor de retorno em `Element`. Defina um valor para a variável `PDF` elemento ao chamar sua `setAttribute` método. Anexe o `PDF` elemento para o `PDFsFromBookmarks` ao chamar o `PDFsFromBookmarks` do elemento `appendChild` método. Passe o `PDF` objeto de elemento como argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Converta o documento DDX.

   * Criar um `javax.xml.transform.Transformer` ao invocar o `javax.xml.transform.Transformer` estática do objeto `newInstance` método.
   * Criar um `Transformer` ao invocar o `TransformerFactory` do objeto `newTransformer` método.
   * Criar um `ByteArrayOutputStream` usando seu construtor.
   * Criar um `javax.xml.transform.dom.DOMSource` usando seu construtor. Passe o `org.w3c.dom.Document` objeto que representa o documento DDX.
   * Criar um `javax.xml.transform.dom.DOMSource` usando seu construtor e transmitindo o `ByteArrayOutputStream` objeto.
   * Preencha o Java `ByteArrayOutputStream` ao invocar o `javax.xml.transform.Transformer` do objeto `transform` método. Passe o `javax.xml.transform.dom.DOMSource` e a variável `javax.xml.transform.stream.StreamResult` objetos.
   * Crie uma matriz de bytes e aloque o tamanho da variável `ByteArrayOutputStream` à matriz de bytes.
   * Preencha a matriz de bytes chamando o `ByteArrayOutputStream` do objeto `toByteArray` método.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo a matriz de bytes.

1. Referencie um documento do PDF para desmontar.

   * Criar um `java.util.Map` objeto usado para armazenar documentos de PDF de entrada usando um `HashMap` construtor.
   * Criar um `java.io.FileInputStream` usando seu construtor e transmitindo o local do documento PDF a ser desmontado.
   * Criar um `com.adobe.idp.Document` objeto. Passe o `java.io.FileInputStream` objeto que contém o documento PDF a ser desmontado.
   * Adicione uma entrada à `java.util.Map` ao invocar seu `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX. (No documento DDX criado dinamicamente, o valor é `AssemblerResultPDF.pdf`.)
      * A `com.adobe.idp.Document` objeto que contém o documento PDF a ser desmontado.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa, chamando um método que pertence à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler para continuar processando um job quando ocorrer um erro, chame o `AssemblerOptionSpec` do objeto `setFailOnError` e passar `false`.

1. Desmonte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX criado dinamicamente
   * A `java.util.Map` objeto que contém o documento PDF a ser desmontado
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do job

   A variável `invokeDDX` o método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém os documentos PDF desmontados e quaisquer exceções que ocorreram.

1. Salve os documentos de PDF desmontados.

   Para obter os documentos de PDF desmontados, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método. Este método retorna um valor de `java.util.Map` objeto.
   * Repita através do `java.util.Map` até encontrar o resultado `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para extrair o documento PDF.

**Consulte também**

[Início rápido (modo SOAP): criando dinamicamente um documento DDX usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Criar dinamicamente um documento DDX usando a API do serviço Web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Crie dinamicamente um documento DDX e desmonte um documento PDF usando a API de serviço do Assembler (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao configurar uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente PDF Assembler.

   * Criar um `AssemblerServiceClient` usando seu construtor padrão.
   * Criar um `AssemblerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `AssemblerServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Crie o documento DDX.

   * Criar um `System.Xml.XmlElement` usando seu construtor.
   * Crie o elemento raiz do documento DDX chamando o `XmlElement` do objeto `CreateElement` método. Este método cria um `Element` objeto que representa o elemento raiz. Transmita um valor de string que represente o nome do elemento para a variável `CreateElement` método. Defina um valor para o elemento DDX chamando seu `SetAttribute` método. Por fim, anexe o elemento ao documento DDX chamando o `XmlElement` do objeto `AppendChild` método. Passe o objeto DDX como argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Crie o do documento DDX `PDFsFromBookmarks` ao chamar o `XmlElement` do objeto `CreateElement` método. Transmita um valor de string que represente o nome do elemento para a variável `CreateElement` método. Em seguida, defina um valor para o elemento chamando seu `SetAttribute` método. Anexe o `PDFsFromBookmarks` elemento ao elemento raiz chamando o `DDX` do elemento `AppendChild` método. Passe o `PDFsFromBookmarks` objeto de elemento como argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Crie o do documento DDX `PDF` ao chamar o `XmlElement` do objeto `CreateElement` método. Transmita um valor de string que represente o nome do elemento para a variável `CreateElement` método. Em seguida, defina um valor para o elemento filho chamando seu `SetAttribute` método. Anexe o `PDF` elemento para o `PDFsFromBookmarks` ao chamar o `PDFsFromBookmarks` do elemento `AppendChild` método. Passe o `PDF` objeto de elemento como argumento. As linhas de código a seguir mostram essa lógica de aplicação:

     ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Converta o documento DDX.

   * Criar um `System.IO.MemoryStream` usando seu construtor.
   * Preencha o `MemoryStream` com o documento DDX usando o `XmlElement` objeto que representa o documento DDX. Chame o `XmlElement` do objeto `Save` e transmita o `MemoryStream` objeto.
   * Crie uma matriz de bytes e preencha-a com dados na variável `MemoryStream` objeto. O código a seguir mostra essa lógica de aplicação:

     ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Criar um `BLOB` objeto. Atribua a matriz de bytes à variável `BLOB` do objeto `MTOM` campo.

1. Referencie um documento do PDF para desmontar.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento PDF de entrada. Este `BLOB` objeto é passado para o `invokeOneDocument` como argumento.
   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` propriedade o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa atribuindo um valor a um membro de dados que pertença à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando um job quando ocorrer um erro, atribua `false` para o `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Desmonte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX criado dinamicamente
   * A variável `mapItem` matriz que contém o documento PDF de entrada
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   A variável `invokeDDX` o método retorna um `AssemblerResult` objeto que contém os resultados do trabalho e quaisquer exceções que ocorreram.

1. Salve os documentos de PDF desmontados.

   Para obter os documentos PDF recém-criados, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` que é um `Map` objeto que contém os documentos PDF desmontados.
   * Repita através do `Map` para obter cada documento resultante. Em seguida, converta os membros da matriz `value` para um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando seus `BLOB` do objeto `MTOM` propriedade. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
