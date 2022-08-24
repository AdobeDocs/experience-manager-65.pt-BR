---
title: Montagem de Documentos de PDF não interativos
seo-title: Assembling Non-Interactive PDF Documents
description: Use um formulário PDF não interativo como entrada para montar um documento PDF não interativo usando a API do Java e a API do serviço da Web.
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
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---

# Montagem de Documentos de PDF não interativos {#assembling-non-interactive-pdf-documents}

Você pode montar um documento PDF não interativo ao usar um formulário PDF interativo como entrada. Ou seja, suponha que você tenha um formulário que os usuários possam usar para inserir dados em seus campos. Você pode passar esse formulário para o serviço Assembler, resultando no retorno do serviço Assembler de um documento PDF que impede que os usuários informem dados em seus campos. Este documento é um formulário PDF não interativo. Por exemplo, a ilustração a seguir mostra um aplicativo de hipoteca que representa um formulário interativo.

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

Nesse documento DDX, observe que o atributo de origem recebe o valor `inDoc`. Nas situações em que apenas um documento PDF de entrada é passado para o serviço Assembler e um documento PDF é retornado, e você chama o `invokeOneDocument` , atribua o valor `inDoc` para o atributo PDF source. Ao invocar o `invokeOneDocument` , a `inDoc` é uma chave predefinida que deve ser especificada no documento DDX.

Por outro lado, ao passar dois ou mais documentos PDF de entrada para o serviço Assembler, você pode chamar o `invokeDDX` operação. Nessa situação, atribua o nome do arquivo do documento PDF de entrada ao `source` atributo.

Este documento DDX contém a variável `NoXFA` , que instrui o serviço Assembler a retornar um documento PDF não interativo.

O serviço Assembler pode reunir documentos PDF não interativos sem que o serviço de Saída faça parte de sua instalação de formulários AEM se o documento PDF de entrada for baseado em um formulário Acrobat ou em um formulário XFA estático. No entanto, se o documento PDF de entrada for um formulário XFA dinâmico, o serviço de Saída deverá fazer parte da instalação do AEM forms. Se o Serviço de saída não fizer parte de sua instalação de formulários AEM quando um formulário XFA dinâmico for montado, uma exceção será lançada. Consulte [Criando Fluxos de Saída de Documento](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos do PDF usando o serviço Assembler. Esta seção não discute conceitos, como criar um objeto de coleção que contenha documentos de entrada ou aprender a extrair os resultados do objeto de coleção retornado. (Consulte [Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar um documento PDF não interativo, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Assembler PDF.
1. Faça referência a um documento DDX existente.
1. Faça referência a um documento de PDF interativo.
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

Um documento DDX deve ser referenciado para montar um documento PDF. Este documento DDX deve conter a variável `NoXFA` , que instrui o serviço Assembler a retornar um documento PDF não interativo.

**Referência a um documento de PDF interativo**

Um documento PDF interativo deve ser referenciado e passado ao serviço Assembler para recuperar um documento PDF não interativo.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrua o serviço Assembler a continuar processando um trabalho se um erro for encontrado.

**Montar o documento PDF**

Depois de criar o cliente do serviço Assembler, fazer referência ao documento DDX, fazer referência a um documento de PDF interativo e definir opções de tempo de execução, você pode chamar o `invokeOneDocument` operação. Como apenas um documento PDF de entrada é passado para o serviço Assembler e um único documento é retornado, você pode usar o `invokeOneDocument` em vez de `invokeDDX` operação.

**Salve o documento PDF não interativo**

Se apenas um único documento PDF for passado para o serviço Assembler, o serviço Assembler retornará um único documento em vez de um objeto de coleção. Ou seja, ao invocar o `invokeOneDocument` , um único documento é retornado. Como o documento DDX referenciado nesta seção contém instruções para criar um documento PDF não interativo, o serviço Assembler retorna um documento PDF não interativo que pode ser salvo como um arquivo PDF.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Monte um documento PDF não interativo usando a API do Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Monte um documento PDF não interativo usando a API do Assembler Service (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente Assembler.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `AssemblerServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e passando um valor de string que especifica o local do arquivo DX.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Faça referência a um documento de PDF interativo.

   * Crie um `java.io.FileInputStream` usando seu construtor e transmitindo o local de um documento PDF interativo.
   * Crie um `com.adobe.idp.Document` e transmita o `java.io.FileInputStream` objeto que contém o documento PDF. Essa `com.adobe.idp.Document` é passado para o `invokeOneDocument` método .

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios, chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, chame a função `AssemblerOptionSpec` do objeto `setFailOnError` método e pass `false`.

1. Monte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeOneDocument` e transmita os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX. Certifique-se de que este documento DDX contém o valor `inDoc` para o elemento PDF source .
   * A `com.adobe.idp.Document` objeto que contém o documento PDF interativo.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do trabalho.

   O `invokeOneDocument` método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo.

   * Crie um `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `Document` do objeto `copyToFile` para copiar o conteúdo da `Document` ao arquivo. Certifique-se de usar a variável `Document` que a variável `invokeOneDocument` método retornado.

* &quot;Início rápido (modo SOAP): Montagem de um documento do PDF não interativo usando a API do Java&quot;

## Monte um documento PDF não interativo usando a API do serviço da Web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Monte um documento de PDF não interativo usando a API do Assembler Service (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente Assembler.

   * Crie um `AssemblerServiceClient` usando seu construtor padrão.
   * Crie um `AssemblerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `AssemblerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a um documento DDX existente.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento DDX.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento DX e o modo para abrir o arquivo no.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Faça referência a um documento de PDF interativo.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento PDF de entrada. Essa `BLOB` é passado para o `invokeOneDocument` como um argumento.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF de entrada e o modo para abrir o arquivo no.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos da empresa, atribuindo um valor a um membro de dados pertencente à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, atribua `false` para `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Monte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeOneDocument` e transmita os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX
   * A `BLOB` objeto que representa o documento PDF interativo
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   O `invokeOneDocument` método retorna um `BLOB` objeto que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo.

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF não interativo e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` que a variável `invokeOneDocument` método retornado. Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` campo.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

* &quot;Início rápido (MTOM): Montagem de um documento PDF não interativo usando a API do serviço da Web&quot;.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
