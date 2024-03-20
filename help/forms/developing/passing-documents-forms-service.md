---
title: Enviar documentos para o FormsService
description: Passe um objeto com.adobe.idp.Document que contém o design de formulário para o serviço Forms. O serviço Forms renderiza o design do formulário no objeto com.adobe.idp.Document.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 0%

---

# Passar documentos para o serviço da Forms {#passing-documents-to-the-formsservice}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

O serviço AEM Forms renderiza PDF forms interativos em dispositivos clientes, geralmente navegadores da Web, para coletar informações dos usuários. Um formulário PDF interativo é baseado em um design de formulário que normalmente é salvo como um arquivo XDP e criado no Designer. A partir do AEM Forms, você pode passar uma `com.adobe.idp.Document` objeto que contém o design do formulário para o serviço Forms. O serviço Forms renderiza o design do formulário na `com.adobe.idp.Document` objeto.

Uma vantagem de passar um `com.adobe.idp.Document` para o serviço Forms é que outras operações de serviço retornam um `com.adobe.idp.Document` instância. Ou seja, você pode obter um `com.adobe.idp.Document` instância de outra operação de serviço e renderizá-la. Por exemplo, suponha que um arquivo XDP esteja armazenado em um nó do Content Services (obsoleto) chamado `/Company Home/Form Designs`, conforme mostrado na ilustração a seguir.

Você pode recuperar programaticamente Loan.xdp do Content Services (desaprovado) (desaprovado) e passar o arquivo XDP para o serviço Forms em um `com.adobe.idp.Document` objeto.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para passar um documento obtido do Content Services (obsoleto) (obsoleto) para o serviço Forms, execute as seguintes tarefas:

1. Incluir arquivos de projeto.
1. Crie um Forms e um objeto de API do cliente de gerenciamento de documentos.
1. Recuperar o design do formulário do Content Services (desaprovado).
1. Renderize o formulário PDF interativo.
1. Execute uma ação com o fluxo de dados de formulário.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um Forms e um objeto de API do cliente de gerenciamento de documentos**

Antes de executar programaticamente uma operação da API de serviço do Forms, crie um objeto da API de cliente do Forms. Além disso, como esse fluxo de trabalho recupera um arquivo XDP do Content Services (obsoleto), crie um objeto de API do Document Management.

**Recuperar o design do formulário do Content Services (desaprovado)**

Recupere o arquivo XDP do Content Services (obsoleto) usando o Java ou a API do serviço da Web. O arquivo XDP é retornado em um `com.adobe.idp.Document` instância (ou um `BLOB` instância se você estiver usando serviços da web). Em seguida, você pode passar o `com.adobe.idp.Document` para o serviço Forms.

**Renderizar um formulário PDF interativo**

Para renderizar um formulário interativo, passe o `com.adobe.idp.Document` que foi retornada do Content Services (descontinuada) para o serviço Forms.

>[!NOTE]
>
>Você pode passar um `com.adobe.idp.Document` que contém o design do formulário para o serviço Forms. Dois novos métodos chamados `renderPDFForm2` e `renderHTMLForm2` aceitar um `com.adobe.idp.Document` objeto que contém um design de formulário.

**Executar uma ação com o fluxo de dados de formulário**

Dependendo do tipo de aplicativo cliente, você pode gravar o formulário em um navegador da Web cliente ou salvá-lo como um arquivo PDF. Um aplicativo baseado na Web normalmente grava o formulário em um navegador da Web. No entanto, um aplicativo de desktop normalmente salva o formulário como um arquivo PDF.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API de serviço do Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Enviar documentos para o serviço Forms usando a API Java {#pass-documents-to-the-forms-service-using-the-java-api}

Envie um documento obtido do Content Services (desaprovado) usando o serviço do Forms e a API do Content Services (desaprovado) (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar e adobe-contentservices-client.jar, no caminho de classe do projeto Java.

1. Criar um Forms e um objeto de API do cliente de gerenciamento de documentos

   * Criar um `ServiceClientFactory` objeto que contém propriedades de conexão. (Consulte [Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Criar um `FormsServiceClient` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.
   * Criar um `DocumentManagementServiceClientImpl` usando seu construtor e transmitindo o `ServiceClientFactory` objeto.

1. Recuperar o design do formulário do Content Services (desaprovado)

   Chame o `DocumentManagementServiceClientImpl` do objeto `retrieveContent` e passe os seguintes valores:

   * Um valor de string que especifica o armazenamento em que o conteúdo é adicionado. A loja padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.

   A variável `retrieveContent` o método retorna um `CRCResult` objeto que contém o arquivo XDP. Obter um `com.adobe.idp.Document` ao invocar a variável `CRCResult` do objeto `getDocument` método.

1. Renderizar um formulário PDF interativo

   Chame o `FormsServiceClient` do objeto `renderPDFForm2` e passe os seguintes valores:

   * A `com.adobe.idp.Document` objeto que contém o design de formulário recuperado dos Serviços de conteúdo (obsoleto).
   * A `com.adobe.idp.Document` objeto que contém dados a serem mesclados com o formulário. Se não quiser mesclar dados, passe uma tag vazia `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Esse valor é um parâmetro opcional, e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI. Esse valor é um parâmetro opcional, e você pode especificar `null`.
   * A `java.util.HashMap` objeto que armazena anexos de arquivo. Esse valor é um parâmetro opcional, e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   A variável `renderPDFForm` o método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da web do cliente.

1. Executar uma ação com o fluxo de dados de formulário

   * Criar um `com.adobe.idp.Document` ao invocar o `FormsResult` object&#39;s `getOutputContent` método.
   * Obter o tipo de conteúdo do `com.adobe.idp.Document` ao invocar seu `getContentType` método.
   * Defina o `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto chamando seu `setContentType` e transmitindo o tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Criar um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados de formulário no navegador da web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método.
   * Criar um `java.io.InputStream` ao invocar o `com.adobe.idp.Document` do objeto `getInputStream` método.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados de formulário chamando o `InputStream` do objeto `read` método. Transmita a matriz de bytes como argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados de formulário para o navegador web cliente. Passe a matriz de bytes para o `write` método.

**Consulte também**

[Início rápido (modo SOAP): passar documentos para o serviço Forms usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Definindo propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Enviar documentos para o serviço Forms usando a API do serviço Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Envie um documento obtido do Content Services (desaprovado) usando o serviço do Forms e a API (serviço da Web) do Content Services (desaprovado):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Como este aplicativo cliente invoca dois serviços AEM Forms, crie duas referências de serviço. Use a seguinte definição WSDL para a referência de serviço associada ao serviço Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Gerenciamento de Documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Como a variável `BLOB` tipo de dados for comum a ambas as referências de serviço, qualifique totalmente o `BLOB` tipo de dados ao usá-lo. No início rápido do serviço Web correspondente, todas as `BLOB` As instâncias do são totalmente qualificadas.

   >[!NOTE]
   >
   >Substituir `localhost`com o endereço IP do servidor que hospeda o AEM Forms.

1. Criar um Forms e um objeto de API do cliente de gerenciamento de documentos

   * Criar um `FormsServiceClient` usando seu construtor padrão.
   * Criar um `FormsServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Transmita um valor de string que especifique o WSDL para o serviço AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormsService?WSDL`). Não é necessário usar a variável `lc_version` atributo. Esse atributo é usado quando você cria uma referência de serviço.)
   * Criar um `System.ServiceModel.BasicHttpBinding` obtendo o valor do `FormsServiceClient.Endpoint.Binding` campo. Converter o valor de retorno em `BasicHttpBinding`.
   * Defina o `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que a MTOM seja usada.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor de senha correspondente ao campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita essas etapas para a variável `DocumentManagementServiceClient`cliente de serviço.

1. Recuperar o design do formulário do Content Services (desaprovado)

   Recupere o conteúdo chamando o `DocumentManagementServiceClient` do objeto `retrieveContent` e transmitindo os seguintes valores:

   * Um valor de string que especifica o armazenamento em que o conteúdo é adicionado. A loja padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.
   * Um parâmetro de saída da string que armazena o valor do link de pesquisa.
   * A `BLOB` parâmetro de saída que armazena o conteúdo. Você pode usar esse parâmetro de saída para recuperar o conteúdo.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` parâmetro de saída que armazena atributos de conteúdo.
   * A `CRCResult` parâmetro de saída. Em vez de usar esse objeto, você pode usar o `BLOB` para obter o conteúdo.

1. Renderizar um formulário PDF interativo

   Chame o `FormsServiceClient` do objeto `renderPDFForm2` e passe os seguintes valores:

   * A `BLOB` objeto que contém o design de formulário recuperado dos Serviços de conteúdo (obsoleto).
   * A `BLOB` objeto que contém dados a serem mesclados com o formulário. Se não quiser mesclar dados, passe uma tag vazia `BLOB` objeto.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Esse valor é um parâmetro opcional, e você pode especificar `null` se não quiser especificar opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI. Esse valor é um parâmetro opcional, e você pode especificar `null`.
   * A `Map` objeto que armazena anexos de arquivo. Esse valor é um parâmetro opcional, e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um parâmetro de saída longo que é usado para armazenar a contagem de páginas.
   * Um parâmetro de saída da string que é usado para armazenar o valor do local.
   * A `FormsResult` parâmetro de saída usado para armazenar o formulário PDF interativo `.`

   A variável `renderPDFForm2` o método retorna um `FormsResult` objeto que contém o formulário PDF interativo.

1. Executar uma ação com o fluxo de dados de formulário

   * Criar um `BLOB` objeto que contém dados de formulário obtendo o valor do `FormsResult` do objeto `outputContent` campo.
   * Criar um `System.IO.FileStream` invocando seu construtor. Transmita um valor de string que represente o local do arquivo do documento PDF interativo e o modo no qual o arquivo será aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto recuperado do `FormsResult` objeto. Preencha a matriz de bytes obtendo o valor de `BLOB` do objeto `MTOM` membro de dados.
   * Criar um `System.IO.BinaryWriter` objeto chamando seu construtor e transmitindo o `System.IO.FileStream` objeto.
   * Grave o conteúdo da matriz de bytes em um arquivo PDF, chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
