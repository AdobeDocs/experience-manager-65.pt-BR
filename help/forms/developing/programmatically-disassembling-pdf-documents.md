---
title: Desmontando Documentos PDF de Forma Programática
seo-title: Programmatically Disassembling PDF Documents
description: Use o serviço Assembler para desmontar um único documento de PDF em vários documentos de PDF usando a API Java e a API do serviço da Web.
seo-description: Use the Assembler service to disassemble a single PDF document into multiple PDF documents using the Java API and the Web Service API.
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 0%

---

# Desmontando Documentos PDF de Forma Programática {#programmatically-disassembling-pdf-documents}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

Você pode desmontar um documento PDF passando-o para o serviço Assembler. Normalmente, essa tarefa é útil quando o documento PDF foi criado originalmente a partir de muitos documentos individuais, como uma coleção de instruções. Na ilustração a seguir, o DocA é dividido em vários documentos resultantes, em que o primeiro marcador de nível 1 em uma página identifica o início de um novo documento resultante.

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

Para desmontar um documento PDF, verifique se `PDFsFromBookmarks` elemento está localizado no documento DDX. A variável `PDFsFromBookmarks` elemento é um elemento resultante e só pode ser um elemento filho de `DDX` elemento. Ele não tem um `result` porque pode resultar na geração de vários documentos.

A variável `PDFsFromBookmarks` elemento faz com que um único documento seja gerado para cada marcador de nível 1 no documento de origem.

Para o propósito desta discussão, considere que o documento DDX a seguir seja usado.

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
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos do PDF usando o serviço Assembler. (Consulte [Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Ao passar um único documento de PDF para o serviço Assembler e recuperar um único documento, você pode chamar o `invokeOneDocument` operação. No entanto, para desmontar um documento PDF, use o `invokeDDX` operação porque, embora um documento de PDF de entrada seja passado para o serviço Assembler, o serviço Assembler retorna um objeto de coleção que contém um ou mais documentos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para desmontar um documento PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDF Assembler.
1. Consulte um documento DDX existente.
1. Referencie um documento do PDF para desmontar.
1. Definir opções de tempo de execução.
1. Desmonte o documento PDF.
1. Salve os documentos de PDF desmontados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível que não seja JBoss, você deverá substituir adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado.

**Criar um cliente do PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referencie um documento DDX existente**

Um documento DDX deve ser referenciado para desmontar um documento PDF. Este documento DDX deve conter a `PDFsFromBookmarks` elemento.

**Referencie um documento do PDF para desmontar**

Para desmontar um documento PDF, consulte um arquivo PDF que representa o documento PDF a ser desmontado. Quando passado para o serviço Assembler, um documento PDF separado é retornado para cada marcador de nível 1 no documento.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado.

**Desmontar o documento PDF**

Depois de criar o cliente de serviço do Assembler, fazer referência ao documento DDX, fazer referência a um documento PDF para desmontar e definir opções de tempo de execução, você poderá desmontar um documento PDF chamando o `invokeDDX` método. Desde que o documento DDX contenha instruções para desmontar o documento PDF, o serviço do Assembler retornará documentos PDF desmontados dentro de um objeto de coleção.

**Salve os documentos de PDF desmontados**

Todos os documentos de PDF desmontados são retornados dentro de um objeto de coleção. Repita o processo através do objeto de coleção e salve cada documento de PDF como um arquivo de PDF.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Desmontar um documento PDF usando a API Java {#disassemble-a-pdf-document-using-the-java-api}

Desmonte um documento PDF usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente PDF Assembler.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `AssemblerServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Consulte um documento DDX existente.

   * Criar um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DDX.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Referencie um documento do PDF para desmontar.

   * Criar um `java.util.Map` objeto usado para armazenar documentos de PDF de entrada usando um `HashMap` construtor.
   * Criar um `java.io.FileInputStream` usando seu construtor e transmitindo o local do documento PDF a ser desmontado.
   * Criar um `com.adobe.idp.Document` e transmita o `java.io.FileInputStream` objeto que contém o documento PDF a ser desmontado.
   * Adicione uma entrada à `java.util.Map` ao invocar seu `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX.
      * A `com.adobe.idp.Document` objeto que contém o documento PDF a ser desmontado.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa, chamando um método que pertence à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler para continuar processando um job quando ocorrer um erro, chame o `AssemblerOptionSpec` do objeto `setFailOnError` e passar `false`.

1. Desmonte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado
   * A `java.util.Map` objeto que contém o documento PDF a ser desmontado
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do job

   A variável `invokeDDX` o método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém os documentos PDF desmontados e quaisquer exceções que ocorreram.

1. Salve os documentos de PDF desmontados.

   Para obter os documentos de PDF desmontados, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método. Isso retorna um `java.util.Map` objeto.
   * Repita através do `java.util.Map` até encontrar o resultado `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para extrair o documento PDF.

**Consulte também**

[Desmontando Documentos PDF de Forma Programática](#programmatically-disassembling-pdf-documents)

[Início rápido (modo SOAP): desmontagem de um documento PDF usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Desmontar um documento PDF usando a API de serviço Web {#disassemble-a-pdf-document-using-the-web-service-api}

Desmonte um documento PDF usando a API de serviço do Assembler (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao configurar uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento DDX e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Referencie um documento do PDF para desmontar.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento PDF de entrada. Este `BLOB` objeto é passado para o `invokeOneDocument` como argumento.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` o conteúdo da matriz de bytes.
   * Criar um `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de coleção é usado para armazenar o PDF a ser desmontado.
   * Criar um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua um valor de string que represente o nome da chave à `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` campo. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX.
   * Atribua a `BLOB` objeto que armazena o documento PDF para o `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` campo.
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto para o `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` object&quot; `Add` e transmita o `MyMapOf_xsd_string_To_xsd_anyType` objeto.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa atribuindo um valor a um membro de dados que pertença à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando um job quando ocorrer um erro, atribua `false` para o `AssemblerOptionSpec` do objeto `failOnError` campo.

1. Desmonte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX que desmonta o documento PDF
   * A variável `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém o documento PDF a ser desmontado
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   A variável `invokeDDX` o método retorna um `AssemblerResult` objeto que contém os resultados do processo e quaisquer exceções que ocorreram.

1. Salve os documentos de PDF desmontados.

   Para obter os documentos PDF recém-criados, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` que é um `Map` objeto que contém os documentos PDF desmontados.
   * Repita através do `Map` para obter cada documento resultante. Em seguida, converta os membros da matriz `value` para um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando seus `BLOB` do objeto `MTOM` propriedade. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também**

[Desmontando Documentos PDF de Forma Programática](#programmatically-disassembling-pdf-documents)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
