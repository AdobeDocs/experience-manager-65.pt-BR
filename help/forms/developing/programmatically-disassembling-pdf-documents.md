---
title: Desmontagem programática de Documentos PDF
seo-title: Desmontagem programática de Documentos PDF
description: 'null'
seo-description: nulo
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 0%

---


# Desmontagem programática de Documentos PDF {#programmatically-disassembling-pdf-documents}

Você pode desmontar um documento PDF transmitindo-o para o serviço Assembler. Normalmente, essa tarefa é útil quando o documento PDF foi criado originalmente de vários documentos individuais, como uma coleção de declarações. Na ilustração a seguir, o DocA é dividido em vários documentos resultantes, em que o primeiro marcador de nível 1 em uma página identifica o start de um novo documento resultante.

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

Para desmontar um documento PDF, verifique se o elemento `PDFsFromBookmarks` está localizado no documento DDX. O elemento `PDFsFromBookmarks` é um elemento resultante e pode ser apenas um elemento filho do elemento `DDX`. Ele não tem um atributo `result` porque pode resultar na geração de vários documentos.

O elemento `PDFsFromBookmarks` faz com que um único documento seja gerado para cada marcador de nível 1 no documento de origem.

Para a finalidade desta discussão, suponha que o seguinte documento DX seja usado.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos PDF usando o serviço Assembler. (Consulte [Montagem Programática de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Ao passar um único documento PDF para o serviço Assembler e recuperar um único documento, você pode chamar a operação `invokeOneDocument`. No entanto, para desmontar um documento PDF, use a operação `invokeDDX` porque, embora um documento PDF de entrada seja transmitido ao serviço Assembler, o serviço Assembler retorna um objeto de coleção que contém um ou mais documentos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para desmontar um documento PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente do Montador de PDF.
1. Faça referência a um documento DDX existente.
1. Consulte um documento PDF para desmontar.
1. Defina as opções de tempo de execução.
1. Desmonte o documento PDF.
1. Salve os documentos PDF desmontados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se a AEM Forms estiver implantada em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms estiver implantado em JBoss)

se a AEM Forms for implantada em um servidor de aplicativos J2EE compatível que não seja JBoss, você deverá substituir adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual a AEM Forms está implantada.

**Criar um cliente de Montador de PDF**

Antes de poder executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para desmontar um documento PDF. Esse documento DDX deve conter o elemento `PDFsFromBookmarks`.

**Referência a um documento PDF para desmontar**

Para desmontar um documento PDF, consulte um arquivo PDF que representa o documento PDF a ser desmontado. Quando passado para o serviço Assembler, um documento PDF separado é retornado para cada marcador de nível 1 no documento.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando uma tarefa se um erro for encontrado.

**Desmonte o documento PDF**

Depois de criar o cliente de serviço Assembler, consulte o documento DDX, consulte um documento PDF para desmontar e defina as opções de tempo de execução, você pode desmontar um documento PDF invocando o método `invokeDDX`. Desde que o documento DDX contenha instruções para desmontar o documento PDF, o serviço Assembler retorna documentos PDF desmontados dentro de um objeto de coleção.

**Salve os documentos PDF desmontados**

Todos os documentos PDF desmontados são retornados dentro de um objeto de coleção. Insira o objeto de coleção e salve cada documento PDF como um arquivo PDF.

**Consulte também:**

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Desmonte um documento PDF usando a API Java {#disassemble-a-pdf-document-using-the-java-api}

Desmonte um documento PDF usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente do Montador de PDF.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Faça referência a um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Consulte um documento PDF para desmontar.

   * Crie um objeto `java.util.Map` usado para armazenar documentos PDF de entrada usando um construtor `HashMap`.
   * Crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local do documento PDF a ser desmontado.
   * Crie um objeto `com.adobe.idp.Document` e passe o objeto `java.io.FileInputStream` que contém o documento PDF a ser desmontado.
   * Adicione uma entrada ao objeto `java.util.Map` invocando seu método `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX.
      * Um objeto `com.adobe.idp.Document` que contém o documento PDF a ser desmontado.

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios chamando um método que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, chame o método `AssemblerOptionSpec` do objeto `setFailOnError` e passe `false`.

1. Desmonte o documento PDF.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX a ser usado
   * Um objeto `java.util.Map` que contém o documento PDF a ser desmontado
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível do log de trabalhos

   O método `invokeDDX` retorna um objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contém os documentos PDF desmontados e quaisquer exceções que ocorreram.

1. Salve os documentos PDF desmontados.

   Para obter os documentos PDF desmontados, execute as seguintes ações:

   * Chame o método `AssemblerResult` do objeto `getDocuments`. Isso retorna um objeto `java.util.Map`.
   * Itere pelo objeto `java.util.Map` até encontrar o objeto `com.adobe.idp.Document` resultante.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento PDF.

**Consulte também:**

[Desmontagem programática de Documentos PDF](#programmatically-disassembling-pdf-documents)

[Start rápido (modo SOAP): Desmontagem de um documento PDF usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Desmonte um documento PDF usando a API de serviço da Web {#disassemble-a-pdf-document-using-the-web-service-api}

Desmonte um documento PDF usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao definir uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP do servidor que hospeda o AEM Forms.

1. Crie um cliente do Montador de PDF.

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
   * Crie um objeto `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento DDX e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Consulte um documento PDF para desmontar.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento PDF de entrada. Esse objeto `BLOB` é passado para `invokeOneDocument` como um argumento.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.
   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType`. Esse objeto de coleção é usado para armazenar o PDF a ser desmontado.
   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Atribua um valor de string que representa o nome da chave ao campo `MyMapOf_xsd_string_To_xsd_anyType_Item` `key` do objeto. Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX.
   * Atribua o objeto `BLOB` que armazena o documento PDF ao campo `MyMapOf_xsd_string_To_xsd_anyType_Item` `value` do objeto.
   * Adicione o objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` ao objeto `MyMapOf_xsd_string_To_xsd_anyType`. Chame o método `MyMapOf_xsd_string_To_xsd_anyType` object’ `Add` e passe o objeto `MyMapOf_xsd_string_To_xsd_anyType`.

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios atribuindo um valor a um membro de dados que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, atribua `false` ao campo `AssemblerOptionSpec` do objeto `failOnError`.

1. Desmonte o documento PDF.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX que desmonta o documento PDF
   * O objeto `MyMapOf_xsd_string_To_xsd_anyType` que contém o documento PDF a ser desmontado
   * Um objeto `AssemblerOptionSpec` que especifica opções de tempo de execução

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Salve os documentos PDF desmontados.

   Para obter os documentos PDF recém-criados, execute as seguintes ações:

   * Acesse o campo `AssemblerResult` do objeto `documents`, que é um objeto `Map` que contém os documentos PDF desmontados.
   * Itere pelo objeto `Map` para obter cada documento resultante. Em seguida, converta `value` desse membro da matriz em `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade `BLOB` do objeto `MTOM`. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também:**

[Desmontagem programática de Documentos PDF](#programmatically-disassembling-pdf-documents)

[Invocar o AEM Forms usando o MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
