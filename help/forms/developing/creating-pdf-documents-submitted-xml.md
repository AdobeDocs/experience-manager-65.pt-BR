---
title: Criação de Documentos PDF com dados XML enviados
seo-title: Criação de Documentos PDF com dados XML enviados
description: Use o serviço Forms para recuperar os dados de formulário inseridos pelo usuário em um formulário interativo. Transmita os dados do formulário para outra operação de serviço da AEM Forms e crie um documento PDF usando os dados.
seo-description: Use o serviço Forms para recuperar os dados de formulário inseridos pelo usuário em um formulário interativo. Transmita os dados do formulário para outra operação de serviço da AEM Forms e crie um documento PDF usando os dados.
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 0%

---


# Criação de Documentos PDF com dados XML enviados {#creating-pdf-documents-with-submittedxml-data}

## Criação de Documentos PDF com dados XML enviados {#creating-pdf-documents-with-submitted-xml-data}

Aplicativos baseados na Web que permitem que os usuários preencham formulários interativos exigem que os dados sejam enviados de volta ao servidor. Usando o serviço Forms, é possível recuperar os dados do formulário inseridos pelo usuário em um formulário interativo. Em seguida, é possível passar os dados do formulário para outra operação do serviço AEM Forms e criar um documento PDF usando os dados.

>[!NOTE]
>
>Antes de ler esse conteúdo, é recomendável que você tenha uma sólida compreensão sobre como lidar com formulários enviados. Conceitos como a relação entre um design de formulário e os dados XML enviados são abordados em Manuseio da Forms submetido.

Considere o seguinte fluxo de trabalho que envolve três serviços da AEM Forms:

* Um usuário envia dados XML para o serviço Forms a partir de um aplicativo baseado na Web.
* O serviço Forms é usado para processar os campos de formulário e de extração enviados. Os dados do formulário podem ser processados. Por exemplo, os dados podem ser submetidos a um banco de dados corporativo.
* Os dados do formulário são enviados ao serviço de Saída para criar um documento PDF não interativo.
* O documento PDF não interativo é armazenado no Content Services (obsoleto).

O diagrama a seguir fornece uma representação visual deste fluxo de trabalho.

![cd_cd_finsrv_arch_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

Depois que o usuário envia o formulário do navegador da Web cliente, o documento PDF não interativo é armazenado no Content Services (obsoleto). A ilustração a seguir mostra um documento PDF armazenado no Content Services (obsoleto).

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### Resumo das etapas {#summary-of-steps}

Para criar um documento PDF não interativo com dados XML enviados e armazená-lo no documento PDF no Content Services (obsoleto), execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie objetos Forms, Output e Documento Management.
1. Recupere dados de formulário usando o serviço Forms.
1. Crie um documento PDF não interativo usando o serviço de Saída.
1. Armazene o formulário PDF no Content Services (obsoleto) usando o serviço de Gerenciamento de Documentos.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar objetos Forms, Output e Gerenciamento de Documentos**

Antes de executar programaticamente uma operação de API de serviço da Forms, crie um objeto de API do Forms Client. Da mesma forma, como esse fluxo de trabalho chama os serviços de Gerenciamento de Documentos e Saída, crie um objeto de API do Cliente de Saída e um objeto de API do Cliente de Gerenciamento de Documentos.

**Recuperar dados de formulário usando o serviço Forms**

Recuperar dados de formulário enviados ao serviço Forms. Você pode processar dados enviados para atender às suas necessidades de negócios. Por exemplo, você pode armazenar dados de formulário em um banco de dados corporativo. Entretanto, para criar um documento PDF não interativo, os dados do formulário são passados para o serviço de Saída.

**Crie um documento PDF não interativo usando o serviço de Saída.**

Use o serviço de Saída para criar um documento PDF não interativo baseado em um design de formulário e em dados de formulário XML. No fluxo de trabalho, os dados do formulário são recuperados do serviço Forms.

**Armazenar o formulário PDF no Content Services (obsoleto) usando o serviço de Gerenciamento de Documentos**

Use a API de serviço de Gerenciamento de Documentos para armazenar um documento PDF no Content Services (obsoleto).

**Consulte também:**

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API de serviço da Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Crie um Documento PDF com dados XML enviados usando a API Java {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Crie um documento PDF com dados XML enviados usando a Forms, Output e a API de gerenciamento de Documentos (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, adobe-output-client.jar e adobe-contentservices-client.jar no caminho de classe do seu projeto Java.

1. Criar objetos Forms, Output e Gerenciamento de Documentos

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.
   * Crie um objeto `OutputClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.
   * Crie um objeto `DocumentManagementServiceClientImpl` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Recuperar dados de formulário usando o serviço Forms

   * Chame o método `FormsServiceClient` do objeto `processFormSubmission` e passe os seguintes valores:

      * O objeto `com.adobe.idp.Document` que contém os dados do formulário.
      * Um valor de string que especifica variáveis de ambiente, incluindo todos os cabeçalhos HTTP relevantes. Especifique o tipo de conteúdo a ser tratado especificando um ou mais valores para a variável de ambiente `CONTENT_TYPE`. Por exemplo, para manipular dados XML, especifique o seguinte valor de string para esse parâmetro: `CONTENT_TYPE=text/xml`.
      * Um valor de string que especifica o valor do cabeçalho `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Um objeto `RenderOptionsSpec` que armazena opções de tempo de execução.

      O método `processFormSubmission` retorna um objeto `FormsResult` contendo os resultados do envio do formulário.

   * Determine se o serviço Forms terminou de processar os dados do formulário chamando o método `FormsResult` `getAction` do objeto. Se esse método retornar o valor `0`, os dados estarão prontos para serem processados.
   * Recupere dados de formulário criando um objeto `com.adobe.idp.Document` chamando o método `FormsResult` do objeto `getOutputContent`. (Esse objeto contém dados de formulário que podem ser enviados para o serviço de Saída.)
   * Crie um objeto `java.io.InputStream` chamando o construtor `java.io.DataInputStream` e transmitindo o objeto `com.adobe.idp.Document`.
   * Crie um objeto `org.w3c.dom.DocumentBuilderFactory` chamando o método `org.w3c.dom.DocumentBuilderFactory` estático do objeto `newInstance`.
   * Crie um objeto `org.w3c.dom.DocumentBuilder` chamando o método `org.w3c.dom.DocumentBuilderFactory` do objeto `newDocumentBuilder`.
   * Crie um objeto `org.w3c.dom.Document` invocando o método `org.w3c.dom.DocumentBuilder` do objeto `parse` e transmitindo o objeto `java.io.InputStream`.
   * Recupere o valor de cada nó dentro do documento XML. Uma maneira de realizar essa tarefa é criar um método personalizado que aceite dois parâmetros: o objeto `org.w3c.dom.Document` e o nome do nó cujo valor você deseja recuperar. Este método retorna um valor de string representando o valor do nó. No exemplo de código que segue esse processo, esse método personalizado é chamado `getNodeText`. O corpo deste método é mostrado.


1. Crie um documento PDF não interativo usando o serviço de Saída.

   Crie um documento PDF chamando o método `OutputClient` do objeto `generatePDFOutput` e transmitindo os seguintes valores:

   * Um valor de enumeração `TransformationFormat`. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica o nome do design de formulário. Verifique se o design de formulário é compatível com os dados de formulário recuperados do serviço Forms.
   * Um valor de string que especifica a raiz do conteúdo na qual o design de formulário está localizado.
   * Um objeto `PDFOutputOptionsSpec` que contém opções de tempo de execução de PDF.
   * Um objeto `RenderOptionsSpec` que contém opções de tempo de execução de renderização.
   * O objeto `com.adobe.idp.Document` que contém a fonte de dados XML que contém os dados a serem unidos ao design de formulário. Verifique se esse objeto foi retornado pelo método `FormsResult` do objeto `getOutputContent`.
   * O método `generatePDFOutput` retorna um objeto `OutputResult` que contém os resultados da operação.
   * Recupere o documento PDF não interativo chamando o método `OutputResult` do objeto `getGeneratedDoc`. Este método retorna uma instância `com.adobe.idp.Document` que representa o documento PDF não interativo.

1. Armazenar o formulário PDF no Content Services (obsoleto) usando o serviço de Gerenciamento de Documentos

   Adicione o conteúdo chamando o método `DocumentManagementServiceClientImpl` do objeto `storeContent` e transmitindo os seguintes valores:

   * Um valor de string que especifica o armazenamento no qual o conteúdo é adicionado. A loja padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do espaço em que o conteúdo é adicionado (por exemplo, `/Company Home/Test Directory`). Esse valor é um parâmetro obrigatório.
   * O nome do nó que representa o novo conteúdo (por exemplo, `MortgageForm.pdf`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o tipo de nó. Para adicionar novo conteúdo, como um arquivo PDF, especifique `{https://www.alfresco.org/model/content/1.0}content`. Esse valor é um parâmetro obrigatório.
   * Um objeto `com.adobe.idp.Document` que representa o conteúdo. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o valor de codificação (por exemplo, `UTF-8`). Esse valor é um parâmetro obrigatório.
   * Um valor de lista discriminada `UpdateVersionType` que especifica como lidar com as informações da versão (por exemplo, `UpdateVersionType.INCREMENT_MAJOR_VERSION` para incrementar a versão do conteúdo. ) Esse valor é um parâmetro obrigatório.
   * Uma instância `java.util.List` que especifica aspectos relacionados ao conteúdo. Esse valor é um parâmetro opcional e você pode especificar `null`.
   * Um objeto `java.util.Map` que armazena atributos de conteúdo.

   O método `storeContent` retorna um objeto `CRCResult` que descreve o conteúdo. Usando um objeto `CRCResult`, você pode, por exemplo, obter o valor identificador exclusivo do conteúdo. Para executar essa tarefa, chame o método `CRCResult` do objeto `getNodeUuid`.

**Consulte também:**

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
