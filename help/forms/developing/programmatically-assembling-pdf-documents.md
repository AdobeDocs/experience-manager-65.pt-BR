---
title: Montagem programática de documentos do PDF
seo-title: Programmatically Assembling PDF Documents
description: Use a API de serviço do Assembler para reunir vários documentos de PDF em um único documento de PDF usando a API Java e a API de serviço da Web.
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

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

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

Este documento DDX mescla dois documentos PDF chamados *map.pdf* e *directs.pdf* em um único documento PDF.

>[!NOTE]
>
>Para ver um documento DDX que desmonta um documento PDF, consulte [Desmontando Documentos PDF de Forma Programática](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Considerações ao invocar o serviço Assembler usando serviços Web {#considerations-when-invoking-assembler-service-using-web-services}

Ao adicionar cabeçalhos e rodapés durante a montagem de documentos grandes, você pode encontrar um `OutOfMemory` e os arquivos não serão montados. Para reduzir a chance de esse problema ocorrer, adicione um `DDXProcessorSetting` elemento ao seu documento DDX, como mostrado no exemplo a seguir.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Você pode adicionar esse elemento como filho de `DDX` elemento ou como filho de um `PDF result` elemento. O valor padrão para essa configuração é 0 (zero), que desativa o ponto de verificação e o DDX se comporta como se o `DDXProcessorSetting` elemento não está presente. Se você encontrou um `OutOfMemory` erro, talvez seja necessário definir o valor como um número inteiro, normalmente entre 500 e 5000. Um valor de ponto de verificação pequeno resulta em pontos de verificação mais frequentes.

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

**Criar um cliente do PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, você deve criar um cliente Assembler.

**Referencie um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Por exemplo, considere o documento DDX introduzido nesta seção. Este documento DDX instrui o serviço Assembler a unir dois documentos de PDF em um único documento de PDF.

**Documentos de PDF de entrada de referência**

Referencie documentos de PDF de entrada que você deseja passar para o serviço Assembler. Por exemplo, se você quiser passar dois documentos de PDF de entrada chamados Mapa e Direções, será necessário passar os arquivos de PDF correspondentes.

Tanto o arquivo map.pdf quanto o arquivo direction.pdf devem ser colocados em um objeto de coleção. O nome da chave deve corresponder ao valor do atributo de origem PDF no documento DDX. Não importa qual seja o nome do arquivo PDF se a chave e o atributo de origem no documento DDX coincidirem.

>[!NOTE]
>
>Um `AssemblerResult` objeto, que contém um objeto de coleção, será retornado se você chamar o `invokeDDX` operação. Essa operação é usada quando você passa dois ou mais documentos de PDF de entrada para o serviço Assembler. No entanto, se você passar apenas um PDF de entrada para o serviço Assembler e esperar apenas um documento de retorno, chame o `invokeOneDocument` operação. Ao invocar esta operação, um único documento é retornado. Para obter informações sobre como usar essa operação, consulte [Montagem de Documentos PDF Criptografados](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte `AssemblerOptionSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Montar os documentos do PDF de entrada**

Depois de criar o cliente de serviço, fazer referência a um arquivo DDX, criar um objeto de coleção que armazene documentos de PDF de entrada e definir opções de tempo de execução, você pode chamar a operação DDX. Ao usar o documento DDX especificado nesta seção, os arquivos map.pdf e direction.pdf são mesclados em um documento PDF.

**Extrair os resultados**

O serviço Assembler retorna um `java.util.Map` objeto, que pode ser obtido do `AssemblerResult` e que contém os resultados da operação. O resultado `java.util.Map` objeto contém os documentos resultantes e quaisquer exceções.

A tabela a seguir resume alguns dos valores-chave e tipos de objeto que podem ser localizados no `java.util.Map` objeto.

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

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `AssemblerServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Consulte um documento DDX existente.

   * Criar um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DDX.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Referencie documentos de PDF de entrada.

   * Criar um `java.util.Map` objeto usado para armazenar documentos de PDF de entrada usando um `HashMap` construtor.
   * Para cada documento de PDF de entrada, crie um `java.io.FileInputStream` usando seu construtor e transmitindo o local do documento PDF de entrada.
   * Para cada documento de PDF de entrada, crie um `com.adobe.idp.Document` e transmita o `java.io.FileInputStream` objeto que contém o documento PDF.
   * Para cada documento de entrada, adicione uma entrada à `java.util.Map` ao invocar seu `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX.
      * A `com.adobe.idp.Document` objeto (ou `java.util.List` objeto que especifica vários documentos) que contém o documento PDF de origem.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa, chamando um método que pertence à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler para continuar processando um job quando ocorrer um erro, chame o `AssemblerOptionSpec` do objeto `setFailOnError` e passar `false`.

1. Montar os documentos do PDF de entrada.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado
   * A `java.util.Map` objeto que contém os arquivos de PDF de entrada a serem montados
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo fonte padrão e nível de log de job

   A variável `invokeDDX` o método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém os resultados do trabalho e quaisquer exceções que ocorreram.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método. Isso retorna um `java.util.Map` objeto.
   * Repita através do `java.util.Map` até encontrar o resultado `com.adobe.idp.Document` objeto. (Você pode usar o elemento de resultado PDF especificado no documento DDX para obter o documento.)
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para extrair o documento PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` foi definido para produzir um log, você pode extrair o log usando o `AssemblerResult` do objeto `getJobLog` método.

**Consulte também**

[Início rápido (modo SOAP): montagem de um documento PDF usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar documentos do PDF usando a API de serviço Web {#assemble-pdf-documents-using-the-web-service-api}

Montar documentos de PDF usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DDX e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Referencie documentos de PDF de entrada.

   * Para cada documento de PDF de entrada, crie um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento PDF de entrada.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` método. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.
   * Criar um `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de coleção é usado para armazenar documentos de PDF de entrada.
   * Para cada documento de PDF de entrada, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto. Por exemplo, se dois documentos de PDF de entrada forem usados, crie dois `MyMapOf_xsd_string_To_xsd_anyType_Item` objetos.
   * Atribua um valor de string que represente o nome da chave à `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` campo. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX. (Execute esta tarefa para cada documento de PDF de entrada.)
   * Atribua a `BLOB` objeto que armazena o documento PDF para o `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` campo. (Execute esta tarefa para cada documento de PDF de entrada.)
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto para o `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` do objeto `Add` e transmita o `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Execute esta tarefa para cada documento de PDF de entrada.)

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa atribuindo um valor a um membro de dados que pertença à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando um job quando ocorrer um erro, atribua `false` para o `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Montar os documentos do PDF de entrada.

   Chame o `AssemblerServiceClient` do objeto `invoke` e passe os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX.
   * A variável `mapItem` matriz que contém os documentos PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem de PDF e seus valores devem ser os `BLOB` objetos que correspondem a esses arquivos.
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução.

   A variável `invoke` o método retorna um `AssemblerResult` objeto que contém os resultados do trabalho e quaisquer exceções que possam ter ocorrido.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` que é um `Map` objeto que contém os documentos PDF de resultado.
   * Repita através do `Map` até encontrar a chave que corresponde ao nome do documento resultante. Em seguida, converta os membros da matriz `value` para um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando seus `BLOB` do objeto `MTOM` propriedade. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` foi definido para produzir um log, você pode extrair o log obtendo o valor de `AssemblerResult` do objeto `jobLog` membro de dados.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
