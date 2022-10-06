---
title: Montando Documentos Usando a Numeração de Bates
seo-title: Assembling Documents Using Bates Numbering
description: Use a numeração de Bates para montar documentos PDF usando o Java e a API de serviço da Web.
seo-description: Use Bates numbering to assemble PDF documents using the Java and Web Service API.
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 0%

---

# Montando Documentos Usando a Numeração de Bates {#assembling-documents-using-bates-numbering}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

Você pode montar documentos PDF que contêm identificadores de página exclusivos usando a numeração de Bates. *Numeração de Bates* é um método para aplicar identificadores exclusivos a um lote de documentos relacionados. Cada página no documento (ou conjunto de documentos) recebe um número de Bates que identifica exclusivamente a página. Por exemplo, documentos de fabricação que contêm informações de lista de materiais e que estão associados à produção de uma montagem podem conter um identificador. Um número de Bates contém um valor numérico incrementado sequencialmente e um prefixo e sufixo opcionais. O prefixo + sufixo numérico é conhecido como um *padrão de barras*.

A ilustração a seguir mostra um documento PDF que contém um identificador exclusivo localizado no cabeçalho do documento.

![au_au_batesnumber](assets/au_au_batesnumber.png)

Para a finalidade desta discussão, o identificador de página exclusivo é colocado no cabeçalho de um documento. Suponha que o seguinte documento DDX seja usado.

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

Este documento DDX mescla dois documentos PDF nomeados *map.pdf* e *guide.pdf* em um único documento PDF. O documento PDF resultante contém um cabeçalho que consiste em um identificador de página exclusivo. Por exemplo, o documento na ilustração acima mostra 000016.

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos do PDF usando o serviço Assembler. Esta seção não discute os conceitos, como criar um objeto de coleção que contenha documentos de entrada ou extrair os resultados do objeto de coleção retornado. (Consulte [Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar um documento PDF que contenha um identificador de página exclusivo (numeração de Bates), execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Assembler PDF.
1. Faça referência a um documento DDX existente.
1. Faça referência a documentos de PDF de entrada.
1. Defina o valor do número Bates inicial.
1. Monte os documentos de PDF de entrada.
1. Extraia os resultados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

Se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para obter informações sobre a localização de todos os arquivos AEM Forms JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente do Assembler do PDF**

Antes de poder executar programaticamente uma operação Assembler, é necessário criar um cliente de serviço Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Por exemplo, considere o documento DDX que foi introduzido nesta seção. Para montar um documento PDF que contenha identificadores de página exclusivos, o documento DDX deve conter a variável `BatesNumber` elemento.

**Referenciar documentos de PDF de entrada**

Os documentos PDF de entrada devem ser referenciados para montar um documento PDF. Por exemplo, os documentos map.pdf e Direction.pdf devem ser referenciados para reunir esses documentos PDF em um único documento PDF.

**Definir o valor do número Bates inicial**

Você pode definir o valor do número de Bates inicial para atender às suas necessidades comerciais. Por exemplo, suponha que seja um requisito definir o valor inicial como 000100. Se você não definir o valor inicial, o valor da primeira página será 000000.

**Montar os documentos de PDF de entrada**

Após criar o cliente do serviço Assembler, consulte o documento DDX que contém `BatesNumber` informações do elemento, referência a um documento PDF de entrada e definição de opções de tempo de execução, você pode chamar a função `invokeDDX` operação que resulta na montagem pelo serviço Assembler de um documento PDF que contém identificadores de página exclusivos.

**Extraia os resultados**

O serviço Assembler retorna um objeto de coleção que contém os resultados da tarefa. Você pode extrair o documento PDF resultante e quaisquer exceções que forem lançadas. Nessa situação, um documento PDF criptografado está localizado no objeto de coleção.

>[!NOTE]
>
>Um objeto de coleção é retornado se você chamar a variável `invokeDDX` operação. Essa operação é usada ao passar dois ou mais documentos PDF de entrada para o serviço Assembler. No entanto, se você passar apenas um documento PDF de entrada para o serviço Assembler, deverá chamar a função `invokeOneDocument` operação. Para obter informações sobre como usar essa operação, consulte [Montagem de documentos PDF criptografados](/help/forms/developing/assembling-encrypted-pdf-documents.md).

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Monte documentos com a numeração de Bates usando a API Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Monte um documento do PDF que usa identificadores de página exclusivos (numeração de Bates) usando a API do Serviço do Assembler (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente Assembler PDF.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `AssemblerServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e passando um valor de string que especifica o local do arquivo DX.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Faça referência a documentos de PDF de entrada.

   * Crie um `java.util.Map` objeto usado para armazenar documentos PDF de entrada usando um `HashMap` construtor.
   * Para cada documento de PDF de entrada, crie um `java.io.FileInputStream` usando seu construtor e passando o local do documento PDF de entrada. Nessa situação, passe o local de um documento PDF não seguro.
   * Para cada documento de PDF de entrada, crie um `com.adobe.idp.Document` e transmita o `java.io.FileInputStream` objeto que contém o documento PDF.
   * Adicione uma entrada à `java.util.Map` ao invocar seu `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento PDF source especificado no documento DDX. Por exemplo, o nome do arquivo PDF source especificado no documento DDX que é introduzido nesta seção é Loan.pdf.
      * A `com.adobe.idp.Document` objeto que contém o documento PDF não seguro.

1. Defina o valor do número Bates inicial.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina o número de Bates inicial chamando o `AssemblerOptionSpec` do objeto `setFirstBatesNumber` e transmitindo um valor numérico que especifica o valor inicial.

1. Monte os documentos de PDF de entrada.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX.
   * A `java.util.Map` objeto que contém o arquivo PDF não seguro de entrada.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do trabalho.

   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém um documento PDF criptografado por senha.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método . Essa ação retorna um `java.util.Map` objeto.
   * Iterar por meio do `java.util.Map` até encontrar a variável `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento PDF.

**Consulte também**

[Início rápido (modo SOAP): Montagem de um documento do PDF com numeração de barras usando a API do Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Compilar documentos com a numeração de Bates usando a API do serviço da Web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Monte um documento do PDF que usa identificadores de página exclusivos (numeração de Bates) usando a API do Serviço de Assembler (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um cliente Assembler PDF.

   * Crie um `AssemblerServiceClient` usando seu construtor padrão.
   * Crie um `AssemblerServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `AssemblerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a um documento DDX existente.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento DDX.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento DX e o modo para abrir o arquivo no.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Faça referência a documentos de PDF de entrada.

   * Para cada documento de PDF de entrada, crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento PDF de entrada.
   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.
   * Crie um `MyMapOf_xsd_string_To_xsd_anyType` objeto. Esse objeto de coleção é usado para armazenar os documentos PDF de entrada.
   * Para cada documento de PDF de entrada, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto. Por exemplo, se dois documentos PDF de entrada forem usados, crie dois `MyMapOf_xsd_string_To_xsd_anyType_Item` objetos.
   * Atribua um valor de string que represente o nome da chave à variável `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` campo. Esse valor deve corresponder ao valor do elemento PDF source especificado no documento DDX. (Execute esta tarefa para cada documento PDF de entrada.)
   * Atribua o `BLOB` objeto que armazena o documento PDF para o `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` campo. (Execute esta tarefa para cada documento PDF de entrada.)
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` para `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` do objeto `Add` e passe o `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Execute esta tarefa para cada documento PDF de entrada.)

1. Defina o valor do número Bates inicial.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina o número Bates inicial atribuindo um valor numérico à variável `firstBatesNumber` membro de dados que pertence ao `AssemblerOptionSpec` objeto.

1. Monte os documentos de PDF de entrada.

   Chame o `AssemblerServiceClient` do objeto `invoke` e transmita os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX.
   * O `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém os documentos PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem do PDF e seus valores devem ser o `BLOB` objetos que correspondem a esses arquivos.
   * Um `AssemblerOptionSpec` que especifica as opções de tempo de execução.

   O `invoke` retorna um método `AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` , que é um `Map` objeto que contém os documentos PDF de resultado.
   * Iterar por meio do `Map` até encontrar a chave que corresponde ao nome do documento resultante. Em seguida, converta esse membro da matriz `value` para `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando seu `BLOB` do objeto `MTOM` propriedade. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
