---
title: Montagem programática de documentos PDF
seo-title: Montagem programática de documentos PDF
description: Use a API do serviço Assembler para reunir vários documentos PDF em um único documento PDF usando a API do Java e a API do serviço da Web.
seo-description: Use a API do serviço Assembler para reunir vários documentos PDF em um único documento PDF usando a API do Java e a API do serviço da Web.
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2153'
ht-degree: 0%

---


# Assemblagem programática de documentos PDF {#programmatically-assembling-pdf-documents}

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

Este documento DDX mescla dois documentos PDF chamados *map.pdf* e *Instruções.pdf* em um único documento PDF.

>[!NOTE]
>
>Para ver um documento DDX que desmonta um documento PDF, consulte [Desmontando Documentos PDF Programaticamente](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de Serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Considerações ao invocar o serviço Assembler usando serviços da Web {#considerations-when-invoking-assembler-service-using-web-services}

Ao adicionar cabeçalhos e rodapés durante a montagem de documentos grandes, você pode encontrar um erro `OutOfMemory` e os arquivos não serão montados. Para reduzir a chance de esse problema ocorrer, adicione um elemento `DDXProcessorSetting` ao documento DDX, conforme mostrado no exemplo a seguir.

`<DDXProcessorSetting name="checkpoint" value="2000" />`

Você pode adicionar esse elemento como filho do elemento `DDX` ou como filho de um elemento `PDF result`. O valor padrão para essa configuração é 0 (zero), que desativa a marcação de verificação e o DDX se comporta como se o elemento `DDXProcessorSetting` não estivesse presente. Se você encontrou um erro `OutOfMemory`, talvez precise definir o valor como um número inteiro, normalmente entre 500 e 5000. Um pequeno valor de ponto de verificação resulta em uma verificação mais frequente.

## Resumo das etapas {#summary-of-steps}

Para montar um único documento PDF a partir de vários documentos PDF, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Assembler do PDF.
1. Faça referência a um documento DDX existente.
1. Faça referência a documentos PDF de entrada.
1. Defina as opções de tempo de execução.
1. Monte os documentos PDF de entrada.
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

**Referência a documentos PDF de entrada**

Faça referência a documentos PDF de entrada que você deseja passar para o serviço Assembler. Por exemplo, se você quiser transmitir dois documentos PDF de entrada chamados Mapa e Direções, é necessário transmitir os arquivos PDF correspondentes.

O arquivo map.pdf e o arquivo directions.pdf devem ser colocados em um objeto de coleção. O nome da chave deve corresponder ao valor do atributo de origem do PDF no documento DX. Não importa qual é o nome do arquivo PDF se a chave e o atributo de origem no documento DX corresponderem.

>[!NOTE]
>
>Um objeto `AssemblerResult`, que contém um objeto de coleção, é retornado se você chamar a operação `invokeDDX`. Essa operação é usada quando você passa dois ou mais documentos PDF de entrada para o serviço Assembler. No entanto, se você passar apenas um PDF de entrada para o serviço Assembler e esperar apenas um documento de retorno, chame a operação `invokeOneDocument`. Ao invocar esta operação, um único documento é retornado. Para obter informações sobre como usar essa operação, consulte [Assembling Encrypted PDF Documents](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents).

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrua o serviço Assembler a continuar processando um trabalho se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte a referência da classe `AssemblerOptionSpec` em [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Montar os documentos PDF de entrada**

Depois de criar o cliente do serviço, fazer referência a um arquivo DDX, criar um objeto de coleção que armazena documentos PDF de entrada e definir opções de tempo de execução, você pode chamar a operação DDX. Ao usar o documento DDX especificado nesta seção, os arquivos map.pdf e Direction.pdf são unidos em um documento PDF.

**Extraia os resultados**

O serviço Assembler retorna um objeto `java.util.Map`, que pode ser obtido a partir do objeto `AssemblerResult` e que contém os resultados da operação. O objeto `java.util.Map` retornado contém os documentos resultantes e quaisquer exceções.

A tabela a seguir resume alguns dos valores principais e tipos de objeto que podem ser localizados no objeto `java.util.Map` retornado.

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

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Desmontagem programática de documentos PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Monte documentos PDF usando a API Java {#assemble-pdf-documents-using-the-java-api}

Monte um documento PDF usando a API do Serviço de Assembler (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente Assembler do PDF.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Faça referência a um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifique o local do arquivo DX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Faça referência a documentos PDF de entrada.

   * Crie um objeto `java.util.Map` que é usado para armazenar documentos PDF de entrada usando um construtor `HashMap`.
   * Para cada documento PDF de entrada, crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local do documento PDF de entrada.
   * Para cada documento PDF de entrada, crie um objeto `com.adobe.idp.Document` e passe o objeto `java.io.FileInputStream` que contém o documento PDF.
   * Para cada documento de entrada, adicione uma entrada ao objeto `java.util.Map` chamando seu método `put` e passando os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX.
      * Um objeto `com.adobe.idp.Document` (ou `java.util.List` objeto que especifica vários documentos) que contém o documento PDF de origem.

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor .
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios, chamando um método que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, chame o método `AssemblerOptionSpec` do objeto `setFailOnError` e passe `false`.

1. Monte os documentos PDF de entrada.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX a ser usado
   * Um objeto `java.util.Map` que contém os arquivos PDF de entrada a serem montados
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do trabalho

   O método `invokeDDX` retorna um objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o método `AssemblerResult` do objeto `getDocuments`. Isso retorna um objeto `java.util.Map`.
   * Itere pelo objeto `java.util.Map` até encontrar o objeto `com.adobe.idp.Document` resultante. (Você pode usar o elemento de resultado PDF especificado no documento DX para obter o documento.)
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` foi definido para produzir um log, você pode extrair o log usando o método `AssemblerResult` `getJobLog` do objeto.

**Consulte também:**

[Início rápido (modo SOAP): Montagem de um documento PDF usando a API do Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Monte documentos PDF usando a API do serviço da Web {#assemble-pdf-documents-using-the-web-service-api}

Monte documentos PDF usando a API do Serviço de Assembler (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente Assembler do PDF.

   * Crie um objeto `AssemblerServiceClient` usando seu construtor padrão.
   * Crie um objeto `AssemblerServiceClient.Endpoint.Address` usando o construtor `System.ServiceModel.EndpointAddress`. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Você não precisa usar o atributo `lc_version`. Esse atributo é usado ao criar uma referência de serviço.
   * Crie um objeto `System.ServiceModel.BasicHttpBinding` obtendo o valor do campo `AssemblerServiceClient.Endpoint.Binding`. Converta o valor de retorno em `BasicHttpBinding`.
   * Defina o campo `System.ServiceModel.BasicHttpBinding` `MessageEncoding` do objeto para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Atribua o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribua o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a um documento DDX existente.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento DDX.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento DX e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e passando a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Faça referência a documentos PDF de entrada.

   * Para cada documento PDF de entrada, crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF de entrada.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.
   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType`. Esse objeto de coleção é usado para armazenar documentos PDF de entrada.
   * Para cada documento PDF de entrada, crie um objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Por exemplo, se dois documentos PDF de entrada forem usados, crie dois objetos `MyMapOf_xsd_string_To_xsd_anyType_Item` .
   * Atribua um valor de string que represente o nome da chave ao campo `MyMapOf_xsd_string_To_xsd_anyType_Item` `key` do objeto. Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX. (Execute essa tarefa para cada documento PDF de entrada.)
   * Atribua o objeto `BLOB` que armazena o documento PDF ao campo `MyMapOf_xsd_string_To_xsd_anyType_Item` `value` do objeto. (Execute essa tarefa para cada documento PDF de entrada.)
   * Adicione o objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` ao objeto `MyMapOf_xsd_string_To_xsd_anyType`. Chame o método `MyMapOf_xsd_string_To_xsd_anyType` do objeto `Add` e passe o objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Execute essa tarefa para cada documento PDF de entrada.)

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor .
   * Defina as opções de tempo de execução para atender aos requisitos de negócios, atribuindo um valor a um membro de dados que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, atribua `false` ao membro de dados `AssemblerOptionSpec` do objeto `failOnError`.

1. Monte os documentos PDF de entrada.

   Chame o método `AssemblerServiceClient` do objeto `invoke` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX.
   * A matriz `mapItem` que contém os documentos PDF de entrada. Suas chaves devem corresponder aos nomes dos arquivos de origem do PDF e seus valores devem ser os objetos `BLOB` que correspondem a esses arquivos.
   * Um objeto `AssemblerOptionSpec` que especifica as opções de tempo de execução.

   O método `invoke` retorna um objeto `AssemblerResult` que contém os resultados da tarefa e quaisquer exceções que possam ter ocorrido.

1. Extraia os resultados.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Acesse o campo `AssemblerResult` do objeto `documents`, que é um objeto `Map` que contém os documentos PDF de resultado.
   * Itere pelo objeto `Map` até encontrar a chave que corresponde ao nome do documento resultante. Em seguida, converta esse membro da matriz `value` em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade `BLOB` do objeto `MTOM`. Isso retorna uma matriz de bytes que podem ser gravados em um arquivo PDF.

   >[!NOTE]
   >
   >Se `LOG_LEVEL` foi definido para produzir um log, você pode extrair o log obtendo o valor do membro de dados `AssemblerResult` do objeto `jobLog`.

**Consulte também:**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
