---
title: Validação de documentos DDX
seo-title: Validação de documentos DDX
description: 'null'
seo-description: 'null'
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Validação de documentos DDX {#validating-ddx-documents}

Você pode validar programaticamente um documento DDX usado pelo serviço Assembler. Ou seja, usando a API de serviço do Assembler, você pode determinar se um documento DX é válido ou não. Por exemplo, se você atualizou de uma versão anterior do AEM Forms e quiser garantir que seu documento DDX seja válido, é possível validá-lo usando a API de serviço do Assembler.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

>[!NOTE]
>
>Para obter mais informações sobre um documento DX, consulte Serviço de [Montagem e Referência](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Resumo das etapas {#summary-of-steps}

Para validar um documento DDX, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente Assembler.
1. Faça referência a um documento DDX existente.
1. Defina as opções de tempo de execução para validar o documento DX.
1. Execute a validação.
1. Salve os resultados de validação em um arquivo de log.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado em JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms está implantado.

**Criar um cliente de Montador de PDF**

Antes de poder executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referência a um documento DDX existente**

Para validar um documento DDX, é necessário fazer referência a um documento DDX existente.

**Definir opções de tempo de execução para validar o documento DX**

Ao validar um documento DDX, você deve definir opções específicas de tempo de execução que instruem o serviço Assembler a validar o documento DX em vez de executá-lo. Além disso, você pode aumentar a quantidade de informações que o serviço Assembler grava no arquivo de log.

**Executar a validação**

Depois de criar o cliente do serviço Assembler, consultar o documento DX e definir as opções de tempo de execução, você pode chamar a `invokeDDX` operação para validar o documento DX. Ao validar o documento DDX, você pode passar `null` como parâmetro de mapa (esse parâmetro geralmente armazena documentos PDF que o Assembler exige para executar as operações especificadas no documento DX).

Se a validação falhar, uma exceção será lançada e o arquivo de log conterá detalhes que explicam por que o documento DX é inválido pode ser obtido da `OperationException` instância. Após a análise básica do XML e a verificação do esquema, a validação em relação à especificação DDX é realizada. Todos os erros localizados no documento DDX são especificados no log.

**Salvar os resultados de validação em um arquivo de log**

O serviço Assembler retorna os resultados de validação que você pode gravar em um arquivo de log XML. A quantidade de detalhes que o serviço Assembler grava no arquivo de log depende da opção de tempo de execução definida.

**Consulte também:**

[Validar um documento DDX usando a API Java](#validate-a-ddx-document-using-the-java-api)

[Validar um documento DDX usando a API de serviço da Web](#validate-a-ddx-document-using-the-web-service-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem Programática de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Validar um documento DDX usando a API Java {#validate-a-ddx-document-using-the-java-api}

Valide um documento DX usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente do Montador de PDF.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `AssemblerServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que represente o documento DX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DX.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Defina as opções de tempo de execução para validar o documento DX.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina a opção de tempo de execução que instrui o serviço Assembler a validar o documento DX chamando o método setValidateOnly do `AssemblerOptionSpec` objeto e transmitindo `true`.
   * Defina a quantidade de informações que o serviço Assembler grava no arquivo de log chamando o método do `AssemblerOptionSpec` objeto `getLogLevel` e transmitindo um valor de string atende aos seus requisitos. Ao validar um documento DDX, você deseja obter mais informações gravadas no arquivo de log que ajudarão no processo de validação. Como resultado, você pode passar o valor `FINE` ou `FINER`.

1. Execute a validação.

   Chame o método do `AssemblerServiceClient` objeto `invokeDDX` e passe os seguintes valores:

   * Um `com.adobe.idp.Document` objeto que representa o documento DX.
   * O valor `null` do objeto java.io.Map que geralmente armazena documentos PDF.
   * Um `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução.
   O `invokeDDX` método retorna um `AssemblerResult` objeto que contém informações que especificam se o documento DDX é válido.

1. Salve os resultados de validação em um arquivo de log.

   * Crie um `java.io.File` objeto e verifique se a extensão do nome do arquivo é .xml.
   * Chame o `AssemblerResult` método do `getJobLog` objeto. Esse método retorna uma `com.adobe.idp.Document` instância que contém informações de validação.
   * Chame o método do `com.adobe.idp.Document` objeto para copiar o conteúdo do `copyToFile` `com.adobe.idp.Document` objeto para o arquivo.
   >[!NOTE]
   >
   >Se o documento DDX for inválido, um `OperationException` será lançado. Na declaração catch, é possível invocar o `OperationException` método do `getJobLog` objeto.

**Consulte também:**

[Validação de documentos DDX](#validating-ddx-documents)

[Início rápido (modo SOAP): Validação de documentos DX usando a API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) Java (modo SOAP)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Validar um documento DDX usando a API de serviço da Web {#validate-a-ddx-document-using-the-web-service-api}

Valide um documento DX usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua localhost pelo endereço IP do servidor de formulários.

1. Crie um cliente do Montador de PDF.

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
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo sua `MTOM` propriedade ao conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução para validar o documento DX.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina a opção de tempo de execução que instrui o serviço Assembler a validar o documento DX atribuindo o valor true ao membro de `AssemblerOptionSpec` dados do `validateOnly` objeto.
   * Defina a quantidade de informações que o serviço Assembler grava no arquivo de log atribuindo um valor de string ao membro de `AssemblerOptionSpec` dados do `logLevel` objeto. ao validar um documento DDX, você deseja obter mais informações gravadas no arquivo de log que ajudarão no processo de validação. Como resultado, você pode especificar o valor `FINE` ou `FINER`. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte a referência de `AssemblerOptionSpec` classe em Referência [de API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

1. Execute a validação.

   Chame o método do `AssemblerServiceClient` objeto `invokeDDX` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o documento DX.
   * O valor `null` para o `Map` objeto que geralmente armazena documentos PDF.
   * Um `AssemblerOptionSpec` objeto que especifica opções de tempo de execução.
   O `invokeDDX` método retorna um `AssemblerResult` objeto que contém informações que especificam se o documento DDX é válido.

1. Salve os resultados de validação em um arquivo de log.

   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do arquivo de log e o modo para abrir o arquivo. Verifique se a extensão do nome do arquivo é .xml.
   * Crie um `BLOB` objeto que armazene informações de log obtendo o valor do membro de `AssemblerResult` dados do `jobLog` objeto.
   * Crie uma matriz de bytes que armazene o conteúdo do `BLOB` objeto. Preencha a matriz de bytes obtendo o valor do campo do `BLOB` objeto `MTOM` .
   * Crie um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método do `System.IO.BinaryWriter` objeto `Write` e transmitindo a matriz de bytes.
   >[!NOTE]
   >
   >Se o documento DDX for inválido, um `OperationException` será lançado. Na declaração catch, é possível obter o valor do membro do `OperationException` objeto `jobLog` .

**Consulte também:**

[Validação de documentos DDX](#validating-ddx-documents)

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
