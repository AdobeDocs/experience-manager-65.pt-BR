---
title: Montagem de documentos PDF com marcadores
seo-title: Montagem de documentos PDF com marcadores
description: Use o serviço Assembler para modificar um documento PDF que contém marcadores para incluir marcadores usando a API do Java e a API do serviço da Web.
seo-description: Use o serviço Assembler para modificar um documento PDF que contém marcadores para incluir marcadores usando a API do Java e a API do serviço da Web.
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2589'
ht-degree: 0%

---


# Montagem de documentos PDF com marcadores {#assembling-pdf-documents-with-bookmarks}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

Você pode montar um documento PDF que contenha marcadores. Por exemplo, suponha que você tem um documento PDF que não contém marcadores e deseja modificá-lo fornecendo marcadores. Usando o serviço Assembler, você pode transmitir a ele um documento PDF que não contém marcadores e obter um documento PDF que contém marcadores.

Os marcadores contêm as seguintes propriedades:

* Um título que aparece como texto na tela.
* Uma ação que especifica o que acontece quando um usuário clica no marcador. A ação típica de um marcador é mover para outro local no documento atual ou abrir outro documento PDF, embora outras ações possam ser especificadas.

Para a finalidade desta discussão, suponha que o seguinte documento DDX seja usado.

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

Nesse documento DDX, observe que o atributo de origem recebe o valor `Loan.pdf`. Este documento DDX especifica que um único documento PDF é passado para o serviço Assembler. Ao montar um documento PDF com marcadores, você deve especificar um documento XML de marcador que descreva os marcadores no documento de resultado. Para especificar um documento XML de marcador, verifique se o elemento `Bookmarks` está especificado no documento DDX.

Neste exemplo de documento DDX, o elemento `Bookmarks` especifica `doc2` como o valor. Esse valor indica que o mapa de entrada passado para o serviço Assembler contém uma chave chamada `doc2`. O valor da chave `doc2` é um valor `com.adobe.idp.Document` que representa o documento XML do marcador. (Consulte &quot;Linguagem de marcadores&quot; no [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).)

Este tópico usa a seguinte linguagem de marcadores XML para montar um documento PDF contendo marcadores.

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

Nesse documento XML de marcador, observe o elemento Ação que define a ação executada quando um usuário clica no marcador. No elemento Ação está o elemento do Launch que inicia aplicativos, como o NotePad e abre arquivos, como arquivos PDF. Para abrir um arquivo PDF, você deve usar o elemento File que especifica o arquivo a ser aberto. Por exemplo, no arquivo XML do marcador especificado nesta seção, o nome do arquivo aberto é LoanDetails.pdf.

>[!NOTE]
>
>Para obter detalhes completos sobre as ações compatíveis, consulte &quot; `Action` element&quot; no [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

Dado o documento DDX especificado nesta seção e o arquivo XML de marcador como entrada, o serviço Assembler monta um documento PDF que contém os seguintes marcadores.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Quando um usuário clica no marcador *Abrir os Detalhes do Empréstimo*, o LoanDetails.pdf é aberto. Da mesma forma, quando o usuário clica no marcador *Iniciar o NotePad*, o NotePad é iniciado.

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos PDF usando o serviço Assembler. Esta seção não discute conceitos, como criar um objeto de coleção que contenha documentos de entrada ou aprender a extrair os resultados do objeto de coleção retornado. (Consulte [Montagem programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de Serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar um documento PDF que contenha marcadores, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Assembler do PDF.
1. Faça referência a um documento DDX existente.
1. Referencie um documento PDF ao qual os marcadores são adicionados.
1. Faça referência ao documento XML do marcador.
1. Adicione o documento PDF e o documento XML de marcador a uma coleção de Mapa.
1. Defina as opções de tempo de execução.
1. Monte o documento PDF.
1. Salve o documento PDF que contém marcadores.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível diferente do JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para obter informações sobre a localização de todos os arquivos AEM Forms JAR, consulte [Incluindo arquivos da biblioteca AEM Forms Java](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um cliente do Assembler do PDF**

Antes de poder executar programaticamente uma operação Assembler, é necessário criar um cliente de serviço Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Este documento DDX deve conter o elemento `Bookmarks`, que instrui o serviço Assembler a montar um PDF que contenha marcadores. (Consulte o documento DDX mostrado anteriormente nesta seção para obter um exemplo.)

**Referência a um documento PDF ao qual os marcadores são adicionados**

Referencie um documento PDF ao qual os marcadores são adicionados. Não importa se o documento PDF referenciado já contém marcadores. Se o elemento `Bookmarks` for filho do elemento de origem do PDF, os Marcadores substituirão aqueles que já existem na origem do PDF. No entanto, se quiser manter os marcadores existentes, verifique se `Bookmarks` é um irmão do elemento de origem PDF. Por exemplo, considere o seguinte exemplo:

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Referência ao documento XML do marcador**

Para montar um PDF que contenha novos marcadores, você deve fazer referência a um documento XML de marcador. O documento XML do marcador é passado para o serviço Assembler no objeto de coleção Map. (Consulte o documento XML do marcador mostrado anteriormente nesta seção para obter um exemplo.)

>[!NOTE]
>
>Consulte &quot;Idioma dos Marcadores&quot; no [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Adicionar o documento PDF e o documento XML de marcador a uma coleção de Mapa**

Você deve adicionar o documento PDF ao qual os marcadores são adicionados e o documento XML do marcador à coleção de Mapa. Portanto, o objeto de coleção Map contém dois elementos: um documento PDF e o documento XML do marcador.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrua o serviço Assembler a continuar processando um trabalho se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte a referência da classe `AssemblerOptionSpec` em [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Monte o documento PDF**

Para montar um documento PDF que contém novos marcadores, use a operação `invokeDDX` do serviço Assembler. O motivo pelo qual você deve usar a operação `invokeDDX` em vez de outras operações do serviço Assembler, como `invokeOneDocument`, é porque o serviço Assembler requer um documento XML de marcador passado no objeto de coleção de Mapa. Este objeto é um parâmetro da operação `invokeDDX`.

**Salve o documento PDF que contém marcadores**

Você deve extrair os resultados do objeto de mapa retornado e salvar o documento PDF correspondente. (Consulte &quot;Extrair os resultados&quot; em [Montagem programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Consulte também:**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Monte documentos PDF com marcadores usando a API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Monte um documento PDF com marcadores usando a API do Serviço de Assembler (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente Assembler do PDF.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Faça referência a um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifique o local do arquivo DX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Referencie um documento PDF ao qual os marcadores são adicionados.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e passando o local do documento PDF.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e passe o objeto `java.io.FileInputStream` que contém o documento PDF.

1. Faça referência ao documento XML do marcador.

   * Crie um objeto `java.io.FileInputStream` usando seu construtor e transmitindo o local do arquivo XML que representa o documento XML do marcador.
   * Crie um objeto `com.adobe.idp.Document` e passe o objeto `java.io.FileInputStream` que contém o documento PDF.

1. Adicione o documento PDF e o documento XML de marcador a uma coleção de Mapa.

   * Crie um objeto `java.util.Map` usado para armazenar o documento PDF de entrada e o documento XML de marcador.
   * Adicione o documento PDF de entrada chamando o método `put` do objeto e passando os seguintes argumentos:`java.util.Map`

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX.
      * Um objeto `com.adobe.idp.Document` que contém o documento PDF de entrada.
   * Adicione o documento XML do marcador chamando o método `java.util.Map` do objeto `put` e passando os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem Marcadores especificado no documento DX.
      * Um objeto `com.adobe.idp.Document` que contém o documento XML do marcador.


1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor .
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios, chamando um método que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, chame o método `AssemblerOptionSpec` do objeto `setFailOnError` e passe `false`.

1. Monte o documento PDF.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX a ser usado
   * Um objeto `java.util.Map` que contém o documento PDF de entrada e o documento XML de marcador.
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do trabalho

   O método `invokeDDX` retorna um objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Salve o documento PDF que contém marcadores.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o método `AssemblerResult` do objeto `getDocuments`. Isso retorna um objeto `java.util.Map`.
   * Itere pelo objeto `java.util.Map` até encontrar o objeto `com.adobe.idp.Document` resultante. (Você pode usar o elemento de resultado PDF especificado no documento DX para obter o documento.)
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento PDF.

**Consulte também:**

[Início rápido (modo SOAP): Montagem de documentos PDF com marcadores usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Monte documentos PDF com marcadores usando a API de serviço da Web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Monte um documento PDF com marcadores usando a API do serviço Assembler (serviço da Web):

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
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Referencie um documento PDF ao qual os marcadores são adicionados.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o PDF de entrada.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e passando a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Faça referência ao documento XML do marcador.

   * Crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o documento XML do marcador.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read` e passando a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.

1. Adicione o documento PDF e o documento XML de marcador a uma coleção de Mapa.

   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType`. Esse objeto de coleção é usado para armazenar os documentos PDF de entrada e o documento XML de marcador.
   * Para cada documento PDF de entrada e o documento XML de marcador , crie um objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` .
   * Atribua um valor de string que represente o nome da chave ao campo `MyMapOf_xsd_string_To_xsd_anyType_Item` `key` do objeto. Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX.
   * Atribua o objeto `BLOB` que armazena o documento PDF ao campo `MyMapOf_xsd_string_To_xsd_anyType_Item` `value` do objeto.
   * Adicione o objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` ao objeto `MyMapOf_xsd_string_To_xsd_anyType`. Chame o método `MyMapOf_xsd_string_To_xsd_anyType` do objeto `Add` e passe o objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Execute esta tarefa para cada documento PDF de entrada e o documento XML de marcador.)

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor .
   * Defina as opções de tempo de execução para atender aos requisitos de negócios, atribuindo um valor a um membro de dados que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, atribua `false` ao membro de dados `AssemblerOptionSpec` do objeto `failOnError`.

1. Monte o documento PDF.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX
   * A matriz `MyMapOf_xsd_string_To_xsd_anyType` que contém os documentos de entrada
   * Um objeto `AssemblerOptionSpec` que especifica as opções de tempo de execução

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém os resultados da tarefa e quaisquer exceções que possam ter ocorrido.

1. Salve o documento PDF que contém marcadores.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Acesse o campo `AssemblerResult` do objeto `documents`, que é um objeto `Map` que contém os documentos PDF de resultado.
   * Itere pelo objeto `Map` até encontrar a chave que corresponde ao nome do documento resultante. Em seguida, converta esse membro da matriz `value` em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando o campo `BLOB` `MTOM` do objeto. Isso retorna uma matriz de bytes que podem ser gravados em um arquivo PDF.

**Consulte também:**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
