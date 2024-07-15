---
title: Validação de documentos DDX
description: Valide um documento DDX de forma programática usando a API Java e a API do Serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 0%

---

# Validação de documentos DDX {#validating-ddx-documents}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

Você pode validar programaticamente um documento DDX usado pelo serviço do Assembler. Ou seja, usando a API de serviço do Assembler, você pode determinar se um documento DDX é válido ou não. Por exemplo, se você atualizou de uma versão anterior do AEM Forms e deseja garantir que seu documento DDX é válido, é possível validá-lo usando a API de serviço do Assembler.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço do Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para validar um documento DDX, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente Assembler.
1. Consulte um documento DDX existente.
1. Defina as opções de tempo de execução para validar o documento DDX.
1. Execute a validação.
1. Salve os resultados da validação em um arquivo de log.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado.

**Criar um cliente PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referenciar um documento DDX existente**

Para validar um documento DDX, você deve consultar um documento DDX existente.

**Definir opções de tempo de execução para validar o documento DDX**

Ao validar um documento DDX, você deve definir opções de tempo de execução específicas que instruam o serviço Assembler a validar o documento DDX em vez de executá-lo. Além disso, você pode aumentar a quantidade de informações que o serviço Assembler grava no arquivo de log.

**Executar a validação**

Depois de criar o cliente de serviço do Assembler, fazer referência ao documento DDX e definir opções de tempo de execução, você poderá invocar a operação `invokeDDX` para validar o documento DDX. Ao validar o documento DDX, você pode passar `null` como parâmetro de mapa (esse parâmetro geralmente armazena documentos de PDF que o Assembler requer para executar a(s) operação(ões) especificada(s) no documento DDX).

Se a validação falhar, uma exceção será lançada e o arquivo de log conterá detalhes que explicam por que o documento DDX é inválido e que podem ser obtidos da instância `OperationException`. Depois da análise XML básica e da verificação do esquema, a validação em relação à especificação DDX é executada. Todos os erros do documento DDX estão especificados no log.

**Salvar os resultados da validação em um arquivo de log**

O serviço do Assembler retorna os resultados da validação que você pode gravar em um arquivo de log XML. A quantidade de detalhes gravada pelo serviço Assembler no arquivo de log depende da opção de tempo de execução definida.

**Consulte também**

[Validar um documento DDX usando a API Java](#validate-a-ddx-document-using-the-java-api)

[Validar um documento DDX usando a API do serviço Web](#validate-a-ddx-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Validar um documento DDX usando a API Java {#validate-a-ddx-document-using-the-java-api}

Valide um documento DDX usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente PDF Assembler.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Consulte um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do arquivo DDX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Defina as opções de tempo de execução para validar o documento DDX.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina a opção de tempo de execução que instrui o serviço Assembler a validar o documento DDX invocando o método setValidateOnly do objeto `AssemblerOptionSpec` e transmitindo `true`.
   * Defina a quantidade de informações que o serviço Assembler grava no arquivo de log, chamando o método `getLogLevel` do objeto `AssemblerOptionSpec` e transmitindo um valor de cadeia de caracteres que atenda aos seus requisitos. Ao validar um documento DDX, você deseja que mais informações sejam gravadas no arquivo de log que auxiliará no processo de validação. Como resultado, você pode passar o valor `FINE` ou `FINER`.

1. Execute a validação.

   Chame o método `invokeDDX` do objeto `AssemblerServiceClient` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX.
   * O valor `null` do objeto java.io.Map que geralmente armazena documentos PDF.
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução.

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém informações que especificam se o documento DDX é válido.

1. Salve os resultados da validação em um arquivo de log.

   * Crie um objeto `java.io.File` e verifique se a extensão do nome do arquivo é .xml.
   * Invoque o método `getJobLog` do objeto `AssemblerResult`. Este método retorna uma instância `com.adobe.idp.Document` que contém informações de validação.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo.

   >[!NOTE]
   >
   >Se o documento DDX for inválido, `OperationException` será lançado. Na instrução catch, você pode invocar o método `getJobLog` do objeto `OperationException`.

**Consulte também**

[Validação de documentos DDX](#validating-ddx-documents)

[Início rápido (modo SOAP): validação de documentos DDX usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) (modo SOAP)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Validar um documento DDX usando a API do serviço Web {#validate-a-ddx-document-using-the-web-service-api}

Valide um documento DDX usando a API de serviço do Assembler (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua localhost pelo endereço IP do Forms Server.

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

1. Consulte um documento DDX existente.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento DDX.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento DDX e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` com o conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução para validar o documento DDX.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina a opção de tempo de execução que instrui o serviço Assembler a validar o documento DDX atribuindo o valor true ao membro de dados `validateOnly` do objeto `AssemblerOptionSpec`.
   * Defina a quantidade de informações que o serviço Assembler grava no arquivo de log atribuindo um valor de cadeia de caracteres ao membro de dados `logLevel` do objeto `AssemblerOptionSpec`. método Ao validar um documento DDX, você deseja que mais informações sejam gravadas no arquivo de log que auxiliará no processo de validação. Como resultado, você pode especificar o valor `FINE` ou `FINER`. Para obter informações sobre as opções de tempo de execução que você pode definir, consulte a referência de classe `AssemblerOptionSpec` na [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Execute a validação.

   Chame o método `invokeDDX` do objeto `AssemblerServiceClient` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX.
   * O valor `null` do objeto `Map` que geralmente armazena documentos PDF.
   * Um objeto `AssemblerOptionSpec` que especifica opções de tempo de execução.

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém informações que especificam se o documento DDX é válido.

1. Salve os resultados da validação em um arquivo de log.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo de log e o modo em que o arquivo será aberto. Verifique se a extensão do nome do arquivo é .xml.
   * Crie um objeto `BLOB` que armazene informações de log obtendo o valor do membro de dados `jobLog` do objeto `AssemblerResult`.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB`. Popular a matriz de bytes obtendo o valor do campo `MTOM` do objeto `BLOB`.
   * Crie um objeto `System.IO.BinaryWriter` invocando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o método `Write` do objeto `System.IO.BinaryWriter` e transmitindo a matriz de bytes.

   >[!NOTE]
   >
   >Se o documento DDX for inválido, `OperationException` será lançado. Na instrução catch, você pode obter o valor do membro `jobLog` do objeto `OperationException`.

**Consulte também**

[Validação de documentos DDX](#validating-ddx-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
