---
title: Criação dinâmica de Documentos DDX
seo-title: Criação dinâmica de Documentos DDX
description: Crie um documento DDX dinamicamente usando a API Java e a API de serviço da Web. A criação dinâmica de um documento DX permite usar valores no documento DDX obtidos durante o tempo de execução.
seo-description: Crie um documento DDX dinamicamente usando a API Java e a API de serviço da Web. A criação dinâmica de um documento DX permite usar valores no documento DDX obtidos durante o tempo de execução.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2185'
ht-degree: 0%

---


# Criação dinâmica de Documentos DDX {#dynamically-creating-ddx-documents}

Você pode criar dinamicamente um documento DDX que pode ser usado para executar uma operação do Assembler. A criação dinâmica de um documento DX permite usar valores no documento DDX obtidos durante o tempo de execução. Para criar dinamicamente um documento DX, use classes que pertencem à linguagem de programação que você está usando. Por exemplo, se você estiver desenvolvendo seu aplicativo cliente usando Java, use classes que pertencem ao pacote `org.w3c.dom.*`. Da mesma forma, se você estiver usando o Microsoft .NET, use classes que pertencem à namespace `System.Xml`.

Antes de poder passar o documento DDX para o serviço Assembler, converta o XML de uma instância `org.w3c.dom.Document` para uma instância `com.adobe.idp.Document`. Se você estiver usando serviços da Web, converta o XML do tipo de dados usado para criar o XML (por exemplo, `XmlDocument`) para uma instância `BLOB`.

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
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

**Criar um cliente de Montador de PDF**

Antes de executar programaticamente uma operação de Assembler, crie um cliente de serviço de Assembler.

**Criar o documento DDX**

Crie um documento DDX usando a linguagem de programação que você está usando. Para criar um documento DDX que desmonte um documento PDF, verifique se ele contém o elemento `PDFsFromBookmarks`. Converta o tipo de dados usado para criar o documento DDX em uma instância `com.adobe.idp.Document` se você estiver usando a API Java. Se você estiver usando serviços da Web, converta o tipo de dados em uma instância `BLOB`.

**Converter o documento DDX**

Um documento DDX criado usando classes `org.w3c.dom` deve ser convertido em um objeto `com.adobe.idp.Document`. Para executar essa tarefa ao usar a API Java, use classes de transformação Java XML. Se você estiver usando serviços da Web, converta o documento DDX em um objeto `BLOB`.

**Referência a um documento PDF para desmontar**

Para desmontar um documento PDF, consulte um arquivo PDF que representa o documento PDF a ser desmontado. Quando passado para o serviço Assembler, um documento PDF separado é retornado para cada marcador de nível 1 no documento.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando uma tarefa se um erro for encontrado. Para definir opções de tempo de execução, use um objeto `AssemblerOptionSpec`.

**Desmonte o documento PDF**

Desmonte o documento PDF chamando a operação `invokeDDX`. Passe o documento DDX que foi criado dinamicamente. O serviço Assembler retorna documentos PDF desmontados em um objeto de coleção.

**Salve os documentos PDF desmontados**

Todos os documentos PDF desmontados são retornados dentro de um objeto de coleção. Insira o objeto de coleção e salve cada documento PDF como um arquivo PDF.

**Consulte também:**

[Criar dinamicamente um documento DX usando a API Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Criar dinamicamente um documento DX usando a API de serviço da Web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontagem programática de Documentos PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Crie dinamicamente um documento DX usando a API Java {#dynamically-create-a-ddx-document-using-the-java-api}

Crie dinamicamente um documento DX e desmonte um documento PDF usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente do Montador de PDF.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Crie o documento DDX.

   * Crie um objeto Java `DocumentBuilderFactory` chamando o método `DocumentBuilderFactory` class&#39; `newInstance`.
   * Crie um objeto Java `DocumentBuilder` chamando o método `DocumentBuilderFactory` do objeto `newDocumentBuilder`.
   * Chame o método `DocumentBuilder` do objeto `newDocument` para instanciar um objeto `org.w3c.dom.Document`.
   * Crie o elemento raiz do documento DDX chamando o método `org.w3c.dom.Document` do objeto `createElement`. Este método cria um objeto `Element` que representa o elemento raiz. Passe um valor de string representando o nome do elemento para o método `createElement`. Converta o valor de retorno em `Element`. Em seguida, defina um valor para o elemento filho chamando seu método `setAttribute`. Finalmente, acrescente o elemento ao elemento header chamando o método `appendChild` do elemento header e transmita o objeto de elemento filho como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Crie o elemento `PDFsFromBookmarks` chamando o método `Document` do objeto `createElement`. Passe um valor de string representando o nome do elemento para o método `createElement`. Converta o valor de retorno em `Element`. Defina um valor para o elemento `PDFsFromBookmarks` chamando seu método `setAttribute`. Anexe o elemento `PDFsFromBookmarks` ao elemento `DDX` chamando o método `appendChild` do elemento DX. Passe o objeto do elemento `PDFsFromBookmarks` como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Crie um elemento `PDF` chamando o método `Document` do objeto `createElement`. Passe um valor de string que representa o nome do elemento. Converta o valor de retorno em `Element`. Defina um valor para o elemento `PDF` chamando seu método `setAttribute`. Anexe o elemento `PDF` ao elemento `PDFsFromBookmarks` chamando o método `PDFsFromBookmarks` do elemento `appendChild`. Passe o objeto do elemento `PDF` como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Converta o documento DDX.

   * Crie um objeto `javax.xml.transform.Transformer` chamando o método estático `javax.xml.transform.Transformer` do objeto `newInstance`.
   * Crie um objeto `Transformer` invocando o método `TransformerFactory` do objeto `newTransformer`.
   * Crie um objeto `ByteArrayOutputStream` usando seu construtor.
   * Crie um objeto `javax.xml.transform.dom.DOMSource` usando seu construtor. Passe o objeto `org.w3c.dom.Document` que representa o documento DDX.
   * Crie um objeto `javax.xml.transform.dom.DOMSource` usando seu construtor e transmitindo o objeto `ByteArrayOutputStream`.
   * Preencha o objeto Java `ByteArrayOutputStream` chamando o método `javax.xml.transform.Transformer` do objeto `transform`. Passe os objetos `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult`.
   * Crie uma matriz de bytes e aloque o tamanho do objeto `ByteArrayOutputStream` na matriz de bytes.
   * Preencha a matriz de bytes chamando o método `ByteArrayOutputStream` do objeto `toByteArray`.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo a matriz de bytes.

1. Consulte um documento PDF para desmontar.

   * Crie um objeto `java.util.Map` usado para armazenar documentos PDF de entrada usando um construtor `HashMap`.
   * Crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local do documento PDF a ser desmontado.
   * Crie um objeto `com.adobe.idp.Document`. Passe o objeto `java.io.FileInputStream` que contém o documento PDF para desmontar.
   * Adicione uma entrada ao objeto `java.util.Map` invocando seu método `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX. (No documento DDX criado dinamicamente, o valor é `AssemblerResultPDF.pdf`.)
      * Um objeto `com.adobe.idp.Document` que contém o documento PDF a ser desmontado.

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios chamando um método que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, chame o método `AssemblerOptionSpec` do objeto `setFailOnError` e passe `false`.

1. Desmonte o documento PDF.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX criado dinamicamente
   * Um objeto `java.util.Map` que contém o documento PDF a ser desmontado
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível do log de trabalhos

   O método `invokeDDX` retorna um objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contém os documentos PDF desmontados e quaisquer exceções que ocorreram.

1. Salve os documentos PDF desmontados.

   Para obter os documentos PDF desmontados, execute as seguintes ações:

   * Chame o método `AssemblerResult` do objeto `getDocuments`. Este método retorna um objeto `java.util.Map`.
   * Itere pelo objeto `java.util.Map` até encontrar o objeto `com.adobe.idp.Document` resultante.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento PDF.

**Consulte também:**

[Start rápido (modo SOAP): Criação dinâmica de um documento DX usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Criar dinamicamente um documento DX usando a API de serviço da Web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Crie dinamicamente um documento DX e desmonte um documento PDF usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao definir uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente do Montador de PDF.

   * Crie um objeto `AssemblerServiceClient` usando seu construtor padrão.
   * Crie um objeto `AssemblerServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar o atributo `lc_version`. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `AssemblerServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Crie o documento DDX.

   * Crie um objeto `System.Xml.XmlElement` usando seu construtor.
   * Crie o elemento raiz do documento DDX chamando o método `XmlElement` do objeto `CreateElement`. Este método cria um objeto `Element` que representa o elemento raiz. Passe um valor de string representando o nome do elemento para o método `CreateElement`. Defina um valor para o elemento DDX chamando seu método `SetAttribute`. Finalmente, acrescente o elemento ao documento DDX chamando o método `XmlElement` do objeto `AppendChild`. Passe o objeto DDX como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Crie o elemento `PDFsFromBookmarks` do documento DX chamando o método `XmlElement` `CreateElement` do objeto. Passe um valor de string representando o nome do elemento para o método `CreateElement`. Em seguida, defina um valor para o elemento chamando seu método `SetAttribute`. Anexe o elemento `PDFsFromBookmarks` ao elemento raiz chamando o método `DDX` do elemento `AppendChild`. Passe o objeto do elemento `PDFsFromBookmarks` como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Crie o elemento `PDF` do documento DX chamando o método `XmlElement` `CreateElement` do objeto. Passe um valor de string representando o nome do elemento para o método `CreateElement`. Em seguida, defina um valor para o elemento filho chamando seu método `SetAttribute`. Anexe o elemento `PDF` ao elemento `PDFsFromBookmarks` chamando o método `PDFsFromBookmarks` do elemento `AppendChild`. Passe o objeto do elemento `PDF` como um argumento. As seguintes linhas de código mostram essa lógica de aplicativo:

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Converta o documento DDX.

   * Crie um objeto `System.IO.MemoryStream` usando seu construtor.
   * Preencha o objeto `MemoryStream` com o documento DDX usando o objeto `XmlElement` que representa o documento DX. Chame o método `XmlElement` do objeto `Save` e passe o objeto `MemoryStream`.
   * Crie uma matriz de bytes e preencha-a com dados localizados no objeto `MemoryStream`. O código a seguir mostra esta lógica do aplicativo:

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Crie um objeto `BLOB`. Atribua a matriz de bytes ao campo `BLOB` do objeto `MTOM`.

1. Consulte um documento PDF para desmontar.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF de entrada. Esse objeto `BLOB` é passado para `invokeOneDocument` como um argumento.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo a propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios atribuindo um valor a um membro de dados que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, atribua `false` ao membro de dados `AssemblerOptionSpec` do objeto `failOnError`.

1. Desmonte o documento PDF.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX criado dinamicamente
   * A matriz `mapItem` que contém o documento PDF de entrada
   * Um objeto `AssemblerOptionSpec` que especifica opções de tempo de execução

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém os resultados do trabalho e quaisquer exceções que ocorreram.

1. Salve os documentos PDF desmontados.

   Para obter os documentos PDF recém-criados, execute as seguintes ações:

   * Acesse o campo `AssemblerResult` do objeto `documents`, que é um objeto `Map` que contém os documentos PDF desmontados.
   * Itere pelo objeto `Map` para obter cada documento resultante. Em seguida, converta `value` desse membro da matriz em `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade `BLOB` do objeto `MTOM`. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também:**

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocando o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
