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
feature: Adaptive Forms,  Document Services
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 0%

---

# Montagem de Portfolio PDF {#assembling-pdf-portfolios}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

Você pode montar um Portfolio PDF usando o Java do Assembler e a API de serviço Web. Um portfólio pode combinar vários documentos de vários tipos, incluindo arquivos de texto, arquivos de imagem (por exemplo, um arquivo jpeg) e documentos PDF. O layout do portfólio pode ser definido com diferentes estilos, como o *Grade com Visualização*, o *Em uma imagem* layout ou par *Revolução*.

A ilustração a seguir é uma captura de tela de um portfólio com *Em uma imagem* layout de estilo.

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

O documento DXX deve conter uma `Portfolio` com uma tag aninhada `Navigator` tag. Anote a tag `<Resource name="navigator/image.xxx" source="myImage.png"/>` só é necessário se `myNavigator` é atribuído como o navegador de layout onImage: `AdobeOnImage.nav`. Essa tag permite que o serviço Assembler selecione a imagem a ser usada como plano de fundo do portfólio. Incluir `PackageFiles` e `File` para definir o nome do arquivo e o tipo MIME do arquivo empacotado.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Serviço de Assembler e Referência DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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

**Criar um cliente do PDF Assembler**

Antes de executar programaticamente uma operação do Assembler, crie um cliente de serviço do Assembler.

**Referencie um documento DDX existente**

Um documento DDX deve ser referenciado para montar um Portfolio PDF. Este documento DDX deve conter a `Portfolio`, `Navigator` e, `PackageFiles` elementos.

**Referenciar os documentos necessários**

Para montar um Portfolio de PDF, faça referência a todos os arquivos que representam os documentos a serem montados. Por exemplo, transmita todos os arquivos de imagem especificados no documento DDX para o serviço do Assembler. Observe que esses arquivos são referenciados no documento DDX especificado nesta seção: *myImage.png* e *saint_bernard.jpg*.

Ao montar um Portfolio PDF, passe um arquivo NAV (um arquivo de navegador) para o serviço Assembler. O arquivo NAV que você passa para o serviço Assembler depende do tipo de Portfolio PDF a ser criado. Por exemplo, para criar um *Em uma imagem* , passe o arquivo AdobeOnImage.nav. Você pode localizar arquivos NAV na seguinte pasta:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copie o arquivo NAV do diretório de instalação do Acrobat 9 (ou posterior). Coloque o arquivo NAV em um local onde seu aplicativo cliente possa acessá-lo. Todos os arquivos são passados para o serviço Assembler dentro de um objeto de coleção Map.

>[!NOTE]
>
>Os inícios rápidos associados à Montagem de Portfolio PDF usam o AdobeOnImage.nav.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa um job. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando um job se um erro for encontrado.

**Montar o portfólio**

Para montar um Portfolio PDF, você chama o `invokeDDX` operação. O serviço Assembler retorna o Portfolio PDF dentro de um objeto de coleção.

**Salve o portfólio montado**

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

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `AssemblerServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Consulte um documento DDX existente.

   * Criar um `java.io.FileInputStream` objeto que representa o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DDX.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Consulte os documentos necessários.

   * Criar um `java.util.Map` objeto usado para armazenar documentos de PDF de entrada usando um `HashMap` construtor.
   * Criar um `java.io.FileInputStream` usando seu construtor. Transmita o local do arquivo NAV necessário (repita essa tarefa para cada arquivo necessário para criar um portfólio).
   * Criar um `com.adobe.idp.Document` e transmita o `java.io.FileInputStream` objeto que contém o arquivo NAV (repita essa tarefa para cada arquivo necessário para criar um portfólio).
   * Adicione uma entrada à `java.util.Map` ao invocar seu `put` e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Este valor deve corresponder ao valor do elemento de origem especificado no documento DDX. (repita essa tarefa para cada arquivo necessário para criar um portfólio).
      * A `com.adobe.idp.Document` objeto que contém o documento PDF. (repita essa tarefa para cada arquivo necessário para criar um portfólio).

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa, chamando um método que pertence à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler para continuar processando um job quando ocorrer um erro, chame o `AssemblerOptionSpec` do objeto `setFailOnError` e passar `false`.

1. Montar o portfólio.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado
   * A `java.util.Map` objeto que contém os arquivos necessários para criar um Portfolio PDF.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível do log de tarefas

   A variável `invokeDDX` o método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém o Portfolio PDF montado e quaisquer exceções que ocorreram.

1. Salve o portfólio montado.

   Para obter o Portfolio PDF, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método. Este método retorna um valor de `java.util.Map` objeto.
   * Repita através do `java.util.Map` até encontrar o resultado `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para extrair o Portfolio PDF.

**Consulte também**

[Início rápido (modo SOAP): montagem de Portfolio de PDF usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montar um Portfolio de PDF usando a API de serviço Web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Montar um Portfolio de PDF usando a API de serviço do Assembler (serviço da Web):

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
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento DDX e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` método. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Consulte os documentos necessários.

   * Para cada arquivo de entrada, crie um `BLOB` usando seu construtor. A variável `BLOB` é usado para armazenar o arquivo de entrada.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` método. Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.
   * Criar um `MyMapOf_xsd_string_To_xsd_anyType` objeto. Este objeto de coleção é usado para armazenar arquivos de entrada necessários para criar um Portfolio de PDF.
   * Para cada arquivo de entrada, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua um valor de string que represente o nome da chave à `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `key` campo. Este valor deve corresponder ao valor do elemento especificado no documento DDX. (Execute esta tarefa para cada arquivo de entrada.)
   * Atribua a `BLOB` objeto que armazena o arquivo de entrada para o `MyMapOf_xsd_string_To_xsd_anyType_Item` do objeto `value` campo. (Execute esta tarefa para cada documento de PDF de entrada.)
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto para o `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` do objeto `Add` e transmita o `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Execute esta tarefa para cada documento de PDF de entrada.)

1. Definir opções de tempo de execução.

   * Criar um `AssemblerOptionSpec` objeto que armazena opções de tempo de execução usando seu construtor.
   * Defina opções de tempo de execução para atender aos requisitos da sua empresa atribuindo um valor a um membro de dados que pertença à `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando um job quando ocorrer um erro, atribua `false` para o `AssemblerOptionSpec` do objeto `failOnError` membro de dados.

1. Montar o portfólio.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX
   * A variável `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém os arquivos necessários
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   A variável `invokeDDX` o método retorna um `AssemblerResult` objeto que contém os resultados do trabalho e quaisquer exceções que ocorreram.

1. Salve o portfólio montado.

   Para obter o Portfolio PDF recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` que é um `Map` objeto que contém os documentos PDF resultantes.
   * Repita através do `Map` para obter cada documento resultante. Em seguida, converta os membros da matriz `value` para um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando seus `BLOB` do objeto `MTOM` propriedade. Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
