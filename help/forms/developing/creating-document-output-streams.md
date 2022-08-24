---
title: Criando Fluxos de Saída de Documento
seo-title: Creating Document Output Streams
description: Use o serviço de Saída para converter documentos como PDF (incluindo documentos PDF/A), PostScript, PCL (Printer Control Language) e Zebra - ZPL, Intermeca - IPL, Datamax - DPL, e TecToshiba - formatos de etiqueta TPCL.
seo-description: Use the Output service to convert documents as PDF (including PDF/A documents), PostScript, Printer Control Language (PCL), and Zebra - ZPL, Intermec - IPL, Datamax - DPL, and TecToshiba - TPCL label formats.
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '19016'
ht-degree: 0%

---

# Criando Fluxos de Saída de Documento  {#creating-document-output-streams}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

**Sobre o serviço de saída**

O serviço de saída permite a saída de documentos como PDF (incluindo documentos PDF/A), PostScript, PCL (Printer Control Language) e os seguintes formatos de etiqueta:

* Zebra - ZPL
* Interfaces - IPL
* Datamax - DPL
* TecToshiba - TPCL

Usando o serviço Saída, é possível mesclar dados de formulário XML com um design de formulário e enviar o documento para uma impressora ou arquivo de rede.

Há duas maneiras de passar um design de formulário (um arquivo XDP) para o serviço de saída. Você pode passar uma `com.adobe.idp.Document` instância que contém um design de formulário para o serviço Saída. Ou você pode passar um valor de URI que especifica o local do design de formulário. Ambas as maneiras são discutidas em *Programação com formulários AEM*.

>[!NOTE]
>
>O serviço de saída não oferece suporte a documentos do Acroform PDF que contêm scripts específicos de objeto de aplicativo. Os documentos do Acroform PDF que contêm scripts específicos de objeto de aplicativo não são renderizados.

As seções a seguir mostram como passar um design de formulário para o serviço de saída usando um valor de URI:

* [Criação de documentos do PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Criação de documentos do PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)

As seções a seguir mostram como passar um design de formulário em um `com.adobe.idp.Document` instância:

* [Passar documentos localizados em Serviços de conteúdo (obsoleto) para o Serviço de saída](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Criação de documentos do PDF usando fragmentos](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

Uma consideração ao decidir qual técnica usar é se você estiver obtendo o design de formulário de outro serviço da AEM Forms e, em seguida, passá-lo em um `com.adobe.idp.Document` instância. Ambos os *Enviar documentos para o serviço de saída* e *Criação de documentos do PDF usando fragmentos* As seções mostram como obter um design de formulário de outro serviço da AEM Forms. A primeira seção recupera o design de formulário do Content Services (obsoleto). A segunda seção recupera o design de formulário do serviço Assembler.

Se o design de formulário estiver sendo obtido em um local fixo, como o sistema de arquivos, é possível usar qualquer técnica. Ou seja, você pode especificar o valor do URI para um arquivo XDP ou usar um `com.adobe.idp.Document` instância.

Para transmitir um valor de URI que especifica o local do design de formulário ao criar um documento PDF, use a variável `generatePDFOutput` método . Da mesma forma, para passar uma `com.adobe.idp.Document` para o serviço de saída ao criar um documento PDF, use o `generatePDFOutput2` método .

Ao enviar um fluxo de saída para uma impressora de rede, você também pode usar qualquer técnica. Para enviar um fluxo de saída para uma impressora passando uma `com.adobe.idp.Document` instância que contém um design de formulário, use a `sendToPrinter2`método . Para enviar um fluxo de saída para uma impressora transmitindo um valor de URI, use o `sendToPrinter`método . O *Enviando fluxos de impressão para impressoras* A seção usa a variável `sendToPrinter` método .

Você pode realizar essas tarefas usando o Serviço de saída:

* [Criação de documentos do PDF](creating-document-output-streams.md#creating-pdf-documents)
* [Criação de documentos do PDF/A](creating-document-output-streams.md#creating-pdf-a-documents)
* [Passar documentos localizados em Serviços de conteúdo (obsoleto) para o Serviço de saída](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [Criação de documentos do PDF usando fragmentos](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [Imprimindo em Arquivos](creating-document-output-streams.md#printing-to-files)
* [Enviando fluxos de impressão para impressoras](creating-document-output-streams.md#sending-print-streams-to-printers)
* [Criação de vários arquivos de saída](creating-document-output-streams.md#creating-multiple-output-files)
* [Criando regras de pesquisa](creating-document-output-streams.md#creating-search-rules)
* [Nivelar documentos do PDF](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Criação de documentos do PDF {#creating-pdf-documents}

Você pode usar o Serviço de saída para criar um documento PDF baseado em um design de formulário e dados de formulário XML fornecidos. O documento PDF criado pelo serviço de saída não é um documento PDF interativo; um usuário não pode inserir ou modificar dados de formulário.

Se quiser criar um documento PDF para armazenamento de longo prazo, é recomendável criar um documento PDF/A. (Consulte [Criação de documentos do PDF/A](creating-document-output-streams.md#creating-pdf-a-documents).)

Para criar um formulário PDF interativo que permita ao usuário inserir dados, use o serviço Forms. (Consulte [Renderização de PDF forms interativos](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms).)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para criar um documento PDF, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto de Cliente de saída.
1. Faça referência a uma fonte de dados XML.
1. Defina as opções de tempo de execução do PDF.
1. Defina as opções de tempo de execução da renderização.
1. Gere um documento PDF.
1. Recupere os resultados da operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado.

**Criar um objeto de cliente de saída**

Antes de poder executar programaticamente uma operação do Serviço de saída, é necessário criar um objeto cliente do Serviço de saída. Se estiver usando a API do Java, crie um `OutputClient` objeto. Se estiver usando a API de serviço da Web de saída, crie um `OutputServiceService` objeto.

**Referência a uma fonte de dados XML**

Para unir dados ao design de formulário, é necessário referenciar uma fonte de dados XML que contenha dados. Um elemento XML deve existir para cada campo de formulário que você planeja preencher com dados. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML é ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos se todos os elementos XML forem especificados.

Considere o seguinte exemplo de formulário de pedido de empréstimo.

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

Para unir dados nesse design de formulário, é necessário criar uma fonte de dados XML que corresponda ao formulário. O XML a seguir representa uma fonte de dados XML XDP que corresponde ao formulário de aplicativo de hipoteca de exemplo.

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

**Definir opções de tempo de execução PDF**

Defina a opção URI do arquivo ao criar um documento PDF. Essa opção especifica o nome e o local do arquivo PDF gerado pelo serviço de saída.

>[!NOTE]
>
>Em vez de definir a opção de tempo de execução do URI de arquivo, você pode recuperar programaticamente o documento do PDF do tipo de dados complexo retornado pelo serviço de saída. No entanto, ao definir a opção de tempo de execução do URI de arquivo, não é necessário criar uma lógica de aplicativo que recupere programaticamente o documento PDF.

**Definir opções de tempo de execução de renderização**

Você pode definir opções de tempo de execução de renderização ao criar um documento PDF. Embora essas opções não sejam necessárias (ao contrário das opções de tempo de execução de PDF necessárias), é possível executar tarefas como melhorar o desempenho do serviço de Saída. Por exemplo, é possível armazenar em cache o design de formulário que o serviço de saída usa para melhorar seu desempenho.

Se você usar um formulário Acrobat marcado como entrada, não poderá usar o Java do serviço de saída ou a API do serviço da Web para desativar a configuração marcada. Se você tentar definir programaticamente essa opção como `false`, o documento PDF de resultado ainda será marcado.

>[!NOTE]
>
>Se você não especificar as opções de tempo de execução de renderização, os valores padrão serão usados. Para obter informações sobre as opções de tempo de execução de renderização, consulte o `RenderOptionsSpec` referência de classe. (Consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)).

**Gerar um documento PDF**

Depois de fazer referência a uma fonte de dados XML válida que contém dados de formulário e definir opções de tempo de execução, você pode chamar o serviço Saída, o que resulta na geração de um documento PDF.

Ao gerar um documento PDF, você especifica os valores de URI que são exigidos pelo serviço de saída para criar um documento PDF. Um design de formulário pode ser armazenado em locais como o sistema de arquivos do servidor ou como parte de um aplicativo AEM Forms. Um design de formulário (ou outros recursos, como um arquivo de imagem) que existe como parte de um aplicativo Forms pode ser referenciado usando o valor de URI raiz de conteúdo `repository:///`. Por exemplo, considere o seguinte design de formulário chamado *Loan.xdp* localizado em um aplicativo Forms chamado *Aplicativos/FormsApplication*:

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

Para acessar o arquivo Loan.xdp mostrado na ilustração anterior, especifique `repository:///Applications/FormsApplication/1.0/FormsFolder/` como o terceiro parâmetro passado para o `OutputClient` do objeto `generatePDFOutput` método . Especifique o nome do formulário (*Loan.xdp*) como o segundo parâmetro passado para o `OutputClient` do objeto `generatePDFOutput` método .

Se o arquivo XDP contiver imagens (ou outros recursos, como fragmentos), coloque os recursos na mesma pasta de aplicativo que o arquivo XDP. O AEM Forms usa o URI raiz de conteúdo como o caminho base para resolver referências a imagens. Por exemplo, se o arquivo Loan.xdp contiver uma imagem, certifique-se de colocar a imagem em `Applications/FormsApplication/1.0/FormsFolder/`.

>[!NOTE]
>
>Você pode fazer referência a um URI de aplicativo do Forms ao chamar o `OutputClient` do objeto `generatePDFOutput` ou `generatePrintedOutput` métodos.

>[!NOTE]
>
>Para ver uma inicialização rápida completa que cria um documento do PDF referenciando um XDP localizado em um aplicativo Forms, consulte [Início rápido (modo EJB): Criação de um documento do PDF com base em um arquivo XDP do aplicativo usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api).

**Recuperar os resultados da operação**

Depois que o serviço de saída executa uma operação, ele retorna vários itens de dados, como dados de status XML, que especifica se a operação foi bem-sucedida.

**Consulte também**

[Criar um documento do PDF usando a API do Java](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[Criar um documento do PDF usando a API do serviço da Web](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Criar um documento do PDF usando a API do Java {#create-a-pdf-document-using-the-java-api}

Crie um documento do PDF usando a API de saída (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de Cliente de saída.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `OutputClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Faça referência a uma fonte de dados XML.

   * Crie um `java.io.FileInputStream` objeto que representa a fonte de dados XML usada para preencher o documento PDF usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XML.
   * Crie um `com.adobe.idp.Document` usando seu construtor. Passe o `java.io.FileInputStream` objeto.

1. Defina as opções de tempo de execução do PDF.

   * Crie um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção Arquivo URI chamando o `PDFOutputOptionsSpec` do objeto `setFileURI` método . Passe um valor de string que especifica o local do arquivo PDF gerado pelo serviço de saída. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.

1. Defina as opções de tempo de execução da renderização.

   * Crie um `RenderOptionsSpec` usando seu construtor.
   * Armazene em cache o design de formulário para melhorar o desempenho do serviço de saída, chamando a função `RenderOptionsSpec` do objeto `setCacheEnabled` e a passagem `true`.

   >[!NOTE]
   >
   >Não é possível definir a versão do documento do PDF usando o `RenderOptionsSpec` do objeto `setPdfVersion` método se o documento de entrada for um formulário Acrobat (um formulário criado no Acrobat) ou um documento XFA assinado ou certificado. O documento PDF de saída retém a versão PDF original. Da mesma forma, não é possível definir a opção Adobe PDF com tags chamando o `RenderOptionsSpec` do objeto `setTaggedPDF` método se o documento de entrada for um formulário Acrobat ou um documento XFA assinado ou certificado.

   >[!NOTE]
   >
   >Não é possível definir a opção PDF linearizado usando o `RenderOptionsSpec` do objeto `setLinearizedPDF` método se o documento PDF de entrada for certificado ou assinado digitalmente. (Consulte [Assinar documentos do PDF digitalmente ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Gere um documento PDF.

   Crie um documento do PDF chamando o `OutputClient` do objeto `generatePDFOutput` e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica o nome do design de formulário.
   * Um valor de string que especifica a raiz de conteúdo na qual o design de formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução do PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém dados para mesclar com o design de formulário.

   O `generatePDFOutput` retorna um método `OutputResult` que contém os resultados da operação.

   >[!NOTE]
   >
   >Ao gerar um documento PDF chamando o `generatePDFOutput` esteja ciente de que não é possível mesclar dados com um formulário PDF XFA assinado ou certificado. (Consulte [Assinar e certificar documentos digitalmente ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >O `OutputResult` do objeto `getRecordLevelMetaDataList` retornos de método `null`*.*

   >[!NOTE]
   >
   >Você também pode criar um documento do PDF chamando o `OutputClient` do objeto `generatePDFOutput2` método . (Consulte [Passar documentos localizados em Serviços de conteúdo (obsoleto) para o Serviço de saída ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. Recupere os resultados da operação.

   * Recuperar uma `com.adobe.idp.Document` objeto que representa o status do `generatePDFOutput` chamando a `OutputResult` do objeto `getStatusDoc` método . Este método retorna dados XML de status que especificam se a operação foi bem-sucedida.
   * Crie um `java.io.File` que contém os resultados da operação. Certifique-se de que a extensão do nome de arquivo seja .xml.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` para o arquivo (certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `getStatusDoc` método ).

   Embora o serviço de Saída grave o documento PDF no local especificado pelo argumento passado para a variável `PDFOutputOptionsSpec` do objeto `setFileURI` , você pode recuperar programaticamente o documento PDF/A chamando o `OutputResult` do objeto `getGeneratedDoc` método .

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): Criação de um documento do PDF usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Início rápido (modo SOAP): Criação de um documento do PDF usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criar um documento do PDF usando a API do serviço da Web {#create-a-pdf-document-using-the-web-service-api}

Crie um documento do PDF usando a API de saída (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto de Cliente de saída.

   * Crie um `OutputServiceClient` usando seu construtor padrão.
   * Crie um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `OutputServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a uma fonte de dados XML.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar dados XML que serão unidos ao documento PDF.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo XML que contém os dados do formulário.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Definir opções de tempo de execução PDF

   * Crie um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção File URI atribuindo um valor de string que especifica o local do arquivo de PDF que o serviço de saída gera para a variável `PDFOutputOptionsSpec` do objeto `fileURI` membro de dados. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.

1. Defina as opções de tempo de execução da renderização.

   * Crie um `RenderOptionsSpec` usando seu construtor.
   * Armazene em cache o design de formulário para melhorar o desempenho do serviço de Saída atribuindo o valor `true` para `RenderOptionsSpec` do objeto `cacheEnabled` membro de dados.

   >[!NOTE]
   >
   >Não é possível definir a versão do documento do PDF usando o `RenderOptionsSpec` do objeto `setPdfVersion` método se o documento de entrada for um formulário Acrobat (um formulário criado no Acrobat) ou um documento XFA assinado ou certificado. O documento PDF de saída retém a versão PDF original. Da mesma forma, não é possível definir a opção Adobe PDF com tags chamando o `RenderOptionsSpec` do objeto `setTaggedPDF`* método se o documento de entrada for um formulário Acrobat ou um documento XFA assinado ou certificado.*

   >[!NOTE]
   >
   >Não é possível definir a opção PDF linearizado usando o `RenderOptionsSpec` do objeto `linearizedPDF` membro se o documento PDF de entrada for certificado ou assinado digitalmente. (Consulte [Assinar documentos do PDF digitalmente ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. Gere um documento PDF.

   Crie um documento do PDF chamando o `OutputServiceService` do objeto `generatePDFOutput`e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica o nome do design de formulário.
   * Um valor de string que especifica a raiz de conteúdo na qual o design de formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução do PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `BLOB` objeto que contém a fonte de dados XML que contém dados para mesclar com o design de formulário.
   * A `BLOB` que é preenchido pela variável `generatePDFOutput` método . O `generatePDFOutput` O método preenche este objeto com metadados gerados que descrevem o documento. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).
   * A `BLOB` que é preenchido pela variável `generatePDFOutput` método . O `generatePDFOutput` O método preenche esse objeto com dados de resultado. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).
   * Um `OutputResult` que contém os resultados da operação. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).

   >[!NOTE]
   >
   >Ao gerar um documento PDF chamando o `generatePDFOutput` esteja ciente de que não é possível mesclar dados com um formulário PDF XFA assinado ou certificado. (Consulte [Assinar e certificar documentos digitalmente ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*.)*

   >[!NOTE]
   >
   >Você também pode criar um documento do PDF chamando o `OutputClient` do objeto `generatePDFOutput2` método . (Consulte [Passar documentos localizados em Serviços de conteúdo (obsoleto) para o Serviço de saída ](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*.)*

1. Recupere os resultados da operação.

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa um local de arquivo XML que contém dados de resultado. Certifique-se de que a extensão do nome de arquivo seja .xml.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi preenchido com dados de resultado pela variável `OutputServiceService` do objeto `generatePDFOutput` método (o oitavo parâmetro). Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` `field`.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes no arquivo XML chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

   Consulte também:

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >O `OutputServiceService` do objeto `generateOutput` está obsoleto.

## Criação de documentos do PDF/A {#creating-pdf-a-documents}

Você pode usar o Serviço de saída para criar um documento PDF/A. Como o PDF/A é um formato de arquivo para a preservação de longo prazo do conteúdo do documento, todas as fontes são incorporadas e o arquivo é descompactado. Como resultado, um documento PDF/A geralmente é maior do que um documento PDF padrão. Além disso, um documento PDF/A não contém conteúdo de áudio e vídeo. Assim como outras tarefas do Serviço de saída, você fornece um design de formulário e dados para mesclar com um design de formulário para criar um documento PDF/A.

A especificação PDF/A-1 consiste em dois níveis de conformidade, a saber, a e b. A grande diferença entre os dois é em relação ao suporte à estrutura lógica (acessibilidade), que não é necessário para o nível de conformidade b. Independentemente do nível de conformidade, PDF/A-1 determina que todas as fontes são incorporadas no documento PDF/A gerado.

Embora o PDF/A seja o padrão para arquivamento de documentos de PDF, não é obrigatório que o PDF/A seja usado para arquivamento se um documento PDF padrão atender às necessidades da sua empresa. O objetivo do padrão PDF/A é estabelecer um arquivo PDF que possa ser armazenado por um longo período, bem como atender aos requisitos de preservação de documentos. Por exemplo, um URL não pode ser incorporado em um PDF/A porque, com o tempo, o URL pode se tornar inválido.

Sua organização deve avaliar suas próprias necessidades, o tempo que você pretende manter o documento, as considerações de tamanho de arquivo e determinar sua própria estratégia de arquivamento. Você pode determinar programaticamente se um documento PDF é compatível com PDF/A usando o serviço DocConverter. (Consulte [Determinar de forma programática a conformidade do PDF/A](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

Um documento PDF/A deve usar a fonte especificada no design de formulário e as fontes não podem ser substituídas. Como resultado, se uma fonte localizada em um documento PDF não estiver disponível no sistema operacional do host (SO), ocorrerá uma exceção.

Quando um documento PDF/A é aberto no Acrobat, uma mensagem é exibida confirmando que o documento é um documento PDF/A, como mostrado na ilustração a seguir.

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>O site do AIIM tem uma seção Perguntas frequentes do PDF/A que você pode acessar [https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_65).

### Resumo das etapas {#summary_of_steps-1}

Para criar um documento PDF/A, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto de Cliente de saída.
1. Faça referência a uma fonte de dados XML.
1. Defina as opções de PDF/A de tempo de execução.
1. Defina as opções de tempo de execução da renderização.
1. Gere um documento PDF/A.
1. Recupere os resultados da operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo personalizado usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado.

**Criar um objeto de cliente de saída**

Antes de poder executar programaticamente uma operação do Serviço de saída, é necessário criar um objeto cliente do Serviço de saída. Se estiver usando a API do Java, crie um `OutputClient` objeto. Se estiver usando a API de serviço da Web de saída, crie um `OutputServiceService` objeto.

**Referência a uma fonte de dados XML**

Para unir dados ao design de formulário, é necessário referenciar uma fonte de dados XML que contenha dados. Um elemento XML deve existir para cada campo de formulário que você deseja preencher com dados. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML é ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos se todos os elementos XML forem especificados.

**Definir opções de tempo de execução PDF/A**

É possível definir a opção File URI ao criar um documento PDF/A. O URI é relativo ao servidor de aplicativos J2EE que hospeda o AEM Forms. Ou seja, se você definir C:\Adobe, o arquivo será gravado na pasta no servidor, não no computador cliente. O URI especifica o nome e o local do arquivo PDF/A gerado pelo serviço de saída.

**Definir opções de tempo de execução de renderização**

Você pode definir opções de tempo de execução de renderização ao criar documentos PDF/A. Duas opções relacionadas a PDF/A que você pode definir são as `PDFAConformance` e `PDFARevisionNumber` valores. O `PDFAConformance` valor refere-se à forma como um documento PDF adere a requisitos que especificam como os documentos eletrônicos de longo prazo são preservados. Valores válidos para esta opção são `A` e `B`. Para obter informações sobre a conformidade de nível a e b, consulte a especificação ISO PDF/A-1 que é intitulada *ISO 19005-1 Gerenciamento de documentos*.

O `PDFARevisionNumber` valor refere-se ao número de revisão de um documento PDF/A. Para obter informações sobre o número de revisão de um documento PDF/A, consulte a especificação ISO PDF/A-1 intitulada *ISO 19005-1 Gerenciamento de documentos*.

>[!NOTE]
>
>Não é possível definir a opção Adobe PDF com tags como `false` ao criar um documento PDF/A 1A. PDF/A 1A sempre será um documento de PDF marcado. Além disso, não é possível definir a opção Adobe PDF com tags como `true` ao criar um documento PDF/A 1B. PDF/A 1B sempre será um documento PDF não marcado.

**Gerar um documento PDF/A**

Depois de fazer referência a uma fonte de dados XML válida que contém dados de formulário e definir opções de tempo de execução, você pode chamar o serviço Saída, fazendo com que ele gere um documento PDF/A.

**Recuperar os resultados da operação**

Depois que o serviço de saída executa uma operação, ele retorna vários itens de dados, como dados XML, que especifica se a operação foi bem-sucedida.

**Consulte também**

[Criar um documento do PDF/A usando a API do Java](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[Criar um documento PDF/A usando a API do serviço da Web](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Criar um documento do PDF/A usando a API do Java {#create-a-pdf-a-document-using-the-java-api}

Crie um documento PDF/A usando a API de saída (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de Cliente de saída.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `OutputClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Faça referência a uma fonte de dados XML.

   * Crie um `java.io.FileInputStream` objeto que representa a fonte de dados XML usada para preencher o documento PDF/A usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XML.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Defina as opções de PDF/A de tempo de execução.

   * Crie um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção Arquivo URI chamando o `PDFOutputOptionsSpec` do objeto `setFileURI` método . Passe um valor de string que especifica o local do arquivo PDF gerado pelo serviço de saída. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.

1. Defina as opções de tempo de execução da renderização.

   * Crie um `RenderOptionsSpec` usando seu construtor.
   * Defina as `PDFAConformance` chamando o `RenderOptionsSpec` do objeto `setPDFAConformance` e a transmissão de um `PDFAConformance` valor enum que especifica o nível de conformidade. Por exemplo, para especificar o nível de conformidade A, passe `PDFAConformance.A`.
   * Defina as `PDFARevisionNumber` chamando o `RenderOptionsSpec` do objeto `setPDFARevisionNumber` método e aprovação `PDFARevisionNumber.Revision_1`.

   >[!NOTE]
   >
   >A versão PDF de um documento PDF/A é 1.4, independentemente do valor especificado para a variável `RenderOptionsSpec` do objeto `setPdfVersion`*método .*

1. Gere um documento PDF/A.

   Crie um documento PDF/A chamando o `OutputClient` do objeto `generatePDFOutput` e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF/A, especifique `TransformationFormat.PDFA`.
   * Um valor de string que especifica o nome do design de formulário.
   * Um valor de string que especifica a raiz de conteúdo na qual o design de formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução do PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém dados para mesclar com o design de formulário.

   O `generatePDFOutput` retorna um método `OutputResult` que contém os resultados da operação.

   >[!NOTE]
   >
   >O `OutputResult` do objeto `getRecordLevelMetaDataList` retornos de método `null`.

   >[!NOTE]
   >
   >Você também pode criar um documento PDF /A chamando o `OutputClient` do objeto `generatePDFOutput`método 2. (Consulte [Passar documentos localizados em Serviços de conteúdo (obsoleto) para o Serviço de saída](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. Recupere os resultados da operação.

   * Crie um `com.adobe.idp.Document` objeto que representa o status do `generatePDFOutput` chamando o método `OutputResult` do objeto `getStatusDoc` método .
   * Crie um `java.io.File` que conterá os resultados da operação. Certifique-se de que a extensão do nome de arquivo seja .xml.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` para o arquivo (certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `getStatusDoc` método ).

   >[!NOTE]
   >
   >Embora o serviço de Saída grave o documento PDF/A no local especificado pelo argumento passado para a variável `PDFOutputOptionsSpec` do objeto `setFileURI` , você pode recuperar programaticamente o documento PDF/A chamando o `OutputResult` do objeto `getGeneratedDoc` método .

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo SOAP): Criação de um documento do PDF/A usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Criar um documento PDF/A usando a API do serviço da Web {#create-a-pdf-a-document-using-the-web-service-api}

Crie um documento PDF/A usando a API de saída (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto de Cliente de saída.

   * Crie um `OutputServiceClient` usando seu construtor padrão.
   * Crie um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `OutputServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a uma fonte de dados XML.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar dados que serão unidos ao documento PDF/A.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento do PDF a ser criptografado e o modo no qual abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Defina as opções de PDF/A de tempo de execução.

   * Crie um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção File URI atribuindo um valor de string que especifica o local do arquivo de PDF que o serviço de saída gera para a variável `PDFOutputOptionsSpec` do objeto `fileURI` membro de dados. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente

1. Defina as opções de tempo de execução da renderização.

   * Crie um `RenderOptionsSpec` usando seu construtor.
   * Defina as `PDFAConformance` atribuindo um valor de `PDFAConformance` valor enum para a variável `RenderOptionsSpec` do objeto `PDFAConformance` membro de dados. Por exemplo, para especificar o nível de conformidade A, atribua `PDFAConformance.A` para esse membro de dados.
   * Defina as `PDFARevisionNumber` atribuindo um valor de `PDFARevisionNumber` valor enum para a variável `RenderOptionsSpec` do objeto `PDFARevisionNumber` membro de dados. Atribuir `PDFARevisionNumber.Revision_1` para esse membro de dados.

   >[!NOTE]
   >
   >A versão PDF de um documento PDF/A é 1.4, independentemente do valor especificado.

1. Gere um documento PDF/A.

   Crie um documento do PDF chamando o `OutputServiceService` do objeto `generatePDFOutput`e transmitindo os seguintes valores:

   * Um valor de enumeração TransformationFormat. Para gerar um documento PDF, especifique `TransformationFormat.PDFA`.
   * Um valor de string que especifica o nome do design de formulário.
   * Um valor de string que especifica a raiz de conteúdo na qual o design de formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução do PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `BLOB` objeto que contém a fonte de dados XML que contém dados para mesclar com o design de formulário.
   * A `BLOB` que é preenchido pela variável `generatePDFOutput` método . O `generatePDFOutput` O método preenche este objeto com metadados gerados que descrevem o documento. (Esse valor de parâmetro é necessário somente para invocação do serviço da Web.)
   * A `BLOB` que é preenchido pela variável `generatePDFOutput` método . O `generatePDFOutput` O método preenche esse objeto com dados de resultado. (Esse valor de parâmetro é necessário somente para invocação do serviço da Web.)
   * Um `OutputResult` que contém os resultados da operação. (Esse valor de parâmetro é necessário somente para invocação do serviço da Web.)

   >[!NOTE]
   >
   >Você também pode criar um documento PDF /A chamando o `OutputClient` do objeto `generatePDFOutput`método 2. (Consulte [Passar documentos localizados em Serviços de conteúdo (obsoleto) para o Serviço de saída](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service).)

1. Recupere os resultados da operação.

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa um local de arquivo XML que contém dados de resultado. Certifique-se de que a extensão do nome de arquivo seja .xml.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi preenchido com dados de resultado pela variável `OutputServiceService` do objeto `generatePDFOutput` método (o oitavo parâmetro). Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` campo.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes no arquivo XML chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Passar documentos localizados em Serviços de conteúdo (obsoleto) para o Serviço de saída {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

O serviço de saída renderiza um formulário PDF não interativo baseado em um design de formulário que normalmente é salvo como um arquivo XDP e criado no Designer. Você pode passar uma `com.adobe.idp.Document` objeto que contém o design de formulário para o serviço Saída. O serviço Output renderiza o design de formulário localizado na variável `com.adobe.idp.Document` objeto.

Uma vantagem de passar uma `com.adobe.idp.Document` O objeto para o serviço de saída é que outras operações do serviço AEM Forms retornam um `com.adobe.idp.Document` instância. Ou seja, você pode obter um `com.adobe.idp.Document` de outra operação de serviço e renderizá-la. Por exemplo, suponha que um arquivo XDP seja armazenado em um nó Content Services (obsoleto) chamado `/Company Home/Form Designs`, conforme mostrado na ilustração a seguir.

Você pode recuperar programaticamente o Loan.xdp dos Serviços de conteúdo (obsoleto) e passar o arquivo XDP para o serviço de saída em um `com.adobe.idp.Document` objeto.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-2}

Para passar um documento obtido dos Serviços de conteúdo (obsoleto) para o Serviço de saída, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto Output e uma API do cliente de gerenciamento de documentos.
1. Recupere o design de formulário do Content Services (obsoleto).
1. Renderize o formulário PDF não interativo.
1. Execute uma ação com o fluxo de dados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar uma saída e um objeto de API do cliente de gerenciamento de documentos**

Antes de executar programaticamente uma operação de API do serviço de saída, crie um objeto de API do cliente de saída. Além disso, como esse workflow recupera um arquivo XDP do Content Services (obsoleto), crie um objeto de API do Document Management.

**Recuperar o design do formulário do Content Services (obsoleto)**

Recupere o arquivo XDP do Content Services (obsoleto) usando a API do serviço da Web ou do Java. O arquivo XDP é retornado em um `com.adobe.idp.Document` instância (ou uma `BLOB` (se você estiver usando serviços da Web). Você pode passar o `com.adobe.idp.Document` para o serviço de saída.

**Renderizar o formulário PDF não interativo**

Para renderizar um formulário não interativo, passe o `com.adobe.idp.Document` instância que foi retornada do Content Services (obsoleto) para o serviço de saída.

>[!NOTE]
>
>Dois novos métodos nomeados `generatePDFOutput2`e g `eneratePrintedOutput2`aceite um `com.adobe.idp.Document` objeto que contém um design de formulário. Também é possível enviar uma `com.adobe.idp.Document`que contém o design de formulário para o serviço de saída ao enviar um fluxo de impressão para uma impressora de rede.

**Executar uma ação com o fluxo de dados do formulário**

É possível salvar o formulário não interativo como um arquivo PDF. O formulário pode ser exibido no Adobe Reader ou Acrobat.

**Consulte também**

[Passe documentos para o Serviço de saída usando a API Java](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[Passe documentos para o Serviço de saída usando a API de serviço da Web](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Criação de documentos do PDF usando fragmentos](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Passe documentos para o Serviço de saída usando a API Java {#pass-documents-to-the-output-service-using-the-java-api}

Passe um documento recuperado dos Serviços de conteúdo (obsoleto) usando o Serviço de saída e a API dos Serviços de conteúdo (obsoleto):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar e adobe-contentservices-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de saída e de API do cliente de gerenciamento de documentos.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão. (Consulte [Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um `OutputClient` usando seu construtor e passando o `ServiceClientFactory` objeto.
   * Crie um `DocumentManagementServiceClientImpl` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Recupere o design de formulário do Content Services (obsoleto).

   Chame o `DocumentManagementServiceClientImpl` do objeto `retrieveContent` e transmita os seguintes valores:

   * Um valor de string que especifica o armazenamento onde o conteúdo é adicionado. O armazenamento padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.

   O `retrieveContent` método retorna um `CRCResult` objeto que contém o arquivo XDP. Recuperar uma `com.adobe.idp.Document` chamando a `CRCResult` do objeto `getDocument` método .

1. Renderize o formulário PDF não interativo.

   Chame o `OutputClient` do objeto `generatePDFOutput2` e transmita os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica a raiz do conteúdo na qual os recursos adicionais, como imagens, estão localizados.
   * A `com.adobe.idp.Document` objeto que representa o design de formulário (use a instância retornada pelo `CRCResult` do objeto `getDocument` método ).
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução do PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém dados para mesclar com o design de formulário.

   O `generatePDFOutput2` retorna um método `OutputResult` que contém os resultados da operação.

1. Execute uma ação com o fluxo de dados do formulário.

   * Recuperar uma `com.adobe.idp.Document` objeto que representa o formulário não interativo chamando o `OutputResult` do objeto `getGeneratedDoc` método .
   * Crie um `java.io.File` que contém os resultados da operação. Certifique-se de que a extensão de nome de arquivo seja .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` para o arquivo (certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `getGeneratedDoc` método ).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): Passar documentos para o serviço de saída usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Início rápido (modo SOAP): Passar documentos para o serviço de saída usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Passe documentos para o Serviço de saída usando a API de serviço da Web {#pass-documents-to-the-output-service-using-the-web-service-api}

Passe um documento recuperado dos Serviços de conteúdo (obsoleto) usando o Serviço de saída e a API dos Serviços de conteúdo (obsoleto) (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Como esse aplicativo cliente chama dois serviços AEM Forms, crie duas referências de serviço. Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Saída: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Gerenciamento de documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Porque a variável `BLOB` o tipo de dados é comum a ambas as referências de serviço, qualifica totalmente a variável `BLOB` tipo de dados ao usá-lo. Na inicialização rápida do serviço da Web correspondente, todas as `BLOB` as instâncias são totalmente qualificadas.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto de saída e de API do cliente de gerenciamento de documentos.

   * Crie um `OutputServiceClient` usando seu construtor padrão.
   * Crie um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`). Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `OutputServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita essas etapas para a `DocumentManagementServiceClient`cliente de serviço.

1. Recupere o design de formulário do Content Services (obsoleto).

   Recupere o conteúdo chamando o `DocumentManagementServiceClient` do objeto `retrieveContent` e transmitindo os seguintes valores:

   * Um valor de string que especifica o armazenamento onde o conteúdo é adicionado. O armazenamento padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.
   * Um parâmetro de saída de string que armazena o valor do link de navegação.
   * A `BLOB` parâmetro de saída que armazena o conteúdo. Você pode usar esse parâmetro de saída para recuperar o conteúdo.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` parâmetro de saída que armazena atributos de conteúdo.
   * A `CRCResult` parâmetro de saída. Em vez de usar esse objeto, você pode usar a variável `BLOB` parâmetro de saída para recuperar o conteúdo.

1. Renderize o formulário PDF não interativo.

   Chame o `OutputServiceClient` do objeto `generatePDFOutput2` e transmita os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica a raiz do conteúdo na qual os recursos adicionais, como imagens, estão localizados.
   * A `BLOB` objeto que representa o design de formulário (use o `BLOB` instância retornada pelo Content Services (obsoleto).
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução do PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `BLOB` objeto que contém a fonte de dados XML que contém dados para mesclar com o design de formulário.
   * Uma saída `BLOB` que é preenchido pela variável `generatePDFOutput2` método . O `generatePDFOutput2` O método preenche este objeto com metadados gerados que descrevem o documento. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).
   * Uma saída `OutputResult` que contém os resultados da operação. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).

   O `generatePDFOutput2` método retorna um `BLOB` objeto que contém o formulário PDF não interativo.

1. Execute uma ação com o fluxo de dados do formulário.

   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento interativo do PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto recuperado do `generatePDFOutput2` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Transmitindo Documentos localizados no Repositório para o Serviço de Saída {#passing-documents-located-in-the-repository-to-the-output-service}

O serviço de saída renderiza um formulário PDF não interativo baseado em um design de formulário que normalmente é salvo como um arquivo XDP e criado no Designer. Você pode passar uma `com.adobe.idp.Document` objeto que contém o design de formulário para o serviço Saída. O serviço Output renderiza o design de formulário localizado na variável `com.adobe.idp.Document` objeto.

Uma vantagem de passar uma `com.adobe.idp.Document` O objeto para o serviço de saída é que outras operações do serviço AEM Forms retornam um `com.adobe.idp.Document` instância. Ou seja, você pode obter um `com.adobe.idp.Document` de outra operação de serviço e renderizá-la. Por exemplo, suponha que um arquivo XDP seja armazenado no repositório AEM Forms, conforme mostrado na ilustração a seguir.

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

O *FormsFolder* é um local definido pelo usuário no repositório AEM Forms (esse local é um exemplo e não existe por padrão). Neste exemplo, um design de formulário chamado Loan.xdp está localizado nesta pasta. Além do design de formulário, outras garantias de formulário, como imagens, podem ser armazenadas nesse local. O caminho para um recurso localizado no repositório do AEM Forms é:

`Applications/Application-name/Application-version/Folder.../Filename`

Você pode recuperar programaticamente o Loan.xdp do repositório do AEM Forms e passá-lo para o serviço de saída em um `com.adobe.idp.Document` objeto.

Você pode criar um PDF com base em um arquivo XDP localizado no repositório usando uma das duas maneiras. Você pode passar o local XDP por referência ou pode recuperar programaticamente o XDP do repositório e passá-lo para o serviço de saída em um arquivo XDP.

[Início rápido (modo EJB): Criação de um documento do PDF com base em um arquivo XDP do aplicativo usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) (mostra como passar o local do arquivo XDP por referência).

[Início rápido (modo EJB): Passar um documento localizado no Repositório AEM Forms para o serviço de saída usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (mostra como recuperar programaticamente o arquivo XDP do Repositório AEM Forms e passá-lo para o serviço de saída em um `com.adobe.idp.Document` instância). (Esta seção discute como executar essa tarefa)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-3}

Para passar um documento obtido do repositório AEM Forms para o serviço de saída, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto Output e uma API do cliente de gerenciamento de documentos.
1. Recupere o design de formulário do repositório do AEM Forms.
1. Renderize o formulário PDF não interativo.
1. Execute uma ação com o fluxo de dados.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar uma saída e um objeto de API do cliente de gerenciamento de documentos**

Antes de executar programaticamente uma operação de API do serviço de saída, crie um objeto de API do cliente de saída. Além disso, como esse workflow recupera um arquivo XDP do Content Services (obsoleto), crie um objeto de API do Document Management.

**Recuperar o design do formulário do Repositório AEM Forms**

Recupere o arquivo XDP do Repositório AEM Forms usando a API do Repositório. (Consulte [Lendo recursos](/help/forms/developing/aem-forms-repository.md#reading-resources).)

O arquivo XDP é retornado em um `com.adobe.idp.Document` instância (ou uma `BLOB` (se você estiver usando serviços da Web). Você pode passar o `com.adobe.idp.Document` instância do serviço de saída.

**Renderizar o formulário PDF não interativo**

Para renderizar um formulário não interativo, passe o `com.adobe.idp.Document` instância que foi retornada usando a API do Repositório AEM Forms.

>[!NOTE]
>
>Dois novos métodos nomeados `generatePDFOutput2`e `generatePrintedOutput2`aceite um `com.adobe.idp.Document`objeto que contém um design de formulário. Também é possível enviar uma `com.adobe.idp.Document` que contém o design de formulário para o serviço de saída ao enviar um fluxo de impressão para uma impressora de rede.

**Executar uma ação com o fluxo de dados do formulário**

É possível salvar o formulário não interativo como um arquivo PDF. O formulário pode ser exibido no Adobe Reader ou Acrobat.

**Consulte também**

[Passe documentos localizados no Repositório para o Serviço de Saída usando a API Java](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Passe documentos localizados no Repositório para o Serviço de Saída usando a API Java {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

Passe um documento recuperado do Repositório usando o serviço de saída e a API do repositório (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar e adobe-repository-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de saída e de API do cliente de gerenciamento de documentos.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão. (Consulte [Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um `OutputClient` usando seu construtor e passando o `ServiceClientFactory` objeto.
   * Crie um `DocumentManagementServiceClientImpl` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Recupere o design de formulário do AEM Forms Repository.

   Chame o `ResourceRepositoryClient` do objeto `readResourceContent` e transmita um valor de string que especifica o local do URI para o arquivo XDP. Por exemplo, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. Esse valor é obrigatório. Esse método retorna um `com.adobe.idp.Document` que representa o arquivo XDP.

1. Renderize o formulário PDF não interativo.

   Chame o `OutputClient` do objeto `generatePDFOutput2` e transmita os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica a raiz do conteúdo na qual os recursos adicionais, como imagens, estão localizados. Por exemplo, `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * A `com.adobe.idp.Document` objeto que representa o design de formulário (use a instância retornada pelo `ResourceRepositoryClient` do objeto `readResourceContent` método ).
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução do PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém dados para mesclar com o design de formulário.

   O `generatePDFOutput2` retorna um método `OutputResult` que contém os resultados da operação.

1. Execute uma ação com o fluxo de dados do formulário.

   * Recuperar uma `com.adobe.idp.Document` objeto que representa o formulário não interativo chamando o `OutputResult` do objeto `getGeneratedDoc` método .
   * Crie um `java.io.File` que contém os resultados da operação. Certifique-se de que a extensão de nome de arquivo seja .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` para o arquivo (certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `getGeneratedDoc` método ).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): Passar um documento localizado no Repositório AEM Forms para o serviço de saída usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Criação de documentos do PDF usando fragmentos {#creating-pdf-documents-using-fragments}

Você pode usar os serviços Saída e Assembler para criar um fluxo de saída, como um documento PDF, que é baseado em fragmentos. O serviço Assembler monta um documento XDP baseado em fragmentos localizados em vários arquivos XDP. O documento XDP montado é transmitido ao serviço de saída, que cria um documento PDF. Embora esse workflow mostre um documento PDF sendo gerado, o serviço de Saída pode gerar outros tipos de saída, como ZPL, para esse workflow. Um documento PDF é usado somente para fins de discussão.

A ilustração a seguir mostra esse workflow.

![cp_cp_outputassemblefragments](assets/cp_cp_outputassemblefragments.png)

Antes de ler *Criação de documentos do PDF usando fragmentos*, é recomendável que você se familiarize com o uso do serviço Assembler para reunir vários documentos XDP. (Consulte [Montagem de vários fragmentos XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments).)

>[!NOTE]
>
>Você também pode passar um design de formulário montado pelo serviço Assembler para o serviço Forms em vez do serviço Saída. A principal diferença entre o serviço de Saída e o serviço Forms é que o serviço Forms gera documentos PDF interativos e o serviço de Saída produz documentos PDF não interativos. Além disso, o serviço Forms não pode gerar fluxos de saída baseados em impressora como ZPL.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-4}

Para criar um documento PDF com base em fragmentos, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto Cliente de Saída e Assembler.
1. Use o serviço Assembler para gerar o design de formulário.
1. Use o Serviço de saída para gerar o documento PDF.
1. Salve o documento PDF como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de cliente de saída e de Assembler**

Antes de executar programaticamente uma operação de API do serviço de saída, crie um objeto de API do cliente de saída. Além disso, como esse fluxo de trabalho chama o serviço Assembler para criar o design de formulário, crie um objeto de API do cliente Assembler.

**Use o serviço Assembler para gerar o design de formulário**

Use o serviço Assembler para gerar o design de formulário usando fragmentos. O serviço Assembler retorna um `com.adobe.idp.Document` instância que contém o design de formulário.

**Usar o serviço de saída para gerar o documento PDF**

Você pode usar o Serviço de saída para gerar um documento PDF usando o design de formulário criado pelo serviço Assembler. Passe o `com.adobe.idp.Document` instância que o serviço Assembler retornou para o serviço Saída.

**Salve o documento PDF como um arquivo PDF**

Depois que o serviço de saída gera um documento PDF, você pode salvá-lo como um arquivo PDF.

**Consulte também**

[Criar um documento do PDF com base em fragmentos usando a API do Java](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[Criar um documento do PDF com base em fragmentos usando a API do serviço da Web](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[Montagem de vários fragmentos XDP](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[Criação de documentos do PDF](creating-document-output-streams.md#creating-pdf-documents)

### Criar um documento do PDF com base em fragmentos usando a API do Java {#create-a-pdf-document-based-on-fragments-using-the-java-api}

Crie um documento do PDF com base em fragmentos usando a API do serviço de saída e a API do serviço do Assembler (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto Cliente de Saída e Assembler.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `OutputClient` usando seu construtor e passando o `ServiceClientFactory` objeto.
   * Crie um `AssemblerServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Use o serviço Assembler para gerar o design de formulário.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e passe os seguintes valores obrigatórios:

   * A `com.adobe.idp.Document` objeto que representa o documento DDX a ser usado.
   * A `java.util.Map` objeto que contém os arquivos XDP de entrada.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objeto que especifica as opções de tempo de execução, incluindo a fonte padrão e o nível de log do trabalho.

   O `invokeDDX` método retorna um `com.adobe.livecycle.assembler.client.AssemblerResult` objeto que contém o documento XDP montado. Para recuperar o documento XDP montado, execute as seguintes ações:

   * Chame o `AssemblerResult` do objeto `getDocuments` método . Esse método retorna um `java.util.Map` objeto.
   * Iterar por meio do `java.util.Map` até encontrar o resultante `com.adobe.idp.Document` objeto.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para extrair o documento XDP montado.


1. Use o Serviço de saída para gerar o documento PDF.

   Chame o `OutputClient` do objeto `generatePDFOutput2` e transmita os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`
   * Um valor de string que especifica a raiz do conteúdo na qual os recursos adicionais, como imagens, estão localizados
   * A `com.adobe.idp.Document` objeto que representa o design de formulário (use a instância retornada pelo serviço Assembler)
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução PDF
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização
   * O `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém dados para mesclar com o design de formulário

   O `generatePDFOutput2` retorna um método `OutputResult` objeto que contém os resultados da operação

1. Salve o documento PDF como um arquivo PDF.

   * Recuperar uma `com.adobe.idp.Document` objeto que representa o documento PDF chamando o `OutputResult` do objeto `getGeneratedDoc` método .
   * Crie um `java.io.File` que contém os resultados da operação. Certifique-se de que a extensão do nome de arquivo seja .pdf.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` ao arquivo. (Certifique-se de usar a variável `com.adobe.idp.Document` que a variável `getGeneratedDoc` método retornado.)

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): Criação de um documento do PDF com base em fragmentos usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Início rápido (modo SOAP): Criação de um documento do PDF com base em fragmentos usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Criar um documento do PDF com base em fragmentos usando a API do serviço da Web {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

Crie um documento do PDF com base em fragmentos usando a API do Serviço de Saída e a API do Serviço do Assembler (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Saída:

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Use a seguinte definição WSDL para a referência de serviço associada ao serviço Assembler:

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   Porque a variável `BLOB` o tipo de dados é comum a ambas as referências de serviço, qualifica totalmente a variável `BLOB` tipo de dados ao usá-lo. Na inicialização rápida do serviço da Web correspondente, todas as `BLOB` as instâncias são totalmente qualificadas.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto Cliente de Saída e Assembler.

   * Crie um `OutputServiceClient` usando seu construtor padrão.
   * Crie um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `OutputServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribua o nome de usuário dos formulários AEM ao `OutputServiceClient.ClientCredentials.UserName.UserName`campo.
      * Atribua o valor da senha correspondente ao `OutputServiceClient.ClientCredentials.UserName.Password`campo.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` para `BasicHttpBindingSecurity.Transport.ClientCredentialType`campo.
   * Atribua o `BasicHttpSecurityMode.TransportCredentialOnly` valor constante para `BasicHttpBindingSecurity.Security.Mode`campo.

   >[!NOTE]
   >
   >Repita essas etapas para a `AssemblerServiceClient`objeto.

1. Use o serviço Assembler para gerar o design de formulário.

   Chame o `AssemblerServiceClient` do objeto `invokeDDX` e transmita os seguintes valores:

   * A `BLOB` objeto que representa o documento DDX
   * O `MyMapOf_xsd_string_To_xsd_anyType` objeto que contém os arquivos necessários
   * Um `AssemblerOptionSpec` objeto que especifica as opções de tempo de execução

   O `invokeDDX` retorna um método `AssemblerResult` objeto que contém os resultados da tarefa e quaisquer exceções que ocorreram. Para obter o documento XDP recém-criado, execute as seguintes ações:

   * Acesse o `AssemblerResult` do objeto `documents` , que é um `Map` objeto que contém os documentos PDF resultantes.
   * Iterar por meio do `Map` objeto para recuperar o design de formulário montado. Transmita esse membro da matriz `value` para `BLOB`. Passe isto `BLOB` para o serviço de saída.


1. Use o Serviço de saída para gerar o documento PDF.

   Chame o `OutputServiceClient` do objeto `generatePDFOutput2` e transmita os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica a raiz do conteúdo na qual os recursos adicionais, como imagens, estão localizados.
   * A `BLOB` objeto que representa o design de formulário (use o `BLOB` instância retornada pelo serviço Assembler).
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução do PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `BLOB` objeto que contém a fonte de dados XML que contém dados para mesclar com o design de formulário.
   * Uma saída `BLOB` que a variável `generatePDFOutput2` é preenchida. O `generatePDFOutput2` O método preenche este objeto com metadados gerados que descrevem o documento. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).
   * Uma saída `OutputResult` que contém os resultados da operação. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).

   O `generatePDFOutput2` método retorna um `BLOB` objeto que contém o formulário PDF não interativo.

1. Salve o documento PDF como um arquivo PDF.

   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento interativo do PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto recuperado do `generatePDFOutput2` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## Imprimindo em Arquivos {#printing-to-files}

Você pode usar o Serviço de saída para imprimir fluxos como PostScript, PCL (Printer Control Language) ou os seguintes formatos de rótulo em um arquivo:

* Zebra - ZPL
* Interfaces - IPL
* Datamax - DPL
* TecToshiba - TPCL

Com o serviço Saída, é possível mesclar dados XML com um design de formulário e imprimir o formulário em um arquivo. A ilustração a seguir mostra o serviço de saída criando arquivos de laser e rótulo.

>[!NOTE]
>
>Para obter informações sobre o envio de fluxos de impressão para impressoras, consulte [Enviando fluxos de impressão para impressoras](creating-document-output-streams.md#sending-print-streams-to-printers).

>[!NOTE]
>
>Para obter mais informações sobre o serviço Saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-5}

Para imprimir em um arquivo, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto de Cliente de saída.
1. Faça referência a uma fonte de dados XML.
1. Defina as opções de tempo de execução de impressão necessárias para imprimir em um arquivo.
1. Imprima o fluxo de impressão em um arquivo.
1. Recupere os resultados da operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado. (Consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)

**Criar um objeto de cliente de saída**

Antes de poder executar programaticamente uma operação do Serviço de saída, é necessário criar um objeto cliente do Serviço de saída. Se estiver usando a API do Java, crie um `OutputClient` objeto. Se estiver usando a API de serviço da Web de saída, crie um `OutputServiceService` objeto.

**Referência a uma fonte de dados XML**

Para imprimir um documento que contenha dados, é necessário referenciar uma fonte de dados XML que contenha elementos XML para cada campo de formulário que você deseja preencher com dados. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML é ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos se todos os elementos XML forem especificados.

**Defina as opções de tempo de execução de impressão necessárias para imprimir em um arquivo**

Para imprimir em um arquivo, é necessário definir a opção File URI run-time especificando o local e o nome do arquivo para o qual o serviço de saída é impresso. Por exemplo, para instruir o serviço de saída a imprimir um arquivo PostScript chamado *MortgaugeForm.ps* para C:\Adobe, especifique C:\Adobe\MortgageForm.ps.

>[!NOTE]
>
>Há opções opcionais de tempo de execução que você pode definir. Para obter informações sobre todas as opções que podem ser definidas, consulte o `PrintedOutputOptionsSpec` referência de classe em [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Imprimir o fluxo de impressão em um arquivo**

Depois de fazer referência a uma fonte de dados XML válida que contém dados de formulário e definir opções de tempo de execução de impressão, você pode chamar o serviço Saída, o que faz com que ele imprima um arquivo.

**Recuperar os resultados da operação**

Depois que o serviço de saída executa uma operação, ele retorna vários itens de dados, como dados XML, que especifica se a operação foi bem-sucedida.

**Consulte também**

[Imprimir em arquivos usando a API Java](creating-document-output-streams.md#print-to-files-using-the-java-api)

[Imprimir em arquivos usando a API de serviço da Web](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Imprimir em arquivos usando a API Java {#print-to-files-using-the-java-api}

Imprima em um arquivo usando a API de saída (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como o adobe-output-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de Cliente de saída.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `OutputClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Faça referência a uma fonte de dados XML.

   * Crie um `java.io.FileInputStream` objeto que representa a fonte de dados XML usada para preencher o documento usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XML.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Defina as opções de tempo de execução de impressão necessárias para imprimir em um arquivo.

   * Crie um `PrintedOutputOptionsSpec` usando seu construtor.
   * Especifique o arquivo chamando o objeto PrintedOutputOptionsSpec `setFileURI` e transmitindo um valor de string que represente o nome e o local do arquivo. Por exemplo, se você deseja que o serviço de Saída imprima para um arquivo PostScript chamado MortgaugeForm.ps localizado em C:\Adobe, especifique C:\\Adobe\MortgageForm.ps.
   * Especifique o número de cópias a serem impressas chamando a variável `PrintedOutputOptionsSpec` do objeto `setCopies` e transmitindo um valor inteiro que representa o número de cópias.

1. Imprima o fluxo de impressão em um arquivo.

   Imprimir em um arquivo chamando o `OutputClient` do objeto `generatePrintedOutput` e transmitindo os seguintes valores:

   * A `PrintFormat` valor de enumeração que especifica o formato de fluxo de impressão a ser criado. Por exemplo, para criar um fluxo de impressão PostScript, passe `PrintFormat.PostScript`.
   * Um valor de string que especifica o nome do design de formulário.
   * Um valor de string que especifica o local de arquivos de garantia relacionados, como arquivos de imagem.
   * Um valor da string que especifica o local do arquivo XDC a ser usado (você pode passar `null` se você especificou o arquivo XDC a ser usado com o `PrintedOutputOptionsSpec` objeto).
   * O `PrintedOutputOptionsSpec` objeto que contém opções de tempo de execução necessárias para imprimir em um arquivo.
   * O `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém os dados do formulário.

   O `generatePrintedOutput` retorna um método `OutputResult` que contém os resultados da operação.

   >[!NOTE]
   >
   >O `OutputResult` do objeto `getRecordLevelMetaDataList` retornos de método `null`.

1. Recupere os resultados da operação.

   * Crie um `com.adobe.idp.Document` objeto que representa o status do `generatePrintedOutput` chamando o método `OutputResult` do objeto `getStatusDoc` método (o `OutputResult` o objeto foi retornado pelo `generatePrintedOutput` método ).
   * Crie um `java.io.File` que conterá os resultados da operação. Certifique-se de que a extensão do arquivo seja XML.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` para o arquivo (certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `getStatusDoc` método ).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo SOAP): Impressão em um arquivo usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Imprimir em arquivos usando a API de serviço da Web {#print-to-files-using-the-web-service-api}

Imprima em um arquivo usando a API de saída (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto de Cliente de saída.

   * Crie um `OutputServiceClient` usando seu construtor padrão.
   * Crie um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `OutputServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a uma fonte de dados XML.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar dados de formulário.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que especifica o local do arquivo XML que contém os dados do formulário.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `binaryData` com o conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução de impressão necessárias para imprimir em um arquivo.

   * Crie um `PrintedOutputOptionsSpec` usando seu construtor.
   * Especifique o arquivo atribuindo um valor de string que represente o local e o nome do arquivo para a variável `PrintedOutputOptionsSpec` do objeto `fileURI` membro de dados. Por exemplo, se você quiser que o serviço de saída imprima para um arquivo PostScript chamado *MortgaugeForm.ps* localizado em C:\Adobe, especifique C:\\Adobe\MortgageForm.ps.
   * Especifique o número de cópias a serem impressas atribuindo um valor inteiro que represente o número de cópias à `PrintedOutputOptionsSpec` do objeto `copies` membros de dados.

1. Imprima o fluxo de impressão em um arquivo.

   Imprimir em um arquivo chamando o `OutputServiceService` do objeto `generatePrintedOutput` e transmitindo os seguintes valores:

   * A `PrintFormat` valor de enumeração que especifica o formato de fluxo de impressão a ser criado. Por exemplo, para criar um fluxo de impressão PostScript, passe `PrintFormat.PostScript`.
   * Um valor de string que especifica o nome do design de formulário.
   * Um valor de string que especifica o local de arquivos de garantia relacionados, como arquivos de imagem.
   * Um valor da string que especifica o local do arquivo XDC a ser usado (você pode passar `null` se você especificou o arquivo XDC a ser usado com o `PrintedOutputOptionsSpec` objeto).
   * O `PrintedOutputOptionsSpec` objeto que contém as opções de tempo de execução de impressão necessárias para imprimir em um arquivo.
   * O `BLOB` objeto que contém a fonte de dados XML que contém dados de formulário.
   * A `BLOB` que é preenchido pela variável `generatePDFOutput` método . O `generatePDFOutput` O método preenche este objeto com metadados gerados que descrevem o documento. (Esse valor de parâmetro é necessário somente para invocação do serviço da Web.)
   * A `BLOB` que é preenchido pela variável `generatePDFOutput` método . O `generatePDFOutput` O método preenche esse objeto com dados de resultado. (Esse valor de parâmetro é necessário somente para invocação do serviço da Web.)
   * Um `OutputResult` que contém os resultados da operação. (Esse valor de parâmetro é necessário somente para invocação do serviço da Web.)

1. Recupere os resultados da operação.

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa um local de arquivo XML que contém dados de resultado. Certifique-se de que a extensão do arquivo seja XML.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi preenchido com dados de resultado pela variável `OutputServiceService` do objeto `generatePDFOutput` método (o oitavo parâmetro). Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes no arquivo XML chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Enviando fluxos de impressão para impressoras {#sending-print-streams-to-printers}

Você pode usar o Serviço de saída para enviar fluxos de impressão, como PostScript, PCL (Printer Control Language) ou os seguintes formatos de rótulo para impressoras de rede:

* Zebra - ZPL
* Interfaces - IPL
* Datamax - DPL
* TecToshiba - TPCL

Usando o serviço Saída, é possível mesclar dados XML com um design de formulário e exibir o formulário como um fluxo de impressão. Por exemplo, você pode criar um fluxo de impressão PostScript e enviá-lo para uma impressora de rede. A ilustração a seguir mostra o serviço Saída enviando fluxos de impressão para impressoras de rede.

>[!NOTE]
>
>Para demonstrar como enviar um fluxo de impressão para uma impressora de rede, esta seção envia um fluxo de impressão PostScript para uma impressora de rede usando o protocolo de impressora SharedPrinter.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-6}

Para enviar um fluxo de impressão para uma impressora de rede, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto de Cliente de saída.
1. Faça referência a uma fonte de dados XML.
1. Definir opções de tempo de execução de impressão
1. Recupere um documento para imprimir.
1. Envie o documento para uma impressora de rede.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado.

**Criar um objeto de cliente de saída**

Antes de executar programaticamente uma operação do serviço de saída, crie um objeto cliente do serviço de saída. Se estiver usando a API do Java, crie um `OutputClient` objeto. Se estiver usando a API de serviço da Web de saída, crie um `OutputServiceClient` objeto.

**Referência a uma fonte de dados XML**

Para imprimir um documento que contenha dados, é necessário referenciar uma fonte de dados XML que contenha elementos XML para cada campo de formulário que você deseja preencher com dados. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML é ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos se todos os elementos XML forem especificados.

**Definir opções de tempo de execução de impressão**

Você pode definir as opções de tempo de execução ao enviar um fluxo de impressão para uma impressora, incluindo as seguintes opções:

* **Cópias**: Especifica o número de cópias a serem enviadas para a impressora. O valor padrão é 1.
* **Agrafar**: Uma opção XCI é definida quando um grampeador é usado. Essa opção pode ser especificada no modelo de configuração pelo elemento básico e é usada apenas para impressoras PS e PCL.
* **OutputJog**: Uma opção XCI é definida quando as páginas de saída devem ser executadas (movidas fisicamente na bandeja de saída). Essa opção é somente para impressoras PS e PCL.
* **OutputBin**: Valor XCI usado para permitir que o driver de impressão selecione o compartimento de saída apropriado.

>[!NOTE]
>
>Para obter informações sobre todas as opções de tempo de execução que você pode definir, consulte o `PrintedOutputOptionsSpec` referência de classe.

**Recuperar um documento para imprimir**

Recupere um fluxo de impressão para enviar para uma impressora. Por exemplo, você pode recuperar um arquivo PostScript e enviá-lo para uma impressora.

Você pode optar por enviar um arquivo PDF se a impressora suportar PDF. No entanto, um problema ao enviar um documento PDF para uma impressora é que cada fabricante de impressora tem uma implementação diferente do interpretador PDF. Ou seja, alguns fabricantes de impressão usam a interpretação Adobe PDF, mas depende da impressora. Outras impressoras têm seu próprio intérprete de PDF. Como resultado, os resultados da impressão podem variar.

Outra limitação do envio de um documento PDF para uma impressora é que ele apenas imprime; ele não pode acessar duplex, seleção da bandeja de papel e grampeamento, exceto por meio de configurações na impressora.

Para recuperar um documento para imprimir, use o `generatePrintedOutput` método . A tabela a seguir especifica os tipos de conteúdo que são definidos para um determinado fluxo de impressão ao usar o `generatePrintedOutput` método .

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
   <td><p>Cria um dpl203.xdc por padrão ou fluxo de saída xdc personalizado.</p></td>
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
   <td><p>Cria um fluxo de saída PCL (5c) de cor genérica.</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>Cria um fluxo de saída Genérico do Nível 3 de PostScript.</p></td>
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
   <td><p>Cria um fluxo de saída Genérico do Nível 2 de PostScript.</p></td>
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
>Também é possível enviar um fluxo de impressão para uma impressora usando a variável `generatePrintedOutput2` método . No entanto, as inicializações rápidas associadas à seção Enviar fluxos de impressão para impressoras usam o `generatePrintedOutput` método .

**Enviar fluxo de impressão para uma impressora de rede**

Depois de recuperar um documento para imprimir, você pode chamar o Serviço de saída, o que faz com que ele envie um fluxo de impressão para uma impressora de rede. Para que o serviço de saída localize a impressora com êxito, é necessário especificar o servidor de impressão e o nome da impressora. Além disso, você também deve especificar o protocolo de impressão.

>[!NOTE]
>
>Se o PDFG estiver instalado no servidor de formulários e o servidor for executado no Windows Server 2008, você não poderá usar a propriedade SharedPrinter. Nessa situação, use um protocolo de impressora diferente.

>[!NOTE]
>
>Se estiver usando uma impressora de rede e o mecanismo de acesso for SharedPrinter, será necessário especificar o caminho de rede completo da impressora.Enviar um fluxo de impressão para uma impressora de rede usando a API Java

Envie um fluxo de impressão para uma impressora de rede usando a API de saída (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como o adobe-output-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de cliente de saída

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `OutputClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Referência a uma fonte de dados XML

   * Crie um `java.io.FileInputStream` objeto que representa a fonte de dados XML usada para preencher o documento usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XML.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Definir opções de tempo de execução de impressão

   Crie um `PrintedOutputOptionsSpec` objeto que representa opções de tempo de execução de impressão. Por exemplo, você pode especificar o número de cópias a serem impressas chamando a função `PrintedOutputOptionsSpec` do objeto `setCopies` método .

   >[!NOTE]
   >
   >Não é possível definir o valor da paginação usando a variável `PrintedOutputOptionsSpec` do objeto `setPagination` método se estiver gerando um fluxo de impressão ZPL. Da mesma forma, não é possível definir as seguintes opções para um fluxo de impressão ZPL: OutputJog, PageOffset e Staple. O `setPagination` não é válido para geração de PostScript. É válido apenas para geração de PCL.

1. Recuperar um documento para imprimir

   * Recupere um documento para imprimir, chamando o `OutputClient` do objeto `generatePrintedOutput` e transmitindo os seguintes valores:

      * A `PrintFormat` valor de enumeração que especifica o fluxo de impressão. Por exemplo, para criar um fluxo de impressão PostScript, passe `PrintFormat.PostScript`.
      * Um valor de string que especifica o nome do design de formulário.
      * Um valor de string que especifica o local dos arquivos de garantia relacionados, como arquivos de imagem.
      * Um valor de string que especifica o local do arquivo XDC a ser usado.
      * O `PrintedOutputOptionsSpec` objeto que contém opções de tempo de execução necessárias para imprimir em um arquivo.
      * O `com.adobe.idp.Document` objeto que representa a fonte de dados XML que contém dados de formulário a serem unidos ao design de formulário.

      Esse método retorna um `OutputResult` que contém os resultados da operação.

   * Crie um `com.adobe.idp.Document` objeto a ser enviado para a impressora chamando o `OutputResult` objeto &quot;s `getGeneratedDoc` método . Esse método retorna um `com.adobe.idp.Document` objeto.


1. Enviar fluxo de impressão para uma impressora de rede

   Envie o fluxo de impressão para uma impressora de rede chamando o `OutputClient` do objeto `sendToPrinter` e transmitindo os seguintes valores:

   * A `com.adobe.idp.Document` objeto que representa o fluxo de impressão a ser enviado para a impressora.
   * A `PrinterProtocol` valor de enumeração que especifica o protocolo de impressora a ser usado. Por exemplo, para especificar o protocolo SharedPrinter, passe `PrinterProtocol.SharedPrinter`.
   * Um valor de string que especifica o nome do servidor de impressão. Por exemplo, supondo que o nome do servidor de impressão seja PrintServer1, passe `\\\PrintSever1`.
   * Um valor de string que especifica o nome da impressora. Por exemplo, supondo que o nome da impressora seja Printer1, passe `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >O `sendToPrinter` foi adicionado à API do AEM Forms na versão 8.2.1.

### Enviar um fluxo de impressão para uma impressora usando a API do serviço da Web {#send-a-print-stream-to-a-printer-using-the-web-service-api}

Envie um fluxo de impressão para uma impressora de rede usando a API de saída (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto de Cliente de saída.

   * Crie um `OutputServiceClient` usando seu construtor padrão.
   * Crie um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `OutputServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a uma fonte de dados XML.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar dados de formulário.
   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que especifica o local do arquivo XML que contém os dados do formulário.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Determine o comprimento da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução de impressão.

   Crie um `PrintedOutputOptionsSpec` usando seu construtor. Por exemplo, você pode especificar o número de cópias a serem impressas atribuindo um valor inteiro que representa o número de cópias à variável `PrintedOutputOptionsSpec` do objeto `copies` membro de dados.

   >[!NOTE]
   >
   >Não é possível definir o valor da paginação usando a variável `PrintedOutputOptionsSpec` do objeto `pagination` membro de dados se você estiver gerando um fluxo de impressão ZPL. Da mesma forma, não é possível definir as seguintes opções para um fluxo de impressão ZPL: OutputJog, PageOffset e Staple. O `pagination` o membro de dados não é válido para geração de PostScript. É válido apenas para geração de PCL.

1. Recupere um documento para imprimir.

   * Recupere um documento para imprimir, chamando o `OutputServiceService` do objeto `generatePrintedOutput` e transmitindo os seguintes valores:

      * A `PrintFormat` valor de enumeração que especifica o fluxo de impressão. Por exemplo, para criar um fluxo de impressão PostScript, passe `PrintFormat.PostScript`.
      * Um valor de string que especifica o nome do design de formulário.
      * Um valor de string que especifica o local dos arquivos de garantia relacionados, como arquivos de imagem.
      * Um valor de string que especifica o local do arquivo XDC a ser usado.
      * O `PrintedOutputOptionsSpec` objeto que contém opções de tempo de execução de impressão usadas ao enviar um fluxo de impressão para uma impressora de rede.
      * O `BLOB` objeto que contém a fonte de dados XML que contém dados de formulário.
      * A `BLOB` que é preenchido pela variável `generatePrintedOutput` método . O `generatePrintedOutput` O método preenche este objeto com metadados gerados que descrevem o documento. (Esse valor de parâmetro é necessário somente para invocação do serviço da Web.)
      * A `BLOB` que é preenchido pela variável `generatePrintedOutput` método . O `generatePrintedOutput` O método preenche esse objeto com dados de resultado. (Esse valor de parâmetro é necessário somente para invocação do serviço da Web.)
      * Um `OutputResult` que contém os resultados da operação. (Esse valor de parâmetro é necessário somente para invocação do serviço da Web.)
   * Crie um `BLOB` objeto a ser enviado para a impressora obtendo o valor da variável `OutputResult` objeto &quot;s `generatedDoc` método . Esse método retorna um `BLOB` objeto que contém dados PostScript retornados pela variável `generatePrintedOutput` método .


1. Envie o fluxo de impressão para uma impressora de rede.

   Envie o fluxo de impressão para uma impressora de rede chamando o `OutputClient` do objeto `sendToPrinter` e transmitindo os seguintes valores:

   * A `BLOB` objeto que representa o fluxo de impressão a ser enviado para a impressora.
   * A `PrinterProtocol` valor de enumeração que especifica o protocolo de impressora a ser usado. Por exemplo, para especificar o protocolo SharedPrinter, passe `PrinterProtocol.SharedPrinter`.
   * A `bool` que especifica se o valor do parâmetro anterior deve ser usado. Transmita o valor `true`. (Esse valor de parâmetro é necessário somente para invocação do serviço da Web.)
   * Um valor de string que especifica o nome do servidor de impressão. Por exemplo, supondo que o nome do servidor de impressão seja PrintServer1, passe `\\\PrintSever1`.
   * Um valor de string que especifica o nome da impressora. Por exemplo, supondo que o nome da impressora seja Printer1, passe `\\\PrintSever1\Printer1`.

   >[!NOTE]
   >
   >O `sendToPrinter` foi adicionado à API do AEM Forms na versão 8.2.1.

## Criação de vários arquivos de saída {#creating-multiple-output-files}

O serviço de saída pode criar documentos separados para cada registro dentro de uma fonte de dados XML ou um único arquivo que contenha todos os registros (essa funcionalidade é o padrão). Por exemplo, suponha que dez registros estejam localizados em uma fonte de dados XML e você instrua o serviço de Saída a criar documentos PDF separados (ou outros tipos de saída) para cada registro usando a API do Serviço de Saída. Como resultado, o serviço Output gera dez documentos PDF. (Em vez de criar documentos, você pode enviar vários fluxos de impressão para uma impressora.)

A ilustração a seguir também mostra o serviço de saída processando um arquivo de dados XML que contém vários registros. No entanto, suponha que você instrua o Serviço de saída a criar um único documento PDF que contenha todos os registros de dados. Nessa situação, o serviço de Saída gera um documento que contém todos os registros.

A ilustração a seguir mostra o serviço de saída processando um arquivo de dados XML que contém vários registros. Suponha que você instrua o Serviço de saída a criar um documento PDF separado para cada registro de dados. Nessa situação, o serviço Output gera um documento PDF separado para cada registro de dados.

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

Os seguintes dados XML mostram um exemplo de arquivo de dados que contém três registros de dados.

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

Observe que o elemento XML que inicia e encerra cada registro de dados é `LoanRecord`. Esse elemento XML é referenciado pela lógica do aplicativo que gera vários arquivos.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-7}

Para criar vários arquivos PDF com base em uma fonte de dados XML, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto de Cliente de saída.
1. Faça referência a uma fonte de dados XML.
1. Defina as opções de tempo de execução do PDF.
1. Defina as opções de tempo de execução da renderização.
1. Gere vários arquivos PDF.
1. Recupere os resultados da operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado.

**Criar um objeto de cliente de saída**

Antes de poder executar programaticamente uma operação do Serviço de saída, é necessário criar um objeto cliente do Serviço de saída. Se estiver usando a API do Java, crie um `OutputClient` objeto. Se estiver usando a API de serviço da Web de saída, crie um `OutputServiceService` objeto.

**Referência a uma fonte de dados XML**

Faça referência a uma fonte de dados XML que contenha vários registros. Um elemento XML deve ser usado para separar os registros de dados. Por exemplo, no exemplo da fonte de dados XML mostrada anteriormente nesta seção, o elemento XML que separa registros de dados é nomeado `LoanRecord`.

Um elemento XML deve existir para cada campo de formulário que você deseja preencher com dados. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML é ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos se todos os elementos XML forem especificados.

**Definir opções de tempo de execução PDF**

Você deve definir as seguintes opções de tempo de execução para o serviço Saída criar com êxito vários arquivos com base em uma fonte de dados XML:

* **Muitos arquivos**: Especifica se o serviço Saída cria um único documento ou vários documentos. Você pode especificar verdadeiro ou falso. Para criar um documento separado para cada registro de dados na fonte de dados XML, especifique true.
* **URI do arquivo**: Especifica o local dos arquivos gerados pelo serviço de saída. Por exemplo, suponha que você especifique C:\\Adobe\forms\Loan.pdf. Nessa situação, o serviço de Saída cria um arquivo chamado Loan.pdf e coloca o arquivo no diretório C:\\Adobe\forms folder. Quando há vários arquivos, os nomes dos arquivos são Loan0001.pdf, Loan0002.pdf, Loan0003.pdf e assim por diante. Se você especificar um local de arquivo, os arquivos serão colocados no servidor, não no computador cliente.
* **Nome do Registro**: Especifica o nome do elemento XML na fonte de dados que separa os registros de dados. Por exemplo, no exemplo da fonte de dados XML mostrada anteriormente nesta seção, o elemento XML que separa registros de dados é chamado `LoanRecord`. (Em vez de definir a opção Tempo de execução Nome do Registro , você pode definir o Nível de Registro atribuindo a ele um valor numérico que indica o nível do elemento que contém registros de dados. No entanto, é possível definir somente o Nome do Registro ou o Nível do Registro. Não é possível definir ambos os valores.)

**Definir opções de tempo de execução de renderização**

É possível definir opções de tempo de execução de renderização ao criar vários arquivos. Embora essas opções não sejam necessárias (ao contrário das opções de tempo de execução de saída, que são necessárias), é possível executar tarefas como melhorar o desempenho do serviço de Saída. Por exemplo, é possível armazenar em cache o design de formulário que o serviço de saída usa para melhorar o desempenho.

Quando o serviço de saída processa registros em lote, ele lê dados que contêm vários registros de maneira incremental. Ou seja, o serviço de saída lê os dados na memória e libera os dados conforme o lote de registros é processado. O serviço de saída carrega dados de maneira incremental quando uma das duas opções de tempo de execução é definida. Se você definir a opção Tempo de execução Nome do Registro , o serviço de Saída lê os dados de maneira incremental. Da mesma forma, se você definir a opção Registrar nível de tempo de execução como 2 ou superior, o serviço de Saída lê os dados de maneira incremental.

Você pode controlar se o serviço de Saída executa o carregamento incremental usando o `PDFOutputOptionsSpec` ou `PrintedOutputOptionSpec` do objeto `setLazyLoading` método . Você pode passar o valor `false` para este método que desativa o carregamento incremental.

**Gerar vários arquivos PDF**

Depois de fazer referência a uma fonte de dados XML válida que contém vários registros de dados e definir opções de tempo de execução, você pode chamar o serviço de Saída, o que faz com que ele gere vários arquivos. Ao gerar vários registros, a variável `OutputResult` do objeto `getGeneratedDoc` retornos de método `null`.

**Recuperar os resultados da operação**

Depois que o serviço de saída executa uma operação, ele retorna dados XML que especificam se a operação foi bem-sucedida. O XML a seguir é retornado pelo serviço de Saída. Nessa situação, o serviço Output gerou 42 documentos.

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

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Criar vários arquivos PDF usando a API do Java {#create-multiple-pdf-files-using-the-java-api}

Crie vários arquivos PDF usando a API de saída (Java):

1. Incluir arquivos de projeto&quot;

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do seu projeto Java. .

1. Criar um objeto de cliente de saída

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `OutputClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Referência a uma fonte de dados XML

   * Crie um `java.io.FileInputStream` objeto que representa a fonte de dados XML que contém vários registros usando seu construtor e passando um valor de string que especifica o local do arquivo XML.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Definir opções de tempo de execução PDF

   * Crie um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção Muitos arquivos chamando a `PDFOutputOptionsSpec` do objeto `setGenerateManyFiles` método . Por exemplo, passe o valor `true` para instruir o Serviço de saída a criar um arquivo PDF separado para cada registro na fonte de dados XML. (Se você passar `false`, o serviço Output gera um único documento PDF que contém todos os registros).
   * Defina a opção Arquivo URI chamando o `PDFOutputOptionsSpec` do objeto `setFileUri` e transmitindo um valor de string que especifica o local dos arquivos gerados pelo serviço de saída. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.
   * Defina a opção Nome do Registro chamando a `OutputOptionsSpec` do objeto `setRecordName` e transmitindo um valor de string que especifica o nome do elemento XML na fonte de dados que separa os registros de dados. (Por exemplo, considere a fonte de dados XML mostrada anteriormente nesta seção. O nome do elemento XML que separa os registros de dados é LoanRecord).

1. Definir opções de tempo de execução de renderização

   * Crie um `RenderOptionsSpec` usando seu construtor.
   * Armazene em cache o design de formulário para melhorar o desempenho do serviço de saída, chamando a função `RenderOptionsSpec` do objeto `setCacheEnabled` e transmitindo uma `Boolean` valor de `true`.

1. Gerar vários arquivos PDF

   Gere vários arquivos PDF chamando o `OutputClient` do objeto `generatePDFOutput` e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enum. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica o nome do design de formulário.
   * Um valor de string que especifica a raiz de conteúdo na qual o design de formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução do PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém dados para mesclar com o design de formulário.

   O `generatePDFOutput` retorna um método `OutputResult` que contém os resultados da operação.

1. Recuperar os resultados da operação

   * Crie um `java.io.File` objeto que representa um arquivo XML que conterá os resultados da variável `generatePDFOutput` método . Certifique-se de que a extensão do nome de arquivo seja .xml.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` para o arquivo (certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `applyUsageRights` método ).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): Criação de vários arquivos PDF usando a API Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criar vários arquivos PDF usando a API do serviço da Web {#create-multiple-pdf-files-using-the-web-service-api}

Crie vários arquivos PDF usando a API de saída (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto de Cliente de saída.

   * Crie um `OutputServiceClient` usando seu construtor padrão.
   * Crie um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `OutputServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a uma fonte de dados XML.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar dados de formulário que contêm vários registros.
   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo XML que contém vários registros.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Defina as opções de tempo de execução do PDF.

   * Crie um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção Muitos arquivos atribuindo um valor booleano à variável `OutputOptionsSpec` do objeto `generateManyFiles` membro de dados. Por exemplo, atribua o valor `true` para esse membro de dados instruir o Serviço de saída a criar um arquivo PDF separado para cada registro na fonte de dados XML. (Se você atribuir `false` para esse membro de dados, o serviço de Saída gera um único PDF que contém todos os registros).
   * Defina a opção URI do arquivo atribuindo um valor de string que especifica o local dos arquivos gerados pelo serviço de saída para a variável `OutputOptionsSpec` do objeto `fileURI` membro de dados. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.
   * Defina a opção de nome de registro atribuindo um valor de string que especifica o nome do elemento XML na fonte de dados que separa os registros de dados para a variável `OutputOptionsSpec` do objeto `recordName` membro de dados.
   * Defina a opção de cópias atribuindo um valor inteiro que especifique o número de cópias geradas pelo serviço de Saída para a variável `OutputOptionsSpec` do objeto `copies` membro de dados.

1. Defina as opções de tempo de execução da renderização.

   * Crie um `RenderOptionsSpec` usando seu construtor.
   * Armazene em cache o design de formulário para melhorar o desempenho do serviço de Saída atribuindo o valor `true` para `RenderOptionsSpec` do objeto `cacheEnabled` membro de dados.

1. Gere vários arquivos PDF.

   Crie vários arquivos PDF chamando o `OutputServiceService` do objeto `generatePDFOutput`e transmitindo os seguintes valores:

   * Um valor enum TransformationFormat. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica o nome do design de formulário.
   * Um valor de string que especifica a raiz de conteúdo na qual o design de formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução do PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `BLOB` objeto que contém a fonte de dados XML que contém dados para mesclar com o design de formulário.
   * A `BLOB` que é preenchido pela variável `generatePDFOutput` método . O `generatePDFOutput` O método preenche este objeto com metadados gerados que descrevem o documento.
   * A `BLOB` que é preenchido pela variável `generatePDFOutput` método . O `generatePDFOutput` O método preenche esse objeto com dados de resultado.
   * Um `OutputResult` que contém os resultados da operação.

1. Recuperar os resultados da operação

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa um local de arquivo XML que contém dados de resultado. Certifique-se de que a extensão do nome de arquivo seja .xml.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi preenchido com dados de resultado pela variável `OutputServiceService` do objeto `generatePDFOutput` método (o oitavo parâmetro). Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `binaryData` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes no arquivo XML chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Criando regras de pesquisa {#creating-search-rules}

Você pode criar regras de pesquisa que resultam no serviço de saída examinando dados de entrada e usando diferentes designs de formulário com base no conteúdo de dados para gerar saída. Por exemplo, se o texto *hipoteca* estiver localizado nos dados de entrada, o serviço de Saída poderá usar um design de formulário chamado Mortgauge.xdp. Da mesma forma, se o texto *automóvel* estiver localizado nos dados de entrada, o serviço de Saída poderá usar um design de formulário salvo como AutomobileLoan.xdp. Embora o serviço de Saída possa gerar diferentes tipos de saída, esta seção assume que o serviço de Saída gera um arquivo PDF. O diagrama a seguir mostra o serviço de Saída gerando um arquivo PDF processando um arquivo de dados XML e usando um de muitos designs de formulário.

Além disso, o Serviço de saída é capaz de gerar pacotes de documentos, onde vários registros são fornecidos no conjunto de dados e cada registro corresponde a um design de formulário e um único documento é gerado composto de vários designs de formulário.

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>Para obter mais informações sobre o serviço Saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-8}

Para instruir o serviço de Saída a usar regras de pesquisa ao gerar um documento, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto de Cliente de saída.
1. Faça referência a uma fonte de dados XML.
1. Defina as regras de pesquisa.
1. Defina as opções de tempo de execução do PDF.
1. Defina as opções de tempo de execução da renderização.
1. Gere um documento PDF.
1. Recupere os resultados da operação.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no seu projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao classpath do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (obrigatório se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado.

**Criar um objeto de cliente de saída**

Antes de poder executar programaticamente uma operação do Serviço de saída, é necessário criar um objeto cliente do Serviço de saída.

**Referência a uma fonte de dados XML**

Um elemento XML deve existir para cada campo de formulário que você deseja preencher com dados. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML é ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos, desde que todos os elementos XML sejam especificados.

**Definir regras de pesquisa**

Para definir regras de pesquisa, defina um ou mais padrões de texto que os Serviços de saída pesquisam nos dados de entrada. Para cada padrão de texto definido, especifique um design de formulário correspondente que será usado se o padrão de texto estiver localizado. Se um padrão de texto estiver localizado, o serviço Saída usará o design de formulário correspondente para gerar a saída. Um exemplo de padrão de texto é *hipoteca*.

>[!NOTE]
>
>Se os padrões de texto não estiverem localizados, o formulário padrão será usado. Certifique-se de que todos os designs de formulário usados estejam localizados na raiz do conteúdo.

**Definir opções de tempo de execução PDF**

Defina as seguintes opções de tempo de execução do PDF para que o serviço de Saída crie com êxito um documento do PDF com base em vários designs de formulário:

* **URI do arquivo**: Especifica o nome e o local do arquivo PDF gerado pelo serviço de saída.
* **Regras**: Especifica as regras que você definiu.
* **LookAHead**: Especifica o número de bytes a serem usados a partir do início do arquivo de dados de entrada para verificar os padrões de texto definidos. O padrão é 500 bytes.

**Definir opções de tempo de execução de renderização**

Você pode definir opções de tempo de execução de renderização ao criar arquivos PDF. Embora essas opções não sejam necessárias (ao contrário das opções de tempo de execução de PDF), é possível executar tarefas como melhorar o desempenho do serviço de Saída. Por exemplo, é possível armazenar em cache o design de formulário que o serviço de saída usa para melhorar o desempenho.

**Gerar um documento PDF**

Depois de fazer referência a uma fonte de dados XML válida e definir opções de tempo de execução, você pode chamar o serviço de Saída, resultando na geração de um documento PDF. Se o serviço Saída localizar um padrão de texto especificado nos dados de entrada, ele usará o design de formulário correspondente. Se um padrão de texto não for usado, o serviço Saída usará o design de formulário padrão.

**Recuperar os resultados da operação**

Depois que o serviço de saída executa uma operação, ele retorna dados XML que especificam se a operação foi bem-sucedida.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Criar regras de pesquisa usando a API do Java {#create-search-rules-using-the-java-api}

Crie regras de pesquisa usando a API de saída (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de Cliente de saída.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `OutputClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Faça referência a uma fonte de dados XML.

   * Crie um `java.io.FileInputStream` objeto que representa a fonte de dados XML usada para preencher o documento PDF usando seu construtor e transmitindo um valor de string que especifica o local do arquivo XML.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Defina as regras de pesquisa.

   * Crie um `Rule` usando seu construtor.
   * Defina um padrão de texto chamando a função `Rule` do objeto `setPattern` e transmitindo um valor de string que especifica um padrão de texto.
   * Defina o design de formulário correspondente chamando a função `Rule` do objeto `setForm` método . Passe um valor de string que especifica o nome do design de formulário.

   >[!NOTE]
   >
   >Para cada padrão de texto que você deseja definir, repita as três subetapas anteriores.

   * Crie um `java.util.List` usando um `java.util.ArrayList` construtor.
   * Para cada `Rule` objeto criado, chame o `java.util.List` do objeto `add` e passe o `Rule` objeto.


1. Defina as opções de tempo de execução do PDF.

   * Crie um `PDFOutputOptionsSpec` usando seu construtor.
   * Especifique o nome e o local do arquivo de PDF que o serviço de saída gera, chamando a função `PDFOutputOptionsSpec` do objeto `setFileURI` método . Passe um valor de string que especifica o local do arquivo PDF. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.
   * Defina as regras que você definiu chamando a variável `PDFOutputOptionsSpec` do objeto `setRules` método . Passe o `java.util.List` objeto que contém a variável `Rule` objetos.
   * Defina o número de bytes para verificar os padrões de texto definidos chamando a função `PDFOutputOptionsSpec` do objeto `setLookAhead` método . Passe um valor inteiro que representa os números de bytes.

1. Defina as opções de tempo de execução da renderização.

   * Crie um `RenderOptionsSpec` usando seu construtor.
   * Armazene em cache o design de formulário para melhorar o desempenho do serviço de Saída, chamando a função `RenderOptionsSpec` do objeto `setCacheEnabled` e a passagem `true`.

1. Gere um documento PDF.

   Gere um documento do PDF baseado em vários designs de formulário, chamando o `OutputClient` do objeto `generatePDFOutput` e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica o nome do design de formulário padrão. Ou seja, o design de formulário usado se um padrão de texto não estiver localizado.
   * Um valor de string que especifica a raiz de conteúdo na qual os designs de formulário estão localizados.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução do PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `com.adobe.idp.Document` objeto que contém os dados de formulário pesquisados pelo serviço de saída para os padrões de texto definidos.

   O `generatePDFOutput` retorna um método `OutputResult` que contém os resultados da operação.

1. Recupere os resultados da operação.

   * Crie um `com.adobe.idp.Document` objeto que representa o status do `generatePDFOutput` chamando o método `OutputResult` do objeto `getStatusDoc` método .
   * Crie um `java.io.File` que conterá os resultados da operação. Certifique-se de que a extensão do arquivo seja .xml.
   * Chame o `com.adobe.idp.Document` do objeto `copyToFile` para copiar o conteúdo da `com.adobe.idp.Document` para o arquivo (certifique-se de usar a variável `com.adobe.idp.Document` objeto retornado pelo `getStatusDoc` método ).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): Criação de regras de pesquisa usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Início rápido (modo SOAP): Criação de regras de pesquisa usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Criar regras de pesquisa usando a API de serviço da Web {#create-search-rules-using-the-web-service-api}

Crie regras de pesquisa usando a API de saída (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto de Cliente de saída.

   * Crie um `OutputServiceClient` usando seu construtor padrão.
   * Crie um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `OutputServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Faça referência a uma fonte de dados XML.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar dados que serão unidos ao documento PDF.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento do PDF a ser criptografado e o modo no qual abrir o arquivo.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Defina as regras de pesquisa.

   * Crie um `Rule` usando seu construtor.
   * Defina um padrão de texto atribuindo um valor de string que especifique um padrão de texto para a variável `Rule` do objeto `pattern` membro de dados.
   * Defina o design de formulário correspondente atribuindo um valor de string que especifica o design de formulário para a variável `Rule` do objeto `form` membro de dados.

   >[!NOTE]
   >
   >Para cada padrão de texto que você deseja definir, repita as três subetapas anteriores.

   * Crie um `MyArrayOf_xsd_anyType` que armazena as regras.
   * Atribuir cada `Rule` para um elemento da variável `MyArrayOf_xsd_anyType` matriz. Chame o `MyArrayOf_xsd_anyType` do objeto `Add` método para cada `Rule` objeto.


1. Definir opções de tempo de execução PDF

   * Crie um `PDFOutputOptionsSpec` usando seu construtor.
   * Defina a opção URI do arquivo atribuindo um valor de string que especifica o local do arquivo de PDF que o serviço de saída gera para a variável `PDFOutputOptionsSpec` do objeto `fileURI` membro de dados. A opção File URI é relativa ao servidor de aplicativos J2EE que hospeda o AEM Forms, não ao computador cliente.
   * Defina a opção de cópias atribuindo um valor inteiro que especifique o número de cópias geradas pelo serviço de Saída para a variável `PDFOutputOptionsSpec` do objeto `copies` membro de dados.
   * Defina as regras definidas atribuindo a variável `MyArrayOf_xsd_anyType` que armazena as regras para a `PDFOutputOptionsSpec` do objeto `rules` membro de dados.
   * Defina o número de bytes para verificar os padrões de texto definidos, atribuindo um valor inteiro que representa os números de bytes a serem verificados na variável `PDFOutputOptionsSpec` do objeto `lookAhead` método de dados.

1. Definir opções de tempo de execução de renderização

   * Crie um `RenderOptionsSpec` usando seu construtor.
   * Armazene em cache o design de formulário para melhorar o desempenho do serviço de Saída atribuindo o valor `true` para `RenderOptionsSpec` do objeto `cacheEnabled` membro de dados.

   >[!NOTE]
   >
   >Não é possível definir a versão do documento do PDF usando o `RenderOptionsSpec` do objeto `pdfVersion` membro se o documento de entrada for um formulário Acrobat. O documento PDF de saída retém a versão PDF do formulário Acrobat. Da mesma forma, não é possível definir a opção de PDF marcado usando o `RenderOptionsSpec` do objeto `taggedPDF` se o documento de entrada for um formulário Acrobat.

   >[!NOTE]
   >
   >Não é possível definir a opção PDF linearizado usando o `RenderOptionsSpec` do objeto `linearizedPDF` membro se o documento PDF de entrada for certificado ou assinado digitalmente. Para obter mais informações, consulte [Assinar documentos do PDF digitalmente](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).

1. Gerar um documento PDF

   Crie um documento do PDF chamando o `OutputServiceService` do objeto `generatePDFOutput`e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica o nome do design de formulário.
   * Um valor de string que especifica a raiz de conteúdo na qual o design de formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução do PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `BLOB` objeto que contém a fonte de dados XML que contém dados para mesclar com o design de formulário.
   * A `BLOB` que é preenchido pela variável `generatePDFOutput` método . O `generatePDFOutput` O método preenche este objeto com metadados gerados que descrevem o documento. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).
   * A `BLOB` que é preenchido pela variável `generatePDFOutput` método . O `generatePDFOutput` O método preenche esse objeto com dados de resultado. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).
   * Um `OutputResult` que contém os resultados da operação. (Esse valor de parâmetro é necessário somente para a invocação do serviço da Web).

   >[!NOTE]
   >
   >Ao gerar um documento PDF chamando o `generatePDFOutput` esteja ciente de que não é possível mesclar dados com um formulário PDF XFA assinado, certificado ou contendo direitos de uso. Para obter informações sobre direitos de uso, consulte [Aplicação de direitos de uso a documentos do PDF](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).

1. Recuperar os resultados da operação

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa um local de arquivo XML que contém dados de resultado. Certifique-se de que a extensão do arquivo seja XML.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto que foi preenchido com dados de resultado pela variável `OutputServiceService` do objeto `generatePDFOutput` método (o oitavo parâmetro). Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes no arquivo XML chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Nivelar documentos do PDF {#flattening-pdf-documents}

Você pode usar o Serviço de saída para transformar um documento PDF interativo em um PDF não interativo. Um documento PDF interativo permite que os usuários insiram ou modifiquem dados que estejam nos campos do documento do PDF. O processo de transformação de um documento PDF interativo em um documento PDF não interativo é chamado *nivelamento*. Quando um documento PDF é nivelado, um usuário não pode modificar os dados nos campos do documento. Um motivo para nivelar um documento PDF é garantir que os dados não possam ser modificados.

Você pode nivelar os seguintes tipos de documentos PDF:

* Documentos de PDF XFA interativos
* Acrobat Forms

Tentar nivelar um PDF que é um documento PDF não interativo causa uma exceção.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Saída, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary_of_steps-9}

Para nivelar um documento PDF interativo em um documento PDF não interativo, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto de Cliente de saída.
1. Recupere um documento PDF interativo.
1. Transforme o documento PDF.
1. Salve o documento PDF não interativo como um arquivo PDF.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

Os seguintes arquivos JAR devem ser adicionados ao caminho de classe do seu projeto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar (necessário se o AEM Forms estiver implantado no JBoss)
* jbossall-client.jar (obrigatório se o AEM Forms for implantado no JBoss)

se o AEM Forms for implantado em um servidor de aplicativos J2EE compatível que não seja JBoss, será necessário substituir os arquivos adobe-utilities.jar e jbossall-client.jar por arquivos JAR específicos do servidor de aplicativos J2EE no qual o AEM Forms é implantado. Para obter informações sobre a localização de todos os arquivos AEM Forms JAR, consulte [Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Criar um objeto de cliente de saída**

Antes de poder executar programaticamente uma operação do Serviço de saída, é necessário criar um objeto cliente do Serviço de saída. Se estiver usando a API do Java, crie um `OutputClient` objeto. Se estiver usando a API de serviço da Web de saída, crie um `OutputServiceService` objeto.

**Recuperar um documento de PDF interativo**

Recupere um documento de PDF interativo que você deseja transformar em um documento de PDF não interativo. Tentar transformar um documento PDF não interativo causa uma exceção.

**Transformar o documento PDF**

Depois de recuperar um documento PDF interativo, você pode transformá-lo em um documento PDF não interativo. O serviço de saída retorna um documento PDF não interativo.

**Salve o documento PDF não interativo como um arquivo PDF.**

Você pode salvar o documento PDF não interativo como um arquivo PDF.

**Consulte também**

[Nivele um documento do PDF usando a API do Java](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[Nivelar um documento do PDF usando a API do serviço da Web](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Serviço de Saída](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Nivele um documento do PDF usando a API do Java {#flatten-a-pdf-document-using-the-java-api}

Nivele um documento PDF interativo em um documento PDF não interativo usando a API de saída (Java):

1. Inclua arquivos de projeto.

   Inclua arquivos JAR do cliente, como adobe-output-client.jar, no caminho de classe do seu projeto Java.

1. Crie um objeto de Cliente de saída.

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `OutputClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Recupere um documento PDF interativo.

   * Crie um `java.io.FileInputStream` objeto que representa o documento PDF interativo a ser transformado usando seu construtor e transmitindo um valor de string que especifica o local do arquivo PDF interativo.
   * Crie um `com.adobe.idp.Document` usando seu construtor e passando o `java.io.FileInputStream` objeto.

1. Transforme o documento PDF.

   Transforme o documento PDF interativo em um documento PDF não interativo, chamando o `OutputServiceService` do objeto `transformPDF` e transmitindo os seguintes valores:

   * O `com.adobe.idp.Document` objeto que contém o documento PDF interativo.
   * A `TransformationFormat` valor de enum. Para gerar um documento PDF não interativo, especifique `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` valor enum que especifica o número da revisão. Como esse parâmetro se destina a um documento PDF/A, você pode especificar `null`.
   * Um valor de string que representa o número e o ano da alteração, separados por dois pontos. Como esse parâmetro se destina a um documento PDF/A, você pode especificar `null`.
   * A `PDFAConformance` valor enum que representa o nível de conformidade PDF/A. Como esse parâmetro se destina a um documento PDF/A, você pode especificar `null`.

   O `transformPDF` método retorna um `com.adobe.idp.Document` objeto que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo como um arquivo PDF.

   * Crie um `java.io.File` e verifique se a extensão do nome do arquivo é .pdf.
   * Chame o `Document` do objeto `copyToFile` para copiar o conteúdo da `Document` para o arquivo (certifique-se de usar a variável `Document` objeto retornado pelo `transformPDF` método ).

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Início rápido (modo EJB): Transformar um documento do PDF usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Início rápido (modo SOAP): Transformar um documento do PDF usando a API do Java](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Nivelar um documento do PDF usando a API do serviço da Web {#flatten-a-pdf-document-using-the-web-service-api}

Nivele um documento PDF interativo em um documento PDF não interativo usando a API de saída (serviço da Web):

1. Inclua arquivos de projeto.

   Crie um projeto Microsoft .NET que use MTOM. Certifique-se de usar a seguinte definição de WSDL: `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Substituir `localhost` com o endereço IP do servidor que hospeda a AEM Forms.

1. Crie um objeto de Cliente de saída.

   * Crie um `OutputServiceClient` usando seu construtor padrão.
   * Crie um `OutputServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/OutputService?blob=mtom`.) Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado ao criar uma referência de serviço. No entanto, especifique `?blob=mtom` para usar MTOM.
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `OutputServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `OutputServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `OutputServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

1. Recupere um documento PDF interativo.

   * Crie um `BLOB` usando seu construtor. O `BLOB` é usado para armazenar o documento PDF interativo.
   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF interativo.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `System.IO.FileStream` objeto. Você pode determinar o tamanho da matriz de bytes obtendo a variável `System.IO.FileStream` do objeto `Length` propriedade.
   * Preencha a matriz de bytes com dados de fluxo chamando a variável `System.IO.FileStream` do objeto `Read` e transmitindo a matriz de bytes, a posição inicial e o comprimento do fluxo a ser lido.
   * Preencha o `BLOB` ao atribuir seu `MTOM` com o conteúdo da matriz de bytes.

1. Transforme o documento PDF.

   Transforme o documento PDF interativo em um documento PDF não interativo, chamando o `OutputClient` do objeto `transformPDF` e transmitindo os seguintes valores:

   * A `BLOB` objeto que contém o documento PDF interativo.
   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF não interativo, especifique `TransformationFormat.PDF`.
   * A `PDFARevisionNumber` valor enum que especifica o número da revisão.
   * Um valor booleano que especifica se a variável `PDFARevisionNumber` o valor enum é usado. Como esse parâmetro se destina a um documento PDF/A, você pode especificar `false`.
   * Um valor de string que representa o número e o ano da alteração, separados por dois pontos. Como esse parâmetro se destina a um documento PDF/A, você pode especificar `null`.
   * A `PDFAConformance` valor enum que representa o nível de conformidade PDF/A.
   * Valor booleano que especifica se a variável `PDFAConformance` o valor enum é usado. Como esse parâmetro se destina a um documento PDF/A, você pode especificar `false`.

   O `transformPDF` método retorna um `BLOB` objeto que contém um documento PDF não interativo.

1. Salve o documento PDF não interativo como um arquivo PDF.

   * Crie um `System.IO.FileStream` chamando seu construtor e passando um valor de string que representa o local do arquivo do documento PDF não interativo.
   * Crie uma matriz de bytes que armazene o conteúdo de dados do `BLOB` objeto retornado pelo `transformPDF` método . Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Resumo das etapas](creating-document-output-streams.md#summary-of-steps)

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Chamar o AEM Forms usando SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
