---
title: Montagem de Portfolio PDF
description: Monte um portfólio PDF para combinar vários documentos de vários tipos, incluindo arquivos de texto, arquivos de imagem e documentos PDF. Você pode montar um portfólio PDF usando uma API Java e uma API de serviço da Web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 0%

---

# Montagem de Portfolio PDF {#assembling-pdf-portfolios}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

Você pode montar um Portfolio PDF usando o Java do Assembler e a API de serviço Web. Um portfólio pode combinar vários documentos de vários tipos, incluindo arquivos de texto, arquivos de imagem (por exemplo, um arquivo jpeg) e documentos PDF. O layout do portfólio pode ser definido com diferentes estilos, como a *Grade com Visualização*, o *Layout de uma Imagem* ou até mesmo *Revolução*.

A ilustração a seguir é uma captura de tela de um portfólio com o layout de estilo *Em uma Imagem*.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

Criar um Portfolio PDF serve como uma alternativa sem papel para transmitir uma coleção de documentos. Com o AEM Forms, você pode criar portfólios chamando o serviço Assembler com um documento DDX estruturado. O documento DDX a seguir é um exemplo de um documento DDX que cria um Portfolio PDF.

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

O documento DXX deve conter uma marca `Portfolio` com uma marca `Navigator` aninhada. Observe que a marca `<Resource name="navigator/image.xxx" source="myImage.png"/>` só será necessária se `myNavigator` for atribuída como o navegador de layout onImage: `AdobeOnImage.nav`. Essa tag permite que o serviço Assembler selecione a imagem a ser usada como plano de fundo do portfólio. Inclua as marcas `PackageFiles` e `File` para definir o nome de arquivo e o tipo MIME do arquivo empacotado.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço do Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para criar um Portfolio PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente PDF Assembler.
1. Consulte um documento DDX existente.
1. Consulte os documentos necessários.
1. Definir opções de tempo de execução.
1. Montar o portfólio.
1. Salve o portfólio montado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

**Criar um cliente PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, crie um cliente de serviço do Assembler.

**Referenciar um documento DDX existente**

Um documento DDX deve ser referenciado para montar um Portfolio PDF. Este documento DDX deve conter os elementos `Portfolio`, `Navigator` e `PackageFiles`.

**Referenciar os documentos necessários**

Para montar um Portfolio de PDF, faça referência a todos os arquivos que representam os documentos a serem montados. Por exemplo, transmita todos os arquivos de imagem especificados no documento DDX para o serviço do Assembler. Observe que esses arquivos são mencionados no documento DDX especificado nesta seção: *myImage.png* e *saint_bernard.jpg*.

Ao montar um Portfolio PDF, passe um arquivo NAV (um arquivo de navegador) para o serviço Assembler. O arquivo NAV que você passa para o serviço Assembler depende do tipo de Portfolio PDF a ser criado. Por exemplo, para criar um layout *Em uma Imagem*, passe o arquivo AdobeOnImage.nav. Você pode localizar arquivos NAV na seguinte pasta:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copie o arquivo NAV do diretório de instalação do Acrobat 9 (ou posterior). Coloque o arquivo NAV em um local onde seu aplicativo cliente possa acessá-lo. Todos os arquivos são passados para o serviço Assembler dentro de um objeto de coleção Map.

>[!NOTE]
>
>Os inícios rápidos associados à Montagem de Portfolio PDF usam o AdobeOnImage.nav.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado.

**Montar o portfólio**

Para montar um Portfolio PDF, você chama a operação `invokeDDX`. O serviço Assembler retorna o Portfolio PDF dentro de um objeto de coleção.

**Salvar o portfólio montado**

Um Portfolio PDF é retornado em um objeto de coleção. Repita o processo através do objeto de coleção e salve o Portfolio PDF como um arquivo PDF.

**Consulte também**

[Montar um Portfolio PDF usando a API Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Montar um Portfolio de PDF usando a API de serviço Web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de documentos do PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montar um Portfolio PDF usando a API Java {#assemble-a-pdf-portfolio-using-the-java-api}

Montar um Portfolio de PDF usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do projeto Java.

1. Crie um cliente PDF Assembler.

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `AssemblerServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Consulte um documento DDX existente.

   * Crie um objeto `java.io.FileInputStream` que represente o documento DDX usando seu construtor e transmitindo um valor de cadeia de caracteres que especifique o local do arquivo DDX.
   * Crie um objeto `com.adobe.idp.Document` usando seu construtor e transmitindo o objeto `java.io.FileInputStream`.

1. Consulte os documentos necessários.

   * Crie um objeto `java.util.Map` usado para armazenar documentos de PDF de entrada usando um construtor `HashMap`.
   * Crie um objeto `java.io.FileInputStream` usando seu construtor. Transmita o local do arquivo NAV necessário (repita essa tarefa para cada arquivo necessário para criar um portfólio).
   * Crie um objeto `com.adobe.idp.Document` e passe o objeto `java.io.FileInputStream` que contém o arquivo NAV (repita essa tarefa para cada arquivo necessário para criar um portfólio).
   * Adicione uma entrada ao objeto `java.util.Map` invocando seu método `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem especificado no documento DDX. (repita essa tarefa para cada arquivo necessário para criar um portfólio).
      * Um objeto `com.adobe.idp.Document` que contém o documento PDF. (repita essa tarefa para cada arquivo necessário para criar um portfólio).

1. Definir opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos da sua empresa invocando um método que pertença ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, chame o método `setFailOnError` do objeto `AssemblerOptionSpec` e passe `false`.

1. Montar o portfólio.

   Chame o método `invokeDDX` do objeto `AssemblerServiceClient` e passe os seguintes valores obrigatórios:

   * Um objeto `com.adobe.idp.Document` que representa o documento DDX a ser usado
   * Um objeto `java.util.Map` que contém os arquivos necessários para compilar um Portfolio de PDF.
   * Um objeto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do trabalho

   O método `invokeDDX` retorna um objeto `com.adobe.livecycle.assembler.client.AssemblerResult` que contém o Portfolio de PDF montado e quaisquer exceções que ocorreram.

1. Salve o portfólio montado.

   Para obter o Portfolio PDF, execute as seguintes ações:

   * Invoque o método `getDocuments` do objeto `AssemblerResult`. Este método retorna um objeto `java.util.Map`.
   * Repita o objeto `java.util.Map` até encontrar o objeto `com.adobe.idp.Document` resultante.
   * Invoque o método `copyToFile` do objeto `com.adobe.idp.Document` para extrair o Portfolio PDF.

**Consulte também**

[Início rápido (modo SOAP): montagem de Portfolio de PDF usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar um Portfolio de PDF usando a API de serviço Web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Montar um Portfolio de PDF usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao definir uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo sua propriedade `MTOM` com o conteúdo da matriz de bytes.

1. Consulte os documentos necessários.

   * Para cada arquivo de entrada, crie um objeto `BLOB` usando seu construtor. O objeto `BLOB` é usado para armazenar o arquivo de entrada.
   * Crie um objeto `System.IO.FileStream` chamando seu construtor e transmitindo um valor de cadeia de caracteres que representa o local do arquivo de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do objeto `System.IO.FileStream`. Você pode determinar o tamanho da matriz de bytes obtendo a propriedade `Length` do objeto `System.IO.FileStream`.
   * Preencha a matriz de bytes com dados de fluxo invocando o método `Read` do objeto `System.IO.FileStream`. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o objeto `BLOB` atribuindo seu campo `MTOM` com o conteúdo da matriz de bytes.
   * Crie um objeto `MyMapOf_xsd_string_To_xsd_anyType`. Este objeto de coleção é usado para armazenar arquivos de entrada necessários para criar um Portfolio de PDF.
   * Para cada arquivo de entrada, crie um objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Atribua um valor de cadeia de caracteres que represente o nome da chave para o campo `key` do objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Este valor deve corresponder ao valor do elemento especificado no documento DDX. (Execute esta tarefa para cada arquivo de entrada.)
   * Atribua o objeto `BLOB` que armazena o arquivo de entrada ao campo `value` do objeto `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Execute esta tarefa para cada documento de PDF de entrada.)
   * Adicione o objeto `MyMapOf_xsd_string_To_xsd_anyType_Item` ao objeto `MyMapOf_xsd_string_To_xsd_anyType`. Invoque o método `Add` do objeto `MyMapOf_xsd_string_To_xsd_anyType` e passe o objeto `MyMapOf_xsd_string_To_xsd_anyType`. (Execute esta tarefa para cada documento de PDF de entrada.)

1. Definir opções de tempo de execução.

   * Crie um objeto `AssemblerOptionSpec` que armazene opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos comerciais atribuindo um valor a um membro de dados que pertença ao objeto `AssemblerOptionSpec`. Por exemplo, para instruir o serviço Assembler a continuar processando um trabalho quando ocorrer um erro, atribua `false` ao membro de dados `failOnError` do objeto `AssemblerOptionSpec`.

1. Montar o portfólio.

   Chame o método `invokeDDX` do objeto `AssemblerServiceClient` e passe os seguintes valores:

   * Um objeto `BLOB` que representa o documento DDX
   * O objeto `MyMapOf_xsd_string_To_xsd_anyType` que contém os arquivos necessários
   * Um objeto `AssemblerOptionSpec` que especifica as opções de tempo de execução

   O método `invokeDDX` retorna um objeto `AssemblerResult` que contém os resultados do trabalho e as exceções que ocorreram.

1. Salve o portfólio montado.

   Para obter o Portfolio PDF recém-criado, execute as seguintes ações:

   * Acesse o campo `documents` do objeto `AssemblerResult`, que é um objeto `Map` que contém os documentos PDF resultantes.
   * Repita através do objeto `Map` para obter cada documento resultante. Em seguida, converta o `value` desse membro da matriz em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade `MTOM` do objeto `BLOB`. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
