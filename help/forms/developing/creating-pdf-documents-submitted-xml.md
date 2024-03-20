---
title: Criação de documentos PDF com dados XML enviados
description: Use o serviço Forms para recuperar os dados de formulário inseridos pelo usuário em um formulário interativo. Transmita os dados do formulário para outra operação de serviço do AEM Forms e crie um documento PDF usando os dados.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d9d5b94a-9d10-4d90-9e10-5142f30ba4a3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 0%

---

# Criação de documentos PDF com dados XML enviados {#creating-pdf-documents-with-submittedxml-data}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

## Criação de documentos PDF com dados XML enviados {#creating-pdf-documents-with-submitted-xml-data}

Aplicativos baseados na Web que permitem que os usuários preencham formulários interativos exigem que os dados sejam enviados de volta ao servidor. Usando o serviço Forms, você pode recuperar os dados do formulário inseridos pelo usuário em um formulário interativo. Em seguida, é possível passar os dados do formulário para outra operação de serviço do AEM Forms e criar um documento PDF usando os dados.

>[!NOTE]
>
>Antes de ler este conteúdo, é recomendável ter uma sólida compreensão do manuseio de formulários enviados. Conceitos como a relação entre um design de formulário e os dados XML enviados são abordados em Manuseio de Forms enviado.

Considere o seguinte fluxo de trabalho que envolve três serviços da AEM Forms:

* Um usuário envia dados XML para o serviço Forms de um aplicativo baseado na Web.
* O serviço Forms é usado para processar o formulário enviado e extrair campos de formulário. Os dados do formulário podem ser processados. Por exemplo, os dados podem ser submetidos a um banco de dados empresarial.
* Os dados de formulário são enviados para o Serviço de saída para criar um documento PDF não interativo.
* O documento PDF não interativo é armazenado nos Serviços de conteúdo (obsoleto).

O diagrama a seguir fornece uma representação visual desse workflow.

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

Depois que o usuário envia o formulário do navegador da Web do cliente, o documento PDF não interativo é armazenado nos Serviços de conteúdo (desaprovado). A ilustração a seguir mostra um documento PDF armazenado nos Serviços de conteúdo (desaprovado).

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### Resumo das etapas {#summary-of-steps}

Para criar um documento PDF não interativo com dados XML enviados e armazenar no documento PDF no Content Services (desaprovado), execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie objetos do Forms, Output e Document Management.
1. Recupere dados do formulário usando o serviço Forms.
1. Crie um documento PDF não interativo usando o Serviço de saída.
1. Armazene o formulário PDF nos Serviços de conteúdo (obsoleto) usando o serviço Gerenciamento de documentos.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar objetos do Forms, Output e Document Management**

Antes de executar programaticamente uma operação da API de serviço do Forms, crie um objeto da API de cliente do Forms. Da mesma forma, como esse fluxo de trabalho chama os serviços de Gerenciamento de Saída e de Documentos, crie um objeto da API de Cliente de Saída e um objeto da API de Cliente de Gerenciamento de Documentos.

**Recuperar dados do formulário usando o serviço Forms**

Recupere dados de formulário enviados para o serviço Forms. Você pode processar os dados enviados para atender aos requisitos da sua empresa. Por exemplo, você pode armazenar dados de formulário em um banco de dados empresarial. No entanto, para criar um documento PDF não interativo, os dados de formulário são passados para o serviço de Saída.

**Crie um documento PDF não interativo usando o Serviço de saída.**

Use o Serviço de saída para criar um documento PDF não interativo baseado em um design de formulário e dados de formulário XML. No workflow, os dados de formulário são recuperados do serviço Forms.

**Armazenar o formulário PDF nos Serviços de conteúdo (obsoleto) usando o serviço Gerenciamento de documentos**

Use a API do serviço de Gerenciamento de documentos para armazenar um documento PDF nos Serviços de conteúdo (desaprovado).

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Criar um documento PDF com dados XML enviados usando a API Java {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Crie um documento PDF com dados XML enviados usando a API de gerenciamento de documentos (Java), do Forms e de saída:

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, adobe-output-client.jar e adobe-contentservices-client.jar no caminho de classe do projeto Java.

1. Criar objetos do Forms, Output e Document Management

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Criar um `FormsServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.
   * Criar um `OutputClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.
   * Criar um `DocumentManagementServiceClientImpl` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar dados do formulário usando o serviço Forms

   * Chame o `FormsServiceClient` do objeto `processFormSubmission` e passe os seguintes valores:

      * A variável `com.adobe.idp.Document` objeto que contém os dados de formulário.
      * Um valor de string que especifica variáveis de ambiente, incluindo todos os cabeçalhos HTTP relevantes. Especifique o tipo de conteúdo a ser manipulado especificando um ou mais valores para o `CONTENT_TYPE` variável de ambiente. Por exemplo, para manipular dados XML, especifique o seguinte valor de string para esse parâmetro: `CONTENT_TYPE=text/xml`.
      * Um valor de string que especifica a `HTTP_USER_AGENT` valor do cabeçalho, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` objeto que armazena opções de tempo de execução.

     A variável `processFormSubmission` o método retorna um `FormsResult` objeto que contém os resultados do envio do formulário.

   * Determine se o serviço Forms terminou de processar os dados do formulário invocando o `FormsResult` do objeto `getAction` método. Se esse método retornar o valor `0`, os dados estão prontos para serem processados.
   * Recuperar dados do formulário criando uma `com.adobe.idp.Document` ao invocar o `FormsResult` do objeto `getOutputContent` método. (Este objeto contém dados de formulário que podem ser enviados para o Serviço de saída.)
   * Criar um `java.io.InputStream` ao invocar o `java.io.DataInputStream` construtor e transmitindo o `com.adobe.idp.Document` objeto.
   * Criar um `org.w3c.dom.DocumentBuilderFactory` chamando o objeto estático `org.w3c.dom.DocumentBuilderFactory` do objeto `newInstance` método.
   * Criar um `org.w3c.dom.DocumentBuilder` ao invocar o `org.w3c.dom.DocumentBuilderFactory` do objeto `newDocumentBuilder` método.
   * Criar um `org.w3c.dom.Document` ao invocar o `org.w3c.dom.DocumentBuilder` do objeto `parse` e transmitindo o `java.io.InputStream` objeto.
   * Recupere o valor de cada nó no documento XML. Uma maneira de realizar essa tarefa é criar um método personalizado que aceite dois parâmetros: o `org.w3c.dom.Document` e o nome do nó cujo valor você deseja recuperar. Esse método retorna um valor de string que representa o valor do nó. No exemplo de código que segue esse processo, esse método personalizado é chamado de `getNodeText`. O corpo desse método é mostrado.

1. Crie um documento PDF não interativo usando o Serviço de saída.

   Crie um documento PDF chamando o `OutputClient` do objeto `generatePDFOutput` e transmitindo os seguintes valores:

   * A `TransformationFormat` valor de enumeração. Para gerar um documento PDF, especifique `TransformationFormat.PDF`.
   * Um valor de cadeia de caracteres que especifica o nome do design do formulário. Verifique se o design do formulário é compatível com os dados de formulário recuperados do serviço Forms.
   * Um valor de cadeia de caracteres que especifica a raiz do conteúdo onde o design do formulário está localizado.
   * A `PDFOutputOptionsSpec` objeto que contém opções de tempo de execução de PDF.
   * A `RenderOptionsSpec` objeto que contém opções de tempo de execução de renderização.
   * A variável `com.adobe.idp.Document` objeto que contém a fonte de dados XML que contém os dados a serem mesclados com o design do formulário. Verifique se esse objeto foi retornado pela variável `FormsResult` do objeto `getOutputContent` método.
   * A variável `generatePDFOutput` o método retorna um `OutputResult` objeto que contém os resultados da operação.
   * Recupere o documento PDF não interativo chamando o `OutputResult` do objeto `getGeneratedDoc` método. Este método retorna um valor de `com.adobe.idp.Document` que representa o documento PDF não interativo.

1. Armazenar o formulário PDF nos Serviços de conteúdo (obsoleto) usando o serviço Gerenciamento de documentos

   Adicione o conteúdo chamando o `DocumentManagementServiceClientImpl` do objeto `storeContent` e transmitindo os seguintes valores:

   * Um valor de string que especifica o armazenamento em que o conteúdo é adicionado. A loja padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do espaço em que o conteúdo é adicionado (por exemplo, `/Company Home/Test Directory`). Esse valor é um parâmetro obrigatório.
   * O nome do nó que representa o novo conteúdo (por exemplo, `MortgageForm.pdf`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o tipo de nó. Para adicionar novo conteúdo, como um arquivo PDF, especifique `{https://www.alfresco.org/model/content/1.0}content`. Esse valor é um parâmetro obrigatório.
   * A `com.adobe.idp.Document` objeto que representa o conteúdo. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o valor de codificação (por exemplo, `UTF-8`). Esse valor é um parâmetro obrigatório.
   * Um `UpdateVersionType` valor de enumeração que especifica como tratar informações de versão (por exemplo, `UpdateVersionType.INCREMENT_MAJOR_VERSION` para incrementar a versão do conteúdo. ) Esse valor é um parâmetro obrigatório.
   * A `java.util.List` instância que especifica aspectos relacionados ao conteúdo. Esse valor é um parâmetro opcional e você pode especificar `null`.
   * A `java.util.Map` objeto que armazena atributos de conteúdo.

   A variável `storeContent` o método retorna um `CRCResult` objeto que descreve o conteúdo. Uso de um `CRCResult` objeto, você pode, por exemplo, obter o valor do identificador exclusivo do conteúdo. Para executar essa tarefa, chame o `CRCResult` do objeto `getNodeUuid` método.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
