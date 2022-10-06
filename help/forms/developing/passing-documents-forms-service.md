---
title: Passar documentos para o FormsService
seo-title: Passing Documents to the FormsService
description: Passe um objeto com.adobe.idp.Document que contém o design de formulário para o serviço Forms. O serviço Forms renderiza o design de formulário localizado no objeto com.adobe.idp.Document.
seo-description: Pass a com.adobe.idp.Document object that contains the form design to the Forms service. The Forms service renders the form design located in the com.adobe.idp.Document object.
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 0%

---

# Enviar documentos para o serviço do Forms {#passing-documents-to-the-formsservice}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

O serviço AEM Forms renderiza PDF forms interativas para dispositivos clientes, normalmente navegadores da Web, para coletar informações dos usuários. Um formulário PDF interativo é baseado em um design de formulário que normalmente é salvo como um arquivo XDP e criado no Designer. A partir do AEM Forms, você pode enviar uma `com.adobe.idp.Document` objeto que contém o design de formulário para o serviço Forms. O serviço Forms renderiza o design de formulário localizado na `com.adobe.idp.Document` objeto.

Uma vantagem de passar uma `com.adobe.idp.Document` O objeto para o serviço Forms é que outras operações de serviço retornam um `com.adobe.idp.Document` instância. Ou seja, você pode obter um `com.adobe.idp.Document` de outra operação de serviço e renderizá-la. Por exemplo, suponha que um arquivo XDP seja armazenado em um nó Content Services (obsoleto) chamado `/Company Home/Form Designs`, conforme mostrado na ilustração a seguir.

Você pode recuperar programaticamente o Loan.xdp dos Serviços de conteúdo (obsoleto) e passar o arquivo XDP para o serviço da Forms em um `com.adobe.idp.Document` objeto.

>[!NOTE]
>
>Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para passar um documento obtido dos Serviços de conteúdo (obsoleto) (obsoleto) para o serviço da Forms, execute as seguintes tarefas:

1. Inclua arquivos de projeto.
1. Crie um Forms e um objeto de API do cliente de gerenciamento de documentos.
1. Recupere o design de formulário do Content Services (obsoleto).
1. Renderize o formulário PDF interativo.
1. Execute uma ação com o fluxo de dados do formulário.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um Forms e um objeto de API do cliente de gerenciamento de documentos**

Antes de executar programaticamente uma operação de API de serviço do Forms, crie um objeto de API do cliente Forms. Além disso, como esse workflow recupera um arquivo XDP do Content Services (obsoleto), crie um objeto de API do Document Management.

**Recuperar o design do formulário do Content Services (obsoleto)**

Recupere o arquivo XDP do Content Services (obsoleto) usando a API do serviço da Web ou do Java. O arquivo XDP é retornado em um `com.adobe.idp.Document` instância (ou uma `BLOB` (se você estiver usando serviços da Web). Você pode passar o `com.adobe.idp.Document` para o serviço Forms.

**Renderizar um formulário PDF interativo**

Para renderizar um formulário interativo, passe o `com.adobe.idp.Document` instância que foi retornada do Content Services (obsoleto) para o serviço da Forms.

>[!NOTE]
>
>Você pode passar uma `com.adobe.idp.Document` que contém o design de formulário para o serviço Forms. Dois novos métodos nomeados `renderPDFForm2` e `renderHTMLForm2` aceite um `com.adobe.idp.Document` objeto que contém um design de formulário.

**Executar uma ação com o fluxo de dados do formulário**

Dependendo do tipo de aplicativo cliente, é possível gravar o formulário em um navegador da Web cliente ou salvar o formulário como um arquivo PDF. Um aplicativo baseado na Web normalmente grava o formulário no navegador da Web. No entanto, um aplicativo de desktop geralmente salva o formulário como um arquivo PDF.

**Consulte também**

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Passe documentos para o serviço da Forms usando a API do Java {#pass-documents-to-the-forms-service-using-the-java-api}

Passe um documento obtido dos Serviços de conteúdo (obsoleto) usando o serviço da Forms e a API (obsoleta) dos Serviços de conteúdo (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar e adobe-contentservices-client.jar, no caminho de classe do seu projeto Java.

1. Criar um Forms e um objeto de API do cliente de gerenciamento de documentos

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão. (Consulte [Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Crie um `FormsServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.
   * Crie um `DocumentManagementServiceClientImpl` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Recuperar o design do formulário do Content Services (obsoleto)

   Chame o `DocumentManagementServiceClientImpl` do objeto `retrieveContent` e transmita os seguintes valores:

   * Um valor de string que especifica o armazenamento onde o conteúdo é adicionado. O armazenamento padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.

   O `retrieveContent` método retorna um `CRCResult` objeto que contém o arquivo XDP. Obter um `com.adobe.idp.Document` chamando a `CRCResult` do objeto `getDocument` método .

1. Renderizar um formulário PDF interativo

   Chame o `FormsServiceClient` do objeto `renderPDFForm2` e transmita os seguintes valores:

   * A `com.adobe.idp.Document` objeto que contém o design de formulário recuperado dos Serviços de conteúdo (obsoleto).
   * A `com.adobe.idp.Document` objeto que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um vazio `com.adobe.idp.Document` objeto.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Esse valor é um parâmetro opcional e você pode especificar `null` se você não quiser especificar opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI. Esse valor é um parâmetro opcional e você pode especificar `null`.
   * A `java.util.HashMap` que armazena anexos de arquivo. Esse valor é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O `renderPDFForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Executar uma ação com o fluxo de dados do formulário

   * Crie um `com.adobe.idp.Document` chamando o `FormsResult` objeto &quot;s `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `com.adobe.idp.Document` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie um `java.io.InputStream` chamando o `com.adobe.idp.Document` do objeto `getInputStream` método .
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o `InputStream` do objeto `read` método . Transmita a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Início rápido (modo SOAP): Passar documentos para o serviço da Forms usando a API do Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Passe documentos para o serviço da Forms usando a API do serviço da Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Passe um documento obtido dos Serviços de conteúdo (obsoleto) usando o serviço da Forms e a API dos Serviços de conteúdo (obsoleto) (serviço da Web):

1. Incluir arquivos de projeto

   Crie um projeto Microsoft .NET que use MTOM. Como esse aplicativo cliente chama dois serviços AEM Forms, crie duas referências de serviço. Use a seguinte definição de WSDL para a referência de serviço associada ao serviço do Forms: `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Use a seguinte definição WSDL para a referência de serviço associada ao serviço de Gerenciamento de documentos: `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Porque a variável `BLOB` o tipo de dados é comum a ambas as referências de serviço, qualifica totalmente a variável `BLOB` tipo de dados ao usá-lo. Na inicialização rápida do serviço da Web correspondente, todas as `BLOB` as instâncias são totalmente qualificadas.

   >[!NOTE]
   >
   >Substituir `localhost`com o endereço IP do servidor que hospeda a AEM Forms.

1. Criar um Forms e um objeto de API do cliente de gerenciamento de documentos

   * Crie um `FormsServiceClient` usando seu construtor padrão.
   * Crie um `FormsServiceClient.Endpoint.Address` usando o `System.ServiceModel.EndpointAddress` construtor. Passe um valor de string que especifica o WSDL para o serviço do AEM Forms (por exemplo, `http://localhost:8080/soap/services/FormsService?WSDL`). Não é necessário usar a variável `lc_version` atributo. Este atributo é usado ao criar uma referência de serviço.)
   * Crie um `System.ServiceModel.BasicHttpBinding` obtendo o valor da variável `FormsServiceClient.Endpoint.Binding` campo. Converta o valor de retorno para `BasicHttpBinding`.
   * Defina as `System.ServiceModel.BasicHttpBinding` do objeto `MessageEncoding` campo para `WSMessageEncoding.Mtom`. Esse valor garante que o MTOM seja usado.
   * Ative a autenticação HTTP básica executando as seguintes tarefas:

      * Atribuir o nome de usuário dos formulários AEM ao campo `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Atribua o valor correspondente da senha ao campo `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Atribuir o valor constante `HttpClientCredentialType.Basic` ao campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Atribuir o valor constante `BasicHttpSecurityMode.TransportCredentialOnly` ao campo `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Repita essas etapas para a `DocumentManagementServiceClient`cliente de serviço.

1. Recuperar o design do formulário do Content Services (obsoleto)

   Recupere o conteúdo chamando o `DocumentManagementServiceClient` do objeto `retrieveContent` e transmitindo os seguintes valores:

   * Um valor de string que especifica o armazenamento onde o conteúdo é adicionado. O armazenamento padrão é `SpacesStore`. Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica o caminho totalmente qualificado do conteúdo a ser recuperado (por exemplo, `/Company Home/Form Designs/Loan.xdp`). Esse valor é um parâmetro obrigatório.
   * Um valor de string que especifica a versão. Esse valor é um parâmetro opcional e você pode passar uma string vazia. Nessa situação, a versão mais recente é recuperada.
   * Um parâmetro de saída de string que armazena o valor do link de navegação.
   * A `BLOB` parâmetro de saída que armazena o conteúdo. Você pode usar esse parâmetro de saída para recuperar o conteúdo.
   * A `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` parâmetro de saída que armazena atributos de conteúdo.
   * A `CRCResult` parâmetro de saída. Em vez de usar esse objeto, você pode usar a variável `BLOB` parâmetro de saída para obter o conteúdo.

1. Renderizar um formulário PDF interativo

   Chame o `FormsServiceClient` do objeto `renderPDFForm2` e transmita os seguintes valores:

   * A `BLOB` objeto que contém o design de formulário recuperado dos Serviços de conteúdo (obsoleto).
   * A `BLOB` objeto que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um vazio `BLOB` objeto.
   * A `PDFFormRenderSpec` objeto que armazena opções de tempo de execução. Esse valor é um parâmetro opcional e você pode especificar `null` se você não quiser especificar opções de tempo de execução.
   * A `URLSpec` objeto que contém valores de URI. Esse valor é um parâmetro opcional e você pode especificar `null`.
   * A `Map` que armazena anexos de arquivo. Esse valor é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.
   * Um parâmetro de saída longo usado para armazenar a contagem de páginas.
   * Um parâmetro de saída da string usado para armazenar o valor da localidade.
   * A `FormsResult` parâmetro de saída usado para armazenar o formulário PDF interativo `.`

   O `renderPDFForm2` método retorna um `FormsResult` objeto que contém o formulário PDF interativo.

1. Executar uma ação com o fluxo de dados do formulário

   * Crie um `BLOB` objeto que contém dados de formulário obtendo o valor da variável `FormsResult` do objeto `outputContent` campo.
   * Crie um `System.IO.FileStream` chamando seu construtor. Passe um valor de string que representa o local do arquivo do documento interativo do PDF e o modo no qual o arquivo deve ser aberto.
   * Crie uma matriz de bytes que armazene o conteúdo da variável `BLOB` objeto recuperado do `FormsResult` objeto. Preencha a matriz de bytes obtendo o valor da variável `BLOB` do objeto `MTOM` membro de dados.
   * Crie um `System.IO.BinaryWriter` chamando seu construtor e passando o `System.IO.FileStream` objeto.
   * Escreva o conteúdo da matriz de bytes em um arquivo PDF chamando o `System.IO.BinaryWriter` do objeto `Write` e transmitindo a matriz de bytes.

**Consulte também**

[Chamar o AEM Forms usando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
