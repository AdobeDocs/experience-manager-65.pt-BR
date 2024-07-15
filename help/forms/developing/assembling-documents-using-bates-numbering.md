---
title: Montando Documentos Usando Numeração Bates
description: Use a numeração de Bates para montar documentos PDF usando Java e a API de serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# Montando Documentos Usando Numeração Bates {#assembling-documents-using-bates-numbering}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

Você pode montar documentos PDF que contêm identificadores de página exclusivos usando a numeração Bates. *Numeração de Bates* é um método de aplicar identificadores exclusivos a um lote de documentos relacionados. Cada página no documento (ou conjunto de documentos) recebe um número de Bates que identifica exclusivamente a página. Por exemplo, os documentos de fabricação que contêm informações sobre a lista de materiais e estão associados à produção de uma montagem podem conter um identificador. Um número Bates contém um valor numérico incrementado sequencialmente e um prefixo e sufixo opcionais. O prefixo + numérico + sufixo é chamado de *padrão de bates*.

A ilustração a seguir mostra um documento PDF que contém um identificador exclusivo no cabeçalho do documento.

![au_au_batesnumber](assets/au_au_batesnumber.png)

Para fins de discussão, o identificador de página único é colocado no cabeçalho de um documento. Suponha que o seguinte documento DDX seja usado.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="out.pdf">
        <Header>
         <Center>
             <StyledText>
                 <p font-size="20pt"><BatesNumber/></p>
             </StyledText>
         </Center>
     </Header>
           <PDF source="map.pdf" />
          <PDF source="directions.pdf" />
          </PDF>
 </DDX>
```

Este documento DDX mescla dois documentos PDF chamados *map.pdf* e *directions.pdf* em um único documento PDF. O documento PDF resultante contém um cabeçalho que consiste em um identificador de página exclusivo. Por exemplo, o documento na ilustração acima mostra 000016.

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos do PDF usando o serviço Assembler. Esta seção não discute os conceitos, como criar um objeto de coleção que contenha documentos de entrada ou extrair os resultados do objeto de coleção retornado. (Consulte [Assembling Programmatically PDF Documents](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço do Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar um documento PDF que contenha um identificador de página exclusivo (numeração de Bates), execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDF Assembler.
1. Consulte um documento DDX existente.
1. Referencie documentos de PDF de entrada.
1. Defina o valor inicial do número de Bates.
1. Montar os documentos do PDF de entrada.
1. Extraia os resultados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

Se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado. Para obter informações sobre a localização de todos os arquivos JAR do AEM Forms, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referenciar um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Por exemplo, considere o documento DDX introduzido nesta seção. Para montar um documento PDF que contenha identificadores de página exclusivos, o documento DDX deve conter o elemento `BatesNumber`.

**Referenciar documentos de PDF de entrada**

Os documentos de PDF de entrada devem ser referenciados para montar um documento PDF. Por exemplo, os documentos map.pdf e directs.pdf devem ser referenciados para reunir esses documentos PDF em um único documento PDF.

**Definir o valor inicial do número de Bates**

Você pode definir o valor inicial do número de Bates para atender às suas necessidades comerciais. Por exemplo, suponha que seja um requisito definir o valor inicial como 000100. Se você não definir o valor inicial, o valor da primeira página será 000000.

**Montar os documentos de PDF de entrada**

Depois de criar o cliente de serviço do Assembler, fazer referência ao documento DDX que contém informações de elemento `BatesNumber`, fazer referência a um documento PDF de entrada e definir opções de tempo de execução, você poderá invocar a operação `invokeDDX` que resulta na montagem, pelo serviço Assembler, de um documento PDF que contém identificadores de página exclusivos.

**Extrair os resultados**

O serviço Assembler retorna um objeto de coleção que contém os resultados do trabalho. Você pode extrair o documento PDF resultante e quaisquer exceções lançadas. Nessa situação, um documento PDF criptografado está localizado dentro do objeto da coleção.

>[!NOTE]
>
>Um objeto de coleção será retornado se você invocar a operação `invokeDDX`. Essa operação é usada ao passar dois ou mais documentos de PDF de entrada para o serviço Assembler. No entanto, se você passar apenas um documento de PDF de entrada para o serviço Assembler, deverá chamar a operação `invokeOneDocument`. Para obter informações sobre como usar esta operação, consulte [Assembling Encrypted PDF Documents](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar documentos com numeração Bates usando a API Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Montar um documento PDF que use identificadores de página exclusivos (numeração de Bates) usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente PDF Assembler.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Consulte um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do arquivo DDX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Referencie documentos de PDF de entrada.

   * Crie um objeto `java.util.Map` usado para armazenar documentos de PDF de entrada usando um construtor `HashMap`.
   * Para cada documento PDF de entrada, crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local do documento PDF de entrada. Nessa situação, passe o local de um documento PDF não seguro.
   * Para cada documento de PDF de entrada, crie um objeto `com.adobe.idp.Document` e passe o objeto `java.io.FileInputStream` que contém o documento PDF.
   * Adicione uma entrada ao objeto `java.util.Map` invocando seu método `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX. Por exemplo, o nome do arquivo de origem de PDF especificado no documento DDX introduzido nesta seção é Loan.pdf.
      * Um objeto `com.adobe.idp.Document` que contém o documento PDF não seguro.

1. Defina o valor inicial do número de Bates.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina o número de Bates inicial invocando `setFirstBatesNumber` do objeto `AssemblerOptionSpec` e transmitindo um valor numérico que especifica o valor inicial.

1. Montar os documentos do PDF de entrada.

   Invoque o método `invokeDDX` do objeto `AssemblerServiceClient` e passe os seguintes valores obrigatórios:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX.
   * Um objeto `java.util.Map` que contém o arquivo de PDF não seguro de entrada.
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do trabalho.

   O método `invokeDDX` retorna um objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contém um documento PDF criptografado por senha.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Invoque o método `getDocuments` do objeto `AssemblerResult`. Esta ação retorna um objeto `java.util.Map`.
   * Repita através do objeto `java.util.Map` até encontrar o objeto `com.adobe.idp.Document`.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para extrair o documento PDF.

**Consulte também**

[Início rápido (modo SOAP): Montagem de um documento PDF com numeração de bits usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar documentos com numeração de Bates usando a API de serviço Web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Montar um documento PDF que use identificadores de página exclusivos (numeração de Bates) usando a API de Serviço do Assembler (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

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
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` com o conteúdo da matriz de bytes.

1. Referencie documentos de PDF de entrada.

   * Para cada documento de PDF de entrada, crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento de PDF de entrada.
   * Crie um objeto `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` com o conteúdo da matriz de bytes.
   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de coleção é usado para armazenar os documentos de PDF de entrada.
   * Para cada documento de PDF de entrada, crie um objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Por exemplo, se dois documentos de PDF de entrada forem usados, crie dois objetos `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Atribua um valor de cadeia de caracteres que represente o nome da chave para o campo `key` do objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX. (Execute esta tarefa para cada documento de PDF de entrada.)
   * Atribua o objeto `BLOB` que armazena o documento PDF ao campo `value` do objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Execute esta tarefa para cada documento de PDF de entrada.)
   * Adicione o objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` ao objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque o método `Add` do objeto `MyMapOf_xsd_string_To_xsd_anyType` e passe o objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Execute esta tarefa para cada documento de PDF de entrada.)

1. Defina o valor inicial do número de Bates.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina o número inicial de Bates atribuindo um valor numérico ao membro de dados `firstBatesNumber` que pertence ao objeto `AssemblerOptionSpec`.

1. Montar os documentos do PDF de entrada.

   Invoque o método `invoke` do objeto `AssemblerServiceClient` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX.
   * O objeto `MyMapOf_xsd_string_To_xsd_anyType` que contém os documentos de PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem de PDF, e seus valores devem ser os objetos `BLOB` que correspondem a esses arquivos.
   * Um objeto `AssemblerOptionSpec` que especifica opções de tempo de execução.

   O método `invoke` retorna um objeto `AssemblerResult` que contém os resultados do trabalho e as exceções que ocorreram.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Acesse o campo `documents` do objeto `AssemblerResult`, que é um objeto `Map` que contém os documentos de PDF de resultado.
   * Repita através do objeto `Map` até encontrar a chave que corresponde ao nome do documento resultante. Em seguida, converta o `value` desse membro da matriz em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade `MTOM` do objeto `BLOB`. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
