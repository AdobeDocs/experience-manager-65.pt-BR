---
title: Criando Fluxos de Saída de Documento
description: Use o serviço Output para converter documentos como formatos de etiquetas PDF (incluindo documentos PDF/A), PostScript, Printer Control Language (PCL) e Zebra - ZPL, Intermec - IPL, Datamax - DPL e TecToshiba - TPCL.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '19006'
ht-degree: 0%

---

# Criando Fluxos de Saída de Documento  {#creating-document-output-streams}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o Serviço de Saída**

O Serviço de saída permite produzir documentos como PDF (incluindo documentos PDF/A), PostScript, PCL (Printer Control Language) e os seguintes formatos de etiqueta:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Usando o Serviço de saída, você pode mesclar dados de formulário XML com um design de formulário e enviar o documento para uma impressora ou arquivo de rede.

Há duas maneiras de passar um design de formulário (um arquivo XDP) para o serviço de Saída. Você pode passar um `com.adobe.idp.Document` instância que contém um design de formulário para o serviço de Saída. Ou você pode passar um valor de URI que especifica a localização do design do formulário. Ambas as formas são discutidas no *Programação com formulários AEM*.

>[!NOTE]
>
>O serviço de saída não é compatível com documentos do PDF do AcroForm que contenham scripts específicos de objetos de aplicativo. Os documentos de PDF de acroforma que contêm scripts específicos de objeto de aplicativo não são renderizados.

As seções a seguir mostram como passar um design de formulário para o serviço de Saída usando um valor de URI:

* [Criação de documentos PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Criação de documentos PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)

As seções a seguir mostram como passar um design de formulário em um `com.adobe.idp.Document` instância:

* [Envio de documentos localizados nos Serviços de conteúdo (descontinuado) para o Serviço de saída](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Criação de documentos PDF usando fragmentos](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

Uma consideração ao decidir qual técnica usar é se você está obtendo o design do formulário de outro serviço do AEM Forms e, em seguida, passá-lo dentro de um `com.adobe.idp.Document` instância. Ambos os *Passar documentos para o serviço de saída* e *Criação de documentos PDF usando fragmentos* As seções mostram como obter um design de formulário de outro serviço do AEM Forms. A primeira seção recupera o design do formulário do Content Services (desaprovado). A segunda seção recupera o design do formulário do serviço Assembler.

Se você estiver obtendo o design do formulário de um local fixo, como o sistema de arquivos, poderá usar qualquer uma das técnicas. Ou seja, você pode especificar o valor do URI para um arquivo XDP ou usar um `com.adobe.idp.Document` instância.

Para passar um valor de URI que especifique o local do design do formulário ao criar um documento PDF, use o `generatePDFOutput` método. Do mesmo modo, `com.adobe.idp.Document` para o Serviço de saída ao criar um documento PDF, use o `generatePDFOutput2` método.

Ao enviar um fluxo de saída para uma impressora de rede, você também pode usar qualquer uma das técnicas. Para enviar um fluxo de saída para uma impressora passando um `com.adobe.idp.Document` instância que contém um design de formulário, use o `sendToPrinter2`método. Para enviar um fluxo de saída para uma impressora passando um valor de URI, use o `sendToPrinter`método. A variável *Enviando fluxos de impressão para impressoras* A seção usa o `sendToPrinter` método.

Você pode realizar essas tarefas usando o Serviço de saída:

* [Criação de documentos PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Criação de documentos PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)
* [Envio de documentos localizados nos Serviços de conteúdo (descontinuado) para o Serviço de saída](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Criação de documentos PDF usando fragmentos](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [Imprimindo em Arquivos](creating-document-output-streams.md#printing-to-files)
* [Enviando fluxos de impressão para impressoras](creating-document-output-streams.md#sending-print-streams-to-printers)
* [Criação de vários arquivos de saída](creating-document-output-streams.md#creating-multiple-output-files)
* [Criação de regras de pesquisa](creating-document-output-streams.md#creating-search-rules)
* [Nivelamento de documentos PDF](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Criação de documentos PDF {#creating-pdf-documents}

Você pode usar o Serviço de saída para criar um documento PDF baseado em um design de formulário e em dados de formulário XML fornecidos. O documento PDF criado pelo serviço de saída não é um documento PDF interativo; um usuário não pode inserir ou modificar dados de formulário.

Se você deseja criar um documento PDF para armazenamento de longo prazo, é recomendável criar um documento PDF/A. (Consulte [Criação de documentos PDF/A](creating-document-output-streams.md#creating-pdf-a-documents).)

Para criar um formulário PDF interativo que permita ao usuário inserir dados, use o serviço Forms. (Consulte [Renderização de PDF forms interativos](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms).)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para criar um documento PDF, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de saída.
1. Fazer referência a uma fonte de dados XML.
1. Defina as opções de tempo de execução de PDF.
1. Definir opções de tempo de execução de renderização.
1. Gere um documento PDF.
1. Recuperar os resultados da operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir os arquivos adobe-utilities.jar e jbossall-client.jar pelos arquivos JAR específicos ao servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado.

**Criar um objeto do Cliente de saída**

Antes de executar programaticamente uma operação do Serviço de saída, você deve criar um objeto cliente do Serviço de saída. Se estiver usando a API Java, crie uma `OutputClient` objeto. Se você estiver usando a API de serviço Web de saída, crie uma `OutputServiceService` objeto.

**Fazer referência a uma fonte de dados XML**

Para mesclar dados com o design do formulário, você deve fazer referência a uma fonte de dados XML que contém dados. Um elemento XML deve existir para cada campo de formulário que você planeja preencher com dados. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML será ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos se todos os elementos XML forem especificados.

Considere o exemplo de formulário de aplicativo de empréstimo a seguir.

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

Para mesclar dados nesse design de formulário, você deve criar uma fonte de dados XML que corresponda ao formulário. O XML a seguir representa uma fonte de dados XML XDP que corresponde ao exemplo de formulário de aplicativo de hipoteca.

```xml
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

**Definir opções de tempo de execução de PDF**

Defina a opção de URI do arquivo ao criar um documento PDF. Essa opção especifica o nome e o local do arquivo de PDF gerado pelo serviço de Saída.

>[!NOTE]
>
>Em vez de definir a opção de tempo de execução do URI do arquivo, você pode recuperar programaticamente o documento PDF do tipo de dados complexo retornado pelo serviço de Saída. No entanto, ao definir a opção de tempo de execução do URI do arquivo, não é necessário criar uma lógica de aplicativo que recupere programaticamente o documento PDF.

**Definir opções de tempo de execução de renderização**

Você pode definir opções de tempo de execução de renderização ao criar um documento PDF. Embora essas opções não sejam obrigatórias (ao contrário das opções de tempo de execução de PDF que são necessárias), é possível executar tarefas como melhorar o desempenho do serviço de Saída. Por exemplo, é possível armazenar em cache o design do formulário que o serviço de Saída usa para melhorar o desempenho.

Se você usar um formulário Acrobat marcado como entrada, não poderá usar o Java do serviço de saída ou a API do serviço da Web para desativar a configuração marcada. Se você tentar definir esta opção de forma programática como `false`, o documento de PDF de resultado ainda estará marcado.

>[!NOTE]
>
>Se você não especificar opções de tempo de execução de renderização, os valores padrão serão usados. Para obter informações sobre as opções de tempo de execução de renderização, consulte `RenderOptionsSpec` referência de classe. (Consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

**Gerar um documento PDF**

Depois de referenciar uma fonte de dados XML válida que contenha dados de formulário e definir opções de tempo de execução, você pode chamar o serviço de Saída, o que resulta na geração de um documento PDF.

Ao gerar um documento PDF, você especifica valores de URI que são exigidos pelo serviço de Saída para criar um documento PDF. Um design de formulário pode ser armazenado em locais como o sistema de arquivos do servidor ou como parte de um aplicativo do AEM Forms. Um design de formulário (ou outros recursos, como um arquivo de imagem) que existe como parte de um aplicativo do Forms pode ser referenciado usando o valor de URI da raiz de conteúdo `repository:///`. Por exemplo, considere o seguinte design de formulário chamado *Empréstimo.xdp* localizado em um aplicativo do Forms chamado *Aplicativos/FormuláriosAplicativo*:

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

Para acessar o arquivo Loan.xdp mostrado na ilustração anterior, especifique `repository:///Applications/FormsApplication/1.0/FormsFolder/` como o terceiro parâmetro passado para o `OutputClient` do objeto `generatePDFOutput` método. Especifique o nome do formulário (*Empréstimo.xdp*) como o segundo parâmetro passado para o `OutputClient` do objeto `generatePDFOutput` método.

Se o arquivo XDP contiver imagens (ou outros recursos, como fragmentos), coloque os recursos na mesma pasta do aplicativo que o arquivo XDP. O AEM Forms usa o URI da raiz do conteúdo como o caminho base para resolver referências a imagens. Por exemplo, se o arquivo Loan.xdp contiver uma imagem, certifique-se de colocar a imagem em `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>Você pode fazer referência a um URI de aplicativo do Forms ao chamar o `OutputClient` do objeto `generatePDFOutput` ou `generatePrintedOutput` métodos.

>[!NOTE]
>
>Para ver um início rápido completo que cria um documento PDF referenciando um XDP localizado em um aplicativo do Forms, consulte [Início rápido (modo EJB): Criando um documento PDF com base em um arquivo XDP do aplicativo usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api).

**Recuperar os resultados da operação**

Depois que o Serviço de saída executa uma operação, ele retorna vários itens de dados, como dados XML de status, que especificam se a operação foi bem-sucedida.

**Consulte também**

[Criar um documento PDF usando a API Java](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[Criar um documento PDF usando a API de serviço Web](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Criar um documento PDF usando a API Java {#create-a-pdf-document-using-the-java-api}

Crie um documento PDF usando a API de saída (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente de saída.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `OutputClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Fazer referência a uma fonte de dados XML.

   * Criar um `java.io.FileInputStream` objeto que representa a fonte de dados XML usada para preencher o documento PDF usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XML.
   * Criar um `com.adobe.idp.Document` usando seu construtor. Passe o `java.io.FileInputStream` objeto.

1. Defina as opções de tempo de execução de PDF.

   * Criar um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção File URI chamando o `PDFOutputOptionsSpec` do objeto `setFileURI` método. Transmita um valor de string que especifique o local do arquivo de PDF gerado pelo serviço de Saída. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.

1. Definir opções de tempo de execução de renderização.

   * Criar um `RenderOptionsSpec` usando seu construtor.
   * Armazene em cache o design do formulário para melhorar o desempenho do Serviço de saída chamando o `RenderOptionsSpec` do objeto `setCacheEnabled` e transmitindo `true`.

   >[!NOTE]
   >
   >Não é possível definir a versão do documento PDF usando o `RenderOptionsSpec` do objeto `setPdfVersion` se o documento de entrada for um formulário Acrobat (um formulário criado no Acrobat) ou um documento XFA que esteja assinado ou certificado. O documento PDF de saída retém a versão original do PDF. Da mesma forma, não é possível definir a opção Adobe PDF com tags chamando o `RenderOptionsSpec` do objeto `setTaggedPDF` se o documento de entrada for um formulário Acrobat ou um documento XFA assinado ou certificado.

   >[!NOTE]
   >
   >Não é possível definir a opção de PDF linearizado usando o `RenderOptionsSpec` do objeto `setLinearizedPDF` se o documento de PDF de entrada estiver certificado ou assinado digitalmente. (Consulte [Assinatura digital de documentos PDF ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Gere um documento PDF.

   Crie um documento PDF chamando o `OutputClient` do objeto `generatePDFOutput` e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de cadeia de caracteres que especifica o nome do design do formulário.
   * Um valor de cadeia de caracteres que especifica a raiz do conteúdo onde o design do formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário.

   A variável `generatePDFOutput` o método retorna um `OutputResult` objeto que contém os resultados da operação.

   >[!NOTE]
   >
   >Ao gerar um documento PDF chamando o `generatePDFOutput` esteja ciente de que não é possível mesclar dados com um formulário PDF XFA assinado ou certificado. (Consulte [Assinatura digital e documentos de certificação ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >A variável `OutputResult` do objeto `getRecordLevelMetaDataList` o método retorna `null`*.*

   >[!NOTE]
   >
   >Você também pode criar um documento PDF chamando o `OutputClient` do objeto `generatePDFOutput2` método. (Consulte [Envio de documentos localizados nos Serviços de conteúdo (descontinuado) para o Serviço de saída ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. Recuperar os resultados da operação.

   * Recuperar um `com.adobe.idp.Document` objeto que representa o status do `generatePDFOutput` operação, chamando o `OutputResult` do objeto `getStatusDoc` método. Esse método retorna dados XML de status que especificam se a operação foi bem-sucedida.
   * Criar um `java.io.File` objeto que contém os resultados da operação. Verifique se a extensão do nome do arquivo é .xml.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo (certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `getStatusDoc` método).

   Embora o Serviço de saída grave o documento PDF no local especificado pelo argumento que é passado para o `PDFOutputOptionsSpec` do objeto `setFileURI` método, é possível recuperar programaticamente o documento PDF/A chamando o método `OutputResult` do objeto `getGeneratedDoc` método.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): Criação de um documento PDF usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Início rápido (modo SOAP): criação de um documento PDF usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criar um documento PDF usando a API de serviço Web {#create-a-pdf-document-using-the-web-service-api}

Crie um documento PDF usando a API de saída (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de saída.

   * Criar um `OutputServiceClient` usando seu construtor padrão.
   * Criar um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `OutputServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fazer referência a uma fonte de dados XML.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` O objeto é usado para armazenar dados XML que serão mesclados com o documento PDF.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo XML que contém dados de formulário.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução de PDF

   * Criar um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção File URI atribuindo um valor de string que especifique o local do arquivo de PDF gerado pelo serviço de saída para o `PDFOutputOptionsSpec` do objeto `fileURI` membro de dados. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.

1. Definir opções de tempo de execução de renderização.

   * Criar um `RenderOptionsSpec` usando seu construtor.
   * Armazenar em cache o design do formulário para melhorar o desempenho do serviço de Saída atribuindo o valor `true` para o `RenderOptionsSpec` do objeto `cacheEnabled` membro de dados.

   >[!NOTE]
   >
   >Não é possível definir a versão do documento PDF usando o `RenderOptionsSpec` do objeto `setPdfVersion` se o documento de entrada for um formulário Acrobat (um formulário criado no Acrobat) ou um documento XFA que esteja assinado ou certificado. O documento PDF de saída retém a versão original do PDF. Da mesma forma, não é possível definir a opção Adobe PDF com tags chamando o `RenderOptionsSpec` do objeto `setTaggedPDF`* se o documento de entrada for um formulário Acrobat ou um documento XFA assinado ou certificado.*

   >[!NOTE]
   >
   >Não é possível definir a opção de PDF linearizado usando o `RenderOptionsSpec` do objeto `linearizedPDF` membro se o documento de PDF de entrada for certificado ou assinado digitalmente. (Consulte [Assinatura digital de documentos PDF ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Gere um documento PDF.

   Crie um documento PDF chamando o `OutputServiceService` do objeto `generatePDFOutput`e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de cadeia de caracteres que especifica o nome do design do formulário.
   * Um valor de cadeia de caracteres que especifica a raiz do conteúdo onde o design do formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `BLOB` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário.
   * A `BLOB` objeto que é preenchido pelo `generatePDFOutput` método. A variável `generatePDFOutput` O método preenche esse objeto com metadados gerados que descrevem o documento. (Este valor de parâmetro é necessário somente para a invocação do serviço Web).
   * A `BLOB` objeto que é preenchido pelo `generatePDFOutput` método. A variável `generatePDFOutput` O método preenche este objeto com os dados do resultado. (Este valor de parâmetro é necessário somente para a invocação do serviço Web).
   * Um `OutputResult` objeto que contém os resultados da operação. (Este valor de parâmetro é necessário somente para a invocação do serviço Web).

   >[!NOTE]
   >
   >Ao gerar um documento PDF chamando o `generatePDFOutput` esteja ciente de que não é possível mesclar dados com um formulário PDF XFA assinado ou certificado. (Consulte [Assinatura digital e documentos de certificação ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >Você também pode criar um documento PDF chamando o `OutputClient` do objeto `generatePDFOutput2` método. (Consulte [Envio de documentos localizados nos Serviços de conteúdo (descontinuado) para o Serviço de saída ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. Recuperar os resultados da operação.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa um local de arquivo XML que contém dados de resultado. Verifique se a extensão do nome do arquivo é .xml.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi preenchido com dados de resultado pelo `OutputServiceService` do objeto `generatePDFOutput` (o oitavo parâmetro). Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` `field`.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes no arquivo XML chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

   Consulte também:

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >A variável `OutputServiceService` do objeto `generateOutput` está obsoleto.

## Criação de documentos PDF/A {#creating-pdf-a-documents}

Você pode usar o Serviço de saída para criar um documento PDF/A. Como PDF/A é um formato de arquivamento para preservação de longo prazo do conteúdo do documento, todas as fontes são incorporadas e o arquivo é descompactado. Como resultado, um documento PDF/A geralmente é maior do que um documento PDF padrão. Além disso, um documento PDF/A não contém conteúdo de áudio e vídeo. Como outras tarefas do Serviço de saída, você fornece um design de formulário e dados para mesclar com um design de formulário para criar um documento PDF/A.

A especificação PDF/A-1 consiste em dois níveis de conformidade, a saber, a e b. A principal diferença entre os dois está relacionada ao suporte de estrutura lógica (acessibilidade), que não é necessário para o nível de conformidade b. Independentemente do nível de conformidade, o PDF/A-1 determina que todas as fontes sejam incorporadas no documento PDF/A gerado.

Embora PDF/A seja o padrão para o arquivamento de documentos de PDF, não é obrigatório que PDF/A seja usado para arquivamento se um documento de PDF padrão atender às necessidades da sua empresa. O objetivo do padrão PDF/A é estabelecer um arquivo PDF que possa ser armazenado por um longo período de tempo, bem como atender aos requisitos de preservação de documentos. Por exemplo, um URL não pode ser incorporado em um PDF/A porque, com o tempo, o URL pode se tornar inválido.

Sua empresa deve avaliar suas próprias necessidades, o tempo que pretende manter o documento, as considerações sobre o tamanho do arquivo e determinar sua própria estratégia de arquivamento. Você pode determinar programaticamente se um documento de PDF é compatível com PDF/A usando o serviço DocConverter. (Consulte [Determinação Programática Da Conformidade Com PDF/A](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

Um documento PDF/A deve usar a fonte especificada no design do formulário e as fontes não podem ser substituídas. Como resultado, se uma fonte localizada em um documento do PDF não estiver disponível no sistema operacional (SO) do host, ocorrerá uma exceção.

Quando um documento PDF/A é aberto no Acrobat, uma mensagem é exibida confirmando que o documento é um documento PDF/A, como mostrado na ilustração a seguir.

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>O site do AIIM tem uma seção de perguntas frequentes sobre o PDF/A que você pode acessar em [https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml).

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_65).

### Resumo das etapas {#summary_of_steps-1}

Para criar um documento PDF/A, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de saída.
1. Fazer referência a uma fonte de dados XML.
1. Definir opções de tempo de execução de PDF/A.
1. Definir opções de tempo de execução de renderização.
1. Gere um documento PDF/A.
1. Recuperar os resultados da operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação personalizada usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir os arquivos adobe-utilities.jar e jbossall-client.jar pelos arquivos JAR específicos ao servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado.

**Criar um objeto do Cliente de saída**

Antes de executar programaticamente uma operação do Serviço de saída, você deve criar um objeto cliente do Serviço de saída. Se estiver usando a API Java, crie uma `OutputClient` objeto. Se você estiver usando a API de serviço Web de saída, crie uma `OutputServiceService` objeto.

**Fazer referência a uma fonte de dados XML**

Para mesclar dados com o design do formulário, você deve fazer referência a uma fonte de dados XML que contém dados. Um elemento XML deve existir para cada campo de formulário que você deseja preencher com dados. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML será ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos se todos os elementos XML forem especificados.

**Definir opções de tempo de execução de PDF/A**

É possível definir a opção File URI ao criar um documento PDF/A. O URI é relativo ao servidor de aplicativos J2EE que hospeda o AEM Forms. Ou seja, se você definir C:\Adobe, o arquivo será gravado na pasta no servidor, não no computador cliente. O URI especifica o nome e o local do arquivo PDF/A gerado pelo serviço de saída.

**Definir opções de tempo de execução de renderização**

Você pode definir opções de tempo de execução de renderização ao criar documentos PDF/A. Duas opções relacionadas a PDF/A que você pode definir são a `PDFAConformance` e `PDFARevisionNumber` valores. A variável `PDFAConformance` valor refere-se à forma como um documento PDF atende aos requisitos que especificam como os documentos eletrônicos de longo prazo são preservados. Os valores válidos para essa opção são `A` e `B`. Para obter informações sobre a conformidade dos níveis a e b, consulte a especificação PDF/A-1 ISO intitulada *ISO 19005-1 Gestão de documentos*.

A variável `PDFARevisionNumber` value refere-se ao número de revisão de um documento PDF/A. Para obter informações sobre o número de revisão de um documento PDF/A, consulte a especificação ISO PDF/A-1, intitulada *ISO 19005-1 Gestão de documentos*.

>[!NOTE]
>
>Não é possível definir a opção Adobe PDF com tags como `false` ao criar um documento PDF/A 1A. PDF/A 1A será sempre um documento PDF marcado. Além disso, não é possível definir a opção Adobe PDF com tags como `true` ao criar um documento PDF/A 1B. PDF/A 1B será sempre um documento PDF não marcado.

**Gerar um documento PDF/A**

Depois de fazer referência a uma fonte de dados XML válida que contém dados de formulário e definir opções de tempo de execução, você pode chamar o serviço Saída, fazendo com que ele gere um documento PDF/A.

**Recuperar os resultados da operação**

Depois que o Serviço de saída executa uma operação, ele retorna vários itens de dados, como dados XML, que especificam se a operação foi bem-sucedida.

**Consulte também**

[Criar um documento PDF/A usando a API Java](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[Criar um documento PDF/A usando a API de serviço Web](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Criar um documento PDF/A usando a API Java {#create-a-pdf-a-document-using-the-java-api}

Crie um documento PDF/A usando a API de saída (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente de saída.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `OutputClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Fazer referência a uma fonte de dados XML.

   * Criar um `java.io.FileInputStream` objeto que representa a fonte de dados XML usada para preencher o documento PDF/A usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XML.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Definir opções de tempo de execução de PDF/A.

   * Criar um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção File URI chamando o `PDFOutputOptionsSpec` do objeto `setFileURI` método. Transmita um valor de string que especifique o local do arquivo de PDF gerado pelo serviço de Saída. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.

1. Definir opções de tempo de execução de renderização.

   * Criar um `RenderOptionsSpec` usando seu construtor.
   * Defina o `PDFAConformance` ao chamar o `RenderOptionsSpec` do objeto `setPDFAConformance` e passar um `PDFAConformance` valor de enumeração que especifica o nível de conformidade. Por exemplo, para especificar o nível de conformidade A, passe `PDFAConformance.A`.
   * Defina o `PDFARevisionNumber` ao chamar o `RenderOptionsSpec` do objeto `setPDFARevisionNumber` método e transmissão `PDFARevisionNumber.Revision_1`.

   >[!NOTE]
   >
   >A versão de PDF de um documento PDF/A é a 1.4, independentemente do valor especificado para a variável `RenderOptionsSpec` do objeto `setPdfVersion`*método.*

1. Gere um documento PDF/A.

   Crie um documento PDF/A chamando o `OutputClient` do objeto `generatePDFOutput` e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF/A, especifique `TransformationFormat.PDFA`.
   * Um valor de cadeia de caracteres que especifica o nome do design do formulário.
   * Um valor de cadeia de caracteres que especifica a raiz do conteúdo onde o design do formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário.

   A variável `generatePDFOutput` o método retorna um `OutputResult` objeto que contém os resultados da operação.

   >[!NOTE]
   >
   >A variável `OutputResult` do objeto `getRecordLevelMetaDataList` o método retorna `null`.

   >[!NOTE]
   >
   >Você também pode criar um documento PDF /A chamando o `OutputClient` do objeto `generatePDFOutput`2 método. (Consulte [Envio de documentos localizados nos Serviços de conteúdo (descontinuado) para o Serviço de saída](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. Recuperar os resultados da operação.

   * Criar um `com.adobe.idp.Document` objeto que representa o status do `generatePDFOutput` ao invocar o `OutputResult` do objeto `getStatusDoc` método.
   * Criar um `java.io.File` objeto que conterá os resultados da operação. Verifique se a extensão do nome do arquivo é .xml.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo (certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `getStatusDoc` método).

   >[!NOTE]
   >
   >Embora o serviço de saída grave o documento PDF/A no local especificado pelo argumento que é passado para o `PDFOutputOptionsSpec` do objeto `setFileURI` método, é possível recuperar programaticamente o documento PDF/A chamando o método `OutputResult` do objeto `getGeneratedDoc` método.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo SOAP): Criação de um documento PDF/A usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Criar um documento PDF/A usando a API de serviço Web {#create-a-pdf-a-document-using-the-web-service-api}

Crie um documento PDF/A usando a API de saída (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de saída.

   * Criar um `OutputServiceClient` usando seu construtor padrão.
   * Criar um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `OutputServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fazer referência a uma fonte de dados XML.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` O objeto é usado para armazenar dados que serão mesclados com o documento PDF/A.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF a ser criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução de PDF/A.

   * Criar um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção File URI atribuindo um valor de string que especifique o local do arquivo de PDF gerado pelo serviço de saída para o `PDFOutputOptionsSpec` do objeto `fileURI` membro de dados. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente

1. Definir opções de tempo de execução de renderização.

   * Criar um `RenderOptionsSpec` usando seu construtor.
   * Defina o `PDFAConformance` atribuindo um `PDFAConformance` valor de enumeração para o `RenderOptionsSpec` do objeto `PDFAConformance` membro de dados. Por exemplo, para especificar o nível de conformidade A, atribua `PDFAConformance.A` para esse membro de dados.
   * Defina o `PDFARevisionNumber` atribuindo um `PDFARevisionNumber` valor de enumeração para o `RenderOptionsSpec` do objeto `PDFARevisionNumber` membro de dados. Atribuir `PDFARevisionNumber.Revision_1` para esse membro de dados.

   >[!NOTE]
   >
   >A versão de PDF de um documento PDF/A é a 1.4, independentemente do valor especificado.

1. Gere um documento PDF/A.

   Crie um documento PDF chamando o `OutputServiceService` do objeto `generatePDFOutput`e transmitindo os seguintes valores:

   * Um valor de enumeração TransformationFormat. Para gerar um documento PDF, especifique `TransformationFormat.PDFA`.
   * Um valor de cadeia de caracteres que especifica o nome do design do formulário.
   * Um valor de cadeia de caracteres que especifica a raiz do conteúdo onde o design do formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `BLOB` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário.
   * A `BLOB` objeto que é preenchido pelo `generatePDFOutput` método. A variável `generatePDFOutput` O método preenche esse objeto com metadados gerados que descrevem o documento. (Este valor de parâmetro é necessário somente para a invocação do serviço Web.)
   * A `BLOB` objeto que é preenchido pelo `generatePDFOutput` método. A variável `generatePDFOutput` O método preenche este objeto com os dados do resultado. (Este valor de parâmetro é necessário somente para a invocação do serviço Web.)
   * Um `OutputResult` objeto que contém os resultados da operação. (Este valor de parâmetro é necessário somente para a invocação do serviço Web.)

   >[!NOTE]
   >
   >Você também pode criar um documento PDF /A chamando o `OutputClient` do objeto `generatePDFOutput`2 método. (Consulte [Envio de documentos localizados nos Serviços de conteúdo (descontinuado) para o Serviço de saída](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. Recuperar os resultados da operação.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa um local de arquivo XML que contém dados de resultado. Verifique se a extensão do nome do arquivo é .xml.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi preenchido com dados de resultado pelo `OutputServiceService` do objeto `generatePDFOutput` (o oitavo parâmetro). Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` campo.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes no arquivo XML chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Envio de documentos localizados nos Serviços de conteúdo (descontinuado) para o Serviço de saída {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

O serviço de Saída renderiza um formulário de PDF não interativo baseado em um design de formulário normalmente salvo como um arquivo XDP e criado no Designer. Você pode passar um `com.adobe.idp.Document` objeto que contém o design de formulário para o serviço de Saída. O Serviço de saída renderiza o design do formulário localizado no `com.adobe.idp.Document` objeto.

Uma vantagem de passar um `com.adobe.idp.Document` para o Serviço de saída é que outras operações de serviço do AEM Forms retornam um `com.adobe.idp.Document` instância. Ou seja, você pode obter um `com.adobe.idp.Document` instância de outra operação de serviço e renderizá-la. Por exemplo, suponha que um arquivo XDP esteja armazenado em um nó do Content Services (obsoleto) chamado `/Company Home/Form Designs`, conforme mostrado na ilustração a seguir.

Você pode recuperar programaticamente Loan.xdp do Content Services (desaprovado) e passar o arquivo XDP para o serviço de saída em um `com.adobe.idp.Document` objeto.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para passar um documento obtido do Content Services (obsoleto) para o serviço de Saída, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto de Saída e de API do cliente de Gerenciamento de documentos.
1. Recuperar o design do formulário do Content Services (desaprovado).
1. Renderize o formulário de PDF não interativo.
1. Execute uma ação com o fluxo de dados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários ao projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um objeto de Saída e de API do cliente de gerenciamento de documentos**

Antes de executar programaticamente uma operação da API do Serviço de saída, crie um objeto da API do Cliente de saída. Além disso, como esse fluxo de trabalho recupera um arquivo XDP do Content Services (obsoleto), crie um objeto de API do Document Management.

**Recuperar o design do formulário do Content Services (desaprovado)**

Recupere o arquivo XDP do Content Services (obsoleto) usando o Java ou a API do serviço da Web. O arquivo XDP é retornado em um `com.adobe.idp.Document` instância (ou um `BLOB` instância se você estiver usando serviços da web). Em seguida, você pode passar o `com.adobe.idp.Document` para o Serviço de saída.

**Renderizar o formulário de PDF não interativo**

Para renderizar um formulário não interativo, passe o `com.adobe.idp.Document` que foi retornada do Content Services (descontinuada) para o Serviço de saída.

>[!NOTE]
>
>Dois novos métodos chamados `generatePDFOutput2`e g `eneratePrintedOutput2`aceitar um `com.adobe.idp.Document` objeto que contém um design de formulário. Você também pode passar um `com.adobe.idp.Document`que contém o design do formulário para o serviço de saída ao enviar um fluxo de impressão para uma impressora de rede.

**Executar uma ação com o fluxo de dados de formulário**

Você pode salvar o formulário não interativo como um arquivo PDF. O formulário pode ser exibido no Adobe Reader ou no Acrobat.

**Consulte também**

[Enviar documentos para o Serviço de saída usando a API Java](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[Enviar documentos para o Serviço de saída usando a API do serviço Web](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Criação de documentos PDF usando fragmentos](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Enviar documentos para o Serviço de saída usando a API Java {#pass-documents-to-the-output-service-using-the-java-api}

Envie um documento recuperado do Content Services (desaprovado) usando o Serviço de saída e a API do Content Services (desaprovado) (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar e adobe-contentservices-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto de Saída e de API do cliente de Gerenciamento de documentos.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Criar um `OutputClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.
   * Criar um `DocumentManagementServiceClientImpl` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar o design do formulário do Content Services (desaprovado).

   Chame o `DocumentManagementServiceClientImpl` do objeto `retrieveContent` e passe os seguintes valores:

   * Um valor de string que especifica o armazenamento em que o conteúdo é adicionado. A loja padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.

   A variável `retrieveContent` o método retorna um `CRCResult` objeto que contém o arquivo XDP. Recuperar um `com.adobe.idp.Document` ao invocar a variável `CRCResult` do objeto `getDocument` método.

1. Renderize o formulário de PDF não interativo.

   Chame o `OutputClient` do objeto `generatePDFOutput2` e passe os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica a raiz do conteúdo onde os recursos adicionais, como imagens, estão localizados.
   * A `com.adobe.idp.Document` objeto que representa o design do formulário (use a instância retornada pelo `CRCResult` do objeto `getDocument` método).
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário.

   A variável `generatePDFOutput2` o método retorna um `OutputResult` objeto que contém os resultados da operação.

1. Execute uma ação com o fluxo de dados de formulário.

   * Recuperar um `com.adobe.idp.Document` objeto que representa o formulário não interativo chamando o `OutputResult` do objeto `getGeneratedDoc` método.
   * Criar um `java.io.File` objeto que contém os resultados da operação. Verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo (certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `getGeneratedDoc` método).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): Passar documentos para o serviço de saída usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Início rápido (modo SOAP): passar documentos para o serviço de saída usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Enviar documentos para o Serviço de saída usando a API do serviço Web {#pass-documents-to-the-output-service-using-the-web-service-api}

Envie um documento recuperado do Content Services (desaprovado) usando o Serviço de saída e a API do Content Services (desaprovado) (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Como este aplicativo cliente invoca dois serviços AEM Forms, crie duas referências de serviço. Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Saída: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Gerenciamento de Documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Como a variável `BLOB` tipo de dados for comum a ambas as referências de serviço, qualifique totalmente o `BLOB` tipo de dados ao usá-lo. No início rápido do serviço Web correspondente, todas as `BLOB` As instâncias do são totalmente qualificadas.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto de Saída e de API do cliente de Gerenciamento de documentos.

   * Criar um `OutputServiceClient` usando seu construtor padrão.
   * Criar um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `OutputServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita essas etapas para a variável `DocumentManagementServiceClient`cliente de serviço.

1. Recuperar o design do formulário do Content Services (desaprovado).

   Recupere o conteúdo chamando o `DocumentManagementServiceClient` do objeto `retrieveContent` e transmitindo os seguintes valores:

   * Um valor de string que especifica o armazenamento em que o conteúdo é adicionado. A loja padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.
   * Um parâmetro de saída da string que armazena o valor do link de pesquisa.
   * A `BLOB` parâmetro de saída que armazena o conteúdo. Você pode usar esse parâmetro de saída para recuperar o conteúdo.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` parâmetro de saída que armazena atributos de conteúdo.
   * A `CRCResult` parâmetro de saída. Em vez de usar esse objeto, você pode usar o `BLOB` para recuperar o conteúdo.

1. Renderize o formulário de PDF não interativo.

   Chame o `OutputServiceClient` do objeto `generatePDFOutput2` e passe os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica a raiz do conteúdo onde os recursos adicionais, como imagens, estão localizados.
   * A `BLOB` objeto que representa o design do formulário (use o `BLOB` retornada pelo Content Services (desaprovado).
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `BLOB` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário.
   * Uma saída `BLOB` objeto que é preenchido pelo `generatePDFOutput2` método. A variável `generatePDFOutput2` O método preenche esse objeto com metadados gerados que descrevem o documento. (Este valor de parâmetro é necessário somente para a invocação do serviço Web).
   * Uma saída `OutputResult` objeto que contém os resultados da operação. (Este valor de parâmetro é necessário somente para a invocação do serviço Web).

   A variável `generatePDFOutput2` o método retorna um `BLOB` objeto que contém o formato PDF não interativo.

1. Execute uma ação com o fluxo de dados de formulário.

   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento PDF interativo e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto recuperado do `generatePDFOutput2` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Envio de documentos localizados no Repositório para o serviço de saída {#passing-documents-located-in-the-repository-to-the-output-service}

O serviço de Saída renderiza um formulário de PDF não interativo baseado em um design de formulário normalmente salvo como um arquivo XDP e criado no Designer. Você pode passar um `com.adobe.idp.Document` objeto que contém o design de formulário para o serviço de Saída. O Serviço de saída renderiza o design do formulário localizado no `com.adobe.idp.Document` objeto.

Uma vantagem de passar um `com.adobe.idp.Document` para o Serviço de saída é que outras operações de serviço do AEM Forms retornam um `com.adobe.idp.Document` instância. Ou seja, você pode obter um `com.adobe.idp.Document` instância de outra operação de serviço e renderizá-la. Por exemplo, suponha que um arquivo XDP esteja armazenado no repositório do AEM Forms, conforme mostrado na ilustração a seguir.

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

A variável *FormsFolder* pasta é um local definido pelo usuário no repositório do AEM Forms (esse local é um exemplo e não existe por padrão). Neste exemplo, um design de formulário chamado Loan.xdp está localizado nesta pasta. Além do design do formulário, outros materiais de apoio como imagens podem ser armazenados neste local. O caminho para um recurso localizado no repositório do AEM Forms é:

`Applications/Application-name/Application-version/Folder.../Filename`

Você pode recuperar programaticamente o Loan.xdp do repositório do AEM Forms e transmiti-lo para o Serviço de saída em um `com.adobe.idp.Document` objeto.

Você pode criar um PDF com base em um arquivo XDP localizado no repositório usando uma das duas formas a seguir. Você pode passar a localização XDP por referência ou recuperar programaticamente o XDP do repositório e transmiti-lo para o serviço de Saída em um arquivo XDP.

[Início rápido (modo EJB): Criando um documento PDF com base em um arquivo XDP do aplicativo usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) (mostra como passar a localização do arquivo XDP por referência).

[Início rápido (modo EJB): Passar um documento localizado no Repositório do AEM Forms para o serviço de saída usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (mostra como recuperar programaticamente o arquivo XDP do Repositório do AEM Forms e passá-lo para o serviço de Saída em um `com.adobe.idp.Document` instância). (Esta seção discute como executar esta tarefa)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-3}

Para passar um documento obtido do repositório do AEM Forms para o Serviço de saída, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto de Saída e de API do cliente de Gerenciamento de documentos.
1. Recupere o design do formulário do repositório do AEM Forms.
1. Renderize o formulário de PDF não interativo.
1. Execute uma ação com o fluxo de dados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários ao projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um objeto de Saída e de API do cliente de gerenciamento de documentos**

Antes de executar programaticamente uma operação da API do Serviço de saída, crie um objeto da API do Cliente de saída. Além disso, como esse fluxo de trabalho recupera um arquivo XDP do Content Services (obsoleto), crie um objeto de API do Document Management.

**Recuperar o design do formulário do Repositório do AEM Forms**

Recupere o arquivo XDP do Repositório do AEM Forms usando a API do Repositório. (Consulte [Recursos de leitura](/help/forms/developing/aem-forms-repository.md#reading-resources).)

O arquivo XDP é retornado em um `com.adobe.idp.Document` instância (ou um `BLOB` instância se você estiver usando serviços da web). Em seguida, você pode passar o `com.adobe.idp.Document` instância do Serviço de saída.

**Renderizar o formulário de PDF não interativo**

Para renderizar um formulário não interativo, passe o `com.adobe.idp.Document` que foi retornada usando a API do repositório do AEM Forms.

>[!NOTE]
>
>Dois novos métodos chamados `generatePDFOutput2`e `generatePrintedOutput2`aceitar um `com.adobe.idp.Document`objeto que contém um design de formulário. Você também pode passar um `com.adobe.idp.Document` que contém o design do formulário para o serviço de saída ao enviar um fluxo de impressão para uma impressora de rede.

**Executar uma ação com o fluxo de dados de formulário**

Você pode salvar o formulário não interativo como um arquivo PDF. O formulário pode ser exibido no Adobe Reader ou no Acrobat.

**Consulte também**

[Enviar documentos localizados no Repositório para o Serviço de saída usando a API Java](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Enviar documentos localizados no Repositório para o Serviço de saída usando a API Java {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

Envie um documento recuperado do Repositório usando o Serviço de saída e a API do repositório (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar e adobe-repository-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto de Saída e de API do cliente de Gerenciamento de documentos.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Criar um `OutputClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.
   * Criar um `DocumentManagementServiceClientImpl` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere o design do formulário do Repositório do AEM Forms.

   Chame o `ResourceRepositoryClient` do objeto `readResourceContent` e transmita um valor de string que especifique o local do URI para o arquivo XDP. Por exemplo, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. Esse valor é obrigatório. Este método retorna um valor de `com.adobe.idp.Document` que representa o arquivo XDP.

1. Renderize o formulário de PDF não interativo.

   Chame o `OutputClient` do objeto `generatePDFOutput2` e passe os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica a raiz do conteúdo onde os recursos adicionais, como imagens, estão localizados. Por exemplo, `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * A `com.adobe.idp.Document` objeto que representa o design do formulário (use a instância retornada pelo `ResourceRepositoryClient` do objeto `readResourceContent` método).
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário.

   A variável `generatePDFOutput2` o método retorna um `OutputResult` objeto que contém os resultados da operação.

1. Execute uma ação com o fluxo de dados de formulário.

   * Recuperar um `com.adobe.idp.Document` objeto que representa o formulário não interativo chamando o `OutputResult` do objeto `getGeneratedDoc` método.
   * Criar um `java.io.File` objeto que contém os resultados da operação. Verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo (certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `getGeneratedDoc` método).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): Passar um documento localizado no Repositório do AEM Forms para o serviço de saída usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Criação de documentos PDF usando fragmentos {#creating-pdf-documents-using-fragments}

Você pode usar os serviços Saída e Assembler para criar um fluxo de saída, como um documento PDF, baseado em fragmentos. O serviço do Assembler monta um documento XDP baseado em fragmentos localizados em vários arquivos XDP. O documento XDP montado é passado para o Serviço de saída, que cria um documento PDF. Embora esse fluxo de trabalho mostre um documento PDF sendo gerado, o Serviço de saída pode gerar outros tipos de saída, como ZPL, para esse fluxo de trabalho. Um documento PDF é usado apenas para fins de discussão.

A ilustração a seguir mostra esse fluxo de trabalho.

![cp_cp_outputassemblefragments](assets/cp_cp_outputassemblefragments.png)

Antes de ler *Criação de documentos PDF usando fragmentos*, é recomendável que você se familiarize com o uso do serviço Assembler para montar vários documentos XDP. (Consulte [Montagem de vários fragmentos XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments).)

>[!NOTE]
>
>Você também pode passar um design de formulário montado pelo serviço Assembler para o serviço Forms em vez do serviço Output. A principal diferença entre o serviço de saída e o serviço Forms é que o serviço Forms gera documentos PDF interativos e o serviço de saída produz documentos PDF não interativos. Além disso, o serviço Forms não pode gerar fluxos de saída com base em impressora como ZPL.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-4}

Para criar um documento PDF com base em fragmentos, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um objeto Cliente de Saída e Assembler.
1. Use o serviço Assembler para gerar o design do formulário.
1. Use o Serviço de saída para gerar o documento PDF.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto Cliente de Saída e Assembler**

Antes de executar programaticamente uma operação da API do Serviço de saída, crie um objeto da API do Cliente de saída. Além disso, como esse fluxo de trabalho chama o serviço Assembler para criar o design do formulário, crie um objeto de API do cliente Assembler.

**Usar o serviço Assembler para gerar o design do formulário**

Use o serviço Assembler para gerar o design do formulário usando fragmentos. O serviço Assembler retorna um `com.adobe.idp.Document` instância que contém o design do formulário.

**Use o Serviço de saída para gerar o documento PDF**

Você pode usar o Serviço de saída para gerar um documento PDF usando o design de formulário criado pelo serviço Assembler. Passe o `com.adobe.idp.Document` que o serviço Assembler retornou para o serviço Output.

**Salve o documento PDF como um arquivo PDF**

Depois que o serviço de saída gerar um documento PDF, você poderá salvá-lo como um arquivo PDF.

**Consulte também**

[Criar um documento PDF com base em fragmentos usando a API Java](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[Criar um documento PDF com base em fragmentos usando a API de serviço da Web](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Montagem de vários fragmentos XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[Criação de documentos PDF](creating-document-output-streams.md#creating-pdf-documents)

### Criar um documento PDF com base em fragmentos usando a API Java {#create-a-pdf-document-based-on-fragments-using-the-java-api}

Crie um documento PDF com base em fragmentos usando a API de serviço de saída e a API de serviço do Assembler (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto Cliente de Saída e Assembler.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `OutputClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.
   * Criar um `AssemblerServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Use o serviço Assembler para gerar o design do formulário.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado.
   * A `java.util.Map` objeto que contém os arquivos XDP de entrada.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do job.

   A variável `invokeDDX` o método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém o documento XDP montado. Para recuperar o documento XDP montado, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método. Este método retorna um valor de `java.util.Map` objeto.
   * Repita através do `java.util.Map` até encontrar o resultado `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento XDP montado.

1. Use o Serviço de saída para gerar o documento PDF.

   Chame o `OutputClient` do objeto `generatePDFOutput2` e passe os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`
   * Um valor de string que especifica a raiz do conteúdo onde os recursos adicionais, como imagens, estão localizados
   * A `com.adobe.idp.Document` objeto que representa o design do formulário (use a instância retornada pelo serviço Assembler)
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização
   * A variável `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário

   A variável `generatePDFOutput2` o método retorna um `OutputResult` objeto que contém os resultados da operação

1. Salve o documento PDF como um arquivo PDF.

   * Recuperar um `com.adobe.idp.Document` objeto que representa o documento PDF chamando o `OutputResult` do objeto `getGeneratedDoc` método.
   * Criar um `java.io.File` objeto que contém os resultados da operação. Verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo. (Certifique-se de usar a variável `com.adobe.idp.Document` objeto que o `getGeneratedDoc` método retornado.).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): Criação de um documento PDF com base em fragmentos usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Início rápido (modo SOAP): criação de um documento PDF com base em fragmentos usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Criar um documento PDF com base em fragmentos usando a API de serviço da Web {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

Crie um documento PDF com base em fragmentos usando a API de serviço de saída e a API de serviço do Assembler (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Saída:

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Use a seguinte definição WSDL para a referência de serviço associada ao serviço Assembler:

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   Como a variável `BLOB` tipo de dados for comum a ambas as referências de serviço, qualifique totalmente o `BLOB` tipo de dados ao usá-lo. No início rápido do serviço Web correspondente, todas as `BLOB` As instâncias do são totalmente qualificadas.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um objeto Cliente de Saída e Assembler.

   * Criar um `OutputServiceClient` usando seu construtor padrão.
   * Criar um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `OutputServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM à `OutputServiceClient.ClientCredentials.UserName.UserName`campo.
      * Atribua o valor de senha correspondente ao `OutputServiceClient.ClientCredentials.UserName.Password`campo.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` para o `BasicHttpBindingSecurity.Transport.ClientCredentialType`campo.

   * Atribua a `BasicHttpSecurityMode.TransportCredentialOnly` valor constante para o `BasicHttpBindingSecurity.Security.Mode`campo.

   >[!NOTE]
   >
   >Repita essas etapas para a variável `AssemblerServiceClient`objeto.

1. Use o serviço Assembler para gerar o design do formulário.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX
   * A variável `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém os arquivos necessários
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   A variável `invokeDDX` o método retorna um `AssemblerResult` objeto que contém os resultados do trabalho e quaisquer exceções que ocorreram. Para obter o documento XDP recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` que é um `Map` objeto que contém os documentos PDF resultantes.
   * Repita através do `Map` objeto para recuperar o design do formulário montado. Transmitir do membro da matriz `value` para um `BLOB`. Passar este `BLOB` para o Serviço de saída.

1. Use o Serviço de saída para gerar o documento PDF.

   Chame o `OutputServiceClient` do objeto `generatePDFOutput2` e passe os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica a raiz do conteúdo onde os recursos adicionais, como imagens, estão localizados.
   * A `BLOB` objeto que representa o design do formulário (use o `BLOB` instância retornada pelo serviço Assembler).
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `BLOB` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário.
   * Uma saída `BLOB` objeto que o `generatePDFOutput2` é preenchido. A variável `generatePDFOutput2` O método preenche esse objeto com metadados gerados que descrevem o documento. (Este valor de parâmetro é necessário somente para a invocação do serviço Web).
   * Uma saída `OutputResult` objeto que contém os resultados da operação. (Este valor de parâmetro é necessário somente para a invocação do serviço Web).

   A variável `generatePDFOutput2` o método retorna um `BLOB` objeto que contém o formato PDF não interativo.

1. Salve o documento PDF como um arquivo PDF.

   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento PDF interativo e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto recuperado do `generatePDFOutput2` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Imprimindo em Arquivos {#printing-to-files}

Você pode usar o serviço de Saída para imprimir fluxos como PostScript, Printer Control Language (PCL) ou os seguintes formatos de rótulo em um arquivo:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Usando o Serviço de saída, você pode mesclar dados XML com um design de formulário e imprimir o formulário em um arquivo. A ilustração a seguir mostra o Serviço de saída criando arquivos de etiquetas e laser.

>[!NOTE]
>
>Para obter informações sobre como enviar fluxos de impressão para impressoras, consulte [Enviando fluxos de impressão para impressoras](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-5}

Para imprimir em um arquivo, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de saída.
1. Fazer referência a uma fonte de dados XML.
1. Defina as opções de tempo de execução de impressão necessárias para imprimir em um arquivo.
1. Imprima o fluxo de impressão em um arquivo.
1. Recuperar os resultados da operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir os arquivos adobe-utilities.jar e jbossall-client.jar pelos arquivos JAR específicos ao servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado. (Consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)

**Criar um objeto do Cliente de saída**

Antes de executar programaticamente uma operação do Serviço de saída, você deve criar um objeto cliente do Serviço de saída. Se estiver usando a API Java, crie uma `OutputClient` objeto. Se você estiver usando a API de serviço Web de saída, crie uma `OutputServiceService` objeto.

**Fazer referência a uma fonte de dados XML**

Para imprimir um documento que contenha dados, você deve fazer referência a uma fonte de dados XML que contenha elementos XML para cada campo de formulário que você deseja preencher com dados. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML será ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos se todos os elementos XML forem especificados.

**Definir as opções de tempo de execução de impressão necessárias para imprimir em um arquivo**

Para imprimir em um arquivo, você deve definir a opção de tempo de execução do URI de arquivo especificando o local e o nome do arquivo no qual o serviço de Saída é impresso. Por exemplo, para instruir o serviço de saída a imprimir um arquivo PostScript chamado *FormulárioHipoteca.ps* para C:\Adobe, especifique C:\Adobe\MortgageForm.ps.

>[!NOTE]
>
>Há opções opcionais de tempo de execução que podem ser definidas. Para obter informações sobre todas as opções que podem ser definidas, consulte `PrintedOutputOptionsSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Imprimir o fluxo de impressão em um arquivo**

Depois de fazer referência a uma fonte de dados XML válida que contém dados de formulário e definir opções de tempo de execução de impressão, você pode chamar o serviço Saída, o que faz com que ele imprima um arquivo.

**Recuperar os resultados da operação**

Depois que o Serviço de saída executa uma operação, ele retorna vários itens de dados, como dados XML, que especificam se a operação foi bem-sucedida.

**Consulte também**

[Imprimir em arquivos usando a API Java](creating-document-output-streams.md#print-to-files-using-the-java-api)

[Imprimir em arquivos usando a API do serviço Web](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Imprimir em arquivos usando a API Java {#print-to-files-using-the-java-api}

Imprima em um arquivo usando a API de saída (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente de saída.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `OutputClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Fazer referência a uma fonte de dados XML.

   * Criar um `java.io.FileInputStream` objeto que representa a fonte de dados XML usada para preencher o documento usando seu construtor e transmitindo um valor de cadeia de caracteres que especifica o local do arquivo XML.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Defina as opções de tempo de execução de impressão necessárias para imprimir em um arquivo.

   * Criar um `PrintedOutputOptionsSpec` usando seu construtor.
   * Especifique o arquivo chamando o nome do objeto PrintedOutputOptionsSpec `setFileURI` e transmitindo um valor de string que representa o nome e o local do arquivo. Por exemplo, se você quiser que o serviço de Saída imprima em um arquivo PostScript chamado MortgageForm.ps localizado em C:\Adobe, especifique C:\\Adobe\MortgageForm.ps.
   * Especifique o número de cópias a serem impressas chamando o `PrintedOutputOptionsSpec` do objeto `setCopies` e transmitindo um valor inteiro que representa o número de cópias.

1. Imprima o fluxo de impressão em um arquivo.

   Imprima em um arquivo chamando o `OutputClient` do objeto `generatePrintedOutput` e transmitindo os seguintes valores:

   * A `PrintFormat` valor de enumeração que especifica o formato de fluxo de impressão a ser criado. Por exemplo, para criar um fluxo de impressão PostScript, passe `PrintFormat.PostScript`.
   * Um valor de cadeia de caracteres que especifica o nome do design do formulário.
   * Um valor de string que especifica o local dos arquivos de materiais relacionados, como arquivos de imagem.
   * Um valor de cadeia de caracteres que especifica o local do arquivo XDC a ser usado (você pode passar `null` se você especificou o arquivo XDC a ser usado usando o `PrintedOutputOptionsSpec` objeto).
   * A variável `PrintedOutputOptionsSpec` objeto que contém as opções de tempo de execução necessárias para imprimir em um arquivo.
   * A variável `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém dados de formulário.

   A variável `generatePrintedOutput` o método retorna um `OutputResult` objeto que contém os resultados da operação.

   >[!NOTE]
   >
   >A variável `OutputResult` do objeto `getRecordLevelMetaDataList` o método retorna `null`.

1. Recuperar os resultados da operação.

   * Criar um `com.adobe.idp.Document` objeto que representa o status do `generatePrintedOutput` ao invocar o `OutputResult` do objeto `getStatusDoc` (o método `OutputResult` objeto foi retornado pelo `generatePrintedOutput` método).
   * Criar um `java.io.File` objeto que conterá os resultados da operação. Certifique-se de que a extensão do arquivo seja XML.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo (certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `getStatusDoc` método).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo SOAP): impressão em um arquivo usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Imprimir em arquivos usando a API do serviço Web {#print-to-files-using-the-web-service-api}

Imprima em um arquivo usando a API de saída (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de saída.

   * Criar um `OutputServiceClient` usando seu construtor padrão.
   * Criar um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `OutputServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fazer referência a uma fonte de dados XML.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar dados de formulário.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que especifica o local do arquivo XML que contém dados de formulário.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `binaryData` com o conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução de impressão necessárias para imprimir em um arquivo.

   * Criar um `PrintedOutputOptionsSpec` usando seu construtor.
   * Especifique o arquivo atribuindo um valor de string que represente o local e o nome do arquivo à `PrintedOutputOptionsSpec` do objeto `fileURI` membro de dados. Por exemplo, se você quiser que o serviço de saída imprima em um arquivo PostScript chamado *FormulárioHipoteca.ps* localizado em C:\Adobe, especifique C:\\Adobe\MortgageForm.ps.
   * Especifique o número de cópias a serem impressas atribuindo um valor inteiro que represente o número de cópias à `PrintedOutputOptionsSpec` do objeto `copies` membros de dados.

1. Imprima o fluxo de impressão em um arquivo.

   Imprima em um arquivo chamando o `OutputServiceService` do objeto `generatePrintedOutput` e transmitindo os seguintes valores:

   * A `PrintFormat` valor de enumeração que especifica o formato de fluxo de impressão a ser criado. Por exemplo, para criar um fluxo de impressão PostScript, passe `PrintFormat.PostScript`.
   * Um valor de cadeia de caracteres que especifica o nome do design do formulário.
   * Um valor de string que especifica o local dos arquivos de materiais relacionados, como arquivos de imagem.
   * Um valor de cadeia de caracteres que especifica o local do arquivo XDC a ser usado (você pode passar `null` se você especificou o arquivo XDC a ser usado usando o `PrintedOutputOptionsSpec` objeto).
   * A variável `PrintedOutputOptionsSpec` objeto que contém as opções de tempo de execução de impressão necessárias para imprimir em um arquivo.
   * A variável `BLOB` objeto que contém a fonte de dados XML que contém dados de formulário.
   * A `BLOB` objeto que é preenchido pelo `generatePDFOutput` método. A variável `generatePDFOutput` O método preenche esse objeto com metadados gerados que descrevem o documento. (Este valor de parâmetro é necessário somente para a invocação do serviço Web.)
   * A `BLOB` objeto que é preenchido pelo `generatePDFOutput` método. A variável `generatePDFOutput` O método preenche este objeto com os dados do resultado. (Este valor de parâmetro é necessário somente para a invocação do serviço Web.)
   * Um `OutputResult` objeto que contém os resultados da operação. (Este valor de parâmetro é necessário somente para a invocação do serviço Web.)

1. Recuperar os resultados da operação.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa um local de arquivo XML que contém dados de resultado. Certifique-se de que a extensão do arquivo seja XML.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi preenchido com dados de resultado pelo `OutputServiceService` do objeto `generatePDFOutput` (o oitavo parâmetro). Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes no arquivo XML chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Enviando fluxos de impressão para impressoras {#sending-print-streams-to-printers}

Você pode usar o Serviço de saída para enviar fluxos de impressão, como PostScript, PCL (Printer Control Language) ou os seguintes formatos de rótulo, para impressoras de rede:

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Usando o Serviço de saída, você pode mesclar dados XML com um design de formulário e gerar a saída do formulário como um fluxo de impressão. Por exemplo, você pode criar um fluxo de impressão PostScript e enviá-lo para uma impressora de rede. A ilustração a seguir mostra o serviço de Saída enviando fluxos de impressão para impressoras de rede.

>[!NOTE]
>
>Para demonstrar como enviar um fluxo de impressão para uma impressora de rede, esta seção envia um fluxo de impressão PostScript para uma impressora de rede usando o protocolo de impressora SharedPrinter.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-6}

Para enviar um fluxo de impressão para uma impressora de rede, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de saída.
1. Fazer referência a uma fonte de dados XML.
1. Definir opções de tempo de execução de impressão
1. Recupere um documento para imprimir.
1. Envie o documento para uma impressora de rede.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir os arquivos adobe-utilities.jar e jbossall-client.jar pelos arquivos JAR específicos ao servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado.

**Criar um objeto do Cliente de saída**

Antes de executar programaticamente uma operação do Serviço de saída, crie um objeto cliente do Serviço de saída. Se estiver usando a API Java, crie uma `OutputClient` objeto. Se você estiver usando a API de serviço Web de saída, crie uma `OutputServiceClient` objeto.

**Fazer referência a uma fonte de dados XML**

Para imprimir um documento que contenha dados, você deve fazer referência a uma fonte de dados XML que contenha elementos XML para cada campo de formulário que você deseja preencher com dados. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML será ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos se todos os elementos XML forem especificados.

**Definir opções de tempo de execução de impressão**

É possível definir as opções de tempo de execução ao enviar um fluxo de impressão para uma impressora, incluindo as seguintes opções:

* **Cópias**: especifica o número de cópias a serem enviadas para a impressora. O valor padrão é 1.
* **Grampear**: uma opção XCI é definida quando um grampeador é usado. Esta opção pode ser especificada no modelo de configuração pelo elemento de grampo e é usada somente para impressoras PS e PCL.
* **OutputJog**: uma opção XCI é definida quando as páginas de saída devem ser ajustadas (deslocadas fisicamente na bandeja de saída). Esta opção é somente para impressoras PS e PCL.
* **OutputBin**: valor XCI usado para permitir que o driver de impressão selecione o compartimento de saída apropriado.

>[!NOTE]
>
>Para obter informações sobre todas as opções de tempo de execução que podem ser definidas, consulte `PrintedOutputOptionsSpec` referência de classe.

**Recuperar um documento para imprimir**

Recupere um fluxo de impressão para enviar a uma impressora. Por exemplo, é possível recuperar um arquivo PostScript e enviá-lo para uma impressora.

Você pode optar por enviar um arquivo de PDF se a impressora suportar PDF. Entretanto, um problema ao enviar um documento de PDF para uma impressora é que cada fabricante de impressora tem uma implementação diferente do interpretador de PDF. Ou seja, alguns fabricantes de impressão usam a interpretação Adobe PDF, mas isso depende da impressora. Outras impressoras têm seu próprio interpretador PDF. Como resultado, os resultados da impressão podem variar.

Outra limitação do envio de um documento PDF para uma impressora é que ele apenas imprime; ele não pode acessar duplex, seleção de bandeja de papel e grampeamento, exceto pelas configurações da impressora.

Para recuperar um documento para impressão, use o `generatePrintedOutput` método. A tabela a seguir especifica os tipos de conteúdo definidos para um determinado fluxo de impressão ao usar o `generatePrintedOutput` método.

<table>
 <thead>
  <tr>
   <th><p>Formato de impressão </p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>DPL </p></td>
   <td><p>Cria um fluxo de saída xdc padrão ou personalizado dpl203.xdc.</p></td>
  </tr>
  <tr>
   <td><p>DPL 300 DPI </p></td>
   <td><p>Cria um fluxo de saída DPL 300 DPI.</p></td>
  </tr>
  <tr>
   <td><p>DPL 406 DPI </p></td>
   <td><p>Cria um fluxo de saída DPL 400 DPI.</p></td>
  </tr>
  <tr>
   <td><p>DPL 600 DPI </p></td>
   <td><p>Cria um fluxo de saída DPL 600 DPI.</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>Cria um fluxo de saída Generic Color PCL (5c).</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>Cria um fluxo de saída PostScript genérico de nível 3.</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>Cria um fluxo de saída IPL personalizado.</p></td>
  </tr>
  <tr>
   <td><p>IPL 300 DPI </p></td>
   <td><p>Cria um fluxo de saída IPL 300 DPI.</p></td>
  </tr>
  <tr>
   <td><p>IPL 400 DPI </p></td>
   <td><p>Cria um fluxo de saída IPL 400 DPI.</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>Cria um fluxo de saída PCL monocromático genérico (5e).</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>Cria um fluxo de saída PostScript genérico de nível 2.</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>Cria um fluxo de saída TPCL personalizado.</p></td>
  </tr>
  <tr>
   <td><p>TPCL 305 DPI </p></td>
   <td><p>Cria um fluxo de saída TPCL 305 DPI.</p></td>
  </tr>
  <tr>
   <td><p>TPCL 600 DPI </p></td>
   <td><p>Cria um fluxo de saída TPCL 600 DPI.</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>Cria um fluxo de saída ZPL 203 DPI.</p></td>
  </tr>
  <tr>
   <td><p>ZPL 300 DPI </p></td>
   <td><p>Cria um fluxo de saída ZPL 300 DPI.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Também é possível enviar um fluxo de impressão para uma impressora usando o `generatePrintedOutput2` método. No entanto, os inícios rápidos associados à seção Envio de fluxos de impressão para impressoras usam o `generatePrintedOutput` método.

**Enviar o fluxo de impressão para uma impressora de rede**

Depois de recuperar um documento para impressão, você pode chamar o Serviço de saída, o que faz com que ele envie um fluxo de impressão para uma impressora de rede. Para que o Serviço de saída localize a impressora com êxito, você deve especificar o servidor de impressão e o nome da impressora. Além disso, você também deve especificar o protocolo de impressão.

>[!NOTE]
>
>Se o PDFG estiver instalado no servidor de formulários e o servidor for executado no Windows Server 2008, não será possível usar a propriedade SharedPrinter. Nessa situação, use um protocolo de impressora diferente.

>[!NOTE]
>
>Se você estiver usando uma impressora de rede e o mecanismo de acesso for SharedPrinter, será necessário especificar o caminho de rede completo da impressora.Envie um fluxo de impressão para uma impressora de rede usando a API Java

Envie um fluxo de impressão para uma impressora de rede usando a API de saída (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do projeto Java.

1. Criar um objeto do Cliente de saída

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `OutputClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Fazer referência a uma fonte de dados XML

   * Criar um `java.io.FileInputStream` objeto que representa a fonte de dados XML usada para preencher o documento usando seu construtor e transmitindo um valor de cadeia de caracteres que especifica o local do arquivo XML.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Definir opções de tempo de execução de impressão

   Criar um `PrintedOutputOptionsSpec` objeto que representa as opções de tempo de execução de impressão. Por exemplo, você pode especificar o número de cópias a serem impressas chamando o `PrintedOutputOptionsSpec` do objeto `setCopies` método.

   >[!NOTE]
   >
   >Não é possível definir o valor de paginação usando o `PrintedOutputOptionsSpec` do objeto `setPagination` se estiver gerando um fluxo de impressão ZPL. Da mesma forma, não é possível definir as seguintes opções para um fluxo de impressão ZPL: OutputJog, PageOffset e Staple. A variável `setPagination` O método não é válido para geração PostScript. É válido apenas para a geração PCL.

1. Recuperar um documento para imprimir

   * Recupere um documento para imprimir chamando o `OutputClient` do objeto `generatePrintedOutput` e transmitindo os seguintes valores:

      * A `PrintFormat` valor de enumeração que especifica o fluxo de impressão. Por exemplo, para criar um fluxo de impressão PostScript, passe `PrintFormat.PostScript`.
      * Um valor de cadeia de caracteres que especifica o nome do design do formulário.
      * Um valor de string que especifica o local dos arquivos de materiais relacionados, como arquivos de imagem.
      * Um valor de cadeia de caracteres que especifica o local do arquivo XDC a ser usado.
      * A variável `PrintedOutputOptionsSpec` objeto que contém as opções de tempo de execução necessárias para imprimir em um arquivo.
      * A variável `com.adobe.idp.Document` objeto que representa a fonte de dados XML que contém dados de formulário a serem mesclados com o design do formulário.

     Este método retorna um valor de `OutputResult` objeto que contém os resultados da operação.

   * Criar um `com.adobe.idp.Document` para enviar à impressora invocando o `OutputResult` do objeto `getGeneratedDoc` método. Este método retorna um valor de `com.adobe.idp.Document` objeto.

1. Enviar o fluxo de impressão para uma impressora de rede

   Envie o fluxo de impressão para uma impressora de rede chamando o `OutputClient` do objeto `sendToPrinter` e transmitindo os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o fluxo de impressão a ser enviado para a impressora.
   * A `PrinterProtocol` valor de enumeração que especifica o protocolo de impressora a ser usado. Por exemplo, para especificar o protocolo SharedPrinter, passe `PrinterProtocol.SharedPrinter`.
   * Um valor de string que especifica o nome do servidor de impressão. Por exemplo, supondo que o nome do servidor de impressão seja PrintServer1, passe `\\\PrintSever1`.
   * Um valor de cadeia de caracteres que especifica o nome da impressora. Por exemplo, supondo que o nome da impressora seja Printer1, passe `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >A variável `sendToPrinter` O método foi adicionado à API do AEM Forms na versão 8.2.1.

### Enviar um fluxo de impressão para uma impressora usando a API do serviço Web {#send-a-print-stream-to-a-printer-using-the-web-service-api}

Envie um fluxo de impressão para uma impressora de rede usando a API de saída (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de saída.

   * Criar um `OutputServiceClient` usando seu construtor padrão.
   * Criar um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `OutputServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fazer referência a uma fonte de dados XML.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar dados de formulário.
   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de cadeia de caracteres que especifique o local do arquivo XML que contém dados de formulário.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Determine o comprimento da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução de impressão.

   Criar um `PrintedOutputOptionsSpec` usando seu construtor. Por exemplo, você pode especificar o número de cópias a serem impressas atribuindo um valor inteiro que represente o número de cópias à `PrintedOutputOptionsSpec` do objeto `copies` membro de dados.

   >[!NOTE]
   >
   >Não é possível definir o valor de paginação usando o `PrintedOutputOptionsSpec` do objeto `pagination` membro de dados se você estiver gerando um fluxo de impressão ZPL. Da mesma forma, não é possível definir as seguintes opções para um fluxo de impressão ZPL: OutputJog, PageOffset e Staple. A variável `pagination` membro de dados inválido para geração PostScript. É válido apenas para a geração PCL.

1. Recupere um documento para imprimir.

   * Recupere um documento para imprimir chamando o `OutputServiceService` do objeto `generatePrintedOutput` e transmitindo os seguintes valores:

      * A `PrintFormat` valor de enumeração que especifica o fluxo de impressão. Por exemplo, para criar um fluxo de impressão PostScript, passe `PrintFormat.PostScript`.
      * Um valor de cadeia de caracteres que especifica o nome do design do formulário.
      * Um valor de string que especifica o local dos arquivos de materiais relacionados, como arquivos de imagem.
      * Um valor de cadeia de caracteres que especifica o local do arquivo XDC a ser usado.
      * A variável `PrintedOutputOptionsSpec` objeto que contém opções de tempo de execução de impressão que são usadas ao enviar um fluxo de impressão para uma impressora de rede.
      * A variável `BLOB` objeto que contém a fonte de dados XML que contém dados de formulário.
      * A `BLOB` objeto que é preenchido pelo `generatePrintedOutput` método. A variável `generatePrintedOutput` O método preenche esse objeto com metadados gerados que descrevem o documento. (Este valor de parâmetro é necessário somente para a invocação do serviço Web.)
      * A `BLOB` objeto que é preenchido pelo `generatePrintedOutput` método. A variável `generatePrintedOutput` O método preenche este objeto com os dados do resultado. (Este valor de parâmetro é necessário somente para a invocação do serviço Web.)
      * Um `OutputResult` objeto que contém os resultados da operação. (Este valor de parâmetro é necessário somente para a invocação do serviço Web.)

   * Criar um `BLOB` para enviar à impressora obtendo o valor do parâmetro `OutputResult` do objeto `generatedDoc` método. Este método retorna um valor de `BLOB` objeto que contém dados PostScript retornados pelo `generatePrintedOutput` método.

1. Envie o fluxo de impressão para uma impressora de rede.

   Envie o fluxo de impressão para uma impressora de rede chamando o `OutputClient` do objeto `sendToPrinter` e transmitindo os seguintes valores:

   * A `BLOB` objeto que representa o fluxo de impressão a ser enviado para a impressora.
   * A `PrinterProtocol` valor de enumeração que especifica o protocolo de impressora a ser usado. Por exemplo, para especificar o protocolo SharedPrinter, passe `PrinterProtocol.SharedPrinter`.
   * A `bool` valor que especifica se o valor do parâmetro anterior deve ser usado. Transmita o valor `true`. (Este valor de parâmetro é necessário somente para a invocação do serviço Web.)
   * Um valor de string que especifica o nome do servidor de impressão. Por exemplo, supondo que o nome do servidor de impressão seja PrintServer1, passe `\\\PrintSever1`.
   * Um valor de cadeia de caracteres que especifica o nome da impressora. Por exemplo, supondo que o nome da impressora seja Printer1, passe `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >A variável `sendToPrinter` O método foi adicionado à API do AEM Forms na versão 8.2.1.

## Criação de vários arquivos de saída {#creating-multiple-output-files}

O Serviço de saída pode criar documentos separados para cada registro em uma fonte de dados XML ou em um único arquivo que contenha todos os registros (essa funcionalidade é o padrão). Por exemplo, suponha que dez registros estejam localizados em uma fonte de dados XML e você instrua o serviço de Saída a criar documentos de PDF separados (ou outros tipos de saída) para cada registro usando a API de Serviço de Saída. Como resultado, o Serviço de saída gera dez documentos PDF. (Em vez de criar documentos, você pode enviar vários fluxos de impressão para uma impressora.)

A ilustração a seguir também mostra o Serviço de saída processando um arquivo de dados XML que contém vários registros. No entanto, suponha que você instrua o Serviço de saída a criar um único documento de PDF que contenha todos os registros de dados. Nessa situação, o Serviço de saída gera um documento que contém todos os registros.

A ilustração a seguir mostra o Serviço de saída processando um arquivo de dados XML que contém vários registros. Suponha que você instrua o Serviço de saída a criar um documento de PDF separado para cada registro de dados. Nessa situação, o Serviço de saída gera um documento de PDF separado para cada registro de dados.

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

Os dados XML a seguir mostram um exemplo de um arquivo de dados que contém três registros de dados.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <batch>
 <LoanRecord>
     <mortgageAmount>500000</mortgageAmount>
     <lastName>Blue</lastName>
     <firstName>Tony</firstName>
     <SSN>555666777</SSN>
     <PositionTitle>Product Manager</PositionTitle>
     <Address>555 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>TBlue@NoMailServer.com</Email>
     <PhoneNum>555-7418</PhoneNum>
     <FaxNum>555-9981</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>300000</mortgageAmount>
     <lastName>White</lastName>
     <firstName>Sam</firstName>
     <SSN>555666222</SSN>
     <PositionTitle>Program Manager</PositionTitle>
     <Address>557 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SWhite@NoMailServer.com</Email>
     <PhoneNum>555-7445</PhoneNum>
     <FaxNum>555-9986</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>700000</mortgageAmount>
     <lastName>Green</lastName>
     <firstName>Steve</firstName>
     <SSN>55566688</SSN>
     <PositionTitle>Project Manager</PositionTitle>
     <Address>445 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SGreeb@NoMailServer.com</Email>
     <PhoneNum>555-2211</PhoneNum>
     <FaxNum>555-2221</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 </batch>
```

Observe que o elemento XML que inicia e termina cada registro de dados é `LoanRecord`. Esse elemento XML é referenciado pela lógica do aplicativo que gera vários arquivos.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-7}

Para criar vários arquivos de PDF com base em uma fonte de dados XML, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de saída.
1. Fazer referência a uma fonte de dados XML.
1. Defina as opções de tempo de execução de PDF.
1. Definir opções de tempo de execução de renderização.
1. Gere vários arquivos PDF.
1. Recuperar os resultados da operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir os arquivos adobe-utilities.jar e jbossall-client.jar pelos arquivos JAR específicos ao servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado.

**Criar um objeto do Cliente de saída**

Antes de executar programaticamente uma operação do Serviço de saída, você deve criar um objeto cliente do Serviço de saída. Se estiver usando a API Java, crie uma `OutputClient` objeto. Se você estiver usando a API de serviço Web de saída, crie uma `OutputServiceService` objeto.

**Fazer referência a uma fonte de dados XML**

Faça referência a uma fonte de dados XML que contém vários registros. Um elemento XML deve ser usado para separar os registros de dados. Por exemplo, na fonte de dados XML de exemplo mostrada anteriormente nesta seção, o elemento XML que separa registros de dados é nomeado como `LoanRecord`.

Um elemento XML deve existir para cada campo de formulário que você deseja preencher com dados. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML será ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos se todos os elementos XML forem especificados.

**Definir opções de tempo de execução de PDF**

Você deve definir as seguintes opções de tempo de execução para que o serviço de Saída crie com êxito vários arquivos com base em uma fonte de dados XML:

* **Muitos arquivos**: especifica se o serviço de saída cria um único documento ou vários documentos. Você pode especificar verdadeiro ou falso. Para criar um documento separado para cada registro de dados na fonte de dados XML, especifique verdadeiro.
* **URI do arquivo**: especifica o local dos arquivos gerados pelo serviço de Saída. Por exemplo, suponha que você especifique C:\\Adobe\forms\Loan.pdf. Nessa situação, o serviço de saída cria um arquivo chamado Loan.pdf e coloca o arquivo na pasta C:\\Adobe\forms. Quando existem vários arquivos, os nomes dos arquivos são Loan0001.pdf, Loan0002.pdf, Loan0003.pdf e assim por diante. Se você especificar um local de arquivo, os arquivos serão colocados no servidor e não no computador cliente.
* **Nome do registro**: especifica o nome do elemento XML na fonte de dados que separa os registros de dados. Por exemplo, na fonte de dados XML de exemplo mostrada anteriormente nesta seção, o elemento XML que separa os registros de dados é chamado de `LoanRecord`. (Em vez de definir a opção de tempo de execução Nome do registro, você pode definir o Nível do registro atribuindo a ele um valor numérico que indica o nível do elemento que contém registros de dados. No entanto, você pode definir somente o Nome do registro ou o Nível do registro. Não é possível definir ambos os valores.)

**Definir opções de tempo de execução de renderização**

É possível definir opções de tempo de execução de renderização ao criar vários arquivos. Embora essas opções não sejam obrigatórias (ao contrário das opções de tempo de execução de saída, que são obrigatórias), você pode executar tarefas como melhorar o desempenho do serviço de Saída. Por exemplo, você pode armazenar em cache o design do formulário que o serviço de Saída usa para melhorar o desempenho.

Quando o Serviço de saída processa registros em lote, ele lê dados que contêm vários registros de maneira incremental. Ou seja, o Serviço de saída lê os dados na memória e libera os dados conforme o lote de registros é processado. O serviço de saída carrega dados de maneira incremental quando uma das duas opções de tempo de execução é definida. Se você definir a opção de tempo de execução Nome do registro, o serviço de Saída lerá os dados de maneira incremental. Da mesma forma, se você definir a opção de tempo de execução Record Level como 2 ou superior, o serviço Output lerá os dados de maneira incremental.

Você pode controlar se o Serviço de saída executa carregamento incremental usando o `PDFOutputOptionsSpec` ou o `PrintedOutputOptionSpec` do objeto `setLazyLoading` método. Você pode passar o valor `false` para este método que desativa o carregamento incremental.

**Gerar vários arquivos PDF**

Depois de fazer referência a uma fonte de dados XML válida que contém vários registros de dados e definir opções de tempo de execução, você pode chamar o Serviço de saída, o que faz com que ele gere vários arquivos. Ao gerar vários registros, a variável `OutputResult` do objeto `getGeneratedDoc` o método retorna `null`.

**Recuperar os resultados da operação**

Depois que o Serviço de saída executa uma operação, ele retorna dados XML que especificam se a operação foi bem-sucedida. O XML a seguir é retornado pelo serviço de Saída. Nessa situação, o Serviço de saída gerou 42 documentos.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <printResult>
 <status>0</status>
 <requestId>4ad85f9e2</requestId>
 <context/>
 <messages>
 <message>Printed all 42 records successfully.</message>
 </messages>
 <printSpec>
 <input>
 <validated>true</validated>
 <dataFile recordIdField="" recordLevel="0" recordName="LoanRecord"/>
 <sniffRules lookAhead="300"/>
 <formDesign>Loan.xdp</formDesign>
 <contentRoot>C:\Adobe</contentRoot>
 <metadata-spec record="false"/>
 </input>
 <output>
 <format>PDF</format>
 <fileURI>C:\Adobe\forms\Loan.pdf</fileURI>
 <optionString>cacheenabled=true&padebug=false&linearpdf=false&pdfarevisionnumber=1&pdfaconformance=A&taggedpdf=false&TransactionTimeOut=180</optionString>
 <waitForResponse>true</waitForResponse>
 <outputStream>multiple</outputStream>
 </output>
 </printSpec>
 </printResult>
```

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Criar vários arquivos de PDF usando a API Java {#create-multiple-pdf-files-using-the-java-api}

Crie vários arquivos de PDF usando a API de saída (Java):

1. Incluir arquivos de projeto&quot;

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do projeto Java. .

1. Criar um objeto do Cliente de saída

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `OutputClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Fazer referência a uma fonte de dados XML

   * Criar um `java.io.FileInputStream` objeto que representa a fonte de dados XML que contém vários registros usando seu construtor e transmitindo um valor de cadeia de caracteres que especifica o local do arquivo XML.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Definir opções de tempo de execução de PDF

   * Criar um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção Muitos arquivos chamando o botão `PDFOutputOptionsSpec` do objeto `setGenerateManyFiles` método. Por exemplo, passe o valor `true` para instruir o Serviço de saída a criar um arquivo de PDF separado para cada registro na fonte de dados XML. (Se você passar `false`, o Serviço de saída gera um único documento de PDF que contém todos os registros).
   * Defina a opção File URI chamando o `PDFOutputOptionsSpec` do objeto `setFileUri` e transmitindo um valor de string que especifica o local dos arquivos gerados pelo serviço de Saída. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.
   * Defina a opção Nome do registro chamando o `OutputOptionsSpec` do objeto `setRecordName` e transmitindo um valor de string que especifica o nome do elemento XML na fonte de dados que separa os registros de dados. (Por exemplo, considere a fonte de dados XML mostrada anteriormente nesta seção. O nome do elemento XML que separa registros de dados é LoanRecord).

1. Definir opções de tempo de execução de renderização

   * Criar um `RenderOptionsSpec` usando seu construtor.
   * Armazene em cache o design do formulário para melhorar o desempenho do Serviço de saída chamando o `RenderOptionsSpec` do objeto `setCacheEnabled` e a passagem de um `Boolean` valor de `true`.

1. Gerar vários arquivos PDF

   Gere vários arquivos de PDF chamando o `OutputClient` do objeto `generatePDFOutput` e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de cadeia de caracteres que especifica o nome do design do formulário.
   * Um valor de cadeia de caracteres que especifica a raiz do conteúdo onde o design do formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário.

   A variável `generatePDFOutput` o método retorna um `OutputResult` objeto que contém os resultados da operação.

1. Recuperar os resultados da operação

   * Criar um `java.io.File` objeto que representa um arquivo XML que conterá os resultados do `generatePDFOutput` método. Verifique se a extensão do nome do arquivo é .xml.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo (certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `applyUsageRights` método).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): criação de vários arquivos PDF usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criar vários arquivos de PDF usando a API de serviço Web {#create-multiple-pdf-files-using-the-web-service-api}

Crie vários arquivos de PDF usando a API de saída (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de saída.

   * Criar um `OutputServiceClient` usando seu construtor padrão.
   * Criar um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `OutputServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fazer referência a uma fonte de dados XML.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` O objeto é usado para armazenar dados de formulário que contêm vários registros.
   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo XML que contém vários registros.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução de PDF.

   * Criar um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção Muitos arquivos atribuindo um valor booleano à variável `OutputOptionsSpec` do objeto `generateManyFiles` membro de dados. Por exemplo, atribuir o valor `true` a esse membro de dados para instruir o Serviço de saída a criar um arquivo de PDF separado para cada registro na fonte de dados XML. (Se você atribuir `false` para esse membro de dados, o Serviço de saída gera um único PDF que contém todos os registros).
   * Defina a opção de URI de arquivo atribuindo um valor de string que especifica o local do(s) arquivo(s) gerado(s) pelo serviço de saída para o `OutputOptionsSpec` do objeto `fileURI` membro de dados. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.
   * Defina a opção nome do registro atribuindo um valor de sequência de caracteres que especifique o nome do elemento XML na fonte de dados que separa os registros de dados do `OutputOptionsSpec` do objeto `recordName` membro de dados.
   * Defina a opção copies atribuindo um valor inteiro que especifica o número de cópias que o serviço de Saída gera para o `OutputOptionsSpec` do objeto `copies` membro de dados.

1. Definir opções de tempo de execução de renderização.

   * Criar um `RenderOptionsSpec` usando seu construtor.
   * Armazenar em cache o design do formulário para melhorar o desempenho do serviço de Saída atribuindo o valor `true` para o `RenderOptionsSpec` do objeto `cacheEnabled` membro de dados.

1. Gere vários arquivos PDF.

   Crie vários arquivos de PDF chamando o `OutputServiceService` do objeto `generatePDFOutput`e transmitindo os seguintes valores:

   * Um valor de enumeração TransformationFormat. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de cadeia de caracteres que especifica o nome do design do formulário.
   * Um valor de cadeia de caracteres que especifica a raiz do conteúdo onde o design do formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `BLOB` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário.
   * A `BLOB` objeto que é preenchido pelo `generatePDFOutput` método. A variável `generatePDFOutput` O método preenche esse objeto com metadados gerados que descrevem o documento.
   * A `BLOB` objeto que é preenchido pelo `generatePDFOutput` método. A variável `generatePDFOutput` O método preenche este objeto com os dados do resultado.
   * Um `OutputResult` objeto que contém os resultados da operação.

1. Recuperar os resultados da operação

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa um local de arquivo XML que contém dados de resultado. Verifique se a extensão do nome do arquivo é .xml.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi preenchido com dados de resultado pelo `OutputServiceService` do objeto `generatePDFOutput` (o oitavo parâmetro). Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `binaryData` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes no arquivo XML chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Criação de regras de pesquisa {#creating-search-rules}

Você pode criar regras de pesquisa que resultam no serviço de Saída examinando dados de entrada e usando diferentes designs de formulário com base no conteúdo dos dados para gerar a saída. Por exemplo, se o texto *hipoteca* estiver localizado nos dados de entrada, o Serviço de saída poderá usar um design de formulário chamado Mortgage.xdp. Da mesma forma, se o texto *automóvel* estiver localizado nos dados de entrada, o Serviço de saída poderá usar um design de formulário salvo como AutomobileLoan.xdp. Embora o Serviço de saída possa gerar diferentes tipos de saída, esta seção presume que o Serviço de saída gera um arquivo PDF. O diagrama a seguir mostra o Serviço de saída gerando um arquivo de PDF, processando um arquivo de dados XML e usando um dos vários designs de formulário.

Além disso, o Serviço de saída é capaz de gerar pacotes de documentos, em que vários registros são fornecidos no conjunto de dados e cada registro é correspondido a um design de formulário, e um único documento é gerado composto de vários designs de formulário.

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-8}

Para instruir o Serviço de saída a usar regras de pesquisa ao gerar um documento, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de saída.
1. Fazer referência a uma fonte de dados XML.
1. Defina as regras de pesquisa.
1. Defina as opções de tempo de execução de PDF.
1. Definir opções de tempo de execução de renderização.
1. Gere um documento PDF.
1. Recuperar os resultados da operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, você precisará substituir adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos para o servidor de aplicativos J2EE no qual o AEM Forms é implantado.

**Criar um objeto do Cliente de saída**

Antes de executar programaticamente uma operação do Serviço de saída, você deve criar um objeto cliente do Serviço de saída.

**Fazer referência a uma fonte de dados XML**

Um elemento XML deve existir para cada campo de formulário que você deseja preencher com dados. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML será ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos, desde que todos os elementos XML sejam especificados.

**Definir regras de pesquisa**

Para definir regras de pesquisa, defina um ou mais padrões de texto que os serviços de Saída pesquisam nos dados de entrada. Para cada padrão de texto definido, especifique um design de formulário correspondente que será usado se o padrão de texto estiver localizado. Se um padrão de texto estiver localizado, o serviço de Saída usará o design de formulário correspondente para gerar a saída. Um exemplo de padrão de texto é *hipoteca*.

>[!NOTE]
>
>Se os padrões de texto não estiverem localizados, o formulário padrão será usado. Verifique se todos os designs de formulário que você usa estão localizados na raiz do conteúdo.

**Definir opções de tempo de execução de PDF**

Defina as seguintes opções de tempo de execução de PDF para que o serviço de Saída crie com êxito um documento de PDF com base em vários designs de formulário:

* **URI do arquivo**: especifica o nome e o local do arquivo de PDF gerado pelo serviço de Saída.
* **Regras**: especifica as regras que você definiu.
* **LookAHead**: especifica o número de bytes a serem usados desde o início do arquivo de dados de entrada para verificar os padrões de texto definidos. O padrão é 500 bytes.

**Definir opções de tempo de execução de renderização**

É possível definir opções de tempo de execução de renderização ao criar arquivos PDF. Embora essas opções não sejam necessárias (ao contrário das opções de tempo de execução de PDF), é possível executar tarefas como melhorar o desempenho do serviço de Saída. Por exemplo, você pode armazenar em cache o design do formulário que o serviço de Saída usa para melhorar o desempenho.

**Gerar um documento PDF**

Depois de fazer referência a uma fonte de dados XML válida e definir opções de tempo de execução, você pode chamar o serviço de Saída, o que gera um documento PDF. Se o serviço de Saída localizar um padrão de texto especificado nos dados de entrada, ele usará o design de formulário correspondente. Se um padrão de texto não for usado, o serviço de Saída usará o design de formulário padrão.

**Recuperar os resultados da operação**

Depois que o Serviço de saída executa uma operação, ele retorna dados XML que especificam se a operação foi bem-sucedida.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Criar regras de pesquisa usando a API Java {#create-search-rules-using-the-java-api}

Crie regras de pesquisa usando a API de saída (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente de saída.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `OutputClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Fazer referência a uma fonte de dados XML.

   * Criar um `java.io.FileInputStream` objeto que representa a fonte de dados XML usada para preencher o documento PDF usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XML.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Defina as regras de pesquisa.

   * Criar um `Rule` usando seu construtor.
   * Defina um padrão de texto chamando o `Rule` do objeto `setPattern` e transmitindo um valor de string que especifica um padrão de texto.
   * Defina o design do formulário correspondente chamando o `Rule` do objeto `setForm` método . Transmita um valor de cadeia de caracteres que especifique o nome do design do formulário.

   >[!NOTE]
   >
   >Para cada padrão de texto que deseja definir, repita as três subetapas anteriores.

   * Criar um `java.util.List` usando um `java.util.ArrayList` construtor.
   * Para cada `Rule` objeto que você criou, chame o `java.util.List` do objeto `add` e transmita o `Rule` objeto.

1. Defina as opções de tempo de execução de PDF.

   * Criar um `PDFOutputOptionsSpec` usando seu construtor.
   * Especifique o nome e o local do arquivo de PDF que o serviço de Saída gera chamando o `PDFOutputOptionsSpec` do objeto `setFileURI` método. Transmita um valor de string que especifique o local do arquivo de PDF. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.
   * Defina as regras que você definiu chamando o `PDFOutputOptionsSpec` do objeto `setRules` método. Passe o `java.util.List` objeto que contém o `Rule` objetos.
   * Defina o número de bytes para procurar os padrões de texto definidos, chamando o `PDFOutputOptionsSpec` do objeto `setLookAhead` método. Transmita um valor inteiro que represente os números de bytes.

1. Definir opções de tempo de execução de renderização.

   * Criar um `RenderOptionsSpec` usando seu construtor.
   * Armazene em cache o design do formulário para melhorar o desempenho do Serviço de saída chamando o `RenderOptionsSpec` do objeto `setCacheEnabled` e transmitindo `true`.

1. Gere um documento PDF.

   Gere um documento de PDF que seja baseado em vários designs de formulário chamando o `OutputClient` do objeto `generatePDFOutput` e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de sequência de caracteres que especifica o nome do design do formulário padrão. Ou seja, o design do formulário usado se um padrão de texto não estiver localizado.
   * Um valor de sequência de caracteres que especifica a raiz de conteúdo onde os designs de formulário estão localizados.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `com.adobe.idp.Document` objeto que contém os dados de formulário que são pesquisados pelo serviço de Saída para os padrões de texto definidos.

   A variável `generatePDFOutput` o método retorna um `OutputResult` objeto que contém os resultados da operação.

1. Recuperar os resultados da operação.

   * Criar um `com.adobe.idp.Document` objeto que representa o status do `generatePDFOutput` ao invocar o `OutputResult` do objeto `getStatusDoc` método.
   * Criar um `java.io.File` objeto que conterá os resultados da operação. Verifique se a extensão do arquivo é .xml.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` método para copiar o conteúdo do `com.adobe.idp.Document` ao arquivo (certifique-se de usar o `com.adobe.idp.Document` objeto que foi retornado pelo `getStatusDoc` método).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): criando regras de pesquisa usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Início rápido (modo SOAP): criação de regras de pesquisa usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criar regras de pesquisa usando a API de serviço Web {#create-search-rules-using-the-web-service-api}

Crie regras de pesquisa usando a API de saída (serviço Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de saída.

   * Criar um `OutputServiceClient` usando seu construtor padrão.
   * Criar um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `OutputServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fazer referência a uma fonte de dados XML.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` O objeto é usado para armazenar dados que serão mesclados com o documento PDF.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF a ser criptografado e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Defina as regras de pesquisa.

   * Criar um `Rule` usando seu construtor.
   * Defina um padrão de texto atribuindo um valor de string que especifique um padrão de texto para o `Rule` do objeto `pattern` membro de dados.
   * Defina o design do formulário correspondente atribuindo um valor de sequência de caracteres que especifique o design do formulário ao `Rule` do objeto `form` membro de dados.

   >[!NOTE]
   >
   >Para cada padrão de texto que deseja definir, repita as três subetapas anteriores.

   * Criar um `MyArrayOf_xsd_anyType` objeto que armazena as regras.
   * Atribuir cada `Rule` a um elemento da variável `MyArrayOf_xsd_anyType` matriz. Chame o `MyArrayOf_xsd_anyType` do objeto `Add` para cada `Rule` objeto.

1. Definir opções de tempo de execução de PDF

   * Criar um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção de URI de arquivo atribuindo um valor de string que especifica o local do arquivo de PDF gerado pelo serviço de saída para o `PDFOutputOptionsSpec` do objeto `fileURI` membro de dados. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.
   * Defina a opção copies atribuindo um valor inteiro que especifica o número de cópias que o serviço de Saída gera para o `PDFOutputOptionsSpec` do objeto `copies` membro de dados.
   * Defina as regras que você definiu atribuindo a variável `MyArrayOf_xsd_anyType` objeto que armazena as regras para o `PDFOutputOptionsSpec` do objeto `rules` membro de dados.
   * Defina o número de bytes a serem examinados em busca dos padrões de texto definidos, atribuindo um valor inteiro que represente os números de bytes a serem examinados na variável `PDFOutputOptionsSpec` do objeto `lookAhead` método de dados.

1. Definir opções de tempo de execução de renderização

   * Criar um `RenderOptionsSpec` usando seu construtor.
   * Armazenar em cache o design do formulário para melhorar o desempenho do serviço de Saída atribuindo o valor `true` para o `RenderOptionsSpec` do objeto `cacheEnabled` membro de dados.

   >[!NOTE]
   >
   >Não é possível definir a versão do documento PDF usando o `RenderOptionsSpec` do objeto `pdfVersion` membro se o documento de entrada for um formulário Acrobat. O documento PDF de saída retém a versão PDF do formulário Acrobat. Da mesma forma, não é possível definir a opção PDF com tags usando o `RenderOptionsSpec` do objeto `taggedPDF` se o documento de entrada for um formulário Acrobat.

   >[!NOTE]
   >
   >Não é possível definir a opção de PDF linearizado usando o `RenderOptionsSpec` do objeto `linearizedPDF` membro se o documento de PDF de entrada for certificado ou assinado digitalmente. Para obter informações, consulte [Assinatura digital de documentos PDF](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).

1. Gerar um documento PDF

   Crie um documento PDF chamando o `OutputServiceService` do objeto `generatePDFOutput`e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de cadeia de caracteres que especifica o nome do design do formulário.
   * Um valor de cadeia de caracteres que especifica a raiz do conteúdo onde o design do formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `BLOB` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário.
   * A `BLOB` objeto que é preenchido pelo `generatePDFOutput` método. A variável `generatePDFOutput` O método preenche esse objeto com metadados gerados que descrevem o documento. (Este valor de parâmetro é necessário somente para a invocação do serviço Web).
   * A `BLOB` objeto que é preenchido pelo `generatePDFOutput` método. A variável `generatePDFOutput` O método preenche este objeto com os dados do resultado. (Este valor de parâmetro é necessário somente para a invocação do serviço Web).
   * Um `OutputResult` objeto que contém os resultados da operação. (Este valor de parâmetro é necessário somente para a invocação do serviço Web).

   >[!NOTE]
   >
   >Ao gerar um documento PDF chamando o `generatePDFOutput` esteja ciente de que não é possível mesclar dados com um formulário PDF XFA que esteja assinado, certificado ou contenha direitos de uso. Para obter informações sobre direitos de uso, consulte [Aplicação de direitos de uso a documentos PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).

1. Recuperar os resultados da operação

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa um local de arquivo XML que contém dados de resultado. Certifique-se de que a extensão do arquivo seja XML.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi preenchido com dados de resultado pelo `OutputServiceService` do objeto `generatePDFOutput` (o oitavo parâmetro). Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes no arquivo XML chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Nivelamento de documentos PDF {#flattening-pdf-documents}

Você pode usar o Serviço de saída para transformar um documento PDF interativo em um PDF não interativo. Um documento PDF interativo permite que os usuários insiram ou modifiquem dados que estejam nos campos do documento PDF. O processo de transformação de um documento PDF interativo em um documento PDF não interativo é chamado de *achatamento*. Quando um documento PDF é nivelado, o usuário não pode modificar os dados nos campos do documento. Um motivo para nivelar um documento PDF é garantir que os dados não possam ser modificados.

Você pode nivelar os seguintes tipos de documentos PDF:

* Documentos PDF XFA interativos
* Acrobat Forms

A tentativa de nivelar um PDF que é um documento PDF não interativo causa uma exceção.

>[!NOTE]
>
>Para obter mais informações sobre o Serviço de saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-9}

Para nivelar um documento PDF interativo em um documento PDF não interativo, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Crie um objeto Cliente de saída.
1. Recupere um documento PDF interativo.
1. Transforme o documento PDF.
1. Salve o documento PDF não interativo como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (necessário se o AEM Forms for implantado no JBoss)
* jbossall-client.jar (necessário se o AEM Forms for implantado no JBoss)

se o AEM Forms for disponibilizado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir os arquivos adobe-utilities.jar e jbossall-client.jar pelos arquivos JAR específicos ao servidor de aplicativos J2EE no qual o AEM Forms é disponibilizado. Para obter informações sobre a localização de todos os arquivos JAR do AEM Forms, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto do Cliente de saída**

Antes de executar programaticamente uma operação do Serviço de saída, você deve criar um objeto cliente do Serviço de saída. Se estiver usando a API Java, crie uma `OutputClient` objeto. Se você estiver usando a API de serviço Web de saída, crie uma `OutputServiceService` objeto.

**Recuperar um documento PDF interativo**

Recupere um documento PDF interativo que você deseja transformar em um documento PDF não interativo. A tentativa de transformar um documento PDF não interativo causa uma exceção.

**Transforme o documento PDF**

Após recuperar um documento PDF interativo, é possível transformá-lo em um documento PDF não interativo. O serviço de Saída retorna um documento PDF não interativo.

**Salve o documento PDF não interativo como um arquivo PDF**

Você pode salvar o documento PDF não interativo como um arquivo PDF.

**Consulte também**

[Nivelar um documento PDF usando a API Java](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[Nivelar um documento PDF usando a API de serviço Web](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início Rápido da API de Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Nivelar um documento PDF usando a API Java {#flatten-a-pdf-document-using-the-java-api}

Nivelar um documento PDF interativo em um documento PDF não interativo usando a API de saída (Java):

1. Incluir arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do projeto Java.

1. Crie um objeto Cliente de saída.

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `OutputClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recupere um documento PDF interativo.

   * Criar um `java.io.FileInputStream` objeto que representa o documento PDF interativo a ser transformado usando seu construtor e transmitindo um valor de string que especifica o local do arquivo PDF interativo.
   * Criar um `com.adobe.idp.Document` usando seu construtor e transmitindo o `java.io.FileInputStream` objeto.

1. Transforme o documento PDF.

   Transforme o documento PDF interativo em um documento PDF não interativo chamando o `OutputServiceService` do objeto `transformPDF` e transmitindo os seguintes valores:

   * A variável `com.adobe.idp.Document` objeto que contém o documento PDF interativo.
   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF não interativo, especifique `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` valor de enumeração que especifica o número da revisão. Como esse parâmetro se destina a um documento PDF/A, você pode especificar `null`.
   * Um valor de sequência de caracteres que representa o número da alteração e o ano, separados por dois pontos. Como esse parâmetro se destina a um documento PDF/A, você pode especificar `null`.
   * A `PDFAConformance` valor de enumeração que representa o nível de conformidade PDF/A. Como esse parâmetro se destina a um documento PDF/A, você pode especificar `null`.

   A variável `transformPDF` o método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo como um arquivo PDF.

   * Criar um `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `Document` do objeto `copyToFile` método para copiar o conteúdo do `Document` ao arquivo (certifique-se de usar o `Document` objeto que foi retornado pelo `transformPDF` método).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): transformação de um documento PDF usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Início rápido (modo SOAP): transformação de um documento PDF usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Nivelar um documento PDF usando a API de serviço Web {#flatten-a-pdf-document-using-the-web-service-api}

Nivelar um documento PDF interativo em um documento PDF não interativo usando a API de saída (serviço da Web):

1. Incluir arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda o AEM Forms.

1. Crie um objeto Cliente de saída.

   * Criar um `OutputServiceClient` usando seu construtor padrão.
   * Criar um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `OutputServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF interativo.

   * Criar um `BLOB` usando seu construtor. A variável `BLOB` objeto é usado para armazenar o documento PDF interativo.
   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF interativo.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo o `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo invocando o `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo para leitura.
   * Preencha o `BLOB` atribuindo seu `MTOM` com o conteúdo da matriz de bytes.

1. Transforme o documento PDF.

   Transforme o documento PDF interativo em um documento PDF não interativo chamando o `OutputClient` do objeto `transformPDF` e transmitindo os seguintes valores:

   * A `BLOB` objeto que contém o documento PDF interativo.
   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF não interativo, especifique `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` valor de enumeração que especifica o número da revisão.
   * Um valor booliano que especifica se a variável `PDFARevisionNumber` valor enum é usado. Como esse parâmetro se destina a um documento PDF/A, você pode especificar `false`.
   * Um valor de sequência de caracteres que representa o número da alteração e o ano, separados por dois pontos. Como esse parâmetro se destina a um documento PDF/A, você pode especificar `null`.
   * A `PDFAConformance` valor de enumeração que representa o nível de conformidade PDF/A.
   * Valor booleano que especifica se a variável `PDFAConformance` valor enum é usado. Como esse parâmetro se destina a um documento PDF/A, você pode especificar `false`.

   A variável `transformPDF` o método retorna um `BLOB` objeto que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo como um arquivo PDF.

   * Criar um `System.IO.FileStream` chamando seu construtor e transmitindo um valor de string que representa o local do arquivo do documento PDF não interativo.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi retornado pelo `transformPDF` método. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
