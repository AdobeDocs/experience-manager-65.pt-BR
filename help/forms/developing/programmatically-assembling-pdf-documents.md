---
title: Montagem Programática de Documentos PDF
seo-title: Montagem Programática de Documentos PDF
description: 'null'
seo-description: 'null'
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
translation-type: tm+mt
source-git-commit: 868936e0fd20d3867e31f0351d7b388149472fd2

---


# Montagem Programática de Documentos PDF {#programmatically-assembling-pdf-documents}

Você pode usar a API de serviço do Assembler para reunir vários documentos PDF em um único documento PDF. A ilustração a seguir mostra três documentos PDF sendo mesclados em um único documento PDF.

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

Para montar dois ou mais documentos PDF em um único documento PDF, é necessário um documento DDX. Um documento DDX descreve o documento PDF que o serviço Assembler produz. Ou seja, o documento DDX instrui o serviço Assembler sobre as ações a serem executadas.

Para a finalidade desta discussão, suponha que o seguinte documento DX seja usado.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

Este documento DDX mescla dois documentos PDF chamados *map.pdf* e *direcçõespdf* em um único documento PDF.

>[!NOTE]
>
>Para ver um documento DDX que desmonta um documento PDF, consulte Desmontagem [programática de documentos](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)PDF.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

>[!NOTE]
>
>Para obter mais informações sobre um documento DX, consulte Serviço de [Montagem e Referência](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Considerações ao invocar o serviço Assembler usando serviços da Web {#considerations-when-invoking-assembler-service-using-web-services}

Ao adicionar cabeçalhos e rodapés durante a montagem de documentos grandes, você pode encontrar um `OutOfMemory` erro e os arquivos não serão montados. Para reduzir a chance de esse problema ocorrer, adicione um `DDXProcessorSetting` elemento ao documento DDX, como mostrado no exemplo a seguir.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Você pode adicionar esse elemento como filho do `DDX` elemento ou como filho de um `PDF result` elemento. O valor padrão para essa configuração é 0 (zero), que desativa a opção de verificação e o DDX se comporta como se o `DDXProcessorSetting` elemento não estivesse presente. Se tiver encontrado um `OutOfMemory` erro, talvez seja necessário definir o valor como um número inteiro, normalmente entre 500 e 5000. Um pequeno valor de ponto de verificação resulta em um ponto de verificação mais frequente.

## Resumo das etapas {#summary-of-steps}

Para montar um único documento PDF a partir de vários documentos PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente do Montador de PDF.
1. Faça referência a um documento DDX existente.
1. Referência a documentos PDF de entrada.
1. Defina as opções de tempo de execução.
1. Monte os documentos PDF de entrada.
1. Extraia os resultados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado em JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado.

**Criar um cliente de Montador de PDF**

Antes de poder executar programaticamente uma operação do Assembler, é necessário criar um cliente do Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Por exemplo, considere o documento DDX que foi introduzido nesta seção. Este documento DDX instrui o serviço Assembler a unir dois documentos PDF em um único documento PDF.

**Referência a documentos PDF de entrada**

Faça referência a documentos PDF de entrada que você deseja transmitir ao serviço Assembler. Por exemplo, se você quiser passar dois documentos PDF de entrada chamados Mapa e Direções, é necessário passar os arquivos PDF correspondentes.

O arquivo map.pdf e o arquivo Direcções.pdf devem ser colocados em um objeto de coleção. O nome da chave deve corresponder ao valor do atributo de origem do PDF no documento DX. Não importa qual é o nome do arquivo PDF se a chave e o atributo de origem no documento DX correspondem.

>[!NOTE]
>
>Um `AssemblerResult` objeto, que contém um objeto de coleção, será retornado se você chamar a operação `invokeDDX` . Essa operação é usada quando você passa dois ou mais documentos PDF de entrada para o serviço Assembler. No entanto, se você enviar apenas um PDF de entrada para o serviço Assembler e esperar apenas um documento de retorno, chame a `invokeOneDocument` operação. Ao invocar esta operação, um único documento é retornado. Para obter informações sobre como usar essa operação, consulte [Montagem de documentos](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)PDF criptografados.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando uma tarefa se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte a referência de `AssemblerOptionSpec` classe em Referência [de API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Montar os documentos PDF de entrada**

Depois de criar o cliente de serviço, fazer referência a um arquivo DDX, criar um objeto de coleção que armazene documentos PDF de entrada e definir opções de tempo de execução, você pode chamar a operação DDX. Ao usar o documento DDX especificado nesta seção, os arquivos map.pdf e direcçãomo.pdf são mesclados em um documento PDF.

**Extrair os resultados**

O serviço Assembler retorna um `java.util.Map` objeto, que pode ser obtido a partir do `AssemblerResult` objeto e que contém os resultados da operação. O `java.util.Map` objeto retornado contém os documentos resultantes e quaisquer exceções.

A tabela a seguir resume alguns dos principais valores e tipos de objetos que podem ser localizados no `java.util.Map` objeto retornado.

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

**Consulte também:**

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontagem Programática de Documentos PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Montar documentos PDF usando a API Java {#assemble-pdf-documents-using-the-java-api}

Monte um documento PDF usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente do Montador de PDF.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `AssemblerServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que represente o documento DX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DX.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Referência a documentos PDF de entrada.

   * Crie um `java.util.Map` objeto usado para armazenar documentos PDF de entrada usando um `HashMap` construtor.
   * Para cada documento PDF de entrada, crie um `java.io.FileInputStream` objeto usando seu construtor e transmitindo o local do documento PDF de entrada.
   * Para cada documento PDF de entrada, crie um `com.adobe.idp.Document` objeto e passe o `java.io.FileInputStream` objeto que contém o documento PDF.
   * Para cada documento de entrada, adicione uma entrada ao `java.util.Map` objeto chamando seu `put` método e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX.
      * Um `com.adobe.idp.Document` objeto (ou `java.util.List` objeto que especifica vários documentos) que contém o documento PDF de origem.

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, chame o `AssemblerOptionSpec` método do `setFailOnError` objeto e passe `false`.

1. Monte os documentos PDF de entrada.

   Chame o `AssemblerServiceClient` método do `invokeDDX` objeto e passe os seguintes valores obrigatórios:

   * Um `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado
   * Um `java.util.Map` objeto que contém os arquivos PDF de entrada a serem montados
   * Um `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log de trabalhos
   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o `AssemblerResult` método do `getDocuments` objeto. Isso retorna um `java.util.Map` objeto.
   * Iterar pelo `java.util.Map` objeto até encontrar o `com.adobe.idp.Document` objeto resultante. (Você pode usar o elemento de resultado do PDF especificado no documento DX para obter o documento.)
   * Chame o `com.adobe.idp.Document` `copyToFile` método do objeto para extrair o documento PDF.
   >[!NOTE]
   >
   >Se `LOG_LEVEL` foi definido para produzir um log, você pode extrair o log usando o `AssemblerResult` `getJobLog` método do objeto.

**Consulte também:**

[Início rápido (modo SOAP): Montagem de um documento PDF usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar documentos PDF usando a API de serviço da Web {#assemble-pdf-documents-using-the-web-service-api}

Monte documentos PDF usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente do Montador de PDF.

   * Crie um `AssemblerServiceClient` objeto usando seu construtor padrão.
   * Crie um `AssemblerServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço de formulários AEM (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar o `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um `System.ServiceModel.BasicHttpBinding` objeto obtendo o valor do `AssemblerServiceClient.Endpoint.Binding` campo. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` campo do `MessageEncoding` objeto como `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor da senha correspondente ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a um documento DDX existente.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento DX.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DX e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo sua `MTOM` propriedade ao conteúdo da matriz de bytes.

1. Referência a documentos PDF de entrada.

   * Para cada documento PDF de entrada, crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento PDF de entrada.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Esse objeto de coleção é usado para armazenar documentos PDF de entrada.
   * Para cada documento PDF de entrada, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto. Por exemplo, se dois documentos PDF de entrada forem usados, crie dois `MyMapOf_xsd_string_To_xsd_anyType_Item` objetos.
   * Atribua um valor de string que representa o nome da chave ao campo do `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto `key` . Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX. (Execute essa tarefa para cada documento PDF de entrada.)
   * Atribua o `BLOB` objeto que armazena o documento PDF ao `MyMapOf_xsd_string_To_xsd_anyType_Item` campo do `value` objeto. (Execute essa tarefa para cada documento PDF de entrada.)
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto ao `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` método do objeto `Add` e passe o `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Execute essa tarefa para cada documento PDF de entrada.)

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios, atribuindo um valor a um membro de dados que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, atribua `false` ao membro de `AssemblerOptionSpec` dados do objeto `failOnError` .

1. Monte os documentos PDF de entrada.

   Chame o método do `AssemblerServiceClient` objeto `invoke` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o documento DX.
   * O `mapItem` storage que contém os documentos PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem do PDF, e seus valores devem ser os `BLOB` objetos que correspondem a esses arquivos.
   * Um `AssemblerOptionSpec` objeto que especifica opções de tempo de execução.
   O `invoke` método retorna um `AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que possam ter ocorrido.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` campo do `documents` objeto, que é um `Map` objeto que contém os documentos PDF de resultado.
   * Itere pelo `Map` objeto até encontrar a chave que corresponde ao nome do documento resultante. Em seguida, converta o membro do storage `value` em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade do `BLOB` objeto `MTOM` . Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.
   >[!NOTE]
   >
   >Se `LOG_LEVEL` foi definido para produzir um log, você pode extrair o log obtendo o valor do membro de `AssemblerResult` `jobLog` dados do objeto.

**Consulte também:**

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
