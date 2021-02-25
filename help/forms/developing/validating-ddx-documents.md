---
title: Validação de Documentos DDX
seo-title: Validação de Documentos DDX
description: Valide um documento DX de forma programática usando a API Java e a API de serviço da Web.
seo-description: Valide um documento DX de forma programática usando a API Java e a API de serviço da Web.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 0%

---


# Validando Documentos DDX {#validating-ddx-documents}

**Exemplos e exemplos neste documento são apenas para AEM Forms no ambiente JEE.**

Você pode validar programaticamente um documento DDX usado pelo serviço Assembler. Ou seja, usando a API de serviço do Assembler, você pode determinar se um documento DX é válido ou não. Por exemplo, se você atualizou de uma versão anterior do AEM Forms e deseja garantir que seu documento DDX seja válido, é possível validá-lo usando a API de serviço do Assembler.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para validar um documento DDX, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Criar um cliente Assembler.
1. Faça referência a um documento DDX existente.
1. Defina as opções de tempo de execução para validar o documento DDX.
1. Execute a validação.
1. Salve os resultados de validação em um arquivo de log.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

se a AEM Forms for implantada em um servidor de aplicativos J2EE compatível que não seja JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual a AEM Forms está implantada.

**Criar um cliente de Montador de PDF**

Antes de poder executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referência a um documento DDX existente**

Para validar um documento DDX, é necessário fazer referência a um documento DDX existente.

**Definir opções de tempo de execução para validar o documento DDX**

Ao validar um documento DDX, você deve definir opções específicas de tempo de execução que instruem o serviço Assembler a validar o documento DX em vez de executá-lo. Além disso, você pode aumentar a quantidade de informações que o serviço Assembler grava no arquivo de log.

**Executar a validação**

Depois de criar o cliente do serviço Assembler, consultar o documento DDX e definir as opções de tempo de execução, você pode chamar a operação `invokeDDX` para validar o documento DDX. Ao validar o documento DDX, você pode passar `null` como parâmetro de mapa (esse parâmetro geralmente armazena documentos PDF que o Assembler exige para executar as operações especificadas no documento DX).

Se a validação falhar, uma exceção será lançada e o arquivo de log conterá detalhes que explicam por que o documento DX é inválido pode ser obtido da instância `OperationException`. Após a análise básica de XML e a verificação de schema, a validação em relação à especificação DDX é realizada. Todos os erros localizados no documento DDX são especificados no log.

**Salvar os resultados de validação em um arquivo de log**

O serviço Assembler retorna os resultados de validação que você pode gravar em um arquivo de log XML. A quantidade de detalhes que o serviço Assembler grava no arquivo de log depende da opção de tempo de execução definida.

**Consulte também:**

[Validar um documento DX usando a API Java](#validate-a-ddx-document-using-the-java-api)

[Validar um documento DDX usando a API de serviço da Web](#validate-a-ddx-document-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Validar um documento DX usando a API Java {#validate-a-ddx-document-using-the-java-api}

Valide um documento DDX usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente do Montador de PDF.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Faça referência a um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Defina as opções de tempo de execução para validar o documento DDX.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina a opção de tempo de execução que instrui o serviço Assembler a validar o documento DDX chamando o método setValidateOnly do objeto `AssemblerOptionSpec` e transmitindo `true`.
   * Defina a quantidade de informações que o serviço Assembler grava no arquivo de log chamando o método `AssemblerOptionSpec` do objeto `getLogLevel` e transmitindo um valor de string atende aos seus requisitos. Ao validar um documento DDX, você deseja obter mais informações gravadas no arquivo de log que ajudarão no processo de validação. Como resultado, você pode passar o valor `FINE` ou `FINER`.

1. Execute a validação.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX.
   * O valor `null` para o objeto java.io.Map que geralmente armazena documentos PDF.
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução.

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém informações que especificam se o documento DDX é válido.

1. Salve os resultados de validação em um arquivo de log.

   * Crie um objeto `java.io.File` e verifique se a extensão do nome do arquivo é .xml.
   * Chame o método `AssemblerResult` do objeto `getJobLog`. Este método retorna uma instância `com.adobe.idp.Document` que contém informações de validação.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo do objeto `com.adobe.idp.Document` para o arquivo.

   >[!NOTE]
   >
   >Se o documento DDX for inválido, um `OperationException` será lançado. Na declaração catch, você pode chamar o método `OperationException` do objeto `getJobLog`.

**Consulte também:**

[Validação de Documentos DDX](#validating-ddx-documents)

[Start rápido (modo SOAP): Validação de documentos DX usando a API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api)  Java (modo SOAP)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Validar um documento DDX usando a API de serviço da Web {#validate-a-ddx-document-using-the-web-service-api}

Valide um documento DDX usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua localhost pelo endereço IP do servidor de formulários.

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

1. Faça referência a um documento DDX existente.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento DDX.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DX e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução para validar o documento DDX.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina a opção de tempo de execução que instrui o serviço Assembler a validar o documento DDX atribuindo o valor true ao membro de dados `AssemblerOptionSpec` do objeto `validateOnly`.
   * Defina a quantidade de informações que o serviço Assembler grava no arquivo de log atribuindo um valor de string ao membro de dados `AssemblerOptionSpec` do objeto `logLevel`. ao validar um documento DDX, você deseja obter mais informações gravadas no arquivo de log que ajudarão no processo de validação. Como resultado, você pode especificar o valor `FINE` ou `FINER`. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte a referência de classe `AssemblerOptionSpec` em [Referência de API da AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Execute a validação.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX.
   * O valor `null` para o objeto `Map` que geralmente armazena documentos PDF.
   * Um objeto `AssemblerOptionSpec` que especifica opções de tempo de execução.

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém informações que especificam se o documento DDX é válido.

1. Salve os resultados de validação em um arquivo de log.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo de log e o modo para abrir o arquivo. Verifique se a extensão do nome do arquivo é .xml.
   * Crie um objeto `BLOB` que armazene informações de log obtendo o valor do membro `AssemblerResult` de `jobLog` dados do objeto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB`. Preencha a matriz de bytes obtendo o valor do campo `BLOB` `MTOM` do objeto.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

   >[!NOTE]
   >
   >Se o documento DDX for inválido, um `OperationException` será lançado. Na declaração catch, você pode obter o valor do membro `OperationException` do objeto `jobLog`.

**Consulte também:**

[Validação de Documentos DDX](#validating-ddx-documents)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
