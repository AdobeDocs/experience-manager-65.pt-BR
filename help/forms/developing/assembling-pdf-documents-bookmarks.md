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

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

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

Neste documento DDX, observe que o valor é atribuído ao atributo de origem `Loan.pdf`. Este documento DDX especifica que um único documento PDF é passado para o serviço Assembler. Ao montar um documento PDF com marcadores, você deve especificar um documento XML de marcador que descreva os marcadores no documento resultante. Para especificar um documento XML de marcador, verifique se `Bookmarks` elemento está especificado no seu documento DDX.

Neste exemplo de documento DDX, a variável `Bookmarks` element especifica `doc2` como o valor. Esse valor indica que o mapa de entrada passado para o serviço Assembler contém uma chave chamada `doc2`. O valor de `doc2` a chave é um `com.adobe.idp.Document` valor que representa o documento XML do indicador. (Consulte &quot;Idioma de marcadores&quot; no [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).)

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
>Para obter detalhes completos sobre as ações compatíveis, consulte &quot; `Action` element&quot; na caixa [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

Dado o documento DDX especificado nesta seção e o arquivo XML de marcador como entrada, o serviço do Assembler monta um documento PDF que contém os marcadores a seguir.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Quando um usuário clica na variável *Abrir os detalhes do empréstimo* o arquivo LoanDetails.pdf é aberto. Da mesma forma, quando o usuário clica na variável *Iniciar Bloco de Notas* marcador, o Bloco de Notas é iniciado.

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos do PDF usando o serviço Assembler. Esta seção não discute conceitos, como criar um objeto de coleção que contenha documentos de entrada ou saber como extrair os resultados do objeto de coleção retornado. (Consulte [Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado. Para obter informações sobre a localização de todos os arquivos JAR do AEM Forms, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente do PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referencie um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Este documento DDX deve conter a `Bookmarks` elemento, que instrui o serviço Assembler a montar um PDF que contém marcadores. (Consulte o documento DDX mostrado anteriormente nesta seção para ver um exemplo.)

**Referência a um documento do PDF ao qual os marcadores são adicionados**

Referencie um documento PDF ao qual os marcadores são adicionados. Não importa se o PDF referenciado já contém marcadores. Se a variável `Bookmarks` O elemento é filho do elemento de origem PDF, então os Marcadores substituirão os que já existem na origem PDF. No entanto, se desejar manter os marcadores existentes, verifique se `Bookmarks` é um irmão do elemento fonte PDF. Por exemplo, considere o seguinte exemplo:

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
>Consulte &quot;Idioma dos marcadores&quot; no [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Adicionar o documento PDF e o documento XML do marcador a uma coleção de Mapas**

Adicione o documento PDF ao qual os marcadores são adicionados e o documento XML do marcador à coleção Map. Portanto, o objeto de coleção Map contém dois elementos: um documento PDF e o documento XML de marcador.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte `AssemblerOptionSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Montar o documento PDF**

Para montar um documento PDF que contenha novos marcadores, use o `invokeDDX` operação. O motivo pelo qual você deve usar a variável `invokeDDX` operações do Assembler em oposição a outras operações de serviço do Assembler, como `invokeOneDocument` é porque o serviço Assembler requer um documento XML de indicador passado dentro do objeto da coleção Map. Esse objeto é um parâmetro da variável `invokeDDX` operação.

**Salve o documento PDF que contém marcadores**

Extraia os resultados do objeto de mapa retornado e salve o documento PDF correspondente. (Consulte &quot;Extrair os resultados&quot; em [Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar documentos do PDF com marcadores usando a API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Montar um documento PDF com marcadores usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente PDF Assembler.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Criar um `AssemblerServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Consulte um documento DDX existente.

   * Criar um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DDX.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Referencie um documento PDF ao qual os marcadores são adicionados.

   * Criar um `java.io.FileInputStream` usando seu construtor e transmitindo o local do documento PDF.
   * Criar um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto que contém o documento PDF.

1. Referencie o documento XML do marcador.

   * Criar um `java.io.FileInputStream` usando seu construtor e transmitindo o local do arquivo XML que representa o documento XML do marcador.
   * Criar um `com.adobe.idp.Document` e transmita o `java.io.FileInputStream` objeto que contém o documento PDF.

1. Adicione o documento PDF e o documento XML do marcador a uma coleção Map.

   * Criar um `java.util.Map` objeto usado para armazenar o documento PDF de entrada e o documento XML do marcador.
   * Adicione o documento do PDF de entrada chamando o `java.util.Map` do objeto `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX.
      * A `com.adobe.idp.Document` objeto que contém o documento PDF de entrada.

   * Adicione o documento XML do marcador chamando o `java.util.Map` do objeto `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem Marcadores especificado no documento DDX.
      * A `com.adobe.idp.Document` objeto que contém o documento XML do indicador.

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa, chamando um método que pertence à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler para continuar processando um job quando ocorrer um erro, chame o `AssemblerOptionSpec` do objeto `setFailOnError` e passar `false`.

1. Monte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado
   * A `java.util.Map` objeto que contém o documento PDF de entrada e o documento XML do marcador.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo fonte padrão e nível de log de job

   A variável `invokeDDX` o método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém os resultados do trabalho e quaisquer exceções que ocorreram.

1. Salve o documento PDF que contém marcadores.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método. Isso retorna um `java.util.Map` objeto.
   * Repita através do `java.util.Map` até encontrar o resultado `com.adobe.idp.Document` objeto. (Você pode usar o elemento de resultado PDF especificado no documento DDX para obter o documento.)
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para extrair o documento PDF.

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

1. Referencie um documento PDF ao qual os marcadores são adicionados.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` é usado para armazenar o PDF de entrada.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Referencie o documento XML do marcador.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento XML do marcador.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento de PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Adicione o documento PDF e o documento XML do marcador a uma coleção Map.

   * Criar um `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de coleção é usado para armazenar os documentos de PDF de entrada e o documento XML do marcador.
   * Para cada documento PDF de entrada e o documento XML do marcador, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua um valor de string que represente o nome da chave à `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` campo. Este valor deve corresponder ao valor do elemento de origem PDF especificado no documento DDX.
   * Atribua a `BLOB` objeto que armazena o documento PDF para o `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` campo.
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto para o `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` do objeto `Add` e transmita o `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Execute esta tarefa para cada documento de PDF de entrada e para o documento XML de marcador.)

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa atribuindo um valor a um membro de dados que pertença à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando um job quando ocorrer um erro, atribua `false` para o `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Monte o documento PDF.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX
   * A variável `MyMapOf_xsd_string_To_xsd_anyType` matriz que contém os documentos de entrada
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   A variável `invokeDDX` o método retorna um `AssemblerResult` objeto que contém os resultados do trabalho e quaisquer exceções que possam ter ocorrido.

1. Salve o documento PDF que contém marcadores.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` que é um `Map` objeto que contém os documentos PDF de resultado.
   * Repita através do `Map` até encontrar a chave que corresponde ao nome do documento resultante. Em seguida, converta o membro da matriz `value` para um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando seus `BLOB` do objeto `MTOM` campo. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
