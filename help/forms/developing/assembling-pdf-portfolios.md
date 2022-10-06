---
title: Montagem de Portfolio PDF
seo-title: Assembling PDF Portfolios
description: Monte um portfólio do PDF para combinar vários documentos de vários tipos, incluindo arquivo de texto, arquivos de imagem e documentos do PDF. Você pode montar um portfólio do PDF usando uma API Java e uma API do serviço da Web.
seo-description: Assemble a PDF portfolio to combine several documents of various types, including word file, image files, and PDF documents. You can assemble a PDF portfolio using a Java API and a Web Service API.
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 0%

---

# Montagem de Portfolio PDF {#assembling-pdf-portfolios}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

Você pode montar um Portfolio de PDF usando o Java do Assembler e a API do serviço da Web. Um portfólio pode combinar vários documentos de vários tipos, incluindo arquivo de texto, arquivos de imagem (por exemplo, um arquivo jpeg) e documentos PDF. O layout do portfólio pode ser definido para estilos diferentes como o *Grade com Visualização*, o *Em uma imagem* layout ou par *Revolve*.

A ilustração a seguir é uma captura de tela de um portfólio com *Em uma imagem* layout de estilo.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

A criação de um PDF Portfolio serve como uma alternativa sem papel para passar uma coleção de documentos. Usando o AEM Forms, você pode criar portfólios chamando o serviço Assembler com um documento DDX estruturado. O documento DDX a seguir é um exemplo de um documento DDX que cria um PDF Portfolio.

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

O documento DXX deve conter um `Portfolio` com uma tag aninhada `Navigator` . Observe a tag `<Resource name="navigator/image.xxx" source="myImage.png"/>` só é necessário se `myNavigator` é atribuído como navegador de layout onImage: `AdobeOnImage.nav`. Essa tag permite que o serviço Assembler selecione a imagem a ser usada como o plano de fundo do portfólio. Incluir `PackageFiles` e `File` tags para definir o nome do arquivo e o tipo MIME do arquivo empacotado.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para criar um PDF, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Assembler PDF.
1. Faça referência a um documento DDX existente.
1. Faça referência aos documentos necessários.
1. Defina as opções de tempo de execução.
1. Monte o portfólio.
1. Salve o portfólio montado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

**Criar um cliente do Assembler do PDF**

Antes de executar programaticamente uma operação Assembler, crie um cliente de serviço Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para montar um PDF. Este documento DDX deve conter a variável `Portfolio`, `Navigator` e `PackageFiles` elementos.

**Fazer referência aos documentos necessários**

Para montar um Portfolio PDF, faça referência a todos os arquivos que representam os documentos a serem montados. Por exemplo, passe todos os arquivos de imagem especificados no documento DDX para o serviço Assembler. Observe que esses arquivos são referenciados no documento DDX especificado nesta seção: *myImage.png* e *saint_bernard.jpg*.

Ao montar um Portfolio PDF, passe um arquivo NAV (um arquivo de navegador) para o serviço Assembler. O arquivo NAV que você passa para o serviço Assembler depende de que tipo de Portfolio de PDF deve ser criado. Por exemplo, para criar um *Em uma imagem* passe o arquivo AdobeOnImage.nav no layout. Você pode localizar arquivos NAV na seguinte pasta:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copie o arquivo NAV do diretório de instalação do Acrobat 9 (ou posterior). Coloque o arquivo NAV em um local onde seu aplicativo cliente possa acessá-lo. Todos os arquivos são passados para o serviço Assembler em um objeto de coleção Map.

>[!NOTE]
>
>As inicializações rápidas associadas à Montagem de Portfolio de PDF usam o AdobeOnImage.nav.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrua o serviço Assembler a continuar processando um trabalho se um erro for encontrado.

**Monte o portfólio**

Para montar um Portfolio de PDF, você chama o `invokeDDX` operação. O serviço Assembler retorna o PDF Portfolio dentro de um objeto de coleção.

**Salve o portfólio montado**

Um Portfolio PDF é retornado em um objeto de coleção. Itere pelo objeto de coleção e salve PDF Portfolio como um arquivo PDF.

**Consulte também**

[Monte um PDF usando a API do Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Monte um PDF usando a API do serviço da Web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Monte um PDF usando a API do Java {#assemble-a-pdf-portfolio-using-the-java-api}

Monte um PDF usando a API do Assembler Service (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente Assembler PDF.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `AssemblerServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e passando um valor de string que especifica o local do arquivo DX.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Faça referência aos documentos necessários.

   * Crie um `java.util.Map` objeto usado para armazenar documentos PDF de entrada usando um `HashMap` construtor.
   * Crie um `java.io.FileInputStream` usando seu construtor. Passe o local do arquivo NAV necessário (repita essa tarefa para cada arquivo necessário para criar um portfólio).
   * Crie um `com.adobe.idp.Document` e transmita o `java.io.FileInputStream` objeto que contém o arquivo NAV (repita essa tarefa para cada arquivo necessário para criar um portfólio).
   * Adicione uma entrada à `java.util.Map` ao invocar seu `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem especificado no documento DX. (repita essa tarefa para cada arquivo necessário para criar um portfólio).
      * A `com.adobe.idp.Document` objeto que contém o documento PDF. (repita essa tarefa para cada arquivo necessário para criar um portfólio).

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios, chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, chame a função `AssemblerOptionSpec` do objeto `setFailOnError` método e pass `false`.

1. Monte o portfólio.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado
   * A `java.util.Map` objeto que contém os arquivos necessários para criar um Portfolio PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível do log de tarefas

   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém o PDF montado e qualquer exceção que ocorreu.

1. Salve o portfólio montado.

   Para obter o PDF, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método . Esse método retorna um `java.util.Map` objeto.
   * Iterar por meio do `java.util.Map` até encontrar o resultante `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para extrair o Portfolio PDF.

**Consulte também**

[Início rápido (modo SOAP): Montagem de Portfolio PDF usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Monte um PDF usando a API do serviço da Web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Monte um PDF usando a API do Assembler Service (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao definir uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Faça referência aos documentos necessários.

   * Para cada arquivo de entrada, crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o arquivo de entrada.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo de entrada e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` método . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.
   * Crie um `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de coleção é usado para armazenar arquivos de entrada necessários para criar um Portfolio PDF.
   * Para cada arquivo de entrada, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua um valor de string que represente o nome da chave à variável `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` campo. Esse valor deve corresponder ao valor do elemento especificado no documento DDX. (Execute esta tarefa para cada arquivo de entrada.)
   * Atribua o `BLOB` que armazena o arquivo de entrada no `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` campo. (Execute esta tarefa para cada documento PDF de entrada.)
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` para `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` do objeto `Add` e passe o `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Execute esta tarefa para cada documento PDF de entrada.)

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` que armazena opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos da empresa, atribuindo um valor a um membro de dados pertencente à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, atribua `false` para `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Monte o portfólio.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e transmita os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX
   * O `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém os arquivos necessários
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   O `invokeDDX` retorna um método `AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Salve o portfólio montado.

   Para obter o PDF recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` , que é um `Map` objeto que contém os documentos PDF resultantes.
   * Iterar por meio do `Map` para obter cada documento resultante. Em seguida, converta esse membro da matriz `value` para `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando seu `BLOB` do objeto `MTOM` propriedade. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
