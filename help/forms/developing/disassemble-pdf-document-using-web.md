---
title: Desmontar um documento PDF usando a API de serviço Web
seo-title: Disassemble a PDF document usingthe web service API
description: Desmontar um documento PDF usando a API de serviço do Assembler
seo-description: Disassemble a PDF document using the Assembler Service API
uuid: d6283dc5-e333-49d0-abde-1d390662f4fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 49584fb4-8c3a-4d73-acd6-0879a67f6093
role: Developer
exl-id: de2f90ad-5dea-40a0-8c6d-d6b08228310d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# Desmontar um documento PDF usando a API de serviço Web {#disassemble-a-pdf-document-usingthe-web-service-api}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

Desmonte um documento PDF usando a API de serviço do Assembler (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao configurar uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

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
   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento DDX e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Referencie um documento do PDF para desmontar.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento PDF de entrada. Este `BLOB` objeto é passado para o `invokeOneDocument` como argumento.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` o conteúdo da matriz de bytes.
   * Criar um `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de coleção é usado para armazenar o PDF a ser desmontado.
   * Criar um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua um valor de string que represente o nome da chave à `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` campo. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX.
   * Atribua a `BLOB` objeto que armazena o documento PDF para o `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` campo.
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto para o `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` object&quot; `Add` e transmita o `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa atribuindo um valor a um membro de dados que pertença à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando um job quando ocorrer um erro, atribua `false` para o `AssemblerOptionSpec` do objeto `failOnError` campo.

1. Desmonte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX que desmonta o documento PDF
   * A variável `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém o documento PDF a ser desmontado
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   A variável `invokeDDX` o método retorna um `AssemblerResult` objeto que contém os resultados do processo e quaisquer exceções que ocorreram.

1. Salve os documentos de PDF desmontados.

   Para obter os documentos PDF recém-criados, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` que é um `Map` objeto que contém os documentos PDF desmontados.
   * Repita através do `Map` para obter cada documento resultante. Em seguida, converta os membros da matriz `value` para um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando seus `BLOB` do objeto `MTOM` propriedade. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também**

[Desmontando Documentos PDF de Forma Programática](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
