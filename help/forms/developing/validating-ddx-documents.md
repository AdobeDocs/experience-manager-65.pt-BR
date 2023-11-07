---
title: Validação de documentos DDX
seo-title: Validating DDX Documents
description: Valide um documento DDX de forma programática usando a API Java e a API do Serviço da Web.
seo-description: Validate a DDX document programmatically using the Java API and the Web Service API.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 0%

---

# Validação de documentos DDX {#validating-ddx-documents}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

Você pode validar programaticamente um documento DDX usado pelo serviço do Assembler. Ou seja, usando a API de serviço do Assembler, você pode determinar se um documento DDX é válido ou não. Por exemplo, se você atualizou de uma versão anterior do AEM Forms e deseja garantir que seu documento DDX é válido, é possível validá-lo usando a API de serviço do Assembler.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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

**Criar um cliente do PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referencie um documento DDX existente**

Para validar um documento DDX, você deve consultar um documento DDX existente.

**Definir opções de tempo de execução para validar o documento DDX**

Ao validar um documento DDX, você deve definir opções de tempo de execução específicas que instruam o serviço Assembler a validar o documento DDX em vez de executá-lo. Além disso, você pode aumentar a quantidade de informações que o serviço Assembler grava no arquivo de log.

**Executar a validação**

Depois de criar o cliente de serviço do Assembler, fazer referência ao documento DDX e definir as opções de tempo de execução, você poderá chamar o `invokeDDX` operação para validar o documento DDX. Ao validar o documento DDX, você pode enviar `null` como o parâmetro de mapa (este parâmetro geralmente armazena documentos de PDF que o Assembler requer para executar a(s) operação(ões) especificada(s) no documento DDX).

Se a validação falhar, uma exceção será lançada e o arquivo de log conterá detalhes que explicam por que o documento DDX é inválido e podem ser obtidos no `OperationException` instância. Depois da análise XML básica e da verificação do esquema, a validação em relação à especificação DDX é executada. Todos os erros do documento DDX estão especificados no log.

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

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `AssemblerServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Consulte um documento DDX existente.

   * Criar um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DDX.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Defina as opções de tempo de execução para validar o documento DDX.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina a opção de tempo de execução que instrui o serviço Assembler a validar o documento DDX chamando o `AssemblerOptionSpec` método setValidateOnly e transmissão do objeto `true`.
   * Defina a quantidade de informações que o serviço Assembler grava no arquivo de log chamando o `AssemblerOptionSpec` do objeto `getLogLevel` e transmitir um valor de string atende aos seus requisitos. Ao validar um documento DDX, você deseja que mais informações sejam gravadas no arquivo de log que auxiliará no processo de validação. Como resultado, você pode passar o valor `FINE` ou `FINER`.

1. Execute a validação.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX.
   * O valor `null` para o objeto java.io.Map que geralmente armazena documentos PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução.

   A variável `invokeDDX` o método retorna um `AssemblerResult` objeto que contém informações que especificam se o documento DDX é válido.

1. Salve os resultados da validação em um arquivo de log.

   * Criar um `java.io.File` e certifique-se de que a extensão do nome do arquivo seja .xml.
   * Chame o `AssemblerResult` do objeto `getJobLog` método. Este método retorna um valor de `com.adobe.idp.Document` instância que contém informações de validação.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo.

   >[!NOTE]
   >
   >Se o documento DDX for inválido, uma `OperationException` é lançado. Na instrução catch, você pode chamar a variável `OperationException` do objeto `getJobLog` método.

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
   >Substitua localhost pelo endereço IP do servidor de formulários.

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

1. Consulte um documento DDX existente.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento DDX.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DDX e o modo em que o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução para validar o documento DDX.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina a opção de tempo de execução que instrui o serviço Assembler a validar o documento DDX atribuindo o valor true ao `AssemblerOptionSpec` do objeto `validateOnly` membro de dados.
   * Defina a quantidade de informações que o serviço Assembler grava no arquivo de log atribuindo um valor de string ao `AssemblerOptionSpec` do objeto `logLevel` membro de dados. método Ao validar um documento DDX, você deseja que mais informações sejam gravadas no arquivo de log que auxiliará no processo de validação. Como resultado, é possível especificar o valor `FINE` ou `FINER`. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte `AssemblerOptionSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Execute a validação.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX.
   * O valor `null` para o `Map` objeto que geralmente armazena documentos PDF.
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução.

   A variável `invokeDDX` o método retorna um `AssemblerResult` objeto que contém informações que especificam se o documento DDX é válido.

1. Salve os resultados da validação em um arquivo de log.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo de log e o modo em que o arquivo será aberto. Verifique se a extensão do nome do arquivo é .xml.
   * Criar um `BLOB` objeto que armazena informações de log obtendo o valor do `AssemblerResult` do objeto `jobLog` membro de dados.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` campo.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

   >[!NOTE]
   >
   >Se o documento DDX for inválido, uma `OperationException` é lançado. Na instrução catch, é possível obter o valor de `OperationException` do objeto `jobLog` membro.

**Consulte também**

[Validação de documentos DDX](#validating-ddx-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
