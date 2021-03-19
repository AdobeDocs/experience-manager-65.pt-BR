---
title: Validar um documento DDX usando a API do serviço da Web
seo-title: Validar um documento DDX usando a API do serviço da Web
description: Use a API do Serviço de Assembler para validar um documento DDX.
seo-description: Use a API do Serviço de Assembler para validar um documento DDX.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Validar um documento DDX usando a API do serviço da Web {#validate-a-ddx-document-using-theweb-service-api}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

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

[Validação de documentos DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
