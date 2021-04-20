---
title: Montagem de Portfolio de PDF
seo-title: Montagem de Portfolio de PDF
description: Monte um portfólio de PDF para combinar vários documentos de vários tipos, incluindo arquivo de texto, arquivos de imagem e documentos PDF. Você pode reunir um portfólio em PDF usando uma API Java e uma API de serviço da Web.
seo-description: Monte um portfólio de PDF para combinar vários documentos de vários tipos, incluindo arquivo de texto, arquivos de imagem e documentos PDF. Você pode reunir um portfólio em PDF usando uma API Java e uma API de serviço da Web.
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1866'
ht-degree: 0%

---


# Montagem de Portfolio PDF {#assembling-pdf-portfolios}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

Você pode montar um Portfolio PDF usando o Java do Assembler e a API do serviço da Web. Um portfólio pode combinar vários documentos de vários tipos, incluindo arquivo de texto, arquivos de imagem (por exemplo, um arquivo jpeg) e documentos PDF. O layout do portfólio pode ser definido para estilos diferentes, como *Grade com Visualização*, *Em uma imagem* ou até *Revolver*.

A ilustração a seguir é uma captura de tela de um portfólio com *Em um layout de estilo Image*.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

A criação de um Portfolio em PDF é uma alternativa sem papel para transmitir uma coleção de documentos. Usando o AEM Forms, você pode criar portfólios chamando o serviço Assembler com um documento DDX estruturado. O seguinte documento DDX é um exemplo de um documento DDX que cria um Portfolio PDF.

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

O documento DXX deve conter uma tag `Portfolio` com uma tag `Navigator` aninhada. Observe que a tag `<Resource name="navigator/image.xxx" source="myImage.png"/>` só é necessária se `myNavigator` for atribuída como o navegador do layout onImage: `AdobeOnImage.nav`. Essa tag permite que o serviço Assembler selecione a imagem a ser usada como o plano de fundo do portfólio. Inclua `PackageFiles` e `File` tags para definir o nome do arquivo e o tipo MIME do arquivo empacotado.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de Serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para criar um Portfolio PDF, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um cliente Assembler do PDF.
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

Um documento DDX deve ser referenciado para montar um Portfolio PDF. Este documento DDX deve conter os elementos `Portfolio`, `Navigator` e `PackageFiles`.

**Fazer referência aos documentos necessários**

Para montar um Portfolio PDF, faça referência a todos os arquivos que representam os documentos a serem montados. Por exemplo, passe todos os arquivos de imagem especificados no documento DDX para o serviço Assembler. Observe que esses arquivos são referenciados no documento DDX especificado nesta seção: *myImage.png* e *saint_bernard.jpg*.

Ao montar um Portfolio PDF, passe um arquivo NAV (um arquivo de navegador) para o serviço Assembler. O arquivo NAV que você passa para o serviço Assembler depende do tipo de Portfolio de PDF a ser criado. Por exemplo, para criar um layout *Em uma imagem*, passe o arquivo AdobeOnImage.nav. Você pode localizar arquivos NAV na seguinte pasta:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copie o arquivo NAV do diretório de instalação do Acrobat 9 (ou posterior). Coloque o arquivo NAV em um local onde seu aplicativo cliente possa acessá-lo. Todos os arquivos são passados para o serviço Assembler em um objeto de coleção Map.

>[!NOTE]
>
>As inicializações rápidas associadas à Montagem de Portfolio de PDF usam o AdobeOnImage.nav.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrua o serviço Assembler a continuar processando um trabalho se um erro for encontrado.

**Monte o portfólio**

Para montar um Portfolio PDF, você chama a operação `invokeDDX`. O serviço Assembler retorna o Portfolio PDF em um objeto de coleção.

**Salve o portfólio montado**

Um Portfolio PDF é retornado em um objeto de coleção. Itere pelo objeto de coleção e salve o Portfolio em PDF como um arquivo PDF.

**Consulte também:**

[Monte um Portfolio PDF usando a API do Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Monte um Portfolio PDF usando a API do serviço da Web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Monte um Portfolio PDF usando a API Java {#assemble-a-pdf-portfolio-using-the-java-api}

Monte um Portfolio PDF usando a API do serviço Assembler (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente Assembler do PDF.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Faça referência a um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifique o local do arquivo DX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Faça referência aos documentos necessários.

   * Crie um objeto `java.util.Map` que é usado para armazenar documentos PDF de entrada usando um construtor `HashMap`.
   * Crie um objeto `java.io.FileInputStream` usando seu construtor. Passe o local do arquivo NAV necessário (repita essa tarefa para cada arquivo necessário para criar um portfólio).
   * Crie um objeto `com.adobe.idp.Document` e passe o objeto `java.io.FileInputStream` que contém o arquivo NAV (repita essa tarefa para cada arquivo necessário para criar um portfólio).
   * Adicione uma entrada ao objeto `java.util.Map` chamando seu método `put` e passando os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem especificado no documento DX. (repita essa tarefa para cada arquivo necessário para criar um portfólio).
      * Um objeto `com.adobe.idp.Document` que contém o documento PDF. (repita essa tarefa para cada arquivo necessário para criar um portfólio).

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor .
   * Defina as opções de tempo de execução para atender aos seus requisitos de negócios, chamando um método que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, chame o método `AssemblerOptionSpec` do objeto `setFailOnError` e passe `false`.

1. Monte o portfólio.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX a ser usado
   * Um objeto `java.util.Map` que contém os arquivos necessários para criar um Portfolio PDF.
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível do log de tarefas

   O método `invokeDDX` retorna um objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contém o Portfolio PDF montado e qualquer exceção que ocorreu.

1. Salve o portfólio montado.

   Para obter o Portfolio PDF, execute as seguintes ações:

   * Chame o método `AssemblerResult` do objeto `getDocuments`. Este método retorna um objeto `java.util.Map`.
   * Itere pelo objeto `java.util.Map` até encontrar o objeto `com.adobe.idp.Document` resultante.
   * Chame o método `com.adobe.idp.Document` do objeto `copyToFile` para extrair o Portfolio PDF.

**Consulte também:**

[Início rápido (modo SOAP): Montagem de Portfolio de PDF usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Monte um Portfolio PDF usando a API do serviço da Web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Monte um Portfolio PDF usando a API do serviço Assembler (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao definir uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` ao conteúdo da matriz de bytes.

1. Faça referência aos documentos necessários.

   * Para cada arquivo de entrada, crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o arquivo de entrada.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `System.IO.FileStream` do objeto `Length`.
   * Preencha a matriz de bytes com dados de fluxo chamando o método `System.IO.FileStream` do objeto `Read`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` ao conteúdo da matriz de bytes.
   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType`. Esse objeto de coleção é usado para armazenar arquivos de entrada necessários para criar um Portfolio PDF.
   * Para cada arquivo de entrada, crie um objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` .
   * Atribua um valor de string que represente o nome da chave ao campo `MyMapOf_xsd_string_To_xsd_anyType_Item` `key` do objeto. Esse valor deve corresponder ao valor do elemento especificado no documento DDX. (Execute esta tarefa para cada arquivo de entrada.)
   * Atribua o objeto `BLOB` que armazena o arquivo de entrada ao campo `MyMapOf_xsd_string_To_xsd_anyType_Item` `value` do objeto. (Execute essa tarefa para cada documento PDF de entrada.)
   * Adicione o objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` ao objeto `MyMapOf_xsd_string_To_xsd_anyType`. Chame o método `MyMapOf_xsd_string_To_xsd_anyType` do objeto `Add` e passe o objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Execute essa tarefa para cada documento PDF de entrada.)

1. Defina as opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor .
   * Defina as opções de tempo de execução para atender aos requisitos de negócios, atribuindo um valor a um membro de dados que pertence ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar o processamento de uma tarefa quando ocorrer um erro, atribua `false` ao membro de dados `AssemblerOptionSpec` do objeto `failOnError`.

1. Monte o portfólio.

   Chame o método `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX
   * O objeto `MyMapOf_xsd_string_To_xsd_anyType` que contém os arquivos necessários
   * Um objeto `AssemblerOptionSpec` que especifica as opções de tempo de execução

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Salve o portfólio montado.

   Para obter o Portfolio PDF recém-criado, execute as seguintes ações:

   * Acesse o campo `AssemblerResult` do objeto `documents`, que é um objeto `Map` que contém os documentos PDF resultantes.
   * Itere pelo objeto `Map` para obter cada documento resultante. Em seguida, converta o membro da matriz `value` em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade `BLOB` do objeto `MTOM`. Isso retorna uma matriz de bytes que podem ser gravados em um arquivo PDF.

**Consulte também:**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
