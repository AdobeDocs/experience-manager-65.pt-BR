---
title: Montagem de portfólios PDF
seo-title: Montagem de portfólios PDF
description: 'null'
seo-description: 'null'
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 0%

---


# Montagem de portfólios PDF {#assembling-pdf-portfolios}

Você pode montar um Portfólio PDF usando o Assembler Java e a API de serviço da Web. Um portfólio pode combinar vários documentos de vários tipos, incluindo arquivos de texto, arquivos de imagem (por exemplo, um arquivo jpeg) e documentos de PDF. O layout do portfólio pode ser definido para estilos diferentes, como *Grade com Pré-visualização*, *On a Image* layout ou até mesmo *Revolve*.

A ilustração a seguir é uma captura de tela de um portfólio com o layout *Em um estilo de imagem* .

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

Criar um portfólio PDF serve como uma alternativa sem papel para transmitir uma coleção de documentos. Usando AEM Forms, você pode criar portfólios chamando o serviço Assembler com um documento DDX estruturado. O documento DDX a seguir é um exemplo de um documento DDX que cria um portfólio PDF.

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

O documento DXX deve conter uma `Portfolio` tag com uma `Navigator` tag aninhada. Observe que a tag só `<Resource name="navigator/image.xxx" source="myImage.png"/>` é necessária se `myNavigator` for atribuída como o navegador de layout onImage: `AdobeOnImage.nav`. Essa tag permite que o serviço Assembler selecione a imagem a ser usada como o plano de fundo do portfólio. Inclua `PackageFiles` e `File` tags para definir o nome do arquivo e o tipo MIME do arquivo empacotado.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Assembler, consulte Referência de [serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Para obter mais informações sobre um documento DDX, consulte [Assembler Service e DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Resumo das etapas {#summary-of-steps}

Para criar um Portfólio PDF, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um cliente do Montador de PDF.
1. Faça referência a um documento DDX existente.
1. Consulte os documentos necessários.
1. Defina as opções de tempo de execução.
1. Monte o portfólio.
1. Salve o portfólio montado.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (necessário se os AEM Forms forem implantados em JBoss)
* jbossall-client.jar (obrigatório se os AEM Forms forem implantados em JBoss)

**Criar um cliente de Montador de PDF**

Antes de executar programaticamente uma operação de Assembler, crie um cliente de serviço de Assembler.

**Referência a um documento DDX existente**

Um documento DDX deve ser referenciado para montar um Portfólio PDF. Esse documento DDX deve conter os elementos `Portfolio`, `Navigator` e, `PackageFiles` .

**Fazer referência aos documentos necessários**

Para montar um portfólio PDF, consulte todos os arquivos que representam os documentos a serem montados. Por exemplo, passe todos os arquivos de imagem especificados no documento DDX para o serviço Assembler. Observe que esses arquivos são referenciados no documento DDX especificado nesta seção: *myImage.png* e *saint_bernard.jpg*.

Ao montar um Portfólio PDF, passe um arquivo NAV (um arquivo de navegador) para o serviço Assembler. O arquivo NAV que você transmite para o serviço Assembler depende do tipo de Portfólio PDF a ser criado. Por exemplo, para criar um layout *Em uma imagem* , passe o arquivo AdobeOnImage.nav. Você pode localizar arquivos NAV na seguinte pasta:

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Copie o arquivo NAV do diretório de instalação do Acrobat 9 (ou posterior). Coloque o arquivo NAV em um local onde seu aplicativo cliente possa acessá-lo. Todos os arquivos são passados para o serviço Assembler em um objeto de coleção do Mapa.

>[!NOTE]
>
>Os start rápidos associados à Montagem de portfólios PDF usam o AdobeOnImage.nav.

**Definir opções de tempo de execução**

Você pode definir opções de tempo de execução que controlam o comportamento do serviço Assembler enquanto ele executa uma tarefa. Por exemplo, você pode definir uma opção que instrui o serviço Assembler a continuar processando uma tarefa se um erro for encontrado.

**Montar o portfólio**

Para montar um Portfólio PDF, você chama a operação `invokeDDX` . O serviço Assembler retorna o Portfólio PDF dentro de um objeto de coleção.

**Salve o portfólio montado**

Um Portfólio PDF é retornado dentro de um objeto de coleção. Itere pelo objeto de coleção e salve o Portfólio PDF como um arquivo PDF.

**Consulte também:**

[Montagem de um portfólio PDF usando a API Java](#assemble-a-pdf-portfolio-using-the-java-api)

[Montagem de um portfólio PDF usando a API de serviço da Web](#assemble-a-pdf-portfolio-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Montagem programática de Documentos PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Montagem de um portfólio PDF usando a API Java {#assemble-a-pdf-portfolio-using-the-java-api}

Monte um portfólio PDF usando a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-assembler-client.jar, no caminho de classe do seu projeto Java.

1. Crie um cliente do Montador de PDF.

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `AssemblerServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Faça referência a um documento DDX existente.

   * Crie um `java.io.FileInputStream` objeto que represente o documento DDX usando seu construtor e transmitindo um valor de string que especifica o local do arquivo DX.
   * Crie um `com.adobe.idp.Document` objeto usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Consulte os documentos necessários.

   * Crie um `java.util.Map` objeto usado para armazenar documentos PDF de entrada usando um `HashMap` construtor.
   * Crie um `java.io.FileInputStream` objeto usando seu construtor. Passe o local do arquivo NAV necessário (repita essa tarefa para cada arquivo necessário para criar um portfólio).
   * Crie um `com.adobe.idp.Document` objeto e passe o `java.io.FileInputStream` objeto que contém o arquivo NAV (repita essa tarefa para cada arquivo necessário para criar um portfólio).
   * Adicione uma entrada ao `java.util.Map` objeto chamando seu `put` método e transmitindo os seguintes argumentos:

      * Um valor de string que representa o nome da chave. Esse valor deve corresponder ao valor do elemento de origem especificado no documento DDX. (repita essa tarefa para cada arquivo necessário para criar um portfólio).
      * Um `com.adobe.idp.Document` objeto que contém o documento PDF. (repita essa tarefa para cada arquivo necessário para criar um portfólio).

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios chamando um método que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, chame o `AssemblerOptionSpec` método do `setFailOnError` objeto e passe `false`.

1. Monte o portfólio.

   Chame o `AssemblerServiceClient` método do `invokeDDX` objeto e passe os seguintes valores obrigatórios:

   * Um `com.adobe.idp.Document` objeto que representa o documento DX a ser usado
   * Um `java.util.Map` objeto que contém os arquivos necessários para criar um portfólio PDF.
   * Um `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log de trabalhos

   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém o Portfólio PDF montado e quaisquer exceções que ocorreram.

1. Salve o portfólio montado.

   Para obter o Portfólio PDF, execute as seguintes ações:

   * Chame o `AssemblerResult` método do `getDocuments` objeto. Esse método retorna um `java.util.Map` objeto.
   * Iterar pelo `java.util.Map` objeto até encontrar o `com.adobe.idp.Document` objeto resultante.
   * Chame o `com.adobe.idp.Document` `copyToFile` método do objeto para extrair o Portfólio PDF.

**Consulte também:**

[Start rápido (modo SOAP): Montagem de portfólios PDF usando a API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[Incluindo arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Montagem de um portfólio PDF usando a API de serviço da Web {#assemble-a-pdf-portfolio-using-the-web-service-api}

Monte um portfólio PDF usando a API de serviço do Assembler (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto do Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL ao definir uma referência de serviço: `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substitua `localhost` pelo endereço IP das AEM Forms de hospedagem do servidor.

1. Crie um cliente do Montador de PDF.

   * Crie um `AssemblerServiceClient` objeto usando seu construtor padrão.
   * Crie um `AssemblerServiceClient.Endpoint.Address` objeto usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Não é necessário usar o `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço.
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
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo sua `MTOM` propriedade ao conteúdo da matriz de bytes.

1. Consulte os documentos necessários.

   * Para cada arquivo de entrada, crie um `BLOB` objeto usando seu construtor. O `BLOB` objeto é usado para armazenar o arquivo de entrada.
   * Crie um `System.IO.FileStream` objeto chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do arquivo de entrada e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo do `System.IO.FileStream` objeto. É possível determinar o tamanho da matriz de bytes obtendo a propriedade do `System.IO.FileStream` objeto `Length` .
   * Preencha a matriz de bytes com dados de fluxo chamando o método do `System.IO.FileStream` objeto `Read` . Passe a matriz de bytes, a posição inicial e o comprimento do fluxo para ler.
   * Preencha o `BLOB` objeto atribuindo seu `MTOM` campo ao conteúdo da matriz de bytes.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Esse objeto de coleção é usado para armazenar arquivos de entrada necessários para criar um Portfólio PDF.
   * Para cada arquivo de entrada, crie um `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto.
   * Atribua um valor de string que representa o nome da chave ao campo do `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto `key` . Esse valor deve corresponder ao valor do elemento especificado no documento DX. (Execute esta tarefa para cada arquivo de entrada.)
   * Atribua o `BLOB` objeto que armazena o arquivo de entrada ao `MyMapOf_xsd_string_To_xsd_anyType_Item` campo do `value` objeto. (Execute essa tarefa para cada documento PDF de entrada.)
   * Adicione o `MyMapOf_xsd_string_To_xsd_anyType_Item` objeto ao `MyMapOf_xsd_string_To_xsd_anyType` objeto. Chame o `MyMapOf_xsd_string_To_xsd_anyType` método do objeto `Add` e passe o `MyMapOf_xsd_string_To_xsd_anyType` objeto. (Execute essa tarefa para cada documento PDF de entrada.)

1. Defina as opções de tempo de execução.

   * Crie um `AssemblerOptionSpec` objeto que armazene opções de tempo de execução usando seu construtor.
   * Defina as opções de tempo de execução para atender aos requisitos de negócios, atribuindo um valor a um membro de dados que pertence ao `AssemblerOptionSpec` objeto. Por exemplo, para instruir o serviço Assembler a continuar processando uma tarefa quando ocorrer um erro, atribua `false` ao membro de `AssemblerOptionSpec` dados do objeto `failOnError` .

1. Monte o portfólio.

   Chame o método do `AssemblerServiceClient` objeto `invokeDDX` e passe os seguintes valores:

   * Um `BLOB` objeto que representa o documento DDX
   * O `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém os arquivos necessários
   * Um `AssemblerOptionSpec` objeto que especifica opções de tempo de execução

   O `invokeDDX` método retorna um `AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que ocorreram.

1. Salve o portfólio montado.

   Para obter o Portfólio PDF recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` campo do `documents` objeto, que é um `Map` objeto que contém os documentos PDF resultantes.
   * Iterar pelo `Map` objeto para obter cada documento resultante. Em seguida, converta o membro do storage `value` em um `BLOB`.
   * Extraia os dados binários que representam o documento PDF acessando a propriedade do `BLOB` objeto `MTOM` . Isso retorna uma matriz de bytes que você pode gravar em um arquivo PDF.

**Consulte também:**

[Invocar AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Invocar AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
