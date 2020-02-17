---
title: Criação de documentos PDF com dados XML enviados
seo-title: Criação de documentos PDF com dados XML enviados
description: 'null'
seo-description: 'null'
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Criação de documentos PDF com dados XML enviados {#creating-pdf-documents-with-submittedxml-data}

## Criação de documentos PDF com dados XML enviados {#creating-pdf-documents-with-submitted-xml-data}

Aplicativos baseados na Web que permitem que os usuários preencham formulários interativos exigem que os dados sejam enviados de volta ao servidor. Usando o serviço de Formulários, é possível recuperar os dados do formulário inseridos pelo usuário em um formulário interativo. Em seguida, é possível passar os dados do formulário para outra operação do serviço AEM Forms e criar um documento PDF usando os dados.

>[!NOTE]
>
>Antes de ler esse conteúdo, é recomendável que você tenha uma sólida compreensão sobre como lidar com formulários enviados. Conceitos como a relação entre um design de formulário e dados XML enviados são abordados em Manipulação de formulários enviados.

Considere o fluxo de trabalho a seguir que envolve três serviços do AEM Forms:

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
1. Criar objetos Forms, Output e Document Management.
1. Recupere dados de formulário usando o serviço Forms.
1. Crie um documento PDF não interativo usando o serviço de Saída.
1. Armazene o formulário PDF no Content Services (obsoleto) usando o serviço de Gerenciamento de documentos.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar objetos Forms, Output e Document Management**

Antes de executar programaticamente uma operação de API de serviço do Forms, crie um objeto de API do Forms Client. Da mesma forma, como esse fluxo de trabalho chama os serviços de Saída e Gerenciamento de documentos, crie um objeto de API do cliente de saída e um objeto de API do cliente de gerenciamento de documentos.

**Recuperar dados de formulário usando o serviço Forms**

Recuperar dados de formulário enviados ao serviço Forms. Você pode processar dados enviados para atender às suas necessidades comerciais. Por exemplo, você pode armazenar dados de formulário em um banco de dados corporativo. Entretanto, para criar um documento PDF não interativo, os dados do formulário são passados para o serviço de Saída.

**Crie um documento PDF não interativo usando o serviço de Saída.**

Use o serviço de Saída para criar um documento PDF não interativo baseado em um design de formulário e em dados de formulário XML. No fluxo de trabalho, os dados do formulário são recuperados do serviço Forms.

**Armazenar o formulário PDF no Content Services (obsoleto) usando o serviço de Gerenciamento de documentos**

Use a API do serviço de Gerenciamento de documentos para armazenar um documento PDF no Content Services (obsoleto).

**Consulte também:**

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do serviço de formulários](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Criar um documento PDF com dados XML enviados usando a API Java {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Crie um documento PDF com dados XML enviados usando o Forms, Output e Document Management API (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, adobe-output-client.jar e adobe-contentservices-client.jar no caminho de classe do seu projeto Java.

1. Criar objetos Forms, Output e Document Management

   * Crie um `ServiceClientFactory` objeto que contenha propriedades de conexão.
   * Crie um `FormsServiceClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.
   * Crie um `OutputClient` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.
   * Crie um `DocumentManagementServiceClientImpl` objeto usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar dados de formulário usando o serviço Forms

   * Chame o método do `FormsServiceClient` objeto `processFormSubmission` e passe os seguintes valores:

      * O `com.adobe.idp.Document` objeto que contém os dados do formulário.
      * Um valor de string que especifica variáveis de ambiente, incluindo todos os cabeçalhos HTTP relevantes. Especifique o tipo de conteúdo a ser tratado especificando um ou mais valores para a variável de `CONTENT_TYPE` ambiente. Por exemplo, para manipular dados XML, especifique o seguinte valor de string para esse parâmetro: `CONTENT_TYPE=text/xml`.
      * Um valor de string que especifica o valor do `HTTP_USER_AGENT` cabeçalho, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Um `RenderOptionsSpec` objeto que armazena opções de tempo de execução.
      O `processFormSubmission` método retorna um `FormsResult` objeto que contém os resultados do envio do formulário.

   * Determine se o serviço Forms terminou de processar os dados do formulário chamando o método do `FormsResult` objeto `getAction` . Se esse método retornar o valor `0`, os dados estarão prontos para serem processados.
   * Recupere dados de formulário criando um `com.adobe.idp.Document` objeto chamando o `FormsResult` método do `getOutputContent` objeto. (Esse objeto contém dados de formulário que podem ser enviados para o serviço de Saída.)
   * Crie um `java.io.InputStream` objeto chamando o `java.io.DataInputStream` construtor e transmitindo o `com.adobe.idp.Document` objeto.
   * Crie um `org.w3c.dom.DocumentBuilderFactory` objeto chamando o `org.w3c.dom.DocumentBuilderFactory` método do `newInstance` objeto estático.
   * Crie um `org.w3c.dom.DocumentBuilder` objeto chamando o `org.w3c.dom.DocumentBuilderFactory` método do `newDocumentBuilder` objeto.
   * Crie um `org.w3c.dom.Document` objeto chamando o `org.w3c.dom.DocumentBuilder` método do `parse` objeto e transmitindo o `java.io.InputStream` .
   * Recupere o valor de cada nó no documento XML. Uma maneira de realizar essa tarefa é criar um método personalizado que aceite dois parâmetros: o `org.w3c.dom.Document` objeto e o nome do nó cujo valor você deseja recuperar. Este método retorna um valor de string representando o valor do nó. No exemplo de código que segue esse processo, esse método personalizado é chamado `getNodeText`. O corpo deste método é mostrado.


1. Crie um documento PDF não interativo usando o serviço de Saída.

   Crie um documento PDF chamando o método do `OutputClient` objeto `generatePDFOutput` e transmitindo os seguintes valores:

   * Um valor `TransformationFormat` enum. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de string que especifica o nome do design de formulário. Verifique se o design de formulário é compatível com os dados de formulário recuperados do serviço Forms.
   * Um valor de string que especifica a raiz do conteúdo na qual o design de formulário está localizado.
   * Um `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * Um `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * O `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém os dados a serem unidos ao design de formulário. Verifique se esse objeto foi retornado pelo `FormsResult` método do `getOutputContent` objeto.
   * O `generatePDFOutput` método retorna um `OutputResult` objeto que contém os resultados da operação.
   * Recupere o documento PDF não interativo chamando o `OutputResult` método do `getGeneratedDoc` objeto. Esse método retorna uma `com.adobe.idp.Document` instância que representa o documento PDF não interativo.

1. Armazenar o formulário PDF no Content Services (obsoleto) usando o serviço de Gerenciamento de documentos

   Adicione o conteúdo chamando o método do `DocumentManagementServiceClientImpl` objeto `storeContent` e transmitindo os seguintes valores:

   * Um valor de string que especifica o armazenamento no qual o conteúdo é adicionado. A loja padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do espaço em que o conteúdo é adicionado (por exemplo, `/Company Home/Test Directory`). Esse valor é um parâmetro obrigatório.
   * O nome do nó que representa o novo conteúdo (por exemplo, `MortgageForm.pdf`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o tipo de nó. Para adicionar novo conteúdo, como um arquivo PDF, especifique `{https://www.alfresco.org/model/content/1.0}content`. Esse valor é um parâmetro obrigatório.
   * Um `com.adobe.idp.Document` objeto que representa o conteúdo. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o valor de codificação (por exemplo, `UTF-8`). Esse valor é um parâmetro obrigatório.
   * Um valor de `UpdateVersionType` enumeração que especifica como lidar com as informações da versão (por exemplo, `UpdateVersionType.INCREMENT_MAJOR_VERSION` para incrementar a versão do conteúdo). ) Esse valor é um parâmetro obrigatório.
   * Uma `java.util.List` instância que especifica aspectos relacionados ao conteúdo. Esse valor é um parâmetro opcional e você pode especificar `null`.
   * Um `java.util.Map` objeto que armazena atributos de conteúdo.
   O `storeContent` método retorna um `CRCResult` objeto que descreve o conteúdo. Usando um `CRCResult` objeto, você pode, por exemplo, obter o valor identificador exclusivo do conteúdo. Para executar essa tarefa, chame o `CRCResult` método do `getNodeUuid` objeto.

**Consulte também:**

[Incluir arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
