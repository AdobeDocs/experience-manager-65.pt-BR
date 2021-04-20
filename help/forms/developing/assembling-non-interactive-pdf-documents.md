---
title: Montagem de documentos PDF não interativos
seo-title: Montagem de documentos PDF não interativos
description: Use um formulário PDF não interativo como entrada para montar um documento PDF não interativo usando a API do Java e a API do serviço da Web.
seo-description: Use um formulário PDF não interativo como entrada para montar um documento PDF não interativo usando a API do Java e a API do serviço da Web.
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1801'
ht-degree: 0%

---


# Montagem de documentos PDF não interativos {#assembling-non-interactive-pdf-documents}

Você pode montar um documento PDF não interativo ao usar um formulário PDF interativo como entrada. Ou seja, suponha que você tenha um formulário que os usuários possam usar para inserir dados em seus campos. Você pode passar esse formulário para o serviço Assembler, o que resulta no retorno do serviço Assembler de um documento PDF que impede que os usuários insiram dados em seus campos. Este documento é um formulário PDF não interativo. Por exemplo, a ilustração a seguir mostra um aplicativo de hipoteca que representa um formulário interativo.

Para a finalidade desta discussão, suponha que o seguinte documento DDX seja usado.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

Nesse documento DDX, observe que o atributo de origem recebe o valor `inDoc`. Nas situações em que apenas um documento PDF de entrada é passado para o serviço Assembler e um documento PDF é retornado e você chama a operação `invokeOneDocument`, atribua o valor `inDoc` ao atributo de origem PDF. Ao invocar a operação `invokeOneDocument`, o valor `inDoc` é uma chave predefinida que deve ser especificada no documento DX.

Por outro lado, ao transmitir dois ou mais documentos PDF de entrada para o serviço Assembler, você pode chamar a operação `invokeDDX`. Nessa situação, atribua o nome do arquivo do documento PDF de entrada ao atributo `source`.

Este documento DDX contém o elemento `NoXFA`, que instrui o serviço Assembler a retornar um documento PDF não interativo.

O serviço Assembler pode montar documentos PDF não interativos sem que o serviço de saída faça parte de sua instalação de formulários AEM se o documento PDF de entrada for baseado em um formulário Acrobat ou em um formulário XFA estático. No entanto, se o documento PDF de entrada for um formulário XFA dinâmico, o serviço de Saída deverá fazer parte da instalação dos formulários AEM. Se o Serviço de saída não fizer parte de sua instalação de formulários AEM quando um formulário XFA dinâmico for montado, uma exceção será lançada. Consulte [Criando Fluxos de Saída de Documento](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos PDF usando o serviço Assembler. Esta seção não discute conceitos, como criar um objeto de coleção que contenha documentos de entrada ou aprender a extrair os resultados do objeto de coleção retornado. (Consulte [Montagem programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de Serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar um documento PDF não interativo, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Assembler do PDF.
1. Faça referência a um documento DDX existente.
1. Referência a um documento PDF interativo.
1. Defina as opções de tempo de execução.
1. Monte o documento PDF.
1. Salve o documento PDF não interativo.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado.

**Criar um cliente Assembler**

Antes de poder executar programaticamente uma operação Assembler, é necessário criar um cliente de serviço Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Este documento DDX deve conter o elemento `NoXFA`, que instrui o serviço Assembler a retornar um documento PDF não interativo.

**Referência a um documento PDF interativo**

Um documento PDF interativo deve ser referenciado e passado ao serviço Assembler para recuperar um documento PDF não interativo.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrua o serviço Assembler a continuar processando um trabalho se um erro for encontrado.

**Monte o documento PDF**

Depois de criar o cliente do serviço Assembler, consultar o documento DDX, fazer referência a um documento PDF interativo e definir opções de tempo de execução, você pode chamar a operação `invokeOneDocument`. Como apenas um documento PDF de entrada é passado para o serviço Assembler e um único documento é retornado, você pode usar a operação `invokeOneDocument` em vez da operação `invokeDDX`.

**Salvar o documento PDF não interativo**

Se apenas um único documento PDF for passado para o serviço Assembler, o serviço Assembler retornará um único documento em vez de um objeto de coleção. Ou seja, ao invocar a operação `invokeOneDocument`, um único documento é retornado. Como o documento DDX mencionado nesta seção contém instruções para criar um documento PDF não interativo, o serviço Assembler retorna um documento PDF não interativo que pode ser salvo como um arquivo PDF.

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Monte um documento PDF não interativo usando a API Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Monte um documento PDF não interativo usando a API do Assembler Service (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente Assembler.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Faça referência a um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifique o local do arquivo DX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Referência a um documento PDF interativo.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e passando o local de um documento PDF interativo.
   * Crie um objeto `com.adobe.idp.Document` e passe o objeto `java.io.FileInputStream` que contém o documento PDF. Esse objeto `com.adobe.idp.Document` é passado para o método `invokeOneDocument`.

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor .
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios, chamando um método que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, chame o método `AssemblerOptionSpec` do objeto `setFailOnError` e passe `false`.

1. Monte o documento PDF.

   Chame o método `AssemblerServiceClient` do objeto `invokeOneDocument` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX. Certifique-se de que este documento DDX contenha o valor `inDoc` para o elemento de origem PDF.
   * Um objeto `com.adobe.idp.Document` que contém o documento PDF interativo.
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do trabalho.

   O método `invokeOneDocument` retorna um objeto `com.adobe.idp.Document` que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo.

   * Crie um objeto `java.io.File` e verifique se a extensão do nome de arquivo é .pdf.
   * Chame o método `Document` do objeto `copyToFile` para copiar o conteúdo do objeto `Document` para o arquivo. Certifique-se de usar o objeto `Document` retornado pelo método `invokeOneDocument`.

* &quot;Início rápido (modo SOAP): Montagem de um documento PDF não interativo usando a API do Java&quot;

## Monte um documento PDF não interativo usando a API do serviço da Web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Monte um documento PDF não interativo usando a API do Assembler Service (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente Assembler.

   * Crie um objeto `AssemblerServiceClient` usando seu construtor padrão.
   * Crie um objeto `AssemblerServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `AssemblerServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a um documento DDX existente.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento DDX.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento DX e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Referência a um documento PDF interativo.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF de entrada. Esse objeto `BLOB` é passado para `invokeOneDocument` como um argumento.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF de entrada e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor .
   * Defina as opções de tempo de execução para atender aos requisitos de negócios, atribuindo um valor a um membro de dados que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, atribua `false` ao membro de dados `AssemblerOptionSpec` do objeto `failOnError`.

1. Monte o documento PDF.

   Chame o método `AssemblerServiceClient` do objeto `invokeOneDocument` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX
   * Um objeto `BLOB` que representa o documento PDF interativo
   * Um objeto `AssemblerOptionSpec` que especifica as opções de tempo de execução

   O método `invokeOneDocument` retorna um objeto `BLOB` que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF não interativo e o modo para abrir o arquivo no.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `invokeOneDocument`. Preencha a matriz de bytes obtendo o valor do campo `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e passando o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

* &quot;Início rápido (MTOM): Montagem de um documento PDF não interativo usando a API do serviço da Web&quot;.

**Consulte também:**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
