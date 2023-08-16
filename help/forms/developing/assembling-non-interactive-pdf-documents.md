---
title: Montagem de documentos PDF não interativos
seo-title: Assembling Non-Interactive PDF Documents
description: Use um formulário de PDF não interativo como entrada para montar um documento de PDF não interativo usando a API Java e a API de serviço da Web.
seo-description: Use a non-interactive PDF form as input to assemble a non-interactive PDF document using the Java API and Web Service API.
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '1775'
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

Neste documento DDX, observe que o valor é atribuído ao atributo de origem `inDoc`. Em situações em que apenas um documento de PDF de entrada é passado para o serviço Assembler e um documento de PDF é retornado, e você chama o `invokeOneDocument` , atribua o valor `inDoc` para o atributo de origem PDF. Ao invocar a variável `invokeOneDocument` operação, a variável `inDoc` é uma chave predefinida que deve ser especificada no documento DDX.

Por outro lado, ao passar dois ou mais documentos de PDF de entrada para o serviço Assembler, você pode chamar o `invokeDDX` operação. Nessa situação, atribua o nome de arquivo do documento de PDF de entrada ao `source` atributo.

Este documento DDX contém o `NoXFA` elemento, que instrui o serviço Assembler para retornar um documento PDF não interativo.

O serviço Assembler pode montar documentos de PDF não interativos sem que o serviço Output faça parte da instalação dos formulários AEM se o documento de PDF de entrada for baseado em um formulário Acrobat ou um formulário XFA estático. No entanto, se o documento PDF de entrada for um formulário XFA dinâmico, o Serviço de saída deverá fazer parte da instalação do AEM Forms. Se o Serviço de saída não fizer parte da instalação dos formulários AEM quando um formulário XFA dinâmico for montado, uma exceção será lançada. Consulte [Criando Fluxos de Saída de Documento](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos do PDF usando o serviço Assembler. Esta seção não discute conceitos, como criar um objeto de coleção que contenha documentos de entrada ou saber como extrair os resultados do objeto de coleção retornado. (Consulte [Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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

**Referencie um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Este documento DDX deve conter a `NoXFA` elemento, que instrui o serviço Assembler para retornar um documento PDF não interativo.

**Referência a um documento PDF interativo**

Um documento PDF interativo deve ser referenciado e passado ao serviço Assembler para recuperar um documento PDF não interativo.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado.

**Montar o documento PDF**

Depois de criar o cliente de serviço do Assembler, fazer referência ao documento DDX, fazer referência a um documento PDF interativo e definir opções de tempo de execução, você poderá chamar o `invokeOneDocument` operação. Como apenas um documento de PDF de entrada é passado para o serviço Assembler e um único documento é retornado, você pode usar o `invokeOneDocument` operação em oposição à `invokeDDX` operação.

**Salve o documento PDF não interativo**

Se apenas um único documento de PDF for passado para o serviço do Assembler, o serviço do Assembler retornará um único documento em vez de um objeto de coleção. Ou seja, ao invocar o princípio `invokeOneDocument` um único documento é retornado. Como o documento DDX referenciado nesta seção contém instruções para criar um documento PDF não interativo, o serviço do Assembler retorna um documento PDF não interativo que pode ser salvo como um arquivo PDF.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar um documento PDF não interativo usando a API Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Montar um documento PDF não interativo usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente Assembler.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `AssemblerServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Consulte um documento DDX existente.

   * Criar um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DDX.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Consulte um documento PDF interativo.

   * Criar um `java.io.FileInputStream` usando seu construtor e transmitindo o local de um documento PDF interativo.
   * Criar um `com.adobe.idp.Document` e transmita o `java.io.FileInputStream` objeto que contém o documento PDF. Este `com.adobe.idp.Document` objeto é passado para o `invokeOneDocument` método.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa, chamando um método que pertence à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler para continuar processando um job quando ocorrer um erro, chame o `AssemblerOptionSpec` do objeto `setFailOnError` e passar `false`.

1. Monte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeOneDocument` e passe os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX. Verifique se este documento DDX contém o valor `inDoc` para o elemento de origem PDF.
   * A `com.adobe.idp.Document` objeto que contém o documento PDF interativo.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do job.

   A variável `invokeOneDocument` o método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo.

   * Criar um `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo. Certifique-se de usar o `Document` objeto que o `invokeOneDocument` método retornado.

* &quot;Início rápido (modo SOAP): montagem de um documento PDF não interativo usando a API Java&quot;

## Montar um documento PDF não interativo usando a API do serviço Web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Montar um documento PDF não interativo usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente Assembler.

   * Criar um `AssemblerServiceClient` usando seu construtor padrão.
   * Criar um `AssemblerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `AssemblerServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Consulte um documento DDX existente.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento DDX.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DDX e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` método. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Consulte um documento PDF interativo.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento PDF de entrada. Este `BLOB` objeto é passado para o `invokeOneDocument` como argumento.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` método. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa atribuindo um valor a um membro de dados que pertença à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando um job quando ocorrer um erro, atribua `false` para o `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Monte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeOneDocument` e passe os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX
   * A `BLOB` objeto que representa o documento PDF interativo
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   A variável `invokeOneDocument` o método retorna um `BLOB` objeto que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF não interativo e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto que o `invokeOneDocument` método retornado. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` campo.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

* &quot;Início rápido (MTOM): Montagem de um documento PDF não interativo usando a API de serviço da Web.&quot;

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
