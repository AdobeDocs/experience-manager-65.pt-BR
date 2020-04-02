---
title: Montagem de Documentos PDF com marcadores
seo-title: Montagem de Documentos PDF com marcadores
description: 'null'
seo-description: 'null'
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
translation-type: tm+mt
source-git-commit: e3f700b52446505224fa4b4688d439750a66f471

---


# Montagem de Documentos PDF com marcadores {#assembling-pdf-documents-with-bookmarks}

É possível montar um documento PDF que contenha marcadores. Por exemplo, suponha que você tenha um documento PDF que não contenha marcadores e queira modificá-lo fornecendo marcadores. Usando o serviço Assembler, você pode enviar a ele um documento PDF que não contém marcadores e recuperar um documento PDF que contém marcadores.

Os marcadores contêm as seguintes propriedades:

* Um título que aparece como texto na tela.
* Uma ação que especifica o que acontece quando um usuário clica no marcador. A ação típica de um marcador é mover-se para outro local no documento atual ou abrir outro documento PDF, embora outras ações possam ser especificadas.

Para a finalidade desta discussão, suponha que o seguinte documento DX seja usado.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

Nesse documento DDX, observe que o valor é atribuído ao atributo de origem `Loan.pdf`. Esse documento DDX especifica que um único documento PDF é passado para o serviço Assembler. Ao montar um documento PDF com marcadores, você deve especificar um documento XML de marcador que descreve os marcadores no documento resultante. Para especificar um documento XML de marcador, verifique se o `Bookmarks` elemento está especificado no documento DX.

Neste exemplo de documento DDX, o `Bookmarks` elemento especifica `doc2` como o valor. Esse valor indica que o mapa de entrada passado para o serviço Assembler contém uma chave chamada `doc2`. O valor da `doc2` chave é um `com.adobe.idp.Document` valor que representa o documento XML de marcador. (Consulte &quot;Linguagem de Marcadores&quot; no Serviço de [Montagem e Referência](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.)

Este tópico usa o seguinte idioma de marcadores XML para montar um documento PDF contendo marcadores.

```as3
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

Nesse documento XML de marcador, observe o elemento Action que define a ação executada quando um usuário clica no marcador. Sob o elemento Ação está o elemento Iniciar que inicia aplicativos, como o NotePad e abre arquivos, como arquivos PDF. Para abrir um arquivo PDF, é necessário usar o elemento Arquivo que especifica o arquivo a ser aberto. Por exemplo, no arquivo XML de marcador especificado nesta seção, o nome do arquivo aberto é LoanDetails.pdf.

>[!NOTE]
>
>Para obter detalhes completos sobre ações compatíveis, consulte &quot; `Action` element&quot; no Serviço [do Assembler e na Referência](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

Dado o documento DDX especificado nesta seção e o arquivo XML de marcador como entrada, o serviço Assembler monta um documento PDF que contém os seguintes marcadores.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Quando um usuário clica em *Abrir o marcador Detalhes* do empréstimo, o LoanDetails.pdf é aberto. Da mesma forma, quando o usuário clica no marcador *Iniciar o NotePad* , o NotePad é iniciado.

>[!NOTE]
>
>Antes de ler esta seção, é recomendável que você esteja familiarizado com a montagem de documentos PDF usando o serviço Assembler. Esta seção não discute conceitos, como criar um objeto de coleção que contenha documentos de entrada ou aprender a extrair os resultados do objeto de coleção retornado. (Consulte Montagem [Programática De Documentos](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)PDF.)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte Referência de [serviços para formulários](https://www.adobe.com/go/learn_aemforms_services_63)AEM.

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para montar um documento PDF que contenha marcadores, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente do Montador de PDF.
1. Faça referência a um documento DDX existente.
1. Faça referência a um documento PDF ao qual os marcadores são adicionados.
1. Faça referência ao documento XML do marcador.
1. Adicione o documento PDF e o documento XML de marcador a uma coleção de mapa.
1. Defina as opções de tempo de execução.
1. Monte o documento PDF.
1. Salve o documento PDF que contém marcadores.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado em JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado em JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, você deverá substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms está implantado. Para obter informações sobre a localização de todos os arquivos JAR do AEM Forms, consulte [Inclusão de arquivos](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)da biblioteca Java do AEM Forms.

**Criar um cliente de Montador de PDF**

Antes de poder executar programaticamente uma operação do Assembler, você deve criar um cliente de serviço do Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para montar um documento PDF. Esse documento DDX deve conter o `Bookmarks` elemento, que instrui o serviço Assembler a montar um PDF que contenha marcadores. (Consulte o documento DDX mostrado anteriormente nesta seção para ver um exemplo.)

**Referência a um documento PDF ao qual os marcadores são adicionados**

Faça referência a um documento PDF ao qual os marcadores são adicionados. Não importa se o documento PDF referenciado já contém marcadores. Se o `Bookmarks` elemento for filho do elemento de origem do PDF, os Marcadores substituirão os que já existem na fonte do PDF. No entanto, se desejar manter os marcadores existentes, verifique se `Bookmarks` é um irmão do elemento de origem do PDF. Por exemplo, considere o seguinte exemplo:

```as3
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Referência ao documento XML de marcador**

Para montar um PDF que contenha novos marcadores, é necessário referenciar um documento XML de marcador. O documento XML de marcador é transmitido ao serviço Assembler dentro do objeto de coleção Map. (Consulte o documento XML de marcador mostrado anteriormente nesta seção para ver um exemplo.)

>[!NOTE]
>
>Consulte &quot;Linguagem de Marcadores&quot; no Serviço de [Montagem e Referência](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

**Adicionar o documento PDF e o documento XML de marcador a uma coleção de mapas**

É necessário adicionar o documento PDF ao qual os marcadores são adicionados e o documento XML de marcador à coleção de mapa. Portanto, o objeto de coleção Map contém dois elementos: um documento PDF e o documento XML de marcador.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando uma tarefa se um erro for encontrado. Para obter informações sobre as opções de tempo de execução que podem ser definidas, consulte a referência de `AssemblerOptionSpec` classe em Referência [de API do](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Montagem do documento PDF**

Para montar um documento PDF que contenha novos marcadores, use a operação do serviço `invokeDDX` Assembler. O motivo pelo qual você deve usar a `invokeDDX` operação em vez de outras operações de serviço do Assembler, como `invokeOneDocument` o é porque o serviço do Assembler requer um documento XML de marcador passado dentro do objeto de coleção do Mapa. Este objeto é um parâmetro da `invokeDDX` operação.

**Salve o documento PDF que contém marcadores**

Você deve extrair os resultados do objeto de mapa retornado e salvar o documento PDF correspondente. (Consulte &quot;Extrair os resultados&quot; em Montagem [programática de Documentos](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF.)

**Consulte também:**

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montagem de documentos PDF com marcadores usando a API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Monte um documento PDF com marcadores usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente do Montador de PDF.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão. (Consulte [Configuração das propriedades](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)de conexão.)
   * Crie um `AssemblerServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DX.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Faça referência a um documento PDF ao qual os marcadores são adicionados.

   * Crie um `java.io.FileInputStream` objeto usando seu construtor e transmitindo o local do documento PDF.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e passe o `java.io.FileInputStream` objeto que contém o documento PDF.

1. Faça referência ao documento XML do marcador.

   * Crie um `java.io.FileInputStream` objeto usando seu construtor e transmitindo o local do arquivo XML que representa o documento XML de marcador.
   * Crie um `com.adobe.idp.Document` objeto e passe o `java.io.FileInputStream` objeto que contém o documento PDF.

1. Adicione o documento PDF e o documento XML de marcador a uma coleção de mapa.

   * Crie um `java.util.Map` objeto que seja usado para armazenar o documento PDF de entrada e o documento XML de marcador.
   * Adicione o documento PDF de entrada chamando o método do `java.util.Map` objeto `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX.
      * Um `com.adobe.idp.Document` objeto que contém o documento PDF de entrada.
   * Adicione o documento XML de marcador invocando o `java.util.Map` método do objeto `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem Marcadores especificado no documento DDX.
      * Um `com.adobe.idp.Document` objeto que contém o documento XML de marcador.


1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, chame o `AssemblerOptionSpec` método do `setFailOnError` objeto e passe `false`.

1. Monte o documento PDF.

   Chame o `AssemblerServiceClient` método do `invokeDDX` objeto e passe os seguintes valores obrigatórios:

   * Um `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado
   * Um `java.util.Map` objeto que contém o documento PDF de entrada e o documento XML de marcador.
   * Um `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log de trabalhos
   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Salve o documento PDF que contém marcadores.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Chame o `AssemblerResult` método do `getDocuments` objeto. Isso retorna um `java.util.Map` objeto.
   * Iterar pelo `java.util.Map` objeto até encontrar o `com.adobe.idp.Document` objeto resultante. (Você pode usar o elemento de resultado PDF especificado no documento DX para obter o documento.)
   * Chame o `com.adobe.idp.Document` `copyToFile` método do objeto para extrair o documento PDF.

**Consulte também:**

[Start rápido (modo SOAP): Montagem de documentos PDF com marcadores usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montagem de documentos PDF com marcadores usando a API de serviço da Web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Monte um documento PDF com marcadores usando a API de serviço do Assembler (serviço da Web):

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

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento DDX.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DX e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Faça referência a um documento PDF ao qual os marcadores são adicionados.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o PDF de entrada.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Faça referência ao documento XML do marcador.

   * Crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o documento XML de marcador.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF de entrada e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` `Read` objeto e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.

1. Adicione o documento PDF e o documento XML de marcador a uma coleção de mapa.

   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Esse objeto de coleção é usado para armazenar os documentos PDF de entrada e o documento XML de marcador.
   * Para cada documento PDF de entrada e o documento XML de marcador, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua um valor de string que representa o nome da chave ao campo do `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto `key` . Esse valor deve corresponder ao valor do elemento de origem do PDF especificado no documento DX.
   * Atribua o `BLOB` objeto que armazena o documento PDF ao `MyMapOf_xsd_string_To_xsd_anyType_Item` campo do `value` objeto.
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto ao `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` método do objeto `Add` e passe o `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Execute essa tarefa para cada documento PDF de entrada e o documento XML de marcador.)

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios, atribuindo um valor a um membro de dados que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, atribua `false` ao membro de `AssemblerOptionSpec` dados do objeto `failOnError` .

1. Monte o documento PDF.

   Chame o método do `AssemblerServiceClient` objeto `invokeDDX` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o documento DDX
   * A `MyMapOf_xsd_string_To_xsd_anyType` matriz que contém os documentos de entrada
   * Um `AssemblerOptionSpec` objeto que especifica opções de tempo de execução
   O `invokeDDX` método retorna um `AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que possam ter ocorrido.

1. Salve o documento PDF que contém marcadores.

   Para obter o documento PDF recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` campo do `documents` objeto, que é um `Map` objeto que contém os documentos PDF de resultado.
   * Itere pelo `Map` objeto até encontrar a chave que corresponde ao nome do documento resultante. Em seguida, converta o membro do storage `value` em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando o campo do `BLOB` objeto `MTOM` . Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também:**

[Invocar formulários AEM usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
