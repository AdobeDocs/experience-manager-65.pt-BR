---
title: Montagem de Documentos usando a numeração de Bates
seo-title: Montagem de Documentos usando a numeração de Bates
description: 'null'
seo-description: 'null'
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 0%

---


# Montagem de Documentos usando a numeração de Bates {#assembling-documents-using-bates-numbering}

É possível montar documentos PDF que contêm identificadores de página únicos usando a numeração de Bates. *A numeração* de Bates é um método de aplicar identificações exclusivas a um lote de documentos relacionados. A cada página do documento (ou conjunto de documentos) é atribuído um número de Bates que identifica exclusivamente a página. Por exemplo, documentos de fabricação que contêm informações da lista de materiais e que estão associados à produção de uma montagem podem conter um identificador. Um número de Bates contém um valor numérico incrementado sequencialmente e um prefixo e sufixo opcionais. O prefixo + sufixo numérico + é chamado de padrão *de* barras.

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

Esse documento DDX une dois documentos PDF chamados *map.pdf* e *direcçõespdf* em um único documento PDF. O documento PDF resultante contém um cabeçalho que consiste em um identificador de página exclusivo. Por exemplo, o documento na ilustração acima mostra 000016.

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos PDF usando o serviço Assembler. Esta seção não discute os conceitos, como criar um objeto de coleção que contenha documentos de entrada ou extrair os resultados do objeto de coleção retornado. (Consulte Montagem [Programática De Documentos](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF.)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar um documento PDF que contenha um identificador de página exclusivo (numeração de Bates), execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente do Montador de PDF.
1. Faça referência a um documento DDX existente.
1. Faça referência a documentos PDF de entrada.
1. Defina o valor inicial do número de Bates.
1. Monte os documentos PDF de entrada.
1. Extraia os resultados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se os AEM Forms forem implantados em JBoss)
* jbossall-client.jar (obrigatório se os AEM Forms forem implantados em JBoss)

Se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para obter informações sobre a localização de todos os arquivos JAR de AEM Forms, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java de AEM Forms.

**Criar um cliente de Montador de PDF**

Antes de poder executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Por exemplo, considere o documento DDX que foi introduzido nesta seção. Para montar um documento PDF que contenha identificadores de página exclusivos, o documento DX deve conter o `BatesNumber` elemento .

**documentos PDF de entrada de referência**

documentos PDF de entrada devem ser referenciados para montar um documento PDF. Por exemplo, os documentos map.pdf e direcçõesdevem ser referenciados para reunir esses documentos PDF em um único documento PDF.

**Definir o valor inicial do número de Bates**

Você pode definir o valor inicial do número de Bates para atender às suas necessidades comerciais. Por exemplo, suponha que seja um requisito definir o valor inicial como 000100. Se você não definir o valor inicial, o valor da primeira página será 000000.

**Montagem de documentos PDF de entrada**

Depois de criar o cliente do serviço Assembler, consulte o documento DDX que contém informações de `BatesNumber` `invokeDDX` elementos, consulte um documento PDF de entrada e defina as opções de tempo de execução, você pode chamar a operação que resulta na montagem pelo serviço Assembler de um documento PDF que contém identificadores de página exclusivos.

**Extrair os resultados**

O serviço Assembler retorna um objeto de coleção que contém os resultados da tarefa. Você pode extrair o documento PDF resultante e quaisquer exceções que forem lançadas. Nessa situação, um documento PDF criptografado está localizado dentro do objeto de coleção.

>[!NOTE]
>
>Um objeto de coleção é retornado se você chamar a `invokeDDX` operação. Essa operação é usada ao transmitir dois ou mais documentos PDF de entrada ao serviço Assembler. No entanto, se você enviar apenas um documento PDF de entrada para o serviço Assembler, deverá chamar a operação. `invokeOneDocument` Para obter informações sobre como usar essa operação, consulte [Montagem de Documentos](/help/forms/developing/assembling-encrypted-pdf-documents.md)PDF criptografados.

**Consulte também:**

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar documentos com a numeração de Bates usando a API Java {#assemble-documents-with-bates-numbering-using-the-java-api}

Monte um documento PDF que usa identificadores de página exclusivos (numeração de Bates) usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente do Montador de PDF.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `AssemblerServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DX.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Faça referência a documentos PDF de entrada.

   * Crie um `java.util.Map` objeto usado para armazenar documentos PDF de entrada usando um `HashMap` construtor.
   * Para cada documento PDF de entrada, crie um `java.io.FileInputStream` objeto usando seu construtor e transmitindo o local do documento PDF de entrada. Nessa situação, passe o local de um documento PDF não protegido.
   * Para cada documento PDF de entrada, crie um `com.adobe.idp.Document` objeto e passe o `java.io.FileInputStream` objeto que contém o documento PDF.
   * Adicione uma entrada ao `java.util.Map` objeto chamando seu `put` método e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX. Por exemplo, o nome do arquivo de origem PDF especificado no documento DDX que é introduzido nesta seção é Loan.pdf.
      * Um `com.adobe.idp.Document` objeto que contém o documento PDF não protegido.

1. Defina o valor inicial do número de Bates.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina o número de Bates inicial chamando o `AssemblerOptionSpec` objeto `setFirstBatesNumber` e transmitindo um valor numérico que especifique o valor inicial.

1. Monte os documentos PDF de entrada.

   Chame o `AssemblerServiceClient` método do `invokeDDX` objeto e passe os seguintes valores obrigatórios:

   * Um `com.adobe.idp.Document` objeto que representa o documento DDX.
   * Um `java.util.Map` objeto que contém o arquivo PDF não protegido de entrada.
   * Um `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log de trabalhos.

   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém um documento PDF criptografado por senha.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o `AssemblerResult` método do `getDocuments` objeto. Essa ação retorna um `java.util.Map` objeto.
   * Iterar pelo `java.util.Map` objeto até encontrar o `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` `copyToFile` método do objeto para extrair o documento PDF.

**Consulte também:**

[Start rápido (modo SOAP): Montagem de um documento PDF com a numeração de datas usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar documentos com a numeração de Bates usando a API de serviço da Web {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Monte um documento PDF que usa identificadores de página exclusivos (numeração de Bates) usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um cliente do Montador de PDF.

   * Crie um `AssemblerServiceClient` objeto usando seu construtor padrão.
   * Crie um `AssemblerServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar o `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `AssemblerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a um documento DDX existente.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento DDX.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DX e o modo para abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Faça referência a documentos PDF de entrada.

   * Para cada documento PDF de entrada, crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento PDF de entrada.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo sua `MTOM` propriedade ao conteúdo da matriz de bytes.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Esse objeto de coleção é usado para armazenar os documentos PDF de entrada.
   * Para cada documento PDF de entrada, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto. Por exemplo, se dois documentos PDF de entrada forem usados, crie dois `MyMapOf_xsd_string_To_xsd_anyType_Item` objetos.
   * Atribua um valor de string que representa o nome da chave ao campo do `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto `key` . Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX. (Execute essa tarefa para cada documento PDF de entrada.)
   * Atribua o `BLOB` objeto que armazena o documento PDF ao `MyMapOf_xsd_string_To_xsd_anyType_Item` campo do `value` objeto. (Execute essa tarefa para cada documento PDF de entrada.)
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto ao `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` método do objeto `Add` e passe o `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Execute essa tarefa para cada documento PDF de entrada.)

1. Defina o valor inicial do número de Bates.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina o número de Bates inicial atribuindo um valor numérico ao membro de `firstBatesNumber` dados que pertence ao `AssemblerOptionSpec` objeto.

1. Monte os documentos PDF de entrada.

   Chame o método do `AssemblerServiceClient` objeto `invoke` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o documento DDX.
   * O `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém os documentos PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem do PDF, e seus valores devem ser os `BLOB` objetos que correspondem a esses arquivos.
   * Um `AssemblerOptionSpec` objeto que especifica opções de tempo de execução.

   O `invoke` método retorna um `AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` campo do `documents` objeto, que é um `Map` objeto que contém os documentos PDF de resultado.
   * Itere pelo `Map` objeto até encontrar a chave que corresponde ao nome do documento resultante. Em seguida, converta o membro do storage `value` em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade do `BLOB` objeto `MTOM` . Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também:**

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
