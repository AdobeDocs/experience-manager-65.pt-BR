---
title: Validar um documento DDX usando a API do serviço Web
seo-title: Validate a DDX document using theweb service API
description: Use a API de serviço do Assembler para validar um documento DDX.
seo-description: Use the Assembler Service API to validate a DDX document.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Validar um documento DDX usando a API do serviço Web {#validate-a-ddx-document-using-theweb-service-api}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

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

[Validação de documentos DDX](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
