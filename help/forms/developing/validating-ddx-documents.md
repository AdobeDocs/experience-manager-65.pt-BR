---
title: Validação de documentos DDX
seo-title: Validação de documentos DDX
description: Valide um documento DDX de forma programática usando a API do Java e a API do serviço da Web.
seo-description: Valide um documento DDX de forma programática usando a API do Java e a API do serviço da Web.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---


# Validando documentos DDX {#validating-ddx-documents}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

Você pode validar programaticamente um documento DDX usado pelo serviço Assembler. Ou seja, usando a API do serviço Assembler, é possível determinar se um documento DDX é válido ou não. Por exemplo, se você atualizou de uma versão anterior do AEM Forms e quiser garantir que seu documento DDX seja válido, poderá validá-lo usando a API do serviço Assembler.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de Serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para validar um documento DDX, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Assembler.
1. Faça referência a um documento DDX existente.
1. Defina opções de tempo de execução para validar o documento DDX.
1. Execute a validação.
1. Salve os resultados de validação em um arquivo de log.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado.

**Criar um cliente do Assembler do PDF**

Antes de poder executar programaticamente uma operação Assembler, é necessário criar um cliente de serviço Assembler.

**Referência a um documento DDX existente**

Para validar um documento DDX, você deve referenciar um documento DDX existente.

**Definir opções de tempo de execução para validar o documento DDX**

Ao validar um documento DDX, você deve definir opções específicas de tempo de execução que instruam o serviço Assembler a validar o documento DDX em vez de executá-lo. Além disso, você pode aumentar a quantidade de informações que o serviço Assembler grava no arquivo de log.

**Executar a validação**

Depois de criar o cliente do serviço Assembler, fazer referência ao documento DDX e definir opções de tempo de execução, você pode chamar a operação `invokeDDX` para validar o documento DDX. Ao validar o documento DDX, você pode passar `null` como parâmetro de mapa (esse parâmetro geralmente armazena documentos PDF que o Assembler requer para executar a(s) operação(ões) especificada(s) no documento DDX).

Se a validação falhar, uma exceção será lançada e o arquivo de log conterá detalhes que explicam por que o documento DDX é inválido podem ser obtidos da instância `OperationException`. Depois de passar a análise básica do XML e a verificação do esquema, a validação em relação à especificação do DDX é executada. Todos os erros localizados no documento DDX são especificados no log.

**Salve os resultados de validação em um arquivo de log**

O serviço Assembler retorna os resultados de validação que você pode gravar em um arquivo de log XML. A quantidade de detalhes que o serviço Assembler grava no arquivo de log depende da opção de tempo de execução que você definiu.

**Consulte também:**

[Validar um documento DDX usando a API Java](#validate-a-ddx-document-using-the-java-api)

[Validar um documento DDX usando a API do serviço da Web](#validate-a-ddx-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Validar um documento DDX usando a API Java {#validate-a-ddx-document-using-the-java-api}

Valide um documento DDX usando a API do Serviço de Assembler (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente Assembler do PDF.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Faça referência a um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifique o local do arquivo DX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Defina opções de tempo de execução para validar o documento DDX.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor .
   * Defina a opção de tempo de execução que instrui o serviço Assembler a validar o documento DDX chamando o método setValidateOnly do objeto `AssemblerOptionSpec` e transmitindo `true`.
   * Defina a quantidade de informações que o serviço Assembler grava no arquivo de log chamando o método `AssemblerOptionSpec` do objeto `getLogLevel` e transmitindo um valor de string atende aos seus requisitos. Ao validar um documento DDX, você deseja que mais informações sejam gravadas no arquivo de log que ajudará no processo de validação. Como resultado, você pode passar o valor `FINE` ou `FINER`.

1. Execute a validação.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX.
   * O valor `null` para o objeto java.io.Map que geralmente armazena documentos PDF.
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução.

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém informações que especificam se o documento DDX é válido.

1. Salve os resultados de validação em um arquivo de log.

   * Crie um objeto `java.io.File` e verifique se a extensão do nome de arquivo é .xml.
   * Chame o método `AssemblerResult` do objeto `getJobLog`. Esse método retorna uma instância `com.adobe.idp.Document` que contém informações de validação.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo.

   >[!NOTE]
   >
   >Se o documento DDX for inválido, um `OperationException` será lançado. Na declaração catch , você pode chamar o método `OperationException` do objeto `getJobLog`.

**Consulte também:**

[Validação de documentos DDX](#validating-ddx-documents)

[Início rápido (modo SOAP): Validação de documentos DDX usando a API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api)  Java (modo SOAP)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Validar um documento DDX usando a API do serviço da Web {#validate-a-ddx-document-using-the-web-service-api}

Valide um documento DDX usando a API do Serviço de Assembler (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua localhost pelo endereço IP do servidor de formulários.

1. Crie um cliente Assembler do PDF.

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
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e passando a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Defina opções de tempo de execução para validar o documento DDX.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor .
   * Defina a opção de tempo de execução que instrui o serviço Assembler a validar o documento DDX atribuindo o valor true ao membro de dados `AssemblerOptionSpec` do objeto `validateOnly`.
   * Defina a quantidade de informações que o serviço Assembler grava no arquivo de log atribuindo um valor de string ao `AssemblerOptionSpec` membro de dados `logLevel` do objeto. método Ao validar um documento DDX, você deseja que mais informações sejam gravadas no arquivo de log que ajudará no processo de validação. Como resultado, você pode especificar o valor `FINE` ou `FINER`. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte a referência da classe `AssemblerOptionSpec` em [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Execute a validação.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX.
   * O valor `null` para o objeto `Map` que geralmente armazena documentos PDF.
   * Um objeto `AssemblerOptionSpec` que especifica as opções de tempo de execução.

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém informações que especificam se o documento DDX é válido.

1. Salve os resultados de validação em um arquivo de log.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo de log e o modo para abrir o arquivo. Certifique-se de que a extensão do nome de arquivo seja .xml.
   * Crie um objeto `BLOB` que armazena informações de log obtendo o valor do `AssemblerResult` membro de dados `jobLog` do objeto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB`. Preencha a matriz de bytes obtendo o valor do campo `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e passando o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

   >[!NOTE]
   >
   >Se o documento DDX for inválido, um `OperationException` será lançado. Na declaração catch , é possível obter o valor do membro `OperationException` do objeto `jobLog`.

**Consulte também:**

[Validação de documentos DDX](#validating-ddx-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
