---
title: Montagem de documentos do PDF com marcadores
description: Use o serviço Assembler para modificar um documento PDF que não contenha marcadores para incluir marcadores usando a API Java e a API do serviço Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2519'
ht-degree: 0%

---

# Montagem de documentos do PDF com marcadores {#assembling-pdf-documents-with-bookmarks}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

Você pode montar um documento PDF que contenha marcadores. Por exemplo, suponha que você tenha um documento PDF que não contenha marcadores e deseje modificá-lo fornecendo marcadores. Usando o serviço Assembler, você pode passá-lo para um documento PDF que não contenha marcadores e recuperar um documento PDF que contenha marcadores.

Os marcadores contêm as seguintes propriedades:

* Um título que aparece como texto na tela.
* Uma ação que especifica o que acontece quando um usuário clica no marcador. A ação típica de um marcador é mover para outro local no documento atual ou abrir outro documento PDF, embora outras ações possam ser especificadas.

Para o propósito desta discussão, suponha que o seguinte documento DDX seja usado.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

Neste documento DDX, observe que o valor `Loan.pdf` é atribuído ao atributo de origem. Este documento DDX especifica que um único documento PDF é passado para o serviço Assembler. Ao montar um documento PDF com marcadores, você deve especificar um documento XML de marcador que descreva os marcadores no documento resultante. Para especificar um documento XML de marcador, verifique se o elemento `Bookmarks` está especificado no documento DDX.

Neste exemplo de documento DDX, o elemento `Bookmarks` especifica `doc2` como o valor. Este valor indica que o mapa de entrada passado para o serviço Assembler contém uma chave chamada `doc2`. O valor da chave `doc2` é um valor `com.adobe.idp.Document` que representa o documento XML do marcador. (Consulte &quot;Idioma de marcadores&quot; no [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).)

Este tópico usa a seguinte linguagem de marcadores XML para montar um documento PDF que contém marcadores.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
       <Bookmark>
          <Action>
             <Launch NewWindow="true">
                <File Name="C:\Adobe\LoanDetails.pdf" />
             </Launch>
          </Action>
         <Title>Open the Loan document</Title>
       </Bookmark>
 <Bookmark>
          <Action>
             <Launch>
                <Win Name="C:\WINDOWS\notepad.exe" />
             </Launch>
          </Action>
     <Title>Launch NotePad</Title>
       </Bookmark>
 </Bookmarks>
```

Neste documento XML de marcador, observe o elemento Ação que define a ação executada quando um usuário clica no marcador. No elemento Ação está o elemento Iniciar, que inicia aplicativos, como o Bloco de Notas, e abre arquivos, como arquivos PDF. Para abrir um arquivo PDF, você deve usar o elemento File que especifica o arquivo a ser aberto. Por exemplo, no arquivo XML de marcador especificado nesta seção, o nome do arquivo aberto é LoanDetails.pdf.

>[!NOTE]
>
>Para obter detalhes completos sobre as ações com suporte, consulte &quot; `Action` elemento&quot; no [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

Dado o documento DDX especificado nesta seção e o arquivo XML de marcador como entrada, o serviço do Assembler monta um documento PDF que contém os marcadores a seguir.

![aw_bmark](assets/aw_aw_bmark.png)

Quando um usuário clica no marcador *Abrir detalhes do empréstimo*, o arquivo LoanDetails.pdf é aberto. Da mesma forma, quando o usuário clica no *Bloco de Notas do Launch*, o Bloco de Notas é iniciado.

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos do PDF usando o serviço Assembler. Esta seção não discute conceitos, como criar um objeto de coleção que contenha documentos de entrada ou saber como extrair os resultados do objeto de coleção retornado. (Consulte [Assembling Programmatically PDF Documents](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço do Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar um documento PDF que contenha marcadores, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDF Assembler.
1. Consulte um documento DDX existente.
1. Referencie um documento PDF ao qual os marcadores são adicionados.
1. Referencie o documento XML do marcador.
1. Adicione o documento PDF e o documento XML do marcador a uma coleção Map.
1. Definir opções de tempo de execução.
1. Monte o documento PDF.
1. Salve o documento PDF que contém marcadores.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado. Para obter informações sobre a localização de todos os arquivos JAR do AEM Forms, consulte [Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referenciar um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Este documento DDX deve conter o elemento `Bookmarks`, que instrui o serviço Assembler a montar um PDF que contenha marcadores. (Consulte o documento DDX mostrado anteriormente nesta seção para ver um exemplo.)

**Referencie um documento PDF ao qual os marcadores são adicionados**

Referencie um documento PDF ao qual os marcadores são adicionados. Não importa se o PDF referenciado já contém marcadores. Se o elemento `Bookmarks` for filho do elemento de origem PDF, os Marcadores substituirão aqueles que já existem na origem PDF. No entanto, se você quiser manter os marcadores existentes, verifique se `Bookmarks` é irmão do elemento de origem PDF. Por exemplo, considere o seguinte exemplo:

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Referenciar o documento XML do indicador**

Para montar um PDF que contenha novos marcadores, você deve fazer referência a um documento XML de marcador. O documento XML do indicador é passado para o serviço Assembler dentro do objeto da coleção Map. (Consulte o documento XML de marcador mostrado anteriormente nesta seção para obter um exemplo.)

>[!NOTE]
>
>Consulte &quot;Idioma dos Indicadores&quot; no [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Adicionar o documento PDF e o documento XML do marcador a uma coleção de Mapas**

Adicione o documento PDF ao qual os marcadores são adicionados e o documento XML do marcador à coleção Map. Portanto, o objeto de coleção Map contém dois elementos: um documento PDF e o documento XML de marcador.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que você pode definir, consulte a referência de classe `AssemblerOptionSpec` na [Referência da API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Montar o documento PDF**

Para montar um documento PDF que contenha novos marcadores, use a operação `invokeDDX` do serviço Assembler. O motivo pelo qual você deve usar a operação `invokeDDX` em vez de outras operações de serviço do Assembler, como `invokeOneDocument`, é porque o serviço Assembler requer um documento XML de indicador passado dentro do objeto da coleção Map. Este objeto é um parâmetro da operação `invokeDDX`.

**Salve o documento PDF que contém os marcadores**

Extraia os resultados do objeto de mapa retornado e salve o documento PDF correspondente. (Consulte &quot;Extrair os resultados&quot; em [Montando documentos de PDF de forma programática](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar documentos do PDF com marcadores usando a API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Montar um documento PDF com marcadores usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente PDF Assembler.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Consulte um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do arquivo DDX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Referencie um documento PDF ao qual os marcadores são adicionados.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e passe o objeto `java.io.FileInputStream` que contém o documento PDF.

1. Referencie o documento XML do marcador.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local do arquivo XML que representa o documento XML do marcador.
   * Crie um objeto `com.adobe.idp.Document` e passe o objeto `java.io.FileInputStream` que contém o documento PDF.

1. Adicione o documento PDF e o documento XML do marcador a uma coleção Map.

   * Crie um objeto `java.util.Map` que seja usado para armazenar o documento PDF de entrada e o documento XML de marcador.
   * Adicione o documento do PDF de entrada chamando o método `put` do objeto `java.util.Map` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX.
      * Um objeto `com.adobe.idp.Document` que contém o documento de PDF de entrada.

   * Adicione o documento XML de indicador invocando o método `put` do objeto `java.util.Map` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem Marcadores especificado no documento DDX.
      * Um objeto `com.adobe.idp.Document` que contém o documento XML do indicador.

1. Definir opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos da sua empresa invocando um método que pertença ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, chame o método `setFailOnError` do objeto `AssemblerOptionSpec` e passe `false`.

1. Monte o documento PDF.

   Invoque o método `invokeDDX` do objeto `AssemblerServiceClient` e passe os seguintes valores obrigatórios:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX a ser usado
   * Um objeto `java.util.Map` que contém o documento PDF de entrada e o documento XML de marcador.
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do trabalho

   O método `invokeDDX` retorna um objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contém os resultados do trabalho e as exceções que ocorreram.

1. Salve o documento PDF que contém marcadores.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Invoque o método `getDocuments` do objeto `AssemblerResult`. Isso retorna um objeto `java.util.Map`.
   * Repita o objeto `java.util.Map` até encontrar o objeto `com.adobe.idp.Document` resultante. (Você pode usar o elemento de resultado PDF especificado no documento DDX para obter o documento.)
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para extrair o documento PDF.

**Consulte também**

[Início rápido (modo SOAP): montagem de documentos PDF com marcadores usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar documentos do PDF com marcadores usando a API de serviço da Web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Montar um documento PDF com marcadores usando a API de serviço do Assembler (serviço Web):

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
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` com o conteúdo da matriz de bytes.

1. Referencie um documento PDF ao qual os marcadores são adicionados.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o PDF de entrada.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` com o conteúdo da matriz de bytes.

1. Referencie o documento XML do marcador.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento XML do marcador.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` com o conteúdo da matriz de bytes.

1. Adicione o documento PDF e o documento XML do marcador a uma coleção Map.

   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de coleção é usado para armazenar os documentos de PDF de entrada e o documento XML do marcador.
   * Para cada documento PDF de entrada e o documento XML de marcador, crie um objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Atribua um valor de cadeia de caracteres que represente o nome da chave para o campo `key` do objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX.
   * Atribua o objeto `BLOB` que armazena o documento PDF ao campo `value` do objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Adicione o objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` ao objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque o método `Add` do objeto `MyMapOf_xsd_string_To_xsd_anyType` e passe o objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Execute esta tarefa para cada documento de PDF de entrada e para o documento XML de marcador.)

1. Definir opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos comerciais atribuindo um valor a um membro de dados que pertença ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, atribua `false` ao membro de dados `failOnError` do objeto `AssemblerOptionSpec`.

1. Monte o documento PDF.

   Invoque o método `invokeDDX` do objeto `AssemblerServiceClient` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX
   * A matriz `MyMapOf_xsd_string_To_xsd_anyType` que contém os documentos de entrada
   * Um objeto `AssemblerOptionSpec` que especifica as opções de tempo de execução

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém os resultados do trabalho e quaisquer exceções que possam ter ocorrido.

1. Salve o documento PDF que contém marcadores.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Acesse o campo `documents` do objeto `AssemblerResult`, que é um objeto `Map` que contém os documentos de PDF de resultado.
   * Repita através do objeto `Map` até encontrar a chave que corresponde ao nome do documento resultante. Em seguida, converta o `value` desse membro da matriz em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando o campo `MTOM` do objeto `BLOB`. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
