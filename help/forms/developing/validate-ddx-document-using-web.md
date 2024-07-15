---
title: Validar um documento DDX usando a API do serviço Web
description: Use a API de serviço do Assembler para validar um documento DDX.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Validar um documento DDX usando a API do serviço Web {#validate-a-ddx-document-using-theweb-service-api}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

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

[Validação de documentos DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
