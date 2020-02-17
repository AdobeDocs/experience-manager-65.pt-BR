---
title: Validar um documento DDX usando a API de serviço da Web
seo-title: Validar um documento DDX usando a API de serviço da Web
description: 'null'
seo-description: 'null'
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Validar um documento DDX usando a API de serviço da Web {#validate-a-ddx-document-using-theweb-service-api}

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

[Validação de documentos DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
