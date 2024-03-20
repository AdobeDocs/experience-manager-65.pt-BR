---
title: Montagem de Documentos PDF Criptografados
description: Combine documentos de PDF criptografados usando a API Java e a API de serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 0%

---

# Montagem de Documentos PDF Criptografados {#assembling-encrypted-pdf-documents}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

Você pode criptografar um documento PDF com uma senha usando o serviço Assembler. Depois que um documento PDF é criptografado com uma senha, um usuário deve especificar a senha para exibir o documento PDF no Adobe Reader ou Acrobat. Para criptografar um documento PDF com uma senha, o documento DDX deve conter valores de elementos de criptografia necessários para criptografar um documento PDF.

Para o propósito desta discussão, suponha que o seguinte documento DDX seja usado.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="EncryptLoan.pdf" encryption="userProtect">
         <PDF source="inDoc" />
     </PDF>
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
         <OpenPassword>AdobeOpen</OpenPassword>
        </PasswordEncryptionProfile>
 </DDX>
```

Neste documento DDX, observe que o valor é atribuído ao atributo de origem `inDoc`. Em situações em que apenas um documento de PDF de entrada é passado para o serviço Assembler e um documento de PDF é retornado, e você chama o `invokeOneDocument` , atribua o valor `inDoc` para o atributo de origem PDF. Ao invocar a variável `invokeOneDocument` operação, a variável `inDoc` é uma chave predefinida que deve ser especificada no documento DDX.

Por outro lado, ao passar dois ou mais documentos de PDF de entrada para o serviço Assembler, você pode chamar o `invokeDDX` operação. Nessa situação, atribua o nome de arquivo do documento de PDF de entrada ao `source` atributo.

O serviço de criptografia não precisa fazer parte da instalação dos formulários AEM para criptografar um documento PDF com uma senha. Consulte [Criptografar e descriptografar documentos do PDF](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar um documento PDF criptografado, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDF Assembler.
1. Consulte um documento DDX existente.
1. Referencie um documento de PDF não seguro.
1. Definir opções de tempo de execução.
1. Criptografe o documento.
1. Salve o documento PDF criptografado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado. Para obter informações sobre a localização de todos os arquivos JAR do AEM Forms, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente do Assembler**

Antes de executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referencie um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Por exemplo, considere o documento DDX introduzido nesta seção. Para criptografar um documento PDF, o documento DDX deve conter a `PasswordEncryptionProfile` elemento.

**Referenciar um documento de PDF não seguro**

Um documento de PDF não seguro deve ser referenciado e passado para o serviço Assembler para criptografá-lo. Se você fizer referência a um documento PDF que já está criptografado, uma exceção será lançada.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte `AssemblerOptionSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Criptografar o documento**

Depois de criar o cliente de serviço do Assembler, fazer referência ao documento DDX que contém informações de criptografia, fazer referência a um documento PDF não seguro e definir opções de tempo de execução, você poderá chamar a `invokeOneDocument` operação. Como apenas um documento de PDF de entrada está sendo passado para o serviço Assembler (e um documento está sendo retornado), você pode usar o `invokeOneDocument` operação em vez de `invokeDDX` operação.

**Salve o documento PDF criptografado**

Se apenas um único documento de PDF for passado para o serviço Assembler, o serviço Assembler retornará um único documento em vez de um objeto de coleção. Ou seja, ao invocar o princípio `invokeOneDocument` um único documento é retornado. Como o documento DDX referenciado nesta seção contém informações de criptografia, o serviço Assembler retorna um documento PDF que é criptografado com uma senha.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar um documento PDF criptografado usando a API Java {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do projeto Java.

1. Criar um cliente Assembler.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `AssemblerServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Consulte um documento DDX existente.

   * Criar um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DDX.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Referencie um documento de PDF não seguro.

   * Criar um `java.io.FileInputStream` usando seu construtor e transmitindo o local de um documento PDF não seguro.
   * Criar um `com.adobe.idp.Document` e transmita o `java.io.FileInputStream` objeto que contém o documento PDF. Este `com.adobe.idp.Document` objeto é passado para o `invokeOneDocument` método.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa, chamando um método que pertence à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler para continuar processando um job quando ocorrer um erro, chame o `AssemblerOptionSpec` do objeto `setFailOnError` e passar `false`.

1. Criptografe o documento.

   Chame o `AssemblerServiceClient` do objeto `invokeOneDocument` e passe os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX. Verifique se este documento DDX contém o valor `inDoc` para o elemento de origem PDF.
   * A `com.adobe.idp.Document` objeto que contém o documento PDF não seguro.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do job.

   A variável `invokeOneDocument` o método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF criptografado por senha.

1. Salve o documento PDF criptografado.

   * Criar um `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo. Certifique-se de usar o `Document` objeto que o `invokeOneDocument` método retornado.

**Consulte também**

[Início rápido (modo SOAP): montagem de um documento PDF criptografado usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Montar um documento PDF criptografado usando a API de serviço Web {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao configurar uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente Assembler.

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

1. Referencie um documento de PDF não seguro.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento PDF de entrada. Este `BLOB` objeto é passado para o `invokeOneDocument` como argumento.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa atribuindo um valor a um membro de dados que pertença à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando um job quando ocorrer um erro, atribua `false` para o `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Criptografe o documento.

   Chame o `AssemblerServiceClient` do objeto `invokeOneDocument` e passe os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX
   * A `BLOB` objeto que representa o documento PDF não seguro
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   A variável `invokeOneDocument` o método retorna um `BLOB` objeto que contém um documento PDF criptografado.

1. Salve o documento PDF criptografado.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto que o `invokeOneDocument` método retornado. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
