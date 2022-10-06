---
title: Montagem programática de documentos do PDF
seo-title: Programmatically Assembling PDF Documents
description: Use a API do serviço Assembler para reunir vários documentos PDF em um único documento do PDF usando a API do Java e a API do serviço da Web.
seo-description: Use the Assembler service API to assemble multiple PDF documents into a single PDF document using the Java API and the Web Service API.
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 0%

---

# Montagem programática de documentos do PDF {#programmatically-assembling-pdf-documents}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

Você pode usar a API do serviço Assembler para reunir vários documentos PDF em um único documento PDF. A ilustração a seguir mostra três documentos PDF sendo mesclados em um único documento PDF.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

Para montar dois ou mais documentos PDF em um único documento PDF, você precisa de um documento DDX. Um documento DDX descreve o documento PDF produzido pelo serviço Assembler. Ou seja, o documento DDX instrui o serviço Assembler sobre quais ações executar.

Para a finalidade desta discussão, suponha que o seguinte documento DDX seja usado.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

Este documento DDX mescla dois documentos PDF nomeados *map.pdf* e *guide.pdf* em um único documento PDF.

>[!NOTE]
>
>Para ver um documento DDX que desmonta um documento PDF, consulte [Desmontando documentos do PDF de maneira programática](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Considerações ao invocar o serviço Assembler usando serviços da Web {#considerations-when-invoking-assembler-service-using-web-services}

Ao adicionar cabeçalhos e rodapés durante a montagem de grandes documentos, você pode encontrar um `OutOfMemory` e os arquivos não serão montados. Para reduzir a chance de esse problema ocorrer, adicione um `DDXProcessorSetting` para seu documento DDX, como mostrado no exemplo a seguir.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Você pode adicionar esse elemento como filho da variável `DDX` ou como filho de um `PDF result` elemento. O valor padrão para essa configuração é 0 (zero), que desativa a marcação de verificação e o DDX se comporta como se a variável `DDXProcessorSetting` não está presente. Se você encontrou um `OutOfMemory` , talvez seja necessário definir o valor como um número inteiro, normalmente entre 500 e 5000. Um pequeno valor de ponto de verificação resulta em uma verificação mais frequente.

## Resumo das etapas {#summary-of-steps}

Para montar um único documento PDF de vários documentos PDF, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Assembler PDF.
1. Faça referência a um documento DDX existente.
1. Faça referência a documentos de PDF de entrada.
1. Defina as opções de tempo de execução.
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

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado.

**Criar um cliente do Assembler do PDF**

Antes de executar programaticamente uma operação Assembler, é necessário criar um cliente Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Por exemplo, considere o documento DDX que foi introduzido nesta seção. Este documento DDX instrui o serviço Assembler a unir dois documentos PDF em um único documento PDF.

**Referenciar documentos de PDF de entrada**

Faça referência aos documentos do PDF de entrada que você deseja passar para o serviço Assembler. Por exemplo, se você quiser passar dois documentos PDF de entrada chamados Map e Directions, você deverá passar os arquivos PDF correspondentes.

O arquivo map.pdf e o arquivo directions.pdf devem ser colocados em um objeto de coleção. O nome da chave deve corresponder ao valor do atributo PDF source no documento DDX. Não importa qual é o nome do arquivo PDF se a chave e o atributo de origem no documento DX corresponderem.

>[!NOTE]
>
>Um `AssemblerResult` objeto, que contém um objeto de coleção, é retornado se você chamar a variável `invokeDDX` operação. Essa operação é usada quando você passa dois ou mais documentos PDF de entrada para o serviço Assembler. No entanto, se você passar apenas um PDF de entrada para o serviço Assembler e esperar apenas um documento de retorno, chame o `invokeOneDocument` operação. Ao invocar esta operação, um único documento é retornado. Para obter informações sobre como usar essa operação, consulte [Montagem de documentos PDF criptografados](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrua o serviço Assembler a continuar processando um trabalho se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte o `AssemblerOptionSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Montar os documentos de PDF de entrada**

Depois de criar o cliente do serviço, fazer referência a um arquivo DDX, criar um objeto de coleção que armazena documentos PDF de entrada e definir opções de tempo de execução, você pode chamar a operação DDX. Ao usar o documento DDX especificado nesta seção, os arquivos map.pdf e Direction.pdf são unidos em um documento PDF.

**Extraia os resultados**

O serviço Assembler retorna um `java.util.Map` objeto , que pode ser obtido da variável `AssemblerResult` e que contém os resultados da operação. O retorno `java.util.Map` contém os documentos resultantes e quaisquer exceções.

A tabela a seguir resume alguns dos valores principais e tipos de objeto que podem ser localizados no campo de `java.util.Map` objeto.

<table>
 <thead>
  <tr>
   <th><p>Valor-chave</p></th>
   <th><p>Tipo de objeto</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>Contém os documentos resultantes especificados em um elemento resultante DDX</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>Contém qualquer exceção para o documento</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>Contém o registro de tarefas</p></td>
  </tr>
 </tbody>
</table>

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontando documentos do PDF de maneira programática](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Monte documentos do PDF usando a API do Java {#assemble-pdf-documents-using-the-java-api}

Monte um documento do PDF usando a API do serviço de Assembler (Java):

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
   * Para cada documento de PDF de entrada, crie um `java.io.FileInputStream` usando seu construtor e passando o local do documento PDF de entrada.
   * Para cada documento de PDF de entrada, crie um `com.adobe.idp.Document` e transmita o `java.io.FileInputStream` objeto que contém o documento PDF.
   * Para cada documento de entrada, adicione uma entrada ao `java.util.Map` ao invocar seu `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento PDF source especificado no documento DDX.
      * A `com.adobe.idp.Document` objeto (ou `java.util.List` que especifica vários documentos) que contém o documento PDF de origem.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios, chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, chame a função `AssemblerOptionSpec` do objeto `setFailOnError` método e pass `false`.

1. Monte os documentos de PDF de entrada.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado
   * A `java.util.Map` objeto que contém os arquivos PDF de entrada a serem montados
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo fonte padrão e nível de log de tarefas

   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método . Isso retorna uma `java.util.Map` objeto.
   * Iterar por meio do `java.util.Map` até encontrar o resultante `com.adobe.idp.Document` objeto. (Você pode usar o elemento PDF result especificado no documento DDX para obter o documento.)
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento PDF.

   >[!NOTE]
   >
   >If `LOG_LEVEL` foi definido para produzir um log, você pode extrair o log usando a variável `AssemblerResult` do objeto `getJobLog` método .

**Consulte também**

[Início rápido (modo SOAP): Montagem de um documento do PDF usando a API do Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Monte documentos do PDF usando a API do serviço da Web {#assemble-pdf-documents-using-the-web-service-api}

Monte documentos do PDF usando a API do serviço Assembler (serviço da Web):

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
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento DX e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Faça referência a documentos de PDF de entrada.

   * Para cada documento de PDF de entrada, crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento PDF de entrada.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.
   * Crie um `MyMapOf_xsd_string_To_xsd_anyType` objeto. Esse objeto de coleção é usado para armazenar documentos PDF de entrada.
   * Para cada documento de PDF de entrada, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto. Por exemplo, se dois documentos PDF de entrada forem usados, crie dois `MyMapOf_xsd_string_To_xsd_anyType_Item` objetos.
   * Atribua um valor de string que represente o nome da chave à variável `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` campo. Esse valor deve corresponder ao valor do elemento PDF source especificado no documento DDX. (Execute esta tarefa para cada documento PDF de entrada.)
   * Atribua o `BLOB` objeto que armazena o documento PDF para o `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` campo. (Execute esta tarefa para cada documento PDF de entrada.)
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` para `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` do objeto `Add` e passe o `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Execute esta tarefa para cada documento PDF de entrada.)

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos da empresa, atribuindo um valor a um membro de dados pertencente à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, atribua `false` para `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Monte os documentos de PDF de entrada.

   Chame o `AssemblerServiceClient` do objeto `invoke` e transmita os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX.
   * O `mapItem` matriz que contém os documentos PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem do PDF e seus valores devem ser o `BLOB` objetos que correspondem a esses arquivos.
   * Um `AssemblerOptionSpec` que especifica as opções de tempo de execução.

   O `invoke` retorna um método `AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que possam ter ocorrido.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` , que é um `Map` objeto que contém os documentos PDF de resultado.
   * Iterar por meio do `Map` até encontrar a chave que corresponde ao nome do documento resultante. Em seguida, converta esse membro da matriz `value` para `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando seu `BLOB` do objeto `MTOM` propriedade. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

   >[!NOTE]
   >
   >If `LOG_LEVEL` foi definido para produzir um log, você pode extrair o log obtendo o valor do `AssemblerResult` do objeto `jobLog` membro de dados.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
