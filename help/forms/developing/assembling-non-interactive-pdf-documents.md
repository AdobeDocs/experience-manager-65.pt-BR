---
title: Montagem de documentos PDF não interativos
description: Use um formulário de PDF não interativo como entrada para montar um documento de PDF não interativo usando a API Java e a API de serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 0%

---

# Montagem de documentos PDF não interativos {#assembling-non-interactive-pdf-documents}

Você pode montar um documento PDF não interativo ao usar um formulário PDF interativo como entrada. Ou seja, suponha que você tenha um formulário que os usuários possam usar para inserir dados em seus campos. Você pode passar esse formulário para o serviço Assembler, resultando no serviço Assembler retornando um documento PDF que impede que os usuários insiram dados em seus campos. Este documento é um formulário PDF não interativo. Por exemplo, a ilustração a seguir mostra um aplicativo de hipoteca que representa um formulário interativo.

Para o propósito desta discussão, suponha que o seguinte documento DDX seja usado.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

Neste documento DDX, observe que o valor `inDoc` é atribuído ao atributo de origem. Nas situações em que somente um documento de PDF de entrada é passado para o serviço Assembler e um documento de PDF é retornado, e você invoca a operação `invokeOneDocument`, atribua o valor `inDoc` ao atributo de origem PDF. Ao invocar a operação `invokeOneDocument`, o valor `inDoc` é uma chave predefinida que deve ser especificada no documento DDX.

Por outro lado, ao passar dois ou mais documentos de PDF de entrada para o serviço Assembler, você pode invocar a operação `invokeDDX`. Nessa situação, atribua o nome de arquivo do documento de PDF de entrada ao atributo `source`.

Este documento DDX contém o elemento `NoXFA`, que instrui o serviço Assembler a retornar um documento PDF não interativo.

O serviço Assembler pode montar documentos de PDF não interativos sem que o serviço Output faça parte da instalação dos formulários AEM se o documento de PDF de entrada for baseado em um formulário Acrobat ou um formulário XFA estático. No entanto, se o documento PDF de entrada for um formulário XFA dinâmico, o Serviço de saída deverá fazer parte da instalação do AEM Forms. Se o Serviço de saída não fizer parte da instalação dos formulários AEM quando um formulário XFA dinâmico for montado, uma exceção será lançada. Consulte [Criando Fluxos de Saída de Documentos](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos do PDF usando o serviço Assembler. Esta seção não discute conceitos, como criar um objeto de coleção que contenha documentos de entrada ou saber como extrair os resultados do objeto de coleção retornado. (Consulte [Assembling Programmatically PDF Documents](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço do Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar um documento PDF não interativo, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDF Assembler.
1. Consulte um documento DDX existente.
1. Consulte um documento PDF interativo.
1. Definir opções de tempo de execução.
1. Monte o documento PDF.
1. Salve o documento PDF não interativo.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado.

**Criar um cliente do Assembler**

Antes de executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referenciar um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Este documento DDX deve conter o elemento `NoXFA`, que instrui o serviço Assembler a retornar um documento PDF não interativo.

**Referenciar um documento PDF interativo**

Um documento PDF interativo deve ser referenciado e passado ao serviço Assembler para recuperar um documento PDF não interativo.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado.

**Montar o documento PDF**

Depois de criar o cliente de serviço do Assembler, fazer referência ao documento DDX, referenciar um documento PDF interativo e definir opções de tempo de execução, você poderá invocar a operação `invokeOneDocument`. Como apenas um documento de PDF de entrada é passado para o serviço Assembler e um único documento é retornado, você pode usar a operação `invokeOneDocument`, em vez da operação `invokeDDX`.

**Salvar o documento PDF não interativo**

Se apenas um único documento de PDF for passado para o serviço do Assembler, o serviço do Assembler retornará um único documento em vez de um objeto de coleção. Ou seja, ao invocar a operação `invokeOneDocument`, um único documento é retornado. Como o documento DDX referenciado nesta seção contém instruções para criar um documento PDF não interativo, o serviço do Assembler retorna um documento PDF não interativo que pode ser salvo como um arquivo PDF.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar um documento PDF não interativo usando a API Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Montar um documento PDF não interativo usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente Assembler.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Consulte um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do arquivo DDX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Consulte um documento PDF interativo.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local de um documento PDF interativo.
   * Crie um objeto `com.adobe.idp.Document` e passe o objeto `java.io.FileInputStream` que contém o documento PDF. Este objeto `com.adobe.idp.Document` é passado para o método `invokeOneDocument`.

1. Definir opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos da sua empresa invocando um método que pertença ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, chame o método `setFailOnError` do objeto `AssemblerOptionSpec` e passe `false`.

1. Monte o documento PDF.

   Invoque o método `invokeOneDocument` do objeto `AssemblerServiceClient` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX. Verifique se este documento DDX contém o valor `inDoc` para o elemento de origem PDF.
   * Um objeto `com.adobe.idp.Document` que contém o documento PDF interativo.
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do trabalho.

   O método `invokeOneDocument` retorna um objeto `com.adobe.idp.Document` que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo.

   * Crie um objeto `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Invoque o método `copyToFile` do objeto `Document` para copiar o conteúdo do objeto `Document` para o arquivo. Certifique-se de usar o objeto `Document` retornado pelo método `invokeOneDocument`.

* &quot;Início rápido (modo SOAP): montagem de um documento PDF não interativo usando a API Java&quot;

## Montar um documento PDF não interativo usando a API do serviço Web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Montar um documento PDF não interativo usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente Assembler.

   * Crie um objeto `AssemblerServiceClient` usando seu construtor padrão.
   * Crie um objeto `AssemblerServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado quando você cria uma referência de serviço.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `AssemblerServiceClient.Endpoint.Binding`. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `MessageEncoding` do objeto `System.ServiceModel.BasicHttpBinding` como `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Consulte um documento DDX existente.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento DDX.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento DDX e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` com o conteúdo da matriz de bytes.

1. Consulte um documento PDF interativo.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento de PDF de entrada. Este objeto `BLOB` é passado para `invokeOneDocument` como argumento.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos comerciais atribuindo um valor a um membro de dados que pertença ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, atribua `false` ao membro de dados `failOnError` do objeto `AssemblerOptionSpec`.

1. Monte o documento PDF.

   Invoque o método `invokeOneDocument` do objeto `AssemblerServiceClient` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX
   * Um objeto `BLOB` que representa o documento PDF interativo
   * Um objeto `AssemblerOptionSpec` que especifica as opções de tempo de execução

   O método `invokeOneDocument` retorna um objeto `BLOB` que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF não interativo e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `invokeOneDocument`. Popular a matriz de bytes obtendo o valor do campo `MTOM` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

* &quot;Início rápido (MTOM): Montagem de um documento PDF não interativo usando a API de serviço da Web.&quot;

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
