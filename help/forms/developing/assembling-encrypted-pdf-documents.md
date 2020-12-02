---
title: Montagem de Documentos PDF criptografados
seo-title: Montagem de Documentos PDF criptografados
description: 'null'
seo-description: nulo
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 0%

---


# Montagem de Documentos PDF criptografados {#assembling-encrypted-pdf-documents}

É possível criptografar um documento PDF com uma senha usando o serviço Assembler. Depois que um documento PDF é criptografado com uma senha, o usuário deve especificar a senha para visualização do documento PDF no Adobe Reader ou Acrobat. Para criptografar um documento PDF com uma senha, o documento DDX deve conter valores de elementos de criptografia necessários para criptografar um documento PDF.

Para a finalidade desta discussão, suponha que o seguinte documento DX seja usado.

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

Nesse documento DDX, observe que o valor `inDoc` é atribuído ao atributo source. Nas situações em que apenas um documento PDF de entrada é passado para o serviço Assembler e um documento PDF é retornado e você chama a operação `invokeOneDocument`, atribua o valor `inDoc` ao atributo de origem do PDF. Ao invocar a operação `invokeOneDocument`, o valor `inDoc` é uma chave predefinida que deve ser especificada no documento DX.

Por outro lado, ao transmitir dois ou mais documentos PDF de entrada ao serviço Assembler, você pode chamar a operação `invokeDDX`. Nessa situação, atribua o nome do arquivo do documento PDF de entrada ao atributo `source`.

O serviço de criptografia não precisa fazer parte da instalação de formulários AEM para criptografar um documento PDF com uma senha. Consulte [Criptografando e descriptografando Documentos PDF](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar um documento PDF criptografado, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um cliente do Montador de PDF.
1. Faça referência a um documento DDX existente.
1. Referência a um documento PDF não protegido.
1. Defina as opções de tempo de execução.
1. Criptografe o documento.
1. Salve o documento PDF criptografado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

se a AEM Forms for implantada em um servidor de aplicativos J2EE compatível que não seja JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual a AEM Forms está implantada. Para obter informações sobre a localização de todos os arquivos AEM Forms JAR, consulte [Incluindo arquivos da biblioteca AEM Forms Java](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente Assembler**

Antes de poder executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Por exemplo, considere o documento DDX que foi introduzido nesta seção. Para criptografar um documento PDF, o documento DDX deve conter o elemento `PasswordEncryptionProfile`.

**Referência a um documento PDF não protegido**

Um documento PDF não protegido deve ser referenciado e passado ao serviço Assembler para criptografá-lo. Se você fizer referência a um documento PDF que já está criptografado, uma exceção será lançada.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando uma tarefa se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte a referência de classe `AssemblerOptionSpec` em [Referência de API da AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Criptografar o documento**

Depois de criar o cliente de serviço Assembler, consulte o documento DDX que contém informações de criptografia, consulte um documento PDF não protegido e defina as opções de tempo de execução, você pode chamar a operação `invokeOneDocument`. Como apenas um documento PDF de entrada está sendo transmitido ao serviço Assembler (e um documento está sendo retornado), você pode usar a operação `invokeOneDocument` em vez da operação `invokeDDX`.

**Salvar o documento PDF criptografado**

Se apenas um único documento PDF estiver sendo transmitido ao serviço Assembler, o serviço Assembler retornará um único documento em vez de um objeto de coleção. Ou seja, ao chamar a operação `invokeOneDocument`, um único documento é retornado. Como o documento DX mencionado nesta seção contém informações de criptografia, o serviço Assembler retorna um documento PDF criptografado com uma senha.

**Consulte também:**

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montagem de um documento PDF criptografado usando a API Java {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Criar um cliente Assembler.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Faça referência a um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Referência a um documento PDF não protegido.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local de um documento PDF não protegido.
   * Crie um objeto `com.adobe.idp.Document` e passe o objeto `java.io.FileInputStream` que contém o documento PDF. Esse objeto `com.adobe.idp.Document` é passado para o método `invokeOneDocument`.

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios chamando um método que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, chame o método `AssemblerOptionSpec` do objeto `setFailOnError` e passe `false`.

1. Criptografe o documento.

   Chame o método `AssemblerServiceClient` do objeto `invokeOneDocument` e passe os seguintes valores:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX. Verifique se esse documento DDX contém o valor `inDoc` para o elemento de origem do PDF.
   * Um objeto `com.adobe.idp.Document` que contém o documento PDF não protegido.
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log de trabalhos.

   O método `invokeOneDocument` retorna um objeto `com.adobe.idp.Document` que contém um documento PDF criptografado por senha.

1. Salve o documento PDF criptografado.

   * Crie um objeto `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o método `Document` do objeto `copyToFile` para copiar o conteúdo do objeto `Document` para o arquivo. Certifique-se de usar o objeto `Document` retornado pelo método `invokeOneDocument`.

**Consulte também:**

[Start rápido (modo SOAP): Montagem de um documento PDF criptografado usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Montagem de um documento PDF criptografado usando a API de serviço da Web {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao definir uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Criar um cliente Assembler.

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
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Referência a um documento PDF não protegido.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF de entrada. Esse objeto `BLOB` é passado para `invokeOneDocument` como um argumento.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF de entrada e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios atribuindo um valor a um membro de dados que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, atribua `false` ao membro de dados `AssemblerOptionSpec` do objeto `failOnError`.

1. Criptografe o documento.

   Chame o método `AssemblerServiceClient` do objeto `invokeOneDocument` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX
   * Um objeto `BLOB` que representa o documento PDF não protegido
   * Um objeto `AssemblerOptionSpec` que especifica opções de tempo de execução

   O método `invokeOneDocument` retorna um objeto `BLOB` que contém um documento PDF criptografado.

1. Salve o documento PDF criptografado.

   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF criptografado e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `BLOB` retornado pelo método `invokeOneDocument`. Preencha a matriz de bytes obtendo o valor do membro de dados `BLOB` do objeto `MTOM`.
   * Crie um objeto `System.IO.BinaryWriter` chamando seu construtor e transmitindo o objeto `System.IO.FileStream`.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF chamando o método `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também:**

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
