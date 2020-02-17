---
title: Montagem de documentos PDF não interativos
seo-title: Montagem de documentos PDF não interativos
description: 'null'
seo-description: 'null'
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Montagem de documentos PDF não interativos {#assembling-non-interactive-pdf-documents}

É possível montar um documento PDF não interativo ao usar um formulário PDF interativo como entrada. Ou seja, suponha que você tenha um formulário que os usuários possam usar para inserir dados em seus campos. Você pode passar esse formulário para o serviço Assembler, resultando no retorno de um documento PDF pelo serviço Assembler que impede que os usuários digitem dados em seus campos. Este documento é um formulário PDF não interativo. Por exemplo, a ilustração a seguir mostra um aplicativo de hipoteca que representa um formulário interativo.

Para a finalidade desta discussão, suponha que o seguinte documento DX seja usado.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

Neste documento DDX, observe que o valor é atribuído ao atributo de origem `inDoc`. Nas situações em que apenas um documento PDF de entrada é passado para o serviço Assembler e um documento PDF é retornado e você chama a `invokeOneDocument` operação, atribua o valor `inDoc` ao atributo de origem PDF. Ao chamar a `invokeOneDocument` operação, o `inDoc` valor é uma chave predefinida que deve ser especificada no documento DX.

Por outro lado, ao passar dois ou mais documentos PDF de entrada para o serviço Assembler, é possível chamar a `invokeDDX` operação. Nessa situação, atribua o nome do arquivo do documento PDF de entrada ao `source` atributo.

Este documento DDX contém o `NoXFA` elemento, que instrui o serviço Assembler a retornar um documento PDF não interativo.

O serviço Assembler pode reunir documentos PDF não interativos sem que o serviço de Saída faça parte da instalação de formulários AEM se o documento PDF de entrada for baseado em um formulário Acrobat ou XFA estático. Entretanto, se o documento PDF de entrada for um formulário XFA dinâmico, o serviço de Saída deverá fazer parte da instalação de formulários AEM. Se o serviço de Saída não fizer parte da instalação de formulários AEM quando um formulário XFA dinâmico for montado, uma exceção será lançada. Consulte [Criação de fluxos](/help/forms/developing/creating-document-output-streams.md)de saída de documentos.

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos PDF usando o serviço Assembler. Esta seção não discute conceitos, como criar um objeto de coleção que contenha documentos de entrada ou aprender a extrair os resultados do objeto de coleção retornado. (Consulte Montagem [Programática De Documentos](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF.)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

>[!NOTE]
>
>Para obter mais informações sobre um documento DX, consulte Serviço de [Montagem e Referência](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Resumo das etapas {#summary-of-steps}

Para montar um documento PDF não interativo, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente do Montador de PDF.
1. Faça referência a um documento DDX existente.
1. Faça referência a um documento PDF interativo.
1. Defina as opções de tempo de execução.
1. Monte o documento PDF.
1. Salve o documento PDF não interativo.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado em JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms está implantado.

**Criar um cliente Assembler**

Antes de poder executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Este documento DDX deve conter o `NoXFA` elemento, que instrui o serviço Assembler a retornar um documento PDF não interativo.

**Referência a um documento PDF interativo**

Um documento PDF interativo deve ser referenciado e passado ao serviço Assembler para recuperar um documento PDF não interativo.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando uma tarefa se um erro for encontrado.

**Montagem do documento PDF**

Depois de criar o cliente do serviço Assembler, consultar o documento DDX, fazer referência a um documento PDF interativo e definir opções de tempo de execução, você pode chamar a `invokeOneDocument` operação. Como apenas um documento PDF de entrada é transmitido ao serviço Assembler e um único documento é retornado, você pode usar a `invokeOneDocument` operação em vez da `invokeDDX` .

**Salvar o documento PDF não interativo**

Se apenas um único documento PDF for transmitido ao serviço Assembler, o serviço Assembler retornará um único documento em vez de um objeto de coleção. Ou seja, ao invocar a `invokeOneDocument` operação, um único documento é retornado. Como o documento DX mencionado nesta seção contém instruções para criar um documento PDF não interativo, o serviço Assembler retorna um documento PDF não interativo que pode ser salvo como um arquivo PDF.

**Consulte também:**

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem Programática de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar um documento PDF não interativo usando a API Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Monte um documento PDF não interativo usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente Assembler.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `AssemblerServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que represente o documento DX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DX.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Faça referência a um documento PDF interativo.

   * Crie um `java.io.FileInputStream` objeto usando seu construtor e transmitindo o local de um documento PDF interativo.
   * Crie um `com.adobe.idp.Document` objeto e passe o `java.io.FileInputStream` objeto que contém o documento PDF. Esse `com.adobe.idp.Document` objeto é passado para o `invokeOneDocument` método.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, chame o `AssemblerOptionSpec` método do `setFailOnError` objeto e passe `false`.

1. Monte o documento PDF.

   Chame o método do `AssemblerServiceClient` objeto `invokeOneDocument` e passe os seguintes valores:

   * Um `com.adobe.idp.Document` objeto que representa o documento DX. Certifique-se de que esse documento DDX contenha o valor `inDoc` do elemento de origem do PDF.
   * Um `com.adobe.idp.Document` objeto que contém o documento PDF interativo.
   * Um `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log de trabalhos.
   O `invokeOneDocument` método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo.

   * Crie um `java.io.File` objeto e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o método do `Document` objeto para copiar o conteúdo do `copyToFile` `Document` objeto para o arquivo. Certifique-se de usar o `Document` objeto retornado pelo `invokeOneDocument` método.

* &quot;Início rápido (modo SOAP): Montagem de um documento PDF não interativo usando a API Java&quot;

## Montar um documento PDF não interativo usando a API de serviço da Web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Monte um documento PDF não interativo usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente Assembler.

   * Crie um `AssemblerServiceClient` objeto usando seu construtor padrão.
   * Crie um `AssemblerServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço de formulários AEM (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar o `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `AssemblerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a um documento DDX existente.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento DX.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DX e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Faça referência a um documento PDF interativo.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento PDF de entrada. Esse `BLOB` objeto é passado para o `invokeOneDocument` como um argumento.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF de entrada e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios, atribuindo um valor a um membro de dados que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, atribua `false` ao membro de `AssemblerOptionSpec` dados do objeto `failOnError` .

1. Monte o documento PDF.

   Chame o método do `AssemblerServiceClient` objeto `invokeOneDocument` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o documento DDX
   * Um `BLOB` objeto que representa o documento PDF interativo
   * Um `AssemblerOptionSpec` objeto que especifica opções de tempo de execução
   O `invokeOneDocument` método retorna um `BLOB` objeto que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo.

   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF não interativo e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do `BLOB` objeto retornado pelo `invokeOneDocument` método. Preencha a matriz de bytes obtendo o valor do campo do `BLOB` objeto `MTOM` .
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.

* &quot;Início rápido (MTOM): Montagem de um documento PDF não interativo usando a API de serviço da Web&quot;.

**Consulte também:**

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
