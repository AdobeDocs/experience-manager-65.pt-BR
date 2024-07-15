---
title: Montagem programática de documentos do PDF
description: Use a API de serviço do Assembler para reunir vários documentos de PDF em um único documento de PDF usando a API Java e a API de serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2105'
ht-degree: 0%

---

# Montagem programática de documentos do PDF {#programmatically-assembling-pdf-documents}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

Você pode usar a API de serviço do Assembler para reunir vários documentos de PDF em um único documento de PDF. A ilustração a seguir mostra três documentos PDF sendo mesclados em um único documento PDF.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

Para reunir dois ou mais documentos PDF em um único documento PDF, é necessário um documento DDX. Um documento DDX descreve o documento PDF produzido pelo serviço Assembler. Ou seja, o documento DDX instrui o serviço do Assembler sobre quais ações executar.

Para o propósito desta discussão, suponha que o seguinte documento DDX seja usado.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

Este documento DDX mescla dois documentos PDF chamados *map.pdf* e *directions.pdf* em um único documento PDF.

>[!NOTE]
>
>Para ver um documento DDX que desmonta um documento PDF, consulte [Desmontando Documentos PDF de Forma Programática](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço do Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Considerações ao invocar o serviço Assembler usando serviços Web {#considerations-when-invoking-assembler-service-using-web-services}

Ao adicionar cabeçalhos e rodapés durante a montagem de documentos grandes, você pode encontrar um erro `OutOfMemory` e os arquivos não serão montados. Para reduzir a chance deste problema, adicione um elemento `DDXProcessorSetting` ao seu documento DDX, como mostrado no exemplo a seguir.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Você pode adicionar este elemento como filho do elemento `DDX` ou como filho de um elemento `PDF result`. O valor padrão dessa configuração é 0 (zero), que desativa o ponto de verificação e o DDX se comporta como se o elemento `DDXProcessorSetting` não estivesse presente. Se você encontrou um erro `OutOfMemory`, talvez precise definir o valor como um inteiro, normalmente entre 500 e 5000. Um valor de ponto de verificação pequeno resulta em pontos de verificação mais frequentes.

## Resumo das etapas {#summary-of-steps}

Para montar um único documento PDF a partir de vários documentos PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDF Assembler.
1. Consulte um documento DDX existente.
1. Referencie documentos de PDF de entrada.
1. Definir opções de tempo de execução.
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

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado.

**Criar um cliente PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, você deve criar um cliente Assembler.

**Referenciar um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Por exemplo, considere o documento DDX introduzido nesta seção. Este documento DDX instrui o serviço Assembler a unir dois documentos de PDF em um único documento de PDF.

**Referenciar documentos de PDF de entrada**

Referencie documentos de PDF de entrada que você deseja passar para o serviço Assembler. Por exemplo, se você quiser passar dois documentos de PDF de entrada chamados Mapa e Direções, será necessário passar os arquivos de PDF correspondentes.

Tanto o arquivo map.pdf quanto o arquivo direction.pdf devem ser colocados em um objeto de coleção. O nome da chave deve corresponder ao valor do atributo de origem PDF no documento DDX. Não importa qual seja o nome do arquivo PDF se a chave e o atributo de origem no documento DDX coincidirem.

>[!NOTE]
>
>Um objeto `AssemblerResult`, que contém um objeto de coleção, será retornado se você invocar a operação `invokeDDX`. Essa operação é usada quando você passa dois ou mais documentos de PDF de entrada para o serviço Assembler. No entanto, se você passar apenas um PDF de entrada para o serviço Assembler e esperar apenas um documento de retorno, chame a operação `invokeOneDocument`. Ao invocar esta operação, um único documento é retornado. Para obter informações sobre como usar esta operação, consulte [Assembling Encrypted PDF Documents](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que você pode definir, consulte a referência de classe `AssemblerOptionSpec` na [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Montar os documentos de PDF de entrada**

Depois de criar o cliente de serviço, fazer referência a um arquivo DDX, criar um objeto de coleção que armazene documentos de PDF de entrada e definir opções de tempo de execução, você pode chamar a operação DDX. Ao usar o documento DDX especificado nesta seção, os arquivos map.pdf e direction.pdf são mesclados em um documento PDF.

**Extrair os resultados**

O serviço do Assembler retorna um objeto `java.util.Map`, que pode ser obtido do objeto `AssemblerResult`, e que contém os resultados da operação. O objeto `java.util.Map` retornado contém os documentos resultantes e quaisquer exceções.

A tabela a seguir resume alguns dos valores de chave e tipos de objeto que podem estar no objeto `java.util.Map` retornado.

<table>
 <thead>
  <tr>
   <th><p>Valor da chave</p></th>
   <th><p>Tipo de objeto</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>Contém os documentos resultantes que são especificados em um elemento resultante DDX</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>Contém qualquer exceção para o documento</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>Contém o log do trabalho</p></td>
  </tr>
 </tbody>
</table>

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontando Documentos PDF de Forma Programática](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Montar documentos do PDF usando a API Java {#assemble-pdf-documents-using-the-java-api}

Montar um documento PDF usando a API de serviço do Assembler (Java):

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
   * Para cada documento PDF de entrada, crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local do documento PDF de entrada.
   * Para cada documento de PDF de entrada, crie um objeto `com.adobe.idp.Document` e passe o objeto `java.io.FileInputStream` que contém o documento PDF.
   * Para cada documento de entrada, adicione uma entrada ao objeto `java.util.Map` invocando seu método `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX.
      * Um objeto `com.adobe.idp.Document` (ou objeto `java.util.List` que especifica vários documentos) que contém o documento PDF de origem.

1. Definir opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos da sua empresa invocando um método que pertença ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, chame o método `setFailOnError` do objeto `AssemblerOptionSpec` e passe `false`.

1. Montar os documentos do PDF de entrada.

   Chame o método `invokeDDX` do objeto `AssemblerServiceClient` e passe os seguintes valores obrigatórios:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX a ser usado
   * Um objeto `java.util.Map` que contém os arquivos de PDF de entrada a serem montados
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do trabalho

   O método `invokeDDX` retorna um objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contém os resultados do trabalho e as exceções que ocorreram.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Invoque o método `getDocuments` do objeto `AssemblerResult`. Isso retorna um objeto `java.util.Map`.
   * Repita o objeto `java.util.Map` até encontrar o objeto `com.adobe.idp.Document` resultante. (Você pode usar o elemento de resultado PDF especificado no documento DDX para obter o documento.)
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para extrair o documento PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` foi definido para produzir um log, você pode extrair o log usando o método `getJobLog` do objeto `AssemblerResult`.

**Consulte também**

[Início rápido (modo SOAP): Montagem de um documento PDF usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar documentos do PDF usando a API de serviço Web {#assemble-pdf-documents-using-the-web-service-api}

Montar documentos de PDF usando a API de serviço do Assembler (serviço da Web):

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
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento DDX e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com os dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` com o conteúdo da matriz de bytes.

1. Referencie documentos de PDF de entrada.

   * Para cada documento de PDF de entrada, crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento de PDF de entrada.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` com o conteúdo da matriz de bytes.
   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de coleção é usado para armazenar documentos de PDF de entrada.
   * Para cada documento de PDF de entrada, crie um objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Por exemplo, se dois documentos de PDF de entrada forem usados, crie dois objetos `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Atribua um valor de cadeia de caracteres que represente o nome da chave para o campo `key` do objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX. (Execute esta tarefa para cada documento de PDF de entrada.)
   * Atribua o objeto `BLOB` que armazena o documento PDF ao campo `value` do objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Execute esta tarefa para cada documento de PDF de entrada.)
   * Adicione o objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` ao objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque o método `Add` do objeto `MyMapOf_xsd_string_To_xsd_anyType` e passe o objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Execute esta tarefa para cada documento de PDF de entrada.)

1. Definir opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos comerciais atribuindo um valor a um membro de dados que pertença ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, atribua `false` ao membro de dados `failOnError` do objeto `AssemblerOptionSpec`.

1. Montar os documentos do PDF de entrada.

   Chame o método `invoke` do objeto `AssemblerServiceClient` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX.
   * A matriz `mapItem` que contém os documentos de PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem de PDF, e seus valores devem ser os objetos `BLOB` que correspondem a esses arquivos.
   * Um objeto `AssemblerOptionSpec` que especifica opções de tempo de execução.

   O método `invoke` retorna um objeto `AssemblerResult` que contém os resultados do trabalho e quaisquer exceções que possam ter ocorrido.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Acesse o campo `documents` do objeto `AssemblerResult`, que é um objeto `Map` que contém os documentos de PDF de resultado.
   * Repita através do objeto `Map` até encontrar a chave que corresponde ao nome do documento resultante. Em seguida, converta o `value` desse membro da matriz em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade `MTOM` do objeto `BLOB`. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` foi definido para produzir um log, você pode extrair o log obtendo o valor do membro de dados `jobLog` do objeto `AssemblerResult`.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
